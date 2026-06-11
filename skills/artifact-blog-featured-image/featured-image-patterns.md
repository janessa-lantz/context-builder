# Featured Image Patterns

Reference for [artifact-blog-featured-image](SKILL.md). Conventions, style archetypes, and
text-on-image rules.

## Conventions

- Hero: 1200 x 630 (1.91:1). Doubles as the Open Graph default, so it competes in feeds too.
- Social share variant: 1200 x 1200. LinkedIn and X favor square cards in feed over landscape.
- Safe zone: critical elements inside the center 80%; platforms crop edges.
- File size: under 200KB; WebP or optimized JPEG.

The hero and the share card have different jobs. The hero sets tone for a reader already on
the page and can be subtle; the share card fights for a click and must decode in 2 to 3
seconds, usually with denser composition and a text overlay.

## Five style archetypes

Pick one per blog category and apply it to every post in that category. Consistency builds
recognition; per-post variety reads as no design system at all.

1. **Abstract geometric.** Bold flat shapes in brand colors, generous whitespace, concept hinted rather than illustrated. The B2B SaaS default; fits product and engineering content.
2. **Illustrated metaphor.** Custom flat illustration, metaphor-led, warm. Fits how-to, education, and customer-success content.
3. **Photo with overlay.** Editorial photo under a brand-color overlay at 30 to 60% opacity. Journalistic; fits customer stories and executive commentary. Skip it without access to photography that does not read as stock.
4. **Data-viz inspired.** A stylized chart or plausible dashboard crop in brand colors. Fits research, benchmarks, and data-led thought leadership.
5. **Typographic.** Oversized display type is the visual. Editorial and premium; fits opinion and manifesto content.

A typical category mapping: product updates take geometric, how-to takes illustration,
customer stories take photo-overlay, research takes data-viz, opinion takes typographic.

## Text-on-image rules

For share-card overlays:

- 6 words or fewer; needing more means rethinking the concept
- Bold or black weight; regular weights read unstable over imagery
- Contrast passes WCAG AA against the immediate background (4.5:1, or 3:1 for very large display type)
- At least 80px from every edge
- Legible scaled to 300px wide

Skip the overlay when the platform pulls the post title anyway, when text would fight a
metaphor-driven image, or when the brand style is minimalist.

## Anti-patterns

- Stock photography that reads as stock (handshakes, teams at laptops)
- Soft gradients; they read as low-effort or AI-generated
- A different visual style for every post
- The logo as focal point; the URL already signals the brand
- Full-bleed brand color with nothing else; reads as a placeholder
- Illegible or low-contrast overlay text
