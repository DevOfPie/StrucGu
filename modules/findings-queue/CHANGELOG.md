# Changelog — findings-queue

Newest first. Versions follow [semantic versioning](https://semver.org/spec/v2.0.0.html),
with bumps defined by what a previously clean adopter will newly see rather than
by how much source changed. See [SPEC.md](../../SPEC.md).

## 0.3.0 — 2026-08-03

**What a previously clean adopter will newly see: nothing.** No check, no
obligation, no role and no template changed. The addition is inside `fixtures/`.

`fixtures/violates-FQ-06-reference-link/` is a second violating tree for
`FQ-06`. Its only broken link is a reference-style one — `[label]` in the row,
`[label]: archive/findings.md` at the foot of the file — so it pins that a
reference link is a link at all. [SPEC.md](../../SPEC.md) says how a link
resolves and never says what a link is, and a checker extracting inline links
only reports `ok` on this tree while reproducing every other tree in the
catalog. Reference links are commonest in exactly the documents this module
describes, where one destination is cited many times.

The tree is permitted by [SPEC.md](../../SPEC.md)'s relaxed `fixtures/` row: a
check may now carry more than one violating tree.

`FQ-04`'s prose said "Any one pattern matching is sufficient", which
contradicts [SPEC.md](../../SPEC.md) — every listed pattern must match. The
check carries a single alternation, so nothing behaves differently; the sentence
generalised wrongly.

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

Four obligations: the destination exists, rows carry evidence, rows carry a
review state, and the queue states that its rows are not commitments. Six
checks, `FQ-01` through `FQ-06`.

Declares [triage-rule](../triage-rule/) as a prerequisite. A checker reports
`skip` for every check here when it is not adopted — without a rule defining what
counts as out of scope, no row can be wrong about anything.

[README.md](README.md) carries a warning that a repository publishing its
documentation directory as a static site will publish this file to the public
web. That is a real consequence of a documentation convention and the role map
exists partly to avoid it.

Extracted from LinkCtrl `docs/build-notes/deferred-findings.md`.
