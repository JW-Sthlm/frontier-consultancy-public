# Discovery call — Nordwind Aerospace AB

**Date:** two weeks ago, Thursday 14:00–15:30.
**Location:** Nordwind HQ, Stockholm (Kista).
**Your notes. Scrappy. Not rewritten.**

---

## Company

- **Nordwind Aerospace AB.** HQ Stockholm (Kista), mission ops and ground station in Kiruna.
- ~120 people. Founded 2017. Series C closed last year.
- Operates **18 small Earth-observation satellites**. Sun-synchronous orbit.
- Core products: **wildfire tracking**, **flood-extent mapping**, **illegal-fishing monitoring**. Sold to governments, NGOs, increasingly to reinsurance.
- Just signed a **3-year contract with a European reinsurance consortium**. Volume about to 10x on wildfire + flood.

## In the room

- **Ingrid Aslaug** — CTO. PhD signal processing. Pragmatic. Skeptical of buzzwords. Reads the Azure roadmap.
- **Magnus Velde** — Head of Mission Operations. Former Swedish Space Corp. "I have 6 engineers running 18 birds. You cannot hire your way out of this."
- **Sara Lindqvist** — VP Product. Ex-management-consulting. Pushing the "agent" idea after reading about it in *The Economist*.

## What Ingrid said (close to verbatim)

- "Our engineers spend 40% of their time triaging satellite anomalies. Half of those are false alarms. The pattern is learnable. We have not had the time."
- "Our customers still get their imagery by **FTP**. In 2026. I know."
- "Sara keeps saying 'can we just use ChatGPT for this?' I don't think so, but I cannot explain why well enough. Help me make the case internally."
- "We are on Azure. Some workloads there, some on-prem at Kiruna. Nobody is sure what is where."
- "The board wants to hear 'AI' at the next meeting. I do not want to lie to them."

## What Sara said

- "ChatGPT already answers better than our internal wiki. Why can't we just use that for anomaly triage?"
- "We have the data. We just need to plug it in, right?"
- "Everybody's doing agents. We should be doing agents."

## What Magnus said

- "If one thing breaks our operator console during a satellite pass, we lose the imagery. Downtime costs us a customer. Whatever you build has to be **rock solid**."
- "We cannot have an AI tell an engineer to ignore an alert, and then a bird tumbles."

## Current state (what you picked up between the lines)

- Mostly Python scripts in GitHub. CI is inconsistent. No ML platform.
- **Some Azure** — a few VMs, one storage account they use heavily, an OpenAI resource Sara spun up last month. "Not used for anything production yet."
- **No landing zone.** Nobody mentioned networking, identity, policy, or observability without prompting.
- Customer data delivery pipeline is the FTP server and a scheduled rsync.
- Analyst-side anomaly triage is a web console pointing at a Postgres DB. Engineers click through alerts. Engineers are tired.

## Their explicit ask

> "Come back in two weeks with a **one-pager** we can show the board. Answer Sara's question. Tell us what 'doing AI properly' actually looks like for an ops team like ours. Be specific about what we would **buy, build, or stop doing**."

## Budget signal

- No number on the table.
- Ingrid said "serious 2026 investment" twice.
- Magnus mentioned their infrastructure budget is "substantially underspent" because they have not been able to hire fast enough to use it.

## What the board cares about (Ingrid, offhand, walking to the lift)

1. Can we scale mission ops without doubling headcount?
2. Are we defensible on quality and safety if regulators start looking?
3. Does any of this actually make the reinsurance contract deliverable?

## Your opportunity

A brief that:

- Reframes Sara's "just use ChatGPT" question in a way that does not make her look stupid (she is not) but gives Ingrid the argument she needs internally.
- Explains what an **Azure Landing Zone for AI** is and why it is the right foundation *for this specific company* — not a generic pitch.
- Introduces the **Microsoft Agent Framework** as the pattern for mission-ops agents (anomaly triage, customer delivery, customer comms) with a clear boundary between what an agent decides and what a human decides.
- Gives three honest next steps. Two weeks, two months, two quarters. No ten-year roadmap.

You have about fifteen minutes before your next call. Go.
