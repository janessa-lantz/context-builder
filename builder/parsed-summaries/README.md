# Parsed Summaries

One summary per raw asset, mapping the asset to the messaging components. The summary is the
builder's record of everything it found in that asset, and it is the durable artifact you
keep (see [raw assets](../raw-assets/) for why the source itself usually isn't stored).

The [content index](../../context/content-index.md) is built by aggregating these summaries:
each summary's frontmatter becomes one index row.

Each summary is a markdown file named by the asset id, with frontmatter and a body.

## Frontmatter

- `id`: matches the filename and the content-index row
- `source`: the locator (a URL for hosted, a file path for captured)
- `surface`: where the asset lives (see the content index)
- `ingested`: date the asset came in
- `parsed`: date it was parsed
- `components_version`: which version of the components was used
- one field per component id: a short note on how that component appears in this asset, or `null` if absent

For `sales-call` and `customer` sources, also include:

- `discovery-channel`: how this source first found the company (first touch, not how they got to today's meeting), or `null`
- `icp-fit`: `yes` when the source is your ideal customer, or `no` with a short reason (a channel/reseller partner, a procurement-side buyer, an out-of-segment company). Flagging non-ICP keeps the analyzer from treating an off-profile call as a pattern.

## Body

- one section per component that was found, with the full extracted content
- a `Confidence notes` section flagging anything the parser was unsure about, with the reason

## Example

```markdown
---
id: homepage
source: https://example.com
surface: key_page
ingested: 2026-06-04
parsed: 2026-06-04
components_version: 1
positioning: Positions as the simplest way for ops teams to close the books
category-name: Calls the space "close management"
capabilities: Three named modules (import, review, sign-off)
point-of-view: null
pricing-model: null
---

## positioning
[the full positioning language found on the page]

## capabilities
[the full capability content found on the page]

## Confidence notes
- differentiators: unclear whether "unlike legacy tools" is a real competitive frame or generic copy
```
