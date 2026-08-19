# AIBS Frontier Consultancy - Hands-on exercise for RFP processing in Scout Co-create

**A 100-question RFP just landed in your inbox: a Word cover, two appendices, and a sprawling Excel response form. The deadline is short and the answers have to be defensible. You have Microsoft Scout with Co-create and the RFP processing skill. Let's turn that pile of source files into a structured, traceable, export-ready response, without leaving Scout.**

This exercise runs **entirely inside Microsoft Scout Co-create**, and it is built around one specific tool: the **`rfp-processing`** **Scout skill**. There is no VS Code, no repo to clone, no local build. The skill does the whole motion: it ingests the raw sources, builds a Markdown wiki with stable IDs and source traceability, drafts answers grounded in Microsoft Learn, holds an approval gate, and only then exports the filled deliverables. The skill, and everything you need to install it, ships with this exercise in [`rfp-ip/`](rfp-ip/).

> **Credit:** the `rfp-processing` skill was created by **[Joris Kalz](https://www.linkedin.com/in/joris-kalz/)**. This exercise packages his work into a hands-on Frontier Consultancy scenario.

> **Before the workshop:** run the prep checks in [`rfp-setup-overview.md`](rfp-setup-overview.md). You will need Microsoft Scout installed and signed in, the Co-create capability, the `rfp-processing` skill installed from [`rfp-ip/`](rfp-ip/), the Microsoft Learn MCP server added to Scout for grounding, and the Zava source pack from [`client/zava-rfp/`](client/zava-rfp/).

***

## Why this skill matters for Frontier Consultancy

Responding to an RFP is one of the most expensive, least repeatable things a partner does. The source material is messy (Word, Excel, PDF, email, workshop notes), the questions run into the hundreds, and every answer has to be both accurate and traceable back to something. Under deadline pressure, teams copy last year's answers, lose the thread on which claim came from where, and ship responses no one can audit.

The RFP processing skill closes that gap by treating an RFP as a **knowledge base, not a document**. It gives a consultant:

* **Structure over chaos** - raw sources become a navigable wiki: a question inventory, requirement pages, extracted source excerpts, and an index that ties them together.
* **Traceability by construction** - every question, requirement, source, and decision carries a stable ID (`Q-`, `REQ-`, `SRC-`, `DEC-`), and every answer cites the exact source location or the Microsoft Learn page that backs it.
* **Grounded product claims** - capability statements about Dynamics 365, Azure, or Power Platform are verified against first-party Microsoft Learn documentation, not asserted from memory.
* **A real review discipline** - answers move through an explicit status lifecycle and cannot be exported until every question is approved. No drafts leak into the deliverable.

For a partner, this is the difference between AI that *drafts words* and AI that *runs the bid*. It is the AI-first delivery motion applied to pursuit itself.

***

## Why Scout, and not Copilot Chat, Cowork, or GitHub Copilot

The RFP skill produces a wiki: a couple of hundred small, cross-linked Markdown files that get created, updated, and status-tracked over the life of a bid. The other Copilot surfaces can each touch part of that job, but each has a catch for a *shared, non-technical* bid team. Here is the honest comparison.

| Surface                              | Where it falls short for this exercise                                                                                                                                                                                                                                                                                                                                              |
| ------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Microsoft 365 Copilot Chat**       | Turn-based chat with no persistent, browsable project workspace. It can draft a single answer, but it cannot hold and evolve a 200-file wiki across a session, keep the files cross-linked, or track per-question status. The knowledge base has nowhere to live.                                                                                                                   |
| **Copilot Cowork**                   | Cowork can generate and work the wiki, but it keeps those files to itself: it does not give you and your colleagues shared, live access to the wiki files as it works. Without that shared visibility there is no genuine *co-create* experience, the team cannot open, read, and edit the same evolving wiki alongside the agent.                                                  |
| **GitHub Copilot in VS Code (GHCP)** | You *can* run this exercise in GHCP, it is a very capable file-and-repo environment. But VS Code is a developer's tool: an IDE with a cloned repo, extensions, and source control. That is a better fit for a technical audience than for the bid managers and functional consultants this exercise trains, and it pulls the work into a coding context rather than a business one. |

**Scout Co-create is the sweet spot.** You get a real, persistent **workspace** that holds the whole wiki, files you and your colleagues can open, read, and watch the agent build and edit **in place, together** (local OneDrive-backed, or shared through SharePoint). That shared, live access to the same files is the co-create experience Cowork does not provide. Yet it stays a **non-technical working environment**: no IDE, no repo to clone, no Git, no build step. In short, Scout gives a proposal team the multi-file power of a developer tool with the approachability and shared access of a document workspace, which is exactly what an RFP response needs.

***

## The scenario

You are responding to a bid from **Zava Retail Group**, a fictional but realistic multi-national omnichannel retailer selecting a Dynamics 365 Commerce platform across Canada, the United States, and the United Kingdom. The source pack (in [`client/zava-rfp/`](client/zava-rfp/)) is four files:

| File                                               | What it is                                                                                                                                    |
| -------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| **Zava - RFP D365 Commerce - Cover Document.docx** | The issuer-side RFP narrative: background, objectives, scope, markets, and how to respond                                                     |
| **Zava - RFP D365 Commerce - Appendix A.docx**     | Store and channel footprint: estate size, formats, volumes, currencies, languages                                                             |
| **Zava - RFP D365 Commerce - Appendix B.docx**     | Integration landscape and reference architecture                                                                                              |
| **Zava - RFP D365 Commerce - Response Form.xlsx**  | Appendix C: the response matrix, 105 functional requirements, 27 NFRs, 8 use cases, with a MoSCoW priority column and an A-F compliance model |

These four files are the exercise input. They are **immutable**, the skill never edits raw sources, it only derives from them. You will copy them into your workspace's `input/` folder when you set up (under **Prompts**, below).

***

## What you will do

The skill runs a five-stage motion, all in one Co-create workspace. Here is the shape it produces, then the five stages that fill it.

### The workspace it builds

By the end of Phase 1 you will have this shape inside your Co-create workspace:

```text
/zava-d365-commerce-2026/
  input/        # the immutable Zava source pack you dropped in
  wiki/
    index.md            # navigation hub
    source-map.md       # every source registered with an SRC- id
    open-items.md       # unclear / missing / contradictory items
    answer-strategy.md  # how this RFP will be answered
    decision-log.md     # DEC- decisions
    context/            # customer / project context
    requirements/       # REQ- requirement pages
    questions/          # Q- question pages (one per RFP question)
    sources/            # extracted source Markdown
    answers/            # answer drafts
    reviews/            # review notes
    logs/               # processing-log.md
  working/      # scratch space for intermediate work
  exports/      # the filled matrix + response doc (created only after the approval gate)
```

Every page carries YAML front matter (`type`, `id`, `status`, `source_refs`, `related`), and citations pin the exact location, for example `SRC-XLSX-001#sheet=Functional Requirements&row=42`.

### Phase 1 - Ingest and structure

Point the skill at the Zava source pack. It inspects every file in `input/`, extracts the content into `wiki/sources/`, registers each source in a `source-map.md`, builds thematic `context/` and `requirements/` pages, and turns every concrete RFP question into its own page under `wiki/questions/` with a stable ID and source reference.

**The result is a navigable wiki, not a wall of text.**

### Phase 2 - Set the response strategy

Before drafting a single answer, decide *how* you will win this RFP. The skill captures that in `wiki/answer-strategy.md`: the positioning and win themes, which requirements to lead on, where the fit is strong versus partial, how to handle gaps and assumptions, and the overall tone of the response. A good strategy makes every later answer faster and more consistent, because the skill drafts against it.

> **Tip:** do not write the strategy cold. Ask Scout to analyse the ingested RFP first and propose one: *"Read the wiki you just built and propose the best response strategy for this RFP: win themes, where we are strong, where we are weak, and how to handle the gaps."* Refine its proposal, then lock it into `answer-strategy.md`.

### Phase 3 - Draft and ground

For each question, the skill assembles a focused context package (the question, its requirement, related Q&A, the relevant source excerpts) and drafts an answer. For any Microsoft product capability claim, it verifies against official documentation on Microsoft Learn and cites the Learn URL. Drafts land at status `needs_review`.

### Phase 4 - Review and approve

You review. Answers move `drafted` to `needs_review` to `approved`. This is the human gate: you confirm each answer addresses the exact question, is consistent with related answers, and is backed by a source or a Learn citation. Nothing is invented; genuine uncertainty is kept, not smoothed over.

> **Exercise shortcut, force-approve the remainder.** A real Zava response has 100-plus questions and you will not hand-review them all in a workshop. Review a handful properly to build the muscle, then tell the skill to approve the rest in bulk so you can reach the export step: *"Approve all remaining question pages and set their status to approved so we can demonstrate the export."* This is a deliberate exercise shortcut. In a real bid every answer earns its approval; you never bulk-approve to beat the gate.

### Phase 5 - Export (gated)

**The skill will not export until every question page is** **`approved`.** Once the gate is clear, it produces the export-ready deliverables in `exports/`: a filled Excel response matrix, a Word response document, and a Markdown answer pack, then flips the approved questions to `exported`.

***

## Prompts and actions

### Action 1 - Set up your Co-create workspace

Before you prompt anything, create the workspace the skill will work inside. This is Co-create, so the work happens in a **workspace**, not an ordinary chat.

1. In Scout, open the **Co-create** panel and **create a new workspace** named `zava-d365-commerce-2026`. A workspace can be a **local folder**, **a cloud folder** (backed by OneDrive), or **shared with your team** (backed by SharePoint). Any of these works for this exercise.
2. From here on, all the work happens **inside this workspace**. Keep it active and run the steps below in order: the skill creates the folder structure (Prompt 1), you add the source files (Action 2), then the skill ingests them (Prompt 2).

### Prompt 1 - Create the folder structure

```
/rfp-processing

Create the folder structure required to process rfp's.
```

### Action 2 - Add the Zava source files to `input/`

Download the four Zava RFP source files and place them in the **`input/`** folder the skill just created:

* [Cover Document (.docx)](client/zava-rfp/Zava%20-%20RFP%20D365%20Commerce%20-%20Cover%20Document.docx)
* [Appendix A (.docx)](client/zava-rfp/Zava%20-%20RFP%20D365%20Commerce%20-%20Appendix%20A.docx)
* [Appendix B (.docx)](client/zava-rfp/Zava%20-%20RFP%20D365%20Commerce%20-%20Appendix%20B.docx)
* [Response Form (.xlsx)](client/zava-rfp/Zava%20-%20RFP%20D365%20Commerce%20-%20Response%20Form.xlsx)

All four live in [`client/zava-rfp/`](client/zava-rfp/). Treat them as **immutable**, the skill only reads them, it never edits raw sources.

### Prompt 2 - Ingest and build the wiki

```
/rfp-processing

I am responding to the Zava D365 Commerce RFP. The source pack (cover document, Appendix A,
Appendix B, and the Excel response form) is in input/. Ingest all of
it: build the rest of the RFP wiki alongside it in the workspace folder, register every source in the source
map, extract the questions into individual question pages with stable IDs, and create the
requirement and context pages. Treat input/ as immutable. When you are done, show me the index and
tell me how many questions, requirements, and sources you created.
```

### Prompt 3 - Set the response strategy

```
Read the wiki you just built and propose the best response strategy for this Zava RFP: our win
themes, where Dynamics 365 Commerce is a strong fit, where it is only a partial fit, and how to
handle the gaps and assumptions. Write it to wiki/answer-strategy.md. I will refine it before you
start drafting.
```

### Prompt 4 - Draft grounded answers

```
Draft answers for the functional requirement questions, following the response strategy. For every
claim about a Dynamics 365 Commerce capability, verify it against official documentation on
Microsoft Learn and cite the Learn URL. Note any assumptions and a confidence level on each answer.
Leave every answer at status needs_review, do not approve anything yet.
```

This exercise uses MS Learn as the knowledge base to ground on, which it can be for Dynamics 365 Commerce. If you have a tailored knowledge source available, point to this instead or combine with MS Learn.

### Prompt 5 - Review and approve a batch

```
Walk me through the first 10 drafted answers one at a time. For each, show the question, your
draft, and its sources. I will tell you to approve it or send it back for a change. Update the
status accordingly.
```

### Prompt 6 - Try to export early (see the gate)

```
Export the filled Excel response matrix now.
```

You should be **refused**. The skill will report the outstanding question IDs that are not yet `approved` and refuse to export drafts. That refusal is the exercise working as intended.

### Prompt 7 - Approve the rest (exercise shortcut)

```
Approve all remaining question pages and set their status to approved so we can demonstrate the
export step. This is an exercise shortcut only; in a real bid every answer earns its own approval.
```

### Prompt 8 - Export for real

```
Now that every question page is approved, export the deliverables to exports/: the filled Excel
response matrix and a Word response document. Then set the exported question pages to status
exported.
```

***

## What good looks like

* **After Prompt 1** the empty wiki folder structure exists in your workspace: an `input/` folder plus the `wiki/`, `working/`, and `exports/` scaffold, ready for the source files.
* **After Prompt 2** you have a populated `wiki/` tree: an `index.md` you can navigate, a `source-map.md` listing each source with an `SRC-` id, and one question page per RFP question with front matter and a source reference. The skill reports counts (on the order of a hundred-plus questions for the Zava pack).
* **After Prompt 3** `wiki/answer-strategy.md` holds a clear, refined response strategy, win themes, fit assessment, and how gaps will be handled, that the drafting builds on.
* **After Prompt 4** functional answers are drafted at status `needs_review`, each Microsoft capability claim carrying a Microsoft Learn citation, and assumptions and confidence noted.
* **After Prompt 5** the batch you reviewed sits at `approved`, and any you sent back shows your requested change.
* **After Prompt 6** the export is **blocked** with a clear list of the not-yet-approved question IDs. This is the approval gate doing its job.
* **After Prompt 7** the remaining questions flip to `approved` (the exercise shortcut), clearing the gate.
* **After Prompt 8** `exports/` contains a filled response matrix and a Word response document, and the source question pages read `status: exported`.

***

## If something goes wrong - in this order

1. **Ask Scout itself.** Paste the error or describe what looks off. Ask *"what does this mean, and how do I fix it?"* Using the agent to unstick itself is the muscle you are training.
2. **Check the source pack is in** **`input/`.** If ingestion finds nothing, the files are probably in the wrong folder or the workspace root, not `input/`. Move them and re-run Prompt 2.
3. **Check the Learn MCP server is on.** If answers cite no documentation, Scout cannot reach Microsoft Learn. Confirm the **Microsoft Learn MCP server** is added and **Enabled** in **Settings > Extensions**, restart Scout, then re-run the draft step.
4. **Trust the export refusal.** If the skill refuses to export, that is not a bug. Something is still short of `approved`. Ask it to list the outstanding question IDs and their status, then finish the review.
5. **Ask a neighbour or the facilitator.**

***

## Take this home

The pattern you ran today is reusable across every pursuit, not just this one:

1. Drop the raw RFP sources into `input/` and treat them as immutable.
2. Let the skill build a traceable wiki: questions, requirements, sources, all ID-linked.
3. Set a response strategy and let it steer the drafting.
4. Draft answers grounded in first-party Microsoft documentation.
5. Review to `approved`, honouring the gate.
6. Export the filled matrix and response document, with every claim traceable.

The more structured your discovery, the better the wiki. The better the wiki, the faster and more auditable the response. A bid that used to consume a team for a week becomes a reviewed, traceable, defensible response assembled in a fraction of the time, with the reasoning behind every answer preserved rather than lost. This is what AI-first delivery looks like applied to the pursuit motion itself.

***

### Reference

* [Get started with Microsoft Scout](https://learn.microsoft.com/en-us/microsoft-scout/get-started) - install Scout, sign in, and set up your first workspace
* [Use Microsoft Scout](https://learn.microsoft.com/en-us/microsoft-scout/use-microsoft-scout) - files, Co-create, extensions, and permissions
* [Microsoft Learn MCP server](https://learn.microsoft.com/en-us/training/support/mcp) - the first-party documentation the skill grounds on (added to Scout via Settings > Extensions)
* [Dynamics 365 Commerce documentation](https://learn.microsoft.com/en-us/dynamics365/commerce/) - the product area the Zava RFP targets
* The RFP wiki conventions (folder layout, stable IDs, status lifecycle, and the export gate) are defined inside the `rfp-processing` skill itself; ask Scout to show them if you want the detail.

