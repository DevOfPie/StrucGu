# Changelog

Notable changes, newest first. The format follows
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/) and versions follow
[semantic versioning](https://semver.org/spec/v2.0.0.html).

Two things are versioned separately and it matters when deciding whether to
upgrade:

| | Versioned by | A breaking change means |
| --- | --- | --- |
| The module contract | This repository's version | An adoption record or a checker written against the old contract needs changing |
| Each module | Its own version, pinned in your adoption record | New findings are possible in a repository that was clean — see that module's changelog |

`0.x` here means the shape will move. The whole catalog was extracted from one
repository, which is not enough to tell a general convention from one project's
habits, so pins are cheap and the [objection channel](docs/objections.md) is the
point rather than the exception.

## [Unreleased]

Nothing yet.

## [0.1.0] — 2026-07-31

First release. A module contract, five modules, and the fixtures that show the
checks detect anything.

### The contract

[SPEC.md](SPEC.md) defines what a module is, how a repository declares which of
its own paths play which roles, a closed vocabulary of seven check kinds, five
output states, and what a remediation may and may not touch.

Three properties are load-bearing and are argued rather than asserted: modules
describe **structure and use, not content**; a **new check never ships in a
minor version**, because that would let this repository publish findings into
yours; and an audit **writes nothing** to the repository it reads.

### The modules

| Module | | |
| --- | --- | --- |
| [triage-rule](modules/triage-rule/) | base | The line between what the work in flight requires and everything else. |
| [decision-log](modules/decision-log/) | base | Why choices were made. Dated, append-only, indexed. |
| [findings-queue](modules/findings-queue/) | base | Where a finding goes when it is real but not scope. |
| [work-units](modules/work-units/) | optional | Falsifiable definitions of done, and rules stated once. |
| [investigations](modules/investigations/) | optional | What was tested, what was observed, what rules came out. |

All at `0.1.0`. Each carries a README arguing both sides, with at least three
concrete costs and a one-line exit instruction.

### There is no checker

This is the largest single decision in the release and the largest cost to a
first adopter: **you write the checker**, in whatever your project already uses.
What you get instead of a tool is a specification precise enough to implement
and 33 fixture trees that tell you whether your implementation is right.

The reasoning, including what was given up, is in
[decisions.md](docs/records/decisions.md#there-is-no-runner-and-that-is-the-largest-single-decision-here).

### What this does not do

- **It does not enforce anything.** No badge, no score, no adopter registry, no
  gate. This repository keeps no record of anyone who uses it.
- **It does not fix your repository.** A remediation may create a file that is
  absent or move existing content; it may never author substance and never
  applies itself. The argument is in
  [decisions.md](docs/records/decisions.md#remediation-may-move-content-but-never-author-it).
- **It does not check that anyone follows a process.** Nothing here can. The
  checks confirm records exist and have the shape their obligation needs — which
  is the part that rots silently.
- **It does not cover verification.** Commit gates, the sabotage discipline, and
  the documentation pass are all in the source material and none are here; they
  are verification obligations, not records obligations, and belong to a family
  that does not exist yet.
- **Six checks were cut** for being satisfiable by a machine writing a word.
  They are listed with the reasoning in
  [decisions.md](docs/records/decisions.md#six-checks-were-cut-for-measuring-presence-rather-than-thought).

### Known limitations

- `role_referenced` resolves markdown links only, so a record naming its
  destination in prose is not covered — and prose is the form the original
  defect took. Recorded as `F2` in
  [findings.md](docs/records/findings.md).
- `DL-03` is the one check with no self-contained fixture; it reads git history,
  and a fixture cannot carry a nested repository. Its tree ships with the
  commands to build the violating history.
- `WU-04` has the highest false-positive rate in the catalog. Any
  angle-bracketed literal matches its placeholder pattern.
- The deviation mechanism is specified and worked through in three documents and
  **untested by use** — this repository has no genuine deviation, and one was
  not invented to exercise it.
