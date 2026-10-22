# Security Policy

## 1. Security model

SASD Moschus processes historical and potentially malformed files. Every file,
metadata field, path, length, offset, count, compressed stream and embedded
object is untrusted.

The project aims to fail in a controlled and diagnosable manner. No parser can
be declared perfectly safe; defence therefore combines bounded architecture,
negative testing, fuzzing, modern analysis and a responsible disclosure
process.

## 2. Supported versions

Until the first stable release, security fixes are applied to the current
`main` branch and explicitly named release candidates where practical. After
stable releases begin, the repository will publish a version support table
here and in release notes.

Historical epoch tags are immutable reference points. A vulnerability found in
an old epoch is fixed in a new release; the old tag is not moved. Advisories
state which historical builds are affected.

## 3. Reporting a vulnerability

Do not open a public issue containing an unpatched exploit, private data or a
malicious fixture.

Preferred reporting path:

1. use GitHub Private Vulnerability Reporting for the repository when enabled;
2. if unavailable, contact the repository owner privately through the contact
   method published on the GitHub profile;
3. provide only the minimum sensitive attachment needed and agree on a secure
   transfer method before sending large or confidential files.

A useful report includes:

- affected commit, version and platform;
- exact format/version if known;
- operation (`probe`, `read`, `validate`, `recover`, `write`, `convert`);
- resource limits and options;
- expected and observed result;
- reproducible steps or a minimized input;
- impact assessment;
- sanitizer trace or debugger information if available;
- whether the sample contains confidential or copyrighted data.

## 4. In-scope vulnerability classes

- out-of-bounds read or write;
- use-after-free, double-free or invalid ownership;
- integer overflow leading to unsafe access or allocation;
- uncontrolled memory, CPU, recursion or decompression use;
- infinite loops or cyclic-reference failure;
- path traversal or unintended file overwrite;
- command, macro, script or printer-language execution;
- unintended network access or external resource resolution;
- validation bypass that causes a false safe/valid result;
- unsafe recovery behaviour;
- data exposure through logs, temporary files or reports;
- dependency or build-chain compromise affecting distributed artifacts.

Ordinary unsupported-format errors, documented conversion losses and
performance requests without a denial-of-service condition are usually not
security vulnerabilities, though they may still be valid bugs.

## 5. Response process

The maintainers aim to:

1. acknowledge receipt and establish a private tracking record;
2. reproduce and classify the issue;
3. determine affected versions, codecs and operations;
4. minimize the reproducer where legally possible;
5. develop a fix plus negative regression tests;
6. review adjacent code paths and language implementations;
7. prepare releases and an advisory;
8. coordinate disclosure with the reporter;
9. update architecture or secure-coding guidance if the issue reveals a
   systemic weakness.

No fixed response time is promised during the foundation phase. Critical
reports take priority over roadmap work.

## 6. Disclosure and credit

Coordinated disclosure is preferred until a fix or mitigation is available.
Reporter credit is given when requested and legally possible. A reporter may
remain anonymous.

The project may publish:

- affected versions and formats;
- impact and severity;
- fixed versions;
- mitigation;
- technical root cause at a level that supports users without needlessly
  exposing private data.

## 7. Secure development requirements

All parser work must:

- use bounded streams/slices;
- use checked offset and length arithmetic;
- validate before allocation and access;
- apply explicit resource budgets;
- separate strict and recovery behaviour;
- avoid mutable global operation state;
- keep active content inert;
- test truncation and malformed lengths;
- clean up partial output and temporary files;
- preserve structured security diagnostics.

Modern sanitizer, static-analysis and fuzzing builds complement historical
compiler tests. A successful Turbo C or Microsoft C build is not a security
analysis.

## 8. Malicious and confidential fixtures

Potentially malicious samples must not be committed casually. Before inclusion:

- remove personal/confidential content or create a synthetic reproducer;
- confirm redistribution rights;
- minimize to the relevant bytes;
- label the fixture and metadata clearly;
- store it only in the designated corpus location;
- ensure tests never execute embedded content;
- consider publishing a hash-only reference when redistribution is unsafe.

## 9. Dependency and release security

- keep runtime dependencies minimal;
- pin release-time tools where reproducibility requires it;
- inventory licenses and versions;
- build releases from clean, immutable commits;
- publish cryptographic checksums;
- never vendor proprietary compiler/runtime material;
- document generated files and generators;
- treat unexpected network access during builds as a failure.

## 10. Security limitations

Moschus is not a malware scanner, sandbox, emulator or proof that a file is
safe to open in another program. `validate` determines conformance to declared
format rules; it does not certify absence of all malicious content.

Users processing hostile archives should also apply OS-level isolation,
least-privilege accounts, file-size quotas and process limits appropriate to
their threat model.

