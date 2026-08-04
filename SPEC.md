# The module contract

Normative. Everything in [modules/](modules/) is downstream of this file.

No runner ships with this repository, so this document is the only thing that
makes two independent implementations agree. It is written to be implemented
from, not read once.

---

## Vocabulary

| Term | Meaning |
| --- | --- |
| **Module** | A named set of conventions with a README, a version, and numbered checks. |
| **Obligation** | One statement a module makes about a repository that adopted it. |
| **Check** | One observable test of an obligation. The unit that reports. |
| **Role** | A logical artifact name a module refers to. Never a path, never a filename. |
| **Adoption** | A repository's recorded claim that a module applies to it, at a pinned version and a stated scope. Voluntary, revocable, never inferred. |
| **Adoption record** | The one file in the consuming repository carrying every adoption, role map, exclusion and deviation. Hand-edited; no tool writes it. |
| **Base** | A module required for an adoption to be an adoption. Three of them. |
| **Prerequisite** | A module another module needs in order to be falsifiable. Not an obligation on anyone. |
| **Audit** | A read-only run of a module's checks against a repository. Writes nothing. |
| **Finding** | One failed check, with a location and evidence. A report, not a task. |
| **Deviation** | A finding the owner accepted, with a reason and an expiry. Reported every run, never a failure. |
| **Proposal** | A suggested remediation. Emitted as a diff; applied only by a person. |
| **Objection** | An argument that the module is wrong rather than the repository. Filed by a person. |
| **Checker** | Any implementation of this document. There is no reference one. |
| **Owner** | Whoever the adoption record names. The only party who accepts a deviation, applies a proposal, or files an objection. |

Three words are banned from every file in this repository: **certified**,
**certification**, and **compliant** used as a repository-level status.
"Conforms to `DL-03`" is a statement about one check and is fine. "A compliant
repository" is a grade, and a grade implies a grader.

---

## What a module is

A directory under [modules/](modules/) containing exactly these, and — where a
row names a directory — exactly what that row lists inside it:

| File | | |
| --- | --- | --- |
| `README.md` | required | The adoption decision. Benefits, at least three concrete costs, who should not adopt this, and how to stop using it in one line. |
| `module.md` | required | The obligations and checks in prose. **Normative.** |
| `module.yaml` | required | The same obligations and checks as data. Convenience. |
| `CHANGELOG.md` | required | Per version, what a previously clean adopter will newly see. |
| `templates/` | required | Starting files, one per role where a starting file makes sense. Licensed MIT-0. |
| `fixtures/` | required | A `satisfies/` tree, at least one `violates-<CHECK-ID>/` tree per check, `expected.md`, and `expected.yaml`. A check with more than one boundary worth pinning may carry further trees named `violates-<CHECK-ID>-<suffix>/` — a boundary needing two trees is otherwise unpinnable, and an unpinned boundary is where two correct-looking checkers disagree. A boundary pinned by a tree where **every check passes** is named `satisfies-<suffix>/`, for the case `satisfies/` cannot hold because the content that pins it contradicts what that tree already carries. Each name asserts what its tree does: `violates-<CHECK-ID>` that the tree violates that check, `satisfies-` that nothing here fails. See [Fixture expectations](#fixture-expectations). |

**Prose is normative; the manifest is convenience.** A checker may read either.
If they disagree, `module.md` wins **and the disagreement is a defect — report
it, do not pick.** A checker that silently prefers one is hiding a bug in this
repository.

### Structure and use, not content

The rule the rest of this document rests on.

A module describes the **shape** a record has and **what it is for**. It never
describes what to write in it. A module may require that a findings queue has an
evidence column and may say what that column is for; it may not say what belongs
in the column.

Two consequences, and the second is the more useful one.

*Remediation is safe.* If only structure is checked, a proposal can only
relocate existing content or create empty structure, because authoring substance
is outside what the module describes. See [Remediation](#remediation).

*There is a cut criterion.* A behaviour check that a machine could satisfy by
authoring text is measuring presence rather than thought. The canonical failure:
a required Risks section, satisfied by writing "Low." The check passes, the
section now reads as considered, and the signal it existed to carry is gone
permanently. **Cut those checks**, and record what was cut — that list is worth
more than the checks that survive.

### Declaration checks and behaviour checks

The cut criterion above applies to one of two kinds, and applying it to both
removes most of the value.

A **declaration check** tests that a record states its own contract — a decision
log saying it is append-only, a findings queue saying its rows are unscheduled.
A machine can obviously write that sentence, and that is fine: the sentence is a
notice to a reader who would otherwise do the wrong thing, and whether it is
*true* is tested elsewhere. Declaration checks may be scaffolded.

**A declaration check must name the behaviour check that tests whether its
declaration is true.** One with no such pairing anywhere is decoration; say so in
`module.md` or cut it.

A **behaviour check** tests what the repository actually did. Never scaffolded,
never satisfiable by authoring text, and the cut criterion applies in full.

Every check in a manifest carries `nature: declaration` or `nature: behaviour`.

---

## Roles

A module names roles. The adoption record maps roles to paths. Nothing else
connects them, and nothing in a module may name a path.

```
module says:      role  decision_log   "where rationale is recorded"
consumer says:    decision_log: doc/adr/
check binds:      in: decision_log
```

This is what lets a repository adopt a convention without renaming anything.
"Milestone" already means something on GitHub, "finding" already means something
to a security scanner, and a repository with years of history has no interest in
moving files to satisfy a convention it just adopted.

A role declares a `cardinality` of `file` or `dir`. A role of `cardinality: dir`
may also declare an `exclude` list.

When a role is `dir`, a check bound to it applies to every markdown file in that
directory **and below it**, minus that role's `exclude` list — matched against
each file's basename, at any depth — and the adoption record's, matched against
the path relative to the repository root. A record filed in a subdirectory is
still a record; a directory a checker declines to descend into is reported as
neither checked nor skipped, which is the one outcome the five states exist to
prevent.

The check reports **one** state for the role: `finding` if any file fails it,
`ok` only if every file passes. A role with no surviving markdown file fails
`path_exists`, so a content check never runs vacuously over an empty directory
and reports `ok` from nothing having been looked at.

When an obligation declares `forms` and the shape differs between them, a role
declares `cardinality: by_form` and a `cardinality_by_form` map from form id to
`file` or `dir`. A checker resolves it against the `form` the adoption record
declares. If the adoption record declares no form for a module that has them,
that is an unparseable record — a run that cannot start, not a finding.

**An unmapped role produces `skip` on every check bound to it — never `ok`.**
Absence of a declaration is not evidence of anything.

---

## Obligations

```yaml
- id: decision-log-append-only
  title: A decision record is never edited away; a later entry corrects an earlier one
  purpose: >
    The record that an earlier belief was held is the thing being preserved.
    Editing an entry to make it current destroys exactly what the log is for.
  required: true
  forms:
    - id: single-log
      of: One growing file, newest entry last.
    - id: per-decision-files
      of: One file per decision, plus an index.
  roles: [decision_log]
```

`purpose` is load-bearing and not decoration. It is the thing an objection has to
argue against: a repository claiming its way is better must show its alternative
serves the stated purpose, not merely that it prefers it. An obligation with a
vague purpose cannot be objected to, which makes it unfalsifiable.

`forms` exist so that a legitimate alternative shape is *configuration* rather
than a deviation. A module whose first impression is that there is one true way
contradicts the posture of the whole catalog.

`required: conditional` is permitted and must carry a `condition` in prose. The
condition is evaluated by a person at adoption time, never by a checker — a
module that decides for itself whether it applies is a module that imposes.

---

## Check vocabulary

Closed. Adding a kind is a change to this document, not to a module. Adding a
check of an existing kind is a module edit. That friction ratio is deliberate.

| kind | observes | binds |
| --- | --- | --- |
| `path_exists` | The role resolves to an existing path. Where the audited root is a git repository the path must also be tracked — a role mapped at an ignored or never-added path exists for its author and for nobody who clones. Where it is not a repository, existence is the whole test: trackedness has no truth value there, and requiring it would fail every check on an exported tree, including these fixtures. For a `dir` role, the directory must also contain at least one **markdown** file that survives exclusions — a directory holding only an empty-directory placeholder satisfies a filesystem check while satisfying nothing the obligation wanted. | one role |
| `heading_present` | Every listed pattern matches at least one heading. | one role |
| `pattern_present` | Every listed pattern matches somewhere in the target. | one role |
| `pattern_absent` | No listed pattern matches anywhere in the target. | one role |
| `links_resolve` | Every relative link and anchor in the target resolves. | one or more roles |
| `role_referenced` | The target contains a relative link resolving to another role's path, anywhere in it. | two roles |
| `history_deletions` | Commits removed lines from the target. Requires `effective_from`. Read from the repository whose root is the audited root. | one role |

**There is no `kind: shell` and there never will be.** A manifest that can carry
an executable string means adopting a module is arbitrary code execution on the
adopter's machine, and the data format degenerates into "run this script" within
a month. A check that cannot be expressed here becomes a `judgment` entry, which
is the honest fallback.

### Matching rules

Patterns are extended regular expressions, matched case-insensitively. A checker
that uses a different regex flavour is conformant as long as it produces the
findings in `expected.md` for every fixture.

`heading_present` matches against the *text* of markdown ATX headings (`#`
through `######`), with the leading hashes and surrounding whitespace stripped.

`links_resolve` resolves a relative target against the directory of the file
containing it. Anchors use GitHub's slug algorithm: lowercase, strip every
character that is not `[a-z0-9 _-]`, then replace each space with one hyphen.
**Runs of spaces are not collapsed** — collapsing them is the obvious
implementation and it is wrong; it rejects correct anchors. External schemes
(`http`, `https`, `mailto`) are not checked, because a check that depends on
someone else's uptime fails for reasons the repository cannot fix.

**Code is not scanned for links** — neither fenced blocks nor inline spans.
Found by running the check over this repository, twice: a module's own check
patterns are written in fences, and a pattern of the shape
`in` followed by a bracketed alternation contains the exact byte sequence a
naive link extractor matches on. Excluding fences alone was not enough, because
the same pattern appears inline in this file and in the decision log. A checker
without both rules reports findings against regular expressions, including the
ones in the specification that told it what to do.

`role_referenced` produces `skip`, not a finding, when the referenced role is
unmapped or its module is not adopted. This is what makes it safe in a
repository that adopts one module and not another. It tests that the link's
*path* resolves to the other role, not that any anchor on it resolves — a link
to the right document with a rotted anchor passes here and is reported by
`links_resolve`, which is where it belongs.

**A check whose target cannot be read reports `skip`, not a finding.** When
`path_exists` fails for a role, every other check bound to **only** that role
skips: they did not observe anything, and reporting five findings for one absent
file tells a reader the repository is five times more broken than it is.

A check bound to more than one role evaluates over the roles that did resolve,
and skips only when none of them did. A `links_resolve` bound to three roles, one
of which is absent, has read two of them and reporting `skip` would claim it
could not tell.

`history_deletions` reports commits, not lines, and **must not be run over
history earlier than the adoption record's `effective_from`.** Without that
bound, the first run on a mature repository produces four-figure findings, and
an audit that reports four thousand findings on day one is deleted the same day.

**History comes from the repository rooted at the audited root** — the directory
holding `strucgu.yaml`. A checker does not discover the repository by walking up
from there: an adoption record vendored inside a larger repository, or a
submodule checked out in place, would otherwise be audited against history its
owner does not control, producing findings naming commits they cannot see.

### Known false positives

A checker is not wrong to report these. `module.md` must name them per check so
an adopter can recognise one.

- `pattern_present` and `pattern_absent` cannot see intent. A pattern matching
  inside a code block, a quotation, or an example is a match.
- `role_referenced` resolves markdown links only. A record that names its
  destination in prose rather than as a link is not covered — which makes this a
  limitation on the **obligation** rather than a false positive in the check:
  an obligation served by this kind asks for a link, never for a name, or it
  claims coverage the check does not have. `F2` in
  [findings.md](docs/records/findings.md) is closed on that reading, and
  `triage-destination` is the obligation that was reworded to it.
- `history_deletions` cannot distinguish an entry being erased from a file being
  split or renamed. It reports for a look; the judgment is a person's.

### Judgment entries

Everything a check cannot decide. A manifest declares them so that a purely
mechanical run can never look complete: **a checker emits one `judgment` line per
entry whether or not anyone is available to judge it**, and whether or not the
roles it names resolve. Where a `read:` role is unmapped or unreadable the line
says so — the entry is still emitted, because a mechanical run must never look
complete, but a person handed the output must not be sent to a document that is
not there. The state does not vary by tree; the annotation does.

```yaml
judgment:
  - id: decision-log.claim-shaped
    obligation: decision-log-entries-are-claims
    question: Are entry headings assertions that can be true or false, or topics?
    read: [decision_log]
    evidence: Quote headings verbatim. "Caching" is a topic. "Cache TTL is clamped to link expiry" is a claim.
    do_not_report: Headings that are claims but that you would have worded differently.
```

`do_not_report` is required. Without it a judgment entry becomes an invitation to
report taste, and taste reported as a finding is how an adopter learns to ignore
the whole output.

---

## The manifest

```yaml
schema: strucgu/module@1
id: glossary
version: 0.1.0
title: Project glossary
summary: >
  One place defining the terms this project uses in a sense a newcomer would
  not guess, so that a reader who has not been here can read anything else.
base: false
requires: []

applies_when:
  - The project has invented or narrowed a term whose everyday meaning differs.
  - Someone will read this repository without having been in the conversations.
not_for:
  - A project whose vocabulary is entirely standard for its field.
  - A glossary nobody maintains; a stale definition is worse than none.

roles:
  - id: glossary
    cardinality: file
    of: Where terms are defined.

obligations:
  - id: glossary-exists
    title: Terms used in a non-obvious sense are defined in one place
    purpose: >
      A reader who guesses a term's meaning wrongly misreads every document that
      uses it, and does not know they have.
    required: true
    roles: [glossary]

checks:
  - id: GL-01
    obligation: glossary-exists
    nature: behaviour
    kind: path_exists
    in: glossary
    finding: >
      No glossary is declared or present. Terms used in a project-specific sense
      have no definition a reader can find.
    false_positives: none

  - id: GL-02
    obligation: glossary-exists
    nature: behaviour
    kind: links_resolve
    in: [glossary]
    finding: >
      A relative link or anchor in the glossary does not resolve. A definition
      pointing at something that moved costs a reader their trust in the rest.
    false_positives: none

judgment:
  - id: glossary.non-obvious
    obligation: glossary-exists
    question: Does the glossary define terms whose everyday meaning differs, or does it define terms nobody would misread?
    read: [glossary]
    evidence: Quote an entry. "API — application programming interface" defines nothing.
    do_not_report: Entries that are non-obvious but that you would have worded differently.
```

The example is deliberately **not** one of the five modules in this repository,
so that this document describes a contract rather than its only instances.

### Field reference

| Field | | |
| --- | --- | --- |
| `schema` | required | `strucgu/module@1`. |
| `id` | required | Directory name. Lowercase, hyphenated. |
| `version` | required | Semantic version. Must match the newest `CHANGELOG.md` entry. |
| `title`, `summary` | required | Human-facing. |
| `base` | required | Whether an adoption is incomplete without it. Three modules carry `true`. |
| `requires` | required | Module ids this one needs to be falsifiable. May be empty. |
| `applies_when`, `not_for` | required | Evaluated by a person at adoption time, never by a checker. |
| `roles` | required | `id`, `cardinality`, `of`, and `exclude` on a `dir` role. May be empty only if every check binds roles from a prerequisite. |
| `obligations` | required | See [Obligations](#obligations). |
| `checks` | required | Every check names an existing obligation and existing roles. |
| `judgment` | required | May be empty, and empty is a claim worth questioning. |

---

## The adoption record

One hand-edited file at the consuming repository's root: **`strucgu.yaml`**.
Visible rather than a dotfile — it is a claim the repository makes about itself,
and hiding it contradicts writing for a reader who does not trust you.

**No tool writes this file.** A checker that edits the adoption record can make
itself pass.

```yaml
schema: strucgu/adoption@1

modules:
  decision-log:
    version: "0.1.0"
    adopted: 2026-07-31
    form: per-decision-files
    effective_from: 9f3c1ab
    roles:
      decision_log: doc/adr/
      decision_index: doc/adr/README.md
  findings-queue:
    version: "0.1.0"
    adopted: 2026-07-31
    roles:
      findings: .github/QUALITY.md
  work-units:
    version: "0.1.0"
    adopted: 2026-07-31
    roles:
      unit_dir: ~
      unit_template: ~
      unit_index: ~

exclude:
  - vendor/**
  - docs/legacy/**

deviations:
  - check: DL-03
    title: Decision records are edited in place when superseded
    accepted: 2026-07-31
    by: maintainer@example.org
    reason: >
      The tooling the whole team uses rewrites a superseded record's status line
      in place. The supersession pointer is preserved, which is the property
      DL-03 protects.
    scope: doc/adr/**
    review_by: 2027-01-31
    upstream: DevOfPie/StrucGu#14
```

| Field | | |
| --- | --- | --- |
| `version` | required | **Exact.** A checker refuses to run against a floating version — see [Versioning](#versioning). |
| `adopted` | required | The date the claim was made. |
| `form` | when the module declares `forms` | Which shape this repository uses. |
| `effective_from` | when any adopted check is `history_deletions` | A commit or a date — a commit if git resolves it, a date otherwise. **Exclusive:** the named commit is the last one out of scope, and where a date is given commits are compared by committer date. History before it is not out of compliance; it is not covered. |
| `roles` | required | Role id to path. `~` means deliberately unmapped, and every check bound to it reports `skip`. |
| `exclude` | optional | Globs excluded from every `dir` role. |
| `deviations` | optional | Accepted findings. |

### Deviations

| Field | | |
| --- | --- | --- |
| `check` | required | The check id being deviated from. |
| `title`, `reason` | required | **A deviation with no reason is indistinguishable from a bug.** |
| `accepted`, `by` | required | When, and by whom. |
| `scope` | required | Where the deviation applies. |
| `review_by` | required | An expiry. **A deviation with no expiry is a silent fork.** Past it, the check reports a finding again — detection reasserting itself without anyone enforcing anything. |
| `upstream` | optional | A filed objection. This is where "my way is more correct" is recorded next to the deviation it justifies. |

Deviations live in the consuming repository. **This repository keeps no registry
of anyone who adopts anything** — that is the structural guarantee that there is
nothing to grade against, rather than a promise of good behaviour.

---

## Audit output

A checker must distinguish five states and must never fold one into another.

| State | Meaning |
| --- | --- |
| `ok` | The check passed. |
| `finding` | The check failed. Carries a location and evidence. |
| `skip` | The role is unmapped, unreadable, or its module is not adopted. **"I could not tell", which is not the same as "fine".** |
| `waived` | An accepted deviation. The reason is echoed every run, not silently suppressed. |
| `judgment` | Needs a person. Emitted whether or not one is present. |

A run's summary states all five counts. A run reporting only `ok` and `finding`
is hiding something.

**A checker writes nothing to the repository it audits.** Auditing and fixing
are separate acts; an audit that edits is a push. Read-only git operations only.

### Exit status, and why the default is not a gate

Recommended: **exit zero when the audit ran, non-zero only when it could not** —
an unparseable adoption record, an unpinned version, a module directory that is
not there. Findings are output, not failure.

A consumer who wants to gate on findings should have to ask for it explicitly,
and should wire it in only after their first clean run. A check that fails on day
one in a repository with required status checks gets made non-required within the
hour, and then nobody looks at it again. That is how a gate dies, and a dead gate
is worse than no gate because it looks like coverage.

### Ambiguity is a missing fixture

Since no implementation is normative, two correct-looking checkers can disagree
about a real repository. **That is not a defect in either.** It is a check whose
fixtures do not pin the boundary.

File it — see [docs/objections.md](docs/objections.md) — and the fixture that
settles it becomes part of the specification. This is the ordinary way the
specification gets sharper, not an edge case.

---

## Fixture expectations

Every module states its fixture results twice. `expected.md` is prose: why each
tree exists and which boundary it pins. `expected.yaml` is the same statement as
data, so that the one question an implementer actually has — *did my run match?*
— is answered mechanically rather than by reading every tree against every
document.

```yaml
schema: strucgu/expected@1

checks:
  satisfies:
    GL-01: ok
    GL-02: ok
  violates-GL-01:
    GL-01: finding
    GL-02: skip
  violates-GL-02:
    GL-01: ok
    GL-02: finding

judgment:
  glossary.non-obvious: judgment
```

Two sections, and nothing else in the file.

| Section | | |
| --- | --- | --- |
| `checks` | required | Keyed by fixture tree, then by check id. |
| `judgment` | required | Keyed by judgment entry id. **Not per tree** — one line is emitted per entry on every tree whether or not anyone is available to judge it, so the value cannot vary by tree, and that invariance is the property being recorded. |

Every value is one of the five states in [Audit output](#audit-output). **The
vocabulary is closed there rather than here:** a sixth value is a change to this
document, and cannot enter through a fixture directory.

A file keyed by check id alone cannot express a judgment entry, because those
carry their own ids. A conformance test built on one would be silent on the one
output channel that stops a mechanical run from looking complete.

**Every tree in the directory has an entry, and every entry names a tree that is
there.** A missing row and a passing check are otherwise indistinguishable. Only
the module's own checks and judgment entries appear, even where a tree adopts a
prerequisite as well — the prerequisite's results are that module's fixtures.

**No finding text.** What a finding must carry is a location and evidence, which
[Vocabulary](#vocabulary) already states and each check's `finding` field
already explains; how it reads is the implementer's. A file pinning the wording
would make one implementation's phrasing normative, which is the thing shipping
no runner refused.

**`expected.md` stays the statement of intent.** The two must agree. Where they
do not, that is a defect to report and not a precedence order to apply — the
same rule `module.md` and `module.yaml` already carry.

---

## Remediation

A checker may propose. It may not fix.

| Permitted | |
| --- | --- |
| **Scaffold** | Create a role's artifact when its path does not exist. **Refuses if the path exists at all, even malformed.** Create-if-absent is the only write mode that cannot destroy information. Only for `declaration` checks and `path_exists`. |
| **Relocate** | Move existing content into the structure the module describes. |
| **Emit** | A unified diff, to standard output or a scratch path. |

| Forbidden | |
| --- | --- |
| Authoring substance | Never a Risks section, a definition-of-done bullet, or an evidence cell. |
| Moving content out of an append-only record | A move is a deletion at the source. |
| Applying anything | The owner decides. |

**The append-only exception has a worked precedent.** When LinkCtrl's findings
queue moved out of `Plan.md`, the section left behind became a forwarding stub
rather than a hole. From an append-only record the proposal is always a pointer,
never a move.

**Never touched, under any flag:** decision-log entries, any approval or review
state, any dated field, git history, commit messages, the adoption record, or
any file with uncommitted changes.

**Read-only git only** — `ls-files`, `status --porcelain`, `rev-parse`, `log`.
Never `checkout`, `stash`, `reset`, `clean`, `add`, `commit`, `update-index`.
`git checkout` used to make a fix atomic is the single operation that has already
destroyed uncommitted work in the repository this catalog was extracted from,
twice.

One finding, one patch. Bundling is how a remediation becomes the largest
unreviewed change in a repository's history.

Any proposal for a `declaration` check must print, verbatim:

> This makes the check pass. It does not make the claim true.

### Objections are drafted, not filed

A checker may print a prefilled objection body. **A person posts it.**

Audit output from a private repository contains file paths, internal project
names, and quoted lines. A tool that posts that to a public tracker is an
exfiltration channel with a friendly name.

---

## Base and prerequisites

**Base** — a module without which an adoption is not an adoption. Three carry
`base: true`.

**This section is the argument's one normative home.** Every other document that
mentions the base set links here rather than restating it, including
[README.md](README.md). Two prose statements that must agree and that no check
can compare will eventually disagree, and the one that gets edited is whichever a
reader arrived at first.

| Base module | What breaks without it |
| --- | --- |
| `triage-rule` | Nothing decides what belongs in the findings queue, so no row in it can be wrong about anything. |
| `decision-log` | There is no record of why a choice was made, so a project that disagrees with a module here has nothing to argue from. |
| `findings-queue` | Every incidental discovery becomes scope, which is the failure this whole family exists to prevent. |

Each module's own README argues its adoption in full, at a length this table is
not trying to reach. What is normative here is which three are base and what
their absence breaks.

Nothing forces adoption of anything, and a repository may copy a template and owe
nothing at all. But "adopt this catalog and skip the decision log" is like "use
semantic versioning and skip version numbers" — refusing to call that an adoption
is a definition, not a demand.

**The base list stays at three.** Growing it is a major version that must argue
its case. A base list that grows makes adoption all-or-nothing, and
all-or-nothing is enforcement wearing a new name.

**Prerequisite** — a module another module needs to be falsifiable, declared in
`requires`. `findings-queue` requires `triage-rule`, because with no rule
deciding what belongs in the queue no row can be wrong. A prerequisite is a
dependency edge inside the catalog and imposes nothing on anyone; a checker
reports `skip` for checks whose prerequisite is not adopted.

---

## Versioning

Bumps are defined by **what a previously clean adopter will newly see**, not by
how much source changed.

| Bump | |
| --- | --- |
| MAJOR | A check was added. An obligation was added or its shape changed. The base list changed. A role was renamed. |
| MINOR | A check was narrowed. A `form` was recognised. A template or README changed. Nothing a clean adopter newly sees. |
| PATCH | Wording. A false positive documented. |

**A new check never ships in a minor version.** If it could, upstream would be
able to publish findings into every adopting repository at will — enforcement by
release, through a channel nobody would think to close. Exact pins exist for the
same reason, and a checker that accepts a floating version hands the same power
back.

Every `CHANGELOG.md` entry states, in a fixed sentence, what a previously clean
adopter will newly see. For a first release that sentence is "nothing", **written
out rather than omitted** — an omitted sentence is indistinguishable from a
forgotten one.

Propagation is pull-only. No bot, no pull request, no notification. The mechanism
is the pin: a checker notices the module it read is newer than the version
declared and prints one line pointing at that module's changelog. That is the
entire push surface, and it is a print statement.

**A checker evaluates the module as it reads it.** Nothing in a module lets it
evaluate a version other than the one in the working tree, so an exact pin that
is behind the module on disk does not withhold newly added checks — it records
what the adopter agreed to and produces the notice. Where the read version is a
MAJOR ahead of the pin, checks may have been added since the adopter agreed, and
the notice says so. The pin documents intent and reports drift; it does not
constrain what runs, and a reader should not assume otherwise.
