# Shared conformance suite

This directory will contain language-neutral manifests describing expected
behaviour for every supported format/version.

A conformance case should identify:

- format and version;
- fixture checksum and provenance;
- expected detection result;
- expected model or selected semantic assertions;
- expected diagnostics;
- expected strict-mode and recovery-mode outcomes;
- required round-trip properties;
- resource limits relevant to the case.

Every language implementation must report which conformance revision it passes.
Implementation-specific unit tests remain inside the corresponding library.
