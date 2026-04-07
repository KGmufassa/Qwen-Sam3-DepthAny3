# Slice 7 Tickets

## Scope

Generate and register export bundles that preserve the accepted stitched-scene semantics and active artifacts.

## Tickets

### S7-001: Add shared export record and export manifest types

- Owner area: shared contracts
- Dependencies: Slice 6 complete
- Deliverable: typed export contracts

### S7-002: Create Python compose/export worker package

- Owner area: worker
- Dependencies: Slice 6 complete
- Deliverable: runnable export worker skeleton

### S7-003: Implement export job orchestration

- Owner area: control plane
- Dependencies: S7-001
- Deliverable: `export.bundle` job creation and dispatch

### S7-004: Implement export trigger/list/retrieve APIs

- Owner area: control plane
- Dependencies: S7-003
- Deliverable: export endpoints and record retrieval

### S7-005: Serialize saved stitched-scene graph into export manifest input

- Owner area: control plane
- Dependencies: S7-003
- Deliverable: explicit export payload with scene semantics

### S7-006: Implement export worker bundle generation

- Owner area: worker
- Dependencies: S7-002, S7-005
- Deliverable: package active assets and manifest into export bundle

### S7-007: Register export bundle and manifest artifacts

- Owner area: control plane
- Dependencies: S7-006
- Deliverable: export artifacts and export records persisted

### S7-008: Build export UX in editor

- Owner area: frontend
- Dependencies: S7-004, S7-007
- Deliverable: export trigger, status, and retrieval UI

### S7-009: Validate Slice 7 end-to-end

- Owner area: QA
- Dependencies: S7-003 through S7-008
- Deliverable: verified export parity with stitched-scene semantics
