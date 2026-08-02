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

M5 and M6 may be swapped. M1–M4 must not be reordered — each one's *Done means*
is the next one's input.

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
