# Commercializer in Codex

Add Commercializer to Codex (the CLI, the IDE extension and the Codex app share one configuration), sign in once, and
Codex can read the registers for your company.

## Before you start

- A Commercializer account and a workspace with your company set up.
- Codex, recent (`codex --version`).

## Connect

### The server

```sh
codex mcp add commercializer --url https://commercializer.ai/mcp
codex mcp login commercializer
```

`login` opens your browser on commercializer.ai: sign in, choose the workspace and press **Allow**. Codex keeps the
tokens and refreshes them.

### Or the plugin (server and skills)

```sh
codex plugin marketplace add Commercializer-ai/commercializer
```

then in Codex open **/plugins**, choose the **Commercializer** marketplace and **Install** the plugin; sign in when it
asks.

### Or by hand

`~/.codex/config.toml` (or `.codex/config.toml` in a trusted project):

```toml
[mcp_servers.commercializer]
url = "https://commercializer.ai/mcp"
```

then `codex mcp login commercializer`.

### In the IDE extension

Gear menu → **MCP servers → Add server**: name `commercializer`, **Streamable HTTP**, URL
`https://commercializer.ai/mcp`, **Save**, **Restart extension**, then **Authenticate**.

## Check it works

```sh
codex mcp list
```

shows `commercializer` with its status. In a session, ask *Using Commercializer, what does my workspace hold about our
company?*

## With an API key instead

```toml
[mcp_servers.commercializer]
url = "https://commercializer.ai/mcp"
bearer_token_env_var = "COMMERCIALIZER_KEY"
```

and `export COMMERCIALIZER_KEY=czk_…` before starting Codex. See [API keys](api-keys.md).

## Disconnect

```sh
codex mcp logout commercializer
codex mcp remove commercializer
```

and **Disconnect** it on the **MCP** page of Commercializer.

## Troubleshooting

- **`login` cannot open a browser (SSH):** copy the address it prints into a browser on your own machine; or use an API
  key.
- More in [Troubleshooting](troubleshooting.md).
