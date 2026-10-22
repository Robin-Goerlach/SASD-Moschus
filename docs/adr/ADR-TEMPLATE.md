# ADR-NNNN: [Decision title]

| Field | Value |
|---|---|
| Status | Proposed |
| Date proposed | YYYY-MM-DD |
| Date decided | — |
| Decision owners | [roles/names] |
| Scope | [components/formats/epochs] |
| Related requirements | [LAS/Pflichtenheft references] |
| Related architecture | [ARC IDs/sections] |
| Supersedes | None |
| Superseded by | None |

## 1. Context

Describe the problem, why a decision is needed now and what happens if no
decision is made. Separate facts from assumptions.

## 2. Decision drivers

- [correctness requirement]
- [security/resource requirement]
- [historical compiler/platform constraint]
- [compatibility/maintainability requirement]
- [testability/reproducibility requirement]

Rank drivers when they conflict.

## 3. Constraints and evidence

| ID | Constraint/evidence | Source or test | Confidence |
|---|---|---|---|
| C-1 | [item] | [reference] | confirmed/probable/open |

Include actual compiler/version experiments for toolchain decisions. Do not
treat memory or modern compiler behaviour as evidence for a historical target.

## 4. Considered options

### Option A — [name]

Description.

Advantages:

- …

Disadvantages and risks:

- …

### Option B — [name]

Description, advantages and disadvantages.

### Option C — Status quo / defer

Explain the cost and safety of postponement.

## 5. Decision

State the selected option precisely. Define:

- public and internal boundaries;
- defaults and mandatory behaviour;
- prohibited alternatives;
- version/platform applicability;
- conditions that would trigger reconsideration.

For a Proposed ADR this section contains the recommendation and remains
non-binding until status becomes Accepted.

## 6. Consequences

### Positive

- …

### Negative

- …

### Neutral or operational

- …

## 7. Security and resource impact

Describe trust boundaries, failure modes, limits and required negative tests.
Write “No additional impact” only with a reason.

## 8. Compatibility and migration

Cover:

- existing source/API/ABI/data compatibility;
- old compiler and platform effects;
- format and language epoch separation;
- deprecation path;
- rollback or escape hatch.

## 9. Validation plan

List builds, tests, prototypes and acceptance evidence that prove the decision
works.

| Validation ID | Check | Expected result |
|---|---|---|
| V-1 | [test/build] | [result] |

## 10. Implementation plan

1. [small step]
2. [small step]
3. [documentation/test step]

Implementation commits link this ADR but do not rewrite its historical
reasoning.

## 11. Open questions

| ID | Question | Owner | Due before |
|---|---|---|---|
| O-1 | [question] | [role] | [milestone] |

An Accepted ADR should have no unresolved question that changes the selected
option's meaning.

## 12. References

- [requirements]
- [architecture]
- [standards/source notes]
- [prototype/test results]

## 13. Decision record

On acceptance or rejection record:

- decision and final status;
- date;
- decision owner(s);
- concise rationale;
- dissent or material reservation;
- follow-up issue/commit links.

