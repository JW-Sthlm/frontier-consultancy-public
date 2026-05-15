# Tier 3 — Ground the brief in real Azure (super-stretch, ~5 min)

Only do this if Tiers 1 and 2 are done and you still have time.

**What you will do:** add the Azure MCP to Copilot so it can query your own Azure subscription, then ask the brief to include a "your current state" section grounded in your real resources.

---

## Pre-reqs

- An Azure subscription you can `az login` to — personal MSDN, partner sandbox, Visual Studio subscription, or your own.
- **Azure CLI** installed. Check: `az --version`. Install: [aka.ms/azcli](https://aka.ms/azcli).
- You are logged in: `az login`. Pick the subscription you want Copilot to see.

**Read/list-only permissions are enough for this tier.** You are not deploying anything.

---

## Step 1 — Add the Azure MCP

Inside Copilot CLI:

```
I want to add the Azure MCP server to my Copilot CLI config. Here is the
docs URL:
https://github.com/Azure/azure-mcp

Set it up to use my current az login (DefaultAzureCredential). Add it to
~/.copilot/mcp-config.json next to the microsoft-learn entry. Tell me how
to verify.
```

Approve. Run `/mcp` to confirm **azure** is listed.

---

## Step 2 — Ground the brief

Prompt Copilot:

```
Using the Azure MCP, list the resource groups and AI-relevant services
(OpenAI, AI Services, AI Search, Storage, Key Vault, Log Analytics) in my
current subscription. Just a summary — names, regions, SKUs.

Then add a "Your current state" section to brief.md. It should honestly
compare what Nordwind actually has against what the Azure Landing Zone for
AI recommends, and call out the top 3 gaps.
```

Watch the Azure MCP calls. Read the updated brief. Notice how specific it is — not "you should have a landing zone", but "you have 3 resource groups, no Log Analytics workspace, storage in a different region from your AI Services — here is the gap".

---

## Why this matters

A brief that quotes your client's actual cloud footprint is different from a generic one by an order of magnitude. This is the kind of grounded output your consultants would spend an hour preparing manually. Copilot did it in twenty seconds.

The Azure MCP inherits your `az login` identity and the RBAC on it. **Scope your login down** if you are not sure — run the exercise against a read-only subscription, or use a sandbox. Never point this at customer production.
