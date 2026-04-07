# Data Schema And Scene Graph Plan

## Document Purpose

This document defines the canonical data model for the MVP.

It answers:

- what entities exist
- how they relate
- what the stitched scene graph contains
- how groups, layers, artifacts, jobs, and exports are represented
- what becomes part of the contract boundary for Stage 3 and implementation

This document is the authoritative schema-level interpretation of the frozen Stage 1 decisions.

---

## Design Principles

- the stitched scene is the primary runtime unit
- the local app/control plane is the source of truth
- artifacts are first-class entities
- groups are flat scene-graph entities
- layers are versioned scene objects
- preview and export consume the same scene graph
- responsive parallax is represented through scene-level defaults plus group-level overrides

---

## Core Entity Set

The MVP requires the following primary entities:

- `Project`
- `StitchedScene`
- `SourceImage`
- `Group`
- `Layer`
- `LayerVersion`
- `Artifact`
- `PipelineRun`
- `Job`
- `ExportRecord`

Optional supporting entities may later be introduced, but the MVP contract should not depend on them.

---

## Entity Definitions

### Project

Represents the top-level user workspace.

Required fields:

- `id`
- `owner_id`
- `name`
- `status`
- `created_at`
- `updated_at`
- `active_scene_id`

Relationships:

- one project has one or more stitched scenes
- one project has many export records

### StitchedScene

Represents one continuous scroll canvas derived from multiple source images.

Required fields:

- `id`
- `project_id`
- `name`
- `status`
- `canvas_width`
- `canvas_height`
- `scroll_axis`
- `scene_defaults`
- `preview_settings`
- `export_settings`
- `created_at`
- `updated_at`

Relationships:

- one stitched scene has many source images
- one stitched scene has many groups
- one stitched scene has many layers
- one stitched scene has many pipeline runs
- one stitched scene has many artifacts
- one stitched scene has many export records

### SourceImage

Represents one original uploaded image that participates in the stitched scene.

Required fields:

- `id`
- `scene_id`
- `artifact_id_original`
- `artifact_id_normalized`
- `source_index`
- `placement_hint`
- `provenance`
- `created_at`

Relationships:

- many source images belong to one stitched scene
- one source image may contribute to one or more layer artifacts indirectly through provenance

### Group

Represents a flat organizational and runtime container for parallax behavior.

Required fields:

- `id`
- `scene_id`
- `name`
- `order_index`
- `is_enabled`
- `parallax_mapping`
- `responsive_overrides`
- `scroll_segment`
- `created_at`
- `updated_at`

Relationships:

- many groups belong to one stitched scene
- one group has many layers

Constraints:

- groups are flat only
- groups are not nested

### Layer

Represents one editable scene object derived from a committed segmentation result.

Required fields:

- `id`
- `scene_id`
- `group_id` nullable
- `name`
- `order_index`
- `is_visible`
- `blend_mode`
- `transform`
- `depth_settings`
- `parallax_override` nullable
- `source_mask_artifact_id`
- `active_version_id`
- `provenance`
- `created_at`
- `updated_at`

Relationships:

- many layers belong to one stitched scene
- one layer belongs to zero or one group
- one layer has many versions

Constraints:

- a layer may belong to at most one group

### LayerVersion

Represents a reversible version of a layer’s image payload.

Required fields:

- `id`
- `layer_id`
- `version_index`
- `kind`
- `rgba_artifact_id`
- `alpha_artifact_id` nullable
- `thumbnail_artifact_id` nullable
- `is_active`
- `created_by_stage`
- `created_at`

Kinds may include:

- `base_extract`
- `matte_refine`
- `qwen_refine`
- `manual_replace`

Relationships:

- many layer versions belong to one layer

### Artifact

Represents a first-class registered file or machine-readable generated output.

Required fields:

- `id`
- `scene_id`
- `pipeline_run_id` nullable
- `job_id` nullable
- `stage`
- `type`
- `storage_path`
- `mime_type`
- `checksum`
- `width` nullable
- `height` nullable
- `coordinate_space`
- `producer`
- `created_at`

Types should at minimum support:

- `source_original`
- `source_normalized`
- `stitched_scene`
- `stitched_preview`
- `mask`
- `mask_preview`
- `layer_rgba`
- `layer_alpha`
- `layer_thumbnail`
- `depth_map`
- `depth_preview`
- `export_bundle`
- `export_manifest`

### PipelineRun

Represents one tracked multi-stage processing attempt against a stitched scene.

Required fields:

- `id`
- `scene_id`
- `kind`
- `status`
- `started_at`
- `completed_at` nullable
- `summary`

Kinds may include:

- `scene_build`
- `segmentation_session`
- `depth_generation`
- `export_generation`

### Job

Represents one executable unit of asynchronous work.

Required fields:

- `id`
- `scene_id`
- `pipeline_run_id` nullable
- `type`
- `status`
- `request_payload_ref`
- `result_payload_ref` nullable
- `retry_count`
- `created_at`
- `started_at` nullable
- `completed_at` nullable
- `failed_at` nullable
- `error_summary` nullable

Supported MVP job types:

- `stitch.generate`
- `segment.generate`
- `extract.layer`
- `depth.generate`
- `matte.layer`
- `layer.refine`
- `export.bundle`

### ExportRecord

Represents one generated export tied to saved scene state.

Required fields:

- `id`
- `scene_id`
- `pipeline_run_id`
- `status`
- `bundle_artifact_id`
- `manifest_artifact_id`
- `created_at`

---

## Relationship Summary

- `Project` 1 -> many `StitchedScene`
- `StitchedScene` 1 -> many `SourceImage`
- `StitchedScene` 1 -> many `Group`
- `StitchedScene` 1 -> many `Layer`
- `Layer` 1 -> many `LayerVersion`
- `StitchedScene` 1 -> many `Artifact`
- `StitchedScene` 1 -> many `PipelineRun`
- `PipelineRun` 1 -> many `Job`
- `StitchedScene` 1 -> many `ExportRecord`

---

## Scene Graph Structure

The stitched scene graph should be represented conceptually as:

- scene metadata
- scene-level defaults
- ordered groups
- ordered ungrouped layers
- ordered grouped layers
- references to active layer versions
- references to artifacts required for preview/export

### Scene Graph Required Sections

The scene graph must contain:

- scene identity and dimensions
- source image provenance references
- responsive parallax defaults
- group list
- layer list
- group membership
- active asset references
- preview settings
- export settings

---

## Scene Defaults

Scene defaults are the baseline runtime rules for the stitched scene.

They should contain at minimum:

- global scroll direction
- base parallax settings
- medium-aware defaults for `phone`, `tablet`, and `desktop`
- default depth-to-motion mapping settings
- reduced motion compatibility flags

These defaults are inherited unless overridden downstream.

---

## Group Model

Groups are first-class scene graph entities.

Each group must be able to store:

- identity and order
- group enable/disable state
- shared parallax mapping
- bounded scroll segment participation
- medium-specific overrides

### Group inheritance behavior

Layers within a group inherit:

- shared parallax mapping
- group scroll segment participation
- group responsive overrides

unless the layer explicitly overrides those properties.

---

## Layer Model

Layers are versioned scene objects.

Each layer must be able to store:

- identity and order
- visibility state
- transform state
- depth settings
- group membership
- active version reference
- source mask reference
- provenance

### Layer provenance

Layer provenance must allow tracing back to:

- originating source image(s)
- stitched scene coordinate placement
- segmentation stage
- extraction stage

---

## Responsive Parallax Representation

Responsive parallax uses one shared model.

### Scene-level representation

The scene stores:

- `responsive_defaults.phone`
- `responsive_defaults.tablet`
- `responsive_defaults.desktop`

These define the baseline mapping for each medium.

### Group-level representation

Each group may store:

- `responsive_overrides.phone`
- `responsive_overrides.tablet`
- `responsive_overrides.desktop`

These modify scene defaults where needed.

### Layer-level representation

Baseline MVP does not require layer-level medium-specific overrides.

Layers may still have general per-layer parallax overrides that apply across media.

---

## Scroll Segment Representation

Groups may participate only within bounded sections of the continuous stitched scene.

Each group scroll segment should support:

- `start_progress`
- `end_progress`
- `activation_mode`

MVP constraint:

- one simple bounded segment definition per group

No nested segment systems or timeline logic are required.

---

## Artifact Registration Rules

Artifacts are registered by the control plane, not by workers directly.

Each artifact must record:

- producing stage
- producer runtime/model
- associated scene
- associated pipeline run when relevant
- associated job when relevant
- storage location
- checksum
- coordinate space

This is required for reproducibility and safe retries.

---

## Export-Relevant State

The export pipeline must be able to derive all required output from the saved scene graph and referenced active artifacts.

Therefore the schema must explicitly persist:

- layer order
- group order
- transforms
- visibility
- depth settings
- group mappings
- scene responsive defaults
- group responsive overrides
- active layer versions

Hidden defaults are not allowed.

---

## Status Models

The schema should normalize status values for:

- scenes
- pipeline runs
- jobs
- exports

Recommended status classes:

- `pending`
- `running`
- `completed`
- `failed`
- `canceled`

Scene-specific states may also include:

- `draft`
- `ready_for_preview`
- `ready_for_export`

---

## Constraints And Invariants

The following must always hold true:

- each stitched scene has one continuous scroll canvas
- each layer belongs to exactly one scene
- each layer belongs to at most one group
- groups are flat, not nested
- each layer has exactly one active version
- each registered export references one saved scene state
- preview and export consume the same graph state

---

## Out-Of-Scope Schema Features

The MVP schema does not need:

- nested groups
- timeline animation tracks
- reusable group templates
- collaborative editing branches
- per-layer medium-specific overrides as a baseline requirement

---

## Open Questions Deferred To Later Stages

These are intentionally not required to freeze this schema plan:

- collaborative audit log granularity
- advanced manual image-alignment tooling
- future multi-scene storytelling containers beyond stitched scenes

---

## Stage 2 Freeze Criteria

This plan is ready to freeze when:

- all core entities are accepted
- group and layer semantics are accepted
- responsive parallax representation is accepted
- artifact registration rules are accepted
- preview/export state requirements are accepted

---

## Final Schema Statement

The MVP data model centers on a stitched scene graph composed of source images, flat groups, versioned layers, first-class artifacts, pipeline runs, jobs, and export records. This schema is designed so that stitching, segmentation, depth normalization, responsive parallax, preview, and export all operate from one authoritative state model.
