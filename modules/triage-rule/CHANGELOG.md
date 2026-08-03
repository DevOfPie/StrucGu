# Changelog — triage-rule

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

Three obligations: the boundary, its destination, and what to do when two
governing documents disagree. Five checks, `TR-01` through `TR-05`.

`TR-04` ships as a declaration check with no paired behaviour check, which
[SPEC.md](../../SPEC.md) classes as decoration. It is documented as such in
[module.md](module.md) rather than quietly included; an adopter who disagrees
should turn it off.

Extracted from LinkCtrl `docs/build-notes/workflow.md`. The commit gates, the
sabotage discipline, the documentation pass, and the standing rules in that file
are deliberately not part of this module — they are verification obligations
rather than records obligations, and belong to a family that does not exist yet.
