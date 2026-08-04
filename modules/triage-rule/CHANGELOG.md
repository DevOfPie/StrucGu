# Changelog — triage-rule

Newest first. Versions follow [semantic versioning](https://semver.org/spec/v2.0.0.html),
with bumps defined by what a previously clean adopter will newly see rather than
by how much source changed. See [SPEC.md](../../SPEC.md).

## 0.4.0 — 2026-08-04

**What a previously clean adopter will newly see: nothing.** No check was added,
removed, or changed. `TR-03` resolves markdown links exactly as it did at
`0.1.0`, so no repository that passed it starts failing it.

`triage-destination` used to read *the document **names** where out-of-scope
findings go*. It now reads *the document **links to*** it. The obligation
claimed coverage the check never had: a document naming its destination in a
sentence and nowhere else was described as satisfying the obligation while
`TR-03` reported a finding on it, and the module's own `module.md` called that a
false positive and advised recording a deviation. That advice is withdrawn. The
remedy is one link.

This is the narrowing of an obligation to what its check can observe, not the
widening of a check to what it cannot. Which direction to move was left open
from the first release and is settled now on use rather than on review — the
reasoning, and what the rejected option would have cost, is in
[decisions.md](../../docs/records/decisions.md#the-obligation-is-narrowed-to-what-the-check-can-see-rather-than-the-check-widened-to-prose).

`fixtures/satisfies-prose-destination/` is new: a rule that names the findings
queue in prose, with the resolving link two sections further down, on which
`TR-03` reports `ok`. It is the first tree in the catalog whose name is neither
`satisfies/` nor `violates-<CHECK-ID>/`, and
[SPEC.md](../../SPEC.md) changed in the same release to admit the shape. That is
a contract change and is versioned by the repository — see the
[root changelog](../../CHANGELOG.md).

## 0.3.0 — 2026-08-03

**What a previously clean adopter will newly see: nothing.** No check, no
obligation, no role and no template changed. The addition is inside `fixtures/`.

`fixtures/satisfies/triage.md` gains a fenced example containing a link to a
`scope.md` that is not in the tree. `TR-05` must still report `ok`, because
**code is not scanned for links** — a rule [SPEC.md](../../SPEC.md) gives its own
paragraph and a learned-the-hard-way provenance, and which no fixture tested. A
checker that scans fences reports a finding against an example of its own check.

`TR-04`'s prose said "Any one pattern matching is sufficient", which
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
