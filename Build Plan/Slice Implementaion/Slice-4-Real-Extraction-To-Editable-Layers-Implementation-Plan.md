# Slice 4: Real Extraction To Editable Layers Implementation Plan

## Purpose

This document defines the concrete implementation plan for Slice 4.

Slice 4 turns committed layer seeds into real editable layer assets with base versions, thumbnails, and proper editor integration.

This is the slice where the editor becomes materially useful beyond structural setup.

---

## Slice Goal

By the end of Slice 4, a user should be able to:

1. commit masks into layer seeds
2. trigger or receive real layer extraction
3. obtain real RGBA layer outputs
4. see those outputs as editable layers in the editor
5. manage layer order, visibility, names, and group assignment against real assets

---

## Scope Boundary

### In scope

- extraction job flow
- extraction output registration
- layer version creation
- thumbnail generation
- active version assignment
- editor layer panel using real extracted assets
- baseline group assignment UI with real layers

### Explicitly out of scope

- real depth generation
- real parallax preview
- export generation

---

## Slice Dependency

Slice 4 depends on successful Slice 3 outcomes:

- committed layer seeds exist
- seed semantics are stable
- candidate/accepted mask distinction is preserved

---

## Slice Outcome

At completion, the system should have:

- extraction jobs
- base extracted RGBA layers
- optional alpha assets where applicable
- thumbnails
- active layer versions
- editor operations against real extracted layer assets

---

## Required Deliverables

### Backend/control-plane deliverables

- extraction job orchestration
- layer version persistence
- active version assignment
- thumbnail artifact registration
- scene graph updates for extracted layers

### Worker or extraction-stage deliverables

- extraction execution path
- crop/alpha output generation
- typed output metadata

### Frontend deliverables

- editor layer list populated from real extracted layers
- active layer selection on real assets
- group assignment interactions on real layers
- visible distinction between extracted layers and any pending seeds

---

## Required Data And State Changes

To complete Slice 4, the implementation must support:

### Layer state

- real layer records tied to scene
- source mask artifact reference
- active version id
- transform/default visibility/order fields

### Layer version state

- base extraction version
- RGBA artifact id
- optional alpha artifact id
- thumbnail artifact id
- active state

### Artifact state

- extracted RGBA artifact registration
- optional alpha registration
- thumbnail registration

---

## Extraction Contract Application

The extraction implementation must:

- consume committed masks
- consume stitched scene artifact
- produce base extracted layer assets
- return artifact metadata

The extraction path must not:

- invent parallax behavior
- bypass active version registration

---

## Minimum API Surface Needed

Recommended minimum routes for Slice 4:

- `POST /v1/scenes/{scene_id}/layers/extract`
- `GET /v1/jobs/{job_id}`
- `PATCH /v1/layers/{layer_id}`
- `POST /v1/groups/{group_id}/layers`
- `GET /v1/scenes/{scene_id}`

---

## Backend Task Breakdown

### 1. Extraction orchestration

Implement:

- extraction job creation
- extraction stage invocation
- result ingestion

### 2. Layer version model

Implement:

- base version creation
- active version assignment
- thumbnail and asset registration

### 3. Scene graph mutation

Implement:

- conversion of committed seeds into real layer state
- editor-facing scene payload updates

---

## Frontend Task Breakdown

### 1. Layer list from real data

Build:

- layer rows using real extracted assets
- active version indicator
- real visibility and order state

### 2. Inspector support

Build:

- name editing
- visibility editing
- transform editing shell against real layers
- group assignment controls

### 3. Seed/extraction state visibility

Build:

- clear status if a seed is not yet extracted
- clear status when extraction is complete

---

## UX Expectations For Slice 4

The user should understand:

- committed masks become real editable layers only after extraction
- extracted layers are now real scene assets
- group assignment now applies to actual layers, not placeholders

---

## Failure Handling For Slice 4

Must support:

- extraction failure for one layer but not others
- registration failure after extraction output
- active version assignment failure

Required behavior:

- unaffected layers remain usable
- failed layers are clearly marked
- retry is available where appropriate

---

## QA Checks For Slice 4

Minimum manual checks:

- committed seeds can be extracted into real layers
- extracted RGBA artifacts are registered
- thumbnails are registered
- active layer version is assigned correctly
- editor loads and displays real extracted layers
- one failed extraction does not break unrelated layers

---

## Exit Criteria

Slice 4 is complete when:

1. committed layer seeds can be extracted into real assets
2. extracted layer versions are created and registered
3. active versions are assigned correctly
4. the editor uses real extracted layers
5. users can manage names, visibility, order, and group membership on real layers
6. extraction failures are visible and retryable

---

## What This Slice Proves

If completed successfully, Slice 4 proves:

- the editor can move from semantic seeds to real visual assets
- the layer version model works
- scene graph state and artifact lifecycle remain aligned

---

## What Comes Next

The next slice after successful completion is:

- depth to parallax preview

That slice will attach depth-driven meaning and visible product value to the real stitched layers produced here.

---

## Final Slice Statement

Slice 4 turns committed masks into real editable layer assets with registered versions and thumbnails, making the stitched-scene editor materially usable as a visual authoring environment rather than only a semantic setup shell.
