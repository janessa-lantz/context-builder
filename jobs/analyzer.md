# Analyzer

A job you run to find where your messaging breaks down. The analyzer reads the
[parsed summaries](../builder/parsed-summaries/) and the
[canon](../context/messaging-canon.md), produces structured findings, and writes them to
[issues](../builder/issues/). You trigger it. It does not run automatically the way the parser
runs on every ingested asset.

Three principles:

- **Structured findings, not prose.** The analyzer produces data, not reports or recommendations.
- **Reproducible.** Same inputs in, same findings out.
- **Peers, not a pipeline.** Each comparison runs independently; they don't chain.

## What it finds

Findings group into three kinds, each a different comparison:

- **mismatched**: the canon does not match your customers. Compares the canon against your customer summaries (sales calls, reviews, interviews), component by component, and flags where customers frame a component differently than the canon does.
- **misaligned**: company content is misaligned to the canon. Compares your company content (blog, decks, other surfaces) against the canon, and flags where a published surface says something different from the approved messaging.
- **missing**: a gap exists in the canon or your content. Flags components with no canon entry, and customer topics that no company asset covers.

These three are the analyzer's gap comparisons. Issues can also carry other kinds surfaced
from the same summaries, for example a recurring `objection` or a `product` signal. The set
is open (see [issues](../builder/issues/)).

## Output

Findings land in [issues](../builder/issues/), each tagged by kind (mismatched / misaligned /
missing) and by component. The backlog format is still being defined (see issues).

The analyzer reads customer summaries from
[parsed-summaries](../builder/parsed-summaries/), which exist even though customer content is
not added to the content index.
