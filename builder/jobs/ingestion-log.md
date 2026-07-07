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

*(the rows below are examples; delete them when you start logging real inputs)*

| created | type | source | scan_id | route | status | result |
|---------|------|--------|---------|-------|--------|--------|
| 2026-07-07 | url | https://example.com | scan-keypages-0707 | parser + registers | done | registered as homepage; minted clm-001 clm-002, 2 evidence rows |
| 2026-07-07 | url | https://competitor.com | scan-competitive-0707 | parser | done | parsed; competitor, entity updated, nothing minted |
| 2026-07-07 | text | raw-assets/acme-winloss-0603.txt |  | parser | done | parsed; sales transcript, 3 private evidence rows |
| 2026-07-11 | pdf | raw-assets/analyst-brief.pdf |  | parser | pending |  |
