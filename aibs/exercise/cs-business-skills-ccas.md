# Copilot Studio Business Skills (CCAS Config Automation)

**A step-by-step guide, prompts, and reusable templates to implement Business Skills in Copilot Studio for Dynamics 365 Contact Centre configuration automation.**

This repository provides a step-by-step guide, prompts, and reusable templates to implement Business Skills in Copilot Studio for Dynamics 365 Contact Centre configuration automation.

The approach is demonstrating how to:

- Create Business Skills using prompts
- Configure D365 Contact Centre
- Generate demo data
- Validate an end-to-end scenario using Copilot Studio agents

---

## Overview

Business Skills enable you to:

- Define business processes once
- Store them centrally in Dataverse
- Allow Copilot Studio agents to discover and execute them
- Ensure consistent, repeatable execution

For more information, see [Business skills overview (Microsoft Learn)](https://learn.microsoft.com/en-us/power-apps/maker/data-platform/data-platform-business-skill-overview).

---

## Prerequisites

### Environment

- [Managed Power Platform environment](https://learn.microsoft.com/en-us/power-platform/admin/managed-environment-enable)
- [Dataverse Intelligence](https://learn.microsoft.com/en-us/power-apps/maker/data-platform/data-platform-intelligence) set to ON
- [MCP client access to Dataverse MCP Server](https://learn.microsoft.com/en-us/power-apps/maker/data-platform/data-platform-mcp-disable) enabled

### Copilot Studio

- Create an agent
- Add tool: [Microsoft Dataverse MCP Server](https://learn.microsoft.com/en-us/microsoft-copilot-studio/add-tools-custom-agent)

---

## Step-by-Step Implementation

### 1. Where to find Business Skills

1. Open Power Apps.
2. Scroll to Business Skills (Preview).
3. Open the feature.

For more information, see [Create and use business skills (Microsoft Learn)](https://learn.microsoft.com/en-us/power-apps/maker/data-platform/data-platform-business-skills).

### 2. Configure Environment Settings

In Power Platform Admin Center:

- [Environment is Managed](https://learn.microsoft.com/en-us/power-platform/admin/managed-environment-enable)
- [Enable MCP Client to Dataverse MCP Server](https://learn.microsoft.com/en-us/power-apps/maker/data-platform/data-platform-mcp-disable)
- [Enable Dataverse Intelligence](https://learn.microsoft.com/en-us/power-apps/maker/data-platform/data-platform-intelligence)

### 3. Configure Copilot Studio Agent

1. Open [Copilot Studio](https://learn.microsoft.com/en-us/microsoft-copilot-studio/fundamentals-what-is-copilot-studio).
2. [Create a new agent](https://learn.microsoft.com/en-us/microsoft-copilot-studio/fundamentals-get-started).
3. Add Microsoft Dataverse MCP Server (required) under tools. See [Add tools to custom agents (Microsoft Learn)](https://learn.microsoft.com/en-us/microsoft-copilot-studio/add-tools-custom-agent).

---

## Prompts Used in Demo

Run the prompts below in order inside your Copilot Studio agent in the Chat interface.

### Prompt 1 - Create Business Skills

```
Create business skills focused on Dynamics 365 Customer Service and Dynamics 365 Contact Center demos.

Use official Microsoft guidance and relevant up-to-date web sources.

Create business skills:

1. A business skill to configure Dynamics 365 Contact Center chat channel.
2. A business skill to generate industry-specific demo data based on an industry.
3. A business skill to execute configuration via MCP service.
4. A business skill to provide step-by-step instructions to test and validate the setup after configuration and data creation.

Ensure all skills support an end-to-end demo scenario.
```

### Prompt 2 - Configuration

```
Use the configuration skill to configure the environment for a basic Dynamics 365 Contact Center demo on the chat channel.

Identify any manual steps required and provide them clearly.
```

### Prompt 3 - Demo Data

```
Use the industry-specific demo data skill to create demo data for a specified industry.

Create:
- Accounts
- Contacts
- Cases

Provide steps to validate that the data was created successfully.
```

### Prompt 4 - Validation

```
Use the validation skill to test and verify the Dynamics 365 Contact Center setup.

Validate:
- Chat channel
- Workstream
- Queues
- Demo data
- End-to-end chat routing

Provide step-by-step validation results.
```

---

## Execution Flow

1. Run the Business Skills creation prompt.
2. Agent generates multiple skills.
3. Execute the Configuration Skill, Demo Data Skill, and Validation Skill.
4. Complete any manual steps.
5. Test the end-to-end scenario.

## What good looks like

- **After Prompt 1** the agent generates multiple Business Skills covering configuration, demo data, MCP execution, and validation.
- **After Prompt 2** the chat channel is configured and any manual steps are clearly listed.
- **After Prompt 3** demo data is created: Accounts, Contacts, and Cases, with validation steps provided.
- **After Prompt 4** you have step-by-step validation results covering chat channel, workstream, queues, demo data, and end-to-end chat routing.

---

## End-to-End Test

After setup:

1. Open Power Pages or the chat experience.
2. Start a conversation.
3. Confirm:

   - Chat widget loads
   - Routing works
   - Data is available
   - Agent responds correctly

---

## Pro Tips

> - Start with small, modular skills
> - Use multiple skills instead of one large skill
> - Let Copilot generate skills via prompts
> - Use phased execution (configuration, data, validation)
> - Extend with additional skills (for example intent and quality)

---

## Architecture Summary

- Copilot Studio Agent orchestrates execution
- Dataverse stores Business Skills
- MCP Server enables discovery and execution
- Skills drive configuration, data creation, and validation

---

## Outcome

Using this approach, you can:

- Configure a D365 Contact Centre demo
- Generate demo data
- Validate the solution

All within about 20 minutes using Business Skills.

---

## Repository Usage

Clone and customize this repo to:

- Accelerate partner demos
- Standardize implementations
- Reuse skills across projects

---

## Topics

Copilot Studio, Dynamics 365, D365 Contact Centre, Business Skills, Dataverse, MCP, Power Platform, AI Agents, Partner Enablement