---
name: artifact-youtube-thumbnail
description: Use when asked to design YouTube thumbnails. Generates 3 thumbnail concepts with distinct CTR hypotheses and a design-generation prompt, from the visual identity.
---

# Artifact: YouTube Thumbnail

Generates 3 thumbnail concepts (1280x720), each with a distinct click-through hypothesis, and
a design-generation prompt producing all three. A human picks and tests; never assume one
concept wins.

## Reads from context

- The full [visual identity](../../context/brand-visual-identity.md). Note the caveat in
  [thumbnail-patterns.md](thumbnail-patterns.md): thumbnails run bolder and more saturated
  than the brand's web palette, so treat the identity as the base to push from, not a cage.
- From [brand-writing-identity](../../context/brand-writing-identity.md): `lexicon` for any
  words on the thumbnail. From the [canon](../../context/messaging-canon.md): `themes`/`topics`
  to confirm the video sits in the company's content territory.

## Asks the human

One at a time, and only what context cannot hold:

1. **The video.** Title and the one-sentence take it argues.
2. **Faces.** Is there a presenter or guest photo available? (Face-led patterns outperform for creator and interview content, but need a real photo.)
3. **The feed.** What do this channel's existing thumbnails and the competition's look like? Pattern interrupt depends on what surrounds the thumbnail.

## Workflow

1. Read the visual identity and the canon components above.
2. Ask the three questions.
3. Pick 3 different patterns from [thumbnail-patterns.md](thumbnail-patterns.md), each with a stated hypothesis for why it earns the click (curiosity gap, stat shock, transformation, and so on).
4. Write each concept: pattern, composition, color treatment, text (4 words maximum), and the hypothesis.
5. Build the design-generation prompt: all 3 variants at 1280x720, visual identity as the base, per-concept specs.
6. Run the checklist, including the 300px legibility test on each concept.

## Checklist

- Three genuinely different patterns, not one pattern in three colorways
- Each concept states its CTR hypothesis
- Text is 4 words or fewer, bold sans-serif, sized per the reference file
- Every concept passes the 300px test: text reads, focal point clear, stands out on a white feed
- No words that violate `lexicon`
- No stock photos, emoji, dominant logos, or gradients
