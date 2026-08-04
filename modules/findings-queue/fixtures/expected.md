# Expected findings — findings-queue

What a correct checker produces on each tree here. If yours produces something
else, one of the two is wrong; if you believe it is this file, that is an
[objection](../../../docs/objections.md) rather than a defect in your
implementation.

**Scope.** Only `FQ-*` checks are listed. Each tree also adopts
[triage-rule](../../triage-rule/), because this module declares it as a
prerequisite and every check here would otherwise `skip`. Its `TR-*` results are
not this module's fixtures and are not listed.

**These trees deliberately contain broken links.** They are fixtures, not
documentation, and are excluded from any repository-wide link check.

## `satisfies/`

No findings. `FQ-01` through `FQ-06` all `ok`.

## `violates-FQ-01/`

`findings.md` is not present.

| Check | |
| --- | --- |
| `FQ-01` | **finding** — no findings queue is declared or present |
| `FQ-02` `FQ-03` `FQ-04` `FQ-05` `FQ-06` | `skip` — the target cannot be read |

## `violates-FQ-02/`

The table has `Finding`, `Where`, `Severity` and `Reviewed` columns, and no
`Evidence`.

| Check | |
| --- | --- |
| `FQ-02` | **finding** — the queue has no evidence column |
| `FQ-01` `FQ-03` `FQ-04` `FQ-05` `FQ-06` | `ok` |

## `violates-FQ-03/`

Evidence is there; nothing records whether anyone has reviewed a row.

| Check | |
| --- | --- |
| `FQ-03` | **finding** — the queue has no review-state column |
| `FQ-01` `FQ-02` `FQ-04` `FQ-05` `FQ-06` | `ok` |

`FQ-04` still passes: the file says rows are approved *individually*, which is
one of its patterns. That separation is deliberate — this fixture tests the
column, not the declaration.

## `violates-FQ-04/`

Both columns are present. Nothing tells a reader the rows are unscheduled, so
the file reads as a backlog.

| Check | |
| --- | --- |
| `FQ-04` | **finding** — the queue does not state that its rows are not commitments |
| `FQ-01` `FQ-02` `FQ-03` `FQ-05` `FQ-06` | `ok` |

## `violates-FQ-05/`

A well-formed queue that never points at the rule deciding what belongs in it.

| Check | |
| --- | --- |
| `FQ-05` | **finding** — no link resolving to the triage document |
| `FQ-01` `FQ-02` `FQ-03` `FQ-04` `FQ-06` | `ok` |

## `violates-FQ-06/`

A row cites `triage.md#glossary`. The document is there; that heading is not.

| Check | |
| --- | --- |
| `FQ-06` | **finding** — anchor `#glossary` does not resolve in `triage.md` |
| `FQ-01` `FQ-02` `FQ-03` `FQ-04` `FQ-05` | `ok` |

**`FQ-05` passing here is the point of this fixture.** The link's path resolves
to the triage document, which is all `role_referenced` asks; the rotted anchor
belongs to `links_resolve`. A checker that fails both has conflated two checks
that answer different questions.

## `violates-FQ-06-reference-link/`

**Pins which markdown constructs count as a link.** The `Where` cell uses a
reference-style link, `[the old queue][old]`, defined at the foot of the file as
`archive/findings.md`. That path is not in the tree.

| Check | |
| --- | --- |
| `FQ-06` | **finding** — the reference definition points at `archive/findings.md`, which does not resolve |
| everything else | `ok` |

`violates-FQ-06/` pins a rotted anchor on an inline link. This tree pins that a
reference-style link is a link at all. [SPEC.md](../../../SPEC.md) says how a
link resolves and never says what a link is, so a checker extracting inline
links only reports `ok` here — and reference links are commonest in exactly the
documents this module describes, where one destination is cited many times.
