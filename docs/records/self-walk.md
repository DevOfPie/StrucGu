# Self-walk — 0.1.0

Every check in all five modules, applied to this repository by hand through
[strucgu.yaml](../../strucgu.yaml), on 2026-07-31.

**Committed so a later reader can diff against it rather than take the claim.**

**What this is worth.** Close to nothing as evidence. The walk was performed by
the party that wrote the checks, by hand, with no implementation to disagree
with them, on a repository written by the same party. An author unconsciously
writes rules they already satisfy, so a clean result here is the expected
outcome and not a finding about quality. The evidence that these checks detect
anything is the 33 fixture trees under `modules/*/fixtures/`. This file exists to
dogfood the escape hatches — the `skip` path, the role map, the conditional
obligation — and to be diffable later.

The one thing here that *is* evidence is `TR-03`, which failed on the first pass.
See [decisions.md](decisions.md#the-first-check-to-fire-fired-on-this-repository).

---

## triage-rule 0.1.0

`triage_doc` → [triage.md](triage.md)

| | Check | |
| --- | --- | --- |
| `ok` | `TR-01` | present |
| `ok` | `TR-02` | both boundary terms, Vocabulary table |
| `ok` | `TR-03` | links to [findings.md](findings.md) — **failed on the first pass, see below** |
| `ok` | `TR-04` | Precedence paragraph |
| `ok` | `TR-05` | all links and anchors resolve |

`TR-03` reported a finding on the first walk: the queue was named inside a
fenced block rather than as a link. Every word-matching check passed while
nothing resolved to the queue — the same defect this catalog was built after
finding in LinkCtrl. Fixed by naming the queue as a link beneath the block.

## decision-log 0.1.0 — form `single-log`

`decision_log` → [decisions.md](decisions.md) · `decision_index` → the same file

| | Check | |
| --- | --- | --- |
| `ok` | `DL-01` | present |
| `ok` | `DL-02` | dated section headings |
| `ok` | `DL-03` | no history before `effective_from`; nothing to read |
| `ok` | `DL-04` | states append-only in its preamble |
| `ok` | `DL-05` | passes because both roles map to one file — see the note below |
| `ok` | `DL-06` | all links and anchors resolve |

`DL-03` passing here means nothing. There is no history yet. It is the only
check in the catalog that cannot be exercised by a first release.

`DL-05` is the documented weakness of that check under `single-log`: both roles
resolve to the same path, so it cannot fail while `DL-01` passes. Judged
separately below.

## findings-queue 0.1.0

`findings` → [findings.md](findings.md) · prerequisite `triage-rule` adopted

| | Check | |
| --- | --- | --- |
| `ok` | `FQ-01` | present |
| `ok` | `FQ-02` | `Evidence` column |
| `ok` | `FQ-03` | `Reviewed` column |
| `ok` | `FQ-04` | states rows are unscheduled and reviewed individually |
| `ok` | `FQ-05` | links to [triage.md](triage.md) |
| `ok` | `FQ-06` | all links and anchors resolve |

## work-units 0.1.0

`unit_dir` → [work/](work/) · `unit_template` → [work/_template.md](work/_template.md)
· `unit_index` → [work/README.md](work/README.md)

| | Check | |
| --- | --- | --- |
| `ok` | `WU-01` | present |
| `ok` | `WU-02` | template has Done means and Risks |
| `ok` | `WU-03` | all seven records have both |
| `ok` | `WU-04` | no placeholder text; the only match in the tree is `_template.md`, excluded by `_*` |
| `ok` | `WU-05` | present |
| `ok` | `WU-06` | template asks for Depends on and Discharges |
| `ok` | `WU-07` | all links and anchors resolve |

## investigations 0.1.0

`investigations` → **unmapped**

| | Check | |
| --- | --- | --- |
| `skip` | `IN-01` | role deliberately unmapped |
| `skip` | `IN-02` | role deliberately unmapped |
| `skip` | `IN-03` | role deliberately unmapped |
| `skip` | `IN-04` | role deliberately unmapped |

No investigation here has outgrown a decision entry, so the obligation's
condition is unmet. **These four are the point of this walk.** They are the only
exercise the `skip` path and the conditional obligation get anywhere in the
repository, and a checker reporting them as `ok` would be converting "I did not
look" into "I looked and it was fine".

---

## Summary

```
28 checks: 24 ok, 0 findings, 4 skipped, 0 waived.
17 for judgment.
```

Not a grade. Four of these say "I could not tell", which is not the same as
"fine", and seventeen were never mechanically decided at all.

## Judgment

The 17 `judgment` entries were read and none produced a finding. Two are worth
recording because they came closest, and because a judgment pass that reports
nothing is usually a judgment pass that was not adversarial enough.

**`decision-log.index-exists-in-substance`** — the index is a section of the log
rather than a separate file, so `DL-05` passes for free. Read directly: the
Index table lists every entry with an anchor link, and a reader can reach any
entry without reading the file top to bottom. The obligation is met in
substance, not only in the check.

**`work-units.risks-considered`** — the pattern to watch for is every record
saying "Low", which is the section satisfied rather than considered. None of the
seven does; each names a specific unknown, and four of them name the same one in
different forms — that this catalog is generalised from a single repository by
the person who will also be its first adopter. That the same risk recurs is
information, and it is the risk the [objection channel](../objections.md) exists
to answer.

The remaining fifteen were read against their `do_not_report` clauses and
produced nothing worth a row in [findings.md](findings.md).

## Open findings

Both rows in [findings.md](findings.md) — `F1` and `F2` — were already recorded
before this walk and are unreviewed. Neither was produced by a check; both are
observations about the catalog's own construction that no check here can see,
which is itself a fact about the coverage.
