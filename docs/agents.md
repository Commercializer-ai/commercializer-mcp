# Connect yourself to Commercializer

This page is written for an AI assistant. If a person gave you this, connect yourself to their Commercializer
workspace, or, where you cannot change your own configuration, give them the exact steps for the client you run in.

## The server

- **URL:** `https://commercializer.ai/mcp`, MCP over Streamable HTTP (`POST`, JSON-RPC, JSON answers; no event stream,
  no session; `GET` answers 405).
- **Sign-in:** OAuth 2.1 with PKCE (S256). An unauthenticated request answers 401 with
  `WWW-Authenticate: Bearer resource_metadata="https://commercializer.ai/.well-known/oauth-protected-resource"`; from there
  the authorization server metadata is `https://commercializer.ai/.well-known/oauth-authorization-server`. Register with
  dynamic client registration (`POST https://commercializer.ai/oauth/register`) or present a client ID metadata document
  (an `https` client ID). Public client, no secret. Scope `commercializer` (`offline_access` accepted). Redirects may be
  `https`, loopback `http` on any port, or an app scheme. The person signs in on commercializer.ai, chooses the workspace
  you reach and presses Allow. Access tokens last an hour; refresh tokens thirty days and rotate on use.
- **Or an API key:** where you cannot open a browser, the person makes a key on the **MCP** page of their workspace on
  commercializer.ai and you send it on every request as `Authorization: Bearer czk_…`.

## By client

| You run in | What to do |
| --- | --- |
| Claude Code | `claude mcp add --transport http commercializer https://commercializer.ai/mcp`, then the person runs `/mcp` and authenticates. Or the plugin: `/plugin marketplace add Commercializer-ai/commercializer-mcp` and `/plugin install commercializer@commercializer`. |
| Claude (claude.ai, desktop) | The person adds it: Customize → Connectors → Add → Add custom connector, URL above, then Connect. |
| ChatGPT | The person adds it: Plugins → Add → Add custom MCP server, URL above, authentication OAuth, then Connect. |
| Codex | `codex mcp add commercializer --url https://commercializer.ai/mcp` then `codex mcp login commercializer`. |
| Cursor | Add `{"mcpServers": {"commercializer": {"url": "https://commercializer.ai/mcp"}}}` to `~/.cursor/mcp.json`, then sign in (Tools & MCP → Needs login, or `cursor-agent mcp login commercializer`). |
| GitHub Copilot (VS Code) | Add `{"servers": {"commercializer": {"type": "http", "url": "https://commercializer.ai/mcp"}}}` to `mcp.json`, or `code --add-mcp '{"name":"commercializer","type":"http","url":"https://commercializer.ai/mcp"}'`; VS Code signs in when a tool first runs. |
| Copilot CLI | `copilot plugin marketplace add Commercializer-ai/commercializer-mcp` then `copilot plugin install commercializer@commercializer`, or `copilot mcp add --transport http commercializer https://commercializer.ai/mcp`. |
| Copilot coding agent | An API key as the repository secret `COPILOT_MCP_COMMERCIALIZER_KEY`, and in Settings → Copilot → MCP servers: `{"mcpServers": {"commercializer": {"type": "http", "url": "https://commercializer.ai/mcp", "headers": {"Authorization": "Bearer $COPILOT_MCP_COMMERCIALIZER_KEY"}, "tools": ["*"]}}}`. |
| Microsoft Copilot Studio | Tools → Add a tool → New tool → Model Context Protocol, URL above, OAuth 2.0 → Dynamic discovery. |
| Antigravity | `{"mcpServers": {"commercializer": {"serverUrl": "https://commercializer.ai/mcp"}}}` in `~/.gemini/config/mcp_config.json` (the key is `serverUrl`). |
| A client that runs only local servers | `npx -y mcp-remote@latest https://commercializer.ai/mcp` as the server command. |
| Your own code | The MCP SDK's Streamable HTTP client with the API key header; or JSON-RPC by hand, `{"jsonrpc":"2.0","id":1,"method":"tools/list"}`. |

## Check it works

Call `get_profile`. It returns the person's company as they described it and the findings kept about it. Greet them with
the company's name. If it answers that the workspace has no primary profile, call `list_profiles` and tell them to set
their company up on commercializer.ai.
