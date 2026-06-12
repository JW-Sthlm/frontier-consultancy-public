# ERP Skill Builder

Skill files are a core part of AI-first delivery on Dynamics 365 F&O. A skill file is a structured, self-contained document that tells your AI assistant exactly how to configure a specific module: which parameters to set, which menu paths to use, which number sequences and batch jobs to configure, and which business processes are covered.

You can write skill files manually — but you don't have to. The prompt below generates a complete `skill.md` for any F&O module using two knowledge sources:

- **The Business Process Catalog (BPC)** — Microsoft's structured catalog of end-to-end Dynamics 365 business processes, organized by area and process group.
- **The MS Learn MCP server** (`microsoft_docs_search` / `microsoft_docs_fetch`) — live access to Microsoft's official Dynamics 365 documentation, including setup guides, configuration parameters, and module overviews.

Together, these sources enable an AI agent to produce a skill file that covers configuration steps, menu paths, BPC process mapping, a recommended configuration sequence, and a delivery workshop plan — without manual research.

---

## How to use this prompt

1. Open GitHub Copilot (or another MCP-capable agent) in agent mode.
2. Make sure the [MS Learn MCP server](https://github.com/microsoftdocs/mcp) is connected.
3. Replace `[MODULE NAME]` in the prompt below with the module you want to build a skill for — for example:
   - Accounts Payable
   - Fixed Assets
   - Project Management and Accounting
   - Transportation Management
4. Run the prompt. The agent will research the BPC and MS Learn, then write the skill file.

> **Output location:** The prompt instructs the agent to save the result to `.github/skills/[module name]-configuration/skill.md`. Adjust the path if your repo uses a different skills folder convention.

> **Granularity:** You don't have to generate a skill file for an entire module at once. Tailor the scope to the pace of your implementation — one setup area, one workstream, or one BPC process group at a time. Smaller skill files require more coordination between files, but they are quicker to generate and execute, carry less token overhead, and are less prone to error. A good rule of thumb: scope each skill file to what a consultant can realistically configure in a single session.

---

## Skill builder prompt

Replace `[MODULE NAME]` before running.

```
You are a Microsoft Dynamics 365 implementation expert. Your task is to create a skill.md file for implementing the **[MODULE NAME]** module in Dynamics 365 [Finance / Supply Chain Management / Commerce / etc.].

Follow this exact process:

## Step 1 — Research the Business Process Catalog

Use the `microsoft_docs_search` MCP tool to find the Business Process Catalog (BPC) entries for this module. Search for:
- "[Module name] business process catalog Dynamics 365"
- "BPC [area code] [module name] end-to-end processes"

Then use `microsoft_docs_fetch` to retrieve full content from any high-value BPC pages. 

Identify:
- The BPC area number (e.g., 60 = Inventory and Warehouse, 20 = Finance, etc.)
- All end-to-end business process groups (e.g., 60.10, 60.20)
- All level-3 process steps within each group (e.g., 60.10.010, 60.10.020)

## Step 2 — Research Configuration Steps on MS Learn

Use `microsoft_docs_search` to find all setup/configuration pages for this module. Search for:
- "Dynamics 365 [module name] setup configuration"
- "Dynamics 365 [module name] parameters"
- "Dynamics 365 [module name] module get started"

For each major setup area found, use `microsoft_docs_fetch` to get the full configuration details including:
- Configuration item names
- Exact menu paths (e.g., "Module > Setup > Area > Item")
- Type (Parameters / List of values / Number sequences / Wizard / Batch job)

## Step 3 — Write the skill.md

Produce a skill.md file with this exact structure and frontmatter:

---
name: [module name]-configuration
description: Complete configuration steps for Dynamics 365 [Module Name]

---

# [Module Name] — Configuration Steps

> **Source**: Business Process Catalog (BPC) Reference — [current version]  
> **Scope**: Dynamics 365 [app name] — [Module Name] module  

---

## Overview

[2-3 paragraph overview of what the module does, its key purpose, and any important modes or deployment variants]

---

## Table of Contents

[Numbered list of all setup areas]

---

## [Numbered setup sections]

For each setup area, provide a markdown table:

| # | Configuration Item | Menu Path | Type |
|---|---|---|---|
| N.M | **Item Name** | Module > Setup > Area > Item | Type |

Include context notes (blockquotes) where important dependencies, sequencing requirements, or integration points exist.

---

## [N]. Business Processes Covered

Map each BPC process group and its level-3 steps to a table:

| Seq | Process | Description |
|---|---|---|
| XX.YY.ZZZ | Process name | What this process achieves |

---

## Recommended Configuration Sequence

Ordered numbered list of setup steps from foundational to advanced. Prioritize dependencies.

---

## Delivery Plan Workshops (Success by Design)

| Workshop | Description |
|---|---|
| **XX.NN — Workshop title** | What is covered |

---

## Output requirements

- Use the exact table format shown above (pipe tables, bold item names, numbered IDs)
- Every configuration item must include its full menu path
- Do not omit periodic tasks, batch jobs, number sequences, or clean-up jobs
- Do not hallucinate menu paths — only include items you found in MS Learn documentation
- If MS Learn does not cover a setup area, note it as "See MS Learn for current menu path"
- The skill.md must be self-contained — a consultant should be able to use it without internet access
- Save the output to: .github/skills/[module name]-configuration/skill.md
```

---

## What a skill file is used for

Once generated, a skill file can be:

- **Loaded into GitHub Copilot** via `.github/copilot-instructions.md` as background knowledge for configuration tasks
- **Used directly** as a reference during workshops and configuration sessions
- **Extended** with client-specific decisions, customisations, and ISV notes
- **Versioned** in your project repo so the whole team works from the same baseline

The skill file is the AI's configuration knowledge for that module. Maintaining and extending it is the core of the consultant's work in an AI-first delivery.
