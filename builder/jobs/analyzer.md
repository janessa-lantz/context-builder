# Analyzer

A job you run to find where your messaging breaks down. The analyzer reads the
[parsed summaries](../parsed-summaries/), the
[canon](../../context/messaging-canon.md), and competitor [entity Profiles](../../context/entities/), produces structured findings, and writes them to
[issues](../issues/). You trigger it. It does not run automatically the way the parser
runs on every ingested asset.

Three principles:

- **Structured findings, not prose.** The analyzer produces data, not reports or recommendations.
- **Reproducible.** Same inputs in, same findings out.
- **Peers, not a pipeline.** Each comparison runs independently; they don't chain.

## What it finds

Findings group into four kinds, each a different comparison:

- **mismatched**: the canon does not match your customers. Compares the canon against your customer summaries (sales calls, reviews, interviews), component by component, and flags where customers frame a component differently than the canon does.
- **misaligned**: company content is misaligned to the canon. Compares your company content (blog, decks, other surfaces) against the canon, and flags where a published surface says something different from the approved messaging.
- **missing**: a gap exists in the canon or your content. Flags components with no canon entry, and customer topics that no company asset covers.
- **competitive**: a competitor contests the canon. Compares the canon against competitor [entity Profiles](../../context/entities/), component by component, and flags where a competitor occupies, matches, or undercuts a component the canon claims. Competitor Profiles are raw intelligence, so a competitive issue flags pressure for you to judge, never a change to make.

These four are the analyzer's comparisons. Issues can also carry other kinds surfaced
from the same summaries, for example a recurring `objection` or a `product` signal. The set
is open (see [issues](../issues/)).

## Output

Findings land in [issues](../issues/) as **themes**: recurring patterns, each tagged
by kind and component, rated with a confidence of high, medium, or low, and backed by the
summary IDs that evidence them. See [issues](../issues/) for the backlog format.

The analyzer reads customer summaries from
[parsed-summaries](../parsed-summaries/), which exist even though customer content is
not added to the content index.
