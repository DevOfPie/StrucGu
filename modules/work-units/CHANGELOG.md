# Changelog — work-units

Newest first. Versions follow [semantic versioning](https://semver.org/spec/v2.0.0.html),
with bumps defined by what a previously clean adopter will newly see rather than
by how much source changed. See [SPEC.md](../../SPEC.md).

## 0.1.0 — 2026-07-31

**What a previously clean adopter will newly see: nothing — first release.**

Four obligations: done is stated as falsifiable claims, risks are considered,
each record names its dependencies and the promise it closes, and rules common
to every unit are stated once. Seven checks, `WU-01` through `WU-07`.

`base: false`. A project is not broken without this.

Known limitation stated rather than hidden: the checks are written against
files, because a checker cannot read an issue tracker. A project whose units of
work live in a tracker should leave the roles unmapped — every check then reports
`skip` and nothing is broken. If the obligations are right but the file
assumption is wrong, that is a good objection and this module is the one most
likely to receive the first one.

`WU-04` has the highest false-positive rate in the catalog. Any angle-bracketed
literal in a record matches its placeholder pattern. Documented in
[module.md](module.md) with the recommendation to turn it off rather than reword
records around it.

Extracted from LinkCtrl `docs/build-notes/phase-details/_template.md` and
`README.md`. "Milestone" and "phase" are not carried across as mandated names.
