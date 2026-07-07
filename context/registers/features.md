# Features Register

The product truth, one row per capability or feature. The `claims` column records which
[claims](../claims.md) are made about each, so messaging stays traceable to what the product
actually does, and you can see which parts of the product have no messaging at all.

Rows are material, not statements: the feature "SAML SSO" lives here; the claim "SSO works
out of the box with Okta and Entra" lives in the claims register typed `features`. The parser
adds rows as product pages and docs are parsed. **Human seeding is allowed and expected**:
product truth is often unpublished, and a human-added row with no claims is one of the
sharpest gap signals the [map](../claims-map.md) can show.

## Columns

- `id`: unique kebab-case slug
- `name`: the capability or feature name
- `grain`: `capability` (workflow-grain: what the product enables) / `feature` (named product functionality)
- `product`: which product it belongs to (from the `products` component), blank for single-product companies
- `description`: one line, factual
- `source`: where it's documented (URL, file path, or `human`)
- `claims`: the `clm-` IDs asserted about it, space-separated (blank = unmessaged product truth)
- `last_confirmed`: `YYYY-MM-DD`

## Register

*(the first row is an example; delete it when you add real features)*

| id | name | grain | product | description | source | claims | last_confirmed |
|----|------|-------|---------|-------------|--------|--------|----------------|
| saml-sso | SAML SSO | feature | | Single sign-on via Okta, Entra, and any SAML 2.0 IdP | https://example.com/security | clm-002 | 2026-07-07 |
