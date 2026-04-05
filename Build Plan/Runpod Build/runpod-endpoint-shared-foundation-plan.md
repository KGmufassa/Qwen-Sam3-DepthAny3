# Runpod Endpoint Shared Foundation Plan

## Purpose

This document defines the shared implementation plan for all Runpod remote inference endpoints used by the application.

These endpoints are:

- segmentation
- depth
- matting
- layer refinement

The goal is to keep Runpod as a pure remote inference layer while the local application remains the source of truth for:

- projects
- scenes
- jobs
- artifacts
- scene graph state
- export state

## Core Rule

Runpod performs compute only.

Runpod must not become the system of record.

That means Runpod should not own:

- persistent project metadata
- scene versions
- final artifact registration
- retry policy
- orchestration logic
- editor state

## Shared Architecture

### Local Side Responsibilities

The local API is responsible for:

- creating jobs
- generating signed input URLs
- calling Runpod endpoints
- receiving or polling for results
- storing artifact metadata
- updating job status
- updating scene graph state
- caching repeated requests

### Runpod Side Responsibilities

Each Runpod endpoint is responsible for:

- validating request payloads
- downloading inputs from signed URLs
- loading the requested model runtime
- running inference
- uploading outputs to signed artifact URLs or returning output metadata
- returning structured result payloads
- surfacing clear error codes

## Shared Request Pattern

Every endpoint request should contain:

- `request_id`
- `job_id`
- `project_id`
- `scene_id`
- `input`
- `model`
- `params`
- `output_targets`
- `trace`

### Required Request Fields

```json
{
  "request_id": "req_123",
  "job_id": "job_123",
  "project_id": "prj_123",
  "scene_id": "scn_123",
  "model": {
    "id": "model-name",
    "version": "v1"
  },
  "input": {},
  "params": {},
  "output_targets": {},
  "trace": {
    "source": "local-api",
    "timestamp": "2026-04-04T12:00:00Z"
  }
}
```

## Shared Response Pattern

Every endpoint response should contain:

- `request_id`
- `job_id`
- `status`
- `artifacts`
- `metrics`
- `warnings`
- `error`

### Success Response

```json
{
  "request_id": "req_123",
  "job_id": "job_123",
  "status": "succeeded",
  "artifacts": [],
  "metrics": {
    "duration_ms": 3200,
    "model_load_ms": 0
  },
  "warnings": [],
  "error": null
}
```

### Failure Response

```json
{
  "request_id": "req_123",
  "job_id": "job_123",
  "status": "failed",
  "artifacts": [],
  "metrics": {
    "duration_ms": 820
  },
  "warnings": [],
  "error": {
    "code": "INPUT_DOWNLOAD_FAILED",
    "message": "Could not fetch source asset",
    "retryable": true
  }
}
```

## Shared Error Codes

All endpoints should normalize errors into a common set first.

### Input Errors

- `INVALID_REQUEST`
- `MISSING_REQUIRED_FIELD`
- `BAD_SIGNED_URL`
- `INPUT_DOWNLOAD_FAILED`
- `UNSUPPORTED_IMAGE_FORMAT`

### Runtime Errors

- `MODEL_NOT_AVAILABLE`
- `MODEL_INIT_FAILED`
- `INFERENCE_FAILED`
- `OUT_OF_MEMORY`
- `TIMEOUT`

### Output Errors

- `OUTPUT_UPLOAD_FAILED`
- `INVALID_OUTPUT_PAYLOAD`

## Shared Output Strategy

Prefer output upload targets over returning large binary payloads inline.

### Recommended Flow

1. Local API generates signed input URLs.
2. Local API generates signed output URLs or output target descriptors.
3. Runpod downloads input artifacts.
4. Runpod runs inference.
5. Runpod uploads outputs to object storage.
6. Runpod returns artifact metadata only.

## Shared Authentication Plan

### Recommended Controls

- static service token between local API and Runpod
- HMAC request signing if needed later
- short-lived signed URLs for input/output assets
- strict request timestamp tolerance

### Rule

Never expose raw internal storage credentials to Runpod containers.

## Shared Timeout Plan

### Suggested Limits

- segmentation: 30 to 60 seconds
- depth: 30 to 60 seconds
- matting: 30 to 90 seconds
- layer refine: 60 to 180 seconds

### Local API Rule

The local API should enforce:

- client timeout
- retry policy
- job cancellation
- stale job cleanup

Runpod should only report execution status.

## Shared Logging Plan

Each endpoint should emit:

- request id
- job id
- model id
- start time
- end time
- duration
- image dimensions
- device used
- warning list
- error details if failure

## Shared Health Endpoints

Each Runpod service should expose:

- `GET /healthz`
- `GET /readyz`

### `healthz`

Checks:

- process alive
- HTTP service responding

### `readyz`

Checks:

- model configured
- runtime initialized or lazy-init possible
- storage access libraries available

Do not force full model reload on every readiness probe.

## Shared Implementation Order

1. define common request and response schemas
2. define shared error codes
3. implement shared artifact download/upload utilities
4. implement auth verification middleware
5. implement health endpoints
6. implement structured logging
7. implement one endpoint fully
8. reuse the foundation across all remaining endpoints

## Shared Efficiency Suggestion

Create a common inference SDK used by all Runpod services.

This SDK should provide:

- request validation
- signed URL download helpers
- image decode utilities
- output upload helpers
- standard response formatting
- error normalization
- timing instrumentation

This will significantly reduce duplicated logic and make all endpoints easier to maintain.
