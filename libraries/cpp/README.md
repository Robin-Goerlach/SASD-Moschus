# Moschus C++ library

This directory is reserved for the C++20 reference implementation.

Planned responsibilities:

- bounded byte and text input/output primitives;
- format registry and version probing;
- neutral domain models;
- readers, writers, and validators;
- conversion diagnostics;
- public CMake package;
- unit and integration tests.

The command-line converter in `tools/converter-cpp/` must depend only on this
library's public API.

No placeholder public API is committed during the foundation phase. The first
headers will be introduced together with tests and an architecture decision.
