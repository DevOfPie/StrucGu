# investigations — obligations and checks

Normative. [module.yaml](module.yaml) carries the same content as data; if the
two disagree, this file wins and the disagreement is a defect to report.

Contract terms are defined in [SPEC.md](../../SPEC.md).

## Roles

| Role | Cardinality | Of |
| --- | --- | --- |
| `investigations` | dir | One record per investigation. |

Module-level exclusions: `_*`, `README.md`, `index.md`.

## Obligations

### `investigation-records-exist` — an investigation that outgrew a decision entry has its own record

**Purpose.** Evidence substantial enough that a log entry cannot hold it gets
lost when it is squeezed into one anyway. What survives is the conclusion, with
nothing a later reader can re-examine.

**Required.** Conditional — applies once the project has run at least one
investigation whose findings did not fit in a single decision-log entry. A
project that has not is not missing anything.

**Provenance.** LinkCtrl `docs/adr/0001-partitioning-and-sqlc.md`, and the note
in `docs/build-notes/decisions.md` that longer investigations live separately.

**Not currently satisfied in this repository.** No investigation here has
outgrown a decision entry, so the role is deliberately unmapped in
[strucgu.yaml](../../strucgu.yaml) and every check below reports `skip`. That is
the conditional path working, and it is the only place in this repository where
it is exercised.

### `investigation-states-what-it-tested-against` — the record says what was used, with versions

**Purpose.** Findings true of one version of one thing, recorded without saying
which, become folklore. The underlying thing changes, the rule stays, and nobody
can detect that it is now wrong because the record never said what it was true
of.

**Required.** Yes, when the module applies.

**Provenance.** LinkCtrl `docs/adr/0001-partitioning-and-sqlc.md`, its status
line naming both tool versions and the unit of work that ran the investigation.

### `investigation-separates-evidence-from-rules` — observations and the rules drawn from them are distinct sections

**Purpose.** They have different lifetimes. An observation stays true of what it
was observed against; a rule drawn from it can stop being right while the
observation stays correct. Merged, neither can be revisited without redoing the
work.

**Required.** Yes, when the module applies.

**Provenance.** LinkCtrl `docs/adr/0001-partitioning-and-sqlc.md`, its numbered
claim-first findings section followed by a separate decisions section.

### `investigation-is-reproducible` — the record says how to run it again, or says the artifacts are gone

**Purpose.** The findings are the durable part and the setup usually is not.
Saying so explicitly — including "the spike was not committed, here is what it
would take to redo it" — is more useful than silence, which reads as though
reproduction is possible and leaves the reader to discover it is not.

**Required.** Yes, when the module applies.

**Provenance.** LinkCtrl `docs/adr/0001-partitioning-and-sqlc.md`, its
reproduction section stating the spike was deliberately not committed.

## Checks

### `IN-01` · `path_exists` · behaviour

**Binds** `investigations`.

**Finding.** The module is adopted and marked applicable, but no investigation
records are present.

**Reports `skip`** when the role is unmapped — which is the correct state for a
project that has not yet run an investigation needing one.

**Known false positives.** None.

### `IN-02` · `heading_present` · behaviour

**Binds** `investigations`. Applies to every record. All four patterns must
match.

```
context|background|question
finding|observ|result
decision|rule|conclusion
reproduc|redo|re-run|repeat
```

**Finding.** An investigation record is missing its context, its observations,
the rules drawn from them, or how to run it again. A record without separated
observations and rules states conclusions with no evidence a reader can
re-examine.

**Known false positives.** A record that genuinely has nothing to reproduce
still needs the section, saying so. That is the obligation, not a false
positive.

### `IN-03` · `pattern_present` · behaviour

**Binds** `investigations`. Applies to every record. Both patterns must match.

```
[0-9]{4}-[0-9]{2}-[0-9]{2}
verified against|tested against|observed against|measured against|status
```

**Finding.** An investigation record does not state when it was run or what it
was run against. Its findings cannot be aged, and a rule drawn from them cannot
be re-checked when the underlying thing changes.

**Known false positives.** The word `status` matches a status line that names no
version. The check confirms the line exists; whether it names what was tested is
the judgment entry below.

### `IN-04` · `links_resolve` · behaviour

**Binds** `investigations`.

**Finding.** A relative link or anchor in an investigation record does not
resolve. Records commonly point at the decision entries they came from and the
work that ran them.

**Known false positives.** None. External schemes are not checked.

## Judgment

### `investigations.findings-are-observed`

**Question.** Are the findings things that were observed, or things that were
expected?

**Read** `investigations`.

**Evidence.** Quote the finding. "sqlc emits a junk model for every child
partition, output below" is an observation. "sqlc should handle this correctly"
is an expectation with a confident tone. An investigation of expectations is
reasoning that was labelled as evidence, which is worse than no record.

**Do not report.** Observations recorded more briefly than you would have
recorded them.

### `investigations.versions-are-named`

**Question.** Does the status line name specific versions of what was tested, or
does it name the things without versions?

**Read** `investigations`.

**Evidence.** Quote the line. "Verified against the database" ages invisibly.
"Verified against PostgreSQL 17.10 and sqlc v1.31.1" can be checked against what
is in use now.

**Do not report.** A version named for the primary subject but not for
incidental tooling.

### `investigations.right-size`

**Question.** Did this investigation need its own record, or would a decision
entry have held it?

**Read** `investigations`.

**Evidence.** Whether the record carries evidence a log entry could not. A
directory of records for things that did not need one makes the ones that
mattered harder to find, which is the failure mode of adopting this module too
eagerly.

**Do not report.** A record that is short because the investigation was short
but its evidence is genuinely substantial.
