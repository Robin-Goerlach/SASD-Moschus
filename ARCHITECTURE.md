# Architecture

## 1. Purpose

SASD Moschus separates historical format knowledge from programming-language
implementations. This prevents one implementation from becoming an
undocumented specification and allows C++, C#, Java, and future libraries to be
tested against the same behavioural contract.

## 2. Layers

### 2.1 Specifications

`specifications/` is the canonical description of format families, versions,
records, fields, encodings, limits, and known application deviations.

A specification must distinguish verified facts, implementation decisions,
inferences, and unresolved questions.

### 2.2 Language libraries

Each directory below `libraries/` contains an independent implementation.
Libraries expose equivalent concepts where practical, while following the
idioms and safety facilities of their language.

The 1990 language epoch begins with a portable ANSI C89 / ISO C90 core so that
the same codec logic can be verified with GCC and selected historical Borland
and Microsoft C toolchains. The command-line converter is written in C++ and
uses only the compiler subset defined for the active language epoch.

After the 1990 release is tagged, the C++ implementation advances in controlled
steps through C++98, C++03, C++11, C++14, C++17, and C++20. Old formats remain
covered by the shared conformance suite during every migration.

### 2.3 Neutral domain models

Readers do not convert directly to another file format. They decode into a
domain model suitable for the information represented:

- tabular model;
- document model;
- raster image model;
- vector/metafile model;
- chunked media model where required.

Models preserve source-specific metadata in a controlled extension area without
letting implementation details leak into the common semantic fields.

### 2.4 Tools

`tools/converter-cpp/` contains the C++ command-line application. The tool is a
consumer of the public C++ library and must not contain private format parsers.

The planned commands are:

- `moschus info`
- `moschus validate`
- `moschus convert`
- `moschus formats`

### 2.5 Shared tests

`tests/conformance/` describes language-neutral expected behaviour.
`tests/corpus/` contains only files that may lawfully be redistributed,
together with provenance and checksums.

### 2.6 Compiler and platform compatibility

`platform/` centralises compiler detection, integer-width guarantees,
byte-order access, checked arithmetic, file adapters, resource limits, DOS
memory models, and generation of 8.3-compatible source bundles.

Conditional compilation must remain inside this layer whenever practical.
Historical proprietary compilers are locally supplied tools and are never
vendored or downloaded by public CI.

## 3. Codec contract

A complete codec provides:

1. format and version probing with a confidence explanation;
2. bounded parsing into a neutral model;
3. structural and semantic validation;
4. deterministic writing for declared versions;
5. warnings for unsupported or lossy features;
6. conformance fixtures for valid, boundary, truncated, and malformed inputs;
7. documentation of preservation and canonicalisation behaviour.

Reading, validation, and repair are separate operations. A tolerant reader must
not silently make a damaged file appear valid.

## 4. Conversion policy

Conversion routes are capability-based rather than all-to-all. A route is
permitted only when the two formats share a meaningful domain model.

Every conversion result includes diagnostics classified as:

- information;
- compatibility warning;
- lossy conversion;
- unsupported feature;
- invalid source data;
- resource or security limit.

The command-line tool should fail by default when loss is not explicitly
accepted.

## 5. Security boundaries

All parsers treat input as untrusted. Implementations must check integer
overflow, offset and length arithmetic, allocation size, nesting depth,
decompression expansion, record counts, and cyclic references.

No parser executes embedded code, macros, commands, external links, or bundled
programs. Recovery mode remains bounded by the same resource limits as strict
mode.

## 6. Versioning

Format versions, product releases, format horizons, and language epochs are
different concepts. Public APIs follow semantic versioning once declared
stable. Historical writers require an explicit target format version; they
must not silently select the newest known variant. Each completed language
epoch is preserved by a reproducible tag before the minimum language level is
raised.

## 7. Dependency direction

```text
converter -> active C++ API -> portable C89/C90 core -> codec interfaces
                                      |                    |
                                      |                    +-> domain models
                                      +-> platform compatibility

all language libraries -> shared specifications + conformance manifests
```

Specifications and conformance data never depend on an implementation.
