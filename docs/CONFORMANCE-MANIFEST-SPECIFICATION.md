# Conformance manifest specification

| Field | Value |
|---|---|
| Document version | 0.1 |
| Status | Architecture baseline; serialization syntax pending ADR-0004 |
| Scope | Language-neutral behavioural test cases |

## 1. Purpose

A conformance manifest defines observable behaviour without depending on the
classes, memory layout or test framework of one programming language. C, C++,
C# and Java implementations consume the same logical cases.

This document defines the information model. ADR-0004 will select the concrete
serialization format and canonicalization rules.

## 2. Principles

1. A case has one stable identity and one primary purpose.
2. Inputs are immutable and identified by cryptographic hash.
3. Format version, operation, options and limits are explicit.
4. Expectations use public model projections, not private objects.
5. Diagnostics are checked by stable code and parameters, not translated text.
6. Ordering is asserted only when semantically guaranteed.
7. Platform-dependent expectations are isolated and justified.
8. A failed or unsupported case is not silently skipped.

## 3. Manifest hierarchy

```text
manifest suite
├── suite metadata
├── shared resources and defaults
└── cases
    ├── identity and purpose
    ├── input set
    ├── operation and policy
    ├── expected status/diagnostics
    ├── expected model/output projection
    └── evidence and traceability
```

## 4. Suite metadata

Required logical fields:

| Field | Meaning |
|---|---|
| `schema_version` | concrete manifest schema version |
| `suite_id` | permanent suite identity |
| `suite_version` | version of expectations |
| `title` | human-readable title |
| `format_ids` | covered exact formats/profiles |
| `specification_refs` | specification versions/commits |
| `default_limits` | named resource profile or explicit defaults |
| `created` | creation date |
| `reviewed` | latest review date |
| `license` | manifest license |

Optional fields include maintainers, tags, historical application profiles and
superseded suite references.

## 5. Stable case identity

Case IDs should follow a readable namespace, for example:

```text
TC-DBF3-READ-MINIMAL-001
TC-GIF89-VALIDATE-TRUNCATED-GCE-001
TC-SDF-WRITE-FIELD-OVERFLOW-001
```

An ID is never reused for a different purpose. A corrected expectation keeps
the ID and increments suite version when the test intent is unchanged;
materially different intent receives a new case.

## 6. Inputs

A case can define:

- primary byte fixture;
- companion files with logical roles;
- generated input recipe;
- model input for writer cases;
- stdin/seekability properties;
- optional caller hints.

Each file reference includes:

| Field | Requirement |
|---|---|
| fixture ID | stable corpus identity |
| relative path | path within approved corpus |
| hash algorithm | approved cryptographic algorithm |
| hash value | exact content hash |
| size | exact byte size |
| role | primary/memo/index/resource/etc. |
| metadata reference | provenance and rights record |

Hash-only local fixtures may be referenced but must be marked unavailable in
public CI. They cannot be the sole evidence for a public Stable claim unless an
equivalent redistributable test covers the rule.

## 7. Operation

Allowed core operations:

- `probe`;
- `read`;
- `validate_stream`;
- `validate_model`;
- `recover`;
- `write`;
- `round_trip`;
- `convert_plan`;
- `convert`;
- `describe_capability`.

Each case names exactly one primary operation. A round-trip case can contain
defined substeps but is evaluated as a single preservation contract.

## 8. Options and policies

The case records every non-default semantic choice:

- forced or expected format ID;
- encoding policy and selected codepage;
- strict/recovery mode;
- unknown-record policy;
- preservation/canonical writer mode;
- loss policy;
- target format/profile;
- companion resolver mapping;
- resource limits;
- deterministic clock/metadata values if relevant.

No test may rely silently on host locale, local timezone, environment path or
filesystem enumeration order.

## 9. Expected top-level result

| Field | Meaning |
|---|---|
| status | success/warning/failure/unsupported/limit/internal |
| completeness | complete/partial/recovered/none |
| validity | valid/invalid/not_checked/indeterminate |
| format ID | confirmed/detected source identity |
| target format ID | exact writer target where applicable |
| bytes consumed | exact/range/not asserted |
| resource outcome | within limits or named limit hit |

Status vocabulary will be fixed with the public result contract. Manifests use
stable symbolic names, not language enum ordinals.

## 10. Diagnostic expectations

A diagnostic expectation can assert:

- exact stable code;
- severity and category;
- selected parameters;
- source byte/record/field location;
- target property;
- loss class;
- multiplicity;
- ordering only when contractually stable.

Matching modes:

| Mode | Use |
|---|---|
| exact sequence | order is part of public behaviour |
| exact set | same diagnostics, order irrelevant |
| contains | additional non-breaking informational diagnostics allowed |
| excludes | dangerous or misleading diagnostic must not occur |

Human-readable message text is not a cross-language assertion.

## 11. Model projections

A projection exposes only stable public semantics needed by the case.

Example logical projection:

```text
table.schema.columns[0].name = "NAME"
table.schema.columns[0].type = "character"
table.records.count = 2
table.records[1].deleted = true
```

Projection operators should support:

- scalar equality;
- byte/string equality with explicit encoding;
- numeric exact/range/tolerance comparison;
- presence/absence;
- ordered and unordered collections;
- count and selected element checks;
- hash of large pixel/blob content;
- preservation/loss markers;
- source-location mapping.

Private memory addresses, class names and allocator details are forbidden.

## 12. Writer output expectations

A writer case may assert one or more levels:

1. exact byte hash for deterministic canonical output;
2. byte regions/masks for intentionally variable fields;
3. successful re-read and model projection;
4. independent validator/reference-program acceptance;
5. expected diagnostics and loss report.

Exact hashes are preferred where the writer contract is deterministic. A
semantic check must explain why byte identity is inappropriate.

## 13. Round-trip expectations

Every round-trip case declares its preservation level:

- `byte_exact`;
- `canonical_bytes`;
- `semantic_exact`;
- `semantic_subset`;
- `recovery_preservation`.

It also names compared properties and permitted normalization. “Round-trip
passes” without these details is invalid.

## 14. Conversion expectations

Plan and execution are checked separately.

The plan expectation contains:

- route and transformations;
- required loss permissions;
- predicted losses/assumptions;
- rejection reason when unavailable.

Execution expectations contain:

- actual transformations;
- actual loss report;
- target bytes/model checks;
- no unplanned loss;
- cleanup/absence of output on failure.

## 15. Probe expectations

A probe case can assert:

- ordered or unordered candidate set;
- confidence class;
- positive and negative evidence IDs;
- ambiguity requirement;
- bytes/seeks within probe budget;
- no full parse side effect.

A filename extension may be an input hint but cannot be the only asserted
reason for an exact result.

## 16. Resource and security cases

Cases should cover:

- arithmetic overflow before access;
- input and output limits;
- single and total allocation limits;
- count, depth and cycle limits;
- decompression size/ratio;
- malformed companion references;
- output path isolation at application level;
- no external network/process execution;
- cleanup after controlled failure.

Resource cases assert the named limit and stable diagnostic, not a platform-
specific crash or wall-clock time unless a dedicated performance suite is used.

## 17. Conditional applicability

A case may require a declared capability such as seekable input or a specific
language package. Conditions are explicit and machine-readable.

Allowed outcomes for an inapplicable case:

- `not_applicable` because the suite excludes that product component;
- `unsupported` when the published capability says so;
- never silent omission.

Compiler bugs or platform failures are tracked separately and cannot be hidden
as ordinary skips.

## 18. Traceability

Each case links:

- one or more format specification rule IDs;
- relevant requirement/architecture IDs where useful;
- source/evidence IDs;
- regression issue or advisory if applicable;
- coverage capability supported by the case.

## 19. Schema evolution

- schema versions follow explicit compatibility rules;
- readers reject unknown major versions;
- additive optional fields may increment a minor version;
- migrations are deterministic and versioned;
- canonical serialization is defined before hashes/signatures are applied;
- old release manifests remain readable with their matching tools.

## 20. Validation of manifests

Automated validation checks:

- unique suite and case IDs;
- known format and diagnostic IDs;
- valid fixture paths and hashes;
- no implicit host defaults;
- operation-appropriate expectations;
- existing specification rule references;
- permitted matching modes;
- all committed fixtures possess corpus metadata.

## 21. Minimal logical example

The serialization below is illustrative, not the ADR-0004 syntax:

```yaml
case_id: TC-DBF3-READ-MINIMAL-001
operation: read
format_id: example.dbf.dbase3
input:
  fixture: corpus/dbase3/minimal.dbf
  sha256: "<hash>"
policy:
  mode: strict
  encoding: cp437
expect:
  status: success
  validity: valid
  diagnostics: []
  projection:
    table.schema.columns.count: 1
    table.records.count: 1
trace:
  specification_rules: [DBF3-HDR-001, DBF3-REC-001]
```

## 22. Open decisions for ADR-0004

- JSON, YAML or another serialization syntax;
- canonical ordering and numeric representation;
- schema validation technology compatible with project tooling;
- model projection query syntax;
- diagnostic set/sequence matching representation;
- generated fixture recipes;
- large expected-output storage;
- cross-platform path normalization;
- signature/checksum strategy for released suites.

