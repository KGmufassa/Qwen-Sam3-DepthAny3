# Slice 3: Real Segmentation To Committed Layer Seeds Implementation Plan

## Purpose

This document defines the concrete implementation plan for Slice 3.

Slice 3 introduces real segmentation against the real stitched scene produced in Slice 2 and carries results far enough to create committed layer seeds in scene state.

This slice proves the transition from image understanding to first meaningful scene semantics.

---

## Slice Goal

By the end of Slice 3, a user should be able to:

1. open a stitched scene backed by a real stitched artifact
2. request segmentation candidates on the stitched scene
3. review returned candidate masks
4. accept selected masks
5. commit those accepted masks into layer seeds in the stitched scene graph

The result is not yet full editable RGBA layers. It is committed semantic structure.

---

## Scope Boundary

### In scope

- segmentation request flow
- segmentation worker integration
- candidate mask artifact registration
- candidate review UX
- accepted mask commit flow
- layer seed creation in scene state
- rejection behavior for unused candidates

### Explicitly out of scope

- real layer extraction assets
- real depth generation
- preview/parallax rendering
- export generation

---

## Slice Dependency

Slice 3 depends on successful Slice 2 outcomes:

- real stitched scene artifact exists
- editor loads from stitched scene state
- artifact registration is working
- stitch status and retry behavior exist

---

## Slice Outcome

At completion, the system should have:

- real segmentation requests against stitched scene artifacts
- candidate masks stored as first-class artifacts
- accepted masks committed into scene-layer seed records
- rejected candidates clearly separated from committed state

---

## Required Deliverables

### Backend/control-plane deliverables

- segmentation predict endpoint
- segmentation session or request orchestration
- job creation for `segment.generate` if async
- candidate mask artifact registration
- commit-mask endpoint
- layer seed creation logic
- job status and retry behavior

### Worker deliverables

- runnable segmentation worker
- prompt input handling
- candidate mask generation
- candidate metadata output
- failure reporting

### Frontend deliverables

- segmentation request UI
- candidate list or candidate overlay review UI
- accept/reject interactions
- committed state feedback in the editor

---

## Required Data And State Changes

To complete Slice 3, the implementation must support:

### Candidate state

- candidate masks associated to one segmentation request/session
- candidate status visible in UI

### Layer seed state

- committed masks become layer seeds
- committed layer seeds are attached to the stitched scene
- committed seeds are distinct from extracted layers

### Artifact state

- candidate masks are artifacts
- accepted mask provenance is traceable to the segmentation job

---

## Segmentation Worker Contract Application

The worker must:

- consume the stitched scene artifact
- consume prompt inputs
- produce candidate mask artifacts and metadata

The worker must not:

- create final layer records directly
- decide which masks are accepted
- mutate scene graph state directly

That responsibility remains with the control plane.

---

## Minimum API Surface Needed

Recommended minimum routes for Slice 3:

- `POST /v1/scenes/{scene_id}/segment/predict`
- `GET /v1/jobs/{job_id}`
- `POST /v1/scenes/{scene_id}/layers/commit-mask`
- `POST /v1/jobs/{job_id}/retry`
- `GET /v1/scenes/{scene_id}`

Optional helper route if useful:

- `GET /v1/scenes/{scene_id}/segmentation/candidates`

---

## Backend Task Breakdown

### 1. Segmentation orchestration

Implement:

- request validation
- segmentation job creation
- worker dispatch
- result ingestion

### 2. Candidate artifact handling

Implement:

- candidate mask registration
- candidate metadata persistence
- linkage to request/job provenance

### 3. Commit flow

Implement:

- accepted mask commit logic
- committed layer seed creation
- scene graph update

---

## Worker Task Breakdown

### 1. Input handling

Implement:

- prompt ingestion
- stitched-scene artifact access
- coordinate-space-aware output handling

### 2. Segmentation runtime

Implement:

- candidate generation
- candidate metadata production

### 3. Result handling

Implement:

- output artifact emission
- typed warning/error return

---

## Frontend Task Breakdown

### 1. Segmentation initiation UX

Build:

- trigger segmentation request
- visible “segmentation running” state

### 2. Candidate review UX

Build:

- candidate preview or list
- accept action
- reject or ignore action
- clear distinction between candidate and committed state

### 3. Committed state UX

Build:

- committed masks reflected as layer seeds in the editor shell
- status indication that they are seeds, not yet extracted full assets

---

## UX Expectations For Slice 3

The user should understand:

- segmentation results are candidates until committed
- only committed masks affect scene structure
- committed masks prepare the scene for extraction, not final visual readiness

---

## Failure Handling For Slice 3

Must support:

- segmentation worker unavailable
- segmentation request failure
- invalid/empty candidate results
- commit-mask mutation failure

Required behavior:

- failure is visible
- retry is available where appropriate
- existing scene state remains intact

---

## QA Checks For Slice 3

Minimum manual checks:

- run segmentation successfully on a stitched scene
- receive candidate masks
- accept selected masks
- reject/ignore unused candidates
- committed masks become layer seeds
- candidates do not silently become committed state
- segmentation failure is visible and retryable

---

## Exit Criteria

Slice 3 is complete when:

1. segmentation can run on a real stitched scene artifact
2. candidate masks are returned and registered
3. users can review candidate masks
4. accepted masks can be committed
5. committed masks create layer seeds in the stitched scene graph
6. unaccepted candidates remain non-authoritative
7. failures are visible and retryable

---

## What This Slice Proves

If completed successfully, Slice 3 proves:

- the stitched scene can be converted into structured semantic editing units
- control plane and worker roles remain clean
- scene graph mutation from accepted segmentation works correctly

---

## What Comes Next

The next slice after successful completion is:

- real extraction to editable layers

That slice should consume the committed layer seeds created here and turn them into active visual layer assets.

---

## Final Slice Statement

Slice 3 introduces real segmentation against the stitched scene and establishes the commit boundary between candidate understanding and authoritative scene structure by turning accepted masks into committed layer seeds in the stitched scene graph.
