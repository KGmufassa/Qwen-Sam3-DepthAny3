# Runpod Segmentation Endpoint Plan

## Purpose

This document defines the implementation plan for the Runpod segmentation endpoint.

This endpoint runs SAM3 and returns user-guided mask predictions for selected image elements.

## Endpoint Goal

Accept an image plus user prompts and return:

- candidate masks
- scores
- bounding boxes
- artifact references for saved masks
- optional low-resolution previews

## Endpoint Definition

- `POST /segment`

## Responsibilities

The segmentation endpoint is responsible for:

- validating segmentation requests
- downloading the source image
- decoding and normalizing the image
- applying user prompts
- running SAM3 inference
- producing one or more candidate masks
- uploading mask artifacts if configured
- returning structured results

The endpoint is not responsible for:

- project persistence
- scene graph updates
- retries
- prompt editing workflow
- accepted-mask storage policy beyond requested upload targets

## Inputs

### Required

- image URL
- prompt mode
- prompt payload
- model id/version
- output target definitions

### Supported Prompt Types

- positive points
- negative points
- bounding box
- optional initial mask

### Example Request

```json
{
  "request_id": "req_seg_001",
  "job_id": "job_seg_001",
  "project_id": "prj_001",
  "scene_id": "scn_001",
  "model": {
    "id": "sam3-large",
    "version": "2026-04"
  },
  "input": {
    "image_url": "https://signed-url/input.png"
  },
  "params": {
    "mode": "points_and_box",
    "positive_points": [[420, 133], [450, 180]],
    "negative_points": [[390, 210]],
    "box": [300, 100, 700, 950],
    "return_candidates": 3
  },
  "output_targets": {
    "mask_uploads": [
      "https://signed-url/mask1.png",
      "https://signed-url/mask2.png",
      "https://signed-url/mask3.png"
    ]
  }
}
```

## Outputs

### Required Outputs

- candidate list
- score per candidate
- bbox per candidate
- uploaded mask artifact metadata
- timing info

### Example Response

```json
{
  "request_id": "req_seg_001",
  "job_id": "job_seg_001",
  "status": "succeeded",
  "artifacts": [
    {
      "type": "mask",
      "candidate_id": "cand_1",
      "url": "https://storage/mask1.png",
      "width": 1024,
      "height": 1024
    }
  ],
  "candidates": [
    {
      "candidate_id": "cand_1",
      "score": 0.94,
      "bbox": [300, 100, 700, 950]
    }
  ],
  "metrics": {
    "duration_ms": 2800
  },
  "warnings": [],
  "error": null
}
```

## Internal Processing Steps

### Step 1 - Validate Request

- verify required fields
- verify prompt structure
- verify image URL format
- verify model id is supported
- reject malformed coordinate arrays

### Step 2 - Download Input Image

- fetch from signed URL
- validate content type
- validate byte size
- store to temp working path

### Step 3 - Decode And Normalize

- decode to RGB
- preserve original width and height
- normalize orientation
- reject corrupted files

### Step 4 - Convert Prompt Coordinates

- confirm coordinate system
- map prompts to model input size if resizing is required
- preserve transform metadata if returned to caller

### Step 5 - Run SAM3

- load or reuse warm SAM3 predictor
- prepare image embedding
- apply prompt encoding
- generate mask candidates
- compute confidence scores

### Step 6 - Post-Process Masks

- threshold masks if needed
- derive bounding boxes
- validate mask dimensions
- optionally generate small preview overlays

### Step 7 - Upload Outputs

- upload each candidate mask to provided signed URL
- verify upload success
- collect output metadata

### Step 8 - Return Result

- return candidates
- return artifact references
- return timings and warnings

## Failure Handling

### Retryable Errors

- signed URL fetch timeout
- transient storage upload failure
- temporary GPU memory failure if endpoint supports internal retry

### Non-Retryable Errors

- bad prompts
- unsupported image format
- invalid coordinates
- model id mismatch
- malformed request body

## Performance Considerations

### Warm Model Strategy

- load SAM3 on process startup or first request
- reuse predictor across requests
- avoid reloading model per request

### Input Resolution Policy

- if source image is extremely large, run a bounded inference size
- return transform metadata so local API can map masks accurately later

### Suggested Guardrails

- max image dimension
- max request body size
- max candidate count
- request timeout

## Implementation Tasks

1. define request schema
2. define response schema
3. implement auth middleware
4. implement image download utility
5. implement prompt validation utility
6. integrate SAM3 runtime
7. implement candidate serialization
8. implement output upload helper
9. implement structured errors
10. add health and readiness endpoints
11. add metrics logging
12. test with point-only, box-only, and mixed prompts

## Test Plan

### Unit Tests

- request validation
- prompt parsing
- bbox extraction
- error response formatting

### Integration Tests

- signed image download
- successful SAM3 inference
- multi-candidate upload
- malformed request rejection

### Manual Tests

- portrait image with simple subject
- image with multiple objects
- image with small thin objects
- prompt correction with positive and negative points

## Exit Criteria

- endpoint returns correct candidate masks
- errors are normalized
- uploaded masks are retrievable
- latency is acceptable for interactive usage
- local API can integrate without endpoint-specific hacks

## Efficiency Suggestion

Cache image embeddings for repeated prompt refinement on the same image.

This will significantly improve interactive segmentation because later prompt adjustments can reuse the image embedding instead of recomputing it on every call.
