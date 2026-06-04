# context-builder
Build your context layer for messaging. Keep your team and your AI tools drawing from one source of truth.

## How it works

Three parts:

- **[context/](context/)** is the source of truth your team and AI draw from: your messaging canon (built on defined components), plus the content index of everything you've published.
- **[builder/](builder/)** is the engine. The parser reads jobs, extracts the messaging components it finds, and writes into context.
- **[jobs/](jobs/)** is the work you hand the builder. Add a source (a URL or a transcript) and the builder runs it.

The flow is one direction: add a job, the builder parses it against the components, and it writes the result to the content index and, for key pages, the canon.
