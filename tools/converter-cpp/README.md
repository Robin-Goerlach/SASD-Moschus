# Moschus C++ converter

This directory will contain the C++20 command-line converter.

Planned commands:

```text
moschus info <file>
moschus validate <file>
moschus convert <input> --to <format> --output <file>
moschus formats
```

The converter is intentionally thin. It performs argument handling, selects
library capabilities, renders diagnostics, and chooses exit codes. All format
detection, parsing, validation, writing, and conversion logic belongs in the
public C++ library.

Conversions that may lose information must require explicit acknowledgement
and produce machine-readable as well as human-readable diagnostics.
