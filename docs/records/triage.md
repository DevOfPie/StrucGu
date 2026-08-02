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

### A check is written

Write the violating fixture first, or at the same time. A check nobody has
watched fail has not been shown to detect anything.

If no tree can violate the check, the check is measuring nothing — cut it, and
record what was cut in [decisions.md](decisions.md). That list is worth more
than the checks that survived.

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

**Stop and ask** for: destructive operations, scope changes, growing the base
set, anything the owner would reasonably want to decide. Proceed without asking
for reversible work that follows from the current work unit.
