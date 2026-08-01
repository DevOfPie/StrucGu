# Decisions

Why things are the way they are. [work/README.md](work/README.md) states what is
true and what the status is; this file states why. Rationale in the work index
and status in this log are both wrong.

Entries are append-only and dated. A later entry may correct an earlier one; the
earlier text is left in place with a pointer rather than edited away, because
deleting it destroys the record that the earlier belief was ever held.

Headings are claims — things that can be true or false. "Check kinds" is a
topic; "The check vocabulary is closed" is a claim. Topics accumulate; claims
can be contradicted by a later entry, which is the whole point of the file.

Longer investigations that outgrow an entry here get their own record.

---

## Index

Navigation only — adding to it is not editing an entry. Newest last, matching
the file. Append a row when you append an entry.

| Entry | Covers |
| --- | --- |
| [StrucGu exists because LinkCtrl's workflow is not reusable](#strucgu-exists-because-linkctrls-workflow-is-not-reusable) | Why the repository exists at all |
| [The catalog is five small modules, not one](#the-catalog-is-five-small-modules-not-one) | Granularity |
| [Three modules are base, and the list is closed at three](#three-modules-are-base-and-the-list-is-closed-at-three) | What "required" means |
| [There is no runner, and that is the largest single decision here](#there-is-no-runner-and-that-is-the-largest-single-decision-here) | Spec-only |
| [Modules define structure and use, not content](#modules-define-structure-and-use-not-content) | The keystone rule |
| [Declaration checks and behaviour checks are different things](#declaration-checks-and-behaviour-checks-are-different-things) | A refinement of the keystone rule |
| [The check vocabulary gained a seventh kind before any module was written](#the-check-vocabulary-gained-a-seventh-kind-before-any-module-was-written) | `role_referenced` |
| [Adoption is one visible file at the repository root](#adoption-is-one-visible-file-at-the-repository-root) | Consumer binding |
| [Remediation may move content but never author it](#remediation-may-move-content-but-never-author-it) | Auto-fix, reversed |
| [Self-application is dogfooding, not evidence](#self-application-is-dogfooding-not-evidence) | Why fixtures are the proof |
| [StrucGu's own records use different filenames from LinkCtrl's](#strucgus-own-records-use-different-filenames-from-linkctrls) | Naming as evidence |
| [The commit gates and the sabotage rule are deliberately not extracted](#the-commit-gates-and-the-sabotage-rule-are-deliberately-not-extracted) | What v1 leaves out |
| [A new check never ships in a minor version](#a-new-check-never-ships-in-a-minor-version) | Versioning |
| [Objections are drafted by a tool and filed by a person](#objections-are-drafted-by-a-tool-and-filed-by-a-person) | The feedback loop |
| [Six checks were cut for measuring presence rather than thought](#six-checks-were-cut-for-measuring-presence-rather-than-thought) | What did not ship, and why |

---

## 2026-07-31 — before anything was written

### StrucGu exists because LinkCtrl's workflow is not reusable

LinkCtrl accumulated a set of process conventions that work: a triage rule that
keeps incidental discoveries out of scope, an append-only decision log, a
findings queue where approval is per item, definitions of done written as
falsifiable claims. None of it is portable. Starting another project means
rebuilding it from memory, and any improvement discovered while using it dies in
the repository that discovered it.

Two defects found in LinkCtrl while scoping this repository settle that the
problem is real rather than theoretical:

1. `docs/build-notes/workflow.md:34` still instructs the reader to append a
   deferred finding to `Plan.md`. The queue moved to
   `docs/build-notes/deferred-findings.md`; `Plan.md:454` is now a forwarding
   stub. Nothing caught it — `check-links.sh` validates markdown links, and this
   reference is prose.
2. `docs/build-notes/phase-details/README.md:10` says "**Status lives here**, and
   only here" while `Plan.md:388` maintains a second status table. Two status
   homes, one of them declared exclusive.

Both are exactly the class of drift a structural check finds and a human
re-reading their own docs does not, because the author knows what the sentence
was supposed to mean.

### The catalog is five small modules, not one

The alternative was a single `process-records` module with required and optional
sections. One README, one version, one thing to explain.

Five was chosen because the other two mechanisms are meaningless without it.
Prerequisites between modules have nothing to operate on when there is one
module. "Base" becomes an all-or-nothing gate rather than a flag on a module.
And an existing repository that wants only the decision log would have to take
the whole thing or use per-check opt-out as its only escape, which turns the
common case into an exception.

The cost is real and is paid in maintenance: five READMEs, five version numbers,
five changelogs, and five places where a shared idea can be stated
inconsistently. Accepted because the alternative fails the case this repository
exists to serve, which is a repository with years of history adopting one
convention rather than a process.

### Three modules are base, and the list is closed at three

"Required" has three readings and only two of them are usable.

*Prerequisites between modules* — a module another module needs to be
falsifiable. `findings-queue` requires `triage-rule` because without a rule
deciding what belongs in the queue, no row can be wrong. This imposes nothing on
anyone; it is a dependency edge inside the catalog.

*Required given a repository's own claim* — the audit has nothing to say until
the repository declares which paths play which roles. The declaration generates
the obligation. This is the mechanism that keeps the third reading honest.

*Required of adopters* — the reading that sounds like enforcement. It is not,
provided adoption is voluntary: "adopt StrucGu but skip the decision log" is
like "use semantic versioning but skip version numbers", and refusing to call
that an adoption is a definition rather than a demand. What makes it enforcement
is the base list growing. A base set of three is a definition; a base set of
twelve is all-or-nothing adoption with a friendlier name.

So the guard is procedural: **three, each with a written statement of what breaks
without it, and growing the list is a major version that has to argue its case.**
The three:

- `triage-rule` — without it nothing decides what belongs in the findings queue.
- `decision-log` — without it a repository that thinks a module is wrong has no
  record of its own reasoning to argue from, and the feedback loop has nothing
  to point at.
- `findings-queue` — without it every incidental discovery becomes scope.

Note that the third is the one whose absence breaks the *user*, and the second is
the one whose absence breaks *StrucGu*. That asymmetry is deliberate and is
worth watching: a base module that only serves upstream is enforcement.

### There is no runner, and that is the largest single decision here

Three options were weighed.

A **reference implementation in POSIX shell** — the stack LinkCtrl already
proves is language-neutral, since `check-links.sh` and `release-check.sh` are
both pure shell in a Go project. Zero install, clone and run.

A **distributed static binary** — best code quality, no runtime for consumers,
but StrucGu acquires a language, a build, cross-compilation, a release pipeline
and signing, and stops being language-neutral in its own tree.

**Spec only** — chosen. Each check defined precisely enough to implement, plus
fixtures that tell an implementer whether they got it right. The consumer writes
the checker in whatever their project already uses.

Spec-only was chosen over the shell runner despite the shell runner being
cheaper for a first adopter. The reason is the failure mode of a reference
implementation: it becomes the definition. A check would come to mean whatever
the shell script does, including its bugs, and a consumer on a platform where
the script is awkward would be told their platform is the problem. Defining the
check by its meaning and its fixtures keeps a PowerShell-only shop a first-class
adopter.

The cost is stated plainly and not hidden: **the first adopter has to write a
checker before they get anything.** That is a real barrier and it will suppress
adoption. It is accepted because the fixtures make the checker verifiable, and
because a wrong checker that agrees with the fixtures is a fixture problem —
which is a shared, fixable, upstream problem rather than a private one.

New consequence that only exists under spec-only: two correct-looking checkers
can disagree about a real repository. That is not a bug in either. It is a check
whose fixtures do not pin the boundary, and it is routed into the objection
channel rather than treated as an edge case.

### Modules define structure and use, not content

The owner's rule, and it turned out to be the keystone the rest hangs from.

A module says a findings queue has an evidence column and what that column is
for. It never says what belongs in the column. The consequence that makes it
load-bearing is about remediation: if only structure is checked, a proposed fix
can only relocate existing content or create empty structure, because authoring
substance is outside what the module describes. A tool physically cannot satisfy
a check by faking its substance.

It also gives a cut criterion, which is the more valuable half. A check a machine
could satisfy by writing text is measuring presence rather than thought. The
canonical example: a required Risks section, satisfied by writing "Low." The
check passes, the section now falsely reads as considered, and the signal it
existed to carry is destroyed permanently. The set of trivially fixable checks
and the set of checks not worth having overlap almost exactly.

### Declaration checks and behaviour checks are different things

This corrects an over-broad reading of the entry above rather than the entry
itself.

Taken literally, "cut any check a machine could satisfy by writing text" cuts
the requirement that a decision log state its own append-only contract — a
machine can obviously paste that sentence. But the sentence is not the claim;
it is a notice to a reader who would otherwise edit an entry, and whether it is
*true* is tested by a different check that looks at what commits actually did to
the file.

So there are two kinds and they get different rules:

- A **declaration** check — the record states its own contract. Legitimately
  satisfiable by writing the sentence, and legitimately scaffolded, because a
  paired behaviour check tests whether the sentence is true. A declaration check
  with no paired behaviour check anywhere is decoration; say so in the module or
  cut it.
- A **behaviour** check — what the repository actually did. Never scaffoldable,
  never satisfiable by authoring text.

The cut criterion applies to the second kind only. Without this split the
catalog loses every check that makes a record self-explaining to someone who
arrives without context, which is most of the value.

### The check vocabulary gained a seventh kind before any module was written

The vocabulary started closed at six: `path_exists`, `heading_present`,
`pattern_present`, `pattern_absent`, `links_resolve`, `history_deletions`.

Writing `triage-rule` immediately showed it could not express the check that
matters most. The obligation is that a triage document names where out-of-spec
findings go. The available kinds could confirm the document exists and mentions
the words — which is precisely what LinkCtrl's `workflow.md:34` still does while
pointing at the wrong file. The check would have passed on the defect that
motivated the repository.

`role_referenced` was added: *the document mapped to role A contains a relative
link that resolves to the path mapped to role B.* It is structural, needs no
knowledge of the target's contents, and catches the real defect. It also
produces `skip` rather than a finding when role B is unmapped, which is what
makes it safe for a repository that adopts one module and not another.

Adding a kind before shipping any module is cheap; adding one after adopters
exist is a specification change they all inherit. That the vocabulary needed
widening on contact with the first real obligation is evidence it was designed
in the abstract, and the next module family should expect the same.

Known limitation, recorded as [F2](findings.md) rather than fixed: the kind
resolves markdown links only. A record that names its destination in prose
rather than as a link is not covered, and prose is exactly the form the original
LinkCtrl defect took.

### Adoption is one visible file at the repository root

`strucgu.yaml`. Alternatives and why not:

- **Git submodule** — adds a `.gitmodules` entry as well as the directory, is
  silently empty without `--recursive` on clone, and pins hard.
- **Vendored copy** — no drift detection, and a copy of upstream's normative
  text sitting inside a consumer's repository invites local edits that then look
  like upstream's position.
- **Reusable CI action** — requires a specific forge, and turns the audit into a
  gate, which is the posture this repository rejects.
- **Convention only, no file** — nothing to check against, and no way to know
  which version a repository is claiming.

Visible rather than a dotfile, because it is a claim the repository makes about
itself and hiding it contradicts writing for a reader who does not trust you.
The cost is one more line of root clutter in a directory that usually has
fifteen already.

Roles rather than paths throughout, so nothing is renamed. "Milestone" already
means something on GitHub, "finding" already means something to a security
scanner, and a repository with three years of history has no interest in
renaming files to satisfy a convention it just adopted.

### Remediation may move content but never author it

The owner's original framing was that an out-of-spec repository should fix
itself into alignment. That was reversed, and the argument that reversed it is
worth keeping because it is not the obvious one.

An auto-fixer violates the module it implements. The triage rule says out of
spec means do not fix — append a row and continue. An audit finding is, by
construction, out of spec of whatever is in flight. An agent that fixes findings
is doing precisely the thing the process exists to prevent, shipped as a feature
of the catalog that forbids it.

The second argument is the structural one, and it is in the keystone entry
above: fixability is evidence of shallowness.

Concrete failure modes that decided the boundaries. An append-only log
normalised in one unreviewable diff destroys the invariant being checked. A
review column written by a tool forges the owner's approval. A heading renamed
to satisfy a slug rule breaks inbound links from issues and other repositories
that no local check can see. A template applied to a malformed file flattens
hand-built content. `git checkout` used to make a fix atomic is the single
operation that has already destroyed uncommitted work in LinkCtrl twice.

What survives is two capabilities, deliberately not called fixing:

- **Scaffold** — create a role's artifact when its path does not exist. Refuses
  if the path exists at all, even malformed. Create-if-absent is the only write
  mode that cannot destroy information.
- **Relocate** — move existing content into the structure the module describes.

With one exception that has a worked precedent: **never move content out of an
append-only record**, because a move is a deletion at the source. LinkCtrl's
findings queue moved out of `Plan.md` and left `Plan.md:454` as a forwarding
stub rather than a hole. That is the shape.

Both are emitted as a diff and applied by a person. The owner's phrasing —
allow the maintainer to decide on the appropriate fix — is the rule.

### Self-application is dogfooding, not evidence

StrucGu carries its own records and its own adoption record. That is worth doing:
the escape hatches are where every adopter will spend their time and are the
part most likely to be badly designed, and self-application is the only way to
exercise them before anyone else does.

It is not evidence the modules work, and the README says so. An author
unconsciously writes rules they already satisfy. LinkCtrl's rules are
load-bearing because reality pushed back — checkout destroyed work twice, the
executable bit broke CI one step into a job, a slug collapser rejected twenty
correct anchors on first run. Every one of those is an incident report wearing a
rule's clothing. A documentation repository with one author gets almost none of
that pushback, so its self-application will find nothing and prove nothing.

Worse, leaning on self-application actively degrades the catalog: a repository
required to satisfy everything it publishes will avoid publishing anything it
cannot easily satisfy, which biases toward cheap presence checks — exactly the
ones the keystone rule says to cut.

So the evidence is fixtures. Every check ships with a tree that violates it and
the finding a correct checker must produce. A check with no violating fixture
does not ship. This is LinkCtrl's sabotage rule translated: break the thing the
check claims to protect, confirm it fails, and a check that has never failed has
not been shown to test anything.

Auditing LinkCtrl was considered as a third source of evidence and rejected for
now — it is the only repository available that was not written to fit these
modules, and it already yields two detections, but running a catalog against a
live project before the catalog has fixtures produces findings nobody can trust.
The two known defects are used as fixture source material instead.

### StrucGu's own records use different filenames from LinkCtrl's

`docs/records/` with `triage.md`, `decisions.md`, `findings.md`, `work/` —
against LinkCtrl's `docs/build-notes/` with `workflow.md`, `decisions.md`,
`deferred-findings.md`, `phase-details/`.

The divergence is the point. If StrucGu's own paths matched the source
repository's, nothing would demonstrate that the obligations are about roles
rather than about LinkCtrl's filenames, and the first adopter with a
`CONTRIBUTING.md` playing the triage role would reasonably wonder whether they
were doing it wrong. Two instances with different names is the smallest possible
proof that the mapping layer is real.

The cost is that anyone reading both repositories has to hold two vocabularies.
Accepted; the mapping is one table.

### The commit gates and the sabotage rule are deliberately not extracted

LinkCtrl's `workflow.md` carries more than triage: a commit gate table, the
sabotage discipline, a whole-repository documentation pass, and standing rules.
All of it is good and none of it is in this release.

They are verification obligations rather than records obligations. Checking that
a passing test was actually sabotaged and restored is not something a check on
the shape of a record can see, and approximating it with a check that the rule is
*written down* produces a declaration with no paired behaviour check — decoration
by the rule two entries above.

They belong to a second module family. Recording the omission here so a later
reader can tell it was a choice rather than an oversight, and so the family has
somewhere to start from.

### A new check never ships in a minor version

Version bumps are defined by what happens to a repository that was clean
yesterday, not by how much source changed.

The rule that matters: adding a check is a major version. If a new check could
arrive in a minor, upstream could publish findings into every adopting
repository at will. That is enforcement by release — it produces exactly the
outcome the non-enforcement posture forbids, through a channel nobody would
think to close. Pins are exact for the same reason; a checker that accepts a
floating version hands upstream the same power back.

Each module changelog states, in a fixed sentence, what a previously clean
adopter will newly see. For a first release the answer is "nothing", and it is
written out rather than omitted, because an omitted sentence is indistinguishable
from a forgotten one.

### Objections are drafted by a tool and filed by a person

The feedback loop is the reason the catalog can improve: the repository using a
module in anger is the one positioned to find out it is wrong.

Automating the filing was rejected on a ground unrelated to taste. Audit output
from a private repository contains file paths, internal project names, and
quoted lines. A tool that posts that to a public tracker is an exfiltration
channel with a friendly name. So a checker may print a prefilled objection body;
a person posts it.

The required fields exist to keep an objection from being a preference. What the
audit reported verbatim, what this repository does instead, evidence the
alternative serves the obligation's *stated purpose*, and what complying would
cost. The last one is the filter — an objection with no cost is a preference,
and the four outcomes all turn on whether the cost is real.

---

## 2026-07-31 — building the catalog

### Six checks were cut for measuring presence rather than thought

The work record for the fixtures unit asks for this list and says it is worth
more than the list of checks that survived. It is, because each of these is a
check that would have looked useful in a summary and would have been satisfied by
a machine writing a word.

1. **A risks section is non-empty.** Satisfied by writing "Low." The check
   passes, the section then reads as considered, and the signal is destroyed
   permanently. What ships instead is `WU-02` and `WU-03`, which check the
   section exists at all, plus a judgment entry that looks at whether every
   record in the directory says "Low" — the *pattern* is observable where the
   individual instance is not.
2. **Done bullets are falsifiable.** No pattern separates "every handler returns
   a mapped error, asserted by the error-mapping test" from "error handling is
   correct". Moved to judgment.
3. **Evidence cells contain evidence.** Same shape. "This is broken" fills the
   column. `FQ-02` checks the column exists; whether anything in it could be
   checked by someone who does not trust you is judgment.
4. **Decision headings are claims rather than topics.** A heading either can or
   cannot be contradicted, and no regular expression sees the difference.
5. **The triage boundary is drawn by claim rather than by subsystem.** The most
   consequential rule in `triage-rule` and completely invisible to a check.
6. **A passing test was sabotaged and restored.** Not observable in the shape of
   any record, and the reason the whole verification family is deferred.

The pattern across all six: what makes them valuable is a judgment someone made,
and a record only ever carries the trace of a judgment, never the judgment.
Every one is now a `judgment` entry, which is why a mechanical run emits those
lines whether or not anyone is there to read them.
