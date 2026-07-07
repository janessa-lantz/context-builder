# Registers

Logs of your material, one register per kind: [content](content.md),
[customer-proof](customer-proof.md), [features](features.md), and [offers](offers.md). Each
register is a table of things you have — an asset, a case study, a feature, an offer — and
the `claims` column records which [claims](../claims.md) each item carries. That link is the
point: for any claim, which material carries it; for any material, which claims it makes, and
are they in the canon or not.

## Component or register?

**A component types claims (statements); a register logs material (stuff you have).**
`customer-proof`, `features`, and `offers` exist as both, and the distinction is the grain:
"Acme cut close time 40%" is a claim typed `customer-proof`; the Acme case study that
proves it is a row in the [customer-proof register](customer-proof.md). Reference components
by ID, registers by path.

## Shared rules

- **Row IDs are kebab-case slugs**, unique within their register.
- **The `claims` column holds space-separated `clm-` IDs** from the
  [claims register](../claims.md). Registers never define claims; they reference them.
- **Canon-membership is not duplicated here.** Whether a row's claims are canon is read from
  the claims register and compiled into the [map](../claims-map.md); a register row that
  carries a non-canon claim shows up there as misaligned.
- **The parser maintains registers.** Rows land as sources are parsed; the register is the
  result, not something you maintain by hand. Exception: [features](features.md) may be
  human-seeded, because product truth is often unpublished.
- **Absence is a signal.** An empty register after a scan means the material doesn't exist;
  say so, don't pad.
