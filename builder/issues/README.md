# Issues

Messaging issues produced by the [analyzer](../../jobs/analyzer.md). Each issue points to a
place the messaging needs attention, for you to act on. Every issue has a **kind**, and the
set of kinds is open.

The analyzer's gap analysis produces three:

- **mismatched**: the canon does not match your customers
- **misaligned**: company content is misaligned to the canon
- **missing**: a gap exists in the canon or your content

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

## Confidence and attention

Each theme carries a `confidence` score (1 to 10) and an `attention` band. The two are
coupled: the band follows from the score.

| confidence | attention | meaning |
|------------|-----------|---------|
| 1-3 | `act` | strong, well-evidenced pattern; ready to act on |
| 4-5 | `engage` | pattern is real; humans should be paying attention |
| 6-7 | `watch` | gathering evidence; the analyzer is keeping eyes on it |
| 8-10 | `monitor` | single signal; passive watching for recurrence |

The scale runs counter to intuition: a **lower** number means **more** evidence and **more**
confidence. A brand-new single-signal theme starts at 10, and as evidence accumulates the
score drops toward 1.

`act` and `engage` (1 to 5) are the themes that want human attention. `watch` and `monitor`
(6 to 10) are the ones the analyzer is still gathering evidence on.

**Coupling rule**: whenever the analyzer sets or changes a theme's confidence, it updates the
attention band to match. When the score crosses a band boundary (for example 5 to 6), the
band changes with it.

## Columns

- `id`: unique identifier for the theme
- `kind`: mismatched / misaligned / missing / objection / product / ...
- `component`: which message component the theme is about
- `description`: a short summary of the pattern
- `confidence`: 1 to 10
- `attention`: act / engage / watch / monitor (coupled to confidence)
- `evidence`: the parsed-summary IDs supporting the theme
- `status`: `open` (default), `actioned`, or `dismissed` (set by a human)
- `last_run`: when the analyzer last touched the theme

## How themes evolve

When the analyzer runs:

1. For each existing theme, check whether new summaries add evidence.
2. If they do: add to the evidence list, lower the confidence score (more data, more confidence), and update `last_run` and the attention band.
3. If a new pattern matches no existing theme, create a new theme at confidence 10 with its single piece of evidence.
4. Themes marked `actioned` or `dismissed` are closed; the analyzer does not reopen them automatically.

**Human-seeded themes**: you can add a theme by hand. The analyzer then backfills its evidence
by scanning existing summaries for matches, and tracks it going forward. So the analyzer spots
patterns, and you can seed hypotheses for it to evidence.

---

## Backlog

*(the rows below are examples; delete them when the analyzer writes real themes)*

| id | kind | component | description | confidence | attention | evidence | status | last_run |
|----|------|-----------|-------------|------------|-----------|----------|--------|----------|
| iss-001 | mismatched | value-drivers | Customers frame the value as saving the deal; canon frames it as efficiency | 2 | act | acme-winloss-0603, neotax-0504, telos-0427 | open | 2026-06-04 |
| iss-002 | missing | objections | Customers raise procurement-approval concerns; no canon objection covers it | 4 | engage | acme-winloss-0603, orbital-0417 | open | 2026-06-04 |
| iss-003 | misaligned | positioning | Blog positions as a reporting tool; canon positions as a decision platform | 7 | watch | blog-close-faster | open | 2026-06-04 |
