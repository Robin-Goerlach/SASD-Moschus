# Moschus C++ converter

This directory contains the C++ command-line consumer of the public Moschus
C++ library.

## Architectural role

The converter orchestrates library operations and renders results. It does not
contain private parsers, writers or conversion semantics. If a capability
cannot be used through the public library, the API must be improved rather than
adding a CLI-only shortcut.

## Planned commands

```text
moschus formats
moschus probe <file>
moschus info <file>
moschus validate <file>
moschus convert <source> <target>
```

Exact syntax is decided in ADR-0008.

## Responsibilities

- parse arguments and configuration;
- construct explicit policies and resource limits;
- call public C++ application services;
- render human-readable output;
- render versioned machine-readable output;
- map structured results to stable process status codes;
- protect existing targets from accidental overwrite;
- support dry-run through the same Conversion Planner.

## Non-responsibilities

- format probing logic beyond passing caller hints;
- validating or rewriting model internals;
- deciding an undocumented default format version;
- suppressing diagnostics to make conversion appear successful;
- executing active embedded content;
- performing implicit network access.

## Output contract

Human output may evolve and be localized. Automation uses the versioned
machine schema and stable diagnostic IDs. Data and operational diagnostics are
kept distinguishable. Colour is optional and never the sole meaning carrier.

## Language epochs

The initial converter uses the early C++ subset selected for the 1990 epoch.
After the `format-era-1990` tag it advances through C++98, C++03, C++11, C++14,
C++17 and C++20 in separate migrations.

## Testing

- argument and status-code tests;
- golden machine-output schema tests;
- end-to-end format/conversion cases through public APIs;
- overwrite, temporary-file and partial-failure tests;
- non-seekable input cases where supported;
- platform path and encoding cases;
- no duplicated parser behaviour.

