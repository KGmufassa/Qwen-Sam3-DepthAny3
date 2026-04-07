# MVP Scope Plan

## Document Purpose

This document defines the exact scope of the first shippable MVP for the parallax story board application.

Its job is to answer five questions with no ambiguity:

- what the MVP must do
- what the MVP must not do
- what quality bar it must meet
- what assumptions it depends on
- what counts as complete

This document is a release-boundary artifact, not a wishlist.

---

## Product Summary

The MVP is a multi-image stitched parallax story editor that lets a user:

1. create a project
2. upload multiple source images
3. order and stitch those images into one continuous scroll canvas
4. segment meaningful elements within that stitched workflow
5. convert accepted selections into editable layers
6. group elements for shared parallax behavior
7. generate and normalize depth-informed parallax defaults
8. preview a scroll-based stitched parallax effect
9. export the result as a working web scene bundle

The MVP is not a full creative suite.

---

## Problem Statement

Users who want to create cinematic scroll-parallax experiences from multiple related images currently need to combine multiple disconnected tools:

- image stitching and alignment tools
- segmentation tools
- layer extraction tools
- depth estimation tools
- image editors
- front-end runtime code

This workflow is slow, error-prone, and difficult to repeat.

The MVP solves this by giving users one structured workflow for going from multiple source images to a stitched, editable, layered parallax scene.

---

## Target User

Primary user:

- a designer, creative technologist, or product-minded maker who wants to turn multiple images into one stitched interactive web scene without manually stitching together multiple ML and editing tools

Secondary user:

- a developer or technical artist who wants to export a reusable stitched parallax scene bundle rather than build the runtime from scratch

---

## MVP Outcome

At MVP completion, a user should be able to go from multi-image upload to export inside one guided application flow and end with:

- a saved project
- a saved stitched scene graph
- editable extracted layers
- flat groups for coordinated parallax behavior
- depth-informed and normalized parallax defaults
- a working stitched scroll preview
- a working exported web scene bundle

---

## Core User Journey

### Step 1: Project setup

The user creates or opens a project and uploads multiple images.

### Step 2: Image ordering and stitching

The user orders or confirms images for one continuous stitched scene. The system aligns and stitches them into a continuous scroll canvas.

### Step 3: Guided segmentation

The user selects meaningful image elements using the segmentation workflow and commits accepted mask results.

### Step 4: Layer extraction

The committed masks are converted into editable layer assets tied to the stitched scene.

### Step 5: Grouping and parallax setup

The user can create flat groups, assign layers to groups, and use those groups to coordinate parallax behavior and bounded scroll segment participation.

### Step 6: Depth generation and normalization

The system produces depth outputs and normalized layer-level parallax suggestions across the stitched scene.

### Step 7: Editor adjustments

The user can:

- rename layers
- reorder layers
- toggle visibility
- adjust transforms
- adjust group-level parallax behavior
- adjust layer-level parallax overrides

### Step 8: Preview

The user previews the stitched scroll-parallax scene and validates that grouped and ungrouped layers behave correctly.

### Step 9: Export

The user exports a working web scene bundle generated from the saved stitched scene graph.

---

## In-Scope Features

The MVP must include the following.

### Project and scene management

- create project
- create one stitched scene from multiple uploaded images
- persist project and stitched scene state

### Upload flow

- upload multiple source images
- create normalized working assets
- support progress and state transitions from upload into stitch workflow

### Stitching workflow

- image ordering or selection for scene composition
- stitched scene creation
- continuous stitched scroll canvas as the canonical scene surface
- source-image provenance retained inside the stitched workflow

### Segmentation workflow

- user-guided segmentation with SAM3-backed or equivalent segmentation flow
- candidate mask generation
- candidate review
- mask commit

### Layer extraction workflow

- convert committed masks into editable RGBA layers
- create layer thumbnails
- register resulting artifacts in persistent state

### Scene graph support

- continuous stitched scene model
- ordered layers
- flat groups
- layer names
- layer visibility
- layer transforms
- group membership
- layer depth settings
- group-level parallax settings
- layer-level override settings
- preview and export settings required by MVP

### Grouping capabilities

- create flat groups
- add and remove layers from groups
- zero-or-one group membership per layer
- group behavior used for both organization and runtime parallax control
- no nested groups in MVP

### Depth workflow

- generate stitched-scene depth output using Depth Anything 3
- compute and normalize per-layer depth metrics across the stitched scene
- assign default parallax/depth suggestions
- allow user override of suggested depth behavior

### Editor workflow

- load layers into editor
- select layers
- reorder layers
- rename layers
- show and hide layers
- create and manage flat groups
- modify depth/parallax controls
- modify transform controls required by MVP

### Parallax capabilities

- continuous scroll-driven parallax across one stitched scene
- depth-informed default parallax values
- group-level parallax mapping
- layer-level parallax overrides
- layer inheritance from group behavior by default
- bounded scroll segment participation for groups within the continuous scene
- responsive parallax behavior for phone, tablet, and desktop
- scene-level medium-aware defaults for responsive parallax behavior
- group-level medium-specific parallax overrides
- no baseline requirement for layer-level medium-specific overrides
- preview/export parity for saved parallax behavior

### Preview workflow

- render scene from saved stitched scene state
- support scroll-parallax preview across the continuous stitched canvas
- reflect user overrides, not just system defaults
- reflect group-level mappings and bounded scroll participation
- reflect medium-aware parallax behavior for phone, tablet, and desktop

### Export workflow

- compile the saved stitched scene graph into a web scene bundle
- include assets and manifest data needed to reproduce the scene
- preserve group-based parallax behavior and layer overrides
- preserve medium-aware parallax mappings defined at scene and group level
- produce downloadable export output

### Async job support

- create jobs for heavy processing stages
- expose job status
- handle failed and retryable states at MVP level

### Reliability baseline

- visible processing status
- visible failure state
- retry support for core pipeline stages

---

## Explicit Non-Goals

The MVP does not include the following.

### Advanced grouping and motion systems

- no nested groups
- no reusable group templates
- no timeline animation editor
- no keyframe animation system
- no physics-based scene simulation
- no baseline requirement for layer-level medium-specific parallax overrides

### Full creative suite behavior

- no PSD-first editing environment
- no advanced paint tools
- no high-end compositing toolkit
- no frame-by-frame animation authoring system

### Advanced collaboration

- no real-time multi-user editing
- no branching or version collaboration workflows

### Full automation of quality repair

- no requirement that all difficult layers be fixed automatically
- no requirement that Qwen refinement runs by default on all layers

### Full production orchestration maturity

- no requirement for full autoscaling sophistication in the initial release
- no requirement for Kubernetes-specific production deployment

### Advanced camera systems

- no free-camera 3D navigation
- no cinematic camera timeline system
- no procedural motion graph system

---

## Product Principles

The MVP should follow these principles:

- multiple images, one stitched scene, one clear workflow
- local app remains the source of truth
- workers provide inference, not workflow ownership
- the stitched scene graph must drive both preview and export
- default automation must remain user-correctable
- grouped motion should be expressive without requiring a full animation system
- difficult layers should not block the whole experience

---

## User Value Threshold

The MVP is only valuable if it achieves all of the following:

- multi-image upload does not feel disconnected from stitched scene creation
- stitched scene creation is understandable and reliable
- segmentation results can be committed into usable layers
- extracted layers are editable in a meaningful way
- grouping produces visibly coordinated parallax behavior
- depth defaults provide a visible stitched-scene parallax benefit
- parallax behavior remains usable across phone, tablet, and desktop
- export produces something practically reusable

If any one of those fails, the product is not at MVP quality even if the system is technically functional.

---

## Core Success Criteria

The MVP must satisfy all of the following:

1. a user can create a project and upload multiple images
2. a user can create one continuous stitched scene from those images
3. a user can generate segmentation candidates and commit chosen masks
4. each committed mask becomes an editable layer
5. the editor loads the saved stitched scene state correctly
6. flat groups can be created and used for parallax control
7. depth outputs are generated and normalized for stitched-scene behavior
8. the preview reflects saved layer order, group mappings, and parallax behavior
9. scene-level medium-aware parallax defaults work for phone, tablet, and desktop
10. group-level medium-specific overrides work within the stitched scene model
11. the user can manually override layer-level parallax behavior
12. the export bundle is generated from the same stitched scene graph used by preview
13. core failures are visible and retryable

---

## Out-Of-Scope But Allowed If Low Cost

The following may be included only if they do not delay MVP completion:

- lightweight layer edge refinement toggle
- better layer naming suggestions
- minor UX polish in preview controls
- simple export variants that do not change the core scene graph contract

These are optional and must not shift the release boundary.

---

## Required Technical Assumptions

This MVP assumes:

- a hybrid control-plane plus worker architecture
- remote or local worker support for stitching, segmentation, and depth
- persistent storage for projects, scenes, jobs, groups, and artifacts
- reproducible stitched scene graph state
- artifact registration as first-class system behavior
- cross-image depth normalization support in the stitched workflow
- responsive parallax support for phone, tablet, and desktop using scene-level defaults and group-level overrides

If any of these assumptions change, the scope must be reevaluated.

---

## Required UX Assumptions

This MVP assumes:

- users will accept a staged workflow
- users will manually approve masks
- users will manually correct depth ordering when needed
- users will use flat groups for coordinated motion
- users do not require full Photoshop-class controls

---

## Release Boundary

The MVP release stops at:

- multi-image stitched scene creation
- segmentation-to-layer workflow
- group-aware depth-assisted parallax preview
- web scene bundle export

The MVP release does not extend to:

- automated difficult-layer enhancement as a baseline
- nested grouping systems
- advanced collaboration
- advanced publishing or analytics features

---

## Exit Conditions For Scope Freeze

This document is considered approved when:

- all in-scope features are agreed
- all non-goals are agreed
- the release boundary is explicit
- the success criteria are measurable
- Qwen refinement is confirmed as optional, not baseline
- multi-image stitched-scene scope is confirmed
- grouping and parallax capabilities are confirmed as MVP features

---

## Final Scope Statement

The MVP is a multi-image, stitched-scene, scene-graph-based scroll-parallax editor that uses guided segmentation, flat runtime groups, and depth estimation to produce editable layers, interactive stitched preview, and exportable web scene output inside one structured workflow.
