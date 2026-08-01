# 0001 — Does the store hold ordering under concurrent writes

**Status:** accepted, 2026-07-31
**Verified against:** store 4.2.1, two writers, 10000 records each.

## Context

The design assumes ordering holds. Getting it wrong would have meant rewriting
the reader, so it was tested rather than assumed.

## Findings

**1. Ordering holds for a single writer.** 10000 records, read back in order,
no inversions.

**2. It does not hold across two writers.** 41 inversions in 20000 records.
This is the same conclusion the design expected but for a different reason —
the failure is interleaving at commit, not at write.

## Decisions

1. A reader must not assume global ordering.
2. Per-writer ordering may be assumed and is asserted by the reader test.

## Reproducing

The harness was deliberately not kept. Rebuilding it means two writers against
one store and a reader checking for inversions; the findings above are the
durable part.

See also [the storage decision](../decisions.md#the-store-is-append-only).
