# Slice 5 Task List

## Goal

Generate stitched-scene depth, normalize it across source images, and deliver the first real depth-informed parallax preview.

## Workspace And Shared

- Add depth artifact shared types
- Add layer depth metric types
- Add preview payload types with default parallax state

## Frontend

- Build depth generation trigger or auto-start flow
- Build depth status UI
- Build preview mode using real payload
- Build medium selector UI:
  - phone
  - tablet
  - desktop
- Show depth/parallax summaries in inspector

## Control Plane

- Implement `POST /v1/scenes/{scene_id}/depth`
- Implement `GET /v1/scenes/{scene_id}/depth/status`
- Implement preview payload generation with medium selection
- Create `depth.generate` jobs
- Register canonical depth and preview depth artifacts
- Bind normalized depth metrics to layers
- Derive default parallax behavior from depth

## Worker

- Implement Python depth worker
- Load stitched-scene artifact
- Run depth model
- Emit canonical depth artifact
- Emit preview depth artifact
- Return typed metadata for aggregation

## Infrastructure

- Add depth queue
- Add depth worker service config
- Add worker readiness checks for model availability

## QA And Verification

- Verify depth runs on real stitched scenes
- Verify canonical and preview depth artifacts are registered
- Verify layer depth metrics exist
- Verify preview shows visible motion differences
- Verify medium switching works without rerunning heavy jobs

## Exit Checklist

- Depth-informed preview exists
- Cross-image depth normalization works
- The first real parallax product value is visible
