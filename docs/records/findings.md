# Findings

Where out-of-spec issues go the moment they are found, instead of being fixed on
the spot or forgotten. Anything discovered while a work unit is in flight that is
not required by that unit lands here as one row: what, where, the evidence it is
real, and a suspected severity.

**Nothing here is scheduled work.** The owner reviews each row and approves it
individually. An unreviewed row is a report, not a commitment — which is what
keeps "I noticed something" from turning into unplanned scope.

Issues that make the *current* work unit's own claim false are in spec by
definition and get fixed immediately, whatever file they turn up in. The test is
the claim, not the file.

The rule that decides which side of the line something falls on is in
[triage.md](triage.md).

---

## Open

| # | Finding | Where | Evidence | Severity | Reviewed |
| --- | --- | --- | --- | --- | --- |
| F1 | The base set is argued in two places and could drift | [README.md](../../README.md) "Why three modules are base", and [SPEC.md](../../SPEC.md) "Base" | Both carry the what-breaks-without-it justification for the three base modules. The wording already differs — the README says "cannot be wrong about anything" where SPEC.md says "unfalsifiable". Neither is wrong today; nothing keeps them together tomorrow, and no check can see prose agreeing with prose. | Low. Both statements are currently true, and the base set is fixed at three by a rule that requires a major version to change. The risk is a future edit to one that is not made to the other. | No |
| F2 | `role_referenced` cannot see a reference written as prose | [SPEC.md](../../SPEC.md) check kinds | The check that catches a record pointing at a destination that has moved resolves markdown links only. The real drift it was modelled on — a triage document naming its findings destination in a sentence rather than a link — would not be caught if the destination were named in prose instead of linked. `TR-03`'s fixture uses a link, so the fixture passes while the general case leaks. | Moderate for what the check claims. It is the highest-value check in the catalog and its coverage is narrower than its obligation reads. Options are narrowing the obligation's wording or adding a kind that matches a path-shaped string anywhere in the target; the second produces false positives on any prose that quotes a path. | No |

## Closed

*(empty)*
