# Changelog — decision-log

Newest first. Versions follow [semantic versioning](https://semver.org/spec/v2.0.0.html),
with bumps defined by what a previously clean adopter will newly see rather than
by how much source changed. See [SPEC.md](../../SPEC.md).

## 0.3.0 — 2026-08-03

**What a previously clean adopter will newly see: nothing.** No check, no
obligation, no role and no template changed.

`DL-03`'s expected result is corrected on five fixture trees, from `ok` to
`skip`. None of those trees is a git repository, so a checker running `DL-03`
there reads no history and observes nothing — and `skip` is the state for that.
The old expectation required folding `skip` into `ok`, which
[SPEC.md](../../SPEC.md) and [auditing.md](../../docs/auditing.md) between them
name four times as the failure that matters most. The prose was right and the
fixtures were wrong; the fixtures moved.

This affects an adopter only where the audited root is not a git repository —
an export, a tarball, a tree that has never committed. `DL-03` reports `skip`
there instead of `ok`. That is not a new finding, it is a passing result
correctly downgraded to "I could not tell".

`fixtures/satisfies/decisions.md` gains a second index entry whose anchor
carries two hyphens, because its heading has an em dash between two spaces and
runs of spaces are **not** collapsed when slugging. It pins a rule
[SPEC.md](../../SPEC.md) argues for and no fixture tested: a checker that
collapses them rejects a correct anchor and reports `DL-06` here.

`DL-04`'s prose said "Any one pattern matching is sufficient", which
contradicts [SPEC.md](../../SPEC.md) — every listed pattern must match. The
check carries a single alternation, so nothing behaves differently; the sentence
generalised wrongly and an implementer carrying it to a multi-pattern check got
that check wrong.

[SPEC.md](../../SPEC.md) changed in the same release, in ways that change what a
conformant checker outputs rather than what this module asks for. Those are
contract changes and are versioned by the repository, not here — see the
[root changelog](../../CHANGELOG.md).

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
