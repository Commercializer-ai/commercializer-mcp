---
name: commercializer
description: How to work a commercializer.ai workspace through its MCP tools — read the governed registers before stating any figure, cite every read, keep findings, run workflows and watches, and hand hard questions to the agent. Use whenever the commercializer server's tools are available and the person asks about a medical device or life-science company, its regulatory path, safety record, evidence, patents, payment, buyers, tenders, competitors or money.
---

# Commercializer

The `commercializer` MCP server is the person's workspace on commercializer.ai: one primary company (their own) and the
competitors it tracks, each a profile. Every tool runs as the person, through the same functions the site uses, so what
you read, keep and start lands where they see it, marked as yours.

## Rules

1. **Read before you state a figure.** Every register answer starts with `[read dr_…]`; cite that id beside the figure.
   Where the registers hold no answer, say so. Never invent a record, a clearance, a tender, a price or a date.
2. **Start from the profile.** `profiles`, then `profile` (what they make, markets, products, goals, competitors, and what
   was kept, with sources). The server's instructions already carry the primary profile's head.
3. **Resolve names first.** `resolve kind=company` turns a company name into its canonical identity; pass that UUID to
   `company_footprint`, `graph_compare`, `lookup`, `recalls_find` and `trials_find` instead of a free-text name.
4. **Keep what is worth knowing next time** with `kept` (`store`): one line, naming the reads that show it. Forget a kept
   finding that no longer holds. Never keep a guess.
5. **Deliverables are workflows.** For a structured answer (market entry, submission checklist, competitor footprint, a
   company brief) use `workflows` to see what fits, `workflow_start`, then follow the run with `workflow_run` and answer
   its checkpoints with `workflow_answer` after asking the person. `watch_start` keeps a deliverable current weekly or
   monthly. Runs and watches count against the workspace's plan; `workflows` says which ones it runs.
6. **Hand a hard question to the agent** with `ask_agent` when it needs several reads woven together; read it back with
   `agent_answer` if it is still working.
7. **Name records in English** when you write for the person: "510(k) decisions", "recalls", "registered trials" — never
   a dataset id or a table name.

## The tools

| Need | Tool |
| --- | --- |
| The companies in the workspace | `profiles`, `profile` |
| A name → canonical identity, a code, a term | `resolve`, `lookup` |
| One company across authorizations, registrations, safety and trials | `company_footprint` |
| A listed company's financials, filings, insiders | `company_profile` (ticker or CIK) |
| A device's predicates and its chain | `device_trace` (brand, product code or K/DEN/PMA number) |
| Two to five companies side by side | `graph_compare` |
| Trials; recalls | `trials_find`, `recalls_find` |
| Passages from authorised corpora | `document_search`, `document_get` |
| The rest of a long answer | `result_page` with its `continuation.next_cursor` |
| Memory of the company | `kept` (`store`, `recall`, `forget`) |
| Deliverables | `workflows`, `workflow_start`, `workflow_run`, `workflow_step`, `workflow_answer`, `workflow_mail` |
| Standing deliverables | `watches`, `watch_start`, `watch_stop` |
| The agent | `ask_agent`, `agent_answer` |

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

`workflows` returns each with its deliverable, steps, the inputs already filled from the profile, and whether the plan runs
it; a workflow marked `readsProduct` starts from one of the profile's products and refuses with none.

## A typical turn

```
profiles → profile                       who we work for, what is kept
resolve kind=company "Shockwave"         → the UUID
company_footprint <uuid>                 → [read dr_…] clearances, registrations, recalls, trials
recalls_find firm=[<uuid>] …             → [read dr_…]
kept store "…" sources=[dr_…, dr_…]      one line, cited
```

Answer in the person's words with the reads cited; offer the workflow that would take it further.
