# Offers Register

The ways in, one row per offer: free tiers, trials, credits, programs, promos. The `claims`
column records which [claims](../claims.md) each offer carries, so an SDR program or a
campaign can pull the current offers and the approved language for each.

Rows are material, not statements: the offer "14-day free trial" lives here; the claim "Start
free, no credit card required" lives in the claims register typed `offers`. The parser adds
rows as pricing and signup surfaces are parsed; expired offers are marked, never deleted.

## Columns

- `id`: unique kebab-case slug
- `name`: the offer's name
- `type`: `free-tier` / `trial` / `credit` / `program` / `promo`
- `description`: one line: what's included, and any time bound
- `source`: where it's published (URL or file path)
- `claims`: the `clm-` IDs this offer carries, space-separated
- `status`: `active` / `expired`
- `last_confirmed`: `YYYY-MM-DD`

## Register

*(the first row is an example; delete it when you add real offers)*

| id | name | type | description | source | claims | status | last_confirmed |
|----|------|------|-------------|--------|--------|--------|----------------|
| free-trial | 14-day free trial | trial | Full platform, 14 days, no credit card | https://example.com/pricing | | active | 2026-07-07 |
