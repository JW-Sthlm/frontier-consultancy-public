# AIBS Frontier Consultancy - Hands-on exercise for CE (Customer Engagement)

**You have a Dynamics 365 Customer Engagement environment, GitHub Copilot, and the Dataverse MCP. Let's see how fast you can stand up realistic demo data and configure the model - straight from VS Code.**

This exercise shows how to use the **Dataverse MCP within Visual Studio Code** to bring your Dataverse configuration and demos to the next level.

---

## Before you start - set up the Dataverse MCP

You have two ways to connect the Dataverse MCP server. Pick the **fastest setup** if you just want to get going; use the **alternative setup** when you want full control or are adding an individual MCP server.

### Fastest setup

First, enable the Dataverse MCP Server for GitHub in Power Platform, then follow the Microsoft Learn guides:

- [Connect Dataverse MCP with GitHub Copilot in Visual Studio Code and Copilot CLI](https://learn.microsoft.com/en-us/power-apps/maker/data-platform/data-platform-mcp-vscode)
- [Configure the Dataverse model context protocol (MCP) server](https://learn.microsoft.com/en-us/power-apps/maker/data-platform/data-platform-mcp-disable)

### Alternative setup

1. Download and install [Visual Studio Code](https://code.visualstudio.com/).
2. Log in with your GitHub account.
3. Enable **GitHub Copilot Chat** under **Extensions**.
4. If you don't have GitHub Copilot yet, go to [GitHub Copilot at Microsoft](https://copilot.github.microsoft.com/) and follow the steps. Microsoft employees get GitHub Copilot and advanced LLMs for free.
5. Install the **.NET 8.0 SDK** from the command prompt:

   ```
   winget install Microsoft.DotNet.SDK.8
   ```

6. Run the .NET tool to install the Dataverse MCP:

   ```
   dotnet tool install --global --add-source https://api.nuget.org/v3/index.json Microsoft.PowerPlatform.Dataverse.MCP
   ```

7. Configure MCP in VS Code. Open (or create) your VS Code MCP configuration file. The location depends on your setup - open File Explorer at user level and enter:

   ```
   %APPDATA%\Code\User\mcp.json
   ```

8. Add **one** of the following configurations.

   **Full configuration** - fill in the highlighted values from your own Dataverse environment:

   ```json
   {
     "servers": {
       "DataverseMCP": {
         "type": "stdio",
         "command": "Microsoft.PowerPlatform.Dataverse.MCP",
         "args": [
           "--ConnectionUrl",
           "https://make.powerapps.com/environments/<Environment ID>/connections?apiName=shared_commondataserviceforapps&connectionName=<Your Dataverse Connection ID>",
           "--MCPServerName",
           "DataverseMCPServer",
           "--TenantId",
           "<Your Tenant ID>",
           "--EnableHttpLogging",
           "true",
           "--EnableMsalLogging",
           "false",
           "--Debug",
           "false",
           "--BackendProtocol",
           "HTTP"
         ]
       }
     }
   }
   ```

   **Minimal configuration:**

   ```json
   {
     "servers": {
       "dataverse": {
         "type": "stdio",
         "command": "Microsoft.PowerPlatform.Dataverse.MCP",
         "args": []
       }
     }
   }
   ```

#### Fill in your environment values

Fill out the highlighted values with information from your own Dataverse environment. Go to [make.powerapps.com](https://make.powerapps.com) and open **Connections**. Create a new, or open an existing, Dataverse connection, then:

1. Copy the **environment ID** found after `environments/` and the **connection ID** found after `...apps/` into the configuration.
2. Get the **tenant ID** via **Settings -> Session details**, then copy the tenant ID from the pop-up window.
3. Restart VS Code.
4. Search for the MCP server in the search bar and **enable MCP for Dataverse**.

---

## The exercise

With the Dataverse MCP connected, open a new GitHub Copilot Chat session (agent mode) against your D365 Customer Service environment and run the prompts below in order.

> **Model selection:** use an Anthropic model (Sonnet or Opus) - these currently have the best MCP tool-calling capability.

### Prompt 1 - Generate demo accounts

```
Create 10 individual accounts for a coffee roaster company that is delivering to different customer
groups like companies, supermarkets, restaurants etc. within Europe in D365 customer service. Always
add "(MCP)" in the end as an identifier. Come up with unique account names and add additional account
information for all fields on the account table that are realistic for a large size coffee roaster
company. Also add primary contact and email (primary contact).
```

### Prompt 2 - Configure a new field and place it on the form

```
Add a new drop-down field on the account table called "Coffee Purchasing Profile" with the following
options:

- Commercial / Bulk Coffee
- Classic / Everyday Coffee
- Premium Coffee
- Specialty Coffee
- Sustainable / Ethical Coffee

Add the field to the account form on the "Details" tab on the "Company Profile" tile below "Regions".
```

---

## What good looks like

- **After Prompt 1** you have 10 realistic coffee-roaster accounts in D365 Customer Service, each ending in `(MCP)`, with populated account fields plus a primary contact and email.
- **After Prompt 2** the account table has a new **Coffee Purchasing Profile** choice field with the five options, surfaced on the account form under **Details -> Company Profile**, below **Regions**.

---

## If something goes wrong - in this order

1. **Ask Copilot itself.** Paste the error. Ask *"what does this mean, and how do I fix it?"* Using Copilot to unstick itself is the muscle you are training today.
2. **Use your Dataverse knowledge.** Read the error Copilot returned, then instruct Copilot explicitly on how to work around it - wrong table, missing publisher prefix, unpublished customization.
3. **Ask a neighbour or the facilitator.**

---

## Take this home

The pattern you used today is reusable across any Customer Engagement app. Connect the Dataverse MCP once, then drive data generation and model configuration - tables, fields, option sets, forms - directly from natural-language prompts in VS Code. The clearer your instructions, the faster and more auditable the configuration. This is what AI-first delivery looks like for CE consultancy.
