# Portable C89/C90 core

`libraries/c89/` is the first executable reference implementation for the
1990 language epoch. It targets ANSI C89 / ISO C90 plus only the explicitly
approved compiler/platform adapters.

## Responsibilities

- public C result, diagnostic and capability contracts;
- bounded byte and stream operations;
- checked arithmetic and resource limits;
- allocator and ownership contracts;
- static format registry;
- neutral model foundations;
- format probes, readers, validators, recovery logic and writers;
- adapters for shared conformance manifests.

## Non-responsibilities

- command-line parsing or terminal output;
- C++-specific convenience types;
- direct OS/Compiler conditionals outside approved platform interfaces;
- execution of embedded active content;
- network access;
- silent tolerance or unreported conversion loss.

## Language rules

- no C99 or later syntax/library dependency in the portable baseline;
- no assumptions about `char` signedness or host endian;
- no variable-length arrays, designated initializers or `stdint.h` dependency
  unless an approved compatibility layer provides equivalent types;
- no `//` comments in strictly compiled C90 sources;
- declarations and naming must remain compatible with ADR-0002 targets;
- public symbols use the project prefix selected by the API ADR.

## Ownership and errors

All public functions document:

- who owns input/output memory;
- which allocator is used;
- whether partial results can exist;
- cleanup requirements;
- status and diagnostic behaviour;
- reentrancy/thread guarantees;
- resource limits.

Library code never terminates the host process and never writes directly to
stdout/stderr.

## Planned module groups

```text
include/        public portable headers
src/core/       status, diagnostics, limits and checked operations
src/io/         streams, slices and endian access
src/model/      neutral domain-model primitives
src/registry/   static format/capability registration
src/codecs/     domain/family-specific implementations
tests/          C-level unit and adapter tests
```

Exact layout waits for ADR-0001 and ADR-0005.

## Build and verification

The first mandatory build is modern GCC in strict C90 mode. Modern sanitizer
and analysis builds test safety. Selected Turbo and Microsoft compilers provide
local historical portability evidence; proprietary tools are never vendored.

No public API should be added before ownership, stream, diagnostic, identifier
and resource-limit ADRs are accepted.

