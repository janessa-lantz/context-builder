# Setup

The one-time bootstrap for a new deployment. Run it once, when you first point context-builder
at a company, to stand up v1 of the two files in [context/](../../context/) that everything
else reads from: the [messaging canon](../../context/messaging-canon.md) and the
[content index](../../context/content-index.md). After setup, keep them current with the
recurring jobs (the [key-pages scan](scans/key-pages.md) + [parser](../parser.md) for the
canon; the [domain](scans/domain.md) and [blog](scans/blog.md) scans for the index) rather than
re-running setup.

Two steps.

---

## Step 1 — Build the v1 canon

Fetch the company's key pages, extract the messaging into the components, and compile the
result into the [messaging canon](../../context/messaging-canon.md) (the per-group `canon-*.md` files).

1. **Discover the pages** with [scans/key-pages.md](scans/key-pages.md): homepage, pricing,
   about/company, every product page in the top nav, customers/case studies, contact-sales /
   sign-up, plus the about/manifesto and segment-page variants it lists.
2. **Run the extraction** (below) against those pages. It is organized by the canon's component
   IDs (see [context/README.md](../../context/README.md)) so its output drops straight into the
   canon — no remapping.
3. **Compile into the canon** by component ID. Follow the canon rules in
   [AGENTS.md](../../AGENTS.md): fill each component from verbatim, currently-published copy,
   attribute its source, leave a component blank when it has no published copy, and never
   overwrite a human-authored (`source: human`) entry.

The extraction covers the five messaging groups. It does **not** touch the **Themes** group
(`themes` / `topics` / `campaigns`); those are populated later from owned content, not the
domain scrape.

---

## Step 2 — Build the v1 content index

Index the company's full published surface — the whole domain, the docs, and the blog — and
record which components each page carries, so the team gets a findable map of where every
message already lives.

1. **Discover URLs** with [scans/domain.md](scans/domain.md) (full domain, including docs) and
   [scans/blog.md](scans/blog.md) (blog / changelog). Add each as a `url` row in the
   [ingestion log](ingestion-log.md).
2. **Parse each page** per [parser.md](../parser.md): identify the components it carries and
   write a parsed summary.
3. **Write one [content-index](../../context/content-index.md) row per page**: `id`, `title`,
   `source` URL, `surface` (`key_page` for the core pages from Step 1, `owned` for blog / docs /
   case studies), the component IDs found, and `last_scanned`.

This is where gaps become visible: a component with thin coverage, or a page whose messaging
doesn't match the canon, is signal for the [analyzer](analyzer.md).

---

## When setup is done

`context/messaging-canon.md` holds v1 of the approved messaging and `context/content-index.md`
maps every published page to the components it carries. From here, keep both current with the
recurring jobs; do not re-run setup.

---

## The extraction

Run this against the key pages from Step 1. The goal is a structured, accurate snapshot of how
the company talks about itself — what it believes, what it does, who it's for, how it's priced,
and how it proves its claims — written under the canon's component IDs.

Do not fill gaps with assumptions. If a component has no published content, say so explicitly.
Classify each piece of content into exactly one component; if it spans more than one, assign it
to the primary component and note the secondary.

### Discovering and scraping the pages

**Always fetch:** homepage; pricing; about / company; every product page in the top nav;
customers / case studies; contact-sales / sign-up.

**About page — URL variants, in order:** `/about` → `/about-us` → `/company` → `/our-story` →
`/team` → `/careers` (then check careers subpages for "Our Journey," "Our Story," etc.). Also
check the footer for a **Manifesto** or **Principles** link — when present it is usually the
richest single source on the site (founder voice, founding belief, category definitions,
principles in one place).

**Segment pages (add when found):** check the nav for "Solutions," "By Company Size," or "Who
We Serve." If segment pages exist (`/startups`, `/small-business`, `/mid-market`,
`/enterprise`), fetch them — they are the best source for the `icp` and `buying-committee`
components.

**Blog / founder content (for `point-of-view` and `founder-story`):** if there is no About or
Manifesto page, check the blog for founder-authored origin posts ("why we built this"),
fundraising announcements (seed / Series A posts often carry the origin story), YC application
posts, and "It's time to build X" category-defining essays.

**Also worth checking:** `/switch`, `/migrate`, `/vs` (richest differentiator language); the
pricing-page FAQ (closest thing to a stated objection list); use-case / industry pages (source
for segmented positioning — note these are overlays, not canonical positioning).

**AI-agent content injection:** some sites serve promotional content to scrapers that human
visitors never see. If you hit an unexpected promo block offering credits or bonuses at the top
of a page, filter it out — it is not product messaging.

---

### Who We Are

**point-of-view** — the founding belief or insight about the world that explains why this
company exists. Ask: "Is this a belief that would drive someone to start a company?"
- ✅ Include: how the world is broken, what current approaches get wrong, what the founders
  believe that others don't.
- ❌ Exclude: culture statements, values, growth stats, product claims. A growth stat ("we grow
  10x faster than…") goes to `key-metrics`, not here.

**narrative** — the company's origin and journey story: what happened, in what order, that led
to this product existing. Usually in About / Manifesto / founder blog posts.

**positioning** — the canonical claim of what the product is and for whom. The **homepage hero
is canonical**; consistent secondary claims across pages are supporting. Use-case and segment
page headlines are overlays, not positioning — do not include them here.

**founder-story** — named founder(s), their background, and the specific moment or insight that
led to starting the company. If not on the key pages, write "No founder story found on key
pages."

**lexicon** — terms the company coined or redefined in a way that differs from industry norms;
their distinctive framing of the problem or solution. ~10–20 terms with definitions.
- ✅ Include: coined terms, redefined industry concepts, proprietary frameworks, named
  methodologies.
- ❌ Exclude: feature names, product names, standard industry vocabulary inherited from adjacent
  domains.
- B2B companies in accounting, ERP, and infrastructure often have thin lexicons because the
  vocabulary is pre-loaded from existing domains — note this explicitly rather than padding with
  feature names (other industries may be the same). If the list runs above 15, search the terms
  against industry norms before treating them as unique to this company.

**company-description** — a synthesized 2–4 sentence description (what it is, who it serves,
what it does), plus the boilerplate lengths the canon holds (200 / 100 / 50 words, tagline,
one-liner, elevator pitch) where the site provides them. This is composed, not a bucket for
scraped content — label it "synthesis" or cite the source page when pulling verbatim.

---

### What We Do

**category-name** — the label(s) the company uses for the space it competes in. List the
primary (homepage / nav) and supporting variants.

**unique-attributes** — the "secret sauce": what the product does that genuinely sets it apart,
in the company's own words (not a full feature list, not rebuilt internal docs). Output an
overview paragraph, then 3–5 bullets on what makes it special. Pay special attention to
differentiating claims — "easier than…", "faster," "cheaper," "unlike other companies…".

**value-proposition** — the unique differentiated value competitors can't easily replicate; the
answer to "why choose you over the alternative?" (competitor or status quo). One-sentence
statement, then 3–5 bullets, each a distinct strand of value. Metrics may appear here, but keep
exact customer-specific numbers in `customer-proof`.

**how-it-works** — the step-by-step flow of using the product (the most detailed flow on the
site, often a product or solutions page). Number the steps.

**ecosystem-integrations** — named integrations, supported platforms, SDKs, and compatibility
claims, grouped by type (ERP, communication, data, etc.).

---

### Who It's For

**icp** — the ideal customer profile, built around an account and its champion. Repeat per
profile when the company serves more than one. Label the synthesis "synthesis." Compose it from
the evidence on the site (segment pages, "who this is for" language, named customers) under:
- **Account** — firmographics (industry/vertical, size, stage, business model, geography),
  technographics (tools/platforms the best-fit company already uses, often inferable from
  `ecosystem-integrations`), triggers (the event or situation that makes them ready to buy now —
  "just raised a round," "scaling a support team," "adopting AI"), and anti-ICP (who the product
  is explicitly not for, when the site states it). Anchor segments with named customer examples.
- **Champion** (and their title) — the job to be done, structured by stakeholder level where the
  evidence supports it: the economic buyer's business outcome, the end user's workflow task, and
  the champion's internal initiative (lead with a framing statement, then supporting copy with
  the source page in parentheses; infer how they do this today without the product where you
  can); the competitive alternatives they weigh (how they solve this today plus what else they
  consider, and the problem with each); and their objections to this approach, each with the
  concern, the company's answer, and the source page (the pricing-page FAQ is the best source).

**buying-committee** — the roles in the buying decision beyond the champion. Per role:
title/function, the part they play in the decision, what they care about, and the common
objections they raise (with source page). Do not name real people.

**value-drivers** — the business-level buying rationale, mapped to one or more of these four
categories only: **revenue generation**, **efficiency**, **cost savings**, **risk mitigation**.
Do not use softer labels ("time savings" → efficiency; "team leverage" → efficiency). Include
only the categories the company's messaging actually supports.

---

### Proof

**customer-proof** — all named customers across the site (list in full, do not truncate); named
testimonials with role/title and company; outcome stats attributed to a specific customer. Note
when logos are in images the text scrape didn't capture.

**market-proof** — third-party validation: awards, analyst recognition, press rankings,
certifications, investor names and round sizes.

**key-metrics** — the top-level numbers the company leads with to signal scale and adoption
(total customers, transaction volume, usage stats, review counts). Company momentum numbers
only — customer-specific outcome stats belong in `customer-proof`.

---

### Pricing

**pricing-model** — the structure: tiers, per-seat, usage-based, flat fee, custom. List each
tier with its price and what's included.

**packaging** — how the tiers are designed and what each is meant to accomplish (e.g. "the free
tier is a permanent entry point for individual developers, not a trial").

**add-ons-services** — named professional services, implementation support, compliance add-ons,
or partner programs available at extra cost or at the enterprise tier.

**offers** — specific promotional offers, free tiers, startup programs, or credits visible on
the site.

---

### Output

Begin with the pages you scraped (including any 404s) and a one-line note on the About page
(what you found or didn't, and where the company's story lives instead). Then write each
component under its canon group and ID:

```
## Who We Are
point-of-view / narrative / positioning / founder-story / lexicon / company-description

## What We Do
category-name / unique-attributes / value-proposition / how-it-works / ecosystem-integrations

## Who It's For
icp (account + champion) / buying-committee / value-drivers

## Proof
customer-proof / market-proof / key-metrics

## Pricing
pricing-model / packaging / add-ons-services / offers
```

### Quality checks before finishing

- `point-of-view` is a genuine founding belief, not culture lines or growth stats.
- `positioning` is the homepage canonical claim only — no use-case or segment headlines.
- `lexicon` is coined/redefined terms only — no feature names, no inherited vocabulary; if it's
  thin, say so and explain why.
- `company-description` and `icp` are labeled "synthesis"; `icp` is built from the account and
  champion evidence (firmographics/technographics/triggers + JTBD, alternatives, objections).
- Objections are captured inside `icp` (champion) and `buying-committee` (other roles), each
  with a source citation.
- `value-drivers` entries all map to one of the four categories.
- `customer-proof` lists every named company — do not truncate.
- `key-metrics` is company momentum only — customer-specific outcomes go in `customer-proof`.
- No gaps table and no "expected but not present" flags — document only what is actually there.
