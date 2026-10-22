# Contributing to SASD Moschus

Thank you for helping preserve access to historical file formats. Moschus
values small, reviewable and well-evidenced contributions over broad claims of
support.

## 1. Before contributing

Read these documents first:

1. [Agent instructions](AGENTS.md) — repository-wide autonomous workflow and WSL rules;
2. [Lastenheft](LASTENHEFT.md) — what the project must achieve;
3. [Pflichtenheft](PFLICHTENHEFT.md) — technical requirements;
4. [Architecture](ARCHITECTURE.md) — boundaries and dependency rules;
5. [Roadmap](ROADMAP.md) — current order of work;
6. [Security policy](SECURITY.md) — private vulnerability reporting;
7. [Source and corpus policy](docs/SOURCE-AND-CORPUS-POLICY.md) — copyright,
   provenance and test-file rules.

Do not upload scans, book pages, proprietary compiler files, application
binaries or historical sample files unless their redistribution rights are
explicitly documented.

## 2. Ways to contribute

- identify and document a format version;
- locate a primary specification or manufacturer document;
- reconcile contradictory sources;
- contribute a lawfully redistributable fixture;
- add or improve a format specification;
- implement or review a probe, reader, validator, recovery rule or writer;
- add negative, boundary, truncation or resource-limit tests;
- improve a language binding, CLI, build profile or documentation;
- reproduce behaviour with a historical application or compiler;
- report incorrect support claims or security issues.

Research-only contributions are valuable. It is better to record an unresolved
question accurately than to guess in code.

## 3. Contribution workflow

### 3.1 Choose one coherent change

A contribution should have one primary purpose. Examples:

- specify the dBASE III header;
- add checked 32-bit multiplication;
- add a truncated GIF header fixture;
- document a Turbo C build result.

Avoid combining formatting cleanup, API redesign and a new codec in one change.

### 3.2 Establish traceability

Before implementation, identify:

- applicable `LAS-*` requirements;
- applicable Pflichtenheft sections;
- applicable `ARC-*` rules and ADRs;
- exact format/version/profile;
- specification section;
- required tests and fixtures.

### 3.3 Research before claiming support

For format changes:

1. create or update the coverage row;
2. record sources and evidence class;
3. update the format specification;
4. add fixtures and expected results;
5. implement the smallest capability;
6. run conformance and robustness tests;
7. raise status only after its criteria are met.

### 3.4 Branch and review model

External contributors should normally create a focused branch and pull
request. Maintainers may commit directly to `main` for reviewed documentation,
repository administration or explicitly authorised work. Direct commits must
meet the same test, traceability and documentation standards as pull requests.

Never force-push `main`, move a published release tag or rewrite public history.

### 3.5 Commit style

Use imperative, scoped commit subjects where practical:

```text
docs: define DBF provenance rules
core: add checked offset addition
dbase: parse dBASE III field descriptors
tests: cover truncated GIF extension
build: add strict GCC C90 profile
```

Each commit should build and test when the project stage permits it. Mechanical
changes should be separated from behavioural changes.

## 4. Format specification contributions

Start with
[`docs/FORMAT-SPECIFICATION-TEMPLATE.md`](docs/FORMAT-SPECIFICATION-TEMPLATE.md).

A specification must distinguish:

- verified normative facts;
- secondary-source claims;
- empirical observations;
- project interpretation decisions;
- unresolved questions.

It must name exact versions. “Supports Word”, “supports TIFF” or “supports
dBASE” is not sufficiently precise.

Tables should state byte order, offsets, sizes, types, constraints, version
conditions and behaviour for unknown values. Security-sensitive lengths,
offsets, recursion, compression and references require explicit limits.

## 5. Code contributions

### 5.1 C89/C90 core

- remain within the language subset defined by the active ADRs;
- do not assume `char` signedness, integer width or host byte order;
- use project checked-arithmetic and stream primitives;
- make ownership and cleanup explicit;
- avoid mutable global state;
- keep declarations compatible with selected historical compilers;
- place compiler/OS conditionals in `platform/` whenever practical;
- use `/* ... */` where `//` is unavailable in the C90 profile.

### 5.2 C++ code

- use only the active language epoch;
- the converter must depend on public C++ interfaces;
- do not duplicate codec semantics in the CLI;
- preserve all structured diagnostics and resource limits;
- document RAII/ownership behaviour permitted by the active compiler profile.

### 5.3 Later language libraries

- implement shared behaviour idiomatically;
- reuse specifications and conformance manifests;
- do not claim native implementation when merely launching the converter;
- keep format identifiers and diagnostic codes compatible.

### 5.4 Comments

Comments should explain why a rule exists, cite a specification section or
describe a non-obvious historical/compiler constraint. Comments should not
merely restate the code.

Public APIs require documentation of:

- purpose and preconditions;
- ownership and lifetime;
- valid ranges;
- error and diagnostic behaviour;
- resource-limit interaction;
- thread/reentrancy guarantees;
- format/profile applicability.

## 6. Testing requirements

Choose tests according to the change:

- unit tests for primitives and local rules;
- positive fixtures for valid structures;
- negative fixtures for invalid values;
- truncation at every meaningful boundary;
- overflow and resource-limit cases;
- round-trip tests with explicit preservation criteria;
- conversion tests with expected loss classes;
- cross-language conformance cases;
- historical reference results where legally possible.

An accepted parse is not enough. Tests should verify the structured result and
diagnostics.

Every committed fixture needs metadata, provenance, rights information and a
cryptographic hash as defined by the corpus policy.

## 7. Security expectations

Treat all file bytes and metadata as untrusted. Do not:

- allocate from an unchecked file length;
- add or multiply offsets without overflow checks;
- recurse without a depth limit;
- decompress without output and ratio limits;
- execute macros, scripts, printer commands or embedded programs;
- resolve external links or paths implicitly;
- weaken limits in recovery or debug mode;
- print file contents in diagnostics without explicit opt-in.

Potential vulnerabilities should be reported privately as described in
[SECURITY.md](SECURITY.md), not demonstrated in a public issue before a fix is
available.

## 8. Documentation expectations

Update all affected material in the same contribution:

- format specification;
- `docs/format-coverage.md`;
- API/CLI documentation;
- examples;
- source/provenance notes;
- roadmap or ADR when scope/architecture changes;
- changelog for user-visible changes.

Links should be relative inside the repository. Examples must not depend on
non-redistributable files.

## 9. Review checklist

- [ ] One coherent purpose
- [ ] Exact format/version/profile identified
- [ ] Requirements and architecture rules considered
- [ ] Sources and evidence recorded
- [ ] No copyrighted or proprietary material added without permission
- [ ] Bounds, overflow, allocation and cleanup checked
- [ ] Strict and recovery behaviour remain distinct
- [ ] Structured diagnostics added or updated
- [ ] Positive, negative and boundary tests present
- [ ] Fixtures have metadata and hashes
- [ ] Coverage and documentation match behaviour
- [ ] Active compiler/language epoch respected
- [ ] No unrelated generated or local files committed

## 10. Status changes

A contributor may propose a coverage-state change, but the evidence determines
the outcome. `Stable` requires the complete project Definition of Done and
maintainer review. Missing evidence results in a lower honest status, not an
exception to the rule.

## 11. Communication and conduct

Disagreement about historical behaviour is resolved through evidence,
reproducible tests and respectful technical discussion. Critique the claim or
code, not the person. Private or personal data found in historical files must
not be posted in issues or fixtures.

For ordinary questions use the channels listed in [SUPPORT.md](SUPPORT.md).
Security matters follow [SECURITY.md](SECURITY.md).

