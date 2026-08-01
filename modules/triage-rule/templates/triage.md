# Triage

Operating rules for whoever is building this, human or model.

**Style.** Keep this terse and organised by trigger rather than by topic. It is
read at the start of a task, so it is optimized for scanning. Explanations of
*why* a rule exists belong in the decision log, not here.

**Precedence.** Name the document that wins on *what* is in scope, and say that
this file wins on *process*. If they conflict, the conflict is a defect — report
it, do not pick.

---

## Vocabulary

| Term | Meaning |
| --- | --- |
| **In spec** | Required by the unit of work currently being built. |
| **Out of spec** | Anything else, including defects found by accident. |
| **Work** | A change beyond spelling, phrasing, formatting, or the wording of docs. Say concretely what counts in this project. |
| **Owner** | Who approves deferred findings and merges. Name the role, or the person. |

---

## Triggers

### An issue is found — any time, any source

```
in spec      → fix now, inside the current unit of work
out of spec  → DO NOT FIX
               append one row to <link to your findings queue>
               continue the current unit of work
```

Row: what, where (`file:line`), evidence it is real, suspected severity.

Out-of-spec items are worked only after the owner reviews and approves that
item. Approval is per item, not per batch — an unreviewed row is a report, not a
commitment.

A defect that makes the *current* unit of work's claim false is in spec, whatever
it looks like. Judge by the claim, not by the file.

### Before completing a commit

List the gates that must hold. Keep the list to things that actually get run.

| Gate | Condition |
| --- | --- |
| | |

### Add the triggers this project actually has

Delete this heading. A trigger belongs here when someone has been caught out by
its absence — a rule with no incident behind it is a guess, and a file of guesses
stops being read.

---

## Standing rules

**Verify, do not assume.** If a check passed for a reason you cannot name, it did
not pass.

**Report failures plainly.** Checks that fail, steps skipped, things not
verified — say so, with the output. A green summary over a red run is the worst
possible output.

**Stop and ask** for: destructive operations, scope changes, anything the owner
would reasonably want to decide. Proceed without asking for reversible work that
follows from the current unit.
