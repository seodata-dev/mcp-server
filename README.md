# seodata.dev MCP server

Keyword search volume, CPC, competition and similar keywords for AI assistants,
in 50+ countries. A remote MCP server: nothing to install, and it works without
an account.

```
https://mcp.seodata.dev/mcp
```

- Transport: Streamable HTTP
- Auth: optional. OAuth 2.1 (PKCE, dynamic client registration, client ID
  metadata documents) or an API key as `Authorization: Bearer sd_live_…`
- Registry: [`dev.seodata/keywords`](https://registry.modelcontextprotocol.io/v0/servers?search=dev.seodata/keywords)
- Docs: [seodata.dev/mcp](https://www.seodata.dev/mcp)

This repository holds the connection configs and registry metadata. The server
itself is hosted by seodata.dev; there is no code to run.

## Connect

**Claude (claude.ai and Desktop).** Settings → Connectors → Add custom
connector. Name it seodata.dev and paste the URL. Claude opens the sign-in page
the first time it needs more than the anonymous limit.

**Claude Code**

```bash
claude mcp add --transport http seodata https://mcp.seodata.dev/mcp
```

Then run `/mcp` inside Claude Code to sign in, or add
`--header "Authorization: Bearer sd_live_…"` to use an API key.

**ChatGPT.** Settings → Apps → Advanced → turn on developer mode. Create an app
with the URL and OAuth as the authentication method.

**Cursor** (`~/.cursor/mcp.json` or `.cursor/mcp.json`)

```json
{ "mcpServers": { "seodata": { "url": "https://mcp.seodata.dev/mcp" } } }
```

**VS Code** (`.vscode/mcp.json`)

```json
{ "servers": { "seodata": { "type": "http", "url": "https://mcp.seodata.dev/mcp" } } }
```

**Codex** (`~/.codex/config.toml`)

```toml
[mcp_servers.seodata]
url = "https://mcp.seodata.dev/mcp"
```

**Gemini CLI**

```bash
gemini extensions install https://github.com/seodata-dev/mcp-server
```

**Other clients.** Add the URL with the Streamable HTTP transport and let the
client run OAuth, or send the API key header. Clients that only accept a URL can
use `https://mcp.seodata.dev/mcp?key=sd_live_…`; keep that URL private.

## Tools

All three are read-only.

| Tool | What it does | Inputs |
|---|---|---|
| `lookup_keyword` | Monthly Google search volume, CPC (USD), competition (0 to 1) and similar keywords with their own volumes, for one keyword in one country | `keyword`, `country` (ISO 3166-1 alpha-2, default `us`) |
| `lookup_keywords` | The same for up to 25 keywords at once; use it to compare or prioritize a list | `keywords` (1 to 25), `country` |
| `get_usage` | The plan this connection uses and the lookups left today and this month | none |

Example `lookup_keyword` result (trimmed):

```json
{
  "keyword": "keyword research",
  "country": "us",
  "found": true,
  "volume": 301000,
  "cpc": 12.73,
  "similar": [
    { "keyword": "keyword research tool", "volume": 12100, "cpc": 15.55 },
    { "keyword": "seo keyword research", "volume": 22200, "cpc": 16.58 }
  ]
}
```

## Limits and pricing

| | Lookups |
|---|---|
| No account | 20 a day |
| Free account | 50 a day, 500 a month |
| Unlimited, $4.99 a month | Unlimited (up to 10,000 new keywords a day) |

One lookup is one keyword in one country. The MCP server and the
[HTTP API](https://www.seodata.dev/docs) share the same key and quota.
[Pricing](https://www.seodata.dev/pricing) ·
[Get a key](https://www.seodata.dev/get-key)

## Support

[hello@seodata.dev](mailto:hello@seodata.dev) ·
[Privacy](https://www.seodata.dev/privacy) ·
[Terms](https://www.seodata.dev/terms)
