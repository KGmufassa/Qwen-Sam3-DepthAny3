# Runpod Matting Endpoint Plan

## Purpose

This document defines the implementation plan for the Runpod matting endpoint.

This endpoint refines a base extracted layer using a source crop and mask and returns a refined alpha plus refined RGBA output.

## Endpoint Goal

Accept a source crop and a mask and return:

- refined alpha
- refined RGBA
- optional refined mask
- quality metadata
- timing metrics

## Endpoint Definition

- `POST /matte`

## Responsibilities

The matting endpoint is responsible for:

- validating requests
- downloading crop and mask inputs
- aligning dimensions
- running dedicated alpha or edge refinement
- producing refined alpha
- composing refined RGBA
- uploading outputs
- returning metadata

The endpoint is not responsible for:

- deciding whether refinement should be auto-applied
- persisting scene graph changes
- replacing base assets
- project state management

## Inputs

### Required

- source crop URL
- mask URL
- model id/version
- output target definitions

### Optional

- trimap mode
- feather radius
- background cleanup mode

### Example Request

```json
{
  "request_id": "req_matte_001",
  "job_id": "job_matte_001",
  "project_id": "prj_001",
  "scene_id": "scn_001",
  "model": {
    "id": "matting-model-1",
    "version": "2026-04"
  },
  "input": {
    "crop_url": "https://signed-url/crop.png",
    "mask_url": "https://signed-url/mask.png"
  },
  "params": {
    "trimap_mode": "auto",
    "preserve_transparency": true
  },
  "output_targets": {
    "alpha_upload_url": "https://signed-url/alpha.png",
    "rgba_upload_url": "https://signed-url/refined_rgba.png"
  }
}
```

## Outputs

### Required Outputs

- refined alpha artifact
- refined RGBA artifact
- image dimensions
- timing information
- optional warnings

### Example Response

```json
{
  "request_id": "req_matte_001",
  "job_id": "job_matte_001",
  "status": "succeeded",
  "artifacts": [
    {
      "type": "alpha",
      "url": "https://storage/alpha.png",
      "width": 900,
      "height": 1200
    },
    {
      "type": "refined_rgba",
      "url": "https://storage/refined_rgba.png",
      "width": 900,
      "height": 1200
    }
  ],
  "metrics": {
    "duration_ms": 3500
  },
  "warnings": [],
  "error": null
}
```

## Internal Processing Steps

### Step 1 - Validate Request

- verify crop URL and mask URL
- verify model id
- verify output target URLs
- verify optional params

### Step 2 - Download Inputs

- fetch crop image
- fetch mask image
- validate both
- store in temp workspace

### Step 3 - Align Dimensions

- ensure crop and mask dimensions match
- reject or normalize mismatches explicitly
- convert mask to expected format
- derive trimap if required

### Step 4 - Run Matting Model

- load or reuse model runtime
- preprocess crop and mask
- run alpha refinement
- obtain refined alpha map

### Step 5 - Compose Refined RGBA

- apply refined alpha to crop
- preserve source color channels
- validate output bounds and alpha values

### Step 6 - Optional Quality Checks

- detect empty output
- detect alpha collapse
- detect suspicious hard-edge fallback
- add warnings if needed

### Step 7 - Upload Outputs

- upload alpha
- upload refined RGBA
- verify upload success

### Step 8 - Return Result

- return artifact metadata
- return timings
- return warnings

## Failure Handling

### Retryable Errors

- transient download failure
- transient upload failure
- temporary GPU inference failure

### Non-Retryable Errors

- crop and mask dimension mismatch if policy is strict
- malformed mask
- unsupported image mode
- invalid request parameters

## Performance Considerations

### Runtime Reuse

- keep model warm
- avoid per-request initialization

### Input Sizing

- reject extreme dimensions early
- avoid silent resizing that misaligns alpha unless explicitly logged

### Output Integrity

- verify alpha image is not all-zero
- verify refined RGBA dimensions match crop dimensions

## Implementation Tasks

1. define request/response schema
2. implement crop and mask downloader
3. implement dimension matching validation
4. integrate matting runtime
5. implement trimap generation if needed
6. implement RGBA recomposition
7. implement output upload
8. implement error normalization
9. add health endpoints
10. add logs and warnings
11. test against portrait, hair, and thin-edge examples

## Test Plan

### Unit Tests

- request validation
- dimension checks
- alpha recomposition
- warning generation

### Integration Tests

- crop + mask download
- successful alpha generation
- output upload verification
- malformed mask rejection

### Manual Tests

- hair edges
- semi-transparent fabric
- thin object edges
- simple hard-edge object as control case

## Exit Criteria

- endpoint produces refined alpha and RGBA correctly
- outputs are usable as reversible alternate layer assets
- failures are explicit and easy for local API to classify

## Efficiency Suggestion

Only invoke matting on user-approved difficult layers, not all layers.

This matches the product rule, reduces GPU cost, and avoids spending compute on already-clean cutouts.
