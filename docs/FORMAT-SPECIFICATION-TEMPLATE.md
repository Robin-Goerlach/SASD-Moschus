# Format specification template

Copy this file to `specifications/<domain>/<format-id>.md`. Replace all
instructional text and bracketed placeholders. One document may cover closely
related versions only when every differing field and rule remains explicit.

---

# [Format family, version and profile]

| Field | Value |
|---|---|
| Specification ID | `[stable-format-id]` |
| Family | [family] |
| Variant | [manufacturer/platform variant] |
| Version | [exact on-disk version] |
| Profile | [profile or none] |
| Domain | [tabular/document/raster/vector/…] |
| Historical cutoff | [in scope / out of scope / unresolved, with evidence] |
| Status | Draft / Review / Accepted / Superseded |
| Document version | 0.1 |
| Maintainer | [name or role] |
| Last reviewed | YYYY-MM-DD |
| Supersedes | [ID or none] |

## 1. Purpose and scope

State exactly what this specification defines. Name excluded revisions,
application-private extensions, companion files and unsupported features.

## 2. Historical identity

### 2.1 Names and aliases

List official names, common names, filename extensions and MIME identifiers.
Mark extensions as hints, not proof.

### 2.2 Product and on-disk versions

Map marketing/application releases to on-disk versions where evidence exists.
Do not infer identity from similar names.

| Product/version | On-disk version/profile | Earliest evidence | Confidence | Source |
|---|---|---|---|---|
| [value] | [value] | [date] | confirmed/probable/unresolved | [SRC-ID] |

### 2.3 Relationship to other versions

Describe predecessor, successor, shared structures and incompatible changes.

## 3. Evidence and sources

| Source ID | Evidence class | Citation | Scope used | Notes/conflicts |
|---|---|---|---|---|
| SRC-… | normative/secondary/empirical/derived | [citation] | [sections] | [notes] |

Explain conflicts. A project decision that resolves ambiguity must cite its ADR
or explicit interpretation rule.

## 4. Conformance terminology

Define what “valid”, “well-formed”, “supported”, “reserved” and “ignored” mean
for this format. State whether the original standard defines these terms.

## 5. Physical representation

### 5.1 Byte order and primitive types

| Type | Size | Byte order/encoding | Range | Notes |
|---|---:|---|---|---|
| [type] | [bytes/bits] | [little/big/text] | [range] | [constraints] |

State signed representation, floating-point format, alignment, padding and
assumptions about byte width.

### 5.2 Character encodings

List declared, implied and application-dependent encodings. Define invalid
byte handling, terminators, padding, control characters and line endings.

### 5.3 Overall layout

```text
[Header]
[Directory/records/chunks]
[Payload]
[Trailer]
```

State whether order, repetition and optional sections are significant.

## 6. Detection and version identification

### 6.1 Positive evidence

| Evidence ID | Bytes/structure | Strength | Versions | False-positive considerations |
|---|---|---|---|---|
| DET-… | [rule] | exact/strong/plausible/weak | [versions] | [notes] |

### 6.2 Exclusion evidence

List conditions that disqualify a version even if a signature matches.

### 6.3 Ambiguity

Explain indistinguishable versions and what user hint or companion file is
required. Do not invent certainty.

### 6.4 Probe budget

State maximum bytes, seeks, records and companion-file access required for
normal detection.

## 7. Structures

Create one subsection per header, record, chunk, directory, token or table.

### 7.x [Structure name]

| Offset | Size | Type | Field | Versions | Constraints | Evidence |
|---:|---:|---|---|---|---|---|
| 0 | 1 | u8 | [name] | [versions] | [rules] | [SRC-ID] |

For variable-length fields state how size is determined and bounded. For every
count/offset pair state:

- valid range;
- origin/base of offset;
- overflow-safe relationship;
- alignment;
- behaviour at EOF;
- whether overlap is allowed;
- validation severity.

## 8. Records, chunks or tokens

| Code | Name | Version | Payload | Multiplicity/order | Unknown-code policy |
|---|---|---|---|---|---|
| [code] | [name] | [version] | [reference] | [rule] | reject/preserve/skip |

Unknown or reserved values require an explicit policy. “Ignore” must state how
length and safe skipping are established.

## 9. Semantic model mapping

Map file structures to the relevant Moschus domain model.

| Source property | Model property | Conversion | Loss/assumption |
|---|---|---|---|
| [field] | [property] | [rule] | [none/class] |

Distinguish absent, null, empty, deleted, invalid and unknown where applicable.

## 10. Companion files and external references

For each relationship specify:

- file identity and naming convention;
- mandatory/optional status;
- resolver lookup key;
- consistency checks;
- behaviour when missing or conflicting;
- security and path restrictions;
- independent coverage status.

## 11. Compression or packing

Describe exact algorithm variants, bit order, reset rules, terminators and
malformed-stream behaviour. Define maximum output, expansion ratio, dictionary
size and step limits.

If no compression exists, state “Not applicable”.

## 12. Validation rules

Assign stable rule IDs.

| Rule ID | Level | Condition | Severity | Recovery relevance | Evidence |
|---|---|---|---|---|---|
| VAL-… | container/syntax/semantic/profile | [rule] | info/warning/error/fatal | [notes] | [source] |

Explain cases that are accepted by historical software but contradict a
written specification.

## 13. Strict reader behaviour

State:

- required preconditions;
- unsupported-feature behaviour;
- partial-result policy;
- unknown-data preservation;
- diagnostics;
- resource limits specific to the format.

## 14. Recovery behaviour

List each permitted heuristic with:

- trigger;
- search window/step limit;
- plausibility test;
- confidence;
- output marking;
- possible false recovery;
- required diagnostic code.

Recovery must not redefine formal validity.

## 15. Writer behaviour

### 15.1 Target selection

State the exact version/profile ID required by the writer.

### 15.2 Representability checks

List model limits, type widths, encoding restrictions and unsupported features.

### 15.3 Canonical layout

Define order, padding, reserved values, timestamps and other choices needed for
deterministic output.

### 15.4 Compatibility profiles

Name historical applications only when behaviour was tested and the limitation
is documented.

### 15.5 Transactional output

State which errors can occur before and during emission and how partial output
is handled.

## 16. Preservation and round-trip contract

| Property | Read | Write | Semantic round-trip | Byte-exact | Notes |
|---|---|---|---|---|---|
| [property] | yes/no/partial | yes/no/partial | guaranteed/not | guaranteed/not | [conditions] |

Define canonical equivalence and permitted normalization. Do not label a test
“round-trip” without naming the preservation level.

## 17. Conversion considerations

List meaningful source/target domains, required transformations and expected
loss classes. Pair-specific routes belong in separate conversion specs when
they add semantics beyond the common model.

## 18. Security and resource analysis

| Threat | Source field/structure | Limit/control | Required tests |
|---|---|---|---|
| overflow | [field] | checked operation | [case IDs] |
| excessive allocation | [count] | [limit] | [case IDs] |

Consider cycles, nesting, compression, large counts, path handling, active
content and diagnostic data exposure.

## 19. Known application deviations

| Application/version | Deviation | Evidence | Moschus policy |
|---|---|---|---|
| [name] | [behaviour] | [source/test] | [strict/profile/recovery] |

## 20. Conformance cases

| Case ID | Purpose | Fixture | Expected capability/result |
|---|---|---|---|
| TC-… | [purpose] | [fixture ID] | [result] |

Include valid minimal, representative, boundary, truncated, malformed,
unknown-extension, limit, writer and round-trip cases.

## 21. Unsupported features and open questions

| ID | Question/feature | Impact | Needed evidence | Target milestone |
|---|---|---|---|---|
| OPEN-… | [item] | [impact] | [source/fixture] | [milestone] |

## 22. Implementation notes

Non-normative guidance only. Link implementation modules; do not make code the
sole specification.

## 23. Change history

| Version | Date | Change | Evidence/decision |
|---|---|---|---|
| 0.1 | YYYY-MM-DD | Initial draft | [links] |

