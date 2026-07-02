---
name: artifact-blog-featured-image
description: Use when asked to create a blog hero image, featured image, or social share card for a post. Generates an image concept and a design-generation prompt from the visual identity, keyed to the post's category.
---

# Artifact: Blog Featured Image

Generates a featured-image draft for a blog post: a concept description and a
design-generation prompt for the hero (1200x630) and an optional social share card
(1200x1200). A human reviews it before it ships.

## Reads from context

- The full [visual identity](../../context/brand-visual-identity.md), especially the `style`
  section. If `style` records an image treatment per blog category, inherit it; editorial
  consistency within a category beats per-post novelty.
- From the [canon](../../context/messaging-canon.md): `themes` and `topics`, to confirm where
  the post sits. From [brand-writing-identity](../../context/brand-writing-identity.md): the
  `lexicon` for any text overlay.

If `style` has no per-category treatment yet, propose one from the archetypes in
[featured-image-patterns.md](featured-image-patterns.md) and flag it for a human to record in
the visual identity, so the next post in this category inherits it. Do not record it
yourself.

## Asks the human

One at a time, and only what context cannot hold:

1. **The post.** Title and category (or a link to the draft).
2. **Share card.** Hero only, or hero plus the 1200x1200 social variant?
3. **Text overlay.** None, or up to 6 words on the share card? (The hero usually needs none; the title renders above it on the page.)

## Workflow

1. Read the visual identity and confirm the post's category treatment.
2. Ask the three questions.
3. Pick the style archetype: the category's recorded treatment, or your flagged proposal.
4. Write the concept: archetype, composition, focal point, color application, and the text overlay if any.
5. Build the design-generation prompt: dimensions per deliverable, visual identity inlined, the concept spelled out, safe zones respected.
6. Run the checklist.

## Checklist

- The archetype matches the category's recorded treatment, or the deviation is flagged
- One focal point; 1200x630 is too small for complex composition
- Text overlay (if any) is 6 words or fewer, bold weight, and passes contrast against its background
- No stock-photo look, no soft gradients, no logo as the focal point
- The share card variant works in 2 to 3 seconds; the hero may be subtler
- The generation prompt inlines the visual identity and exact dimensions
