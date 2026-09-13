---
tags:
  - gen_ai
  - gen_ai/agents
created: 2026-07-31T10:23
modified: 2026-09-06T11:49
published:
sources:
  - "[x402 Bazaar — CDP Discovery Endpoints](https://docs.cdp.coinbase.com/x402/bazaar)"
topics:
  - Service Discovery
  - x402
  - Semantic Search
authors:
  - Opus 4.8
ai-assisted: true
hidden: false
public: true
human-review: true
banner: https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRSkVlstDH194TA9THB9DO84SQbG1dUYIiE2YLJ1kTLE_uevVxmRkkAg9c&s=10
---
# x402 Bazaar
- Bazaar discovery endpoints let developers and AI agents browse and search for x402-enabled services that are cataloged through the [CDP Facilitator](https://docs.cdp.coinbase.com/x402/core-concepts/facilitator). 
- The Bazaar indexes payable API endpoints with semantic descriptions, payment metadata, and trust signals derived from on-chain activity
- [[Introducing Agentic.Market]] ([Link](https://www.coinbase.com/developer-platform/discover/launches/agentic-market))
	- https://agentic.market/
	- Coinbase's public directory of x402 services
	- Shows subset of what is listed on the Bazaar
### Access modes
- **Paginated catalog (HTTP)** (`GET /v2/x402/discovery/resources`) — inventory-style browsing with `limit` and `offset`
- **Semantic search (HTTP)** (`GET /v2/x402/discovery/search`) — same CDP index as the catalog, optimized for query, filters, and [quality ranking](#quality-ranking), not for walking the full catalog
- **MCP Server** (`GET /v2/x402/discovery/mcp`) — for AI agents via Model Context Protocol .
## How it works
- In x402 v2, the Bazaar has been codified as an official extension in the reference SDK (`@x402/extensions/bazaar`). This extension enables:
	- **When does my endpoint appear?** There is no separate registration step. The CDP Facilitator catalogs your service the first time it **settles** a payment for that endpoint (the usual client flow is verify then settle; indexing happens when settlement succeeds). 
	- **Staying visible — 30-day rolling window:** All endpoints apply a recency filter. Resources that have been called at least once but have had no activity in the last 30 days are excluded from results. Newly indexed resources with no calls yet are not subject to this filter.
## Curated endpoints
Some resources in the Bazaar are **Coinbase-curated**: they have passed a partner-admission and verification bar on top of the automatic indexing every Bazaar-enabled route gets. Curation is a trust and quality signal — it does not change how you integrate as a buyer or seller, it changes how a resource surfaces.


