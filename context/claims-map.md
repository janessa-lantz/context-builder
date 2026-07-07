# Claims Map

*Compiled by the [analyzer](../builder/jobs/analyzer.md). Do not edit; regenerate.*

The coverage view over the whole system: every [claim](claims.md)'s evidence depth and reach
across the [registers](registers/), every [component](README.md)'s claim count with the
zeros written out, and every asset carrying messaging that isn't canon. Gaps — missing or
misaligned — read directly off this file. Absence is a signal, so empty is spelled out,
never omitted.

compiled: 2026-07-07 · components_version: 2 · deployment: Mintlify

All evidence is `public`: no sales-call or customer sources have been ingested, so every
`private ev` count is 0 — that column starts moving when transcripts arrive.

## Coverage by component

| component | canon | candidate | retired | public ev | private ev | assets |
|-----------|-------|-----------|---------|-----------|------------|--------|
| point-of-view | 3 | 1 | 0 | 4 | 0 | 2 |
| narrative | 3 | 0 | 0 | 3 | 0 | 2 |
| positioning | 2 | 0 | 0 | 3 | 0 | 2 |
| founder-story | 2 | 0 | 0 | 2 | 0 | 1 |
| company-description | 1 | 0 | 0 | 1 | 0 | 0 |
| category-name | 1 | 1 | 0 | 4 | 0 | 4 |
| products | 2 | 3 | 0 | 5 | 0 | 5 |
| capabilities | 8 | 0 | 0 | 8 | 0 | 12 |
| features | 9 | 0 | 0 | 9 | 0 | 12 |
| unique-attributes | 5 | 0 | 0 | 6 | 0 | 5 |
| value-proposition | 8 | 0 | 0 | 9 | 0 | 7 |
| how-it-works | 1 | 1 | 0 | 2 | 0 | 3 |
| ecosystem-integrations | 2 | 1 | 0 | 3 | 0 | 4 |
| icp | 1 | 0 | 0 | 1 | 0 | 0 |
| buying-committee | 0 | 0 | 0 | 0 | 0 | 0 |
| value-drivers | 2 | 1 | 0 | 3 | 0 | 3 |
| customer-proof | 7 | 1 | 0 | 11 | 0 | 13 |
| market-proof | 2 | 0 | 0 | 3 | 0 | 3 |
| key-metrics | 6 | 1 | 0 | 11 | 0 | 6 |
| pricing-model | 1 | 0 | 0 | 1 | 0 | 2 |
| packaging | 2 | 0 | 0 | 2 | 0 | 2 |
| add-ons-services | 1 | 0 | 0 | 1 | 0 | 1 |
| offers | 2 | 0 | 0 | 2 | 0 | 6 |
| themes | 0 | 0 | 0 | 0 | 0 | 0 |
| topics | 0 | 0 | 0 | 0 | 0 | 0 |
| campaigns | 0 | 0 | 0 | 0 | 0 | 0 |

Totals: 71 canon · 10 candidate · 0 retired · 94 evidence rows. The `buying-committee` zero
is a real gap (iss-005); the `themes`/`topics`/`campaigns` zeros are deliberate — setup
defers them to owned-content analysis.

## Claims

Flags: `unevidenced` (no evidence), `stale` (last_confirmed lags), `orphan` (in no register
row), `divergent` (variants live on published surfaces), `contested` (competitor pressure —
none possible yet; no entities tracked).

| id | claim | status | public ev | private ev | assets | flags |
|----|-------|--------|-----------|------------|--------|-------|
| clm-001 | "The knowledge infrastructure agents build on" | canon | 2 | 0 | 2 | |
| clm-002 | "Self-updating documentation for startups, enterprises, and agents." | canon | 1 | 0 | 1 | |
| clm-003 | "knowledge infrastructure" | canon | 1 | 0 | 1 | divergent |
| clm-004 | "AI-native documentation platform" | candidate | 3 | 0 | 3 | divergent |
| clm-005 | machines-as-majority-readers | canon | 1 | 0 | 1 | |
| clm-006 | humans-maintaining-docs is a losing battle | canon | 1 | 0 | 1 | |
| clm-007 | knowledge as self-improving infrastructure | canon | 1 | 0 | 1 | |
| clm-008 | "Raw code is a poor interface for coding agents." | candidate | 1 | 0 | 1 | |
| clm-009 | role of documentation shifted dramatically | canon | 1 | 0 | 1 | |
| clm-010 | "no longer just content. It's infrastructure." | canon | 1 | 0 | 1 | |
| clm-011 | "50% for humans, 50% for AI" | canon | 1 | 0 | 1 | |
| clm-012 | 2022 mission origin (Han Wang) | canon | 1 | 0 | 1 | |
| clm-013 | 2am stale-README origin | canon | 1 | 0 | 1 | |
| clm-014 | company description (synthesis) | canon | 1 | 0 | 0 | orphan |
| clm-015 | "One platform for your entire knowledge stack..." | canon | 1 | 0 | 1 | |
| clm-016 | Mintlify Agent description | candidate | 1 | 0 | 1 | |
| clm-017 | AI Assistant description | candidate | 1 | 0 | 1 | |
| clm-018 | Slack agent description | canon | 1 | 0 | 1 | |
| clm-019 | agent + automations engine description | candidate | 1 | 0 | 1 | |
| clm-020 | "Self-updating knowledge" | canon | 1 | 0 | 2 | |
| clm-021 | "Automate documentation updates" | canon | 1 | 0 | 2 | |
| clm-022 | edit from Slack/GitHub/browser | canon | 1 | 0 | 2 | |
| clm-023 | "Turn Slack threads into pull requests" | canon | 1 | 0 | 2 | |
| clm-024 | "AI-powered chat for your users" | canon | 1 | 0 | 2 | |
| clm-025 | personalized content by role/plan/type | canon | 1 | 0 | 2 | |
| clm-026 | staleness/confusion insights | canon | 1 | 0 | 2 | |
| clm-027 | "Control who has access" | canon | 1 | 0 | 2 | |
| clm-028 | API playground from OpenAPI | canon | 1 | 0 | 2 | |
| clm-029 | exact-answer search | canon | 1 | 0 | 2 | |
| clm-030 | assistant explains concepts and API behavior | canon | 1 | 0 | 2 | |
| clm-031 | MCP server from Starter | canon | 1 | 0 | 2 | |
| clm-032 | Slack/Discord bots | canon | 1 | 0 | 2 | |
| clm-033 | SSO, SCIM & RBAC at Enterprise | canon | 1 | 0 | 2 | |
| clm-034 | feedback widgets | canon | 1 | 0 | 2 | |
| clm-035 | content structured for humans and LLMs | canon | 1 | 0 | 2 | |
| clm-036 | grounded, cited answers | canon | 1 | 0 | 2 | |
| clm-037 | "purpose built for developers" | canon | 1 | 0 | 1 | |
| clm-038 | docs-as-code as table stakes | canon | 1 | 0 | 2 | |
| clm-039 | "AI-native, beautiful out-of-the-box..." | canon | 2 | 0 | 2 | |
| clm-040 | "Built for humans and AI" | canon | 1 | 0 | 1 | |
| clm-041 | data never used to train models | canon | 1 | 0 | 1 | |
| clm-042 | docs handle support; fewer tickets | canon | 1 | 0 | 1 | |
| clm-043 | "Docs developers (and LLMs) love" | canon | 1 | 0 | 1 | |
| clm-044 | team's source of truth | canon | 1 | 0 | 1 | |
| clm-045 | +64% precision, +39% discoverability, 2X tokens | canon | 2 | 0 | 2 | |
| clm-046 | launch beautiful docs in minutes | canon | 1 | 0 | 1 | |
| clm-047 | startup speed, enterprise scale | canon | 1 | 0 | 1 | |
| clm-048 | 50% support-ticket reduction | canon | 1 | 0 | 1 | |
| clm-049 | 2x faster first API call | canon | 1 | 0 | 1 | |
| clm-050 | Slack agent flow (mention → PR) | canon | 1 | 0 | 2 | |
| clm-051 | detect → surface → generate | candidate | 1 | 0 | 1 | |
| clm-052 | Claude, Codex, Cursor, custom MCPs | canon | 1 | 0 | 2 | |
| clm-053 | Slack, GitHub, Discord, OpenAPI | canon | 1 | 0 | 1 | |
| clm-054 | GitHub/GitLab/Vercel/Cloudflare deploys | candidate | 1 | 0 | 1 | |
| clm-055 | ICP (synthesis) | canon | 1 | 0 | 0 | orphan |
| clm-056 | cost savings via support deflection | canon | 1 | 0 | 1 | |
| clm-057 | efficiency via automated updates | canon | 1 | 0 | 1 | |
| clm-058 | docs as highest-intent demand channel | candidate | 1 | 0 | 1 | |
| clm-059 | Coinbase 20min → 60s | canon | 2 | 0 | 3 | |
| clm-060 | HubSpot 50% eng-resource reduction | canon | 1 | 0 | 2 | |
| clm-061 | Zapier 3x faster updates | canon | 2 | 0 | 3 | |
| clm-062 | Laravel 3-day migration | canon | 1 | 0 | 2 | |
| clm-063 | Fidelity 99.99% uptime | canon | 1 | 0 | 2 | |
| clm-064 | Anthropic 2M+ MAU, 3+ products | canon | 2 | 0 | 3 | |
| clm-065 | Browserbase "docs are the product" | canon | 1 | 0 | 2 | |
| clm-066 | Coinbase $106K–$239K support savings | candidate | 1 | 0 | 3 | |
| clm-067 | $45M Series B, $500M valuation | canon | 1 | 0 | 1 | |
| clm-068 | YC partner quote | canon | 2 | 0 | 2 | |
| clm-069 | 20,000+ companies | canon | 3 | 0 | 3 | |
| clm-070 | 300M+ visitors/yr | canon | 1 | 0 | 1 | |
| clm-071 | 2B+ agents/yr | canon | 1 | 0 | 1 | |
| clm-072 | 99.99% uptime | canon | 2 | 0 | 2 | |
| clm-073 | 100M+ builders worldwide | canon | 2 | 0 | 2 | divergent |
| clm-074 | ~50% of docs traffic from AI agents | canon | 1 | 0 | 1 | |
| clm-075 | 23M+ monthly doc queries | candidate | 1 | 0 | 1 | |
| clm-076 | tiers + credit pricing | canon | 1 | 0 | 3 | |
| clm-077 | tier audiences | canon | 1 | 0 | 2 | |
| clm-078 | Pro/Enterprise ladders | canon | 1 | 0 | 1 | |
| clm-079 | white-glove migration | canon | 1 | 0 | 1 | |
| clm-080 | first month of credits free | canon | 1 | 0 | 3 | |
| clm-081 | startup/YC program | canon | 1 | 0 | 3 | |

## Misaligned assets

Register rows carrying `candidate` claims: published material saying something the canon
doesn't (or doesn't yet).

| register row | claims | issue |
|--------------|--------|-------|
| blog-trieve-acquisition | clm-004 clm-075 | iss-001 |
| docs | clm-004 clm-054 | iss-001 |
| library-mintlify-vs-docusaurus | clm-004 | iss-001 |
| blog-demand-channel | clm-058 | iss-002 |
| blog-agents-launch | clm-016 | — |
| blog-ai-assistant | clm-017 | — |
| blog-autopilot | clm-019 clm-051 | — |
| blog-structured-docs-coding-agents | clm-008 | — |
| customer-coinbase | clm-066 | — |

Rows marked — carry launch-post candidates awaiting normal promotion review via
[codify](../builder/jobs/codify.md), not drift.
