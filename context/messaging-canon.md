# Messaging Canon

Your company's approved messaging, split by group into six files. Fill each in and keep it current; this is the source your team and your AI tools draw from. Each entry is verbatim from a live published surface (source noted) or human synthesis (marked `source: human`); the LLM fills only verbatim entries and never overwrites a human-authored one. See the [README](README.md) for what each component is.

- [Who We Are](canon-who-we-are.md): point-of-view, narrative, positioning, founder-story, company-description
- [What We Do](canon-what-we-do.md): category-name, products, unique-attributes, value-proposition, how-it-works, ecosystem-integrations
- [Who It's For](canon-who-its-for.md): icp, buying-committee, value-drivers
- [Proof](canon-proof.md): customer-proof, market-proof, key-metrics
- [Pricing](canon-pricing.md): pricing-model, packaging, add-ons-services, offers
- [Themes](canon-themes.md): themes, topics, campaigns

Voice, guardrails, and lexicon live in [brand-writing-identity.md](brand-writing-identity.md). Visual conventions live in [brand-visual-identity.md](brand-visual-identity.md).

## Entry format

Write each entry the way an analyst reports evidence: a short synthesis lead where it helps the reader, then the verbatim copy with its source noted inline. An example, drawn from a real extraction:

> ### positioning
>
> - Primary: "Ship quality AI at scale" (homepage hero)
> - Supporting: "AI observability and eval platform for production AI" (manifesto footer, consistent across the site)
> - Category label: "AI observability platform" (nav and meta)
>
> Lead with quality, not observability; the category label is for the nav and analysts, not the hero.
> source: human, 2026-07-02

What the example shows:

- **Quoted text is verbatim** from a live page, with the page noted in parentheses. These are the entries the LLM writes and refreshes on a re-scan.
- **Labeled bullets rank the evidence.** The primary claim is the canonical statement; the rest is supporting.
- **A plain paragraph marked `source: human` is human synthesis.** The LLM never edits or overwrites it.
- **Absence is written down** ("No founder story found on key pages"), never padded over.
- Components the LLM composes rather than quotes (`company-description`, `icp`) are labeled "synthesis" with the pages they draw from.
