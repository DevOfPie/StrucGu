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

### The contract

[SPEC.md](SPEC.md) defines a third schema identifier, `strucgu/expected@1`, and
the list of what a module directory holds now names `fixtures/expected.yaml`.
Nothing an adoption record or a checker written against `0.1.0` has to change —
a checker that ignores the file is still a checker.

**A checker written against `0.1.0` does have to change now.** The first
independent implementation was built from this specification alone and came back
with eighteen places it did not determine what the checker should do. The
answers are written into the contract, and most of them change what a conformant
run outputs:

- A `dir` role reaches into subdirectories; its `exclude` list lives on the role
  and matches basenames at any depth, while the adoption record's matches paths
  from the repository root. Per-file results collapse to **one** state for the
  role — `finding` if any file fails, `ok` only if every file passes.
- `path_exists` requires a **tracked** path only where the audited root is a git
  repository, and a `dir` role needs a surviving **markdown** file rather than
  any file.
- A check bound to more than one role evaluates over the roles that resolved and
  skips only when none did. It no longer skips because one of three was absent.
- `history_deletions` reads the repository rooted at the audited root and does
  not walk up to find one. A record vendored inside a monorepo was otherwise
  audited against history its owner does not control.
- `effective_from` is **exclusive**, and a date is compared against committer
  date.
- A `judgment` line names the roles it could not read, instead of pointing a
  person at a document that is not there.
- The exact version pin documents intent and reports drift. It does not, and
  cannot, stop a checker evaluating the module it actually read — the previous
  wording implied otherwise.
- `fixtures/` takes **at least** one violating tree per check, with further
  trees named `violates-<CHECK-ID>-<suffix>/`. A check with two boundaries worth
  pinning could not previously have both pinned.

[auditing.md](docs/auditing.md) gains the missing entry in its closed list of
reasons a run cannot start — an adopted `history_deletions` check with no
`effective_from` — and states that history is read from the audited root.

The full record, including the readings that were available and the ones
declined, is
[investigations/0001](docs/records/investigations/0001-what-the-specification-does-not-determine.md).

### The modules

All five moved to `0.2.0` when `expected.yaml` was added: the same expected
results as data, keyed by fixture tree and check id, plus one entry per judgment
id, with the prose file staying as the statement of intent.

Since then, all five have moved again:

| Module | | | A previously clean adopter newly sees |
| --- | --- | --- | --- |
| [decision-log](modules/decision-log/) | `0.3.0` | `DL-03` reports `skip`, not `ok`, where no history is readable. A fixture pins that runs of spaces are not collapsed when slugging an anchor. | Nothing, unless the audited root is not a git repository — there `DL-03` reports `skip` instead of `ok`, which is a pass correctly downgraded to "I could not tell". |
| [findings-queue](modules/findings-queue/) | `0.3.0` | A second violating tree for `FQ-06` pins that a reference-style link is a link. | Nothing. |
| [triage-rule](modules/triage-rule/) | `0.3.0` | A fixture pins that code is not scanned for links. | Nothing. |
| [investigations](modules/investigations/) | `0.2.1` | Its `module.md` no longer says this repository leaves the role unmapped, because it does not. | Nothing. |
| [work-units](modules/work-units/) | `0.2.1` | `WU-04`'s pattern was HTML-escaped in `module.md` and could not match the placeholder text the check exists to catch. Repaired. Two fixtures pin how a `dir` role aggregates and that `pattern_present` needs every pattern. | **Findings**, if your checker read `module.md` rather than `module.yaml`. `WU-04` fires on angle-bracketed placeholders it previously ignored. |

Three of those fixtures pin rules this specification argues for at length and no
tree had ever tested. They exist because the implementation was broken on purpose
nine ways and re-run: five breakages went unnoticed by the catalog as it stood,
and none goes unnoticed now.

`work-units` is the one row where the honest answer is not "nothing", and it is a
**patch** anyway. The obligation, the check, its violating fixture and the
behaviour described to adopters in that module's README and `0.1.0` changelog are
all unchanged — the prose half had been carrying a corrupted transcription of a
pattern the manifest and the fixture expectations have both stated since the
first release. A checker that followed the normative half literally was doing
what it was told and its adopters are surprised anyway; that cost is named rather
than argued away in
[decisions.md](docs/records/decisions.md#repairing-a-checks-transcription-is-not-adding-a-check).
Turning `WU-04` off remains the recommendation for records that legitimately
quote angle-bracketed literals.

Adoption records are deliberately left pinned at `0.1.0` in the fixture trees. A
pin is a dated claim about what was reviewed, and the
[self-walk](docs/records/self-walk.md) was run against `0.1.0`.

This repository's own [strucgu.yaml](strucgu.yaml) now maps `investigations`,
which was `~` from the first release. The four `IN-*` checks stop reporting
`skip` because a real investigation exists, and the repository loses its only
live demonstration of the `skip` path.

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
