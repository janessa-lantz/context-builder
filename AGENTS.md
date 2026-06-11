# Operating context-builder

You are an AI coding agent operating this repo. context-builder turns a company's scattered
messaging into one structured source of truth. This file is the entry point: it tells you how
to run the system. The detailed specs live in each section's files, linked below.

## The model

Three groups. The rule that separates them: **the builder writes into context; skills read
out of it.**

- **[context/](context/)** is what you know: the messaging **canon** (built on the components defined in [context/README.md](context/README.md)), the **content index** of company-owned assets, the **[visual identity](context/visual-identity.md)**, and **[entities](context/entities/)**, the raw record of the outside world you track. This is what the team and their AI tools draw from.
- **[builder/](builder/)** is everything that keeps context current: the [parser](builder/parser.md), [raw-assets](builder/raw-assets/), [parsed-summaries](builder/parsed-summaries/), [issues](builder/issues/), and [jobs/](builder/jobs/), the recurring work you run (the [ingestion log](builder/jobs/ingestion-log.md), [scans](builder/jobs/scans/), and the [analyzer](builder/jobs/analyzer.md)). Jobs run the same way every time, on a cadence.
- **[skills/](skills/)** is on-demand production: each skill reads the canon and visual identity to generate an asset when a human asks for one. Skills consume context; they never write to it.

## What to do when the user asks

- **"Build or refresh our canon"** → run the key-pages flow. Read [builder/jobs/scans/key-pages.md](builder/jobs/scans/key-pages.md) for the targets, fetch the key pages, parse each per [builder/parser.md](builder/parser.md), and compile the canon ([context/messaging-canon.md](context/messaging-canon.md)) from the key-page extractions.
- **"Add this source"** (a URL, transcript, or PDF) → append a row to [builder/jobs/ingestion-log.md](builder/jobs/ingestion-log.md), then follow [builder/parser.md](builder/parser.md): save captured sources to [builder/raw-assets/](builder/raw-assets/), write a parsed summary to [builder/parsed-summaries/](builder/parsed-summaries/), and for marketing surfaces add a [content-index](context/content-index.md) row.
- **"Run the key-pages / domain / blog scan"** → read the scan's file in [builder/jobs/scans/](builder/jobs/scans/) for its targets, discover the URLs, and add each as a `url` row in the ingestion log.
- **"Run the competitive scans"** → [competitive-profile](builder/jobs/scans/competitive-profile.md) parses each competitor's key pages into that competitor's [entity](context/entities/) Profile; [competitive-feed](builder/jobs/scans/competitive-feed.md) appends Feed rows for new competitor signals. Competitor intelligence is raw: it lands in [context/entities/](context/entities/), never the canon or index.
- **"Build or refresh the visual identity"** → run [builder/jobs/visual-identity.md](builder/jobs/visual-identity.md): extract the observable identity from the live key pages, write it to [context/visual-identity.md](context/visual-identity.md), and never overwrite a human-authored entry.
- **"Find issues" or "what's off in our messaging"** → run the analyzer per [builder/jobs/analyzer.md](builder/jobs/analyzer.md): read the parsed summaries and the canon, and write themes to [builder/issues/](builder/issues/).
- **"Build me a deck / one-pager / carousel / ..."** → run the matching skill in [skills/](skills/). Read the canon components and visual identity it names; ask the human only for the job-specific variables the skill defines, never for anything the context already holds.

## Rules you must follow

- **The LLM fills the canon from verbatim copy only; a human may synthesize.** When you populate a component, use verbatim, currently-published copy, attributed to its source; never invent, draft, or aspirational-fill, and leave a component blank if it has no published copy. A human may override or augment any component with synthesis and context; those entries are marked `source: human`, and you must never overwrite a human-authored entry on a re-scan. The same rule governs the visual identity: the LLM records only what is observable on live surfaces.
- **Nothing is indexed without being parsed.** Only marketing surfaces (company-owned content) go in the content index. Customer transcripts and competitor pages are parsed but not indexed.
- **Entities are raw, never vetted.** Entity pages are knowledge of the outside world, kept in [context/entities/](context/entities/) at a different trust level from the canon. Never treat them as approved messaging or ship their text. Anything shippable is a separate, human-vetted artifact built on top.
- **Skills read context; they do not write it.** A skill never edits the canon, the index, the visual identity, or an entity. If a skill run reveals a gap in context, surface the gap; do not patch it inline.
- **Do not fill gaps with assumptions.** If a component is absent from a source, say so. Absence is a signal, not a hole to patch.
- **Reference components by their ID** (the kebab-case slugs in [context/README.md](context/README.md)).

## Where the detail lives

| To understand | Read |
|---|---|
| the components and their IDs | [context/README.md](context/README.md) |
| how a source becomes context | [builder/parser.md](builder/parser.md) |
| intake and routing | [builder/jobs/ingestion-log.md](builder/jobs/ingestion-log.md) |
| discovering sources | [builder/jobs/scans/](builder/jobs/scans/) |
| the visual identity and how it's built | [context/visual-identity.md](context/visual-identity.md) and [builder/jobs/visual-identity.md](builder/jobs/visual-identity.md) |
| the outside world you track | [context/entities/](context/entities/) |
| finding messaging issues | [builder/jobs/analyzer.md](builder/jobs/analyzer.md) and [builder/issues/](builder/issues/) |
| generating assets from context | [skills/](skills/) |
