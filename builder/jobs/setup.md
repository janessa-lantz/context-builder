# Setup

The one-time bootstrap for a new deployment. Run it once, when you first point context-builder at a company. It stands up the [messaging canon](../../context/messaging-canon.md) and the [content index](../../context/content-index.md), then baselines the [issues backlog](../issues/README.md). After setup, keep them current with the recurring jobs, not by re-running setup.

Three steps.

---

## Step 1: Build the v1 canon

Fetch the company's key pages, extract the messaging into the components, and compile the result into the [messaging canon](../../context/messaging-canon.md) (the per-group `canon-*.md` files).

1. **Discover the pages** with [scans/key-pages.md](scans/key-pages.md): homepage, pricing, about/company, every product page in the top nav, customers/case studies, contact-sales / sign-up, plus the about and segment-page variants it lists.
2. **Run the extraction** (below) against those pages. It is organized by component ID (see [context/README.md](../../context/README.md)), so its output drops straight into the canon.
3. **Compile into the canon** by component ID. The extraction's output is written directly into the per-group `canon-*.md` files; there is no intermediate artifact to file. Follow the canon rules in [AGENTS.md](../../AGENTS.md): fill each component from verbatim, currently-published copy, attribute the source, leave a component blank when it has no published copy, and never overwrite a `source: human` entry.
4. **Log and index the pages.** One `url` row per key page in the [ingestion log](ingestion-log.md) (result: "canon extraction"), and one [content-index](../../context/content-index.md) row per key page (`surface: key_page`, components from the extraction).

The extraction covers every group except Themes (see below). It also extracts `lexicon`, which is written to [brand-writing-identity.md](../../context/brand-writing-identity.md), not the canon.

---

## Step 2: Build the v1 content index

Index the company's full published surface (the whole domain, the docs, and the blog) and record which components each page carries, so the team gets a findable map of where every message already lives.

1. **Discover URLs** with [scans/domain.md](scans/domain.md) and [scans/blog.md](scans/blog.md). Add each as a `url` row in the [ingestion log](ingestion-log.md). The domain scan will rediscover the Step 1 key pages; they are already logged and indexed, so skip them rather than parsing them twice.
2. **Parse each page** per [parser.md](../parser.md): identify the components it carries and write a parsed summary.
3. **Write one [content-index](../../context/content-index.md) row per page**: `id`, `title`, `source` URL, `surface` (`owned` for blog, docs, and case studies), the component IDs found, and `last_scanned`.

Gaps become visible here. A component with thin coverage, or a page whose messaging does not match the canon, is signal for the [analyzer](analyzer.md).

---

## Step 3: Baseline the issues

Run the [analyzer](analyzer.md) once over what setup built, so the team starts with a real backlog instead of an empty file.

With only your own pages parsed, two of its four comparisons have data:

- **missing**: components with no canon entry. The sharpest v1 finding: what the site does not say.
- **misaligned**: a published page that says something different from the canon.

`mismatched` needs customer sources and `competitive` needs competitor Profiles; neither exists yet. Do not force findings the data cannot support. Those comparisons start working as transcripts and competitive scans are ingested.

---

## When setup is done

The canon holds v1 of the approved messaging, the content index maps every published page to the components it carries, and the issues backlog holds the baseline findings. From here, keep them current with the recurring jobs. Do not re-run setup.

Setup deliberately leaves parts of context empty:

- **Visual identity**: run the [visual-identity job](visual-identity.md) next; it is this job's visual counterpart.
- **Voice and guardrails**: human-authored in [brand-writing-identity.md](../../context/brand-writing-identity.md); setup fills only the lexicon.
- **Themes** (`themes`, `topics`, `campaigns`): populated later from owned content, not the domain scrape.
- **Entities**: run the [competitive scans](scans/) when you are ready to track competitors.

---

## The extraction

Run this against the Step 1 key pages, discovered per [scans/key-pages.md](scans/key-pages.md). The goal is an accurate snapshot of how the company talks about itself, written under the canon's component IDs.

Do not fill gaps with assumptions. If a component has no published content, say so. Put each piece of content under exactly one component; if it spans more than one, assign the primary and note the secondary.

---

### Who We Are

**point-of-view:** the founding belief about the world that explains why the company exists. Ask: "Is this a belief that would drive someone to start a company?"
- ✅ Include: how the world is broken, what current approaches get wrong, what the founders believe that others don't.
- ❌ Exclude: culture statements, values, growth stats, product claims. A growth stat ("we grow 10x faster than…") goes to `key-metrics`.

**narrative:** the origin and journey story, in order, that led to this product. Usually in About, Manifesto, or founder blog posts.

**positioning:** the canonical claim of what the product is and for whom. The homepage hero is canonical; consistent secondary claims across pages are supporting. Use-case and segment headlines are overlays, not positioning.

**founder-story:** named founder(s), their background, and the moment or insight that led to starting the company. If not on the key pages, write "No founder story found on key pages."

**company-description:** a synthesized 2-4 sentence description (what it is, who it serves, what it does), plus the boilerplate lengths the canon holds (200, 100, and 50 words, tagline, one-liner, elevator pitch) where the site provides them. Composed, not a bucket for scraped content. Label it "synthesis" or cite the source when pulling verbatim.

---

### What We Do

**category-name:** the label(s) the company uses for the space it competes in. List the primary (homepage or nav) and supporting variants.

**products:** the discrete offerings in the portfolio: the umbrella name, then one entry per product (what it is and how it relates to the others). Pull from the top nav and product pages. A single-product company gets a single entry.

**unique-attributes:** the "secret sauce," what the product does that genuinely sets it apart, in the company's own words (not a full feature list). Output an overview paragraph, then 3-5 bullets on what makes it special. Watch for differentiating claims: "easier than…", "faster," "cheaper," "unlike other companies…".

**value-proposition:** the unique differentiated value competitors can't easily replicate; the answer to "why choose you over the alternative?" (competitor or status quo). A one-sentence statement, then 3-5 bullets, each a distinct strand of value. Keep exact customer-specific numbers in `customer-proof`.

**how-it-works:** the step-by-step flow of using the product, taken from the most detailed flow on the site. Number the steps.

**ecosystem-integrations:** named integrations, supported platforms, SDKs, and compatibility claims, grouped by type (ERP, communication, data).

---

### Who It's For

**icp:** the ideal customer profile, built around an account and its champion. Repeat per profile when the company serves more than one. Label it "synthesis." Compose it from the evidence on the site (segment pages, "who this is for" language, named customers):
- **Account:** firmographics (industry, size, stage, business model, geography), technographics (tools the best-fit company already uses, often inferable from `ecosystem-integrations`), triggers (the event that makes them ready to buy, like "just raised a round" or "scaling a support team"), and anti-ICP (who the product is explicitly not for, when stated). Anchor segments with named customer examples.
- **Champion** (and their title): the job to be done (the economic buyer's business outcome, the end user's workflow task, the champion's internal initiative); the competitive alternatives they weigh (how they solve this today, what else they consider, and the problem with each); and their objections to this approach, each with the concern, the company's answer, and the source page (the pricing-page FAQ is the best source).

**buying-committee:** the roles in the buying decision beyond the champion. Per role: title, the part they play, what they care about, and the common objections they raise (with source page). Do not name real people.

**value-drivers:** the business-level buying rationale, mapped to one or more of four categories only: **revenue generation**, **efficiency**, **cost savings**, **risk mitigation**. Do not use softer labels ("time savings" maps to efficiency). Include only the categories the messaging supports.

---

### Proof

**customer-proof:** every named customer across the site (list in full); named testimonials with role, title, and company; outcome stats attributed to a specific customer. Note when logos are in images the text scrape missed.

**market-proof:** third-party validation: awards, analyst recognition, press rankings, certifications, investor names and round sizes.

**key-metrics:** the top-level numbers the company leads with to signal scale and adoption (total customers, transaction volume, usage stats, review counts). Company momentum only; customer-specific outcomes go in `customer-proof`.

---

### Pricing

**pricing-model:** the structure (tiers, per-seat, usage-based, flat fee, custom). List each tier with its price and what's included.

**packaging:** how the tiers are designed and what each is meant to accomplish (e.g. "the free tier is a permanent entry point for individual developers, not a trial").

**add-ons-services:** named professional services, implementation support, compliance add-ons, or partner programs available at extra cost or at the enterprise tier.

**offers:** specific promotional offers, free tiers, startup programs, or credits visible on the site.

---

### Brand writing identity

**lexicon:** terms the company coined or redefined in a way that differs from industry norms. Around 10 to 20 terms with definitions. Write these to [brand-writing-identity.md](../../context/brand-writing-identity.md), not the canon.
- ✅ Include: coined terms, redefined industry concepts, proprietary frameworks, named methodologies.
- ❌ Exclude: feature names, product names, standard industry vocabulary inherited from adjacent domains.
- Accounting, ERP, and infrastructure companies often have thin lexicons because the vocabulary is pre-loaded from existing domains. Note that rather than padding with feature names. If the list runs above 15, check the terms against industry norms before treating them as unique to this company.

---

### Output

Begin with the pages you scraped (including any 404s) and a one-line note on the About page (what you found, and where the company's story lives instead). Then write each component under its group and ID:

```
## Who We Are
point-of-view / narrative / positioning / founder-story / company-description

## What We Do
category-name / products / unique-attributes / value-proposition / how-it-works / ecosystem-integrations

## Who It's For
icp (account + champion) / buying-committee / value-drivers

## Proof
customer-proof / market-proof / key-metrics

## Pricing
pricing-model / packaging / add-ons-services / offers

## Brand writing identity
lexicon
```

### Quality checks before finishing

- `point-of-view` is a genuine founding belief, not culture lines or growth stats.
- `positioning` is the homepage canonical claim only, no use-case or segment headlines.
- `lexicon` is coined or redefined terms only, written to brand-writing-identity, not the canon. If it's thin, say so and explain why.
- `company-description` and `icp` are labeled "synthesis." `icp` is built from the account and champion evidence.
- Objections are captured inside `icp` (champion) and `buying-committee` (other roles), each with a source citation.
- `value-drivers` entries all map to one of the four categories.
- `customer-proof` lists every named company.
- `key-metrics` is company momentum only; customer-specific outcomes go in `customer-proof`.
- No gaps table and no "expected but not present" flags. Document only what is there.
