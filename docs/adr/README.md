# Architecture Decision Records

ADRs record significant design decisions for SASD Moschus. They preserve not
only the result but also the problem, constraints, alternatives and
consequences.

## 1. When an ADR is required

Create an ADR when a decision:

- changes dependency direction or component boundaries;
- defines a public API, ABI, identifier or schema;
- selects a compiler/language/platform baseline;
- establishes ownership, error, stream or resource contracts;
- changes security or trust boundaries;
- affects more than one format or language implementation;
- is costly to reverse;
- resolves a disputed interpretation with project-wide effect;
- introduces a major dependency or packaging model.

Routine local implementation choices do not need an ADR unless they become a
project-wide precedent.

## 2. Status lifecycle

```text
Proposed -> Accepted -> Superseded
       \-> Rejected
```

- **Proposed:** open for review; not yet binding.
- **Accepted:** binding for affected implementation.
- **Rejected:** considered and not selected; retained for context.
- **Superseded:** replaced by a named later ADR; retained unchanged.

An accepted ADR may be amended only for typographical corrections that do not
change meaning. New evidence or changed direction creates a new ADR.

## 3. Numbering and filenames

Use four digits and a concise lowercase slug:

```text
0001-architecture-boundaries.md
0002-retro-compiler-matrix.md
```

Numbers are assigned sequentially and never reused, including rejected ADRs.
The title inside the document starts with `ADR-NNNN:`.

## 4. Decision process

1. Copy `ADR-TEMPLATE.md` and assign the next number.
2. State the problem without assuming a solution.
3. Link requirements and architecture rules.
4. List constraints and measurable decision criteria.
5. Describe realistic alternatives, including status quo.
6. Evaluate security, portability, historical accuracy, maintenance and
   migration consequences.
7. Record unresolved evidence and validation plan.
8. Request review.
9. Mark Accepted/Rejected with date and decision owner.
10. Implement in separate or clearly linked commits and add tests.

## 5. ADR index

| ADR | Title | Status | Decision date | Superseded by |
|---|---|---|---|---|
| ADR-0001 | Schichten, Registry, Diagnosen und API-Grenzen | Planned | — | — |
| ADR-0002 | Compiler-, DOS- und Speichermodellmatrix | Planned | — | — |
| ADR-0003 | Textdarstellung und historische Codepages | Planned | — | — |
| ADR-0004 | Sprachneutrales Konformitätsmanifest | Planned | — | — |
| ADR-0005 | Ownership-, Allocator- und Streamverträge | Planned | — | — |
| ADR-0006 | Formatkennungen und Profile | Planned | — | — |
| ADR-0007 | Ressourcenlimitprofile | Planned | — | — |
| ADR-0008 | CLI-Schema, Statuscodes und Verlustfreigabe | Planned | — | — |
| ADR-0009 | Reproduzierbare Tags und C++-Epochenübergang | Planned | — | — |

`Planned` in this index means no numbered ADR file has yet been proposed. It is
not an ADR lifecycle status and carries no decision authority.

## 6. Review checklist

- [ ] Problem and scope are clear
- [ ] Requirements and architecture links are correct
- [ ] Alternatives are real and fairly evaluated
- [ ] Historical toolchain constraints are evidence-based
- [ ] Security and resource effects are covered
- [ ] Compatibility and migration are described
- [ ] Decision is testable
- [ ] Open questions and risks are visible
- [ ] Decision owner and date are recorded
- [ ] Follow-up tasks are identified

