# Changelog — decision-log

Newest first. Versions follow [semantic versioning](https://semver.org/spec/v2.0.0.html),
with bumps defined by what a previously clean adopter will newly see rather than
by how much source changed. See [SPEC.md](../../SPEC.md).

## 0.1.0 — 2026-07-31

**What a previously clean adopter will newly see: nothing — first release.**

Four obligations: rationale is recorded, entries are dated, entries are never
edited away, and the log is indexed. Six checks, `DL-01` through `DL-06`.

Two forms ship together — one growing file, or one file per decision plus an
index. Shipping both in a first release was deliberate: a repository that already
keeps decision records almost certainly keeps them as separate files, and
treating the common shape as a deviation would make the module unusable for the
adopters most likely to want it.

`DL-03` requires `effective_from` in the adoption record. Without a history
bound, a mature repository's first run reports every commit that ever removed a
line from its decision records.

Known conflict, documented in [README.md](README.md) rather than left to be
discovered: tools that manage per-file decision records commonly rewrite a
superseded record's status line in place, which `DL-03` will report. That is a
legitimate deviation and the README shows how to record it.

Extracted from LinkCtrl `docs/build-notes/decisions.md`.
