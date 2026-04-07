# Slice 2 Task List

## Goal

Replace mock stitched-scene generation with a real stitch/alignment pipeline and load the editor from a real stitched artifact.

## Workspace And Shared

- Add Python worker package for stitch/alignment
- Add shared stitch job/result payload definitions
- Add stitched provenance types

## Frontend

- Add stitch status UI
- Add stitch pending state
- Add stitch failed state
- Add stitch retry action
- Gate editor entry on real stitch readiness

## Control Plane

- Implement `POST /v1/scenes/{scene_id}/stitch/start`
- Implement `GET /v1/scenes/{scene_id}/stitch/status`
- Implement `GET /v1/jobs/{job_id}`
- Implement `POST /v1/jobs/{job_id}/retry`
- Add `stitch.generate` job creation
- Add Redis enqueue for stitch jobs
- Add stitch result ingestion handler
- Register stitched artifact and stitched preview artifact
- Persist source-to-stitched provenance metadata
- Update scene status transitions for stitch lifecycle

## Worker

- Implement Python stitch worker skeleton
- Implement input artifact fetch from MinIO
- Implement ordered image ingestion
- Implement stitch/alignment runtime call
- Emit stitched output to MinIO
- Return typed artifact metadata and placement/provenance data
- Return typed errors and warnings

## Infrastructure

- Add stitch worker service config
- Add Redis queue binding for stitch jobs
- Add MinIO credentials/config to stitch worker
- Add worker readiness checks

## QA And Verification

- Verify stitch job creation works
- Verify stitch worker consumes job correctly
- Verify stitched artifact is created and registered
- Verify editor loads from real stitched output
- Verify failed stitch leaves source image state intact
- Verify retry works after failure

## Exit Checklist

- Mock stitch is no longer required for baseline flow
- Real stitched artifact exists and is authoritative
- Scene readiness tracks stitch status correctly
