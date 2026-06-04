# Content Index

Every piece of content that exists, one row per asset. This is the current-state registry:
what content the company has, and which messaging components each piece carries.

It answers "what do we have, and what's in it?" The builder populates it by running
[jobs](../jobs/ingestion-log.md) through the [parser](../builder/parser.md). The index is the
result, not something you maintain by hand.

The `components` column references the component IDs defined in this folder's
[README](README.md). That link is the point of the index: it tells you, for any asset,
exactly which messaging it is carrying.

---

## Columns

- `id`: unique kebab-case slug for the asset
- `title`: human-readable label
- `source`: the locator (URL or file path)
- `ledger`: `company`, `customer`, or `market` (see values below)
- `surface`: the specific source type within that ledger (see values below)
- `components`: the component IDs found in this asset, space-separated
- `last_scanned`: date the asset was last read, `YYYY-MM-DD`

## Controlled values

**ledger / surface**

- `company` (what the company says about itself): `key_page`, `owned`, `earned`, `paid`, `internal`
- `customer` (what customers and prospects say): `sales_call`, `customer_interview`, `review`, `support`, `organic`
- `market` (what the market says about the category): `competitor`, `analyst`, `media`, `discourse`

`key_page` is reserved for the load-bearing pages expected to carry full messaging (homepage,
pricing, about, product pages, signup/contact-sales). These are the source for the messaging
canon.

---

## Index

*(the first row is an example; delete it when you add real content)*

| id | title | source | ledger | surface | components | last_scanned |
|----|-------|--------|--------|---------|------------|--------------|
| example-homepage | Homepage | https://example.com | company | key_page | positioning category-name capabilities differentiators value-drivers | 2026-06-04 |
