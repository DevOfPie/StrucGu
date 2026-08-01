# Decisions

Entries are append-only and dated. A later entry corrects an earlier one and the
earlier text stays in place.

## Index

| Entry | Covers |
| --- | --- |
| [The store is append-only](#the-store-is-append-only) | Storage shape |
| [Caching was reverted](#caching-was-reverted) | Performance |

---

## 2026-07-31 — first pass

### The store is append-only

Updating in place would lose the record that the earlier value was ever held.
See [the caching investigation](investigations/0002-caching.md).

### Caching was reverted

No faster, and no better, are different claims.
