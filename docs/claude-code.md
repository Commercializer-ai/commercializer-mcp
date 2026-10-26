# Commercializer in Claude Code

Install the Commercializer plugin: the server, a skill that teaches Claude how to work your workspace, and four skills
you call by name. Or add just the server.

## Before you start

- A Commercializer account and a workspace with your company set up.
- Claude Code, recent enough for plugins (`claude --version`; update with `claude update`).

## Install the plugin

In Claude Code:

```
/plugin marketplace add Commercializer-ai/commercializer-mcp
/plugin install commercializer@commercializer
```

Or from your shell:

```sh
claude plugin marketplace add Commercializer-ai/commercializer-mcp
claude plugin install commercializer@commercializer
```

Restart Claude Code (or run `/reload-plugins`) so the server and skills load.

## Sign in

Type `/mcp`, choose **commercializer** and **Authenticate**. Your browser opens commercializer.ai: sign in, choose the
workspace it reaches and press **Allow Claude Code**. Back in Claude Code, `/mcp` shows it **connected**.

**On a remote machine** (SSH, a cloud session) the browser lands on a `localhost` page that does not load. Copy that
page's full address from the address bar and paste it back into Claude Code when it asks; that completes the sign-in.

## Check it works

```
/commercializer:workspace
```

lays out your company, what is kept, the watches and the workflows your plan runs.

## Use it

| You type | It does |
| --- | --- |
| `/commercializer:ask <question>` | Hands the question to Commercializer's agent and returns its cited answer. |
| `/commercializer:run <workflow>` | Starts a workflow and walks each checkpoint with you. |
| `/commercializer:workspace` | Where your workspace stands. |
| `/commercializer:setup` | Connects and checks it works. |

Or just ask. The `commercializer` skill loads when the conversation is about a medical device or life-science company,
and has Claude read before stating a figure, cite every read and keep what is worth knowing.

## Just the server, no plugin

```sh
claude mcp add --transport http commercializer https://commercializer.ai/mcp
```

Add `--scope user` to have it in every project. Then `/mcp` to sign in.

## With an API key instead

For a headless machine or CI, make a key on the **MCP** page of your workspace and:

```sh
claude mcp add --transport http commercializer https://commercializer.ai/mcp \
  --header "Authorization: Bearer $COMMERCIALIZER_KEY"
```

See [API keys](api-keys.md).

## Update and remove

```sh
claude plugin marketplace update commercializer
claude plugin update commercializer@commercializer
claude plugin uninstall commercializer@commercializer
```

Disconnecting on the **MCP** page ends its access whether or not the plugin stays installed.

## Troubleshooting

- **`/mcp` shows "failed" or "needs authentication":** choose it and **Reconnect** or **Authenticate**. A server that
  failed when Claude Code started is not retried until you do.
- **The skills do not appear:** run `/plugin` and check `commercializer@commercializer` is enabled, then restart.
- More in [Troubleshooting](troubleshooting.md).
