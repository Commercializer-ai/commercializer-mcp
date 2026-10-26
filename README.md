# Commercializer for Claude

Your [commercializer.ai](https://commercializer.ai) workspace inside Claude Code: the governed registers (clearances,
registrations, recalls, trials, patents, payments, tenders), what was kept about your company, the workflows and
watches, and the agent — through one MCP server, with a skill that teaches Claude how to work it and three commands.

## Install

In Claude Code:

```
/plugin marketplace add cvxn-founder/commercializer-claude
/plugin install commercializer@commercializer
/mcp
```

`/mcp` opens commercializer.ai once: sign in and choose the workspace it reaches. Every read, finding and run it makes
is listed on your workspace's Assistants page, under its name, and you can disconnect it there any time.

## Commands

| Command | What it does |
| --- | --- |
| `/commercializer:ask <question>` | Hands the question to Commercializer's agent; the answer comes back with every record cited. |
| `/commercializer:run <workflow>` | Starts a workflow on your company and follows it, answering each checkpoint with you. |
| `/commercializer:workspace` | Your company and its competitors, what is kept, the watches running, the workflows your plan runs. |

Without a command, just ask: the skill tells Claude to read the registers before stating a figure, cite each read, and
keep what is worth knowing next time.

## Without the plugin

Any MCP client that speaks Streamable HTTP connects to `https://commercializer.ai/mcp` and signs in the same way. A
script or a client with no browser uses an API key made on the Assistants page, sent as `Authorization: Bearer <key>`:

```
claude mcp add --transport http commercializer https://commercializer.ai/mcp --header "Authorization: Bearer <key>"
```

The step-by-step for Claude, ChatGPT, Cursor and VS Code is at
[commercializer.ai/product/assistant](https://commercializer.ai/product/assistant).
