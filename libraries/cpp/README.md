# C++ library

`libraries/cpp/` provides the C++ API used by the Moschus converter and evolves
through explicitly separated language epochs.

## Initial role

During the 1990 epoch the C++ layer is a thin, type-safe facade over the
portable C89/C90 core. It must preserve every diagnostic, resource limit and
format/version distinction.

The exact early C++ subset and supported Turbo/Microsoft/GCC compilers will be
fixed by ADR-0002. The project does not use the ambiguous phrase “C++ 1990” as
a complete toolchain definition.

## Responsibilities

- public C++ handles and value types;
- lifetime/cleanup wrappers permitted by the active epoch;
- stream and model adapters;
- capability, probe, validation and conversion APIs;
- API consumed by `tools/converter-cpp/`;
- C++ examples and tests;
- migration path across language epochs.

## Boundaries

- no private API available only to the converter;
- no duplicate format parser in C++ merely for convenience;
- no swallowed C-core diagnostic or loss detail;
- no use of a newer standard before its accepted epoch;
- no format behaviour change hidden inside a language migration.

## Planned language epochs

1. early portable subset for the format-era-1990 release;
2. C++98;
3. C++03;
4. C++11;
5. C++14;
6. C++17;
7. C++20.

Each migration has a compiler matrix, ADR/migration document, complete 1990
conformance run, API compatibility assessment and immutable completion tag.

## API design expectations

- exact target format/version is explicit;
- result and diagnostics remain inspectable;
- loss policy defaults to safe rejection;
- ownership and exception/status mapping are documented;
- ranges/containers cannot bypass resource limits;
- active content remains inert;
- APIs are testable without the CLI.

Implementation begins only after the shared C contracts are sufficiently
defined for the required converter slice.

