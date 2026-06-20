# APIs.io

This is the GitHub organization for [**APIs.io**](https://apis.io) — a federated, agent-friendly directory of public-internet APIs.

The organization README shown on [github.com/api-search](https://github.com/api-search) lives in [`profile/README.md`](profile/README.md) and documents the full public network: the path-namespaced catalogs, the search API and MCP server, the RFC 9727 `api-catalog` linkset, and the `llms.txt` agent feeds.

**The whole network is served from a single origin** — one S3 + CloudFront distribution on `apis.io`. This org holds only the build pipeline ([`network`](https://github.com/api-search/network)); each catalog is built from the upstream [api-evangelist](https://github.com/api-evangelist) provider repos and synced into the apex site. Legacy per-subdomain hosts (`providers.apis.io`, …) now `301`-redirect to their apex paths. The network is consumed entirely through its public infrastructure:

- **[apis.io](https://apis.io)** — the search-and-discovery hub for the whole network
- Per-entity catalogs — [providers](https://apis.io/providers/), [apis](https://apis.io/apis/), [schemas](https://apis.io/schemas/), [collections](https://apis.io/collections/), [asyncapi](https://apis.io/asyncapis/), [graphql](https://apis.io/graphqls/), [events](https://apis.io/channels/), [arazzo](https://apis.io/arazzos/), [json-ld](https://apis.io/jsonld/), [rules](https://apis.io/rules/), [vocabularies](https://apis.io/vocabularies/), [examples](https://apis.io/examples/)
- Discovery dimensions — [tags](https://apis.io/tags/), [industries](https://apis.io/industries/), [regions](https://apis.io/regions/)
- Agent surfaces — [skills](https://apis.io/skills/), [mcp](https://apis.io/servers/)
- Commercial & operational — [plans](https://apis.io/plans/), [rate-limits](https://apis.io/rate-limits/), [finops](https://apis.io/finops/)
- Programmatic access — the [search API](https://apis.io/api/v1) and [MCP server](https://apis.io/mcp) (metered & tiered; see [apis.io/developer](https://apis.io/developer))

The site publishes `llms.txt`, `sitemap.xml`, RFC 9727 `api-catalog`, and (where relevant) `search-index.json`. Start at [apis.io/.well-known/api-catalog](https://apis.io/.well-known/api-catalog) or [apis.io/llms.txt](https://apis.io/llms.txt).

The catalog is licensed for public use including search indexing, AI grounding / RAG, and model training — see [apis.io/terms/](https://apis.io/terms/).

Questions or issues: open an issue on this repo, or email [info@apievangelist.com](mailto:info@apievangelist.com).
