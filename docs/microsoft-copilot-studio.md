# Commercializer in Microsoft Copilot Studio

Give an agent in Copilot Studio the Commercializer tools; publish it to Microsoft 365 Copilot, Teams or a website, and
each person who uses it signs in to Commercializer as themselves.

## Before you start

- A Copilot Studio environment where you can make agents, with **generative orchestration** on (MCP tools need it).
- A Commercializer account; each person who uses the agent needs their own.

## Connect

1. Open your agent in **Copilot Studio** and go to **Tools → Add a tool → New tool → Model Context Protocol**.
2. Fill in:
   - **Server name:** `Commercializer`
   - **Server description:** `Commercial strategy for medical device and life-science companies, read from the governed registers.`
   - **Server URL:** `https://commercializer.ai/mcp`
3. **Authentication:** **OAuth 2.0**, type **Dynamic discovery**. Copilot Studio finds Commercializer's sign-in and
   registers itself; there is no client ID or secret to enter.
4. **Create**. In the connection step, choose **Create new connection** and sign in: commercializer.ai opens, you choose
   the workspace and press **Allow**.
5. **Add to agent**. The tools appear under the server; turn off any the agent should not use.

## Check it works

In the **Test** pane, ask:

> What does Commercializer hold about our company?

The activity map shows `get_profile` running and the agent answers with your company.

## Use it

- Describe in the agent's **Instructions** when to use it: *For anything about our company, competitors, regulatory
  pathways or the registers, use Commercializer and cite every read.*
- Leave write tools (`keep_finding`, `run_tool`, `start_workflow`, `answer_checkpoint`) on only if the agent should change
  things in Commercializer; Copilot Studio can ask the user before each one.
- **Publish** to Teams and Microsoft 365 Copilot; each user is asked to sign in to Commercializer the first time.

## With an API key instead

For an agent that acts as one service identity, choose **Authentication: API key**, **Header**, name `Authorization`,
and give the value `Bearer <key>` from the **MCP** page. Every user then works in that key's workspace; prefer OAuth.

## Disconnect

Remove the tool from the agent; each user can remove their connection in **Settings → Connections**. In Commercializer,
**Disconnect** it on the **MCP** page.

## Troubleshooting

- **The first connection fails with a redirect error:** connect again; Copilot Studio registers its redirect on the first
  attempt.
- **A tool is missing from the list:** Copilot Studio drops tools whose inputs it cannot read; tell us at
  hello@commercializer.ai which one.
- More in [Troubleshooting](troubleshooting.md).
