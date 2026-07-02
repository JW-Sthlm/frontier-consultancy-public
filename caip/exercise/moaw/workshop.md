---
published: false
type: workshop
title: Frontier Consultancy CAIP - In-Workshop Exercise
short_title: CAIP In-Workshop
description: Twenty-five minutes in Copilot CLI. Build Ingrid a grounded one-page brief for Nordwind Aerospace using the Microsoft Learn MCP, then sharpen it and package the pattern into a reusable skill.
level: beginner
authors:
  - Johan Wallquist
contacts:
  - jwallquist@microsoft.com
duration_minutes: 25
tags: copilot cli, ai, mcp, microsoft learn, azure, agentic
navigation_levels: 2
navigation_numbering: true
---

# In the workshop - the exercise

**This is the only page you need open during the workshop.** Twenty-five minutes. Three steps. You stay in Copilot CLI the entire time.

If you have not done the environment setup yet, stop. Open the [Before the workshop](https://aka.ms/ws?src=gh:JW-Sthlm/frontier-consultancy-public/main/caip/exercise/moaw/setup/) workshop first. If you skipped it and you are reading this in the room, use the Codespaces fallback: **[click here](https://codespaces.new/JW-Sthlm/frontier-consultancy-public?quickstart=1)** to spin up a prepared browser environment, ~90 seconds.

---

# Read this before you start

**You will not download anything yourself. You will not run `git clone`. You will not `cd` into folders. You will not open files in a text editor to edit them by hand.**

You will paste three prompts into Copilot CLI. Copilot does the rest. It clones the exercise repo for you, sets up its own MCP server, reads the client meeting notes, researches current Microsoft guidance, and writes a brief.

If your instinct is "wait, am I supposed to download the repo first?" - no, you are not. Copilot does it in Step 1. Just paste the prompt.

## Show your work (gateways)

This is a workshop, not a silent lab. Three times below you hit a **gateway**: a quick beat to show what you have got.

- **Remote:** drop a screenshot in the meeting chat.
- **In the room:** turn your screen around, or the facilitator puts one up on the big screen.

It keeps the group roughly together, it lets the facilitator catch anyone stuck early, and it is genuinely more interesting to see what other people's agents came back with. Two seconds each. Do not overthink it.

---

# The scenario

You are the solution architect on a new partner consultancy motion. Your client is **Nordwind Aerospace**, a Swedish company that runs 18 small satellites watching Earth for wildfires and floods. Their business is about to grow 10x.

Every day their satellites throw off alerts. A temperature reads wrong, a signal drops, an orbit drifts a little. Someone has to look at each alert and decide one thing: real fault, or false alarm? Six engineers do this by hand. It eats 40% of their week, and half the alerts turn out to be nothing.

Their VP Product has an idea. Paste each alert into ChatGPT, let it make the call, no more manual checking. Their CTO, Ingrid, has a bad feeling about handing a safety-critical decision to a general chatbot, but she cannot explain why well enough to win the room. The board meets in ten days. She wants a one-page brief that answers one question:

> *"Can we just use ChatGPT to decide which satellite alerts are real, or do we need something more?"*

You have 15 minutes before your next call with Ingrid. Use Copilot + the Microsoft Learn MCP to build her a brief that actually answers her question.

## If you get stuck - in this order

Read this now, before you start, so you know the path when something breaks. Something usually does, and that is fine. Getting unstuck is part of the muscle.

1. **Ask Copilot CLI itself.** Paste the error. Ask *"what does this mean, and how do I fix it?"* Copilot is right there. Using it to unstick itself is the muscle we are training.
2. **Check the [FAQ](https://aka.ms/ws/page?src=gh:JW-Sthlm/frontier-consultancy-public/main/caip/exercise/FAQ.md).** The top twenty failure modes are documented with one-line fixes.
3. **Ask a neighbour or the facilitator.** Last resort. Save it for the genuinely weird stuff.

---

# Step 1 - Start Copilot in yolo mode, let it set up the exercise

Open a terminal (PowerShell on Windows, Terminal on Mac).

```
copilot --allow-all
```

**What `--allow-all` does ("yolo mode"):**

- Copilot can run shell commands without asking each time.
- Copilot can read and write files without asking each time.
- Copilot can fetch any URL without asking each time.

For this exercise, yes, this is safe. You are in a sandbox. For real customer work, keep the default (Copilot asks before doing anything risky).

You see a `>` prompt. This is where the workshop happens for the next 25 minutes. Paste this whole block as one prompt:

```
I'm starting an AI workshop exercise. Please do the following for me:

1. Clone this repo to a sensible folder on my machine:
   https://github.com/JW-Sthlm/frontier-consultancy-public
   You pick the folder. Tell me the full path when done.

2. Change into the `caip/exercise/` subfolder of the clone, so everything
   you do next happens there. That is where `README.md`, `client/`, and
   the workshop files live.

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

> **Codespaces users:** the repo is already cloned and you are already in `caip/exercise/`. Copilot will detect that and skip straight to the MCP setup. Let it proceed.

Copilot narrates what it is doing as it goes:

- Clones the repo to a folder. **Watch for the full path it prints.** You need it if you want to open the folder in VS Code later as a file viewer.
- Changes into `caip/exercise/`. From here on, when Copilot reads `client/meeting-notes.md`, it is reading from inside that folder.
- Fetches the Learn MCP docs, figures out the config, edits `~/.copilot/mcp-config.json`.
- Tells you to type `/mcp` to verify, and `/restart` first if the reload is needed.

Then type:

```
/mcp
```

You should see **microsoft-learn** (or similar) in the list with a non-zero tool count. If it shows zero tools or is not listed, run `/restart` to reload the config, then `/mcp` again.

> **You just told an AI to set up your workshop environment.** Download code, configure another AI tool, verify it worked. You wrote no code. You touched no config. That is AI-first delivery, in 60 seconds.

> 📸 **Gateway 1, green light.** Screenshot your `/mcp` output, with microsoft-learn listed and a non-zero tool count, and drop it in the chat. This is how we confirm every environment is live before the real work starts. If yours comes back empty, now is the moment to say so.

---

# Step 2 - Run the Nordwind exercise

Same Copilot session. Copilot is inside the `caip/exercise/` folder from Step 1, so the file paths below resolve without you doing anything.

Paste this prompt:

```
Read client/meeting-notes.md and client/README.md so you have the full
scenario. Then research current Microsoft guidance on the Azure Landing
Zone for AI and the Microsoft Agent Framework.

Use the Microsoft Learn MCP tools to search and fetch. Do not type out
learn.microsoft.com URLs from memory, and do not guess paths. Let the
Learn MCP hand you the canonical links. If a page errors or redirects,
follow the redirect or search again through the MCP instead of stopping.

Then fill in client/brief-template.md and save the result as brief.md at
the repo root. Answer Ingrid's question directly: can Nordwind "just use
ChatGPT" for this, or do they need something more? Be specific to
Nordwind, quote their own words, and include only the Learn links the MCP
actually returned. Be commercially honest. Do not hedge.
```

Watch Learn MCP calls stream past in the terminal. That is grounded research happening live in front of you, ~3 to 5 minutes.

> **You will see some red text, and that is fine.** The agent tries a few sources and follows redirects as Microsoft shifts pages around. It checks itself and keeps going. Red here is the agent working, not failing. Let it finish before you judge the result.

When Copilot finishes, look at `brief.md`. Either ask Copilot to show it:

```
show me brief.md
```

...or open the folder in VS Code if you prefer a markdown preview. See the [VS Code helper](https://aka.ms/ws/page?src=gh:JW-Sthlm/frontier-consultancy-public/main/caip/exercise/help-vscode.md) for the two-minute setup.

> 📸 **Gateway 2, the brief.** Screenshot Ingrid's answer, can Nordwind just use ChatGPT or not, and drop it in the chat. Quick gut check for the group: did grounding it in Learn actually change the answer versus plain ChatGPT?

---

# Step 3 - Sharpen it

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

AI-first delivery is not "generate and ship". It is "generate, critique, sharpen". The second prompt is the one that trains the critique muscle.

> 📸 **Gateway 3, sharpened.** Drop the three weakest claims your agent found, or the fix you made to one of them, in the chat. This is the muscle you will actually use back at work, so it is worth showing.

---

# You are done with the core

**Showcase round.** If there is time, one or two of you walk the room through your brief, start to finish, about two minutes each. Not a polished pitch. Just show what your agent produced and the one thing that surprised you. This is the debrief, and it is where the good ideas spread.

- **Compare `brief.md` with your neighbour.** What did Learn MCP add beyond baseline ChatGPT? That contrast is the lesson.
- **Got time and a scratch GitHub repo?** Go to the [GitHub issue stretch](https://aka.ms/ws/page?src=gh:JW-Sthlm/frontier-consultancy-public/main/caip/exercise/stretch-github-issue.md). It ships the brief as a real issue.
- **Got an Azure subscription?** Go to the [Azure grounding stretch](https://aka.ms/ws/page?src=gh:JW-Sthlm/frontier-consultancy-public/main/caip/exercise/stretch-azure-grounding.md). It grounds the brief in your actual cloud footprint.
- **Still hungry? Go for the Boss Level.** The **optional stretch** on the next page is the advanced path: build a Copilot skill for a task you actually do every week, then share it. Hardest tier, biggest payoff, the one thing you keep. This is where the high scores are.

Do not jump to the stretch tiers if the core is not done. A good brief beats a half-finished stretch.

---

# 🎮 Boss Level (Extra Credit) - build a skill you will actually use

**Only for the ones who finished the core and want more.** This is the advanced path, the hardest tier, and the biggest payoff. The two file-linked stretches above make the agent *do* more. This one leaves you with a tool you open again on Monday, and a high score worth showing off.

Everything below is optional. Skip it and you have still done the workshop. Clear it and you walk out with reusable IP, not a demo. If you are the kind of person who reads "optional" as "obviously," this one is for you. 😏

## The point

You just produced a grounded brief in fifteen minutes. Good. But you did it once, by hand, prompt by prompt. That is a demo, not a capability.

The capability is when a repeatable task runs itself, the same way every time, for anyone who has the skill installed. They run one command. The pattern runs. That is the difference between a clever individual and a team that ships AI-first by default.

So you are not going to rebuild the Nordwind brief. You are going to pick a task **you actually do most weeks and dislike repeating**, and package that into a Copilot skill. A status email. A meeting recap. A PR description. A test-plan scaffold. An onboarding checklist for a new joiner. The release note nobody wants to write. Pick the one you would pay to never do by hand again.

The Nordwind brief was the worked example. This is the same moves, pointed at your real work.

## What you are building

A **Copilot CLI skill**: a small folder Copilot loads automatically, that captures one repeatable motion behind a single trigger. Once it exists, you type something like:

```
Write the weekly status update for project <X> from this week's notes.
```

...and Copilot runs the whole pattern you would otherwise do by hand.

## Step A - Let Copilot research how skills work

Same Copilot session. You are not going to hand-write the skill format from memory. Do exactly what you did with the Learn MCP in Step 1: point the agent at the docs and let it figure out the shape.

```
I want to build a reusable Copilot CLI skill. First, research how custom
skills work in Copilot CLI: where they live on disk, the folder structure,
and what the skill definition file needs (name, description, trigger,
instructions). Use the Microsoft Learn MCP and the public GitHub Copilot
CLI docs. Show me the format before you build anything.
```

If it is unsure, push it: *"find the canonical docs, do not guess the format."* Same muscle as the core.

## Step B - No task in mind? Let Copilot find one

Do not stall trying to think of the perfect task on the spot. That is the hardest part, so hand it to the agent. Tell Copilot who you are and what your week looks like, and let it pitch candidates back.

```
I want to build a Copilot CLI skill that automates something I do most
weeks. Here is my role and the kind of work I do: <two or three sentences
about your role, what you produce, and the repetitive chores you dislike>.

Suggest five tasks from my world that would make good, self-contained
skills. For each one: the trigger phrase, the inputs it needs, the output
it produces, and why it is a good fit for automation. Then tell me which
single one you would start with, and why.
```

Read the five. Pick one. The best first skill is small, repeatable, and has a clear input and a clear output. Do not over-reach on your first one. You can build the ambitious one second.

## Step C - Build the skill for your real task

Describe your weekly task to Copilot in plain English and have it build the skill. Template prompt, swap in your own task:

```
Now build me a Copilot CLI skill for a task I do most weeks: <describe the
task in two or three sentences - what goes in, what comes out, what good
looks like>.

The skill should take the inputs I named, do the work, and produce the
output in the format I actually send. Where it helps, ground the research
through an MCP I already have (Microsoft Learn, GitHub, whatever fits).
End by self-critiquing the result: the three weakest spots and a fix or
cut for each.

Bundle any template the skill needs into its folder so it is
self-contained. Write the description so Copilot triggers it when I ask
for this task in normal words. Put it in the right place on my machine and
tell me how to verify it loaded.
```

Verify it. Ask Copilot to confirm it can see the new skill.

## Step D - Run it for real (this is the test)

A skill that only worked once, on the example you built it with, is not reusable. Run it on this week's actual inputs (or last week's, if this week is thin). Real notes, real project, real output.

If it produces something you would genuinely send, with light editing, you have built reusable IP. If it is generic or wrong, fix the *skill*, not the output. The fix belongs in the pattern, so it is fixed for next week too. Run it again. That loop, run and sharpen the skill, is the whole point.

## Step E - Share it, then take it home

Two moves. The first gets you feedback today. The second is where the value actually compounds.

**1. Share it now for feedback.** Put your result where I can react to it:

- Drop it in the workshop chat, **or**
- Email it to me at **jwallquist@microsoft.com**: the skill folder (or repo link) plus two lines on what it does.

I will read these and come back to you. Half the value is a second pair of eyes on whether the pattern is right.

**2. Take it back to your team.** This is the real prize, and it is yours, not mine. A skill on your laptop helps one person. A skill your practice adopts changes how the whole bench works.

- Drop the skill in a public repo with a short README so a colleague can install it in a minute. Ask Copilot to scaffold the README and, if you did the GitHub-issue stretch, to create and push the repo for you.
- Show it to two colleagues next week. Let them point it at *their* version of the task. Watch where it breaks, then harden it.
- Multiply. Ten of these and a consultant's first hour on any engagement looks completely different. That is the motion we are really teaching. The brief was just the on-ramp.

Strip anything client-confidential before you share anything. This is a *method*, not a deliverable. Nothing real or sensitive in the repo.

> 📸 **Gateway 4, the exam.** Post your result in the chat **or** email it to me at **jwallquist@microsoft.com**: the **public repo link**, or a **screenshot of your skill running** on real inputs. This is your exam piece. It shows you did not just use an agent, you built something you and your team will reuse. If you got here, you are ahead of most of the room, and I want to see it. 🤩

## Why this matters

This is the whole Frontier thesis in one artefact. Your job in a modern consultancy is not to do the task faster. It is to design the pattern once so everyone on the bench runs it, on demand, at the same quality. One person's clever afternoon becomes the team's default. A reusable skill is small, but it is the unit that scales, from you, to your team, to the wider practice.
