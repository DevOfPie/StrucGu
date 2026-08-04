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

**One tree here is in a third shape.** `satisfies-prose-destination/` is neither
`satisfies/` nor a `violates-*` tree: every check passes, and it exists because
the content that pins its boundary contradicts what `satisfies/` has to hold.
[SPEC.md](../../../SPEC.md) admits the shape as `satisfies-<suffix>/`.

## `satisfies/`

No findings. `TR-01` through `TR-05` all `ok`. Four `judgment` lines still
emitted — a mechanical run is never complete.

**`TR-05` staying `ok` is load-bearing.** The document ends with a fenced example
containing a link to `scope.md`, which is not in this tree. Code is not scanned
for links, so a correct checker does not see it. A checker that scans fences
reports `TR-05: finding` here — which is the failure
[SPEC.md](../../../SPEC.md) records having hit twice, now with a tree behind
it.

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

## `satisfies-prose-destination/`

**The tree that states the limitation instead of hiding it.** The rule names its
destination in prose — "write one row in the findings queue and carry on" — and
the resolving link is in a table two sections further down, under a heading that
says why it is there.

| Check | |
| --- | --- |
| `TR-01` `TR-02` `TR-03` `TR-04` `TR-05` | `ok` |

`TR-03` reporting `ok` is the whole tree. `triage-destination` asks for a link
and says nothing about where in the document it sits, so a rule that reads as a
sentence rather than as a path conforms to `TR-03` on the strength of a link
elsewhere.
A checker that looked for the link in the sentence stating the rule — a reading
the obligation's old wording invited, since it spoke of the document *naming* a
destination — reports a finding here and is wrong.

Read it against [`violates-TR-03/`](violates-TR-03/), which is the same shape
with the link absent altogether: prose alone is a finding, prose plus a link
anywhere is `ok`. The pair is what closed `F2` in
[findings.md](../../../docs/records/findings.md) — the check was left as strict
as it was and the obligation was narrowed to match it.

This tree pins its adoption record at `0.4.0` where the others pin `0.1.0`,
because a pin is a dated claim about what was reviewed and this tree was
reviewed against the obligation as `0.4.0` words it.

## `waives-TR-02/`

**The only tree in the catalog where a check reports `waived`.** It carries the
same `triage.md` as [`violates-TR-02/`](violates-TR-02/) — the boundary between
in spec and out of spec is not stated — and the same failure. What differs is the
adoption record, which accepts the deviation with a reason, a scope, an accepting
party and an expiry.

| Check | |
| --- | --- |
| `TR-02` | `waived` |
| `TR-01` `TR-03` `TR-04` `TR-05` | `ok` |

Two foldings are both wrong and both tempting. Folding `waived` into `ok` hides an
accepted deviation from every run after the one that accepted it, which is the
thing the state exists to prevent — the reason is echoed every time, not
suppressed once. Folding it into `finding` ignores a record the adopter wrote by
hand and makes the deviation channel pointless.

**This tree's expectation is dated, and that is a property of the fixture rather
than of any checker.** A deviation must carry a `review_by`, and past it the
check reports a finding again. So a tree pinning `waived` is true only until its
expiry, and the choice is between a realistic date that makes this row wrong on a
known future morning and a distant one that models a deviation nobody will ever
review. This tree takes `2099-12-31` and says so here rather than letting a
reader discover it. Read the pair below as the whole statement: the expiry is
tested, it is just tested somewhere the clock cannot reach.

## `violates-TR-02-expired-deviation/`

The same deviation, with `review_by: 2026-08-01` and nothing renewed.

| Check | |
| --- | --- |
| `TR-02` | `finding` |
| `TR-01` `TR-03` `TR-04` `TR-05` | `ok` |

**Detection reasserts itself without anyone enforcing anything.** That sentence is
in [SPEC.md](../../../SPEC.md#deviations) and until this tree existed nothing
tested it: a checker that reads `deviations` and never looks at `review_by`
reports `waived` here and reproduces every other row in the catalog. It is the
cheapest possible implementation of the field and it silently converts every
expiry into a permanent waiver.

The two trees are one statement in two halves and neither is much use alone.

