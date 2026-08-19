---
name: "rfp-processing"
description: "Ingests, structures, analyzes, and answers Requests for Proposal (RFPs) by turning raw"
---

# RFP Processing

## What this skill does

Transforms raw RFP source material (Word, Excel, PDF, PowerPoint, email, notes) into a
structured, Markdown-based wiki with traceable sources, stable IDs, cross-references, a
question inventory, answer drafts, review state, and export-ready deliverables.

The goal is **not** to answer isolated questions. It is to preserve the full RFP context and
use only the *relevant* context for each answer, with every claim traceable to a source or to
official Microsoft documentation.

## Base structure

Work inside one folder per RFP, using a stable lowercase slug `<customer-or-project>-<year>/`:

```text
<customer-or-project>-<year>/
  input/      # raw source material, treated as immutable
  wiki/       # derived Markdown (index.md, source-map.md, open-items.md,
              # answer-strategy.md, decision-log.md, + context/ requirements/
              # questions/ sources/ answers/ reviews/ logs/)
  working/    # scratch space for intermediate work
  exports/    # export-ready Excel/Word/Markdown deliverables
```

See `references/wiki-conventions.md` for the full folder and page conventions.

## Core conventions

* **Stable IDs**: `Q-` questions, `REQ-` requirements, `SRC-` sources, `DEC-` decisions,
  `RISK-` risks, `OPEN-` clarifications. Requirement IDs follow `<ProcessCode>.<nn>`.

* **Front matter**: every generated page starts with YAML front matter (`type`, `id`,
  `status`, `source_refs`, `related`) where meaningful.

* **Status values**: `new`, `needs_context`, `researching`, `drafted`, `needs_review`,
  `approved`, `blocked`, `exported`.

* **Cross-references**: relative Markdown links; keep `wiki/index.md` current.
* **Source citations**: compact form — `SRC-XLSX-001#sheet=Requirements&row=42`,
  `SRC-PDF-002#page=14`, `SRC-DOCX-001#section=3.2`. See `references/source-citation.md`.

## Ingestion workflow

1. Identify the target RFP folder. This would be the current workspace folder.
2. Create the base folder structure.
3. Have the user place the customer supplied source files in the `input/` folder.
4. Inspect `input/` and list every source file. Treat `input/` as immutable — never edit,
   overwrite, normalize, or delete raw sources.
5. Extract or summarize source content into Markdown under `wiki/sources/`.
6. Create or update `wiki/source-map.md` with traceability metadata.
7. Build or update thematic pages under `wiki/context/` and `wiki/requirements/`.
8. Extract concrete RFP questions into `wiki/questions/` with stable IDs.
9. Update `wiki/index.md` navigation.
10. Update `wiki/open-items.md` for unclear, missing, contradictory, or risky items.
11. Append an entry to `wiki/logs/processing-log.md` describing what changed.

Mark uncertainty explicitly when source extraction quality is unclear. Do not treat extracted
Markdown as final truth.

## Context assembly for each answer

Do not send the entire wiki to the model. Assemble a focused package: the exact question page,
its parent requirement/topic, customer/project context, related Q\&A, the relevant source
excerpts, the answer strategy and known decisions, and — where product facts are involved —
official documentation retrieved through the **Microsoft Learn MCP server** (see below).

## Answer drafting workflow

1. Read the question page and its related links.
2. Identify missing context or ambiguity; resolve from internal wiki context first.
3. For any Microsoft product capability claim, verify against official docs using the
   Microsoft Learn MCP server before asserting it.
4. Draft the answer under `wiki/answers/` (or the question page's answer section), with
   assumptions, source references, and a confidence note.
5. Set status to `needs_review` unless the user explicitly approves it.

Keep answers concise, factual, and reusable for export. Do not invent unsupported
capabilities and do not remove uncertainty when the source material is unclear.

## Using the Microsoft Learn MCP server

This skill uses the Microsoft Learn MCP (remote MCP server) that grounds answers in
first-party Microsoft/Azure/Dynamics 365 documentation. Use it whenever an answer depends on a
Microsoft product capability:

* `microsoft_docs_search` — semantic search for the relevant doc (e.g. "Dynamics 365 Commerce
  offline POS", "Commerce distributed order management").

* `microsoft_docs_fetch` — pull the full page for the top hit, then cite it in the answer.
* `microsoft_code_sample_search` — retrieve an official code/integration example when a
  question needs one.

Prefer official documentation over training data or general web content. Cite the Learn URL in
the answer's source references so reviewers can verify the claim.

## Review and quality rules

Before marking an answer `approved`: confirm it answers the exact question; check consistency
with related answers; ensure product claims are backed by sources or Learn documentation; flag
assumptions clearly; never invent capabilities; never remove genuine uncertainty.

## Export workflow

**Approval gate (mandatory):** do **not** export until *every* question page has
`status: approved`. Before any export, verify there are no question pages left in `new`,
`needs_context`, `researching`, `drafted`, `needs_review` or `blocked`. If any question is
not `approved`, stop and report the outstanding items (with their IDs and current status) to
the user, and resume the export only after they have been approved. Never export drafts.

Export-ready content belongs in `exports/`: a filled Excel response matrix, a Word response
document, a Markdown answer pack, an executive summary, or a risk-and-assumptions register.
Once exported, set the source question pages' status to `exported`. Do not overwrite exported
files unless the user explicitly asks for regeneration.

## Additional resources

* **`references/wiki-conventions.md`** — full wiki folder and page structure, required files,
  front-matter fields, and status lifecycle.

* **`references/source-citation.md`** — source citation format and traceability rules.

