# HTAG Property Intelligence MCP

HTAG Property Intelligence MCP gives AI agents read-only access to Australian property intelligence: address standardisation, property summaries and estimates, sold/rented listing search, suburb/LGA market metrics, demographics, economics, geographic concordance, and H3 spatial layers.

This repository publishes the metadata for HTAG's public Model Context Protocol (MCP) servers - **70+ read-only public tools** across three connectors - so they can be discovered, evaluated, and configured by AI clients, MCP directories, and integration partners.

<p align="left">
  <img src="assets/htag_logo_blue.svg" alt="HTAG" height="48" />
</p>

---

## What agents can do with this

- **Standardise and enrich an address.** Resolve free-text Australian addresses to canonical form, then pull property summary, demographics, and environment for that location.
- **Estimate value and rent.** Get current price and rent estimates for a property, plus market context (growth, scores, trends) for its suburb or LGA.
- **Search comparable sales and rentals.** Query sold and rented listings filtered by location, attributes, and time window to support comps and rental benchmarking.
- **Profile a suburb, LGA, or postcode.** Combine market metrics, demographics, census medians, and economic indicators (CPI, cash rate) for a single locality view.
- **Reason over spatial layers.** Pull H3 hex-indexed price/rent/yield surfaces, socio-environmental indicators, and risk layers; convert between H3 cells and administrative boundaries.
- **Discover capabilities at runtime.** List available MCP servers, tools, REST endpoints, and micro-agents via the public Docs connector - no credentials required.

---

## Connectors

| Connector | Registry name | Endpoint | Tools | Auth |
|---|---|---|---|---|
| HTAG Intelligence | `com.htagai/htag-intelligence` | `https://api.htagai.com/mcp/v1/servers/htag/mcp` | 59 read-only | OAuth 2.0 or `x-api-key` |
| HTAG Spatial | `com.htagai/htag-spatial` | `https://api.htagai.com/mcp/v1/servers/htag-spatial/mcp` | 6 read-only | OAuth 2.0 or `x-api-key` |
| HTAG Docs | `com.htagai/htag-docs` | `https://api.htagai.com/mcp/v1/servers/htag-docs/mcp` | 5 read-only | Public (no auth) |

All connectors use **Streamable HTTP** transport.

### HTAG Intelligence
Read-only property intelligence tools covering address standardisation, property summaries and estimates, sold/rented listing search, suburb and LGA market metrics, market trends, demographics, economics, and geographic concordance across HTAG's property dataset.

### HTAG Spatial
Read-only H3 spatial tools for hex-indexed price, rent and yield surfaces, socio-environmental indicators, risk layers, H3 geometry and resolution utilities, and H3-to-administrative concordance.

### HTAG Docs
Public capability-discovery connector for listing HTAG MCP servers and their tools, REST API endpoints and OpenAPI operations, and micro-agents. No authentication required.

---

## Endpoints

All endpoints accept MCP requests over HTTPS using Streamable HTTP:

```
https://api.htagai.com/mcp/v1/servers/htag/mcp
https://api.htagai.com/mcp/v1/servers/htag-spatial/mcp
https://api.htagai.com/mcp/v1/servers/htag-docs/mcp
```

---

## Authentication

- **OAuth 2.0** - recommended for end-user / interactive agents. Authorization server metadata is discovered directly from each MCP URL; clients that support Dynamic Client Registration with authorization-code + PKCE can sign the user in without any pre-created OAuth client or API key.
- **`x-api-key` header** - optional alternate for server-to-server / headless agents. Issue keys from the [Developer Portal](https://developer.htagai.com) and pass as a request header.
- **Public** - HTAG Docs requires no credentials.

Never commit API keys to client config files in source control. Store them in your client's secrets store or environment variables.

---

## Scope & Security

- **Public-only scope.** This repo documents the three connectors that are safe to expose externally (Intelligence, Spatial, Docs). Internal / non-public connectors are intentionally omitted from this listing.
- **Read-only.** All connectors are read-only; no HTAG data is mutated by these MCP servers.
- **HTTPS only.** Requests and responses traverse HTTPS only.
- **No pre-provisioning for interactive clients.** OAuth 2.0 metadata is discovered directly from the MCP URL and supports Dynamic Client Registration with authorization-code + PKCE, so MCP-capable clients can complete sign-in without a pre-created OAuth client or API key. API keys remain an optional alternate for headless use and are issued from the HTAG Developer Portal; never commit them to MCP client config in source control.
- **Metadata only.** This is a metadata repository - no server source code, per-tool schemas, or operational details are published here. Live tool inventories are authoritative via each server's `tools/list` response and the [API reference](https://developer.htagai.com/api-reference).
- **Identity and audit.** API keys identify the caller for rate limiting, quota, and audit; rotate keys via the Developer Portal.
- **Terms.** For acceptable use, data retention, and redistribution of property data, see the Developer Portal.

---

## Not Included in This Public Listing

- Internal / non-public HTAG connectors.
- Per-tool input/output schemas - see live `tools/list` responses or the [API reference](https://developer.htagai.com/api-reference).
- Internal routing, infrastructure, and implementation details.

---

## Links

- Developer Portal - https://developer.htagai.com
- MCP setup hub - https://developer.htagai.com/agents-mcp
- API reference - https://developer.htagai.com/api-reference
- Support - [copilot@htag.com.au](mailto:copilot@htag.com.au)
- Security disclosures - see [SECURITY.md](SECURITY.md)

---

## License

[MIT](LICENSE) (c) HTAG Analytics
