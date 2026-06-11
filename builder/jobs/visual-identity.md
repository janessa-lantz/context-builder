# Visual Identity Job

A job you run to build or refresh [context/visual-identity.md](../../context/visual-identity.md).
It is the visual counterpart to the key-pages flow: where the parser extracts what the company
says from its key pages, this job extracts what the company looks like from the same pages.
Run it at setup, after a redesign, or when generated assets start looking off-brand.

## The run

1. Take the key-page targets from the [key-pages scan](scans/key-pages.md). The homepage and
   one or two content-rich pages are usually enough; visual identity is consistent by design.
2. Extract the observable design facts:
   - **colors**: from CSS custom properties and computed styles. Classify by role (primary,
     accent, neutrals) based on observed usage, not guesswork. Note the rough proportions.
   - **typography**: font families from CSS, split by display and body usage. Weights and
     scale as observed.
   - **logo**: the file in use (header, favicon, og:image), its variants, and how it is
     treated against light and dark backgrounds.
   - **style**: illustration vs. photography vs. geometric graphics, icon style, chart
     conventions, and any per-category image pattern visible on the blog.
3. Write each finding to [context/visual-identity.md](../../context/visual-identity.md),
   attributed to the URL where it was observed and dated.
4. Never overwrite an entry marked `source: human`. On a re-run, refresh the observed entries
   and flag any conflict between a new observation and a human entry rather than resolving it.

## What this job cannot see

The live site shows what is present, not what is forbidden or aspired to. The `avoid` and
`admired-references` sections are human-authored, and print or deck conventions that never
appear on the web need a human to add them. Leave those sections alone and note when they are
empty; an empty `avoid` section means a human has not weighed in yet, not that anything goes.
