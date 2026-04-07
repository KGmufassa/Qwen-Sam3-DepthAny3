# Canonical Math Plan

## Document Purpose

This document defines the canonical coordinate systems, transforms, progression model, and responsive parallax math assumptions for the MVP.

Its purpose is to stop math drift across:

- stitching
- segmentation
- extraction
- editor interactions
- preview rendering
- export generation

If this document and implementation disagree, this document wins.

---

## Design Principles

- one continuous stitched scene is the canonical runtime surface
- every artifact must declare its coordinate space
- transforms must be composable and deterministic
- responsive parallax must derive from one shared model
- preview and export must use the same math model

---

## Canonical Coordinate Spaces

The MVP uses the following coordinate spaces.

### 1. Source Image Space

The native pixel space of one uploaded image before normalization.

Properties:

- origin at top-left
- units in source pixels
- local to one source image only

Use cases:

- initial upload provenance
- source-specific troubleshooting

### 2. Normalized Image Space

The normalized pixel space of one source image after orientation and preprocessing normalization.

Properties:

- origin at top-left
- units in normalized pixels
- local to one normalized source image

Use cases:

- worker input preparation
- pre-stitch processing

### 3. Stitched Scene Space

The canonical 2D coordinate space for the continuous scene canvas.

Properties:

- origin at top-left of the stitched scene
- units in stitched scene pixels
- continuous across the full stitched canvas

Use cases:

- segmentation contract
- layer extraction provenance
- group scroll mapping
- editor placement
- preview math
- export math

This is the authoritative scene graph coordinate space.

### 4. Mask Space

The pixel space of a mask artifact.

Properties:

- tied to a declared parent space
- typically stitched scene aligned for MVP

Use cases:

- segmentation outputs
- layer extraction
- depth aggregation

### 5. Crop Space

The local pixel space of an extracted layer crop or variant.

Properties:

- origin at top-left of the crop
- local to the layer version

Use cases:

- RGBA layer assets
- alpha variants
- thumbnail generation

### 6. Editor View Space

The local viewport space used by the editing UI.

Properties:

- camera/zoom dependent
- derived from stitched scene space
- not authoritative for persistence

Use cases:

- hit testing
- drag interactions
- viewport transforms

### 7. Preview Runtime Space

The runtime rendering space for a specific medium profile.

Properties:

- derived from stitched scene space plus responsive mapping rules
- medium-dependent

Use cases:

- phone preview
- tablet preview
- desktop preview

### 8. Export Runtime Space

The runtime output coordinate space produced by export.

Properties:

- semantically equivalent to preview runtime space
- must preserve saved scene graph behavior

Use cases:

- web bundle runtime
- downstream playback

---

## Canonical Space Hierarchy

Math should flow in this direction:

- source image space
- normalized image space
- stitched scene space
- crop space where needed for asset-local operations
- editor view / preview runtime / export runtime as derived spaces

Persistence should prefer stitched scene space, not editor space.

---

## Stitch Placement Model

Each normalized source image maps into stitched scene space by a placement transform.

That transform should minimally define:

- translation
- scale if needed
- rotation only if the stitch workflow truly requires it

MVP preference:

- avoid arbitrary rotation unless stitching quality requires it
- keep stitched scene placement as simple and reproducible as possible

---

## Layer Placement Model

Each layer has a canonical scene placement defined in stitched scene space.

A layer’s visible placement should be described by:

- anchor point
- bounding box
- transform

The transform should support:

- translation x/y
- scale x/y
- rotation
- opacity if handled in runtime state rather than visual metadata

MVP should keep transform composition order fixed.

Recommended order:

1. local crop normalization
2. anchor translation into stitched scene space
3. scale
4. rotation
5. runtime parallax offset

---

## Group Mapping Model

Groups do not create a new coordinate space.

Instead, groups define behavioral mappings applied to member layers.

A group may define:

- parallax intensity multipliers
- motion range modifiers
- bounded scroll segment participation
- responsive overrides by medium

Layer scene placement remains expressed in stitched scene space.

---

## Scroll Progress Model

The stitched scene has one continuous normalized scroll progress range.

Canonical range:

- `0.0` = start of stitched scene scroll
- `1.0` = end of stitched scene scroll

All group segment participation must be defined relative to this canonical progress range.

---

## Group Scroll Segment Model

Each group may specify one bounded segment:

- `start_progress`
- `end_progress`

Constraints:

- `0.0 <= start_progress < end_progress <= 1.0`

Interpretation:

- before `start_progress`, group mapping is inactive or at pre-entry state
- between `start_progress` and `end_progress`, group mapping is active
- after `end_progress`, group mapping is inactive or at post-exit state depending on runtime rule

MVP should keep this behavior simple and deterministic.

---

## Depth Model

Depth is used to derive parallax behavior, not to define a full 3D scene simulation.

Canonical stored depth outputs:

- one scene-level depth artifact
- one preview depth artifact
- per-layer aggregated depth metrics

Required per-layer metrics:

- mean depth
- median depth
- nearest depth
- farthest depth

Cross-image depth normalization must produce values meaningful within one stitched scene.

---

## Depth-To-Parallax Mapping

The MVP should use a deterministic mapping from depth metrics to default parallax behavior.

Conceptual rule:

- nearer elements move more
- farther elements move less

The exact mapping curve can be tuned later, but the contract must preserve:

- monotonic relation
- reproducibility
- manual override support

Scene defaults define the baseline mapping.

Groups can modify the baseline.

Layers can override final applied values.

---

## Responsive Parallax Model

The MVP uses one shared parallax model across all media.

### Medium profiles

The canonical supported media profiles are:

- `phone`
- `tablet`
- `desktop`

### Scene-level defaults

The scene defines default modifiers for each medium.

Example categories:

- intensity multiplier
- motion range multiplier
- scroll compression/expansion factor

### Group-level responsive overrides

A group may override selected medium values for:

- phone
- tablet
- desktop

### Layer-level responsive overrides

Not required for baseline MVP.

---

## Runtime Offset Model

Runtime parallax offset should be derived from:

- canonical scroll progress
- scene-level medium profile
- group-level mapping
- layer-level override if present
- depth-derived default

Conceptually:

`final_offset = base_layer_position + runtime_parallax_offset`

Where runtime parallax offset is derived in a consistent order:

1. scene default by medium
2. group-level mapping
3. group medium override if present
4. layer override if present

---

## Editor Math Rules

The editor must always convert user interactions back into stitched scene space before persisting.

This means:

- drag is persisted in stitched scene coordinates
- zoom never changes persisted coordinates
- selection bounds are computed against stitched scene placement, not viewport coordinates

---

## Preview And Export Equivalence

Preview and export must be semantically equivalent.

This means:

- same scroll progress model
- same group segment behavior
- same medium-aware rules
- same transform composition order

Minor rendering differences are acceptable.

Different math rules are not.

---

## Canonical Units

Use:

- pixels for scene and asset coordinates
- normalized `0.0 -> 1.0` progress for stitched scroll progression
- normalized or consistently scaled depth metrics for depth-to-parallax mapping

Avoid mixing percent-like values and pixel offsets without explicit conversion.

---

## Required Metadata On Artifacts

Every math-relevant artifact must declare:

- coordinate space
- width
- height
- parent scene or source reference

Masks and layer crops are especially sensitive to missing space metadata.

---

## Invariants

The following math invariants must hold:

- stitched scene space is authoritative
- all persisted layer placement is expressed in stitched scene space
- scroll progress is continuous from `0.0` to `1.0`
- groups do not create nested coordinate spaces
- responsive parallax uses the same core model across all media

---

## Out-Of-Scope Math Features

The MVP math model does not require:

- full 3D transforms
- perspective camera simulation
- nested scroll timelines
- per-layer medium-specific responsive overrides as a baseline

---

## Freeze Criteria

This plan is ready to freeze when:

- all coordinate spaces are accepted
- scroll progress semantics are accepted
- group segment model is accepted
- responsive parallax model is accepted
- preview/export equivalence rules are accepted

---

## Final Math Statement

The MVP uses stitched scene space as its authoritative coordinate system, normalized continuous scroll progress as its movement driver, and a shared medium-aware parallax model that applies scene defaults, group mappings, and optional layer overrides consistently across editor, preview, and export.
