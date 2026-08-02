# Triage

**Precedence.** The scope document wins on *what*. If they conflict, the
conflict is a defect — report it, do not pick. See [scope.md](scope.md).

| Term | Meaning |
| --- | --- |
| **In spec** | Required by the unit of work currently being built. |
| **Out of spec** | Anything else, including defects found by accident. |

## Triggers

### An issue is found

In spec, fix it now. Out of spec, append one row to [findings.md](findings.md).
