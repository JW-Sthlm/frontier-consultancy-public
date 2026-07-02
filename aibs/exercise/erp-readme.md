# AIBS Frontier Consultancy - Hands-on exercise for ERP

**You just walked out of nine Zava DIY implementation workshops. The whiteboard is full, the transcripts are long, and your next task is Dynamics 365 warehouse configuration. You have Copilot and the D365 ERP MCP. Let's see how fast this goes.**

---

> **Before the workshop:** run the prereq check in [`erp-setup-overview.md`](erp-setup-overview.md). You will need a GitHub Copilot seat, VS Code with agent mode, the D365 ERP MCP configured, the Copilot instructions and skill files in your workspace, and a Dynamics 365 Tier 2 or UDE environment connected to Dataverse. A Tier 1 or CHE environment is not sufficient.

## The scenario

You are a functional consultant on a Dynamics 365 Supply Chain Management implementation for **Zava DIY**, a fictional home improvement retailer based in Seattle. Zava operates a single distribution centre (ZAVDC1) in **WHS-Only mode** - Dynamics 365 Warehouse Management is the system of record for the DC, and an external OMS (ZAVA-OMS) handles order processing.

You have completed nine design workshops. Two documents came out of them:

- **Decision log** ([`client/zava_whs_decision_list.md`](client/zava_whs_decision_list.md)) - 22 validated design decisions covering deployment mode, zone architecture, inventory statuses, wave processing, picking strategy, replenishment, mobile device menus, and more.
- **Workshop transcripts** ([`client/zava_whs_implementation_workshop_transcripts.md`](client/zava_whs_implementation_workshop_transcripts.md)) - nine sessions of discussion capturing rationale, open items, and decisions in context. In a real engagement these would come from recorded meeting transcripts; for the purpose of this exercise they are provided as a single text file in Markdown format.

The next step is D365 WHS configuration. You will do it in two phases.

---

## What you will do

### Phase 0 - Validate your skill file

Before generating a runbook, confirm that a skill.md exists for the configuration work you are about to do. The skill file is what tells Copilot how to configure the module — without it, the runbook will be incomplete.

Check your workspace for a skill file at .github/skills/[relevant-module]/skill.md. For this exercise, the WHS skill is provided in [implementation-ip/](implementation-ip/) and is already covered in the setup guide.

If you are working on a module or setup area that is **not** covered by an existing skill, generate one first using the [ERP Skill Builder](erp-skillbuilder.md) before continuing to Phase 1.
### Phase 1 - Generate a configuration runbook

Open a new GitHub Copilot Chat session (agent mode). Attach both client files and enter **Prompt 1** below.

Copilot will use the D365 ERP MCP skill to analyse both source documents and generate a structured runbook - every configuration action in the correct order, with the actual data, each item traceable back to the decision log and the workshop sessions.

> **The runbook is an approval artefact.** Before anything is created in D365, a consultant reviews it. If it looks right, you move to Phase 2.

### Phase 2 - Execute the configuration

Enter **Prompt 2** below. Copilot will use the runbook and the D365 ERP MCP to configure Warehouse Management in your legal entity, checking off each action as it completes.

---

## Prompts

### Prompt 1 - Create the runbook

```
We are implementing Dynamics 365 ERP with a home improvement retailer named Zava DIY. We have been
running implementation workshops, and the resulting meeting transcripts and decision log are stored
in the corresponding md files. These are added as attachments.

Your task: I want to set up a WHS only warehouse for this company. Do not create the actual
configuration in Dynamics, but instead use the skill to create a new runbook named
zava_whs_runbook.md that contains the runbook of the actions to be undertaken, including the
configuration data to be stored. For configuration actions, use the Excel sheet data in the BPC
reference folder, and use the MS Learn MCP server. For configuration data, use the decision list md
and implementation workshop transcript md. Only use files mentioned in your instructions or files
added as attachments. Do not use any other files available in the workspace as they could be for
different purposes.

When creating the runbook, include references to the BPC, the decision list and the workshop
information so the consultant validating the runbook will know where the data originated from.
Every action in the runbook should have an empty checkbox so we can track progress later.
```

### Prompt 2 - Execute the configuration

```
I just created a new legal entity in D365 named "zav1". Your task: configure WHS only mode in this
legal entity using the runbook provided. Update your progress in the runbook by checking the
checkbox when the task is completed.
```

---

## What good looks like

**After Phase 1** you should have a `zava_whs_runbook.md` that:

- Covers all 22 decisions from the decision log
- Has every action with an empty `[ ]` checkbox
- References the specific decision ID and workshop session for each data item
- Is structured by D365 configuration entity (legal entity → sites → warehouses → zones → locations → inventory statuses → wave templates → replenishment → picking → mobile device menus)

**After Phase 2** you should have WHS configured in D365 with all configuration items imported and the runbook checkboxes checked off.

---

## If something goes wrong - in this order

1. **Ask Copilot itself.** Paste the error. Ask *"what does this mean, and how do I fix it?"* Using Copilot to unstick itself is the muscle you are training today.
2. **Use your D365 ERP skills.** Read the error Copilot returned. Apply your functional knowledge to identify what is wrong - wrong sequence, missing prerequisite, incorrect entity - then instruct Copilot explicitly on how to work around it.
3. **Ask a neighbour or the facilitator.**

---

## Take this home

The runbook pattern you generated today is reusable. Every D365 product - Finance, Supply Chain, Project Operations - can be approached the same way:

1. Bring your discovery artefacts (workshops, decision logs, scope documents)
2. Generate a module-specific runbook from them
3. Review and approve the runbook
4. Execute configuration via the D365 ERP MCP

The more structured your discovery artefacts, the better the runbook. The better the runbook, the faster and more auditable the configuration. This is what AI-first delivery looks like for ERP consultancy.