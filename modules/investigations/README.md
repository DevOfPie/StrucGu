# investigations

optional · 0.1.0 · requires nothing

When something had to be tested before it could be decided, the record of what
was tested, what was observed, and what rules came out of it.

## What it is for

Some decisions cannot be reasoned to. You have to go and find out — does this
tool actually behave that way, does that approach hold at this size, is the
assumption the whole design rests on true.

Afterwards there are two things worth keeping and they are different. The
**observations** are durable and expensive to reproduce. The **rules** extracted
from them are what people will actually follow. Collapsing the two produces a
document that states conclusions with no evidence, which a later reader has no
way to re-examine when circumstances change.

A decision-log entry is the right size for most of this. This module is for the
ones that are not — where the evidence is substantial enough that burying it in
a log entry loses it.

## The field that matters most

**What it was verified against**, with versions.

An investigation whose findings are true of one version of one tool, recorded
without saying which, becomes folklore within a year. Someone reads a rule, the
underlying thing changed two versions ago, and the rule is now wrong in a way
nobody can detect because the record does not say what it was ever true of.

## Benefits

- **Expensive knowledge stops being re-derived.** Someone will ask the same
  question again, probably you.
- **Evidence stays separable from conclusions,** so a later reader can re-examine
  the reasoning without repeating the work.
- **Assumptions get tested before they are built on** rather than discovered
  wrong afterwards, which is the actual value and it comes from the discipline,
  not the file.
- **Expectations that turned out wrong are visible.** "This is the conclusion we
  expected, but for a different reason than expected" is the most useful sentence
  in this kind of record, and it only exists if the format has room for it.

## Costs

- **Writing one is a real interruption** at the moment you have just learned the
  thing and want to use it.
- **Records date silently.** The version note tells a reader to check, but
  nothing tells them the record is now wrong.
- **It is easy to over-apply.** Most investigations belong in a decision-log
  entry. A directory of investigation records for things that did not need one
  is bureaucracy, and it makes the ones that mattered harder to find.
- **The reproduction section is usually written and never used.** Worth having
  anyway, but be honest that it is insurance.

## Who should not adopt this

- Projects where decisions are reasoned rather than tested.
- Anyone without a decision log. Start there — this module exists for the
  overflow, and overflow without the thing it overflows from is just a second
  decision log with a longer format.

## Adopting

```yaml
modules:
  investigations:
    version: "0.1.0"
    adopted: 2026-07-31
    roles:
      investigations: docs/adr/
```

If you already keep architecture decision records, they probably play this role
and you should map them rather than creating a second directory. Note that the
format here is a spike report rather than a classic decision record — it
separates observations from the rules drawn from them, which most decision-record
formats do not.

The obligation is `conditional`: it applies once your project has actually run
an investigation that did not fit in a decision-log entry. Before that, leave
the role unmapped and every check reports `skip`.

## How to stop using it

Delete the `investigations` block from your `strucgu.yaml`. The records are
plain markdown and stay yours.

## Details

[module.md](module.md) — the obligations and checks.
[templates/_investigation.md](templates/_investigation.md) — a starting record.
