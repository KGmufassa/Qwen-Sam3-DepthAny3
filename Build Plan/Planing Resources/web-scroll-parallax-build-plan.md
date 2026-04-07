# Web Scroll Parallax Build Plan

## Overview

This document defines the implementation plan for a web application that:

- lets a user upload an image,
- lets the user define image elements,
- uses SAM3 to segment those elements,
- uses Depth Anything 3 to infer relative depth and parallax ordering,
- uses optional matting/refinement and optional Qwen-based enhancement for finer details,
- exposes a 2D canvas layer editor,
- maps parallax to scroll progress in a web experience,
- and later expands to multi-image stitching.

This plan treats the current repository as a planning/meta-repo, not a directly runnable integrated application.

## Product Goal

Build a first-version web app where a user can:

1. create a project,
2. upload one image,
3. choose elements with AI assistance,
4. extract those elements as editable layers,
5. preview depth-based parallax in a web scroll experience,
6. optionally refine difficult edges,
7. export the result as a web scene bundle.

## Non-Goals For MVP

- no multi-image stitching in the first release,
- no full 3D authoring tool,
- no automatic refinement application,
- no requirement that Qwen runs on every element,
- no full PSD-first creative suite in version one.

## Product Rules

- The scene graph is the source of truth.
- AI models never directly own project state.
- Refinement is auto-suggested but never auto-applied.
- All heavy inference is async, cached, and cancellable.
- The first release uses a 2D canvas layer editor.
- Depth is used for ordering and parallax strength, not full 3D transforms.

## Model Responsibilities

### SAM3

- user-guided segmentation,
- promptable mask prediction,
- iterative mask refinement,
- element boundary selection.

### Depth Anything 3

- monocular depth estimation,
- element depth ranking,
- default parallax factor estimation,
- default z-order suggestions.

### Matting / Dedicated Refinement

- edge cleanup,
- alpha refinement,
- soft detail preservation,
- halo cleanup,
- thin structure preservation.

### Qwen Image Layered / Qwen Layer Refinement

- optional advanced layer enhancement,
- difficult cutout cleanup,
- selective content-aware detail repair,
- not required in the baseline extraction path.

## Chosen Technical Architecture

### Frontend

- Next.js
- TypeScript
- React
- PixiJS for canvas/runtime
- Zustand for state
- patch-based undo/redo

### Backend Control Plane

- FastAPI
- Postgres
- Redis
- S3 or MinIO
- SSE for progress updates

### Workers

- segmentation worker
- depth worker
- matting worker
- optional Qwen layer-refine worker
- compose/export worker

### Container Strategy

- separate containers per service,
- separate GPU workers by model family,
- separate CPU services for control-plane and export,
- avoid one monolithic container.

## Monorepo Layout

```text
apps/
  web/
  api/
  realtime/
workers/
  segmentation/
  depth/
  matting/
  layer-refine/
  compose-export/
packages/
  contracts/
  scene-schema/
  storage/
  telemetry/
infra/
  docker/
  k8s/
```

## Canonical Domain Objects

### Project

- contains scenes,
- owns uploaded source assets,
- tracks export history.

### Scene

- one editable scroll experience,
- points to a base image,
- contains ordered layers,
- contains preview/export settings.

### Layer

- one editable element extracted from the source image,
- stores base and refined variants,
- stores transform and depth values,
- stores visibility and order.

### Asset

- immutable uploaded or normalized source file.

### Artifact

- immutable output from a job,
- examples: mask, rgba crop, alpha map, depth map, thumbnail, export bundle.

### PipelineRun

- a tracked execution of one or more processing stages.

### Job

- one concrete async unit of work in the pipeline.

## Scene Graph Schema

```json
{
  "scene_id": "scn_1",
  "project_id": "prj_1",
  "base_asset_id": "ast_original_1",
  "canvas": { "width": 1920, "height": 1080 },
  "scroll": {
    "mode": "vertical",
    "duration": 1.0,
    "easing": "linear"
  },
  "layers": [
    {
      "layer_id": "lyr_1",
      "name": "Foreground subject",
      "visible": true,
      "locked": false,
      "mask_asset_id": "art_mask_1",
      "base_rgba_asset_id": "art_rgba_1",
      "refined_rgba_asset_id": "art_rgba_1_refined",
      "active_rgba_asset_id": "art_rgba_1_refined",
      "bbox": { "x": 100, "y": 200, "w": 480, "h": 700 },
      "transform": { "x": 0, "y": 0, "scale": 1, "rotation": 0, "opacity": 1 },
      "depth": {
        "source": "depth-anything-3",
        "mean": 0.18,
        "manual_override": null,
        "parallax_factor": 0.72
      },
      "refinement": {
        "suggested": true,
        "enabled": true,
        "reasons": ["thin edges", "halo"]
      },
      "z_index": 10
    }
  ],
  "background": {
    "asset_id": "art_bg_1"
  },
  "version": 7
}
```

## Storage Layout

```text
raw/{project_id}/{asset_id}/original.{ext}
normalized/{project_id}/{asset_id}/image.png
normalized/{project_id}/{asset_id}/preview.webp
normalized/{project_id}/{asset_id}/thumb.webp
artifacts/{project_id}/{scene_id}/{pipeline_run_id}/segmentation/masks/{layer_id}.png
artifacts/{project_id}/{scene_id}/{pipeline_run_id}/segmentation/manifest.json
artifacts/{project_id}/{scene_id}/{pipeline_run_id}/depth/depth.exr
artifacts/{project_id}/{scene_id}/{pipeline_run_id}/depth/depth_preview.png
artifacts/{project_id}/{scene_id}/{pipeline_run_id}/matting/{layer_id}/alpha.png
artifacts/{project_id}/{scene_id}/{pipeline_run_id}/matting/{layer_id}/rgba.png
artifacts/{project_id}/{scene_id}/{pipeline_run_id}/layer_refine/{layer_id}/rgba.png
artifacts/{project_id}/{scene_id}/{pipeline_run_id}/compose/scene.json
artifacts/{project_id}/{scene_id}/{pipeline_run_id}/compose/layers/{index}_{layer_id}.webp
exports/{project_id}/{scene_id}/{pipeline_run_id}/scene_bundle.zip
```

## Database Tables

- projects
- assets
- artifacts
- scenes
- scene_versions
- layers
- pipeline_runs
- jobs
- job_events
- model_registry
- cache_entries

## API Surface

### Projects And Assets

- `POST /v1/projects`
- `POST /v1/assets/upload-url`
- `POST /v1/assets/{asset_id}/finalize`
- `POST /v1/projects/{project_id}/scenes`
- `GET /v1/scenes/{scene_id}`
- `PATCH /v1/scenes/{scene_id}`

### Segmentation

- `POST /v1/scenes/{scene_id}/segment/start`
- `POST /v1/scenes/{scene_id}/segment/predict`
- `POST /v1/scenes/{scene_id}/layers/commit-mask`

### Refinement

- `POST /v1/scenes/{scene_id}/layers/{layer_id}/matte`
- `POST /v1/scenes/{scene_id}/layers/{layer_id}/toggle-refinement`
- `POST /v1/scenes/{scene_id}/layers/{layer_id}/refine-content`

### Depth, Preview, Export

- `POST /v1/scenes/{scene_id}/depth`
- `POST /v1/scenes/{scene_id}/preview`
- `POST /v1/scenes/{scene_id}/export`

### Jobs And Pipeline Runs

- `GET /v1/pipeline-runs/{pipeline_run_id}`
- `GET /v1/pipeline-runs/{pipeline_run_id}/events`
- `POST /v1/jobs/{job_id}/cancel`

## Job Catalog

- `asset.normalize`
- `segment.generate`
- `segment.refine`
- `extract.layer`
- `quality.analyze`
- `matte.refine`
- `layer.refine`
- `depth.generate`
- `scene.compose`
- `preview.render`
- `export.bundle`

## Queue Layout

- `gpu-segmentation`
- `gpu-depth`
- `gpu-matting`
- `gpu-layer-refine`
- `cpu-compose`
- `cpu-export`

## Detailed Build Phases

## Phase 0 - Freeze Contracts

### Objective

Define the app's non-negotiable data contracts before implementation.

### Tasks

1. Define schemas for Project, Scene, Layer, Asset, Artifact, PipelineRun, and Job.
2. Define identifier strategy for all object types.
3. Define versioning rules for scene edits and pipeline outputs.
4. Define editor/runtime split between serializable scene data and transient canvas state.
5. Define one canonical artifact naming strategy.

### Deliverables

- JSON schemas
- shared TypeScript types
- backend validation models
- scene versioning rules

### Exit Criteria

- frontend and backend both compile against the same contracts,
- every pipeline stage has a declared input and output type,
- no model writes undocumented output structures.

## Phase 1 - Project Creation And Uploads

### Objective

Allow a user to create a project and upload a single source image.

### Frontend Tasks

1. Build project creation UI.
2. Build upload component with progress.
3. Implement signed-upload flow.
4. Handle upload completion and scene creation.

### Backend Tasks

1. Create `POST /v1/projects`.
2. Create `POST /v1/assets/upload-url`.
3. Create `POST /v1/assets/{asset_id}/finalize`.
4. Add asset metadata extraction.
5. Add `asset.normalize` job.

### Worker Tasks

1. Normalize uploaded image.
2. Produce canonical PNG working image.
3. Produce preview WebP.
4. Produce thumbnail.
5. Store dimensions, mime type, sha256, and color metadata.

### Deliverables

- project creation flow,
- working image normalization,
- stored preview assets.

### Exit Criteria

- a user can upload one image,
- normalized and preview assets exist,
- a scene can be created from the image.

## Phase 2 - Segmentation Session And Mask Approval

### Objective

Let the user define elements with SAM3-assisted selection.

### Frontend Tasks

1. Create `Select elements` mode in the editor.
2. Add positive point, negative point, and box selection tools.
3. Draw prompt overlays on the preview image.
4. Display candidate masks with scores.
5. Allow retry, merge, split, and accept operations.

### Backend Tasks

1. Create segmentation session endpoints.
2. Validate prompt payloads.
3. Route jobs to the segmentation worker.
4. Persist candidate artifacts for accepted masks.

### Worker Tasks

1. Load preview image.
2. Run SAM3 predictor.
3. Produce candidate masks.
4. Return score, bbox, and artifact references.

### Deliverables

- segmentation tool,
- candidate mask review UI,
- accepted mask commit flow.

### Exit Criteria

- the user can define at least one element,
- accepted masks are saved as layer seeds,
- rejected masks do not pollute final scene state.

## Phase 3 - Layer Extraction

### Objective

Turn accepted masks into editable image layers.

### Tasks

1. Align accepted mask from preview coordinates to full-resolution coordinates.
2. Crop RGBA layer from the full-resolution normalized image.
3. Create mask artifact.
4. Compute padded bbox.
5. Create layer thumbnail.
6. Create background hole image or hole region manifest.
7. Register the new layer in the scene graph.

### Outputs Per Layer

- `mask.png`
- `rgba.png`
- `bbox.json`
- `thumb.webp`
- `edge_metrics.json`

### Exit Criteria

- each accepted mask creates one editable layer,
- the layer can be loaded in the editor,
- the scene graph stores correct asset references.

## Phase 4 - Refinement Suggestion Engine

### Objective

Detect difficult edges and suggest refinement without applying it.

### Tasks

1. Analyze mask boundary complexity.
2. Detect thin protrusions and high-frequency edge regions.
3. Detect halo/background leakage.
4. Compute a quality score.
5. Produce suggestion reasons.
6. Update layer metadata with suggestion fields.

### UI Behavior

- show `Refine suggested` badge,
- expose reasons in tooltip or inspector,
- never trigger refinement automatically.

### Exit Criteria

- difficult layers are flagged,
- clean layers are not over-flagged,
- users remain in control of refinement.

## Phase 5 - 2D Canvas Editor

### Objective

Build the main editing environment.

### Frontend Module Breakdown

- `editor-shell`
- `layer-list`
- `inspector-panel`
- `pixi-runtime`
- `history-store`
- `job-progress`
- `scroll-preview`

### Supported Editor Actions

- select layer,
- move,
- scale,
- rotate,
- rename,
- toggle visibility,
- lock/unlock,
- reorder layers,
- adjust depth/parallax,
- toggle refinement asset.

### Runtime Rules

- PixiJS owns rendering,
- React owns app shell and panels,
- runtime-only objects stay out of the persistent scene graph,
- render on demand except during drag and preview playback.

### Exit Criteria

- the user can edit at least three extracted layers,
- undo/redo works for layer edits,
- the canvas stays responsive during non-inference operations.

## Phase 6 - Depth Anything 3 Integration

### Objective

Generate depth maps and assign default parallax behavior.

### Tasks

1. Add `depth.generate` job submission.
2. Run Depth Anything 3 on the normalized full image.
3. Store full depth map and preview depth map.
4. Compute per-layer depth metrics using each layer mask.
5. Set suggested z-order and parallax factor.
6. Expose manual override controls in the inspector.

### Layer Depth Fields

- source model,
- mean depth,
- median depth,
- nearest depth,
- farthest depth,
- parallax factor,
- manual override.

### Exit Criteria

- every layer has a default depth value,
- the editor can override suggested depth,
- z-order suggestions are usable but not authoritative.

## Phase 7 - Scroll Preview

### Objective

Let the user preview scroll-driven parallax in the editor.

### Tasks

1. Add preview progress state from `0` to `1`.
2. Compute layer render transforms from parallax factor and progress.
3. Add global scroll strength control.
4. Add per-layer motion tuning.
5. Add mobile sensitivity preview settings.
6. Keep preview state out of undo history.

### V1 Motion Rules

- 2D translation only,
- no perspective warp,
- no 3D camera transforms,
- minimal x/y drift allowed,
- depth changes motion strength only.

### Exit Criteria

- the user can scrub scroll progress,
- layers move at different rates,
- the preview reflects manual depth overrides.

## Phase 8 - Manual Matting Toggle

### Objective

Allow the user to apply edge refinement only when desired.

### Tasks

1. Add `Refine edges` toggle per layer.
2. Add `Refine selected` batch action.
3. Submit `matte.refine` jobs.
4. Store alpha and refined RGBA outputs separately.
5. Swap active asset reference when the toggle is enabled.
6. Allow revert to base layer instantly.

### Requirements

- preserve both base and refined asset references,
- do not destructively overwrite base extraction,
- keep refinement optional and reversible.

### Exit Criteria

- the user can turn refinement on and off,
- the scene graph updates active asset references correctly,
- the refined layer appears in preview and export.

## Phase 9 - Optional Qwen Enhancement

### Objective

Add advanced layer refinement for difficult cases.

### Tasks

1. Add `Enhance layer` action in the inspector.
2. Add prompt input or preset enhancements.
3. Submit `layer.refine` job.
4. Store enhanced RGBA outputs as additional layer versions.
5. Allow compare and revert.

### Scope Control

- do not make this part of the base extraction path,
- limit to user-invoked difficult cases,
- preserve all prior versions.

### Exit Criteria

- a difficult layer can be enhanced without breaking the layer workflow,
- Qwen remains optional,
- enhancement results remain reversible.

## Phase 10 - Export Bundle

### Objective

Generate a working web scene package.

### Tasks

1. Resolve the latest approved scene version.
2. Collect active layer assets.
3. Optimize output images.
4. Write `scene.json`.
5. Write minimal runtime JS/CSS.
6. Package bundle as ZIP.
7. Validate the bundle in a preview sandbox.

### Export Contents

```text
scene.json
assets/
  bg.webp
  layer_01.webp
  layer_02.webp
runtime/
  viewer.js
  viewer.css
index.html
```

### Exit Criteria

- exported bundle reproduces the editor scene,
- scroll-linked parallax works outside the editor,
- the user can download one ZIP package.

## Phase 11 - Production Hardening

### Objective

Make the system reliable and scalable.

### Tasks

1. Add deterministic caching keys.
2. Add retries and cancellation.
3. Add model warm-state health checks.
4. Add telemetry and timing metrics.
5. Add asset cleanup/retention policies.
6. Add GPU worker memory profile logic.

### Exit Criteria

- jobs can be retried safely,
- stale jobs can be canceled,
- model workers report readiness,
- expensive stages reuse cached outputs.

## Phase 12 - Multi-Image Stitching (Post-MVP)

### Objective

Extend the single-image system into a multi-image scroll scene.

### Tasks

1. Allow multiple source images per project.
2. Estimate overlap/alignment between adjacent images.
3. Create stitch groups in the scene graph.
4. Normalize depth scales across images.
5. Merge scene sections into one long scroll narrative.
6. Add transition controls between stitched sections.

### Important Rule

Do not start this phase until the single-image pipeline is stable.

## Frontend Precision Plan

### Editor State Layers

#### Persistent State

- project data,
- scene graph,
- layer metadata,
- inspector values,
- history entries.

#### Runtime State

- Pixi containers and sprites,
- selection overlay,
- hover state,
- active drag state,
- preview progress,
- in-flight tool state.

### Undo/Redo Strategy

- use semantic commands,
- store patch-based history,
- exclude blobs and temporary runtime state,
- group drag operations into sensible history steps.

### Asset Handling Rules

- originals are immutable,
- preview assets are used in-editor whenever possible,
- full-res assets are used for extraction and export,
- do not store base64 blobs in app state,
- dispose GPU textures with LRU behavior if needed.

## Backend Precision Plan

### Control Plane Responsibilities

- auth/session hooks,
- project and scene CRUD,
- upload finalization,
- job submission,
- job polling,
- scene versioning,
- event streaming.

### Orchestration Responsibilities

- validate pipeline requests,
- expand requests into jobs,
- enforce dependencies,
- manage retries,
- manage cancellation,
- attach outputs back to scene versions.

### Worker Responsibilities

#### Segmentation Worker

- load SAM3,
- accept prompt inputs,
- return masks, scores, bboxes,
- support iterative refinement.

#### Depth Worker

- load Depth Anything 3,
- produce depth map outputs,
- compute layer-level depth metrics.

#### Matting Worker

- accept source crop and mask,
- produce refined alpha and RGBA,
- support the manual refinement toggle.

#### Layer Refine Worker

- accept user-invoked difficult layers,
- run optional Qwen enhancement,
- output alternate refined assets.

#### Compose/Export Worker

- compile scene graph into export assets,
- render previews,
- package final bundles.

## Caching Strategy

### Cacheable Outputs

- normalized images,
- segmentation masks for identical inputs,
- depth maps,
- matting outputs,
- Qwen outputs for identical source + prompt + params.

### Non-Cacheable Outputs

- manual editor actions,
- undo/redo history,
- user-specific in-memory view state.

### Cache Key Inputs

- source asset checksum,
- model version,
- stage parameters,
- parent artifact checksums.

## Container Strategy

### Local Development

- web,
- api,
- realtime,
- postgres,
- redis,
- minio,
- CPU workers locally if needed,
- remote GPU workers if local GPU is unavailable.

### Production

- CPU pool for control plane,
- GPU pool for segmentation/depth/matting,
- separate GPU pool for optional heavy Qwen refinement if needed,
- autoscale workers based on queue depth and memory profile.

## Risks

- segmentation alone will not solve soft alpha details,
- background hole regions may need later inpainting support,
- large images can create browser and GPU memory pressure,
- Qwen enhancement can be slow and must remain optional,
- depth order can be wrong and must be manually overridable.

## Acceptance Criteria For MVP

1. A user can create a project and upload one image.
2. A user can define at least three elements with SAM3-assisted selection.
3. Each element becomes an editable layer.
4. The system suggests refinement on difficult edges but never auto-applies it.
5. The user can move, reorder, rename, and hide layers.
6. The system computes default depth/parallax values from Depth Anything 3.
7. The user can preview scroll-linked parallax in the editor.
8. The user can export a working web scene bundle.

## Recommended Build Order

1. Freeze schemas and API contracts.
2. Implement upload and asset normalization.
3. Implement scene creation and persistence.
4. Implement segmentation and mask approval.
5. Implement layer extraction.
6. Implement refinement suggestion scoring.
7. Implement the 2D canvas editor.
8. Implement depth generation and layer defaults.
9. Implement scroll preview.
10. Implement manual refinement toggle.
11. Implement export bundle generation.
12. Harden caching, retries, cancellation, and telemetry.
13. Start stitching only after the single-image workflow is stable.

## Final Recommendation

Build the first version as a single-image, 2D canvas, scroll-parallax editor with:

- SAM3 for user-guided segmentation,
- dedicated matting for optional refinement,
- Depth Anything 3 for depth ordering and parallax defaults,
- optional Qwen refinement for advanced difficult cases,
- a scene-graph-based editor architecture,
- and a containerized service split from day one.

That gives the fastest path to a strong MVP without blocking the future roadmap toward multi-image stitching and richer scene composition.
