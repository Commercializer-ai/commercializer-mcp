# The tools

Every tool runs as you, in the workspace you approved. **Reads** change nothing. **Writes** add something (a finding, a
tool answer, a run, a watch, a question to the agent). **Removes** stop or drop something. Each tool tells your assistant which it is,
so the assistant can ask you first.

## Your workspace

| Tool | Kind | What it does |
| --- | --- | --- |
| `search` | Read | Finds what a query names in the workspace (profiles, kept findings, workflow runs) and the registry companies by that name. |
| `fetch` | Read | One `search` result in full: a profile, a kept finding with its sources, a run with its step headlines, or a registry company's footprint (a cited register read). |
| `list_profiles` | Read | Your company, the competitors it tracks, and your own profiles. |
| `get_profile` | Read | A company as you described it and the findings kept about it, with their sources and age. |

## The registers

Every answer starts with `[read dr_…]`, the id to cite and to keep a finding from.

| Tool | Kind | What it reads |
| --- | --- | --- |
| `resolve` | Read | What a name refers to: a company's canonical identity (with its family), a device, a condition, a drug, a reaction, a specialty, a place or a time. |
| `company_footprint` | Read | One company across authorisations, registrations, safety and trials. |
| `company_profile` | Read | A listed company's identity, three years of financials, recent filings and insider trades. |
| `device_trace` | Read | A device by brand, product code or K/DEN/PMA number, and its predicate chain. |
| `graph_compare` | Read | A company against up to four others: shared product codes, review panels, paid clinicians, trials. |
| `lookup` | Read | From one thing to another along the built links: a company's rivals, its product codes, the clinicians it pays, the trials it runs. |
| `trials_find` | Read | Registered trials by condition, intervention, sponsor, status, phase, dates and sites. |
| `recalls_find` | Read | FDA device recalls with their 510(k) and PMA numbers. |
| `document_search` | Read | Passages from authorised document collections. |
| `document_get` | Read | A citable passage in full. |
| `result_page` | Read | The rest of a long answer, from the cursor it gave. |
| `list_registers` | Read | Every other register by name: EU registrations, certificates and registered companies; Canadian, Australian and Chinese device registers; Japanese and Korean procedure volumes; public tenders and buyers; Medicare payment rates; hospitals and clinicians; US device listings and adverse event reports; patents, published studies, filings and holders. Asked by name, their input schemas. |
| `read_register` | Read | Runs one register from `list_registers` with its arguments. |

## What is kept

| Tool | Kind | What it does |
| --- | --- | --- |
| `recall_findings` | Read | The findings kept about a company that bear on a query; a finding the registers have revised since is marked stale. |
| `keep_finding` | Write | Keeps one finding in one line, citing the reads that show it; shown on the profile with your assistant's name. |
| `forget_finding` | Remove | Drops a kept finding that no longer holds, with the reason; the record of it stays. |

## Tools

One question answered in a minute or two, the same answer as the Tools page on commercializer.ai. Each answer starts with
`[read dr_…]`, cites its sources and names the workflows that go deeper.

| Tool | Kind | What it does |
| --- | --- | --- |
| `list_tools` | Read | Every tool, with what it answers, its inputs with the values your profile fills them with, and the workflows that go deeper; `category` narrows it to one kind. |
| `run_tool` | Write | Runs one and waits up to 45 seconds for the answer. The same inputs answered today come back at no cost. Draws on your plan's monthly agent use. |
| `get_tool_run` | Read | A tool answer that was still running: running, failed with why, or done with its rows and sources. |

### The 48 tools

| Kind | Tools |
| --- | --- |
| Patents and IP | Claim elements · Patents like mine · Patents near my products · FTO screen · New filings near me · Patent status check · Patent whitespace · Rival patents |
| Regulatory route | Product code finder · Device name finder · Predicate finder · Standards cited · Regulation search · MDR class · 510(k) change test · A company's devices, every register · What launching everywhere takes · US pathway · Where it's registered · Post-market duties · Filing checklist by market |
| Safety | Adverse events · Recalls in a code · Hazards in a code |
| Clinical evidence | Device trials · Question map · Evidence for a claim · Trial landscape · CROs and trial sites · Endpoints in use |
| Market, payment and buyers | IVF labs · What patients say · How Medicare pays · Open tenders · Who wins tenders · Who distributes in my market · Who does the procedure · Clinicians a company pays · Your lists |
| Competitors | Claims rivals can make · Who sells in my code · Rivals before revenue · Rival financials · Who owns it |
| Funding | Who's investing in my space · Is this fund still investing · Money without equity · Who to meet on a trip |

## Workflows and watches

| Tool | Kind | What it does |
| --- | --- | --- |
| `list_workflows` | Read | The workflows you can run on a profile, with what each delivers, its steps, its inputs filled from the profile and whether your plan runs it. |
| `start_workflow` | Write | Starts one; counts against your plan. |
| `get_workflow_run` | Read | A run's state, each step's headline, and the question when a step waits. |
| `get_workflow_step` | Read | One saved step in full, with its sources. |
| `answer_checkpoint` | Write | Answers a step's question with your choice; changing an answer runs only the steps it affects. |
| `note_workflow_run` | Write | A note the run reads at its next question. |
| `stop_workflow_step` | Remove | Ends the running step with what it has. |
| `list_watches` | Read | Workflows set to run again, with their last run. |
| `start_watch` | Write | Runs a workflow again every day, week or month. |
| `stop_watch` | Remove | Stops a watch; its runs stay. |

### The 31 workflows

| Pack | Workflows |
| --- | --- |
| Regulatory | Pathway decision · Submission checklist · Evidence bar · Clinical tier · Launch readiness · Change assessment · Portfolio and registration upkeep · Post-market obligations · Global lifecycle map · Safety burden · Signal watch · Competitor regulatory footprint · Similar patents |
| Commercial | Market entry · Go-to-market brief · Market whitespace · Provider targeting · Clinician and KOL map · Tender and bid watch · Patent whitespace |
| Evidence | Clinical evidence mapper · Trial map |
| Innovation | Need finding · Need sizing · Value proposition |
| Capital | Raise plan · Competitor financial watch · Acquisition and partner screen · Ownership watch |
| Programme | Company analysis · Company brief |

## The agent

| Tool | Kind | What it does |
| --- | --- | --- |
| `ask_agent` | Write | Asks Commercializer's own agent; it reads, keeps what it finds and answers within a minute or two. |
| `get_agent_answer` | Read | The answer, once it is done. |

## Prompts to start from

- *What does Commercializer hold about our company?*
- *What clearances and recalls does our closest competitor hold, register by register?*
- *Which US pathway fits our device, and which predicates would we lean on?*
- *Which public tenders are open for our device in France and Germany, and who usually wins them?*
- *Compare our regulatory footprint with our two closest competitors and keep what matters.*
- *Which trials are recruiting for our indication in Europe, and who sponsors them?*
- *Run a market entry workflow for Germany and the UK on our lead product.*
- *Set a weekly signal watch on our product code.*
