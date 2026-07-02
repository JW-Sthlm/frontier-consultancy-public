# Before the workshop - environment setup

Twenty minutes the day before, on your own laptop. A short typed setup to get the CLI running, then everything else is plain English. The goal is a working setup you keep using after the workshop, so we try the simple install first and only fall back if we have to.

> **Aim for a local setup.** Run Part A on your own laptop, about 15 minutes. That leaves you with a working environment you keep after the workshop, which is the whole point. If the install will not go (a locked-down laptop, usually), a one-click [Codespace](https://codespaces.new/JW-Sthlm/frontier-consultancy-public?quickstart=1) is your safety net, and step 2 walks you to it. One catch worth knowing up front: the Codespace lives in a browser tab, so it leaves nothing on your machine afterward. That is why it is the last resort, not the first.

This page is **only about getting your environment ready.** The actual exercise lives in [`IN-WORKSHOP.md`](IN-WORKSHOP.md). Do not read that one yet.

> **A note on IT access.** If your work laptop blocks the install, that is useful signal worth raising with IT. You do not need to sort it out before the workshop. Use the Codespaces path on the day, get the full experience, then have the access conversation with IT on your own time.

---

## Part A - get the CLI running

> **What is the CLI?** It is Copilot, running in a terminal instead of a chat box. The same plain-English conversation you already use, it just looks more technical. You still type what you want in normal words. The difference is reach: in the terminal, Copilot can pull in far more tools and act on your machine. It does not stop at answering. That is what the workshop is about.

This is the only part that needs typed commands, and here is why. You are installing the tool that understands plain English, so you cannot ask it to install itself yet. Three steps, then you are done with syntax for the night.

Two of these run in a terminal. Here is how to open one.

- **Windows:** press Start, type `PowerShell`, press Enter.
- **Mac:** press Cmd+Space, type `Terminal`, press Enter.

A terminal is just a window where you type a line and read what comes back. Copy, paste, press Enter, look at the answer. That is the whole skill, and it is the last of it for tonight.

### 1. GitHub account with Copilot · browser

Open [`github.com/settings/copilot`](https://github.com/settings/copilot). You should see *Copilot Pro*, *Copilot Business*, or *Copilot Enterprise* marked **Active**. Any of the three works.

No Copilot? [`help-no-account.md`](help-no-account.md) gets you a free 30-day Pro trial in two minutes.

### 2. Install Copilot CLI · terminal

Copy the command for your computer, paste it into the terminal, press Enter. Wait a moment. When a fresh empty line comes back, it is done. You do not need to know what the command says.

**On Windows:**
```
winget install GitHub.Copilot
```

**On a Mac:**
```
brew install copilot-cli
```

No red errors? You are done. Skip to step 3.

**If it threw an error, climb one rung.** The line above is the easy installer. The other way in works on any machine, it just adds one step: you install Node first, then the CLI.

First, download Node from [nodejs.org](https://nodejs.org/), the big green **LTS** button. Run the installer, then close and reopen the terminal. Then paste this and press Enter:

```
npm install -g @github/copilot
```

That covers Windows, Mac, and Linux. (More installers are in [GitHub's docs](https://docs.github.com/en/copilot/how-tos/copilot-cli/set-up-copilot-cli/install-copilot-cli) if you want them.)

**Still stuck after that?** Now, and only now, reach for the Codespace. [Open the exercise in a Codespace.](https://codespaces.new/JW-Sthlm/frontier-consultancy-public?quickstart=1) It runs in the cloud with the CLI already installed, so you can do the whole workshop from a browser tab. The reason it is the last rung: it leaves nothing on your own laptop, so you would start over after the workshop. Locked down by IT? Take this rung today, then sort the local install with IT later.

### 3. Launch it · terminal

```
copilot
```

First run asks you to type `/login`. Follow the prompt, authorize in the browser, come back. When you land on the Copilot prompt, you are in. From here you type sentences, not commands.

---

## Part B - now just talk to it

Everything below you type **into** a running `copilot`, in your own words. No flags, no syntax. This is the actual skill the workshop builds, so treat it as the warm-up.

### 4. Check your laptop can reach Microsoft Learn · in the CLI

At the Copilot prompt, paste this sentence:

```
Fetch https://learn.microsoft.com/training/support/mcp and tell me the HTTP status code.
```

Copilot asks permission to make the request. Allow it. A **200** means you are good. A timeout, a connection error, or a corporate proxy page means your laptop's network blocks that endpoint, which the workshop's Microsoft Learn step needs. The Codespace fixes this.

That is the whole setup. One install line, one launch, one sentence. Everything else happens in the room.

---

## Bonus pre-work: arrive with data, not curiosity

Two free instruments. Local-only. Try one or both this week and you walk in with **your own numbers** to compare against the exercise output. Not required. Strongly recommended. These two are a notch more technical, since they need Node 22 or newer installed on your machine. If that means nothing to you, skip them with a clear conscience and come to the workshop anyway.

### AgentRC - score one of your repos in five minutes

[**microsoft/agentrc**](https://github.com/microsoft/agentrc) scores any Git repo across nine pillars (style, build, testing, docs, dev environment, code quality, observability, security, AI tooling) and places you on a maturity ladder: Functional -> Documented -> Standardized -> Optimized -> Autonomous.

Pick a repo you actually own. At the Copilot prompt, in plain English:

```
Score the Git repo at <path-to-your-repo> with microsoft/agentrc readiness. Save the scorecard and tell me the maturity level.
```

Under the hood that runs `npx -y github:microsoft/agentrc readiness`, so this one needs Node 22+ and `gh auth status` returning your username. Five minutes. Bring the maturity level number to the workshop.

### AI Engineering Coach - your personal AI-usage dashboard

[**microsoft/AI-Engineering-Coach**](https://github.com/microsoft/AI-Engineering-Coach) is a VS Code extension that reads your existing Copilot Chat, Copilot CLI, Cursor, Claude Code, and Codex session logs **locally** and shows you the patterns you would never spot yourself. Anti-patterns, prompt repetition, token burn, which workspaces eat your time. Nothing leaves your machine.

> **Coach is not in the VS Code Marketplace.** Searching the marketplace for "Coach" returns unrelated extensions. You install it by cloning the repo and building the `.vsix` yourself. The fastest path is to let Copilot CLI do it for you. At the prompt:
>
> ```
> Install https://github.com/microsoft/AI-Engineering-Coach as a VS Code extension on my machine. Read the repo README, run the build steps, install the resulting .vsix. Tell me when done.
> ```

Open VS Code, find the Coach icon in the sidebar. If you have used AI in VS Code or Copilot CLI for a few weeks, the dashboard populates immediately.

**Why bother before the workshop:** the workshop trains the *pattern* of AI-first delivery. AgentRC and Coach tell you *where your team actually is* on that pattern today. Combine them with the workshop output and you have a one-slide story for your next leadership conversation.

---

## More on the Codespace (the last rung)

If the ladder in step 2 sent you here, this is what you get: a full terminal in a browser tab, the CLI already installed, the workshop file open. It runs in the cloud, so your laptop's locks do not apply. Same experience as local, not a stripped-down one. Click the link, wait about 90 seconds, you land in a working terminal. Free on a personal GitHub account, 60 hours a month, and this workshop uses a fraction of that.

It is the last rung for one reason: it lives in the browser, so nothing stays on your laptop afterward. Use it to get through the day, then have the install conversation with IT so you end up with a local setup too. See [`help-codespaces.md`](help-codespaces.md) for the detail.

---

## On the day, bring this

- The laptop you set up, or just the Codespace link
- Your GitHub credentials
- The AgentRC scorecard, if you ran it (one number, one minute of share-back)

The **core** uses only the Microsoft Learn MCP. That endpoint is public, needs no token, and works in nearly every enterprise. The **stretch tiers** add a GitHub MCP (your own PAT) and an Azure MCP (your own `az login`). If either is locked down on your laptop, skip the stretch. The core alone is the workshop.

When you sit down in the room, open [`IN-WORKSHOP.md`](IN-WORKSHOP.md).
