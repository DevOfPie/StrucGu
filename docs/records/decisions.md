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
| [Declining a module is a stronger answer than mapping its roles to nothing](#declining-a-module-is-a-stronger-answer-than-mapping-its-roles-to-nothing) | Corrects what `adopting.md` recommends |
| [The second repository's intake file is its findings queue, and mapping it elsewhere would have hidden the answer](#the-second-repositorys-intake-file-is-its-findings-queue-and-mapping-it-elsewhere-would-have-hidden-the-answer) | The mapping M11 turns on |
| [An objection was filed rather than a deviation recorded, because a waiver claims a reason that is not settled](#an-objection-was-filed-rather-than-a-deviation-recorded-because-a-waiver-claims-a-reason-that-is-not-settled) | The objection channel's first real use |
| [The catalog cannot reach a scope contract unless a repository has units of work](#the-catalog-cannot-reach-a-scope-contract-unless-a-repository-has-units-of-work) | M11's more valuable half |
| [A redacted audit is weaker evidence than an open one, and the release gate is deviated from knowingly](#a-redacted-audit-is-weaker-evidence-than-an-open-one-and-the-release-gate-is-deviated-from-knowingly) | What the walk record is worth |
| [The first objection is declined, and what that costs the channel is not argued away](#the-first-objection-is-declined-and-what-that-costs-the-channel-is-not-argued-away) | Disposes of M11's objection, and what a decline teaches |
| [The base set argument is normative in SPEC.md, and the README links to it](#the-base-set-argument-is-normative-in-specmd-and-the-readme-links-to-it) | Closes `F1` |
| [The obligation is narrowed to what the check can see, rather than the check widened to prose](#the-obligation-is-narrowed-to-what-the-check-can-see-rather-than-the-check-widened-to-prose) | Closes `F2`, and what the rejected option would have cost |
| [A passing fixture tree that `satisfies/` cannot hold is named `satisfies-<suffix>/`](#a-passing-fixture-tree-that-satisfies-cannot-hold-is-named-satisfies-suffix) | Answers the naming question A17 left open |
| [Conformance is measured against `expected.yaml`, and reproducing it is not evidence of correctness](#conformance-is-measured-against-expectedyaml-and-reproducing-it-is-not-evidence-of-correctness) | What the criterion measures, and what it proves |
| [The register a prospective adopter wants is the register a standards body keeps](#the-register-a-prospective-adopter-wants-is-the-register-a-standards-body-keeps) | Why `F14`'s gap stays open, and what that costs |
| [The only implementation in existence does not conform to `decision-log` 0.3.0](#the-only-implementation-in-existence-does-not-conform-to-decision-log-030) | Stale rather than false, on a live instance |
| [Two clauses were cut for having no origin, and a third for being an expiry](#two-clauses-were-cut-for-having-no-origin-and-a-third-for-being-an-expiry) | What M9's clause-origin rule removed |
| [The two versioning rules measure different readers, and the conflict is reported rather than picked](#the-two-versioning-rules-measure-different-readers-and-the-conflict-is-reported-rather-than-picked) | Reports a conflict between SPEC.md and CHANGELOG.md, and which governs which version |
| [Below 1.0.0, a breaking change collapses into the minor digit](#below-100-a-breaking-change-collapses-into-the-minor-digit) | Closes `F7`, and sizes this release |
| [The second walk exercises `skip` nowhere, and that is a loss rather than a cleaner summary](#the-second-walk-exercises-skip-nowhere-and-that-is-a-loss-rather-than-a-cleaner-summary) | What mapping `investigations` cost the self-walk |
| [Two data points adjacent to the author are not a track record](#two-data-points-adjacent-to-the-author-are-not-a-track-record) | What the rewritten 0.x section may and may not claim |
| [A shipped unit whose claim is false is reopened, not succeeded](#a-shipped-unit-whose-claim-is-false-is-reopened-not-succeeded) | The fourth status word, and why a successor is the worse record |
| [No row leaves a tracker without saying where it went](#no-row-leaves-a-tracker-without-saying-where-it-went) | Extends findings.md's own rule to the other trackers |
| [A decision reached in conversation is written down before it is acted on](#a-decision-reached-in-conversation-is-written-down-before-it-is-acted-on) | Ordering, not volume |
| [A prompt without costs is a request for permission, not a decision](#a-prompt-without-costs-is-a-request-for-permission-not-a-decision) | What a decision prompt has to contain |
| [A documentation claim this repository has just falsified fails the commit, not the release walk](#a-documentation-claim-this-repository-has-just-falsified-fails-the-commit-not-the-release-walk) | The new commit gate row, and the finding that argues it |
| [Eight record files with no index is the failure this catalog is about](#eight-record-files-with-no-index-is-the-failure-this-catalog-is-about) | Why `docs/records/` gets a map, and why it does not close `F9` |
| [One tracker is watched for silent removal, and it is watched by the check that cannot judge](#one-tracker-is-watched-for-silent-removal-and-it-is-watched-by-the-check-that-cannot-judge) | Corrects the entry above it — `DL-03` sees deletions, and no process rule here is checkable |
| [Phase three measures before it grows, and the housekeeping goes first](#phase-three-measures-before-it-grows-and-the-housekeeping-goes-first) | Why measurement beat growth and evidence, and the one hard ordering constraint |
| [What the phase does to the queue, stated because approval is per row](#what-the-phase-does-to-the-queue-stated-because-approval-is-per-row) | Which nine findings the plan schedules, and why the other seven stay open |
| [The cheap corrections go last, because the phase moves the records they correct](#the-cheap-corrections-go-last-because-the-phase-moves-the-records-they-correct) | Corrects the ordering above it — three of five corrections would be done twice |
| [A phase that changes the contract and does not publish a release is not finished](#a-phase-that-changes-the-contract-and-does-not-publish-a-release-is-not-finished) | Why M20 exists, and why M21 needs it |
| [LinkCtrl adopting proves nothing about generality, and is worth doing anyway](#linkctrl-adopting-proves-nothing-about-generality-and-is-worth-doing-anyway) | What the third adoption is not, and the three things it is |

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

---

## 2026-08-03 — M11, the second repository adopts

### Declining a module is a stronger answer than mapping its roles to nothing

The second repository adopted the three base modules and declined both optional
ones outright, rather than adopting them with `~` roles. [adopting.md](../adopting.md)
recommends the second shape — "leave roles unmapped rather than inventing files"
— and it is the wrong recommendation for a repository the module does not apply
to at all.

An adoption is a claim that a module applies. A module adopted with every role
unmapped makes that claim and then reports `skip` on every check, which reads as
*applies, not got round to it yet*. Declining says *does not apply*, which is
what was true in both cases: one module asks for records of work that comes in
units, and that repository's records of intent describe work nobody has committed
to; the other asks for an investigation that outgrew a decision entry, and that
repository states the opposite position deliberately in its own scope contract.
[SPEC.md](../../SPEC.md) already supports this — adoption is "voluntary,
revocable, never inferred" and a partial adoption reports nothing — so nothing
changes except which shape gets recommended for which case.

`~` is still right where a module applies and a role is genuinely absent. The
distinction is whether the module's `applies_when` is met, and that is exactly
the question `applies_when` and `not_for` exist to make a person answer at
adoption time.

**What this costs.** The run produced no `skip` at all, in either module or
anywhere else. Combined with this repository's own record — which lost its last
`skip` in [M10](work/m10.md) — the catalog's most important escape hatch now has
no live demonstration in any committed output. [M13](work/m13.md) reports that.

### The second repository's intake file is its findings queue, and mapping it elsewhere would have hidden the answer

That repository's process document sends anything out of scope of the work in
flight to one file. That file is therefore its findings destination, and
`findings` was mapped to it — which produced three findings on the first run,
two of which are still standing.

The alternative was to leave `findings` unmapped on the grounds that the file
holds a different kind of thing from the one `findings-queue` was extracted
around. That would have reported `skip` for six checks and `skip` for `TR-03`,
and a `skip` means *I could not tell*. It was tellable. Choosing the mapping that
produces no findings, over the mapping that matches what the repository's own
rule says, is the failure [work/m11.md](work/m11.md) names in its Risks section —
an audit performed to pass — and it would have been invisible in the output,
because a clean run and a run that looked away are the same document.

The counter-argument is real and is recorded rather than answered: if the mapping
is wrong, the two standing findings are artifacts of the mapping and not
information about anything. The objection below is the mechanism that settles
which, and it carries the counter-argument in its own body.

### An objection was filed rather than a deviation recorded, because a waiver claims a reason that is not settled

Two checks report findings against that repository's queue: it has no evidence
column and no review-state column. Both were left standing.

[work/m11.md](work/m11.md) permits three disposals — fixed, waived with a reason
in that repository's own adoption record, or filed as an objection. A waiver was
available and was not taken. A deviation reports the check as `waived` with its
reason echoed every run, and the reason on offer is that the obligations are
wrong about queues of this shape — which is not a deviation's kind of reason. A
deviation says *this is genuinely local to us*. This claim is that a module
assumes a queue whose rows persist, and that a queue whose rows are consumed by a
mandatory triage step serves both obligations' purposes by a mechanism no check
can see. That is an argument about the module, and [objections.md](../objections.md)
is where an argument about the module goes.

**No quota produced this.** [A quota for objections manufactures the
disagreement it counts](#a-quota-for-objections-manufactures-the-disagreement-it-counts)
removed the requirement that one be filed, and the cost field is what filtered
this one: complying puts a decision back into a capture step that repository's
first principle requires to cost nothing, and duplicates a state that already
lives in the record its triage produces. Had the cost been "we would rather not",
the answer would have been a deviation and this entry would not exist.

**Its outcome is not this unit's to take.** Three of the four outcomes in
[objections.md](../objections.md) change a shipped module's version, and all four
are the owner's. The objection stands undisposed, both checks report `finding`
every run until it is disposed of, and that is the honest state rather than a
gap in the record.

### The catalog cannot reach a scope contract unless a repository has units of work

The more valuable half of this unit was never the findings. It is the record
shapes that repository keeps which this catalog has no role for, and four are
recorded in [findings.md](findings.md) as `F9` through `F12` — two of them a
module this catalog is missing, two of them out of scope, each answered in the
catalog's own vocabulary rather than by describing that repository.

`F9` is the one worth naming here. The audit could reach that repository's
process document, its rationale and its deferral destination, and could not reach
its scope contract at all — the document stating what is true and what is in
scope for the project. The only role that comes near it is `work-units`'
`unit_index`, which binds the scope contract to a repository having units of
work. That repository has none, declined the module, and its most load-bearing
record is invisible to every check in the catalog.

This repository could not have found that by looking at itself.
[work/README.md](work/README.md) is both its scope contract and its unit index,
so the coupling has never cost it anything, and a self-walk cannot see a coupling
it satisfies by coincidence. That is what a second adopter is for, and it is a
better argument for the whole exercise than the check results are.

**Nothing becomes a module in this phase.** `F9` and `F10` are rows, and closing
either is a major-version argument in its own right — see
[work/README.md](work/README.md) "Not in this phase".

### A redacted audit is weaker evidence than an open one, and the release gate is deviated from knowingly

[second-repository-walk.md](second-repository-walk.md) is committed with every
path, filename and quoted line removed. [triage.md](triage.md) requires every
documented claim to be verifiable by a reader who does not trust you, and that
file is not. The conflict between two governing documents is reported here rather
than resolved silently, which is the rule [triage.md](triage.md) states for
exactly this case.

The deviation is confined to that one record. Redaction and evidence pull against
each other and redaction wins, on the same reasoning as
[Enumerating a private repository's record shapes was itself the leak](#enumerating-a-private-repositorys-record-shapes-was-itself-the-leak):
a public repository is not where a private one's shape gets published as a side
effect of a milestone. The objection's body is the sharpest instance —
[objections.md](../objections.md) requires "what your project does instead,
concretely, with paths", so a redacted objection is not a filed one, and the body
lives in that repository's own adoption record where it can carry the paths.

**What the reader gets instead of verifiability**: the walk states what it is
worth before it states any result, names redaction in its title, and says which
of its claims are attested rather than checkable. That is not a substitute and is
not offered as one.

**And a clean map was expected.** That repository imported this catalog's source
conventions deliberately and on its own record, so re-application inside one
lineage is what this tests. It is not evidence of generality, no objection would
have been the uninformative case rather than the reassuring one, and
[M13](work/m13.md) is forbidden from reporting the one as the other.

### The first objection is declined, and what that costs the channel is not argued away

The objection filed above is **declined.** Both checks now report `waived` in
that repository with its reason echoed every run, and the deviation block naming
this entry is written in its adoption record.

**The argument, as it was made, at full strength.** `findings-carry-evidence`
exists because "a row saying something is broken, written a month ago by someone
who is no longer sure, cannot be acted on and cannot be dismissed. It sits there
forever." `findings-have-review-state` exists because "this is what separates
noticing something from committing to fix it", and because per-item approval is
"the whole mechanism". Both purposes describe a queue whose rows **persist** and
are annotated in place, and both are stated as purposes rather than as shapes.

That repository's queue is **consumed.** Every row is removed by a triage step
that is mandatory per row and resolves each to exactly one of four outcomes, one
of which is a rejection that still leaves a durable record. So the aged
unactionable row the first obligation describes cannot form — not because someone
is diligent, but because the structure gives a row nowhere to age. And the
separation the second obligation wants is structural rather than columnar:
nothing in that file is ever work, work begins only when triage produces a
separate record, and every judging transition on that record is approved
individually through a review the owner has to sign. Both purposes are served.
Neither check can see it, because both read for a column.

The cost of complying is real and was named concretely, which is the filter
[objections.md](../objections.md) applies: two columns on that file turn capture
from "append a line" into "append a row and decide what goes in three cells",
against a first principle stating that capture must cost seconds or it does not
happen, and a recorded decision that capture and triage were split precisely
because they have opposite requirements. The review-state cell would also
duplicate a state that already lives in the record triage produces — two places
to look for one fact, which is the failure that module's own README names when it
warns against two queues.

**That is a good objection.** It is not a preference, it names a cost, and it
argues against the `purpose` field rather than around it. It is declined anyway,
for two reasons.

**One repository is thin evidence for a form.** A `form` is the catalog saying a
shape is *legitimately common* — configuration from then on, for everyone. What
is known here is that one repository has a consumed queue, and that repository
shares a convention lineage with the one these modules were extracted from, which
is the same limit
[The second repository is private, and it tests re-application rather than generality](#the-second-repository-is-private-and-it-tests-re-application-rather-than-generality)
puts on everything else this unit produced. A deviation is what the catalog has
for legitimately *local*, and one instance is what local looks like.

**And the phase's own scope contract forbids it.**
[work/README.md](work/README.md) "Specification edits are in scope, and this is
the list" names three units and the edits each forces —
[M8](work/m8.md), [M10](work/m10.md), [M12](work/m12.md). A `findings-queue` form
is on none of them. That section exists because the first version of it listed no
specification changes while three units were forcing them, and recognising an
alternative here would be exactly the hidden scope it was written to prevent. The
right time to add a form is a unit that says it is adding one.

**What this costs, stated plainly.** This is the objection channel's first real
use, and the answer is no. [objections.md](../objections.md) calls the channel
"the only way a module here finds out it is wrong", and the first thing it
returned was a decline. An adopter who files carefully, names a genuine cost, and
gets nothing back learns that filing is not worth the effort — and the channel
then fails silently, because a channel nobody uses looks identical to a catalog
nobody disagrees with. That is not argued away here and it is not offset by the
deviation: `waived` is visible and honest, and it is still the adopter carrying
the difference rather than the catalog moving.

**What would change the answer.** A second adopter with a consumed queue. At two
independent instances the shape stops being local and the argument for a form
stops resting on one repository's habits, which is the whole test this catalog
applies to itself. The deviation carries a `review_by` so the question comes back
whether or not anyone remembers it, and this entry is what makes the second
answer consistent with the first — or makes the change of mind visible if it is
not.

---

## 2026-08-04 — M12, F1 and F2 are closed

Both rows were recorded during phase one, neither was produced by a check, and
neither would have been produced by one: they are observations about the
catalog's own construction. They are closed here together because they were
scheduled together, not because they are related.

### The base set argument is normative in SPEC.md, and the README links to it

The what-breaks-without-it argument for `triage-rule`, `decision-log` and
`findings-queue` lived in two documents at once —
[README.md](../../README.md) "Why three modules are base" and
[SPEC.md](../../SPEC.md) "Base and prerequisites" — and had already drifted in
wording, which is what `F1` recorded. Neither statement was wrong. Nothing kept
them together, and no check in this catalog can see prose agreeing with prose.

**[SPEC.md](../../SPEC.md#base-and-prerequisites) is the normative home.** The
three-row table moved there; the README now names the three modules and links.

The choice is not a coin toss between two documents that both explain things.

- SPEC.md declares itself normative in its first line and everything under
  `modules/` is downstream of it. A document that says that about itself and
  then defers the definition of `base` to a README is describing a contract it
  does not hold.
- The base list is a **contract property**. `base: true` is a manifest field
  defined in SPEC.md's field reference, and growing the list is a versioning
  rule defined in SPEC.md's versioning table. The argument for *why three*
  belongs beside both, because it is the thing a major-version proposal to add a
  fourth has to defeat.
- The objection channel argues against stated purposes in normative documents.
  An objection to the base set aimed at a README is aimed at marketing copy.
- One of the two cross-links already existed and already pointed this way:
  [adopting.md](../adopting.md) sends a reader asking about partial adoption to
  `SPEC.md#base-and-prerequisites`, not to the README.

**What it costs.** The front door no longer carries the argument, so a reader
deciding whether to adopt takes one hop to find out what the base set is for.
That is the right trade only because of who edits what: a README is revised for
tone, length and first impressions by people who are not revising the contract,
and every one of those revisions was a chance for the two statements to move
apart again.

**What did not change.** Each module's README still argues its own adoption in
full, at a length the table in SPEC.md is not trying to reach. That is a
hierarchy — the catalog-level claim in one place, the module-level argument in
the module — rather than the duplication `F1` is about.

### The obligation is narrowed to what the check can see, rather than the check widened to prose

`role_referenced` resolves markdown links only. `triage-destination` used to say
the triage document **names** where out-of-scope findings go, which reads as
though a sentence would do. `TR-03` has never accepted a sentence. The gap was
recorded as `F2` at the first release and left open deliberately, because both
ways of closing it were available and neither had any evidence behind it.

**Taken: the obligation is reworded to say what the check does.** It now reads
*the document links to where out-of-scope findings go*, its purpose says why a
link and not a name, and
[`fixtures/satisfies-prose-destination/`](../../modules/triage-rule/fixtures/satisfies-prose-destination/)
is a tree where the rule names its destination in prose, the resolving link sits
two sections away, and `TR-03` reports `ok`. `TR-03` itself is untouched. The
module's advice that a repository hitting this should record a deviation is
withdrawn: the remedy is one link.

**Not taken: a new check kind matching a path-shaped string anywhere in the
target.** That is the option that would have made the obligation's old wording
true, and it is the more generous reading of what an adopter meant. Its cost, in
the order that decided it:

- **A major version on the catalog's highest-value check.** A check added is a
  major bump by a rule this repository argues at length —
  [a new check never ships in a minor version](#a-new-check-never-ships-in-a-minor-version)
  — and it would have landed on a base module, in the one area where the catalog
  claims its checks are worth having.
- **An addition to a deliberately closed vocabulary.** [SPEC.md](../../SPEC.md)
  opens the check-kind table with "Closed. Adding a kind is a change to this
  document, not to a module. That friction ratio is deliberate." An eighth kind
  is affordable exactly once before the friction stops meaning anything.
- **False positives on any prose that quotes a path.** Every document in this
  repository quotes paths; so does every triage rule worth reading. A check that
  reports a pass because a sentence happens to contain something path-shaped is
  measuring the presence of a string, which is the cut criterion in
  [triage.md](triage.md) applied to a behaviour check — and one that passes for
  the wrong reason is worse than one that fails for the right one, because
  nobody investigates a pass.

**The evidence that decided it, and it did not exist when `F2` was written.**

- [M11](work/m11.md)'s second repository named its findings destination in
  fenced code blocks and never linked it. `TR-03` fired. The correct fix was to
  **add the link**, and it was cheap — one edit to a document that was already
  clear to its readers and already wrong for anyone arriving later. Being strict
  about links produced the right outcome on a repository that was not built to
  demonstrate anything.
- [M10](work/m10.md)'s `A12` settled that a reference-style link counts as a
  link, so the strictness being defended here is strictness about *linking*, not
  about one syntax for it.
- `A17` had already relaxed the one-violating-tree-per-check rule, which made
  the third-shape fixture this option needs a smaller specification change than
  it would have been when `F2` was written.

**Why this is a MINOR and not a MAJOR.** No check was added, removed or changed,
and no repository that passed `TR-03` starts failing it — the bump rule is what
a previously clean adopter newly sees, and the answer is nothing. The
obligation's *shape* in the sense the versioning table means it — its id, its
roles, `required`, its condition — is unchanged; what moved is a title and a
purpose, narrowed onto the check that was already there. It is not a PATCH
either: the module now asks for something narrower than the words it shipped
with, and it withdraws advice an adopter may have acted on. The one adopter this
is visible to is one that recorded a deviation on the strength of that advice.
Their deviation still stands — deviations belong to the repository that records
them — but the justification this module offered for it is gone, and they should
add the link.

**On the risk this unit named against itself.** [M12](work/m12.md) warned that
the cheaper option is also the one with the stronger argument available to it,
which is the condition under which a decision gets taken on cost and justified
on principle afterwards. The defence is the ordering — this waited for two units
that produced real instances of the check's behaviour — and the requirement that
the cost of the rejected option be stated, which is the section above. If that
section had been unwritable, the decision would have been convenience.

### A passing fixture tree that `satisfies/` cannot hold is named `satisfies-<suffix>/`

[A check may carry more than one violating fixture tree](#a-check-may-carry-more-than-one-violating-fixture-tree)
left this open in as many words: a `pins-<CHECK-ID>-<what>/` category was
proposed and declined on the grounds that settling a convention by whatever an
implementer happened to call a directory is how an implementation's accidents
become a specification, and "the better name is a decision for whoever needs the
third tree". This is that unit.

**The name is `satisfies-<suffix>/`,** and the reason is the property that makes
`violates-<CHECK-ID>/` a good name: it asserts something about the tree that is
either true or false. `violates-TR-03` claims `TR-03` fails there.
`satisfies-prose-destination` claims nothing fails there, which is exactly what
`expected.yaml` says and exactly what the harness checks. `pins-` would have
named the author's intent instead, and every fixture tree in the catalog pins
something.

The shape is needed because `satisfies/` has to satisfy everything at once, and
a boundary worth pinning here is one where a *correct* repository must not
produce a finding — the content that pins it contradicts the content already in
that tree. Without the shape, the only way to test that a check stays quiet when
it should is to make the canonical satisfying tree carry every such case, and the
first pair of mutually exclusive cases makes that impossible.

[SPEC.md](../../SPEC.md) admits the shape in the same release, and
[auditing.md](../auditing.md) says why such a tree is not a spare copy of
`satisfies/`: a checker can be wrong in a way that produces a finding on a
correct repository, and that failure has nothing to catch it unless a tree exists
where the check must report `ok`.

## 2026-08-04 — M9, the conformance criterion is written

*Deferred from before [M10](work/m10.md) so that it could be written from
questions somebody had actually asked rather than from anticipation — the
reasoning is [above](#the-conformance-criterion-waits-until-an-implementer-has-asked-for-it).
The document is [docs/conformance.md](../conformance.md). Every clause in it
carries the ambiguity record that produced it, in the file, beside the clause.
These entries are the answers that are not obvious from reading it.*

### Conformance is measured against `expected.yaml`, and reproducing it is not evidence of correctness

Two halves, and the second is the one that keeps this document from being a
grading scheme.

**Measured against `expected.yaml`.** Not `expected.md`, which is prose that
nothing verifies and which has already drifted — it is open as `F3` in
[findings.md](findings.md). [auditing.md](../auditing.md) told an implementer to
compare against the finding named in the prose file, which was the honest
instruction before [M8](work/m8.md) made the expectations data and is not one a
criterion can rest on: a test two readers can run and disagree about is not a
test. The row-for-row form, and the insistence that the exact state matches
rather than something near it, comes from
[A03](https://github.com/DevOfPie/strucgu-check/blob/main/ambiguities/A03-history-deletions-with-no-history.md),
where the entire disagreement was `ok` against `skip`.

**And it proves less than it looks.** The first checker's mutation harness broke
it nine ways, one stated rule at a time, and five of the nine produced a clean
run against the catalog as it then stood. So the true content of a matched suite
is *the trees that exist did not catch this implementation*, and the document
says that in those words rather than in a footnote. The trees have since improved
and none of the nine now goes unnoticed, which changes what a claim is worth and
not what it says.

The cost of stating it this way is that the strongest sentence available to an
implementer is weaker than the one they wanted. That is the correct trade for a
catalog that ships no runner: the alternative is a criterion whose plain reading
overstates the evidence, and the overstatement would be this repository's rather
than theirs.

### The register a prospective adopter wants is the register a standards body keeps

`F14` names the gap in as many words: nothing here records which implementations
reproduce which release, so *has anyone implemented this, and does their run
still match?* has no home, and it names this document as the natural one.

**It stays homeless, and the request is the reason to be sure.** A list of
conforming implementations is the artifact every one of these refusals exists to
prevent, and it does not become something else because the first person to want
it wanted it for a good reason. Keeping it would mean upstream holding a record
about someone who uses this, which is the one thing
[README.md](../../README.md#what-this-is-not) promises structurally rather than
as good behaviour — and a structural guarantee that is kept until somebody has a
use for breaking it was never structural.

**What it costs, stated rather than offset.** A prospective adopter has no
evidence that anyone has implemented this successfully except by reading a claim
someone else made and re-running it. Anyone may claim conformance falsely and
this repository will never know, never say so, and have no standing to. Both are
accepted. The defence is that verification is cheap and local — clone, run,
compare — so the claim a register would centralise is one every reader can
already check for themselves, and centralising it buys convenience at the price
of the guarantee.

For the same reason there is no process to register, submit or announce a
conforming implementation: no form, no template, no address. The
[objection channel](../objections.md) is not it, and the distinction is worth
holding — an objection is a disagreement with an obligation and all four of its
outcomes change the catalog, where news about an implementation would change
nothing here except the existence of a list.

### The only implementation in existence does not conform to `decision-log` 0.3.0

[strucgu-check](https://github.com/DevOfPie/strucgu-check) reproduced every row
of every module at `0.2.0`. `decision-log` then went to `0.3.0`, correcting five
`DL-03` rows from `ok` to `skip`
([why](#the-fixtures-were-wrong-about-dl-03-and-the-specification-stays-as-it-is)),
and that checker still reports `ok` on those five. It conforms to `decision-log`
0.2.0. It does not conform to `decision-log` 0.3.0. Both are true, and the
document says so with the module and the version named.

This was the test of whether the criterion could be written honestly. A criterion
under which the only existing checker conformed by construction would be a
criterion shaped around a reference implementation, which is the risk
[m9.md](work/m9.md) names against itself and the reason the unit waited. The
handling is **stale, not false**: a claim is about the version it names and stays
true of that version, and a module releasing a check makes the claim older rather
than wrong. Nobody withdraws anything, because propagation here is pull-only and
falling behind is the designed behaviour rather than a failure of it.

**What the instance exposed on the way past.** `decision-log` `0.3.0` was a
correct MINOR — its changelog says a previously clean adopter newly sees nothing,
and that is true. A conformance claim went stale anyway.
[SPEC.md](../../SPEC.md#versioning) sizes a bump by what an *adopter* sees, and
the reader whose claim just moved is an *implementer*. The versioning table has
no row for that, and the criterion does not need one to work — it names a
version and the version moved — so the gap is recorded as `F16` rather than
closed here.

### Two clauses were cut for having no origin, and a third for being an expiry

[m9.md](work/m9.md) makes a clause with no traceable question a clause written on
anticipation, and cuts it. Recording the cuts costs a paragraph and is worth more
than the clauses that survived, by the same argument this repository already
applies to [the six checks it cut](#six-checks-were-cut-for-measuring-presence-rather-than-thought).

- **"A claim names the catalog commit, not only the module version."** Would have
  guarded against a module's fixtures moving without its version moving. Nobody
  asked: no ambiguity record raises it, and the one instance in evidence did move
  the version. It is anticipation about a hazard that is real, which is the most
  persuasive kind and still anticipation — so the hazard is filed as `F16` and the
  clause is not written.
- **"A conforming implementation publishes the readings it took where the
  specification is silent."** Tempting, because the ambiguity log is the most
  valuable thing [M10](work/m10.md) produced. But it was produced because M10's
  brief required it, not because an implementer asked to be required to, and
  turning one brief's obligation into a condition of conformance is upstream
  setting homework it cannot mark. It is also the first step of a submission
  process, which is [deliberately absent](#the-register-a-prospective-adopter-wants-is-the-register-a-standards-body-keeps).
- **"A claim is re-run each release, or lapses."** This is what `F14` makes one
  want to write, and it is an expiry on a self-assertion. Upstream cannot see
  anyone miss it, so the rule would be decoration; making it enforceable would
  need the register that is refused. **Stale, not false** does the same work
  without either.

## 2026-08-04 — M13, the phase closes and the version is argued

*The release walk is [self-walk-0.2.0.md](self-walk-0.2.0.md), committed beside
the walk at `0.1.0` rather than over it. These entries are the four things the
close decided that reading the walk would not tell you.*

### The two versioning rules measure different readers, and the conflict is reported rather than picked

Two documents in this repository size a version bump, and on this release they
disagree.

- [SPEC.md](../../SPEC.md#versioning) sizes a bump by **what a previously clean
  adopter will newly see**. Read against this phase it says MINOR: no check was
  added, no obligation's shape changed, the base list did not move, no role was
  renamed. Four of the five modules' own changelogs say "nothing" in the fixed
  sentence and they are right.
- [CHANGELOG.md](../../CHANGELOG.md) sizes **this repository's** version, and
  calls a change breaking when *an adoption record or a checker written against
  the old contract needs changing*. Read against this phase it says breaking,
  and not marginally.

[triage.md](triage.md) says a conflict between governing documents is a bug to
report rather than a choice to make quietly, so this is the report.

**Neither is wrong, and they are not measuring the same thing.** SPEC.md's table
is adopter-facing and sized for a *module*: it answers "will my repository start
reporting something new". The CHANGELOG's table is implementer-facing and sized
for the *contract*: it answers "does the thing I wrote against this still work".
This phase changed almost nothing an adopter sees and a great deal an
implementer must re-read:

- the **Roles** paragraph is rewritten — recursion into subdirectories, where
  the `exclude` list lives and what it matches, and per-file results collapsing
  to one state for the role (`A07`, `A10`, `A15`)
- **`effective_from` is exclusive**, and a date is compared against committer
  date (`A13`)
- **`path_exists` on a `dir` role** requires a *markdown* file surviving
  exclusions, not any file (`A02`)
- a check bound to **more than one role** evaluates over the roles that resolved
  and skips only when none did (`A01`)
- `fixtures/` admits **more than one violating tree** per check (`A17`) and a
  **third tree shape**, `satisfies-<suffix>/` (`M12`)

Every one of those changes what a conformant run outputs. A checker written
against `0.1.0` is wrong on all five, and this repository has one to point at.

**Which rule governs which version, stated so the next release does not
re-litigate it.** SPEC.md's table governs a **module's** version, and each
module's changelog answers it in the fixed sentence. The CHANGELOG's table
governs **this repository's** version, which is the module contract's version.
They will disagree again, because a contract change that adds no check is
exactly the shape that makes them disagree, and the answer is that both are
published and neither is overruled.

**The owner settled it: the release is `0.2.0` and is declared breaking.** That
was not this work unit's call — it is the disposition of a reported conflict
between two governing documents, which belongs to the owner by the same rule
that produced the report.

### Below 1.0.0, a breaking change collapses into the minor digit

`F7` asked what a MAJOR means while every version here is `0.x`, and predicted
it would be answered at the worst possible moment: while shipping the change
that forces it. It was.

**The owner's answer: it collapses into the minor digit.** A breaking change
below `1.0.0` moves `0.1.0` to `0.2.0`, not to `1.0.0`.

The reason is the one `F7` already contained. `1.0.0` is not a bigger number; it
is a claim, and the claim is stability. [README.md](../../README.md) says the
opposite in as many words — the shape will move, pins are cheap, breaking
changes will happen, the objection channel is the point rather than the
exception — and this phase supplies no evidence against that. One implementation
and one second adopter is exactly what `0.x` is for. Shipping `1.0.0` here would
have made the version number the most optimistic sentence in the repository.

What it costs: a reader who reads `0.1.0 → 0.2.0` as routine gets no warning
from the digits, and the only thing that tells them the contract moved is the
changelog entry. That is accepted, because the alternative buys the warning by
publishing a claim about stability that is false. `F7` closes on this, and only
`F7` — nothing else in the queue was reviewed.

### The second walk exercises `skip` nowhere, and that is a loss rather than a cleaner summary

The `0.1.0` walk reported `24 ok, 0 findings, 4 skipped`. This one reports
`27 ok, 1 finding, 0 skipped`. Read as a scoreboard that is three checks better
and one worse. Read honestly it is the other way round.

Those four `skip`s were the `IN-*` checks over an unmapped `investigations`
role, and the first walk called them **the point of that walk** — the only
exercise of the `skip` path and of a conditional obligation anywhere in this
repository. [M10](work/m10.md) produced an investigation that genuinely outgrew
a decision entry, the role is
[mapped for that reason](#the-ambiguity-log-is-the-investigation-that-outgrew-a-decision-entry),
and the four checks now report `ok`. The mapping is right. The loss is real
anyway, and the two facts do not cancel.

`skip` is the state this catalog leans on hardest. It is what keeps "I did not
look" from being reported as "I looked and it was fine", it is named in
[triage.md](triage.md)'s standing rules, and
[SPEC.md](../../SPEC.md) and [auditing.md](../auditing.md) between them warn
four times against folding it into `ok`. It is now demonstrated in no recorded
output anywhere: not in this repository's walk, and not in the
[second repository's](second-repository-walk.md), which declined the two modules
that would have produced skips rather than half-adopting them — the honest
answer, and the same absence.

**So the walk says so instead of reporting the better-looking number.** Coverage
survives in the fixture trees, on 23 expected `skip` rows across all five
modules, which is coverage by construction in trees written by the party that
wrote the checks. It is not a demonstration that a real repository produces one.

What would fix it is not available and is not worth faking: a repository that
adopts a module whose conditional obligation is genuinely unmet, audited and
recorded. Inventing one here would be the same move this repository
[refused for deviations](#this-repository-records-no-deviation-of-its-own), and
for the same reason.

### Two data points adjacent to the author are not a track record

[README.md](../../README.md)'s *What 0.x means here* was a disclaimer: the
catalog came from one repository and one instance cannot tell a general
convention from one project's habits. This release replaces it with findings,
which is [m13.md](work/m13.md)'s discharge and is the whole point of the phase.

**The risk in doing that is that findings read as maturity.** They are more
persuasive than a disclaimer by construction — that is why they replace it — and
the rewritten section has to carry the same warning while sounding less like
one.

So the section states both limits **where the results are**, rather than in the
work records that already admit them:

- [M10](#the-first-checker-is-whippys-and-its-independence-is-partial)'s
  implementer shares a **model lineage** with phase one's co-author. It was
  written from the published repository alone under a no-questions rule, which
  bounds one channel and not the reading.
- [M11](#the-second-repository-is-private-and-it-tests-re-application-rather-than-generality)'s
  adopter shares a **convention lineage** with the repository the catalog was
  extracted from. It tests whether an extraction survives re-application inside
  that lineage. It does not test generality, and a clean map there was the
  expected outcome.

That is two data points, both adjacent to the author. It is a great deal more
than phase one had, and it is not a track record. The generality question still
needs a repository built by someone who has never read LinkCtrl, and nothing in
this release moves it.

**The sharpest number in the section is the one that flatters least.** The first
implementation found eighteen places the specification did not determine what a
checker should do — in a specification whose author believed it was precise —
and it resolved six of them at *medium* confidence, meaning the reading it took
is defensible rather than determined. None was resolved at low confidence, and
that says less than it looks: low would have meant a guess the implementer
distrusted, and an implementer who reaches that point files a question instead.
The section reports the medium count for that reason, rather than the zero.

---

## 2026-08-04 — the process contract catches up with the one it was extracted from

[triage.md](triage.md) was written once, on 2026-07-31, as an adaptation of the
operating contract of the repository this catalog was extracted from. That
contract kept moving; this one did not. Four rules were added or hardened there
across the following two days, and one existed hours before the adaptation was
written and was not carried across. None of them is about links or modules, so
nothing here noticed.

The gap is worth naming rather than quietly closing. **A process document that is
forked and then frozen looks maintained** — it is short, internally consistent,
and every rule in it is true. What it stops being is *current*, and the only
signal is that the file has one commit against a repository with sixty.

The entries below take four of those rules. The ones deliberately not taken are
named in each entry: this repository ships no code, runs no loop of its own, and
has no capture queue, so several of the rules on the other side guard machinery
that does not exist here.

### A shipped unit whose claim is false is reopened, not succeeded

The status table had three words — `planned`, `deferred`, `done` — and no way to
say that a `done` row is asserting something untrue. There are three such rows
today. `F3` says `triage-rule`'s expectations state a count matching no reading
of its own fixtures; `F14` says five expectation rows are no longer reproduced by
the only implementation; `F17` says the decision index is one row short of its
entries and has been since M13 shipped.

Each of those is a shipped unit's claim being false. Under the vocabulary as it
stood, correcting one meant a new unit — which leaves the old `done` row in place,
still asserting what was found to be wrong, and splits one piece of work across
two numbers. **A successor is a worse record than a reopening**, and the whole
point of the status table is to be a record.

So `reopened` is the fourth word, and the rule that produces it is in
[triage.md](triage.md). Two details are this repository's rather than inherited:

- **The finding comes first.** A reopening is scheduling, and scheduling is the
  owner's — the same rule that makes an unreviewed queue row a report rather than
  a commitment. Nothing reopens because an actor noticed something.
- **The status word is not where the reopening survives.** It returns to `done`,
  so a table read a month later shows no trace. The unit's own file carries what
  was false and what closed it, which is [findings.md](findings.md)'s rule about
  moving rows rather than deleting them, applied to the other tracker.

The second detail is the one the source contract does not have, and it is not an
improvement so much as a different exposure: over there a reopening is legible in
a milestone's history because the loop that ran it writes an entry either way.
Here nothing writes anything unless a rule says to.

### No row leaves a tracker without saying where it went

[findings.md](findings.md) already has this rule for itself — rows move to
*Closed*, never out — and the reasoning is stated there: a queue that empties by
deletion cannot show what it caught. Nothing extended it to the other trackers.

The exposed one is [work/README.md](work/README.md). Its *Not in this phase* list
and its list of permitted specification edits are both there to stop scope
arriving by drift, and both could be shortened by anyone who decided a line no
longer applied. The second list exists **because that already happened once**: the
first version of that section named no specification changes while three units
forced them. A list that can be quietly shortened has the same failure mode as a
list that was never written.

So removal has two forms and no third: re-homed, with the row saying where it
went, or logged in this file with what was dropped and why. Deciding an item no
longer matters is a decision, and it is the kind that returns a year later as a
fresh idea with its reasoning gone.

This is one of the two rules here that the catalog itself cannot check.
`findings-queue` can see that a queue exists, has evidence and has a review
state; no obligation anywhere can see a row that used to be there. That is not an
argument for adding one — it is the shape of thing `F10` already names, and
closing it is a major-version argument rather than a rule in this file.

### A decision reached in conversation is written down before it is acted on

This repository publishes a module whose whole subject is the record of why
choices were made, and had no rule saying when to write one.

It has been getting away with it. The four scope questions this phase needed were
put to the owner on 2026-08-02, answered in conversation, and written into
[work/README.md](work/README.md) and this file before anything was built —
correctly, and because the actor happened to do it, not because anything required
it. The failure mode is not dramatic: the answer gets acted on, the reasoning
evaporates, and the next session re-derives a slightly different conclusion from
a tree that already reflects the first one.

The rule is ordering, not volume. The entry goes in **before** the change it
authorizes lands. Written afterwards it is a description of the tree, which is
what the tree already is.

### A prompt without costs is a request for permission, not a decision

*Stop and ask* said when to ask and nothing about what an ask contains, so the
shape was the asking actor's habit. The failure is specific and it runs one way:
the actor that raises the prompt is usually the actor that will do the work, and
an unconstrained recommendation drifts toward whatever is cheapest to build. It
does not read as bias, because the cheap option is genuinely defensible and the
expensive one is genuinely expensive; what goes missing is that the trade was
never stated.

So a prompt carries options with what each buys *and* costs, a marked
recommendation that states its own con, and the default — what happens if the
answer is *you decide*. Naming the default is the cheapest part and does the most
work: without it, skipping a question requires re-deriving the whole choice, so
questions get answered by attrition rather than judgment.

If nothing can be recommended, saying so is the answer. Omitting the
recommendation silently is not.

### A documentation claim this repository has just falsified fails the commit, not the release walk

The commit gate checked links, roles, prose-and-manifest agreement, fixtures,
vocabulary, neutrality and scope — everything about a module's internal shape,
and nothing about whether the documents describing the catalog were still true.
Truth was the release documentation pass's job, which is to say it was checked
once per release.

`F15` is what that costs. `M8` made `expected.yaml` a required file in every
module directory; [docs/auditing.md](../auditing.md) describes a `fixtures/`
directory without it and sends the implementer to the prose file instead. The
document written for the one audience that most needs the mechanical answer has
been wrong since M8 shipped, through a release and a documentation pass, because
nothing at the moment of the change asked.

The new gate row is narrow on purpose. It fires only when the unit changed what
an adopter or a reader would observe, and it asks about the three surfaces that
make claims to outsiders — [SPEC.md](../../SPEC.md), [README.md](../../README.md),
and the affected module READMEs. It is not a documentation pass in miniature: the
release pass still exists and still reads everything. This one catches the case
where the person who made the claim false is standing right there.

### Eight record files with no index is the failure this catalog is about

`docs/records/` had eight files and no map. Every one of them is well documented
from the inside — [triage.md](triage.md) states its own precedence,
[findings.md](findings.md) explains what a row is for — and there was no answer
to *what is this directory, and which file do I read first*.

That is uncomfortable in a repository whose subject is records of work, and `F9`
is the sharpened version of it: the second adopter's audit could reach that
repository's process document, its rationale and its deferral destination, and
could not reach its scope contract at all, because no role names it. This
repository hid the gap from itself — [work/README.md](work/README.md) is both its
scope contract and its unit index, so the coupling has never cost it anything.

**The new file is not a module and does not close `F9`.** A sixth module, or
splitting `unit_index` in two, is a major-version argument and stays out of
scope. What the map does is smaller and worth doing anyway: it says what the
directory is, which file wins on what, and — the part no individual file could
state — that these records are simultaneously working documents and this
repository's own adoption evidence, so a change to one of them can move a check
result rather than being documentation wording.

It also carries the disclaimer where the method is, rather than only where the
results are. Somebody reading a working method that produced a specification will
read it as the method the specification recommends. It is not: StrucGu specifies
the shape of records and never their process, and this directory is one
repository's answer on top of that.

### One tracker is watched for silent removal, and it is watched by the check that cannot judge

Correcting [No row leaves a tracker without saying where it
went](#no-row-leaves-a-tracker-without-saying-where-it-went), appended the same
day. That entry closed with *"this is one of the two rules here that the
catalog itself cannot check"*, named no second rule, and was wrong in both
directions. The original stands above; this is what it should have said.

**Wrong on the count.** *None* of the rules added with it is checkable here. A
check reads the shape of a record — that a queue exists, that its rows carry
evidence, that an index is present. Whether a decision was written down
*before* it was acted on, whether a prompt carried its costs, whether a gate
fired at the moment a claim went stale: all are properties of a process rather
than of a record, and this catalog specifies records. That is not a gap to
close. A module that could see any of it would be describing how a repository
works instead of what it keeps, which is the line [SPEC.md](../../SPEC.md)
refuses to cross.

**Wrong on the substance.** The entry said no obligation anywhere can see a row
that used to be there. `DL-03` can, and does — it reads history deletions after
`effective_from`, and `F6` is it firing on this repository, over the redaction
in `e132646`.

So the accurate statement is narrower and worth more than the one it replaces.
**Exactly one tracker here is watched for silent removal, and the other three
are not.** [decisions.md](decisions.md) is watched because the decision log is
the record a project is most tempted to tidy. [findings.md](findings.md),
[work/README.md](work/README.md)'s status table and its two scope lists are
watched by nobody, and the new standing rule is the only thing standing over
them.

The watched one is watched by a check that **cannot tell a justified redaction
from an entry edited away** — `decision-log`'s own
[module.md](../../modules/decision-log/module.md) says so, and `F6` is the live
instance. Which is the honest shape of the whole arrangement: one tracker gets
a check that reports for a look rather than as a defect, three get a sentence
in a process document, and the sentence is load-bearing precisely because
nothing mechanical stands behind it.

`F10` remains the wider version of this — no record anywhere carries an expiry
that forces disposal — and closing it is still a major-version argument rather
than a rule in [triage.md](triage.md).

## 2026-08-04 — phase three is scoped

### Phase three measures before it grows, and the housekeeping goes first

Phase two ended with a catalog that had been implemented once, adopted once,
and walked twice, and with sixteen open findings none of which had been
reviewed. Three things could have been the spine of the next phase and only one
of them can be done from inside this repository.

**Growth** — `F9` and `F10`, the two largest findings the second adopter produced
— would answer the loudest external input this project has received. **Evidence**
— an adopter or implementer who has never read the repository this catalog was
extracted from — would answer the only question that actually matters for a `0.x`
version claiming nothing about generality. **Measurement** — closing the gap
between what the specification asserts and what any tree tests — answers neither,
and is the one this phase takes.

The argument for taking it first is that the other two are worth less until it
is done. A sixth module added to a catalog that cannot test the five it has
grows the untested surface. An outside implementer handed a specification with
a dozen untested normative claims finds them the way the first one did —
eighteen at a time, as ambiguities — and the phase after this one would be
spent on the same work with a stranger's patience being spent instead of ours.

**The housekeeping units go first at the owner's direction, and the ordering
turned out to be load-bearing rather than a preference.** `F19` is this
repository's scope contract describing a phase that has ended; a phase plan
written on top of it inherits the error, which is what nearly happened here.

**One ordering constraint inside the phase is hard.** [M16](work/m16.md) settles
how a version is sized for a change that moves what a conformant run must output
while an adopter sees nothing. [M17](work/m17.md) and [M18](work/m18.md) are the
largest such change this repository has ever made. Deciding the rule after making
the change means deciding it while standing on the instance, which is the failure
[work/m9.md](work/m9.md) named against itself and the reason the conformance
criterion was deferred until there was something to test it on.

### What the phase does to the queue, stated because approval is per row

[triage.md](triage.md) makes an unreviewed finding a report rather than a
commitment, and sixteen of them were unreviewed when this was written. This
plan schedules work that closes **nine**: `F3`, `F5`, `F8`, `F14`, `F15`,
`F16`, `F17`, `F18` and `F19`. Approving the plan is approving those nine rows
and nothing else.

**Seven stay open, and none of them stays open by accident.**

- `F9` and `F10` are the growth argument above. They are the two this phase
  most visibly declines, and declining them makes three refusals in a row
  against outside input — after the first objection was declined at `0.2.0`.
  That cost is real, it accrues to a channel whose entire value is that filing
  is worth doing, and it is recorded here rather than offset.
- `F11` and `F12` are already answered: both are catalog gaps ruled out of
  scope on principle, with the reasoning in their rows.
- `F13` — a judgment entry reading for a field no obligation requires — is
  small and would be a reasonable addition to [M15](work/m15.md). It is left
  out because its two fixes are a new obligation or a reworded entry, and the
  first is the growth argument in miniature.
- `F6` is not a unit at all. It is a disposition the owner takes: record this
  repository's first deviation, or accept a `DL-03` finding on every run
  forever. Both are legitimate and neither is work.
- `F4` is the closest call. The specification does not say what state a check
  reports while its two halves disagree, which is the same family as `F5` and
  `F8` and would sit naturally in [M18](work/m18.md). It is left out because
  its answer changes `WU-04`'s expected result from `finding` to `skip` — an
  expectation change rather than a wording fix — and this phase already has two
  units rewriting expectations. If `M18` reaches it anyway, it is in scope for
  that unit and this entry is where the permission is.

## 2026-08-04 — phase three is reordered, and gains a release and an adoption

### The cheap corrections go last, because the phase moves the records they correct

Correcting [Phase three measures before it grows, and the housekeeping goes
first](#phase-three-measures-before-it-grows-and-the-housekeeping-goes-first),
appended the same day. That entry recorded the owner's direction that the
housekeeping run first, and the plan was written that way. Asked afterwards to
order the phase for efficiency, the answer changed, and this is why.

**Three of the five corrections are about records this phase is going to
move.** [M16](work/m16.md) adds fixture trees to modules whose prose counts
their judgment lines — that is `F3`. [M17](work/m17.md) changes the schema that
the implementer's guide describes — that is `F15`. `M17` bumps every module
past the version this repository's own adoption record pins — that is `F18`.
Fixing them first fixes them twice, and the second fix is the one that
survives.

The other two do not move. `F17` is a missing index row and `F19` is this
repository's scope contract describing a phase that has ended, and nothing
later in the phase touches either. Those go first, and `F19` goes first for a
reason beyond cost: every unit reads the file it is wrong in.

So the corrections split across [M14](work/m14.md) and [M19](work/m19.md)
rather than sitting in one unit at one end of the phase. **The owner's
instruction is not overruled so much as split by it** — the housekeeping that
can be done once is still first, and the housekeeping that would be done twice
is not.

One thing the earlier entry got right and is worth keeping: the ordering
constraint on [M15](work/m15.md) is hard, and it survives the reorder
unchanged.

### A phase that changes the contract and does not publish a release is not finished

The plan as first written had no release unit, which is a gap rather than a
choice. Phase two ended with [M13](work/m13.md) doing the walk, the changelog,
the `0.x` section and the documentation pass; this phase changes the contract
more than that one did and had nothing scheduled to say so. [M20](work/m20.md)
is that unit.

It also became load-bearing for a second reason. An adoption record pins a
version, so [M21](work/m21.md) needs a released one to pin — adopting an
unreleased tree would produce a record that names a version nobody else can
fetch.

### LinkCtrl adopting proves nothing about generality, and is worth doing anyway

The owner asked that LinkCtrl start using this catalog once the phase
completes. [M21](work/m21.md) is that unit, and the first thing it has to
establish is what the result is not.

**LinkCtrl is the repository these conventions were extracted from.** A clean
map there is guaranteed by construction: the rules were written by reading that
tree. [README.md](../../README.md) currently says two data points, both
adjacent to the author; this is a third and it is the most adjacent one
available. The generality question — a repository built by somebody who has
never read LinkCtrl — is untouched by it, and the risk is not that the walk
fails but that it succeeds and gets read as maturity.

Three things make it worth the phase's last unit regardless.

**It is verifiable.** [M11](work/m11.md)'s second repository is private, its
walk is redacted, and a reader cannot check it — a knowing deviation from this
repository's own release gate, named at the gate. LinkCtrl is public. This is
the first adoption record here that an outsider can reproduce line for line,
and it repairs that deviation rather than arguing it again.

**It makes `F9` an observation instead of an argument.** `F9` says no role
reaches a repository's scope contract unless that repository also has units of
work, and admits this repository hides the gap from itself because one file
plays both parts. LinkCtrl separates them: its scope contract is one file and
its unit index is another. The coupling stops being hypothetical against a
public tree.

**LinkCtrl has moved since the extraction.** It keeps record types this catalog
has never seen — a tracker for changes to its own process, a file of questions
with no answer yet, a measurement of what its always-read documents cost. None
has a role. That the catalog cannot reach the records of the one repository it
came from is worth knowing, and the unmapped list is `M21`'s primary output. An
empty one would mean the walk did not look.

**Nothing ships to make this repeatable**, for LinkCtrl or anyone. No action,
no template, no bot, no CI integration. That refusal is unchanged by the
adopter being familiar, and an adopter wanting a scheduled audit builds it from
a checker themselves.

The prerequisite is outside this repository and is named rather than assumed:
the adoption record is a commit in LinkCtrl, placed through LinkCtrl's own
process and around its own unattended build loop. This phase cannot schedule
that. The owner places it; `M21` waits.
