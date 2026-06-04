# Ingestion Log

Every intake event, one row per item, in the order it happened. Append-only: add new rows at
the bottom, never edit or delete the ones above.

This is the event history. It answers "what came in, and when?" Its companion is the
[`content-index.md`](content-index.md), which holds current state ("what exists, and what's
in it?").

A website scan is one event that brings in many pages: each page gets its own row here,
sharing a `scan_id`, and each lands as a row in the content index. Items that never enter the
index (duplicates, rejects, out-of-scope) still get logged here with `event` set to
`skipped`. That is the reason the log exists separately from the index.

---

## Columns

- `ingested_at`: when the item came in, `YYYY-MM-DD`
- `scan_id`: batch id when the item arrived as part of a website scan or bulk intake; blank for one-off items
- `id`: the asset's id, matching its row in the content index (blank if skipped before indexing)
- `source`: the locator (URL or file path)
- `ledger`, `surface`: the same controlled values as the [content index](content-index.md)
- `event`: `new` (first time seen), `rescan` (re-ingested an existing asset), or `skipped` (not added to the index)
- `notes`: optional, for example why an item was skipped

---

## Log

*(the rows below are examples; delete them when you start logging real intake)*

| ingested_at | scan_id | id | source | ledger | surface | event | notes |
|-------------|---------|----|--------|--------|---------|-------|-------|
| 2026-06-04 | scan-2026-06-04 | homepage | https://example.com | company | key_page | new | from full site scan |
| 2026-06-04 | scan-2026-06-04 | pricing | https://example.com/pricing | company | key_page | new | from full site scan |
| 2026-06-04 |  | acme-winloss-0603 | calls/acme-2026-06-03.txt | customer | sales_call | new |  |
| 2026-06-11 | scan-2026-06-11 | homepage | https://example.com | company | key_page | rescan | hero copy changed |
| 2026-06-11 | scan-2026-06-11 | pricing | https://example.com/pricing | company | key_page | skipped | unchanged since last scan |
