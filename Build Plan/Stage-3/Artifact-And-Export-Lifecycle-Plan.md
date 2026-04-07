# Artifact And Export Lifecycle Plan

## Document Purpose

This document defines how artifacts are created, promoted, retained, and consumed through the stitched-scene workflow, with special focus on preview and export.

It answers:

- when artifacts are created
- which artifacts are canonical
- how active layer versions are selected
- how export consumes artifacts
- what retention expectations exist at MVP level

---

## Lifecycle Principles

- artifacts are first-class registered entities
- the control plane decides which artifacts become official scene state
- export consumes saved scene graph state plus active artifacts
- canonical machine-use artifacts and preview-use artifacts must be distinguished
- failed artifacts must not masquerade as accepted outputs

---

## Artifact Lifecycle Stages

Each artifact should move through some subset of these lifecycle stages:

- declared
- produced
- registered
- activated if scene-relevant
- superseded if replaced
- retained or cleaned up according to policy

---

## Canonical Artifact Families

The MVP requires lifecycle handling for:

- source original images
- normalized source images
- stitched scene artifacts
- mask artifacts
- mask preview artifacts
- extracted layer RGBA artifacts
- extracted alpha artifacts
- layer thumbnails
- depth artifacts
- depth preview artifacts
- refined layer artifacts
- export bundle artifacts
- export manifest artifacts

---

## Source Artifact Lifecycle

### Creation

- original upload registered
- normalized version created and registered

### Canonical role

- original supports provenance and reprocessing
- normalized image supports processing pipeline use

### Retention expectation

- both should be retained at MVP unless explicit cleanup policy removes them later

---

## Stitch Artifact Lifecycle

### Creation

- stitch/alignment worker produces stitched scene artifact

### Registration

- control plane registers stitched artifact and provenance metadata

### Canonical role

- stitched scene artifact is the canonical scene-processing image for segmentation and depth

### Replacement behavior

- if a stitch is rerun and accepted, the previous stitched artifact may be superseded but should remain traceable

---

## Mask Artifact Lifecycle

### Creation

- segmentation worker produces candidate mask artifacts

### Registration

- control plane registers mask artifacts

### Promotion

- only accepted masks become layer seeds in scene semantics

### Non-accepted masks

- may remain as artifacts for traceability
- must not be treated as committed layer state

---

## Layer Artifact Lifecycle

### Creation

- extraction produces RGBA and optional alpha outputs
- thumbnail is generated

### Registration

- control plane registers all outputs

### Activation

- extracted base layer version becomes the active version for the new layer

### Refinement behavior

- matte or Qwen refine outputs create alternate versions
- alternate versions are not active unless explicitly promoted

---

## Depth Artifact Lifecycle

### Creation

- depth worker produces canonical depth output and preview visualization

### Registration

- control plane registers both artifacts

### Canonical role

- canonical depth artifact is for machine-use and metric computation
- preview depth artifact is for user inspection

The preview depth artifact must not replace the canonical depth artifact as the machine source.

---

## Version Activation Rules

Only one layer version is active at a time.

Changing active version requires:

- explicit control-plane state mutation
- scene graph update

Failed or incomplete versions must never become active implicitly.

---

## Preview Consumption Rules

Preview should consume:

- current stitched scene graph
- active layer versions
- current group mappings
- current scene and group responsive settings

Preview should never consume:

- unregistered artifacts
- non-active layer versions
- hidden export-only defaults

---

## Export Consumption Rules

Export must consume:

- saved stitched scene graph
- active layer versions
- active stitched scene artifact references where needed
- saved group and responsive behavior

Export must not consume:

- transient preview-only state
- unaccepted segmentation candidates
- failed artifact outputs

---

## Export Bundle Role

The export bundle is a derived artifact generated from the current accepted scene state.

It is not the source of truth for the scene.

The source of truth remains:

- scene graph state
- artifact registry

---

## Manifest Rules

The export manifest should describe:

- scene dimensions
- layer ordering
- group structure
- active assets
- parallax settings
- responsive settings

The manifest must contain enough information to reproduce runtime behavior without hidden defaults.

---

## Artifact Supersession Rules

Supersession happens when:

- a stitched scene is rerun and replaced
- a layer gets a new active version
- an export is regenerated

Superseded artifacts should remain traceable even if they are not active.

MVP does not require immediate hard deletion of superseded artifacts.

---

## Cleanup And Retention Guidance

The MVP should define at least conceptual retention behavior for:

- rejected masks
- failed intermediate outputs
- superseded layer versions
- old exports

Recommended MVP posture:

- preserve traceability first
- defer aggressive cleanup until retention rules are finalized operationally

---

## Artifact State Rules

Artifacts should conceptually be classifiable as:

- `registered`
- `active`
- `inactive`
- `superseded`
- `failed`

This can be represented directly or inferred, but the behavior should remain clear.

---

## Failure Handling In Lifecycle Terms

If a worker produces an artifact but registration fails:

- the artifact is not official scene state
- retry/reconciliation should be possible

If a job fails after partial outputs exist:

- those outputs should not be treated as active without explicit acceptance

---

## Provenance Requirements

Important artifacts should be traceable back to:

- producing stage
- producing job
- pipeline run
- source scene
- producer runtime/model

This is especially important for:

- stitched scene outputs
- masks
- depth artifacts
- refined layer variants
- exports

---

## Out-Of-Scope Lifecycle Features

The MVP does not require:

- aggressive automated cleanup
- full retention automation
- user-facing artifact browser beyond what the editor needs

---

## Freeze Criteria

This plan is ready to freeze when:

- canonical artifact families are accepted
- activation rules are accepted
- preview and export consumption rules are accepted
- supersession rules are accepted
- retention posture is accepted

---

## Final Lifecycle Statement

The MVP artifact and export lifecycle is built around first-class registered artifacts, explicit activation of layer versions, strict separation between canonical machine-use outputs and preview-friendly derivatives, and export generation that consumes only accepted stitched scene state and active artifacts.
