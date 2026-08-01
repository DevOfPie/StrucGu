# findings-queue — obligations and checks

Normative. [module.yaml](module.yaml) carries the same content as data; if the
two disagree, this file wins and the disagreement is a defect to report.

Contract terms are defined in [SPEC.md](../../SPEC.md).

**Requires** [triage-rule](../triage-rule/). Not as an imposition — without a
rule defining what counts as out of scope, no row in this queue can be wrong
about anything, and every check here would be testing the shape of a list with
no meaning. A checker reports `skip` for every check in this module when
`triage-rule` is not adopted.

## Roles

| Role | Cardinality | Of |
| --- | --- | --- |
| `findings` | file | The queue. One row per finding. |

## Obligations

### `findings-destination-exists` — deferred findings have a destination

**Purpose.** "Do not fix it" with nowhere to put it is "forget it", and everyone
reading it knows that, so nobody obeys it. The destination is what makes the
triage rule followable rather than aspirational.

**Required.** Yes.

**Provenance.** LinkCtrl `docs/build-notes/deferred-findings.md`.

**Satisfied in this repository by** [docs/records/findings.md](../../docs/records/findings.md).

### `findings-carry-evidence` — a row records what was observed

**Purpose.** A row saying something is broken, written a month ago by someone who
is no longer sure, cannot be acted on and cannot be dismissed. It sits there
forever. Evidence captured at the moment of noticing is cheap; reconstructed
later it is expensive and usually wrong.

**Required.** Yes.

**Provenance.** LinkCtrl `docs/build-notes/deferred-findings.md:24`, the
`Evidence` column, and its worked instance ending "Confirmed against the live
release body, not inferred."

**Satisfied in this repository by** [docs/records/findings.md](../../docs/records/findings.md).

### `findings-have-review-state` — a row records whether anyone has reviewed it

**Purpose.** This is what separates noticing something from committing to fix
it. Without the state there are only two possibilities — everything in the queue
is work, or nothing is — and both are wrong. The state is also what makes
per-item approval possible, and per-item approval is the whole mechanism.

**Required.** Yes.

**Provenance.** LinkCtrl `docs/build-notes/deferred-findings.md:24`, the
`Reviewed` column.

**Satisfied in this repository by** [docs/records/findings.md](../../docs/records/findings.md).

### `findings-are-unscheduled` — the queue states that its rows are not commitments

**Purpose.** A list of defects, unexplained, reads as a backlog. Read as a
backlog it either creates an obligation nobody agreed to, or gets approved in
bulk to clear it — and bulk approval turns every passing observation into
committed scope, which is the failure the triage rule exists to prevent arriving
through the door built to prevent it.

**Required.** Yes.

**Provenance.** LinkCtrl `docs/build-notes/deferred-findings.md:8-11`.

**Satisfied in this repository by** [docs/records/findings.md](../../docs/records/findings.md).

## Checks

### `FQ-01` · `path_exists` · behaviour

**Binds** `findings`.

**Finding.** No findings queue is declared or present. The triage rule's
instruction not to fix out-of-scope issues has no destination, which makes it an
instruction to forget them.

**Known false positives.** None.

### `FQ-02` · `pattern_present` · behaviour

**Binds** `findings`.

```
\|[^|]*evidence[^|]*\|
```

**Finding.** The findings queue has no evidence column. A row without an
observation is a rumour with a row number — it cannot be acted on and cannot be
dismissed, so it stays forever.

**Known false positives.** Matches any table with a column whose header contains
the word, including an example table in prose. The check confirms the column
exists; whether anything in it is evidence is a judgment entry below.

### `FQ-03` · `pattern_present` · behaviour

**Binds** `findings`.

```
\|[^|]*(reviewed|review|approved|status|state)[^|]*\|
```

**Finding.** The findings queue has no review-state column. There is then
nothing between noticing something and committing to fix it, so the queue is
either an obligation nobody agreed to or a list nobody acts on.

**Known false positives.** The word `status` is common in table headers for
unrelated reasons. A queue with a `Status` column meaning something else passes.

### `FQ-04` · `pattern_present` · declaration

**Binds** `findings`. Any one pattern matching is sufficient.

```
not scheduled|nothing here is scheduled|not a commitment|report, not a|per item|individually
```

**Finding.** The queue does not state that its rows are unscheduled and approved
individually. Read without that, a list of defects is a backlog — and a backlog
gets cleared in bulk, which is how an observation quietly becomes committed
scope.

**Paired behaviour check.** `FQ-03`. The review-state column is the mechanism
that makes per-item approval possible; without it the declaration has nothing
behind it.

**Known false positives.** Matches inside code blocks and quotations.

### `FQ-05` · `role_referenced` · behaviour

**Binds** `findings` → `triage_doc`.

**Finding.** The findings queue does not link to the rule that decides what
belongs in it. A reader arriving at the queue cannot tell what it is for, and a
reader deciding whether to add a row has nothing to check against.

**Reports `skip`** when `triage-rule` is not adopted or `triage_doc` is
unmapped.

**Known false positives.** Resolves markdown links only. See `F2` in
[docs/records/findings.md](../../docs/records/findings.md).

### `FQ-06` · `links_resolve` · behaviour

**Binds** `findings`.

**Finding.** A relative link or anchor in the findings queue does not resolve.
Rows commonly point at the code they were observed in, and a row whose location
has rotted is a row nobody can verify.

**Known false positives.** None. External schemes are not checked.

## Judgment

### `findings.evidence-is-observed`

**Question.** Does each evidence cell contain something observed, or a
restatement of the finding?

**Read** `findings`.

**Evidence.** Quote the cell. "This is broken" restates the finding. A
`file:line`, a quoted output, a confirmed live behaviour is evidence. The
distinction is whether someone else could check it without trusting you.

**Do not report.** Evidence that is real but thinner than you would have
written.

### `findings.severity-argues`

**Question.** Does the severity say what the impact is, or does it name a tier?

**Read** `findings`.

**Evidence.** Quote it. "High" conveys nothing a reader can act on. "Recurs on
every release, and the artefact is invisible in rendered output" lets someone
decide.

**Do not report.** A severity that argues its impact but reaches a conclusion
you disagree with.

### `findings.rows-are-findings`

**Question.** Are the rows observations of defects, or are they complaints,
feature requests, and things someone wanted to say?

**Read** `findings`.

**Evidence.** A row that could not be shown false by anyone. A queue that
accumulates opinions stops being reviewed, because reviewing it stops being
worth the time.

**Do not report.** Rows about documentation or process defects. Those are
findings.

### `findings.queue-is-reviewed`

**Question.** Is anything ever reviewed, or does every row sit unreviewed
indefinitely?

**Read** `findings`.

**Evidence.** The proportion of rows never reviewed, and whether any have been
closed. An unreviewed queue is the module's failure mode, and it looks identical
to a healthy one from the outside.

**Do not report.** A queue that is short or currently empty. Neither is
evidence of neglect.
