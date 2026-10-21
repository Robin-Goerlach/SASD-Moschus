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

The C++20 library is the initial reference implementation because the converter
is written in C++ and historical binary formats benefit from explicit,
bounded byte handling.

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

Format versions and library releases are different concepts. Public APIs follow
semantic versioning. Historical writers require an explicit target format
version; they must not silently select the newest known variant.

## 7. Dependency direction

```text
converter -> C++ public library -> codec interfaces -> domain models
                                      |
                                      +-> bounded byte/text primitives

language libraries -> shared specifications + conformance manifests
```

Specifications and conformance data never depend on an implementation.
