# Slice 7 Task List

## Goal

Generate and register export bundles that preserve the accepted stitched-scene semantics and active artifacts.

## Workspace And Shared

- Add export record shared types
- Add export manifest payload type
- Add export bundle metadata type

## Frontend

- Build export trigger UI
- Build export readiness UI
- Build export pending/success/failure UI
- Build export retrieval/download UI

## Control Plane

- Implement `POST /v1/scenes/{scene_id}/export`
- Implement `GET /v1/scenes/{scene_id}/exports`
- Implement `GET /v1/exports/{export_id}`
- Create `export.bundle` jobs
- Serialize saved scene graph into export manifest payload
- Register export bundle artifact
- Register export manifest artifact
- Persist export records

## Worker

- Implement Python compose/export worker
- Consume explicit export payload
- Package active assets and runtime manifest
- Emit bundle artifact and manifest metadata

## Infrastructure

- Add export queue
- Add compose/export worker service config
- Ensure MinIO paths and bundle outputs are accessible for retrieval

## QA And Verification

- Verify export can be triggered from saved scene state
- Verify export bundle and manifest are generated
- Verify active layer versions are respected
- Verify group and responsive behavior are preserved
- Verify export failure is visible and retryable

## Exit Checklist

- Export exists as a real user-facing capability
- Exported output matches scene semantics
- MVP becomes feature-complete at the product level
