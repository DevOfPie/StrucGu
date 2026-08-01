# Expected findings — decision-log

What a correct checker produces on each tree here. If yours produces something
else, one of the two is wrong; if you believe it is this file, that is an
[objection](../../../docs/objections.md) rather than a defect in your
implementation.

**These trees deliberately contain broken links.** They are fixtures, not
documentation, and are excluded from any repository-wide link check.

## `satisfies/`

No findings. `DL-01` through `DL-06` all `ok`. Form `single-log`, with both
roles mapped at the same file — which is the normal shape for that form.

## `violates-DL-01/`

`decisions.md` is not present.

| Check | |
| --- | --- |
| `DL-01` | **finding** — no decision log is declared or present |
| `DL-05` | **finding** — no index |
| `DL-02` `DL-03` `DL-04` `DL-06` | `skip` — the target cannot be read |

**Two findings, deliberately.** Under `single-log` both roles map to the same
file, so one absent file fails two `path_exists` checks. That is correct rather
than duplicated: the log and its index are two obligations and both are unmet.

## `violates-DL-02/`

An entry with no date anywhere in the file.

| Check | |
| --- | --- |
| `DL-02` | **finding** — no date appears in the decision log |
| `DL-01` `DL-03` `DL-04` `DL-05` `DL-06` | `ok` |

## `violates-DL-03/`

**Not self-contained.** `DL-03` inspects git history and a fixture cannot carry
a nested repository. [`SETUP.md`](violates-DL-03/SETUP.md) has the commands that
build the violating history — commit the log, then edit an entry away rather
than appending a correction.

| Check | |
| --- | --- |
| `DL-03` | **finding**, after setup — a commit after `effective_from` removed lines |
| `DL-01` `DL-02` `DL-04` `DL-05` `DL-06` | `ok` |

Before setup the tree is clean and `DL-03` has no history to read. This is the
one gap in the fixture coverage and it is recorded as such in
[the fixtures work record](../../../docs/records/work/m6.md).

## `violates-DL-04/`

The log is dated and indexed but never states that it is append-only. A reader
arriving without that sentence edits an entry in good faith.

| Check | |
| --- | --- |
| `DL-04` | **finding** — the log does not state that it is append-only |
| `DL-01` `DL-02` `DL-03` `DL-05` `DL-06` | `ok` |

## `violates-DL-05/`

Form `per-decision-files`. The records exist; `decisions/README.md` does not.

| Check | |
| --- | --- |
| `DL-05` | **finding** — the decision log has no index |
| `DL-01` `DL-02` `DL-03` `DL-04` `DL-06` | `ok` |

This is also the fixture that exercises `cardinality: by_form` — `decision_log`
resolves to a directory here and to a file in every other tree.

## `violates-DL-06/`

An entry links to `investigations/0002-caching.md`, which is not there.

| Check | |
| --- | --- |
| `DL-06` | **finding** — link to `investigations/0002-caching.md` does not resolve |
| `DL-01` `DL-02` `DL-03` `DL-04` `DL-05` | `ok` |

Both index anchors resolve. A checker reporting them has the slug algorithm
wrong — spaces map to single hyphens and runs are **not** collapsed.
