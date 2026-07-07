# Content Register

Your company-owned content, one row per asset. This is your findable asset library: which of
your published assets carries which messaging, down to the claim.

It answers "which of our assets support this messaging?" so anyone in sales or marketing can
find them. The builder populates it by running [jobs](../../builder/jobs/ingestion-log.md)
through the [parser](../../builder/parser.md): marketing surfaces land here, while customer
transcripts and competitor pages are parsed but not registered. The register is the result,
not something you maintain by hand.

The `components` column is the coarse link (what the asset discusses); the `claims` column is
the fine one (what it asserts, by `clm-` ID). Together they tell you, for any asset, exactly
which messaging it is carrying, and the [map](../claims-map.md) tells you whether that
messaging is canon.

Customer and market sources are out of scope here for now.

---

## Columns

- `id`: unique kebab-case slug for the asset. Derive it from the URL path (`/pricing` becomes `pricing`, a blog post keeps its slug) or, for captured files, the filename. Prefix with the sub-brand or section only when needed to stay unique.
- `title`: human-readable label
- `source`: the locator (URL or file path)
- `surface`: where the asset lives (see values below)
- `components`: the component IDs found in this asset, space-separated
- `claims`: the `clm-` IDs this asset carries, space-separated
- `last_scanned`: date the asset was last read, `YYYY-MM-DD`

## Surfaces

Company-owned content, by surface:

- `key_page`: core pages expected to carry full messaging (homepage, pricing, about, product pages, signup/contact-sales). These are the source for canon claims.
- `owned`: blog, docs, case studies, ebooks, sales decks
- `earned`: press, keynotes, podcast appearances, media placements
- `paid`: ads, sponsored content
- `internal`: positioning docs, messaging guides, sales enablement

Customer and market sources, by surface. These are parsed for signal but **not** registered
(they are not your published assets); they add [evidence](../evidence.md) and inform the
analyzer, not your asset library:

- `sales-call`: a sales or customer call transcript
- `customer`: a customer interview, win/loss, or support conversation
- `competitor`: a competitor's page, deck, or other material

---

## Register

*(the first row is an example; delete it when you add real content)*

| id | title | source | surface | components | claims | last_scanned |
|----|-------|--------|---------|------------|--------|--------------|
| example-homepage | Homepage | https://example.com | key_page | positioning category-name products value-proposition | clm-001 clm-002 | 2026-07-07 |
