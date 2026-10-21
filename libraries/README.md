# Language libraries

Each subdirectory contains an independent native implementation of the Moschus
library contracts.

Initial implementations:

- [C++20](cpp/) — reference implementation and converter dependency;
- [C#/.NET](csharp/) — native managed implementation;
- [Java](java/) — native JVM implementation.

Libraries share the canonical specifications and conformance corpus. They do
not call the C++ implementation through a foreign-function interface unless a
separate optional adapter is introduced later.

Public APIs should feel natural in their language while preserving equivalent
format identifiers, diagnostics, compatibility states, and safety guarantees.
