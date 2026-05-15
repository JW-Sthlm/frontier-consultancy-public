# Codespaces fallback

When your work laptop will not let you install Node, or global npm, or the Copilot CLI itself, this path lets you do the full exercise in a browser tab. It uses GitHub Codespaces on a personal account. No IT involvement needed.

## When to use this

- One of the prereq checks in [`SETUP-overview.md`](SETUP-overview.md) failed.
- Your corporate firewall blocks `learn.microsoft.com` or general HTTPS to MCP endpoints.
- You want a clean sandbox separate from your work environment.

## The cost story

Codespaces is free on a personal GitHub account, 60 hours per month on the smallest machine. The workshop uses about 90 minutes of compute. You will burn roughly 1.5 hours of your monthly quota. No credit card. No conversion trap.

## Step 1. Sign in with a personal GitHub account

Open [`github.com`](https://github.com) and sign in with a personal account, not your work account. Two reasons:

1. Codespaces on a work account often inherits org policies that block exactly what we are about to do.
2. The Copilot CLI device-code flow inside the Codespace will sign in against this same account. Keeping it personal avoids any work-tenant friction.

If you do not have a personal GitHub account, run [`SETUP-tier0.md`](SETUP-tier0.md) first. Two-minute account creation, free Copilot Pro trial.

## Step 2. Open the exercise as a Codespace

Click this link:

**[Open the exercise in a Codespace →](https://codespaces.new/JW-Sthlm/frontier-consultancy-public?quickstart=1)**

GitHub shows a *"Create codespace"* page. You will see:

- The repo name **JW-Sthlm/frontier-consultancy-public**.
- A *"No codespace to resume"* note. That is normal on first visit, not an error.
- A green **Create new codespace** button.

Click **Create new codespace**. Default options are fine (2-core, 4 GB RAM is plenty).

About 90 seconds to boot. The devcontainer installs Node 20 and Copilot CLI for you while you wait. You will see *"Setting up codespace"* in the bottom-right of the VS Code web UI.

> **Your Codespace is isolated.** It runs on GitHub's infrastructure, in a private container only you can see. You cannot accidentally affect the source material. Edits live only in your Codespace. Nothing pushes anywhere. The Codespace stops on idle and you can delete it when you are done.

## Step 3. Open the terminal

When the Codespace finishes booting, you land in a web VS Code editor. Open the integrated terminal:

- Menu: **Terminal → New Terminal**
- Keyboard: `` Ctrl+` ``

The terminal welcome banner should say **"You are on a custom image defined in your devcontainer.json file"**. That confirms the devcontainer loaded.

If instead you see *"Welcome to Codespaces! You are on our default image"*, the devcontainer did not load. Most common cause: the repo had not synced when you created the Codespace. Fix it one of two ways:

- **Rebuild:** Command Palette (`F1`) → *Codespaces: Rebuild Container*.
- **Manual install:** run `npm install -g @github/copilot` in the terminal. Takes ~30 seconds. Then continue normally.

Verify Copilot CLI is ready:

```
copilot --version
```

You should see **`1.0.46` or newer** (the version published to npm at the time of writing). If you see something old like `1.0.3` or `1.0.1x`, that is the version baked into GitHub's default Codespaces image, which means our devcontainer did not load. Use the rebuild fallback above to fix it.

## Step 3.5. Make the Codespace feel like a terminal

VS Code in the browser opens with three things competing for your attention: the **Explorer** on the left, the **editor** in the middle (probably showing a README preview), and a **Copilot Chat** panel on the right. For this workshop you only need one of them: the terminal at the bottom.

Here is the target layout you want:

```
 ┌─────────────┬───────────────────────────────────────┐
 │ EXPLORER    │   Editor area                         │
 │             │   (file previews appear here when     │
 │ client/     │    you click a file in Explorer)      │
 │ .devcontainer/                                      │
 │ README.md   │                                       │
 │ FAQ.md      │                                       │
 │ ...         │                                       │
 │             ├───────────────────────────────────────┤
 │             │   TERMINAL                            │
 │             │   $ copilot --allow-all               │
 │             │   >                                   │
 │             │   ▶  YOU WORK HERE  ◀                 │
 └─────────────┴───────────────────────────────────────┘
```

The Codespace opens directly inside the exercise folder, so the Explorer shows only the files you need for the workshop.

Three quick moves get you there.

**1. Close the Copilot Chat panel on the right.** Look at the top-right of the screen. You will see a panel labelled **CHAT** with "Build with Agent" or "Describe what to build". Click the **✕** in that panel's top-right corner. Keyboard shortcut: `` Ctrl+Alt+B `` (toggles the auxiliary bar).

Why close it: Copilot Chat is a different product from Copilot CLI. Different runtime, different MCP config, different commands. Having both visible at the same time makes it unclear which one you are talking to. Today's workshop happens in the terminal, not in Chat. Close it and the confusion goes away.

**2. Close the README preview tab (optional).** Codespaces auto-opens `README.md` in a preview tab. You can keep it or close it (click the × on the tab). Either is fine. If you close it, the editor area sits empty until you click a file in Explorer.

**3. Maximize the terminal panel.** Click the **maximize icon** in the terminal panel header (top-right of the panel, looks like a square outline). The terminal expands to fill the editor area, with Explorer still visible on the left. Same effect via Command Palette: `` Ctrl+Shift+P `` → *Toggle Maximized Panel*.

**Bonus tip: click files in Explorer to preview them.** When Copilot writes `brief.md` later in the exercise, you do not have to `cat` it in the terminal. Click the file in the Explorer tree on the left and it opens in a tab in the editor area. Markdown renders nicely. Click back into the terminal to keep working. This is one place a Codespace beats a local terminal.

That is it for the UI. The rest of the workshop happens inside the terminal.

## Step 4. Sign in to Copilot CLI

Same Copilot CLI experience as the local path. Run:

```
copilot
```

Copilot shows a device code and asks you to visit [`github.com/login/device`](https://github.com/login/device). Open the link, paste the code, approve. Use the **personal** GitHub account you signed in with in Step 1.

Come back to the Codespace terminal. You are at the `>` prompt. Type `/exit` for now.

## Step 5. Start Copilot in yolo mode and install the Learn MCP

In the Codespace terminal:

```
copilot --allow-all
```

`--allow-all` lets Copilot run shell commands, read and write files, and fetch URLs without asking each time. In a fresh Codespace, that is exactly what you want.

At the `>` prompt, paste this prompt as one block. The Codespace opens directly in the exercise folder, so the prompt only asks Copilot to set up the MCP.

```
I'm starting an AI workshop exercise. The exercise files are already in
this Codespace and the terminal is open in the exercise folder. Please:

1. Set up the Microsoft Learn MCP server in my Copilot CLI config so you
   can ground your answers in current Microsoft documentation. The docs
   URL for the Learn MCP is:
   https://learn.microsoft.com/training/support/mcp
   Read that page, figure out the right config, add it to
   ~/.copilot/mcp-config.json.

2. When done, tell me to run the slash command /mcp in this same Copilot
   CLI session to verify the server is listed. If the new config needs to
   be reloaded, tell me to use /restart.
```

Copilot will fetch the Learn MCP docs, edit `~/.copilot/mcp-config.json`, and tell you to verify. Type:

```
/mcp
```

You should see **microsoft-learn** listed with a non-zero tool count. If it shows zero tools or is not listed, run `/restart` to reload the config, then `/mcp` again.

> **This is the moment.** You just told an AI to set up its own grounded-research tool from a docs URL. The whole "AI-first delivery" idea sits in this one prompt.

## Step 6. Continue at the Nordwind exercise

From here you join [`SETUP-tier1.md`](SETUP-tier1.md) at **Step 6, Run the Nordwind exercise**. The rest of the workshop runs identically. The Codespace has everything you need.

## When you are done

The Codespace stops automatically after 30 minutes of inactivity. To clean up explicitly: visit [`github.com/codespaces`](https://github.com/codespaces), find your codespace, click **…** → **Delete**. That frees the storage quota too.

## MCP access from Codespaces

Codespaces runs in GitHub's infrastructure, not on your corporate network. Useful properties:

- **Microsoft Learn MCP** always works. Public endpoint, no auth, no firewall in the way.
- **GitHub MCP** (Tier 2 stretch) works fine. Generate a personal access token on your personal account, paste it in. Standard.
- **Azure MCP** (Tier 3 stretch) works if you have an Azure subscription you can `az login` to from inside the Codespace. The Azure CLI is not pre-installed in this devcontainer. Run `curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash` if you want it.

If even Codespaces is unavailable on your personal account (rare, usually means you signed in with a work account by accident), sign out completely, sign back in with a personal email, retry.
