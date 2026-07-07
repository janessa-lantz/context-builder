# Customer-Proof Register

Your proof material, one row per artifact: case studies, quotes, logos, references,
benchmarks. The `claims` column records which [claims](../claims.md) each artifact proves,
so for any claim you can pull the proof, and for any proof you can see what it's for.

Rows are material, not statements: the claim "Acme cut close time 40%" lives in the claims
register typed `customer-proof`; the case study that documents it lives here. The parser adds
rows as proof assets are parsed (a published case study is also an `owned` row in the
[content register](content.md); here it is tracked as proof).

## Columns

- `id`: unique kebab-case slug for the artifact
- `title`: human-readable label
- `customer`: the customer named, or `anonymous`
- `type`: `case-study` / `quote` / `logo` / `reference` / `benchmark`
- `source`: the locator (URL or file path)
- `claims`: the `clm-` IDs this artifact proves, space-separated
- `last_scanned`: `YYYY-MM-DD`

## Register

Deployment: **Mintlify**. The sitemap lists 32 customer pages; this setup run registered the
2 sampled detail pages plus the artifacts visible on /customers and key pages. The remaining
case-study pages are queued for the domain scan, not absent.

| id | title | customer | type | source | claims | last_scanned |
|----|-------|----------|------|--------|--------|--------------|
| coinbase-case-study | Coinbase: 20min → 60s doc updates | Coinbase | case-study | https://mintlify.com/customers/coinbase | clm-059 clm-066 | 2026-07-07 |
| anthropic-case-study | Anthropic accelerates AI development and adoption | Anthropic | case-study | https://mintlify.com/customers/anthropic | clm-064 | 2026-07-07 |
| claude-code-docs-story | How Claude Code's docs team makes feedback actionable | Anthropic (Claude Code) | case-study | https://mintlify.com/blog/how-claude-code-docs-team-uses-mintlify | | 2026-07-07 |
| hubspot-outcome | HubSpot: 50% reduction in eng resources on docs | HubSpot | case-study | https://mintlify.com/customers/hubspot | clm-060 | 2026-07-07 |
| zapier-outcome | Zapier: 3x faster documentation updates | Zapier | case-study | https://mintlify.com/customers/zapier | clm-061 | 2026-07-07 |
| laravel-outcome | Laravel: 3-day migration | Laravel | case-study | https://mintlify.com/customers/laravel | clm-062 | 2026-07-07 |
| fidelity-outcome | Fidelity: 99.99% uptime since launch | Fidelity | case-study | https://mintlify.com/customers/fidelity | clm-063 | 2026-07-07 |
| browserbase-quote | "Our docs are the product" — Paul Klein, CEO | Browserbase | quote | https://mintlify.com/customers | clm-065 | 2026-07-07 |
| replit-quote | Notion/Google-Docs interface backed by version control — Matt Palmer, DevRel | Replit | quote | https://mintlify.com/customers | | 2026-07-07 |
| leffew-quote | "As agentic as the protocols we're shipping" — Kevin Leffew, AI GTM Lead | Coinbase | quote | https://mintlify.com/customers/coinbase | clm-066 | 2026-07-07 |
| customers-logo-wall | 30 named customer logos | multiple | logo | https://mintlify.com/customers | | 2026-07-07 |
