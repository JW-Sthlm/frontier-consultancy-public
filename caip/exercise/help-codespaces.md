# Codespaces fallback - one click to a prepared environment

Use this when your work laptop will not let you install Node, global npm, or the Copilot CLI itself, or when you forgot the prep and the workshop starts in five minutes.

## One click

**[Open the exercise in a Codespace →](https://codespaces.new/JW-Sthlm/frontier-consultancy-public?quickstart=1)**

What happens after the click:

1. GitHub asks you to sign in (use a **personal** account, not your work account - work accounts often inherit policies that block what we are about to do).
2. You see a *"Create codespace"* page. Click **Create new codespace**. Defaults are fine.
3. ~90 seconds of boot. The devcontainer installs Node 20, GitHub CLI, and Copilot CLI for you.
4. You land in a browser VS Code with [`IN-WORKSHOP.md`](IN-WORKSHOP.md) already open and the terminal at the bottom in the right folder.

That is it. From here you follow [`IN-WORKSHOP.md`](IN-WORKSHOP.md) like everyone else.

## Cost

Free on a personal GitHub account. 60 hours per month on the smallest machine. The workshop uses about 90 minutes of compute.

## If something looks off after the boot

If the terminal welcome banner says *"Welcome to Codespaces! You are on our default image"* instead of *"You are on a custom image defined in your devcontainer.json file"*, the devcontainer did not load. Fix it:

- Command Palette (`F1`) -> *Codespaces: Rebuild Container*, **or**
- Run `npm install -g @github/copilot` in the terminal manually (~30 seconds).

Verify:

```
copilot --version
```

You should see `1.0.46` or newer. Anything older means the devcontainer did not load - rebuild.

If you do not have a personal GitHub account, run [`help-no-account.md`](help-no-account.md) first.

## When you are done

The Codespace stops automatically after 30 minutes of inactivity. To delete explicitly: visit [`github.com/codespaces`](https://github.com/codespaces), find your codespace, click **...** -> **Delete**.
