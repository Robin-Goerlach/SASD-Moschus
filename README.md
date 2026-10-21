# SASD Moschus

SASD Moschus is an open-source, multi-language library project for reading,
writing, identifying, validating, and converting historical file formats.

The first compatibility horizon is the PC software landscape up to the end of
1990. Later milestones will move forward through subsequent format generations
without hiding historical differences behind a single ambiguous format name.

> [!IMPORTANT]
> The repository is in its foundation phase. The structure and support policy
> are being established; no file format is production-ready yet.

## Goals

- Preserve access to historical data through documented, testable codecs.
- Provide independent library implementations in multiple programming
  languages.
- Keep format knowledge language-neutral and shared.
- Detect exact format variants instead of trusting filename extensions.
- Read and write supported formats with explicit compatibility levels.
- Report every potentially lossy conversion instead of silently discarding
  information.
- Supply a C++20 command-line converter built on the C++ library.
- Progress from the 1989–1990 baseline toward current formats in dated,
  reviewable milestones.

## Project components

| Component | Purpose | Initial technology |
|---|---|---|
| Format specifications | Canonical, language-neutral description of each format and version | Markdown and structured data |
| C++ library | Reference implementation and foundation for the converter | C++20 |
| C# library | Native .NET implementation of the shared contracts | Modern .NET |
| Java library | Native JVM implementation of the shared contracts | Modern Java |
| Moschus converter | Inspect, validate, and convert files | C++20 |
| Conformance suite | Shared fixtures and expected results for every implementation | Language-neutral manifests |

Additional language implementations can be added under `libraries/` without
changing the specifications or test contracts.

## Architecture

Moschus avoids a direct converter for every possible pair of formats. Each
codec maps a file to an appropriate neutral domain model and back:

```text
historical file
      |
      v
format detector -> reader -> neutral model -> writer -> destination file
                         |          |
                         |          +-> conversion diagnostics
                         +-> validator
```

The initial domain families are expected to include:

- tabular data;
- formatted documents;
- raster images;
- vector drawings and metafiles;
- audio and other chunk-based media where covered by the historical scope.

A conversion is available only when the source and destination share meaningful
semantics. Moschus will not pretend that every format can sensibly be converted
to every other format.

See [ARCHITECTURE.md](ARCHITECTURE.md) for the design rules.

## Historical 1990 baseline

The exact list is controlled by
[docs/format-coverage.md](docs/format-coverage.md). Candidate families include:

- ASCII DELIMITED, SDF, CSV, DIF, SDI, SIF, and SYLK;
- dBASE II, III, III Plus, and IV data and companion files;
- Lotus 1-2-3 and related spreadsheet exchange formats;
- early Microsoft Word, WordStar, WordPerfect, RTF, and DCA/RFT;
- PCX, GEM IMG, IFF, GIF87a/GIF89a, contemporary TIFF variants, and early BMP;
- GEM, CGM, WPG, DXF/DXB, WMF, HP-GL, PCL, and EPS where they fall within the
  verified cutoff.

A name in this list is not a claim of current support. Every individual format
version must be researched, specified, implemented, and tested before its
status changes.

Formats introduced after the cutoff, including later Access and JPEG-era
targets, belong to subsequent historical milestones.

## Repository layout

```text
SASD-Moschus/
├── libraries/
│   ├── cpp/                 C++20 reference library
│   ├── csharp/              C#/.NET library
│   └── java/                Java library
├── tools/
│   └── converter-cpp/       C++ command-line converter
├── specifications/          canonical, language-neutral format specifications
├── tests/
│   ├── conformance/         shared manifests and expected behaviour
│   └── corpus/              redistributable test fixtures and provenance
├── examples/                small usage examples for each implementation
└── docs/
    ├── sources/             bibliographic notes and source provenance
    └── format-coverage.md   support matrix by format and version
```

## Compatibility levels

Each format/version will be assigned one of these states:

| State | Meaning |
|---|---|
| Research | Sources are being collected and reconciled |
| Specified | The Moschus specification is reviewable |
| Read | Valid files can be decoded into the neutral model |
| Write | The neutral model can be encoded in that version |
| Round-trip | Defined preservation tests pass |
| Convert | At least one meaningful conversion route is supported |
| Stable | Public API and behaviour are covered by compatibility guarantees |

Partial support must identify the unsupported records, fields, compression
methods, or application-specific extensions.

## Design principles

1. **Version before extension.** A suffix is a hint, not proof.
2. **No silent data loss.** Every dropped or approximated feature is reported.
3. **Strict and recovery modes.** Validation remains separate from best-effort
   archival recovery.
4. **Bounded parsing.** Lengths, offsets, allocations, recursion, and
   decompression are checked before use.
5. **Deterministic writing.** The same model and options should produce the same
   bytes whenever the format permits it.
6. **Independent implementations.** Libraries share specifications and
   conformance data, not foreign-function bindings to one hidden implementation.
7. **Documented provenance.** Technical claims and test files record where they
   came from and whether redistribution is permitted.
8. **Historical accuracy.** Later extensions are never silently emitted when a
   historical target version was requested.

## Sources and copyright

Two initial research references are:

- Ralf Kussmann, *Dateiformate und Konvertierung*, DATA BECKER, first edition,
  1989.
- Günter Born, *Referenzhandbuch Dateiformate: Grafik, Text, Datenbanken,
  Tabellenkalkulation*, Addison-Wesley, second revised edition / first unchanged
  reprint, 1992, ISBN 3-89319-446-0.

These books guide research and source comparison. They are not part of this
repository, and their text, illustrations, listings, or bundled software must
not be copied into Moschus without a separate legal basis. Implementations and
documentation must be independently written and, where possible, checked
against public standards and lawfully redistributable test files.

See [docs/sources/](docs/sources/) for the source notes.

## Roadmap

The planned sequence starts with infrastructure and simple tabular exchange
formats, then adds dBASE, spreadsheets, formatted documents, raster graphics,
vector/metafile formats, and finally broad conversion and hardening.

See [ROADMAP.md](ROADMAP.md) for the milestone outline. The 1990 baseline is
currently estimated at roughly 540 reviewable commits, with scope reserve for
poorly documented variants and interoperability findings.

## Building

Build instructions will be added with the first implementation milestone.
Until then, the repository intentionally contains architecture and directory
contracts rather than placeholder APIs that might prematurely become public.

## Contributing

Contributions should begin with a format/version entry in the coverage matrix
and a specification change. Code without provenance, boundary tests, and
conformance expectations is not considered complete.

Do not commit copyrighted book scans, proprietary application files, or sample
documents whose redistribution rights are unknown.

## License

SASD Moschus is licensed under the [MIT License](LICENSE).
