# Deployment And Infrastructure Plan

## Document Purpose

This document defines the MVP deployment and infrastructure shape for the stitched-scene platform.

It focuses on:

- control plane deployment
- storage and queue infrastructure
- worker deployment model
- local versus remote execution
- health and readiness expectations
- minimum viable operational topology

---

## Infrastructure Principles

- the control plane is separate from ML workers
- storage and queue infrastructure are first-class system dependencies
- workers are isolated by responsibility
- the app must remain structurally compatible with both local development and production deployment
- the product must not require every worker to run inside one monolith

---

## MVP Infrastructure Topology

The MVP should be built around these infrastructure roles:

- web application
- API/control plane
- database
- object storage
- queue
- stitch worker
- segmentation worker
- depth worker
- matting worker
- optional layer-refine worker
- compose/export worker

---

## Control Plane

### Web application

Responsibilities:

- user-facing routes
- editor UI
- preview UI
- status visualization

### API/control plane

Responsibilities:

- state mutation
- job creation
- job status
- artifact registration
- export orchestration

The API/control plane must be deployable independently from GPU workers.

---

## Data Infrastructure

### Database

Minimum role:

- persistent scene graph storage
- job records
- artifact records
- export records

### Object storage

Minimum role:

- source images
- normalized images
- stitched scene outputs
- masks
- layer assets
- depth outputs
- export bundles

### Queue

Minimum role:

- async dispatch for all heavy stages
- retry support
- worker separation by job type

---

## Worker Deployment Model

Workers should be deployed as isolated services by family.

### Required worker families

- `worker-stitch`
- `worker-segmentation`
- `worker-depth`
- `worker-matting`
- `worker-layer-refine`
- `worker-compose-export`

The optional refine worker is not required to be active for baseline MVP functionality.

---

## Queue Topology

Recommended MVP posture:

- one queue or queue class per worker family
- control plane dispatches work by job type
- workers consume only their assigned job family

This keeps runtime boundaries simple and prevents model-family coupling.

---

## Local Development Topology

The MVP local environment should support:

- running web and control plane locally
- running infrastructure services locally
- using mock workers where needed
- using remote GPU workers where local GPU is unavailable

Recommended local-first posture:

- local database
- local object storage or compatible dev storage
- local queue
- local CPU export worker
- optional local or remote ML workers

The editor must remain usable even when some GPU workers are not available.

---

## Production-Oriented Topology

The MVP should remain deployable using a modest production-like split:

- web application
- API/control plane
- persistent database
- persistent object storage
- durable queue
- remote or dedicated workers by family

This does not require Kubernetes in MVP.

The plan should preserve a path to:

- remote GPU services
- worker autoscaling later
- stronger operational isolation later

---

## Worker Availability Model

The product should be able to degrade by capability.

Examples:

- if depth worker is unavailable, depth generation is disabled but scene editing remains available
- if refine worker is unavailable, baseline scene editing remains available
- if compose/export worker is unavailable, export is unavailable but scene editing remains available

The web application must not depend on all workers being healthy to start.

---

## Health And Readiness

### Control plane readiness should verify

- database connectivity
- storage connectivity
- queue connectivity

### Worker readiness should verify

- worker can reach queue
- worker can reach storage
- worker has required model/runtime readiness

Readiness should be more than “process is alive.”

---

## Secrets And Configuration

The MVP deployment must support explicit configuration for:

- database connection
- storage credentials
- queue credentials
- worker endpoints
- model/runtime configuration
- artifact paths

Secrets should not be hardcoded into the application or worker images.

---

## Storage Layout Guidance

Artifact storage should use stable, scene-linked paths.

Conceptual organization:

- source images
- stitched scene outputs
- masks
- extracted layers
- depth outputs
- exports

Storage layout should remain traceable to:

- project
- scene
- pipeline run
- stage

---

## Deployment Ordering

Minimum recommended deployment order:

1. database
2. object storage
3. queue
4. API/control plane
5. web application
6. compose/export worker
7. stitch worker
8. segmentation worker
9. depth worker
10. matting worker
11. optional refine worker

This order keeps the baseline product path stable while enabling workers incrementally.

---

## Infrastructure Out-Of-Scope

The MVP does not require:

- full autoscaling platform maturity
- Kubernetes-first deployment
- multi-region deployment
- advanced GPU fleet scheduling

---

## Freeze Criteria

This plan is ready to freeze when:

- control plane split is accepted
- infrastructure roles are accepted
- worker deployment model is accepted
- local versus remote worker posture is accepted
- readiness expectations are accepted

---

## Final Infrastructure Statement

The MVP deployment model uses a separated web and control plane, persistent data infrastructure, and isolated worker families for stitching, segmentation, depth, matting, optional refinement, and export so that the product remains operable even when some specialized capabilities are unavailable.
