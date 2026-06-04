# Jobs

The work you hand to the builder. Each row is one job: a source to ingest and parse. Add a
job by appending a row that names its source. The builder reads pending jobs, runs each
through the [parser](../builder/parser.md), writes the results into
[context](../context/messaging/content-index.md), and marks the job done.

A website scan is one batch of jobs that share a `scan_id`, one per page discovered.
Re-processing a source later is a new job, not an edit of an old one. Jobs accumulate, so the
list doubles as the record of everything the builder has ever taken in.

---

## Columns

- `created`: date the job was added, `YYYY-MM-DD`
- `scan_id`: batch id when the job is part of a website scan or bulk add; blank for one-off jobs
- `source`: the locator to ingest (URL or file path)
- `ledger`, `surface`: a hint if you know it (a transcript is `customer` / `sales_call`); otherwise the parser classifies it
- `id`: the asset id the parser assigns; written back here once the job runs
- `status`: `pending`, `done`, or `skipped`
- `result`: what the builder did, or why it was skipped

See the [content index](../context/messaging/content-index.md) for the full `ledger` / `surface` values.

---

## Queue

*(the rows below are examples; delete them when you start adding real jobs)*

| created | scan_id | source | ledger | surface | id | status | result |
|---------|---------|--------|--------|---------|----|--------|--------|
| 2026-06-04 | scan-2026-06-04 | https://example.com | company | key_page | homepage | done | indexed; canon: positioning, capabilities |
| 2026-06-04 | scan-2026-06-04 | https://example.com/pricing | company | key_page | pricing | done | indexed; canon: pricing-model, packaging |
| 2026-06-04 |  | calls/acme-2026-06-03.txt | customer | sales_call | acme-winloss-0603 | done | indexed; objections, value-drivers |
| 2026-06-11 |  | https://example.com/blog/new-post | company | owned |  | pending |  |
