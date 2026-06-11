# Competitive Profile Scan

Builds the **Profile** section of each competitor [entity](../../../context/entities/) page. It
parses every competitor's key pages against all messaging components, capturing how they
position across the same schema as your own messaging. Competitor content is parsed for
intelligence, never added to your content index.

This is the [key-pages](key-pages.md) scan pointed outward: the same key-page discovery and
parser, but the output lands in `context/entities/competitors/` as raw intelligence rather
than in the canon.

Run it periodically. Competitor messaging moves slowly, so a deep re-parse each quarter or on
a known repositioning is enough. For week-to-week change, see
[scan-competitive-feed](competitive-feed.md).

## Targets

- competitor domains (one per line):
