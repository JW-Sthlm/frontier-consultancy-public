# Before the workshop - environment setup

Twenty minutes the day before, on your own laptop. Five short checks. If they all pass, you walk into the workshop and start working. If any fail, you switch to the Codespaces fallback (no IT escalation needed).

This page is **only about getting your environment ready.** The actual exercise lives in [`IN-WORKSHOP.md`](IN-WORKSHOP.md). Do not read that one yet.

> **A note on IT access.** If your work laptop blocks one of these checks (Node, global npm, the Copilot CLI itself), that is useful signal worth raising with IT. You do not need to sort it out before the workshop. Use the Codespaces path on the day, get the full experience, then have the access conversation with IT on your own time.

---

## The five checks

Open a terminal. PowerShell on Windows, Terminal on Mac.

### 1. You have a GitHub account with Copilot

Open [`github.com/settings/copilot`](https://github.com/settings/copilot) in a browser. You should see *Copilot Pro*, *Copilot Business*, or *Copilot Enterprise* listed as **Active**. Any of the three works.

No Copilot? -> [`help-no-account.md`](help-no-account.md) gets you a free 30-day Pro trial in two minutes.

### 2. Node.js is installed

```
node --version
```

You want `v20.x.x` or newer. No version? Install from [nodejs.org](https://nodejs.org/) (LTS button), then close and reopen the terminal.

### 3. You can install global npm packages

```
npm install -g @github/copilot
```

If it finishes without errors, brilliant. If it fails with `EACCES` or *permission denied* on Mac/Linux, see the [FAQ](FAQ.md). If it is silently blocked on a corporate Windows laptop (MDM policy, *"you do not have permission"*), that is your signal to use Codespaces on the day.

### 4. Copilot CLI runs

```
copilot --version
```

You want `GitHub Copilot CLI 1.0.x` or newer. If the command is not found, your terminal has not picked up the new install. Close it, reopen it, try again.

### 5. You can reach learn.microsoft.com

```
curl -sI https://learn.microsoft.com/training/support/mcp
```

The first line should be `HTTP/2 200` or `HTTP/1.1 200`. If you get a connection error, a timeout, or a corporate proxy redirect page, the Microsoft Learn MCP will not work from your laptop. Codespaces fixes this too.

---

## What if a check fails

One fallback solves all five at once: **[Open the exercise in a Codespace](https://codespaces.new/JW-Sthlm/frontier-consultancy-public?quickstart=1)**. Browser tab, ~90 seconds to a working terminal with the workshop file open. Free on a personal GitHub account, 60 hours per month. See [`help-codespaces.md`](help-codespaces.md) if you want the detail.

---

## Bonus pre-work: arrive with data, not curiosity

Two free instruments. Local-only. Install one or both this week and you walk into the workshop with **your own numbers** to compare against the exercise output. Not required. Strongly recommended.

### AgentRC - score one of your repos in five minutes

[**microsoft/agentrc**](https://github.com/microsoft/agentrc) scores any Git repo across nine pillars (style, build, testing, docs, dev environment, code quality, observability, security, AI tooling) and tells you where you sit on the maturity ladder: Functional -> Documented -> Standardized -> Optimized -> Autonomous.

Pick a repo you actually own. From your terminal:

```
cd <path-to-your-repo>
npx -y github:microsoft/agentrc readiness
```

Five minutes. Output is a scorecard. Save it. Bring the maturity level number to the workshop.

**What you need:** Node 20+ (same as check 2 above), `gh auth status` returning your username.

### AI Engineering Coach - your personal AI-usage dashboard

[**microsoft/AI-Engineering-Coach**](https://github.com/microsoft/AI-Engineering-Coach) is a VS Code extension that reads your existing Copilot Chat, Copilot CLI, Cursor, Claude Code, and Codex session logs **locally** and shows you the patterns you would never spot yourself. Anti-patterns, prompt repetition, token burn, which workspaces eat your time. Nothing leaves your machine.

> **Coach is not in the VS Code Marketplace.** Searching the marketplace for "Coach" returns unrelated extensions. You install it by cloning the repo and building the `.vsix` yourself. The fastest path is to let Copilot CLI do it for you. From any folder:
>
> ```
> Install https://github.com/microsoft/AI-Engineering-Coach as a VS Code extension on my machine. Read the repo README, run the build steps, install the resulting .vsix. Tell me when done.
> ```

Open VS Code, find the Coach icon in the sidebar. If you have been using AI in VS Code or Copilot CLI for a few weeks, the dashboard populates immediately.

**Why bother before the workshop:** the workshop trains the *pattern* of AI-first delivery. AgentRC and Coach tell you *where your team actually is* on that pattern today. Combine them with the workshop output and you have a one-slide story for your next leadership conversation.

---

## On the day, bring this

- The laptop you ran the checks on
- Your GitHub credentials
- The AgentRC scorecard, if you ran it (one number, one minute of share-back)

The **core** uses only the Microsoft Learn MCP. That endpoint is public, requires no token, and works in nearly every enterprise. The **stretch tiers** add a GitHub MCP (your own PAT) and an Azure MCP (your own `az login`). If either is locked down on your laptop, skip the stretch. The core alone is the workshop.

When you sit down in the room, open [`IN-WORKSHOP.md`](IN-WORKSHOP.md).
