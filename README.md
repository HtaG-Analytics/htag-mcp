# HTAG Property Intelligence MCP

Public metadata for HTAG's Model Context Protocol (MCP) servers. This repository describes the publicly available HTAG MCP connectors - **70+ read-only public tools** across three connectors - so they can be discovered, evaluated, and configured by AI clients, MCP directories, and integration partners.

<p align="left">
  <img src="assets/htag_logo_blue.svg" alt="HTAG" height="48" />
</p>

---

## Assumptions & Gaps

- **Public-only scope.** This repo documents the three connectors that are safe to expose externally (Intelligence, Spatial, Docs). Internal connectors (Trends, Data Analytics) are intentionally omitted.
- **No source code.** This is a metadata repository. Server implementations, schemas for every tool, and operational details are not published here.
- **Auth setup happens elsewhere.** API keys and OAuth 2.0 clients are provisioned via the HTAG Developer Portal - not in this repo and not in MCP client config files committed to source control.
- **Tool counts are current as of publication.** Live tool inventories are authoritative via each server's `tools/list` response and the [API reference](https://developer.htagai.com/api-reference).

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

- **OAuth 2.0** - recommended for end-user / interactive agents. Configure via the [Developer Portal](https://developer.htagai.com).
- **`x-api-key` header** - for server-to-server / headless agents. Issue keys from the Developer Portal and pass as a request header.
- **Public** - HTAG Docs requires no credentials.

Never commit API keys to client config files in source control. Store them in your client's secrets store or environment variables.

---

## Data Handling

- All connectors are **read-only**. No HTAG data is mutated by these MCP servers.
- Requests and responses traverse HTTPS only.
- API keys identify the caller for rate limiting, quota, and audit; rotate keys via the Developer Portal.
- For terms covering acceptable use, data retention, and redistribution of property data, see the Developer Portal.

---

## Not Included in This Public Listing

- **HTAG Trends** and **HTAG Data Analytics** are internal connectors and are not part of this public MCP listing.
- Per-tool input/output schemas - see live `tools/list` responses or the [API reference](https://developer.htagai.com/api-reference).
- Internal routing, infrastructure, and implementation details.

---

## Links

- Developer Portal - https://developer.htagai.com
- MCP setup hub - https://developer.htagai.com/agents-mcp
- API reference - https://developer.htagai.com/api-reference
- Support - copilot@htag.com.au
- Security disclosures - see [SECURITY.md](SECURITY.md)

---

## License

[MIT](LICENSE) (c) HTAG Analytics
