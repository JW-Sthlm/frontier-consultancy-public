# Copilot Skill Deck Maker

A small Copilot skill for turning notes, meeting recaps, or a topic into a single-file HTML presentation.

It was built for Microsoft partner consultants in Johan Wallquist's Frontier Consultancy CAIP workshop. The idea is simple: you should be able to paste rough material into Copilot and get a deck you can open in a browser, send as one file, and present without fighting formatting late in the evening.

The skill is inspired by Johan's larger Slidemaster agent. This version is intentionally smaller. No framework clone. No PowerPoint dependency. No build step.

## Why it exists

Consultants often leave a meeting with useful notes and a weak next artifact.

This skill gives you a clean first deck from that raw material:

- One self-contained HTML file.
- Partner brand-matched look when you provide a homepage URL.
- Built-in presenter notes via `?presenter=notes`.
- Arrow-key navigation and fullscreen.
- Clear anti-AI writing rules baked into the workflow.

It will not replace your judgement. Good. That is the point.

## Install in Copilot CLI

### 1. Open the skill file

The skill is a single file: [SKILL.md on GitHub](https://github.com/JW-Sthlm/frontier-consultancy-public/blob/main/skills/copilot-skill-deck-maker/SKILL.md). Open it and copy the raw contents.

### 2. Save it into your Copilot skills folder

Save the file to `~/.copilot/skills/copilot-skill-deck-maker/SKILL.md` on your machine. Create the folder if it isn't already there. Copilot loads skills from this location automatically.

On Windows the path resolves to `C:\Users\<you>\.copilot\skills\copilot-skill-deck-maker\SKILL.md`.

### 3. Restart your Copilot CLI session and try it

Skills load when the session starts, so begin a fresh session. Then ask Copilot something like:

- *Make a deck from these notes: ...*
- *Build slides about our AI readiness workshop. Use https://www.example-partner.com for brand matching.*

The skill picks up from there.

## Use it in VS Code Copilot Chat

VS Code Copilot Chat does not load Copilot CLI skills from `~/.copilot/skills` automatically. Two paths work well:

1. Drop the contents of SKILL.md into your repo's `.github/copilot-instructions.md` under a clear heading.
2. Or save it as `.github/instructions/copilot-skill-deck-maker.instructions.md` in the repo.

Then start a new chat and ask Copilot to follow the deck maker instructions. Keep the file in the repo if the whole team should use it.

## Example prompt

> Make a deck from these notes.
> Audience: partner delivery leads.
> Length: 5 slides.
> Brand: https://www.example-partner.com
> Notes:
> - The workshop showed that consultants lose time after meetings.
> - The team wants faster recap, deck, and follow-up creation.
> - Main risk is trusting the first draft too much.
> - Next step is a two-week pilot with three account teams.

## What you get

Open the example deck here:

[example.html](./example.html)

You get a browser presentation with branded styling, speaker notes, and a clean next step. One file. Send it, open it, present it.

Made by [Frontier Consultancy](/partners/) and Johan Wallquist for Microsoft partner consultants.
