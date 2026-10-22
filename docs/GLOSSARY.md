# Glossary

This glossary establishes the meaning of recurring terms in SASD Moschus.
Definitions are intentionally precise because historical format discussions
often use the same word for different concepts.

## A

### Active content

Data that can cause commands, macros, scripts, printer operations or external
resources to be executed or retrieved. Moschus treats active content as inert
data unless a future, separately secured product explicitly states otherwise.

### ADR — Architecture Decision Record

An immutable record of a significant design decision, its context,
alternatives and consequences. An accepted ADR may be superseded, not silently
rewritten.

### Approximation

A conversion in which the destination represents the source only
approximately, for example replacing an unavailable colour. It is a reported
loss class, not a silent successful conversion.

## B

### Begleitdatei / companion file

A separate file required or optionally used to interpret another file, such as
a dBASE memo or index file. Companion files have their own identity and
capability status.

### Bytegleichheit

Exact equality of file bytes. It is stricter than semantic round-trip and is
promised only for explicitly defined profiles.

## C

### Canonical writer

A writer that produces one deterministic, standards-conforming representation
for equivalent model content where the format permits it.

### Capability

A precise operation supported for a specific format/version/profile, such as
Probe, Read, Validate, Write, Round-trip or Convert.

### Codec

The group of operations associated with an exact format family/version. A
codec can provide only a subset of capabilities and must report that subset.

### Conformance manifest

A language-neutral test-case description linking input, operation, options,
expected structured results and diagnostics.

### Conversion

Transfer from one supported format/version to another through an appropriate
domain model and explicit transformations. Conversion does not imply lossless
preservation.

### Corpus

The collection of test files and metadata used to verify behaviour. Inclusion
requires provenance and redistribution assessment.

## D

### Diagnostic code

A stable machine-readable identifier for an information item, warning, loss or
error. Human text can change or be translated; the code and parameters form
the automation contract.

### Domain model

A format-independent representation for one semantic family, such as tabular
data, documents, raster images or vector graphics. Moschus intentionally does
not use one universal untyped model.

## E

### Evidence class

Classification of a format claim as normative, secondary, empirical, derived
or unresolved.

### Extension area

A typed portion of a domain model that can preserve source-specific data
without pretending it is common semantics.

### File extension

The suffix of a filename, such as `.dbf`. It is a hint and never sufficient
proof of the format version.

## F

### Format family

A group of related on-disk formats that share history or structure, for
example TIFF or dBASE DBF. A family is too broad for most support claims.

### Format horizon / Formatepoche

A project scope bounded by historical availability. The first Moschus horizon
ends on 31 December 1990.

### Format ID

A stable machine-readable identity for one family/version/profile. It is
different from filename extension, display name and MIME type.

### Format profile

A documented subset or application-specific interpretation of a broader
format/version.

### Format version

A materially distinct on-disk definition. A product marketing version and an
on-disk version are not automatically identical.

## G

### Gültig / valid

Conforming to all mandatory rules of the selected version/profile. A file can
be readable while invalid.

## I

### Information loss

Any source property that is dropped, approximated, normalized in a relevant
way or replaced by an assumption during transformation or writing.

## K

### Konfidenz / confidence

The strength of a format-identification result based on stated evidence.
Confidence is not validity and not proof that the entire file can be read.

### Konformität / conformance

Agreement of observable implementation behaviour with specifications and
shared manifests.

## L

### Language epoch / Sprachepoche

The minimum C or C++ language standard and compiler set permitted for a project
stage. It is independent of the format horizon.

### Loss policy

The caller's rule for which loss classes may be accepted. The default should
reject unapproved loss.

## M

### Model projection

A stable, canonical subset of a domain model used in conformance tests. It
avoids binding tests to irrelevant internal object layout.

## N

### Normalization

Changing representation while intending to preserve semantics, for example
canonical padding or line ending. Normalization can still matter for exact
preservation and must be reported according to policy.

## P

### Parse

Read structural elements from bytes. Parsing alone neither proves semantic
validity nor guarantees a complete domain model.

### Preservation policy

The explicit statement of which source properties a read/write or conversion
path preserves, canonicalizes, approximates or drops.

### Probe

A bounded operation that ranks plausible format/version candidates and reports
evidence. Probe is not full parsing or validation.

### Provenance

Recorded origin, history, rights and relevant transformations of a source or
test file.

## R

### Reader

A component that decodes a confirmed format/version into a domain model. A
reader reports unsupported and malformed elements rather than silently
discarding them.

### Recovery

An explicit best-effort operation for damaged files. Recovered content carries
heuristics, confidence and gaps and is never relabelled as formally valid.

### Reference program

A named historical or independent application used to create or inspect files
for empirical comparison. It is evidence, not automatically the normative
definition.

### Resource budget

Limits on allocation, bytes, records, nesting, expansion, steps or time for one
operation.

### Round-trip

A read followed by a write and another verification step. Its success is
defined per format: semantic preservation, normalized equivalence or exact
bytes must not be conflated.

## S

### Stable

The highest project support state, awarded only after specification,
implementation, security, conformance, documentation and acceptance criteria
are complete for the stated capability.

### Strict mode

Normal processing that enforces the selected format/profile rules and rejects
invalid structures according to policy. It is separate from Recovery.

### Support claim

A statement that a named version/profile and capability meet a defined project
status. A family name in a roadmap is not a support claim.

## T

### Test fixture

A specific file or generated byte sequence used by a test, accompanied by
expected properties and provenance.

### Toolchain profile

A documented compiler, linker, flags, target, memory model and runtime
combination used for a build claim.

### Transformation

An explicit, named conversion step applied to a domain model, with documented
preconditions, result and possible loss.

## V

### Validate

Check structure and semantics against a selected version/profile. Validation
reports rule violations and is distinct from successful decoding.

### Variant

A materially different manufacturer, platform or application interpretation
within a format family.

## W

### Writer

A component that encodes a domain model into one explicitly selected
format/version/profile after planning compatibility and loss.

## Z

### Zeichensatz / character encoding

A mapping between byte sequences and character values. Host locale, filename
encoding and file-content encoding are separate concepts.

