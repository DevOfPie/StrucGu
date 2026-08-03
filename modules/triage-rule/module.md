# triage-rule — obligations and checks

Normative. [module.yaml](module.yaml) carries the same content as data; if the
two disagree, this file wins and the disagreement is a defect to report.

Contract terms are defined in [SPEC.md](../../SPEC.md).

## Roles

| Role | Cardinality | Of |
| --- | --- | --- |
| `triage_doc` | file | The document stating what the work in flight requires and what happens to everything else. |

## Obligations

### `triage-boundary` — the document distinguishes work in flight from everything else

**Purpose.** Without a written line, the question is answered fresh every time it
comes up, by whoever is holding it, at the moment they are least able to answer
it well. The answer then differs between people and between sessions, and the
scope of a piece of work becomes unknowable after the fact.

**Required.** Yes.

**Provenance.** LinkCtrl `docs/build-notes/workflow.md:16-24`, the Vocabulary
table's *In spec* and *Out of spec* rows.

**Satisfied in this repository by** [docs/records/triage.md](../../docs/records/triage.md).

### `triage-destination` — the document names where out-of-scope findings go

**Purpose.** A boundary with no destination on the far side is an instruction to
forget. The destination must be somewhere a reader can actually reach from the
rule, because a rule naming a place that has moved reads as correct to everyone
who already knows where the place is — which is everyone except the person the
rule was written for.

**Required.** Conditional. Applies when `findings-queue` is adopted. A repository
routing findings to an issue tracker instead satisfies the obligation's purpose
and should record the deviation rather than a mapping.

**Provenance.** LinkCtrl `docs/build-notes/workflow.md:31-36`. This obligation
exists because that passage is the defect that motivated this catalog: it still
directs a reader to a file the queue moved out of, and nothing caught it.

**Satisfied in this repository by** [docs/records/triage.md](../../docs/records/triage.md)
linking to [docs/records/findings.md](../../docs/records/findings.md).

### `triage-precedence` — the document says what to do when two governing documents disagree

**Purpose.** Two documents that both govern the work will eventually contradict
each other. A reader with no instruction picks one, silently, and the
contradiction survives — usually until it produces a decision nobody can explain.
Reporting rather than picking is what turns a contradiction into something that
gets fixed.

**Required.** Yes.

**Provenance.** LinkCtrl `docs/build-notes/workflow.md:10-12`.

**Satisfied in this repository by** [docs/records/triage.md](../../docs/records/triage.md),
its Precedence paragraph.

## Checks

### `TR-01` · `path_exists` · behaviour

**Binds** `triage_doc`.

**Finding.** No triage document is declared or present. Nothing states where the
boundary of the current work is, so nothing can be outside it.

**Known false positives.** None.

### `TR-02` · `pattern_present` · declaration

**Binds** `triage_doc`. Both patterns must match.

```
in[ -](spec|scope)
out[ -]of[ -](spec|scope)
```

**Finding.** The triage document does not name both sides of the boundary. A
document that describes only what is required, without naming the category of
everything else, gives a reader nothing to put a finding into.

**Paired behaviour check.** `TR-03` — the destination the far side names must
resolve.

**Known false positives.** The patterns match inside code blocks, quotations,
and examples. A document quoting this specification will match without stating a
rule of its own.

### `TR-03` · `role_referenced` · behaviour

**Binds** `triage_doc` → `findings`.

**Finding.** The triage document does not contain a link resolving to the
findings queue. The rule names a destination the reader cannot reach from it, or
names one that has moved.

**Reports `skip`** when `findings-queue` is not adopted or the `findings` role
is unmapped.

**Known false positives.** The check resolves markdown links only. A document
naming its destination in prose rather than as a link reports a finding despite
satisfying the obligation's purpose — and prose is the form the original defect
took. Recorded as `F2` in [docs/records/findings.md](../../docs/records/findings.md);
a repository hitting it should record a deviation rather than reword its
document to satisfy a check.

### `TR-04` · `pattern_present` · declaration

**Binds** `triage_doc`. One pattern, alternating over the accepted phrasings —
[SPEC.md](../../SPEC.md) requires every listed pattern to match, and there is
one.

```
conflict|contradict|disagree|precedence|takes precedence|wins on
```

**Finding.** The triage document does not say what to do when two governing
documents disagree. Silence means the reader picks, and the contradiction is
never reported.

**Paired behaviour check. None, and this is stated rather than hidden.** Whether
anyone actually reports a conflict instead of quietly resolving it is not
observable in the shape of a record. Under [SPEC.md](../../SPEC.md) this makes
`TR-04` decoration, and it ships anyway because the sentence is worth having in
front of a reader even when nothing verifies they obeyed it. An adopter who
disagrees should turn it off; that is a legitimate position and not a deviation
worth arguing about.

**Known false positives.** Any prose using these words in another sense. A
document discussing merge conflicts matches.

### `TR-05` · `links_resolve` · behaviour

**Binds** `triage_doc`.

**Finding.** A relative link or anchor in the triage document does not resolve.
A rule pointing at something that moved costs a reader their trust in the rest
of it.

**Known false positives.** None. External schemes are not checked.

## Judgment

### `triage.boundary-is-a-claim`

**Question.** Is the boundary drawn by what the current work *claims*, or by
which part of the project a defect happens to live in?

**Read** `triage_doc`.

**Evidence.** Quote the rule. A boundary drawn by subsystem sends a defect that
falsifies the current work's own claim to the queue, where it sits while the
work is declared done on a claim that is not true.

**Do not report.** A boundary drawn by claim but worded differently than you
would word it.

### `triage.destination-is-real`

**Question.** Is the named destination something anyone reviews, or a list that
exists so findings can be put somewhere?

**Read** `triage_doc`, `findings`.

**Evidence.** Whether the rule says who reviews the destination and when. A rule
that defers without naming a reviewer is a rule for forgetting.

**Do not report.** A queue that is currently empty. Empty is not the same as
unreviewed.
