# Q1 
| Source authority | Who is the named owner who approves the current version of each ops SOP beyond the pilot handling SOP? | Ops lead (Tom Reyes) | 2 Dec 2026 | Owner list per document family, signed off by the ops lead | Which sources may be indexed after the pilot | Index only the one SOP Tom confirms |
# Q2 
| Source freshness | How are superseded SOP versions marked or retired, and how will we know when an approved version changes? | Ops lead, with source owners | 4 Dec 2026 | Written versioning rule and a change-notification route | Re-indexing approach; whether retired versions are excluded or labelled | Treat all non-confirmed versions as unapproved; manual re-check before each demo |
# Q3 
| User identity | Which identity provider and groups define sales, ops, legal and finance users, and who maintains them? | Customer security | 4 Dec 2026 | Group-to-role mapping and test accounts for each role | How permission filtering and leak tests are written | No permission tests possible, so no access beyond synthetic lab users |
# Q4 
| Financial risk | Who approves rate cards and contract terms, and what is the cost when a quoted rate is wrong? | Sales/ops coordinator (Priya Nair), escalated to the commercial owner (to be named) | 9 Dec 2026 | Named rate-card owner; example incident or cost estimate | Whether rate-card lookup (ACME-0042) moves into a later slice | Rate cards stay out of scope |
# Q5 
| Retention | Where may prompts, retrieved snippets and traces be stored, for how long, and may any processing be hosted? | Legal lead (Lena Vogel) | 11 Dec 2026 | Approved data-flow diagram and retention policy | Model hosting (local vs hosted); logging design | Local-first only; minimal logging with no stored prompt content |
# Q6 
| Operational ownership | Will the platform team operate Ask Halyard after handover, and when can they rehearse the runbook? | Platform team lead (to be named), via sponsor | 16 Dec 2026 | Written agreement plus a scheduled runbook rehearsal | Whether a production release is planned at all | Pilot remains a supervised trial; no production handover |
# Q7 
| Baseline measurement | Which matched tasks will we time for one week, who reviews correctness, and how do we avoid monitoring individuals? | Ops lead and sales/ops coordinator | 2 Dec 2026 (start); 9 Dec 2026 (results) | Task definitions, timing rule, correctness reviewer, anonymised results | Whether any time-saving claim can be made | No savings claim; report correctness only 
# Q8 
| Pilot acceptance | What correctness rate, permission-leak result and refusal behaviour would the sponsor and legal accept for the pilot? | Sponsor (accountable); Legal lead for boundary tests | 11 Dec 2026 | Agreed acceptance criteria in writing, including zero permission leaks | Go/no-go for pilot users | Pilot cannot go to users; demo on synthetic data only 
