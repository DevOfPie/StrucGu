# work-units

optional · 0.2.1 · requires nothing

Each unit of work gets a short record: what it depends on, which promise it
closes, a definition of done stated as claims a skeptic could check, and its
risks. Rules common to every unit are stated once, in the index.

## What it is for

"Done" is the word projects lie to themselves with most. A definition of done
written as intentions — improve error handling, make the page faster, clean up
the module — cannot be shown false, so the work is done when someone decides it
feels done. Written as claims a skeptical reader could check, it either holds or
it does not.

The second half is about scale. Once there are more than a handful of units, the
rules that apply to all of them get restated per record, the copies drift, and
nobody can tell which version is current. Stating them once in the index is the
whole fix.

## Benefits

- **Done becomes checkable.** "Every relative link resolves, asserted by the
  link check" can be tested. "Documentation improved" cannot.
- **You find out what a unit depends on before starting it,** not halfway
  through.
- **Deliberate omissions get recorded** instead of being discovered later as
  gaps and treated as oversights.
- **Risks get considered rather than assumed low.** An empty risks section reads
  as "not considered"; writing "Low" forces at least the thought.
- **The record answers "why is this like this" for the unit,** which is a
  question the decision log answers for the project.

## The field worth keeping

**Discharges** — the promise elsewhere in your documentation that this unit
closes. A roadmap entry, a known limitation, a line in the README saying
something is not built yet.

Without it, scope contracts accumulate rows that nothing ever retires. The
document says a thing is not built, the thing gets built, and the document keeps
saying it for two years because nobody was pointed at the sentence. Naming the
promise at the start is the only reliable way it gets removed at the end.

If a unit closes no promise, say so. Inventing one is worse than the gap.

## Costs

- **A record per unit of work is real overhead,** and it is overhead paid before
  the work rather than after.
- **The falsifiable-claim discipline is hard and does not get easy.** Writing
  "the tests pass" takes a second; writing what specifically must be true takes
  ten minutes, and the ten minutes are the point, which does not make them
  cheap.
- **It fits projects whose work comes in units.** If yours is a continuous
  stream of small changes, the record will feel like ceremony because it is.
- **It duplicates part of what your issue tracker does.** Not all of it —
  trackers are bad at falsifiable done and worse at inherited rules — but enough
  that maintaining both is a real cost. See below.
- **Records go stale after the unit ships.** They are a statement of what was
  intended and asserted, not documentation of what exists.

## If you already have an issue tracker

You do, and it plays part of this role. Be honest about whether adding files is
worth it.

The checks here are written against files, because a checker cannot read your
tracker. If your units of work live entirely in a tracker, this module is not
usable as written, and the right move is to leave the roles unmapped — every
check reports `skip`, nothing is broken, and no findings appear.

If you think the obligations are right but the file assumption is wrong, that is
a good objection and it is the first one this catalog expects to receive. See
[docs/objections.md](../../docs/objections.md).

## Who should not adopt this

- Projects with no unit of work larger than a single change.
- Projects where the tracker is genuinely working and people use it.
- Anyone who will write the record after finishing the work. A definition of
  done written afterwards describes what happened, which is not a definition of
  done.

## Adopting

```yaml
modules:
  work-units:
    version: "0.1.0"
    adopted: 2026-07-31
    roles:
      unit_dir: docs/work/
      unit_template: docs/work/_template.md
      unit_index: docs/work/README.md
```

Call them whatever you already call them. The module names roles; "milestone",
"phase", "epic", and "ticket" are all taken and this module claims none of them.

## How to stop using it

Delete the `work-units` block from your `strucgu.yaml`. The records are plain
markdown and stay yours.

## Details

[module.md](module.md) — the obligations and checks.
[templates/](templates/) — a unit record and an index.
