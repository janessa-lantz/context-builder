---
name: artifact-one-pager
description: Use when asked to build a one-pager, solution brief, integration sheet, or vertical leave-behind. Generates a layout spec with copy and a design-generation prompt for a print-ready PDF from the messaging canon and visual identity.
---

# Artifact: One-Pager

Generates a print-ready one-pager draft from approved context: a layout spec with copy per
section, and a design-generation prompt. A human reviews it before it ships.

## Reads from context

From the [canon](../../context/messaging-canon.md), by component ID:

- `positioning`, `category-name`: the header and hero
- `product`, `capabilities`: the body, scoped to the format
- `benefits`, `value-drivers`: the benefit grid, framed as outcomes
- `customer-proof`, `key-metrics`: the proof band
- `ecosystem-integrations`: required for the integration format
- `account`: required for the vertical format (the industry framing)
- `jobs-to-be-done`: the problem statement, in the customer's words

And the full [visual identity](../../context/visual-identity.md) for the generation prompt.

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
3. Pick the format's layout from [one-pager-formats.md](one-pager-formats.md) and populate each section from canon language, enforcing the word counts in the reference file. If a section runs over, cut, never shrink the type.
4. Present the layout spec: each section with its headline, body, and proof, plus the section allocation.
5. Build the design-generation prompt: the layout spec with the visual identity inlined, print-ready at the chosen page size.
6. Run the checklist.

## Checklist

- Exactly 3 benefits; more dilutes
- Every word count in the reference file is respected
- The hero states an outcome, not a hedge ("helps you improve" is a hedge)
- Proof band uses real canon proof; no generic "trusted by leading companies" lines
- CTA is visible in the spec, not buried
- All copy comes from canon language; nothing invented
- The generation prompt inlines the visual identity and the page size
