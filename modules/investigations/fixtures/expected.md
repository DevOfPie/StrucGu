# Expected findings — investigations

What a correct checker produces on each tree here. If yours produces something
else, one of the two is wrong; if you believe it is this file, that is an
[objection](../../../docs/objections.md) rather than a defect in your
implementation.

**These trees deliberately contain broken links.** They are fixtures, not
documentation, and are excluded from any repository-wide link check.

Every tree maps `investigations` at `investigations/`, and maps it — a project
that has not yet run an investigation leaves the role unmapped instead, which is
what [this repository does](../../../strucgu.yaml).

## `satisfies/`

No findings. `IN-01` through `IN-04` all `ok`.

The record is worth reading as the worked example of the format: numbered
claim-first findings with the numbers that were observed, a separate section for
the rules drawn from them, an explicit note that the harness was not kept, and
the sentence that makes this format worth having — *this is the same conclusion
the design expected but for a different reason*.

## `violates-IN-01/`

The directory exists and holds no records.

| Check | |
| --- | --- |
| `IN-01` | **finding** — the module is adopted and applicable, and no records are present |
| `IN-02` `IN-03` `IN-04` | `skip` — there is nothing to read |

**This fixture tests the `dir` rule specifically.** An empty directory satisfies
a filesystem existence test while satisfying nothing the obligation wanted, so
`path_exists` on a `dir` role requires at least one file surviving exclusions.
A checker that reports `ok` here has implemented `path_exists` against the
filesystem rather than against
[SPEC.md](../../../SPEC.md#check-vocabulary).

## `violates-IN-02/`

The record has context, findings and decisions, and never says how to run it
again or that the setup is gone.

| Check | |
| --- | --- |
| `IN-02` | **finding** — the record is missing its reproduction section |
| `IN-01` `IN-03` `IN-04` | `ok` |

Silence here reads as though reproduction is possible, and leaves the next
reader to discover it is not.

## `violates-IN-03/`

All four sections are present. Nothing says when the investigation was run or
what it was run against, so its findings cannot be aged and the rules drawn from
them cannot be re-checked when the underlying thing moves.

| Check | |
| --- | --- |
| `IN-03` | **finding** — the record states neither a date nor what it was tested against |
| `IN-01` `IN-02` `IN-04` | `ok` |

## `violates-IN-04/`

The record links to `../decisions.md`, which is not in this tree.

| Check | |
| --- | --- |
| `IN-04` | **finding** — link to `../decisions.md` does not resolve |
| `IN-01` `IN-02` `IN-03` | `ok` |

The link also carries an anchor. A checker must resolve the path first and not
report the anchor separately when the file itself is absent — one broken link is
one finding.
