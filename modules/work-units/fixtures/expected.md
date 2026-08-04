# Expected findings — work-units

What a correct checker produces on each tree here. If yours produces something
else, one of the two is wrong; if you believe it is this file, that is an
[objection](../../../docs/objections.md) rather than a defect in your
implementation.

**These trees deliberately contain broken links and template placeholders.**
They are fixtures, not documentation, and are excluded from any
repository-wide link check.

Every tree maps `unit_dir` at `work/`, whose module-level exclusions are `_*`,
`README.md` and `index.md` — so `_template.md` and `README.md` living inside it
are the template and the index, not unfilled records.

## `satisfies/`

No findings. `WU-01` through `WU-07` all `ok`.

## `violates-WU-01/`

`work/_template.md` is not present.

| Check | |
| --- | --- |
| `WU-01` | **finding** — no record template |
| `WU-02` `WU-06` | `skip` — the target cannot be read |
| `WU-03` `WU-04` `WU-05` `WU-07` | `ok` — the records and index are fine |

## `violates-WU-02/`

The template has a definition-of-done section and no risks section. Every record
made from it will inherit the gap.

| Check | |
| --- | --- |
| `WU-02` | **finding** — the template has no risks section |
| `WU-01` `WU-03` `WU-04` `WU-05` `WU-06` `WU-07` | `ok` |

## `violates-WU-03/`

The template is correct; `work/m1.md` is missing its risks section.

| Check | |
| --- | --- |
| `WU-03` | **finding** — `work/m1.md` is missing a section its template requires |
| `WU-01` `WU-02` `WU-04` `WU-05` `WU-06` `WU-07` | `ok` |

## `violates-WU-04/`

`work/m1.md` still carries `<title>` from the template.

| Check | |
| --- | --- |
| `WU-04` | **finding** — `work/m1.md` carries template placeholder text |
| `WU-01` `WU-02` `WU-03` `WU-05` `WU-06` `WU-07` | `ok` |

The check that catches this is also the noisiest in the catalog — any
angle-bracketed literal matches. That is documented in
[module.md](../module.md), and an adopter who hits it should turn the check off
rather than reword records around it.

## `violates-WU-05/`

`work/README.md` is not present, so nothing states the rules common to every
unit and nothing indexes them.

| Check | |
| --- | --- |
| `WU-05` | **finding** — no index of units of work |
| `WU-01` `WU-02` `WU-03` `WU-04` `WU-06` `WU-07` | `ok` |

`m1.md` in this tree deliberately does not link to the index, so `WU-07` stays
clean and the fixture tests one check.

## `violates-WU-06/`

The template asks for done and risks, and asks for neither dependencies nor the
promise the unit closes.

| Check | |
| --- | --- |
| `WU-06` | **finding** — the template does not ask for dependencies or discharges |
| `WU-01` `WU-02` `WU-03` `WU-04` `WU-05` `WU-07` | `ok` |

## `violates-WU-03-second-record/`

**Pins how a `dir` role becomes one state.** `work/` holds two records. `m1.md`
is complete; `m2.md` has a definition of done and no risks section.

| Check | |
| --- | --- |
| `WU-03` | **finding** — `work/m2.md` is missing a section its own template requires |
| everything else | `ok` |

`violates-WU-03/` already pins that the check fires on a non-conforming record.
This tree pins something the single-record trees cannot: that one bad record is
enough. A checker reporting `ok` because `m1.md` passes has read
[SPEC.md](../../../SPEC.md) as "finding only if every file fails", and no
single-record tree can tell the two rules apart.

## `violates-WU-06-one-pattern-only/`

**Pins that `pattern_present` requires every listed pattern.** The template asks
for dependencies and never asks what the unit discharges, so exactly one of
`WU-06`'s two patterns matches.

| Check | |
| --- | --- |
| `WU-06` | **finding** — the template does not ask what promise the unit closes |
| everything else | `ok` |

`violates-WU-06/` removes the content matching *both* patterns, so it fires under
either rule. This tree fires only under the rule
[SPEC.md](../../../SPEC.md) states — every listed pattern must match. A checker
satisfied by any one reports `ok` here and reproduces every other tree in the
catalog.

## `violates-WU-07/`

`work/m1.md` declares a dependency on `m0.md`, which does not exist.

| Check | |
| --- | --- |
| `WU-07` | **finding** — link to `m0.md` does not resolve |
| `WU-01` `WU-02` `WU-03` `WU-04` `WU-05` `WU-06` | `ok` |

**The second fixture modelled on real drift.** A dependency edge pointing at a
unit that was renamed or never existed is a dependency graph that is wrong
rather than incomplete, and it reads as correct to anyone who already knows the
graph.
