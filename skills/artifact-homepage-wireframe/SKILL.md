---
name: artifact-homepage-wireframe
description: Use when asked to build a homepage wireframe, mock up a company's homepage, or lay out site information architecture. Produces a black-and-white, IA-focused wireframe of the homepage (plus linked page skeletons) with copy from the messaging canon, then deploys it to S3 as a shareable link. Distinct from artifact-landing-page (a brand-designed campaign page); this is the main-site homepage, wireframe-first.
---

# Artifact: Homepage Wireframe

Builds a structural, black-and-white wireframe of a company's homepage from approved messaging.
The point is information architecture and messaging, not visual design. Output is a set of
linked single-file HTML pages with working internal links, deployed to the user's S3 bucket as
a shareable URL. A human reviews it before any design happens.

Read [homepage-wireframe-patterns.md](homepage-wireframe-patterns.md) before building. It holds
the craft this skill applies: the locked section pattern, the copy discipline, the build
scaffold, and the deploy recipe.

## Reads from context

From the [canon](../../context/messaging-canon.md), by component ID:

- `positioning`, `company-description`: the hero headline and audience framing
- `point-of-view`, `narrative`: the reader-voice opening and the "why it's better" per section
- `products`, `value-proposition`, `how-it-works`: the per-product sections
- `unique-attributes`: each product's OWN "why it's better", one per section, never reused
- `icp`, `buying-committee`: who each section is for
- `customer-proof`, `key-metrics`: proof points and stats used inside benefits

Plus [brand-writing-identity](../../context/brand-writing-identity.md): the voice rules and
banned terms to enforce.

This skill deliberately does **not** read the visual identity. A wireframe has no brand colors,
fonts, or imagery; design comes after the IA and copy are approved. If you reach for
`brand-visual-identity.md`, stop. Theming a wireframe defeats its purpose.

If a section's claim has no canon entry, flag it as a gap. Never invent proof, claims, or numbers.

## Asks the human

One at a time, and only what context cannot hold:

1. **The information architecture.** The top-nav items, dropdown children, and footer columns.
   Ask them to sketch or list it. Reflect the live site's IA back only as a starting point. Do
   not invent nav.
2. **Scope.** Homepage in depth first, or the full skeleton (every nav and footer target as a
   thin page)? Default: homepage deep, the rest wired but thin.
3. **Hero audience.** The one audience the headline addresses across all products (operators,
   founders, RevOps).
4. **The products or pillars.** Which sections, in what order. Confirm the order; the canon
   narrative may argue for a different one.
5. **Pages to align to.** If a product has a live page, get the URL and align that section's
   headline, subhead, and pillars to it.

## Workflow

1. Read the canon components above and the patterns file. Note gaps.
2. Ask the questions, one at a time.
3. Build the chrome once: red IA-disclaimer banner, WIREFRAME tag, top nav from the human's IA
   (dropdowns working on hover), footer mirroring the IA. Wire every nav and footer link to a
   real future filename so links light up as pages get built.
4. Build the hero: one audience-framed headline true across all products, a reader-voice
   positioning subhead, one primary CTA, an optional credibility stamp.
5. Build each product section to the locked pattern: eyebrow, headline, one who/what/why
   subhead, three benefit cards (no label, no numbers), CTA row. Pull each section's "why it's
   better" from that product's own entry in `unique-attributes`. Vary the body to a top-five
   directory list for catalog sections.
6. Render and open after each piece (`open <file>` on macOS). Show it, wait for the reaction,
   change one thing at a time. Cut chrome by default (see the patterns file's cut list).
7. When the homepage is approved, deploy: upload the HTML as-is via the pretty-page uploader
   under a stable project key prefix. Hand back the public URL and note that it is public.
8. Build the remaining skeleton pages on the same chrome when asked; upload under the same
   prefix so internal links resolve.

## Checklist

- Top red banner present: "The primary purpose of this exercise is to show information
  architecture. No copy is final."
- Black and white only. No brand colors, fonts, or real images; hatched placeholders for imagery.
- Nav and footer match the human's IA exactly; every link points to a real filename in the set.
- Hero headline is audience-framed and true across all products; the opening is reader-voice,
  not company-voice.
- Each section: eyebrow, headline, ONE subhead carrying who it's for plus what it does plus why
  it's better, three benefits (no "Benefits" label, no numbers), CTA.
- No two sections share a "why it's better"; each uses its own unique attribute.
- No em dashes; no banned canon terms; specific over general.
- Chrome is lean: no section counters, no redundant labels, no filler second sentences.
- Deployed via pretty-page `upload.py` (not the renderer), HTML unchanged, under a project
  prefix; public URL handed back with the public-access caveat.
