# context-builder

Context-builder is a system to help growing companies manage messaging across product marketing, content & communications, and demand gen. 

Context-builder is for **marketing leaders** who need their team to move fast with AI while keeping the quality bar high. It's like the old messaging doc, built for the AI era.

Common challenges marketing teams are facing today:
- marketing needs to move fast while also keeping the quality bar high
- messaging fragments across internal teams (marketing, CS, and sales) and channel (paid, PR, SEO, AEO)
- AI is intermediating every interaction your customers have with your brand

## Why it exists
This project is built and maintained by [Janessa Lantz](https://www.linkedin.com/in/janessalantz/) (that's me!). I built a communications team at HubSpot (post-IPO), built the dbt Labs marketing team from <$1M to close to $100M in revenue, and now work with earlier stage companies as a fractional marketing leader and consultant. Context-builder exists to support my work. I use pieces of it in every client engagement. If anything here is useful for your own work, take it!


## What it does

The context-builder keeps your messaging current and flags it the moment it drifts. Three things it does:

1. **Keeps a human-validated canon.** One approved statement per messaging component, compiled verbatim from your key pages, with synthesis and context a human can layer on top. The [canon](context/messaging-canon.md) is the core the whole system protects, and what your team and your AI tools read from.
2. **Ingests your knowledge as it accumulates.** Sales calls, win/loss notes, customer interviews, and everything you publish enter through one front door, get parsed against the components, and land as durable summaries. Customer language is captured the moment it shows up, not months later in a doc rewrite.
3. **Surfaces messaging issues proactively.** The analyzer compares the canon against what customers actually say and what your company has published, then writes structured [issues](builder/issues/) tagged mismatched, misaligned, or missing for a human to act on. The LLM finds the drift; you decide what to do about it.

With the canon stable and current, your team builds shared [skills](skills/) on top of it, so every asset is generated from approved messaging rather than from scratch.

![context-builder system diagram: the builder writes each source into context, the analyzer surfaces drift, and skills read context to produce assets, all organized by 24 messaging components](system-diagram.png)

## How it works

Three groups, separated by one rule: the builder writes into context; skills read out of it.

- **[context/](context/)** is the source of truth your team and AI draw from: the [messaging canon](context/messaging-canon.md) (one statement per component, compiled from your key pages), the [content index](context/content-index.md) (every asset you've published and which components it carries), the [brand writing identity](context/brand-writing-identity.md) (voice, guardrails, and lexicon) and the [brand visual identity](context/brand-visual-identity.md) (the observable design facts), and [entities](context/entities/) (raw records of the outside world you track, kept at a different trust level from the canon). The canon and index are organized by a shared library of 24 messaging components.
- **[builder/](builder/)** is everything that keeps context current. The [parser](builder/parser.md) fetches each source, maps it to the components, and writes a durable summary. [Jobs](builder/jobs/) are the recurring work you run: the [ingestion log](builder/jobs/ingestion-log.md) is the front door where every source (a URL, a transcript, a PDF) is logged and routed; [scans](builder/jobs/scans/) discover sources to feed it; the [analyzer](builder/jobs/analyzer.md) finds drift, and its findings land in [issues/](builder/issues/) for you to act on.
- **[skills/](skills/)** is on-demand production. Each skill reads the canon and brand identity to generate an asset (a deck, a one-pager, a carousel) when a human asks for one. Jobs write into context on a cadence; skills read out of it on demand.

## Key Concepts

- **Component**: one of the 24 building blocks of messaging (like positioning or value-drivers), each with a stable kebab-case ID. The schema everything files under.
- **Canon**: your approved messaging structured into approved components. The source of truth your team and AI draw from.
- **Content index**: a findable library of your company-owned assets and which components each one carries.
- **Visual identity**: the observable design facts of the brand (colors, typography, logo treatment, style), kept in context beside the canon. The visual counterpart to the canon: skills read it so every generated asset looks like the company, not just sounds like it.
- **Brand writing identity**: how the company sounds: voice, guardrails, and lexicon, kept beside the visual identity. Skills read it so every generated asset sounds like the company, not just looks like it.
- **Surface**: where an asset lives (key_page, owned, earned, paid, or internal).
- **Raw asset**: a source the system reads, either a live URL or a stored transcript or doc. A pointer, not a copy.
- **Parsed summary**: the parser's record of one asset, mapping it to the components it carries.
- **Entity**: a durable record of an outside-world actor you track (a competitor first, later events or people). Raw intelligence, kept in the builder and never treated as vetted messaging.
- **Profile**: an entity's current-state messaging, parsed against the same components as your own.
- **Feed**: an entity's append-only history of changes, one row per signal.
- **Job**: a unit of recurring work you hand the builder (an ingested source, a scan, or an analysis run). Jobs write into context.
- **Scan**: a job that discovers many URLs to ingest (key-pages, competitive-profile, competitive-feed, domain, blog).
- **Parser**: the engine that maps each raw asset against your canon and writes the result into context.
- **Analyzer**: the job that compares your summaries against the canon and surfaces issues.
- **Issue (theme)**: a place your messaging needs attention, with a kind (mismatched, misaligned, missing, and more) and a confidence (high, medium, low).
- **Skill**: an on-demand generator that reads the canon and brand identity to produce an asset (a deck, a one-pager, a carousel). Skills read out of context and never write into it.
