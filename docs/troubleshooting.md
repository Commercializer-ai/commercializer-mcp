# Troubleshooting

## Signing in

| What you see | Why | What to do |
| --- | --- | --- |
| commercializer.ai says **This assistant could not be identified** | the assistant's registration expired or never finished | remove the server in the assistant and add it again |
| **The assistant asked to return somewhere it did not register** | the redirect changed since it registered | remove and add again |
| **No workspace you can edit** | you are a viewer in every workspace | ask for a member role, or start a workspace from that page |
| the browser ends on a `localhost` page that does not load | the assistant runs on another machine (SSH, cloud) | copy the page's full address and paste it where the assistant asks; or use an [API key](api-keys.md) |
| the assistant keeps asking to sign in | its refresh token was used twice or expired after thirty days unused | sign in again; if it repeats, tell us |

## Connecting

| What you see | Why | What to do |
| --- | --- | --- |
| **401** / "needs authentication" | not signed in, the token expired, or the assistant was disconnected | sign in again; check the **MCP** page that it is still listed |
| **405** on `GET /mcp` | the server answers `POST` only; there is no event stream | nothing: clients fall back to `POST`. A client that requires a stream needs `mcp-remote` ([other clients](other-clients.md)) |
| **429** / "Too many calls in a minute" | the per-connection rate limit | wait a minute |
| no tools, no error (Antigravity) | the entry uses `url` or `httpUrl` | use `serverUrl` |
| the server failed at start and never retried (Claude Code) | it was down or unauthenticated at start | `/mcp` → **Reconnect** |

## Using it

| What you see | Why | What to do |
| --- | --- | --- |
| "This org has no primary profile yet" | no company is set up in the workspace | set your company up on commercializer.ai, or name a profile from `list_profiles` |
| a workflow is "not in the plan" | your plan does not run it | `list_workflows` names the plan that does |
| a workflow "refuses to start" | it reads a product and the profile has none | add a product on the profile's plan pages |
| `keep_finding` is refused | the finding names no source, or a read this workspace cannot see | cite the `[read dr_…]` ids the reads returned |
| a figure has no `[read …]` id | the assistant answered from its own knowledge | ask it to read the registers and cite |

## Still stuck

Write to hello@commercializer.ai with the assistant you use, the time it happened and what it showed. The **MCP** page
of your workspace lists each assistant's last reads, which helps us find it.
