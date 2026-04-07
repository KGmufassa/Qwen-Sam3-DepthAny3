# Slice 9: Optional Difficult-Layer Enhancements Implementation Plan

## Purpose

This document defines the concrete implementation plan for Slice 9.

Slice 9 is intentionally outside the minimum path to MVP completion. It adds optional quality improvements for difficult layers through matting refinement and optional Qwen-based content refinement.

---

## Slice Goal

By the end of Slice 9, a user may be able to:

1. refine difficult layer edges
2. run optional content enhancement on difficult layers
3. create alternate layer versions
4. switch between base and refined versions safely

---

## Scope Boundary

### In scope

- matting worker integration
- optional Qwen refinement integration
- alternate layer version creation
- active version switching against refined outputs
- clear user-facing distinction between base and enhanced versions

### Explicitly out of scope

- making refinement mandatory for baseline MVP
- auto-enhancing all layers
- replacing base versions silently

---

## Slice Dependency

Slice 9 depends on successful Slice 8 outcomes:

- baseline MVP path through export and reliability is already stable
- layer version model is proven
- failure handling is already in place

---

## Slice Outcome

At completion, the system should have:

- optional refine actions for difficult layers
- alternate layer versions
- safe activation and rollback between versions

This slice should improve quality without destabilizing the baseline scene model.

---

## Required Deliverables

### Backend/control-plane deliverables

- matting job orchestration
- layer refine job orchestration
- alternate version registration
- active version switching support

### Worker deliverables

- matting worker integration
- optional Qwen refine worker integration
- typed output metadata

### Frontend deliverables

- refine-edge action if included
- enhance-layer action if included
- active version switch UI
- revert-to-base action

---

## Required Data And State Changes

To complete Slice 9, the implementation must support:

### Layer version state

- additional version kinds:
  - `matte_refine`
  - `qwen_refine`

### Active version state

- explicit switching between base and refined versions
- history-aware version switching behavior

---

## Refinement Rules

The implementation must preserve:

- base extraction remains available
- refined outputs are alternate versions
- activation is explicit
- failed refinement never silently becomes active

These rules are mandatory.

---

## Minimum API Surface Needed

Recommended minimum routes for Slice 9:

- `POST /v1/layers/{layer_id}/matte`
- `POST /v1/layers/{layer_id}/refine-content`
- `PATCH /v1/layers/{layer_id}` or equivalent version-switch mutation
- `GET /v1/jobs/{job_id}`

---

## Backend Task Breakdown

### 1. Matting integration

Implement:

- matte job creation
- result ingestion
- alternate version registration

### 2. Optional Qwen integration

Implement:

- refine job creation
- result ingestion
- alternate version registration

### 3. Version switching

Implement:

- active version mutation
- base version restoration

---

## Frontend Task Breakdown

### 1. Difficult-layer actions

Build:

- refine-edge action
- enhance-layer action

### 2. Version state visibility

Build:

- active version indicator
- alternate version availability
- revert-to-base action

### 3. Failure visibility

Build:

- refinement pending state
- refinement failed state
- retry path if appropriate

---

## UX Expectations For Slice 9

The user should understand:

- refinement is optional
- base layers remain valid
- refined outputs are alternatives, not automatic replacements

---

## Failure Handling For Slice 9

Must support:

- matting worker unavailable
- refine worker unavailable
- failed refined output generation
- failed version activation mutation

Required behavior:

- baseline scene remains usable
- base version remains intact
- failed refinement is visible and retryable where appropriate

---

## QA Checks For Slice 9

Minimum manual checks:

- create matte-refined version
- create Qwen-refined version
- switch active version safely
- revert to base version
- failed refinement does not replace the base version

---

## Exit Criteria

Slice 9 is complete when:

1. alternate refined versions can be generated
2. active version switching works safely
3. base versions remain available
4. refinement remains optional
5. failures do not destabilize the baseline scene

---

## What This Slice Proves

If completed successfully, Slice 9 proves:

- the platform can support quality-enhancement paths without breaking the core MVP
- the layer version model is strong enough for optional advanced workflows

---

## Final Slice Statement

Slice 9 adds optional difficult-layer enhancement through matting and Qwen-based refinement while preserving the baseline stitched-scene workflow, explicit version control, and user ownership over which layer version is active.
