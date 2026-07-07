# Entry Points

On-ramps to your product: named compositions of [claims](claims.md) organized by the way a
buyer arrives — a persona, a technology, an integration. Where a [lockup](lockups.md) shapes
messaging by structure, an entry point shapes it by audience and route: the claims that hook
this arrival, support the story, and prove it.

## Rules

The composition rules are [lockups.md](lockups.md)'s, restated: members are canon claims by
`clm-` ID; every member canon or the entry point stays `draft`; skills render `approved`
only; the LLM drafts, a human approves; slugs are kebab-case and unique across both files.

## How an entry point is written

One `##` section per entry point. Fields: `kind` (`persona` / `technology` / `integration`),
`audience` (who arrives this way), `status` (`draft` / `approved`), `updated` (`YYYY-MM-DD`).
Then an ordered table: `order | claim | role | note`, where `role` is `hook` (why they stop),
`support` (why it's true for them), or `proof` (why they believe it).

---

*(the two entry points below are worked examples; replace them when you compose real ones)*

## head-of-devops

kind: persona · audience: the DevOps leader arriving from a reliability initiative · status: draft · updated: 2026-07-07

| order | claim | role | note |
|-------|-------|------|------|
| 1 | clm-0xx | hook | the outcome their initiative names |
| 2 | clm-0xx | support | the capability that maps to their job to be done |
| 3 | clm-0xx | proof | the customer-proof claim from a peer company |

## snowflake

kind: integration · audience: teams standardized on Snowflake evaluating fit · status: draft · updated: 2026-07-07

| order | claim | role | note |
|-------|-------|------|------|
| 1 | clm-0xx | hook | the ecosystem-integrations claim naming Snowflake |
| 2 | clm-0xx | support | what the integration unlocks |
| 3 | clm-0xx | proof | key metric or proof from a Snowflake-stack customer |
