# Master Planning Index

## Purpose

This document is the top-level index for the frozen planning stack.

It provides:

- one entry point into all planning stages
- a record of what is frozen
- a summary of the system assumptions that downstream implementation must follow
- a bridge from planning into implementation

---

## Planning Status

The planning stack is complete through Stage 4 and reviewed.

### Frozen stages

- Stage 1: strategy foundation
- Stage 2: core contracts
- Stage 3: workflow behavior
- Stage 4: platform and delivery

### Meaning of frozen

These plans are now the authoritative baseline for implementation.

Any foundational change to:

- MVP scope
- stitched scene semantics
- scene graph contracts
- coordinate math
- grouping/parallax behavior
- preview/export equivalence
- worker boundaries

should be treated as a formal reopen of the relevant stage, not as a silent implementation adjustment.

---

## Stage 1 Index

Stage 1 defines the strategic foundation.

### Documents

- [MVP-Scope-Plan.md](/Users/wislemleger/Desktop/GitHub/Qwen-Sam3-DepthAny3/Build%20Plan/Stage-1/MVP-Scope-Plan.md)
- [Decision-Log-Plan.md](/Users/wislemleger/Desktop/GitHub/Qwen-Sam3-DepthAny3/Build%20Plan/Stage-1/Decision-Log-Plan.md)
- [Dependency-Gate-Plan.md](/Users/wislemleger/Desktop/GitHub/Qwen-Sam3-DepthAny3/Build%20Plan/Stage-1/Dependency-Gate-Plan.md)
- [Unified-Architecture-Plan.md](/Users/wislemleger/Desktop/GitHub/Qwen-Sam3-DepthAny3/Build%20Plan/Stage-1/Unified-Architecture-Plan.md)

### Frozen outcomes

- MVP supports multi-image stitched scenes
- stitched scene is one continuous scroll canvas
- groups are flat, first-class scene/runtime units
- parallax is core MVP functionality
- responsive parallax supports phone, tablet, and desktop
- local app/control plane is the source of truth
- workers are execution services only
- preview and export must derive from the same scene graph
- Qwen refinement is optional, not baseline

---

## Stage 2 Index

Stage 2 defines the core contracts.

### Documents

- [Data-Schema-And-Scene-Graph-Plan.md](/Users/wislemleger/Desktop/GitHub/Qwen-Sam3-DepthAny3/Build%20Plan/Stage-2/Data-Schema-And-Scene-Graph-Plan.md)
- [Canonical-Math-Plan.md](/Users/wislemleger/Desktop/GitHub/Qwen-Sam3-DepthAny3/Build%20Plan/Stage-2/Canonical-Math-Plan.md)
- [API-And-Job-Contract-Plan.md](/Users/wislemleger/Desktop/GitHub/Qwen-Sam3-DepthAny3/Build%20Plan/Stage-2/API-And-Job-Contract-Plan.md)
- [Worker-Runtime-Contract-Plan.md](/Users/wislemleger/Desktop/GitHub/Qwen-Sam3-DepthAny3/Build%20Plan/Stage-2/Worker-Runtime-Contract-Plan.md)

### Frozen outcomes

- stitched scene graph is the primary runtime model
- artifacts are first-class and control-plane registered
- stitched scene space is the authoritative persisted coordinate space
- scroll progress is continuous from `0.0` to `1.0`
- groups do not create separate coordinate spaces
- responsive parallax uses scene-level defaults plus group-level overrides
- all heavy processing is async
- workers return artifacts and metadata
- preview and export are semantically equivalent by contract

---

## Stage 3 Index

Stage 3 defines workflow behavior.

### Documents

- [Editor-UX-And-Interaction-Plan.md](/Users/wislemleger/Desktop/GitHub/Qwen-Sam3-DepthAny3/Build%20Plan/Stage-3/Editor-UX-And-Interaction-Plan.md)
- [State-And-History-Plan.md](/Users/wislemleger/Desktop/GitHub/Qwen-Sam3-DepthAny3/Build%20Plan/Stage-3/State-And-History-Plan.md)
- [Fallback-UX-Plan.md](/Users/wislemleger/Desktop/GitHub/Qwen-Sam3-DepthAny3/Build%20Plan/Stage-3/Fallback-UX-Plan.md)
- [Artifact-And-Export-Lifecycle-Plan.md](/Users/wislemleger/Desktop/GitHub/Qwen-Sam3-DepthAny3/Build%20Plan/Stage-3/Artifact-And-Export-Lifecycle-Plan.md)

### Frozen outcomes

- editor is a stitched-scene workspace
- groups are visible as both organization and runtime controls
- inheritance must be explicit in the UI
- undo/redo tracks user-meaningful scene mutations
- failures must be visible and recoverable
- partial completion is supported
- export consumes accepted scene graph state and active artifacts only

---

## Stage 4 Index

Stage 4 defines platform and delivery behavior.

### Documents

- [Deployment-And-Infrastructure-Plan.md](/Users/wislemleger/Desktop/GitHub/Qwen-Sam3-DepthAny3/Build%20Plan/Stage-4/Deployment-And-Infrastructure-Plan.md)
- [Caching-And-Performance-Plan.md](/Users/wislemleger/Desktop/GitHub/Qwen-Sam3-DepthAny3/Build%20Plan/Stage-4/Caching-And-Performance-Plan.md)
- [QA-And-Release-Readiness-Plan.md](/Users/wislemleger/Desktop/GitHub/Qwen-Sam3-DepthAny3/Build%20Plan/Stage-4/QA-And-Release-Readiness-Plan.md)
- [Vertical-Release-Slice-Plan.md](/Users/wislemleger/Desktop/GitHub/Qwen-Sam3-DepthAny3/Build%20Plan/Stage-4/Vertical-Release-Slice-Plan.md)

### Frozen outcomes

- deployment uses a separated control plane and worker model
- deterministic expensive outputs should be cached where safe
- QA must validate stitched-scene, parallax, responsive behavior, and preview/export equivalence
- implementation should proceed through vertical release slices

---

## Canonical Product Model

The frozen product model is:

- multiple uploaded images
- one stitched continuous scene
- segmented and extracted editable layers
- flat groups for shared parallax behavior
- scene-level responsive defaults
- group-level responsive overrides
- medium-aware preview
- exportable web scene bundle

---

## Canonical System Model

The frozen system model is:

- web application
- API/control plane
- persistent database
- object storage
- queue
- isolated workers by family

### Worker families

- stitch/alignment
- segmentation
- depth
- matting
- optional layer-refine
- compose/export

---

## Preview And Export Rule

The most important implementation rule is:

- preview and export must consume the same stitched scene graph semantics

No implementation shortcut should violate that.

---

## Recommended Build Path

Implementation should follow the Stage 4 vertical slices:

1. upload to mock stitched scene
2. real stitch to scene shell
3. real segmentation to committed layer seeds
4. real extraction to editable layers
5. depth to parallax preview
6. grouped and responsive parallax refinement
7. export bundle
8. reliability and recovery
9. optional difficult-layer enhancements

---

## Implementation Companion

The implementation roadmap that operationalizes these frozen plans is:

- [Implementation-Roadmap.md](/Users/wislemleger/Desktop/GitHub/Qwen-Sam3-DepthAny3/Build%20Plan/Implementation-Roadmap.md)

---

## Final Index Statement

This document is the master map of the planning system. Implementation should treat the linked Stage 1–4 documents as the frozen baseline and use the implementation roadmap to translate them into build order and execution.
