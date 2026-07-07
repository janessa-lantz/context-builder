# Builder

Everything that writes into [context](../context/) and keeps it current. The builder reads a
job, fetches the source, parses it against the components, writes the result into context,
and compares what it finds against the canon to surface issues. Skills are the other side of
the line: they [read out of context](../skills%20-%20Work%20in%20Progress/) and never write into it.

## Elements

- **[parser.md](parser.md)**: how the builder works, step by step.
- **[raw-assets/](raw-assets/)**: the unprocessed source material it ingests (transcripts, scraped pages, documents).
- **[parsed-summaries/](parsed-summaries/)**: one summary per raw asset, mapping the asset to the components.
- **[issues/](issues/)**: issues the [analyzer](jobs/analyzer.md) and other runs surface, for you to act on.
- **[jobs/](jobs/)**: the recurring work you run, each executed the same way every time: the [ingestion log](jobs/ingestion-log.md) (the front door and router), [scans](jobs/scans/) (discover sources), the [analyzer](jobs/analyzer.md) (find drift), the [codify job](jobs/codify.md) (turn human corrections into context), and the [visual-identity job](jobs/visual-identity.md) (extract the brand's observable design facts).

## Flow

```
build:    job → raw asset → parsed summary → context (canon + index)
track:    competitive scans → parsed summaries → context (entities: profile + feed)
analyze:  analyzer → parsed summaries → issues
codify:   corrections + issues → codify → context (human-approved) + sharper specs
```

A [job](jobs/ingestion-log.md) names a source. The builder saves it as a **raw asset**,
writes a **parsed summary** that maps it to the components, and folds the result into
**context** (a row in the [content index](../context/content-index.md) for marketing surfaces,
and for key pages the [canon](../context/messaging-canon.md)).

**Issues** are produced separately by the [analyzer](jobs/analyzer.md), a job that reads
the parsed summaries and writes its findings to [issues/](issues/).

The **[codify job](jobs/codify.md)** closes the loop: it reads human corrections and the
open system themes in [issues/](issues/), and with human approval writes the learnings back
into context and into the specs, so each run makes the next one better.

The competitive scans maintain **[entities](../context/entities/)**: raw records of the
outside world, each with a current-state Profile and an accumulating Feed. Entities live in
context because they are knowledge the team draws from, but at a different trust level: raw
intelligence, never vetted messaging.
