# Commercializer in GitHub Copilot

Use Commercializer from Copilot Chat in VS Code, the Copilot CLI, JetBrains IDEs, Visual Studio, Xcode and Eclipse.
For Copilot working on its own on github.com, see [Copilot coding agent](copilot-coding-agent.md).

## Before you start

- A Commercializer account and a workspace with your company set up.
- GitHub Copilot with agent mode. On Copilot Business and Enterprise, your organisation's **MCP servers in Copilot**
  policy must be enabled by an admin.

## VS Code

### One click

[**Add Commercializer to VS Code**](https://vscode.dev/redirect/mcp/install?name=commercializer&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fcommercializer.ai%2Fmcp%22%7D)
opens VS Code and asks to install the server. Choose **Install**.

### Or the plugin (server and skills)

Open the Command Palette, run **Chat: Install Plugin From Source** and enter
`https://github.com/Commercializer-ai/commercializer`. This adds the server and the Commercializer skills (`ask`, `run`,
`workspace`, `setup`).

### Or by hand

Add to `.vscode/mcp.json` in a workspace, or to your user `mcp.json` (Command Palette → **MCP: Open User
Configuration**):

```json
{
  "servers": {
    "commercializer": {
      "type": "http",
      "url": "https://commercializer.ai/mcp"
    }
  }
}
```

### Sign in

VS Code shows **Start** above the server in `mcp.json` (or starts it when you first use a tool). It asks to sign in:
choose **Allow**, your browser opens commercializer.ai, sign in, choose the workspace and press **Allow**.

### Check it works

Open Copilot Chat, switch to **Agent**, open the **tools** picker and make sure **commercializer** is ticked, then ask:

> #commercializer What does my workspace hold about our company?

## Copilot CLI

```sh
copilot plugin marketplace add Commercializer-ai/commercializer
copilot plugin install commercializer@commercializer
```

installs the server and skills. Or just the server:

```sh
copilot mcp add --transport http commercializer https://commercializer.ai/mcp
```

Then in `copilot`, run `/mcp` and sign in to **commercializer** when it asks. Plugins installed with the CLI also show in
VS Code under **Agent Plugins**. Update with `copilot plugin update commercializer`; remove with
`copilot plugin uninstall commercializer`.

## JetBrains, Visual Studio, Xcode, Eclipse

In Copilot Chat, open the agent tools menu (a wrench or tools icon) → **Add MCP server** / **Edit MCP configuration**,
and add:

```json
{
  "servers": {
    "commercializer": {
      "type": "http",
      "url": "https://commercializer.ai/mcp"
    }
  }
}
```

Visual Studio reads the same block from `.mcp.json` in the solution folder or `%USERPROFILE%\.mcp.json`. Each asks you to
sign in the first time a tool runs.

## With an API key instead

Where the IDE cannot open a browser, make a key on the **MCP** page and add a header. In VS Code, keep the key out of the
file with an input:

```json
{
  "inputs": [
    { "type": "promptString", "id": "commercializer-key", "description": "Commercializer API key", "password": true }
  ],
  "servers": {
    "commercializer": {
      "type": "http",
      "url": "https://commercializer.ai/mcp",
      "headers": { "Authorization": "Bearer ${input:commercializer-key}" }
    }
  }
}
```

See [API keys](api-keys.md).

## Use it

- In agent mode, ask in plain words, or reference the server with `#commercializer`.
- Tools that change something (keeping a finding, starting a workflow) ask before they run unless you allow them.
- Starter prompts: *What clearances and recalls does our closest competitor hold, register by register?* · *Which US
  pathway fits our device?* · *Run a market entry workflow for Germany and the UK on our lead product.*

## Disconnect

Remove the server from `mcp.json` (or **MCP: List Servers → commercializer → Uninstall**), or `copilot plugin uninstall commercializer`. In Commercializer, **Disconnect** it on the **MCP** page.

## Troubleshooting

- **"MCP servers are disabled by your organization":** an admin enables the MCP policy in the organisation's Copilot
  settings.
- **The sign-in never finishes:** VS Code needs `https://vscode.dev/redirect` or a local port to receive the sign-in;
  allow the browser to open VS Code when it asks.
- More in [Troubleshooting](troubleshooting.md).
