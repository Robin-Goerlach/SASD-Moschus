# Format specifications

This directory will contain Moschus's canonical, language-neutral format
specifications.

Each format family receives its own directory. A specification should define:

- stable family and version identifiers;
- signatures and detection rules;
- byte order, character encoding, and numeric representation;
- headers, records, chunks, fields, flags, and reserved values;
- offset, length, alignment, and termination rules;
- structural and semantic validation;
- version and application deviations;
- preservation and canonical-writing behaviour;
- resource limits and malformed-input handling;
- mappings to neutral domain models;
- references, verified fixtures, and unresolved questions.

Suggested future layout:

```text
specifications/
└── tabular/
    └── sdf/
        ├── specification.md
        ├── versions.yaml
        └── diagnostics.yaml
```

Structured files must describe behaviour shared by all language
implementations. They must not encode quirks of one library API.
