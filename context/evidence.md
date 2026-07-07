# Evidence Ledger

Proof accumulating against [claims](claims.md), one row per observation. Every claim can be
traced to its sources here; the [map](claims-map.md) counts these rows to show which claims
are well-evidenced and which are asserted on faith. The parser appends rows as it works; the
ledger is the result, not something you maintain by hand.

## Rules

- **Evidence only supports.** A source that contradicts a claim is an
  [issue](../builder/issues/), never an evidence row.
- **Two kinds.** `public` evidence is published: case studies, benchmarks, your own live
  pages. `private` evidence is unpublished: sales calls, customer interviews, win/loss notes.
  Once a sales call adds evidence, it piles up per claim; that pile is the point.
- **Provenance on every row.** `source` is the [parsed-summary](../builder/parsed-summaries/)
  ID wherever one exists, else a locator. No orphan evidence.
- **Private detail is raw.** A quote from a call is provenance at the same trust level as an
  [entity](entities/) page: it explains why the claim holds, and its text is never shipped
  as copy.

## Columns

- `id`: `ev-NNN`, sequential, never reused
- `claim_id`: the `clm-` ID this row supports
- `kind`: `public` / `private`
- `detail`: what was observed, quoted where short (with timestamp or location for calls)
- `source`: parsed-summary ID, or locator when no summary exists
- `date`: when the evidence was captured, `YYYY-MM-DD`

## Ledger

Deployment: **Mintlify**. All rows `public` — no sales-call or customer sources ingested yet,
so no `private` evidence exists. Rows ev-001–ev-081 are each claim's minting sighting; rows
from ev-082 are repeat sightings on other surfaces.

| id | claim_id | kind | detail | source | date |
|----|----------|------|--------|--------|------|
| ev-001 | clm-001 | public | Homepage hero, verbatim | homepage | 2026-07-07 |
| ev-002 | clm-002 | public | Homepage hero subheadline | homepage | 2026-07-07 |
| ev-003 | clm-003 | public | Homepage hero category label | homepage | 2026-07-07 |
| ev-004 | clm-004 | public | "AI-native documentation platform," in body copy | blog-trieve-acquisition | 2026-07-07 |
| ev-005 | clm-005 | public | POV essay, central claim | blog-documentation-is-dead | 2026-07-07 |
| ev-006 | clm-006 | public | POV essay, belief statement | blog-documentation-is-dead | 2026-07-07 |
| ev-007 | clm-007 | public | POV essay close: "This is our bet at Mintlify" | blog-documentation-is-dead | 2026-07-07 |
| ev-008 | clm-008 | public | Essay opening claim | blog-structured-docs-coding-agents | 2026-07-07 |
| ev-009 | clm-009 | public | Series B post, shift recognition | blog-series-b | 2026-07-07 |
| ev-010 | clm-010 | public | Series B post, strategic framing | blog-series-b | 2026-07-07 |
| ev-011 | clm-011 | public | POV essay opening | blog-documentation-is-dead | 2026-07-07 |
| ev-012 | clm-012 | public | Series B post, origin paragraph (Han Wang) | blog-series-b | 2026-07-07 |
| ev-013 | clm-013 | public | Series B post, origin story | blog-series-b | 2026-07-07 |
| ev-014 | clm-014 | public | Synthesis; drawn from homepage hero, series-b metrics, contact-sales subhead | homepage | 2026-07-07 |
| ev-015 | clm-015 | public | Homepage platform section headline | homepage | 2026-07-07 |
| ev-016 | clm-016 | public | Launch post title + description | blog-agents-launch | 2026-07-07 |
| ev-017 | clm-017 | public | Launch post description | blog-ai-assistant | 2026-07-07 |
| ev-018 | clm-018 | public | Slack use-case hero | use-case-slack-agent | 2026-07-07 |
| ev-019 | clm-019 | public | Autopilot post description | blog-autopilot | 2026-07-07 |
| ev-020 | clm-020 | public | Homepage platform category card | homepage | 2026-07-07 |
| ev-021 | clm-021 | public | Enterprise capability section | enterprise | 2026-07-07 |
| ev-022 | clm-022 | public | Help-center capability list | use-case-help-center | 2026-07-07 |
| ev-023 | clm-023 | public | Slack use-case "Capture" feature | use-case-slack-agent | 2026-07-07 |
| ev-024 | clm-024 | public | Enterprise capability section | enterprise | 2026-07-07 |
| ev-025 | clm-025 | public | Help-center capability list | use-case-help-center | 2026-07-07 |
| ev-026 | clm-026 | public | Dev-docs capability list | use-case-developer-documentation | 2026-07-07 |
| ev-027 | clm-027 | public | Homepage platform category card | homepage | 2026-07-07 |
| ev-028 | clm-028 | public | Dev-docs feature list | use-case-developer-documentation | 2026-07-07 |
| ev-029 | clm-029 | public | Dev-docs feature list | use-case-developer-documentation | 2026-07-07 |
| ev-030 | clm-030 | public | Dev-docs feature list | use-case-developer-documentation | 2026-07-07 |
| ev-031 | clm-031 | public | Pricing Starter feature list | pricing | 2026-07-07 |
| ev-032 | clm-032 | public | Dev-docs feature list | use-case-developer-documentation | 2026-07-07 |
| ev-033 | clm-033 | public | Pricing Enterprise feature list | pricing | 2026-07-07 |
| ev-034 | clm-034 | public | Help-center feature list | use-case-help-center | 2026-07-07 |
| ev-035 | clm-035 | public | Dev-docs feature list | use-case-developer-documentation | 2026-07-07 |
| ev-036 | clm-036 | public | Slack use-case "Ask" feature | use-case-slack-agent | 2026-07-07 |
| ev-037 | clm-037 | public | Switch page differentiation | switch | 2026-07-07 |
| ev-038 | clm-038 | public | Switch page differentiation | switch | 2026-07-07 |
| ev-039 | clm-039 | public | Enterprise differentiation | enterprise | 2026-07-07 |
| ev-040 | clm-040 | public | Enterprise differentiation | enterprise | 2026-07-07 |
| ev-041 | clm-041 | public | Slack use-case trust section | use-case-slack-agent | 2026-07-07 |
| ev-042 | clm-042 | public | Help-center hero | use-case-help-center | 2026-07-07 |
| ev-043 | clm-043 | public | Dev-docs hero | use-case-developer-documentation | 2026-07-07 |
| ev-044 | clm-044 | public | Knowledge-base hero | use-case-knowledge-base | 2026-07-07 |
| ev-045 | clm-045 | public | Contact-sales pitch band | contact-sales | 2026-07-07 |
| ev-046 | clm-046 | public | Switch migration section | switch | 2026-07-07 |
| ev-047 | clm-047 | public | Enterprise differentiation pair | enterprise | 2026-07-07 |
| ev-048 | clm-048 | public | Switch reported metrics | switch | 2026-07-07 |
| ev-049 | clm-049 | public | Switch reported metrics | switch | 2026-07-07 |
| ev-050 | clm-050 | public | Slack use-case how-it-works steps | use-case-slack-agent | 2026-07-07 |
| ev-051 | clm-051 | public | Autopilot post, three steps | blog-autopilot | 2026-07-07 |
| ev-052 | clm-052 | public | Contact-sales pitch band | contact-sales | 2026-07-07 |
| ev-053 | clm-053 | public | Dev-docs integrations named | use-case-developer-documentation | 2026-07-07 |
| ev-054 | clm-054 | public | Docs deployment section | docs | 2026-07-07 |
| ev-055 | clm-055 | public | Synthesis; drawn from use-case targets, enterprise/startups segments, switch | use-case-developer-documentation | 2026-07-07 |
| ev-056 | clm-056 | public | Help-center hero subheadline | use-case-help-center | 2026-07-07 |
| ev-057 | clm-057 | public | Enterprise automation section | enterprise | 2026-07-07 |
| ev-058 | clm-058 | public | Demand-channel essay, core argument | blog-demand-channel | 2026-07-07 |
| ev-059 | clm-059 | public | Customers page case-study card | customers | 2026-07-07 |
| ev-060 | clm-060 | public | Customers page case-study card | customers | 2026-07-07 |
| ev-061 | clm-061 | public | Customers page case-study card | customers | 2026-07-07 |
| ev-062 | clm-062 | public | Customers page case-study card | customers | 2026-07-07 |
| ev-063 | clm-063 | public | Customers page case-study card | customers | 2026-07-07 |
| ev-064 | clm-064 | public | Enterprise Anthropic case block | enterprise | 2026-07-07 |
| ev-065 | clm-065 | public | Customers page testimonial | customers | 2026-07-07 |
| ev-066 | clm-066 | public | Coinbase case study metrics | customer-coinbase | 2026-07-07 |
| ev-067 | clm-067 | public | Series B announcement | blog-series-b | 2026-07-07 |
| ev-068 | clm-068 | public | Startups page testimonial | startups | 2026-07-07 |
| ev-069 | clm-069 | public | Homepage social-proof band | homepage | 2026-07-07 |
| ev-070 | clm-070 | public | Homepage metrics band | homepage | 2026-07-07 |
| ev-071 | clm-071 | public | Homepage metrics band | homepage | 2026-07-07 |
| ev-072 | clm-072 | public | Homepage metrics band | homepage | 2026-07-07 |
| ev-073 | clm-073 | public | Switch hero subheadline | switch | 2026-07-07 |
| ev-074 | clm-074 | public | Series B post | blog-series-b | 2026-07-07 |
| ev-075 | clm-075 | public | Trieve acquisition post | blog-trieve-acquisition | 2026-07-07 |
| ev-076 | clm-076 | public | Pricing tiers + credits | pricing | 2026-07-07 |
| ev-077 | clm-077 | public | Pricing tier descriptions | pricing | 2026-07-07 |
| ev-078 | clm-078 | public | Pricing tier feature lists | pricing | 2026-07-07 |
| ev-079 | clm-079 | public | Switch migration promise | switch | 2026-07-07 |
| ev-080 | clm-080 | public | Pricing hero subheadline | pricing | 2026-07-07 |
| ev-081 | clm-081 | public | Startups offer terms | startups | 2026-07-07 |
| ev-082 | clm-001 | public | Contact-sales headline, verbatim repeat | contact-sales | 2026-07-07 |
| ev-083 | clm-069 | public | Customers page bottom band, verbatim repeat | customers | 2026-07-07 |
| ev-084 | clm-069 | public | Contact-sales CTA band, verbatim repeat | contact-sales | 2026-07-07 |
| ev-085 | clm-072 | public | Enterprise performance claim ("99.99% uptime") | enterprise | 2026-07-07 |
| ev-086 | clm-073 | public | "Content reaches more than 100 million people every year" — phrasing differs (people vs builders); see iss-004 | blog-series-b | 2026-07-07 |
| ev-087 | clm-004 | public | Docs landing intro: "AI-native, beautiful out-of-the-box" platform framing | docs | 2026-07-07 |
| ev-088 | clm-004 | public | Library comparison positions Mintlify as the managed AI-native docs platform | library-mintlify-vs-docusaurus | 2026-07-07 |
| ev-089 | clm-045 | public | "64% more precise answers, 39% better discoverability, ~50% fewer tokens, 1.5x faster" | blog-structured-docs-coding-agents | 2026-07-07 |
| ev-090 | clm-059 | public | Case study detail: "20+ minutes to under 60 seconds" | customer-coinbase | 2026-07-07 |
| ev-091 | clm-064 | public | Case study detail: "over 1.5 million developers rely on Anthropic's docs every month" | customer-anthropic | 2026-07-07 |
| ev-092 | clm-068 | public | Same Taggar quote repeated | switch | 2026-07-07 |
| ev-093 | clm-039 | public | Docs landing intro, verbatim repeat | docs | 2026-07-07 |
| ev-094 | clm-061 | public | "Zapier reported a 20% increase in documentation traffic and adoption after switching" | library-mintlify-vs-docusaurus | 2026-07-07 |
