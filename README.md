# context-builder

The context builder is a proactive approach to managing messaging. It builds your messaging canon (based on what you're saying publicly), then maps sales calls and your current content index against that canon to proactively identify messaging that is mismatched to voice of the customer, misaligned to the canon, or simply missing. 

![How context-builder works: jobs feed the builder, which parses each source against 26 messaging components and writes to the canon and content index](system-diagram.png)

## Why it exists

Your marketing team can only move as fast as your messaging. Great messaging:
1. Matches how the customer describes their problem and pain
2. Aligns across all marketing surfaces
3. Is complete and has depth 

Your unique knowledge of the customer and the market is the last advantage you have left. The Context Builder is a partner to your entire marketing team, ensuring a foundation that everyone can work from, while proactively surfacing issues and themes to watch. 

The existing tools for managing messaging were built for a slower world. The messaging doc goes stale the moment product ships or a competitor moves. Turn it into a skill and someone has to update it by hand and pass it around. Even storing context in GitHub, today's gold standard, still depends on a human remembering to add the new context. These tools are reactive by design. The Context Builder is a system that helps product marketing identify issues before anyone else in the org notices. 

## The problem it solves: messaging drift

When teams move fast without a living source of truth, messaging drifts. Drift shows up three ways:

- **Mismatched.** Your messaging describes the problem in your internal language instead of the customer's, so buyers miss that you can solve it. The cost is wasted spend.
- **Misaligned.** Your site, your outreach, and your decks each say something different, so buyers stop trusting you'll deliver. Ask an LLM what you do and it answers differently every time. The cost is eroded trust.
- **Missing.** A common objection comes up on calls and no content exists to resolve it. The cost is stalled pipeline.

## What it does

The context builder maintains your unique knowledge, proactively flags issues for human intervention, and fights messaging drift. Three capabilities:

1. **Keeps a human-validated canon.** One approved statement per messaging component, compiled from your key pages. The [canon](context/messaging-canon.md) is the core the whole system protects, and what your team and your AI tools read from.
2. **Ingests your knowledge as it accumulates.** Sales calls, win/loss notes, customer interviews, and everything you publish enter through one front door, get parsed against the components, and land as durable summaries. Customer language is captured the moment it shows up, not months later in a doc rewrite.
3. **Surfaces drift proactively.** The analyzer compares the canon against what customers actually say and what your company has published, then writes structured [issues](builder/issues/) tagged mismatched, misaligned, or missing for a human to act on. The LLM finds the drift; you decide what to do about it.

With the canon stable and current, you build shared skills on top of it, so every brief, page, and deck is generated from approved messaging rather than from scratch.

## How it works

- **[jobs/](jobs/)** is the work you hand the builder. The [ingestion log](jobs/ingestion-log.md) is the front door: every source (a URL, a transcript, a PDF) is logged and routed to the parser. [Scans](jobs/scans/) discover sources to feed it. The [analyzer](jobs/analyzer.md) is a job you run to find drift.
- **[builder/](builder/)** is the engine. The [parser](builder/parser.md) fetches each source, maps it to the components, and writes a durable summary. The analyzer's findings land in [issues/](builder/issues/) for you to act on.
- **[context/](context/)** is the source of truth your team and AI draw from: the [messaging canon](context/messaging-canon.md) (one statement per component, compiled from your key pages) and the [content index](context/content-index.md) (every asset you've published and which components it carries). Both are organized by a shared library of 26 messaging components.

## Key Concepts

- **Component**: one of the 26 building blocks of messaging (like positioning or value-drivers), each with a stable kebab-case ID. The schema everything files under.
- **Canon**: your approved messaging structured into approved components. The source of truth your team and AI draw from.
- **Content index**: a findable library of your company-owned assets and which components each one carries.
- **Surface**: where an asset lives (key_page, owned, earned, paid, or internal).
- **Raw asset**: a source the system reads, either a live URL or a stored transcript or doc. A pointer, not a copy.
- **Parsed summary**: the parser's record of one asset, mapping it to the components it carries.
- **Entity**: a durable record of an outside-world actor you track (a competitor first, later events or people). Raw intelligence, kept in the builder and never treated as vetted messaging.
- **Profile**: an entity's current-state messaging, parsed against the same components as your own.
- **Feed**: an entity's append-only history of changes, one row per signal.
- **Job**: a unit of work you hand the builder (an ingested source, a scan, or an analysis run).
- **Scan**: a job that discovers many URLs to ingest (key-pages, competitive-profile, competitive-feed, domain, blog).
- **Parser**: the engine that maps each raw asset against your canon and writes the result into context.
- **Analyzer**: the job that compares your summaries against the canon and surfaces issues.
- **Issue (theme)**: a place your messaging needs attention, with a kind (mismatched, misaligned, missing, and more) and a confidence (high, medium, low).
