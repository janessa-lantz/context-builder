# Builder

The engine that turns jobs into context, and flags where messaging breaks down. It reads a
job, fetches the source, parses it against the components, writes the result into context,
and compares what it finds against the canon to surface issues.

## Elements

- **[parser.md](parser.md)**: how the builder works, step by step.
- **[raw-assets/](raw-assets/)**: the unprocessed source material it ingests (transcripts, scraped pages, documents).
- **[parsed-summaries/](parsed-summaries/)**: one summary per raw asset, mapping the asset to the components.
- **[entities/](entities/)**: durable records of the outside world you track (competitors first), kept raw and never treated as vetted messaging.
- **[issues/](issues/)**: messaging issues the [analyzer](../jobs/analyzer.md) surfaces, for you to act on.

## Flow

```
build:    job → raw asset → parsed summary → context (canon + index)
track:    competitive scans → parsed summaries → entities (profile + feed)
analyze:  analyzer → parsed summaries → issues
```

A [job](../jobs/ingestion-log.md) names a source. The builder saves it as a **raw asset**,
writes a **parsed summary** that maps it to the components, and folds the result into
**context** (a row in the [content index](../context/content-index.md) for marketing surfaces,
and for key pages the [canon](../context/messaging-canon.md)).

**Issues** are produced separately by the [analyzer](../jobs/analyzer.md), a job that reads
the parsed summaries and writes its findings to [issues/](issues/).

The builder also keeps **[entities](entities/)**: raw records of the outside world the
competitive scans track, each with a current-state Profile and an accumulating Feed. They stay
in the builder and are never folded into vetted context.
