# Slice 3 Tickets

## Scope

Run real segmentation on the stitched scene and commit accepted masks into authoritative layer seeds.

## Tickets

### S3-001: Add shared segmentation and candidate mask contract types

- Owner area: shared contracts
- Dependencies: Slice 2 complete
- Deliverable: typed contracts for segmentation request, candidate metadata, and committed seeds

### S3-002: Create Python segmentation worker package

- Owner area: worker
- Dependencies: Slice 2 complete
- Deliverable: runnable segmentation worker skeleton

### S3-003: Implement segmentation request/job orchestration

- Owner area: control plane
- Dependencies: S3-001
- Deliverable: `segment.generate` job creation and dispatch

### S3-004: Implement segmentation predict API

- Owner area: control plane
- Dependencies: S3-003
- Deliverable: `POST /v1/scenes/{scene_id}/segment/predict`

### S3-005: Implement segmentation worker stitched-input consumption

- Owner area: worker
- Dependencies: S3-002
- Deliverable: worker loads stitched scene artifact and prompt inputs

### S3-006: Implement segmentation runtime and candidate generation

- Owner area: worker
- Dependencies: S3-005
- Deliverable: candidate mask outputs and metadata

### S3-007: Register candidate mask artifacts and metadata

- Owner area: control plane
- Dependencies: S3-006
- Deliverable: candidate artifacts registered as non-authoritative outputs

### S3-008: Implement commit-mask API and layer seed creation

- Owner area: control plane
- Dependencies: S3-007
- Deliverable: accepted masks become committed layer seeds

### S3-009: Build candidate review and accept/reject UI

- Owner area: frontend
- Dependencies: S3-004, S3-007
- Deliverable: segmentation result review flow in editor

### S3-010: Surface committed seeds in editor state

- Owner area: frontend
- Dependencies: S3-008
- Deliverable: committed seeds visible as pre-extraction scene units

### S3-011: Validate Slice 3 end-to-end

- Owner area: QA
- Dependencies: S3-003 through S3-010
- Deliverable: verified segmentation-to-seed commit flow
