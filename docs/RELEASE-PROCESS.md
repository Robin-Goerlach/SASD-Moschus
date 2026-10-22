# Release process

| Field | Value |
|---|---|
| Version | 0.1 |
| Date | 22 October 2026 |
| Applies to | Libraries, converter, specifications and epoch tags |

## 1. Goals

A Moschus release must be reproducible, traceable and honest about exact format
capabilities. Publishing source archives is not sufficient; release evidence
connects requirements, specifications, builds, tests, licences and known
limitations.

## 2. Release types

| Type | Purpose | Typical version |
|---|---|---|
| Development snapshot | collaboration, no support promise | commit/nightly identifier |
| Alpha | early integrated capabilities, APIs unstable | `0.x.0-alpha.N` |
| Beta | feature-complete candidate scope, validation ongoing | `0.x.0-beta.N` |
| Release candidate | intended final artifacts under acceptance | `X.Y.Z-rc.N` |
| Stable product release | accepted public API/product state | `X.Y.Z` |
| Format-epoch tag | immutable historical scope completion | `format-era-1990` |
| Language-epoch tag | completed implementation-standard migration | named per accepted ADR |
| Security release | fixes an advisory with focused changes | patch/minor as appropriate |

## 3. Version dimensions

Never conflate:

- product semantic version;
- exact file-format version;
- format epoch;
- language epoch;
- manifest/schema version.

A release note reports all relevant dimensions.

## 4. Release roles

- **Product Owner:** accepts scope and milestone/epoch completion.
- **Release maintainer:** coordinates freeze, builds, evidence and publication.
- **Format maintainers:** confirm coverage claims and specifications.
- **Security reviewer:** checks unresolved security findings and mitigations.
- **Verifier:** independently checks artifacts and checksums where practical.

One person may hold several roles in the foundation phase, but the checklist
records who performed each action.

## 5. Preconditions

Before creating a release branch or candidate:

- target scope and version are approved;
- roadmap milestone exit criteria are understood;
- coverage matrix matches intended capabilities;
- required specifications and ADRs are accepted;
- all distributed fixtures have provenance and rights metadata;
- dependency and licence inventory is current;
- no unresolved critical/high security issue affects the scope;
- CI/reference builds are green at the candidate commit;
- changelog and migration notes are drafted.

## 6. Freeze and candidate commit

1. choose one exact commit;
2. ensure the worktree/build input is clean;
3. record source commit, tree and tool versions;
4. stop unrelated changes to the candidate;
5. generate source and binary packages only from that commit;
6. if a code/document change is required, create a new candidate rather than
   silently replacing artifacts.

The candidate number increases for every rebuilt content change. Identical
artifact regeneration must reproduce hashes or document the cause of allowed
variation.

## 7. Required verification

### 7.1 Documentation

- Lastenheft/Pflichtenheft/architecture references valid;
- coverage states agree with delivered code;
- CLI and API docs match behaviour;
- known limitations are complete;
- changelog contains user-visible changes;
- no Draft document is presented as accepted evidence.

### 7.2 Builds

- strict modern GCC C90 baseline;
- active C++ language-epoch builds;
- selected additional modern compilers;
- historical compiler reports required by the milestone;
- clean-package rebuild, not only developer-tree build;
- no unexpected network dependency.

### 7.3 Tests

- unit and integration tests;
- complete applicable conformance suite;
- negative, truncation and resource-limit tests;
- sanitizer/static-analysis runs on supported modern hosts;
- required fuzzing campaign or smoke suite;
- package install/use smoke tests;
- examples compiled/executed as appropriate.

### 7.4 Security and privacy

- security issue review;
- dependency/advisory review;
- temporary-file and overwrite behaviour checked;
- active-content non-execution confirmed;
- release logs contain no confidential data;
- distributed corpus privacy reviewed.

### 7.5 Legal and provenance

- project and third-party licences included;
- source/corpus metadata complete;
- no proprietary compiler/runtime files packaged;
- attributions included;
- generated artifacts identify their source/generator.

## 8. Artifact set

Depending on project stage:

- canonical source archive;
- 8.3-compatible historical source archive;
- supported modern binary packages;
- documentation bundle;
- conformance manifests;
- redistributable corpus subset;
- SBOM/dependency inventory where tooling is established;
- checksums;
- signatures when signing policy exists;
- acceptance and toolchain reports.

Every artifact name includes product version and, where needed, platform and
architecture. Names must not imply unsupported format coverage.

## 9. Release notes

Release notes state:

- version, date, commit and tag;
- release type;
- new/changed/deprecated/removed behaviour;
- exact format/version capability changes;
- language and compiler profiles;
- security fixes/advisories;
- API/CLI/schema migrations;
- known limitations and deferred items;
- artifact/checksum locations;
- upgrade and rollback guidance.

## 10. Coverage attestation

For every `Stable` format/version capability in the release, record:

- specification version;
- implementation component;
- conformance suite version and result;
- corpus set/hash index;
- writer/reference evidence where applicable;
- known limitations;
- reviewer approval.

If evidence is incomplete, lower the status before release.

## 11. Tagging

- tags are annotated where supported;
- tag message names version, commit purpose and evidence location;
- published tags are immutable;
- a correction uses a new version/tag;
- `format-era-1990` is created only after full M8 acceptance;
- language-epoch tags do not move the format-epoch tag.

## 12. Publication sequence

1. verify candidate artifacts and hashes;
2. obtain required acceptance;
3. create immutable version tag;
4. create epoch tag when applicable;
5. publish artifacts and checksums;
6. publish release notes and known limitations;
7. verify downloads against hashes;
8. announce only capabilities present in the coverage attestation;
9. archive the release checklist and reports.

## 13. Post-release verification

- installation/download smoke test from public artifacts;
- links and checksums verified;
- support/coverage pages show the released version;
- next `Unreleased` changelog section opened;
- accidental secrets or prohibited materials checked;
- regressions triaged without altering the tag.

## 14. Rollback and withdrawal

Source-control tags remain historical facts. If artifacts are unsafe or
legally problematic:

- withdraw affected downloads where possible;
- publish a clear notice/advisory;
- issue a fixed release;
- preserve minimal non-sensitive incident evidence;
- never replace files under the same version silently.

## 15. 1990 epoch acceptance appendix

M8 additionally requires:

- all Lastenheft 1990 acceptance criteria;
- all Pflichtenheft codec and delivery criteria;
- all architecture section 40 criteria;
- selected historical toolchain reports;
- final list of included and deferred format versions;
- Product Owner-signed/confirmed acceptance record;
- immutable `format-era-1990` tag.

## 16. Release checklist

### Scope and evidence

- [ ] Version and release type approved
- [ ] Exact candidate commit recorded
- [ ] Coverage audited
- [ ] Specifications/ADRs accepted
- [ ] Stable capability attestations complete

### Build and test

- [ ] Free reference builds pass
- [ ] Required historical reports pass or limitations accepted
- [ ] Unit/integration/conformance tests pass
- [ ] Negative/resource tests pass
- [ ] Security analysis completed
- [ ] Packages smoke-tested

### Legal and documentation

- [ ] Licences and attributions complete
- [ ] Corpus provenance complete
- [ ] No proprietary material included
- [ ] Changelog and release notes complete
- [ ] Known limitations explicit

### Publication

- [ ] Artifacts generated from clean commit
- [ ] Checksums generated and independently checked
- [ ] Immutable tag created
- [ ] Artifacts and notes published
- [ ] Public download verification complete
- [ ] Acceptance record archived

