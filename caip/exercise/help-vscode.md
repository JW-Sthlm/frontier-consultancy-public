# VS Code as a file viewer (optional helper)

**You do not need VS Code for this exercise.** Copilot CLI does everything on its own.

But if you like seeing the files Copilot is creating - in a tree view, syntax-highlighted, with proper markdown preview - open VS Code alongside your terminal. Nothing else changes.

---

## Two-minute setup

1. Install VS Code from **[code.visualstudio.com](https://code.visualstudio.com/)** if you do not have it.
2. After Copilot CLI has cloned the exercise folder for you (happens in Step 1 of [`IN-WORKSHOP.md`](IN-WORKSHOP.md)), open that folder in VS Code: right-click the folder in File Explorer → **Open with Code**, or from inside VS Code, **File → Open Folder**.
3. If you want to run Copilot CLI *inside* VS Code instead of a separate terminal window, open VS Code's integrated terminal: **View → Terminal** (or **Ctrl+`**). Run `copilot --allow-all` in it. Same CLI, same experience, just no window switching.

That is it. Go back to [`IN-WORKSHOP.md`](IN-WORKSHOP.md).

---

## What about GitHub Copilot in VS Code Chat?

Copilot Chat (the panel in VS Code) is a **different** runtime from Copilot CLI. It has its own MCP configuration (`.vscode/mcp.json`) and its own behaviour. For this exercise we stick with Copilot CLI everywhere, because:

- The "install your own MCP by pasting a docs URL" move is sharper in the CLI.
- One set of instructions works for everyone, regardless of editor.
- The CLI is the tool you will actually run on a customer engagement.

Play with Copilot Chat another time. Today we train the CLI muscle.
