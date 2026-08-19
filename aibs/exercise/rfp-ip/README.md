# RFP IP - the skill that powers the exercise

This folder holds the intellectual property a participant needs to run the
[RFP processing exercise](../rfp-exercise.md): the **`rfp-processing`** Microsoft
Scout skill, complete with its reference conventions.

## Credit

The **`rfp-processing`** skill was created by **[Joris Kalz](https://www.linkedin.com/in/joris-kalz/)**.
This folder and the accompanying exercise package his work for use in Frontier
Consultancy.

## What is here

```text
rfp-ip/
  rfp-processing/
    SKILL.md                        # the skill itself: the full RFP processing procedure
    references/
      wiki-conventions.md           # folder layout, stable IDs, front matter, status lifecycle
      source-citation.md            # the compact, traceable source-citation format
```

## How to install the skill

The exercise runs in **Microsoft Scout**. To make the skill available:

1. Copy the whole **`rfp-processing/`** folder into your Scout skills directory
   (on Windows this is `%USERPROFILE%\.scout\m-skills\`).
2. Restart Scout so it loads the skill.
3. In the Scout chat box, type `/` and confirm **`rfp-processing`** now appears in the list.

Installing the skill is the only step to make `/rfp-processing` available. To ground its answers
in Microsoft documentation it also uses the **Microsoft Learn MCP server** (public, no sign-in);
add that to Scout via **Settings > Extensions** as described in
[`../rfp-setup-overview.md`](../rfp-setup-overview.md).

## What the skill does

It turns raw RFP source material into a structured, traceable, Markdown wiki (question inventory,
requirement pages, extracted sources, all ID-linked), drafts answers grounded in first-party
Microsoft documentation, holds a mandatory approval gate, and only then exports the filled
deliverables. The exercise walks through that motion end to end using the Zava RFP source pack in
[`../client/zava-rfp/`](../client/zava-rfp/).
