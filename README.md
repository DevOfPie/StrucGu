# StrucGu

A catalog of small, versioned modules describing how a project keeps the written
record of its own work — what is in scope, why choices were made, where findings
go that are not scope.

Adopt a module and your repository can check itself against what it claimed. It
is a way of finding drift in your own project, run by you, on your own terms.

**Status: 0.1.0.** Five modules, extracted from one repository. Expect the shape
to move. See [what 0.x means here](#what-0x-means-here).

---

## What this is not

Stated first, because every catalog of conventions eventually drifts toward
being a standards body, and the only defence is writing the refusal down where
it will be read.

- **There is no enforcement.** StrucGu never blocks your work, never opens an
  issue on your behalf, and never runs anywhere you did not run it.
- **There is no certification.** No badge, no score, no conformance level, no
  list of adopters. StrucGu keeps no records about anyone who uses it — that is
  a structural guarantee, not a promise of good behaviour. There is nothing to
  certify against because upstream holds nothing.
- **There is no tool to install.** StrucGu ships no runner, no binary, no
  action, no dependency. See [Spec, not software](#spec-not-software).
- **There is no verdict.** A check produces a *finding* — a report, with a
  location and evidence. What it is worth is yours to decide, in your own
  records, in your own words.
- **This is not proof your project is good.** These modules make a record
  recoverable by someone who was not there. That is all they do. None of it
  makes the software work.

---

## Spec, not software

Every audit tool is written in something, and something is always a language.
So StrucGu does not ship one.

What it ships instead is a **specification** — each check defined precisely
enough to implement, plus **fixtures**: tiny repository trees that violate a
check, and the exact finding a correct implementation must produce on each. You
write the checker, in whatever your project already uses, and the fixtures tell
you whether you got it right.

This costs you the checker. It buys three things: nothing new enters your
dependency manifest, your build, or your CI; a shop that has only PowerShell is
not asked to adopt a shell; and a check is defined by what it *means* rather
than by what one implementation happens to do.

If two correct-looking checkers disagree about a real repository, that is not a
bug in either of them. It is a check whose fixtures do not pin the boundary —
[file it](docs/objections.md), and the fixture that settles it becomes part of
the spec.

---

## The modules

| Module | | What it is for |
| --- | --- | --- |
| [triage-rule](modules/triage-rule/) | base | The line between what the work in flight requires and everything else, and what happens on each side. |
| [decision-log](modules/decision-log/) | base | Why choices were made. Dated, append-only, indexed; later entries correct earlier ones rather than replacing them. |
| [findings-queue](modules/findings-queue/) | base | Where a finding goes when it is real but not scope. Evidence per row, approval per item. |
| [work-units](modules/work-units/) | optional | Each unit of work states its dependencies, the promise it closes, a falsifiable definition of done, and its risks. |
| [investigations](modules/investigations/) | optional | An investigation that outgrew one decision entry: what it was tested against, what was observed, what rules came out of it. |

Each module carries a README that argues both sides — what it costs, who should
not adopt it, and how to stop using it in one line.

### Using is not adopting

Two states, both fine.

**Using** — take a template, copy the shape, ignore the rest. No declaration, no
obligations, no base set, nothing owed. Most people should start here.

**Adopting** — record it in a `strucgu.yaml` at your repository root, and your
repository now has something it can check itself against.

### Why three modules are base

Nothing makes you adopt anything. But once you do, three of the five come with
it, because the rest of the catalog rests on them and each one's absence breaks
something specific:

| Base module | What breaks without it |
| --- | --- |
| `triage-rule` | Nothing decides what belongs in the findings queue, so the queue cannot be wrong about anything. |
| `decision-log` | There is no record of why a choice was made, so a project that disagrees with a module here has nothing to argue from. |
| `findings-queue` | Every incidental discovery becomes scope, which is the failure this whole family exists to prevent. |

"Adopt StrucGu but skip the decision log" is like "use semantic versioning but
skip version numbers" — the word stops meaning anything. That is a definition,
not a demand. **The base list stays at three**, and growing it is a major
version that has to argue its case, because a base list that grows makes
adoption all-or-nothing, and all-or-nothing is enforcement wearing a new name.

---

## Adopting, in one file

One hand-edited file at your repository root. Nothing else changes — not your
build, not your CI, not your dependency manifest.

```yaml
# strucgu.yaml
schema: strucgu/adoption@1
modules:
  decision-log:
    version: "0.1.0"
    adopted: 2026-07-31
    form: per-decision-files
    effective_from: 9f3c1ab
    roles:
      decision_log: doc/adr/
      decision_index: doc/adr/README.md
```

You map **roles** to your paths. A module never names a file — it names a role,
and you say what plays it. `doc/adr/`, `NOTES.md`, `.github/QUALITY.md`; the
module does not care and must never be made to.

Start at [docs/adopting.md](docs/adopting.md), which walks both a new repository
and one with years of history and its own opinions. Then
[docs/auditing.md](docs/auditing.md) for what a checker has to do.

---

## The part that makes it worth having

A module can be wrong. The repository using it in anger is the one positioned to
find out.

When your audit reports a finding and you believe your way is the more correct
one, [file an objection](docs/objections.md) — with what your project does
instead, evidence it serves the obligation's stated purpose, and what complying
would cost you. An objection with no cost is a preference.

Four things can happen: the obligation is amended, your shape is recognised as a
legitimate alternative, the check is narrowed because it was a false positive,
or it is declined and you record the deviation with a pointer to the argument.
All four are recorded here and released as a version.

Nothing is pushed at you. The mechanism is the version pin in your own file:
your checker notices it is behind and prints one line. That is the entire push
surface, and it is a print statement.

---

## What 0.x means here

The whole catalog was extracted from a single repository. One instance is not
enough to know which conventions are general and which are one project's habits
wearing a rule's clothing. 0.x is the honest label for that: **pins are cheap,
breaking changes will happen, and the objection channel is the point rather than
the exception.**

## Provenance and evidence

Extracted from [LinkCtrl](https://github.com/DevOfPie/LinkCtrl), whose process
docs were written to be read on every task and turned out to be most of the way
to language-neutral already.

StrucGu keeps its own records under [docs/records/](docs/records/) and maps them
in its own [strucgu.yaml](strucgu.yaml). That is dogfooding, and it is
deliberately **not** offered as evidence the modules work: an author
unconsciously writes rules they already satisfy, and a catalog that leaned on
self-application would drift toward checks that are cheap to satisfy. The
evidence is the fixtures — every check ships with a tree that violates it, and a
check nobody has watched fail has not been shown to detect anything.

## Layout

| Path | |
| --- | --- |
| [SPEC.md](SPEC.md) | The module contract. Normative. Everything else is downstream of it. |
| [modules/](modules/) | The five modules. |
| [docs/](docs/) | Adopting, auditing, objections. |
| [docs/records/](docs/records/) | StrucGu's own records. |
| [strucgu.yaml](strucgu.yaml) | StrucGu's own adoption record. |

## Licence

[MIT](LICENSE) for the specification and documentation.
[MIT-0](LICENSE-templates) for everything under any `templates/` directory — the
templates exist to be copied into your repository, and a licence you have to
think about is friction where there should be none.
