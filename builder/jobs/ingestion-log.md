# Ingestion Log

The front door and the router. Every input to context-builder is logged here, then routed.
Nothing reaches the index without being parsed first.

It accepts three input types:

- `text`: pasted text or a transcript
- `url`: a link to a live page
- `pdf`: an uploaded document

A scan is not an input type. Scans are jobs that discover URLs and feed them back here as
`url` inputs (see [scans/](scans/)).

## Routing

- **Everything** routes to the [parser](../parser.md), which maps the asset against the canon.
- **Marketing surfaces** (your company-owned content) also route to the [index](../../context/content-index.md), so sales and marketing can find which assets carry which messaging.

A sales transcript is parsed but not indexed. Competitor content is parsed but not indexed.
Your own pages and posts are parsed and indexed.

## Columns

- `created`: date the input arrived, `YYYY-MM-DD`
- `type`: `text`, `url`, or `pdf`
- `source`: the input (a URL, or a [raw-asset](../raw-assets/) path for captured text and PDFs)
- `scan_id`: the scan that produced this input, if any; blank for direct inputs
- `route`: `parser`, or `parser + index` for marketing surfaces
- `status`: `pending`, `done`, or `skipped`
- `result`: what happened

---

## Log

*(the rows below are examples; delete them when you start logging real inputs)*

| created | type | source | scan_id | route | status | result |
|---------|------|--------|---------|-------|--------|--------|
| 2026-06-04 | url | https://example.com | scan-keypages-0604 | parser + index | done | indexed as homepage; canon updated |
| 2026-06-04 | url | https://competitor.com | scan-competitive-0604 | parser | done | parsed; competitor, not indexed |
| 2026-06-04 | text | raw-assets/acme-winloss-0603.txt |  | parser | done | parsed; sales transcript, not indexed |
| 2026-06-11 | pdf | raw-assets/analyst-brief.pdf |  | parser | pending |  |
