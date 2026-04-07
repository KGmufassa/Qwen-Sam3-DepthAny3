# Slice 1: Upload To Mock Stitched Scene Implementation Plan

## Purpose

This document defines the concrete implementation plan for Slice 1.

Slice 1 is the first executable vertical slice and exists to prove:

- project creation
- multi-image upload flow
- stitched-scene shell creation
- editor entry
- basic scene graph wiring

without depending on real stitch, segmentation, depth, or export workers.

---

## Slice Goal

By the end of Slice 1, a user should be able to:

1. create a project
2. create a stitched scene
3. upload multiple images
4. finalize those uploads
5. enter the editor with a mock stitched-scene payload
6. see a real editor shell driven by saved state

This slice is about proving the product shell and control-plane wiring, not ML correctness.

---

## Scope Boundary

### In scope

- project creation
- stitched scene creation
- multi-image upload initiation and finalization
- source image registration
- normalized placeholder registration if needed for the flow
- mock stitched-scene artifact registration
- editor shell entry
- initial scene graph loading
- basic job/status placeholders where needed

### Explicitly out of scope

- real stitch worker integration
- real segmentation
- real extraction
- real depth generation
- real parallax behavior
- real export generation

---

## Frozen Dependencies

This slice must follow:

- Stage 1 frozen scope and architecture
- Stage 2 frozen schema, math, API, and worker contracts
- Stage 3 frozen editor and artifact lifecycle rules
- Stage 4 frozen slice ordering and infrastructure assumptions

This slice must not reinterpret those foundations.

---

## Slice Outcome

At completion, the system should have a working shell for:

- `Project`
- `StitchedScene`
- `SourceImage`
- `Artifact`
- minimal `Job` state where needed

and a navigable editor UI with:

- scene canvas shell
- layer/group panel shell
- inspector shell
- preview controls shell
- processing/status area shell

---

## Required Deliverables

### Backend/control-plane deliverables

- project creation endpoint
- stitched scene creation endpoint
- upload init endpoint for multiple files
- upload finalize endpoint
- source image registration logic
- mock stitched-scene creation path
- artifact registration for:
  - source original
  - source normalized placeholder if used
  - mock stitched scene
- scene fetch endpoint for editor load

### Frontend deliverables

- project creation UI
- multi-image upload UI
- upload progress feedback
- stitched-scene creation trigger or implicit flow
- editor route and shell
- editor loading state
- empty-state or mock-state handling

### Integration deliverables

- control plane can persist uploaded source image references
- editor can fetch and render scene shell from saved state
- uploaded images can be associated with the stitched scene

---

## Minimal Data Requirements

To complete Slice 1, the implementation must support at minimum:

### Project

- id
- name
- active scene id

### StitchedScene

- id
- project id
- name
- status
- dimensions
- scene defaults placeholder

### SourceImage

- id
- scene id
- source index
- original artifact id
- normalized artifact id or placeholder reference

### Artifact

- id
- scene id
- type
- storage path
- checksum if available
- coordinate space

No layer/group semantics need to be fully operational yet, but the editor shell should be ready for them.

---

## Mock Stitched Scene Strategy

Slice 1 should not wait for a real stitch worker.

Recommended approach:

- register the uploaded source images normally
- create a mock stitched scene artifact and metadata record
- use a deterministic placeholder scene state that allows the editor to load

Possible mock behavior:

- choose a placeholder stitched canvas size
- register a mock stitched artifact record
- mark the scene as editor-loadable

The mock output must still respect the Stage 2 schema contract.

---

## API Surface Needed For Slice 1

Recommended minimum routes:

- `POST /v1/projects`
- `POST /v1/scenes`
- `POST /v1/scenes/{scene_id}/uploads/init`
- `POST /v1/scenes/{scene_id}/uploads/finalize`
- `POST /v1/scenes/{scene_id}/mock-stitch`
- `GET /v1/scenes/{scene_id}`
- `GET /v1/scenes/{scene_id}/preview`

The preview endpoint may return an empty or shell payload in Slice 1 as long as it follows the frozen contract shape.

---

## Backend Task Breakdown

### 1. Project and scene persistence

Implement:

- project create
- stitched scene create
- project-to-scene linking

### 2. Upload lifecycle

Implement:

- upload init
- upload finalize
- source image registration
- artifact registration for uploaded files

### 3. Mock stitch path

Implement:

- control-plane-only mock stitched artifact generation
- artifact record creation
- scene status update to editor-ready shell state

### 4. Editor scene fetch

Implement:

- scene fetch payload
- preview shell payload

---

## Frontend Task Breakdown

### 1. Project creation flow

Build:

- create project form or action
- navigation into scene creation

### 2. Multi-image upload flow

Build:

- multi-file selection
- upload progress UI
- upload completion state

### 3. Editor shell

Build:

- editor route
- scene canvas placeholder
- layer/group panel placeholder
- inspector placeholder
- preview medium selector placeholder
- status area

### 4. Load and empty states

Build:

- loading state while scene data is fetched
- informative shell state when no layers exist yet

---

## UX Expectations For Slice 1

The user should understand:

- the project exists
- the stitched scene exists
- the uploaded images are registered
- the editor is ready for later processing stages

The user should not be misled into thinking:

- stitching is already real
- segmentation is available
- parallax is already functional

This should be communicated through labels or processing status.

---

## Error Handling For Slice 1

Must support:

- one file upload fails while others succeed
- scene creation succeeds but mock stitch path fails
- editor shell fetch fails

Required behavior:

- errors are visible
- retry path exists where reasonable
- already-saved state is preserved

---

## QA Checks For Slice 1

Minimum manual checks:

- create project successfully
- create stitched scene successfully
- upload multiple images successfully
- one failed upload does not invalidate all successful uploads
- mock stitched scene is registered
- editor loads from saved scene state
- medium selector shell is visible
- status area reflects mock or not-yet-processed state honestly

---

## Exit Criteria

Slice 1 is complete when:

1. a user can create a project and stitched scene
2. a user can upload multiple images
3. uploaded images are registered as source artifacts
4. a mock stitched-scene artifact is registered
5. the editor loads from persisted scene state
6. the editor shell reflects the frozen Stage 3 structure
7. the system does not require a real stitch worker to demonstrate the flow

---

## What This Slice Proves

If completed successfully, Slice 1 proves:

- the base control plane model works
- the scene graph can be persisted and loaded
- the editor can be entered from real saved state
- the product shell can move forward without blocking on ML integration

---

## What Comes Next

The next slice after successful completion is:

- real stitch to scene shell

That slice should replace only the mock stitched-scene generation path while preserving the same control-plane and editor shell assumptions established here.

---

## Final Slice Statement

Slice 1 establishes the stitched-scene product shell: projects, scenes, uploads, artifact registration, and editor entry all work against real saved state, while stitch generation remains mocked so the application can prove its control-plane and UI foundation before introducing worker-driven complexity.
