# findings-queue

**base** · 0.3.0 · requires [triage-rule](../triage-rule/)

Where a finding goes when it is real but is not what you are working on. One row
per finding, with the evidence it is real and a state saying whether anyone has
reviewed it.

## What it is for

The [triage rule](../triage-rule/) says do not fix things that are outside the
current work. That instruction is worthless without somewhere for them to go —
"do not fix it" with no destination is "forget it", and everybody knows it, so
nobody obeys it.

This is the destination. Its job is to make deferring feel safe enough that
people actually defer instead of quietly fixing.

## The part that makes it work

**Approval is per item, not per batch.**

A row here is a report. It is not scheduled work, it is not a commitment, and
nobody owes anyone a fix for it. Someone reviews rows individually and decides
which become work.

Batch approval is how this mechanism dies. Approving the queue wholesale turns
every observation anyone made in passing into committed scope — which is exactly
the failure the triage rule exists to prevent, arriving through the door built to
prevent it. If the queue is ever going to be approved in bulk, do not adopt this
module; keep the findings in your head, where at least the scope creep is
visible.

## Benefits

- **Deferring stops feeling like dropping.** Which is what makes people do it.
- **Evidence is captured while it is fresh.** The `file:line` and the observation
  are cheap now and expensive to reconstruct in a month.
- **You can see how much you are deferring.** A queue growing faster than it
  drains is information about the project that nothing else surfaces.
- **"I noticed something" stops being an interrupt.** For a person and for a
  model — an agent with a queue to write to does not have to choose between
  losing the finding and abandoning the task.

## Costs

- **Someone has to review it, and that is real recurring work.** An unreviewed
  queue is the failure mode, not the exception, and it looks exactly like a
  healthy one from the outside.
- **The evidence column is only as good as the discipline.** "This is broken" is
  not evidence. A row without observation is a rumour with a row number, and no
  check can tell the difference.
- **It can become a place to put things so they stop being your problem.** Watch
  for rows that are complaints rather than findings.
- **It will contain things you never fix,** and reading it will feel bad. That
  is accurate information about the project, not a defect in the queue.

## ⚠️ If your documentation directory is published

**A repository that globs its docs directory into a static site generator will
publish this file to the public web the moment it lands there.** Your internal
list of known defects, with evidence and locations, on your documentation site.

This is a real consequence of adopting a documentation convention and it is easy
to miss until it has already happened. The mitigation is the role map: put the
queue somewhere your generator does not sweep up.

```yaml
roles:
  findings: .github/QUALITY.md   # deliberately not under docs/
```

Check this before you commit anything into it, not after.

## Who should not adopt this

- A project with nobody to review the queue. It becomes a way of never fixing
  anything while feeling organised.
- A project whose issue tracker already plays this role well and whose people
  actually use it. Two queues is worse than one — record a deviation on the
  triage module's destination obligation and point at your tracker.

## Adopting

```yaml
modules:
  findings-queue:
    version: "0.1.0"
    adopted: 2026-07-31
    roles:
      findings: .github/QUALITY.md
```

[triage-rule](../triage-rule/) must be adopted too. Not as a rule imposed on
you — without something defining what counts as out of scope, no row in this
queue can be wrong about anything, so the checks here would be testing the shape
of a list with no meaning.

## How to stop using it

Delete the `findings-queue` block from your `strucgu.yaml`. The file is plain
markdown and stays yours. If you are also dropping the triage rule, delete that
block as well.

## Details

[module.md](module.md) — the obligations and checks.
[templates/findings.md](templates/findings.md) — a starting queue.
