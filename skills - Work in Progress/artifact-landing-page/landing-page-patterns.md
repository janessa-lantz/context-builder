# Landing Page Patterns

Reference for [artifact-landing-page](SKILL.md). Page anatomy, hero formulas, conversion
benchmarks, and testing priorities.

## The 7-section anatomy

Each section has one job. A high-intent visitor reads the whole page in 60 to 70 seconds;
low-intent visitors bounce at sections 1 to 3, and that is fine.

| # | Section | Job |
|---|---|---|
| 1 | Hero | "Am I in the right place, and do I want this?" in 3 seconds |
| 2 | Problem | trigger "yes, that's my pain" recognition |
| 3 | Solution bridge | how the offer moves them from pain to outcome |
| 4 | Value proof | concrete outcomes that justify converting |
| 5 | Social proof | de-risk: "people like me use this" |
| 6 | Objection handler (FAQ) | answer the 2 or 3 reasons they would bounce |
| 7 | CTA block | recapture attention and convert |

## Hero formulas

- **Outcome-led** (demo requests, competitive campaigns): H1 states the specific outcome the buyer wants; subhead says how it is delivered plus the audience qualifier; CTA books the demo.
- **Problem-led** (content downloads, diagnostics): H1 is a punchy problem statement or question; subhead names what the download delivers; CTA gets the asset.
- **Category-led** (free trials, established categories): H1 is "the [category] for [audience]"; subhead differentiates from the category norm; CTA starts free.

## Conversion benchmarks (B2B SaaS, 25th to 75th percentile)

| Page type | Expected | Red flag |
|---|---|---|
| Demo request, brand-aware direct traffic | 3 to 7% | under 1.5% |
| Demo request, paid traffic | 1 to 3% | under 0.5% |
| Free trial, direct | 5 to 15% | under 2% |
| Gated content download | 10 to 25% | under 5% |
| Webinar registration | 15 to 35% | under 8% |

Sources: WordStream, Unbounce, and Databox B2B benchmarks. Below the red flag, the page is
broken; fix hero, CTA, and form friction before anything else.

## Mobile non-negotiables

30 to 50% of B2B landing traffic is mobile (higher for downloads, lower for demos).

- H1 readable at 375px without horizontal scroll
- Primary CTA tappable (44x44px minimum) and above the fold
- Form fields stacked, never side by side
- Logo bar scrolls horizontally rather than shrinking
- FAQ accordions collapsed by default

## Testing priorities

In impact order, assuming enough volume to test at all:

1. Hero H1 (outcome-led vs. problem-led framing)
2. CTA copy
3. Form length
4. Proof placement (logo bar high vs. dedicated section)
5. Page length (short vs. full 7 sections)

Do not test colors, button shapes, or secondary micro-copy; the effect sizes are noise.

## Anti-patterns

- Six or more form fields on a download page; ask for email and role, enrich the rest
- A hero that is clever before it is clear
- Multiple competing CTAs above the fold
- Generic proof with no logos or numbers
- Defensive FAQ answers
- Stock photography
- Hero videos; above-the-fold content should render in under 2 seconds
