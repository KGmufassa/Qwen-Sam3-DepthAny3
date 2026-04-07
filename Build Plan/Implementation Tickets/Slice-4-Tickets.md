# Slice 4 Tickets

## Scope

Turn committed layer seeds into real editable layers with active versions and thumbnails.

## Tickets

### S4-001: Add shared layer version and extraction artifact types

- Owner area: shared contracts
- Dependencies: Slice 3 complete
- Deliverable: typed layer version and extraction output contracts

### S4-002: Create extraction worker or service package

- Owner area: worker
- Dependencies: Slice 3 complete
- Deliverable: extraction execution service skeleton

### S4-003: Implement extraction job orchestration

- Owner area: control plane
- Dependencies: S4-001
- Deliverable: `extract.layer` job creation and dispatch

### S4-004: Implement extraction API

- Owner area: control plane
- Dependencies: S4-003
- Deliverable: `POST /v1/scenes/{scene_id}/layers/extract`

### S4-005: Implement extraction runtime over stitched-scene artifact and masks

- Owner area: worker
- Dependencies: S4-002
- Deliverable: RGBA/alpha/thumbnail outputs for committed seeds

### S4-006: Register extracted artifacts and create base layer versions

- Owner area: control plane
- Dependencies: S4-005
- Deliverable: RGBA/alpha/thumbnail artifacts registered with base `LayerVersion`

### S4-007: Assign active layer version and finalize real layer records

- Owner area: control plane
- Dependencies: S4-006
- Deliverable: real editable layers with active versions

### S4-008: Build real layer list UI from persisted extracted layers

- Owner area: frontend
- Dependencies: S4-007
- Deliverable: layer panel with real layers, active-version indicators, names, visibility, and order

### S4-009: Build real layer inspector shell and group assignment entry points

- Owner area: frontend
- Dependencies: S4-008
- Deliverable: inspector behavior against real extracted layers

### S4-010: Validate Slice 4 end-to-end

- Owner area: QA
- Dependencies: S4-003 through S4-009
- Deliverable: verified extraction-to-editable-layers flow
