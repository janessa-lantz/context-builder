---
name: artifact-landing-page
description: Use when asked to build a campaign landing page. Generates a 7-section wireframe with copy, a design-generation prompt for a visual mockup, and optionally deploy-ready HTML, from the messaging canon and visual identity.
---

# Artifact: Landing Page

Generates a campaign landing page draft from approved context: a 7-section wireframe with
copy, a design-generation prompt for the visual mockup, and (when asked) deploy-ready
single-file HTML with embedded CSS. A human reviews it before it ships.

## Reads from context

From the [canon](../../context/messaging-canon.md), by component ID:

- `positioning`, `benefits`: the hero and value sections
- `jobs-to-be-done`: the problem section, in the customer's words
- `capabilities`, `how-it-works`: the solution bridge
- `customer-proof`, `key-metrics`: the social proof section
- `objections`: the objection-handler / FAQ section; answer the real objections the canon records, directly, not in marketing-speak
- `offers`: the conversion offer, when a trial or free tier is the destination
- `buying-committee`: who the page is qualifying for

And the full [visual identity](../../context/visual-identity.md) for both outputs.

If a section's component has no canon entry, mark the section as a gap. Never invent proof,
objections, or claims.

## Asks the human

One at a time, and only what context cannot hold:

1. **Conversion goal.** Demo request, free trial, content download, or webinar registration? This selects the hero formula.
2. **The offer.** What exactly does the visitor get?
3. **Traffic source.** Paid clicks, organic, or outbound links? This sets how much context the hero must carry.
4. **Output.** Wireframe plus visual mockup prompt, deploy-ready HTML, or both?
5. **Form fields.** Which fields are non-negotiable for sales? Default to the minimum; every field costs conversion.

## Workflow

1. Read the canon components and visual identity listed above. Note any gaps.
2. Ask the five questions.
3. Pick the hero formula by goal (see [landing-page-patterns.md](landing-page-patterns.md)) and draft the 7 sections, each doing its one job, copy from canon language.
4. Present the wireframe with copy per section.
5. Build the requested outputs: the design-generation prompt with visual identity inlined, and/or the single-file HTML (semantic markup, mobile-first, no external dependencies beyond fonts).
6. Run the checklist.

## Checklist

- Hero answers "am I in the right place" in 3 seconds; clear before clever
- One primary CTA above the fold; at most one secondary
- The FAQ answers canon `objections` directly
- Proof is specific: named customers or quantified outcomes, no "trusted by leading companies"
- Form asks only the agreed fields
- Mobile: H1 readable at 375px, CTA tappable at 44x44px minimum and above the fold, fields stacked
- All copy comes from canon language; nothing invented
- HTML output (if any) is a single file, renders above-the-fold content fast, no hero video
