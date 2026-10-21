# Roadmap

This roadmap implements the requirements in
[PFLICHTENHEFT.md](PFLICHTENHEFT.md). Scope is refined as the 1992 Born edition,
the 1989 Kussmann edition, primary specifications, and verified fixtures are
indexed.

The figures are planning ranges for small, reviewable commits. They are not a
substitute for the acceptance criteria in the requirements specification.

## M0 — Requirements and decisions

- maintain the requirements specification;
- create ADR-0001 for layers, diagnostics, and API boundaries;
- create ADR-0002 for exact GCC, Borland, Microsoft, DOS, and memory-model
  targets;
- define the 1990 cutoff and format identifier scheme;
- extend the format/version coverage matrix;
- define source provenance and conformance manifest schemas.

Estimated cumulative point: 35–50 commits.

## M1 — Portable 1990 foundation

- establish the ANSI C89 / ISO C90 core;
- add strict modern GCC C90 builds;
- centralise compiler and platform detection;
- define checked arithmetic, integer-width, byte-order, stream, error, and
  resource-limit primitives;
- create the DOS16 memory profile;
- prepare local Borland and Microsoft build procedures;
- generate 8.3-compatible source bundles without maintaining a second codebase;
- establish the early-C++ converter shell.

Estimated cumulative point: 90–130 commits.

## M2 — Plain and tabular exchange

- ASCII DELIMITED;
- SDF;
- historically accurate CSV profiles;
- encoding and line-ending handling;
- neutral tabular model;
- initial `info`, `validate`, `probe`, and `convert` commands.

Estimated cumulative point: 140–190 commits.

## M3 — dBASE

- DBF family and version detection;
- verified dBASE II, III, III Plus, and IV records;
- memo and index companions as separately scoped codecs;
- deleted records, code pages, numeric/date semantics, recovery, and round
  trips.

Estimated cumulative point: 230–300 commits.

## M4 — Interchange and spreadsheets

- DIF;
- SDI and SIF where sufficiently specified;
- SYLK base records and verified extensions;
- Lotus WKS/WK1 and applicable 1-2-3 variants;
- formula and formatting preservation policy;
- cross-format tabular conformance tests.

Estimated cumulative point: 310–390 commits.

## M5 — Documents

- early Microsoft Word variants;
- WordStar;
- WordPerfect versions within the cutoff;
- RTF and DCA/RFT profiles;
- document-domain model;
- explicit loss and capability diagnostics.

Estimated cumulative point: 430–540 commits.

## M6 — Raster and chunk-based formats

- PCX and GEM IMG;
- selected IFF families;
- GIF87a and GIF89a;
- TIFF revisions verified for the cutoff;
- early Windows and OS/2 bitmap/icon variants;
- palette, compression, metadata, and multi-image preservation rules.

Estimated cumulative point: 540–670 commits.

## M7 — Vector, metafile, and print formats

- GEM metafiles, CGM, and WPG profiles;
- DXF/DXB and WMF profiles within the cutoff;
- HP-GL, PCL, and EPS subsets with explicit capability limits;
- vector/metafile domain model;
- security rules that prevent command or embedded-code execution.

Estimated cumulative point: 650–780 commits.

## M8 — Full 1990 acceptance

- complete conversion planning and loss diagnostics;
- malformed-input, boundary, and resource-limit tests;
- cross-language-ready conformance manifests;
- modern sanitizer, static-analysis, and fuzzing runs;
- documented GCC and selected retro-compiler builds;
- complete user, API, format, source, and build documentation;
- support-matrix audit;
- release candidate, checksums, release notes, and `format-era-1990` tag.

Estimated cumulative point: 750–900 commits.

## M9 — C++98 language epoch

Only after the 1990 acceptance tag:

- define the C++98 migration plan and compiler matrix;
- introduce the first standard C++ public API;
- retain or adapt the portable core behind documented boundaries;
- migrate in small, behaviour-preserving commits;
- run the entire 1990 conformance suite unchanged;
- tag the completed language epoch.

## M10 and later — C++03 through C++20

Each of C++03, C++11, C++14, C++17, and C++20 receives a separate migration,
test, documentation, and acceptance step. New format horizons are planned
separately so that a language migration cannot conceal a codec behaviour
change.

Later format horizons may include Microsoft Access, JPEG-era formats, later
Office generations, modern archives, and current interchange formats.
