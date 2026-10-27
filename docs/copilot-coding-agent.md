# Commercializer for the Copilot coding agent

The Copilot coding agent works on its own on github.com (assigned an issue, or asked in a pull request). It cannot open
a browser to sign in, so it uses a Commercializer API key kept as a repository secret.

## Before you start

- Admin access to the repository on GitHub.
- A Commercializer API key: on commercializer.ai open the **MCP** page, **Connect an assistant → A script or your own
  code** (or **Copilot coding agent**), name the key `Copilot coding agent` and copy it. It is shown once.

## Connect

1. **Keep the key as a secret.** In the repository: **Settings → Secrets and variables → Agents** (or **Environments →
   copilot → Environment secrets** on older settings pages) → **New secret**. Name: `COPILOT_MCP_COMMERCIALIZER_KEY`.
   Value: the key. The name must start with `COPILOT_MCP_`.
2. **Add the server.** **Settings → Copilot → MCP servers** (under *Code, planning, and automation*), and paste:

```json
{
  "mcpServers": {
    "commercializer": {
      "type": "http",
      "url": "https://commercializer.ai/mcp",
      "headers": {
        "Authorization": "Bearer $COPILOT_MCP_COMMERCIALIZER_KEY"
      },
      "tools": [
        "search", "fetch", "list_profiles", "get_profile", "resolve", "company_footprint", "company_profile",
        "device_trace", "graph_compare", "lookup", "trials_find", "recalls_find", "document_search", "document_get",
        "result_page", "recall_findings", "list_tools", "get_tool_run", "list_workflows", "get_workflow_run",
        "get_workflow_step", "list_watches", "get_agent_answer"
      ]
    }
  }
}
```

3. **Save MCP configuration.**

The list allows only the tools that read. To let the agent keep findings or start workflows, add `keep_finding`,
`run_tool`, `start_workflow` or `ask_agent`, or use `"tools": ["*"]`.

## Check it works

Assign an issue to Copilot that needs the registers, for example *Add the FDA product codes of our three closest
competitors to docs/competitors.md*. In the agent's session log, the **Start MCP Servers** step lists the Commercializer
tools; later steps show the reads it made.

## Disconnect

Remove the server block (or the repository's MCP configuration) and delete the secret; revoke the key on the **MCP**
page of Commercializer.

## Troubleshooting

- **The session log says the server failed to start:** the secret name does not match `$COPILOT_MCP_…` in the
  configuration, or the key was revoked.
- **401 from the server:** make a new key and replace the secret.
- More in [API keys](api-keys.md) and [Troubleshooting](troubleshooting.md).
