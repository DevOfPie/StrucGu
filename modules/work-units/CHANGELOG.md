# Changelog — work-units

Newest first. Versions follow [semantic versioning](https://semver.org/spec/v2.0.0.html),
with bumps defined by what a previously clean adopter will newly see rather than
by how much source changed. See [SPEC.md](../../SPEC.md).

## 0.2.1 — 2026-08-03

**What a previously clean adopter will newly see: findings from `WU-04`, if
their checker read `module.md` rather than `module.yaml`.** The fixed sentence is
answered honestly here rather than with "nothing", because "nothing" would be
false for one class of adopter.

`module.md` carried `WU-04`'s pattern as `&lt;[A-Za-z][A-Za-z ]*&gt;`, where
[module.yaml](module.yaml) carries `<[A-Za-z][A-Za-z ]*>`. The escaped form
matches a literal `&lt;` followed by letters and a literal `&gt;`, so it cannot
match `<title>` — the placeholder text this check exists to catch. The two halves
render identically on a website that turns the entities back into the characters,
which is why it survived from the first release. It is repaired here.

A checker that followed the escaped pattern reported `WU-04: ok` on records
holding angle-bracketed placeholders. It will now report findings on them. Those
are records that were always non-conforming; nothing about what this module asks
for has changed.

**This is a repair, not a new check, and the difference is checkable rather than
asserted.** `WU-04` shipped in `0.1.0` with its violating fixture, and
`fixtures/expected.yaml` has said `violates-WU-04` produces `WU-04: finding`
since expectations became data. [README.md](README.md) and this changelog's
`0.1.0` entry both told adopters from the first release that `WU-04` "has the
highest false-positive rate in the catalog — any angle-bracketed literal in a
record matches its placeholder pattern", which describes the unescaped pattern
and no other. The shipped contract never moved; its transcription into the prose
half was corrupt.

**What that costs, stated rather than argued away.** [SPEC.md](../../SPEC.md)
calls `module.md` normative, so a checker that followed it literally was entitled
to the behaviour it got, and its adopters see new findings under a patch bump.
That is the shape of thing a major version exists to announce. It is a patch
because the obligation, the check, the fixture and the documented behaviour are
all unchanged — but an adopter surprised by `WU-04` firing has a real complaint,
and the [objection channel](../../docs/objections.md) is where it goes. Turning
`WU-04` off remains the recommendation in [README.md](README.md) for anyone whose
records legitimately quote angle-bracketed literals.

`fixtures/` gains two trees, neither of which any adopter reads.
`violates-WU-03-second-record/` holds two records where only the second is
incomplete, pinning that a `dir`-bound check reports `finding` if **any** file
fails rather than only if every file does.
`violates-WU-06-one-pattern-only/` has a template asking for dependencies and not
for what the unit discharges, so exactly one of `WU-06`'s two patterns matches —
pinning that `pattern_present` requires **every** listed pattern. A checker with
either rule wrong reproduced all 33 trees before these existed.

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
