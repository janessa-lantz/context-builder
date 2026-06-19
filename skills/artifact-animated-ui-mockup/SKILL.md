---
name: artifact-animated-ui-mockup
description: Use when asked to build an animated UI mockup for a landing page hero, product launch, or social post. Generates an animation concept and a standalone HTML file with CSS animations, from the product canon and visual identity.
---

# Artifact: Animated UI Mockup

Generates a fake UI in motion: an animation concept and a standalone HTML file (inline CSS,
no frameworks, no external dependencies) that embeds anywhere. For showing what the product
feels like; for recording the real product, recommend a demo tool instead (see the
out-of-scope table in [ui-animation-patterns.md](ui-animation-patterns.md)).

## Reads from context

From the [canon](../../context/messaging-canon.md), by component ID:

- `product`, `capabilities`, `how-it-works`: what the fake UI should plausibly show; the mockup must depict a workflow the product actually has
- `lexicon`: labels and terms inside the mock UI use the company's language

And the full [visual identity](../../context/brand-visual-identity.md): the mock UI is rendered in
the brand's colors and type, with accent restraint.

If `how-it-works` has no canon entry, ask the human to describe the workflow and flag the
gap; do not invent product behavior.

## Asks the human

One at a time, and only what context cannot hold:

1. **The moment.** Which workflow or feature is the animation showing, and what should the viewer conclude?
2. **The destination.** Landing page hero, in-page section, or social (which becomes an MP4 screen recording)? This sets dimensions and the file-size budget.
3. **The data.** Plausible fictional data, or real customer names with permission? Obvious placeholder data reads as a template.

## Workflow

1. Read the canon components and visual identity listed above.
2. Ask the three questions.
3. Pick the animation pattern from [ui-animation-patterns.md](ui-animation-patterns.md) that matches what the feature suggests (data populating, dashboard reveal, pipeline flow, or state change).
4. Write the concept: pattern, the sequence with timings, easing, and where the single accent lands.
5. Build the HTML: one file, inline CSS keyframes, the brand's fonts and colors, `prefers-reduced-motion` respected, total size within the reference file's budget.
6. Run the checklist, then state how to embed it for the chosen destination (see the embedding section of the reference file).

## Checklist

- The depicted workflow exists per `how-it-works`; nothing invented
- 3 to 5 second hero sequence with a clean fade-out loop, no jarring reset
- Easing follows the reference file (ease-out on enters, ease-in on exits); nothing linear except continuous flows
- One accent color on one element; the rest neutral
- Mock data looks plausible; UI labels use `lexicon` terms
- `prefers-reduced-motion` shows the final state statically
- Single file, no external dependencies, within the size budget
- No audio
