# Slice 9 Tickets

## Scope

Add optional difficult-layer enhancement workflows without destabilizing the baseline MVP path.

## Tickets

### S9-001: Add shared alternate-version and refinement result types

- Owner area: shared contracts
- Dependencies: Slice 8 complete
- Deliverable: typed contracts for matte and Qwen refine outputs

### S9-002: Create Python matting worker package

- Owner area: worker
- Dependencies: Slice 8 complete
- Deliverable: runnable matting worker skeleton

### S9-003: Create optional Python Qwen refine worker package

- Owner area: worker
- Dependencies: Slice 8 complete
- Deliverable: runnable refine worker skeleton

### S9-004: Implement matte/refine job orchestration

- Owner area: control plane
- Dependencies: S9-001
- Deliverable: job creation and dispatch for matte and refine paths

### S9-005: Implement alternate layer version registration

- Owner area: control plane
- Dependencies: S9-004
- Deliverable: refined outputs stored as alternate versions, not automatic replacements

### S9-006: Implement active version switching and revert-to-base mutation

- Owner area: control plane
- Dependencies: S9-005
- Deliverable: explicit version activation model

### S9-007: Build refine-edge, enhance-layer, and version-switch UI

- Owner area: frontend
- Dependencies: S9-005, S9-006
- Deliverable: optional enhancement actions and version control UI

### S9-008: Add matting and refine worker infrastructure wiring

- Owner area: infrastructure
- Dependencies: S9-002, S9-003
- Deliverable: queues, worker configs, MinIO access, readiness checks

### S9-009: Validate Slice 9 end-to-end

- Owner area: QA
- Dependencies: S9-004 through S9-008
- Deliverable: verified optional enhancement flow with safe fallback to base versions
