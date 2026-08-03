# 0001 — What this specification does not determine

**Status:** accepted, 2026-08-03
**Verified against:** this repository at `4236869` on `main` — all five modules
at version `0.2.0`, 33 fixture trees, [SPEC.md](../../../SPEC.md),
[adopting.md](../../adopting.md), [auditing.md](../../auditing.md),
[objections.md](../../objections.md), [strucgu.yaml](../../../strucgu.yaml),
[README.md](../../../README.md). Implementation:
[DevOfPie/strucgu-check](https://github.com/DevOfPie/strucgu-check), Python
3.14.4 with PyYAML 6.0.3.
**Run during:** [M10](../work/m10.md).

## Context

This catalog ships no runner, deliberately —
[decisions.md](../decisions.md#there-is-no-runner-and-that-is-the-largest-single-decision-here).
[SPEC.md](../../../SPEC.md) is therefore "the only thing that makes two
independent implementations agree", and the question it cannot answer about
itself is whether it succeeds: an author cannot find the gaps in their own
specification, because the gaps are exactly where they knew what they meant.

[M10](../work/m10.md) commissioned the first independent checker to find out.
This record is what it found. The checker covers **all five modules and every
check**, and reproduced every row of every module's `fixtures/expected.yaml`
across all 33 trees as they stood at `4236869`. That was the easy half. The
useful half is the 18 places where this specification did not determine what the
checker should do, each recorded before it was resolved, in the checker
repository's
[`ambiguities/`](https://github.com/DevOfPie/strucgu-check/tree/main/ambiguities).

Two constraints shaped the method and bound what this is worth. Both are
[M10](../work/m10.md)'s and are argued in
[decisions.md](../decisions.md#the-first-checker-is-whippys-and-its-independence-is-partial).

**The reading restriction.** `docs/records/` was not read — not this log's
parent, not the decision log that argues the design, not the findings queue, not
the work record that commissioned the checker. Every reading below was taken
from the specification and the fixtures alone. This is attested, not verifiable:
a kept rule and a broken one leave the same trace in a working checker.

**No questions were asked.** [M10](../work/m10.md) declines them, on the grounds
that a question answered privately is a defect erased rather than found. So every
ambiguity here is one a real second implementer would have hit, rather than one
that survived only because nobody thought to ask.

The restriction had one concrete cost worth naming: **this repository could not
be audited by its own checker.** [strucgu.yaml](../../../strucgu.yaml) maps every
role into `docs/records/`, so the most obvious end-to-end test — run the checker
over the catalog that defines it — was unavailable. A synthetic adopter was built
instead
([`conformance/example/`](https://github.com/DevOfPie/strucgu-check/tree/main/conformance/example)),
which covers the states no fixture reaches but is not the same evidence.

## Findings

Eighteen. Each links to its full record; the summary below is what a reader
deciding where to spend attention needs.

### The specification contradicts its own fixtures — 6

These are the serious ones. In each, a checker following the prose produces a
different answer from a checker following `expected.yaml`, and both are
defensible from what is written.

| | What the prose says | What the fixtures say |
| --- | --- | --- |
| [A01](https://github.com/DevOfPie/strucgu-check/blob/main/ambiguities/A01-multi-role-checks-and-partial-readability.md) | A check bound to a role whose `path_exists` failed skips | `WU-07` and `DL-06` evaluate over the roles that did resolve |
| [A02](https://github.com/DevOfPie/strucgu-check/blob/main/ambiguities/A02-path-exists-on-a-dir-role.md) | A `dir` role needs "at least one file" surviving exclusions | `violates-IN-01`'s `.gitkeep` does not count |
| [A03](https://github.com/DevOfPie/strucgu-check/blob/main/ambiguities/A03-history-deletions-with-no-history.md) | An unreadable target reports `skip`, never `ok` | Five trees with no history report `DL-03: ok` |
| [A05](https://github.com/DevOfPie/strucgu-check/blob/main/ambiguities/A05-tracked-paths-outside-a-repository.md) | `path_exists` requires a **tracked** path | No fixture tree is a repository, and `satisfies` is `ok` |
| [A06](https://github.com/DevOfPie/strucgu-check/blob/main/ambiguities/A06-wu-04-pattern-disagrees-between-halves.md) | `module.md` wins over `module.yaml` | `WU-04`'s prose pattern is HTML-escaped and matches nothing |
| [A08](https://github.com/DevOfPie/strucgu-check/blob/main/ambiguities/A08-pinned-version-does-not-match-the-module.md) | The exact pin stops upstream publishing new findings | Every tree pins `0.1.0` against modules at `0.2.0` |

**[A03](https://github.com/DevOfPie/strucgu-check/blob/main/ambiguities/A03-history-deletions-with-no-history.md)
is the one to read.** [SPEC.md](../../../SPEC.md) and
[auditing.md](../../auditing.md) between them say four times that folding `skip`
into `ok` is the failure that matters most — "it converts 'I did not look' into
'I looked and it was fine', and nothing downstream can tell the difference".
Five `decision-log` fixtures then required exactly that fold for `DL-03`. The
checker did it, to match, and recorded that it believed the fixtures were wrong
rather than the prose. It is the only reading in this document the implementer
argued against their own implementation.

**[A06](https://github.com/DevOfPie/strucgu-check/blob/main/ambiguities/A06-wu-04-pattern-disagrees-between-halves.md)
is a transcription defect with teeth.**
[modules/work-units/module.md](../../../modules/work-units/module.md) carried
`&lt;[A-Za-z][A-Za-z ]*&gt;` where
[module.yaml](../../../modules/work-units/module.yaml) carries
`<[A-Za-z][A-Za-z ]*>`. Verified with `od -c`, because GitHub renders the
entities as the characters and the two halves looked identical on the website.
The normative half's pattern cannot match `<title>`, which is what
`violates-WU-04` exists to be caught by. The checker can be run either way:
`--normative-prose` follows `module.md` and reported `WU-04: ok` where
`expected.yaml` said `finding`.

### The specification is silent — 8

Places with no answer at all, where two implementations would simply differ:
[A04](https://github.com/DevOfPie/strucgu-check/blob/main/ambiguities/A04-which-repository-history-is-read-from.md)
which repository history is read from (the fixture trees sit *inside* this
repository, so walking up to find `.git` audits the wrong history and reports
findings against this repository's own commits);
[A07](https://github.com/DevOfPie/strucgu-check/blob/main/ambiguities/A07-aggregating-a-dir-role-into-one-state.md)
how per-file results over a `dir` role become one state;
[A10](https://github.com/DevOfPie/strucgu-check/blob/main/ambiguities/A10-where-the-exclude-list-lives.md)
whether `exclude` lives on the module or the role, and how its globs match;
[A11](https://github.com/DevOfPie/strucgu-check/blob/main/ambiguities/A11-judgment-entries-over-absent-roles.md)
what a judgment entry does when the document it names is absent;
[A12](https://github.com/DevOfPie/strucgu-check/blob/main/ambiguities/A12-which-link-syntaxes-are-links.md)
which markdown constructs count as a link;
[A13](https://github.com/DevOfPie/strucgu-check/blob/main/ambiguities/A13-effective-from-as-a-date.md)
whether `effective_from` is author or committer date, and whether the boundary is
inclusive;
[A15](https://github.com/DevOfPie/strucgu-check/blob/main/ambiguities/A15-dir-roles-and-subdirectories.md)
whether a `dir` role reaches into subdirectories;
[A18](https://github.com/DevOfPie/strucgu-check/blob/main/ambiguities/A18-what-a-deviations-scope-does.md)
what a deviation's required `scope` field does.

**[A18](https://github.com/DevOfPie/strucgu-check/blob/main/ambiguities/A18-what-a-deviations-scope-does.md)
was found by an adversarial review of the finished checker, not by building it**,
and it is the one place that implementation did something no reading of the
specification supports: it ignored `scope` entirely, so a deviation accepted for
`doc/adr/**` waived a finding anywhere in the repository. Recorded, then fixed.
That it survived the fixtures is unsurprising — no fixture tree carries a
`deviations` block, so `waived` is the one of the five states this catalog never
exercises.

[A09](https://github.com/DevOfPie/strucgu-check/blob/main/ambiguities/A09-pattern-present-all-or-any.md)
is the cheapest to fix and the easiest to get wrong twice: three `module.md`
files said "Any one pattern matching is sufficient" where
[SPEC.md](../../../SPEC.md) says every listed pattern must match. They coincided
because each of those checks carries a single alternation — but the sentence
generalises wrongly, and an implementer carrying it to `WU-06` or `IN-02` gets
those fixtures wrong.

### Two documents disagree with each other — 1

[A16](https://github.com/DevOfPie/strucgu-check/blob/main/ambiguities/A16-a-history-check-with-no-effective-from.md):
[SPEC.md](../../../SPEC.md) makes `effective_from` required when a
`history_deletions` check is adopted; [auditing.md](../../auditing.md)'s closed
list of reasons a run cannot start did not include it. Both readings reproduce
all 33 fixtures, so nothing catches the difference.

### The fixtures cannot express what is needed — 3

[A14](https://github.com/DevOfPie/strucgu-check/blob/main/ambiguities/A14-rules-stated-and-never-pinned.md)
is the finding the implementer did not expect and rates highest.

It was found by breaking the checker on purpose, one rule at a time, and
re-running all 33 trees. A rule the fixtures pin produces mismatches when broken;
a rule they do not pin produces a clean run from a checker that is now wrong.

[`conformance/mutations.py`](https://github.com/DevOfPie/strucgu-check/blob/main/conformance/mutations.py)
runs nine such breakages. **Against the catalog at `4236869`, five went
unnoticed** — the suite reported a clean run from a checker that was measurably
wrong — and the five included the two rules [SPEC.md](../../../SPEC.md) argues
for hardest:

- **"Code is not scanned for links."** Given its own paragraph and a
  discovered-the-hard-way provenance: "Found by running the check over this
  repository, twice [...] A checker without both rules reports findings against
  regular expressions, including the ones in the specification that told it what
  to do." No fixture contained a link-shaped sequence inside a fence.
- **"Runs of spaces are not collapsed."** Named explicitly as "the obvious
  implementation and it is wrong; it rejects correct anchors". Every anchor in
  every fixture targeted a heading with single spaces.

Both rules were learned from a real failure — see
[decisions.md](../decisions.md#the-code-fence-rule-was-wrong-the-first-time).
Both are written down as warnings. Neither had a tree behind it, so an
implementation could ignore both and still present a clean conformance run.

[A17](https://github.com/DevOfPie/strucgu-check/blob/main/ambiguities/A17-one-violating-tree-per-check.md)
is why they stayed unpinned: [SPEC.md](../../../SPEC.md) fixed `fixtures/` at
"one `violates-<CHECK-ID>/` tree per check", in a table introduced as listing
"exactly what that row lists inside it". A check with two boundaries worth
pinning could not have both pinned.

## Decisions

1. **The fixtures are the real specification, and they are ahead of the prose in
   six places and behind it in three.** Where they disagreed, the checker
   followed the fixtures — [M10](../work/m10.md) required reproducing them — and
   recorded the disagreement rather than resolving it silently. Every one of the
   six is a decision for the owner, not a wording fix.

2. **A rule a specification bothers to argue for is a rule it learned by being
   wrong, and those are the ones most worth pinning.** The two most heavily
   argued matching rules in [SPEC.md](../../../SPEC.md) were both untested. The
   correlation is not a coincidence: a rule that felt obvious enough to need no
   argument also felt obvious enough to need no fixture, and a rule that needed
   an argument was argued instead of demonstrated.

3. **Mutation testing is what tells a fixture suite from a fixture collection.**
   Running the suite says an implementation agrees with it. Breaking the
   implementation and re-running says whether the suite would have noticed. The
   second question is the one a specification with no reference implementation
   actually needs answered, and it cost one afternoon and nine deliberate bugs.

4. **`expected.md` is normative-adjacent prose that nothing verifies, and it has
   already drifted.**
   [modules/triage-rule/fixtures/expected.md](../../../modules/triage-rule/fixtures/expected.md)
   states "Four `judgment` lines" for a module declaring two.
   [SPEC.md](../../../SPEC.md) says the two expectation files must agree and that
   a disagreement is a defect to report; nothing reports this one, because
   nothing reads `expected.md`. Independently found and already open as `F3` in
   [findings.md](../findings.md).

5. **A checker cannot honour an exact version pin, and should stop implying it
   can.** Nothing in a module lets a checker evaluate a version other than the
   one in the working tree, so a pin that is behind the catalog does not withhold
   newly added checks — it prints a notice
   ([A08](https://github.com/DevOfPie/strucgu-check/blob/main/ambiguities/A08-pinned-version-does-not-match-the-module.md)).
   The pin documents intent and reports drift. [SPEC.md](../../../SPEC.md)
   presented it as the mechanism preventing enforcement-by-release, and it is not
   one.

6. **The reading restriction was worth its cost.** It removed the most convenient
   end-to-end test and it is the reason these findings are findings — every one
   came from the specification failing to say something, rather than from the
   author saying it in a channel a second implementer would not have.

## What this repository took

Recorded here because a record of an investigation whose conclusions were
partly declined, without saying which, is a record of a conversation that did not
happen. The reasoning is in
[decisions.md](../decisions.md#2026-08-03--m10-the-first-checker-and-what-it-could-not-determine);
this is the list.

- **Taken as proposed:** A01, A02, A04, A05, A07, A09, A10, A11, A13, A15, A16,
  A17, and the fixture half of A14 — three new trees and two additions to
  existing `satisfies/` trees. `fixtures/` now permits more than one violating
  tree per check, which A14's fixtures needed.
- **Inverted:** A03. The owner ruled the fixtures wrong rather than the prose.
  `DL-03` now reports `skip` where no history is readable, which cost five
  expectation rows and left [SPEC.md](../../../SPEC.md) as it was.
- **Taken in part:** A06. The escaped pattern in
  [work-units/module.md](../../../modules/work-units/module.md) is repaired so
  the two halves agree. The general rule the record proposed — what state a
  check reports while its halves disagree — was not taken, so that question is
  still open.
- **Not taken:** the correction to `F3`, which is an out-of-spec finding and
  needs its own review before anything touches it. The wrong count is still in
  [triage-rule's expected.md](../../../modules/triage-rule/fixtures/expected.md).

## Reproducing

The checker, its ambiguity log, and the original of this document are in
[DevOfPie/strucgu-check](https://github.com/DevOfPie/strucgu-check). Everything
below is self-contained apart from a checkout of this repository.

```sh
git clone https://github.com/DevOfPie/StrucGu.git
git clone https://github.com/DevOfPie/strucgu-check.git
cd strucgu-check

# Every fixture tree against the catalog as it stands.
python3 conformance/run_fixtures.py --catalog ../StrucGu

# The rules the catalog's own fixtures do not pin, plus waived, expired
# deviations, unmapped roles and cannot-run.
PYTHONPATH=. python3 -m unittest discover -s tests

# A06 made concrete: the same tree, evaluated from the normative half. Reports
# WU-04: ok before the escaped pattern was repaired, and finding after.
PYTHONPATH=. python3 -m strucgu_check \
  ../StrucGu/modules/work-units/fixtures/violates-WU-04 \
  --catalog ../StrucGu --normative-prose

# Which breakages the fixtures catch. Nine deliberate bugs, one rule each.
python3 conformance/mutations.py --catalog ../StrucGu
```

`violates-DL-03` is the one tree that is not self-contained: `DL-03` inspects git
history and a fixture cannot carry a nested repository. The harness copies it to
a scratch directory and runs its `SETUP.md` block there. Nothing under the
catalog is written to, by the harness or the checker.

**Two numbers move as the catalog changes, and both were measured rather than
claimed.** Against `4236869` the suite was 33 trees and 305 rows, and five of the
nine mutations went unnoticed. With the fixtures from A14 and A17 taken it is 36
trees and 337 rows, and no mutation goes unnoticed — which is the evidence that
the added fixtures do the job they were written for.

`run_fixtures.py` reports five mismatches against the catalog as it now stands,
all of them `DL-03: expected skip, got ok`. That is the A03 inversion above: the
checker was built to reproduce the fixtures and the fixtures moved. It is a
disagreement between this repository and one implementation of it, recorded
rather than resolved by editing either side quietly, and it is exactly the kind
of thing the [objection channel](../../objections.md) is for.

**The artifacts that were deliberately not kept:** none. Every number in this
document comes from a command above.
