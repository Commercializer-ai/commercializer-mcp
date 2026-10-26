---
description: Ask Commercializer's agent about your company (or a profile you name); it reads the registers, keeps what it finds and answers with every record cited.
argument-hint: <question> [--profile <pr_id>]
---

Ask Commercializer's agent this, using the `commercializer` MCP server:

$ARGUMENTS

1. If no profile is named, use the workspace's primary profile (call `profiles` only if you need its id).
2. Call `ask_agent` with the question. It waits up to 45 seconds; if the answer comes back `running`, poll `agent_answer`
   with the turn id every 10 seconds until it is `done`.
3. Give the person the answer as it came, keeping every `[read …]` citation, and the link to the conversation on the site.
4. If the agent could not answer from the registers, say so plainly; do not fill the gap yourself.
