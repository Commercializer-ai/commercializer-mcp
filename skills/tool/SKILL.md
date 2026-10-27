---
name: tool
description: Answer one question with a Commercializer tool — a US pathway, open tenders, who wins tenders, an FTO screen, a trial landscape, how Medicare pays, who is investing in your space and more — in a minute or two, every row with its sources. Use when the person asks one of those questions or says "use a tool".
argument-hint: <question or tool>
---

Answer the person's question with one Commercializer tool.

1. Call `list_tools` for the profile (the primary when none is named). Match the question to one tool by its name or what
   it answers; if two fit, show both in one line each and ask which.
2. Show the inputs it marks `filled` from the profile; ask only for the empty ones that are not optional, or the ones the
   person wants to change. An input with `options` takes their exact words.
3. Call `run_tool`. If it comes back `running`, call `get_tool_run` with the run id every 15 seconds until it is `done`
   or `failed`.
4. Give the headline, then the rows as a short table, each with the sources it cites, and the `[read …]` id the answer
   starts with. Give its link. If it failed, say why in its words.
5. Offer the workflow its `next` names when the person wants the full deliverable, and `keep_finding` for what is worth
   keeping, citing the read.
