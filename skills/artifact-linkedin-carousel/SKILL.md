---
name: artifact-linkedin-carousel
description: Use when asked to build a LinkedIn carousel or document post. Generates slide-by-slide copy, a design-generation prompt for the PDF, and the accompanying post copy from the messaging canon and visual identity.
---

# Artifact: LinkedIn Carousel

Renders a carousel draft from approved context: a designed multi-slide document at 1080x1350,
in the brand's colors and type, plus the accompanying post copy. A human reviews it before it
ships. See [rendering.md](../rendering.md) for the build and QA mechanics.

## What this skill produces

A designed carousel rendered to a 1080x1350 `.pptx` (exported to PDF for the LinkedIn
document post when LibreOffice is available), in the visual identity, plus the post copy in a
companion `.md`. A draft for human review.

## Reads from context

From the [canon](../../context/messaging-canon.md), by component ID:

- `themes`, `topics`: the carousel must sit under an existing theme; if the requested topic matches none, say so before writing
- `point-of-view`: the thesis a thought-leadership carousel argues
- `lexicon`: coined terms to use correctly and banned terms to avoid
- `customer-proof`, `key-metrics`: evidence slides, where the argument needs them
- `jobs-to-be-done`, `objections`: the customer's framing of the problem, in their words

And the full [visual identity](../../context/brand-visual-identity.md) for the render.

## Asks the human

One at a time, and only what context cannot hold:

1. **Topic and thesis.** What is the carousel arguing? One sentence.
2. **Slide count.** 10 is the sweet spot; 8 to 12 acceptable.
3. **Ending.** CTA, recap, checklist, or question? (See the ending patterns in [carousel-patterns.md](carousel-patterns.md).) If there is no concrete offer, do not fake a CTA; recommend recap or checklist.

## Workflow

1. Read the canon components and visual identity listed above. Confirm the topic sits under a canon theme.
2. Ask the three questions.
3. Pick a hook formula from [carousel-patterns.md](carousel-patterns.md) that fits the thesis, and draft slide 1 to carry the whole argument.
4. Plan the remaining slides: one idea per slide, within the density limits in the reference file, at least 3 led by a visual element rather than text.
5. Draft the post copy: hook line matching slide 1, expansion, preview, and the interaction CTA. This goes in the companion `.md`.
6. Render the carousel per [rendering.md](../rendering.md): a `pptxgenjs` build on a 1080x1350 custom layout, visual identity mapped to color constants and brand fonts, one slide per plan row, the brand motif repeated. Export to PDF when LibreOffice is available.
7. Run content and visual QA per [rendering.md](../rendering.md), then the checklist, and hand back the file path.

## Checklist

- Slide 1 carries the thesis; no warm-up slides
- One idea per slide; headline 10 words or fewer, body 35 words or fewer
- No banned terms from `lexicon`; no em/en dashes survive the content QA
- At least 3 slides are visual-led
- Slide structures vary; not every slide is headline-plus-body
- The post's first line matches slide 1 (the hook match rule)
- Post is 100 to 250 words, hook inside the first 150 characters, 3 to 5 topical hashtags at the bottom
- All claims trace to canon language or cited evidence; nothing invented
- The rendered carousel is 1080x1350, on-brand, and QA'd (visual pass run, or its absence stated in the handoff)
