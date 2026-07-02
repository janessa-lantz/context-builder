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

From the [canon](../../context/messaging-canon.md), by component ID:

- `positioning`, `category-name`: the header and hero
- `products`, `unique-attributes`: the body, scoped to the format
- `value-proposition`, `value-drivers`: the benefit grid, framed as outcomes
- `customer-proof`, `key-metrics`: the proof band
- `ecosystem-integrations`: required for the integration format
- `icp` (the account): required for the vertical format (the industry framing)
- `icp` (the champion's job to be done): the problem statement, in the customer's words

And the full [visual identity](../../context/brand-visual-identity.md) for the render, plus
[brand-writing-identity](../../context/brand-writing-identity.md) for voice, guardrails, and lexicon.

If a required component has no canon entry, mark the affected section as a gap and say so.
Never invent messaging to fill it.

## Asks the human

One at a time, and only what context cannot hold:

1. **Format.** Product, solution, integration, or vertical? (See [one-pager-formats.md](one-pager-formats.md).)
2. **Subject.** Which product, which integration partner, or which vertical?
3. **CTA.** The next step, and whether a QR code or URL belongs on the page.
4. **Page size.** US Letter or A4?

## Workflow

1. Read the canon components and visual identity listed above. Note any gaps.
2. Ask the four questions.
3. Pick the format's layout from [one-pager-formats.md](one-pager-formats.md) and fill each section from canon language, enforcing the word counts in the reference file. If a section runs over, cut, never shrink the type.
4. Render the one-pager per [rendering.md](../rendering.md): a `pptxgenjs` build on a page-sized custom layout (US Letter or A4), the visual identity mapped to color constants and the brand fonts, the format's section allocation laid out to the percentages in the reference file. Export to PDF when LibreOffice is available.
5. Run content and visual QA per [rendering.md](../rendering.md). Write a short companion `.md` beside the file logging any canon gaps.
6. Run the checklist and hand back the file path.

## Checklist

- Exactly 3 benefits; more dilutes
- Every word count in the reference file is respected
- The hero states an outcome, not a hedge ("helps you improve" is a hedge)
- Proof band uses real canon proof; no generic "trusted by leading companies" lines
- CTA is visible on the page, not buried
- All copy comes from canon language; nothing invented; no banned terms or em/en dashes survive the content QA
- The rendered file is page-sized, on-brand, and QA'd (visual pass run, or its absence stated in the handoff)
