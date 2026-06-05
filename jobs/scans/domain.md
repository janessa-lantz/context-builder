# Domain Scan

Crawls a full company domain to discover every page worth ingesting.

## Targets

- domain:

## Discovering pages

- Pull the **sitemap index** (try `/sitemap.xml`) and follow it into its sub-sitemaps; each
  `<loc>` is a candidate `url` job.
- A company's sub-brands may live on the main domain (their own sub-sitemap) and/or a separate
  domain. List every domain under Targets.
- **No XML sitemap?** Link-crawl from the homepage (nav + footer). Common for standalone
  product or sub-brand sites.
- **Out of scope:** category/tag archives and pagination — they list other pages, they aren't
  pages themselves. Leave them unqueued.

## Ignore on future scans

Do not re-queue pages the parser already judged non-substantive. Seed this from past `skipped`
results and keep two forms:

- **Patterns** — categories that are never a messaging surface, applied as discovery-time
  filters: legal/policy pages (terms, privacy, disclaimer), versioned or archived duplicates
  (`/.../<version>/`, `/.../versions/`), pagination.
- **Specific URLs** — judgment calls that don't generalize, where sibling pages of the same
  type were indexed (a blanket pattern would over-exclude). List the exact URLs; still
  evaluate newly added pages of that type on their own merits.

Leave both empty until a run produces skips.
