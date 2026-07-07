# Parser

The builder's engine. It maps each raw asset against the
[claims register](../context/claims.md): it reads a source, captures the claims the asset
carries and the components they're typed by, and writes the result into context. It does not
invent messaging; it reads what is already there and files it.

## In and out

**In:** a pending job from the [ingestion log](jobs/ingestion-log.md), naming a source (a
URL or a file).

**Out:**
- a [parsed summary](parsed-summaries/) mapping the asset to components and claims
- for owned surfaces, minted or matched rows in the [claims register](../context/claims.md) and [evidence](../context/evidence.md) rows
- for marketing surfaces, rows in the [registers](../context/registers/): always [content](../context/registers/content.md), plus [customer-proof](../context/registers/customer-proof.md), [features](../context/registers/features.md), or [offers](../context/registers/offers.md) when the asset is that material
- for sales-call and customer sources, `private` [evidence](../context/evidence.md) rows on matched claims
- for competitor sources, an updated [entity](../context/entities/) Profile, kept raw and never registered or minted into claims
- the job marked `done` (or `skipped`), with a note on what it produced

## The run

1. Take the next `pending` job.
2. Fetch the source. A website: discover and pull the key pages (below). A transcript or document: read it directly, and save it to [raw-assets](raw-assets/) (hosted URLs stay where they live).
3. Classify the source by `surface` (see the [content register](../context/registers/content.md) for the values). Whether it is a marketing surface decides if it gets registered.
4. Extract against the [component definitions](../context/README.md). For each component, capture how it appears in this source, or record that it is absent. Put each section of content under exactly one component, and note secondary signals rather than double-filing. Within each component, capture the **claims**: every assertable statement, verbatim, and match each against the [claims register](../context/claims.md) — an existing claim (`clm-NNN`), a divergent phrasing of one (`variant-of:clm-NNN`), or `new`.
5. Write the [parsed summary](parsed-summaries/), then route by surface:
   - **key page**: mint `new` claims into the register as `canon`, add `public` evidence for every claim seen, write the content-register row; where the page is itself proof, feature, or offer material, add the matching register rows.
   - **other owned surfaces**: mint `new` claims as `candidate`, add `public` evidence, write the register rows.
   - **sales-call / customer**: add `private` evidence on matched claims only — never mint. Divergent customer framing is held for the analyzer, not filed as a claim.
   - **competitor**: update the entity Profile only.
6. Mark the job `done` and record the result (claims minted, evidence added, rows written).

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
and competitor material are parsed for signal but are **not** registered (they are not your
published assets), and they **never mint claims** — a prospect echoing your value proposition
is `private` [evidence](../context/evidence.md) on the matched claim; a prospect framing it
differently is signal for the analyzer. Classify them with a non-owned surface (`sales-call`,
`customer`, `competitor`) and parse them like this:

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

## Claims

The [claims register](../context/claims.md) is where extraction lands, and its rules govern
minting:

- **Mint from verbatim, company-published copy only**, source attributed. Key pages mint
  `canon`; other owned surfaces mint `candidate`. Non-owned sources never mint.
- **Match before minting.** The same statement seen again is evidence on the existing claim,
  not a new row. A close-but-different phrasing is a variant row (`variant_of` pointing at
  the primary), not a silent replacement — when key pages disagree (the homepage and pricing
  carry different positioning), the variant row *is* the flag; file the issue too.
- **Refresh, never overwrite.** On a re-run, stamp `last_confirmed` on claims still live.
  Never edit a `source: human` row; never retire a claim the scan can't find — leave
  `last_confirmed` stale and file an issue.

## Before you finish

- Every minted claim is verbatim from the source, attributed, and typed by exactly one component.
- Every evidence row carries its summary ID (or locator). No orphan evidence.
- Nothing was minted from a non-owned source.
- Every `value-drivers` entry maps to one of the four categories.
- `positioning` is the homepage claim only.
- `customer-proof` lists every named customer, not a truncated sample.
- `point-of-view` is a real belief, not a culture line.
- No gaps table and no "expected but not present" flags. Document what is there.
