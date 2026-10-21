# Moschus portable C89/C90 core

This directory is reserved for the portable implementation core of the 1990
language epoch.

The core will contain bounded byte and text primitives, resource limits,
diagnostics, neutral model foundations, format probing, and the codecs selected
for the first historical release. It must compile in strict C90 mode with GCC
and is intended to remain compatible with the exact Borland and Microsoft C
toolchains selected by ADR-0002.

The official converter remains a C++ program and consumes this core through a
documented public interface.

No public headers are introduced until ADR-0001 and ADR-0002 define the API,
compiler matrix, integer model, error contract, and DOS memory profile.
