# Work

The scope contract. This file states **what** is true and what the status is;
[decisions.md](../decisions.md) states **why**. Rationale here and status there
are both wrong.

One file per work unit, named for its number. **Read exactly the one you are
building** — that is what this split is for. Nothing here restates another file.

**Status lives here, and only here.**

| # | Work unit | Depends on | Status |
| --- | --- | --- | --- |
| [M1](m1.md) | The repository states what it is, and its own records exist | — | done |
| [M2](m2.md) | The module contract | M1 | done |
| [M3](m3.md) | The three base modules | M2 | done |
| [M4](m4.md) | The two optional modules | M2 | done |
| [M5](m5.md) | Adoption and the objection loop | M3 M4 | done |
| [M6](m6.md) | Fixtures, and every check observed failing | M3 M4 | done |
| [M7](m7.md) | StrucGu adopts, and 0.1.0 is tagged | M5 M6 | done |
| [M8](m8.md) | Fixture expectations become machine-comparable | M6 | done |
| [M9](m9.md) | Conformance is defined narrowly, and stays self-asserted | M10 | done |
| [M10](m10.md) | The first checker, written from the specification alone | M8 | done |
| [M11](m11.md) | The second repository adopts, and every finding is disposed of by the rule | M10 | done |
| [M12](m12.md) | F1 and F2 are closed, F2 by use rather than by review | M10 M11 (F2 only) | done |
| [M13](m13.md) | The catalog says what a year of one repository could not | M9 M10 M11 M12 | done |

M5 and M6 may be swapped. M1–M4 must not be reordered — each one's *Done means*
is the next one's input.

M8–M13 are **scoped and unstarted.** They are written here rather than in a plan
document because this file is where scope lives, and a phase described anywhere
else is a second home for status. `planned` means agreed and not begun;
`deferred` means agreed to happen later than its number suggests. Neither has
appeared in this table before, and neither means `done`.

`reopened` joins that vocabulary: a shipped unit whose claim was found false and
is being corrected in place rather than succeeded, per
[triage.md](../triage.md). It returns to `done` when the correction lands, and
the unit's own file — not this table — is where the reopening survives.

M10's edge to M8 is hard: an implementer with nothing mechanical to compare
against produces a reading of the spec rather than a test of it. M9's edge to M10
is the deferral, not a dependency of substance — and M13's edge to M9 exists
because nothing else depended on it, which let a deferred unit drift past the
release as a silent cut. M12's edge is hard for `F2` and an ordering preference
for `F1`, which needs neither an implementation nor a second adopter.

### Decisions this phase needed, and what came back

Each was a scope question, and [triage.md](../triage.md) requires stopping and
asking on those rather than deciding them inside a unit. All four were put to the
owner on 2026-08-02 and answered. The reasoning is in
[decisions.md](../decisions.md); the answers are here because they change what
the units say.

1. **A machine-readable expectation file ships under `modules/`,** beside the
   prose it restates. [M8](m8.md).
2. **The conformance document is deferred, not cut** — written after the first
   implementation, from questions that were actually asked. [M9](m9.md).
3. **Whippy writes the first checker**, in a fresh session, from the published
   repository only, under a hard no-questions rule. The independence is partial
   and [M10](m10.md) states in what way.
4. **The second repository is chosen, is private, and is not named here.**
   [M11](m11.md) tests re-application rather than generality, and says so before
   it reports anything.

### Not in this phase

Named because a phase that says only what it includes will acquire the rest by
drift.

- No new module, and no growth of the base set. Both are major-version
  arguments in their own right — see [SPEC.md](../../../SPEC.md) "Base and
  prerequisites".
- No check added on suspicion. Only [M12](m12.md)'s `F2`, and only if the
  reasoning survives.
- Nothing that runs in a consumer's CI, and no action, template, or bot that
  files anything on anyone's behalf.

### Specification edits are in scope, and this is the list

The first version of this section listed no [SPEC.md](../../../SPEC.md) changes
while three units forced them. That is the hidden scope this section exists to
prevent, so the edits are named instead.

- [M8](m8.md) — the module contract's file list, which currently says a module
  directory contains *exactly* the files named and defines `fixtures/` without
  an expectation data file. Plus the definition of that file's schema
  identifier.
- [M10](m10.md) — an unbounded number of fixture additions and obligation
  rewordings, one per ambiguity resolved that way. Unbounded is the honest
  number: the count is the unit's output and cannot be known in advance.
- [M12](m12.md) — either a fixture tree in a third shape, or a new check kind,
  depending on how `F2` closes.

Anything beyond these is out of scope and belongs in
[findings.md](../findings.md).

---

## What every work unit inherits

Stated once. Repeating these per file is how N files come to disagree.

| Rule | Consequence |
| --- | --- |
| A check is written | Its violating fixture is written at the same time, or the check does not ship |
| A check cannot be violated by any tree | Cut it, and record what was cut. That list is worth more than the checks that survived |
| A behaviour check could be satisfied by authoring text | Cut it. A declaration check may stay if a behaviour check tests whether the declaration is true |
| A module names an artifact | It names a **role**, never a path and never a word already taken elsewhere |
| Anything is added under `modules/` | No language, package manager, build tool, or file extension appears in it |
| `module.md` and `module.yaml` both change | They must agree. If they disagree the conflict is a bug — report it, do not pick |
| A README is written for a module | It states at least three concrete costs, who should not adopt it, and how to stop using it in one line |
| A version is bumped | The changelog states what a previously clean adopter will newly see, even when the answer is "nothing" |
| A check is added to a shipped module | Major version. Never a minor — see [decisions.md](../decisions.md#a-new-check-never-ships-in-a-minor-version) |
| Any file is committed | Every relative link and anchor in it resolves |
| A commit is made | One work unit per commit, maximum. Message is prose explaining why |

## Decisions already taken

Do not re-litigate these inside a work unit. They are argued in
[decisions.md](../decisions.md); changing one is its own unit of work.

- Five small modules, three of them base, and the base list is closed at three.
- No runner ships. The specification and its fixtures are the deliverable.
- Modules define structure and use, not content.
- Remediation may scaffold or relocate, never author, and never applies itself.
- Adoption is one visible `strucgu.yaml` at the consumer's repository root.
- Fixtures are the evidence. Self-application is dogfooding and is not offered
  as proof.
