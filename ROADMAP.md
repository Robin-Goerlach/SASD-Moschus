# Roadmap

This roadmap describes the intended order of work. Scope is refined when the
1992 Born edition and the 1989 Kussmann edition have been indexed at the level
needed for implementation.

## M0 — Foundation

- repository and source-provenance structure;
- architecture decisions;
- exact 1990 cutoff policy;
- format/version coverage matrix;
- conformance manifest design;
- C++20 build and test baseline.

Estimated cumulative point: approximately 45 commits.

## M1 — Plain and tabular exchange

- ASCII DELIMITED;
- SDF;
- CSV profiles;
- encoding and line-ending handling;
- initial neutral tabular model;
- `info`, `validate`, and minimal `convert` commands.

Estimated cumulative point: approximately 75 commits.

## M2 — dBASE

- DBF version detection;
- dBASE II, III, III Plus, and IV records where verified;
- memo and index companion formats as separately scoped codecs;
- deleted records, code pages, numeric/date semantics, and round trips.

Estimated cumulative point: approximately 130 commits.

## M3 — Interchange formats

- DIF;
- SDI and SIF where sufficiently specified;
- SYLK base records and verified extensions;
- cross-format tabular conformance tests.

Estimated cumulative point: approximately 185 commits.

## M4 — Historical spreadsheets

- Lotus WKS/WK1 and applicable 1-2-3 variants;
- related chart or picture records where in scope;
- formula and formatting preservation policy.

Estimated cumulative point: approximately 240 commits.

## M5 — Documents

- early Microsoft Word variants;
- WordStar;
- WordPerfect versions within the cutoff;
- RTF and DCA/RFT profiles;
- document-domain conversion diagnostics.

Estimated cumulative point: approximately 330 commits.

## M6 — Raster and chunk-based formats

- PCX and GEM IMG;
- IFF families selected by the coverage matrix;
- GIF87a and GIF89a;
- contemporary TIFF profiles;
- early Windows and OS/2 bitmap/icon variants.

Estimated cumulative point: approximately 405 commits.

## M7 — Vector, metafile, and print formats

- GEM metafiles, CGM, and WPG;
- DXF/DXB and WMF profiles within the cutoff;
- HP-GL, PCL, and EPS subsets with explicit capability limits.

Estimated cumulative point: approximately 480 commits.

## M8 — 1990 release hardening

- complete conversion diagnostics;
- malformed-input and resource-limit tests;
- cross-language conformance;
- documentation and examples;
- support-matrix audit;
- release candidate and compatibility review.

Estimated cumulative point: approximately 540 commits, with reserve up to
roughly 650 if undocumented application variants require separate handling.

## Beyond 1990

Subsequent milestones move the historical cutoff forward. They may include
Microsoft Access, JPEG-era formats, later Office generations, modern archives,
and contemporary interchange formats. They are not part of the first baseline.
