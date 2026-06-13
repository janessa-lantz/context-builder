# context-builder

Context-builder is an always-on system that keeps your messaging accurate to your customer and consistent everywhere it shows up. It maintains an active source of truth for how you talk about yourself, then continuously checks your real messaging against it.

Context-builder is for **marketing leaders** who own how the company talks about itself across all sufraces: product marketing, content & communications, and demand gen. 

Marketing teams are operating in chaos. AI allows everyone to move faster, but without guardrails, the message starts to deteriorate. Your knowledge and understanding of the customer is one of the last advantages you have left. 

Context-builder is a **proactive** approach to managing messaging. It builds your messaging canon (based on what you're saying publicly), then maps sales calls and your current content index against that canon to proactively identify messaging that is mismatched to voice of the customer, misaligned to the canon, or simply missing. 

![How context-builder works: jobs feed the builder, which parses each source against the messaging components and writes to the canon and content index](system-diagram.png)

## Why it exists

Your marketing team can only move as fast as your messaging. Great messaging:
1. Matches how the customer describes their problem and pain
2. Aligns across all marketing surfaces
3. Is complete and has depth 

The existing tools for managing messaging were built for a slower world. The messaging doc goes stale the moment product ships or a competitor moves. Turn it into a skill and someone has to update it by hand and pass it around. Even storing context in GitHub, today's gold standard, still depends on a human remembering to add the new context. These tools are reactive by design. The Context Builder is a system that helps product marketing identify issues before anyone else in the org notices. 

## What it does

The context builder maintains your unique knowledge, proactively flags issues for human intervention, and fights messaging drift. Three capabilities:

1. **Keeps a human-validated canon.** One approved statement per messaging component, compiled verbatim from your key pages, with synthesis and context a human can layer on top. The [canon](context/messaging-canon.md) is the core the whole system protects, and what your team and your AI tools read from.
2. **Ingests your knowledge as it accumulates.** Sales calls, win/loss notes, customer interviews, and everything you publish enter through one front door, get parsed against the components, and land as durable summaries. Customer language is captured the moment it shows up, not months later in a doc rewrite.
3. **Surfaces messaging issues proactively.** The analyzer compares the canon against what customers actually say and what your company has published, then writes structured [issues](builder/issues/) tagged mismatched, misaligned, or missing for a human to act on. The LLM finds the drift; you decide what to do about it.

With the canon stable and current, you build shared [skills](skills/) on top of it, so every brief, page, and deck is generated from approved messaging rather than from scratch.

## How it works

Three groups, separated by one rule: the builder writes into context; skills read out of it.

- **[context/](context/)** is the source of truth your team and AI draw from: the [messaging canon](context/messaging-canon.md) (one statement per component, compiled from your key pages), the [content index](context/content-index.md) (every asset you've published and which components it carries), the [visual identity](context/visual-identity.md) (the observable design facts of the brand), and [entities](context/entities/) (raw records of the outside world you track, kept at a different trust level from the canon). The canon and index are organized by a shared library of 24 messaging components.
- **[builder/](builder/)** is everything that keeps context current. The [parser](builder/parser.md) fetches each source, maps it to the components, and writes a durable summary. [Jobs](builder/jobs/) are the recurring work you run: the [ingestion log](builder/jobs/ingestion-log.md) is the front door where every source (a URL, a transcript, a PDF) is logged and routed; [scans](builder/jobs/scans/) discover sources to feed it; the [analyzer](builder/jobs/analyzer.md) finds drift, and its findings land in [issues/](builder/issues/) for you to act on.
- **[skills/](skills/)** is on-demand production. Each skill reads the canon and visual identity to generate an asset (a deck, a one-pager, a carousel) when a human asks for one. Jobs run on a cadence and write into context; skills run when you need them and read out of it.

## Key Concepts

- **Component**: one of the 24 building blocks of messaging (like positioning or value-drivers), each with a stable kebab-case ID. The schema everything files under.
- **Canon**: your approved messaging structured into approved components. The source of truth your team and AI draw from.
- **Content index**: a findable library of your company-owned assets and which components each one carries.
- **Visual identity**: the observable design facts of the brand (colors, typography, logo treatment, style), kept in context beside the canon. The visual counterpart to the canon: skills read it so every generated asset looks like the company, not just sounds like it.
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
- **Skill**: an on-demand generator that reads the canon and visual identity to produce an asset (a deck, a one-pager, a carousel). Skills read out of context and never write into it.
