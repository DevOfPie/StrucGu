# Expected findings — triage-rule

What a correct checker produces on each tree here. If yours produces something
else, one of the two is wrong; if you believe it is this file, that is an
[objection](../../../docs/objections.md) rather than a defect in your
implementation.

**Scope.** Only `TR-*` checks are listed. Each tree also adopts
[findings-queue](../../findings-queue/), because `TR-03` needs a `findings` role
to point at; its `FQ-*` results are not this module's fixtures and are not
listed.

**These trees deliberately contain broken links.** They are fixtures, not
documentation, and are excluded from any repository-wide link check.

## `satisfies/`

No findings. `TR-01` through `TR-05` all `ok`. Four `judgment` lines still
emitted — a mechanical run is never complete.

## `violates-TR-01/`

`triage.md` is not present, though the adoption record maps it.

| Check | |
| --- | --- |
| `TR-01` | **finding** — no triage document is declared or present |
| `TR-02` `TR-03` `TR-04` `TR-05` | `skip` — the target cannot be read |

The four skips are the point of this fixture as much as the finding. A checker
that reports five findings here is telling a reader the repository is five times
more broken than it is.

## `violates-TR-02/`

The document has a precedence rule and links to the queue, but never names the
two sides of the boundary.

| Check | |
| --- | --- |
| `TR-02` | **finding** — the triage document does not name both sides of the boundary |
| `TR-01` `TR-03` `TR-04` `TR-05` | `ok` |

## `violates-TR-03/`

**The fixture modelled on real drift.** The rule names its destination — "append
a row to the deferred findings table in the plan" — in prose, and the queue is
somewhere else. Every mechanical check that looks at words passes. This is the
LinkCtrl defect that motivated the catalog, reproduced.

| Check | |
| --- | --- |
| `TR-03` | **finding** — no link resolving to the findings queue |
| `TR-01` `TR-02` `TR-04` `TR-05` | `ok` |

## `violates-TR-04/`

Boundary and destination are both present; nothing says what to do when two
governing documents disagree.

| Check | |
| --- | --- |
| `TR-04` | **finding** — the document does not say what to do when governing documents conflict |
| `TR-01` `TR-02` `TR-03` `TR-05` | `ok` |

## `violates-TR-05/`

The document links to `scope.md`, which is not there.

| Check | |
| --- | --- |
| `TR-05` | **finding** — `triage.md` links to `scope.md`, which does not resolve |
| `TR-01` `TR-02` `TR-03` `TR-04` | `ok` |

`TR-03` still passes: the link to the findings queue resolves. Only the other
one is broken, which is what keeps this fixture testing one check.
