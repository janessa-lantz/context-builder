# Scans

A scan is a job that discovers sources and feeds them into the
[ingestion log](../ingestion-log.md) as `url` inputs. A scan finds what to ingest; it does
not parse or index anything itself. Each URL it finds becomes a row in the ingestion log,
tagged with the scan's id.

Each scan is paired with the targets it should crawl. Fill in the targets in the scan's file,
run it, and it queues a `url` job per source it finds.

Four scans to start:

- **[key-pages](key-pages.md)**: your load-bearing company pages; the source for the canon
- **[competitive](competitive.md)**: competitor domains
- **[domain](domain.md)**: a full company domain
- **[blog](blog.md)**: a blog

What each scan crawls precisely is still to be defined.
