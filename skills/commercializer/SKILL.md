---
name: commercializer
description: How to work a Commercializer workspace through its tools — read the governed registers before stating any figure, cite every read, keep findings, run workflows and watches, and hand hard questions to the agent. Use whenever the Commercializer tools are available and the person asks about a medical device or life-science company, its regulatory path, safety record, clinical evidence, patents, payment, buyers, tenders, competitors or money.
---

# Commercializer

The Commercializer server is the person's workspace on commercializer.ai: one primary company (their own) and the
competitors it tracks, each a profile. Every tool runs as the person, through the same functions the app uses, so what you
read, keep and start lands where they see it, marked with your name. The server's instructions already carry the primary
company's profile.

## Rules

1. **Read before you state a figure.** Every register answer starts with `[read dr_…]`; cite that id beside the figure.
   Where the registers hold no answer, say so. Never invent a record, a clearance, a tender, a price or a date.
2. **Resolve names first.** `resolve` with `kind: company` turns a company name into its canonical UUID; pass that UUID
   to `company_footprint`, `graph_compare`, `lookup`, `recalls_find` and `trials_find` instead of free text.
3. **Look before you read again.** `search` finds what the workspace already holds (profiles, kept findings, workflow
   runs) and the registry companies by a name; `fetch` reads one result in full.
4. **Keep what is worth knowing next time** with `keep_finding`: one line, naming the reads that show it. A finding
   without a source is refused. `forget_finding` drops one that no longer holds, with the reason. Never keep a guess.
5. **Deliverables are workflows.** For a structured answer use `list_workflows`, then `start_workflow`; follow it with
   `get_workflow_run`, and when a step waits, show the person its question and choices and send their choice with
   `answer_checkpoint`. `start_watch` keeps a deliverable current. Runs and watches count against the workspace's plan;
   `list_workflows` says which ones it runs.
6. **Hand a question that needs many reads woven together to the agent** with `ask_agent`; if it is still working, read
   it with `get_agent_answer`.
7. **Write for the person.** Name records in English ("510(k) decisions", "recalls", "registered trials"), never a
   dataset id or a table. Say how sure a reading is when the tool says so.

## Which tool for what

| Need | Tool |
| --- | --- |
| What the workspace holds, by a word | `search`, then `fetch` |
| The companies in the workspace | `list_profiles`, `get_profile` |
| A name → canonical identity; a code or term | `resolve`, `lookup` |
| One company across clearances, registrations, safety and trials | `company_footprint` |
| A listed company's financials, filings and insiders | `company_profile` (ticker or CIK) |
| A device's predicates and its chain | `device_trace` (brand, product code or K/DEN/PMA number) |
| Two to five companies side by side | `graph_compare` |
| Registered trials; recalls | `trials_find`, `recalls_find` |
| Passages from authorised documents | `document_search`, `document_get` |
| The rest of a long answer | `result_page`, with the `continuation.next_cursor` it gave |
| Memory of the company | `recall_findings`, `keep_finding`, `forget_finding` |
| Deliverables | `list_workflows`, `start_workflow`, `get_workflow_run`, `get_workflow_step`, `answer_checkpoint`, `note_workflow_run`, `stop_workflow_step` |
| Standing deliverables | `list_watches`, `start_watch`, `stop_watch` |
| The agent | `ask_agent`, `get_agent_answer` |

## The workflows, by pack

- **Regulatory:** pathway-decision, submission-checklist, evidence-bar, clinical-tier, launch-readiness,
  change-assessment, portfolio-upkeep, postmarket-obligations, lifecycle-map, safety-burden, signal-watch,
  competitor-footprint, similar-patents.
- **Commercial:** market-entry, go-to-market, market-whitespace, provider-targeting, kol-map, tender-watch,
  patent-whitespace.
- **Evidence:** clinical-evidence, trial-map.
- **Innovation:** need-finding, need-sizing, value-proposition.
- **Capital:** raise-plan, competitor-financials, deal-screen, ownership-watch.
- **Programme:** company-analysis (a decision brief from six modules), company-brief (a sourced deck in six acts).

`list_workflows` returns each with its deliverable, steps, the inputs already filled from the profile, and whether the
plan runs it; one marked `readsProduct` starts from one of the profile's products and refuses with none.

## A typical turn

```
get_profile                               who we work for, what is kept
resolve kind=company text="Shockwave"     → the canonical UUID
company_footprint company=<uuid>          → [read dr_…] clearances, registrations, recalls, trials
recalls_find firm=[<uuid>]                → [read dr_…]
keep_finding text="…" sources=[dr_…]      one line, cited
```

Answer in the person's words with the reads cited, and offer the workflow that would take it further.
