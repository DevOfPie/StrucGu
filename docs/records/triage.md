# Triage

Operating rules for whoever is building this, human or model.

**Style is deliberate.** Terse, trigger-first, no rationale. The rest of this
project explains itself at length; this file is read at the start of every task,
so it is optimized for scanning instead. Do not rewrite it into prose. Rationale
belongs in [decisions.md](decisions.md).

**Precedence.** [work/README.md](work/README.md) is the scope contract and wins
on *what*. This file wins on *process*. If they conflict, the conflict is a bug
— report it, do not pick.

---

## Vocabulary

| Term | Meaning |
| --- | --- |
| **In spec** | Required by the work unit currently being built. |
| **Out of spec** | Anything else, including defects found by accident. |
| **Work** | A change beyond spelling, phrasing, formatting, or the wording of docs. Anything touching the specification, a module's obligations or checks, a manifest, a template, or a fixture is work. |
| **Owner** | The repository owner. The only one who approves findings and merges. |

---

## Triggers

### An issue is found — any time, any source

```
in spec      → fix now, inside the current work unit
out of spec  → DO NOT FIX
               append one row to the findings queue, under "Open"
               continue the current work unit
```

The queue is [findings.md](findings.md). Row: what, where (`file:line`),
evidence it is real, suspected severity.

Out-of-spec items are worked only after the owner reviews and approves that
item. Approval is per item, not per batch — an unreviewed row is a report, not a
commitment.

A defect that makes the *current* work unit's claim false is in spec, whatever
it looks like. Judge by the claim, not by the file.

### A shipped unit's claim turns out to be false

It **reopens that unit** — status back to `reopened`, the correction written into
the unit's own file — rather than arriving as a successor. A successor leaves a
`done` row asserting something untrue, which is the one outcome worth spending a
reopening to avoid, and it scatters one piece of work across two numbers.

The defect still gets a [findings.md](findings.md) row first. Reopening is
scheduling, and scheduling is the owner's.

A reopened unit returns to `done` when the correction lands, so the status word
is not where the reopening survives. The unit's own file carries what was false,
what closed it, and the finding it came from. A status table that can round-trip
without leaving a mark records only the present — which is the failure
[findings.md](findings.md) moves rows rather than deleting them to avoid.

### A check is written

Write the violating fixture first, or at the same time. A check nobody has
watched fail has not been shown to detect anything.

If no tree can violate the check, the check is measuring nothing — cut it, and
record what was cut in [decisions.md](decisions.md). That list is worth more
than the checks that survived.

### A normative statement about what a checker does is written

```
a tree can pin it    → write the tree, in the same unit
no tree can pin it   → say so where the statement is made, and add it to
                       SPEC.md "What no fixture pins"
neither              → cut the statement
```

The check rule above, one level up. Prose is where an untested claim survives
longest, because nothing re-reads it and no run reports on it.

**The list belongs to [SPEC.md](../../SPEC.md), not here.** An adopter needs the
artifact — which claims are pinned and which are not; the practice that produces
it is this repository's own. Argued in
[decisions.md](decisions.md#the-cut-rule-is-this-repositorys-practice-the-list-it-produces-is-the-catalogs).

### A check could be satisfied by authoring text

Ask which kind it is. A **declaration** check — the record states its own
contract — is legitimately satisfiable by writing the sentence, because a
separate behaviour check tests whether the sentence is true. A **behaviour**
check that a machine could satisfy by writing text is measuring presence rather
than thought. Cut it.

### Before completing a commit

All must hold. Failure means the commit does not happen.

| Gate | Condition |
| --- | --- |
| Links | Every relative link and anchor in tracked `.md` resolves |
| Roles | Every check names a role the module declares; every role a check names is mapped or explicitly unmapped |
| Prose and manifest | `module.md` and `module.yaml` agree. They disagree → the conflict is a bug, report it |
| Fixtures | Every check has a violating fixture and a satisfying one, and `expected.md` names the finding |
| Vocabulary | No banned word. See [Standing rules](#standing-rules) |
| Neutrality | Nothing under `modules/` names a language, package manager, build tool, or file extension |
| Docs | **If the unit changed what an adopter or a reader would observe**, [SPEC.md](../../SPEC.md), [README.md](../../README.md) and the affected `modules/*/README.md` say so now. A claim any of them makes that this unit has just made false is a failing gate, not work for the release documentation pass |
| Scope | **One work unit per commit, maximum.** Never bundle two. Splitting one across several is fine |

Commit messages are long prose explaining *why*, not what. The diff shows what.

### Before a release is tagged

1. Every gate above, over the whole repository rather than the changed files.
2. Walk every check against this repository by hand and record the output.
3. **If the walk triggers work, repeat from step 1.** A fix that is only
   spelling, phrasing, formatting, or docs wording does not re-trigger. Anything
   else does. No exceptions for "obviously safe".
4. Then the documentation pass below.
5. Then tag.

### Documentation pass — after the walk, before the tag

Update, clean, and minimize every documentation file. Not only the ones this
release touched.

| File | Check |
| --- | --- |
| [SPEC.md](../../SPEC.md) | Every field, kind, and state a module actually uses is defined; nothing defined that nothing uses |
| [README.md](../../README.md) | Module table, base set, status line, what 0.x means |
| [CHANGELOG.md](../../CHANGELOG.md) | Entry for what shipped, with what it does not do |
| `modules/*/README.md` | Costs still true, exit instruction still one line |
| `modules/*/CHANGELOG.md` | What a previously clean adopter will newly see, stated even when the answer is "nothing" |
| [decisions.md](decisions.md) | Append-only. Never edit an entry; a later entry corrects an earlier one |
| [triage.md](triage.md) | This file. Rules learned this release |
| [records/README.md](README.md) | The map of this directory. A record file added this release appears in it; one removed does not linger |

Minimize means: delete what is no longer true, merge what is duplicated, and cut
what restates something the reader already read. It does not mean shortening
explanations that carry a reason.

Every documented claim must be verifiable by a reader who does not trust you. No
feature described in the present tense that is not built, and no module
described as adopted by anyone.

---

## Standing rules

**Verify, do not assume.** If a check passed for a reason you cannot name, it
did not pass. An unmapped role reports `skip`, never `ok`.

**Report failures plainly.** Checks that fail, steps skipped, things not
verified — say so, with the output. A green summary over a red run is the worst
possible output.

**Structure and use, not content.** A module says what shape a record has and
what it is for. It never says what to write in it.

**Roles, not names.** Never mandate a word. "Milestone", "phase", and "ADR" are
already taken in most repositories.

**Banned words.** *Certified*, *certification*, and *compliant* as a repository
status. `conforms to DL-03` is fine; "a compliant repo" is not. Both smuggle
certification back in through the README.

**No byte-mangling tools on source.** PowerShell `Get-Content`/`Set-Content` has
corrupted UTF-8 in the repository this was extracted from (em-dashes into
mojibake), and em-dashes are load-bearing for heading anchors. Use editors that
preserve bytes.

**Restore by counter-edit**, never `git checkout` — checkout has twice destroyed
uncommitted work in the repository this was extracted from.

**Nothing leaves a tracker silently.** A row removed from any tracked list —
[work/README.md](work/README.md)'s status table, its *Not in this phase* list and
its list of permitted specification edits, [findings.md](findings.md), the module
table in [README.md](../../README.md) — leaves only one of two ways:

1. **Re-homed.** It appears in another tracker, and the row it left says which.
   Moving is the normal case: a finding becomes a work unit, a question becomes a
   decision.
2. **Logged.** Its removal is an entry in [decisions.md](decisions.md) naming
   what was dropped and why.

Deciding an item no longer matters *is a decision*, and it is the one kind a
project loses without noticing: nobody writes down what they stopped caring
about, so it returns later as a fresh idea with its reasoning gone. A tracker
that can be quietly emptied tracks nothing.

**A decision made in conversation is written down before it is acted on.**
Answers given in prose evaporate — the reasoning is gone by the next session, and
the conclusion gets re-derived differently. The answer goes to
[decisions.md](decisions.md) before the change it authorizes lands, not after,
and most of all when an actor is deciding on the owner's behalf because waiting
would stall the work.

**Stop and ask** for: destructive operations, scope changes, growing the base
set, anything the owner would reasonably want to decide. Proceed without asking
for reversible work that follows from the current work unit.

**Every decision prompt carries options, costs, and a recommendation.** Each
option says what it buys *and* what it costs. The recommended one leads, marked,
and states its own con — a recommendation from the actor that will also do the
work drifts toward whatever is cheapest to build, and naming that cost is what
holds it honest. Name the default too: what happens if the answer is "you
decide", so nobody has to re-derive the choice in order to skip it. If nothing
can be recommended, say why.
