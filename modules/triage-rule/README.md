# triage-rule

**base** · 0.1.0 · requires nothing

One document draws the line between what the work in flight requires and
everything else, says what happens on each side, and says what to do when two
documents that both govern the work disagree.

## What it is for

You are building something and you notice a defect somewhere else. There are two
bad outcomes and one good one. You fix it, and the work in flight quietly grows
until nobody can say what it was supposed to be. You remember it, and forget it.
Or the line was drawn in advance, so the answer is already decided and takes no
judgment at the moment you are least able to exercise it.

The rule is small. Its value is that it exists before you need it, in writing,
where a person joining the work reads the same answer you did.

## Benefits

- **Scope stops drifting silently.** "I noticed something" has a defined
  destination that is not the current work and is not memory.
- **The decision is made once.** Deciding whether to chase something is expensive
  in the moment and cheap in advance.
- **A newcomer inherits the judgment.** Including a model, which is where this
  pays best — an agent given a written boundary behaves consistently; one given
  none re-derives it every session, differently.
- **Conflicts surface instead of being resolved privately.** When two documents
  disagree, the reader reporting it rather than picking is how the contradiction
  gets fixed instead of being papered over by whoever read it last.

## Costs

Stated plainly, because a README that only argues one side is advertising.

- **It forbids the satisfying thing.** You will find real defects and be told to
  write them down and walk away. This is the whole point and it does not stop
  being irritating.
- **A queue nobody reviews is worse than no queue.** Deferring to a list that is
  never read is forgetting with extra steps and a clear conscience. If nobody
  will review it, do not adopt this.
- **It needs an owner.** Someone has to decide what gets promoted from the queue.
  In a project with no such person, deferred items accumulate and the rule
  becomes a way of never fixing anything.
- **The boundary is genuinely hard at the edges.** A defect that makes the
  current work's own claim false *is* in scope even though it looks incidental.
  Getting this wrong in either direction costs something, and no rule removes the
  judgment entirely.

## Who should not adopt this

- A project where one person does everything, remembers everything, and ships
  alone. The overhead is real and the failure it prevents may not be yours.
- A project with no unit of work smaller than "the whole thing" — there is no
  "in flight" for a boundary to be drawn around.
- Exploratory work where scope changing constantly is the point.

## What it does not do

It does not make the software work. It makes the boundary of a piece of work
knowable to someone who was not there when it was drawn.

It also does not check that anyone follows it. Nothing here can. The checks
confirm the rule exists, is complete, and points at a destination that is really
there — which is exactly the thing that rots silently, and is how the repository
this was extracted from ended up with a triage rule pointing at a file the queue
had moved out of.

## Adopting

```yaml
# strucgu.yaml
modules:
  triage-rule:
    version: "0.1.0"
    adopted: 2026-07-31
    roles:
      triage_doc: CONTRIBUTING.md
```

The role can be any document you already have. A section of `CONTRIBUTING.md`
is a perfectly good triage document; you do not need a new file, and you should
not create one if a reader would then have two places to look.

[templates/triage.md](templates/triage.md) is a starting point, not a
requirement. Copy it, cut what does not apply, and rename everything.

## How to stop using it

Delete the `triage-rule` block from your `strucgu.yaml`. Your document is plain
markdown and stays yours.

## Details

[module.md](module.md) — the obligations and checks, with what each one's known
false positives are.
