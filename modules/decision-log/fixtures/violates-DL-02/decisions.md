# Decisions

Entries are append-only. A later entry corrects an earlier one and the earlier
text stays in place.

## Index

| Entry | Covers |
| --- | --- |
| [The store is append-only](#the-store-is-append-only) | Storage shape |

---

### The store is append-only

Updating in place would lose the record that the earlier value was ever held.
