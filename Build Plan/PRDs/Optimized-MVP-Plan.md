# Optimized MVP Plan

This version keeps the original intent, but makes the MVP more efficient by adding missing planning tracks, hard dependency gates, mock-first integration, canonical math rules, and vertical release slices.

## Core Principle

Build the MVP around three parallel tracks instead of one long feature sequence:

- `Core contracts`
  Schema, scene graph, API contracts, artifact contracts, coordinate math, decision log
- `User workflow`
  Upload, segmentation UX, editor UX, preview UX, export UX, fallback UX
- `Execution platform`
  Workers, queues, storage, caching, health, deployment, observability

This prevents frontend, backend, and worker work from blocking each other unnecessarily.

---

# 1. Expanded Planning Stack

The original 8-document planning stack should be expanded into 14 planning documents.

## A. Strategy And Scope

### 1. MVP Scope Plan
Defines:
- exactly what MVP includes
- exactly what MVP excludes
- acceptance criteria
- release boundary

### 2. Decision Log Plan
Tracks irreversible or high-cost decisions:
- canonical scene graph structure
- coordinate-space rules
- depth artifact format
- worker boundaries
- artifact storage rules
- caching rules
- preview vs export fidelity expectations

### 3. Dependency Gate Plan
Defines what must be frozen before downstream work starts.

Examples:
- do not build editor persistence until scene graph is frozen
- do not build preview runtime until depth and motion contracts are frozen
- do not add Qwen refine until base extraction path is stable

---

## B. Contracts And Data

### 4. Unified Architecture Plan
Defines:
- control plane
- worker plane
- service boundaries
- local API vs remote inference responsibilities
- stage handoff contracts

### 5. Data Schema And Scene Graph Plan
Defines:
- `Project`
- `Scene`
- `Layer`
- `Asset`
- `Artifact`
- `PipelineRun`
- `Job`
- `ExportManifest`

Also defines:
- layer versions
- refinement variants
- scene playback settings
- reproducible export state

### 6. API And Job Contract Plan
Defines typed contracts for:
- upload
- segmentation
- mask commit
- extraction
- depth
- matting
- optional refinement
- preview
- export
- job status and retries

### 7. Canonical Math Plan
Defines all coordinate systems and transforms:

- original image space
- normalized image space
- mask space
- crop space
- canvas/editor space
- preview runtime space
- export/runtime space

Also defines:
- origin rules
- scaling rules
- transform composition order
- depth-to-motion mapping rules

This is mandatory for avoiding drift across editor, workers, and export.

---

## C. Workflow And UX

### 8. Editor UX And Interaction Plan
Defines:
- upload to editor path
- segmentation approval flow
- layer list behavior
- inspector behavior
- depth/parallax editing
- reordering
- hide/show
- naming
- undo/redo
- refinement toggles
- layer version switching

### 9. Fallback UX Plan
Defines what happens when:
- segmentation is poor
- depth is wrong
- a worker is offline
- a job stalls
- refinement output is worse
- export fails

### 10. State And History Plan
Defines:
- undoable operations
- redo behavior
- async job effects on history
- alternate layer version handling
- revert-to-base behavior
- autosave and restore semantics

---

## D. Runtime And Operations

### 11. Worker Runtime Contract Plan
Defines:
- each worker’s responsibility
- request/response schemas
- job lifecycle
- timeouts
- idempotency
- retry behavior
- output artifact contract

Workers:
- segmentation
- depth
- matting
- optional layer-refine
- compose/export

### 12. Deployment And Infrastructure Plan
Defines:
- local dev stack
- queue topology
- storage topology
- health checks
- readiness rules
- remote GPU integration
- environment separation
- rollout path from local to production

### 13. Caching And Performance Plan
Defines:
- image normalization caching
- segmentation embedding caching
- depth cache keyed by checksum + model version
- thumbnail/preview caching
- export cache
- performance budgets

Performance budgets should include:
- upload-to-first-mask latency
- depth turnaround
- preview FPS
- export time
- max supported input size

### 14. QA And Release Readiness Plan
Defines:
- golden test image set
- segmentation validation
- depth sanity tests
- editor correctness tests
- preview fidelity checks
- export reproducibility tests
- resume/retry/reconnect QA
- release checklist

---

# 2. Hard Dependency Gates

These gates make the plan more efficient by preventing premature implementation.

## Gate 1: Scope Freeze
Must be complete before implementation starts:
- MVP scope plan approved
- non-goals approved
- release boundary approved

## Gate 2: Contract Freeze
Must be complete before frontend/editor integration:
- architecture plan approved
- scene graph/schema approved
- API/job contracts approved
- canonical math plan approved

## Gate 3: Mock Integration Ready
Must be complete before real worker integration:
- mock responses defined for segmentation, extraction, depth, export
- UI and API can run end-to-end without GPU inference

## Gate 4: Base Pipeline Stable
Must be complete before advanced refinement:
- upload works
- segmentation works
- masks commit correctly
- layers extract correctly
- editor loads layers
- depth works
- preview works
- export works

## Gate 5: Optional Enhancements
Only after Gate 4:
- matting polish
- Qwen layer refine
- advanced heuristics
- multi-image stitching

---

# 3. Mock-First Integration Strategy

This is one of the biggest efficiency gains.

## Build mocks first for:

- `segment.predict`
  returns deterministic mask candidates
- `extract.layer`
  returns deterministic RGBA layer outputs
- `depth.generate`
  returns deterministic depth map metadata and layer metrics
- `export.bundle`
  returns deterministic downloadable scene bundle metadata

## Why this matters

It allows these tracks to move in parallel:

- frontend editor and preview
- backend API routes
- scene graph persistence
- export pipeline
- job orchestration

You do not need real SAM3 or Depth Anything 3 online before the app becomes internally testable.

---

# 4. Recommended Worker Strategy

Split worker planning into two layers.

## Layer A: Worker Runtime Contracts
Focus on:
- input validation
- artifact inputs
- artifact outputs
- timeouts
- retries
- model version reporting
- idempotency keys

## Layer B: Worker Deployment
Focus on:
- Runpod vs local workers
- queue binding
- storage credentials
- health/readiness
- autoscaling
- GPU assignment

Do not mix these concerns in one plan.

---

# 5. Canonical Data And Artifact Rules

To improve efficiency, freeze these rules early.

## Canonical source-of-truth rules

- The local app owns project, scene, layer, artifact, job, and export state.
- Remote workers are pure inference executors.
- Workers never become the source of truth for scene structure.
- Preview and export must both derive from the scene graph, not hidden defaults.

## Canonical artifact rules

Every generated output should be registered as an artifact with:
- artifact id
- scene id
- pipeline run id
- stage
- type
- model name/version
- checksum
- dimensions
- coordinate space
- creation timestamp

## Canonical layer rules

Each layer should track:
- source mask artifact
- current active RGBA artifact
- optional alternate versions
- depth metrics
- transform state
- visibility
- name
- order index
- provenance

---

# 6. Optimized Build Sequence

This is the efficient build order after restructuring.

## Phase 0: Planning Freeze
Deliverables:
- MVP Scope Plan
- Decision Log Plan
- Dependency Gate Plan

## Phase 1: Contract Freeze
Deliverables:
- Unified Architecture Plan
- Data Schema And Scene Graph Plan
- API And Job Contract Plan
- Canonical Math Plan

## Phase 2: Mock End-to-End Slice
Deliverables:
- upload flow
- mock segmentation
- mask commit
- mock layer extraction
- editor loading
- mock depth
- preview loading
- mock export

Goal:
- prove the whole app works without real ML

## Phase 3: Real Segmentation Slice
Deliverables:
- SAM3 worker integration
- segmentation session handling
- mask approval UX
- committed mask persistence

## Phase 4: Real Extraction Slice
Deliverables:
- layer extraction pipeline
- artifact registration
- thumbnails
- editor integration with real layer data

## Phase 5: Real Depth Slice
Deliverables:
- Depth Anything 3 integration
- full depth artifact storage
- preview depth artifact
- per-layer depth metrics
- default parallax settings

## Phase 6: Preview And Motion Slice
Deliverables:
- depth-based motion defaults
- manual depth override
- preview renderer
- playback contract stabilization

## Phase 7: Export Slice
Deliverables:
- export manifest
- scene bundle generation
- reproducible output from scene graph
- export status and download flow

## Phase 8: Reliability Slice
Deliverables:
- retries
- cancellation
- idempotency
- stalled-job handling
- health/readiness checks
- cleanup rules
- observability

## Phase 9: Quality Slice
Deliverables:
- QA image set
- regression checks
- preview/export comparison checks
- reconnect/resume testing

## Phase 10: Optional MVP+ Polish
Only after all MVP acceptance criteria pass:
- matting improvements
- optional Qwen layer refinement
- UX polish for difficult layers

---

# 7. Vertical Release Slices

This is how to make progress visible and testable.

## Slice 1: Upload To Mock Editor
Flow:
- create project
- upload image
- create scene
- inject mock masks/layers
- load editor

Outcome:
- editor and scene graph validated early

## Slice 2: Real Segmentation To Layer Commit
Flow:
- upload image
- run SAM3 prompts
- approve masks
- save layer seeds

Outcome:
- segmentation UX and persistence validated

## Slice 3: Real Extraction To Editable Layers
Flow:
- committed masks
- extract RGBA layers
- generate thumbnails
- load editor with real data

Outcome:
- layer pipeline validated

## Slice 4: Depth To Parallax Preview
Flow:
- run depth
- compute layer metrics
- assign defaults
- preview scroll parallax

Outcome:
- actual product value becomes visible

## Slice 5: Export Bundle
Flow:
- compile scene graph
- package assets
- output bundle
- verify preview/export consistency

Outcome:
- MVP becomes deliverable

## Slice 6: Reliability And Recovery
Flow:
- retry failed jobs
- reconnect after disconnect
- recover from worker failure
- verify cleanup and idempotency

Outcome:
- MVP becomes usable, not just demoable

## Slice 7: Optional Difficult-Layer Enhancements
Flow:
- matting refinement
- optional Qwen enhance
- reversible version switching

Outcome:
- quality improvement without blocking MVP

---

# 8. Parallel Workstreams

To speed implementation, these can run in parallel after contract freeze.

## Parallel Track A: Core Contracts
- schema
- scene graph
- API contracts
- canonical math
- decision log

## Parallel Track B: Frontend Workflow
- upload UX
- segmentation UX
- editor shell
- preview shell
- export UX

## Parallel Track C: Backend Control Plane
- routes
- job orchestration
- artifact registration
- persistence
- job status handling

## Parallel Track D: Worker Integrations
- segmentation
- depth
- matting
- refine
- compose/export

## Parallel Track E: QA And Tooling
- mock payloads
- golden images
- smoke tests
- acceptance harness

---

# 9. Efficiency Rules

These rules keep the plan lean.

- Do not integrate Qwen refine before the base segmentation/extraction/depth/export path is stable.
- Do not let preview invent its own data model; it must consume the scene graph contract.
- Do not let export use hidden defaults; store all export-relevant settings explicitly.
- Do not let workers own scene semantics; workers only produce artifacts and metadata.
- Do not build advanced motion controls before default depth-driven parallax works.
- Do not mix coordinate math across modules; all transforms must derive from the canonical math plan.
- Do not depend on real GPU workers to validate UI or API flow; use mocks first.
- Do not add multi-image stitching in MVP.

---

# 10. Updated MVP Acceptance Criteria

The MVP is complete when all of the following are true:

1. A user can create a project and upload one image.
2. The app can generate or mock segmentation candidates and let the user commit chosen masks.
3. Each committed mask becomes an editable layer in the editor.
4. Each layer has name, visibility, order, transform, and active asset state.
5. The system generates depth outputs and computes per-layer depth defaults.
6. The user can override depth/parallax behavior manually.
7. The preview reflects the saved scene graph and manual overrides.
8. The system exports a working web scene bundle from the same scene graph.
9. Retry, failure, and recovery behavior are defined and usable.
10. Optional Qwen refinement is not required for MVP completion.

---

# 11. Highest-Priority Additions To Your Existing Plan

If you want the biggest efficiency gains immediately, add these first:

1. Decision Log Plan
2. Dependency Gate Plan
3. Canonical Math Plan
4. Mock-First Integration Plan
5. State And History Plan
6. Caching And Performance Plan
7. Fallback UX Plan
8. Vertical Release Slice Plan

---

# 12. Final Recommendation

The most efficient version of this MVP is:

- contract-first
- mock-first
- slice-based
- worker-isolated
- export-reproducible
- Qwen-last

That gives you the fastest path to a usable single-image parallax editor without overbuilding the platform too early.

If you want, I can next turn this into a single markdown master document formatted as:

- `Existing Plans`
- `Missing Plans`
- `Dependency Gates`
- `Parallel Work`
- `Implementation Order`
- `MVP Completion Checklist`
