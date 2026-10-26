# Commercializer in Claude

Add Commercializer as a connector in Claude (claude.ai, the desktop app and the mobile apps) and Claude can read the
registers for your company, keep findings and run workflows.

## Before you start

- A Commercializer account and a workspace with your company set up ([commercializer.ai](https://commercializer.ai)).
- A Claude plan that can add custom connectors (Free allows one; Pro, Max, Team and Enterprise more). On Team and
  Enterprise an owner adds it for the organisation first; see [For a team](#for-a-team).

## Connect

1. In claude.ai or the desktop app, open **Settings → Connectors**.
2. Choose **Add custom connector**.
3. **Name:** `Commercializer`. **Remote MCP server URL:** `https://commercializer.ai/mcp`. Leave the advanced OAuth
   fields empty: Claude identifies itself.
4. **Add**, then **Connect** beside it.

## Sign in

Claude opens commercializer.ai. Sign in, choose the workspace it reaches and press **Allow Claude**. You are back in
Claude with Commercializer connected. Connectors you add on claude.ai appear in the desktop and mobile apps too.

## Check it works

In a new chat, open the **tools** menu under the message box, make sure **Commercializer** is on, and ask:

> What does Commercializer hold about our company?

Claude calls `get_profile` and answers with your company and the findings kept about it.

## Use it

- Ask in plain words; Claude chooses the tools and asks your permission the first time it uses each one (choose
  **Always allow** for the read tools if you like).
- In a **Project**, add the instruction *Use Commercializer for anything about our company, competitors or the
  registers; cite every read.* to make it the default.
- With **Research** on, Claude can run several register reads in one go and write a cited report.

## For a team

On Team and Enterprise, an owner adds the connector once in **Organisation settings → Connectors** with the same URL;
each member then connects it from their own **Settings → Connectors** and signs in to Commercializer as themselves.

## Disconnect

In Claude: **Settings → Connectors → Commercializer → Disconnect** (or remove it). In Commercializer: the **MCP** page,
**Disconnect** beside Claude.

## Troubleshooting

- **The tools do not show in a chat:** turn Commercializer on in the tools menu; on a new chat it may be off.
- **The sign-in page says the workspace cannot be connected:** you are a viewer in it; ask an owner or admin for a member
  role, or choose another workspace.
- More in [Troubleshooting](troubleshooting.md).
