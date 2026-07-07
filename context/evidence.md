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

*(the rows below are examples; delete them when real evidence lands)*

| id | claim_id | kind | detail | source | date |
|----|----------|------|--------|--------|------|
| ev-001 | clm-001 | public | Homepage hero, verbatim | homepage | 2026-07-07 |
| ev-002 | clm-002 | private | "We picked you because SSO just worked with our Okta setup" — prospect, 12:40 | acme-call-0612 | 2026-07-07 |
