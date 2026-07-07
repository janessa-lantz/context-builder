# Raw Assets

A raw asset is a pointer to where a source's words came from, not a copy of them. Sources
come in two kinds, split by whether the content already has a home:

- **Hosted**: a live URL (a blog post, a web page). It lives at its URL. The builder reads it on demand and keeps only the summary. The `source` in the [content register](../../context/registers/content.md) is the URL, and nothing is stored here.
- **Captured**: a transcript, an upload, or pasted notes. It has no home of its own, so the builder stores the file here, named by its asset id (for example `acme-winloss-0603.txt`). Lose it and you can't re-parse it. The `source` is the path to that file.

Either way, the durable artifact is the [parsed summary](../parsed-summaries/), not the raw
asset. This folder holds captured sources only. Hosted pages stay where they live.

Note: a hosted page can change after you parse it. The live URL plus the summary's `parsed`
date is your provenance. If you need a frozen snapshot of what a page said on a given day,
capturing that URL is a deliberate choice, not the default.
