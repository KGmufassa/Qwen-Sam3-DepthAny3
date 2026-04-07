# Slice 2: Real Stitch To Scene Shell Implementation Plan

## Purpose

This document defines the concrete implementation plan for Slice 2.

Slice 2 exists to replace the mock stitched-scene generation path from Slice 1 with real stitch/alignment execution while preserving:

- the same stitched scene graph authority
- the same editor entry pattern
- the same artifact registration model

This slice is still not about segmentation, extraction, or depth. It is about making the stitched scene itself real.

---

## Slice Goal

By the end of Slice 2, a user should be able to:

1. create a project
2. create a stitched scene
3. upload multiple images
4. finalize those uploads
5. trigger a real stitch/alignment job
6. receive a real stitched scene artifact and provenance metadata
7. enter the editor with a scene shell backed by a real stitched output

---

## Scope Boundary

### In scope

- stitch job creation
- stitch worker integration
- ordered source image handling
- stitched scene artifact registration
- stitched-scene provenance registration
- scene status updates based on stitch success/failure
- editor loading from a real stitched-scene artifact
- failure and retry behavior for stitch jobs

### Explicitly out of scope

- real segmentation
- real extraction
- real depth generation
- real parallax playback
- export generation

---

## Slice Dependency

Slice 2 depends on successful Slice 1 outcomes:

- project and stitched scene creation
- source image upload/init/finalize flow
- artifact registration baseline
- editor shell route and scene fetch
- scene shell loading model

If Slice 1 is unstable, Slice 2 should not proceed.

---

## Slice Outcome

At completion, the system should have:

- real stitched scene artifacts
- source-image placement or provenance metadata
- a real stitch job lifecycle
- a control-plane-managed stitched scene readiness state
- editor entry backed by actual stitched outputs rather than mocks

---

## Required Deliverables

### Backend/control-plane deliverables

- stitch start endpoint
- stitch status endpoint
- job creation for `stitch.generate`
- worker dispatch to stitch runtime
- result ingestion and validation
- artifact registration for:
  - stitched scene artifact
  - stitched preview artifact if produced
- provenance registration for source-image-to-stitched-scene placement
- retry support for stitch jobs

### Worker deliverables

- runnable stitch/alignment worker
- typed input handling
- typed output metadata
- artifact output support
- failure reporting

### Frontend deliverables

- stitched-scene build status in the UI
- transition from “mock shell” assumptions to “real stitch in progress” semantics
- retry entry point if stitch fails
- editor entry only when scene is sufficiently ready

---

## Required Data And State Changes

To complete Slice 2, the implementation must support:

### Scene state

- stitched scene status transitions for:
  - pending
  - running
  - completed
  - failed

### Job state

- one `stitch.generate` job per stitch run
- job retry support

### Artifact state

- registration of canonical stitched scene artifact
- registration of stitched preview artifact if available

### Provenance state

- mapping from source images to stitched-scene placement metadata

---

## Stitch Worker Contract Application

Slice 2 should apply the frozen worker runtime contract directly.

The stitch worker must:

- receive ordered normalized source images
- produce a stitched scene artifact
- return placement or provenance metadata
- return typed result payloads

The worker must not:

- mutate scene graph state directly
- assign groups or layers
- decide editor readiness unilaterally

The control plane remains responsible for official registration and scene state mutation.

---

## Minimum API Surface Needed

Recommended minimum routes for Slice 2:

- `POST /v1/scenes/{scene_id}/stitch/start`
- `GET /v1/scenes/{scene_id}/stitch/status`
- `GET /v1/jobs/{job_id}`
- `POST /v1/jobs/{job_id}/retry`
- `GET /v1/scenes/{scene_id}`

The existing upload and scene fetch routes from Slice 1 remain required.

---

## Backend Task Breakdown

### 1. Stitch job orchestration

Implement:

- job creation for `stitch.generate`
- worker dispatch
- job status persistence
- result ingestion

### 2. Artifact registration

Implement:

- stitched scene artifact registration
- optional stitched preview registration
- coordinate space metadata

### 3. Provenance persistence

Implement:

- source-image ordering persistence
- placement/provenance metadata storage

### 4. Scene status transitions

Implement:

- scene pending/running/completed/failed transitions for stitch readiness

---

## Worker Task Breakdown

### 1. Input handling

Implement:

- ingestion of ordered normalized image references
- runtime validation of required artifacts

### 2. Stitch runtime

Implement:

- initial stitch/alignment execution path
- deterministic output generation where possible

### 3. Output handling

Implement:

- stitched artifact output
- placement metadata output
- typed warnings/errors

---

## Frontend Task Breakdown

### 1. Stitch initiation UX

Build:

- trigger or automatic handoff into stitch stage after upload finalize
- visible “stitching in progress” state

### 2. Status and retry UX

Build:

- stitch job status panel or state surface
- failed stitch visibility
- retry action

### 3. Editor readiness UX

Build:

- editor entry only once the stitched scene is real and scene shell is valid
- clear distinction between:
  - waiting for stitch
  - stitch failed
  - stitch completed

---

## UX Expectations For Slice 2

The user should understand:

- the stitched scene is now real, not mocked
- stitching is a heavy background stage
- editor readiness depends on stitch success

The user should not be misled into thinking:

- segmentation or depth is already available just because stitching succeeded

---

## Failure Handling For Slice 2

Must support:

- stitch worker unavailable
- stitch runtime failure
- partial or invalid worker result
- artifact registration failure after worker success

Required behavior:

- failure is visible
- retry is available when appropriate
- uploaded source images remain preserved
- scene state is not corrupted

---

## QA Checks For Slice 2

Minimum manual checks:

- upload multiple images successfully
- start stitch job successfully
- stitch job transitions through expected states
- successful stitch registers real stitched artifact
- editor loads from real stitched scene output
- failed stitch does not destroy source image registrations
- retrying stitch after failure works
- stitch status is visible and understandable

---

## Exit Criteria

Slice 2 is complete when:

1. a real `stitch.generate` job can be created
2. the stitch worker returns a real stitched scene artifact
3. the control plane registers stitched outputs correctly
4. provenance metadata is recorded
5. scene state reflects stitch readiness accurately
6. the editor loads from real stitched scene state
7. stitch failures are visible and retryable

---

## What This Slice Proves

If completed successfully, Slice 2 proves:

- worker-driven scene generation can replace mocks without breaking the shell
- artifact registration and provenance handling are viable
- the stitched scene becomes a real canonical runtime surface

---

## What Comes Next

The next slice after successful completion is:

- real segmentation to committed layer seeds

That slice should consume the real stitched scene artifact produced here and begin turning it into meaningful scene semantics.

---

## Final Slice Statement

Slice 2 replaces the mock stitched-scene shell with a real stitch/alignment pipeline, proving that uploaded source images can be transformed into a canonical stitched scene artifact and loaded into the editor through the same authoritative control-plane and scene graph model established in Slice 1.
