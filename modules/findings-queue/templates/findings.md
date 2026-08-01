# Findings

Where out-of-scope issues go the moment they are found, instead of being fixed
on the spot or forgotten. Anything discovered while a unit of work is in flight
that is not required by that unit lands here as one row: what, where, the
evidence it is real, and a suspected severity.

**Nothing here is scheduled work.** Rows are reviewed and approved
individually. An unreviewed row is a report, not a commitment — which is what
keeps "I noticed something" from turning into unplanned scope.

Issues that make the *current* unit of work's own claim false are in scope by
definition and get fixed immediately, whatever file they turn up in. The test is
the claim, not the file.

The rule that decides which side of the line something falls on is in
&lt;link to your triage document&gt;.

---

## Open

| # | Finding | Where | Evidence | Severity | Reviewed |
| --- | --- | --- | --- | --- | --- |
| F1 | | | | | No |

Evidence means something someone else could check without trusting you: a
`file:line`, a quoted output, a behaviour confirmed live. "This is broken"
restates the finding and is not evidence.

Severity means what the impact is, not which tier it is in. "High" conveys
nothing a reader can act on.

## Closed

*(empty)*
