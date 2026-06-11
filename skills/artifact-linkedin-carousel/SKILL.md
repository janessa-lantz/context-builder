---
name: artifact-linkedin-carousel
description: Use when asked to build a LinkedIn carousel or document post. Generates slide-by-slide copy, a design-generation prompt for the PDF, and the accompanying post copy from the messaging canon and visual identity.
---

# Artifact: LinkedIn Carousel

Generates a carousel draft from approved context: slide-by-slide copy, a design-generation
prompt for the 1080x1350 PDF, and the accompanying post copy. A human reviews it before it
ships.

## Reads from context

From the [canon](../../context/messaging-canon.md), by component ID:

- `themes`, `topics`: the carousel must sit under an existing theme; if the requested topic matches none, say so before writing
- `point-of-view`: the thesis a thought-leadership carousel argues
- `lexicon`: coined terms to use correctly and banned terms to avoid
- `customer-proof`, `key-metrics`: evidence slides, where the argument needs them
- `jobs-to-be-done`, `objections`: the customer's framing of the problem, in their words

And the full [visual identity](../../context/visual-identity.md) for the generation prompt.

## Asks the human

One at a time, and only what context cannot hold:

1. **Topic and thesis.** What is the carousel arguing? One sentence.
2. **Slide count.** 10 is the sweet spot; 8 to 12 acceptable.
3. **Ending.** CTA, recap, checklist, or question? (See the ending patterns in [carousel-patterns.md](carousel-patterns.md).) If there is no concrete offer, do not fake a CTA; recommend recap or checklist.

## Workflow

1. Read the canon components and visual identity listed above. Confirm the topic sits under a canon theme.
2. Ask the three questions.
3. Pick a hook formula from [carousel-patterns.md](carousel-patterns.md) that fits the thesis, and draft slide 1 to carry the whole argument.
4. Draft the remaining slides: one idea per slide, within the density limits in the reference file.
5. Draft the post copy: hook line matching slide 1, expansion, preview, and the interaction CTA.
6. Build the design-generation prompt: 1080x1350 PDF, slide-by-slide spec, visual identity inlined, with at least 3 slides led by a visual element rather than text.
7. Run the checklist.

## Checklist

- Slide 1 carries the thesis; no warm-up slides
- One idea per slide; headline 10 words or fewer, body 35 words or fewer
- No banned terms from `lexicon`
- At least 3 slides are visual-led
- Slide structures vary; not every slide is headline-plus-body
- The post's first line matches slide 1 (the hook match rule)
- Post is 100 to 250 words, hook inside the first 150 characters, 3 to 5 topical hashtags at the bottom
- All claims trace to canon language or cited evidence; nothing invented
