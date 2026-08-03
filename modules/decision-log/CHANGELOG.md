# Changelog — decision-log

Newest first. Versions follow [semantic versioning](https://semver.org/spec/v2.0.0.html),
with bumps defined by what a previously clean adopter will newly see rather than
by how much source changed. See [SPEC.md](../../SPEC.md).

## 0.2.0 — 2026-08-03

**What a previously clean adopter will newly see: nothing.** No check, no
obligation, no role and no template changed. The addition is inside `fixtures/`,
which is read by someone writing a checker and never by an adopted repository.

`fixtures/expected.yaml` joins `expected.md` — the same expected results as
data, keyed by fixture tree and check id, plus one entry per judgment id, with
values drawn from the five audit states and nothing else. It exists so that
*did my run match?* is answered mechanically rather than by reading every tree
against prose. `expected.md` stays and stays the statement of intent; where the
two disagree that is a defect to report, not a precedence order to apply.

[SPEC.md](../../SPEC.md) gained the section defining `strucgu/expected@1`, and
its list of what a module directory holds now names the file. That is why all
five modules move together on the same day.

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
