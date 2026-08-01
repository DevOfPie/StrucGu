# Changelog — investigations

Newest first. Versions follow [semantic versioning](https://semver.org/spec/v2.0.0.html),
with bumps defined by what a previously clean adopter will newly see rather than
by how much source changed. See [SPEC.md](../../SPEC.md).

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
