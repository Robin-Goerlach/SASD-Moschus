# Source and corpus policy

| Field | Value |
|---|---|
| Version | 0.1 |
| Date | 22 October 2026 |
| Applies to | Research notes, specifications, fixtures, reference outputs and bundled software |

## 1. Purpose

Moschus combines historical format knowledge from books, standards,
manufacturer documentation, software behaviour and test files. This policy
keeps technical claims traceable while respecting copyright, licences,
privacy, trade secrets and redistribution limits.

This policy is project guidance, not legal advice. Unclear rights are a reason
to withhold material until clarified.

## 2. Core rules

1. Cite facts; do not copy protected expression unnecessarily.
2. Prefer primary sources when available.
3. Record contradictions instead of silently choosing one source.
4. Do not assume old or abandoned means public domain.
5. Do not assume a book's bundled disk is freely redistributable.
6. Every corpus file requires provenance and rights metadata.
7. Personal or confidential data is excluded or safely redacted.
8. Hash-only references may document local evidence without distributing it.
9. Synthetic fixtures should be independently authored from documented rules.
10. Repository licence compatibility must be checked before inclusion.

## 3. Source classes

### 3.1 Primary normative sources

- official standards;
- manufacturer format specifications;
- official SDK or developer documentation;
- published protocol/format registrations;
- source code released under a compatible licence when it is authoritative.

Record edition, revision, date, publisher/issuer, identifier, page/section and
access location where lawful.

### 3.2 Secondary sources

- technical books, including Kussmann 1989 and Born 1992;
- independent articles and reference manuals;
- preservation-community documentation;
- academic papers.

Secondary sources guide research but may simplify, omit or combine versions.
Material claims should be cross-checked where practical.

### 3.3 Empirical evidence

- bytes produced by a named historical application;
- acceptance/rejection by a named application version;
- behaviour observed under a documented OS/locale/configuration;
- reverse-engineering experiments permitted by applicable law.

Empirical records state exact versions, environment, steps, input hash and
observed result. Observation is not automatically a universal rule.

### 3.4 Derived conclusions

A derived rule explains its reasoning and source inputs. It remains marked as
derived until stronger evidence confirms it.

### 3.5 Unresolved claims

Unverified claims may be recorded as research questions. They cannot justify a
Stable capability or unconditional parser assumption.

## 4. Citation records

Each source note should include:

- stable source ID;
- full title and author/issuer;
- edition/revision/version;
- publisher and date;
- ISBN, standard number or other identifier;
- exact pages/sections used;
- source class;
- rights/access notes;
- formats and versions covered;
- known errors or conflicts;
- date reviewed and reviewer.

Quotes are kept short and only when necessary. Specifications should normally
paraphrase facts and express independently developed tables and rules.

## 5. Books and bundled disks

The physical ownership of Kussmann's and Born's books permits consultation; it
does not by itself grant redistribution rights for scans, text, illustrations,
program listings or disk contents.

Therefore:

- no book scans are committed;
- no substantial verbatim text is copied;
- no disk image or bundled binary is committed without explicit permission;
- bibliographic and page references are permitted as factual citations;
- independently written specifications may describe learned facts;
- any short quotation must be necessary, attributed and legally reviewed when
  uncertain.

## 6. Corpus categories

| Category | Repository treatment |
|---|---|
| Project-generated synthetic | preferred; commit with metadata and MIT-compatible dedication/licence |
| Explicitly public-domain | commit after jurisdiction/source verification |
| Permissively licensed | commit with exact licence and attribution |
| Contributor-created | commit with contributor licence statement and no third-party data |
| Manufacturer sample | only if licence explicitly permits redistribution |
| Historical user document | normally exclude; use only with informed permission and redaction |
| Proprietary application output | evaluate licence and content; hash-only/local may be safer |
| Unknown provenance | do not commit |
| Malicious/security sample | minimize, synthesize and review before any inclusion |

## 7. Required fixture metadata

Each fixture record contains:

- stable fixture ID;
- relative path and filenames;
- SHA-256 or currently approved hash;
- exact size;
- format family/version/profile claim;
- creation/acquisition date;
- creator/source and chain of custody;
- licence/permission statement;
- privacy/confidentiality review;
- transformations such as redaction or minimization;
- expected structural properties;
- related specification and conformance case IDs;
- whether the file is synthetic, real-world, malformed or recovered;
- reviewer and review date.

If the file has companion files, the relationship and individual hashes are
recorded.

## 8. Synthetic fixtures

Synthetic files are built from project specifications, not copied by editing a
proprietary sample byte-for-byte. They should:

- contain invented non-personal data;
- be as small as practical;
- isolate one rule where possible;
- use deterministic generation;
- record generator source/version and options;
- avoid trademarks or copyrighted text beyond necessary format identifiers;
- be independently inspectable.

Generated fixtures may be committed when stable and small, but the generator
remains the auditable source when practical.

## 9. Real-world fixtures

Real files reveal interactions that synthetic cases miss. Before inclusion:

- prove the contributor has authority to license the content;
- remove personal data and hidden metadata;
- inspect embedded resources, thumbnails, deleted records and slack space;
- document the originating application/version;
- avoid confidential business data;
- obtain explicit redistribution terms.

Redaction must not invalidate the structural property under test. If safe
redaction is impossible, retain only a local hash reference.

## 10. Non-redistributable local evidence

A local evidence record may include:

- fixture ID and hash;
- size and format claim;
- acquisition category without exposing protected content;
- exact tool/operation and result;
- relevant byte positions described abstractly;
- access restrictions;
- a synthetic equivalent where possible.

Local evidence is never fetched automatically by public builds. Paths and
credentials are not committed.

## 11. Reference applications and compilers

Proprietary programs, operating systems and compilers are supplied locally by
the researcher. The repository may contain original build instructions and
adapter scripts, but not unlicensed binaries, headers, libraries, keys or disk
images.

Reference reports state:

- product and exact version;
- operating system/environment;
- locale and relevant configuration;
- input/output hashes;
- steps and observed messages;
- date and researcher;
- whether redistribution of output was assessed.

## 12. Reverse engineering

Reverse engineering must follow applicable law and licence obligations.
Project work should focus on interoperability and preservation, use lawfully
obtained materials and avoid distributing circumvention tools or protected
implementation code.

When legal status is unclear:

- pause public distribution;
- document only the open question;
- seek qualified advice;
- prefer published standards and clean, independently written implementation.

## 13. Privacy review

Historical database and document files can contain names, addresses, deleted
records, embedded thumbnails and metadata. Review both visible and hidden
content.

Do not commit:

- real personal identifiers without a clear lawful basis and necessity;
- credentials or licence keys;
- customer/business secrets;
- recoverable deleted personal records;
- filesystem paths revealing private account names when avoidable.

## 14. Removal and incident handling

If questionable material is found:

1. stop further distribution where practical;
2. notify maintainers privately if sensitive;
3. identify commits, releases and mirrors;
4. assess licence, privacy and security impact;
5. replace with a synthetic or permitted fixture;
6. document the corrective action;
7. rewrite history only when necessary and explicitly approved, understanding
   that published copies may persist.

Routine cleanup is not a reason to rewrite public history.

## 15. Corpus review checklist

- [ ] Stable fixture ID
- [ ] Exact hash and size
- [ ] Source and chain of custody
- [ ] Redistribution right documented
- [ ] Privacy and hidden-content review complete
- [ ] Exact format/version claim supported
- [ ] Expected properties stated
- [ ] Companion relationships recorded
- [ ] Synthetic alternative considered
- [ ] Specification and test links present
- [ ] Reviewer/date recorded

