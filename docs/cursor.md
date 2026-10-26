# Commercializer in Cursor

Add the Commercializer server to Cursor in one click, sign in, and Cursor's agent can read the registers for your
company.

## Before you start

- A Commercializer account and a workspace with your company set up.
- Cursor with MCP (any current version).

## Connect

### One click

[**Add Commercializer to Cursor**](https://cursor.com/en/install-mcp?name=commercializer&config=eyJ1cmwiOiJodHRwczovL2NvbW1lcmNpYWxpemVyLmFpL21jcCJ9)
opens Cursor with the server filled in. Choose **Install**.

### Or by hand

**Cursor Settings → Tools & MCP → Add custom MCP** opens `~/.cursor/mcp.json` (or use `.cursor/mcp.json` in a project):

```json
{
  "mcpServers": {
    "commercializer": {
      "url": "https://commercializer.ai/mcp"
    }
  }
}
```

### Or the plugin

Cursor reads Agent Plugins: add `https://github.com/Commercializer-ai/commercializer` from **Cursor Settings → Plugins**
to get the server and the Commercializer skills.

## Sign in

In **Cursor Settings → Tools & MCP**, **commercializer** shows **Needs login**. Press it: commercializer.ai opens, sign
in, choose the workspace and press **Allow Cursor**. The dot turns green and the tools are listed.

## Check it works

In the agent chat, ask:

> Using Commercializer, what does my workspace hold about our company?

## With an API key instead

```json
{
  "mcpServers": {
    "commercializer": {
      "url": "https://commercializer.ai/mcp",
      "headers": { "Authorization": "Bearer ${env:COMMERCIALIZER_KEY}" }
    }
  }
}
```

with `COMMERCIALIZER_KEY` set in the environment Cursor starts from. See [API keys](api-keys.md).

## Disconnect

Turn the server off or delete it in **Tools & MCP**; **Disconnect** it on the **MCP** page of Commercializer.

## Troubleshooting

- **"Needs login" comes back:** press it again; if it repeats, delete the server and add it again so Cursor registers
  afresh.
- More in [Troubleshooting](troubleshooting.md).
