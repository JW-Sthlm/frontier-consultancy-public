# Wiki conventions (reference)

Full structure and conventions for an RFP wiki. The `SKILL.md` body summarizes these; this
file holds the detail, loaded on demand.

## Folder layout per RFP

```text
<customer-or-project>-<year>/
  input/                      # immutable raw sources
  wiki/
    index.md                  # navigation hub — keep current
    source-map.md             # traceability metadata for every source
    open-items.md             # unclear / missing / contradictory / risky items
    answer-strategy.md        # how this RFP will be answered
    decision-log.md           # DEC- decisions
    context/                  # customer / project context pages
    requirements/             # REQ- requirement pages
    questions/                # Q- question pages
    sources/                  # extracted source Markdown
    answers/                  # answer drafts
    reviews/                  # review notes
    logs/                     # processing-log.md
  working/                    # scratch, scripts
  exports/                    # export-ready deliverables
```

## RFP folder naming

One folder per RFP, stable lowercase slug:`<customer-or-project>-<year>/`.
Examples: `contoso-crm-modernization-2026/`, `fabrikam-ai-contact-center-2026/`.
Do not rename after wiki work has started unless the user asks.

## Raw source handling

* Treat `input/` as immutable source storage.
* Do not edit, overwrite, normalize, or delete raw source files.
* If a source file must be renamed for clarity, ask the user first.
* Derived Markdown belongs in `wiki/`, not `input/`.
* Keep references traceable to the original file, page, sheet, row, table, or section.

## Stable IDs

* `Q-` questions, `REQ-` requirements, `SRC-` sources, `DEC-` decisions, `RISK-` risks,
  `OPEN-` clarification items.

* Examples: `Q-SEC-001`, `REQ-INT-004`, `SRC-PDF-003`, `OPEN-012`.
* Requirement IDs also follow `<ProcessCode>.<nn>`, e.g. `POS01.02`, `OMS02.01`.

## Front matter

```yaml
---
type: question
id: Q-SEC-001
status: draft
source_refs:
  - SRC-XLSX-001#sheet=Security&row=42
related:
  - ../requirements/security.md
---
```

Use only fields that are meaningful for the page.

## Status lifecycle

`new` -> `needs_context` -> `researching` -> `drafted` -> `needs_review` -> `approved` ->
`exported`. `blocked` may apply at any point (document why in the page).

**Export gate:** a question may only reach `exported` from `approved`. Do not export any
deliverable to `exports/` until *every* question page is `approved`; if any question is still
in an earlier state, stop and report the outstanding IDs instead of exporting drafts.

## Templates

Use consistent templates for: RFP index, source map, requirement page, question page, answer
page, open items, decision log, processing log. If a template is missing, create a suitable
Markdown page using the same conventions.
