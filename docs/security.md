# Security and data

## What a connected assistant can do

- It works **as you**, in the **one workspace** you approved when you signed in (or the one a key was made in), with
  your role there. It can do nothing you cannot.
- It can read your company profiles and what is kept about them, read the governed registers, keep and forget findings
  with their sources, start, steer and stop workflows and watches, and ask Commercializer's agent.
- It cannot see your other workspaces, change members, plans, billing or settings, or read another organisation's data.
- Workflow runs and research count against your workspace's plan, as the app's own do.

## What is kept

- **Who connected what:** each connected assistant or key, who connected it, when, and when it was last used.
- **What it did:** every register read it made (kept so a finding can cite it), every finding it kept and every run it
  started, each marked with its name. These show on the **MCP** page and on the profiles.
- **Credentials:** only a hash of each token and key. An access token lasts an hour; a refresh token thirty days and is
  replaced each time it is used. An API key lasts until revoked, and opens the MCP server alone: the app's own routes
  refuse it.
- Commercializer does not receive your conversation with the assistant: only the tool calls it makes, with their
  arguments.

## Your controls

- **Disconnect** an assistant or **Revoke** a key on the **MCP** page; it stops at once. Owners and admins can cut off
  any assistant in the workspace; members their own.
- Leaving a workspace ends every assistant and key you connected to it.
- A viewer cannot connect an assistant or make a key.

## Sign-in

OAuth 2.1 with PKCE (S256). Assistants register themselves or identify themselves with a client metadata document; the
consent page names the assistant, where it is asking from, the workspace it will reach and what it will be able to do.
A sign-in can only return to an address the assistant registered (`https`, a loopback address, or an app scheme).

Full terms: [Privacy](https://commercializer.ai/privacy) · [Terms](https://commercializer.ai/terms). Questions:
hello@commercializer.ai.
