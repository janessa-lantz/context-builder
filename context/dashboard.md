# Dashboard — Mintlify

*Compiled by the [analyzer](../builder/jobs/analyzer.md). Do not edit; regenerate. Every
deployment renders these same sections and the same columns — only the deployment name and
the counts differ. This is the home view: start here, then follow the links.*

deployment: Mintlify (mintlify.com) · compiled: 2026-07-07 · components_version: 2

## Vitals

| measure | count | open it |
|---------|-------|---------|
| Claims | 81 — 71 canon, 10 candidate, 0 retired | [claims.md](claims.md) |
| Evidence | 94 — 94 public, 0 private | [evidence.md](evidence.md) |
| Sources parsed | 25 — 14 key pages, 11 owned | [ingestion log](../builder/jobs/ingestion-log.md) |
| Open issues | 8 | [issues](../builder/issues/) |
| Coverage detail | 26 components | [claims-map.md](claims-map.md) |

## Canon by group

| group | canon | candidate | gaps (components with no claims) | view |
|-------|-------|-----------|----------------------------------|------|
| Who We Are | 11 | 1 | — | [canon-who-we-are](canon-who-we-are.md) |
| What We Do | 36 | 6 | — | [canon-what-we-do](canon-what-we-do.md) |
| Who It's For | 3 | 1 | buying-committee | [canon-who-its-for](canon-who-its-for.md) |
| Proof | 15 | 2 | — | [canon-proof](canon-proof.md) |
| Pricing | 6 | 0 | — | [canon-pricing](canon-pricing.md) |
| Themes | 0 | 0 | themes, topics, campaigns (deferred to owned-content analysis) | [canon-themes](canon-themes.md) |

## Material and compositions

| register / slice | rows | what it holds | open it |
|------------------|------|---------------|---------|
| Content | 25 | published pages and the claims each carries | [registers/content.md](registers/content.md) |
| Customer proof | 11 | case studies, quotes, logos | [registers/customer-proof.md](registers/customer-proof.md) |
| Features | 17 | capabilities and features, by product | [registers/features.md](registers/features.md) |
| Offers | 4 | free tier, credits, startup programs | [registers/offers.md](registers/offers.md) |
| Lockups | 0 approved | composed units of messaging | [lockups.md](lockups.md) |
| Entry points | 0 approved | on-ramps by persona, technology, integration | [entry-points.md](entry-points.md) |

## What needs attention

| id | kind | component | the gap |
|----|------|-----------|---------|
| iss-001 | misaligned | category-name | "knowledge infrastructure" (homepage) vs "AI-native documentation platform" (docs, Trieve post, comparison) — repositioning hasn't propagated |
| iss-002 | missing | value-drivers | revenue / demand-channel story lives only on one blog post, no key page |
| iss-003 | missing | founder-story | no About page on the domain; origin lives off-site and in blog posts |
| iss-004 | misaligned | key-metrics | scale stats drift across surfaces (20k vs 10k companies; Anthropic 2M vs 1.5M devs) |
| iss-005 | missing | buying-committee | zero claims for anyone but the champion, despite pricing-FAQ objection signals |
| iss-006 | process | company-description | synthesis-vs-verbatim spec gap for LLM-composed claims |
| iss-007 | process | pricing-model | Pro price rendered as placeholder digits to the scraper |
| iss-008 | missing | positioning | strongest support line ("two readers now") only on contact-sales |

→ full backlog with confidence and evidence: [builder/issues/](../builder/issues/)

## How this was built

`setup → parser (claims + evidence + registers) → analyzer (issues + map + canon views + this
dashboard)`. The rule that holds it together: the builder writes context, skills read it. See
[AGENTS.md](../AGENTS.md) for the operating model.
