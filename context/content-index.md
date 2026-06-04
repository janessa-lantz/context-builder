# Content Index

Your company-owned content, one row per asset. This is your findable asset library: which of
your published assets carries which messaging.

It answers "which of our assets support this messaging?" so anyone in sales or marketing can
find them. The builder populates it by running [jobs](../jobs/ingestion-log.md) through the
[parser](../builder/parser.md): marketing surfaces land here, while customer transcripts and
competitor pages are parsed but not indexed. The index is the result, not something you
maintain by hand.

The `components` column references the component IDs defined in this folder's
[README](README.md). That link is the point of the index: it tells you, for any asset,
exactly which messaging it is carrying.

Customer and market sources are out of scope here for now.

---

## Columns

- `id`: unique kebab-case slug for the asset
- `title`: human-readable label
- `source`: the locator (URL or file path)
- `surface`: where the asset lives (see values below)
- `components`: the component IDs found in this asset, space-separated
- `last_scanned`: date the asset was last read, `YYYY-MM-DD`

## Surfaces

Company-owned content, by surface:

- `key_page`: load-bearing pages expected to carry full messaging (homepage, pricing, about, product pages, signup/contact-sales). These are the source for the canon.
- `owned`: blog, docs, case studies, ebooks, sales decks
- `earned`: press, keynotes, podcast appearances, media placements
- `paid`: ads, sponsored content
- `internal`: positioning docs, messaging guides, sales enablement

Customer and market sources, by surface. These are parsed for signal but **not** indexed (they are not your published assets); they inform the canon and the analyzer, not your asset library:

- `sales-call`: a sales or customer call transcript
- `customer`: a customer interview, win/loss, or support conversation
- `competitor`: a competitor's page, deck, or other material

---

## Index

*(the first row is an example; delete it when you add real content)*

| id | title | source | surface | components | last_scanned |
|----|-------|--------|---------|------------|--------------|
| example-homepage | Homepage | https://example.com | key_page | positioning category-name product capabilities differentiators value-drivers | 2026-06-04 |
