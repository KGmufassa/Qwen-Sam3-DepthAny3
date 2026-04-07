# Slice 1 Tickets

## Scope

Upload multiple images and enter the editor with a mock stitched-scene shell backed by real persisted state.

## Tickets

### S1-001: Create monorepo workspace skeleton

- Owner area: workspace
- Dependencies: none
- Deliverable: package structure for web app, control plane, workers, and shared contracts

### S1-002: Add shared core types for project, stitched scene, source image, and artifact

- Owner area: shared contracts
- Dependencies: S1-001
- Deliverable: shared types package with baseline entity definitions used by web and control plane

### S1-003: Provision local development infrastructure

- Owner area: infrastructure
- Dependencies: none
- Deliverable: Postgres, Redis, and MinIO available locally with environment wiring

### S1-004: Implement initial database schema and migrations for project/scene/source image/artifact

- Owner area: control plane
- Dependencies: S1-001, S1-002, S1-003
- Deliverable: working persistence model for Slice 1 entities

### S1-005: Build project creation API

- Owner area: control plane
- Dependencies: S1-004
- Deliverable: `POST /v1/projects`

### S1-006: Build stitched scene creation API

- Owner area: control plane
- Dependencies: S1-004, S1-005
- Deliverable: `POST /v1/scenes`

### S1-007: Build upload init/finalize APIs for multiple source images

- Owner area: control plane
- Dependencies: S1-004, S1-006
- Deliverable: upload init and finalize endpoints with source image registration

### S1-008: Implement artifact registration service for source originals and mock stitched artifact

- Owner area: control plane
- Dependencies: S1-004, S1-007
- Deliverable: reusable artifact registration path for Slice 1 files

### S1-009: Implement mock stitched-scene creation path

- Owner area: control plane
- Dependencies: S1-008
- Deliverable: mock stitched artifact and scene-ready shell state

### S1-010: Implement scene fetch API for editor load

- Owner area: control plane
- Dependencies: S1-006, S1-009
- Deliverable: `GET /v1/scenes/{scene_id}` returning editor-ready shell payload

### S1-011: Build project creation UI flow

- Owner area: frontend
- Dependencies: S1-005
- Deliverable: project creation screen/flow

### S1-012: Build stitched scene creation UI flow

- Owner area: frontend
- Dependencies: S1-006, S1-011
- Deliverable: scene creation entry flow after project creation

### S1-013: Build multi-image upload UI with progress

- Owner area: frontend
- Dependencies: S1-007, S1-012
- Deliverable: multi-file upload experience and status feedback

### S1-014: Build editor shell route and layout

- Owner area: frontend
- Dependencies: S1-010
- Deliverable: scene canvas shell, layer/group shell, inspector shell, preview control shell, status area

### S1-015: Build editor loading and empty-state UX

- Owner area: frontend
- Dependencies: S1-014
- Deliverable: clear shell behavior before real layers exist

### S1-016: Add control-plane health endpoints

- Owner area: control plane
- Dependencies: S1-003
- Deliverable: readiness/liveness endpoints checking database, Redis, and MinIO connectivity

### S1-017: Validate end-to-end Slice 1 flow

- Owner area: QA
- Dependencies: S1-005 through S1-015
- Deliverable: verified flow from project create to editor shell with persisted mock stitched-scene state
