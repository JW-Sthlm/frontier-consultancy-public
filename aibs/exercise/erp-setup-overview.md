# ERP exercise - Before the workshop

This is the prep page for the **ERP (F&O) exercise**. Allow 20 minutes on your own machine the day before. If all checks pass, you walk in and start working.

## What you need

- **VS Code** with GitHub Copilot Chat extension (agent mode required)
- **GitHub Copilot Pro** or better - or a **D365 Finance/SCM Premium license**, or **M365 Copilot license**, or **Copilot Studio Credits** (see [Running costs](#running-costs) below)
- The **D365 ERP MCP server** configured in VS Code
- The **MS Learn MCP server** configured in VS Code
- **Python** installed locally (required for working with Excel files)
- A **Dynamics 365 Tier 2 environment or a UDE environment** connected to Dataverse (a Tier 1 / CHE environment is not sufficient)
- The **Copilot instructions file** and **WHS skill file** placed in your VS Code workspace (see check 5 below)

---

## The six checks

### 1. You have a GitHub Copilot seat with agent mode

Open [github.com/settings/copilot](https://github.com/settings/copilot). Confirm *Copilot Pro* or *Copilot Business* shows as **Active**.

No Copilot seat? Sign up for a 30-day free Pro trial at [github.com/copilot](https://github.com/copilot).

> **Model selection:** Use an Anthropic model (Sonnet or Opus) - these currently have the best MCP tool-calling capability.

### 2. VS Code is installed with GitHub Copilot Chat

Open VS Code. In the Copilot Chat sidebar, look for the agent mode toggle (the model picker dropdown). If you do not see it, update VS Code to the latest version.

### 3. The D365 ERP MCP and MS Learn MCP are configured

Two MCP servers are needed for this exercise:

- **D365 ERP MCP** - enables Copilot to read and write Dynamics 365 configuration data directly. Required for Phase 2.
  Setup guide: [Connect to the Dynamics 365 ERP MCP server by using Visual Studio Code](https://learn.microsoft.com/en-us/dynamics365/fin-ops-core/dev-itpro/copilot/mcp-server-vscode)

- **MS Learn MCP** - enables Copilot to look up D365 configuration steps from Microsoft Learn during runbook generation. Required for Phase 1.
  Setup guide: [Microsoft Learn MCP Server overview](https://learn.microsoft.com/en-us/microsoftlearn-mcp/overview)

To verify both are configured: open VS Code, go to Copilot Chat (agent mode), and check the tool picker for both servers. If either is missing, follow its setup guide above or ask your facilitator.

### 4. You have a compatible D365 environment

You need a Dynamics 365 environment where you can create a new legal entity (`zav1`) and configure Warehouse Management freely.

**Environment requirements:**

- **Tier 2 (Standard Acceptance Testing)** or **UDE (Unified Development Environment)** - both are connected to Dataverse and will work.
- A **Tier 1 (cloud-hosted or developer VM)** or **CHE (Cloud-Hosted Environment)** is **not sufficient** - these are not connected to Dataverse and the ERP MCP will not function correctly.

### 5. The Copilot instructions and skill files are in your workspace

Two files must be present in your VS Code workspace before the exercise starts. They configure Copilot's behaviour and enable the warehouse management skill.

Download them from the [implementation-ip/](implementation-ip/) folder in this exercise and place them as follows in your workspace root:

| File in this repo | Place it at in your workspace |
|---|---|
| `implementation-ip/copilot-instructions.md` | `.github/copilot-instructions.md` |
| `implementation-ip/skills/warehouse-management-only-mode-configuration/skill.md` | `.github/skills/warehouse-management-only-mode-configuration/skill.md` |

To verify: open VS Code in your workspace folder and confirm both files exist at the paths above. If the `.github/` folder does not exist yet, create it.

> **About the WHS skill:** The warehouse management skill provided here is a sample for this exercise. It covers WHS-Only mode configuration for Dynamics 365 Supply Chain Management. If you want to build skill files for other F&O modules — Accounts Payable, Fixed Assets, Project Management and Accounting, and others — use the [ERP Skill Builder](erp-skillbuilder.md). It provides a prompt that generates a complete skill file for any module using the Business Process Catalog and the MS Learn MCP server as knowledge sources.

### 6. Python is installed and the library is available

Python is required when working with Excel files (BPC reference data). Verify with:

```bash
python --version
```

If Python is not installed, download it from [python.org](https://www.python.org/downloads/). Or ask GitHub Copilot to set it up for you.

---

## What if a check fails?

| Check failed | Action |
|---|---|
| No Copilot seat | Sign up for a 30-day Pro trial at [github.com/copilot](https://github.com/copilot), or check D365 Premium / M365 Copilot licensing |
| No qualifying D365 environment | Ask your facilitator - a shared Tier 2 environment is provided for workshop attendees |
| D365 ERP MCP not configured | Follow the [ERP MCP setup guide](https://learn.microsoft.com/en-us/dynamics365/fin-ops-core/dev-itpro/copilot/mcp-server-vscode) or ask your facilitator |
| MS Learn MCP not configured | Follow the [MS Learn MCP setup guide](https://learn.microsoft.com/en-us/microsoftlearn-mcp/overview) or ask your facilitator |
| Copilot instructions or skill files missing | Download from the `implementation-ip/` folder in this repo and place them at the paths shown in check 5 |
| Python not installed | Download from [python.org](https://www.python.org/downloads/) |

---

## Running costs

- **LLM cost** - covered by your GitHub Copilot subscription. See [Plans for GitHub Copilot](https://docs.github.com/en/copilot/about-github-copilot/plans-for-github-copilot).
- **MCP server execution cost** - billed at **0.1 Copilot Credits per tool call**, *unless*:
  1. The user has a **D365 Finance or SCM Premium license** assigned.
  2. The MCP server is called from **Copilot Studio** - cost is then included in the Copilot Studio *Agent Action* cost.

**Official documentation:** [MCP Server Licensing](https://learn.microsoft.com/en-us/dynamics365/fin-ops-core/dev-itpro/copilot/mcp-server-licensing), [Copilot Studio licensing](https://learn.microsoft.com/en-us/microsoft-copilot-studio/requirements-licensing-subscriptions), [Copilot Studio Billing rates and management](https://learn.microsoft.com/en-us/microsoft-copilot-studio/requirements-messages-management)

---

## On the day

Bring the machine you ran the checks on. Know your GitHub credentials and your D365 environment URL.

Phase 1 (runbook creation) works entirely from the attached documents - no live D365 access needed. Phase 2 requires live access to your D365 F&O environment.

See you in the room.
