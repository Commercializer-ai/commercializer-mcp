# API keys

An API key lets a script, a CI job, the Copilot coding agent or any client that cannot open a browser use Commercializer
as you, in one workspace. It works on the MCP server and on the app's own API.

## Make a key

1. On [commercializer.ai](https://commercializer.ai), open the **MCP** page of the workspace the key should reach.
2. **Connect an assistant**, choose the client (or **A script or your own code**), then **An API key**.
3. Name it for where it will live (`CI`, `Build server`), **Continue**, and copy it. It starts `czk_` and is **shown
   once**; only its last four characters are kept to tell keys apart.

A key signs as the person who made it, in the workspace it was made in, with that person's role. A viewer cannot make
one.

## Use it on the MCP server

Send it as a bearer token on every request:

```sh
curl https://commercializer.ai/mcp \
  -H "Authorization: Bearer $COMMERCIALIZER_KEY" \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/list"}'
```

A tool call:

```sh
curl https://commercializer.ai/mcp \
  -H "Authorization: Bearer $COMMERCIALIZER_KEY" \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","id":2,"method":"tools/call","params":{"name":"recalls_find","arguments":{"initiated_from":"2026-01-01"}}}'
```

With the official MCP SDKs:

```ts
// TypeScript: npm i @modelcontextprotocol/sdk
import { Client } from '@modelcontextprotocol/sdk/client/index.js';
import { StreamableHTTPClientTransport } from '@modelcontextprotocol/sdk/client/streamableHttp.js';

const client = new Client({ name: 'my-script', version: '1.0.0' });
await client.connect(new StreamableHTTPClientTransport(new URL('https://commercializer.ai/mcp'), {
  requestInit: { headers: { Authorization: `Bearer ${process.env.COMMERCIALIZER_KEY}` } },
}));
const profile = await client.callTool({ name: 'get_profile', arguments: {} });
```

```python
# Python: pip install mcp
import asyncio, os
from mcp import ClientSession
from mcp.client.streamable_http import streamablehttp_client

async def main():
    headers = {"Authorization": f"Bearer {os.environ['COMMERCIALIZER_KEY']}"}
    async with streamablehttp_client("https://commercializer.ai/mcp", headers=headers) as (read, write, _):
        async with ClientSession(read, write) as session:
            await session.initialize()
            print(await session.call_tool("get_profile", {}))

asyncio.run(main())
```

## Use it on the app's API

The same key signs requests to the routes the Commercializer app calls, as you, with no browser session:

```sh
curl https://commercializer.ai/api/profiles -H "Authorization: Bearer $COMMERCIALIZER_KEY"
```

These routes are the app's own and may change with it; for anything you build to last, use the MCP server's tools.

## In each client

| Client | Where the key goes |
| --- | --- |
| Claude Code | `claude mcp add --transport http commercializer https://commercializer.ai/mcp --header "Authorization: Bearer …"` |
| VS Code / Copilot | `headers` in `mcp.json`, from a `promptString` input ([guide](github-copilot.md#with-an-api-key-instead)) |
| Copilot coding agent | a `COPILOT_MCP_` secret ([guide](copilot-coding-agent.md)) |
| Cursor | `headers` in `mcp.json` with `${env:…}` |
| Codex | `bearer_token_env_var` in `config.toml` |
| Antigravity | `headers` beside `serverUrl` |
| Copilot Studio | Authentication: API key, header `Authorization`, value `Bearer …` |

## Keep it safe

- Treat it as a password: keep it in a secret store or an environment variable, never in a repository.
- One key per place, so revoking one does not stop the others.
- Its reads, findings and runs are marked with its name on the **MCP** page; check what it did there.
- **Revoke** it on the **MCP** page; it stops at once. A key also stops if its maker leaves the workspace.
