---
name: artifact-paid-ad-creative
description: Use when asked to build paid ad creative for LinkedIn or Meta. Generates a multi-variant concept table across distinct angles and a design-generation prompt, from the messaging canon and visual identity.
---

# Artifact: Paid Ad Creative

Generates an ad-variant set from approved context: a concept table (angle, copy, visual
direction per variant) and a design-generation prompt that produces the full set. A human
reviews it before anything runs.

## Reads from context

Each ad angle maps to specific canon components (see the mapping in
[ad-patterns.md](ad-patterns.md)):

- `customer-proof`, `key-metrics`: social proof and customer story angles
- `differentiators`: the comparison angle
- `jobs-to-be-done`, `objections`: the problem/solution angle, in the customer's words
- `point-of-view`, `founder-story`: the founder POV angle
- `positioning`, `benefits`: the claim and supporting copy throughout
- `offers`: what the ad drives to, when a free tier or trial is the destination
- `buying-committee`, `account`: who the targeting should reach

And the full [visual identity](../../context/visual-identity.md) for the generation prompt.

An angle whose components have no canon entry is dropped from the set, and the drop is
stated. Never invent proof, stats, or customer stories.

## Asks the human

One at a time, and only what context cannot hold:

1. **Objective and funnel stage.** Awareness, demand capture, or competitive takeaway? This selects the angles.
2. **Platforms.** LinkedIn (1200x627), Meta (1080x1080), or both?
3. **Destination.** The page or offer the ads drive to, and the CTA button label.
4. **Volume.** Default is 6 variants (3 per platform); algorithms starve below that.

## Workflow

1. Read the canon components and visual identity listed above.
2. Ask the four questions.
3. Select angles by funnel stage from [ad-patterns.md](ad-patterns.md), each variant a different angle. Never 6 variants of one angle.
4. Build the concept table: variant, platform, angle, headline, body, CTA, and visual direction, within each platform's copy limits.
5. Build the design-generation prompt: the full set in one pass, visual identity inlined, exact dimensions per platform.
6. Run the checklist.

## Checklist

- Every variant is a distinct angle
- Copy respects each platform's limits (see the reference file)
- Every claim and stat traces to a canon entry; nothing invented
- Accent color appears on one element per creative, not everywhere
- CTA labels are platform defaults ("Learn more," "Download," "Sign up")
- The generation prompt specifies exact dimensions per platform
- The handoff notes include the testing guidance from the reference file (rotation, decay signals)
