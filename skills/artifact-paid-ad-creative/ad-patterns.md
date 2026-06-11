# Ad Patterns

Reference for [artifact-paid-ad-creative](SKILL.md). Six B2B ad angles mapped to canon
components, platform specs and copy limits, and the testing framework.

## Six angles, mapped to canon

Match angle to funnel stage, and build each from the components listed.

| Angle | Pattern | Funnel stage | Canon components |
|---|---|---|---|
| Social proof | "Join [number] [target role]s" | Mid; aware but hesitant | `key-metrics`, `customer-proof` |
| Customer story | "How [customer] achieved [outcome]" | Mid to bottom; evaluating | `customer-proof` |
| Comparison | direct contrast with the alternative | Bottom; competitive takeaway | `differentiators` |
| Stat shock | big number plus implication | Top; awareness | `key-metrics` or cited research |
| Problem / solution | the pain in the customer's words, then the fix | Any; the workhorse | `jobs-to-be-done`, `benefits` |
| Founder POV | "I [experience]. Here's what I learned." | Top; brand | `founder-story`, `point-of-view` |

## Copy limits

LinkedIn sponsored content:

- Headline on the creative: 70 characters or fewer
- Body on the creative: 150 characters or fewer
- Text on at most 20% of the creative surface; more reads as a slide
- Post text: 100 to 200 characters, hook first

Meta feed:

- Headline on the creative: 40 characters or fewer (smaller viewport)
- Body on the creative: 125 characters or fewer
- Post text: 80 to 125 characters; Meta users read less than LinkedIn users
- Run Meta's text-overlay preview before launch

Both platforms: CTA buttons stay on platform defaults.

## Dimensions (as of 2026)

- LinkedIn single image: 1200 x 627 (1.91:1), JPG or PNG, max 5MB; keep critical copy out of the bottom 20% (mobile crop)
- LinkedIn square: 1200 x 1200
- Meta feed: 1080 x 1080 square, or 1080 x 1350 portrait (higher engagement), max 30MB
- Meta stories: 1080 x 1920; top and bottom 250px are UI-reserved

## Testing framework

- **Volume**: 6 creatives per campaign minimum (3 per platform); 9 to 12 ideal. A single creative starves the algorithm.
- **First 48 hours**: let the algorithm find the winner; do not pause variants early.
- **Days 3 to 14**: keep winners, pause losers (CTR under 0.5% on LinkedIn, under 1% on Meta).
- **Day 14+**: watch for decay; CTR typically falls 20 to 40% between weeks 2 and 4 on the same creative.
- **Decay signals**: CTR down 25%+ from peak, frequency above 3 to 4 per user, rising negative feedback. Refresh with new visuals and hooks, not a color swap.

## Testing pitfalls

- Testing several variables at once; isolate headline, visual, or CTA
- Reading results under 10K impressions; that is noise
- Assuming the LinkedIn winner wins on Meta; test separately
- Not segmenting results by audience; a creative that wins with one role can lose with another
