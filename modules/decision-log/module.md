# decision-log — obligations and checks

Normative. [module.yaml](module.yaml) carries the same content as data; if the
two disagree, this file wins and the disagreement is a defect to report.

Contract terms are defined in [SPEC.md](../../SPEC.md).

## Roles

| Role | Cardinality | Of |
| --- | --- | --- |
| `decision_log` | by form — `file` under `single-log`, `dir` under `per-decision-files` | Where rationale is recorded. |
| `decision_index` | file | Navigation. Under `single-log` this may be a section of the log itself, in which case both roles map to the same path. |

## Forms

| Form | Shape |
| --- | --- |
| `single-log` | One growing file, newest entry last. |
| `per-decision-files` | One file per decision, plus an index file. |

Both satisfy every obligation. The second exists because a repository that
already keeps decision records almost certainly keeps them that way, and
treating the common shape as a deviation would make the module unusable for the
adopters most likely to want it.

## Obligations

### `decision-rationale-recorded` — reasoning has a place that is not a commit message

**Purpose.** Rationale that exists only in commit messages is not recoverable by
a reader who does not already know what to search for. Rationale that exists only
in someone's head is not recoverable at all.

**Required.** Yes.

**Provenance.** LinkCtrl `docs/build-notes/decisions.md`.

**Satisfied in this repository by** [docs/records/decisions.md](../../docs/records/decisions.md).

### `decision-entries-dated` — every entry carries a date

**Purpose.** An undated log cannot show that a later entry corrects an earlier
one, which is the mechanism the next obligation depends on. It also cannot show
what was known when.

**Required.** Yes.

**Provenance.** LinkCtrl `docs/build-notes/decisions.md`, its dated section
headings.

**Satisfied in this repository by** [docs/records/decisions.md](../../docs/records/decisions.md).

### `decision-log-append-only` — an entry is never edited away

**Purpose.** The record that an earlier belief was held is the thing being
preserved. Editing an entry to make it current destroys exactly what the log is
for, and leaves a document that reads as though the project always knew.

**Required.** Yes.

**Provenance.** LinkCtrl `docs/build-notes/decisions.md`, its preamble, and the
worked instance where an entry that had become false was left in place with a
pointer rather than corrected.

**Satisfied in this repository by** [docs/records/decisions.md](../../docs/records/decisions.md).

### `decision-log-indexed` — the log has an index

**Purpose.** Past a few hundred lines an unindexed log is written to and never
read from. A log nobody reads is a cost with no benefit, and it will be
abandoned — correctly.

**Required.** Yes.

**Provenance.** LinkCtrl `docs/build-notes/decisions.md`, its `## Index` section
and the rule that adding a row to it is not editing an entry.

**Satisfied in this repository by** [docs/records/decisions.md](../../docs/records/decisions.md),
its Index section.

## Checks

### `DL-01` · `path_exists` · behaviour

**Binds** `decision_log`.

**Finding.** No decision log is declared or present. Rationale is recoverable
only by whoever already knows it.

**Known false positives.** None.

### `DL-02` · `pattern_present` · behaviour

**Binds** `decision_log`.

```
[0-9]{4}-[0-9]{2}-[0-9]{2}
```

**Finding.** No date appears in the decision log. An undated log cannot show
that a later entry corrects an earlier one.

**Known false positives.** Any date in any context matches — a date inside an
entry's prose satisfies the check without any entry being dated. This is the
weakest check in the module and it is here because the alternative is a check on
heading shape, which would mandate a format and this module does not mandate
formats.

### `DL-03` · `history_deletions` · behaviour

**Binds** `decision_log`. **Requires `effective_from`.**

**Finding.** Commits after `effective_from` removed lines from the decision log.
Reported for a look, not as a defect — a rename, a file split, or an index
rewrite is legitimate; an entry edited away is not, and the two are
indistinguishable to a checker.

**Known false positives.** Many, by construction. Splitting a log into two files
reports every line moved. This check produces something for a person to look at
and is deliberately not a pass-or-fail signal. A checker must not run it over
history before `effective_from`.

### `DL-04` · `pattern_present` · declaration

**Binds** `decision_log`. Any one pattern matching is sufficient.

```
append[ -]only|never edit an entry|not edited|corrects an earlier
```

**Finding.** The decision log does not state that it is append-only. A reader
who does not know will edit an entry to bring it up to date, in good faith, and
destroy the record it existed to keep.

**Paired behaviour check.** `DL-03`.

**Known false positives.** Matches inside code blocks and quotations.

### `DL-05` · `path_exists` · behaviour

**Binds** `decision_index`.

**Finding.** The decision log has no index. Past a few hundred lines it becomes
a file that is written to and never read from.

**Known false positives.** Under `single-log`, `decision_index` normally maps to
the same path as `decision_log`, so this check passes whenever `DL-01` does. That
is intended — under that form the index is a section, and no check here can see
a section. The judgment entry below covers it.

### `DL-06` · `links_resolve` · behaviour

**Binds** `decision_log`, `decision_index`.

**Finding.** A relative link or anchor in the decision records does not resolve.
An index whose links have rotted is an index nobody can use, which returns the
log to being unindexed.

**Known false positives.** None. External schemes are not checked.

## Judgment

### `decision-log.claim-shaped`

**Question.** Are entry headings assertions that can be true or false, or are
they topics?

**Read** `decision_log`.

**Evidence.** Quote headings verbatim. "Caching" is a topic; "Cache lifetime is
clamped to the link's expiry" is a claim. Topics accumulate and can never be
contradicted, so a log of topics cannot correct itself — which disables the
mechanism the whole module is built on.

**Do not report.** Headings that are claims but that you would have worded
differently.

### `decision-log.corrections-preserve`

**Question.** Where a later entry contradicts an earlier one, is the earlier
text still present with a pointer, or was it edited away?

**Read** `decision_log`.

**Evidence.** Two entry headings that cannot both be true, and whether the
earlier one acknowledges the later.

**Do not report.** An earlier entry that is merely incomplete rather than
contradicted.

### `decision-log.index-exists-in-substance`

**Question.** Under `single-log`, does the file actually contain an index, or
does `DL-05` pass only because both roles point at the same file?

**Read** `decision_index`.

**Evidence.** Whether a reader can find an entry without reading the file
top to bottom.

**Do not report.** An index that is short because the log is short.

### `decision-log.rationale-not-status`

**Question.** Does the log contain status — what is currently true, what is
done — rather than reasoning?

**Read** `decision_log`.

**Evidence.** Quote the passage. A log that accumulates status has to be kept
current, and a document that has to be kept current cannot be append-only. The
two obligations destroy each other and the log loses.

**Do not report.** Status stated as part of the context a decision was made in.
