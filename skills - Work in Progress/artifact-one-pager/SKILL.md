---
name: artifact-one-pager
description: Use when asked to build a one-pager, solution brief, integration sheet, or vertical leave-behind. Generates a layout spec with copy and a design-generation prompt for a print-ready PDF from the messaging canon and visual identity.
---

# Artifact: One-Pager

Renders a print-ready one-pager draft from approved context: a designed, page-sized file in
the brand's colors and type. A human reviews it before it ships. See
[rendering.md](../rendering.md) for the build and QA mechanics.

## What this skill produces

A designed one-pager rendered to a page-sized `.pptx` (exported to PDF when LibreOffice is
available), in the visual identity, plus a short companion `.md` logging any canon gaps. A
draft for human review.

## Reads from context

Slices first, from [lockups](../../context/lockups.md) and
[entry-points](../../context/entry-points.md) (`approved` only):

- the `value-prop-core` lockup: the hero and the benefit grid (its lead claim is the hero;
  its capability and feature claims fill the body and benefits)
- for the integration format: the matching integration entry point (e.g. `snowflake`)
- for the vertical format: the matching persona or vertical entry point

Then canon [claims](../../context/claims.md) by component ID, for what no slice covers:

- `positioning`, `category-name`: the header, when the lockup doesn't carry them
- `customer-proof`, `key-metrics`: the proof band
- `ecosystem-integrations`: required for the integration format
- `icp` (the account): required for the vertical format (the industry framing)
- `icp` (the champion's job to be done): the problem statement, in the customer's words

And the full [visual identity](../../context/brand-visual-identity.md) for the render, plus
[brand-writing-identity](../../context/brand-writing-identity.md) for voice, guardrails, and lexicon.

If a needed slice is missing or `draft`, fall back to canon claims by component and log the
gap. If a required component has no canon claims, mark the affected section as a gap and say
so. Only `canon` claims are rendered. Never invent messaging to fill a hole.

## Asks the human

One at a time, and only what context cannot hold:

1. **Format.** Product, solution, integration, or vertical? (See [one-pager-formats.md](one-pager-formats.md).)
2. **Subject.** Which product, which integration partner, or which vertical?
3. **CTA.** The next step, and whether a QR code or URL belongs on the page.
4. **Page size.** US Letter or A4?

## Workflow

1. Read the slices, canon claims, and visual identity listed above. Note any gaps (missing
   slices, draft slices, empty components).
2. Ask the four questions.
3. Pick the format's layout from [one-pager-formats.md](one-pager-formats.md) and fill each section from the slice's claims (then canon claims where no slice covers), enforcing the word counts in the reference file. If a section runs over, cut, never shrink the type.
4. Render the one-pager per [rendering.md](../rendering.md): a `pptxgenjs` build on a page-sized custom layout (US Letter or A4), the visual identity mapped to color constants and the brand fonts, the format's section allocation laid out to the percentages in the reference file. Export to PDF when LibreOffice is available.
5. Run content and visual QA per [rendering.md](../rendering.md). Write a short companion `.md` beside the file logging any gaps, and file each as a theme in [issues](../../builder/issues/) with this run as evidence.
6. Run the checklist and hand back the file path.

## Checklist

- Exactly 3 benefits; more dilutes
- Every word count in the reference file is respected
- The hero states an outcome, not a hedge ("helps you improve" is a hedge)
- Proof band uses real canon `customer-proof` claims; no generic "trusted by leading companies" lines
- CTA is visible on the page, not buried
- Every rendered statement traces to a `canon` claim (by `clm-` ID in the companion `.md`); nothing invented, no candidates; no banned terms or em/en dashes survive the content QA
- The rendered file is page-sized, on-brand, and QA'd (visual pass run, or its absence stated in the handoff)
