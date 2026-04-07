# Slice 8 Task List

## Goal

Harden the baseline MVP path for release through retries, timeouts, degraded capability handling, and partial-completion support.

## Workspace And Shared

- Add shared error/status types where missing
- Add retryable-state classification helpers
- Add timeout-state handling types

## Frontend

- Build stage-specific error states
- Build retry entry points for:
  - stitch
  - segmentation
  - extraction
  - depth
  - export
- Build degraded capability messaging
- Build partial completion status UI

## Control Plane

- Implement retry orchestration for major job types
- Implement timeout-to-failed/timeout state transitions
- Implement late-result protection
- Implement partial artifact reconciliation rules
- Ensure failed stages do not wipe saved scene configuration

## Worker

- Ensure worker responses carry enough metadata for retry/reconciliation
- Ensure workers handle duplicate/idempotent invocations safely where applicable

## Infrastructure

- Add timeout monitoring/handling strategy per job family
- Validate queue retry semantics
- Validate readiness and unavailable-worker behavior

## QA And Verification

- Verify retry works for stitch
- Verify retry works for segmentation
- Verify retry works for extraction
- Verify retry works for depth
- Verify retry works for export
- Verify worker-unavailable states degrade correctly
- Verify timeouts exit loading states
- Verify scene state survives failed operations

## Exit Checklist

- Failures are visible and actionable
- Timeouts are explicit
- Worker unavailability degrades by capability
- Saved scene state remains trustworthy
- MVP becomes release-ready
