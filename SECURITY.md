# Security Policy

## Reporting a vulnerability

If you believe you have found a security vulnerability in any HTAG MCP server or in this metadata repository, please report it privately.

**Email:** copilot@htag.com.au

Please include:
- A description of the issue and its potential impact.
- Steps to reproduce, proof-of-concept, or relevant logs (with secrets redacted).
- Your contact details so we can follow up.

We aim to acknowledge reports promptly and will coordinate a disclosure timeline with you once the issue is triaged.

## Do not open public issues with secrets

Do **not** include API keys, OAuth client secrets, access tokens, personal data, or any other sensitive material in public GitHub issues, pull requests, or discussions on this repository. If a secret has been exposed:

1. Rotate the credential immediately via the [HTAG Developer Portal](https://developer.htagai.com).
2. Email copilot@htag.com.au with the details.

## Scope

This repository contains **public metadata only** - server descriptors, install guides, and the public server card. Source code for the MCP servers themselves is not in scope here; vulnerabilities affecting HTAG's production MCP endpoints should be reported via the same email address above.
