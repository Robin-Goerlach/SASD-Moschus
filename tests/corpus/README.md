# Test corpus

This directory contains only lawfully redistributable fixtures plus complete
metadata. See `docs/SOURCE-AND-CORPUS-POLICY.md` for the governing policy.

## Planned layout

```text
tests/corpus/
├── generated/       deterministic project-created fixtures
├── licensed/        third-party fixtures with explicit permission
├── malformed/       minimized negative/security cases
├── metadata/        provenance and rights records
└── generators/      source for deterministic synthetic files
```

The concrete layout may be refined by ADR-0004 and corpus tooling.

## Admission requirements

Every file needs:

- stable fixture ID;
- exact size and cryptographic hash;
- source/creator and chain of custody;
- redistribution licence/permission;
- privacy and hidden-content review;
- exact format/version/profile claim;
- expected properties;
- companion-file relationships;
- specification and conformance links;
- reviewer and date.

## Prohibited material

- book scans or copied book disks without permission;
- proprietary applications, compilers, headers or libraries;
- customer data, credentials or private documents;
- unknown-provenance files;
- samples whose redistribution terms are merely assumed;
- malicious files without minimization and security review.

## Local non-redistributable evidence

Keep outside the repository. Commit only an approved metadata/hash reference
and provide an equivalent synthetic fixture where possible. Public CI never
downloads restricted material automatically.

## Integrity

Tests verify fixture hashes before interpreting results. A changed fixture is a
new reviewed artifact; do not silently replace bytes under an existing ID.

