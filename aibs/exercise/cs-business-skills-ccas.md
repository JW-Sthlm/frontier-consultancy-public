# Copilot Studio Business Skills (CCAS Config Automation)

This repository provides a step-by-step guide, prompts, and reusable templates to implement Business Skills in Copilot Studio for Dynamics 365 Contact Centre configuration automation.

The approach is demonstrating how to:

- Create Business Skills using prompts
- Configure D365 Contact Centre
- Generate demo data
- Validate an end-to-end scenario using Copilot Studio agents

## Overview

Business Skills enable you to:

- Define business processes once
- Store them centrally in Dataverse
- Allow Copilot Studio agents to discover and execute them
- Ensure consistent, repeatable execution

## Prerequisites

### Environment

- Managed Power Platform environment
- Dataverse Intelligence set to ON
- MCP client access to Dataverse MCP Server enabled

### Copilot Studio

- Create an agent
- Add tool: Microsoft Dataverse MCP Server

## Step-by-Step Implementation

### 1. Configure Environment Settings

In Power Platform Admin Center:

- Environment is Managed
- Enable MCP Client to Dataverse MCP Server
- Enable Dataverse Intelligence

### 4. Configure Copilot Studio Agent

1. Open Copilot Studio.
2. Create a new agent.
3. Add Microsoft Dataverse MCP Server (required) under tools.

## Prompts Used in Demo

### Main Prompt: Create Business Skills

Create business skills focused on Dynamics 365 Customer Service and Dynamics 365 Contact Center demos.

Use official Microsoft guidance and relevant up-to-date web sources.

Create business skills:

1. A business skill to configure Dynamics 365 Contact Center chat channel.
2. A business skill to generate industry-specific demo data based on an industry.
3. A business skill to execute configuration via MCP service.
4. A business skill to provide step-by-step instructions to test and validate the setup after configuration and data creation.

Ensure all skills support an end-to-end demo scenario.

### Execution Prompt: Configuration

Use the configuration skill to configure the environment for a basic Dynamics 365 Contact Center demo on the chat channel.

Identify any manual steps required and provide them clearly.

### Data Prompt: Demo Data

Use the industry-specific demo data skill to create demo data for a specified industry.

Create:

- Accounts
- Contacts
- Cases

Provide steps to validate that the data was created successfully.

### Validation Prompt

Use the validation skill to test and verify the Dynamics 365 Contact Center setup.

Validate:

- Chat channel
- Workstream
- Queues
- Demo data
- End-to-end chat routing

Provide step-by-step validation results.

## Execution Flow

1. Run the Business Skills creation prompt.
2. Agent generates multiple skills.
3. Execute the Configuration Skill, Demo Data Skill, and Validation Skill.
4. Complete any manual steps.
5. Test the end-to-end scenario.

## Example Output from Demo

- Chat channel configured
- Workstream and queues created
- Demo data generated:
- Validation instructions provided
- End-to-end test via chat

## End-to-End Test

After setup:

1. Open Power Pages or the chat experience.
2. Start a conversation.
3. Confirm:

- Chat widget loads
- Routing works
- Data is available
- Agent responds correctly

## Pro Tips

- Start with small, modular skills
- Use multiple skills instead of one large skill
- Let Copilot generate skills via prompts
- Use phased execution (configuration, data, validation)
- Extend with additional skills (for example intent and quality)

## Architecture Summary

- Copilot Studio Agent orchestrates execution
- Dataverse stores Business Skills
- MCP Server enables discovery and execution
- Skills drive configuration, data creation, and validation

## Outcome

Using this approach, you can:

- Configure a D365 Contact Centre demo
- Generate demo data
- Validate the solution

All within about 20 minutes using Business Skills.

## Repository Usage

Clone and customize this repo to:

- Accelerate partner demos
- Standardize implementations
- Reuse skills across projects

## Topics

Copilot Studio, Dynamics 365, D365 Contact Centre, Business Skills, Dataverse, MCP, Power Platform, AI Agents, Partner Enablement