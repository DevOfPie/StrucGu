# 0001 — The store is append-only

**Date:** 2026-07-31
**Status:** accepted

Entries are append-only; a later record corrects an earlier one and the earlier
text is not edited away.

## Context

Updating in place would lose the record that the earlier value was ever held.
