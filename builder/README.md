# Builder

The engine that turns jobs into context, and flags where messaging breaks down. It reads a
job, fetches the source, parses it against the components, writes the result into context,
and compares what it finds against the canon to surface issues.

## Elements

- **[parser.md](parser.md)**: how the builder works, step by step.
- **[raw-assets/](raw-assets/)**: the unprocessed source material it ingests (transcripts, scraped pages, documents).
- **[parsed-summaries/](parsed-summaries/)**: one summary per raw asset, mapping the asset to the components.
- **[issues/](issues/)**: messaging issues the builder surfaces, for you to act on.

## Flow

```
job → raw asset → parsed summary → context (canon + index) → issues
```

A [job](../jobs/ingestion-log.md) names a source. The builder saves it as a **raw asset**, writes a
**parsed summary** that maps it to the components, and folds the result into **context** (a
row in the [content index](../context/content-index.md) for marketing surfaces, and for key
pages the [canon](../context/messaging-canon.md)). It then compares what it found against the
canon and records any **issues**.
