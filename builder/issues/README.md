# Issues

Messaging issues produced by the [analyzer](../../jobs/analyzer.md). Each issue points to a
place the messaging needs attention, for you to act on. Every issue has a **kind**, and the
set of kinds is open.

The analyzer's canon comparisons produce four:

- **mismatched**: the canon does not match your customers
- **misaligned**: company content is misaligned to the canon
- **missing**: a gap exists in the canon or your content
- **competitive**: a competitor contests a component the canon claims

Other kinds capture signals that aren't canon comparisons, for example:

- **objection**: a recurring customer objection the messaging should address
- **product**: a product signal customers raise

More kinds can be added.

---

## The backlog tracks themes, not findings

Issues are **themes**, not individual findings. A theme is a pattern observed across the data.
The same observation showing up in five summaries is one theme with five pieces of evidence,
not five issues. Evidence accumulates against a theme over time, and its confidence rises as
more data confirms the pattern.

## Confidence

Each theme carries a `confidence` label, which rises as more evidence confirms the pattern:

- **high**: a strong, well-evidenced pattern. Engage and act on it.
- **medium**: a real pattern worth attention. Keep building evidence.
- **low**: a single signal so far. Watch for recurrence.

A new theme starts at **low** and climbs to **medium** and **high** as more summaries confirm
it.

## Columns

- `id`: unique identifier for the theme
- `kind`: mismatched / misaligned / missing / competitive / objection / product / ...
- `component`: which message component the theme is about
- `description`: a short summary of the pattern
- `confidence`: high / medium / low
- `evidence`: the parsed-summary or entity IDs supporting the theme
- `status`: `open` (default), `actioned`, or `dismissed` (set by a human)
- `last_run`: when the analyzer last touched the theme

## How themes evolve

When the analyzer runs:

1. For each existing theme, check whether new summaries add evidence.
2. If they do: add to the evidence list, raise the confidence as the pattern strengthens, and update `last_run`.
3. If a new pattern matches no existing theme, create a new theme at `low` confidence with its single piece of evidence.
4. Themes marked `actioned` or `dismissed` are closed; the analyzer does not reopen them automatically.

**Human-seeded themes**: you can add a theme by hand. The analyzer then backfills its evidence
by scanning existing summaries for matches, and tracks it going forward. So the analyzer spots
patterns, and you can seed hypotheses for it to evidence.

---

## Backlog

*(the rows below are examples; delete them when the analyzer writes real themes)*

| id | kind | component | description | confidence | evidence | status | last_run |
|----|------|-----------|-------------|------------|----------|--------|----------|
| iss-001 | mismatched | value-drivers | Customers frame the value as saving the deal; canon frames it as efficiency | high | acme-winloss-0603, vertex-0504, summit-0427 | open | 2026-06-04 |
| iss-002 | missing | objections | Customers raise procurement-approval concerns; no canon objection covers it | medium | acme-winloss-0603, meridian-0417 | open | 2026-06-04 |
| iss-003 | misaligned | positioning | Blog positions as a reporting tool; canon positions as a decision platform | low | blog-close-faster | open | 2026-06-04 |
