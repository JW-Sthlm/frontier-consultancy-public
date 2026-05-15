# Tier 2 — Ship the brief as a GitHub issue (stretch, ~5 min)

Only do this if your Tier 1 brief is done. Otherwise finish the core first.

**What you will do:** add the GitHub MCP to Copilot so it can open an issue in your own scratch repo, using `brief.md` as the body.

---

## Pre-req

You need a repo you can write to. If you do not have one, create one:

1. Go to **[github.com/new](https://github.com/new)**.
2. Name it `caip-exercise-scratch`. Keep it **private**. Click **Create**.

---

## Step 1 — Create a GitHub Personal Access Token (2 min)

1. Go to **[github.com/settings/tokens?type=beta](https://github.com/settings/tokens?type=beta)** (fine-grained tokens).
2. Click **Generate new token**.
3. Name: `caip-exercise`. Expiration: **7 days**.
4. Repository access: **Only select repositories** → pick your `caip-exercise-scratch` repo.
5. Permissions → Repository → **Issues: Read and write**, **Contents: Read**.
6. Click **Generate token**. **Copy the token now** — you cannot see it again.

---

## Step 2 — Add the GitHub MCP

Inside Copilot CLI, at the `>` prompt:

```
I want to add the GitHub MCP server to my config so you can open issues in
my repos. Here is the docs URL:
https://github.com/github/github-mcp-server

Set it up to use this PAT as an environment variable: <paste-your-token>.
Add it to ~/.copilot/mcp-config.json next to the microsoft-learn entry.
Tell me how to verify.
```

Approve the config edit (if you are not in yolo mode). Run `/mcp` to confirm you now see **github** in the list.

---

Ship the brief. Prompt Copilot (still in the same CLI session):

```
Using the GitHub MCP, open a new issue in my repo <your-username>/caip-exercise-scratch.
Title: "Workshop brief: Nordwind Aerospace".
Body: the full contents of brief.md.
Labels: "workshop-output".
After creating it, give me the issue URL.
```

Copilot opens the issue. Visit the URL in your browser. Confirm the brief is there, formatted cleanly.

---

## Why this matters

This is Copilot touching a production system. Not reading, **writing**. Same idea as an agent opening a ticket in ADO, or a delivery dashboard agent posting a status update into a customer portal. The pattern generalises. The PAT is the only thing keeping you safe. **Revoke it when you are done:** `github.com/settings/tokens` → find the token → **Delete**.
