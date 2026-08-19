# Source citation (reference)

Compact, traceable citation format for RFP sources.

## Format

```text
SRC-XLSX-001#sheet=Requirements&row=42
SRC-PDF-002#page=14
SRC-DOCX-001#section=3.2
SRC-EML-004#from=vendor&date=2026-08-13
```

- `SRC-<TYPE>-<nnn>` identifies the source document (registered in `wiki/source-map.md`).
- The `#...` fragment pins the exact location within that source.

## Rules

- When an exact page/row/section is unavailable, cite the closest known location and mark the
  reference as approximate.
- Every extracted claim in an answer should carry at least one source reference, or a
  Microsoft Learn documentation URL when the claim is a Microsoft product capability.
- Keep `wiki/source-map.md` as the single registry mapping each `SRC-` ID to its original file
  and metadata (filename, received date, type, provenance).

## Grounding product claims

For Microsoft product capability statements, cite the Learn documentation retrieved through the
Microsoft Learn MCP server, for example:

```text
Learn: https://learn.microsoft.com/en-us/dynamics365/commerce/ (fetched via microsoft_docs_fetch)
```

This lets a reviewer independently verify the capability against first-party documentation.
