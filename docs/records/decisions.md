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
| [The first check to fire, fired on this repository](#the-first-check-to-fire-fired-on-this-repository) | Evidence `TR-03` works |
| [Three specification gaps were found by use, not by review](#three-specification-gaps-were-found-by-use-not-by-review) | Spec changes during the build |
| [This repository records no deviation of its own](#this-repository-records-no-deviation-of-its-own) | Corrects part of the M7 work record |
| [The code-fence rule was wrong the first time](#the-code-fence-rule-was-wrong-the-first-time) | Corrects the entry above |
| [Fixture expectations become data, and the wording of a finding stays out of them](#fixture-expectations-become-data-and-the-wording-of-a-finding-stays-out-of-them) | `expected.yaml`, and the no-runner line |
| [The conformance criterion waits until an implementer has asked for it](#the-conformance-criterion-waits-until-an-implementer-has-asked-for-it) | Why M9 is deferred rather than cut |
| [The first checker is Whippy's, and its independence is partial](#the-first-checker-is-whippys-and-its-independence-is-partial) | What M10's evidence is worth |
| [The second repository is private, and it tests re-application rather than generality](#the-second-repository-is-private-and-it-tests-re-application-rather-than-generality) | What M11 does and does not answer |
| [The first checker's inputs exclude this repository's records](#the-first-checkers-inputs-exclude-this-repositorys-records) | Corrects M10's input rule |
| [The confidence field measures noticed ambiguity, and the lineage risk is unmeasured](#the-confidence-field-measures-noticed-ambiguity-and-the-lineage-risk-is-unmeasured) | Corrects the entry above it |
| [Separating the checker's repository does not stop it being the reference implementation](#separating-the-checkers-repository-does-not-stop-it-being-the-reference-implementation) | What M10 cannot claim |
| [A quota for objections manufactures the disagreement it counts](#a-quota-for-objections-manufactures-the-disagreement-it-counts) | Corrects M11's done-means |
| [Enumerating a private repository's record shapes was itself the leak](#enumerating-a-private-repositorys-record-shapes-was-itself-the-leak) | A redaction, and why it is not a correction |
| [The phase edits the specification, and hiding that in three work units was the drift](#the-phase-edits-the-specification-and-hiding-that-in-three-work-units-was-the-drift) | Corrects "Not in this phase" |
| [Judgment expectations are recorded once per module, not once per tree](#judgment-expectations-are-recorded-once-per-module-not-once-per-tree) | The shape of `expected.yaml`, and its schema identifier |
| [The modules bump to 0.2.0 and no adoption record moves with them](#the-modules-bump-to-020-and-no-adoption-record-moves-with-them) | Why a pin left behind is deliberate |
| [The first checker is DevOfPie/strucgu-check, and it is public](#the-first-checker-is-devofpiestrucgu-check-and-it-is-public) | Names M10's repository before M10 starts |
| [The fixtures were wrong about `DL-03`, and the specification stays as it is](#the-fixtures-were-wrong-about-dl-03-and-the-specification-stays-as-it-is) | Corrects five fixture expectations M6 shipped |
| [A check may carry more than one violating fixture tree](#a-check-may-carry-more-than-one-violating-fixture-tree) | The `fixtures/` shape rule, relaxed |
| [A transcription defect is repaired; the rule it exposed is left open](#a-transcription-defect-is-repaired-the-rule-it-exposed-is-left-open) | `WU-04`, and what a check reports while its halves disagree |
| [The ambiguity log is the investigation that outgrew a decision entry](#the-ambiguity-log-is-the-investigation-that-outgrew-a-decision-entry) | Why the `investigations` role is mapped now |
| [Four modules move a minor version and the fifth waits for a decision](#four-modules-move-a-minor-version-and-the-fifth-waits-for-a-decision) | Bumps for M10, and the one that is not the worker's to take |
| [Repairing a check's transcription is not adding a check](#repairing-a-checks-transcription-is-not-adding-a-check) | Answers the entry above, and bumps `work-units` |

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

### The first check to fire, fired on this repository

While walking the checks against StrucGu before writing its adoption record,
`TR-03` reported a finding: [triage.md](triage.md) named the findings queue
inside a fenced code block —

```
out of spec  → DO NOT FIX
               append one row to findings.md → "Open"
```

— rather than as a link. The word is there, so `TR-02` passes and every
word-matching check passes. Nothing resolves to the queue.

This is the LinkCtrl defect that motivated the entire repository, reproduced
independently, in the repository built to catch it, by the person who wrote the
check. That is worth recording precisely because it is embarrassing: the failure
mode is not carelessness, it is that a document naming its destination in prose
reads as correct to everyone who already knows where the destination is —
including its author, ten minutes after writing it.

Fixed by naming the queue as a link in the line beneath the block. The block
keeps the terse form; the link carries the reference.

It also sharpens [F2](findings.md): `role_referenced` catching this depended
entirely on the fix being a link. Had the sentence been reworded in prose, the
check would have gone quiet while the defect remained. The narrowness of that
coverage is now evidenced rather than theorised.

### Three specification gaps were found by use, not by review

Each was found by writing a module or running a check against real files, and
none by re-reading the specification. Recorded together because the pattern is
the point: the contract was designed in the abstract and was wrong in three
places on contact.

1. **A role's shape can depend on the form.** `decision_log` is a file under
   `single-log` and a directory under `per-decision-files`. The specification
   allowed one cardinality per role. Fixed with `cardinality: by_form`.
2. **`path_exists` on a directory must require contents.** An empty directory
   satisfies a filesystem existence test while satisfying nothing the obligation
   wanted. Found writing the `violates-IN-01` fixture, which was intended to
   demonstrate a missing record and instead demonstrated a passing check.
3. **`links_resolve` must skip fenced code blocks.** A module's own check
   patterns are written in fences, and `in[ -](spec|scope)` contains the exact
   byte sequence a naive link extractor matches on. Found by running the link
   check over this repository, which reported two findings against regular
   expressions.

The third is the one worth generalising: a check run only against fixtures its
author wrote will not find this class of defect, because the author does not
write the pathological input. The fixtures prove a check detects what it was
built to detect. Only a real corpus finds what it detects by accident.

### This repository records no deviation of its own

This corrects the work record for M7, which required one so that the deviation
shape would be tested by use rather than only specified. The requirement was
wrong and has been rewritten there.

No genuine deviation exists. Every check StrucGu adopts, it passes. The options
were to invent one, or to state the absence.

Inventing one would put a false claim in the single file whose entire purpose is
to be a truthful claim the repository makes about itself — to exercise a
mechanism, in a catalog whose posture is that records are for readers who do not
trust you. The mechanism stays untested by use until a real deviation arrives,
and that is the honest state.

Worth noting what this says about self-application generally, which is already
argued above: a repository that passes every check it publishes is not evidence
the checks work. It is the expected result of an author writing rules they
already satisfy. The fixtures are the evidence, and `TR-03` firing on this
repository is the only accidental evidence in the whole build.

### The code-fence rule was wrong the first time

This corrects item 3 of [Three specification gaps were found by use, not by
review](#three-specification-gaps-were-found-by-use-not-by-review) above. That
text stays as it is.

The rule as first written said `links_resolve` must skip **fenced code blocks**.
Implementing it and re-running the link check over this repository dropped the
false positives from four to two. The survivors were the same pattern written as
an *inline* code span — in the specification's own prose, and in the entry being
corrected. The rule now reads: code is not scanned, neither fences nor inline
spans.

The specification and the decision log both described the defect, and both were
instances of it. That is the sharpest available demonstration of the point the
original entry was making — a check run only against fixtures its author wrote
will not find this class of defect, because the author does not write the
pathological input — and it is why the entry it corrects is worth leaving in
place rather than quietly widening.

Final state: 0 broken of 185 relative links and anchors, repository-wide,
excluding the fixture trees, which contain broken links as test data.

---

## 2026-08-02 — planning the second phase

Four scope questions, put to the owner before any of [M8](work/m8.md) through
[M13](work/m13.md) began, because [triage.md](triage.md) requires stopping and
asking on scope rather than deciding it inside a unit. What came back, and what
it costs.

### Fixture expectations become data, and the wording of a finding stays out of them

Each module gains a `fixtures/expected.yaml` beside its `expected.md`, giving one
of the five audit states per tree per check id. The prose file stays and stays
normative on intent; the data file answers the only question an implementer
actually has, which is whether their run matched.

**Finding text is deliberately excluded.** An expectation file that pinned the
wording would make one implementation's phrasing normative — the thing [There is
no runner](#there-is-no-runner-and-that-is-the-largest-single-decision-here)
refused, arriving as a data format instead of as a program. What a finding must
carry, a location and evidence, is already specified; how it reads is the
implementer's.

Two costs, both accepted. The neutrality rule — nothing under `modules/` names a
language, package manager, build tool, or file extension — is under strain, and
the defence is that `module.yaml` already established that a data file naming
nothing is not an implementation. And this is the closest thing to shipping
software the no-runner decision permits: the next request after it will be for a
harness that reads it. Where that line falls is now discovered rather than
declared, which is the next entry.

### The conformance criterion waits until an implementer has asked for it

A document stating what passing the fixtures means was proposed for before the
first implementation and is deferred until after it. Not cut — deferred, so the
choice gets made against evidence.

The reasoning: a criterion drafted now answers questions nobody has asked. There
are zero implementations, so every clause would be anticipation, and anticipated
clauses are where a conformance document quietly becomes a certification
document. Drafted after [M10](work/m10.md), every clause can be traced to a
question an implementer actually hit.

The cost is real and is recorded in [M8](work/m8.md) rather than in the deferred
unit: between shipping a machine-readable expectation file and having a stated
criterion, nothing written down guards the line against a harness. Holding it is
the owner's judgment in that window. The second cost is that the first
implementation now defines the criterion by example, which is a reference
implementation arriving through the back door — the clause-origin rule in
[M9](work/m9.md) is the counter-pressure and may not be enough.

### The first checker is Whippy's, and its independence is partial

Phase one was written by the owner with an Opus 5 instance co-authoring. The
first checker is written by a different Opus 5 instance, in a fresh session,
from the published repository only, under a rule that the author does not answer
questions about what a check means.

That is a different session and a different reader. **It is not a different
lineage,** and the failure mode has no signature in the output: a reader from the
same model family may reconstruct the co-author's reading of an ambiguous check
without noticing there was a fork, and the result looks exactly like a
specification that was simply clear.

The only instrument against it is recording each ambiguity *before* resolving it,
with the readings available and how confident the choice was. An ambiguity
resolved correctly at low confidence is a coin-flip that landed, and counting
those separately is the difference between "the spec was precise" and "two
instances of one model guessed alike". [M6](work/m6.md) named the first
independent checker as the real test; this is a weaker instrument than that, it
is what is available, and calling it what it is costs nothing.

The alternative considered and rejected was the owner writing it — fastest, and
producing close to no evidence, since an author implementing their own
specification tests it against the understanding already encoded in it.

### The second repository is private, and it tests re-application rather than generality

A second repository was chosen and adopts in [M11](work/m11.md). It is private,
and **it is not named in this repository.** The owner's own records name it; this
one does not, because a public repository is not where a private one's shape gets
published as a side effect of planning. That is the same rule
[objections.md](../objections.md) states about audit output carrying paths,
internal names, and quoted lines, applied to the plan that will produce that
output rather than only to the output.

The cost of withholding it is real: a reader here cannot check the claims below
about what that repository contains, and has to take them. Stating that is worth
more than the alternative, which is a plan that reads as though its evidence were
open.

It is not the repository this catalog was extracted from, and its own decision
log already names StrucGu as the intended canonical home for its process rules,
recording those rules as provisional and written to be lifted out later. The
audit is therefore the first step of a migration that repository has already
chosen, rather than an exercise staged to produce a result.

**It shares a convention lineage with LinkCtrl, and that caps what it can
prove.** It imported LinkCtrl's three-file split, its terse process file, and its
deferred-findings discipline, deliberately and on the record. LinkCtrl is where
these modules came from. So a clean map is the *expected* outcome and is not
evidence that these conventions generalise — it is evidence that an extraction
survives re-application within the lineage it was extracted from. That is worth
knowing and it is a different claim, and [M13](work/m13.md) is forbidden from
reporting the one as the other.

The generality question needs a repository built by someone who has never read
LinkCtrl. Nothing in this phase answers it, and the alternative — deferring the
second adoption until an outside adopter appears — was rejected because it has no
done condition the owner controls and would defer the whole phase's conclusion
indefinitely.

The more valuable half of that unit's output is therefore not findings against
the second repository but the record shapes it has that this catalog has no role
for. Each is either out of scope for a catalog about records of work, or a
module this catalog is missing. Both answers go in [findings.md](findings.md) as
rows, and neither becomes a module in this phase.

> Redacted 2026-08-03. This paragraph enumerated four of those shapes. The
> enumeration is removed rather than corrected by a later entry, because a
> correction that leaves the text in place would keep publishing the thing the
> entry above it forbids publishing. The redaction is recorded here and argued
> below; nothing else in this entry changed.

---

## 2026-08-03 — an adversarial review of the plan, and what it corrected

The plan above was reviewed adversarially before any unit started. Fourteen
findings; the verdict was that it was not executable as written. The entries
below correct entries in the section above rather than editing them — that is
what this file is for, and it is the first time the mechanism has been used on a
real disagreement.

Two classes of correction are not given their own entries. Several arguments had
been written out in full in two or three places at once — the work records now
carry pointers and the reasoning lives here, which is the split
[work/README.md](work/README.md) already states and which the `work-units`
module names as an obligation. And several done-means bullets that could be
satisfied by asserting them are now labelled attested-not-verifiable rather than
sitting among falsifiable ones.

### The first checker's inputs exclude this repository's records

This corrects [The first checker is Whippy's, and its independence is
partial](#the-first-checker-is-whippys-and-its-independence-is-partial), which
set the implementer's inputs to the published repository and left it there.

The published repository contains the plan that grades the implementer. It says
an empty ambiguity list will be read as the independence rule leaking, a thin
one as suspicious, and low-confidence resolutions as counted separately. An
implementer who reads that has been handed the scoring function before starting,
and will produce the shape it rewards — a healthy list with mixed confidence —
with nothing in the plan able to tell manufactured ambiguity from found
ambiguity. The earlier text worried only about the list being too thin. The
published rubric biases it the other way.

Inputs are now the normative surface only: the specification, the modules, and
the three consumer-facing documents. `docs/records/` is excluded. The observer's
notebook does not go to the subject.

### The confidence field measures noticed ambiguity, and the lineage risk is unmeasured

This corrects the same entry, which called the confidence field "the only
instrument against" the shared-lineage risk immediately after stating that the
risk "has no signature in the output". Both cannot be true.

A same-lineage reader who reconstructs the co-author's reading without noticing
there was a fork reports *no ambiguity, high confidence* — which the instrument
files under "the specification was clear". Confidence bounds the ambiguity the
implementer noticed and nothing else. It catches coin-flips; it cannot catch the
fork nobody saw.

The honest position: the shared-lineage risk is **unmeasured in this phase** and
is discharged only by a later implementation from a different lineage. The
confidence field stays, because noticed ambiguity is worth counting, and it is
no longer offered as a defence against the risk it cannot see.

### Separating the checker's repository does not stop it being the reference implementation

This corrects the same entry and sharpens [The conformance criterion
waits](#the-conformance-criterion-waits-until-an-implementer-has-asked-for-it),
which already admitted the back door and then let the next unit claim it was
closed.

Location was never the operative variable. A checker commissioned by the
catalog's owner, written by the owner's agent, named in the catalog's records
before it exists, the only implementation in existence, and the thing any
eventual criterion gets derived from **is** the reference implementation
wherever it lives. Putting it in another repository buys one thing —
discoverability by adjacency — and the record now says that instead of implying
the problem is solved. Whether that repository is public is recorded with its
name, because a public first mover is a stronger de facto reference than a
private one.

### A quota for objections manufactures the disagreement it counts

This corrects [The second repository is private](#the-second-repository-is-private-and-it-tests-re-application-rather-than-generality),
whose unit required that at least one objection be filed or the absence recorded
as a finding.

Two defects. The escape arm was satisfiable by writing a sentence, which is the
shape this repository's own cut criterion exists to remove. And the requirement
itself was justified by an inverted inference: the unit argued that a shared
convention lineage raises the odds of an honestly clean run *and therefore*
makes a clean run more suspicious. It makes it **less** informative. If honesty
and looking-away predict the same observation, the observation distinguishes
nothing, and the correct response is to weight the evidence down rather than to
require a disagreement be produced.

With one person as objector, audited owner, checker commissioner, and module
author, a required objection would have been scripted by the plan that measures
it — and [objections.md](../objections.md) makes cost the filter, so an objection
filed to satisfy a done bullet has manufactured cost by construction. The quota
is gone. What remains is the disposal rule: every finding fixed, waived in
writing, or objected. That forces the channel exactly when a real disagreement
exists and never otherwise.

### Enumerating a private repository's record shapes was itself the leak

The entry that established not naming the second repository went on to list four
of its record shapes, and the unit repeated the list. Naming what a repository
keeps records of describes it about as well as naming it does, so the rule was
being stated and broken in the same breath.

The enumeration is removed from both places — a redaction rather than a
correction, marked where it was. Append-only exists so a belief that was held is
not erased; it does not oblige this repository to keep publishing a third
party's shape while arguing that it should not. What survives is what
[M11](work/m11.md) needs: where that repository keeps something this catalog has
no role for, the gap is recorded in the catalog's own vocabulary, as a row that
names the missing module rather than the repository's structure.

The review that found this also held that the surviving disclosures narrow the
field to roughly one repository. For a reader who can see the owner's private
repositories, yes. For an outside reader, who can enumerate the public ones and
not the private ones, "some private repository of this owner's" is not an
identification. The redaction stands on the first argument, not the second.

### The phase edits the specification, and hiding that in three work units was the drift

This corrects the "Not in this phase" list, which named no specification changes
while three units forced them.

[M8](work/m8.md) falsifies two sentences in the module contract the moment it
lands: a module directory contains *exactly* the listed files, and `fixtures/`
is a `satisfies/` tree, one `violates-<CHECK-ID>/` tree per check, and
`expected.md`. Its schema identifier also has to be defined where the other two
are, or it is a pin to nothing. [M10](work/m10.md) produces an unbounded number
of fixture and obligation edits, one per ambiguity resolved that way.
[M12](work/m12.md) adds either a fixture tree in a third shape or a check kind.

A section that lists exclusions and omits the largest inclusion is worse than no
section — it reads as a boundary while being a decoration. The edits are now
listed as scope.

**One further defect, corrected in the unit rather than here:** the expectation
file was keyed by check id alone, which cannot express judgment entries, since
those carry their own ids. The first checker's only conformance test would have
been silent on the one output channel that keeps a mechanical run from looking
complete.

---

## 2026-08-03 — M8, fixture expectations become data

### Judgment expectations are recorded once per module, not once per tree

`fixtures/expected.yaml` carries two sections. `checks` is keyed by fixture tree
and then by check id, because a check's result is exactly what varies from one
tree to the next. `judgment` is keyed by entry id alone, with no tree above it.

The asymmetry is the point. [SPEC.md](../../SPEC.md) requires one `judgment`
line per entry whether or not anyone is available to judge it, so the value is
`judgment` on every tree — including the trees where the role is absent and
every check reports `skip`. Keying it per tree would produce 33 copies of an
invariant and invite a reader to hunt for the tree where it differs. There is
none, and that absence is the property worth recording.

The identifier is `strucgu/expected@1`, and it is defined in
[SPEC.md](../../SPEC.md) beside `strucgu/module@1` and `strucgu/adoption@1`
rather than only used inside a fixture directory. An identifier defined nowhere
is a pin to nothing.

### The modules bump to 0.2.0 and no adoption record moves with them

Adding `expected.yaml` is a minor bump under [SPEC.md](../../SPEC.md)
"Versioning": a previously clean adopter newly sees nothing, because nothing
inside `fixtures/` is ever read against an adopting repository. All five modules
gain the file, so all five move on the same day.

Every `version:` pin stays at `0.1.0` — in the 33 fixture adoption records, and
in [this repository's own](../../strucgu.yaml). A pin is a dated claim about
what was reviewed and adopted, not a field kept current. The
[self-walk](self-walk.md) was performed against `0.1.0` on 2026-07-31, and
moving the pin would assert a review that did not happen. A checker reading a
`0.2.0` module against a `0.1.0` pin prints one line saying so, which is the
propagation mechanism working rather than a defect.

This is recorded because the gap reads as an oversight. Anyone tidying it away
is undoing a decision, not fixing a slip.

---

## 2026-08-03 — naming M10's repository, before M10 starts

*No work unit was under way. This entry answers a precondition
[M10](work/m10.md) states for itself, and is written before the unit is
started rather than inside it.*

### The first checker is DevOfPie/strucgu-check, and it is public

[M10](work/m10.md) requires its repository "named before the unit starts, and
whether that repository is public is recorded with the name". The name is
`DevOfPie/strucgu-check` and it is public. It does not exist yet; naming it is
what M10 asked for, not creating it.

**Public**, because M10 already says this will be the only implementation in
existence and that the second implementer will find it and read it. A private
reference implementation costs the discoverability that separating the
repository was meant to preserve, and buys only room to get the ambiguity log
wrong unobserved — which is the log whose whole value is that it was written
before the resolutions were.

**Under `DevOfPie` rather than the implementer's own account**, which is the
option that costs the most and was chosen anyway. M10's bullet on separation is
careful: location was never the operative variable, primacy is, and separating
the repository "buys discoverability-by-adjacency and nothing more". Putting it
in the catalog owner's organisation spends even that. An implementation sitting
beside the catalog reads as the reference implementation by adjacency, and the
record's answer is not to deny it — the bullet already refuses to claim the
problem away — but to stop pretending the org boundary was ever doing work the
separate repository was not. The alternative was an account boundary that looks
like independence while the commissioning, the naming, and the primacy all stay
exactly where they were.

What this does *not* buy is any part of the independence M10 is actually after.
That is bought by the input restriction — the normative surface only,
`docs/records/` excluded, this file included — and by nothing about where the
repository sits.

### The orchestrator that landed M8 is disqualified from implementing M10

M10 excludes `docs/records/` from the implementer's inputs, "this file
included", because an implementer who has read the scoring function produces the
shape it rewards. The session that validated and accepted [M8](work/m8.md) has
read this log, [self-walk.md](self-walk.md), [findings.md](findings.md) and
[m10.md](work/m10.md) itself. It cannot brief an implementer without leaking
exactly what the exclusion exists to prevent, so it does not: M10 opens in a
fresh session whose first read is the published repository.

The cost is a session boundary and the re-derivation of context that already
existed, and that cost is the point rather than a side effect. The cheaper path
— briefing a worker from this session — was rejected because its failure would
be invisible. M10 says so in its own risks: a checker built with help still
passes the fixtures, so the output of the compromised run and the honest one
look identical, and only the ambiguity log would have differed.

This is recorded rather than left in conversation because the rule it applies is
attested and not verifiable. A kept restriction and a broken one leave the same
trace in the checker, so the trace has to be here instead.

---

## 2026-08-03 — M10, the first checker and what it could not determine

*The checker itself is [DevOfPie/strucgu-check](https://github.com/DevOfPie/strucgu-check),
built in a separate session under the input restriction this log records above.
Its 18 ambiguity records and the write-up drawn from them are filed here as
[investigations/0001](investigations/0001-what-the-specification-does-not-determine.md).
These entries are the catalog's answers to what that log found, and only the
answers that are not obvious from the diff.*

### The fixtures were wrong about `DL-03`, and the specification stays as it is

The checker's [A03](https://github.com/DevOfPie/strucgu-check/blob/main/ambiguities/A03-history-deletions-with-no-history.md)
found the sharpest contradiction in the catalog. Five `decision-log` fixture
trees — `satisfies`, `violates-DL-02`, `violates-DL-04`, `violates-DL-05`,
`violates-DL-06` — expected `DL-03: ok`. None of them is a git repository, so a
checker running `DL-03` there reads no history at all. [SPEC.md](../../SPEC.md)
and [auditing.md](../auditing.md) say four times between them that folding `skip`
into `ok` is the failure that matters most, because it converts "I did not look"
into "I looked and it was fine". The fixtures required exactly that fold, and
`expected.yaml` is the file an implementer is told to compare against.

The implementer took the fixtures, because reproducing them was the brief, and
recorded that they believed the prose had the better of it. They were right. The
five rows are corrected to `DL-03: skip` and the specification is not touched.

The choice is worth recording because the cheaper repair was available and was
proposed: one sentence in `SPEC.md`'s `history_deletions` row saying that a
target with no readable history reports `ok`. That sentence would have made
every tree pass and would have made `DL-03` report `ok` on every repository that
has never committed, every shallow clone, every export and every extracted
tarball — indistinguishably from a repository whose log has genuinely never been
edited. `DL-03` is the only behaviour check behind `decision-log-append-only`,
and `DL-04`, the declaration check, names `DL-03` as the thing that tests whether
its declaration is true. A `DL-03` that passes without looking makes `DL-04`
decoration, and [SPEC.md](../../SPEC.md) says decoration should be cut.

**What this admits.** The fixtures shipped in [M6](work/m6.md) and were reviewed
in [M8](work/m8.md) when they became data, and the contradiction survived both.
Neither pass caught it because both were performed by the party that wrote the
rule it violates. It took an implementation to find, which is what
[M10](work/m10.md) was for and is the first concrete return on it.

**What is deliberately not written down.** `SPEC.md` still does not say, in the
`history_deletions` row, what the check reports when there is no history. The
general rule already covers it — a check whose target cannot be read reports
`skip` — and the five fixtures now pin it. Adding a special case for one check to
restate a rule that already applies is how a specification acquires the
redundancy that later drifts.

### A check may carry more than one violating fixture tree

`fixtures/` used to be specified as "one `violates-<CHECK-ID>/` tree per check",
in a table introduced as listing exactly what each row names. It is now "at least
one", with further trees permitted as `violates-<CHECK-ID>-<suffix>/`.

The constraint had a consequence nobody had needed until an implementation
existed: **a check with more than one boundary worth pinning could not have them
pinned.** One tree demonstrates one way for a check to fail, and three of the
rules this catalog argues hardest for need a tree in which the check *passes* and
a wrong implementation reports a finding. `satisfies/` cannot hold them either,
because it has to satisfy everything at once and these need contradictory
content.

This was taken because the alternative was measured rather than imagined. The
checker's
[mutation harness](https://github.com/DevOfPie/strucgu-check/blob/main/conformance/mutations.py)
breaks it nine ways, one stated rule at a time, and re-runs every tree. Against
the catalog as it stood, five breakages went unnoticed — a suite reporting a
clean run from a checker that is measurably wrong — and two of the five were the
matching rules `SPEC.md` gives their own paragraphs and a
learned-the-hard-way provenance: code is not scanned for links, and runs of
spaces are not collapsed when slugging an anchor. Both were written as warnings.
Neither had a tree behind it. With the trees this relaxation allows, no breakage
goes unnoticed.

That correlation is the finding, not the fixtures: **a rule a specification
bothers to argue for is a rule it learned by being wrong, and those are exactly
the ones that were argued instead of demonstrated.**

The naming convention is left alone deliberately. A tree called
`violates-<CHECK-ID>` asserts that the tree violates that check, and the trees
added here are the opposite — a correct checker reports nothing. The implementer
proposed and then declined a `pins-<CHECK-ID>-<what>/` category on the grounds
that settling a naming convention by whatever an implementer happened to call a
directory is how an implementation's accidents become a specification. That is
right, and the better name is a decision for whoever needs the third tree.

### A transcription defect is repaired; the rule it exposed is left open

`modules/work-units/module.md` carried `WU-04`'s pattern as
`&lt;[A-Za-z][A-Za-z ]*&gt;` where [module.yaml](../../modules/work-units/module.yaml)
carries `<[A-Za-z][A-Za-z ]*>`. The escaped form matches a literal `&lt;`, and
cannot match `<title>` — which is what `violates-WU-04` exists to be caught by.
The two halves render identically on GitHub, which is why it survived from M3 to
here; it was found with `od -c`.

The prose half is repaired. That is forced: the module's own
[CHANGELOG](../../modules/work-units/CHANGELOG.md) and
[README](../../modules/work-units/README.md) have told adopters since 0.1.0 that
`WU-04` matches any angle-bracketed literal, so the escaped pattern was never the
shipped contract — it was a corrupted rendering of it.

The general rule the implementer proposed alongside is **not** taken. It would
have `SPEC.md` say what state a check reports while its two halves disagree:
evaluate under `module.md`, emit the disagreement, and report `skip` where
`module.md`'s form cannot be evaluated at all. It is a real hole — "report it, do
not pick" currently leaves a check with no state to be in, and a check must
report one of five — but the wording changes what `WU-04` reports on
`violates-WU-04` from `finding` to `skip`, which changes an expectation, which is
not a wording fix. It stays open rather than being decided inside a unit that was
not scoped for it.

### The ambiguity log is the investigation that outgrew a decision entry

[strucgu.yaml](../../strucgu.yaml) maps `investigations` at
`docs/records/investigations/`. It was `~` from 0.1.0 until now, and
[M10](work/m10.md) required that it stop being `~` **because a real
investigation exists, not because one was invented to exercise the checks.**

It qualifies on the module's own test: eighteen ambiguity records, a mutation
experiment with nine deliberate bugs, and two counts that only mean anything
stated together — 33 trees at 305 rows with five breakages unnoticed, against 36
trees at 337 rows with none. None of that fits in an entry here, and squeezing it
in would leave the conclusion with nothing a later reader can re-examine, which is
the failure the `investigations` module exists to name.

**What it costs.** The four `IN-*` checks were the only exercise the `skip` path
and the conditional obligation got anywhere in this repository, and
[self-walk.md](self-walk.md) describes them as the point of that walk. They now
report `ok`. The repository has lost its only live demonstration that an unmapped
role produces `skip` rather than `ok` — the single behaviour it insists on most
loudly. That is a real loss and it is [M13](work/m13.md)'s to record; the
[self-walk](self-walk.md) is a dated artifact of 0.1.0 and is left as it was
rather than rewritten to match a later state.

### Four modules move a minor version and the fifth waits for a decision

`decision-log`, `findings-queue` and `triage-rule` move to `0.3.0`;
`investigations` moves to `0.2.1`. None of the three checks or obligations
changed in any of them, and no adopter newly sees a finding. The bumps are for
fixture content that pins a boundary the fixtures did not pin before, which is
the same reading [M8](work/m8.md) took when `expected.yaml` was added — a
substantive change that a clean adopter never sees is a minor, and wording alone
is a patch. `investigations` gets a patch because the only thing that changed is
a paragraph in its `module.md` describing this repository's own adoption, which
stopped being true when the role was mapped.

`work-units` is not bumped here. Its version and its changelog entry are held
open on a question that went to the owner unanswered. Repairing
`WU-04`'s escaped pattern is either a patch — the shipped contract was always the
unescaped one and the file is being brought to it — or a major, because a checker
that followed the normative half literally reported nothing for that check and
now reports findings against records that were clean. The inherited rule is
absolute in one direction: a check added to a shipped module is a major version,
never a minor. Whether repairing an inert one counts as adding it is not a
question a worker should answer by picking, and in `0.x` a major has a second
unsettled meaning — nothing here says whether it means `1.0.0` or collapses into
the minor digit, and `1.0.0` would assert a stability
[README.md](../../README.md) explicitly disclaims.

### Repairing a check's transcription is not adding a check

`work-units` moves to `0.2.1`. A **patch**, for a change that makes `WU-04` fire
where it did not fire before.

That sentence looks like the versioning rule being bent, which is why this entry
exists. [SPEC.md](../../SPEC.md) defines a bump by what a previously clean
adopter will newly see, and the rule every unit inherits is absolute in one
direction: **a check added to a shipped module is a major version, never a
minor.** A checker that read the normative half of `work-units` literally
reported `WU-04: ok` on records holding `<title>` and will now report findings on
them. Under a mechanical reading of the bump rule that is a major.

**The shipped contract never moved; only its transcription did.** That is the
argument, and it is checkable rather than a matter of taste. `WU-04` shipped in
`0.1.0` with a violating fixture built to be caught by the unescaped pattern.
`modules/work-units/fixtures/expected.yaml` has said `violates-WU-04` produces
`WU-04: finding` since [M8](work/m8.md) made expectations data — third-party
evidence, written before anyone knew the halves disagreed, of which pattern was
meant. [module.yaml](../../modules/work-units/module.yaml) has carried the
unescaped form since [M3](work/m3.md). And the module's own
[README](../../modules/work-units/README.md) and `0.1.0`
[changelog](../../modules/work-units/CHANGELOG.md) both told adopters from the
first release that `WU-04` "has the highest false-positive rate in the catalog —
any angle-bracketed literal in a record matches its placeholder pattern", which
describes the unescaped pattern and no other, and recommend turning the check off
rather than rewording records around it.

Four independent artifacts describe one check. One of them — the prose — went
through a markdown-escaping step at some point between being written and being
committed, and came out matching a literal `&lt;`. Nothing decided that; it
happened. A version bump announces a change in what this repository asks of an
adopter, and this repository has asked the same thing since `0.1.0`.

**The counter-argument is real and this entry does not dispose of it.**
[SPEC.md](../../SPEC.md) calls `module.md` normative and says so in the same
paragraph that tells a checker `module.md` wins. An implementer who followed that
instruction was doing exactly what they were told, and their adopters see new
findings arrive under a patch bump — which is enforcement-by-release through
precisely the channel
[a new check never ships in a minor version](#a-new-check-never-ships-in-a-minor-version)
was written to close. That cost is not argued away. It is accepted, on the
grounds that the alternative — a major version for a typo — buys the surprised
adopter nothing they cannot get from the `0.1.0` changelog they already have,
and spends the catalog's only major bump on a defect rather than a decision.
Anyone it surprises has a genuine objection and
[objections.md](../objections.md) is where it goes.

**What would make this reasoning wrong.** If the two halves had stated
*materially different* obligations rather than the same one twice, `module.md`
would win on the merits and changing it would be a real change to what the module
asks. The test is whether the disagreement is about intent or about
transcription, and it is not always as easy to answer as it was here — four
corroborating artifacts is a luxury. Where it cannot be answered, the answer is
major.

**What is deliberately left undecided.** Whether a MAJOR bump below `1.0.0` means
`1.0.0` or collapses into the minor digit. Nothing in this repository says, and
this entry did not need to know: the bump is a patch. Deciding the general rule
off the one instance that did not require it is how a convention gets fixed by
whatever the first case happened to be, which is the same failure the
[fixture naming](#a-check-may-carry-more-than-one-violating-fixture-tree)
discussion above declined to commit. It stays open until something actually needs
a major.
