# Slice 4 Task List

## Goal

Turn committed layer seeds into real editable layers with active versions and thumbnails.

## Workspace And Shared

- Add `Layer` and `LayerVersion` shared contract types
- Add extraction output artifact types
- Add thumbnail artifact types

## Frontend

- Populate layer panel from real extracted layers
- Add active version indicator in layer UI
- Add real layer selection flow
- Add name/visibility/order editing against persisted layers
- Add baseline group assignment UI against real layers

## Control Plane

- Implement `POST /v1/scenes/{scene_id}/layers/extract`
- Implement `PATCH /v1/layers/{layer_id}`
- Implement extraction job orchestration
- Create `extract.layer` jobs
- Persist base layer records and version records
- Register RGBA, alpha, and thumbnail artifacts
- Assign active version on successful extraction

## Worker

- Implement extraction worker or extraction stage service
- Consume stitched-scene artifact and committed masks
- Produce RGBA crops
- Produce alpha outputs when applicable
- Produce thumbnails
- Return typed output metadata

## Infrastructure

- Add extraction queue binding
- Add extraction service credentials for MinIO

## QA And Verification

- Verify committed seeds become extracted layers
- Verify RGBA and thumbnail artifacts are registered
- Verify active version is set correctly
- Verify one failed extraction does not break unrelated layers
- Verify editor loads real layers correctly

## Exit Checklist

- Real extracted layers exist
- Active versions exist
- Editor is meaningfully usable against real layer assets
