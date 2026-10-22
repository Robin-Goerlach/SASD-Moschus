# Examples

Examples demonstrate supported public APIs with small, redistributable inputs.
They are documentation and release-tested clients, not hidden test utilities.

## Planned organization

```text
examples/
├── c89/
├── cpp/
├── csharp/
└── java/
```

Only directories with a real runnable example should be created.

## Example progression

For each active language, provide examples for:

1. list formats and capabilities;
2. probe an unknown stream;
3. read and inspect a model;
4. validate with structured diagnostics;
5. write an explicit target version;
6. plan and perform a conversion;
7. set resource limits;
8. invoke recovery and distinguish partial results;
9. resolve companion files safely.

## Rules

- compile against public installed headers/packages;
- use only redistributable corpus data or generated in-memory bytes;
- show status and diagnostics, not only the happy-path value;
- set or explain format/version and loss policies;
- avoid platform-specific code unless the example is explicitly platform-
  specific;
- remain small enough to read as teaching material;
- be built/tested in the relevant release pipeline.

An example cannot be used as evidence that a format is Stable unless the same
behaviour is covered by conformance tests.

