---
name: artifact-sales-deck
description: Use when asked to build a sales deck, pitch deck, demo follow-up deck, or executive brief. Generates a slide-by-slide outline, speaker notes, and a design-generation prompt from the messaging canon and visual identity.
---

# Artifact: Sales Deck

Generates a deck draft from approved context: a slide-by-slide outline, speaker notes, and a
paste-ready design-generation prompt. A human reviews it before it ships.

## Reads from context

From the [canon](../../context/messaging-canon.md), by component ID:

- `positioning`, `company-description`: the title slide and the through-line
- `point-of-view`, `narrative`: the shift and the why-now (pitch decks live on these)
- `product`, `capabilities`, `how-it-works`: the solution slides
- `benefits`, `value-drivers`: the promised land, framed as business outcomes
- `differentiators`: competitive framing where the meeting calls for it
- `customer-proof`, `market-proof`, `key-metrics`: the proof slides
- `objections`: what the deck should preempt
- `pricing-model`, `packaging`: the path-forward slide, when pricing belongs in the deck

And the full [visual identity](../../context/visual-identity.md) for the generation prompt.

If a component the chosen framework needs has no canon entry, say which slide is affected and
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
4. Build the slide outline: a table of slide number, role, headline, body direction, and visual direction. Headlines are concrete, never "TBD."
5. Write speaker notes, 2 to 3 sentences per slide: what to emphasize, what to skip, and the transition to the next slide.
6. Build the design-generation prompt: 16:9, the slide-by-slide spec, and the visual identity inlined (colors, typography, logo rules, style, usage notes).
7. Run the checklist.

## Checklist

- Framework matches the stated purpose
- Every headline is concrete; the only placeholders are marked canon gaps
- Every slide has visual direction, not "design something"
- At least two slides carry proof from `customer-proof`, `market-proof`, or `key-metrics`
- The closing slide carries the CTA
- All copy comes from canon language; nothing invented
- The generation prompt inlines the visual identity and specifies 16:9 and export formats
