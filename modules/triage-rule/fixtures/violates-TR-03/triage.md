# Triage

**Precedence.** The scope document wins on *what*, this file wins on *process*.
If they conflict, the conflict is a defect — report it, do not pick.

| Term | Meaning |
| --- | --- |
| **In spec** | Required by the unit of work currently being built. |
| **Out of spec** | Anything else. |

## Triggers

### An issue is found

In spec, fix it now. Out of spec, do not fix it — append a row to the deferred
findings table in the plan and carry on.
