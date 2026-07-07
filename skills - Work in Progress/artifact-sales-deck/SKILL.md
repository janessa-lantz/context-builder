---
name: artifact-sales-deck
description: Use when asked to build a sales deck, pitch deck, demo follow-up deck, or executive brief. Generates a slide-by-slide outline, speaker notes, and a design-generation prompt from the messaging canon and visual identity.
---

# Artifact: Sales Deck

Renders a deck draft from approved context: a designed `.pptx` in the brand's colors and
type, slide by slide, with speaker notes in the notes pane. A human reviews it before it
ships. See [rendering.md](../rendering.md) for the build and QA mechanics.

## What this skill produces

A designed `.pptx` deck (16:9), rendered in the visual identity, with speaker notes in the
notes pane, plus a short companion `.md` logging any canon gaps. A draft for human review.

## Reads from context

From the [canon](../../context/messaging-canon.md), by component ID:

- `positioning`, `company-description`: the title slide and the through-line
- `point-of-view`, `narrative`: the shift and the why-now (pitch decks live on these)
- `products`, `unique-attributes`, `how-it-works`: the solution slides
- `value-proposition`, `value-drivers`: the promised land, framed as business outcomes
- `icp` (the champion's competitive alternatives): competitive framing where the meeting calls for it
- `customer-proof`, `market-proof`, `key-metrics`: the proof slides
- the objections in `icp` and `buying-committee`: what the deck should preempt
- `pricing-model`, `packaging`: the path-forward slide, when pricing belongs in the deck

And the full [visual identity](../../context/brand-visual-identity.md) for the render, plus
[brand-writing-identity](../../context/brand-writing-identity.md) for voice, guardrails, and lexicon.

If a component the chosen framework needs has no canon claims, say which slide is affected and
what is missing, build that slide as a clearly marked placeholder, and move on. Never invent
messaging to fill the gap.

## Asks the human

One at a time, and only what context cannot hold:

1. **Purpose.** First-call pitch, demo follow-up, or executive brief?
2. **The room.** Which prospect or segment, and who specifically will see this?
3. **Slide count.** See the guidance in [deck-frameworks.md](deck-frameworks.md); push back on 20+ slides for a pitch.
4. **CTA.** The next step the deck drives to.

## Workflow

1. Read the canon components and visual identity listed above. Note any gaps.
2. Ask the four questions.
3. Pick the framework by purpose (see [deck-frameworks.md](deck-frameworks.md)): pitch takes Raskin, demo follow-up takes Problem-Agitate-Solve, executive brief takes Challenger.
4. Plan the slides: for each, a role, a concrete headline (never "TBD"), body copy from canon language, and a visual treatment. This plan is internal scaffolding for the build, not the deliverable.
5. Write speaker notes, 2 to 3 sentences per slide: what to emphasize, what to skip, the transition to the next slide. These go in the `.pptx` notes pane.
6. Render the deck per [rendering.md](../rendering.md): a `pptxgenjs` build at `LAYOUT_16x9`, the visual identity mapped to color constants and the brand fonts, one slide per plan row, the brand motif repeated, speaker notes added with `slide.addNotes`. Title and closing slides full-bleed in the brand's dark and primary colors.
7. Run content and visual QA per [rendering.md](../rendering.md). Write a short companion `.md` beside the deck logging any canon gaps the build had to mark.
8. Run the checklist and hand back the file path.

## Checklist

- Framework matches the stated purpose
- Every headline is concrete; the only placeholders are marked canon gaps
- Every slide has a visual treatment, not a bare title and bullets
- At least two slides carry proof from `customer-proof`, `market-proof`, or `key-metrics`
- The closing slide carries the CTA
- All copy comes from canon language; nothing invented; no banned terms or em/en dashes survive the content QA
- The rendered `.pptx` is 16:9, on-brand, and QA'd (visual pass run, or its absence stated in the handoff)
