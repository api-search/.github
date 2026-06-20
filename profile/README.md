# APIs.io — Federated API Search Network

[**APIs.io**](https://apis.io) is a federated, agent-friendly directory of public-internet APIs. It indexes API providers from across the web — their APIs, JSON Schemas, event-driven specifications, governance rules, vocabularies, JSON-LD contexts, pricing plans, rate limits, FinOps profiles, the agent surfaces they publish (Agent Skills and MCP servers), and the industries and regions they serve — and publishes every slice of metadata as its own browsable section of the site.

The whole network is served from a **single origin** — one S3 + CloudFront distribution on the apex domain [`apis.io`](https://apis.io). Each catalog renders into its own path namespace (`apis.io/providers/`, `apis.io/schemas/`, …), and a read-only **search API** and an **MCP server** are served as paths under the same origin. The legacy per-subdomain sites (`providers.apis.io`, `schemas.apis.io`, …) now `301`-redirect to their apex paths and are kept only as aliases. Every section carries the same agent-readiness baseline (`llms.txt`, RFC 9727 `api-catalog`, permissive `robots.txt`, schema.org JSON-LD).

> **The network is consumed via [apis.io](https://apis.io), the [search API](https://apis.io/developer) and [MCP server](https://apis.io/mcp), the RFC 9727 `api-catalog` linkset, the `llms.txt` / `llms-full.txt` agent feeds, and the sitemaps.** Everything below is open-access content, free to search, ground LLMs against, train on, or republish — see [https://apis.io/terms/](https://apis.io/terms/) for the full terms.

## The network — public catalogs

### Search & discovery hub

| Section | What you'll find |
|---|---|
| **[apis.io](https://apis.io)** | Search hub for the whole network — search by provider, schema, tag, or name; blog; cross-network insights |
| **[apis.io/tags/](https://apis.io/tags/)** | Tag index across the network — every provider and API that carries a tag, scored and ranked |
| **[apis.io/industries/](https://apis.io/industries/)** | 29 industry verticals (Financial Services, Healthcare, Manufacturing, Transportation, Energy, Government, …) |
| **[apis.io/regions/](https://apis.io/regions/)** | 17 macro sales regions (North America, LATAM, EMEA, APAC, Greater China, ANZ, …) |
| **[apis.io/developer](https://apis.io/developer)** | Developer portal & machine-readable feeds |

### Per-entity catalogs

| Section | What you'll find |
|---|---|
| **[apis.io/providers/](https://apis.io/providers/)** | API provider profiles — one page per organization, with cross-links to every artifact that organization publishes |
| **[apis.io/apis/](https://apis.io/apis/)** | Individual API records — one page per published API, with the OpenAPI spec and provider link |
| **[apis.io/schemas/](https://apis.io/schemas/)** | JSON Schemas extracted from every indexed API — Google Dataset Search ingestion-ready |
| **[apis.io/collections/](https://apis.io/collections/)** | Postman Collections and Open Collections — ready-to-run request sets for thousands of APIs |
| **[apis.io/asyncapis/](https://apis.io/asyncapis/)** | AsyncAPI event-driven specifications |
| **[apis.io/graphqls/](https://apis.io/graphqls/)** | GraphQL API specifications — endpoint URLs, documentation, and reference links |
| **[apis.io/channels/](https://apis.io/channels/)** | Event channels drilled out of every AsyncAPI spec — one page per channel |
| **[apis.io/arazzos/](https://apis.io/arazzos/)** | Arazzo API workflow specs — provider-specific and cross-provider multi-step workflows |
| **[apis.io/jsonld/](https://apis.io/jsonld/)** | JSON-LD contexts and semantic vocabularies |
| **[apis.io/rules/](https://apis.io/rules/)** | Spectral governance rulesets |
| **[apis.io/vocabularies/](https://apis.io/vocabularies/)** | Provider tag vocabularies powering the advanced search |
| **[apis.io/examples/](https://apis.io/examples/)** | API usage examples |

### Agent surfaces

| Section | What you'll find |
|---|---|
| **[apis.io/skills/](https://apis.io/skills/)** | Official Claude Agent Skill index — `SKILL.md` files published by providers, with per-skill and per-provider pages |
| **[apis.io/servers/](https://apis.io/servers/)** | Official Model Context Protocol server index — one page per MCP server, with install hints and source links |

### Commercial & operational surfaces

| Section | What you'll find |
|---|---|
| **[apis.io/plans/](https://apis.io/plans/)** | API pricing-plan profiles (API Commons Plans format) |
| **[apis.io/rate-limits/](https://apis.io/rate-limits/)** | API rate-limit profiles (API Commons Rate Limits format) |
| **[apis.io/finops/](https://apis.io/finops/)** | API FinOps profiles aligned with the FinOps Foundation FOCUS framework |

## Agentic access — search API & MCP server

The same catalog is queryable programmatically, served as paths under the apex origin:

| Surface | URL |
|---|---|
| **Search API** (REST, metered & tiered) | [apis.io/api/v1](https://apis.io/api/v1) — see [apis.io/developer](https://apis.io/developer) |
| **MCP server** (Streamable HTTP, tier-gated tools) | [apis.io/mcp](https://apis.io/mcp) |

Access is **metered, tiered, and monetized** — a free tier plus paid tiers (GitHub OAuth sign-in, API keys, Stripe billing). The developer portal at [apis.io/developer](https://apis.io/developer) documents the endpoints, authentication, and tiers.

## Machine-readable feeds

| Feed | URL |
|---|---|
| **RFC 9727 `api-catalog` linkset** | [apis.io/.well-known/api-catalog](https://apis.io/.well-known/api-catalog) |
| **`llms.txt` (agent overview)** | [apis.io/llms.txt](https://apis.io/llms.txt) |
| **`llms-full.txt` (dense reference)** | [apis.io/llms-full.txt](https://apis.io/llms-full.txt) |
| **Sitemap index (all sections)** | [apis.io/sitemap_index.xml](https://apis.io/sitemap_index.xml) |
| **APIs.json self-description** | [apis.io/apis.json](https://apis.io/apis.json) |

Each catalog section also publishes its own `llms.txt`, `sitemap.xml`, and (where relevant) `search-index.json` for client-side search.

## How it works

A central build pipeline (the [`network`](https://github.com/api-search/network) repo) reads from a set of upstream provider repos at [github.com/api-evangelist](https://github.com/api-evangelist) — Git-versioned [APIs.json](https://apisjson.org) profiles, one per provider — and emits Jekyll collections for every catalog. Each catalog is built independently, then **synced into one S3 bucket** and served through a single CloudFront distribution on `apis.io`; the search API and MCP server run as Lambdas behind API Gateway on the same origin.

Every provider, API, schema, and operational profile page carries:

- A 1–3 paragraph generated prose `overview`, derived deterministically from the structured frontmatter (unique per page; no LLM-randomness)
- Schema.org JSON-LD typed to the entity — `Organization` + `ItemList` on providers, `WebAPI` on APIs, `Dataset` on schemas and operational profiles, `CollectionPage` on industry and region pages, `BlogPosting` on posts, all with `BreadcrumbList` siblings
- Open Graph and Twitter Card metadata
- Cross-page internal links — "Other APIs from this provider", "Related industries", "Related regions"
- A per-collection title suffix that telegraphs page type in SERPs (e.g. `Stripe Charges API — Documentation, OpenAPI | APIs.io APIs`)

Providers also get a composite rating (0–100, banded Exemplar / Strong / Developing / Thin / Minimal) recomputed on every build — see [apis.io/rating/](https://apis.io/rating/).

## Related projects

- **[APIs.json](https://apisjson.org)** ([github.com/apis-json](https://github.com/apis-json)) — the machine-readable API discovery format this network is built on
- **[API Commons](https://apicommons.org)** ([github.com/api-commons](https://github.com/api-commons)) — the standard vocabulary of common API operational properties (plans, rate limits, etc.)
- **[api-evangelist](https://github.com/api-evangelist)** — the upstream provider profile repos this network is built from

## Support

APIs.io, [APIs.json](https://apisjson.org), and [API Commons](https://apicommons.org) are projects led by **Kin Lane** and **Steve Willmott** — open infrastructure for the next generation of API discovery. Email [info@apievangelist.com](mailto:info@apievangelist.com) for site-related questions, or open issues at [github.com/apis-json](https://github.com/apis-json) and [github.com/api-commons](https://github.com/api-commons) for spec-level questions.

The catalog is licensed for public use including search indexing, AI grounding / RAG, and model training — see [apis.io/terms/](https://apis.io/terms/).
