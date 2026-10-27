<p align="center"><img src="assets/logo.png" width="96" height="96" alt="Commercializer"></p>

<h1 align="center">Commercializer</h1>

<p align="center">Commercial strategy for medical device and life-science companies, read from the governed registers.<br>
Bring it into the AI assistant you already use.</p>

<p align="center">
<a href="https://vscode.dev/redirect/mcp/install?name=commercializer&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fcommercializer.ai%2Fmcp%22%7D"><img alt="Add to VS Code" src="https://img.shields.io/badge/Add_to-VS_Code-FF5B14?style=for-the-badge&logo=visualstudiocode&logoColor=white"></a>
<a href="https://cursor.com/en/install-mcp?name=commercializer&config=eyJ1cmwiOiJodHRwczovL2NvbW1lcmNpYWxpemVyLmFpL21jcCJ9"><img alt="Add to Cursor" src="https://img.shields.io/badge/Add_to-Cursor-FF5B14?style=for-the-badge&logo=cursor&logoColor=white"></a>
<a href="docs/claude-ai.md"><img alt="Add to Claude" src="https://img.shields.io/badge/Add_to-Claude-FF5B14?style=for-the-badge&logo=claude&logoColor=white"></a>
<a href="docs/chatgpt.md"><img alt="Add to ChatGPT" src="https://img.shields.io/badge/Add_to-ChatGPT-FF5B14?style=for-the-badge&logo=openai&logoColor=white"></a>
</p>

Connected, your assistant works on your company the way the [Commercializer](https://commercializer.ai) app does. It reads
the governed registers (FDA clearances and approvals, EU and other registrations, recalls and adverse event reports,
registered trials, patents, payments to clinicians, public tenders and company filings), cites every record it uses,
keeps the findings worth remembering on your company's profile, and runs workflows that deliver a pathway decision, a
submission checklist, a market entry plan, a competitor footprint or a company brief, asking you at each decision.

Everything it does happens as you, in the workspace you choose, and is listed on the **MCP** page of your workspace under
its name, where you can disconnect it at any time.

- **The server:** `https://commercializer.ai/mcp` (Streamable HTTP; sign in with OAuth 2.1, or use an API key).
- **This repository:** [`github.com/Commercializer-ai/commercializer-mcp`](https://github.com/Commercializer-ai/commercializer-mcp), the plugin and a guide for every assistant.
- **The page:** [commercializer.ai/product/assistant](https://commercializer.ai/product/assistant).
- **Let the assistant set itself up:** give it [`https://commercializer.ai/mcp/llms.txt`](https://commercializer.ai/mcp/llms.txt). It says how to connect from
  each client, how to sign in, how to work the workspace and every tool.

## Connect your assistant

| Assistant | Fastest way | Full guide |
| --- | --- | --- |
| **ChatGPT** | Plugins → Add → Add custom MCP server, URL `https://commercializer.ai/mcp`, OAuth | [ChatGPT](docs/chatgpt.md) |
| **Claude** (claude.ai, desktop, mobile) | Customize → Connectors → Add → Add custom connector | [Claude](docs/claude-ai.md) |
| **Claude Code** | `/plugin marketplace add Commercializer-ai/commercializer-mcp` | [Claude Code](docs/claude-code.md) |
| **GitHub Copilot** (VS Code, Copilot CLI, JetBrains, Visual Studio) | [Add to VS Code](https://vscode.dev/redirect/mcp/install?name=commercializer&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fcommercializer.ai%2Fmcp%22%7D) or `copilot plugin marketplace add Commercializer-ai/commercializer-mcp` | [GitHub Copilot](docs/github-copilot.md) |
| **Copilot coding agent** (on github.com) | Repository settings → Copilot → MCP servers, with an API key | [Copilot coding agent](docs/copilot-coding-agent.md) |
| **Microsoft Copilot Studio** (agents for Microsoft 365 Copilot and Teams) | Tools → Add a tool → Model Context Protocol, OAuth dynamic discovery | [Copilot Studio](docs/microsoft-copilot-studio.md) |
| **Cursor** (editor and CLI) | [Add to Cursor](https://cursor.com/en/install-mcp?name=commercializer&config=eyJ1cmwiOiJodHRwczovL2NvbW1lcmNpYWxpemVyLmFpL21jcCJ9), or `cursor-agent mcp login commercializer` | [Cursor](docs/cursor.md) |
| **Codex** (CLI, IDE, app) | `codex mcp add commercializer --url https://commercializer.ai/mcp` | [Codex](docs/codex.md) |
| **Antigravity** (and Gemini CLI) | `serverUrl` in `mcp_config.json` | [Antigravity](docs/antigravity.md) |
| **Devin Desktop, Windsurf, Kiro, Zed, Goose and others** | the server URL, or `mcp-remote` for a stdio-only client | [Other clients](docs/other-clients.md) |
| **A script or your own code** | an API key as `Authorization: Bearer` | [API keys](docs/api-keys.md) |
| **Any assistant, on its own** | give it `https://commercializer.ai/mcp/llms.txt` | [For assistants](docs/agents.md) |

Signed in to Commercializer, the **MCP** page of your workspace walks the same steps for the assistant you pick and makes
an API key when you need one.

## The plugin

This repository is also a plugin: the server, a skill that teaches the assistant how to work the workspace (read before
stating a figure, cite every read, keep findings, use the tools, run workflows), and five skills you can call by name.

| Skill | What it does |
| --- | --- |
| `ask` | Hands a question to Commercializer's agent; the answer comes back with every record cited. |
| `tool` | Answers one question with a tool, every row with its sources. |
| `run` | Starts a workflow on your company and follows it, answering each checkpoint with you. |
| `workspace` | Your company and its competitors, what is kept, the watches running, the workflows your plan runs. |
| `setup` | Connects and checks it works. |

It follows the open [Agent Plugins](https://agent-plugins.org) format (`plugin.json`, `mcp.json`, `skills/`) that
ChatGPT, Codex, GitHub Copilot, VS Code and Cursor read, and carries a Claude Code manifest (`.claude-plugin/`) beside it.

```
Claude Code      /plugin marketplace add Commercializer-ai/commercializer-mcp
                 /plugin install commercializer@commercializer
Copilot CLI      copilot plugin marketplace add Commercializer-ai/commercializer-mcp
                 copilot plugin install commercializer@commercializer
VS Code          Command Palette → Chat: Install Plugin From Source → https://github.com/Commercializer-ai/commercializer-mcp
Codex            codex plugin marketplace add Commercializer-ai/commercializer-mcp
                 codex plugin add commercializer@commercializer
Cursor           Cursor Settings → Plugins → https://github.com/Commercializer-ai/commercializer-mcp
```

It is also listed in the [MCP Registry](https://registry.modelcontextprotocol.io) as `ai.commercializer/commercializer`.

## What it can do

[Every tool](docs/tools.md), with what it reads or changes. In short:

- **Read the registers:** `resolve`, `company_footprint`, `company_profile`, `device_trace`, `graph_compare`, `lookup`,
  `trials_find`, `recalls_find`, `document_search`, `document_get`. Every answer starts with a read id you can cite.
- **Know your company:** `search`, `fetch`, `list_profiles`, `get_profile`, `recall_findings`, `keep_finding`,
  `forget_finding`.
- **Answer one question with a tool:** `list_tools`, `run_tool`, `get_tool_run`; 48 tools, from a US pathway and an FTO
  screen to open tenders, a trial landscape and who is investing in your space.
- **Run workflows and watches:** `list_workflows`, `start_workflow`, `get_workflow_run`, `answer_checkpoint` and more;
  31 workflows across regulatory, commercial, evidence, innovation, capital and programme work.
- **Ask the agent:** `ask_agent`, `get_agent_answer`.

Try:

- *What clearances and recalls does our closest competitor hold, register by register?*
- *Which US pathway fits our device, and which predicates would we lean on?*
- *Run a market entry workflow for Germany and the UK on our lead product.*

## Privacy and control

- It works as you, in the one workspace you approved, and can do only what you can do there.
- Every read, finding and run it makes is marked with its name on the MCP page and on the profile.
- Disconnect an assistant or revoke a key on the MCP page; it stops at once.
- Workflow runs and research count against your workspace's plan, as the app's own do.

More in [Security and data](docs/security.md). Problems: [Troubleshooting](docs/troubleshooting.md).

## Support

[commercializer.ai/contact](https://commercializer.ai/contact) · hello@commercializer.ai ·
[Privacy](https://commercializer.ai/privacy) · [Terms](https://commercializer.ai/terms)
