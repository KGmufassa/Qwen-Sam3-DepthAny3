# Slice 8 Tickets

## Scope

Harden the baseline MVP path for release through retries, timeouts, degraded capability handling, and partial-completion support.

## Tickets

### S8-001: Add shared retry, timeout, and degraded-state contract helpers

- Owner area: shared contracts
- Dependencies: Slice 7 complete
- Deliverable: normalized error/status models for recovery handling

### S8-002: Implement retry orchestration for major job families

- Owner area: control plane
- Dependencies: S8-001
- Deliverable: retry behavior for stitch, segmentation, extraction, depth, and export

### S8-003: Implement timeout state transitions and timeout-safe job handling

- Owner area: control plane
- Dependencies: S8-001
- Deliverable: visible timeout states instead of indefinite pending states

### S8-004: Implement late-result and partial-artifact protection

- Owner area: control plane
- Dependencies: S8-002, S8-003
- Deliverable: no stale/partial outputs silently become authoritative

### S8-005: Build stage-specific failure and retry UX

- Owner area: frontend
- Dependencies: S8-002, S8-003
- Deliverable: visible errors and retry paths by stage

### S8-006: Build degraded capability UX for unavailable workers

- Owner area: frontend
- Dependencies: S8-001
- Deliverable: capability-specific unavailable messaging while preserving usable editor features

### S8-007: Add worker readiness and queue timeout monitoring

- Owner area: infrastructure
- Dependencies: prior worker slices complete
- Deliverable: readiness checks and timeout observability across worker families

### S8-008: Validate Slice 8 end-to-end

- Owner area: QA
- Dependencies: S8-002 through S8-007
- Deliverable: verified recovery, retry, timeout, and degraded capability behavior
