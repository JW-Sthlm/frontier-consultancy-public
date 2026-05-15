# Before the workshop

This is the prep page. Twenty minutes the day before, on your own laptop. Five short checks. If they all pass, you walk into the workshop and start working. If any of them fail, you have a backup path that needs nothing from your IT team.

## Why we prep ahead

The workshop is hands-on. Every minute we spend on installer dialogues is a minute we are not spending on the exercise. The five checks below are the actual prereqs. Run them. If they pass, brilliant. If they do not, scroll to *"What if a check fails"*. There is a fallback that works from any browser.

> **A note on IT access.** If your work laptop blocks one of these checks (Node, global npm, the Copilot CLI itself), that is useful signal. It is worth raising with your IT team at some point. You do not need to sort it out before this workshop. Use the Codespaces path for the day, get the full experience, then have the access conversation with IT on your own time.

## The five checks

Open a terminal. PowerShell on Windows, Terminal on Mac.

### 1. You have a GitHub account with Copilot

Open [`github.com/settings/copilot`](https://github.com/settings/copilot) in a browser. You should see *Copilot Pro* or *Copilot Business* listed as **Active**.

No Copilot? → [`SETUP-tier0.md`](SETUP-tier0.md) gets you a free 30-day Pro trial in two minutes.

### 2. Node.js is installed

```
node --version
```

You want `v20.x.x` or newer. No version? Install from [nodejs.org](https://nodejs.org/) (LTS button), then close and reopen the terminal.

### 3. You can install global npm packages

```
npm install -g @github/copilot
```

If it finishes without errors, brilliant. If it fails with `EACCES` or *permission denied* on Mac/Linux, see the [FAQ](FAQ.md). If it is silently blocked on a corporate Windows laptop (MDM policy, "you do not have permission"), that is your signal that Codespaces is your path for the day.

### 4. Copilot CLI runs

```
copilot --version
```

You want `GitHub Copilot CLI 1.0.x` or higher. If the command is not found, your terminal has not picked up the new install. Close it, reopen it, try again.

### 5. You can reach learn.microsoft.com

```
curl -sI https://learn.microsoft.com/training/support/mcp
```

The first line of the response should be `HTTP/2 200` or `HTTP/1.1 200`. If you get a connection error, a timeout, or a corporate proxy redirect page, the Microsoft Learn MCP will not work from your laptop. Codespaces fixes this too.

## What if a check fails

You have one fallback that solves all five at once: **[`SETUP-codespaces.md`](SETUP-codespaces.md)**. Codespaces runs the entire exercise in a browser tab on GitHub's infrastructure. Free on a personal GitHub account, 60 hours a month. Use it for the day.

The original access gap (no Node, no global npm, no MCP traffic) is worth raising with your IT team afterwards. Having Copilot CLI work on your real laptop long term is genuinely useful. It just is not a blocker for what we are doing on the day.

## Pick your path

| You have… | Start here |
|---|---|
| All five checks pass | [`SETUP-tier1.md`](SETUP-tier1.md) |
| One or more checks fail | [`SETUP-codespaces.md`](SETUP-codespaces.md) |
| No GitHub or no Copilot seat | [`SETUP-tier0.md`](SETUP-tier0.md), then back to Tier 1 |

## On the day

Bring the laptop you ran the checks on. Bring your GitHub credentials.

One thing worth knowing about the exercise architecture: the **core** uses only the Microsoft Learn MCP. That endpoint is public, requires no token, and works in nearly every enterprise. The **stretch tiers** add a GitHub MCP (your own personal access token) and an Azure MCP (your own `az login`). If your access is locked down on either of those, skip them. The core alone is the workshop. The stretch tiers are extra colour.

See you in the room.
