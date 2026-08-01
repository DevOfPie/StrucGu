# Adopting

Two paths. Both end at one file added, with no change to your build, your
continuous integration, or any dependency manifest.

Before either: **you do not have to adopt anything.** Copying a template out of
[modules/](../modules/) and ignoring the rest is a legitimate and common way to
use this repository. Adoption is for when you want your repository to be able to
check itself against what it claimed.

## The honest cost, stated before the instructions

**No checker ships with this repository.** Adopting gets you a declaration and a
specification; running an audit means writing an implementation, in whatever
your project already uses.

That is a real barrier and it is the largest cost of the whole thing. What makes
it tractable: each module's `fixtures/` directory holds trees that violate each
check and the exact finding a correct implementation produces, so you can tell
whether yours is right. And the reasoning is in
[decisions.md](records/decisions.md#there-is-no-runner-and-that-is-the-largest-single-decision-here)
if you want to argue with it.

If that is not worth it to you, use the templates and skip the rest. Nothing is
lost.

---

## A new repository

1. Copy the templates you want out of the modules you want.
2. Write `strucgu.yaml` at the root.

```yaml
schema: strucgu/adoption@1

modules:
  triage-rule:
    version: "0.1.0"
    adopted: 2026-07-31
    roles:
      triage_doc: docs/triage.md
  decision-log:
    version: "0.1.0"
    adopted: 2026-07-31
    form: single-log
    effective_from: 2026-07-31
    roles:
      decision_log: docs/decisions.md
      decision_index: docs/decisions.md
  findings-queue:
    version: "0.1.0"
    adopted: 2026-07-31
    roles:
      findings: docs/findings.md
```

That is the base set. Add [work-units](../modules/work-units/) and
[investigations](../modules/investigations/) if their READMEs argue you into
them; both READMEs also argue the other way.

---

## A repository with years of history

The one this catalog is actually designed for, and the one where adoption most
often fails. Work in this order.

### 1. Map what you already have

Do not create files. Find the documents already playing these roles.

| Role | Very often already exists as |
| --- | --- |
| `triage_doc` | A section of `CONTRIBUTING.md`, or a wiki page about what gets fixed when |
| `decision_log` | `doc/adr/`, `docs/decisions/`, a design-notes directory |
| `findings` | A `KNOWN_ISSUES.md`, a tech-debt file, a pinned issue |
| `unit_dir` | Design documents per feature, RFCs, or nothing — leave it unmapped |

A section of an existing file is a perfectly good mapping. Creating a new
document because a role has a name is how you end up with two places to look,
which is worse than the state you started in.

### 2. Adopt one module

`decision-log` is usually the one. It is base, it is the one whose absence
breaks the feedback loop, and if you already keep decision records it costs a
mapping and nothing else.

Adopting one base module without the other two is a partial adoption. That is a
real and supported state — nothing reports a finding about it.

### 3. Set `effective_from` and mean it

Required for `decision-log`, because `DL-03` inspects history. Without a bound,
your first run reports every commit that ever removed a line from your decision
records, going back years.

**An audit that reports four hundred findings on day one is deleted on day one.**
Set it to the commit where you adopted. History before that is not out of
compliance; it is not covered.

### 4. Leave roles unmapped rather than inventing files

```yaml
  work-units:
    version: "0.1.0"
    adopted: 2026-07-31
    roles:
      unit_dir: ~        # our work lives in the issue tracker
      unit_template: ~
      unit_index: ~
```

Every check bound to an unmapped role reports `skip` — never `ok`, and never a
finding. `skip` means "I could not tell", which is exactly what is true.

### 5. Do not wire it into your gates yet

Run it by hand until it is clean. A check that fails on day one in a repository
with required status checks gets made non-required within the hour, and then
nobody looks at it again — which is worse than never adding it, because it looks
like coverage.

---

## Collisions, and what to do about each

These are the four that come up. None of them are reasons not to adopt; all of
them are reasons to adopt deliberately.

### Your documentation directory is published

**This is the one that can actually hurt you.** A repository that globs its docs
directory into a static site generator will publish its findings queue — an
internal list of known defects, with locations and evidence — to the public web,
the first time it builds after you commit the file.

Map the role outside the published tree:

```yaml
  findings-queue:
    roles:
      findings: .github/QUALITY.md
```

Check this before you commit anything into the queue, not after.

### Your commit messages are machine-parsed

If you run a conventional-commit linter or derive versions from commit types,
long prose commit messages will be rejected outright or will break your release
automation.

Nothing in this release checks commit messages, so there is no collision today.
It is named here because the source material this catalog was extracted from
does prescribe prose commit messages, and a future verification module may carry
that obligation. If it does, it will be off by default and this line will point
at it.

### Your decision-record tooling rewrites records in place

Common, and it conflicts directly with `decision-log`'s append-only obligation:
these tools rewrite a superseded record's status line where it stands.

Record the deviation. Do not change your tooling for this.

```yaml
deviations:
  - check: DL-03
    title: Superseded records are edited in place by our tooling
    accepted: 2026-07-31
    by: you@example.org
    reason: >
      The tool rewrites the status line of a superseded record. The supersession
      pointer is preserved, which is the property DL-03 protects.
    scope: doc/adr/**
    review_by: 2027-01-31
```

`reason` and `review_by` are both required. A deviation without a reason is
indistinguishable from a defect; one without an expiry is a silent fork.

### You already have a contributing guide

Adoption never requires replacing it. Map `triage_doc` at a section of it, or
add a link from it to whatever does play that role. Nothing here claims a
filename.

---

## Partial adoption, exclusions, and leaving

**Partial adoption** is normal. Adopt one module, leave three unmapped roles,
turn off a check you find noisy. The only thing that is not partial is the base
set's relationship to the word "adoption" — see
[SPEC.md](../SPEC.md#base-and-prerequisites).

**Exclusions** keep vendored and legacy trees out of every directory-shaped
role:

```yaml
exclude:
  - vendor/**
  - docs/legacy/**
```

**Leaving** is one line per module: delete its block from `strucgu.yaml`. Every
artifact is plain markdown and stays yours, readable with nothing installed. Each
module's README states this too, because a module you cannot leave is
enforcement by lock-in and the exit should be documented where you decide to
enter.

## Next

[docs/auditing.md](auditing.md) — what a checker has to do.
[docs/objections.md](objections.md) — when a module is wrong about your project.
