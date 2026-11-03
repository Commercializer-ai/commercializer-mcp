---
name: ask
description: Ask Commercializer's agent a question about your company or a competitor; it reads the registers, keeps what it finds and answers with every record cited. Use when the person says "ask Commercializer" or asks a question that needs many register reads woven together.
argument-hint: <question>
---

Ask Commercializer's agent the person's question with the Commercializer tools.

1. Pass the profile the person means (`list_profiles` gives the ids). A workspace with one company takes it when
   `profile` is left out; one with several refuses the call with their ids, so ask which.
2. Call `ask_agent` with the question in the person's words. It waits up to 45 seconds; if the answer comes back
   `running`, call `get_agent_answer` with the turn id every 10 seconds until it is `done`.
3. Give the answer as it came, keeping every `[read …]` citation, with the link to the conversation on commercializer.ai.
4. If the agent could not answer from the registers, say so plainly; do not fill the gap yourself.
