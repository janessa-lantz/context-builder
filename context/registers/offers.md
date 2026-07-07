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

Deployment: **Mintlify** — setup run 2026-07-07.

| id | name | type | description | source | claims | status | last_confirmed |
|----|------|------|-------------|--------|--------|--------|----------------|
| starter-free | Starter tier | free-tier | $0/mo: full platform, custom domain, web editor, authentication, MCP server, API playground; 10,000 credits/mo | https://mintlify.com/pricing | clm-076 clm-077 clm-080 | active | 2026-07-07 |
| first-month-credits | First month of credits free | credit | "Get started for free, your first month of credits on us" | https://mintlify.com/pricing | clm-080 | active | 2026-07-07 |
| startup-program | Startup program | program | Eligible startups and YC alumni: 50% off Pro for one year | https://mintlify.com/startups | clm-081 | active | 2026-07-07 |
| yc-batch-program | YC current-batch program | program | 12 months of Pro free through launch, plus priority support | https://mintlify.com/startups | clm-081 | active | 2026-07-07 |
