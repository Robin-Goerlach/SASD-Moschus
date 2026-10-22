# C# library

This directory is reserved for a future native C#/.NET implementation of the
Moschus contracts.

## Start conditions

Development begins after:

- stable format IDs and diagnostic codes;
- an accepted conformance-manifest schema;
- at least one proven domain model;
- representative M2/M3 specifications and fixtures;
- an ADR choosing .NET/runtime/package baselines;
- CI and maintenance responsibility are available.

## Goals

- idiomatic .NET APIs and stream integration;
- structured results, diagnostics and resource limits;
- independent format implementation from shared specifications;
- common conformance behaviour with C/C++;
- deterministic writers and explicit loss policies;
- package, examples and API documentation.

## Non-goals

- merely launching the C++ converter;
- claiming full coverage because another language has it;
- depending on Windows-only APIs without an explicit package/profile decision;
- weakening limits because managed memory is available.

The eventual directory will contain source, tests, packaging and examples in a
layout selected by its ADR. Until then no placeholder API is published.

