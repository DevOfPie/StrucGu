# How this repository is built

A map of this directory, for someone reviewing *how* StrucGu is built rather
than what it specifies. The catalog is [SPEC.md](../../SPEC.md) and
[README.md](../../README.md); the method is the files here.

It summarizes. Every file named below is the authority on its own subject, and
where this page disagrees with one of them, it is wrong.

## Why this directory is unusual

These records are working documents **and** the repository's adoption evidence
at the same time. [strucgu.yaml](../../strucgu.yaml) maps five modules onto eight
roles across five entries here — `triage_doc` on [triage.md](triage.md),
`decision_log` and `decision_index` both on [decisions.md](decisions.md),
`findings` on [findings.md](findings.md), `unit_dir`, `unit_index` and
`unit_template` on [work/](work/), and `investigations` on
[investigations/](investigations/) — so the catalog this repository publishes is
checked against the records this repository keeps while building it.

Two roles on one file is not tidiness. Under `single-log` the decision index is a
section rather than a separate document, which is why `DL-05` passes here
whenever `DL-01` does — a documented weakness of that check, covered by a
judgment entry rather than hidden.

That is worth naming precisely, because it is easy to over-claim. It is
dogfooding, not evidence. An author writes rules they already satisfy, so a clean
run here proves very little; the fixtures under `modules/*/fixtures/` are what
show the checks detect anything. The argument is in
[decisions.md](decisions.md#self-application-is-dogfooding-not-evidence).

The second thing it means is that a change to these files can move a check
result. Anything under a mapped role is [triage.md](triage.md)'s definition of
work, not documentation wording.

## The shape of it

| File | Holds | Read when |
| --- | --- | --- |
| [triage.md](triage.md) | The operating rules. What must hold, and what to do when something is found | Every task |
| [work/README.md](work/README.md) | Scope and status. What is in, what is out, and where every unit stands | Deciding *what* |
| [work/](work/) | One definition of done per unit, plus the template new ones start from | Building one unit |
| [decisions.md](decisions.md) | Why. Append-only; a later entry corrects an earlier one, nothing is edited | Wondering why something is the way it is |
| [findings.md](findings.md) | Issues found at the wrong moment, parked rather than fixed. Open, then closed with a disposition | Something turns up out of scope |
| [investigations/](investigations/) | Questions that outgrew a decision entry and needed working through | A decision entry would have to become an essay |
| [self-walk.md](self-walk.md), [self-walk-0.2.0.md](self-walk-0.2.0.md) | Every check walked against this repository by hand, per release | Asking what a run here actually returns |
| [second-repository-walk.md](second-repository-walk.md) | The same, against a repository that is not this one | Asking whether any of it survives re-application |

Precedence is fixed and a conflict is a bug rather than a choice:
[work/README.md](work/README.md) wins on *what*, [triage.md](triage.md) wins on
*process*. An actor that finds them disagreeing reports it instead of picking.

The adopter-facing documents are one directory up and are not records:
[adopting.md](../adopting.md), [auditing.md](../auditing.md),
[conformance.md](../conformance.md) and [objections.md](../objections.md).

## Three ideas that carry most of the weight

**A finding is parked, not fixed.** Anything noticed while building something
else goes to [findings.md](findings.md) as a row with its evidence, and waits for
the owner to approve it individually. Fixing it on the spot is how a reviewable
change becomes an unreviewable one, and an unreviewed row is a report rather than
a commitment.

**A check nobody has watched fail has not been shown to detect anything.** Every
check ships with a tree that violates it and a tree that satisfies it, and a
check no tree can violate is cut — with what was cut recorded. That list is worth
more than the checks that survived.

**The records outlive whoever wrote them.** Most of the work here is done by a
language model with no memory between sessions, so a decision not written down
did not happen and an intention held in someone's head is lost at the next
boundary. Every rule in [triage.md](triage.md) is a response to that, and most
were added after the corresponding failure actually occurred —
[decisions.md](decisions.md) is append-only and records which.

## What this method is not

It is not offered as the thing the catalog recommends. StrucGu specifies the
*shape* of records and what they are for, never their content or their process,
and this directory is one repository's answer rather than the answer. A reader
looking for what adoption requires wants [adopting.md](../adopting.md); what is
here is what one project chose on top of it.
