# Issues

Issues the system surfaces for you to act on. Most are messaging issues produced by the
[analyzer](../jobs/analyzer.md); skill and job runs also file here when they hit a gap or
produce something a human had to correct. Each issue points to a place the messaging, or the
system itself, needs attention. Every issue has a **kind**, and the set of kinds is open.

The analyzer's canon comparisons produce four:

- **mismatched**: the canon does not match your customers
- **misaligned**: company content is misaligned to the canon
- **missing**: a gap exists in the canon or your content
- **competitive**: a competitor contests a component the canon claims

Other kinds capture signals that aren't canon comparisons, for example:

- **objection**: a recurring customer objection the messaging should address
- **product**: a product signal customers raise

Two kinds are about the system rather than the messaging, and are consumed by the
[codify job](../jobs/codify.md):

- **correction**: a human corrected a generated artifact before it shipped; the learning is
  waiting to be codified into context or a skill file
- **process**: the system misbehaved: a spec was misread, a rule broken, a parse missed
  something

A skill run that hits a canon gap files it as a **missing** theme with the run as its
evidence; the gap is the same whether the analyzer or a skill finds it.

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

- `id`: unique identifier for the theme, `iss-NNN`, numbered sequentially
- `kind`: mismatched / misaligned / missing / competitive / objection / product / ...
- `component`: which message component the theme is about
- `claims`: the `clm-` IDs the theme is about, space-separated; blank for component-level themes
- `description`: a short summary of the pattern
- `confidence`: high / medium / low
- `evidence`: what supports the theme: parsed-summary or entity IDs, or for system kinds the run or artifact (a skill run, a shipped correction)
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

Deployment: **Mintlify** — baselined by the setup run's analyzer pass, 2026-07-07. Only
`missing` and `misaligned` (and `process`) have data: no customer sources or entity Profiles
exist yet, so `mismatched` and `competitive` were skipped, not forced.

| id | kind | component | claims | description | confidence | evidence | status | last_run |
|----|------|-----------|--------|-------------|------------|----------|--------|----------|
| iss-001 | misaligned | category-name | clm-003 clm-004 | Homepage now says "knowledge infrastructure"; docs, the Trieve post, and the library comparison still say "AI-native documentation platform" — the agent-era repositioning hasn't propagated | medium | blog-trieve-acquisition, docs, library-mintlify-vs-docusaurus | open | 2026-07-07 |
| iss-002 | missing | value-drivers | clm-058 | Revenue-generation framing (docs as the highest-intent demand channel) lives only on an owned blog post; no key page makes the business case beyond support deflection | low | blog-demand-channel | open | 2026-07-07 |
| iss-003 | missing | founder-story | | No About page exists on the domain; the origin story lives off-site (YC post linked from careers) and in blog posts | low | careers | open | 2026-07-07 |
| iss-004 | misaligned | key-metrics | clm-069 clm-073 | Scale stats drift across surfaces: "20,000+ companies" (homepage) vs "over ten thousand companies" (careers); "100 million builders" (switch) vs "100 million people" (series-b); Anthropic "2M+" (enterprise) vs "1.5M developers" (case study) | medium | careers, switch, blog-series-b, customer-anthropic | open | 2026-07-07 |
| iss-005 | missing | buying-committee | | Zero claims for the buying committee; pricing-FAQ topics (SOC 2, authentication, credits) signal evaluator objections but no published content addresses roles beyond the champion | low | pricing, claims-map zero row | open | 2026-07-07 |
| iss-006 | process | company-description | clm-014 clm-055 | Spec gap: the extraction requires composed synthesis for company-description and icp, but the claims trust model says the LLM mints verbatim only — rows marked "synthesis" pending a codify ruling on how LLM synthesis is labeled | low | context/claims.md rows clm-014, clm-055 | open | 2026-07-07 |
| iss-007 | process | pricing-model | clm-076 | The pricing page renders the Pro price as placeholder digits to the scraper (JS-rendered); the register carries tier structure but no Pro price — needs a browser-rendered fetch or human capture | low | pricing | open | 2026-07-07 |
| iss-008 | missing | positioning | clm-001 | "Your docs have two readers now: the developers and the agents they sent ahead" appears only on contact-sales — the strongest supporting line is absent from the homepage and unminted | low | contact-sales | open | 2026-07-07 |
