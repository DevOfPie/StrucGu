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

In spec, fix it now inside the current unit. Out of spec, do not fix it —
append one row to [findings.md](findings.md) and carry on.
