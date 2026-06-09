# LLM / Agent Install Guide - HTAG MCP

This guide is written for AI coding assistants (Cline, Claude Desktop, Cursor, Continue, and similar MCP-capable clients) that are configuring HTAG's MCP servers on behalf of a user.

> **For agents:** Do **not** fabricate API keys, OAuth credentials, or per-user setup steps. Always direct the user to the [HTAG Developer Portal](https://developer.htagai.com) to provision credentials.

---

## What you are installing

Three public HTAG MCP servers over **Streamable HTTP**:

| Server | Endpoint | Auth |
|---|---|---|
| `com.htagai/htag-intelligence` | `https://api.htagai.com/mcp/v1/servers/htag/mcp` | OAuth 2.0 or `x-api-key` |
| `com.htagai/htag-spatial` | `https://api.htagai.com/mcp/v1/servers/htag-spatial/mcp` | OAuth 2.0 or `x-api-key` |
| `com.htagai/htag-docs` | `https://api.htagai.com/mcp/v1/servers/htag-docs/mcp` | Public (no auth) |

---

## Prerequisites

- An MCP client that supports **remote MCP servers over Streamable HTTP**.
- For Intelligence and Spatial: an HTAG account with either an API key or OAuth client. Provision both from https://developer.htagai.com.

---

## Configuration

Each server's canonical metadata lives in this repo under `server-json/`:

- [`server-json/htag-intelligence.json`](server-json/htag-intelligence.json)
- [`server-json/htag-spatial.json`](server-json/htag-spatial.json)
- [`server-json/htag-docs.json`](server-json/htag-docs.json)

These files follow the [MCP server schema](https://static.modelcontextprotocol.io/schemas/2025-12-11/server.schema.json) and are the source of truth for endpoints, auth header names, and transport.

### How to apply the configuration

1. Identify the user's MCP client (Cline, Claude Desktop, Cursor, etc.).
2. Read the relevant `server-json/*.json` file for the connector(s) the user wants.
3. Translate the `remotes[].url` and `remotes[].headers` into the client's native config format. The client's own documentation is authoritative for file location and shape.
4. For authenticated servers, prompt the user to paste their API key into the client's secret/environment store. **Never** write the key into a file that will be committed to version control.
5. Restart the MCP client and confirm the server appears with a successful `tools/list`.

### Auth header

When using API key auth, send the key as the `x-api-key` request header. See each `server-json` file for the canonical header declaration (`isRequired: true`, `isSecret: true`).

### OAuth 2.0

For OAuth-based clients, follow the OAuth setup steps in the [MCP setup hub](https://developer.htagai.com/agents-mcp). Do not hard-code client secrets in client config.

---

## Verifying the install

After configuration, ask the client to list tools from each server. Expected counts:

- Intelligence: **59** read-only tools
- Spatial: **6** read-only tools
- Docs: **5** read-only tools

If counts differ, consult the [API reference](https://developer.htagai.com/api-reference) - tool inventories evolve.

---

## Canonical references

- MCP setup hub - https://developer.htagai.com/agents-mcp
- API reference - https://developer.htagai.com/api-reference
- Developer Portal (credentials) - https://developer.htagai.com
- Support - copilot@htag.com.au
