# Language libraries

This directory contains language-specific Moschus library implementations.
They share specifications, format identifiers, diagnostic semantics and
conformance manifests, but each library remains independently usable.

## Implementations

| Directory | Role | Initial status |
|---|---|---|
| `c89/` | portable reference core for the 1990 language epoch | first implementation |
| `cpp/` | C++ facade and later standard-C++ evolution | begins with converter needs |
| `csharp/` | native .NET implementation | planned after shared contracts stabilize |
| `java/` | native JVM implementation | planned after shared contracts stabilize |

Additional languages require an architecture/roadmap decision and must consume
the same conformance definitions.

## Shared behavioural contract

All implementations must agree on:

- exact format/version/profile identifiers;
- capability states;
- probe evidence and ambiguity semantics;
- domain-model meaning;
- strict, validation and recovery separation;
- stable diagnostic codes and loss classes;
- resource-limit outcomes;
- writer target versions and preservation contracts;
- language-neutral conformance cases.

They may differ idiomatically in naming, ownership syntax, exceptions, stream
types, collections and packaging.

## Independence

A native language library is not considered implemented merely because it:

- starts the C++ command-line converter;
- forwards every operation through a hidden network service;
- exposes a thin FFI without a separately documented package status.

An optional FFI package may exist later, but it must be labelled accurately.

## Dependency rule

Language libraries depend on specifications and tests. Specifications never
depend on a language library. Libraries do not call one another to establish
format truth.

## Minimum structure per language

- public API and version metadata;
- core result, diagnostic and limit types;
- stream/input abstractions;
- registry and capability reporting;
- codecs grouped by domain/family;
- tests consuming shared manifests;
- package/build files;
- examples and API documentation;
- support matrix matching actual behaviour.

## Adding an implementation

Before starting a new language:

1. shared identifiers and manifest schema must be stable;
2. at least one domain model and several codecs must be proven;
3. package/runtime baseline must be decided by ADR;
4. CI and release ownership must be available;
5. no support status may exceed its conformance evidence.

See the root architecture and roadmap for the complete policy.

