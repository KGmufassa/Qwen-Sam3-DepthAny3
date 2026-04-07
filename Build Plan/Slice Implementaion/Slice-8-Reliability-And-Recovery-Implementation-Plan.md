# Slice 8: Reliability And Recovery Implementation Plan

## Purpose

This document defines the concrete implementation plan for Slice 8.

Slice 8 is focused on making the baseline MVP path resilient under normal failure conditions, retries, timeouts, worker unavailability, and partial completion scenarios.

---

## Slice Goal

By the end of Slice 8, the MVP should remain usable when:

- uploads partially fail
- stitch jobs fail
- segmentation jobs fail
- extraction jobs fail
- depth jobs fail
- export jobs fail
- workers are unavailable
- jobs time out

This slice does not introduce new product value. It makes the baseline value release-worthy.

---

## Scope Boundary

### In scope

- retry handling
- timeout handling
- worker unavailable behavior
- partial completion behavior
- scene-state preservation guarantees
- recovery-oriented UI states
- artifact reconciliation basics where needed

### Explicitly out of scope

- advanced automatic repair systems
- predictive failure prevention systems
- large-scale operational automation

---

## Slice Dependency

Slice 8 depends on successful Slice 7 outcomes:

- baseline stitched-scene flow exists end to end
- export exists
- preview exists
- jobs exist across all major stages

---

## Slice Outcome

At completion, the baseline MVP path should be:

- visible in failure
- recoverable in expected failure modes
- stable under partial completion
- clear about what remains usable versus unavailable

---

## Required Deliverables

### Backend/control-plane deliverables

- retry endpoints or retry support for major jobs
- timeout state handling
- worker unavailable state handling
- safe late-result handling
- artifact registration reconciliation behavior

### Frontend deliverables

- visible failure states by stage
- retry entry points
- partial completion messaging
- worker unavailable messaging
- export failure messaging

### Integration deliverables

- end-to-end failure handling across stitch, segmentation, extraction, depth, and export

---

## Reliability Scenarios To Implement

The implementation must explicitly support:

- one upload fails while others succeed
- stitch fails but source image state remains intact
- segmentation fails after stitched scene creation
- extraction fails for one layer but not others
- depth fails while editor remains usable
- export fails while scene remains unchanged
- a worker family is unavailable at request time
- a job times out and exits loading state visibly

---

## Required Backend Behaviors

### 1. Retry behavior

Implement:

- stage-appropriate retry actions
- idempotent retry-safe orchestration where relevant

### 2. Timeout behavior

Implement:

- timeout-to-failed or timeout-to-explicit-timeout state transition
- no indefinite pending UI state

### 3. Late-result safety

Implement:

- safe handling if a result arrives after timeout or cancellation
- no silent scene corruption from outdated worker responses

### 4. Partial artifact safety

Implement:

- partial outputs do not become authoritative automatically

---

## Required Frontend Behaviors

### 1. Stage-specific errors

The UI should identify:

- which stage failed
- what remains usable
- what action is available next

### 2. Retry UX

The UI should expose retry when valid for:

- stitch
- segmentation
- extraction
- depth
- export

### 3. Partial completion UX

The UI should clearly show:

- ready
- pending
- failed
- retryable

### 4. Degraded capability UX

If a worker family is unavailable:

- the relevant capability should show as unavailable
- unrelated editing features should remain available

---

## State Preservation Rules To Enforce

The implementation must preserve:

- saved groups
- saved layer order
- saved transforms
- saved parallax settings
- saved responsive overrides
- active version choices

Failures must not wipe valid scene configuration.

---

## QA Checks For Slice 8

Minimum manual checks:

- retry a failed stitch successfully
- retry a failed segmentation successfully
- retry a failed extraction successfully
- retry a failed depth job successfully
- retry a failed export successfully
- verify worker unavailable behavior
- verify timeout exits loading state
- verify scene state survives failed operations

---

## Exit Criteria

Slice 8 is complete when:

1. failures are visible by stage
2. retries exist for the major recoverable stages
3. timeouts do not leave the UI hanging indefinitely
4. worker unavailability degrades by capability
5. saved scene state survives stage failures intact
6. late or partial outputs do not silently corrupt official state

---

## What This Slice Proves

If completed successfully, Slice 8 proves:

- the baseline MVP path is operationally trustworthy enough to release
- failure and retry handling match the frozen fallback UX and lifecycle rules

---

## What Comes Next

The next slice after successful completion is:

- optional difficult-layer enhancements

That slice should not be required for MVP completion but can improve output quality for difficult cases.

---

## Final Slice Statement

Slice 8 hardens the stitched-scene platform for release by making failures visible, retries safe, degraded capability states understandable, and partial completion survivable without corrupting the saved scene graph.
