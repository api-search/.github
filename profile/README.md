# APIs.io — Federated API Search Network

[**APIs.io**](https://apis.io) is a federated, agent-friendly API discovery network. It indexes the public surface of API providers across the internet — their APIs, capabilities, schemas, event-driven specs, governance rules, vocabularies, and JSON-LD contexts — and exposes each slice of metadata at its own subdomain. Each site is a separate Jekyll deploy on GitHub Pages, all sharing the same upstream provider catalog.

## The Network

| Site | Repo | What it indexes |
|---|---|---|
| [apis.io](https://apis.io) | [network](https://github.com/api-search/network) | Search hub, blog, build pipeline |
| [developer.apis.io](https://developer.apis.io) | [portal](https://github.com/api-search/portal) | Developer portal & feeds |
| [providers.apis.io](https://providers.apis.io) | [providers](https://github.com/api-search/providers) | API provider profiles |
| [apis.apis.io](https://apis.apis.io) | [apis](https://github.com/api-search/apis) | Individual API records |
| [capabilities.apis.io](https://capabilities.apis.io) | [capabilities](https://github.com/api-search/capabilities) | Naftiko capability specs |
| [schemas.apis.io](https://schemas.apis.io) | [schemas](https://github.com/api-search/schemas) | JSON Schemas |
| [asyncapi.apis.io](https://asyncapi.apis.io) | [asyncapi](https://github.com/api-search/asyncapi) | AsyncAPI event-driven specs |
| [json-ld.apis.io](https://json-ld.apis.io) | [json-ld](https://github.com/api-search/json-ld) | JSON-LD contexts |
| [rules.apis.io](https://rules.apis.io) | [rules](https://github.com/api-search/rules) | Spectral governance rulesets |
| [vocabularies.apis.io](https://vocabularies.apis.io) | [vocabularies](https://github.com/api-search/vocabularies) | Provider vocabularies |
| [tags.apis.io](https://tags.apis.io) | [tags](https://github.com/api-search/tags) | API tag index |
| [examples.apis.io](https://examples.apis.io) | [examples](https://github.com/api-search/examples) | API usage examples |

## How it works

The [network](https://github.com/api-search/network) repo is the build hub. Its [`scripts/build.py`](https://github.com/api-search/network/blob/main/scripts/build.py) reads from the [api-evangelist](https://github.com/api-evangelist) provider repos — Git-versioned APIs.json profiles, one per provider — and emits Jekyll collections into every other site repo above. Each site then renders independently from its own collection.

Topical search nodes (e.g. `payments-node`, `healthcare-node`, `weather-node`, `us-federal-government-node`) are vertical slices of the same catalog, scoped to a domain.

## Backing services

A set of headless service repos backs the search and admin surfaces:

- [apis-io-engine](https://github.com/api-search/apis-io-engine), [apis-io-search](https://github.com/api-search/apis-io-search), [apis-io-publishing](https://github.com/api-search/apis-io-publishing)
- [apis-io-ratings](https://github.com/api-search/apis-io-ratings), [apis-io-linter](https://github.com/api-search/apis-io-linter), [apis-io-rules](https://github.com/api-search/apis-io-rules)
- [apis-io-properties](https://github.com/api-search/apis-io-properties), [apis-io-tags](https://github.com/api-search/apis-io-tags)
- [apis-io-maintainers](https://github.com/api-search/apis-io-maintainers), [apis-io-authentication](https://github.com/api-search/apis-io-authentication)

## Related projects

- [APIs.json](https://apisjson.org) ([github.com/apis-json](https://github.com/apis-json)) — the machine-readable specification this network is built on
- [API Commons](https://apicommons.org) ([github.com/api-commons](https://github.com/api-commons)) — the standard vocabulary of common API operational properties
- [Naftiko](https://github.com/naftiko/framework) — the open-source framework that runs capability specs as REST, MCP, and Agent Skill surfaces
- [api-evangelist](https://github.com/api-evangelist) — the upstream provider profile repos this network is built from

## Support

APIs.io, [APIs.json](https://apisjson.org), and [API Commons](https://apicommons.org) are projects led by Kin Lane and Steve Willmott — open infrastructure for the next generation of API discovery. Open issues on the relevant site repo for site-specific questions, on [github.com/apis-json](https://github.com/apis-json) for spec questions, or email [info@apievangelist.com](mailto:info@apievangelist.com).
