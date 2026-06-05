# Competitive Feed Scan

Builds the **Feed** section of each competitor [entity](../../builder/entities/) page. It
watches for discrete changes since the last cycle and appends one Feed row per signal, each
carrying the `summary_id` of the source that evidenced it. It does not re-derive the Profile;
for that, see [scan-competitive-profile](competitive-profile.md).

Run it frequently. The Feed is the running record of what competitors did; the Profile is what
they currently are.

## Signals

One of: `product-update` / `pricing-change` / `messaging-shift` / `partnership` / `funding` /
`hiring-signal` / `press-coverage` / `other`. (`buyer-signal` rows reach the same Feed from the
sales-call parsing path, not this scan.)

The signals split across two source types:

- **Their own surfaces** (product and pricing pages, their blog): `product-update`,
  `pricing-change`, `messaging-shift`
- **Third-party news** (Crunchbase, industry press, G2, LinkedIn jobs): `funding`,
  `partnership`, `hiring-signal`, `press-coverage`

A `messaging-shift` signal is a cue that the Profile may be stale: flag the entity for a
[profile](competitive-profile.md) re-scan.

## Targets

- competitor domains (one per line):
