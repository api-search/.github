# APIs.io — Federated API Search Network

[**APIs.io**](https://apis.io) is a federated, agent-friendly directory of public-internet APIs. It indexes API providers from across the web — their APIs, JSON Schemas, event-driven specifications, governance rules, vocabularies, JSON-LD contexts, pricing plans, rate limits, FinOps profiles, the agent surfaces they publish (Agent Skills and MCP servers), and the industries and regions they serve — and exposes each slice of metadata at its own subdomain.

Every site is a separate Jekyll deploy on GitHub Pages. All share one upstream provider catalog, all carry the same agent-readiness baseline (`llms.txt`, RFC 9727 `api-catalog`, permissive `robots.txt`, schema.org JSON-LD), and all are publicly accessible at the URLs below.

> The repos in this organization are private. **The network is consumed via the public subdomains, the RFC 9727 `api-catalog` linkset, the `llms.txt` / `llms-full.txt` agent feeds, and the per-subdomain sitemaps.** Everything below is open-access content, free to search, ground LLMs against, train on, or republish — see [https://apis.io/terms/](https://apis.io/terms/) for the full terms.

## The network — public sites

### Search & discovery hub

| Site | What you'll find |
|---|---|
| **[apis.io](https://apis.io)** | Search hub for the whole network — search by provider, schema, tag, or name; blog; cross-network insights |
| **[tags.apis.io](https://tags.apis.io)** | Tag index across the network — every provider and API that carries a tag, scored and ranked |
| **[industries.apis.io](https://industries.apis.io)** | 29 industry verticals (Financial Services, Healthcare, Manufacturing, Transportation, Energy, Government, …) |
| **[regions.apis.io](https://regions.apis.io)** | 17 macro sales regions (North America, LATAM, EMEA, APAC, Greater China, ANZ, …) |
| **[developer.apis.io](https://developer.apis.io)** | Developer portal & machine-readable feeds |

### Per-entity catalogs

| Site | What you'll find |
|---|---|
| **[providers.apis.io](https://providers.apis.io)** | API provider profiles — one page per organization, with cross-links to every artifact that organization publishes |
| **[apis.apis.io](https://apis.apis.io)** | Individual API records — one page per published API, with the OpenAPI spec and provider link |
| **[schemas.apis.io](https://schemas.apis.io)** | JSON Schemas extracted from every indexed API — Google Dataset Search ingestion-ready |
| **[collections.apis.io](https://collections.apis.io)** | Postman Collections and Open Collections — ready-to-run request sets for thousands of APIs |
| **[asyncapi.apis.io](https://asyncapi.apis.io)** | AsyncAPI event-driven specifications |
| **[graphql.apis.io](https://graphql.apis.io)** | GraphQL API specifications — endpoint URLs, documentation, and reference links |
| **[events.apis.io](https://events.apis.io)** | Event channels drilled out of every AsyncAPI spec — one page per channel |
| **[arazzo.apis.io](https://arazzo.apis.io)** | Arazzo API workflow specs — provider-specific and cross-provider multi-step workflows |
| **[json-ld.apis.io](https://json-ld.apis.io)** | JSON-LD contexts and semantic vocabularies |
| **[rules.apis.io](https://rules.apis.io)** | Spectral governance rulesets |
| **[vocabularies.apis.io](https://vocabularies.apis.io)** | Provider tag vocabularies powering the advanced search |
| **[examples.apis.io](https://examples.apis.io)** | API usage examples |

### Agent surfaces

| Site | What you'll find |
|---|---|
| **[skills.apis.io](https://skills.apis.io)** | Official Claude Agent Skill index — `SKILL.md` files published by providers, with per-skill and per-provider pages |
| **[mcp.apis.io](https://mcp.apis.io)** | Official Model Context Protocol server index — one page per MCP server, with install hints and source links |

### Commercial & operational surfaces

| Site | What you'll find |
|---|---|
| **[plans.apis.io](https://plans.apis.io)** | API pricing-plan profiles (API Commons Plans format) |
| **[rate-limits.apis.io](https://rate-limits.apis.io)** | API rate-limit profiles (API Commons Rate Limits format) |
| **[finops.apis.io](https://finops.apis.io)** | API FinOps profiles aligned with the FinOps Foundation FOCUS framework |

## Machine-readable feeds

| Feed | URL |
|---|---|
| **RFC 9727 `api-catalog` linkset (full network)** | [apis.io/.well-known/api-catalog](https://apis.io/.well-known/api-catalog) |
| **`api-catalog` (providers slice)** | [providers.apis.io/.well-known/api-catalog](https://providers.apis.io/.well-known/api-catalog) |
| **`api-catalog` (APIs slice)** | [apis.apis.io/.well-known/api-catalog](https://apis.apis.io/.well-known/api-catalog) |
| **`llms.txt` (agent overview, per site)** | [apis.io/llms.txt](https://apis.io/llms.txt) |
| **`llms-full.txt` (dense reference)** | [apis.io/llms-full.txt](https://apis.io/llms-full.txt) |
| **Sitemap index (all subdomains)** | [apis.io/sitemap_index.xml](https://apis.io/sitemap_index.xml) |
| **APIs.json self-description** | [apis.io/apis.json](https://apis.io/apis.json) |

Each subdomain publishes its own `llms.txt`, `sitemap.xml`, and (where relevant) `search-index.json` for client-side search.

## How it works

A central build pipeline reads from a set of upstream provider repos at [github.com/api-evangelist](https://github.com/api-evangelist) — Git-versioned [APIs.json](https://apisjson.org) profiles, one per provider — and emits Jekyll collections into every subdomain site. Each site then renders independently from its own collection.

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
