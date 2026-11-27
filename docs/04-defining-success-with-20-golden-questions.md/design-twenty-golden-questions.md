# Design Twenty Golden Questions

## Goal
Define what "working" means for Ask Halyard before anything is built: twenty reviewable golden cases with owners, eligible metrics, pass types and severity, plus thresholds, scoring and a freeze strategy, without inventing any policy answers.

## Steps taken
1. Created [eval-plan.md](../eval-plan.md) and pasted the module's twenty case designs under `## Golden cases`.
2. Replaced principal names with lab test emails, keeping the team in brackets.
3. Added five columns. Every locator reads "blocked gold, owner: …" because no approved documents exist.
4. Classified each case's eligible metrics, pass type and severity, and counted the denominators (R = 20, D = 9, C = 15, L = 20).
5. Wrote detailed records for G02 (grounded answer), G13 (abstention) and G17 (tool use).
6. Designed G21 (permission revocation), marked as proposed and not in the frozen set.
7. Added the four thresholds unchanged, with denominator rules, then the Scoring and Dataset freeze sections.

## Commands
```bash
git add docs/eval-plan.md docs/04-defining-success-with-evals/design-twenty-golden-questions.md
git commit -m "04-defining-success-with-evals: design twenty golden questions"
git push
```

## Results
- [docs/eval-plan.md](../eval-plan.md): 20 classified cases, 3 detailed records, proposed G21, thresholds, scoring and dataset freeze.
- 7 cases block release on failure (G04, G05, G07, G08, G09, G10, G17); the other 13 count towards thresholds.
- 20/20 cases are blocked gold pending owner review, so `retrieved_expected_doc` and `answer_correct` can't be scored yet.

## Observations
- **Hardest case to classify: G19** (summarise an unresolved ticket). It reads like a grounded answer, but the key behaviour is refusing to invent a resolution. I classed it as abstention, because the failure we fear is invention, not a missing citation.
- G02 and G18 test two of Halyard's worst failures (obsolete policy, outage reported as "no document") but only count towards thresholds. I'd ask the sponsor whether either should block release.
- All gold is blocked, so the plan is a contract for review, not a scoreable test yet.