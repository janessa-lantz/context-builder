# Operating context-builder

You are an AI coding agent operating this repo. context-builder turns a company's scattered
messaging into one structured source of truth. This file is the entry point: it tells you how
to run the system. The detailed specs live in each section's files, linked below.

## The model

Three groups. The rule that separates them: **the builder writes into context; skills read
out of it.**

- **[context/](context/)** is what you know, keyed on the **claim**: one assertable statement, typed by a component (defined in [context/README.md](context/README.md)). It holds the **[claims register](context/claims.md)** (rows with `status: canon` are the canon; the `canon-*.md` files are compiled views of it), the **[evidence ledger](context/evidence.md)**, the **[registers](context/registers/)** of your material (content, customer proof, features, offers) and the claims each item carries, **[lockups](context/lockups.md)** and **[entry points](context/entry-points.md)** (composed slices of claims that skills render), the compiled **[claims map](context/claims-map.md)** (coverage and gaps), the brand identities for how it sounds (**[brand-writing-identity](context/brand-writing-identity.md)**) and how it looks (**[brand-visual-identity](context/brand-visual-identity.md)**), and **[entities](context/entities/)**, the raw record of the outside world you track. This is what the team and their AI tools draw from.
- **[builder/](builder/)** is everything that keeps context current: the [parser](builder/parser.md), [raw-assets](builder/raw-assets/), [parsed-summaries](builder/parsed-summaries/), [issues](builder/issues/), and [jobs/](builder/jobs/), the recurring work you run (the [ingestion log](builder/jobs/ingestion-log.md), [scans](builder/jobs/scans/), and the [analyzer](builder/jobs/analyzer.md)). Jobs run the same way every time, on a cadence.
- **[skills - Work in Progress/](skills%20-%20Work%20in%20Progress/)** is on-demand production: each skill reads approved slices (lockups, entry points), canon claims, and the brand identities to generate an asset when a human asks for one. Skills consume context; they never write to it.

## What to do when the user asks

- **"Set up" / "bootstrap a new deployment" / "build our v1"** → run [builder/jobs/setup.md](builder/jobs/setup.md): the one-time bootstrap that fills the claims register from the key pages and builds v1 of the registers (from the full domain, docs, and blog), then compiles the first map. Run it once when first pointing context-builder at a company; after that, keep everything current with the recurring jobs below rather than re-running setup.
- **"Fill or refresh our claims" / "refresh the canon"** → run the key-pages flow. Read [builder/jobs/scans/key-pages.md](builder/jobs/scans/key-pages.md) for the targets, fetch the key pages, parse each per [builder/parser.md](builder/parser.md), mint and confirm claims in [context/claims.md](context/claims.md) per its rules, and recompile the canon views.
- **"Add this source"** (a URL, transcript, or PDF) → append a row to [builder/jobs/ingestion-log.md](builder/jobs/ingestion-log.md), then follow [builder/parser.md](builder/parser.md): save captured sources to [builder/raw-assets/](builder/raw-assets/), write a parsed summary to [builder/parsed-summaries/](builder/parsed-summaries/), mint or match claims and add [evidence](context/evidence.md), and for marketing surfaces add the [register](context/registers/) rows.
- **"Run the key-pages / domain / blog scan"** → read the scan's file in [builder/jobs/scans/](builder/jobs/scans/) for its targets, discover the URLs, and add each as a `url` row in the ingestion log.
- **"Run the competitive scans"** → [competitive-profile](builder/jobs/scans/competitive-profile.md) parses each competitor's key pages into that competitor's [entity](context/entities/) Profile; [competitive-feed](builder/jobs/scans/competitive-feed.md) appends Feed rows for new competitor signals. Competitor intelligence is raw: it lands in [context/entities/](context/entities/), never the claims register or the registers.
- **"Build or refresh the visual identity"** → run [builder/jobs/visual-identity.md](builder/jobs/visual-identity.md): extract the observable identity from the live key pages, write it to [context/brand-visual-identity.md](context/brand-visual-identity.md), and never overwrite a human-authored entry.
- **"Find issues" or "what's off in our messaging"** → run the analyzer per [builder/jobs/analyzer.md](builder/jobs/analyzer.md): read the parsed summaries and the canon, and write themes to [builder/issues/](builder/issues/).
- **"This is what shipped" / "codify these corrections" / "learn from this edit"** → run [builder/jobs/codify.md](builder/jobs/codify.md): diff generated against shipped, classify each correction by what would have prevented it, propose where the learning lands (brand identity, the claims register, a lockup, a skill file, or a rule), and write only what the human approves.
- **"Show me coverage" / "where are the gaps"** → read the [claims map](context/claims-map.md); if it's stale (summaries newer than its compile date), run the [analyzer](builder/jobs/analyzer.md) first, then answer from the map: zero-claim components, unevidenced or orphan claims, misaligned assets.
- **"Build a lockup / entry point"** → draft it in [context/lockups.md](context/lockups.md) or [context/entry-points.md](context/entry-points.md) from canon claims only, per their composition rules, and leave it `draft`. A human flips it to `approved`; never approve your own draft.
- **"Build me a deck / one-pager / carousel / ..."** → run the matching skill in [skills - Work in Progress/](skills%20-%20Work%20in%20Progress/). Read the slices and claims it names (approved lockups and entry points first, canon claims by component as fallback) plus the brand identities; ask the human only for the job-specific variables the skill defines, never for anything the context already holds.

## Rules you must follow

- **The LLM mints claims from verbatim copy only; a human may synthesize.** Every claim you mint is verbatim, currently-published copy, attributed to its source: key pages mint `canon`, other owned surfaces mint `candidate`, and non-owned sources never mint. Never invent, draft, or aspirational-fill; a component with no published claims stays empty. A human may add synthesized claims marked `source: human`; you never edit, retire, or re-status those rows. Demotion out of `canon` is human-only, and rows are never deleted — `retired` keeps the ID. The same rule governs the brand identities: the LLM records only what is observable on live surfaces.
- **Nothing is registered without being parsed.** Only marketing surfaces (company-owned content) go in the [registers](context/registers/). Customer transcripts add `private` evidence and competitor pages land in entities; neither is registered.
- **Entities are raw, never vetted.** Entity pages are knowledge of the outside world, kept in [context/entities/](context/entities/) at a different trust level from the canon. Never treat them as approved messaging or ship their text. Anything shippable is a separate, human-vetted artifact built on top.
- **Skills read context; they do not write it.** A skill never edits the claims register, the registers, the slices, the brand identities, or an entity. If a skill run reveals a gap in context, file it as a theme in [builder/issues/](builder/issues/) with the run as evidence; do not patch it inline. The [codify job](builder/jobs/codify.md) is the only path from a skill run's learnings back into context, and it writes only what a human approves.
- **Do not fill gaps with assumptions.** If a component or claim is absent from a source, say so. Absence is a signal, not a hole to patch.
- **Reference everything by its ID**: components by their kebab-case slugs ([context/README.md](context/README.md)), claims as `clm-NNN`, evidence as `ev-NNN`, issues as `iss-NNN`, lockups and entry points by their slugs.

## Where the detail lives

| To understand | Read |
|---|---|
| the components and their IDs | [context/README.md](context/README.md) |
| claims, evidence, and their rules | [context/claims.md](context/claims.md) and [context/evidence.md](context/evidence.md) |
| your material and the claims it carries | [context/registers/](context/registers/) |
| units of messaging and on-ramps | [context/lockups.md](context/lockups.md) and [context/entry-points.md](context/entry-points.md) |
| coverage and gaps | [context/claims-map.md](context/claims-map.md) |
| how a source becomes context | [builder/parser.md](builder/parser.md) |
| intake and routing | [builder/jobs/ingestion-log.md](builder/jobs/ingestion-log.md) |
| discovering sources | [builder/jobs/scans/](builder/jobs/scans/) |
| the visual identity and how it's built | [context/brand-visual-identity.md](context/brand-visual-identity.md) and [builder/jobs/visual-identity.md](builder/jobs/visual-identity.md) |
| voice, guardrails, and lexicon | [context/brand-writing-identity.md](context/brand-writing-identity.md) |
| the outside world you track | [context/entities/](context/entities/) |
| finding messaging issues | [builder/jobs/analyzer.md](builder/jobs/analyzer.md) and [builder/issues/](builder/issues/) |
| turning corrections into lasting context | [builder/jobs/codify.md](builder/jobs/codify.md) |
| generating assets from context | [skills - Work in Progress/](skills%20-%20Work%20in%20Progress/) |
