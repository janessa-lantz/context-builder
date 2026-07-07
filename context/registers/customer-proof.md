# Customer-Proof Register

Your proof material, one row per artifact: case studies, quotes, logos, references,
benchmarks. The `claims` column records which [claims](../claims.md) each artifact proves,
so for any claim you can pull the proof, and for any proof you can see what it's for.

Rows are material, not statements: the claim "Acme cut close time 40%" lives in the claims
register typed `customer-proof`; the case study that documents it lives here. The parser adds
rows as proof assets are parsed (a published case study is also an `owned` row in the
[content register](content.md); here it is tracked as proof).

## Columns

- `id`: unique kebab-case slug for the artifact
- `title`: human-readable label
- `customer`: the customer named, or `anonymous`
- `type`: `case-study` / `quote` / `logo` / `reference` / `benchmark`
- `source`: the locator (URL or file path)
- `claims`: the `clm-` IDs this artifact proves, space-separated
- `last_scanned`: `YYYY-MM-DD`

## Register

*(the first row is an example; delete it when you add real proof)*

| id | title | customer | type | source | claims | last_scanned |
|----|-------|----------|------|--------|--------|--------------|
| acme-case-study | How Acme cut close time 40% | Acme | case-study | https://example.com/customers/acme | clm-002 | 2026-07-07 |
