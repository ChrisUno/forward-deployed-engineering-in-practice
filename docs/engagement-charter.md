# Ask Halyard engagement charter

**Sponsor:** Hugh Jass, Halyard operations sponsor

**Security Lead:** Lena Vogel, legal lead

**SME/Domain Expert:** Tom Reyes, sales/ops coordinator

**Engineer:** Priya Nair, embedded FDE (customer-side staff member)

---

## Outcome

Reduce time finding approved operational guidance. Measure current search times for one week, then compare against time for matched tasks after deployment. Success includes both speed and answer correctness.

---

## First users

Operations staff only for initial pilot. Sales users deferred to later phase.

**Pilot workflow:** Handling SOP questions (Tom can identify current approved version for this domain).

**Example question:** "What is our demurrage policy for Felixstowe?"

---

## Scope

### In scope
- Read-only access to approved operational guidance sources
- Grounded citations on every answer
- Permission-aware retrieval (ops policies visible to sales; legal documents restricted)
- Clear "cannot answer" response when approved evidence is missing
- Escalation path to appropriate owner when answer not found

### Not in scope
- Autonomous shipment changes or issuing credits
- Legal advice or answers presented as contractual authority without source
- Fine-tuning ticket summarization model (deferred)
- MCP server (HTTP API only for first release)
- Sales users (ops only initially)
- General freight knowledge when approved evidence is missing

---

## Decision rights

**Security (Lena):** Approves all access controls, permissions, data flows, and retention policies

**Sponsor (Hugh):** Approves scope, timeline, release timing, and business outcomes  

**SME (Tom):** Approves operational guidance content accuracy and validates current policy versions

---

## Evidence gate

Before production release:
1. **SME-reviewed evaluation questions** - Tom validates answer correctness
2. **Zero permission leaks** - Lena reviews legal boundary tests
3. **Permission leak tests in evaluation set** - covers all retrieval paths
4. **Source access approved** - by customer security (Lena)

**Success criteria:**
- Answers are correct (not just liked by users)
- No permission leaks in any test scenario
- Citations present on every answer

---

## Stop conditions

Pause release immediately on:
1. Any access-control failure or permission leak
2. Unapproved external data transfer
3. Answer presented as contractual authority without source citation
4. Legal disclosure (even confirming existence of restricted document)

**Escalation on stop:**
- Engineer pauses release immediately
- Security Team (Lena) investigates and approves remediation
- Sponsor (Hugh) decides on communication and timeline

---

## Source approval and versioning

**Current state (from Tom):**
- Filename v2 convention unreliable (old files copied to new folders)
- Modification time does not indicate approval status
- Tom can identify current handling SOP for pilot
- Need owner list for other policy domains

**Requirements:**
- Do not assume modification time means approval
- Each source needs named authoritative owner
- Start with handling SOP (approved source identified)

---

## Security and data handling

**Permission boundaries (from Lena):**
- Sales must not see legal documents
- Ops policies visible to sales
- Legal has access to finance material (not vice versa)
- **Critical:** Do not reveal legal document title or snippet when denying access - even confirming existence is a disclosure

**Data flow requirements:**
- Production data to hosted model: NOT APPROVED
- Must show data flow and retention policy before external processing
- Synthetic material approved for lab/testing
- Production prompts and traces may contain confidential material - logging requires security review

---

## Handover and operations

**Service ownership (from Tom):**
- Platform team may operate post-deployment (not yet confirmed)
- Platform team must rehearse runbook before handover accepted
- Read-only operation initially
- Escalation to person is part of workflow, not a failure

---

## Open assumptions

1. **Hosting and infrastructure:** Production identity, network location, retention, data residency, and egress restrictions unconfirmed
2. **Source owner approval:** Real-data sampling requires approval from source owners
3. **Response time target:** Priya suggests "a few seconds feels good" but cannot approve SLA for all users
4. **Production timeline:** Sponsor wants something demonstrable quickly but has not approved production date or budget
5. **Model outage handling:** Distinguished from empty search results (different operational problems)

---

## Success measurement

**Before (baseline - measure for one week):**
- Time to find approved policy answers
- Frequency of "which version is current" questions (Priya: "several per day")
- Example: 15 minutes to resolve temperature-sensitive shipment handling policy question

**After:**
- Time for matched tasks
- Answer correctness (not just user satisfaction)
- Comparison against baseline for same question types

