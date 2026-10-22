# AGENTS.md — SASD Moschus

This file is the repository-wide operating contract for Codex and other coding
agents. It applies to the repository root and every subdirectory unless a more
specific `AGENTS.md` or `AGENTS.override.md` exists below it.

The goal is high autonomy with evidence: inspect the live repository, make the
smallest correct change, test it thoroughly in WSL, update the owned
documentation, and leave a clean, understandable result.

## 1. Project mission

SASD Moschus is an open-source, multi-language project for identifying,
reading, validating, recovering, writing and converting historical file
formats.

The first format horizon ends on **31 December 1990**. The first implementation
horizon uses:

- a portable ANSI C89 / ISO C90 core;
- a C++ library/facade using the explicitly approved early compiler subset;
- a C++ command-line converter;
- shared language-neutral specifications and conformance tests;
- later independent C# and Java libraries;
- later, separately controlled C++98, C++03, C++11, C++14, C++17 and C++20
  language epochs.

Correctness, transparent information loss, security, historical accuracy and
evidence take priority over the number of nominally supported formats.

## 2. Current project phase

The repository is in the foundation/M0 phase unless the live `ROADMAP.md`,
coverage matrix and Git history show that a later milestone has been accepted.

At foundation time:

- no file format is production-ready merely because it appears in a plan;
- public C/C++ APIs are not frozen;
- exact historical compiler versions remain ADR decisions;
- format candidates remain `Research` until the required evidence exists;
- implementation must not jump ahead of unresolved foundational ADRs.

Always derive the current state from the checked-out branch. Do not rely on a
previous chat, memory, issue description or this paragraph when the repository
contains newer evidence.

## 3. Authority and sources of truth

Read only what is relevant, but respect this order:

1. law, licences and explicit user instructions;
2. `LASTENHEFT.md` — product need, scope and acceptance;
3. `PFLICHTENHEFT.md` — technical requirements;
4. `ARCHITECTURE.md` — boundaries, components and architecture rules;
5. accepted files under `docs/adr/` — named design decisions;
6. version-specific files under `specifications/` — on-disk format behaviour;
7. conformance manifests and corpus metadata;
8. public API/CLI documentation;
9. implementation details.

Supporting documents:

- `README.md` — project overview;
- `ROADMAP.md` — milestone order and current work;
- `docs/format-coverage.md` — exact claimed support state;
- `CONTRIBUTING.md` — contribution and review workflow;
- `SECURITY.md` — vulnerability and secure-processing policy;
- `docs/SOURCE-AND-CORPUS-POLICY.md` — evidence and fixture rights;
- `docs/RELEASE-PROCESS.md` — releases and immutable tags;
- `docs/GLOSSARY.md` — project terminology;
- `GOVERNANCE.md` — decision authority.

If two sources conflict, do not choose silently. Identify the conflict, follow
the higher-authority document for reversible work, and stop before an
irreversible or public decision.

## 4. Instruction scope

Codex discovers agent instructions from repository root toward the current
working directory. A deeper file may refine commands, style or tests for its
subtree. It must not silently weaken root security, copyright, format-version,
testing or historical-accuracy rules.

When adding a subtree `AGENTS.md`:

- keep it local to that subtree's technology and commands;
- link rather than repeat this root file;
- state exactly which paths it covers;
- avoid contradictory definitions of Done;
- use `AGENTS.override.md` only for a deliberate complete local override.

## 5. Default autonomy

For an implementation request, proceed end to end without asking the user to
approve routine steps:

1. inspect repository state and applicable instructions;
2. locate the current milestone and relevant requirements;
3. inspect existing code/tests/history before designing;
4. make reasonable, reversible assumptions;
5. add or update tests;
6. implement the smallest complete slice;
7. run focused and broader verification;
8. update specifications, coverage and user documentation when affected;
9. review the diff for security, scope and unintended changes;
10. report the observed result and remaining limitations.

Do not stop after writing a plan when the user asked for implementation. Do not
ask for information that can be obtained safely from repository files, tool
help, compiler output or focused experimentation.

### 5.1 Make autonomous assumptions when

- the choice is local, conventional and easily reversible;
- existing project patterns clearly establish the answer;
- the conservative option meets all higher-level requirements;
- a temporary implementation detail does not freeze a public contract;
- tests can prove the assumption.

Record a meaningful assumption in code comments, an ADR proposal, the task
summary or an open-question table as appropriate.

### 5.2 Stop and ask only when

- product scope or an acceptance criterion genuinely changes;
- a missing decision would freeze a public API/ABI/schema incorrectly;
- alternatives differ materially in data preservation or historical accuracy;
- a destructive action, force push, tag move or history rewrite is required;
- rights to a source, fixture, book disk or binary are unclear;
- credentials, paid services or new external authority are required;
- an existing dirty change overlaps the same code and cannot be preserved;
- the requested action would weaken a security boundary;
- an unrecoverable migration or broad dependency addition needs approval;
- repository evidence contradicts the user's stated baseline in a way that
  would make the requested change invalid.

When blocked, provide the exact evidence, affected paths and two or three
concrete options. Continue any independent safe work first.

## 6. Mandatory WSL preflight

Assume development runs in a Linux distribution under WSL unless the live
environment proves otherwise.

At the beginning of a coding task, run a concise read-only preflight:

```sh
pwd
git status --short --branch
git log -5 --oneline --decorate
uname -a
printf 'WSL_DISTRO_NAME=%s\n' "${WSL_DISTRO_NAME-}"
```

Then inspect only relevant files with `rg --files`, `rg`, `sed` or dedicated
tools. Determine:

- repository root and current branch;
- clean/dirty/untracked state;
- applicable nested agent instructions;
- active milestone and ADRs;
- available build manifests and scripts;
- compiler/tool versions needed by the task;
- whether the repository is on the Linux filesystem or a Windows mount.

Do not dump all environment variables. They may contain secrets.

## 7. WSL working rules

### 7.1 Paths and filesystem

- Prefer a repository stored in the WSL Linux filesystem for C/C++ build
  performance and predictable permissions.
- Work correctly if the user chose `/mnt/c` or another Windows mount; do not
  relocate the repository without permission.
- Use POSIX paths inside WSL.
- Quote paths and filenames safely.
- Do not assume case-insensitive filenames.
- Do not create files that differ only by case.
- Keep source and repository text as UTF-8 without BOM unless an exact test
  fixture requires other bytes.
- Use LF for project text files. Do not normalize binary corpus files.
- Preserve executable bits deliberately.
- Avoid placing build output or temporary files in tracked source directories.

### 7.2 Windows interoperability

- Do not invoke Windows tools or PowerShell from WSL unless the task requires
  a Windows-specific verification or the native WSL tool is unavailable.
- Treat Windows and WSL tool installations as separate toolchains.
- Do not assume a Windows `git`, `cmake`, compiler or environment variable is
  visible or compatible in WSL.
- When comparing outputs across Windows and WSL, separate platform differences
  from file-format semantics.
- Never embed drive-specific absolute paths in source, tests or manifests.

### 7.3 Packages and system changes

- Use already installed tools first.
- Prefer repository-local or documented build dependencies.
- Do not run `sudo`, modify the distribution, enable services or install system
  packages without explicit user authority.
- If a package is essential, identify the exact Debian/Ubuntu package and why;
  continue all work that does not require it.
- Do not curl-and-execute installation scripts.

## 8. Repository inspection

Use `rg`/`rg --files` before broad directory listings or slow searches.

For every task:

1. find applicable `AGENTS.md`/`AGENTS.override.md` files;
2. inspect `git status` before edits;
3. inspect relevant recent commits when behaviour or intent is unclear;
4. search for existing names, APIs, tests and similar modules;
5. read the relevant requirement/architecture sections;
6. inspect build/test commands from repository files, not memory;
7. identify generated files and their generators;
8. preserve unrelated user work.

Never infer that a feature is missing from a filename alone. Search code,
tests, specifications, history and coverage state.

## 9. Planning and task sizing

For a small local change, plan mentally and proceed.

For a complex feature, new codec, public API, major refactor, migration or work
expected to span several sessions, create or update a self-contained execution
plan under `docs/plans/` after its scope is clear. Use a filename such as:

```text
docs/plans/M1-checked-arithmetic.md
docs/plans/M3-dbase-iii-reader.md
```

An execution plan must include:

- status and last update;
- source requirements, ADRs and specifications;
- objective and observable outcome;
- in-scope and explicit non-goals;
- prerequisites and decisions;
- files/components expected to change;
- red/green/refactor steps;
- focused and full verification commands;
- security, resource, portability and recovery concerns;
- acceptance criteria;
- evidence and decision log;
- remaining work and restart instructions.

Keep the plan current while implementing. A plan is not evidence that work or
tests succeeded. Do not create planning bureaucracy for a one-file obvious fix.

## 10. Change discipline

- Make the smallest coherent change that fully satisfies the task.
- Preserve established architecture and naming.
- Do not refactor unrelated code opportunistically.
- Separate mechanical formatting from behavioural changes.
- Do not create placeholder public APIs merely to fill a directory.
- Do not add dependencies for functionality that is small and safe to
  implement with existing project primitives.
- Generated files are changed through their generator when one exists.
- Keep source, tests, specification and coverage state consistent.
- Do not claim support beyond the tested exact version/profile.

Use `apply_patch` for deliberate text edits when available. Formatting or
generator tools may perform mechanical rewrites after the intended source
change is reviewed.

## 11. Git safety and branch behaviour

### 11.1 Preserve work

- Treat all existing modifications and untracked files as user work.
- Never run `git reset --hard`, `git clean -fd`, destructive checkout/restore or
  broad deletion unless the user explicitly requests the exact action.
- Do not use `git stash` to hide unexpected changes without explaining it.
- Do not amend, rebase or squash commits that may already be public unless
  explicitly authorised.
- Never force-push `main`.
- Never move a published release or epoch tag.

### 11.2 Branch selection

- Work on the current branch unless the user or repository workflow requires a
  new branch.
- When the user explicitly requests direct work on `main`, first confirm that
  local `main` is current and that the intended update is fast-forward-safe.
- Do not switch branches with overlapping dirty changes.
- Fetch before relying on remote state when network access and authority exist.

### 11.3 Commits and pushes

Editing authority does not automatically grant commit or push authority.

- Commit and push only when the user explicitly asks, the active workflow says
  to do so, or the task clearly includes repository publication.
- Before commit, run required tests and `git diff --check`.
- Inspect the staged diff; do not stage unrelated files.
- Use small imperative commit subjects, for example:
  - `core: add checked offset addition`
  - `dbase: parse dBASE III field descriptors`
  - `tests: cover truncated GIF extension`
  - `docs: define format identifier policy`
- If pushing, use a normal fast-forward push and verify the resulting remote
  commit.

## 12. C89/C90 core rules

Code under `libraries/c89/` must remain valid for the active strict C90 profile
and the selected historical toolchains.

### 12.1 Language subset

- use C89/C90 syntax only;
- use `/* ... */` comments, not `//`;
- place declarations before statements where required by the target subset;
- no variable-length arrays;
- no designated initializers;
- no compound literals;
- no `inline`, `_Bool`, `restrict` or C99-only library assumptions;
- no unconditional `long long`, `stdint.h` or newer headers;
- no assumptions about `char` signedness;
- no assumptions about type width, alignment or host byte order;
- avoid undefined, unspecified and implementation-defined behaviour where file
  interpretation would depend on it.

### 12.2 API and state

- prefix public symbols consistently after the relevant ADR decides the prefix;
- make ownership and lifetime explicit;
- pass operation context explicitly;
- no mutable global codec state;
- no direct output to stdout/stderr;
- no process exit from library code;
- return structured status and diagnostics;
- make allocation failure a normal tested path;
- keep public structs opaque when required for compatibility.

### 12.3 Portability boundary

- keep compiler/OS conditionals in `platform/` whenever practical;
- do not fork format semantics by compiler;
- verify integer-width requirements;
- use project checked arithmetic and endian accessors;
- use bounded stream/slice APIs;
- test modern safety builds even when retro compilers accept the source.

## 13. C++ rules

- Use only the active language epoch defined by accepted ADRs and build files.
- Before ADR-0002, do not freeze a public early-C++ subset by accident.
- The C++ layer preserves C-core status, diagnostics, limits and format IDs.
- The converter uses public C++ APIs only.
- Do not duplicate parsers or loss rules in the CLI.
- RAII, exceptions, templates and standard-library facilities may be used only
  when supported by the active epoch and compiler matrix.
- A language-standard migration and a format-behaviour change belong in
  separate commits and verification steps.

## 14. Other language implementations

For C# and Java:

- implement shared semantics idiomatically;
- use the same format IDs and diagnostic codes;
- consume the same conformance manifests;
- keep resource bounds despite managed memory;
- never use the host-default charset silently;
- do not claim native support for a subprocess wrapper;
- report coverage per language and exact version;
- do not start a public implementation before its baseline ADR and shared
  contracts are stable.

## 15. Format implementation workflow

For a new format/version/profile, follow this sequence:

1. identify the exact format/version and historical cutoff status;
2. add or refine its coverage row without overstating status;
3. record sources and evidence classes;
4. create/update the language-neutral format specification from
   `docs/FORMAT-SPECIFICATION-TEMPLATE.md`;
5. define probe evidence and ambiguity;
6. define domain-model mapping;
7. define validation, resource and security rules;
8. define strict behaviour and separate recovery heuristics;
9. add lawful fixtures and corpus metadata;
10. add conformance cases;
11. implement Probe/Read/Validate before complex Write where practical;
12. add Writer, preservation and round-trip tests;
13. add only meaningful conversion routes with loss planning;
14. raise capability status only after its exit criteria pass.

Do not implement from a file extension or a single unverified sample.

## 16. Format precision

Every format change must consider:

- family, variant, version and profile;
- marketing version versus on-disk version;
- byte order and primitive representation;
- platform and application deviations;
- character encoding and line endings;
- companion files;
- unknown/reserved records;
- lengths, offsets, counts and alignment;
- compression and expansion limits;
- active content and external references;
- canonical writing and preservation levels;
- exact, semantic and subset round trips.

Access and JPEG are not part of the 1990 acceptance. Do not pull later format
features into an earlier writer because they are easier to implement.

## 17. Security requirements

Treat every input byte and metadata value as hostile.

Mandatory controls:

- checked addition, subtraction and multiplication;
- range validation before seek, access or allocation;
- bounded streams and substreams;
- maximum input/output/allocation/record/depth/step limits;
- decompression output and ratio limits;
- cycle detection or hard traversal limits;
- safe companion-file resolution supplied by the caller;
- transactional output and cleanup after failure;
- no automatic execution of macros, scripts, printer commands or programs;
- no implicit network access;
- no uncontrolled materialization of embedded paths;
- no weaker limits in recovery/debug mode;
- no sensitive file content in ordinary diagnostics.

For a potential vulnerability, follow `SECURITY.md`. Do not place an exploit or
confidential sample in a public issue or commit.

## 18. Copyright, provenance and test data

- Do not copy scans, substantial text, tables, listings or disk contents from
  Kussmann, Born or other books without a separate legal basis.
- Physical ownership does not establish redistribution permission.
- Do not commit proprietary applications, compilers, SDKs, headers, libraries,
  keys or disk images.
- Every corpus file needs origin, rights, privacy review, exact hash and
  expected properties.
- Prefer deterministic synthetic fixtures with invented non-personal content.
- Keep non-redistributable evidence outside the repository; commit only an
  approved metadata/hash reference.
- Inspect hidden/deleted content and embedded metadata before accepting a real
  historical file.

When rights are unclear, stop distribution work and continue with a synthetic
fixture or documentation of the open question.

## 19. Testing strategy

### 19.1 Red, green, refactor

For behavioural fixes and features:

1. add the smallest meaningful failing test or conformance case;
2. confirm it fails for the expected reason when practical;
3. implement the minimum correct behaviour;
4. confirm the focused test passes;
5. refactor without broadening scope;
6. run the relevant broader suite;
7. run formatting/static checks and `git diff --check`.

For pure documentation or build metadata, use the closest objective validation
instead of manufacturing a meaningless failing test.

### 19.2 Required test classes

Select all relevant classes:

- primitive unit tests;
- minimal and representative valid files;
- invalid values and structures;
- truncation at every meaningful boundary;
- integer overflow and allocation failure;
- record/count/depth/resource limits;
- unknown records/extensions;
- deterministic writer output;
- preservation/round-trip contract;
- conversion plan and actual losses;
- historical reference-program behaviour;
- cross-language conformance;
- regression test for every corrected defect;
- fuzzing/sanitizer coverage for complex parsers.

### 19.3 Test truthfulness

- Never say tests passed unless they were run in the current worktree.
- Report the exact command and summarized result.
- Distinguish pass, fail, unsupported, skipped and not run.
- A pre-existing failure must be reproduced and separated from the new change.
- Do not delete or weaken a test merely to make the suite green.
- Do not substitute a parser smoke test for semantic validation.

## 20. Build and verification commands

Discover commands from the live repository. Do not invent `make test`, CMake
targets or package commands before their files exist.

When the corresponding infrastructure exists, use a progression like:

1. focused unit/conformance test;
2. affected component build;
3. full free reference build/test;
4. strict C90 warnings-as-errors profile;
5. modern sanitizer/static analysis profile;
6. package/example smoke tests;
7. local historical compiler procedure when required and available.

Always finish text/code changes with:

```sh
git diff --check
git status --short
```

Inspect the final diff. If no automated build exists yet, run objective
documentation checks available in the repository and state the limitation.

## 21. Diagnostics and errors

- Use stable machine-readable diagnostic codes.
- Human messages may be translated; tests must not depend on full prose.
- Preserve severity, category, source location, format context and loss class.
- Distinguish invalid data, unsupported feature, resource limit, I/O failure,
  rejected loss policy and internal contract failure.
- Partial or recovered results carry an explicit completeness state.
- Libraries do not log or print unless the caller supplies a diagnostic sink.
- Never turn an internal error into an ordinary invalid-file message to hide a
  defect.

## 22. Documentation updates

Update the documents owned by a behaviour change in the same task:

- exact format specification;
- `docs/format-coverage.md`;
- conformance manifest and corpus metadata;
- public API/CLI documentation;
- examples;
- source notes;
- relevant ADR;
- `CHANGELOG.md` for user-visible changes;
- `ROADMAP.md` only when milestone scope/status changes.

Do not duplicate normative rules across many files. Link to the owning source
and summarize only what the local reader needs.

Documentation and code comments should normally be clear technical English for
the public project. German is appropriate in the established German
requirements and architecture documents. Preserve the existing language of a
document unless the task includes translation.

## 23. Comments and readability

The user wants code to remain understandable. Add comments where they explain:

- why a historical rule exists;
- why a boundary/overflow check is necessary;
- why a compiler workaround is safe;
- what a non-obvious invariant protects;
- which specification rule or ADR applies;
- why a recovery heuristic is bounded.

Do not add comments that merely repeat syntax. Prefer small functions, clear
names and explicit contracts. Public functions require ownership, errors,
limits and format applicability documentation.

## 24. Dependency policy

- Keep runtime dependencies minimal.
- Prefer project primitives for byte parsing, bounds and diagnostics.
- New dependencies require licence, maintenance, platform and retro-toolchain
  analysis.
- Do not add a dependency that prevents the active historical profile unless
  it is isolated to a later language/tool layer.
- Pin/version release-time tools when reproducibility requires it.
- No build step may fetch executable code unexpectedly.
- Do not vendor dependencies or generated copies without a documented reason.

## 25. Performance and resource work

- Optimize only after correctness and safety.
- Use representative files and record the command/environment.
- Measure memory separately from elapsed time.
- Prefer bounded streaming/iteration for large records and blobs.
- Do not bypass validation or diagnostics in a fast path.
- Avoid full-file allocation when the format permits incremental processing.
- Keep deterministic count/depth/byte limits even when optional wall-clock
  limits are available on modern WSL hosts.

## 26. Review before completion

Perform a self-review of the final diff:

### Scope

- Does every changed file serve the requested task?
- Did the change cross a milestone or public-contract boundary?
- Are assumptions explicit and reversible?

### Correctness

- Is the exact format/version/profile named?
- Are unknown and malformed values handled?
- Are byte order, encoding and host-width assumptions removed?
- Do diagnostics match the operation outcome?

### Security

- Are lengths/offsets/counts checked before use?
- Can allocation, recursion, expansion or traversal grow without a limit?
- Can active content, paths or external references escape the trust boundary?
- Are temporary/partial outputs cleaned safely?

### Portability

- Does C code remain within the active C90 subset?
- Are compiler branches localized?
- Did WSL-specific behaviour leak into format semantics?
- Are line endings, locale and filesystem order deterministic?

### Evidence

- Did relevant tests actually run?
- Are specification, coverage, fixtures and docs consistent?
- Are rights/provenance recorded?
- Does the final report state remaining limitations honestly?

## 27. Definition of Done

A task is complete when:

- the requested observable behaviour exists;
- the change respects requirements, architecture and active ADRs;
- relevant tests cover success, failure and boundaries;
- focused and appropriate broader verification pass;
- security and resource implications are addressed;
- exact format/version status is truthful;
- documentation and changelog are updated where owned;
- no unrelated user changes were overwritten;
- `git diff --check` is clean;
- the final worktree state is known and reported;
- commit/push is completed and remotely verified only when authorised;
- remaining risks or unrun tests are explicit.

“Code written” is not Done. “Works on one sample” is not Done. “Compiler
accepted it” is not proof of format correctness.

## 28. Final report

Lead with the outcome. Include:

- what changed and why;
- important files/modules;
- exact tests/checks run and their results;
- format/compiler/platform scope;
- remaining limitations or decisions;
- commit/branch/remote result when relevant.

Keep the report concise relative to the work. Do not paste full command logs;
summarize material evidence. If blocked, name the blocker precisely and state
what is already complete.

## 29. Prohibited shortcuts

Do not:

- claim broad family support from one sample;
- infer format only from extension;
- merge strict parsing and recovery silently;
- accept information loss without a diagnostic/policy;
- use unbounded allocation or decompression;
- execute active embedded content;
- copy copyrighted book/disk content into the repository;
- distribute proprietary toolchains;
- add hidden network or telemetry behaviour;
- make the converter a second implementation of codecs;
- bypass public APIs for convenience;
- start later language epochs before the current epoch is tagged;
- edit generated artifacts independently of their source;
- hide failing tests or dirty files;
- force-push, move tags or destroy local work;
- invent build/test success.

## 30. Official Codex references

This repository policy is informed by the official OpenAI guidance that Codex
loads `AGENTS.md` as persistent repository context and combines instructions
from root to the current directory:

- https://developers.openai.com/cookbook/examples/gpt-5/codex_prompting_guide
- https://developers.openai.com/cookbook/examples/codex/iterating-development-workflows-with-codex

Repository requirements remain authoritative for Moschus-specific behaviour.
