# context-builder

Build your context layer for messaging. Keep your team and your AI tools drawing from one source of truth.

![How context-builder works: jobs feed the parser, which extracts against 26 messaging components and writes to the content index and canon](system.png)

## Who it's for

Marketing and messaging teams who want one place their whole company, and every AI tool they point at their messaging, can rely on. If you write copy, brief an agency, or hand your positioning to an LLM, this is the source those efforts pull from.

## The problem it solves

A company's messaging lives scattered: some on the website, some in a deck, some in a founder's head, some buried in a call transcript. Teams and AI tools end up pulling from whatever they happen to find, so the story drifts and goes stale. context-builder gives you a single structured context layer that stays current as new content comes in, so everyone and everything draws the same approved messaging.

## What it does

1. **Defines your messaging in 26 components, across 5 groups.** Who We Are, What We Do, Who It's For, Proof, and Pricing. Every claim files under one component, so all of your messaging shares one schema instead of living in scattered prose.
2. **Parses any source against that schema.** Hand it a URL, a transcript, or a document. The parser fetches it, classifies it, extracts which components it carries, and records the result in the content index. It files what is actually there and flags what is absent rather than inventing messaging to fill the gap.
3. **Compiles an approved canon you can trust.** One canonical statement per component, rolled up from your key pages and kept current as those pages change. This is what your team and your AI tools read from.

## How it works

Three parts:

- **[context/](context/)** is the source of truth your team and AI draw from: your messaging canon (built on defined components), plus the content index of everything you've published.
- **[builder/](builder/)** is the engine. It maps each raw asset against your messaging canon and writes the result into context. The analyzer's findings land in its issues.
- **[jobs/](jobs/)** is the work you hand the builder: an ingestion log that routes every incoming source (text, url, or pdf) to the parser, scans that discover sources to feed it, and an analyzer that reads the parsed summaries to find messaging gaps.

The flow is one direction: add a job, the builder parses it against the components, and it writes the result to the content index and, for key pages, the canon.
