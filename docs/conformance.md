# Conformance

What it means to say a checker conforms to a module, and — at greater length,
because it is the part that goes wrong — what it does not mean.

[SPEC.md](../SPEC.md) is normative and defines the checks. [auditing.md](auditing.md)
is written for someone about to implement one. This file answers the question
those two leave open: **your run matched every fixture. What have you got?**

The short answer is one sentence. A checker **conforms to a module at a version**
when it reproduces every row of that module's `fixtures/expected.yaml` at that
version. Everything below is the qualifications, and they are worth more than the
sentence.

**Written after the first implementation, not before it.** Every clause carries
the question that produced it, because a criterion assembled from anticipation is
exactly how a document like this quietly becomes a certification scheme — the
reasoning is in
[decisions.md](records/decisions.md#the-conformance-criterion-waits-until-an-implementer-has-asked-for-it).
The questions are real ones: the first independent checker recorded
[eighteen places](records/investigations/0001-what-the-specification-does-not-determine.md)
where this specification did not determine what it should do, each recorded
before it was resolved. Clauses that could not be traced to one of them were cut.

---

## What conformance is not

Stated before what it is, for the reason [README.md](../README.md#what-this-is-not)
states its refusals first: every catalog of conventions drifts toward being a
standards body, and the only defence is writing the refusal down where it will be
read.

- **There is no badge, no score, and no conformance level.** Nothing here grades
  an implementation, ranks two of them, or issues a mark to put in a readme. A
  checker either reproduces a module's expectations at a version or it does not,
  and that is a fact about a run rather than a status conferred by anyone.
- **There is no list of conforming implementations.** StrucGu keeps no register,
  no directory, and no roll of adopters or implementers. There is nothing to be
  on and nothing to fall off. One implementation is named in these records — it
  is named because this repository commissioned it as a unit of work and had to
  say where the evidence came from, and what those records say about it is that
  [its run no longer matches](records/findings.md), which is the opposite of what
  a register entry is for.
- **There is no record kept upstream of anyone who claims it.** A conformance
  claim is made by you, about your own run, and held by you. Upstream holds
  nothing with which to contradict a false one.

That last refusal is the load-bearing one, and it cuts both ways on purpose.
Because upstream keeps no record, there is nothing to certify against and nothing
to revoke — that is a **structural guarantee** rather than a promise of good
behaviour, and it is the same guarantee
[README.md](../README.md#what-this-is-not) makes about adoption. It is also an
**accepted cost**: anyone may claim conformance falsely and this repository will
never know, never say so, and have no standing to. A reader who wants the claim
checked runs the fixtures themselves, which is cheap, offline, and the only
verification that was ever on offer.

**Origin.** The cost is not hypothetical and was not invented here to look
even-handed. `F14` in [findings.md](records/findings.md) records the pressure
directly: an implementation fell behind the catalog, and what the row names as
missing is that *"nothing in this repository records which implementations
reproduce which release, so the one piece of evidence a prospective adopter would
want — has anyone implemented this, and does their run still match? — has no
home"*, and names this document as the natural place for it. The answer is that it
stays homeless. The register a prospective adopter wants and the register a
standards body keeps are the same file.

### Nothing to register, submit, or announce

**Deliberately not built.** There is no form, no issue template, no tracker
label, no branch, and no address for telling upstream that you have written a
conforming checker. There is nowhere to send it, and that is the design rather
than an omission to be filled in later.

The [objection channel](objections.md) exists and is not this. It carries a
disagreement about an *obligation* — with what your project does instead, and what
complying would cost — and its four outcomes all change the catalog. It does not
carry news about your implementation, and a checker's conformance is not a thing
this repository has an opinion about.

**Origin.** The same `F14`, and the refusal already in
[auditing.md](auditing.md#objections-are-drafted-not-filed) — a checker files
nothing anywhere. An address to send conformance news to is a queue, a queue
someone reads is a review, and a review someone records is the list refused
above.

---

## The criterion

### 1. The unit is a module at a version

A conformance claim names a module and a version: *this checker conforms to
`decision-log` 0.3.0*. Not the catalog, not a release, not a checker in general.

**Origin.** [A08](https://github.com/DevOfPie/strucgu-check/blob/main/ambiguities/A08-pinned-version-does-not-match-the-module.md),
which asked what an exact version pin means when the module on disk is a
different version. It established that **a checker evaluates the module as it
reads it** — it cannot evaluate any other version — which is now stated in
[SPEC.md](../SPEC.md#versioning). If a run is always a run against one version of
one module, a claim about that run cannot be broader than that.

### 2. Measured against `expected.yaml`, row for row, in all five states

Run the checker over every tree in the module's `fixtures/` directory. For every
check id on every tree, and for every judgment entry id, the state it reports
must equal the state `expected.yaml` records. No row missing, none added, and
the [five states](../SPEC.md#audit-output) distinguished — `ok`, `finding`,
`skip`, `waived`, `judgment`. A checker reporting `ok` where the file says `skip`
does not conform, however defensible its reasoning.

The measurement is against `expected.yaml` and **not** against `expected.md`.
The prose file states intent and nothing verifies it; it has already drifted once
and is open as `F3` in [findings.md](records/findings.md). A criterion resting on
a file nothing checks would be a criterion nobody could apply twice and get the
same answer.

**Origin.**
[A03](https://github.com/DevOfPie/strucgu-check/blob/main/ambiguities/A03-history-deletions-with-no-history.md)
for the row-for-row part and for the insistence on the exact state: it is the
record where the fixtures and the prose gave different answers for `DL-03`, the
implementer had to be told which one the claim was measured against, and the gap
between `ok` and `skip` was the whole disagreement. That one was
[resolved against the fixtures](records/decisions.md#the-fixtures-were-wrong-about-dl-03-and-the-specification-stays-as-it-is).
[A11](https://github.com/DevOfPie/strucgu-check/blob/main/ambiguities/A11-judgment-entries-over-absent-roles.md)
for judgment entries being in scope at all — it asked what a judgment entry
reports when the document it names is absent, and the answer made the judgment
section something a run can be compared against. `expected.md` is excluded on the
strength of finding 4 in
[investigations/0001](records/investigations/0001-what-the-specification-does-not-determine.md).

### 3. Matching every row is necessary and is not sufficient

Reproducing a module's expectations means **the fixtures did not catch you**. It
does not mean the implementation is right, and this catalog has measured the
difference rather than asserting it.

The first checker was broken on purpose, one stated rule at a time, and every
tree re-run. Against the catalog as it then stood, **five of nine deliberate
breakages produced a clean run** — a suite reporting agreement with a checker
that was measurably wrong. Two of the five were the matching rules
[SPEC.md](../SPEC.md#matching-rules) argues for hardest, both learned from a real
failure and neither with a tree behind it.

So the honest reading of a conformance claim is: *this implementation was not
caught by the trees that exist*. The trees have since improved — with the ones
added in the same release, none of the nine breakages goes unnoticed — which
moves what a claim is worth without changing its shape.

**Origin.**
[A14](https://github.com/DevOfPie/strucgu-check/blob/main/ambiguities/A14-rules-stated-and-never-pinned.md),
which is the measurement, and
[A17](https://github.com/DevOfPie/strucgu-check/blob/main/ambiguities/A17-one-violating-tree-per-check.md),
which found why the gaps persisted — `fixtures/` was specified as exactly one
violating tree per check, so a check with two boundaries worth pinning could not
have both pinned. That rule is
[now relaxed](records/decisions.md#a-check-may-carry-more-than-one-violating-fixture-tree).

### 4. Partial conformance is the ordinary case

Conformance is per module. A checker that conforms to `triage-rule` 0.4.0 and to
`decision-log` 0.3.0, and implements neither optional module, says exactly that
and has said something useful. There is no all-or-nothing claim to fall short of,
because a criterion that recognised only the full catalog would push an
implementer toward claiming more than they have — which is a worse outcome than a
narrow claim, and the only one a stricter criterion would actually produce.

The module is the floor as well as the ceiling. A claim covering some of a
module's checks and not the rest is not a partial conformance claim, because the
module's expectations include every check and every judgment entry on every tree;
it is a report of a run in progress, which is a useful thing to publish and a
different thing to say.

**Origin.**
[A16](https://github.com/DevOfPie/strucgu-check/blob/main/ambiguities/A16-a-history-check-with-no-effective-from.md)
and
[A06](https://github.com/DevOfPie/strucgu-check/blob/main/ambiguities/A06-wu-04-pattern-disagrees-between-halves.md),
which are the same question asked in two places: how far does one thing a checker
cannot do propagate? A16 weighed refusing the whole audit over one missing
`effective_from` against skipping one check — *"refusing the entire run
[...] over one absent field is the heavier response, and heavier responses are
what get a tool removed from a pipeline"*. A06 weighed refusing all of
`work-units` over one self-contradicting check and declined, on the grounds that
the module *"is still able to report every other check"*. Both settled on the
smallest unit that stays honest, and a conformance claim takes the same shape.

### 5. A new check makes a prior claim stale, not false

A claim is about the version it names, and stays true of that version for good. If
the module then releases a check, the claim does not become a lie — it becomes a
statement about an older version, which is a different and weaker thing. Nobody
has to withdraw anything, because nobody published anything to withdraw.

**This is the one clause with a live worked example, and it is unflattering.** The
only implementation in existence reproduced every row of every module at `0.2.0`.
`decision-log` then went to `0.3.0`, correcting five `DL-03` rows from `ok` to
`skip`, and that checker still reports `ok` on those five. So it **conforms to
`decision-log` 0.2.0** and **does not conform to `decision-log` 0.3.0**. Both
sentences are true at once, neither is a defect in the checker, and the second is
the designed behaviour rather than a failure of it: propagation here is pull-only
by rule, so an implementation is expected to fall behind until someone pulls. It
is open as `F14` in [findings.md](records/findings.md).

A criterion that could not say this — one under which the only existing checker
conformed by construction — would be a criterion bent around a reference
implementation, which is the risk [work/m9.md](records/work/m9.md) names against
itself and the reason this document was deferred until there was something to test
it on.

One consequence is worth stating plainly, because it surprised this repository.
`decision-log` `0.3.0` was a MINOR, correctly: its
[changelog](../modules/decision-log/CHANGELOG.md) states that a previously clean
adopter newly sees nothing, and that is true. A conformance claim went stale
anyway. [SPEC.md](../SPEC.md#versioning) sizes a bump by what an **adopter** sees,
and an adopter and an implementer are not the same reader.

**That is now answered, and this clause is unchanged by the answer.** Every
`CHANGELOG.md` entry from 2026-08-04 carries a second fixed sentence naming what
an implementer must re-run, so the signal exists — but it exists beside the
version number rather than inside it, and the version number still sizes for the
adopter alone. A claim naming a version stays true of that version, a later
release can still make it stale, and an implementer now reads that from a
sentence instead of inferring it from a digit that was never carrying it.
Entries published before that date carry only the adopter sentence and are not
backfilled, so `F14`'s instance — the one worked example above — remains
something a reader works out from this clause rather than from a changelog.

**Origin.**
[A08](https://github.com/DevOfPie/strucgu-check/blob/main/ambiguities/A08-pinned-version-does-not-match-the-module.md)
again — the pin *"documents intent and reports drift; it does not constrain what
runs"*. `F14` is the instance, not the origin; the question was asked while the
first checker was being built, and the instance arrived afterwards to demonstrate
it.

---

## What a conformance claim cannot cover

Every item here is a place the fixtures cannot reach. They are listed because a
criterion that names only what it proves is the shape of thing that gets quoted
as a guarantee.

| Not covered | Why |
| --- | --- |
| `waived` and its expiry together | **Covered since `triage-rule` 0.5.0, in two halves.** `modules/triage-rule/fixtures/waives-TR-02/` pins the state; `violates-TR-02-expired-deviation/` pins that detection reasserts itself past `review_by`. A claim covering every row now demonstrates all five states. What no single tree can reach is both properties at once — a deviation must carry an expiry, so a tree pinning `waived` is true only until a date, and that one takes `2099-12-31`. The first `waived` anywhere still came from a second repository rather than from a fixture — see [second-repository-walk.md](records/second-repository-walk.md). |
| Almost everything git | Exactly one tree becomes a repository, and only by running the setup block in `modules/decision-log/fixtures/violates-DL-03/SETUP.md`. That `path_exists` additionally requires a **tracked** path inside a repository, that history is read from the audited root and never by walking up, and that `effective_from` is exclusive and compared by committer date are all stated in [SPEC.md](../SPEC.md) and tested by nothing. A checker can get all three wrong and reproduce every row. |
| Refusing to run | The conditions under which an audit **cannot start** — no adoption record, an unparseable one, an inexact pin, a missing module directory, a `forms` module with no `form`, a `history_deletions` check with no `effective_from` — cannot be expressed. `expected.yaml`'s values are the five audit states and none of them means *the run did not happen*. Open as `F5`. |
| Directories below a `dir` role | No fixture tree has a subdirectory, so whether a `dir` role reaches into one is unpinned in both directions. |
| Several link cases | A link to a directory, an anchor on a non-markdown file, and GitHub's `-1` suffix on a duplicate heading are each decided and each untested. |

**Origin.** `waived` from
[A18](https://github.com/DevOfPie/strucgu-check/blob/main/ambiguities/A18-what-a-deviations-scope-does.md),
which found the gap while asking what a deviation's `scope` field does. The git
row from
[A05](https://github.com/DevOfPie/strucgu-check/blob/main/ambiguities/A05-tracked-paths-outside-a-repository.md)
— *"this ambiguity is invisible to anyone who only ever runs the checker against
the fixtures or only ever against a real adopter"* — with
[A04](https://github.com/DevOfPie/strucgu-check/blob/main/ambiguities/A04-which-repository-history-is-read-from.md)
and
[A13](https://github.com/DevOfPie/strucgu-check/blob/main/ambiguities/A13-effective-from-as-a-date.md).
Refusing to run from A08 and A16, which each wanted a tree that could not be
written. Subdirectories from
[A15](https://github.com/DevOfPie/strucgu-check/blob/main/ambiguities/A15-dir-roles-and-subdirectories.md),
link cases from
[A12](https://github.com/DevOfPie/strucgu-check/blob/main/ambiguities/A12-which-link-syntaxes-are-links.md).

### Two conforming checkers can still disagree

They can both reproduce every row and then differ on a real repository, and
neither is wrong. That is not a conformance dispute and there is no arbiter for
one — it is [a check whose fixtures do not pin the boundary](../SPEC.md#ambiguity-is-a-missing-fixture).
[File it](objections.md), and the fixture that settles it becomes part of the
specification, at which point one of the two implementations stops conforming to
the next version and knows why.

**Origin.**
[A07](https://github.com/DevOfPie/strucgu-check/blob/main/ambiguities/A07-aggregating-a-dir-role-into-one-state.md),
which implemented an aggregation rule and then recorded that *"the aggregation
rule this checker implements is **not pinned by any fixture**"*, and A12 and A15,
each of which ends by listing what its reading leaves undetermined.

---

## Saying it

Two subjects use the same verb and they are not the same claim.

| Claim | Subject | Example |
| --- | --- | --- |
| A repository conforms to a **check** | the repository being audited | *this repository conforms to `DL-03`* |
| A checker conforms to a **module at a version** | the implementation | *this checker conforms to `decision-log` 0.3.0* |

Neither is a status anyone confers, and the words *certified*, *certification*
and *compliant* are not used for either — they smuggle back in the thing
[README.md](../README.md#what-this-is-not) refuses, and a repository or a checker
described as one of them has acquired a property rather than reported a result.

A claim worth reading names the module, the version, and how it was produced, so
that a reader can re-run it. `run over every tree in modules/decision-log/fixtures/
at 0.3.0, all rows matched` is a claim. `conformant` is not.

**Origin.** The standing rule in [SPEC.md](../SPEC.md#vocabulary) — the three
words are banned because a grade implies a grader. The two-subject distinction is
here because this file introduces the second subject: until now "conforms to" was
only ever said about a repository and a check.

---

## Verifying it

There is no service to ask. Clone the catalog at the version you care about, run
your checker over every tree in that module's `fixtures/` directory, and compare
against `expected.yaml`. That is the whole of it, it is offline, and it is
available to anyone reading your claim as readily as to you — which is the only
verification this design can offer and the reason it does not need to keep a
record of you.

[auditing.md](auditing.md#verifying-your-implementation) describes the fixture
directory. [SPEC.md](../SPEC.md#fixture-expectations) defines `expected.yaml`.

This repository's own checks against itself are not evidence for any of it, for
the reason [decisions.md](records/decisions.md#self-application-is-dogfooding-not-evidence)
gives: an author unconsciously writes rules they already satisfy. The fixtures
are the evidence, and this document is about what passing them is worth.
