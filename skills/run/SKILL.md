---
name: run
description: Start a Commercializer workflow on your company — a pathway decision, submission checklist, market entry, competitor footprint, company brief and more — and follow it, answering each checkpoint with you. Use when the person asks for one of those deliverables or says "run a workflow".
argument-hint: <workflow or what you need>
---

Run a Commercializer workflow for the person with the Commercializer tools.

1. Call `list_workflows` for the profile (the primary when none is named). Match what they asked to one workflow by its
   id, name or deliverable; if two fit, show both in one line each and ask which.
2. If it is not in the plan (`inPlan: false`), say which plan runs it and stop.
3. If it is marked `readsProduct` and the profile has no products, say to add one on the profile's plan pages in
   Commercializer, and stop.
4. Show the inputs `list_workflows` prefilled; ask only for the empty ones or the ones the person wants to change.
5. Call `start_workflow`. If the person wants it to run on its own, pass `away: true` so Commercializer's agent answers
   the checkpoints. Otherwise call `get_workflow_run` every 15 seconds; when a step is `needs-input`, show its question
   and choices, and send the person's choice with `answer_checkpoint`. Report each step's headline as it saves.
6. When the run is `done`, give its link and every step's headline. Offer `start_watch` if it is worth keeping current.
