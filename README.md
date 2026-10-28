# Implications of AI and Big Data

By Jay Bennett · Oct 28, 2026

## 1. The shift

Big data made it cheap to store and count everything; AI makes it cheap to understand it. Together they turn data from a record of what happened into a system that reads, decides and acts.

| Era | Core question | Bottleneck |
| --- | --- | --- |
| Reporting (1990s–2000s) | What happened? | Getting data into one warehouse |
| Big data (2010s) | What happened, at scale? | Storage and compute |
| Machine learning (late 2010s) | What will happen? | Labeled data and specialist talent |
| AI on big data (now) | What does it mean, and what should we do? | Trust, cost and governance |

The bottleneck has moved from technology to judgment: the hard part is no longer computing an answer but knowing whether to believe it.

## 2. Work and skills

AI moves the scarce skill from writing code to specifying problems and checking answers. Routine implementation shrinks; architecture, data modeling and evaluation grow.

| Role | What shrinks | What grows |
| --- | --- | --- |
| Data engineer | Hand-written ETL, boilerplate SQL | Architecture, data contracts, cost control, AI pipelines |
| Analyst | Pulling data, building pivot tables | Framing questions, judging AI output, storytelling |
| Data scientist | Feature engineering by hand | Evaluation design, causal reasoning, model risk |
| Business user | Waiting on IT tickets | Self-serve answers through SQL AI functions and chat interfaces |
| Manager | Status reporting | Deciding what to automate and owning the outcome |

The risk is a hollowed-out middle: juniors who never learn fundamentals because AI writes the first draft. Teams that pair AI speed with deliberate review and training keep their bench strong.

## 3. Data becomes the moat

When anyone can rent the same model, the advantage moves to the data only you have and how well it is organized.

- **Unstructured data wakes up.** Emails, contracts, call transcripts, tickets and PDFs — most of an organization's information — were effectively dark. AI turns them into queryable columns.
- **Proprietary context beats bigger models.** A smaller model with your clean, well-labeled history often outperforms a frontier model with none.
- **Data quality debt comes due.** Duplicates, missing lineage and inconsistent definitions used to slow reports; now they produce confident wrong answers at scale.
- **Metadata matters as much as data.** Catalogs, definitions and access rules are what let AI find and use the right table.

The practical implication: investment in data modeling and governance, long seen as overhead, becomes the main source of AI advantage.

## 4. Architecture: AI moves to the data

The old pattern exported data to a separate ML stack. The new pattern brings models to where data already lives.

| Layer | Before | Now |
| --- | --- | --- |
| Storage | Proprietary warehouse formats | Open lakehouse: Apache Iceberg tables over Parquet |
| Compute | One engine per team | Many engines on the same tables (Spark, Trino/Starburst, Snowflake, DuckDB) |
| AI | Separate Python services | SQL scalar functions (`AI_CLASSIFY`, `ai_query`), vector search, agents with tool access |
| Movement | Batch copies between systems | Federation and streaming (Kafka) instead of copies |
| Interface | Dashboards and tickets | Natural-language questions answered over governed data |

Three consequences follow. Fewer copies means less exposure and less reconciliation. Open formats mean engines compete for your workload instead of owning your data. And every query can now carry a model call, so architecture decisions become cost and risk decisions.

## 5. Economics

AI changes data costs from mostly fixed to mostly variable, and shifts who captures the value.

- **Cost scales with rows × tokens.** A query that cost cents can cost thousands when it calls a model on every row. FinOps for AI becomes a core discipline: filter first, cache results, choose the smallest model that passes evaluation.
- **Marginal cost of analysis falls toward zero.** Questions that were never worth an analyst's day become worth asking, so demand for answers rises.
- **Value concentrates at three points:** owners of unique data, owners of compute and models, and teams that turn both into decisions. Generic middleware and manual reporting get squeezed.
- **Build vs. buy tilts to assemble.** Most organizations will compose hosted models, open table formats and their own data rather than train models themselves.

The winners measure cost per decision, not cost per query.

## 6. Privacy, security and governance

AI makes data more useful and more dangerous at the same time: it can find, combine and infer facts no one intended to expose.

| Risk | How AI and big data amplify it | Control |
| --- | --- | --- |
| Re-identification | Models link "anonymous" records across datasets | Minimize fields, aggregate, test for linkage |
| Inference | Models infer health, finances or beliefs from innocuous data | Restrict sensitive inferences by policy, not just columns |
| Data leakage | Prompts send internal data to external APIs | In-platform models, retention terms, redaction |
| Prompt injection | Hidden instructions in documents hijack agents | Least-privilege tools, human approval for writes |
| Shadow AI | Staff paste data into consumer tools | Approved tools that are easier than the workaround |

Governance shifts from "who can see this table" to "what can be done with it, by which model, for what purpose."

## 7. Trust: reproducibility, bias and accountability

Traditional data systems give the same answer twice. AI systems may not, and that breaks assumptions built into audits, reports and decisions.

- **Reproducibility.** Pin model versions, store prompts and outputs, and use table snapshots (Iceberg time travel) so any decision can be replayed exactly.
- **Bias at scale.** A biased rule applied by hand affects hundreds of cases; applied by a model across a warehouse, it affects millions. Test outcomes across groups before and after launch.
- **Silent errors.** A wrong AI label looks identical to a right one. Hand-labeled evaluation sets and spot checks are the equivalent of unit tests.
- **Accountability.** "The model decided" is not an answer regulators or customers accept. Every AI-driven decision needs a named human owner and a record of what the model saw.

Trust is the real bottleneck; organizations that can prove their AI outputs will be allowed to use them more.

## 8. Society and markets

The effects reach well beyond IT departments.

- **Concentration.** Training frontier models takes capital, chips and data few firms have, which concentrates power in a handful of providers. Open models and open data formats are the main counterweight.
- **Regulation.** Rules are arriving in layers: the EU AI Act's obligations phase in through 2027, US rules come mostly from sector regulators (banking model-risk guidance, healthcare, consumer protection) and state laws. Expect requirements for documentation, risk assessment and human oversight.
- **Energy and infrastructure.** AI data centers are a fast-growing source of electricity demand, which ties AI strategy to power prices, grid capacity and siting decisions.
- **Information quality.** Cheap generated content floods the same data sources future models learn from, so verified, first-party data gains value.
- **Markets.** Faster data-driven decisions shorten the window in which any information edge lasts; advantage shifts to execution and proprietary data.

None of these are reasons to wait. They are reasons to build with documentation, measurement and exit options from the start.

## 9. What to do now

A short playbook for teams putting AI on top of their data:

1. **Inventory your dark data.** List the text and document sources no one queries today; that is where AI adds the most.
2. **Standardize on open formats.** Put core tables in Iceberg/Parquet so you can switch engines and models without migrating.
3. **Enrich once, persist always.** Run AI functions in batch, store the results as tables, and never recompute them inside views.
4. **Build an evaluation set before scaling.** 100–200 hand-labeled examples per AI task, rerun on every model or prompt change.
5. **Set cost guardrails.** Budgets and alerts per job; filter before calling a model.
6. **Govern purpose, not just access.** Decide which models may use which data for which decisions, and log it.
7. **Name an owner for every AI decision.** A person who can explain what the model saw and why the result was accepted.
8. **Train people, not just models.** Teach staff to frame questions and check answers; that skill compounds.
