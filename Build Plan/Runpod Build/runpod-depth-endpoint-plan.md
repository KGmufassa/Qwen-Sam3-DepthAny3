# Runpod Depth Endpoint Plan

## Purpose

This document defines the implementation plan for the Runpod depth endpoint.

This endpoint runs Depth Anything 3 and returns a depth map plus metadata useful for parallax setup.

## Endpoint Goal

Accept an image and return:

- full depth map artifact
- preview depth visualization
- optional confidence map
- optional image-level metadata
- optional summary metrics for the local API

## Endpoint Definition

- `POST /depth`

## Responsibilities

The depth endpoint is responsible for:

- validating depth requests
- downloading the source image
- decoding and normalizing the image
- running Depth Anything 3
- producing exportable depth artifacts
- uploading outputs
- returning metadata

The endpoint is not responsible for:

- layer depth aggregation using scene-state decisions
- final z-order decisions
- local scene graph updates
- parallax tuning
- retries or orchestration state

## Inputs

### Required

- image URL
- model id/version
- output target definitions

### Optional

- request confidence map
- request visualization map
- request precision format

### Example Request

```json
{
  "request_id": "req_depth_001",
  "job_id": "job_depth_001",
  "project_id": "prj_001",
  "scene_id": "scn_001",
  "model": {
    "id": "depth-anything-3-large",
    "version": "2026-04"
  },
  "input": {
    "image_url": "https://signed-url/input.png"
  },
  "params": {
    "output_confidence": true,
    "output_preview": true,
    "depth_format": "exr"
  },
  "output_targets": {
    "depth_upload_url": "https://signed-url/depth.exr",
    "preview_upload_url": "https://signed-url/depth_preview.png",
    "confidence_upload_url": "https://signed-url/confidence.exr"
  }
}
```

## Outputs

### Required Outputs

- depth artifact metadata
- preview artifact metadata if requested
- confidence artifact metadata if requested
- timing information
- original image dimensions

### Example Response

```json
{
  "request_id": "req_depth_001",
  "job_id": "job_depth_001",
  "status": "succeeded",
  "artifacts": [
    {
      "type": "depth_map",
      "url": "https://storage/depth.exr",
      "width": 1920,
      "height": 1080,
      "format": "exr"
    },
    {
      "type": "depth_preview",
      "url": "https://storage/depth_preview.png",
      "width": 1920,
      "height": 1080,
      "format": "png"
    }
  ],
  "metrics": {
    "duration_ms": 4100
  },
  "warnings": [],
  "error": null
}
```

## Internal Processing Steps

### Step 1 - Validate Request

- verify required fields
- verify image URL
- verify supported model id
- verify requested output format
- verify target URLs are present for requested outputs

### Step 2 - Download Input Image

- fetch image from signed URL
- validate content type
- validate byte size
- save to temp workspace

### Step 3 - Decode And Normalize

- normalize orientation
- convert to model-compatible format
- preserve source dimensions
- log image size

### Step 4 - Run Depth Anything 3

- load or reuse model runtime
- preprocess image
- run forward inference
- obtain raw depth tensor
- optionally obtain confidence map if supported

### Step 5 - Post-Process Depth

- resize back to source resolution if needed
- normalize only for preview output
- preserve raw/scaled depth data for machine use
- generate preview visualization
- validate numeric ranges

### Step 6 - Upload Outputs

- upload depth map
- upload preview visualization
- upload confidence map if requested
- verify each upload

### Step 7 - Return Result

- return artifact list
- return timings
- return warnings if normalization or fallback occurred

## Failure Handling

### Retryable Errors

- input download failure
- output upload failure
- transient inference timeout
- transient GPU failure

### Non-Retryable Errors

- unsupported image format
- bad output format request
- invalid request shape
- missing target URL for requested output

## Performance Considerations

### Warm Runtime

- keep model warm across requests
- avoid repeated initialization

### Numeric Format Policy

- keep machine-readable output distinct from human preview output
- do not use preview-normalized depth as the canonical artifact

### Suggested Constraints

- cap very large image size or tile later if needed
- fail clearly if memory ceiling is exceeded

## Implementation Tasks

1. define request and response schemas
2. implement image downloader
3. integrate Depth Anything 3 runtime
4. implement raw depth serialization
5. implement preview rendering
6. implement confidence handling if available
7. implement uploads
8. implement structured errors
9. add health endpoints
10. add logs and timings
11. run dimensional consistency tests

## Test Plan

### Unit Tests

- request validation
- depth output format selection
- preview generation
- error mapping

### Integration Tests

- valid image request
- large image request
- confidence output request
- output upload verification

### Manual Tests

- portrait image
- landscape image
- cluttered scene
- image with strong foreground/background separation

## Exit Criteria

- endpoint returns valid depth artifacts
- preview output matches expected dimensions
- raw depth artifact is suitable for local layer aggregation
- endpoint can be called repeatedly without model reload issues

## Efficiency Suggestion

Add deterministic depth caching keyed by image checksum and model version.

Depth inference is expensive and often repeated unchanged. Reusing stored outputs will significantly reduce latency and cost.
