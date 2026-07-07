# Lockups

Units of messaging: named compositions of [claims](claims.md) that travel together. A lockup
is a slice of the canon with a shape — a value proposition supported by three capabilities
and six features, a "how it works" sequence — ready for a [skill](../skills%20-%20Work%20in%20Progress/)
to render into an asset. Claims are the atoms; lockups are the molecules.

## Rules

- **Members are claims, referenced by `clm-` ID.** A lockup composes; it never rewords. The
  phrasing lives in the claims register.
- **Every member must be `canon` or the lockup stays `draft`.** Skills render `approved`
  lockups only. A candidate claim in a slot is a gap to surface, not a pass.
- **The LLM may draft a lockup from canon claims; a human approves it.** Approval is a human
  flipping `status` to `approved`. The LLM never approves.
- **Slugs are kebab-case and unique across this file and [entry-points.md](entry-points.md)**;
  skills reference both as "slices."

## How a lockup is written

One `##` section per lockup. Fields on the first lines: `kind` (`value-prop` /
`how-it-works` / `custom`), `status` (`draft` / `approved`), `updated` (`YYYY-MM-DD`). Then a
member table: `role | claim | note`. Roles are the lockup's own vocabulary (lead, capability,
feature, step, proof); the note says why the claim holds that slot.

---

*(the two lockups below are worked examples; replace them when you compose real ones)*

## value-prop-core

kind: value-prop · status: draft · updated: 2026-07-07

The default answer to "why us": the lead value proposition, the capabilities that make it
credible, and the features that make it concrete.

| role | claim | note |
|------|-------|------|
| lead | clm-001 | the promise |
| capability | clm-0xx | first supporting capability |
| capability | clm-0xx | second |
| capability | clm-0xx | third |
| feature | clm-002 | concrete proof the capability is real |
| feature | clm-0xx | one row per feature claim, up to six |

## how-it-works

kind: how-it-works · status: draft · updated: 2026-07-07

The product's story in order: each row a `how-it-works` claim, sequenced.

| role | claim | note |
|------|-------|------|
| step 1 | clm-0xx | connect |
| step 2 | clm-0xx | configure |
| step 3 | clm-0xx | see value |
