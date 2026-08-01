# decision-log

**base** · 0.1.0 · requires nothing

Why choices were made, recorded as they are made. Dated, append-only, indexed.
A later entry corrects an earlier one; the earlier text stays where it is.

## What it is for

Six months from now someone will look at a strange decision and have exactly two
options: assume it was a mistake and undo it, or leave it alone because it looks
deliberate and nobody knows. Both are bad, and both happen constantly.

Version control records *what* changed. Issue trackers record what was asked
for. Neither records the reasoning, and reasoning is the part that does not
survive in anyone's head. This module is the place it goes.

## The append-only part

This is the obligation people push back on, so here is the argument.

When a decision turns out to be wrong, the instinct is to fix the entry. Doing
that destroys the only record that the earlier belief was ever held — and that
record is the useful one. It is what tells a later reader that the question was
considered, what was known at the time, and what changed. An entry silently
brought up to date reads as though the project always knew.

So: never edit an entry. Append a new one that corrects it and says so. The old
text stays, wrong, with a pointer.

The cost is a file that grows and contains statements that are no longer true.
That is the trade, and it is worth naming: **you are choosing a longer, partly
obsolete record over a short, confident one that quietly lies about its own
history.**

## Benefits

- **Reasoning survives the people who had it.** Including your own reasoning,
  which you will not remember.
- **You stop re-litigating.** A decision with a written argument gets reopened
  when there is new information, rather than every time someone new arrives.
- **Wrong turns stay visible.** The correcting entry teaches more than the
  correct one, because it shows what looked right and why.
- **It is what an objection is made of.** If a convention here is wrong for your
  project, the argument you file upstream is your reasoning — and you need to
  have written it down to have it.

## Costs

- **It only works if you write entries as you decide, not afterwards.**
  Reconstructed rationale is the rationale you would give now, which is not what
  you were actually thinking. This is the discipline the module needs and cannot
  check.
- **The file grows and never shrinks.** A mature log is thousands of lines
  containing statements that are no longer true. The index is what keeps it
  usable, and the index is manual.
- **Append-only conflicts with common tooling.** Several decision-record tools
  rewrite a superseded record's status line in place. If you use one, you have a
  real deviation to record — see below.
- **The temptation to tidy is constant** and every instance of giving in
  destroys something you cannot get back.
- **Entries written speculatively read exactly like entries written from
  experience.** Nothing in the format distinguishes them.

## Who should not adopt this

- A project where decisions are genuinely obvious and reversible. Not everything
  needs a paper trail.
- Anyone who will treat it as documentation to be kept current. It is a log, not
  a description of the present. If you cannot leave wrong text in place, this
  module will make you unhappy and you will quietly break it.

## Two forms, both supported

| Form | Shape |
| --- | --- |
| `single-log` | One growing file, newest entry last, with an index section. |
| `per-decision-files` | One file per decision in a directory, plus an index file. The common architecture-decision-record layout. |

Both satisfy every obligation. If you already keep decision records, you almost
certainly want the second and you should not restructure anything.

**Known conflict.** Tools that manage per-file decision records commonly rewrite
a superseded record's status line in place. That is edit-in-place and `DL-03`
will report it. It is a legitimate deviation: the supersession pointer is
preserved, which is most of what append-only protects. Record it rather than
change your tooling —

```yaml
deviations:
  - check: DL-03
    title: Superseded records are edited in place by our tooling
    accepted: 2026-07-31
    by: you@example.org
    reason: >
      The tool rewrites the status line of a superseded record. The supersession
      pointer is preserved, which is the property DL-03 protects.
    scope: doc/adr/**
    review_by: 2027-01-31
```

## Adopting

```yaml
modules:
  decision-log:
    version: "0.1.0"
    adopted: 2026-07-31
    form: per-decision-files
    effective_from: 9f3c1ab
    roles:
      decision_log: doc/adr/
      decision_index: doc/adr/README.md
```

`effective_from` is required and matters more than it looks. `DL-03` inspects
history, and without a bound it reports every commit that ever removed a line
from your decision records — which on a mature repository is a wall of findings
on day one, and an audit that produces a wall of findings on day one gets deleted
on day one. Set it to the commit where you adopted.

## How to stop using it

Delete the `decision-log` block from your `strucgu.yaml`. Your entries are plain
markdown and stay yours, readable with nothing installed.

## Details

[module.md](module.md) — the obligations and checks.
[templates/](templates/) — a starting log and a starting per-decision record.
