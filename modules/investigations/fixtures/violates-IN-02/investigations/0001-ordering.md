# 0001 — Does the store hold ordering under concurrent writes

**Status:** accepted, 2026-07-31
**Verified against:** store 4.2.1, two writers, 10000 records each.

## Context

The design assumes ordering holds, so it was tested rather than assumed.

## Findings

**1. Ordering holds for a single writer.** 10000 records, no inversions.

**2. It does not hold across two writers.** 41 inversions in 20000 records.

## Decisions

1. A reader must not assume global ordering.
