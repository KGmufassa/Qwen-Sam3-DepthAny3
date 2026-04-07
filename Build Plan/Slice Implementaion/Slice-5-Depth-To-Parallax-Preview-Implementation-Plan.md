# Slice 5: Depth To Parallax Preview Implementation Plan

## Purpose

This document defines the concrete implementation plan for Slice 5.

Slice 5 introduces scene-level depth generation, cross-image normalization, and the first real depth-informed parallax preview.

This is the first slice that should clearly demonstrate the core stitched-scene product value.

---

## Slice Goal

By the end of Slice 5, a user should be able to:

1. generate depth for a stitched scene
2. attach normalized depth metrics to real extracted layers
3. derive default parallax behavior from those metrics
4. preview the stitched scene with visible depth-informed motion

---

## Scope Boundary

### In scope

- depth job orchestration
- depth worker integration
- canonical depth artifact registration
- depth preview artifact registration
- cross-image normalization handling
- per-layer depth metric attachment
- preview payload generation with default parallax values
- medium-selectable preview shell using real depth-informed defaults

### Explicitly out of scope

- advanced group-specific parallax authoring
- export generation
- optional difficult-layer refinement

---

## Slice Dependency

Slice 5 depends on successful Slice 4 outcomes:

- real stitched scene exists
- real extracted layers exist
- active layer versions are stable
- editor layer state is real

---

## Slice Outcome

At completion, the system should have:

- canonical depth outputs for stitched scenes
- normalized per-layer depth metrics
- default parallax settings for the preview
- a preview that demonstrates real scene depth differences

---

## Required Deliverables

### Backend/control-plane deliverables

- depth generation endpoint
- depth job orchestration
- depth artifact registration
- per-layer depth metric binding
- preview payload generation from saved scene graph plus derived defaults

### Worker deliverables

- depth worker integration
- canonical depth artifact output
- preview depth visualization output
- typed metadata output

### Frontend deliverables

- trigger depth generation if not automatic
- visible depth status
- preview mode with real parallax
- medium switch in preview using saved/default responsive logic

---

## Required Data And State Changes

To complete Slice 5, the implementation must support:

### Depth artifacts

- canonical depth artifact
- preview depth artifact

### Layer depth state

- mean depth
- median depth
- nearest depth
- farthest depth
- default parallax settings derived from depth

### Preview state

- scene payload enriched with depth-informed defaults

---

## Depth Contract Application

The depth worker must:

- consume the stitched scene artifact
- produce canonical depth output
- produce preview-friendly depth output
- return metadata for control-plane binding

The control plane must:

- bind resulting depth meaning to layers
- preserve manual override capability

---

## Minimum API Surface Needed

Recommended minimum routes for Slice 5:

- `POST /v1/scenes/{scene_id}/depth`
- `GET /v1/scenes/{scene_id}/depth/status`
- `GET /v1/scenes/{scene_id}/preview?medium=...`
- `PATCH /v1/layers/{layer_id}` for later manual override compatibility

---

## Backend Task Breakdown

### 1. Depth orchestration

Implement:

- depth job creation
- worker dispatch
- result ingestion

### 2. Depth registration

Implement:

- canonical depth artifact registration
- preview depth artifact registration

### 3. Metric aggregation

Implement:

- layer-level depth metric computation or binding
- cross-image normalization application
- default parallax derivation

### 4. Preview payload generation

Implement:

- preview payload including default parallax state
- medium-selectable response shape

---

## Frontend Task Breakdown

### 1. Depth status UX

Build:

- visible “depth pending/running/completed/failed” state
- retry entry point if needed

### 2. Preview runtime

Build:

- preview mode using returned payload
- visible depth-informed motion
- medium switch shell

### 3. Layer inspector visibility

Build:

- display layer depth values and default parallax summary
- communicate that manual overrides remain possible

---

## UX Expectations For Slice 5

The user should understand:

- depth is generating the first meaningful parallax defaults
- preview is now expressing real scene motion value
- defaults are suggestions, not permanent truth

---

## Failure Handling For Slice 5

Must support:

- depth worker unavailable
- depth job failure
- invalid or missing depth outputs
- partial scene still editable when depth fails

Required behavior:

- the editor remains usable
- preview should communicate missing depth state clearly
- retry is available

---

## QA Checks For Slice 5

Minimum manual checks:

- depth job can run on real stitched scenes
- depth artifacts are registered
- per-layer depth metrics are attached
- preview shows visible motion differences across layers
- medium switching works against the same scene graph
- failed depth does not block the rest of editing

---

## Exit Criteria

Slice 5 is complete when:

1. depth can be generated for a stitched scene
2. canonical depth and preview depth artifacts are registered
3. layer-level normalized depth metrics exist
4. preview uses real depth-informed defaults
5. medium-selectable preview works
6. depth failures are visible and recoverable

---

## What This Slice Proves

If completed successfully, Slice 5 proves:

- stitched-scene depth generation works
- cross-image depth meaning can be normalized into one scene
- the product’s core parallax value can be demonstrated

---

## What Comes Next

The next slice after successful completion is:

- grouped and responsive parallax refinement

That slice should turn the default parallax experience into the full MVP motion-control model.

---

## Final Slice Statement

Slice 5 connects the stitched-scene editor to the product’s core value by generating scene-level depth, binding normalized depth meaning to real layers, and driving the first real depth-informed parallax preview across supported media.
