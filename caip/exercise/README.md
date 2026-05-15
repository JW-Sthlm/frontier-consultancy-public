# CAIP Frontier Consultancy — Hands-on exercise

**You have 15 minutes before your next call with Nordwind Aerospace. Use Copilot + the Microsoft Learn MCP to build them a briefing that actually lands.**

---

> **Before the workshop:** run the five-minute prereq check in [`SETUP-overview.md`](SETUP-overview.md). It tells you what to install ahead of time and what to do if your work laptop blocks any of it. Codespaces is the fallback. No IT escalation needed for the day itself.

## Workshop context

The slides, storyboard, and one-pager from the session live on the public partner site. Open any of these in a new tab:

- **[CAIP track landing](https://jw-sthlm.github.io/frontier-consultancy-public/caip/)** — overview of the track.
- **[Workshop deck (HTML)](https://jw-sthlm.github.io/frontier-consultancy-public/caip/presentation/)** — the slides you saw, press `P` for the presenter view.
- **[Storyboard](https://jw-sthlm.github.io/frontier-consultancy-public/caip/storyboard.html)** — the narrative for each slide if you want to revisit a section.
- **[Frontier one-pager](https://jw-sthlm.github.io/frontier-consultancy-public/partner-overview/)** — the motion in a single page.
- **[Partner landing](https://jw-sthlm.github.io/frontier-consultancy-public/partners/)** — where this all sits across tracks.

---

## The scenario

You are the solution architect on a new partner consultancy motion. Your client is **Nordwind Aerospace**, a Kiruna-based small-satellite operator. They just landed a big reinsurance contract and their ops team is drowning. Their CTO wants a one-page brief that answers one question:

> *"Can we just use ChatGPT for this, or do we need something more?"*

Everything you need to walk into that brief is in [`client/`](client/README.md). Read the meeting notes first. They are scrappy. They are real.

## What you will do

1. **Set up Copilot** with the Microsoft Learn MCP — your grounded-research tool.
2. **Read the Nordwind discovery notes** (`client/meeting-notes.md`).
3. **Prompt Copilot** to build a one-page briefing using the template (`client/brief-template.md`), grounded in current Microsoft Azure guidance — specifically the **Azure Landing Zone for AI** and the **Microsoft Agent Framework**.
4. **Compare with your neighbour.** What did the Learn MCP change versus baseline ChatGPT?

You should walk out with a `brief.md` you would actually be comfortable sending to a client.

## Pick your path

| You have… | Start here |
|-----------|------------|
| Done the [prereq check](SETUP-overview.md), everything passed | **[Tier 1 — Copilot CLI](SETUP-tier1.md)** |
| A prereq check failed, or your work laptop blocks installs | **[Codespaces fallback](SETUP-codespaces.md)** |
| No GitHub account, or no Copilot seat | **[Tier 0 — Fresh account in 10 minutes](SETUP-tier0.md)** |

There is **one path**: Copilot CLI. It looks intimidating for about sixty seconds, and then something magical happens — you prompt Copilot to install its own MCP server by giving it a docs URL. That is the moment the whole "AI-first delivery" story clicks. You will feel it.

Prefer looking at the files you are creating in a nice editor? Open VS Code alongside — it is just a file viewer in this exercise. See the short note in [`SETUP-vscode.md`](SETUP-vscode.md). Everything you *do* still happens in Copilot CLI.

## Stretch tiers (only if you finish early)

- **[Tier 2 — Ship the brief as a GitHub issue](SETUP-tier2.md)** — adds the GitHub MCP.
- **[Tier 3 — Ground the brief in your real Azure footprint](SETUP-tier3.md)** — adds the Azure MCP.

Do **not** jump to Tier 2/3 if the core is not done. A good brief beats a half-finished stretch.

## Timing

- Pre-workshop: ~10 minutes on a fresh account, ~3 minutes if you already have a Copilot seat.
- Workshop core (Tier 1): **20 minutes** of real work.
- Share-back: **5 minutes**.

## If something goes wrong — in this order

1. **Ask Copilot CLI itself.** Paste the error. Ask *"what does this mean, and how do I fix it?"* Copilot is right there. Using it to unstick itself is the muscle we are training today.
2. **Check the [FAQ](FAQ.md).** The top twenty failure modes are documented with one-line fixes.
3. **Ask a neighbour or the facilitator.** Last resort — save it for the genuinely weird stuff.

## What "good" looks like

A completed sample brief sits in [`facilitator/sample-output.md`](facilitator/sample-output.md) — but don't peek until you have your own first pass. Yours will be better than you expect.
