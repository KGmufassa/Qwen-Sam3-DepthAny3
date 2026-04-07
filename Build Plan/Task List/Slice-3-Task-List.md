# Slice 3 Task List

## Goal

Run real segmentation on the stitched scene and commit accepted masks into authoritative layer seeds.

## Workspace And Shared

- Add shared segmentation payload types
- Add candidate mask metadata types
- Add layer-seed state types

## Frontend

- Build segmentation request UI
- Build segmentation in-progress UI
- Build candidate review UI
- Build accept/reject candidate actions
- Show committed layer-seed state in editor

## Control Plane

- Implement `POST /v1/scenes/{scene_id}/segment/predict`
- Implement `POST /v1/scenes/{scene_id}/layers/commit-mask`
- Implement candidate metadata persistence
- Implement candidate mask artifact registration
- Create `segment.generate` jobs
- Bind accepted masks to committed layer seeds
- Keep rejected/unaccepted masks non-authoritative

## Worker

- Implement Python segmentation worker
- Load stitched-scene artifact from MinIO
- Execute segmentation runtime with prompt inputs
- Emit mask artifacts and optional previews
- Return candidate metadata

## Infrastructure

- Add segmentation worker service config
- Add segmentation queue
- Add segmentation worker readiness checks

## QA And Verification

- Verify segmentation runs on real stitched scenes
- Verify candidate masks are returned
- Verify accepted masks commit correctly
- Verify rejected masks do not become seeds
- Verify failure and retry states are visible

## Exit Checklist

- Segmentation works against stitched scenes
- Committed layer seeds exist in authoritative scene state
- Candidate and committed states are cleanly separated
