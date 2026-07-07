# Analyzer

A job you run to find where your messaging breaks down. The analyzer reads the
[parsed summaries](../parsed-summaries/), the [claims register](../../context/claims.md), the
[evidence ledger](../../context/evidence.md), the [registers](../../context/registers/), and
competitor [entity Profiles](../../context/entities/), produces structured findings at claim
grain, writes them to [issues](../issues/), and recompiles the
[claims map](../../context/claims-map.md) and the canon views. You trigger it. It does not
run automatically the way the parser runs on every ingested asset.

Three principles:

- **Structured findings, not prose.** The analyzer produces data, not reports or recommendations.
- **Reproducible.** Same inputs in, same findings out.
- **Peers, not a pipeline.** Each comparison runs independently; they don't chain.

## What it finds

Findings group into four kinds, each a different comparison:

- **mismatched**: the canon does not match your customers. Compares canon claims against your customer summaries (sales calls, reviews, interviews) and flags where customers frame a claim differently than the canon states it. The customer phrasing stays in the issue (and its evidence rows), never in the register.
- **misaligned**: company content is misaligned to the canon. Reads the registers for rows carrying `candidate` or divergent-variant claims, and flags each published surface saying something the approved messaging doesn't.
- **missing**: a gap exists in the claims or your coverage. Flags components with zero claims (the map's zero rows), canon claims with no evidence (`unevidenced`), canon claims no asset carries (`orphan`), and customer topics no company asset covers.
- **competitive**: a competitor contests a claim. Compares canon claims against competitor [entity Profiles](../../context/entities/) and Feed rows, and flags where a competitor occupies, matches, or undercuts a claim (`contested` on the map, by `clm-` ID where the Feed names one). Competitor Profiles are raw intelligence, so a competitive issue flags pressure for you to judge, never a change to make.

These four are the analyzer's comparisons. Issues can also carry other kinds surfaced
from the same summaries, for example a recurring `objection` or a `product` signal. The set
is open (see [issues](../issues/)).

## The run

1. Gather the parsed summaries added or updated since the backlog's most recent `last_run`.
2. Run each comparison above, claim by claim and component by component, against those
   summaries. Skip a comparison whose inputs don't exist yet: `mismatched` needs customer
   summaries, `competitive` needs entity Profiles. Never force findings the data cannot
   support.
3. Update the backlog per [issues](../issues/): add evidence to existing themes, raise
   confidence as patterns strengthen, open new themes at `low`, and leave `actioned` and
   `dismissed` themes closed. Name the `clm-` IDs a theme is about in its `claims` column.
4. Stamp `last_run` on every theme touched.
5. **Recompile the compiled views wholesale**, in this order, each replaced entirely and
   never hand-merged:
   - the [claims map](../../context/claims-map.md) — every component row including the zeros, every claim's evidence and asset counts and flags, the misaligned-assets table;
   - the six canon views (`canon-*.md`) from the register, per [messaging-canon.md](../../context/messaging-canon.md);
   - the [dashboard](../../context/dashboard.md) — the home view, rolled up from the map, the registers, and the backlog. Keep its fixed sections and columns so every deployment renders the same; only the counts and deployment name change.

Run it after each meaningful batch of new summaries (a set of sales calls, a completed scan),
or whenever someone asks what's off. The first run happens at the end of
[setup](setup.md), to baseline the backlog.

## Output

Findings land in [issues](../issues/) as **themes**: recurring patterns, each tagged
by kind, component, and the claims involved, rated with a confidence of high, medium, or low,
and backed by the summary IDs that evidence them. See [issues](../issues/) for the backlog
format. The recompiled [claims map](../../context/claims-map.md) is the other output: the
coverage view the themes point into, rolled up into the [dashboard](../../context/dashboard.md)
home view.

The analyzer reads customer summaries from
[parsed-summaries](../parsed-summaries/), which exist even though customer content is
not added to the registers.
