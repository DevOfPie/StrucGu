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
| [M8](m8.md) | Fixture expectations become machine-comparable | M6 | planned |
| [M9](m9.md) | Conformance is defined narrowly, and stays self-asserted | M8 | planned |
| [M10](m10.md) | The first independent checker, written from the specification alone | M8 | planned |
| [M11](m11.md) | A second repository adopts, and the objection channel is used in anger | M10 | planned |
| [M12](m12.md) | F1 and F2 are closed by use rather than by review | M10 M11 | planned |
| [M13](m13.md) | The catalog says what a year of one repository could not | M10 M11 M12 | planned |

M5 and M6 may be swapped. M1–M4 must not be reordered — each one's *Done means*
is the next one's input.

M8–M13 are **planned, not agreed.** They are written here rather than in a plan
document because this file is where scope lives, and a phase described anywhere
else is a second home for status. Nothing in them is started until the owner has
taken the four decisions below; `planned` means proposed and unstarted, and no
other status word in this table has ever meant that.

M9's edge to M8 is an *ordering preference* — a conformance criterion is easier
to write once expectations are mechanical, and could be written first. M10's edge
to M8 is hard: an independent implementer with nothing mechanical to compare
against produces a reading of the spec rather than a test of it.

### Decisions this phase needs before M8 starts

Each is a scope question, and [triage.md](../triage.md) requires stopping and
asking on those rather than deciding them inside a unit.

1. **Does a machine-readable expectation file belong under `modules/` at all?**
   It is the closest thing to shipping software the no-runner decision permits.
   See [M8](m8.md) risks.
2. **Is a conformance document a step toward the certification this repository
   refuses?** If yes, [M9](m9.md) is cut and [M10](m10.md) compares against
   [M8](m8.md)'s files alone.
3. **Who writes the independent checker, and is the no-questions rule
   acceptable?** It is slow, it is the entire value of [M10](m10.md), and it
   cannot be added back afterwards.
4. **Which second repository.** It must not be the one the catalog was extracted
   from. See [M11](m11.md) risks for what the available candidates do and do not
   prove.

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
