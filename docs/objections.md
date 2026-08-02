# Objections

Your audit reported a finding. You think your project is right and the module is
wrong. File an objection.

This is not a complaint channel bolted on for politeness. **It is the only way a
module here finds out it is wrong.** These conventions were extracted from one
repository; the repository using one in anger is the one positioned to discover
what the author could not.

## When to file

- A check reports a finding on something you believe serves the obligation's
  stated purpose by other means.
- An obligation is wrong, or true only for the kind of project it was extracted
  from.
- A check is right but produces false positives often enough to be noise.
- **Two correct-looking checkers disagree about your repository.** That is a
  check whose fixtures do not pin the boundary, and it is a specification defect
  rather than a bug in either implementation.

## When not to file

- You do not want to do the work. That is a deviation — record it in your
  `strucgu.yaml` with a reason and move on. Nobody needs to be convinced.
- The obligation does not apply to your project. Leave the role unmapped or do
  not adopt the module. Neither requires an argument.

## Required fields

An objection missing any of these cannot be acted on.

| Field | |
| --- | --- |
| **Module, version, check id** | Objecting to a check and objecting to an obligation are different repairs. |
| **What the audit reported** | Verbatim. |
| **What your project does instead** | The alternative, concretely, with paths. |
| **Evidence it serves the obligation's stated purpose** | Not that you prefer it. The `purpose` field in `module.md` is what you are arguing against; quote it and show your alternative serves it. |
| **What complying would cost** | **The filter.** An objection with no cost is a preference. |
| **Requested outcome** | One of the four below. |

The cost field is doing most of the work. Every outcome turns on whether the
cost is real, and an objection that cannot name one is describing a
disagreement about taste — which is fine, and is what a deviation is for.

## The four outcomes

| Outcome | | Version |
| --- | --- | --- |
| **Obligation amended** | The requirement was wrong, or narrower than its purpose warranted. | major |
| **Alternative recognised** | Your shape becomes a `form` on the obligation. It is configuration from then on, not a deviation. | minor |
| **Check narrowed** | The obligation was right; the check produced a false positive. Usually ships with a new fixture. | patch |
| **Declined** | The deviation is genuinely local. | none |

All four are recorded in [decisions.md](records/decisions.md) with the reasoning,
including declined ones — a declined objection is an argument someone else will
make again, and the record is what makes the second answer consistent with the
first.

On a decline, record the deviation in your own `strucgu.yaml` with `upstream`
pointing at the objection:

```yaml
deviations:
  - check: WU-04
    title: Angle-bracketed type parameters trip the placeholder check
    accepted: 2026-07-31
    by: you@example.org
    reason: >
      Our unit records quote type signatures. WU-04 reads them as unfilled
      template placeholders.
    scope: docs/work/**
    review_by: 2027-01-31
    upstream: DevOfPie/StrucGu#14
```

The check then reports `waived` with your reason echoed, every run, forever.
That is the honest end state: visible, explained, and not pretending to be
`ok`.

## Where to file

A GitHub issue on `DevOfPie/StrucGu` is where this repository lives and is the
low-friction path.

**The fields are normative; the channel is not.** Adoption does not require a
GitHub account, so an objection carrying the fields above is an objection
however it arrives. A pull request against the relevant `module.md` works, and
carries the advantage of showing exactly what you want changed.

## A checker may draft one. A person files it.

Your checker may print a prefilled objection body with the module, version,
check id, and verbatim output already in it. That is useful — most of the fields
are mechanical.

**It must not post it.** Audit output from a private repository contains file
paths, internal project names, and quoted lines from your documents. A tool that
posts that to a public tracker is an exfiltration channel with a friendly name,
and the fact that the tool means well does not change what it is.

## What happens on this side

An accepted objection becomes a decision entry and a released version. There is
no notification, no bot, and no pull request opened against anyone.

Propagation is pull-only: your pin is exact, so your checker notices the module
it read is newer than the version you declared and prints one line pointing at
that module's changelog. You upgrade when you choose to.

That is the entire push surface, deliberately. A catalog that can change what
other repositories are checked against, without those repositories doing
anything, is enforcing — whatever the README says.
