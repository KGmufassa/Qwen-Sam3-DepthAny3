# API And Job Contract Plan

## Document Purpose

This document defines the application-facing API contract and asynchronous job contract for the MVP.

It focuses on:

- resource boundaries
- route domains
- request and response patterns
- job lifecycles
- status semantics
- how workers are invoked through the control plane

This plan does not define worker-internal implementation details. Those belong in the worker runtime contract plan.

---

## Contract Principles

- the control plane owns workflow state
- workers are invoked through explicit job contracts
- all heavy operations are asynchronous jobs
- all request payloads should be typed and versionable
- all result payloads should reference registered artifacts, not raw implicit files

---

## API Domains

The MVP API surface should be organized into these domains:

- projects
- stitched scenes
- uploads
- stitching
- segmentation
- layers
- groups
- depth
- preview
- exports
- jobs

---

## Standard Response Envelope

All non-streaming API responses should use a consistent envelope:

- `success`
- `data`
- `error`
- `request_id`

Optional:

- `warnings`

This keeps route behavior predictable across the app.

---

## Standard Job Result Shape

Every job-oriented response should expose at minimum:

- `job_id`
- `pipeline_run_id` if applicable
- `status`
- `scene_id`
- `type`
- `created_at`

Result payloads should be retrieved either:

- directly when complete, or
- through the jobs/status endpoint

---

## Core Route Set

### Projects

#### `POST /v1/projects`

Creates a project.

#### `GET /v1/projects/{project_id}`

Returns project metadata and active scene references.

---

### Uploads

#### `POST /v1/scenes/{scene_id}/uploads/init`

Creates upload targets for multiple source images.

Request should include:

- filename
- mime type
- size hint
- source index

Response should include:

- upload target metadata
- upload token or signed target

#### `POST /v1/scenes/{scene_id}/uploads/finalize`

Registers uploaded source images and creates normalized preprocessing jobs if needed.

---

### Stitching

#### `POST /v1/scenes/{scene_id}/stitch/start`

Creates a stitch job for one set of source images.

Request should include:

- ordered source image references
- stitch options

Response:

- created job metadata

#### `GET /v1/scenes/{scene_id}/stitch/status`

Returns current stitch job and stitched artifact status.

---

### Segmentation

#### `POST /v1/scenes/{scene_id}/segment/predict`

Creates a segmentation job or segmentation session request using the stitched scene artifact.

Request should include:

- prompt inputs
- image reference
- segmentation session reference if used

Response:

- job metadata or immediate candidate session metadata

#### `POST /v1/scenes/{scene_id}/layers/commit-mask`

Commits one approved mask into a layer seed.

Request should include:

- mask artifact reference
- candidate metadata
- naming hint if present

Response:

- committed seed state

---

### Layers

#### `POST /v1/scenes/{scene_id}/layers/extract`

Creates extraction jobs for committed masks.

#### `PATCH /v1/layers/{layer_id}`

Updates layer properties.

Supported fields may include:

- name
- visibility
- order index
- transform
- depth settings
- parallax override
- group id

#### `POST /v1/layers/{layer_id}/matte`

Creates a matte refinement job for one layer version.

#### `POST /v1/layers/{layer_id}/refine-content`

Creates an optional Qwen refinement job for one layer version.

---

### Groups

#### `POST /v1/scenes/{scene_id}/groups`

Creates one group.

#### `PATCH /v1/groups/{group_id}`

Updates one group.

Supported fields may include:

- name
- order index
- parallax mapping
- responsive overrides
- scroll segment

#### `POST /v1/groups/{group_id}/layers`

Assigns or reassigns layers to one group.

MVP contract:

- each layer may belong to at most one group

---

### Depth

#### `POST /v1/scenes/{scene_id}/depth`

Creates a depth job for the stitched scene.

Request should include:

- stitched scene artifact reference
- depth options

Response:

- job metadata

#### `GET /v1/scenes/{scene_id}/depth/status`

Returns depth artifact and normalization status.

---

### Preview

#### `GET /v1/scenes/{scene_id}/preview`

Returns normalized preview payload derived from saved scene graph state.

This payload must include:

- scene dimensions
- layer order
- group mappings
- active assets
- responsive defaults
- group responsive overrides

---

### Exports

#### `POST /v1/scenes/{scene_id}/export`

Creates an export job.

#### `GET /v1/scenes/{scene_id}/exports`

Lists export history for the scene.

#### `GET /v1/exports/{export_id}`

Returns one export record.

---

### Jobs

#### `GET /v1/jobs/{job_id}`

Returns one job status record.

#### `POST /v1/jobs/{job_id}/retry`

Retries a retryable job.

#### `POST /v1/jobs/{job_id}/cancel`

Requests cancellation where supported.

---

## Job Types

The MVP should support these job types:

- `stitch.generate`
- `segment.generate`
- `extract.layer`
- `depth.generate`
- `matte.layer`
- `layer.refine`
- `export.bundle`

Each job must be tied to:

- one stitched scene
- one type
- one status lifecycle

---

## Job Status Lifecycle

Standard lifecycle:

- `pending`
- `running`
- `completed`
- `failed`
- `canceled`

Optional intermediate states may include:

- `queued`
- `uploading_results`

But the public contract should remain simple.

---

## Job Ownership Model

The control plane owns:

- job creation
- validation
- deduping/idempotency rules
- job state transitions
- artifact registration from results

Workers own:

- execution
- raw result generation
- result payload return

Workers do not mark scene semantics complete on their own.

---

## Idempotency Rules

Heavy operations should support idempotency by:

- scene id
- job type
- relevant input checksum
- model/version identity where relevant

This is especially important for:

- stitch jobs
- depth jobs
- export jobs

---

## Artifact Referencing Rules

All API contracts that produce meaningful outputs must return:

- artifact ids
- artifact types
- artifact metadata references

They should not rely on unnamed or implicit files.

---

## Preview Payload Contract

The preview endpoint should return a scene-graph-derived payload that is sufficient for runtime rendering.

At minimum it must contain:

- stitched scene metadata
- active layer assets
- layer transforms
- group membership
- group parallax mappings
- scene-level medium defaults
- group-level medium overrides
- layer-level general parallax overrides

This payload should be medium-selectable.

Suggested query parameter:

- `medium=phone|tablet|desktop`

---

## Export Contract

The export endpoint must create a job from saved scene graph state.

The export result should include:

- export record id
- bundle artifact id
- manifest artifact id
- exported scene version reference if tracked

Export must not derive behavior from hidden defaults not stored in the scene graph.

---

## Error Model

Errors should be normalized into classes such as:

- validation error
- authorization error
- conflict error
- not found error
- worker unavailable error
- job failed error
- timeout error

Error payloads should be concise and typed enough for UI handling.

---

## Versioning Guidance

The API should be versioned under `/v1`.

Contract-breaking changes after freeze should require:

- new version, or
- explicit migration strategy

---

## Out-Of-Scope API Features

The MVP does not require:

- websocket-only job handling
- collaborative edit APIs
- per-layer responsive override APIs as baseline
- timeline animation endpoints

---

## Freeze Criteria

This plan is ready to freeze when:

- route domains are accepted
- job lifecycle semantics are accepted
- preview payload shape is accepted
- export contract is accepted
- group and responsive parallax controls are represented

---

## Final Contract Statement

The MVP API contract is a control-plane-first, job-oriented interface where stitched scenes, groups, layers, depth generation, preview, and export are all represented explicitly, and where all heavy work is routed through typed asynchronous jobs whose outputs are registered as first-class artifacts.
