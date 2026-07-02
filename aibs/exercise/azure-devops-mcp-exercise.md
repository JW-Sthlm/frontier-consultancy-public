# AIBS Frontier Consultancy - Hands-on exercise for the Azure DevOps MCP

**You have GitHub Copilot, VS Code, and an Azure DevOps project. Let's see how fast you can stand up and manage a delivery backlog - planning, triaging, and writing work items - straight from natural-language prompts in VS Code.**

This exercise shows how to connect the **remote Azure DevOps MCP server** to GitHub Copilot in Visual Studio Code and use it to drive real delivery work: creating user stories, setting priorities, and querying the board.

---

## Why this MCP matters for Frontier Consultancy

Delivery teams live in Azure DevOps - the backlog, the board, the sprint, the pull requests. But the day-to-day admin around it (writing well-formed user stories, keeping acceptance criteria consistent, triaging priorities, linking work to commits and PRs) is slow, manual, and easy to skip under deadline pressure.

The Azure DevOps MCP server closes that gap. It brings the **full Azure DevOps surface - work items, boards, repos, pipelines, wikis, and test plans - directly into the agent** your consultants already use to write code and configure Dynamics. That means a consultant can:

- **Turn a workshop conversation into a backlog** in minutes - well-structured user stories with consistent acceptance criteria, instead of a half-filled board after the session.
- **Triage and plan at the speed of thought** - "find the security-related bugs and assign them to the current sprint" is one prompt, not an afternoon of clicking.
- **Keep delivery artifacts connected** - link work items to the branches, commits, and pull requests that implement them, so traceability is automatic rather than aspirational.
- **Stay in one place** - the same VS Code agent that authors the Dynamics model and the code also runs the delivery process. No context switching, no copy-paste between tools.

For an SI delivery team, this is the difference between AI helping you *write code* and AI helping you *run the engagement*. It is the AI-first delivery motion applied to project management itself.

---

## Azure DevOps setup - before the workshop

Allow about 10 minutes on your own machine before the session. If all four checks pass, you walk in and start working.

The **remote** Azure DevOps MCP server is the recommended option: nothing to install, hosted by Azure DevOps, authenticated with your Microsoft Entra account. (A local `npx`-based server also exists if you need a local `stdio` setup - see the [GitHub repo](https://github.com/microsoft/azure-devops-mcp) - but for this exercise use the remote server.)

### What you need

- **VS Code** with the GitHub Copilot Chat extension (agent mode required)
- A **GitHub Copilot** seat (Pro or Business)
- The **remote Azure DevOps MCP server** configured in VS Code
- An **Azure DevOps organization connected to Microsoft Entra ID**, plus a **test project** you can write to

---

### The four checks

#### 1. You have a GitHub Copilot seat with agent mode

Open [github.com/settings/copilot](https://github.com/settings/copilot) and confirm *Copilot Pro* or *Copilot Business* shows as **Active**. No seat? Sign up for a 30-day free Pro trial at [github.com/copilot](https://github.com/copilot).

> **Model selection:** use an Anthropic model (Sonnet or Opus) - these currently have the best MCP tool-calling capability.

#### 2. VS Code is installed with GitHub Copilot Chat

Open VS Code. In the Copilot Chat sidebar, look for the agent mode toggle (the model picker dropdown). If you do not see it, update VS Code to the latest version.

#### 3. You have an Azure DevOps organization and a test project

You need an Azure DevOps organization **connected to Microsoft Entra ID** and membership in a project you can write to. Don't have one? Create a free org at [dev.azure.com](https://dev.azure.com) and add a test project. Note the **organization name** (the part after `dev.azure.com/`, for example `contoso`) - you'll need it for the configuration below.

#### 4. The remote Azure DevOps MCP is configured and starts

Follow the configuration steps below, then confirm `ado-remote-mcp` shows as **Running** in **MCP: List Servers** and its tools appear in the agent's tool picker.

---

### Configure the remote MCP server

1. Open (or create) your VS Code MCP configuration. To make the server available across **all** workspaces, use the global user file - open File Explorer at user level and enter:

   ```
   %APPDATA%\Code\User\mcp.json
   ```

   (For a single project instead, create `.vscode/mcp.json` in the project root.)

2. Add the remote server, replacing `{organization}` with your Azure DevOps organization name (for example `contoso`):

   ```json
   {
     "servers": {
       "ado-remote-mcp": {
         "type": "http",
         "url": "https://mcp.dev.azure.com/{organization}"
       }
     },
     "inputs": []
   }
   ```

3. Save the file. In VS Code, open **MCP: List Servers** from the Command Palette, select **ado-remote-mcp**, and **Start** it.

4. The first time a tool runs, a browser opens to **authenticate with your Microsoft Entra account**. Sign in with the account that has access to your organization.

5. After authentication, the Azure DevOps tools appear in the agent's tool list. You're ready.

> **Tip - scope the toolset.** Azure DevOps exposes a large surface. You can restrict what loads by adding headers. For a backlog-focused session, limit to work-item and core tools, and optionally make the server read-only while exploring:
>
> ```json
> {
>   "servers": {
>     "ado-remote-mcp": {
>       "type": "http",
>       "url": "https://mcp.dev.azure.com/{organization}",
>       "headers": {
>         "X-MCP-Toolsets": "wit,work"
>       }
>     }
>   },
>   "inputs": []
> }
> ```
>
> Available toolsets: `repos`, `wit` (work items), `pipelines`, `wiki`, `work` (iterations/capacity), `testplan`. Add `"X-MCP-Readonly": "true"` to prevent any changes.

### What if a check fails?

| Check failed | Action |
|---|---|
| No Copilot seat | Sign up for a 30-day Pro trial at [github.com/copilot](https://github.com/copilot) |
| No agent mode toggle in VS Code | Update VS Code to the latest version and confirm the GitHub Copilot Chat extension is enabled |
| No Azure DevOps org / project | Create a free org and test project at [dev.azure.com](https://dev.azure.com); confirm it is connected to Microsoft Entra ID |
| Server won't start or no tools appear | Re-check the `url` format (`https://mcp.dev.azure.com/{organization}`), restart the server from **MCP: List Servers**, and start a fresh chat session |
| Authentication fails | Sign in with the Microsoft Entra account that has access to the organization |

---

## What tools you get

The remote server groups its tools into **toolsets**. The most relevant for delivery work:

### Core (always available)

| Tool | What it does |
|---|---|
| `core_list_orgs` | List Azure DevOps organizations you can access |
| `core_list_projects` | List projects in an organization |
| `core_list_project_teams` | List teams in a project |

### Work items (`wit`)

| Tool | What it does |
|---|---|
| `wit_work_item` (get / get_batch / my / list_comments / list_revisions / list_for_iteration / get_type) | Read work items and their details |
| `wit_query` (get / get_results) | Run saved queries |
| `wit_backlog` (list / list_work_items) | List backlog levels and their items |
| `search_workitem` | Full-text work item search |
| `wit_work_item_write` (create / update / update_batch / add_child) | Create and update work items |
| `wit_work_item_comment_write` (add / update) | Add and edit comments |
| `wit_work_item_link_write` (link / unlink / link_to_pull_request / add_artifact_link) | Link work items to each other, to PRs, branches, commits, and builds |
| `wit_work_item_attachment` | Download a work item attachment |

### Work / boards (`work`)

| Tool | What it does |
|---|---|
| `work` (list_iterations / list_team_iterations / get_team_settings / get_team_capacity / get_iteration_capacities) | Read iterations, team settings, and capacity |
| `work_iteration_write` / `work_capacity_write` | Create and assign iterations; update capacity |

### Repos (`repos`)

| Tool | What it does |
|---|---|
| `repo_repository` / `repo_branch` / `repo_file` | Read repositories, branches, and file content |
| `repo_pull_request` (get / list / list_by_commits) | Read pull requests |
| `repo_pull_request_thread` | Read PR comment threads |
| `repo_search_commits` / `search_code` | Search commits and code |
| `repo_pull_request_write` / `repo_pull_request_thread_write` / `repo_create_branch` | Create and update PRs, comment threads, and branches |

### Pipelines, wiki, test plans

| Toolset | Highlights |
|---|---|
| `pipelines` | List/run builds and definitions, read logs, manage artifacts (`pipelines_build`, `pipelines_run`, `pipelines_build_log`, `pipelines_write`) |
| `wiki` | List wikis and pages, read and upsert page content (`wiki`, `search_wiki`, `wiki_upsert_page`) |
| `testplan` | List and create test plans, suites, and cases (`testplan`, `testplan_test_case_write`) |

> The full, current list is in the [Available tools](https://learn.microsoft.com/en-us/azure/devops/mcp-server/remote-mcp-server?view=azure-devops#available-tools) documentation. Tools marked write (create/update) respect the `X-MCP-Readonly` header.

---

## The exercise

The scenario: you are kicking off a **Dynamics 365 Field Service** project for a coffee-roaster company and need to stand up the initial backlog. With the MCP connected, open a new GitHub Copilot Chat session (agent mode) and run the prompts below in order.

> **Model selection:** use an Anthropic model (Sonnet or Opus) - these currently have the best MCP tool-calling capability.

### Prompt 1 - Verify the connection

```
List the projects in my Azure DevOps organization, then show me my assigned work items for the test project.
```

You should see your org's projects and (likely empty) work item list returned from live Azure DevOps. That confirms auth and tools are working.

### Prompt 2 - Generate a backlog

```
Create 10 user stories in the <Your Project> project for a D365 Field Service solution for a coffee
roaster company. Cover preventive maintenance scheduling, technician mobile access, roaster asset and
component tracking, spare parts on service trucks, emergency breakdown booking, skill-based technician
assignment, IoT temperature alerts, service agreements and entitlements, on-site inspection checklists,
and a post-service customer report and invoice. For each story, write a proper "As a / I want / so that"
narrative and 3 acceptance criteria in the description using Markdown. Tag each with "Field Service" and
"Coffee Roaster".
```

> **Note on work item types:** if your project uses the **Basic** process, the requirement-level type is **Issue**, not **User Story** (and there is no Acceptance Criteria field). Tell Copilot to use **Issue** and put the acceptance criteria in the description. If your project uses **Agile**, **Scrum**, or **CMMI**, it will have **User Story** / **Product Backlog Item** with a dedicated Acceptance Criteria field. Let Copilot check the backlog levels first if unsure: *"list the backlog levels for the <team> team and tell me what requirement work item type this project uses."*

### Prompt 3 - Triage and prioritise

```
Review the 10 work items you just created. Set Priority 1 on the foundational stories (asset tracking,
mobile access, emergency booking), Priority 2 on the core operations stories, and Priority 3 on the
advanced/value-add stories (IoT, inspection checklist, report & invoice). Use a batch update.
```

### Prompt 4 - Query the result

```
Show me all the work items in the backlog grouped by priority, with their IDs and titles, so I can
confirm the triage.
```

---

## What good looks like

- **After Prompt 1** you get live data back from your Azure DevOps organization - proof the remote MCP and Entra auth are working.
- **After Prompt 2** the project backlog has 10 well-formed work items, each with an "As a / I want / so that" narrative, three acceptance criteria, and the two tags.
- **After Prompt 3** the items carry a sensible priority spread (P1 foundation, P2 core, P3 advanced), applied in a single batch update.
- **After Prompt 4** Copilot reads the board back to you grouped by priority - the same triage, now queried live from Azure DevOps.

---

## Going further (optional)

- **Connect work to code:** *"Link work item 1234 to pull request 56 in the <repo> repository."*
- **Plan a sprint:** *"List the iterations for the <team> team, then assign the three Priority 1 stories to the current iteration."*
- **Document it:** *"Create a wiki page '/Field Service/Backlog Overview' summarising the 10 stories and their priorities."*

---

## If something goes wrong - in this order

1. **Server not found / no tools:** confirm `ado-remote-mcp` shows as **Running** in **MCP: List Servers** and that its tools are enabled in the agent's tool picker. Newly started servers sometimes only attach to a **new** chat session - start a fresh chat.
2. **Authentication fails:** verify you signed in with the Microsoft Entra account that has access to the organization, and that the org is connected to Entra ID. Check the URL format: `https://mcp.dev.azure.com/{organization}`.
3. **Wrong work item type (e.g. "User Story does not exist"):** your project uses a different process. Ask Copilot to list backlog levels and use the correct requirement type (often **Issue** on the Basic process).
4. **Ask Copilot itself.** Paste the error. Ask *"what does this mean, and how do I fix it?"* Using Copilot to unstick itself is the muscle you are training today.
5. **Ask a neighbour or the facilitator.**

---

## Take this home

The pattern you used today is reusable across any engagement. Connect the Azure DevOps MCP once, then run the delivery process - backlog creation, triage, sprint planning, traceability, documentation - from natural-language prompts in the same VS Code agent that writes your code and configures Dynamics. The clearer your instructions, the faster and more auditable the result. This is what AI-first delivery looks like applied to project management itself.

---

### Reference

- [Set up the remote Azure DevOps MCP Server (Microsoft Learn)](https://learn.microsoft.com/en-us/azure/devops/mcp-server/remote-mcp-server?view=azure-devops)
- [Azure DevOps MCP Server GitHub repository](https://github.com/microsoft/azure-devops-mcp)
- [Available tools](https://learn.microsoft.com/en-us/azure/devops/mcp-server/remote-mcp-server?view=azure-devops#available-tools)
