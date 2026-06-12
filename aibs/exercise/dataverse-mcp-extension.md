# AIBS Frontier Consultancy - Hands-on exercise: Extending the Dataverse MCP

**The Dataverse MCP is great at reading and writing data. But what if you want Copilot to author the *model* too - tables, fields, choices, forms - without leaving VS Code? In this exercise you build a custom MCP server that does exactly that, then point Copilot at it to configure a Dynamics 365 Customer Engagement environment for a coffee-roaster scenario.**

This is the "build the tool, then use the tool" exercise. You extend the Microsoft Dataverse MCP experience with your own schema-authoring MCP server, register it in VS Code, and let GitHub Copilot drive it.

---

> **Before the workshop:** you will need a GitHub Copilot seat, VS Code with agent mode, the **.NET 8.0 SDK**, and a Dynamics 365 Customer Engagement environment you can connect to (the same one used in the [CE exercise](ce-readme.md)). Complete the [CE exercise](ce-readme.md) first if you have not - it gets the environment and Dataverse MCP basics in place.

## Set up the prerequisites

1. Install the **.NET 8.0 SDK** if you do not have it:

   ```
   winget install Microsoft.DotNet.SDK.8
   ```

2. Open VS Code with **GitHub Copilot Chat** enabled in agent mode.

3. Have your Dynamics 365 CE environment URL ready, for example `https://yourorg.crm.dynamics.com`.

> **Model selection:** use an Anthropic model (Sonnet or Opus) - these currently have the best MCP tool-calling capability.

---

## The scenario

You are a consultant on a Dynamics 365 Customer Engagement engagement for a fictional **coffee roaster**. The out-of-the-box Dataverse MCP can generate demo data, but your customer also wants rapid **model changes** - new fields and form layout tweaks - driven straight from natural language.

Rather than clicking through the maker portal, you will build a small **MCP server** that exposes schema-authoring tools (create fields, choices, forms, tabs, sections, place fields, publish), register it in VS Code, and then ask Copilot to use it to add a **Coffee Purchasing Profile** field to the account form.

You will do it in three phases.

---

## What you will do

### Phase 1 - Scaffold the MCP server

Open a new GitHub Copilot Chat session (agent mode) in an empty folder and enter **Prompt 1**. Copilot will scaffold a .NET 8 console project that uses the **ModelContextProtocol** SDK and the **Microsoft.PowerPlatform.Dataverse.Client**, wired up to talk over stdio.

> **The project is an approval artefact.** Review the scaffolded structure before you build - you want a clean separation between the connection service and the individual tools.

### Phase 2 - Add the schema-authoring tools

Enter **Prompt 2**. Copilot will add MCP tools for creating fields and choices, and for working with forms - listing forms, reading FormXML, adding tabs and sections, and placing a field directly below an existing one - plus a publish tool. Build the project so the server is ready to run.

### Phase 3 - Register and use it

Register the server in VS Code (`.vscode/mcp.json`), start it, then enter **Prompt 3** to configure the coffee-roaster account model with your new tools.

---

## Prompts

### Prompt 1 - Scaffold the server

```
Create a new C# / .NET 8 MCP server called DataverseSchemaMcp that connects to a Dynamics 365
Customer Engagement (Dataverse) environment. Use the ModelContextProtocol SDK over stdio and the
Microsoft.PowerPlatform.Dataverse.Client ServiceClient. Read the connection string from a
DATAVERSE_CONNECTION_STRING environment variable and expose the connection through a single shared
provider service. Keep tools in separate files from the connection service. Build it and confirm the
server starts.
```

### Prompt 2 - Add fields, choices, and form tools

```
Extend the MCP server with tools to author the D365 CE model, similar to a development MCP:

- create_field: create columns (string, memo, integer, decimal, money, boolean, datetime)
- create_option_set_field: create a local choice (drop-down) column from a list of options
- list_forms / get_form_xml: discover a table's main forms and inspect their FormXML
- create_form / add_tab_to_form / add_section_to_form: build form structure
- add_field_to_form: place an existing field into a section, with an option to insert it directly
  below a named existing field
- publish_customizations: publish a single table or all customizations

Publish changes automatically by default. Build the project and fix any compile errors.
```

### Prompt 3 - Configure the account model

```
Using the DataverseSchemaMcp server, add a new drop-down field on the account table called
"Coffee Purchasing Profile" with the following options:

- Commercial / Bulk Coffee
- Classic / Everyday Coffee
- Premium Coffee
- Specialty Coffee
- Sustainable / Ethical Coffee

Then add the field to the account form on the "Details" tab in the "Company Profile" section,
directly below "Ownership", and publish.
```

---

## Registering the server in VS Code

Add the built server to your VS Code MCP configuration so Copilot can call it. You can register it in **one** of two scopes:

- **Workspace** (`.vscode/mcp.json` in the project) - only available when this workspace is open, and travels with the project. Use `${workspaceFolder}` in the path.
- **Global / user** (your VS Code user `mcp.json`) - available in **every** workspace on your machine. Use an **absolute** path to the DLL, because `${workspaceFolder}` does not resolve outside the project.

For this exercise we register it **globally** so it is available everywhere. Open the Command Palette (`Ctrl+Shift+P`) and run **MCP: Open User Configuration**, then add the `dataverse-schema` entry:

```json
{
  "servers": {
    "dataverse-schema": {
      "type": "stdio",
      "command": "dotnet",
      "args": ["c:/Projects/DataverseSchemaMcp/bin/Debug/net8.0/DataverseSchemaMcp.dll"],
      "env": {
        "DATAVERSE_CONNECTION_STRING": "${input:dataverseConnectionString}"
      }
    }
  },
  "inputs": [
    {
      "id": "dataverseConnectionString",
      "type": "promptString",
      "description": "Dataverse connection string",
      "password": true
    }
  ]
}
```

> If you keep a workspace `.vscode/mcp.json` as well, give it a different server name to avoid a duplicate entry. Adjust the absolute path to match where you built the project.

A working interactive connection string looks like:

```
AuthType=OAuth;Url=https://yourorg.crm.dynamics.com;AppId=51f81489-12ee-4a9e-aaae-a2591f45987d;RedirectUri=http://localhost;LoginPrompt=Auto
```

> The redirect URI must be a loopback address (`http://localhost`). Start the server from the MCP view, sign in when the browser opens, and Copilot can now call your tools.

### Verify the server is listed

Before running Prompt 3, confirm VS Code discovered the server:

1. Open the **global search** bar at the top of the VS Code window and type `>` to switch it into command mode.
2. Run **MCP: List Servers** (or open the Chat view and pick the MCP server selector).
3. You should see **dataverse-schema** in the list, with a scope label - **Global in Code** when registered in the user config, or the workspace `mcp.json` path when registered per-workspace.
4. Select it and choose **Start**. The status should change from *Stopped* to *Running* (you will be prompted for the connection string on first start).

If it does not appear, reload the window (**Developer: Reload Window**) and make sure MCP discovery is enabled (`"chat.mcp.discovery.enabled": true`).

---

## What good looks like

- **After Phase 1** you have a building .NET 8 MCP server that starts cleanly and exposes its tool list over stdio.
- **After Phase 2** the server exposes field, choice, form, and publish tools, and the project compiles with no errors.
- **After registering**, typing `>` in the global search and running **MCP: List Servers** shows **dataverse-schema** (scope **Global in Code**), and you can start it to *Running*.
- **After Phase 3** the account table has a new **Coffee Purchasing Profile** choice field with the five options, placed on the account form under **Details -> Company Profile**, **directly below Ownership**, and the customization is published - visible in the Customer Service Hub.

---

## If something goes wrong - in this order

1. **Ask Copilot itself.** Paste the error. Ask *"what does this mean, and how do I fix it?"* Using Copilot to unstick itself is the muscle you are training today.
2. **Use your Dataverse knowledge.** Common snags: the redirect URI must be `http://localhost`; new columns need a publisher prefix (for example `new_`); the field must exist and be published before it can be placed on a form; the section name in FormXML may differ from its display label.
3. **Ask a neighbour or the facilitator.**

---

## Reference - how the server is built

> This section documents the reference implementation so you can compare your result, or build straight from it. The clearer you understand the structure, the easier it is to extend.

### Did we extend the standard Dataverse MCP?

**No.** The Microsoft Dataverse MCP servers (the hosted `…/api/mcp` endpoints and the Microsoft-shipped development MCP binary) are closed products - you cannot add tools to them. `dataverse-schema` is a **separate, standalone MCP server written from scratch** in C# / .NET 8. It *mirrors* the schema-authoring experience of a development MCP, but it is entirely your own code, running as a local stdio process that talks to your environment directly.

### Technology

- **[ModelContextProtocol](https://www.nuget.org/packages/ModelContextProtocol) SDK** - hosts the MCP server over **stdio** and auto-discovers tools from the assembly.
- **[Microsoft.PowerPlatform.Dataverse.Client](https://www.nuget.org/packages/Microsoft.PowerPlatform.Dataverse.Client)** - the `ServiceClient` used to connect to the environment.
- **Xrm SDK metadata messages** - `CreateAttributeRequest`, `CreateEntityRequest`, `CreateOneToManyRequest`, `CreateManyToManyRequest`, `PublishXmlRequest`, and friends - plus direct **FormXML** manipulation for form changes.
- **Microsoft.Extensions.Hosting** - generic host and dependency injection.

Authentication is via a single `DATAVERSE_CONNECTION_STRING` environment variable. Schema changes are **published automatically** by default.

### Project structure

```
DataverseSchemaMcp/
├─ Program.cs                     # Host + DI; registers the MCP stdio server, auto-discovers tools
├─ DataverseSchemaMcp.csproj      # ModelContextProtocol + Dataverse.Client + Hosting packages
├─ Services/
│  ├─ DataverseClientProvider.cs  # Lazy, shared ServiceClient from DATAVERSE_CONNECTION_STRING
│  ├─ SchemaHelpers.cs            # Label, required-level, and logical-name helpers
│  ├─ PublishHelper.cs            # PublishXml / PublishAllXml requests
│  └─ FormHelper.cs               # FormXML read/build/save + control classid mapping
└─ Tools/                         # One [McpServerToolType] class per domain
   ├─ TableTools.cs
   ├─ FieldTools.cs
   ├─ OptionSetTools.cs
   ├─ RelationshipTools.cs
   ├─ FormTools.cs
   └─ PublishTools.cs
```

**How a tool is wired:** each public method is annotated with `[McpServerTool(Name = "…")]` and a `[Description]`; parameters carry `[Description]` attributes so Copilot knows how to call them. `Program.cs` registers the MCP server with `.WithStdioServerTransport().WithToolsFromAssembly()`, and the shared `DataverseClientProvider` is injected into every tool. Logging goes to **stderr** so it never corrupts the JSON-RPC stream on stdout.

### All tools

The server exposes **19 tools** across six domains.

**Tables**
| Tool | Purpose |
| --- | --- |
| `create_table` | Create an entity with its primary name column (ownership, activities, notes) |
| `delete_table` | Delete a table and its data |

**Fields (columns)**
| Tool | Purpose |
| --- | --- |
| `create_field` | Create a column: String, Memo, Integer, BigInt, Decimal, Double, Money, Boolean, DateTime |
| `update_field` | Update display name, description, or required level |
| `delete_field` | Delete a column |

**Choices (option sets)**
| Tool | Purpose |
| --- | --- |
| `create_option_set_field` | Create a local choice (drop-down) column with inline options |
| `create_global_option_set` | Create a reusable global choice |
| `create_field_with_existing_global_option_set` | Create a choice column bound to an existing global choice |
| `add_option_to_global_option_set` | Add an option to an existing global choice |

**Relationships**
| Tool | Purpose |
| --- | --- |
| `create_lookup_field` | Create a lookup column via a 1:N relationship (configurable delete behavior) |
| `create_many_to_many_relationship` | Create an N:N relationship with an auto intersect entity |
| `delete_relationship` | Delete a relationship by schema name |

**Forms**
| Tool | Purpose |
| --- | --- |
| `list_forms` | List a table's main forms with their ids |
| `get_form_xml` | Return raw FormXML for inspection |
| `create_form` | Create a new main form (tab + section) |
| `add_tab_to_form` | Add a tab (with a section) |
| `add_section_to_form` | Add a section to a tab |
| `add_field_to_form` | Place a field in a section - supports inserting directly below an existing field (`afterFieldLogicalName`) |

**Publishing**
| Tool | Purpose |
| --- | --- |
| `publish_customizations` | Publish a single table, or all customizations |

### Extending it further

The same pattern scales: add a new method with `[McpServerTool]` in a `Tools/` class, inject `DataverseClientProvider`, call the relevant SDK request, and rebuild. Natural next steps are security roles, business rules, status/state columns, calculated/rollup fields, or app-module placement.

---

## Take this home

You just turned a natural-language request into a working MCP server *and* used it to configure a live D365 environment. The same pattern extends to any platform capability: define a tool, expose it over MCP, and let Copilot orchestrate it. Add lookups and relationships, table creation, security roles, business rules - the server grows with your needs. The clearer your tool descriptions, the better Copilot uses them. This is what AI-first delivery looks like when you build your own tooling.
