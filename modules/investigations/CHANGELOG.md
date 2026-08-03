# Changelog — investigations

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

Four obligations: the record exists, it says what it was tested against with
versions, it keeps observations separate from the rules drawn from them, and it
says how to run it again or that the artifacts are gone. Four checks, `IN-01`
through `IN-04`.

`base: false`, and the first obligation is `conditional` — it applies once a
project has actually run an investigation that did not fit in a decision-log
entry. This is the only module in the catalog whose conditional path is
exercised: StrucGu leaves the role unmapped in its own
[strucgu.yaml](../../strucgu.yaml), so every check here reports `skip` rather
than `ok`.

The format is a spike report rather than a classic decision record. The
difference is the separation of observations from the rules drawn from them,
which most decision-record formats do not have and which is the whole reason
this module is not just a second decision log.

Extracted from LinkCtrl `docs/adr/0001-partitioning-and-sqlc.md`, format only.
