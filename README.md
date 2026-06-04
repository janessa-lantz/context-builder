# context-builder
Build your context layer for messaging. Keep your team and your AI tools drawing from one source of truth.

## How it works

Three parts:

- **[context/](context/)** is the source of truth your team and AI draw from: your messaging canon (built on defined components), plus the content index of everything you've published.
- **[builder/](builder/)** is the engine. It maps each raw asset against your messaging canon, writes the result into context, and surfaces messaging issues to act on.
- **[jobs/](jobs/)** is the work you hand the builder: an ingestion log that routes every incoming source (text, url, or pdf) to the parser, plus scans that discover sources to feed it.

The flow is one direction: add a job, the builder parses it against the components, and it writes the result to the content index and, for key pages, the canon.
