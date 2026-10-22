# Platform and compiler compatibility

`platform/` isolates differences that do not belong to file-format semantics.

## Responsibilities

- compiler and feature detection;
- exact-width integer guarantees/fallbacks;
- byte-order access;
- checked arithmetic primitives;
- file, stream and binary-mode adapters;
- path and temporary-file operations;
- symbol visibility and calling conventions;
- DOS16/DOS32/modern resource profiles;
- portable time/locale/environment access when needed;
- 8.3-compatible source-package generation support.

## Boundary rule

Format codecs use platform contracts. They do not scatter `#ifdef` blocks for
compiler, OS or memory model. Platform code cannot decide format versions or
silently change format semantics.

## Planned profiles

| Profile | Purpose |
|---|---|
| modern GCC strict C90 | free, repeatable reference build |
| modern diagnostics/sanitizers | safety and undefined-behaviour analysis |
| selected Turbo C/C++ | local historical compatibility evidence |
| selected Microsoft C/C++ | local historical compatibility evidence |
| DOS16 resource profile | constrained memory/size behaviour |

Exact proprietary versions and memory models remain an ADR-0002 decision.

## Adding a platform adapter

An adapter must include:

- exact target/compiler detection;
- conservative fallback or explicit unsupported error;
- contract-equivalent behaviour;
- unit tests on an available host or documented local verification;
- known limitations;
- no proprietary redistributed headers or libraries;
- update to toolchain documentation.

## Safety rules

- verify integer widths at build/startup as appropriate;
- never emulate a wider safe range with unchecked narrow arithmetic;
- partial reads/writes remain visible;
- temporary files use safe names/permissions available on the target;
- paths from file contents are never directly trusted;
- old compiler success never replaces modern sanitizer testing.

