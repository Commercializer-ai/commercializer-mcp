# Commercializer in ChatGPT

Add Commercializer to ChatGPT as a custom MCP server, sign in once, and ChatGPT can read the registers for your company, keep
findings and run workflows in any chat.

## Before you start

- A Commercializer account and a workspace with your company set up ([commercializer.ai](https://commercializer.ai)).
- Any ChatGPT plan, Free included. Custom servers are added on **chatgpt.com** on the web; the desktop and mobile apps
  then use them.

## Connect

1. In ChatGPT on the web, open **Plugins** in the sidebar.
2. Press **Add** (top right) and choose **Add custom MCP server**.
3. Fill in:
   - **Icon:** optional; the 128 px PNG in [`assets/icon.png`](../assets/icon.png) fits its 10 KB limit.
   - **Name:** `Commercializer`
   - **Description:** `Commercial strategy for medical device and life-science companies, read from the governed registers.`
   - **Connection:** **Server URL**, `https://commercializer.ai/mcp`
   - **Authentication:** `OAuth`. Leave **Advanced OAuth settings** as they are: ChatGPT finds Commercializer's sign-in
     and identifies itself.
4. Tick **I understand and want to continue**, then **Create as a plugin**.

## Sign in

ChatGPT asks to **Connect Commercializer**. Press it: commercializer.ai opens, sign in, choose the workspace it reaches
and press **Allow ChatGPT**. You are back on the Plugins page with Commercializer under **Installed**.

## Check it works

Start a chat and ask:

> Using Commercializer, what does my workspace hold about our company?

ChatGPT calls `get_profile` and answers with your company's name and the findings kept about it. Then try a register
read:

> What recalls has our closest competitor had since 2024? Cite the reads.

Each figure carries a `[read dr_…]` id.

## Use it

- Ask in plain words; ChatGPT picks the tools. Name **Commercializer** in the message when you want it used.
- Tools that change something (keeping a finding, starting a workflow, answering a checkpoint) follow the permission you
  set under **Settings → Plugins** (by default ChatGPT asks before them).
- For long deliverables, ask ChatGPT to start a workflow and leave it running; open the link it gives on
  commercializer.ai to watch it, or ask *How is the run going?* later.
- In **Deep research**, choose Commercializer as a source: it searches your workspace and the registry companies with
  `search` and reads each result with `fetch`.

Starter prompts:

- *What clearances and recalls does our closest competitor hold, register by register?*
- *Which US pathway fits our device, and which predicates would we lean on?*
- *Run a market entry workflow for Germany and the UK on our lead product.*

## For a team (Business, Enterprise, Edu)

A custom server you add is yours. A workspace admin can make it available to everyone from the workspace's plugin
settings; each person still signs in to Commercializer as themselves, so each sees only their own workspaces.

## Disconnect

In ChatGPT: **Settings → Plugins → Commercializer**, then disconnect or remove it. In Commercializer: the **MCP** page,
**Disconnect** beside ChatGPT. Either ends its access at once.

## Troubleshooting

- **No "Add custom MCP server" in the Add menu:** your workspace admin has turned custom servers off.
- **"This assistant could not be identified" on commercializer.ai:** remove the plugin in ChatGPT and add it again.
- **It stops working after some time:** disconnect and connect again; ChatGPT keeps a refresh token and should not need
  this, so tell us at hello@commercializer.ai if it happens twice.
- More in [Troubleshooting](troubleshooting.md).
