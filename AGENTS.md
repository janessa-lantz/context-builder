# Operating context-builder

You are an AI coding agent operating this repo. context-builder turns a company's scattered
messaging into one structured source of truth. This file is the entry point: it tells you how
to run the system. The detailed specs live in each section's files, linked below.

## The model

- **[context/](context/)** is the source of truth: the messaging **canon** (built on the components defined in [context/README.md](context/README.md)) and the **content index** of company-owned assets. This is what the team and their AI tools draw from.
- **[builder/](builder/)** is the engine and its materials: the [parser](builder/parser.md), [raw-assets](builder/raw-assets/), [parsed-summaries](builder/parsed-summaries/), [entities](builder/entities/), and [issues](builder/issues/).
- **[jobs/](jobs/)** is the work you run: the [ingestion log](jobs/ingestion-log.md) (router), [scans](jobs/scans/), and the [analyzer](jobs/analyzer.md).

## What to do when the user asks

- **"Build or refresh our canon"** → run the key-pages flow. Read [jobs/scans/key-pages.md](jobs/scans/key-pages.md) for the targets, fetch the key pages, parse each per [builder/parser.md](builder/parser.md), and compile the canon ([context/messaging-canon.md](context/messaging-canon.md)) from the key-page extractions.
- **"Add this source"** (a URL, transcript, or PDF) → append a row to [jobs/ingestion-log.md](jobs/ingestion-log.md), then follow [builder/parser.md](builder/parser.md): save captured sources to [builder/raw-assets/](builder/raw-assets/), write a parsed summary to [builder/parsed-summaries/](builder/parsed-summaries/), and for marketing surfaces add a [content-index](context/content-index.md) row.
- **"Run the key-pages / domain / blog scan"** → read the scan's file in [jobs/scans/](jobs/scans/) for its targets, discover the URLs, and add each as a `url` row in the ingestion log.
- **"Run the competitive scans"** → [competitive-profile](jobs/scans/competitive-profile.md) parses each competitor's key pages into that competitor's [entity](builder/entities/) Profile; [competitive-feed](jobs/scans/competitive-feed.md) appends Feed rows for new competitor signals. Competitor intelligence is raw: it lands in [builder/entities/](builder/entities/), never the canon or index.
- **"Find issues" or "what's off in our messaging"** → run the analyzer per [jobs/analyzer.md](jobs/analyzer.md): read the parsed summaries and the canon, and write themes to [builder/issues/](builder/issues/).

## Rules you must follow

- **The canon records only what IS.** Populate each component from verbatim, currently-published copy, attributed to its source. If there is no published copy for a component, leave it blank. Never invent, draft, or aspirational-fill messaging in the canon.
- **Nothing is indexed without being parsed.** Only marketing surfaces (company-owned content) go in the content index. Customer transcripts and competitor pages are parsed but not indexed.
- **Entities are raw, never vetted.** Competitor and other entity pages live in the builder. Never treat them as approved messaging or ship their text. Anything shippable is a separate, human-vetted artifact built on top.
- **Do not fill gaps with assumptions.** If a component is absent from a source, say so. Absence is a signal, not a hole to patch.
- **Reference components by their ID** (the kebab-case slugs in [context/README.md](context/README.md)).

## Where the detail lives

| To understand | Read |
|---|---|
| the components and their IDs | [context/README.md](context/README.md) |
| how a source becomes context | [builder/parser.md](builder/parser.md) |
| intake and routing | [jobs/ingestion-log.md](jobs/ingestion-log.md) |
| discovering sources | [jobs/scans/](jobs/scans/) |
| the outside world you track | [builder/entities/](builder/entities/) |
| finding messaging issues | [jobs/analyzer.md](jobs/analyzer.md) and [builder/issues/](builder/issues/) |
