---
description: Start a Commercializer workflow on your company and follow it, answering each checkpoint with you.
argument-hint: <workflow-id or a few words of what you need> [--profile <pr_id>] [--away]
---

Run a Commercializer workflow for the person, using the `commercializer` MCP server:

$ARGUMENTS

1. Call `workflows` for the profile (the primary when none is named). Match what they asked to one workflow by id or by
   its name and deliverable; if two fit, show both in one line each and ask which.
2. If the workflow is not in the plan (`inPlan: false`), say which plan runs it and that one run can be bought for $99 on
   the site; stop there unless they have bought one (`bought > 0`).
3. If it is marked `readsProduct` and the profile has no products, tell them to add one on the site's plan pages; stop.
4. Show the inputs `workflows` prefilled and ask only for the ones that are empty or that they would change.
5. Call `workflow_start`. With `--away`, pass `away: true` so Commercializer's agent answers the checkpoints; otherwise
   poll `workflow_run` every 15 seconds. When a step is `needs-input`, show its question and choices and call
   `workflow_answer` with what the person chooses. Report each step's headline as it saves.
6. When the run is `done`, give the link to the run on the site and the headlines of every step. Offer `watch_start` if
   it is a deliverable worth keeping current.
