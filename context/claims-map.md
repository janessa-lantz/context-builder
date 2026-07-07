# Claims Map

*Compiled by the [analyzer](../builder/jobs/analyzer.md). Do not edit; regenerate.*

The coverage view over the whole system: every [claim](claims.md)'s evidence depth and reach
across the [registers](registers/), every [component](README.md)'s claim count with the
zeros written out, and every asset carrying messaging that isn't canon. Gaps — missing or
misaligned — read directly off this file. Absence is a signal, so empty is spelled out,
never omitted.

compiled: — · components_version: 2

## Coverage by component

Every component appears, including the zero rows; a component with no claims is the map's
sharpest finding.

*(structure shown with example rows; the analyzer replaces the whole table on each compile)*

| component | canon | candidate | retired | public ev | private ev | assets |
|-----------|-------|-----------|---------|-----------|------------|--------|
| positioning | 1 | 1 | 0 | 1 | 0 | 2 |
| founder-story | 0 | 0 | 0 | 0 | 0 | 0 |

## Claims

One row per claim, with derived counts and flags:

- `unevidenced`: no evidence rows
- `stale`: `last_confirmed` predates the latest scan of its source
- `orphan`: appears in no register row
- `divergent`: variants of it are live on published surfaces
- `contested`: a competitor [entity](entities/) Feed row contests it

| id | claim | status | public ev | private ev | assets | flags |
|----|-------|--------|-----------|------------|--------|-------|
| clm-001 | "Ship quality AI at scale" | canon | 1 | 0 | 2 | divergent |

## Misaligned assets

Register rows carrying `candidate` or `retired` claims: published material saying something
the canon doesn't. Each row names the [issue](../builder/issues/) tracking it.

| register row | claims | issue |
|--------------|--------|-------|
| blog-why-quality | clm-003 | iss-0xx |
