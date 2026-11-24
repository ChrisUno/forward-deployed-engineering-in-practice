# Role boundaries and decision rights

## Context
This document defines who performs work and who approves decisions across the Ask Halyard engagement. It distinguishes execution responsibility from approval authority.

## Roles

**Sponsor** (Hugh Jass, Halyard operations sponsor)
- Approval authority for scope, timeline, and business outcomes
- Final decision on go/no-go for releases
- Budget and resource allocation

**Engineer** (Eileen Dover, embedded FDE)
- Execution of technical work
- Discovery, implementation, testing, and documentation
- Escalation of blockers and risks

**Security Team**
- Approval authority for all access controls and permissions
- Review of security architecture and data flows
- Incident response coordination

**SME/Domain Expert** (approval pending identification)
- Approval authority for operational guidance content
- Validation of question/answer accuracy
- Review of business logic correctness

---

## Decision matrix

| Activity | Responsible (does the work) | Accountable (approves) | Status |
|----------|----------------------------|------------------------|---------|
| **Discovery** | Engineer | Sponsor | Active |
| **Source approval** | Engineer proposes sources | SME/Domain Expert validates content accuracy | Approval pending SME identification |
| **Deployment** | Engineer executes deployment | Sponsor approves release timing<br>Security approves access controls | Active |
| **Incident response** | Engineer triages and mitigates | Security Team approves containment actions<br>Sponsor approves communication | Active |
| **Acceptance** | Engineer demonstrates functionality | Sponsor accepts business outcomes<br>SME validates content correctness | Approval pending |

---

## Approval checkpoints

### Source approval
- **Who approves**: SME/Domain Expert (approval pending identification)
- **What they approve**: Accuracy and authoritativeness of operational guidance sources
- **When**: Before sources are used to answer user questions
- **Criteria**: Source is current, accurate, and matches Halyard operational policy

### Deployment approval
- **Who approves**: 
  - Security Team (access controls and permissions)
  - Sponsor (release timing and scope)
- **What they approve**: 
  - Zero permission leaks (Security)
  - Feature completeness against charter (Sponsor)
- **When**: Before production release
- **Criteria**: Evidence gate passed (SME-reviewed questions and zero permission leaks)

### Acceptance approval
- **Who approves**: 
  - Sponsor (business outcomes)
  - SME (content accuracy)
- **What they approve**: Solution meets outcome criteria in charter
- **When**: After deployment to first users
- **Criteria**: Time reduction measured against baseline; SME validates answer quality

### Incident response approval
- **Who approves**: 
  - Security Team (containment and remediation actions)
  - Sponsor (communication and business impact decisions)
- **What they approve**: Response actions that affect service availability or data access
- **When**: Upon detection of access-control failure or security incident
- **Criteria**: Stop condition triggered (pause release on any access control failure)

---

## Escalation paths

### Access control failure
1. Engineer detects failure
2. Engineer immediately pauses release
3. Security Team investigates and approves remediation
4. Sponsor decides on communication and timeline

### Content accuracy concern
1. Engineer or user identifies incorrect guidance
2. Engineer disables affected content
3. SME validates correction (approval pending identification)
4. Engineer redeploys after approval

### Scope change request
1. Engineer documents requested change
2. Sponsor approves or rejects scope change
3. If approved, Engineer executes; if security-related, Security Team also approves

---

## Notes

- **Invented approvals are not permitted**: Where approval authority is uncertain, this document states "approval pending" and identifies the gap.
- **Separation of execution and approval**: The person doing work does not approve their own work.
- **Fictitious titles are acceptable**: Role names may be generalized (e.g., "SME") but approval authority must map to real people once identified.
