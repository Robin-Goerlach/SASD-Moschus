# Governance

## 1. Purpose

This document defines how SASD Moschus makes decisions, accepts changes and
publishes support claims. It complements, but does not replace, the
requirements and architecture documents.

## 2. Roles

### 2.1 Product Owner

The Product Owner is Robin Goerlach / SASD-GmbH. The Product Owner:

- owns product scope and priorities;
- accepts or rejects Lastenheft changes;
- approves the release scope of each format epoch;
- confirms milestone and final acceptance;
- decides unresolved product-level trade-offs.

### 2.2 Maintainers

Maintainers:

- review and merge contributions;
- enforce architecture, security and evidence standards;
- maintain releases, tags and support matrices;
- decide implementation details within accepted requirements and ADRs;
- may reject claims that lack adequate specification or tests.

Initially the Product Owner may also act as maintainer.

### 2.3 Format stewards

A format steward may be designated for a family or domain. The steward:

- curates sources and open questions;
- reviews specifications and fixtures;
- checks version boundaries and coverage claims;
- does not unilaterally change project-wide architecture.

### 2.4 Contributors and reviewers

Contributors propose research, documentation, tests or code. Reviewers assess
changes against evidence, requirements and quality rules. Authorship does not
guarantee acceptance, and review authority does not justify undocumented
rejection.

## 3. Decision classes

| Decision | Owner | Required record |
|---|---|---|
| Product scope or acceptance | Product Owner | Lastenheft/change record |
| Technical requirement | Product Owner and maintainers | Pflichtenheft change |
| Cross-cutting architecture | Maintainers, Product Owner for major trade-offs | ADR |
| Format interpretation | Format steward/maintainer review | specification plus evidence |
| Coverage status | Maintainer review | tests and coverage change |
| Security response | security maintainers | private incident record and advisory |
| Release | Product Owner and release maintainer | release checklist and acceptance report |
| Routine implementation | contributor plus reviewer/maintainer | commit or pull request |

## 4. Decision process

1. State the problem and affected requirements.
2. Record evidence, constraints and alternatives.
3. Identify security, compatibility, legal and historical consequences.
4. Choose the smallest decision level that can validly decide it.
5. Document the decision before or with implementation.
6. Link tests and follow-up work.
7. Revisit only with new evidence or changed requirements.

Consensus is preferred. When timely consensus is impossible, the accountable
owner decides and documents the reasoning. Silence is not approval.

## 5. Architecture Decision Records

ADRs use the process in [`docs/adr/README.md`](docs/adr/README.md). Accepted
ADRs are not edited to conceal history. Material corrections create a new ADR
that supersedes the old one.

## 6. Coverage and support claims

No individual may promote a format status based on code alone. Status changes
require the artifacts defined by Lastenheft, Pflichtenheft and the format
coverage rules. A maintainer may lower an inaccurate status immediately and
record the missing evidence.

## 7. Direct commits and pull requests

Pull requests are the normal public contribution path. Maintainers may commit
directly to `main` when:

- the work is explicitly authorised;
- it is internally reviewed or mechanically verifiable;
- branch protection permits it;
- the change preserves a clean, bisectable history;
- the same build, test and documentation standards are applied.

Direct commits are not an exemption from reviewability. Force pushes and
rewriting published history are prohibited.

## 8. Releases and tags

Release tags are immutable. The Product Owner confirms epoch acceptance and a
release maintainer verifies the checklist in `docs/RELEASE-PROCESS.md`.

If a released defect is found, publish a new version or advisory. Never move
the old tag to make history appear correct.

## 9. Conflicts of interest

Reviewers disclose when they authored the reference implementation, control a
proprietary source, or otherwise cannot independently assess a claim. A second
review should be sought for security-sensitive, legally uncertain or broad
support changes.

## 10. Amendments

Governance changes require Product Owner approval and a documented commit. A
change may not retroactively invalidate already published licenses or rewrite
the factual record of previous decisions.

