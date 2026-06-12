# CAIP Frontier Consultancy - Hands-on exercise

**You have 15 minutes before your next call with Nordwind Aerospace. Use Copilot + the Microsoft Learn MCP to build them a briefing that actually lands.**

---

## Just two files to read

| When | Open |
|------|------|
| **Day before** | [`BEFORE-WORKSHOP.md`](BEFORE-WORKSHOP.md) - five prereq checks, ~20 minutes |
| **In the room** | [`IN-WORKSHOP.md`](IN-WORKSHOP.md) - the three-step exercise, ~25 minutes |

No time to prep? Use the Codespaces fallback: **[Open the exercise in a Codespace →](https://codespaces.new/JW-Sthlm/frontier-consultancy-public?quickstart=1)** Browser tab, no installs, ~90 seconds to a working terminal with the workshop file open.

---

## The scenario

You are the solution architect on a new partner consultancy motion. Your client is **Nordwind Aerospace**, a Kiruna-based small-satellite operator. They just landed a big reinsurance contract and their ops team is drowning. Their CTO, Ingrid, wants a one-page brief that answers one question:

> *"Can we just use ChatGPT for this, or do we need something more?"*

The brief, the meeting notes, and the template all live in this repo under [`client/`](client/). You will not download them yourself. Copilot CLI does that for you in Step 1 of [`IN-WORKSHOP.md`](IN-WORKSHOP.md).

---

## Workshop context

- **[CAIP track landing](https://jw-sthlm.github.io/frontier-consultancy-public/caip/)** - overview of the track.
- **[Workshop deck (HTML)](https://jw-sthlm.github.io/frontier-consultancy-public/caip/presentation/)** - the slides you saw, press `P` for presenter view.
- **[Frontier one-pager](https://jw-sthlm.github.io/frontier-consultancy-public/partner-overview/)** - the motion in a single page.

---

## Helper files (only if you need them)

- [`help-codespaces.md`](help-codespaces.md) - more detail on the Codespaces fallback
- [`help-vscode.md`](help-vscode.md) - optional VS Code file viewer alongside Copilot CLI
- [`help-no-account.md`](help-no-account.md) - no GitHub or no Copilot seat? Fresh setup in 10 minutes
- [`FAQ.md`](FAQ.md) - top 20 failure modes with one-line fixes

## Stretch tiers (only if the core brief is done)

- [`stretch-github-issue.md`](stretch-github-issue.md) - ship the brief as a real GitHub issue
- [`stretch-azure-grounding.md`](stretch-azure-grounding.md) - ground the brief in your real Azure footprint

---

## Take this home: measure where you actually are

Two free, local-only instruments. If you ran them in the BEFORE-WORKSHOP bonus section, you already have data. If not, install them this week. They tell you where your team is on the AI-first ramp without needing anything from Microsoft.

> **You do not have to type the commands below.** The Copilot CLI pattern you just used works here too. Open Copilot CLI in any folder and paste:
>
> ```
> Install https://github.com/microsoft/agentrc for me and run a readiness scan on this repo.
> ```
>
> Copilot fetches the README, picks the right commands for your machine, runs them, and explains what it did. Same trick for Coach.

### 1. AgentRC: score one of your repos

[**microsoft/agentrc**](https://github.com/microsoft/agentrc) scores any Git repo across nine pillars (style, build, testing, docs, dev environment, code quality, observability, security, AI tooling) and gives you a maturity level: Functional -> Documented -> Standardized -> Optimized -> Autonomous.

```bash
cd <your-repo>
npx -y github:microsoft/agentrc readiness
```

Five minutes. Run it on three different repos in your portfolio (a customer project, an internal product, this exercise repo) and compare. The contrast is the lesson.

**Prereqs:** Node 20+, `gh auth status` returning a username.

### 2. AI Engineering Coach: your personal AI-usage dashboard

[**microsoft/AI-Engineering-Coach**](https://github.com/microsoft/AI-Engineering-Coach) is a VS Code extension that reads your existing AI session logs locally (Copilot Chat, Copilot CLI, Cursor, Claude Code, Codex) and shows you the patterns you would never spot yourself. Anti-patterns, prompt repetition, token burn, which workspaces eat your time. Nothing leaves your machine.

> **Coach is not in the VS Code Marketplace.** Searching the marketplace for "Coach" returns unrelated extensions. You install it by cloning the repo and building the `.vsix` yourself, **or** by letting Copilot CLI do it for you with the prompt above.

Manual install if you prefer:

```bash
git clone https://github.com/microsoft/AI-Engineering-Coach.git
cd AI-Engineering-Coach
npm install
npm run package
code --install-extension ai-engineer-coach-*.vsix
# Use code-insiders --install-extension ... if you are on Insiders
```

Open VS Code, find the Coach icon in the sidebar. If you have been using AI in VS Code or Copilot CLI for a few weeks, the dashboard populates immediately.

### When to use them

| When | Use |
|------|-----|
| Quarterly repo health check | AgentRC on your top 3 repos |
| Per-developer reflection | Coach, weekly. Look at anti-patterns, not totals |
| Before the next Frontier session | Run both. Bring one number to the conversation |

### Where these fit in the Frontier story

These are the **diagnostic layer**. They tell you where you are. The workshop you just did is the **method layer** (how to deliver AI-first). The follow-up paths on the deck (hackathon, deep dive, co-delivery, shadow) are the **adoption layer** (how to make it stick).
