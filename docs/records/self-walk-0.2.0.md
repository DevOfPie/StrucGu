# Self-walk — 0.2.0

Every check in all five modules, applied to this repository through
[strucgu.yaml](../../strucgu.yaml), on 2026-08-04. It sits inside the release
walk [triage.md](triage.md) requires before a tag, so the gates that walk runs
first are recorded here too.

**A second file, not a rewrite.** [self-walk.md](self-walk.md) is the walk at
`0.1.0` and is left exactly as it was. The diff between the two is the first
thing in this repository that shows movement, and overwriting the first walk
would have destroyed it to save a filename.

**What this is worth.** A little more than the first walk, and still not much.
The same party wrote the checks, the rules and the repository, and
[self-application is dogfooding rather than evidence](decisions.md#self-application-is-dogfooding-not-evidence).
Two things changed since `0.1.0`: an implementation now exists, so every state
below was produced by hand *and* by a program that disagrees with nothing, and
the repository has a year less of the benefit of the doubt because there is now
something to compare against. The evidence that these checks detect anything is
still the 37 fixture trees under `modules/*/fixtures/`.

---

## Step 1 — every commit gate, over the whole repository

[triage.md](triage.md) "Before a release is tagged" runs the *Before completing
a commit* table over the whole repository rather than over changed files. There
are no `make` targets; StrucGu ships no code and every gate below was run by
hand.

| Gate | Output |
| --- | --- |
| Links | 123 tracked `.md`, 681 relative links outside the fixture trees, **0 failures**. 59 links inside the fixture trees, **7 deliberate failures**, unchanged from `0.1.0` and each one the thing its tree exists to violate. |
| Roles | 28 checks across five modules. Every `in:` names a role its own module declares, except `triage.destination-is-real` and `TR-03`, which name `findings` across a module boundary — legitimate, and the subject of `F8`. Every role the five modules declare is mapped in [strucgu.yaml](../../strucgu.yaml); **none is left `~`**, which is the change this walk is about. |
| Prose and manifest | Every check id, obligation id, role id, judgment id and every `patterns:` and `heading:` string in the five `module.yaml` files appears verbatim in the matching `module.md`. No disagreement. `module.md` deliberately carries no version; the version lives in the manifest and the changelog. |
| Fixtures | 37 trees. Every one of the 28 checks has at least one `violates-` tree and a satisfying tree, and `expected.md` names every check id. `expected.yaml` covers all 37. |
| Vocabulary | *Certified*, *certification* and *compliant* occur 23 times across thirteen lines, every one of them either a refusal ([README.md](../../README.md), [conformance.md](../conformance.md)) or the rule that bans them ([SPEC.md](../../SPEC.md), [triage.md](triage.md)). None is used as a repository status. |
| Neutrality | Nothing under `modules/` names a language, package manager, build tool or file extension. The only matches are the English words *make* and *go*. |
| Scope | One work unit, `M13`. |

**The conformance harness, as a second reading of the fixtures gate.**
[strucgu-check](https://github.com/DevOfPie/strucgu-check)'s harness over this
catalog reports `37 trees, 344 expectation rows, 5 mismatch(es)`, all of the
form `DL-03: expected skip, got ok`. The expectations are right and the
implementation is behind — that is `F14`, it is open, and it is not this walk's
to close.

## Step 2 — every check, by hand

The states below were derived by reading each check against the mapped role and
then compared against
[strucgu-check](https://github.com/DevOfPie/strucgu-check)'s output. They agree
everywhere. That agreement is worth less than it sounds: the same party wrote
the specification the checker was written from, and the checker's own
[ambiguity log](investigations/0001-what-the-specification-does-not-determine.md)
records eighteen places where it had to choose.

Each module is pinned at `0.1.0` in [strucgu.yaml](../../strucgu.yaml) and every
module is now ahead of its pin, so every section below also emits a drift
notice. That is the pin working as
[SPEC.md](../../SPEC.md#versioning) describes — it documents what was agreed to
and reports drift; it does not constrain what runs.

### triage-rule 0.4.0 — pinned 0.1.0

`triage_doc` → [triage.md](triage.md)

| | Check | |
| --- | --- | --- |
| `note` | | `triage-rule 0.4.0 is newer than the pinned 0.1.0` |
| `ok` | `TR-01` | present |
| `ok` | `TR-02` | *In spec* and *Out of spec*, Vocabulary table |
| `ok` | `TR-03` | links to [findings.md](findings.md) |
| `ok` | `TR-04` | Precedence paragraph — "the conflict is a bug — report it, do not pick" |
| `ok` | `TR-05` | all links and anchors resolve |

### decision-log 0.3.0 — pinned 0.1.0, form `single-log`

`decision_log` → [decisions.md](decisions.md) · `decision_index` → the same file

| | Check | |
| --- | --- | --- |
| `note` | | `decision-log 0.3.0 is newer than the pinned 0.1.0` |
| `ok` | `DL-01` | present |
| `ok` | `DL-02` | dated section headings |
| **`finding`** | `DL-03` | `e132646 "Correct the plan's decisions by appending, and redact by removing" removed 4 line(s) (and 1 more), after 2026-07-31` |
| `ok` | `DL-04` | states append-only in its preamble |
| `ok` | `DL-05` | passes because both roles map to one file — the documented weakness, judged below |
| `ok` | `DL-06` | all links and anchors resolve |

**`DL-03` is the one state that moved from `ok` to a finding, and it moved for
a good reason.** At `0.1.0` there was no history after `effective_from` and the
`ok` said nothing. There is history now, and one commit in it removed lines
from the decision log — a redaction, argued in
[decisions.md](decisions.md#enumerating-a-private-repositorys-record-shapes-was-itself-the-leak).
The check cannot tell a justified redaction from an entry edited away, which is
the check working as specified and is why `decision-log`'s own `module.md`
documents `DL-03` as reported for a look rather than as a defect.

**It is recorded, not disposed of.** This is `F6` in
[findings.md](findings.md), open and unreviewed since `M10`. The two available
dispositions — this repository recording its first deviation, or accepting the
finding on every run forever — are both the owner's, and taking either inside
this work unit would be deciding an open row because it was inconvenient to
have one during a release. The release therefore ships with a repository that
reports a finding against itself.

### findings-queue 0.3.0 — pinned 0.1.0

`findings` → [findings.md](findings.md) · prerequisite `triage-rule` adopted

| | Check | |
| --- | --- | --- |
| `note` | | `findings-queue 0.3.0 is newer than the pinned 0.1.0` |
| `ok` | `FQ-01` | present |
| `ok` | `FQ-02` | `Evidence` column |
| `ok` | `FQ-03` | `Reviewed` column |
| `ok` | `FQ-04` | states rows are unscheduled and reviewed individually |
| `ok` | `FQ-05` | links to [triage.md](triage.md) |
| `ok` | `FQ-06` | all links and anchors resolve |

### work-units 0.2.1 — pinned 0.1.0

`unit_dir` → [work/](work/) · `unit_template` → [work/_template.md](work/_template.md)
· `unit_index` → [work/README.md](work/README.md)

| | Check | |
| --- | --- | --- |
| `note` | | `work-units 0.2.1 is newer than the pinned 0.1.0` |
| `ok` | `WU-01` | present |
| `ok` | `WU-02` | template has Done means and Risks |
| `ok` | `WU-03` | all thirteen records have both |
| `ok` | `WU-04` | no angle-bracketed placeholder and no `TODO`/`TBD`/`FIXME` in any of the thirteen |
| `ok` | `WU-05` | present |
| `ok` | `WU-06` | template asks for Depends on and Discharges |
| `ok` | `WU-07` | all links and anchors resolve |

`WU-04` is walked here against the **repaired** pattern — `<[A-Za-z][A-Za-z ]*>`,
the one `module.yaml` has carried since the first release and `module.md` now
carries too. At `0.1.0` this walk was run against the escaped transcription and
could not have failed. Thirteen records were read for it rather than seven.

### investigations 0.2.1 — pinned 0.1.0

`investigations` → [investigations/](investigations/)

| | Check | |
| --- | --- | --- |
| `note` | | `investigations 0.2.1 is newer than the pinned 0.1.0` |
| `ok` | `IN-01` | a markdown file survives the role's exclusions |
| `ok` | `IN-02` | Context, Findings, Decisions, Reproducing |
| `ok` | `IN-03` | `**Status:** accepted, 2026-08-03` |
| `ok` | `IN-04` | all links and anchors resolve |

## What these four `ok`s cost, stated rather than banked

At `0.1.0` these four reported `skip`, because the `investigations` role was
deliberately unmapped and the module's first obligation is conditional. The
first self-walk called them **the point of that walk**. They are `ok` now
because [M10](work/m10.md)'s ambiguity log is a real investigation that outgrew
a decision entry and the role is
[mapped for that reason](decisions.md#the-ambiguity-log-is-the-investigation-that-outgrew-a-decision-entry),
not because anything was invented to fill it.

**The second walk exercises `skip` nowhere.** Those four were the only exercise
of the `skip` path and of a conditional obligation anywhere in this repository,
and the [second repository's walk](second-repository-walk.md) produced no `skip`
either — it declined the two modules that would have produced them, which is
the honest answer and the same loss. So the catalog's most important escape
hatch, the one that keeps "I did not look" from being reported as "I looked and
it was fine", now has **no live demonstration in any recorded output at all.**

Coverage of it survives only in the fixture trees, where `skip` is an expected
value on 23 rows across all five modules. That is coverage of the state, by
construction, in trees written by the same party. It is not a demonstration
that a real repository ever produces one.

A summary reading `0 skipped` therefore looks better than `4 skipped` and is
worse. Recorded here rather than in a footnote, because the point of running
this walk twice is to see what moved, and this moved backwards.

## M11's deviation from the verifiability gate, recorded at the gate

[triage.md](triage.md)'s documentation pass requires that **every documented
claim be verifiable by a reader who does not trust you.**
[second-repository-walk.md](second-repository-walk.md) is not. The repository it
audits is private and unnamed, every path, filename and quoted line is
`[redacted]`, and a reader has nothing to check the states against.

**This walk does not pass over it.** It is a knowing deviation, confined to that
record, argued in
[decisions.md](decisions.md#a-redacted-audit-is-weaker-evidence-than-an-open-one-and-the-release-gate-is-deviated-from-knowingly),
and declared in the file's own title and first paragraph rather than discovered.
The alternative was not publishing an unredacted audit — that was never
available — but publishing nothing, and the trade is stated where the results
are. The rule for a conflict between governing documents is to report it rather
than pick, and this is the report: the release gate is not met by that file, and
the release ships anyway with the failure named.

Nothing else in this release deviates from the gate. Every other claim here
points at a file in this repository or at a public one.

## Step 3 — did the walk trigger work?

**No.** [triage.md](triage.md) requires repeating from step 1 if the walk
triggers work, where work is anything beyond spelling, phrasing, formatting or
docs wording.

- `DL-03`'s finding is `F6`, open, unreviewed, and its disposition is the
  owner's. Recording it changes nothing in the tree.
- The five harness mismatches are `F14`, open, and live in another repository.
- `triage.destination-is-real` is annotated `[unresolved role: findings —
  nothing to read]` while `findings` is mapped and `FQ-01` reports `ok` in the
  same run. That is `F8`, open, and a defect in the implementation and the
  specification's silence rather than in this repository.
- **`decisions.md`'s index carries 51 rows against 52 entries.** Found by the
  judgment pass below, new, and nobody's defect but this repository's. Filed as
  `F17`.
- **Every module pin in [strucgu.yaml](../../strucgu.yaml) is behind**, and this
  walk is the review that would justify moving them. Filed as `F18`.

Nothing in that list is required by this work unit's own claim, so nothing was
fixed and step 1 was not repeated. The two new rows are the release gate
producing findings, which is what
[triage.md](triage.md) says to do with anything out of spec — fixing them here
because they surfaced during a release is the drift the queue exists to stop.
Everything written in this release after the walk is documentation wording,
which [triage.md](triage.md) names explicitly as not re-triggering.

---

## Summary

```
28 checks: 27 ok, 1 finding, 0 skipped, 0 waived.
17 for judgment.
```

Against the walk at `0.1.0` — `24 ok, 0 findings, 4 skipped, 17 for judgment`:

| | 0.1.0 | 0.2.0 | |
| --- | --- | --- | --- |
| `ok` | 24 | 27 | the four `IN-*` checks stopped skipping, and `DL-03` stopped passing |
| `finding` | 0 | 1 | `DL-03`, on real history that did not exist before |
| `skip` | 4 | **0** | the loss, not the improvement |
| `waived` | 0 | 0 | still exercised only in another repository |
| judgment | 17 | 17 | unchanged |

Not a grade, and not progress. One line moved from "I could not tell" to a real
answer and four moved the other way, from "I could not tell" to an answer that
is no longer demonstrated anywhere.

## Judgment

The 17 `judgment` entries were read again. Three produced something worth
recording; the rest are unchanged from the first walk and are listed with what
was read.

**`decision-log.index-exists-in-substance`** — still passes for free, because
both roles map to one file under `single-log`, and reading it directly is what
the entry is for. **The index is incomplete.** It is exactly one row short of
its entries — 51 against 52 as this walk was run, 55 against 56 once this unit's
four appends land. *The orchestrator that landed M8 is disqualified from
implementing M10* was appended on 2026-08-03 without its row, so one entry is
unreachable from the index and `DL-05` cannot see it. That is a real defect in the one place the check is
documented as blind, found by the judgment channel rather than by a check, which
is the argument for having the channel. It is filed as `F17` rather than
repaired here — see [step 3](#step-3--did-the-walk-trigger-work). The
[second repository's walk](second-repository-walk.md) is why this was re-read
rather than answered from the first walk: there the same entry caught a log of
five hundred lines with no index at all. Here it caught a hole one row wide, at
the second time of asking.

**`work-units.risks-considered`** — thirteen records now rather than seven, and
the recurring risk the first walk named has not gone away: four records name
some form of *this catalog is generalised from a single repository by the person
who will also be its first adopter*, and [m13.md](work/m13.md) names the same
risk in a sharper form — that this phase produces enough evidence to be read as
maturity. Nothing here says "Low". Nothing to report, and the recurrence is
still information.

**`findings.queue-is-reviewed`** — the entry's stated failure mode is a queue
nobody returns to, which "looks identical to a healthy one from the outside".
At the moment of the walk this queue had **fourteen open rows and not one
marked reviewed**. Two rows have closed in its lifetime, both in `M12`; `F7`
closes with this release and two more open with it. The entry's
`do_not_report` clause covers a short queue, and fourteen is not short. **This
is the closest the judgment channel has come to a finding against this
repository**, and it is not raised as one because the disposition is per-row
owner review, which is exactly what these rows are waiting for. It is recorded
so the next walk can see whether the number moved.

The remaining fourteen were read against their `do_not_report` clauses and
produced nothing worth a row in [findings.md](findings.md).

## What this walk did not exercise, and what it cannot say

- **`skip` and the conditional obligation.** Nowhere, for the first time.
  Stated above at length because it is the one thing this walk lost.
- **`waived`.** Exercised only in the [second repository](second-repository-walk.md),
  whose record a reader cannot verify. This repository still
  [records no deviation of its own](decisions.md#this-repository-records-no-deviation-of-its-own).
- **Whether anyone follows a process.** Nothing here observes that, and nothing
  in the catalog can. Every state above is a statement about the shape of a
  record.
- **Correctness of the checker that agreed with it.** Agreement between a hand
  walk and an implementation written from the same specification by parties
  sharing a lineage is not independent confirmation. What it rules out is a
  transcription slip, which is not nothing and is not much.

## Open findings

Fifteen rows in [findings.md](findings.md) are open and unreviewed after this
release: `F3` to `F6`, `F8` to `F16`, and the two this walk added, `F17` and
`F18`. `F7` closes, and only `F7`, because the owner settled what a breaking
change means below `1.0.0` — see
[decisions.md](decisions.md#below-100-a-breaking-change-collapses-into-the-minor-digit).
`F3` is knowingly wrong and stays that way, unreviewed like the rest.

Of the fifteen, exactly one — `F6` — was produced by a check. `F17` was
produced by the judgment channel. The other thirteen are observations no check
and no judgment entry here can see, which is itself a fact about the coverage,
and the same fact the first walk recorded with two rows instead of fifteen.
