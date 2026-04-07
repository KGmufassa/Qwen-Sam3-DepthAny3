# Slice 7: Export Bundle Implementation Plan

## Purpose

This document defines the concrete implementation plan for Slice 7.

Slice 7 turns the saved stitched scene graph into a real export bundle and proves that the scene can leave the editor as a reusable deliverable.

---

## Slice Goal

By the end of Slice 7, a user should be able to:

1. trigger export from the stitched-scene editor
2. generate an export bundle from saved scene state
3. receive an export artifact and manifest
4. download or access the bundle

The bundle must reflect active layer versions, groups, responsive behavior, and the saved scene graph semantics.

---

## Scope Boundary

### In scope

- export job orchestration
- export worker integration
- export manifest generation
- export bundle generation
- export artifact registration
- export history listing/basic retrieval
- export readiness UX

### Explicitly out of scope

- advanced export variants beyond the baseline bundle
- publishing/distribution platform integration

---

## Slice Dependency

Slice 7 depends on successful Slice 6 outcomes:

- stitched scene graph is stable
- active layer versions are meaningful
- grouped and responsive parallax semantics are complete
- preview semantics are stable enough to preserve through export

---

## Slice Outcome

At completion, the system should have:

- export job support
- export bundle artifacts
- export manifest artifacts
- export history records
- editor-facing export readiness and result visibility

---

## Required Deliverables

### Backend/control-plane deliverables

- export trigger endpoint
- export job orchestration
- export record persistence
- manifest payload generation
- artifact registration for export outputs

### Worker deliverables

- compose/export worker integration
- bundle generation path
- typed export result output

### Frontend deliverables

- export action in UI
- export pending/success/failure state
- export download or retrieval link
- export readiness messaging

---

## Required Data And State Changes

To complete Slice 7, the implementation must support:

### Export state

- export record creation
- export status transitions
- bundle artifact reference
- manifest artifact reference

### Manifest state

Manifest must include:

- scene dimensions
- layer ordering
- group structure
- active assets
- parallax settings
- responsive settings

---

## Export Contract Application

The export path must consume:

- saved stitched scene graph
- active layer versions
- active stitched scene references where needed
- scene and group responsive behavior

The export path must not consume:

- transient preview-only state
- failed artifacts
- unaccepted candidate state

---

## Minimum API Surface Needed

Recommended minimum routes for Slice 7:

- `POST /v1/scenes/{scene_id}/export`
- `GET /v1/scenes/{scene_id}/exports`
- `GET /v1/exports/{export_id}`
- `GET /v1/jobs/{job_id}`

---

## Backend Task Breakdown

### 1. Export orchestration

Implement:

- export job creation
- worker dispatch
- export status persistence

### 2. Manifest generation

Implement:

- scene graph serialization into export manifest form
- validation that required scene fields are present

### 3. Export artifact registration

Implement:

- export bundle artifact registration
- export manifest artifact registration
- export record linking

---

## Worker Task Breakdown

### 1. Export input handling

Implement:

- consume explicit export payload
- validate required asset references

### 2. Bundle generation

Implement:

- package assets
- package runtime metadata
- return typed output metadata

---

## Frontend Task Breakdown

### 1. Export action UX

Build:

- export trigger
- export pending state
- export failed state
- export success state

### 2. Export readiness UX

Build:

- show when export is blocked by missing prerequisites
- show when export is allowed

### 3. Export retrieval UX

Build:

- export list or latest export visibility
- download or retrieve action

---

## UX Expectations For Slice 7

The user should understand:

- export packages the saved scene, not unsaved implicit UI state
- export is derived from the same semantics used in preview
- export may take time and should expose status clearly

---

## Failure Handling For Slice 7

Must support:

- export worker unavailable
- export generation failure
- artifact registration failure after bundle generation

Required behavior:

- export failure is visible
- scene remains intact
- retry is available

---

## QA Checks For Slice 7

Minimum manual checks:

- export job can be created
- export bundle is generated
- export manifest is generated
- export bundle reflects active layer versions
- export preserves group and responsive behavior
- export failure is visible and retryable

---

## Exit Criteria

Slice 7 is complete when:

1. export can be triggered from saved scene state
2. export bundle and manifest artifacts are registered
3. export records are persisted
4. the editor exposes export readiness and results
5. exported output preserves saved scene semantics
6. export failure is visible and retryable

---

## What This Slice Proves

If completed successfully, Slice 7 proves:

- the stitched scene can be delivered as a reusable product output
- export parity with scene semantics is viable
- the artifact lifecycle and export contract are operational

---

## What Comes Next

The next slice after successful completion is:

- reliability and recovery

That slice should harden retries, timeouts, worker unavailability handling, and partial completion behavior across the full baseline product path.

---

## Final Slice Statement

Slice 7 makes the stitched-scene platform deliverable by turning the accepted scene graph and active artifacts into a real export bundle and manifest while preserving the same semantics used by the editor and preview.
