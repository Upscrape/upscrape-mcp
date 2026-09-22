# Security

## Reporting a vulnerability

Email **founders@upscrape.com** with "Security" in the subject line. Include a
description of the issue, the steps to reproduce it and the affected URL or
tool. Please do not open a public issue for a security problem.

We acknowledge reports within two business days and keep you informed until the
issue is resolved.

## Scope

- The MCP server at `https://data.upscrape.com/mcp`
- OAuth authorization at `https://app.upscrape.com`
- The configuration files in this repository

## How the server protects your account

- OAuth 2.1 with PKCE; access tokens are bound to the MCP resource and can be
  revoked at any time.
- A connection can be restricted to selected platforms, or to read-only use,
  on the consent page.
- Results come from third-party websites and are marked as untrusted content.
  Treat them as data, never as instructions.

See [MCP security](https://docs.upscrape.com/docs/mcp/security) for details.
