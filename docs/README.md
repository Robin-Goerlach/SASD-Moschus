# SASD Moschus documentation

This directory contains project-wide guidance, research notes and templates.
The root documents define product and architecture policy; files below `docs/`
support implementation and verification.

## 1. Document map

### 1.1 Product and technical baseline

| Document | Purpose |
|---|---|
| [Lastenheft](../LASTENHEFT.md) | What Moschus must deliver and why |
| [Pflichtenheft](../PFLICHTENHEFT.md) | How the agreed requirements are implemented |
| [Architecture](../ARCHITECTURE.md) | System boundaries, components and technical rules |
| [Roadmap](../ROADMAP.md) | Milestones, dependencies and acceptance path |
| [Format coverage](format-coverage.md) | Status by exact format/version/capability |

### 1.2 Project operation

| Document | Purpose |
|---|---|
| [Contributing](../CONTRIBUTING.md) | Contribution workflow and review expectations |
| [Governance](../GOVERNANCE.md) | Roles and decision authority |
| [Security](../SECURITY.md) | Threat model and private vulnerability process |
| [Support](../SUPPORT.md) | How to request help or report ordinary defects |
| [Changelog](../CHANGELOG.md) | User-visible project history |
| [Release process](RELEASE-PROCESS.md) | Release candidates, verification, tags and evidence |

### 1.3 Research, specifications and tests

| Document | Purpose |
|---|---|
| [Glossary](GLOSSARY.md) | Stable terminology used across the project |
| [Format specification template](FORMAT-SPECIFICATION-TEMPLATE.md) | Required structure for an exact format version |
| [Conformance manifest specification](CONFORMANCE-MANIFEST-SPECIFICATION.md) | Language-neutral test-case contract |
| [Source and corpus policy](SOURCE-AND-CORPUS-POLICY.md) | Evidence, copyright, provenance and fixture rules |
| [Source notes](sources/README.md) | Index of bibliographic research notes |
| [ADR process](adr/README.md) | Architecture-decision lifecycle and index |
| [ADR template](adr/ADR-TEMPLATE.md) | Template for proposed decisions |

## 2. Sources of truth

The documents have different responsibilities:

- the Lastenheft controls product need, scope and acceptance;
- the Pflichtenheft controls technical requirements;
- the architecture controls boundaries and dependency rules;
- accepted ADRs control named design decisions;
- format specifications control exact on-disk interpretation;
- conformance manifests control language-neutral observable examples;
- source code implements those contracts;
- `format-coverage.md` reports only what the evidence supports.

Source code does not silently override a format specification. A discovered
discrepancy triggers a documented specification or ADR change plus tests.

## 3. Documentation states

| State | Meaning |
|---|---|
| Draft | incomplete and not a basis for support claims |
| Review | internally coherent and awaiting evidence/review |
| Accepted | approved for implementation and verification |
| Superseded | retained for history, replaced by a named successor |
| Archived | no longer active, retained for provenance |

Every format specification and ADR states its status. Ordinary guides are
versioned through Git history and release tags.

## 4. Language

The primary requirement and architecture documents are currently German.
Repository operational documents may be English to support contributors.
Translations must identify the normative original while both versions are not
maintained with automated parity checks.

Technical identifiers, format names, diagnostic codes and requirement IDs are
not translated.

## 5. Linking and identifiers

- use relative links for repository documents;
- link exact headings where stable and helpful;
- do not duplicate normative text when a precise link is enough;
- retain permanent requirement, architecture, ADR, format and test IDs;
- when renaming a file, update all inbound links in the same change;
- do not reuse an identifier for a different meaning.

## 6. Review responsibilities

| Change | Minimum review focus |
|---|---|
| Requirement | scope, acceptance and stakeholder intent |
| Architecture | dependency direction, portability, security and reversibility |
| Format specification | evidence, versions, byte rules and unknown values |
| Corpus metadata | provenance, rights, privacy and expected properties |
| Test manifest | deterministic expectations and cross-language portability |
| Release documentation | exact commit, artifacts, limitations and checksums |

## 7. Adding a new format document

1. add a version-specific row to `format-coverage.md`;
2. create a source note or extend the relevant one;
3. copy the format specification template under `specifications/`;
4. choose a stable format ID according to the future ADR-0006;
5. record unresolved facts instead of guessing;
6. prepare conformance cases and corpus metadata;
7. request review before raising the coverage status.

## 8. Documentation quality checks

The project will automate:

- broken relative links;
- duplicate `LAS-*`, `ARC-*`, ADR and test identifiers;
- missing required specification headings;
- coverage entries without matching specification metadata;
- corpus files without metadata/hash;
- invalid conformance manifests;
- release notes without a version and date.

Until checks exist, reviewers apply the same rules manually.

