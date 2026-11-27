# Write the Decomposition Memo

## Goal
Recommend a bounded feasibility experiment for the pilot, compare it with non-AI and tuning alternatives, and define owners, exit criteria and stop rules.

## Steps taken
1. Created [decomposition-memo.md](../decomposition-memo.md) from the module starter with all eight headings.
2. Scored three options and named the finding that would favour non-AI clean-up.
3. Replaced the dependency graph with decision dependencies, including legal review feeding the permission checks.
4. Gave each work package a responsible role, an accountable approver and an exit criterion, keeping capability apart from approval.
5. Separated blockers (with owners and clearing conditions) from risks (with likelihood, impact, mitigation and trigger).
6. Wrote the response to unavailable policy authority: record "approval pending", continue only on approval-free work, and tell the sponsor.
7. Worked through the Friday demo scenario.
8. Checked the discovery canvas: the first slice (handling SOP lookup) is unchanged, so no update was needed.

## Commands
```bash
git add docs/decomposition-memo.md docs/03-data-and-feasibility-assessment/write-the-decomposition-memo.md
git commit -m "03-data-and-feasibility-assessment: write decomposition memo"
git push
git tag module-03
git push origin module-03
```

## Results
- [docs/decomposition-memo.md](../decomposition-memo.md): options table, Mermaid dependency graph, eight work packages with exit criteria, a blockers-and-risks table, a response to unavailable policy authority, stop/continue rules, ranged estimate and the Friday demo decision.
- Blockers: no approved SOP yet, identity mapping not validated, legal review outstanding. Everything else is a managed risk.
- Recommendation: approve a 2–4 week feasibility spike for the handling-SOP lookup. Ticket tuning scores lowest and is deferred.

## Observations
- **Estimate I trust least: the 2–4 week elapsed time.** It depends on security, legal and the ops lead responding within a week, and none of them has committed. Getting a review date from each owner in writing would firm it up.
- The Friday demo shows that a deadline must not create an approval. Safe behaviours (refusals, fail-closed) can be demonstrated on synthetic data without one.