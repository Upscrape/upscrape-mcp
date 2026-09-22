# Upscrape MCP server

<!-- mcp-name: com.upscrape/mcp -->

Real-time data APIs for 50+ commerce, grocery, social and maps platforms, over
one remote MCP server. AI clients such as Claude, ChatGPT, Cursor, VS Code,
Codex and Gemini CLI connect with OAuth and get structured JSON from the live
source.

This repository holds connection instructions and the registry description.
The server itself is hosted by Upscrape; there is nothing to install or run.

| | |
|---|---|
| Server URL | `https://data.upscrape.com/mcp` |
| Transport | Streamable HTTP (remote) |
| Authentication | OAuth 2.1 with PKCE and dynamic client registration, or an API key as a bearer token |
| MCP Registry name | [`com.upscrape/mcp`](https://registry.modelcontextprotocol.io/v0/servers?search=upscrape) |
| Documentation | [docs.upscrape.com/docs/mcp/overview](https://docs.upscrape.com/docs/mcp/overview) |
| Catalog | [upscrape.com/scrapers](https://upscrape.com/scrapers) |

## Connect

Add the server URL to your client and sign in to Upscrape when the browser
opens. No API key is needed with OAuth. You can also generate a configuration
for your client at [Connect MCP](https://app.upscrape.com/app/mcp).

### Claude and ChatGPT

Add a custom connector with this URL and sign in:

```text
https://data.upscrape.com/mcp
```

### Claude Code

```bash
claude mcp add --transport http upscrape https://data.upscrape.com/mcp
```

Then open `/mcp` in Claude Code and authenticate.

### Cursor

This repository is also a Cursor plugin ([manifest](.cursor-plugin/plugin.json)).
To configure it by hand, add to your MCP configuration
([example](examples/cursor-mcp.json)):

```json
{
  "mcpServers": {
    "upscrape": {
      "url": "https://data.upscrape.com/mcp"
    }
  }
}
```

### VS Code

Save as `.vscode/mcp.json`, start the server and authenticate
([example](examples/vscode-mcp.json)):

```json
{
  "servers": {
    "upscrape": {
      "type": "http",
      "url": "https://data.upscrape.com/mcp"
    }
  }
}
```

### Codex

Add to your Codex configuration, then run `codex mcp login upscrape`
([example](examples/codex-config.toml)):

```toml
[mcp_servers.upscrape]
url = "https://data.upscrape.com/mcp"
```

### Gemini CLI

Add to `settings.json`, then run `/mcp auth upscrape`
([example](examples/gemini-settings.json)):

```json
{
  "mcpServers": {
    "upscrape": {
      "httpUrl": "https://data.upscrape.com/mcp"
    }
  }
}
```

### API key instead of OAuth

Clients that accept a bearer token can use an Upscrape API key. See
[API key setup](https://docs.upscrape.com/docs/mcp/api-key).

## Tools

The default connection exposes four tools:

| Tool | What it does | Cost |
|---|---|---|
| `upscrape_search_capabilities` | Finds capabilities by task, platform, URL or category. Top matches include their input schema | Free |
| `upscrape_describe_capability` | Returns a capability's exact input schema, example input, timeout and price | Free |
| `upscrape_execute` | Runs one capability. Supports a credit ceiling (`max_credits`) and safe retries (`operation_key`) | The capability's published price, charged only when the job succeeds |
| `upscrape_get_job_result` | Retrieves a job started earlier, including large results in chunks | Free |

Every tool carries read-only and destructive hints. No tool is destructive.

To expose specific platforms or capabilities as their own named tools, add them
to the URL, for example `https://data.upscrape.com/mcp?platforms=blinkit`. See
[tool pinning](https://docs.upscrape.com/docs/mcp/pinning) and
[tools](https://docs.upscrape.com/docs/mcp/tools).

## Pricing

Prepaid credits, fixed price per request, no subscription. Each capability
publishes its price. Failed requests are not charged and purchased credits do
not expire. New accounts get up to 100 free credits to start. See
[pricing](https://upscrape.com/pricing).

## Security

- Access tokens are bound to the MCP resource and can be revoked at any time.
- The consent page can restrict a connection to selected platforms or disable
  execution. See [scoped access](https://docs.upscrape.com/docs/mcp/scoped-access).
- Results come from third-party websites. Treat them as data, never as
  instructions. See [security](https://docs.upscrape.com/docs/mcp/security).

Upscrape is not affiliated with the platforms in its catalog. Platform names
are trademarks of their respective owners.

## Support

Email [founders@upscrape.com](mailto:founders@upscrape.com) or open an issue in
this repository.
