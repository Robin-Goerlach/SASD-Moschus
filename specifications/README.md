# Format specifications

`specifications/` is the canonical, language-neutral description of exact
file-format versions and profiles.

## Authority

Implementations follow accepted specifications. If observed code behaviour and
a specification disagree, investigate and update the correct artifact with
evidence; do not silently make code the new specification.

## Planned layout

```text
specifications/
├── tabular/
├── database/
├── document/
├── raster/
├── vector/
├── print/
└── shared/
```

Directories are created when the first real specification is added.

## Required process

1. add/version the coverage entry;
2. assign a stable format ID according to ADR-0006;
3. copy `docs/FORMAT-SPECIFICATION-TEMPLATE.md`;
4. record sources and evidence classes;
5. describe exact bytes, rules and unknown-value policy;
6. define security/resource analysis;
7. define preservation and round-trip contract;
8. link conformance cases;
9. obtain review before status `Accepted`/`Specified`.

## Precision rules

- one family name is not a version;
- filename extension is not proof;
- marketing and on-disk versions are mapped explicitly;
- byte order, encoding and platform assumptions are stated;
- offsets/counts include origins, ranges and overflow behaviour;
- unknown and reserved values have explicit policies;
- application deviations are separate from base rules;
- recovery heuristics are non-normative and separately marked;
- later features are never projected backward into the 1990 epoch.

## Review gates

Draft → Review requires a complete structure and source list.

Review → Accepted requires resolved contradictions or explicit open issues,
security analysis and enough fixtures to test the claimed capability.

Accepted specification → Stable codec additionally requires implementation,
conformance, documentation and release criteria outside this directory.

