# Java library

This directory is reserved for a future native Java implementation of the
Moschus contracts.

## Start conditions

- shared identifiers and manifests are stable;
- domain-model semantics have been validated by existing codecs;
- a JDK/runtime and module/package baseline is selected by ADR;
- common corpus execution is available in CI;
- maintenance and release ownership are assigned.

## Goals

- idiomatic stream/channel and model APIs;
- explicit bounded processing despite managed memory;
- stable diagnostic-code compatibility;
- independent parsers and writers based on shared specifications;
- shared conformance results with other implementations;
- reproducible package and examples.

## Non-goals

- converter subprocess wrapping as the native library;
- unbounded allocation from file-declared counts;
- host-default charset interpretation;
- automatic external resource or active-content execution;
- blanket support claims for an entire format family.

Exact source layout, minimum JDK and packaging are intentionally undecided
until the corresponding ADR.

