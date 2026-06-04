# Parser

The builder's engine. It takes one job (a source), extracts the messaging components present,
and writes the result into context. It does not invent messaging. It reads what is already
there and files it.

## In and out

**In:** a pending job from [`../jobs/jobs.md`](../jobs/jobs.md), naming a source (a URL or a
file).

**Out:**
- a row in [`../context/content-index.md`](../context/content-index.md) listing the component IDs found
- for key pages, updated entries in [`../context/messaging/messaging-canon.md`](../context/messaging/messaging-canon.md)
- the job marked `done` (or `skipped`), with a note on what it produced

## The run

1. Take the next `pending` job.
2. Fetch the source. A website: discover and pull the key pages (below). A transcript or document: read it directly.
3. Classify the source into a `ledger` and `surface` (see the content index for the values).
4. Extract against the components in [`../context/messaging/messaging-components.md`](../context/messaging/messaging-components.md). For each component, capture how it appears in this source, or record that it is absent. Put each section of content under exactly one component, and note secondary signals rather than double-filing.
5. Write to context: add or update the source's row in the content index, and for key pages fold the extraction into the canon.
6. Mark the job `done` and record the result.

Rule throughout: do not fill gaps with assumptions. If a component is absent, say so. Absence
is a signal, not a hole to patch.

## Discovering pages (websites)

Always fetch: homepage, pricing, about or company, every product page in the top nav,
customers or case studies, contact-sales or sign-up.

For the about page, try in order: `/about`, `/about-us`, `/company`, `/our-story`, `/team`,
`/careers`. Check the footer for a Manifesto or Principles link. When present it is usually
the richest single source on the site.

Add when found:
- segment pages (`/startups`, `/enterprise`, "Who We Serve") for `account` and `buying-committee`
- `/vs`, `/switch`, `/migrate` for `differentiators`
- the pricing FAQ for `objections`

If there is no about or manifesto page, check the blog for founder posts, fundraising
announcements, or category-defining essays for `point-of-view` and `founder-story`.

## Classification notes

A few components are easy to confuse. The lines that matter:

- `point-of-view` is a founding belief about the world, not culture statements or growth stats. A growth stat belongs in `key-metrics`.
- `positioning` is the homepage canonical claim. Use-case and segment headlines are overlays, not positioning.
- `lexicon` is only coined or redefined terms, not feature names or inherited industry vocabulary. If the lexicon is thin, say so rather than padding it.
- `benefits` are product-level outcomes ("90% of transactions auto-coded"). `value-drivers` are business-level rationale, and each must map to revenue generation, efficiency, cost savings, or risk mitigation.
- `differentiators` need a competitive frame ("vs. X," "the only platform that..."). "Easy to use" is not a differentiator without a comparison.
- `customer-proof` is customer-specific outcomes. `key-metrics` and `social-proof` are company-level momentum numbers.
- `jobs-to-be-done`: separate the economic buyer's outcome, the end user's task, and the champion's initiative where the evidence supports it.

## The canon

The [canon](../context/messaging/messaging-canon.md) is derived, not authored separately. It
is compiled from the key-page extractions: one canonical statement per component, rolled up
from every key page where that component appears. When key pages disagree (the homepage and
pricing carry different positioning), flag the divergence rather than quietly picking one.
Re-run the canon when key pages change.

## Before you finish

- Every `value-drivers` entry maps to one of the four categories.
- `positioning` is the homepage claim only.
- `customer-proof` lists every named customer, not a truncated sample.
- `point-of-view` is a real belief, not a culture line.
- No gaps table and no "expected but not present" flags. Document what is there.
