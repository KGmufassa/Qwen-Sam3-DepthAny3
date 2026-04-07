# Implementation Roadmap

## Purpose

This document translates the frozen planning stack into an implementation-first roadmap.

It defines:

- build order
- execution phases
- slice goals
- cross-cutting workstreams
- what should happen before writing large amounts of production code

This roadmap is designed to reduce rework and keep visible progress aligned with the vertical slice strategy.

---

## Roadmap Principles

- implement in visible vertical slices
- keep contracts authoritative
- do not let optional features delay baseline value
- validate with mocks before depending on real ML workers
- preserve preview/export equivalence from the start

---

## Immediate Execution Rule

Before major implementation begins:

- Stage 1 must remain frozen
- Stage 2 contracts must remain frozen
- Stage 3 workflow rules must remain frozen
- Stage 4 delivery model must remain frozen

Implementation should not reopen any frozen stage unless there is a true blocker.

---

## Workstreams

Implementation should run in coordinated workstreams.

### Workstream A: Control plane

Focus:

- project/scene persistence
- jobs
- artifact registration
- API routes

### Workstream B: Web application

Focus:

- upload flow
- editor shell
- layer/group UI
- preview UX
- status handling

### Workstream C: Workers

Focus:

- stitch
- segmentation
- depth
- matting
- optional refine
- export

### Workstream D: Infrastructure

Focus:

- database
- storage
- queue
- deployment wiring
- health/readiness

### Workstream E: QA and validation

Focus:

- golden test scenes
- smoke flows
- contract checks
- preview/export consistency checks

---

## Recommended Execution Phases

### Phase 0: Repo And Runtime Setup

Goal:

- establish the codebase and infrastructure skeleton needed for execution

Deliverables:

- project structure aligned with control plane, web app, workers, and shared contracts
- local database/storage/queue setup
- environment configuration
- baseline health endpoints

### Exit condition

- developers can run the product shell and core infrastructure locally

---

### Phase 1: Core State And Contract Scaffolding

Goal:

- encode the frozen Stage 2 model into implementation scaffolding

Deliverables:

- stitched scene data model
- artifact model
- group/layer model
- job model
- API scaffolding for core domains
- shared type definitions

### Exit condition

- the codebase can represent the core entities and route domains without placeholder contract ambiguity

---

### Phase 2: Slice 1 - Upload To Mock Stitched Scene

Goal:

- make the shell usable before real worker integration

Deliverables:

- project creation
- multi-image upload flow
- mock stitched-scene generation
- editor shell loading from scene graph state
- mock groups/layers if needed

### Exit condition

- users can upload images and land in a meaningful stitched-scene editor shell

---

### Phase 3: Slice 2 - Real Stitch To Scene Shell

Goal:

- replace mock stitched scene generation with real stitch/alignment execution

Deliverables:

- stitch job flow
- stitch worker integration
- stitched artifact registration
- source provenance wiring

### Exit condition

- stitched scene artifacts are real and editor loads from them

---

### Phase 4: Slice 3 - Real Segmentation To Layer Seeds

Goal:

- make the segmentation workflow operational on real stitched scenes

Deliverables:

- segmentation request flow
- candidate handling
- mask commit logic
- seed layer creation

### Exit condition

- accepted masks mutate real scene state

---

### Phase 5: Slice 4 - Real Extraction To Editable Layers

Goal:

- convert committed seeds into real editable layer assets

Deliverables:

- extraction jobs
- base layer version registration
- thumbnails
- editor layer/group panel with real data

### Exit condition

- users can edit real extracted layers

---

### Phase 6: Slice 5 - Depth To Parallax Preview

Goal:

- deliver the core stitched-scene parallax value

Deliverables:

- depth job flow
- canonical depth artifact registration
- cross-image depth normalization
- preview payload generation
- preview runtime using real defaults

### Exit condition

- preview shows meaningful depth-informed parallax behavior

---

### Phase 7: Slice 6 - Grouped And Responsive Parallax

Goal:

- complete the core parallax control model

Deliverables:

- group CRUD
- group assignment UI
- group mapping controls
- bounded scroll segment controls
- phone/tablet/desktop preview switching
- group responsive overrides

### Exit condition

- grouped and responsive parallax works as specified in the frozen plans

---

### Phase 8: Slice 7 - Export Bundle

Goal:

- turn the scene into a deliverable product output

Deliverables:

- export job flow
- manifest generation
- export bundle generation
- download/access flow

### Exit condition

- exported bundle reflects saved scene graph semantics

---

### Phase 9: Slice 8 - Reliability And Recovery

Goal:

- make the MVP usable under failure conditions

Deliverables:

- retries
- timeout handling
- worker unavailable handling
- partial completion UX
- cleanup/reconciliation basics

### Exit condition

- failures are visible, recoverable, and do not corrupt scene state

---

### Phase 10: Slice 9 - Optional Difficult-Layer Enhancements

Goal:

- add quality improvements without delaying MVP shipment

Deliverables:

- matting refinement
- optional Qwen refinement
- alternate version activation behavior

### Exit condition

- enhancements work without destabilizing the baseline product path

---

## Execution Guardrails

During implementation:

- do not add nested groups
- do not add per-layer medium-specific responsive overrides unless required
- do not make workers the source of truth
- do not allow preview/export semantics to drift
- do not let optional refinement delay the baseline path

---

## Parallelization Guidance

Parallel work is encouraged, but should respect slice boundaries.

### Good parallel examples

- API scaffold work while web upload flow is being built
- editor shell work while stitch worker is being integrated
- preview shell work while depth contracts are being implemented
- export contract work while reliability handling is being added

### Bad parallel examples

- building refine worker before baseline extraction path is stable
- implementing preview math before stitched scene space is respected in code
- building export semantics before active artifact rules are honored

---

## QA Timing Guidance

QA should not be delayed until the end.

Recommended timing:

- smoke validation after every slice
- preview/export consistency checks starting at Slice 5
- recovery testing starting at Slice 8

---

## Definition Of MVP Implementation Complete

Implementation is complete when:

- the baseline slices through export and reliability are working
- Stage 1–4 frozen assumptions are still intact
- preview/export equivalence is acceptable
- grouped and responsive parallax are implemented
- stitched scene workflow works end to end

Optional refinement work is not required for MVP completion.

---

## Final Roadmap Statement

The MVP should be implemented as a contract-first, slice-first stitched-scene platform, where each phase proves a visible product outcome before the next layer of complexity is added, and where the baseline path to stitched parallax preview and export is always prioritized over optional enhancement work.
