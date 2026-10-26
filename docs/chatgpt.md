# Commercializer in ChatGPT

Add Commercializer to ChatGPT as an app, sign in once, and ChatGPT can read the registers for your company, keep
findings and run workflows in any chat.

## Before you start

- A Commercializer account and a workspace with your company set up ([commercializer.ai](https://commercializer.ai)).
- A ChatGPT plan that can add custom apps: developer mode is on Plus, Pro, Business, Enterprise and Edu (on Business,
  Enterprise and Edu an admin may need to allow it). Custom apps are added on **chatgpt.com** on the web; the desktop and
  mobile apps then use them.

## Connect

1. In ChatGPT on the web, open **Settings → Apps** (called **Apps & Connectors** on some plans).
2. Under **Advanced settings**, turn on **Developer mode**.
3. Back in **Apps**, choose **Create app** (or **Create**).
4. Fill in:
   - **Name:** `Commercializer`
   - **Description:** `Commercial strategy for medical device and life-science companies, read from the governed registers.`
   - **MCP server URL:** `https://commercializer.ai/mcp`
   - **Authentication:** `OAuth`. Leave the client ID and secret empty: ChatGPT registers itself.
5. Tick that you trust the app, then **Create**.

## Sign in

ChatGPT opens commercializer.ai. Sign in, choose the workspace it reaches and press **Allow ChatGPT**. You are back in
ChatGPT with the app connected.

## Check it works

Start a chat, choose **Commercializer** from the **+** menu (under **More** if it is not listed), and ask:

> Using Commercializer, what does my workspace hold about our company?

ChatGPT calls `get_profile` and answers with your company's name and the findings kept about it. Then try a register
read:

> What recalls has our closest competitor had since 2024? Cite the reads.

Each figure carries a `[read dr_…]` id.

## Use it

- Ask in plain words; ChatGPT picks the tools. Name **Commercializer** in the message when you want it used.
- Write actions (keeping a finding, starting a workflow, answering a checkpoint) show a confirmation in developer mode
  before they run.
- For long deliverables, ask ChatGPT to start a workflow and leave it running; open the link it gives on
  commercializer.ai to watch it, or ask *How is the run going?* later.
- In **Deep research**, choose Commercializer as a source: it searches your workspace and the registry companies with
  `search` and reads each result with `fetch`.

Starter prompts:

- *What clearances and recalls does our closest competitor hold, register by register?*
- *Which US pathway fits our device, and which predicates would we lean on?*
- *Run a market entry workflow for Germany and the UK on our lead product.*

## For a team (Business, Enterprise, Edu)

An app created in developer mode starts as a draft for you. A workspace admin publishes it from **Workspace settings →
Apps** so everyone can add it; each person still signs in to Commercializer as themselves, so each sees only their own
workspaces.

## Disconnect

In ChatGPT: **Settings → Apps → Commercializer → Disconnect** (or delete the app). In Commercializer: the **MCP** page,
**Disconnect** beside ChatGPT. Either ends its access at once.

## Troubleshooting

- **No "Create app" button:** developer mode is off, or your plan or workspace does not allow it.
- **"This assistant could not be identified" on commercializer.ai:** delete the app in ChatGPT and create it again; it
  registers afresh.
- **It stops working after some time:** disconnect and connect again; ChatGPT keeps a refresh token and should not need
  this, so tell us at hello@commercializer.ai if it happens twice.
- More in [Troubleshooting](troubleshooting.md).
