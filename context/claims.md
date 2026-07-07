# Claims Register

The source of truth for your messaging, one claim per row. A **claim** is a single assertable
statement, typed by a [component](README.md) ID. The rows with `status: canon` **are** the
canon: your approved messaging. Everything downstream keys on the claim: [evidence](evidence.md)
accumulates against it, [registers](registers/) log which material carries it,
[lockups](lockups.md) and [entry points](entry-points.md) compose it into units of messaging,
and the [map](claims-map.md) shows its coverage. If it can fit into a spreadsheet it can be
wrangled and managed; this table is that spreadsheet.

The [builder](../builder/) maintains this register. Skills read it and never write it.

## Rules

- **The LLM mints claims from verbatim, company-published copy only**, source attributed.
  Claims found on live key pages enter as `canon`; claims found on other owned surfaces enter
  as `candidate`. Customer and competitor material never mints a claim; it adds
  [evidence](evidence.md) or files an [issue](../builder/issues/).
- **A human may add synthesized claims**, marked `source: human`. The LLM never edits,
  retires, or re-statuses a `source: human` row.
- **Demotion is human-only.** The LLM never moves a claim out of `canon`. If a re-scan cannot
  find a canon claim on any live surface, leave `last_confirmed` stale and file an issue;
  never silently retire.
- **Rows are never deleted.** A dead claim becomes `retired` and keeps its ID and history.
- **Absence is a signal.** A component with no claims is a finding (the [map](claims-map.md)
  writes the zero), not a hole to patch with invention.

## Columns

- `id`: `clm-NNN`, sequential, never reused
- `component`: the component ID this claim is typed by (see [README](README.md))
- `claim`: the statement itself; verbatim from a live surface, or human synthesis
- `status`: see below
- `variant_of`: blank for a primary claim; a `clm-` ID when this row is a divergent phrasing
  of that claim
- `source`: the surface carrying the phrasing (a register row ID or URL), or `human`
- `first_seen`: date the claim entered the register, `YYYY-MM-DD`
- `last_confirmed`: date the claim was last seen live (or last affirmed by a human)

## Statuses

- `canon`: approved messaging. Verbatim from a live key page, or human-authored. Skills ship it.
- `candidate`: observed on an owned surface but not approved. Skills do not ship it. A human
  promotes a candidate to canon (often via [codify](../builder/jobs/codify.md)).
- `retired`: no longer messaging. Kept for history; the ID is never reused.

## Variants

Divergent phrasings of the same claim are their own rows, each pointing at the primary via
`variant_of`. The primary row carries the canonical phrasing. To make a variant canonical, a
human swaps the direction of the pointer. Variants let the map show `divergent` messaging in
the wild without collapsing real differences into one row.

## Register

*(the rows below are examples; delete them when you mint real claims)*

| id | component | claim | status | variant_of | source | first_seen | last_confirmed |
|----|-----------|-------|--------|------------|--------|------------|----------------|
| clm-001 | positioning | "Ship quality AI at scale" | canon | | homepage | 2026-07-07 | 2026-07-07 |
| clm-002 | features | "SSO works out of the box with Okta and Entra" | canon | | security | 2026-07-07 | 2026-07-07 |
| clm-003 | positioning | "The AI quality platform for production teams" | candidate | clm-001 | blog-why-quality | 2026-07-07 | 2026-07-07 |
| clm-004 | value-proposition | Lead with quality, not observability; observability is the category label, not the promise | canon | | human | | 2026-07-07 |
