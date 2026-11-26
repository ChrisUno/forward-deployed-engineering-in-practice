Question 1 
# CRM 
accounts and contacts,
shipments
opportunities

# shared drive
ops SOPs
incident reports
rate cards
legal 
finance

tickets
The access-rules file
The search index
The lakehouse.

question 2

1. CRM – accounts and contacts
Field	-   Value
Source owner	-   Unknown; owner: sponsor to name CRM owner [Validate]
Format	-   API records [Fact]
Estimated volume	-   120 accounts, 400 contacts [Fact]
Update cadence	-   Unknown; owner: CRM owner. Changes available via updated_since [Fact]
Access method	-   Read-only client-credentials token, cursor pagination by (updatedAt, id) [Fact]; token never logged [Planned]
Sensitivity	-   Contacts contain personal data; access by user role still to be defined [Validate]
Authoritative-version rule	-   CRM is the system of record for account and contact data; latest non-deleted record wins [Assumption]
Deletion behaviour	-   Soft deletions [Fact]; soft-deleted records must leave the index [Planned]
Quality concerns	-   Unknown; owner: CRM owner. Possible stale contacts [Assumption]
Intended use	-   Not needed for the pilot; later, linking an account to its rate card [Decision (proposed)]
Validation status	-   Requires customer validation
Sample evidence	-   One page of accounts and one soft-deleted contact
Approval dependency	-   CRM owner and customer security approve read scope

2. CRM – shipments
Field   - 	Value
Source owner	-   Unknown; owner: ops lead to confirm [Validate]
Format	-   API records [Fact]
Estimated volume	-   2,000 shipments [Fact]
Update cadence	-   Frequent; exact rate unknown; owner: ops lead [Assumption]
Access method	-   Read-only token, cursor pagination, updated_since; must handle 429 Retry-After and 503s without duplicates [Fact / Planned]
Sensitivity	-   Customer commercial data; who may see it is not yet defined [Validate]
Authoritative-version rule	-   CRM is the authority for shipment status, never a PDF or ticket [Decision]
Deletion behaviour	-   Soft deletions; deleted shipments must not be cited [Planned]
Quality concerns	-   Changes made during a copy may be missed; retries may create duplicates [Assumption]
Intended use	-   Out of the pilot. Read-only lookups later; never changes [Decision] (HF-INT-01 Q9)
Validation status	-   Requires customer validation
Sample evidence	-   A shipment updated during a paged copy; a 503-then-retry run
Approval dependency	-   Ops lead and customer security

3. CRM – opportunities
Field	-   Value
Source owner	Unknown; owner: sales leadership (to be named) [Validate]
Format	API records [Fact]
Estimated volume	300 opportunities [Fact]
Update cadence	Unknown; owner: sales leadership
Access method	Read-only token, as above [Fact]
Sensitivity	Commercially sensitive; should not reach ops by default [Assumption]
Authoritative-version rule	CRM record is authoritative [Assumption]
Deletion behaviour	Soft deletions [Fact]; exclude from index [Planned]
Quality concerns	Unknown; owner: sales leadership
Intended use	None for the pilot [Decision (proposed)]
Validation status	Requires customer validation
Sample evidence	None until a use case exists
Approval dependency	Sales leadership and customer security

4. Shared drive – ops SOPs (ops/)

Corrected from the module's worked row using HF-INT-01.

Field	-   Value
Source owner	-   Ops lead (Tom Reyes) for the pilot handling SOP only; owners of other SOPs not yet named [Claim] (HF-INT-01)
Format	-   PDF [Fact]
Estimated volume	-   Unknown; owner: ops lead. Several SOP PDFs on the same topic exist [Claim]
Update cadence	-   Unknown; owner: ops lead
Access method	-   Read-only folder listing and file fetch [Planned]
Sensitivity	-   Readable by sales and ops [Fact] (acl.json; HF-INT-01, Lena)
Authoritative-version rule	-   Only a named owner's confirmation counts. Filename "v2", modification date and folder location are not proof [Claim] (HF-INT-01, Tom)
Deletion behaviour	-   Removed or superseded files must leave the index before the next answer [Planned / not verified]
Quality concerns	-   Superseded versions; old files copied into new folders; page text may extract badly [Claim / Assumption]
Intended use	-   Pilot: temperature-sensitive handling policy lookup [Decision (proposed)]
Validation status	-   Requires customer validation
Sample evidence	-   Current handling SOP, one superseded version, one copied duplicate
Approval dependency	-   Ops lead approves the pilot SOP; other SOPs wait for an owner list (DQ Q1)

5. Shared drive – ops incident reports (ops/)
Field	-   Value
Source owner	-   Ops lead [Assumption]
Format	-   PDF [Fact]
Estimated volume	-   Unknown; owner: ops lead
Update cadence	-   When an incident happens [Assumption]
Access method	-   Read-only fetch [Planned]
Sensitivity	-   Same folder as SOPs, so readable by sales and ops [Fact]; may mention customers [Assumption]
Authoritative-version rule	-   Never policy. An incident records one event [Claim] (HF-INT-01, Tom)
Deletion behaviour	-   Same as SOPs [Planned]
Quality concerns	-   Contains a prompt-injection PDF [Fact]; easily confused with SOPs [Claim]
Intended use	-   Excluded from policy answers in the pilot [Decision (proposed)]
Validation status	-   Requires customer validation
Sample evidence	-   The injection PDF; the incident note Priya found next to the SOPs
Approval dependency	-   Ops lead confirms classification rule

6. Shared drive – sales rate cards (sales/)
Field	-   Value
Source owner	-   Unknown; nobody named [Fact] (HF-INT-01, DQ Q4)
Format	-   Spreadsheet [Fact]; location in sales/ [Assumption]
Estimated volume	-   Unknown; owner: commercial owner (to be named)
Update cadence	-   Unknown; owner: commercial owner
Access method	-   Read-only fetch; sheet/cell extraction [Planned]
Sensitivity	-   Readable by sales [Fact]; financial consequences if wrong [Fact] (HF-BRIEF-01)
Authoritative-version rule	-   None defined. Cannot tell which rate card is current [Validate]
Deletion behaviour	-   Unknown; must drop expired rate cards [Planned]
Quality concerns	-   Multiple versions per account; citations must name sheet and cell [Assumption]
Intended use	-   Rate-card question (ACME-0042), deferred [Decision (proposed)]
Validation status	-   Requires customer validation
Sample evidence	-   One rate card with a known cell value
Approval dependency	-   A commercial owner must be named first

7. Shared drive – legal (legal/)
Field	-   Value
Source owner	-   Legal lead (Lena Vogel) [Claim]
Format	-   PDF contracts and legal notes [Fact]
Estimated volume	-   Unknown; owner: legal lead
Update cadence	-   Unknown; owner: legal lead
Access method	-   Not ingested for the pilot [Decision (proposed)]
Sensitivity	-   Legal only. Sales and finance must not see content, titles, snippets, or confirmation a document exists [Fact / Claim] (acl.json; HF-INT-01, Lena)
Authoritative-version rule	-   Unknown; owner: legal lead
Deletion behaviour	-   Unknown; must be immediate if ever ingested [Planned]
Quality concerns	-   Highly sensitive; litigation notes [Claim]
Intended use	-   None. Legal advice is out of scope [Decision] (HF-BRIEF-01)
Validation status	-   Requires customer validation
Sample evidence	-   Used only as the target of the Ana permission test (synthetic)
Approval dependency	-   Legal lead review of the access boundary (blocker before any ingestion)

8. Shared drive – finance (finance/)
Field	-   Value
Source owner	-   Unknown; owner: finance lead (to be named) [Validate]
Format	-   Unknown; owner: finance lead
Estimated volume	-   Unknown; owner: finance lead
Update cadence	-   Unknown; owner: finance lead
Access method	-   Not ingested for the pilot [Decision (proposed)]
Sensitivity	-   Readable by finance and legal; not by sales or ops [Fact] (acl.json)
Authoritative-version rule	-   Unknown; owner: finance lead
Deletion behaviour	-   Unknown
Quality concerns	-   Unknown
Intended use	-   None for the pilot
Validation status	-   Requires customer validation
Sample evidence	-   None
Approval dependency	-   Finance lead and customer security

9. Support tickets (lab/tickets.jsonl)
Field	-   Value
Source owner	-   Unknown; owner: support lead (to be named) [Validate]
Format	-   JSON Lines [Fact]
Estimated volume	-   1,500 records [Fact]
Update cadence	-   Static export [Fact]; production cadence unknown
Access method	-   File read [Planned]
Sensitivity	-   Likely personal data [Assumption]; retention unknown [Fact] (HF-BRIEF-01)
Authoritative-version rule	-   Never authoritative for policy or instructions; patterns and summaries only [Decision]
Deletion behaviour	-   Unknown; retention policy needed (DQ Q5)
Quality concerns	-   Missing resolutions, label quality unknown [Assumption]
Intended use	-   Later ticket summariser, deferred [Decision (proposed)]
Validation status	-   Requires customer validation
Sample evidence	-   Tickets with and without resolutions; one with personal data
Approval dependency	-   Legal (retention) and support lead

10. Access rules (lab/shared-drive/acl.json)
Field	-   Value
Source owner	-   Customer security [Assumption]
Format	-   JSON [Fact]
Estimated volume	-   4 teams, 5 named lab principals [Fact]
Update cadence	-   Unknown; production identity source not confirmed [Fact] (HF-BRIEF-01)
Access method	-   Read at index and query time; filter applied inside the search query [Planned]
Sensitivity	-   Defines who sees what; tampering would leak data
Authoritative-version rule	-   Lab: acl.json. Production: identity provider groups (unconfirmed) [Validate] (DQ Q3)
Deletion behaviour	-   A removed membership must take effect on the next query [Planned]
Quality concerns	-   Folder-level only; a missing or unknown principal must return nothing (fail closed) [Decision]
Intended use	-   Enforce permissions for every retrieval
Validation status	-   Lab file supplied; production mapping requires customer validation
Sample evidence	-   Priya (sales+ops), Ana (sales), Tom (ops), Lena (legal), Omar (finance), and one unknown user
Approval dependency	-   Customer security validates mapping; legal reviews boundary tests

11. Search index (PostgreSQL + pgvector), derived
Field	-   Value
Source owner	-   Engineering during pilot; platform team after handover (not agreed) [Claim] (HF-INT-01, Tom)
Format	-   Passages with source, page, version and ACL metadata [Planned]
Estimated volume	-   Pilot: one SOP and its samples [Planned]
Update cadence	-   Rebuilt when an approved source changes [Planned]
Access method	-   Query with the requesting principal's groups in the same query [Planned]
Sensitivity	-   Holds copies of source text, so inherits the strictest sensitivity of what it holds
Authoritative-version rule	-   Never authoritative itself; points back to the source
Deletion behaviour	-   Source deletion or supersession removes passages [Planned / not verified]
Quality concerns	-   Stale passages if deletions don't propagate
Intended use	-   Pilot retrieval
Validation status	-   Planned
Sample evidence	-   Re-run on unchanged input produces identical passages
Approval dependency	-   Legal review of what is stored and for how long (DQ Q5)

12. Lakehouse (./lakehouse bronze/silver/gold), derived
Field	-   Value
Source owner	-   Engineering [Assumption]
Format	-   DuckDB / DuckLake tables [Fact]
Estimated volume	-   Unknown; owner: engineering
Update cadence	-   Unknown; owner: engineering
Access method	-   Analytics and replay only [Decision]
Sensitivity	-   Copies of record data; not a permission authority [Decision]
Authoritative-version rule	-   Bronze keeps lineage back to source; never the source of truth for answers
Deletion behaviour	-   Unknown; deletions must flow through all three layers [Planned]
Quality concerns	-   Extra copies widen the exposure for personal data
Intended use	-   Not required for the pilot policy lookup [Decision (proposed)]
Validation status	-   Planned
Sample evidence	-   None for the pilot
Approval dependency	Legal (retention) before holding any real data

Question 3
Concentrate on four fields: sensitivity, the rule for which version is authoritative, deletion behaviour and who must approve.

## What the inventory tells us
1. **Row 6 – Rate cards.** Nobody owns the current version, and answers would need sheet-and-cell citations with financial consequences. **Decision:** rate-card lookup stays out of the first slice until a commercial owner is named (DQ Q4).
2. **Row 5 – Ops incident reports.** They sit in the same `ops/` folder as SOPs, are readable by sales, are not policy, and one contains prompt injection. **Decision:** classify by document type, not folder; exclude incidents from policy answers in the pilot, and make the injection sample a blocker test.
3. **Row 10 – Access rules.** The lab ACL is folder-level and production identity is unconfirmed. **Decision:** the pilot runs on synthetic lab principals only, fails closed for unknown users, and can't reach real users until security validates the mapping (DQ Q3).

## Sample selection
| Sample | Why it matters | Result needed to proceed | If it fails: blocker or risk? |
|---|---|---|---|
| One current approved SOP | The pilot's main source | Text and page numbers extract correctly | **Blocker**: no usable source, no pilot |
| A superseded SOP version | Old guidance must not be served as current | Marked superseded and excluded from answers | **Blocker**: would serve outdated policy |
| Duplicate bytes under different filenames | The same content stored twice | Counted as one source | **Risk**: duplicate citations, no leak |
| A spreadsheet rate card | Answers must cite sheet and cell | Cell citation is correct | **Risk**: rate cards out of the pilot |
| An unsupported file | Some formats can't be read | Explicit "unsupported" verdict, not silence | **Risk**: tolerable if logged visibly |
| An oversized input | Very large files strain the pipeline | >250 MB profile-only; >2 GB rejected | **Risk**: handled by size rules |
| Incident PDF with "Ignore previous instructions…" | Prompt injection inside a valid file | Treated as data; behaviour and access unchanged | **Blocker**: could cause a leak |
| Ana (sales) asks for legal content | Permission boundary | Nothing returned, not even a title or "access denied to X" | **Blocker**: any leak stops release |
| Unknown or missing principal | Fail closed | Empty result | **Blocker**: open access by default |