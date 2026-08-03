# Auditing

What a checker has to do, what it must never do, and what its output means.

[SPEC.md](../SPEC.md) is normative. This file is the practical version, written
for someone about to implement one.

## What an audit is

Read a repository's `strucgu.yaml`. For each adopted module, read its
`module.md` — or `module.yaml`, they say the same thing — resolve each check's
roles to paths, evaluate, and report.

That is all. It is a read operation that produces a list.

## The five states

Distinguish all five. **Never fold one into another**, and in particular never
report `skip` as `ok`.

| State | Meaning |
| --- | --- |
| `ok` | The check passed. |
| `finding` | The check failed. Report the location and what was observed. |
| `skip` | The role is unmapped, unreadable, or its module's prerequisite is not adopted. **"I could not tell."** |
| `waived` | An accepted deviation. Echo the reason every run. |
| `judgment` | Needs a person. Emit one per entry whether or not anyone is there to judge it. |

`skip` folded into `ok` is the failure that matters most, because it converts "I
did not look" into "I looked and it was fine", and nothing downstream can tell
the difference.

Emitting `judgment` lines even with nobody to read them is deliberate. A purely
mechanical run must never look complete, because it is not.

## Output

Any format. This shape works:

```
== decision-log 0.1.0 ==

  ok       DL-01  docs/decisions.md
  ok       DL-02  docs/decisions.md
  waived   DL-03  accepted 2026-07-31, review by 2027-01-31
                  Our tooling rewrites a superseded record's status line in
                  place. The supersession pointer is preserved.
  ok       DL-04  docs/decisions.md
  ok       DL-05  docs/decisions.md
  finding  DL-06  docs/decisions.md:41
                  Link to "adr/0004-caching.md" does not resolve.
  judgment decision-log.claim-shaped
  judgment decision-log.corrections-preserve
  judgment decision-log.index-exists-in-substance
  judgment decision-log.rationale-not-status

  6 checks: 4 ok, 1 finding, 0 skipped, 1 waived. 4 for judgment.

  Findings are candidates for your own findings queue, where you decide what
  they are worth. This is not a grade.
```

The summary states all five counts, including zeros. A run reporting only `ok`
and `finding` is hiding two states.

## Exit status

**Zero when the audit ran. Non-zero only when it could not.**

Could not run: no `strucgu.yaml`, an unparseable one, a version pin that is not
exact, a module directory that is not there, an adopted module with `forms` and
no `form` declared, or an adopted `history_deletions` check with no
`effective_from` — the bound is required, because without it the first run on a
mature repository produces the four-figure output that gets an audit deleted on
day one.

Findings are output, not failure. This is not a soft default that people are
expected to override — it is the recommended behaviour, and a flag to gate on
findings should exist but should have to be asked for.

**Why.** A check that fails on day one in a repository with required status
checks gets made non-required within the hour, and then nobody looks at it
again. That is how a gate dies, and a dead gate is worse than no gate because it
looks like coverage. Wire it in after your first clean run, when you are opting
into something you have seen the output of.

## What a checker must never do

**Write anything to the repository it audits.** Auditing and fixing are separate
acts; an audit that edits is a push.

**Write the adoption record.** A checker that edits `strucgu.yaml` can make
itself pass.

**Run history checks before `effective_from`.** Not a style preference — this is
the difference between a first run that produces a handful of findings and one
that produces four hundred, and an audit that produces four hundred findings on
day one is deleted on day one.

**Use write-side git.** Read-only operations only: `ls-files`, `status
--porcelain`, `rev-parse`, `log`. Never `checkout`, `stash`, `reset`, `clean`,
`add`, `commit`, `update-index`. `git checkout` used to make an operation atomic
is the single command that has already destroyed uncommitted work in the
repository this catalog came from, twice.

**Read history from the audited root, not from whatever encloses it.** Git finds
a repository by walking up; a checker must not. An adoption record vendored
inside a monorepo, or a submodule checked out in place, is otherwise audited
against history its owner does not control. Where the audited root is not itself
a repository root there is no history to read.

**File anything anywhere.** See [objections](#objections-are-drafted-not-filed).

## Remediation

A checker may propose. It may not fix. If yours does nothing but report, it is
complete — this section is optional capability.

| May | |
| --- | --- |
| **Scaffold** | Create a role's artifact when its path **does not exist**. Refuse if anything is there, even if malformed. Create-if-absent is the only write mode that cannot destroy information. Only for `declaration` checks and `path_exists`. |
| **Relocate** | Move existing content into the structure the module describes. |
| **Emit** | A unified diff, to standard output or a scratch path. |

| Must not | |
| --- | --- |
| Author substance | Never a risks section, a done bullet, an evidence cell, a severity. |
| Move content out of an append-only record | A move is a deletion at the source. |
| Apply anything | The owner decides. |

**Never touched under any flag:** decision-log entries, approval or review
state, dated fields, git history, commit messages, the adoption record, or any
file with uncommitted changes.

One finding, one patch. Bundling is how a remediation becomes the largest
unreviewed change in a repository's history.

Any proposal for a `declaration` check prints, verbatim:

> This makes the check pass. It does not make the claim true.

### The append-only exception, with its worked precedent

You will hit this. A triage document points at a findings queue that has moved,
and the obvious proposal is to move the section.

**If the source is append-only, do not move it.** Leave a forwarding pointer
instead. When LinkCtrl's findings queue moved out of `Plan.md`, what stayed
behind was a stub saying where it went — not a hole. A reader arriving at the old
location from a bookmark, an issue, or a stale link finds the way forward rather
than nothing.

### Why not just fix things

The full argument is in
[decisions.md](records/decisions.md#remediation-may-move-content-but-never-author-it).
The short version is two arguments, and the second is the one that generalises:

An auto-fixer violates the module it implements. The triage rule says out of
scope means do not fix. An audit finding is by construction out of scope of
whatever is in flight.

And fixability is evidence of shallowness. If a machine can satisfy a check by
writing text, the check was measuring presence rather than thought — a required
risks section, satisfied by writing "Low", passes while destroying the signal it
existed to carry. That is why the catalog cuts those checks rather than
automating them.

## Objections are drafted, not filed

A checker may print a prefilled objection body. **A person posts it.**

Audit output from a private repository contains file paths, internal project
names, and quoted lines. A tool that posts that to a public tracker is an
exfiltration channel with a friendly name. See
[objections.md](objections.md).

## Two checkers, one disagreement

No implementation is normative, so two correct-looking checkers can disagree
about a real repository.

**That is not a defect in either.** It is a check whose fixtures do not pin the
boundary. File it — the fixture that settles it becomes part of the
specification, and every other implementation gets it. This is the ordinary way
the specification gets sharper.

## Verifying your implementation

Each module has a `fixtures/` directory:

```
fixtures/
  satisfies/           a tree where every check passes
  violates-DL-01/      a tree where exactly DL-01 fails
  violates-DL-02/
  ...
  expected.md          per fixture, the exact finding a correct checker produces
```

Run yours against all of them. `satisfies/` must produce no findings; each
`violates-*` must produce exactly the finding named in `expected.md` and no
others.

This is what makes a specification with no reference implementation workable,
and it is also the only evidence the checks detect anything at all — a check
nobody has watched fail has not been shown to detect anything.
