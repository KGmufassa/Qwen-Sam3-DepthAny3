# Slice 1 Task List

## Goal

Upload multiple images and enter the editor with a mock stitched-scene shell backed by real persisted state.

## Workspace And Shared

- Create monorepo app/service package layout for:
  - `apps/web`
  - `apps/control-plane`
  - `workers/*`
  - `packages/shared-types`
- Add shared TypeScript types for:
  - `Project`
  - `StitchedScene`
  - `SourceImage`
  - `Artifact`
- Add environment configuration for:
  - Postgres
  - Redis
  - MinIO
- Create initial database schema/migrations for:
  - projects
  - stitched scenes
  - source images
  - artifacts

## Frontend

- Build project creation page/flow
- Build stitched scene creation flow
- Build multi-image uploader UI
- Build upload progress UI
- Build editor route and shell layout
- Build editor loading state
- Build empty-state shell for no layers yet
- Build status area showing mock/not-yet-processed state

## Control Plane

- Implement `POST /v1/projects`
- Implement `POST /v1/scenes`
- Implement `POST /v1/scenes/{scene_id}/uploads/init`
- Implement `POST /v1/scenes/{scene_id}/uploads/finalize`
- Implement `POST /v1/scenes/{scene_id}/mock-stitch`
- Implement `GET /v1/scenes/{scene_id}`
- Implement artifact registration service for:
  - source original
  - normalized placeholder
  - mock stitched artifact
- Persist uploaded source image metadata
- Persist stitched-scene shell state

## Worker

- No real worker required in Slice 1
- Add worker interface stubs for future slices

## Infrastructure

- Provision local Postgres
- Provision local Redis
- Provision local MinIO
- Wire web and control-plane services to local infra
- Add health endpoints for control plane

## QA And Verification

- Verify project creation works
- Verify stitched scene creation works
- Verify multiple uploads complete successfully
- Verify one failed upload does not invalidate successful uploads
- Verify mock stitched artifact is registered
- Verify editor shell loads from persisted scene state

## Exit Checklist

- Project and stitched scene persistence works
- Multi-image upload works
- Mock stitched-scene shell loads in editor
- Real persisted state, not local-only mocks, drives the flow
