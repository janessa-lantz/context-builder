# Entities

Durable records of the outside-world actors the system tracks. Competitors first, and later
events, key people, and amplifiers. An entity page is the builder's accumulating knowledge of
one actor: its current state and the history of how it changed.

Entities are the outward-facing counterpart to the [content index](../content-index.md).
The content index aggregates *your* assets; entities aggregate *the outside world you track*.

## Raw, not vetted

Entities live in `context/` because they are knowledge the team draws from, but they sit at a
different trust level from everything else here. The canon, index, and visual identity are
vetted and safe to ship. Entity pages are scraped and synthesized intelligence: useful, but
unconfirmed and sometimes stale. Never treat an entity page as a sanctioned battlecard, and
never drop its text into a published asset. Anything shippable is a separate, human-vetted
artifact built on top of this raw material, never the material itself.

## Structure

`context/entities/{type}/{slug}.md`, one file per entity. Types group entities by what they
are:

- `competitors/`: companies you position against
- (future) `events/`, `key-people/`, `amplifiers/`

## An entity page

Two sections: a current-state **Profile** and an accumulating **Feed**.

### Frontmatter

- `id`: matches the filename
- `type`: the entity type (`competitor`, ...)
- `domain`: the entity's primary URL, when it has one
- `status`: `active`, `acquired`, or `defunct`
- `first_seen`: date the entity was first added, `YYYY-MM-DD`
- `last_scanned`: date a scan last touched this page
- `latest_summary`: id of the current [parsed summary](../../builder/parsed-summaries/) snapshot

### Profile

The current-state synthesis: who they are, their buyer, category posture, how they position.
Itemized by component where the evidence supports it, so it stays diffable against the canon.
Rewritten only when a scan detects the positioning shifted, not every cycle.

### Feed

Append-only. One row per detected change. Every row carries the `summary_id` of the source
that evidenced it, so provenance holds no matter which job wrote the row.

| column | meaning |
|--------|---------|
| `date` | when the change was observed or published, `YYYY-MM-DD` |
| `kind` | the signal type (below) |
| `component` | the message component it touches, by id, when one applies |
| `detail` | a short description of the change |
| `summary_id` | the parsed summary that evidenced it |

Signal kinds: `product-update` / `pricing-change` / `messaging-shift` / `partnership` /
`funding` / `hiring-signal` / `press-coverage` / `buyer-signal` / `other`.

## How entity pages are maintained

Two scans maintain a competitor entity, each owning one section:

- **[scan-competitive-profile](../../builder/jobs/scans/competitive-profile.md)** builds the **Profile**: parses each
  competitor's key pages against all components. Periodic, since messaging moves slowly. It is
  the [key-pages](../../builder/jobs/scans/key-pages.md) scan pointed outward, with output landing here
  rather than in the canon.
- **[scan-competitive-feed](../../builder/jobs/scans/competitive-feed.md)** builds the **Feed**: watches for the
  signal kinds above across the competitor's own surfaces and third-party news. Frequent.

The Feed has more than one producer. `buyer-signal` rows arrive from the sales-call parsing
path, not the competitive scans. The `summary_id` on every row keeps the source unambiguous.

## Example

```markdown
---
id: rival-co
type: competitor
domain: rival.example
status: active
first_seen: 2026-01-10
last_scanned: 2026-03-01
latest_summary: rival-co-2026-03-01
---

## Profile

- positioning: "The all-in-one platform for the close." Positions as a full-suite incumbent
  spanning import, review, and sign-off.
- buying-committee: finance and accounting leaders.
- unique-attributes: breadth across the full close workflow.

## Feed

| date | kind | component | detail | summary_id |
|------|------|-----------|--------|------------|
| 2026-02-18 | buyer-signal | unique-attributes | A prospect evaluated them but found the broad suite did not solve the specific close need | acme-winloss-0218 |
| 2026-01-22 | product-update | products | Shipped an AI assistant across the suite | rival-co-2026-01-22 |
```
