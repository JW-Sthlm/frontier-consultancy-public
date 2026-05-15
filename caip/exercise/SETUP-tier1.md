# Tier 1 — Copilot CLI

**What you will do:** install Copilot CLI, let Copilot set up the exercise for itself, then run the Nordwind brief — all without typing a single `git clone` or `cd` command.

This takes about **5 minutes** if you have Node.js already, **8 minutes** if you do not.

---

## Step 1 — Install Node.js (if you do not have it)

Open a terminal. On Windows that means **PowerShell** or **Windows Terminal** (search for either in the Start menu). On Mac, open **Terminal** (Spotlight → "Terminal").

Type:

```
node --version
```

**If you see something like `v20.x.x` or newer**, skip to Step 2.

**If you see "command not found"**, install Node:

- **Windows:** download from **[nodejs.org](https://nodejs.org/)** — click the big **LTS** button. Run the installer. Accept all defaults. **Close and reopen** your terminal.
- **Mac:** same, or if you use Homebrew: `brew install node`.

Check again:

```
node --version
```

You should see two version numbers.

---

## Step 2 — Install Copilot CLI

In your terminal:

```
npm install -g @github/copilot
```

About 30 seconds of scrolling text. When it stops, check:

```
copilot --version
```

You should see something like:

```
GitHub Copilot CLI 1.0.35-2.
```

> **[SCREENSHOT #3 — see `capture-guide.md`]** — successful install.

---

## Step 3 — Sign in

```
copilot
```

Copilot shows a device code and asks you to visit **github.com/login/device**. Open that in a browser, paste the code, approve. Come back to the terminal.

> **[SCREENSHOT #4 — see `capture-guide.md`]** — the device-code page.

You now see a Copilot prompt — something like `>`. You are in. Type `/exit` to leave.

---

## Step 4 — Start Copilot in yolo mode

This is where it gets fun. Run:

```
copilot --allow-all
```

**What `--allow-all` does ("yolo mode"):**

- Copilot can **run shell commands** without asking each time.
- Copilot can **read and write files** on your machine without asking each time.
- Copilot can **fetch any URL** without asking each time.

**Is this safe?** For this exercise, yes. You are in a sandbox, the repo is fresh, there is nothing to break. For real customer work, keep the default (Copilot asks before doing anything risky). You will feel the difference immediately — with yolo on, Copilot flies. Without it, you click "yes" a lot.

Think of `--allow-all` as "I trust you — go". You can turn it off any time by starting Copilot without the flag.

---

## Step 5 — Let Copilot do the setup

At the `>` prompt, paste this **entire block** as one prompt:

```
I'm starting an AI workshop exercise. Please do the following for me:

1. Download the CAIP Frontier Consultancy exercise from this repo:
   <exercise-repo-url>
   Put it somewhere sensible on my machine. You pick the folder. Tell me
   the full path when done.

2. Change into that folder so everything you do next happens there.

3. Set up the Microsoft Learn MCP server in my Copilot CLI config so you
   can ground your answers in current Microsoft documentation. The docs
   URL for the Learn MCP is:
   https://learn.microsoft.com/training/support/mcp
   Read that page, figure out the right config, add it to
   ~/.copilot/mcp-config.json (alongside anything already there).

4. When done, tell me to run the slash command /mcp in this same Copilot
   CLI session to verify the server is listed. If the new config needs to
   be reloaded, tell me to use /restart.
```

*(The facilitator will give you the exact exercise repo URL on the day. Paste it in where it says `<exercise-repo-url>`.)*

Copilot will:

- Pick a folder (usually `~/Documents` or `~/projects`), create it, download the exercise into it.
- Change its working directory into that folder.
- Fetch the Learn MCP docs page, figure out the correct config, edit `~/.copilot/mcp-config.json`.
- Tell you to type `/mcp` to see the server running, and `/restart` first if the reload is needed.

Type:

```
/mcp
```

You should see **microsoft-learn** (or similar) in the list, with a non-zero tool count. If it shows zero or is not listed, run `/restart` to reload config, then `/mcp` again.

> **This is the moment.** You just told an AI to set up your workshop environment — download code, configure another AI tool, verify it worked. You wrote no code. You touched no config. That is AI-first delivery.

---

## Step 6 — Run the Nordwind exercise

Same Copilot session. Next prompt:

```
Read client/meeting-notes.md and client/README.md so you have the full
scenario. Using the Microsoft Learn MCP, research the current Microsoft
guidance on the Azure Landing Zone for AI and the Microsoft Agent
Framework. Then fill in client/brief-template.md and save the result as
brief.md at the repo root.

Answer Ingrid's question directly: can Nordwind "just use ChatGPT" for
this, or do they need something more? Be specific to Nordwind — quote
their own words. Include the URLs of the Learn pages you used. Be
commercially honest. Do not hedge.
```

Watch Learn MCP calls stream past. Grounded research, happening live.

When Copilot finishes, open `brief.md` — either ask Copilot to show it (`show me brief.md`), or if you installed VS Code as a file viewer, open the folder there.

---

## Step 7 — Sharpen it

Two follow-up prompts in the same session. **The second one is the one you will use at work.**

```
Add a 5-question discovery checklist I should run with Ingrid on our
next call to validate these recommendations.
```

```
Now re-read brief.md critically and tell me the three weakest claims.
For each one, either suggest a specific edit that strengthens it, or
recommend we cut it.
```

AI-first delivery is not "generate and ship". It is "generate, critique, sharpen". The second prompt trains the critique muscle.

---

## You are done with the core

- Compare `brief.md` with your neighbour. What did Learn MCP add beyond baseline Copilot?
- Got time and a scratch GitHub repo? → **[Tier 2](SETUP-tier2.md)**.
- Got an Azure subscription? → **[Tier 3](SETUP-tier3.md)**.
- Something broken? **Ask Copilot first**, then check [`FAQ.md`](FAQ.md), then ask a neighbour.
