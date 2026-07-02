# Parser

The builder's engine. It maps each raw asset against your messaging canon: it reads a source,
finds which components the asset carries, and writes the result into context. It does not
invent messaging; it reads what is already there and files it.

## In and out

**In:** a pending job from the [ingestion log](jobs/ingestion-log.md), naming a source (a
URL or a file).

**Out:**
- a [parsed summary](parsed-summaries/) mapping the asset to the components
- for marketing surfaces, a row in the [content index](../context/content-index.md), aggregated from that summary
- for key pages, updated entries in the [canon](../context/messaging-canon.md)
- for competitor sources, an updated [entity](../context/entities/) Profile, kept raw and never indexed or folded into the canon
- the job marked `done` (or `skipped`), with a note on what it produced

## The run

1. Take the next `pending` job.
2. Fetch the source. A website: discover and pull the key pages (below). A transcript or document: read it directly, and save it to [raw-assets](raw-assets/) (hosted URLs stay where they live).
3. Classify the source by `surface` (see the content index for the values). Whether it is a marketing surface decides if it gets indexed.
4. Extract against the [component definitions](../context/README.md). For each component, capture how it appears in this source, or record that it is absent. Put each section of content under exactly one component, and note secondary signals rather than double-filing.
5. Write the [parsed summary](parsed-summaries/). For marketing surfaces, aggregate it into a content index row; for key pages, fold it into the canon.
6. Mark the job `done` and record the result.

Rule throughout: do not fill gaps with assumptions. If a component is absent, say so. Absence
is a signal, not a hole to patch.

## Discovering pages (websites)

Discover key pages per [key-pages](jobs/scans/key-pages.md): the always-fetch list, the
about-page variants, segment pages, and the competitive and FAQ pages worth checking. The
same guidance serves the competitive-profile scan pointed at a competitor's domain.

## Working through a large queue

A full-domain scan queues hundreds of pages of uneven value. Parse by expected signal rather
than treating every job the same:

- **Rich**: homepage, pricing, about, product, segment, and blog pages: full extraction
  across every component the page carries.
- **Light**: repetitive or low-signal pages (near-duplicate variants, versioned or archived
  copies, thin technical or changelog notes): a focused pass for product, capabilities,
  positioning, and metrics. If the page carries no distinct message, mark it `skipped`.

Skip rather than pad. A near-duplicate of a page you already parsed, a legal/policy page, or a
purely technical note is `skipped` with a one-line reason, not a thin summary. Every skip is a
signal: feed the skipped URLs back to the scan's ignore list (see [scans](jobs/scans/README.md))
so the next run does not re-queue them.

## Sales calls and other non-marketing sources

Not every source is your own marketing. Sales-call and customer transcripts, win/loss notes,
and competitor material are parsed for signal but are **not** indexed (they are not your
published assets). Classify them with a non-owned surface (`sales-call`, `customer`,
`competitor`) and parse them like this:

- **The prospect's own words are the signal.** Quote them and attach a timestamp or location. Your paraphrase is the last resort.
- **1:1 with this source.** Never reference another call, customer, or source by name inside a summary, even when a connection feels obvious. Cross-source patterns are the analyzer's job, not the parser's. If you notice one, hold it.
- **Capture every objection**, even the ones handled well. Patterns across calls matter more than how any single one went.
- **"Nothing to note"** for a section with no finding, so a reader knows you looked and found nothing rather than skipped it.

For a sales or customer call, the components that usually carry signal are `icp` (who the
buyer is, the champion's job to be done, the alternatives they weigh, and their objections),
`buying-committee` (who else is involved in the decision, and their objections),
`value-drivers` (the business rationale), and any competitor or alternative they mention
(signal for that competitor's [entity](../context/entities/) Feed). The company-side
components (products, unique-attributes, positioning, proof) appear only where the seller
described them; record those as the seller's framing, not as approved messaging.

Two fields specific to these sources (see the [parsed summary](parsed-summaries/) frontmatter):

- **`discovery-channel`** = first touch: how this person originally found the company, not how they reached today's meeting. Minor in one summary; across all of them it reveals which channels actually convert.
- **`icp-fit`** = whether the source is your ideal customer. Flag the ones that are **not** (a channel/reseller partner, a procurement-side buyer, an out-of-segment company) with a short reason, so an off-profile call is not mistaken for a pattern.

## Classification notes

A few components are easy to confuse. The lines that matter:

- `point-of-view` is a founding belief about the world, not culture statements or growth stats. A growth stat belongs in `key-metrics`.
- `positioning` is the homepage canonical claim. Use-case and segment headlines are overlays, not positioning.
- `lexicon` (coined or redefined terms, not feature names or inherited vocabulary) is written to brand-writing-identity, not the canon. If it is thin, say so rather than padding it.
- Product-level outcomes ("90% of transactions auto-coded") belong in `value-proposition`. `value-drivers` are business-level rationale, and each must map to revenue generation, efficiency, cost savings, or risk mitigation.
- `unique-attributes` and `value-proposition` need a competitive frame ("vs. X," "the only platform that..."). "Easy to use" is not differentiation without a comparison.
- `customer-proof` is customer-specific outcomes. `key-metrics` is company-level momentum numbers; `market-proof` is institutional recognition.
- Inside `icp`, separate the economic buyer's outcome, the end user's task, and the champion's initiative where the evidence supports it.

## The canon

The [canon](../context/messaging-canon.md) holds two kinds of entry. What the LLM compiles is
derived from the key-page extractions: one canonical statement per component, rolled up from
every key page where that component appears, quoted verbatim and attributed. What a human adds
is synthesis and context, marked `source: human`. On a re-run, refresh the verbatim entries and
never overwrite a human-authored one. When key pages disagree (the homepage and pricing carry
different positioning), flag the divergence rather than quietly picking one.

## Before you finish

- Every `value-drivers` entry maps to one of the four categories.
- `positioning` is the homepage claim only.
- `customer-proof` lists every named customer, not a truncated sample.
- `point-of-view` is a real belief, not a culture line.
- No gaps table and no "expected but not present" flags. Document what is there.
