# Decisions

Why things are the way they are. Entries are append-only and dated; a later
entry corrects an earlier one and the earlier text stays in place.

## Index

| Entry | Covers |
| --- | --- |
| [The store is append-only](#the-store-is-append-only) | Storage shape |
| [First pass](#2026-07-31--first-pass) | Everything below that heading |

The second row's anchor carries two hyphens. Its heading is `## 2026-07-31 —
first pass`; the em dash is stripped from between two spaces and both spaces
become hyphens, because runs of spaces are not collapsed. A checker that
collapses them reports `DL-06` here.

---

## 2026-07-31 — first pass

### The store is append-only

Updating in place would lose the record that the earlier value was ever held,
and that record is the one anybody actually needs later.
