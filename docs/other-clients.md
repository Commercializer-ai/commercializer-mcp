# Commercializer in other MCP clients

Any client that speaks the Model Context Protocol over Streamable HTTP connects to
`https://commercializer.ai/mcp` and signs in with OAuth 2.1: it finds the sign-in through the server's metadata,
registers itself (or brings a client metadata document) and opens commercializer.ai for you to approve. A client that
cannot sign in uses an API key in the `Authorization` header.

| Client | Configuration | Sign in |
| --- | --- | --- |
| **Devin Desktop** (formerly Windsurf) | `~/.config/devin/mcp_config.json` (Windows `%APPDATA%\devin\mcp_config.json`): `{"mcpServers": {"commercializer": {"serverUrl": "https://commercializer.ai/mcp"}}}` | Cascade → MCP servers → **Authenticate** |
| **Kiro** | `~/.kiro/settings/mcp.json` or `.kiro/settings/mcp.json`: `{"mcpServers": {"commercializer": {"url": "https://commercializer.ai/mcp"}}}` | when Kiro first connects |
| **Zed** | `settings.json`: `"context_servers": {"commercializer": {"url": "https://commercializer.ai/mcp"}}` | Agent panel → server → **Authenticate** |
| **Goose** | `goose configure` → **Add extension → Remote extension (Streamable HTTP)** → `https://commercializer.ai/mcp` | when Goose first connects |
| **LM Studio, Raycast, others** | their MCP settings, server URL `https://commercializer.ai/mcp`, type HTTP / Streamable HTTP | as the client offers; else an API key |

## A client that runs only local (stdio) servers

Bridge it with [`mcp-remote`](https://www.npmjs.com/package/mcp-remote), which signs in for it:

```json
{
  "mcpServers": {
    "commercializer": {
      "command": "npx",
      "args": ["-y", "mcp-remote@latest", "https://commercializer.ai/mcp"]
    }
  }
}
```

The first start opens commercializer.ai in your browser to sign in and approve.

## With an API key

Most clients take headers beside the URL:

```json
{
  "mcpServers": {
    "commercializer": {
      "url": "https://commercializer.ai/mcp",
      "headers": { "Authorization": "Bearer czk_…" }
    }
  }
}
```

With `mcp-remote`, add `"--header", "Authorization: Bearer ${COMMERCIALIZER_KEY}"` to the arguments and set
`COMMERCIALIZER_KEY` in `env`. See [API keys](api-keys.md).

## For client developers

| | |
| --- | --- |
| Transport | Streamable HTTP, `POST https://commercializer.ai/mcp`, JSON answers; no server stream and no session (`GET` is 405) |
| Protocol versions | `2025-11-25`, `2025-06-18`, `2025-03-26` |
| Protected resource metadata | `https://commercializer.ai/.well-known/oauth-protected-resource` (also named in the 401's `WWW-Authenticate`) |
| Authorization server metadata | `https://commercializer.ai/.well-known/oauth-authorization-server` |
| Registration | dynamic (`POST /oauth/register`) or a client ID metadata document (an `https` client ID) |
| Grant | authorization code with PKCE S256; refresh tokens rotate on use; access tokens last an hour, refresh tokens thirty days |
| Scope | `commercializer` (`offline_access` accepted) |
| Client authentication | none (public clients); a client ID sent by HTTP Basic is accepted |
| Redirects | `https`, loopback `http` on any port, or an app scheme |
