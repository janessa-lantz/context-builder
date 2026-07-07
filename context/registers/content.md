# Content Register

Your company-owned content, one row per asset. This is your findable asset library: which of
your published assets carries which messaging, down to the claim.

It answers "which of our assets support this messaging?" so anyone in sales or marketing can
find them. The builder populates it by running [jobs](../../builder/jobs/ingestion-log.md)
through the [parser](../../builder/parser.md): marketing surfaces land here, while customer
transcripts and competitor pages are parsed but not registered. The register is the result,
not something you maintain by hand.

The `components` column is the coarse link (what the asset discusses); the `claims` column is
the fine one (what it asserts, by `clm-` ID). Together they tell you, for any asset, exactly
which messaging it is carrying, and the [map](../claims-map.md) tells you whether that
messaging is canon.

Customer and market sources are out of scope here for now.

---

## Columns

- `id`: unique kebab-case slug for the asset. Derive it from the URL path (`/pricing` becomes `pricing`, a blog post keeps its slug) or, for captured files, the filename. Prefix with the sub-brand or section only when needed to stay unique.
- `title`: human-readable label
- `source`: the locator (URL or file path)
- `surface`: where the asset lives (see values below)
- `components`: the component IDs found in this asset, space-separated
- `claims`: the `clm-` IDs this asset carries, space-separated
- `last_scanned`: date the asset was last read, `YYYY-MM-DD`

## Surfaces

Company-owned content, by surface:

- `key_page`: core pages expected to carry full messaging (homepage, pricing, about, product pages, signup/contact-sales). These are the source for canon claims.
- `owned`: blog, docs, case studies, ebooks, sales decks
- `earned`: press, keynotes, podcast appearances, media placements
- `paid`: ads, sponsored content
- `internal`: positioning docs, messaging guides, sales enablement

Customer and market sources, by surface. These are parsed for signal but **not** registered
(they are not your published assets); they add [evidence](../evidence.md) and inform the
analyzer, not your asset library:

- `sales-call`: a sales or customer call transcript
- `customer`: a customer interview, win/loss, or support conversation
- `competitor`: a competitor's page, deck, or other material

---

## Register

Deployment: **Mintlify** — setup run 2026-07-07. Step 2 sampled 11 of ~200 discoverable
owned pages (127 blog posts, 51 library guides, 32 customer pages, full docs per the
sitemap); the domain and blog scans have the rest queued.

| id | title | source | surface | components | claims | last_scanned |
|----|-------|--------|---------|------------|--------|--------------|
| homepage | Homepage | https://mintlify.com | key_page | positioning category-name products capabilities customer-proof key-metrics | clm-001 clm-002 clm-003 clm-015 clm-020 clm-027 clm-069 clm-070 clm-071 clm-072 | 2026-07-07 |
| pricing | Pricing | https://mintlify.com/pricing | key_page | pricing-model packaging features add-ons-services offers buying-committee | clm-031 clm-033 clm-076 clm-077 clm-078 clm-080 | 2026-07-07 |
| customers | Customers | https://mintlify.com/customers | key_page | customer-proof icp key-metrics | clm-059 clm-060 clm-061 clm-062 clm-063 clm-065 clm-069 | 2026-07-07 |
| enterprise | Enterprise | https://mintlify.com/enterprise | key_page | capabilities unique-attributes value-proposition value-drivers customer-proof key-metrics | clm-021 clm-024 clm-039 clm-040 clm-047 clm-057 clm-064 clm-072 | 2026-07-07 |
| startups | Startups | https://mintlify.com/startups | key_page | offers market-proof icp | clm-068 clm-081 | 2026-07-07 |
| switch | Why teams switch | https://mintlify.com/switch | key_page | unique-attributes value-proposition add-ons-services customer-proof market-proof key-metrics | clm-037 clm-038 clm-046 clm-048 clm-049 clm-068 clm-073 clm-079 | 2026-07-07 |
| use-case-developer-documentation | Use case: Developer documentation | https://mintlify.com/use-cases/developer-documentation | key_page | value-proposition capabilities features ecosystem-integrations icp | clm-026 clm-028 clm-029 clm-030 clm-032 clm-035 clm-043 clm-053 | 2026-07-07 |
| use-case-help-center | Use case: Help center | https://mintlify.com/use-cases/help-center | key_page | value-proposition capabilities features value-drivers | clm-022 clm-025 clm-034 clm-042 clm-056 | 2026-07-07 |
| use-case-knowledge-base | Use case: Knowledge base | https://mintlify.com/use-cases/knowledge-base | key_page | value-proposition capabilities features | clm-044 | 2026-07-07 |
| use-case-slack-agent | Use case: Slack agent | https://mintlify.com/use-cases/slack-agent | key_page | products capabilities features unique-attributes how-it-works ecosystem-integrations | clm-018 clm-023 clm-036 clm-041 clm-050 | 2026-07-07 |
| careers | Careers | https://mintlify.com/careers | key_page | narrative key-metrics | | 2026-07-07 |
| contact-sales | Contact sales | https://mintlify.com/contact/sales | key_page | positioning value-proposition ecosystem-integrations customer-proof key-metrics | clm-001 clm-045 clm-052 clm-069 | 2026-07-07 |
| blog-documentation-is-dead | Documentation is dead. Long live documentation. | https://mintlify.com/blog/documentation-is-dead | key_page | point-of-view narrative category-name | clm-005 clm-006 clm-007 clm-011 | 2026-07-07 |
| blog-series-b | Series B announcement | https://mintlify.com/blog/series-b | key_page | narrative founder-story market-proof key-metrics | clm-009 clm-010 clm-012 clm-013 clm-067 clm-073 clm-074 | 2026-07-07 |
| blog-demand-channel | Your documentation is a demand channel | https://mintlify.com/blog/documentation-is-a-demand-channel | owned | value-drivers icp themes | clm-058 | 2026-07-07 |
| blog-agents-launch | Introducing the Mintlify Agent | https://mintlify.com/blog/agents-launch | owned | products capabilities how-it-works | clm-016 | 2026-07-07 |
| blog-autopilot | The next step towards self-updating docs | https://mintlify.com/blog/autopilot | owned | products how-it-works unique-attributes | clm-019 clm-051 | 2026-07-07 |
| blog-structured-docs-coding-agents | Docs as an abstraction layer for coding agents | https://mintlify.com/blog/structured-docs-coding-agents | owned | point-of-view positioning value-proposition capabilities | clm-008 clm-045 | 2026-07-07 |
| blog-claude-code-docs | How Claude Code's docs team uses Mintlify | https://mintlify.com/blog/how-claude-code-docs-team-uses-mintlify | owned | customer-proof capabilities icp | | 2026-07-07 |
| blog-trieve-acquisition | Mintlify acquires Trieve | https://mintlify.com/blog/mintlify-acquires-trieve-to-improve-rag-search-in-documentation | owned | category-name features key-metrics market-proof | clm-004 clm-075 | 2026-07-07 |
| blog-ai-assistant | Introducing AI Assistant | https://mintlify.com/blog/introducing-ai-assistant-2025 | owned | products capabilities features | clm-017 | 2026-07-07 |
| library-mintlify-vs-docusaurus | Mintlify vs Docusaurus | https://mintlify.com/library/mintlify-vs-docusaurus-which-documentation-platform-should-you-choose | owned | features unique-attributes customer-proof icp category-name | clm-004 clm-061 | 2026-07-07 |
| customer-coinbase | Coinbase case study | https://mintlify.com/customers/coinbase | owned | customer-proof features value-drivers ecosystem-integrations | clm-059 clm-066 | 2026-07-07 |
| customer-anthropic | Anthropic case study | https://mintlify.com/customers/anthropic | owned | customer-proof features value-drivers | clm-064 | 2026-07-07 |
| docs | Documentation home | https://mintlify.com/docs | owned | features unique-attributes ecosystem-integrations how-it-works category-name | clm-039 clm-054 | 2026-07-07 |
