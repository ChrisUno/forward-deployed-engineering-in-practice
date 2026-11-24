# Role boundaries and decision rights

Question 1;
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

**Security Team**(John Cena, Halyard Security Lead) -Approval Pending
- Approval authority for all access controls and permissions
- Review of security architecture and data flows
- Incident response coordination

**SME/Domain Expert** (Mike Hawk, DevOps Engineer) 
- Approval authority for operational guidance content
- Validation of question/answer accuracy
- Review of business logic correctness

### Responsibility table

| Activity | Responsible (does work) | Accountable (approves) |
|----------|------------------------|------------------------|
| Discovery | Engineer | Sponsor |
| Source access/approval | Engineer | SME/Domain Expert |
| Deployment | Engineer | Sponsor + Security Team |
| Incident response | Engineer | Security Team + Sponsor |
| Acceptance | Engineer | Sponsor + SME |

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
- **Who approves**: SME/Domain Expert
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
Question 2;
Explain what scope you remove if capacity halves, and which safety gates remain.

## Capacity-reduction decision

Answer; Keep the user outcome and narrow the scope around it. Remove or hide features, not safeguards.

### Scope removed or deferred (in this order)

| Order | Item | Why it goes first |
|---|---|---|
| 1 | MCP server | A second integration surface; the HTTP API alone serves first users |
| 2 | Ticket-summarisation model | Separate capability with its own evaluation and data-approval cost |
| 3 | Sales users | Start with operations only: one workflow, one SME group, one set of permissions |
| 4 | Lower-priority sources | Limit to sources with a named authoritative owner and approved access |
| 5 | UI polish and extra demo scenarios | No effect on correctness or safety |

### Safety gates that remain (non-negotiable)

| Gate | Owner (accountable) | Why it stays |
|---|---|---|
| Permission filtering on every retrieval path | Halyard Security (approval pending) | A leak is a release-blocking failure, not a missing feature |
| Permission leak tests in the evaluation set | FDE (responsible), Security (accountable) | Without them, a leak can go unnoticed |
| SME-reviewed evaluation questions | Operations lead (approval pending) | The only evidence that answers are correct |
| Citations on every answer | FDE | Lets users verify guidance and stops answers being invented |
| Pause release on access-control failure | Sponsor (approval pending) | The escalation rule from the charter is unchanged |
| Source access approved by customer security | Halyard Security | Decision rights don't move because time is short |

### Communication

The reduction is stated in writing to the sponsor, with the deferred items
listed as a backlog. Nothing is removed silently.

### Tension check

- **Sponsor (speed):** gets a smaller release sooner, for one user group.
- **Legal (confidentiality):** all permission controls and leak tests stay.
- **Operations (reliability):** the narrower scope makes the system easier to
  run and support.

# Goal
To discover roles, their boundaries, responsibilities and decison abilities.

# Steps taken
1. Create tables clearly defining roles, owners, abilities and ask for approval from client
2. Write escalation paths for each role for clarity.
3. Write acceptance approval paths
4. answer questions under steps section

# Commands
git add .
git commit -m "01-the-forward-deployed-engineer-role: role boundaries"
git push
git tag module-01
git push origin module-01

# Results
tables created above in markdown, not the prettiest but readable.

# Observations
A template of reply tends to be used for every client contact; pleasant, positive but options provided and discovery of source issue.
