# Slice 2 Tickets

## Scope

Replace mock stitched-scene generation with a real stitch/alignment pipeline and load the editor from a real stitched artifact.

## Tickets

### S2-001: Add shared stitch job/result contract types

- Owner area: shared contracts
- Dependencies: Slice 1 complete
- Deliverable: request/result/provenance types for stitch execution

### S2-002: Create Python stitch worker package

- Owner area: worker
- Dependencies: Slice 1 complete
- Deliverable: runnable stitch worker skeleton with config loading

### S2-003: Implement stitch job creation and queue dispatch

- Owner area: control plane
- Dependencies: S2-001
- Deliverable: `stitch.generate` job creation and Redis enqueue flow

### S2-004: Implement stitch start/status/retry APIs

- Owner area: control plane
- Dependencies: S2-003
- Deliverable: stitch start, stitch status, and retry endpoints

### S2-005: Implement stitch worker input fetch from MinIO

- Owner area: worker
- Dependencies: S2-002
- Deliverable: worker can load ordered normalized source images

### S2-006: Implement real stitch/alignment runtime integration

- Owner area: worker
- Dependencies: S2-005
- Deliverable: stitched output generation from uploaded source images

### S2-007: Emit stitched artifact and provenance metadata from worker

- Owner area: worker
- Dependencies: S2-006
- Deliverable: typed outputs for stitched artifact and placement/provenance data

### S2-008: Ingest stitch worker results and register stitched artifacts

- Owner area: control plane
- Dependencies: S2-007
- Deliverable: stitched artifact registration and scene state update

### S2-009: Persist source-to-stitched provenance metadata

- Owner area: control plane
- Dependencies: S2-008
- Deliverable: canonical provenance records attached to stitched scene state

### S2-010: Build stitch status and retry UI

- Owner area: frontend
- Dependencies: S2-004
- Deliverable: visible pending, failed, and retryable stitch state

### S2-011: Gate editor entry on real stitch readiness

- Owner area: frontend
- Dependencies: S2-008, S2-010
- Deliverable: editor loads only from real stitched-scene state

### S2-012: Validate Slice 2 end-to-end

- Owner area: QA
- Dependencies: S2-003 through S2-011
- Deliverable: verified real stitching flow with artifact registration and editor entry
