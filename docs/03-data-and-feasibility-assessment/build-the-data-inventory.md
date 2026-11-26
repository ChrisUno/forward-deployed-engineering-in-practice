# Build the Data Inventory

## Goal
Assess the fictional Halyard estate source by source, without inventing profiling results, and decide which sources are safe to use for the first pilot.

## Steps taken
1. Listed every source from HF-BRIEF-01 and the module's lab targets, splitting the CRM and shared drive by entity, folder and sensitivity, to get 12 rows in [data-inventory.md](../data-inventory.md).
2. Filled all thirteen fields per row, using "Unknown; owner: …" where the sources say nothing, and labelled every value.
3. Corrected the module's worked ops-SOP row against HF-INT-01: Tom only owns the pilot SOP; filename, date and folder are not proof; incident reports in the same folder are not policy.
4. Spent most effort on sensitivity, authoritative-version rule, deletion behaviour and approval dependency.
5. Wrote three findings, each tied to a decision.
6. Built the sample-selection table, adding the injection PDF, Ana's permission test and an unknown principal, and marked each as blocker or risk.

## Commands
```bash
git add docs/data-inventory.md docs/03-data-and-feasibility-assessment/build-the-data-inventory.md
git commit -m "03-data-and-feasibility-assessment: build data inventory and sample plan"
git push
```

## Results
- [docs/data-inventory.md](../data-inventory.md): 12 sources × 13 fields, three findings and a sample plan with nine samples.
- Findings: rate cards deferred (no owner); incident reports excluded from policy answers (injection and authority); pilot limited to synthetic principals until identity is validated.

## Observations
- **Source I would refuse to ingest today: `legal/`.** Legal hasn't reviewed the access boundary, the pilot doesn't need it, and even a leaked title counts as disclosure (HF-INT-01, Lena). Ingesting it would create risk with no benefit.
- The ops folder mixes SOPs and incident reports, so folder-based classification is not enough. Document type must be classified.
- Most "Unknown" values are owned by people not yet named. Naming owners is the first piece of feasibility work.