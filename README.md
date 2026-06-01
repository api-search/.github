# APIs.io

This is the GitHub organization for [**APIs.io**](https://apis.io) — a federated, agent-friendly directory of public-internet APIs.

The organization README shown on [github.com/api-search](https://github.com/api-search) lives in [`profile/README.md`](profile/README.md) and documents the full public network: the per-subdomain sites, the RFC 9727 `api-catalog` linkset, and the `llms.txt` agent feeds.

**The repos in this organization are private.** The network is consumed entirely through its public infrastructure:

- **[apis.io](https://apis.io)** — the search-and-discovery hub for the whole network
- Per-entity subdomains — [providers](https://providers.apis.io), [apis](https://apis.apis.io), [schemas](https://schemas.apis.io), [asyncapi](https://asyncapi.apis.io), [events](https://events.apis.io), [json-ld](https://json-ld.apis.io), [rules](https://rules.apis.io), [vocabularies](https://vocabularies.apis.io), [examples](https://examples.apis.io)
- Discovery dimensions — [tags](https://tags.apis.io), [industries](https://industries.apis.io), [regions](https://regions.apis.io)
- Agent surfaces — [skills](https://skills.apis.io), [mcp](https://mcp.apis.io)
- Commercial & operational — [plans](https://plans.apis.io), [rate-limits](https://rate-limits.apis.io), [finops](https://finops.apis.io)

Each site publishes its own `llms.txt`, `sitemap.xml`, RFC 9727 `api-catalog`, and (where relevant) `search-index.json`. Start at [apis.io/.well-known/api-catalog](https://apis.io/.well-known/api-catalog) or [apis.io/llms.txt](https://apis.io/llms.txt).

The catalog is licensed for public use including search indexing, AI grounding / RAG, and model training — see [apis.io/terms/](https://apis.io/terms/).

Questions or issues: open an issue on this repo, or email [info@apievangelist.com](mailto:info@apievangelist.com).
