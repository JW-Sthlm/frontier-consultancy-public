# In the workshop - the exercise

**This is the only file you need open during the workshop.** Twenty minutes. Three steps. You stay in Copilot CLI the entire time.

If you have not done the environment setup yet, stop. Open [`BEFORE-WORKSHOP.md`](BEFORE-WORKSHOP.md) first. If you skipped it and you are reading this in the room, use the Codespaces fallback: **[click here](https://codespaces.new/JW-Sthlm/frontier-consultancy-public?quickstart=1)** to spin up a prepared browser environment, ~90 seconds.

---

## Read this before you start

**You will not download anything yourself. You will not run `git clone`. You will not `cd` into folders. You will not open files in a text editor to edit them by hand.**

You will paste three prompts into Copilot CLI. Copilot does the rest. It clones the exercise repo for you, sets up its own MCP server, reads the client meeting notes, researches current Microsoft guidance, and writes a brief.

If your instinct is "wait, am I supposed to download the repo first?" - no, you are not. Copilot does it in Step 1. Just paste the prompt.

---

## The scenario

You are the solution architect on a new partner consultancy motion. Your client is **Nordwind Aerospace**, a Kiruna-based small-satellite operator. They just landed a big reinsurance contract and their ops team is drowning. Their CTO, Ingrid, wants a one-page brief that answers one question:

> *"Can we just use ChatGPT for this, or do we need something more?"*

You have 15 minutes before your next call with Ingrid. Use Copilot + the Microsoft Learn MCP to build her a briefing that actually lands.

---

## Step 1 - Start Copilot in yolo mode, let it set up the exercise

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

---

## Step 2 - Run the Nordwind exercise

Same Copilot session. Copilot is inside the `caip/exercise/` folder from Step 1, so the file paths below resolve without you doing anything.

Paste this prompt:

```
Read client/meeting-notes.md and client/README.md so you have the full
scenario. Using the Microsoft Learn MCP, research the current Microsoft
guidance on the Azure Landing Zone for AI and the Microsoft Agent
Framework. Then fill in client/brief-template.md and save the result as
brief.md at the repo root.

Answer Ingrid's question directly: can Nordwind "just use ChatGPT" for
this, or do they need something more? Be specific to Nordwind - quote
their own words. Include the URLs of the Learn pages you used. Be
commercially honest. Do not hedge.
```

Watch Learn MCP calls stream past in the terminal. That is grounded research happening live in front of you, ~3 to 5 minutes.

When Copilot finishes, look at `brief.md`. Either ask Copilot to show it:

```
show me brief.md
```

...or open the folder in VS Code if you prefer a markdown preview. See [`help-vscode.md`](help-vscode.md) for the two-minute setup.

---

## Step 3 - Sharpen it

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

---

## You are done with the core

- **Compare `brief.md` with your neighbour.** What did Learn MCP add beyond baseline ChatGPT? That contrast is the lesson.
- **Got time and a scratch GitHub repo?** -> [`stretch-github-issue.md`](stretch-github-issue.md) ships the brief as a real issue.
- **Got an Azure subscription?** -> [`stretch-azure-grounding.md`](stretch-azure-grounding.md) grounds the brief in your actual cloud footprint.

Do not jump to the stretch tiers if the core is not done. A good brief beats a half-finished stretch.

---

## If something goes wrong - in this order

1. **Ask Copilot CLI itself.** Paste the error. Ask *"what does this mean, and how do I fix it?"* Copilot is right there. Using it to unstick itself is the muscle we are training.
2. **Check the [FAQ](FAQ.md).** The top twenty failure modes are documented with one-line fixes.
3. **Ask a neighbour or the facilitator.** Last resort. Save it for the genuinely weird stuff.
