# Format coverage

This matrix is the planning authority for format and version support. A family
is not supported merely because it appears here.

States: **Research**, **Specified**, **Read**, **Write**, **Round-trip**,
**Convert**, and **Stable**.

| Domain | Family or version candidate | Cutoff status | Current state | Notes |
|---|---|---|---|---|
| Tabular | ASCII DELIMITED | Verify profile | Research | Delimiters, quoting, encoding, and line endings require profiles |
| Tabular | SDF | In scope | Research | Fixed-width field rules must be versioned |
| Tabular | CSV | Verify historical profile | Research | Modern CSV behaviour must not be projected backward |
| Tabular | DIF | In scope | Research | Version and application deviations pending |
| Tabular | SDI / SIF | Verify | Research | Include only with sufficient specification and fixtures |
| Tabular | SYLK | In scope | Research | Base records before application extensions |
| Database | dBASE II DBF | In scope | Research | Companion files tracked separately |
| Database | dBASE III / III Plus DBF | In scope | Research | Code-page behaviour requires fixtures |
| Database | dBASE IV DBF / DBT | In scope | Research | Index and memo variants require separate capability rows |
| Spreadsheet | Lotus WKS / WK1 | In scope | Research | Exact application versions pending |
| Document | Microsoft Word 3.0–5.0 candidates | Verify each version | Research | Binary structures and feature limits pending |
| Document | WordStar | In scope | Research | Exact revisions pending |
| Document | WordPerfect 5.0 candidate | Verify | Research | Later revisions excluded from the baseline |
| Document | RTF 1.0 profile | In scope | Research | Parser and writer subsets must be explicit |
| Document | DCA/RFT | In scope | Research | Profile and interchange semantics pending |
| Raster | PCX | In scope | Research | Header versions and palettes tracked separately |
| Raster | GEM IMG | In scope | Research | Compression variants pending |
| Raster | IFF ILBM candidates | Verify | Research | Chunk support will be capability-based |
| Raster | GIF87a / GIF89a | In scope | Research | Extension and preservation policy pending |
| Raster | TIFF variants available by cutoff | Verify each revision | Research | Later TIFF revisions excluded |
| Raster | Early BMP / OS/2 BMP / ICO | Verify each version | Research | Header family must be detected explicitly |
| Vector | GEM metafile / CGM / WPG | Verify each version | Research | Broad standards require bounded profiles |
| Vector | DXF / DXB | Verify each version | Research | Text and binary variants tracked separately |
| Vector | WMF | Verify cutoff profile | Research | Record capability matrix required |
| Print | HP-GL / PCL / EPS | Verify subsets | Research | No execution of embedded commands or code |

## Rules

1. Add a row for every materially different on-disk version.
2. Change a state only when the required specification and conformance evidence
   exist.
3. Record read and write support independently in detailed per-format
   specifications.
4. Do not infer support from a shared filename extension.
5. Post-1990 variants belong to later milestone tables.
