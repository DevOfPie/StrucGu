# 0001 — Does the store hold ordering under concurrent writes

## Context

The design assumes ordering holds, so it was tested rather than assumed.

## Findings

**1. Ordering holds for a single writer.** 10000 records, no inversions.

**2. It does not hold across two writers.** 41 inversions in 20000 records.

## Decisions

1. A reader must not assume global ordering.

## Reproducing

The harness was deliberately not kept.
