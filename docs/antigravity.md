# Commercializer in Antigravity (and Gemini CLI)

Antigravity (the IDE and the `agy` CLI) replaced Gemini CLI on 18 June 2026. Both connect to Commercializer the same
way.

## Before you start

- A Commercializer account and a workspace with your company set up.

## Connect

### Antigravity CLI and IDE

Add the server to `mcp_config.json`: globally `~/.gemini/config/mcp_config.json`, or `.agents/mcp_config.json` in a
workspace. In the CLI, `/mcp` opens the MCP manager and shows the file it uses.

```json
{
  "mcpServers": {
    "commercializer": {
      "serverUrl": "https://commercializer.ai/mcp"
    }
  }
}
```

The key is `serverUrl`: with `url` or `httpUrl` Antigravity loads no tools and shows no error.

### Gemini CLI (until you move)

```sh
gemini mcp add --transport http commercializer https://commercializer.ai/mcp
```

or in `~/.gemini/settings.json`:

```json
{ "mcpServers": { "commercializer": { "httpUrl": "https://commercializer.ai/mcp" } } }
```

## Sign in

Antigravity and Gemini CLI find Commercializer's sign-in on their own. In the CLI, `/mcp auth commercializer` (Gemini) or
the MCP manager's **Authenticate** (Antigravity) opens commercializer.ai: sign in, choose the workspace and press
**Allow**.

## Check it works

`/mcp` lists **commercializer** as connected with its tools. Ask *Using Commercializer, what does my workspace hold about
our company?*

## With an API key instead

```json
{
  "mcpServers": {
    "commercializer": {
      "serverUrl": "https://commercializer.ai/mcp",
      "headers": { "Authorization": "Bearer czk_…" }
    }
  }
}
```

(Gemini CLI: `gemini mcp add --transport http -H "Authorization: Bearer czk_…" commercializer https://commercializer.ai/mcp`.)
See [API keys](api-keys.md).

## Disconnect

Remove the block from `mcp_config.json` (or `gemini mcp remove commercializer`), and **Disconnect** it on the **MCP** page
of Commercializer.

## Troubleshooting

- **No tools and no error:** the entry uses `url` or `httpUrl`; Antigravity needs `serverUrl`.
- **Sign-in on a remote machine:** OAuth needs a browser that can reach `localhost` on the machine running the CLI; use an
  API key there.
- More in [Troubleshooting](troubleshooting.md).
