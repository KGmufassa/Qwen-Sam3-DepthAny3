# Slice 5 Tickets

## Scope

Generate stitched-scene depth, normalize it across source images, and deliver the first real depth-informed parallax preview.

## Tickets

### S5-001: Add shared depth artifact, layer metric, and preview payload types

- Owner area: shared contracts
- Dependencies: Slice 4 complete
- Deliverable: typed contracts for depth outputs and preview payloads

### S5-002: Create Python depth worker package

- Owner area: worker
- Dependencies: Slice 4 complete
- Deliverable: runnable depth worker skeleton

### S5-003: Implement depth job orchestration

- Owner area: control plane
- Dependencies: S5-001
- Deliverable: `depth.generate` job creation and dispatch

### S5-004: Implement depth API and status API

- Owner area: control plane
- Dependencies: S5-003
- Deliverable: depth trigger and status endpoints

### S5-005: Implement depth worker stitched-scene consumption

- Owner area: worker
- Dependencies: S5-002
- Deliverable: worker loads stitched artifact and options

### S5-006: Implement depth runtime and output emission

- Owner area: worker
- Dependencies: S5-005
- Deliverable: canonical depth artifact, preview depth artifact, typed metadata

### S5-007: Register depth artifacts and bind normalized metrics to layers

- Owner area: control plane
- Dependencies: S5-006
- Deliverable: layer metrics plus default parallax values

### S5-008: Implement medium-selectable preview payload generation

- Owner area: control plane
- Dependencies: S5-007
- Deliverable: `GET /v1/scenes/{scene_id}/preview?medium=...`

### S5-009: Build real preview runtime with medium selector

- Owner area: frontend
- Dependencies: S5-008
- Deliverable: first real depth-informed parallax preview

### S5-010: Surface depth and default parallax summaries in inspector

- Owner area: frontend
- Dependencies: S5-007, S5-009
- Deliverable: visible layer depth/parallax information

### S5-011: Validate Slice 5 end-to-end

- Owner area: QA
- Dependencies: S5-003 through S5-010
- Deliverable: verified depth-to-preview product value
