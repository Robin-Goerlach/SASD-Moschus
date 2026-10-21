# Compiler and platform compatibility

This directory centralises all compiler, operating-system, file-system, integer,
memory-model, and DOS compatibility code.

Planned areas include:

- compiler detection and capability macros;
- fixed-width integer substitutes for the C89/C90 epoch;
- byte-order helpers;
- file and stream adapters;
- checked arithmetic and resource limits;
- 16-bit DOS memory-model support;
- generation of 8.3-compatible source bundles;
- build profiles for GCC, Borland, and Microsoft toolchains.

Format codecs must not scatter compiler detection across their implementation.
Every unavoidable compiler-specific branch belongs here or requires a recorded
architecture decision.
