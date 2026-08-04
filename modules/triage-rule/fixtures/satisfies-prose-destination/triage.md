# Triage

**Precedence.** The scope document wins on *what*. This file wins on *process*.
If they conflict, the conflict is a defect — report it, do not pick.

## Vocabulary

| Term | Meaning |
| --- | --- |
| **In spec** | Required by the unit of work currently being built. |
| **Out of spec** | Anything else, including defects found by accident. |

## Triggers

### An issue is found

In spec, fix it now inside the current unit. Out of spec, do not fix it — write
one row in the findings queue and carry on.

The queue is reviewed row by row by whoever owns the work. An unreviewed row is
a report, not a commitment.

## Where the records are

Named here once, so that a rule above can be read as a sentence rather than as a
path.

| Record | |
| --- | --- |
| The findings queue | [findings.md](findings.md) |
