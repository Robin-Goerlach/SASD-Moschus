# Test corpus

This directory will contain only small, redistributable fixtures with documented
provenance and cryptographic checksums.

Corpus categories should include:

- minimal valid files;
- representative application-generated files;
- boundary values;
- truncated and malformed files;
- ambiguous signatures;
- preservation and deterministic-writing fixtures.

Do not commit:

- scans of reference books;
- bundled software from books;
- proprietary application binaries;
- personal or confidential documents;
- files with unknown redistribution rights.

Locally available research files belong in the ignored
`tests/corpus/private/` directory. Public manifests may describe their
properties without exposing copyrighted or sensitive bytes.
