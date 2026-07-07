# Claims Register

The source of truth for your messaging, one claim per row. A **claim** is a single assertable
statement, typed by a [component](README.md) ID. The rows with `status: canon` **are** the
canon: your approved messaging. Everything downstream keys on the claim: [evidence](evidence.md)
accumulates against it, [registers](registers/) log which material carries it,
[lockups](lockups.md) and [entry points](entry-points.md) compose it into units of messaging,
and the [map](claims-map.md) shows its coverage. If it can fit into a spreadsheet it can be
wrangled and managed; this table is that spreadsheet.

The [builder](../builder/) maintains this register. Skills read it and never write it.

## Rules

- **The LLM mints claims from verbatim, company-published copy only**, source attributed.
  Claims found on live key pages enter as `canon`; claims found on other owned surfaces enter
  as `candidate`. Customer and competitor material never mints a claim; it adds
  [evidence](evidence.md) or files an [issue](../builder/issues/).
- **A human may add synthesized claims**, marked `source: human`. The LLM never edits,
  retires, or re-statuses a `source: human` row.
- **Demotion is human-only.** The LLM never moves a claim out of `canon`. If a re-scan cannot
  find a canon claim on any live surface, leave `last_confirmed` stale and file an issue;
  never silently retire.
- **Rows are never deleted.** A dead claim becomes `retired` and keeps its ID and history.
- **Absence is a signal.** A component with no claims is a finding (the [map](claims-map.md)
  writes the zero), not a hole to patch with invention.

## Columns

- `id`: `clm-NNN`, sequential, never reused
- `component`: the component ID this claim is typed by (see [README](README.md))
- `claim`: the statement itself; verbatim from a live surface, or human synthesis
- `status`: see below
- `confidence`: `high` / `medium` / `low` — how far the claim can be trusted as captured (see below)
- `variant_of`: blank for a primary claim; a `clm-` ID when this row is a divergent phrasing
  of that claim
- `source`: the surface carrying the phrasing (a register row ID or URL), or `human`
- `first_seen`: date the claim entered the register, `YYYY-MM-DD`
- `last_confirmed`: date the claim was last seen live (or last affirmed by a human)

## Statuses

- `canon`: approved messaging. Verbatim from a live key page, or human-authored. Skills ship it.
- `candidate`: observed on an owned surface but not approved. Skills do not ship it. A human
  promotes a candidate to canon (often via [codify](../builder/jobs/codify.md)).
- `retired`: no longer messaging. Kept for history; the ID is never reused.

## Confidence

A trust signal on each claim, rendered as a dot in the views (🟢 high · 🟡 medium · 🔴 low).
It is orthogonal to status: a candidate can be high-confidence, a canon claim can be low.

- **high** 🟢: verbatim from a live key page, unambiguous, no conflicting version elsewhere, no open issue about its accuracy. Ship as-is.
- **medium** 🟡: verbatim but flagged — a `divergent` variant is live, a stat differs across surfaces, or the unit is ambiguous. Check before shipping.
- **low** 🔴: a value the parser could not verify, or LLM synthesis the [rules](#rules) say a human should author. Needs a human.

The parser sets it on mint; the [analyzer](../builder/jobs/analyzer.md) lowers it when an
open [issue](../builder/issues/) contradicts the claim.

## Variants

Divergent phrasings of the same claim are their own rows, each pointing at the primary via
`variant_of`. The primary row carries the canonical phrasing. To make a variant canonical, a
human swaps the direction of the pointer. Variants let the map show `divergent` messaging in
the wild without collapsing real differences into one row.

## Register

Deployment: **Mintlify** (mintlify.com). Minted by the setup run of 2026-07-07 from the live
key pages; candidates from the owned-surface sample. Synthesis rows (`company-description`,
`icp`) are labeled in `source`; see iss-006.

| id | component | claim | status | confidence | variant_of | source | first_seen | last_confirmed |
|----|-----------|-------|--------|------------|------------|--------|------------|----------------|
| clm-001 | positioning | "The knowledge infrastructure agents build on" | canon | high | | homepage | 2026-07-07 | 2026-07-07 |
| clm-002 | positioning | "Self-updating documentation for startups, enterprises, and agents." | canon | high | | homepage | 2026-07-07 | 2026-07-07 |
| clm-003 | category-name | "knowledge infrastructure" | canon | medium | | homepage | 2026-07-07 | 2026-07-07 |
| clm-004 | category-name | "AI-native documentation platform" | candidate | medium | clm-003 | blog-trieve-acquisition | 2026-07-07 | 2026-07-07 |
| clm-005 | point-of-view | "When the majority of your readers are machines, not humans, beautiful documentation and elegant UI become secondary concerns." | canon | high | | blog-documentation-is-dead | 2026-07-07 | 2026-07-07 |
| clm-006 | point-of-view | "Expecting humans to maintain up-to-date documentation will always be a losing battle." | canon | high | | blog-documentation-is-dead | 2026-07-07 | 2026-07-07 |
| clm-007 | point-of-view | "The future belongs to companies that treat knowledge as self-improving infrastructure." | canon | high | | blog-documentation-is-dead | 2026-07-07 | 2026-07-07 |
| clm-008 | point-of-view | "Raw code is a poor interface for coding agents." | candidate | high | | blog-structured-docs-coding-agents | 2026-07-07 | 2026-07-07 |
| clm-009 | narrative | "Since we started, the role of documentation has shifted more dramatically than we ever expected." | canon | high | | blog-series-b | 2026-07-07 | 2026-07-07 |
| clm-010 | narrative | "Documentation is no longer just content. It's infrastructure." | canon | high | | blog-series-b | 2026-07-07 | 2026-07-07 |
| clm-011 | narrative | "Today, it's 50% for humans, 50% for AI, and the ratio is shifting fast." | canon | high | | blog-documentation-is-dead | 2026-07-07 | 2026-07-07 |
| clm-012 | founder-story | "When Hahnbee and I started Mintlify in 2022, it was on a very simple mission: empower builders and make it effortless for developers to understand how software works." (Han Wang) | canon | high | | blog-series-b | 2026-07-07 | 2026-07-07 |
| clm-013 | founder-story | "We were the developers at 2am trying to integrate an API, piecing together answers from a stale README." | canon | high | | blog-series-b | 2026-07-07 | 2026-07-07 |
| clm-014 | company-description | Mintlify is the knowledge-infrastructure company: an AI-native documentation platform 20,000+ companies use for self-updating docs that serve developers and the AI agents they send ahead. | canon | low | | synthesis: homepage, blog-series-b, contact-sales | 2026-07-07 | 2026-07-07 |
| clm-015 | products | "One platform for your entire knowledge stack. Agents that keep work moving 24/7." | canon | high | | homepage | 2026-07-07 | 2026-07-07 |
| clm-016 | products | Mintlify Agent "helps you write and maintain documentation using AI" | candidate | high | | blog-agents-launch | 2026-07-07 | 2026-07-07 |
| clm-017 | products | AI Assistant: "a fully embedded, conversational experience that helps users get to the right answer faster with your documentation" | candidate | high | | blog-ai-assistant | 2026-07-07 | 2026-07-07 |
| clm-018 | products | "A personal agent for your team's knowledge, in Slack" | canon | high | | use-case-slack-agent | 2026-07-07 | 2026-07-07 |
| clm-019 | products | Agent and automations: "a self-updating documentation engine grounded in your codebase" | candidate | high | | blog-autopilot | 2026-07-07 | 2026-07-07 |
| clm-020 | capabilities | "Self-updating knowledge" | canon | high | | homepage | 2026-07-07 | 2026-07-07 |
| clm-021 | capabilities | "Automate documentation updates" — continuous updates based on code changes | canon | high | | enterprise | 2026-07-07 | 2026-07-07 |
| clm-022 | capabilities | "Update articles directly from Slack, GitHub, or browser" | canon | high | | use-case-help-center | 2026-07-07 | 2026-07-07 |
| clm-023 | capabilities | "Turn Slack threads into pull requests" | canon | high | | use-case-slack-agent | 2026-07-07 | 2026-07-07 |
| clm-024 | capabilities | "AI-powered chat for your users" | canon | high | | enterprise | 2026-07-07 | 2026-07-07 |
| clm-025 | capabilities | "Personalized content by role, plan, or customer type" | canon | high | | use-case-help-center | 2026-07-07 | 2026-07-07 |
| clm-026 | capabilities | "Insights that surface outdated or confusing content" | canon | high | | use-case-developer-documentation | 2026-07-07 | 2026-07-07 |
| clm-027 | capabilities | "Control who has access" | canon | high | | homepage | 2026-07-07 | 2026-07-07 |
| clm-028 | features | "Interactive API refs generated from OpenAPI specs" | canon | high | | use-case-developer-documentation | 2026-07-07 | 2026-07-07 |
| clm-029 | features | "Fast search that returns exact answers, not pages" | canon | high | | use-case-developer-documentation | 2026-07-07 | 2026-07-07 |
| clm-030 | features | "AI assistant that explains concepts and API behavior" | canon | high | | use-case-developer-documentation | 2026-07-07 | 2026-07-07 |
| clm-031 | features | MCP server, included from the Starter tier | canon | high | | pricing | 2026-07-07 | 2026-07-07 |
| clm-032 | features | "Slack and Discord bots for real-time questions" | canon | high | | use-case-developer-documentation | 2026-07-07 | 2026-07-07 |
| clm-033 | features | "SSO, SCIM & RBAC" at the Enterprise tier | canon | high | | pricing | 2026-07-07 | 2026-07-07 |
| clm-034 | features | "Feedback widgets to flag gaps and unclear content" | canon | high | | use-case-help-center | 2026-07-07 | 2026-07-07 |
| clm-035 | features | "Content structured for both humans and LLMs" | canon | high | | use-case-developer-documentation | 2026-07-07 | 2026-07-07 |
| clm-036 | features | Ask: "Answers grounded in your docs, with sources" | canon | high | | use-case-slack-agent | 2026-07-07 | 2026-07-07 |
| clm-037 | unique-attributes | "Purpose built for developers" | canon | high | | switch | 2026-07-07 | 2026-07-07 |
| clm-038 | unique-attributes | "Treats docs as code as table stakes, not an afterthought" | canon | high | | switch | 2026-07-07 | 2026-07-07 |
| clm-039 | unique-attributes | "AI-native, beautiful out-of-the-box, and built for collaboration" | canon | high | | enterprise | 2026-07-07 | 2026-07-07 |
| clm-040 | unique-attributes | "Built for humans and AI" | canon | high | | enterprise | 2026-07-07 | 2026-07-07 |
| clm-041 | unique-attributes | "Data is never used to train models" | canon | high | | use-case-slack-agent | 2026-07-07 | 2026-07-07 |
| clm-042 | value-proposition | "Docs that handle support for you" — "fewer tickets and faster resolution" | canon | high | | use-case-help-center | 2026-07-07 | 2026-07-07 |
| clm-043 | value-proposition | "Docs developers (and LLMs) love" | canon | high | | use-case-developer-documentation | 2026-07-07 | 2026-07-07 |
| clm-044 | value-proposition | "Your team's source of truth" — "replaces scattered notes and institutional memory with a unified system that stays accurate" | canon | high | | use-case-knowledge-base | 2026-07-07 | 2026-07-07 |
| clm-045 | value-proposition | "+64% agent precision, +39% discoverability, 2X token efficiency" | canon | high | | contact-sales | 2026-07-07 | 2026-07-07 |
| clm-046 | value-proposition | "You can launch beautiful docs in minutes" | canon | high | | switch | 2026-07-07 | 2026-07-07 |
| clm-047 | value-proposition | "Ship at startup speed. Build at enterprise scale." | canon | high | | enterprise | 2026-07-07 | 2026-07-07 |
| clm-048 | value-proposition | "50% reduction in support tickets" | canon | high | | switch | 2026-07-07 | 2026-07-07 |
| clm-049 | value-proposition | "2x faster time to first API call" | canon | high | | switch | 2026-07-07 | 2026-07-07 |
| clm-050 | how-it-works | "Mention @mintlify in any channel or DM" → "agent reads full thread context" → "opens pull request in docs repository" → "live status updates until PR ready" | canon | high | | use-case-slack-agent | 2026-07-07 | 2026-07-07 |
| clm-051 | how-it-works | "Detect code changes that require documentation updates" → "surface the updates" → "generate documentation drafts" | candidate | high | | blog-autopilot | 2026-07-07 | 2026-07-07 |
| clm-052 | ecosystem-integrations | "Connect Claude, Codex, Cursor and custom MCPs" | canon | high | | contact-sales | 2026-07-07 | 2026-07-07 |
| clm-053 | ecosystem-integrations | Slack, GitHub, Discord, and OpenAPI integrations across the platform | canon | high | | use-case-developer-documentation | 2026-07-07 | 2026-07-07 |
| clm-054 | ecosystem-integrations | Deployment via GitHub, GitLab, Vercel, and Cloudflare | candidate | high | | docs | 2026-07-07 | 2026-07-07 |
| clm-055 | icp | Account: developer-facing software companies, "from frontier AI companies to consumer brands" and global enterprises, docs-as-code stacks (GitHub/GitLab, OpenAPI), Slack-centered teams; triggers: AI-agent traffic to docs, migration off legacy docs tools, new startup/YC batch. Champion: the docs/DevEx owner (DevRel, technical writing, platform eng) accountable for onboarding, activation, and support deflection. | canon | low | | synthesis: use-cases, enterprise, startups, switch | 2026-07-07 | 2026-07-07 |
| clm-056 | value-drivers | Cost savings: docs deflect support — "fewer tickets and faster resolution" | canon | high | | use-case-help-center | 2026-07-07 | 2026-07-07 |
| clm-057 | value-drivers | Efficiency: "Automate documentation updates" frees engineering time | canon | high | | enterprise | 2026-07-07 | 2026-07-07 |
| clm-058 | value-drivers | Revenue generation: "Documentation is often the highest-traffic, highest-intent surface in the entire funnel." | candidate | high | | blog-demand-channel | 2026-07-07 | 2026-07-07 |
| clm-059 | customer-proof | Coinbase: "20min → 60s Doc update time reduction" | canon | high | | customers | 2026-07-07 | 2026-07-07 |
| clm-060 | customer-proof | HubSpot: "50% Reduction in eng resources on docs" | canon | high | | customers | 2026-07-07 | 2026-07-07 |
| clm-061 | customer-proof | Zapier: "3x Faster documentation updates" | canon | high | | customers | 2026-07-07 | 2026-07-07 |
| clm-062 | customer-proof | Laravel: "3 days Migration time" | canon | high | | customers | 2026-07-07 | 2026-07-07 |
| clm-063 | customer-proof | Fidelity: "99.99% Uptime since launch" | canon | high | | customers | 2026-07-07 | 2026-07-07 |
| clm-064 | customer-proof | Anthropic: "2M+ Monthly active developers," "3+ Products serviced: Claude API, MCP, and Claude Code" | canon | medium | | enterprise | 2026-07-07 | 2026-07-07 |
| clm-065 | customer-proof | "At Browserbase, our docs are the product." — Paul Klein, CEO, Browserbase | canon | high | | customers | 2026-07-07 | 2026-07-07 |
| clm-066 | customer-proof | Coinbase: "Projected annual support savings: $106K–$239K" | candidate | high | | customer-coinbase | 2026-07-07 | 2026-07-07 |
| clm-067 | market-proof | "$45M Series B at a $500M valuation" led by Andreessen Horowitz and Salesforce Ventures; $67M total funding | canon | high | | blog-series-b | 2026-07-07 | 2026-07-07 |
| clm-068 | market-proof | "Every YC batch we consistently see the top performing startups use Mintlify to build their docs." — Harj Taggar, Group Partner, Y Combinator | canon | high | | startups | 2026-07-07 | 2026-07-07 |
| clm-069 | key-metrics | "20,000+ of the world's most ambitious companies building for agents" | canon | medium | | homepage | 2026-07-07 | 2026-07-07 |
| clm-070 | key-metrics | "300M+ visitors in the past year" | canon | high | | homepage | 2026-07-07 | 2026-07-07 |
| clm-071 | key-metrics | "2B+ agents in the past year" | canon | medium | | homepage | 2026-07-07 | 2026-07-07 |
| clm-072 | key-metrics | "99.99% uptime across all services" | canon | high | | homepage | 2026-07-07 | 2026-07-07 |
| clm-073 | key-metrics | "Documentation experiences for over 100 million builders worldwide" | canon | medium | | switch | 2026-07-07 | 2026-07-07 |
| clm-074 | key-metrics | "Nearly 50% of documentation traffic now comes from AI agents" | canon | high | | blog-series-b | 2026-07-07 | 2026-07-07 |
| clm-075 | key-metrics | "Answers over 23 million queries in documentation every month" | candidate | high | | blog-trieve-acquisition | 2026-07-07 | 2026-07-07 |
| clm-076 | pricing-model | Three tiers — Starter "$0/mo", Pro (monthly or annual), Enterprise ("Contact us") — plus usage credits: Starter includes "10,000 / month, $0.01 per credit for overages" | canon | low | | pricing | 2026-07-07 | 2026-07-07 |
| clm-077 | packaging | Starter "for individuals and small teams"; Pro "for startups and growing teams"; Enterprise "for scaling and global teams" | canon | high | | pricing | 2026-07-07 | 2026-07-07 |
| clm-078 | packaging | Pro adds Agent, Assistant, Automations, preview deployments, admin APIs; Enterprise adds "SSO, SCIM & RBAC," "Performance SLA," "Advanced insights," "Enterprise security & legal," "Migration & support" | canon | high | | pricing | 2026-07-07 | 2026-07-07 |
| clm-079 | add-ons-services | "White-glove service to seamlessly transition your entire documentation" | canon | high | | switch | 2026-07-07 | 2026-07-07 |
| clm-080 | offers | "Get started for free, your first month of credits on us." | canon | high | | pricing | 2026-07-07 | 2026-07-07 |
| clm-081 | offers | Startups: "50% off Pro for the year"; YC alumni: 50% off Pro for one year; current YC batch: "12 months of Pro free through launch" plus "priority support" | canon | high | | startups | 2026-07-07 | 2026-07-07 |
