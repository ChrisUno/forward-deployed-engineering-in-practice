# Ask Halyard discovery canvas
## Users and jobs
- [Fact] Halyard Freight has about 600 staff in Rotterdam, Felixstowe and Singapore. (HF-BRIEF-01)
- [Fact] The proposed first users are sales and ops staff. (HF-BRIEF-01)
- [Claim] Their job is to find the current approved guidance for a specific task, such as which handling policy applies to a temperature-sensitive shipment. (HF-INT-01, Priya)
- [Claim] Questions like this come up "several" times a day. The volume hasn't been counted. (HF-INT-01, Priya)
- [Claim] Staff currently interrupt colleagues to confirm which version is authoritative. (HF-BRIEF-01; HF-INT-01, Priya)

## Current workflow and baseline
- [Claim] Current workflow: search the shared drive, find several candidate documents (two SOP PDFs and an incident note), then ask the ops lead which one is current. (HF-INT-01, Priya)
- [Claim] One lookup takes about fifteen minutes. This was not timed and is not a baseline. (HF-INT-01, Priya)
- [Decision (proposed)] Measure the baseline over one week on matched tasks, recording both time and answer correctness, not satisfaction alone. (HF-INT-01, Priya's suggestion)
- [Decision (proposed)] The baseline study measures the workflow, not individuals. No staff rankings and no unnecessary personal data. (Module guidance)

## Wrong-answer cost
- [Claim] Operational error: applying an outdated or wrong handling policy to a shipment. (HF-INT-01, Tom)
- [Claim] Confidential disclosure: sales seeing legal material, including document titles, snippets or even confirmation that a litigation note exists. (HF-INT-01, Lena)
- [Fact] Rates and contract terms can have financial consequences, so a misquoted rate is a financial risk. (HF-BRIEF-01)
- [Claim] Treating an incident record as policy is an error. Incidents describe one event and are not general authority. (HF-INT-01, Tom)
- [Claim] An answer presented as contractual authority without a source is a reason to stop a release. (HF-INT-01, Lena)

## First slice and exclusions
- [Decision (proposed)] First slice: one approved ops policy lookup, using the current handling SOP that Tom can identify, with a candidate question such as "What is our demurrage policy for Felixstowe?" (HF-INT-01, Tom and Priya)
- [Claim] A useful answer gives the current approved policy, a page reference, and a clear statement when the documents don't answer the question. (HF-INT-01, Tom)
- [Claim] If no approved evidence is found, the assistant says it can't answer from the sources available and refers the user to the right owner. It doesn't fall back on general freight knowledge. (HF-INT-01, Tom)
- [Decision] Read-only: no shipment changes, credits or compensation decisions. (HF-BRIEF-01; HF-INT-01, Tom)
- [Decision] Excluded: autonomous external messages and legal advice. (HF-BRIEF-01)
- [Decision (proposed)] Deferred: account-specific rate-card questions (for example, ACME-0042), the MCP server, and the ticket-summarisation model. (HF-BRIEF-01, which describes these as long-term goals rather than first-slice scope)
- [Claim] One reliable workflow is preferred over many polished guesses. (HF-INT-01, Priya)

## Systems and data owners
- [Fact] Systems in scope: read-only CRM (accounts, contacts, shipments, opportunities), `lab/shared-drive/` team folders, and `lab/tickets.jsonl`. (HF-BRIEF-01)
- [Fact] Document types: contracts, SOPs, incident reports, spreadsheet rate cards and policies. Duplicates, superseded versions and sensitive legal documents are expected. (HF-BRIEF-01)
- [Claim] Tom can identify the current handling SOP for the pilot. Owners for the other documents are still pending. (HF-INT-01, Tom)
- [Assumption] A filename ending in "v2" means a newer version. This is unreliable, because teams copy old files into new folders. (HF-INT-01, Tom)
- [Decision] A file's modification time does not prove approval. Authority comes from a named owner. (HF-INT-01, Tom)
- [Claim] Operations ownership: the platform team *may* run the service but hasn't agreed to. (HF-INT-01, Tom)
## Success hypothesis
- [Assumption] Correct, cited answers to the pilot policy question will reduce lookup time on matched tasks compared with the measured baseline, without lowering correctness.
- [Assumption] Escalation to a person is a valid outcome and counts as success when the evidence is missing. (HF-INT-01, Tom)
- [Fact] No production date, budget or service-level target has been approved. This hypothesis is not a delivery commitment. (HF-BRIEF-01)
- [Claim] "A few seconds" of response time would feel good, but no number has been approved. (HF-INT-01, Priya)


## Constraints and approvals
- [Claim] Sending documents to a hosted model is not approved. The data flow and retention policy must be shown first. (HF-INT-01, Lena)
- [Claim] Production prompts and logs may contain confidential material, so logging is part of the legal review. (HF-INT-01, Lena)
- [Claim] Access rules: sales can't see legal material. Ops policies can be visible to sales. Legal can see finance material, but finance can't see legal. (HF-INT-01, Lena)
- [Claim] A denied response must not reveal a legal document's title or snippet. (HF-INT-01, Lena)
- [Claim] Legal will review the legal boundary tests, not model benchmarks. (HF-INT-01, Lena)
- [Fact] Production identity, network location, retention, data residency and outbound data rules are all unconfirmed. (HF-BRIEF-01)
- [Fact] Source owners must approve any sampling of real data. The lab uses generated data with seed 20261103. (HF-BRIEF-01)
- [Claim] Reasons to stop a release: any permission leak, any unapproved external data transfer, or an unsourced answer presented as contractual authority. (HF-INT-01, Lena)
- [Claim] A model outage and an empty search are different operational problems and must be handled separately. (HF-INT-01, Tom)

## Questions to validate
Owner, evidence needed, due date, consequence if unanswered.

## Exercise 1 Question 3

We recommend the first pilot workflow be a single read-only lookup: "Which
handling policy applies to a temperature-sensitive shipment?" answered from the one handling SOP that Tom Reyes confirms as current (HF-INT-01).
 This is the only candidate grounded in an observed recent event (Priya's lookup) and backed by a named authority.  Ops policies may be visible to sales (HF-INT-01, Lena), so the access risk is low.  The source set includes two SOP PDFs and an incident note,
which tests the hard behaviours: choosing the approved version, refusing to treat an incident as policy, citing a page, and saying "I can't answer from the accessible sources" with a referral to the owner when the evidence is missing. 
The pilot stays read-only, gives no legal advice and uses local-first or synthetic data only, because hosted transfer is not approved (HF-INT-01, Lena). Success is judged against a measured one-week baseline of matched tasks, covering time and correctness, not against the unmeasured fifteen-minute estimate.

The demurrage question for Felixstowe is the next candidate once a policy owner is named. The account-specific rate-card question (ACME-0042) needs more feasibility work before it is a pilot. It joins read-only CRM account data with spreadsheet rate cards, so retrieval must handle tables and account matching, not just policy text. Rates and contractual terms have financial consequences (HF-BRIEF-01), and no owner has been identified to confirm which rate card is current. 
Account data also makes permission filtering harder than for a shared ops policy. We will keep it in the question log, naming the owner, the evidence needed and the decision it affects, rather than adding it to the first slice.