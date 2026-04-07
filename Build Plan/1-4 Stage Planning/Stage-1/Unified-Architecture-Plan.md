# Unified Architecture Plan

## Document Purpose

This document defines the target high-level architecture for the MVP.

It unifies three architectural strengths identified in the source repos:

- Depth Anything 3 style multi-surface platform contract
- SAM3 style model assembly and runtime discipline
- Qwen-image-layered style explicit stage-based workflow

The result is one product architecture, not three loosely attached subsystems.

---

## Architectural Goal

Build a multi-image stitched parallax scene platform with:

- one authoritative application state model
- one staged processing workflow
- multiple isolated execution surfaces
- predictable preview and export behavior

The architecture must support:

- multi-image upload
- image ordering and stitching
- user-guided segmentation
- layer extraction
- group-aware parallax behavior
- responsive parallax behavior across phone, tablet, and desktop
- depth-driven and normalized defaults
- interactive editing
- scroll-parallax preview
- exportable scene bundles

---

## Architectural Principles

### 1. One source of truth

The local application owns:

- project state
- stitched scene state
- layer state
- group state
- artifact registry
- pipeline run state
- job state
- export state

Workers do not own workflow truth.

### 2. Workers are execution services

Workers do:

- inference
- transformation
- artifact production
- metadata generation

Workers do not:

- mutate scene semantics directly
- decide product workflow state
- become the system of record

### 3. Scene graph drives preview and export

Preview and export must derive from the same saved stitched scene graph model.

No hidden preview-only or export-only logic should redefine scene meaning.

### 4. Stable contracts first

The architecture favors:

- frozen contracts
- artifact identity
- predictable job lifecycles

over:

- ad hoc worker-specific shortcuts
- UI-driven implicit state

### 5. Stage-oriented user flow

The user experience remains explicit and legible:

1. upload
2. order
3. stitch
4. segment
5. commit
6. extract
7. depth normalize
8. edit
9. preview
10. export

---

## Top-Level Architecture

The system is split into three major planes.

### A. Experience plane

This is the web application surface.

Responsibilities:

- project and scene UI
- multi-image upload flow
- ordering and stitch workflow
- segmentation interaction flow
- editor UI
- preview UI
- export UI
- job-status visibility
- failure and retry visibility

Primary technology direction:

- Next.js or equivalent web application shell
- typed frontend client contracts

### B. Control plane

This is the application backend that coordinates product behavior.

Responsibilities:

- authentication and authorization
- route handling
- validation
- persistent stitched scene graph updates
- artifact registration
- job creation and orchestration
- worker dispatch
- status aggregation
- export registration

The control plane is the system authority for workflow and persistence.

### C. Execution plane

This is the worker layer.

Responsibilities:

- run stitching or alignment
- run segmentation
- run depth estimation and normalization support
- run matting when used
- run optional Qwen refinement when invoked
- run composition/export compilation where appropriate

The execution plane is optimized for model/runtime isolation.

---

## Core System Components

### 1. Web application

Handles:

- user-facing flows
- editor interactions
- preview interactions
- export triggering

### 2. API/control service

Handles:

- stateful orchestration
- contract validation
- stitched scene graph persistence
- group and layer mutation
- artifact registration
- worker dispatch and result ingestion

### 3. Database

Stores:

- projects
- stitched scenes
- groups
- layers
- jobs
- pipeline runs
- references to artifacts
- export records

### 4. Object storage

Stores:

- uploaded originals
- normalized images
- stitched scene artifacts
- masks
- RGBA layers
- depth outputs
- thumbnails
- preview derivatives
- export bundles

### 5. Queue system

Carries:

- stitch jobs
- segmentation jobs
- extraction jobs if asynchronous
- depth jobs
- matting jobs
- refinement jobs
- export jobs

### 6. Worker services

Model-family-isolated services for:

- stitch/alignment
- segmentation
- depth
- matting
- optional layer-refine
- compose/export

---

## Recommended Service Boundaries

### Control plane service boundary

The control plane owns:

- request validation
- state transitions
- scene graph mutation
- group and layer mutation
- job creation
- artifact registration
- permission checks

### Stitch/alignment worker boundary

The stitch worker owns:

- image alignment
- stitched scene artifact creation
- stitched provenance metadata

It must return artifacts and metadata, not final workflow truth.

### Segmentation worker boundary

The segmentation worker owns:

- loading segmentation runtime
- prompt-to-mask inference
- candidate confidence metadata
- outputting mask artifacts and metadata

### Depth worker boundary

The depth worker owns:

- loading depth model runtime
- generating canonical depth artifact
- generating preview visualization artifact
- returning metadata needed for control-plane normalization and aggregation

### Matting worker boundary

The matting worker owns:

- alpha refinement
- refined RGBA output generation

### Optional Qwen refine boundary

The refine worker owns:

- user-invoked difficult-layer enhancement
- alternate RGBA artifact generation

It must not be part of baseline extraction by default.

### Compose/export worker boundary

The export worker owns:

- scene compilation
- export packaging
- derived bundle output

It consumes saved state; it does not invent scene structure.

---

## Workflow Architecture

The product workflow is stage-based.

### Stage 1: Upload

Input:

- multiple source images

Output:

- original artifacts
- normalized artifacts
- pending stitched scene record

### Stage 2: Order and stitch

Input:

- uploaded images
- image ordering or selection rules

Output:

- stitched scene artifact
- provenance metadata linking source images to stitched result
- continuous stitched scene canvas as canonical scene surface

### Stage 3: Segmentation

Input:

- stitched scene artifact
- prompt inputs

Output:

- candidate masks
- mask metadata

### Stage 4: Commit

Input:

- approved masks

Output:

- committed layer seeds
- stitched scene graph updates

### Stage 5: Extraction

Input:

- stitched scene artifact
- committed masks

Output:

- RGBA layer artifacts
- thumbnails
- layer records

### Stage 6: Depth and normalization

Input:

- stitched scene artifact
- committed layers or masks for aggregation

Output:

- scene depth artifact
- preview depth artifact
- normalized per-layer depth metrics

### Stage 7: Edit

Input:

- saved stitched scene graph
- layer artifacts
- group settings
- depth defaults

Output:

- updated stitched scene graph state

### Stage 8: Preview

Input:

- saved stitched scene graph

Output:

- interactive runtime preview across the continuous stitched scene

### Stage 9: Export

Input:

- saved stitched scene graph
- active artifacts

Output:

- export bundle
- export manifest

---

## Scene Graph Architecture

The stitched scene graph must include first-class support for:

- stitched scene identity
- ordered layers
- flat groups
- group membership
- layer transforms
- layer visibility
- depth/parallax settings
- group-level parallax mappings
- layer-level overrides

### Group model

Groups are flat scene-graph entities used for both organization and parallax runtime control.

For MVP:

- a layer belongs to zero or one group
- groups are not nested
- groups can define shared parallax behavior
- groups can participate in bounded scroll segments inside the continuous stitched scene

---

## Parallax Runtime Model

Parallax behavior is modeled at three levels.

### Scene level

The scene owns:

- the continuous stitched scroll progression
- the overall scroll space

### Group level

Groups own:

- shared parallax mapping behavior
- optional bounded scroll segment participation
- medium-specific parallax overrides when needed for phone, tablet, or desktop

### Layer level

Layers own:

- final layer-specific state
- overrides of inherited group behavior when needed

### Inheritance rule

Layers inherit group behavior by default unless explicitly overridden.

### Responsive rule

The parallax system uses one shared model with:

- scene-level medium-aware defaults
- group-level medium-specific overrides
- no baseline requirement for layer-level medium-specific overrides in MVP

---

## Data Ownership Model

### App-owned entities

The control plane owns:

- projects
- stitched scenes
- groups
- layers
- job records
- pipeline runs
- artifact metadata
- export metadata

### Worker-produced artifacts

Workers may produce:

- files
- checksums
- metrics
- model version data

But all of those must be registered by the control plane before becoming official system state.

---

## Artifact Architecture

Artifacts are first-class entities.

Every meaningful file produced by the system should be representable as:

- a typed artifact
- tied to a pipeline run
- tied to a stitched scene
- tied to a generating stage
- traceable to a producing model/runtime

This allows:

- reproducibility
- retries
- version switching
- export traceability

### Required artifact classes

The architecture should account for:

- source image artifacts
- normalized image artifacts
- stitched scene artifacts
- mask artifacts
- extracted layer artifacts
- depth artifacts
- preview derivatives
- export bundle artifacts

---

## Preview And Export Relationship

Preview and export are siblings, not separate truth systems.

### Preview

Purpose:

- interactive validation of current stitched scene state

### Export

Purpose:

- package the saved stitched scene state into reusable output

### Shared rule

Both must consume:

- saved layer order
- saved group membership
- saved transforms
- saved depth/parallax settings
- saved bounded group participation rules
- saved active layer versions
- saved medium-aware parallax settings at scene and group level

If preview and export diverge, the architecture is being violated.

---

## Runtime Surface Strategy

Following the strongest pattern from the comparison report, the system should support multiple thin surfaces around one core contract.

### Required MVP surfaces

- web UI
- local API/control plane
- worker endpoints

### Optional later surfaces

- CLI tooling
- admin diagnostics surface
- benchmark/evaluation scripts

These are not required for MVP completion.

---

## Model Assembly Strategy

Borrowing the SAM3 discipline, heavyweight model setup should be isolated from request handling.

This means:

- worker startup handles model loading
- requests should not reconstruct model pipelines repeatedly
- model version identity must be exposed in worker outputs

This is especially important for:

- stitch runtime reuse
- segmentation runtime reuse
- depth runtime reuse
- optional refine runtime reuse

---

## Queue And Job Strategy

Heavy operations should be asynchronous jobs.

Recommended job families:

- `stitch.generate`
- `segment.generate`
- `extract.layer`
- `depth.generate`
- `matte.layer`
- `layer.refine`
- `export.bundle`

The control plane owns:

- job creation
- retries
- timeout interpretation
- final state mutation

---

## Reliability Posture

The architecture must assume:

- workers may be unavailable
- inference may fail
- outputs may be delayed
- partial artifacts may exist

Therefore:

- all core stages require explicit status handling
- artifact registration must be idempotent
- late results must be safely handled
- failed stages must not corrupt the stitched scene graph

---

## Local Versus Remote Runtime Strategy

The architecture supports hybrid execution.

### Local control plane

Runs:

- product logic
- persistence
- orchestration
- user-facing API

### Local or remote workers

Run:

- stitching
- model inference
- heavy transformation stages

This keeps the product architecture stable regardless of whether workers run:

- locally in development
- remotely on Runpod
- in later production infrastructure

---

## What This Architecture Explicitly Avoids

The system should avoid:

- embedding all models inside one monolithic app runtime
- letting workers mutate scene truth directly
- letting preview invent state not represented in the stitched scene graph
- building export as a separate ad hoc representation
- requiring Qwen refinement in the baseline flow
- tying the product to one deployment target
- introducing nested groups in MVP

---

## MVP Architectural Success Criteria

This architecture is successful for MVP if:

1. the local app remains the source of truth
2. workers remain replaceable execution services
3. the stitched scene graph drives both preview and export
4. stitching, segmentation, extraction, and depth can operate as isolated stages
5. group-based parallax mappings work within one continuous stitched scene
6. responsive parallax behavior works across phone, tablet, and desktop using the agreed model
7. the baseline flow works without requiring optional refinement
8. the architecture remains valid for both local and remote worker execution

---

## Final Architecture Statement

The MVP architecture is a staged, stitched-scene, scene-graph-driven product system with a web experience plane, an authoritative control plane, and isolated execution workers. It combines explicit user workflow, reusable worker boundaries, flat runtime groups, and export-reproducible state so that stitching, segmentation, depth, editing, preview, and export all operate as parts of one coherent platform.
