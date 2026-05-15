# FAQ — common failures, quick fixes

**Before you open this page: ask Copilot CLI itself first.** Paste the error into the `>` prompt and ask *"what does this mean, and how do I fix it?"* — Copilot is right there, the whole point of this workshop is to train that muscle. Come here if Copilot's answer does not land, or if you want a second opinion.

This page covers the top twenty failure modes from dry-runs. Keep it open in a tab during the workshop.

---

## Install and auth

| Symptom | Cause | Fix |
|---------|-------|-----|
| `node: command not found` | Node not installed | **[nodejs.org](https://nodejs.org/)** → LTS installer → reopen terminal |
| `npm install -g @github/copilot` fails with EACCES / permission denied on Mac/Linux | Global npm needs sudo or a user prefix | `npm config set prefix ~/.npm-global` then `export PATH=~/.npm-global/bin:$PATH` then retry |
| `npm install -g` silently blocked on Windows corp laptop | MDM blocks global npm | Use the **[Codespaces fallback](SETUP-codespaces.md)** for the day. Raise the access gap with IT afterwards. |
| Device code page opens but "authentication failed" | Browser signed into wrong GitHub account | Sign out of GitHub in browser, retry `copilot` — you will be prompted fresh |
| `copilot` starts but says "no Copilot plan" | Trial not activated or wrong account | Verify at `github.com/settings/copilot` — must show **Active** |
| Anything else on the prereq check fails | Corporate laptop policy, firewall, or proxy | Use the **[Codespaces fallback](SETUP-codespaces.md)**. It solves all five prereq checks at once. |

---

## MCP problems

| Symptom | Cause | Fix |
|---------|-------|-----|
| `/mcp` shows Learn MCP but "0 tools" | Server started but handshake failed | Restart Copilot CLI (`/exit` then `copilot`). If still zero, check firewall — Learn MCP needs HTTPS to `learn.microsoft.com` |
| Learn MCP "connection refused" | Corporate firewall blocks Learn endpoint | Switch to the **[Codespaces fallback](SETUP-codespaces.md)** — Codespaces runs outside your corp network. If you cannot switch mid-workshop, run the exercise **without** MCP for now: `copilot -p "<prompt>"`. Narrate to the room that this is baseline vs grounded. |
| VS Code shows MCP server with red status | Server failed to start | Click the server entry in the MCP panel → **View output**. Usually a typo in `.vscode/mcp.json` |
| Azure MCP (Tier 3) "no credential" error | `az login` not run in the same terminal | Run `az login` in the shell VS Code inherited from, then restart the MCP server |
| GitHub MCP (Tier 2) 403 on issue create | PAT scope wrong | Token needs **Repository → Issues: Read and write**. Regenerate the PAT. |

---

## Copilot answer problems

| Symptom | What to say to the room |
|---------|-------------------------|
| Brief is generic, does not reference Nordwind specifically | "Prompt it again: 'Rewrite this as if you are writing *to* Ingrid, quoting her actual words from the notes.' The prompt is the product." |
| Brief hedges everywhere | "Ask it: 'Remove every hedge. If you are not sure, cut the claim.' Watch the second draft." |
| Brief cites no Learn pages | "Add to the prompt: 'Include the URLs of the Learn pages you used.' Grounded means cited." |
| Copilot refuses / content filter | Try a less loaded phrasing. Content filters on Copilot are conservative around anything that looks like it touches safety-critical systems. The brief itself is fine; ask it to "write a neutral technical assessment of the options". |

---

## Last-resort fallbacks

- **One participant fully stuck** — pair them with a neighbour who is working. They still get the experience.
- **Network completely dead** — do a live facilitator demo on the projector. Participants follow along mentally. Most of the learning is the *pattern*, not the typing.
- **Copilot service outage** — highly unlikely but possible. Open the `facilitator/sample-output.md` sample brief on screen. Walk the room through *how* it was produced, prompt by prompt. Still valuable.

---

## What NOT to do

- Do not try to fix someone's install in the middle of the exercise block. Pair them up and move on.
- Do not edit other people's `.vscode/mcp.json` or config files from the facilitator laptop. Tell them what to type, let them type it.
- Do not extend the exercise past 25 minutes. The story needs the Trust Boundary close.
