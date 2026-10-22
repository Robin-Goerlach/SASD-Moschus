# Language-neutral conformance tests

This directory holds manifests and expected public behaviour shared by every
Moschus language implementation.

## Purpose

Conformance tests answer whether independent implementations agree on:

- format/version identification;
- structured model semantics;
- validity and completeness;
- diagnostic codes and loss classes;
- resource-limit outcomes;
- deterministic writer output or declared semantic equivalence;
- round-trip and conversion contracts.

They do not require identical internal classes, allocation strategy or private
function boundaries.

## Planned layout

```text
tests/conformance/
├── schema/          manifest schema and migrations
├── suites/          domain/format suites
├── projections/     reusable public-model projections
├── runners/         language adapters or runner contracts
└── reports/         ignored/generated local output definitions
```

## Manifest rules

Follow `docs/CONFORMANCE-MANIFEST-SPECIFICATION.md`. Each case has a permanent
ID, immutable hashed inputs, explicit options/limits, structured expectations
and traceability to specification rules.

## Required case classes

- minimal valid;
- representative valid;
- boundary values;
- truncation at meaningful boundaries;
- malformed lengths/offsets/counts;
- unknown records/extensions;
- resource-limit activation;
- writer representability and deterministic output;
- format-specific round-trip;
- conversion planning and actual loss;
- regression cases for fixed defects.

## Results

A runner must report pass, fail, unsupported or not-applicable explicitly.
Silent skips are prohibited. Reports identify implementation version, suite
version, platform and active toolchain profile.

Serialization details remain pending ADR-0004; no ad-hoc permanent schema
should be introduced beforehand.

