<!-- SPDX-FileCopyrightText: 2026 Nostalgia and Imperial Auto Governor contributors -->
<!-- SPDX-License-Identifier: CC-BY-SA-4.0 -->

# OGAS Research Evidence

Research data accompanying [OGAS](https://github.com/V2t-Nostalgia/OGAS)
`v0.6.0-alpha.1`. This repository contains reviewed evidence, not a game, an
installer, an executable runtime or a second execution system.

## Scope and Access

The primary [index](index.jsonl) inventories **32,411 paths / 54,350,245,449
original bytes**, including repeated paths and duplicate content. Of these,
**13,549 paths** have downloadable data: 9,574 exact originals and 3,975 explicitly
labeled privacy-neutralized derivatives. They map to 9,276 unique compressed
content-addressed objects. [ARCHIVE.json](ARCHIVE.json) records exact counts and
hashes. [REVIEW.json](REVIEW.json) preserves withholding and source-format review
decisions. [Supplemental evidence](supplemental/ARCHIVE.json) adds 31 indexed paths,
30 downloadable paths/objects, including recovered project-source archive members
and publication receipts. It has its own index; it is not merged into a prior run.
The separate [publication checks](publication-checks/ARCHIVE.json) retain the final
678-test regression, the earlier harness configuration errors, and CI correction
receipts. Five of its six paths are downloadable; one log is conservatively
withheld by the credential/content prefilter, with the original retained.

Failures, interruptions, rejected candidates, superseded reports, earlier source
snapshots and corrected passes remain indexed. Nothing is promoted because it is
the latest report or because native `IsValid` returned true. An index path may
refer to raw observations, generated analysis or human interpretation; consult
the artifact and its original receipts for the actual evidence level.

Proprietary game binaries, full saves/state/databases, unreviewed artwork and
third-party source, private configurations and possible credentials are **not
public downloads**. Their original hashes and access dispositions remain in the
index. Original bytes and full private path mappings are retained in restricted
storage; a derivative cannot reconstruct its original. Obtain matching game
binaries through your own lawful installation. Access to withheld material is
subject to privacy and redistribution review, not guaranteed by this index.

## Download, Verify and Restore

```bash
git clone https://github.com/V2t-Nostalgia/OGAS.git
git clone https://github.com/V2t-Nostalgia/OGAS-research-evidence.git
cd OGAS
git checkout v0.6.0-alpha.1
python scripts/research/archive_evidence.py verify --index ../OGAS-research-evidence/index.jsonl --objects ../OGAS-research-evidence/objects
python scripts/research/archive_evidence.py verify --index ../OGAS-research-evidence/supplemental/index.jsonl --objects ../OGAS-research-evidence/supplemental/objects
python scripts/research/archive_evidence.py verify --index ../OGAS-research-evidence/publication-checks/index.jsonl --objects ../OGAS-research-evidence/publication-checks/objects
python scripts/research/archive_evidence.py restore --index ../OGAS-research-evidence/index.jsonl --objects ../OGAS-research-evidence/objects --output ../NEW_RESTORED_DIRECTORY
```

Use a new restore directory. Restore supplemental data separately with its own
index/object directory and another new output directory. The verifier checks the
**uncompressed SHA-256** of every referenced object, not just gzip checksums. A
rotated log already compressed in the original experiment restores as its original
gzip file; decompress that restored file to inspect its records.

Every index row has a browsable `entry` under `paths/`, an original hash, access
decision, public hash and object link when downloadable. `public_original` means
byte-exact; `public_redacted_derivative_original_retained` means explicitly changed
for publication. A restricted row has no public object. [BATCHES.json](BATCHES.json)
groups path namespaces for navigation, not as an assertion of experimental success.

```bash
cd ../OGAS-research-evidence
sha256sum -c CONTENTS.sha256
gpg --import SIGNING_KEY.asc
gpg --verify CONTENTS.sha256.asc CONTENTS.sha256
gpg --verify index.jsonl.asc index.jsonl
git verify-commit HEAD
```

Check the key fingerprint against the independently published OGAS source
signature: `FAA5513C23C3F379F56EF061B2CFB0BD581F74A1`. An included public key alone
does not establish trust. Git uses binary attributes to preserve original bytes.

## Provenance and Reproduction Limits

[PROVENANCE.json](PROVENANCE.json) binds this publication to actual signed source
checkpoints and export/review tool snapshots. It does **not** retroactively assign
those commits or the current Python environment to historical experiments. Some
experiments ran from dirty trees; missing original source/tool provenance remains
unknown. `reported_context` is extracted context, not independent verification.

Exact game identities, SDK fingerprints, input hashes and session receipts belong
to their individual experiments. Static recovery, offline construction, native
legality, actual execution, causal save pairing and multiplayer synchronization
are distinct. The 351-entry SDK catalog does not mean 351 usable gameplay actions.
No Command was submitted and no running game was modified by this publication.

Publication attempts interrupted before finalization and pre-review exports are
retained privately. The reviewed tree excludes uncleared bytes rather than adding
them to Git and deleting them later. Remote originals additionally have hash
inventories and retention copies. Where retention used hardlinks, those protect
against pathname removal, **not in-place mutation**; original SHA-256 remains
authoritative. A single changing status-file snapshot is separately preserved.

See the source project's [evidence guide](https://github.com/V2t-Nostalgia/OGAS/blob/main/docs/research/EVIDENCE_ARCHIVE.md)
and publication receipt for pinned archive revision and independent download checks.
Report sensitive findings through [private security reporting](https://github.com/V2t-Nostalgia/OGAS/security/advisories/new),
never by posting private originals or credentials in an issue.

## Licensing

Project-authored code remains GPL-3.0-only and project-authored documentation
CC-BY-SA-4.0 unless a file states otherwise. Third-party MIT notices remain
applicable to their components; see [NOTICE](NOTICE) and `LICENSES/`. Indexing a
withheld file grants no rights to redistribute it. This repository is independent
of, and not endorsed by, Paradox Interactive or other third-party rights holders.
