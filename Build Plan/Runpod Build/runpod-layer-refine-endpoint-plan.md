# Runpod Layer Refine Endpoint Plan

## Purpose

This document defines the implementation plan for the optional Runpod layer refinement endpoint.

This endpoint uses Qwen-style refinement only for difficult user-invoked layers.

## Endpoint Goal

Accept a layer crop, mask, and optional prompt and return:

- enhanced RGBA output
- optional repaired details
- optional alternate alpha-preserving output
- timing and warning metadata

## Endpoint Definition

- `POST /refine-layer`

## Responsibilities

The layer refinement endpoint is responsible for:

- validating requests
- downloading input crop and optional mask
- loading Qwen refinement runtime
- applying requested refinement prompt or preset
- preserving alpha behavior if requested
- uploading refined results
- returning metadata

The endpoint is not responsible for:

- deciding which layers need enhancement automatically
- base segmentation
- basic matting
- scene graph state updates
- export registration

## Inputs

### Required

- crop URL
- model id/version
- output target definitions

### Optional

- mask URL
- prompt
- preserve alpha flag
- preset name
- strength setting

### Example Request

```json
{
  "request_id": "req_refine_001",
  "job_id": "job_refine_001",
  "project_id": "prj_001",
  "scene_id": "scn_001",
  "model": {
    "id": "qwen-image-edit",
    "version": "2026-04"
  },
  "input": {
    "crop_url": "https://signed-url/crop.png",
    "mask_url": "https://signed-url/mask.png"
  },
  "params": {
    "prompt": "restore fine hair strands and clean the shoulder edge",
    "preserve_alpha": true,
    "preset": "detail_cleanup",
    "strength": 0.35
  },
  "output_targets": {
    "rgba_upload_url": "https://signed-url/refined_layer.png"
  }
}
```

## Outputs

### Required Outputs

- refined RGBA artifact
- dimensions
- timing info
- warning list

### Example Response

```json
{
  "request_id": "req_refine_001",
  "job_id": "job_refine_001",
  "status": "succeeded",
  "artifacts": [
    {
      "type": "refined_rgba",
      "url": "https://storage/refined_layer.png",
      "width": 900,
      "height": 1200
    }
  ],
  "metrics": {
    "duration_ms": 12800
  },
  "warnings": [],
  "error": null
}
```

## Internal Processing Steps

### Step 1 - Validate Request

- verify crop URL
- verify prompt or preset policy
- verify output target URL
- verify strength range
- verify alpha-preservation flag type

### Step 2 - Download Inputs

- fetch crop
- fetch optional mask
- validate inputs
- save to temp workspace

### Step 3 - Prepare Refinement Context

- normalize crop
- apply mask guidance if provided
- build final prompt from prompt plus preset if needed
- decide whether alpha must be preserved exactly or approximately

### Step 4 - Run Qwen Refinement

- load or reuse warm model
- run refinement
- collect output image
- detect gross failures or invalid output

### Step 5 - Preserve Or Reapply Alpha

- if `preserve_alpha=true`, reapply source or refined alpha policy
- validate dimensions and mode
- ensure output remains editor-compatible

### Step 6 - Upload Outputs

- upload refined RGBA
- verify upload success

### Step 7 - Return Result

- return artifact metadata
- return timings
- return warnings if alpha reapplication or fallback happened

## Failure Handling

### Retryable Errors

- transient download failure
- transient upload failure
- temporary GPU failure
- internal timeout if caller policy allows retry

### Non-Retryable Errors

- malformed prompt parameters
- unsupported crop format
- missing required output target
- invalid strength value

## Product Safeguards

### Required Product Rules

- endpoint is never called automatically for all layers
- endpoint is user-invoked only
- outputs are stored as alternate layer versions
- base assets remain untouched
- compare/revert remains possible

## Performance Considerations

### Runtime Reuse

- keep heavy Qwen runtime warm
- avoid cold-starting on every request

### Invocation Policy

- use only for difficult cases
- keep disabled by default in local workflows

### Output Validation

- reject blank outputs
- warn on drastic dimension mismatch
- warn if preserve-alpha was requested but exact preservation was not possible

## Implementation Tasks

1. define request/response schemas
2. implement crop and mask download utilities
3. implement prompt/preset resolver
4. integrate Qwen runtime
5. implement alpha preservation policy
6. implement upload flow
7. implement error normalization
8. add timings and warnings
9. add health endpoints
10. validate manual-only product integration

## Test Plan

### Unit Tests

- prompt validation
- preset expansion
- strength validation
- alpha preservation policy

### Integration Tests

- valid crop refinement
- crop + mask refinement
- upload verification
- malformed request rejection

### Manual Tests

- difficult hair layer
- clothing edge cleanup
- partially occluded object repair
- no-prompt preset-only invocation

## Exit Criteria

- endpoint produces reversible enhanced layer outputs
- endpoint does not disturb the base extraction workflow
- local API can safely classify and store outputs as optional alternates

## Efficiency Suggestion

Do not expose free-form refinement first.

Start with a small preset set such as:

- `detail_cleanup`
- `edge_cleanup`
- `minor_repair`

This will reduce prompt variance, improve repeatability, and make caching more effective.
