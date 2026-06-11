# UI Animation Patterns

Reference for [artifact-animated-ui-mockup](SKILL.md). Four animation patterns, motion
principles, embedding guidance, and performance budgets.

## Four patterns

Match the pattern to what the feature suggests.

1. **Data populating.** Rows or cards fade in sequentially, as if the system is working. Suggests live data and processing. Shell visible at t=0, first row at 0.3s, then staggered 200ms apart up to 5 to 7 rows, optional highlight on the key row, fade-out loop. For dashboards, lists, and analytics.
2. **Dashboard reveal.** Sections slide in staggered: main KPI card first, supporting cards 100ms apart, the chart last, settled by about 2.5s. Suggests a comprehensive, polished view. For homepage heroes of dashboard products.
3. **Pipeline flow.** Items move through visible stages, new ones entering as others advance, continuous loop. Suggests process automation and visibility. For workflow, pipeline, and funnel products.
4. **State change.** One interaction: a simulated click, a loading state, a success state, settle, loop. Suggests responsiveness and polish. For single-feature callouts.

## Motion principles

Violating these makes an animation feel wrong even when the viewer cannot say why.

- **Easing.** Enters decelerate: `ease-out` or `cubic-bezier(0.16, 1, 0.3, 1)`. Exits accelerate: `ease-in`. Continuous flows take `ease-in-out` or `linear`. Springs read juvenile for enterprise; use sparingly.
- **Duration.** Micro-interactions 100 to 200ms; component enters 200 to 400ms; section reveals 400 to 600ms; the full hero sequence 3 to 6 seconds; loop resets fade 300 to 500ms.
- **Stagger.** Multiple items animate 50 to 100ms apart. Synchronized reads mechanical; over-staggered reads slow.
- **Reduced motion.** Respect `prefers-reduced-motion: reduce` with a media query that jumps every animation to its final state.

## Embedding

- **Webflow / Framer**: code embed component, or host and iframe.
- **Static sites and most CMSs**: drop the HTML in directly, or iframe a hosted copy.
- **Notion**: no arbitrary HTML; screen-record to MP4 and upload the video.
- **Landing pages**: direct embed is cleanest. Below the fold, lazy-load with Intersection Observer; above the fold, keep total size under 200KB.
- **Social**: screen-record to MP4; 1080x1080 or 1080x1350 for LinkedIn.

## Performance budget

- Under 500KB total as a standalone file; under 200KB when above the fold on a landing page
- CSS keyframes only; no animation libraries (they cover 90% of cases at zero bytes)
- Web-font links cost 50 to 100KB; fall back to system fonts when the budget is tight

## Out of scope: recommend instead

This skill fakes a UI in motion. For the real product:

| Need | Tool |
|---|---|
| Interactive demo of the actual UI | Arcade |
| Narrated walkthrough | Loom |
| Branching product tours | Navattic, Storylane |
| In-app onboarding | Appcues, Userpilot, Intro.js |

## Anti-patterns

- Sequences over 6 seconds
- Everything animating at once
- Linear easing on enters
- A loop that jumps instead of fading
- Brand color on every element; one accent reads premium
- Placeholder-obvious fake data
- Autoplay audio, ever
