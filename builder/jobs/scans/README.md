# Scans

A scan is a job that discovers sources and feeds them into the
[ingestion log](../ingestion-log.md) as `url` inputs. A scan finds what to ingest; it does
not parse or index anything itself. Each URL it finds becomes a row in the ingestion log,
tagged with the scan's id.

Each scan is paired with the targets it should crawl. Fill in the targets in the scan's file,
run it, and it queues a `url` job per source it finds.

Scans split by where their output lands. Inward scans feed your own context (the canon and
content index). Outward scans feed [entities](../../../context/entities/), the raw record of the
outside world you track.

Inward:

- **[key-pages](key-pages.md)**: your core company pages; the source for the canon
- **[domain](domain.md)**: a full company domain
- **[blog](blog.md)**: a blog

Outward:

- **[competitive-profile](competitive-profile.md)**: competitor key pages, parsed against all components, into each competitor's entity Profile
- **[competitive-feed](competitive-feed.md)**: competitor changes (product, pricing, messaging, funding, partnerships, hiring, press), into each competitor's entity Feed

What each scan crawls precisely is still to be defined.

## Ignoring known non-substantive pages

A re-run should not re-queue pages the parser already judged non-substantive. Each scan keeps
an **ignore list** (see [domain](domain.md)), seeded from past `skipped` results:

- **Patterns** for categories that are never a messaging surface: legal/policy pages,
  versioned or archived duplicates, pagination.
- **Specific URLs** for judgment calls that don't generalize, where sibling pages of the same
  type were kept (a blanket pattern would over-exclude).

Skips flow back from the [parser](../../parser.md): what it marks `skipped`, the scan
stops discovering.
