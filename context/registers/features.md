# Features Register

The product truth, one row per capability or feature. The `claims` column records which
[claims](../claims.md) are made about each, so messaging stays traceable to what the product
actually does, and you can see which parts of the product have no messaging at all.

Rows are material, not statements: the feature "SAML SSO" lives here; the claim "SSO works
out of the box with Okta and Entra" lives in the claims register typed `features`. The parser
adds rows as product pages and docs are parsed. **Human seeding is allowed and expected**:
product truth is often unpublished, and a human-added row with no claims is one of the
sharpest gap signals the [map](../claims-map.md) can show.

## Columns

- `id`: unique kebab-case slug
- `name`: the capability or feature name
- `grain`: `capability` (workflow-grain: what the product enables) / `feature` (named product functionality)
- `product`: which product it belongs to (from the `products` component), blank for single-product companies
- `description`: one line, factual
- `source`: where it's documented (URL, file path, or `human`)
- `claims`: the `clm-` IDs asserted about it, space-separated (blank = unmessaged product truth)
- `last_confirmed`: `YYYY-MM-DD`

## Register

Deployment: **Mintlify**. Products above these rows: the docs platform, Agent, Assistant,
Automations, and the Slack agent (see `products` claims clm-015–019). Seeded from key pages,
pricing tier lists, and docs — not yet human-augmented.

| id | name | grain | product | description | source | claims | last_confirmed |
|----|------|-------|---------|-------------|--------|--------|----------------|
| self-updating-docs | Self-updating documentation | capability | Automations | Monitors codebase, detects user-facing changes, proposes updates on ship | https://mintlify.com/enterprise | clm-020 clm-021 | 2026-07-07 |
| slack-github-editing | Edit from Slack, GitHub, or browser | capability | platform | Update articles from where work happens | https://mintlify.com/use-cases/help-center | clm-022 | 2026-07-07 |
| threads-to-prs | Slack threads to pull requests | capability | Slack agent | Captures conversations into docs-repo PRs | https://mintlify.com/use-cases/slack-agent | clm-023 clm-050 | 2026-07-07 |
| conversational-assistant | AI-powered chat over docs | capability | Assistant | Embedded conversational answers for users | https://mintlify.com/enterprise | clm-024 clm-030 | 2026-07-07 |
| personalization | Personalized content | capability | platform | Content by role, plan, or customer type | https://mintlify.com/use-cases/help-center | clm-025 | 2026-07-07 |
| staleness-insights | Staleness and confusion insights | capability | platform | Surfaces outdated or confusing content | https://mintlify.com/use-cases/developer-documentation | clm-026 | 2026-07-07 |
| access-control | Access control | capability | platform | "Control who has access"; authentication from Starter | https://mintlify.com | clm-027 | 2026-07-07 |
| api-playground | API playground | feature | platform | Interactive API refs generated from OpenAPI specs | https://mintlify.com/use-cases/developer-documentation | clm-028 | 2026-07-07 |
| semantic-search | Exact-answer search | feature | platform | "Fast search that returns exact answers, not pages" | https://mintlify.com/use-cases/developer-documentation | clm-029 | 2026-07-07 |
| mcp-server | MCP server | feature | platform | Included from Starter; connects docs to agents | https://mintlify.com/pricing | clm-031 clm-052 | 2026-07-07 |
| slack-discord-bots | Slack and Discord bots | feature | Slack agent | Real-time, self-serve answers | https://mintlify.com/use-cases/developer-documentation | clm-032 | 2026-07-07 |
| sso-scim-rbac | SSO, SCIM & RBAC | feature | platform | Enterprise-tier identity and access | https://mintlify.com/pricing | clm-033 | 2026-07-07 |
| feedback-widgets | Feedback widgets | feature | platform | Flag gaps and unclear content | https://mintlify.com/use-cases/help-center | clm-034 | 2026-07-07 |
| human-llm-structure | Human + LLM content structure | feature | platform | Content structured for both humans and LLMs (llms.txt, markdown export) | https://mintlify.com/use-cases/developer-documentation | clm-035 | 2026-07-07 |
| grounded-answers | Grounded, cited answers | feature | Slack agent | "Answers grounded in your docs, with sources" | https://mintlify.com/use-cases/slack-agent | clm-036 | 2026-07-07 |
| web-editor | Web editor | feature | platform | Browser-based editing, from Starter | https://mintlify.com/pricing | clm-076 | 2026-07-07 |
| git-sync | Git sync | feature | platform | Docs-as-code workflow with git workflows | https://mintlify.com/use-cases/knowledge-base | clm-038 | 2026-07-07 |
