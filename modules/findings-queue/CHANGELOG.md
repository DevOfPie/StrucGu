# Changelog — findings-queue

Newest first. Versions follow [semantic versioning](https://semver.org/spec/v2.0.0.html),
with bumps defined by what a previously clean adopter will newly see rather than
by how much source changed. See [SPEC.md](../../SPEC.md).

## 0.1.0 — 2026-07-31

**What a previously clean adopter will newly see: nothing — first release.**

Four obligations: the destination exists, rows carry evidence, rows carry a
review state, and the queue states that its rows are not commitments. Six
checks, `FQ-01` through `FQ-06`.

Declares [triage-rule](../triage-rule/) as a prerequisite. A checker reports
`skip` for every check here when it is not adopted — without a rule defining what
counts as out of scope, no row can be wrong about anything.

[README.md](README.md) carries a warning that a repository publishing its
documentation directory as a static site will publish this file to the public
web. That is a real consequence of a documentation convention and the role map
exists partly to avoid it.

Extracted from LinkCtrl `docs/build-notes/deferred-findings.md`.
