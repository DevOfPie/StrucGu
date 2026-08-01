# Decisions

Why things are the way they are. Entries are append-only and dated; a later
entry corrects an earlier one and the earlier text stays in place.

## Index

| Entry | Covers |
| --- | --- |
| [The store is append-only](#the-store-is-append-only) | Storage shape |

---

## 2026-07-31 — first pass

### The store is append-only

Updating in place would lose the record that the earlier value was ever held,
and that record is the one anybody actually needs later.
