# Second-repository walk — 0.3.0, redacted

**This record is redacted.** The repository audited here is private and is not
named. Every path, every filename, and every quoted line from its documents has
been removed and replaced with `[redacted]`. What remains is the catalog's own
vocabulary — module ids, check ids, role ids, and the five output states — plus
the checker's own text.

That is a deliberate deviation from [triage.md](triage.md)'s release gate, which
requires every documented claim to be verifiable by a reader who does not trust
you. **A reader cannot verify this file.** The deviation is confined to this
record, it is argued in
[decisions.md](decisions.md#the-second-repository-is-private-and-it-tests-re-application-rather-than-generality),
and [work/m13.md](work/m13.md) records it at the gate rather than letting the
release walk pass silently over it. The rule for a conflict between governing
documents is to report it, not to pick, and this is the report.

**What this walk is worth.** Less than a first reading suggests. The repository
audited shares a convention lineage with
[LinkCtrl](https://github.com/DevOfPie/LinkCtrl), which is where these modules
came from — it imported that repository's conventions deliberately and on its own
record. **A clean map is the expected outcome here and is not evidence that these
conventions generalise.** It is evidence that an extraction survives
re-application inside the lineage it was extracted from, which is a different and
smaller claim. The generality question needs a repository built by someone who has
never read LinkCtrl, and this walk does not answer it. **No objection would have
been the uninformative case, not the reassuring one** — a clean run is what both
an honest audit and an audit that looked away would produce.

**Run by** [DevOfPie/strucgu-check](https://github.com/DevOfPie/strucgu-check),
the implementation written in [M10](work/m10.md), against the catalog as it stands
at that milestone. Not by hand: unlike [self-walk.md](self-walk.md), the states
below are a program's output rather than an author's reading of his own rules.
That is the one respect in which this walk is stronger evidence than the
self-walk, and it is offset by everything above.

---

## What was adopted

| Module | Version | | |
| --- | --- | --- | --- |
| [triage-rule](../../modules/triage-rule/) | `0.3.0` | adopted | `triage_doc` mapped |
| [decision-log](../../modules/decision-log/) | `0.3.0` | adopted, form `single-log` | `decision_log` and `decision_index` mapped to one path |
| [findings-queue](../../modules/findings-queue/) | `0.3.0` | adopted | `findings` mapped |
| [work-units](../../modules/work-units/) | — | **not adopted** | Its `applies_when` is not met. That repository's records of intent describe work nobody has committed to, which is a different claim from a unit of work. Adopting with three `~` roles would assert the module applies and has not been got round to. |
| [investigations](../../modules/investigations/) | — | **not adopted** | Its `applies_when` asks for an investigation that outgrew a decision entry. That repository states the opposite position deliberately in its own scope contract. The obligation is conditional and its condition is unmet by choice. |

**No role is mapped at a path that did not already exist.** Nothing was renamed,
moved or created to make a role fill. Two roles that a first pass might have
filled were left unfilled by declining the modules outright, which is the honest
form of "this does not apply" — see [adopting.md](../adopting.md) step 4.

## The run

Three runs. The first is the tree as it was found; the second is after the three
fixes below; the third is after the objection was declined and the deviation
recorded. All three are kept, because a record that shows only the last is a
record of the disposals rather than of the audit.

### As found

| | Check | State |
| --- | --- | --- |
| triage-rule | `TR-01` `TR-02` `TR-04` `TR-05` | `ok` |
| | `TR-03` | **`finding`** — `no link resolves to role findings at [redacted]` |
| decision-log | `DL-01` `DL-02` `DL-04` `DL-05` `DL-06` | `ok` |
| | `DL-03` | `ok` — `since [redacted]`; see the limit below |
| findings-queue | `FQ-01` `FQ-05` `FQ-06` | `ok` |
| | `FQ-02` | **`finding`** — `nothing matches /\|[^\|]*evidence[^\|]*\|/` |
| | `FQ-03` | **`finding`** — `nothing matches /\|[^\|]*(reviewed\|review\|approved\|status\|state)[^\|]*\|/` |
| | `FQ-04` | **`finding`** — `nothing matches /not scheduled\|nothing here is scheduled\|not a commitment\|report, not a\|per item\|individually/` |

`Total: 13 ok, 4 finding, 0 skipped, 0 waived, 10 for judgment.`

### After the fixes, objection undisposed

| | Check | State |
| --- | --- | --- |
| triage-rule | all five | `ok` |
| decision-log | all six | `ok` |
| findings-queue | `FQ-01` `FQ-04` `FQ-05` `FQ-06` | `ok` |
| | `FQ-02` `FQ-03` | **`finding`**, left standing — objection filed, see below |

`Total: 15 ok, 2 finding, 0 skipped, 0 waived, 10 for judgment.`

This state was committed to nothing and is recorded because it is the honest
shape of an argument in flight. A deviation written here would have reported both
checks `waived` with a reason, and the reason was the objection's outcome, which
had not been decided.

### After the decline

| | Check | State |
| --- | --- | --- |
| triage-rule | all five | `ok` |
| decision-log | all six | `ok` |
| findings-queue | `FQ-01` `FQ-04` `FQ-05` `FQ-06` | `ok` |
| | `FQ-02` `FQ-03` | **`waived`** — deviation accepted 2026-08-03, review by 2027-02-03, reason echoed in full on every run |

`Total: 15 ok, 0 finding, 0 skipped, 2 waived, 10 for judgment.`

**This is the catalog's first `waived` anywhere.** The deviation mechanism has
been specified across three documents since `0.1.0` and
[CHANGELOG.md](../../CHANGELOG.md) has described it as untested by use since then
— this repository has no genuine deviation of its own and
[declined to invent one](decisions.md#this-repository-records-no-deviation-of-its-own).
It is now exercised, by a real disagreement, on a repository that reached it
through the objection channel rather than by reaching for it first. That
ordering — finding, objection, decline, deviation — is the one the documents
describe and it had never been walked end to end.

**No check reported `skip` in any of the three runs.** That zero is information.
Every adopted role resolved, so nothing here is a pass that is really an absence,
and the two modules that would have produced skips were declined instead of
half-adopted. The escape hatch this catalog leans on hardest is exercised nowhere
in this run, and nowhere in this repository's own record since
[M10](work/m10.md).

## Every finding, and how it was disposed of

Three disposals exist — fixed, waived with a reason in that repository's own
adoption record, or filed as an objection. "Not really a problem" is not one of
them.

| Check | Disposal | |
| --- | --- | --- |
| `TR-03` | **fixed** | The process document named its out-of-scope destination in fenced blocks only, so no link resolved to it. This is the defect this catalog was extracted after finding in LinkCtrl, reproduced independently in a second repository, and it is the second time `TR-03` has been the first check to fire — see [The first check to fire, fired on this repository](decisions.md#the-first-check-to-fire-fired-on-this-repository). Fixed by adding the link. Not a reword to satisfy a check: before the fix a reader following that rule had nothing to follow. |
| `FQ-04` | **fixed** | The queue did not state that its rows are not commitments. It is a `declaration` check and was satisfied by writing the sentence, which is what a declaration check is for — the paired behaviour check is `FQ-03`, and `FQ-03` is the one under objection. The sentence is true of that repository independently of this audit; it was simply nowhere written down. |
| `FQ-02` | **objection filed** | Filed, then **declined**. The deviation the decline produces is recorded in that repository's adoption record and the check now reports `waived`. See below. |
| `FQ-03` | **objection filed** | The same objection, the same decline, the same disposal. |

**Nothing was waived before the objection was disposed of, and both are waived
now.** The order matters and is the point of recording both runs: a deviation
written while the argument was open would have echoed a reason that had not been
settled, which makes `waived` a claim the record could not support. `finding` was
the truthful state until the decline, and `waived` is the truthful state after
it. Neither is `ok`, and at no point was either check reported as passing.

## The objection

**Filed, not posted.** The body carries the six fields
[objections.md](../objections.md) requires and lives in that repository's own
adoption record, because it quotes its paths and its documents. **Publishing it
here is exactly the exfiltration channel [objections.md](../objections.md) refuses
to be**, and a redacted objection is not a filed one: "what your project does
instead, concretely, with paths" is a required field and redaction removes it.

What can be said here without publishing anything:

| Field | |
| --- | --- |
| Module, version, check ids | `findings-queue` `0.3.0` — `FQ-02` and `FQ-03`. The objection is to the obligations `findings-carry-evidence` and `findings-have-review-state`, not to the regular expressions. |
| The claim | Both obligations assume a queue whose rows **persist and are annotated in place**. A queue whose rows are *consumed* — removed by a mandatory triage step that produces a durable record elsewhere — serves both stated purposes by a mechanism no check in the module can see. |
| Evidence it serves the purposes | `findings-carry-evidence` exists because an aged row nobody is sure of "sits there forever". No row can age where triage is mandatory per row. `findings-have-review-state` exists to separate noticing from committing and to make per-item approval possible. Both hold structurally in that repository: nothing in the intake file is ever work, and every judging transition is approved individually. |
| What complying would cost | Columns on the intake file put a decision back into the one step that repository's first principle requires to cost none, and duplicate a state that already lives in the record triage produces — two places to look for one fact, which is the failure that module's own README names for two queues. |
| Requested outcome | **Alternative recognised** — a `form` on the two obligations distinguishing a standing queue from a consumed one, under which the evidence and review-state obligations bind the record triage produces rather than the intake file. `minor`. |

**The strongest argument against it is recorded with it:** that the intake file is
not a findings queue at all and the mapping is wrong, because the module is about
defects and that file is about something else. It was not taken, because leaving
the role unmapped would produce two `skip`s where the honest answer is known, and
because that repository's own triage rule names that file as its destination. A
reader who thinks the counter-argument wins should read the two findings as
evidence of a bad mapping rather than a bad module; both readings are on the
record and the disposition settles which.

**Declined, 2026-08-03.** The outcome was not this unit's to take — all four
belong to the owner, and three of them change a shipped module's version. The
reasoning is in
[decisions.md](decisions.md#the-first-objection-is-declined-and-what-that-costs-the-channel-is-not-argued-away),
which carries the argument as made rather than a summary that makes the verdict
look obvious, and states the cost without offsetting it: **this was the objection
channel's first real use and the answer was no.** An adopter who files carefully,
names a genuine cost and gets nothing back learns that filing is not worth doing.

Two reasons. One instance is thin evidence for a `form`, which is the catalog
saying a shape is legitimately *common* rather than legitimately *local* — and
local is what a deviation is for. And [work/README.md](work/README.md)
"Specification edits are in scope, and this is the list" names the three units
permitted to change the specification this phase; a `findings-queue` form is on
none of them, so recognising the alternative here would be the hidden scope that
section exists to prevent.

**What would change the answer: a second adopter with a consumed queue.** The
deviation carries a review date so the question returns whether or not anyone
remembers it.

## The ten judgment lines, answered

A mechanical run that emits ten `judgment` lines and no answers is a run that
looks complete and is not. Each is answered, with what was read.

### triage-rule

| Entry | Answer |
| --- | --- |
| `triage.boundary-is-a-claim` | **Drawn by the claim.** The boundary is what advances the work in flight, not which part of the repository a discovery lands in. A discovery that falsifies the work in flight advances it and is therefore in scope, so the carve-out this catalog states separately is not needed there. Nothing to report. |
| `triage.destination-is-real` | **Real, and demonstrably reviewed.** The rule names who reviews the destination and when, and its history shows one full pass: the destination was emptied, every row resolved to exactly one outcome, and one of those outcomes was a rejection. This is the strongest single answer in the walk, and it is the one the checker misreported — see `F8`. |

**One observation this entry does not ask for, recorded because it is the sharpest
thing the walk found.** That repository's destination takes one kind of thing, and
a defect in its own records is not that kind of thing. So an audit finding about
the repository has nowhere to go inside it, and this walk's own out-of-spec
observations had to be carried here instead. That is not a finding against the
module — `findings-destination-exists` asks for a destination and there is one —
and it is not a catalog gap either, because `findings-queue` is exactly the module
that would cover it. It is what a partial adoption looks like from the inside.

### decision-log

| Entry | Answer |
| --- | --- |
| `decision-log.claim-shaped` | **Mixed, and self-correcting.** The earliest entry groups its reasoning under topic headings; every entry from the first review onward carries a heading that can be true or false. The claims in the early entry exist — they are the bold lead-ins one level below the heading — so the log can be contradicted, but not by heading. **Disposed of as waived**, with the reason in that repository's adoption record: rewriting the headings of entries already written would be editing entries in a log whose first rule is that entries are not edited, and the pattern has already corrected itself without intervention. |
| `decision-log.corrections-preserve` | **Yes, repeatedly and in the strongest form.** Several entries carry an inline correction that leaves the original text in place and points forward, including one correcting a claim that was false when written. Superseded passages are marked as superseded rather than removed. Nothing to report. |
| `decision-log.index-exists-in-substance` | **No, as found. Yes, after the fix.** `DL-05` passed on the first run only because both roles point at one path, which is the documented weakness of that check under `single-log` — and here the weakness was live: there was no index at all, in a log of five hundred and three lines carrying twenty-four entries. **Disposed of as fixed:** an index section was added, listing every entry with an anchor. Adding a row is not editing an entry, which is the rule that makes an index compatible with append-only, and that rule is stated in the section itself. This is the first time the judgment entry has caught what it was written for; in [self-walk.md](self-walk.md) the same line was answered "yes" and carried no work. |
| `decision-log.rationale-not-status` | **Reasoning, with one near-miss.** Two sections carry state — what was open, what was next — but both are frozen inside dated entries and read as the context a decision was taken in, which is what the entry's `do_not_report` clause covers. Nothing to report. |

### findings-queue

These four read the role under objection, and answering them honestly is most of
the objection's evidence.

| Entry | Answer |
| --- | --- |
| `findings.evidence-is-observed` | **No cells, so nothing to grade — and the question does not survive the shape.** What a row records is the noticer's own words captured at the moment of noticing, which is the thing the obligation says is cheap then and expensive later. It is preserved into the record triage produces. Part of the objection. |
| `findings.severity-argues` | **No severity exists.** No obligation in the module requires one, so this judgment entry reads for something no check and no obligation asks for. Recorded as `F13` rather than answered — the entry is asking about a field the module never obliged. |
| `findings.rows-are-findings` | **No — the rows are, by that repository's design, the category this entry warns about.** The entry's stated failure mode is a queue that accumulates opinions until reviewing it stops being worth the time. That failure mode is answered: the queue does not accumulate, because triage empties it. This is the clearest evidence that the module's model and that repository's are different rather than one being wrong, and it is why the requested outcome is a `form` rather than an amendment. |
| `findings.queue-is-reviewed` | **Yes, with dated evidence.** The queue has been emptied once, in full, with every row disposed of. Its current rows are hours old. The entry's `do_not_report` clause covers a short queue, and this one is short because it was reviewed rather than because nothing arrives. |

## What this walk did not exercise, and what it cannot say

- **`DL-03` remains unexercised**, for the second time. `effective_from` is the
  date this adoption was written, and every deletion from that repository's
  decision log predates it. The check has no history to read and its `ok` says
  nothing. That was true in [self-walk.md](self-walk.md) for the same reason and
  it is still the only check in the catalog that a fresh adoption cannot exercise.
- **No `skip` was produced anywhere in the run.** The `skip` path is now
  unexercised in both this repository's own walk and this one, which means the
  catalog's most important escape hatch has no live demonstration in any recorded
  output. That is `M13`'s to report.
- **Nothing here observes whether anyone follows a process.** Every state above
  is a statement about the shape of a record. That repository's process has been
  run once end to end; one run is not a history, and the checks would report the
  same states over documents nobody had ever used.
- **The audit found things no check found.** At least one claim in that
  repository's own scope contract is stale — it describes a state that its history
  contradicts. No check in the catalog can see it, because seeing it would mean
  reading content rather than structure, which is the line
  [SPEC.md](../../SPEC.md) draws deliberately. It is recorded here as a limit of
  the catalog rather than as a finding against the repository.
- **LinkCtrl was not modified**, for extraction or for a reference. That is a
  claim about a third repository and is **attested, not verifiable from here.**
