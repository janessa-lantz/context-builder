# Ingestion Log

The front door and the router. Every input to context-builder is logged here, then routed.
Nothing reaches the registers without being parsed first.

It accepts three input types:

- `text`: pasted text or a transcript
- `url`: a link to a live page
- `pdf`: an uploaded document

A scan is not an input type. Scans are jobs that discover URLs and feed them back here as
`url` inputs (see [scans/](scans/)).

## Routing

- **Everything** routes to the [parser](../parser.md), which maps the asset against the [claims register](../../context/claims.md).
- **Marketing surfaces** (your company-owned content) also route to the [registers](../../context/registers/), so sales and marketing can find which assets carry which claims.

A sales transcript is parsed but not registered (it adds `private` evidence). Competitor
content is parsed but not registered (it lands in [entities](../../context/entities/)). Your
own pages and posts are parsed and registered.

## Columns

- `created`: date the input arrived, `YYYY-MM-DD`
- `type`: `text`, `url`, or `pdf`
- `source`: the input (a URL, or a [raw-asset](../raw-assets/) path for captured text and PDFs)
- `scan_id`: the scan that produced this input, if any, as `scan-{name}-{MMDD}` (for example `scan-keypages-0604`); blank for direct inputs
- `route`: `parser`, or `parser + registers` for marketing surfaces
- `status`: `pending`, `done`, or `skipped`
- `result`: what happened

---

## Log

Deployment: **Mintlify** — setup run of 2026-07-07. Step 2 ran as a sample (11 of ~200
discoverable owned pages); the domain and blog scans have more to feed on later runs.

| created | type | source | scan_id | route | status | result |
|---------|------|--------|---------|-------|--------|--------|
| 2026-07-07 | url | https://mintlify.com | scan-keypages-0707 | parser + registers | done | registered as homepage; minted clm-001–003, 015, 020, 027, 069–072 |
| 2026-07-07 | url | https://mintlify.com/pricing | scan-keypages-0707 | parser + registers | done | registered as pricing; minted clm-031, 033, 076–078, 080; Pro price not rendered to scraper (iss-007) |
| 2026-07-07 | url | https://mintlify.com/customers | scan-keypages-0707 | parser + registers | done | registered as customers; minted clm-059–063, 065; 32 case studies discovered, 2 detail pages sampled |
| 2026-07-07 | url | https://mintlify.com/enterprise | scan-keypages-0707 | parser + registers | done | registered as enterprise; minted clm-021, 024, 039, 040, 047, 057, 064 |
| 2026-07-07 | url | https://mintlify.com/startups | scan-keypages-0707 | parser + registers | done | registered as startups; minted clm-068, 081 |
| 2026-07-07 | url | https://mintlify.com/switch | scan-keypages-0707 | parser + registers | done | registered as switch; minted clm-037, 038, 046, 048, 049, 073, 079 |
| 2026-07-07 | url | https://mintlify.com/use-cases/developer-documentation | scan-keypages-0707 | parser + registers | done | registered; minted clm-026, 028–030, 032, 035, 043, 053 |
| 2026-07-07 | url | https://mintlify.com/use-cases/help-center | scan-keypages-0707 | parser + registers | done | registered; minted clm-022, 025, 034, 042, 056 |
| 2026-07-07 | url | https://mintlify.com/use-cases/knowledge-base | scan-keypages-0707 | parser + registers | done | registered; minted clm-044 |
| 2026-07-07 | url | https://mintlify.com/use-cases/slack-agent | scan-keypages-0707 | parser + registers | done | registered; minted clm-018, 023, 036, 041, 050 |
| 2026-07-07 | url | https://mintlify.com/careers | scan-keypages-0707 | parser + registers | done | registered as careers; no claims minted (values page; story links out to YC post) |
| 2026-07-07 | url | https://mintlify.com/contact/sales | scan-keypages-0707 | parser + registers | done | registered; minted clm-045, 052; repeat evidence for clm-001, 069 |
| 2026-07-07 | url | https://mintlify.com/blog/documentation-is-dead | scan-keypages-0707 | parser + registers | done | founder POV essay (About-page substitute per key-pages scan); minted clm-005–007, 011 |
| 2026-07-07 | url | https://mintlify.com/blog/series-b | scan-keypages-0707 | parser + registers | done | founder narrative (About-page substitute); minted clm-009, 010, 012, 013, 067, 074 |
| 2026-07-07 | url | https://mintlify.com/blog/documentation-is-a-demand-channel | scan-blog-0707 | parser + registers | done | registered; minted clm-058 (candidate) |
| 2026-07-07 | url | https://mintlify.com/blog/agents-launch | scan-blog-0707 | parser + registers | done | registered; minted clm-016 (candidate) |
| 2026-07-07 | url | https://mintlify.com/blog/autopilot | scan-blog-0707 | parser + registers | done | registered; minted clm-019, 051 (candidates) |
| 2026-07-07 | url | https://mintlify.com/blog/structured-docs-coding-agents | scan-blog-0707 | parser + registers | done | registered; minted clm-008 (candidate); evidence for clm-045 |
| 2026-07-07 | url | https://mintlify.com/blog/how-claude-code-docs-team-uses-mintlify | scan-blog-0707 | parser + registers | done | registered; no new claims; customer-proof register row (Anthropic/Claude Code) |
| 2026-07-07 | url | https://mintlify.com/blog/mintlify-acquires-trieve-to-improve-rag-search-in-documentation | scan-blog-0707 | parser + registers | done | registered; minted clm-004, 075 (candidates) |
| 2026-07-07 | url | https://mintlify.com/blog/introducing-ai-assistant-2025 | scan-blog-0707 | parser + registers | done | registered; minted clm-017 (candidate) |
| 2026-07-07 | url | https://mintlify.com/library/mintlify-vs-docusaurus-which-documentation-platform-should-you-choose | scan-domain-0707 | parser + registers | done | registered; evidence for clm-004, 061 |
| 2026-07-07 | url | https://mintlify.com/customers/coinbase | scan-domain-0707 | parser + registers | done | registered; minted clm-066 (candidate); customer-proof register row |
| 2026-07-07 | url | https://mintlify.com/customers/anthropic | scan-domain-0707 | parser + registers | done | registered; customer-proof register row; evidence for clm-064 |
| 2026-07-07 | url | https://mintlify.com/docs | scan-domain-0707 | parser + registers | done | registered (light parse); minted clm-054 (candidate); evidence for clm-004, 039 |
