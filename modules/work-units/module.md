# work-units — obligations and checks

Normative. [module.yaml](module.yaml) carries the same content as data; if the
two disagree, this file wins and the disagreement is a defect to report.

Contract terms are defined in [SPEC.md](../../SPEC.md).

## Roles

| Role | Cardinality | Of |
| --- | --- | --- |
| `unit_dir` | dir | One record per unit of work. |
| `unit_template` | file | The skeleton new records start from. |
| `unit_index` | file | The index, and the one place rules common to all units are stated. |

Module-level exclusions from `unit_dir`: `_*`, `README.md`, `index.md`. A
template and an index living inside the directory they describe is the common
layout and must not be reported as an unfilled record.

## Obligations

### `unit-done-is-falsifiable` — a record states done as claims that can be shown false

**Purpose.** A definition of done written as an intention cannot be wrong, so
the work finishes when someone decides it feels finished. Written as claims a
skeptical reader could check, the question of whether it is done has an answer
that does not depend on who is asked.

**Required.** Yes.

**Provenance.** LinkCtrl `docs/build-notes/phase-details/_template.md:12-21`.

**Satisfied in this repository by** [docs/records/work/](../../docs/records/work/).

### `unit-risks-considered` — a record has a risks section, and it is not empty

**Purpose.** An empty risks section reads as "not considered" rather than
"considered and small", and the two are indistinguishable to a later reader who
needs to know which. Writing "Low" costs nothing and carries information.

**Required.** Yes.

**Provenance.** LinkCtrl `docs/build-notes/phase-details/_template.md:28-32`.

**Satisfied in this repository by** [docs/records/work/](../../docs/records/work/).

### `unit-states-dependencies-and-discharges` — a record names what it needs and what promise it closes

**Purpose.** Dependencies found halfway through a unit are worth more before it
starts. And a scope contract with no discharge field accumulates rows nothing
ever retires — a document says a thing is not built, the thing gets built, and
the document keeps saying it because nobody was pointed at the sentence.

**Required.** Yes.

**Provenance.** LinkCtrl `docs/build-notes/phase-details/_template.md:3-7`. The
`Discharges` field is the notable invention there and is the reason this
obligation exists separately from the one above.

**Satisfied in this repository by** [docs/records/work/](../../docs/records/work/).

### `unit-rules-stated-once` — rules common to every unit live in the index

**Purpose.** Restated per record, a shared rule is copied N times, the copies
drift, and no reader can tell which is current. The failure is silent: every
individual record looks correct.

**Required.** Yes.

**Provenance.** LinkCtrl `docs/build-notes/phase-details/README.md`, its
inherited-rules table, and the footer of `_template.md` stating that those rules
are not repeated per file.

**Satisfied in this repository by** [docs/records/work/README.md](../../docs/records/work/README.md).

## Checks

### `WU-01` · `path_exists` · behaviour

**Binds** `unit_template`.

**Finding.** No record template. Every unit's record is then invented fresh, and
the sections that carry the obligations appear in some records and not others.

**Known false positives.** None.

### `WU-02` · `heading_present` · behaviour

**Binds** `unit_template`. Both patterns must match.

```
done means|definition of done|acceptance|complete when
risk
```

**Finding.** The record template has no definition-of-done section or no risks
section. Records made from it will be missing the obligation they exist to
carry.

**Known false positives.** None material.

### `WU-03` · `heading_present` · behaviour

**Binds** `unit_dir`. Applies to every record. Both patterns must match.

```
done means|definition of done|acceptance|complete when
risk
```

**Finding.** A unit record is missing a section its own template requires.

**Known false positives.** A record for a unit that was abandoned rather than
completed is reported like any other. Exclude it or close it.

### `WU-04` · `pattern_absent` · behaviour

**Binds** `unit_dir`. No pattern may match.

```
&lt;[A-Za-z][A-Za-z ]*&gt;
TODO|TBD|FIXME
```

**Finding.** A unit record still carries template placeholder text. A record
half-filled is read as a record fully filled, and the unwritten parts are read
as deliberate.

**Known false positives.** Material. Any angle-bracketed literal in a record —
a generic type, a tag, a placeholder in a quoted command — matches the first
pattern. A record legitimately listing a TODO as a deliberate omission matches
the second. This check has the highest false-positive rate in the catalog and
an adopter who finds it noisy should turn it off rather than reword their
records around it.

### `WU-05` · `path_exists` · behaviour

**Binds** `unit_index`.

**Finding.** No index of units of work. Rules common to all of them get restated
per record, and the copies drift.

**Known false positives.** None.

### `WU-06` · `pattern_present` · behaviour

**Binds** `unit_template`. Both patterns must match.

```
depends on|depends upon|requires
discharges|closes|retires|satisfies
```

**Finding.** The record template does not ask for dependencies or does not ask
what promise the unit closes. Records made from it will state neither, and the
scope contract will accumulate rows nothing ever retires.

**Known false positives.** The words are common; a template using "requires" in
another sense passes.

### `WU-07` · `links_resolve` · behaviour

**Binds** `unit_dir`, `unit_index`, `unit_template`.

**Finding.** A relative link or anchor in a unit record, the index, or the
template does not resolve. Records link to each other for dependencies, so a
rotted link is a dependency graph that is wrong rather than merely incomplete.

**Known false positives.** None. External schemes are not checked.

## Judgment

### `work-units.done-is-falsifiable`

**Question.** Could a skeptical reader show each done bullet false?

**Read** `unit_dir`.

**Evidence.** Quote the bullet. "Improve error handling" cannot be shown false.
"Every handler returns a mapped error, asserted by the error-mapping test" can.
This is the obligation the module exists for and no check can see it.

**Do not report.** Bullets that are falsifiable but that you would have written
differently.

### `work-units.rules-not-repeated`

**Question.** Are rules common to every unit stated once in the index, or
repeated per record?

**Read** `unit_index`, `unit_dir`.

**Evidence.** A rule appearing in more than one record, and whether the copies
already differ. Copies that have already drifted are the finding; copies that
agree are the warning.

**Do not report.** A rule repeated in one record because that record needs to
state an exception to it.

### `work-units.discharges-is-real`

**Question.** Does the discharge field name a promise that actually exists
elsewhere, or was one invented to fill the field?

**Read** `unit_dir`.

**Evidence.** Follow the reference. A field filled with a restatement of the
unit's own title discharges nothing, and the obligation is better served by
saying it closes none.

**Do not report.** A unit that states it closes no promise. That is the correct
answer when it is true.

### `work-units.risks-considered`

**Question.** Do the risks sections contain considered judgments, or a word
placed there to satisfy the section?

**Read** `unit_dir`.

**Evidence.** Quote it. "Low" alone across every record in the directory is a
pattern, and the pattern is the finding rather than any single instance.

**Do not report.** A single record whose risk is genuinely low and says so.
