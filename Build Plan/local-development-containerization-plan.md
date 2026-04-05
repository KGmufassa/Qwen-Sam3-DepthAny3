# Local Development Containerization Plan

## Goal

Set up the application for local development first, with a container strategy that:

- is easy to boot on one machine,
- preserves clean service boundaries,
- supports optional GPU workers,
- allows heavy services to be added incrementally,
- and stays structurally compatible with later production deployment.

## Core Principle

Containerize this system as a control plane plus isolated workers, not as one giant app image.

That means:

- the frontend runs separately,
- the API/control plane runs separately,
- storage and queue infrastructure run separately,
- each AI worker is isolated by responsibility,
- and optional heavy services can be omitted without breaking the base app.

## Local-First Objectives

- make the base stack easy to start,
- let developers work without requiring every model locally,
- allow GPU workers to be added only when needed,
- avoid rebuilding giant images for small code changes,
- keep model weights outside normal image builds.

## Phase 1 - Define The Local Service Set

### Required Day-1 Services

- `web`
- `api`
- `postgres`
- `redis`
- `minio`
- `worker-compose-export`

### Optional Local Services

- `worker-segmentation`
- `worker-depth`
- `worker-matting`
- `worker-layer-refine`

### Rule

The application must start and remain usable even when GPU workers are not running.

That means:

- unavailable workers disable specific features,
- they do not block the entire stack,
- and the frontend/API should degrade gracefully.

## Phase 2 - Freeze Service Boundaries

### `web`

- Next.js only
- no Python
- no model code
- talks only to API and SSE endpoints

### `api`

- FastAPI control plane
- owns project and scene CRUD
- owns upload finalization
- owns job creation and job status
- owns access to Postgres, Redis, and MinIO

### `worker-compose-export`

- CPU-only worker
- handles scene compilation, preview packaging, and export bundling
- used early to validate queue wiring without GPU complexity

### `worker-segmentation`

- runs SAM3 only
- accepts segmentation prompts
- returns masks, scores, and boxes

### `worker-depth`

- runs Depth Anything 3 only
- returns depth maps and layer depth metrics

### `worker-matting`

- dedicated edge and alpha refinement only
- supports the manual `Refine edges` toggle

### `worker-layer-refine`

- Qwen-only worker
- optional
- used for advanced difficult-case enhancement

### Rule

Keep one worker per model family.

Do not combine segmentation, depth, matting, and Qwen in one ML container.

## Phase 3 - Standardize Local Environment Variables

### Shared Variables

- `APP_ENV=development`
- `LOG_LEVEL=debug`
- `DATABASE_URL`
- `REDIS_URL`
- `S3_ENDPOINT`
- `S3_BUCKET`
- `S3_ACCESS_KEY_ID`
- `S3_SECRET_ACCESS_KEY`
- `S3_FORCE_PATH_STYLE=true`

### Frontend Variables

- `NEXT_PUBLIC_API_URL`
- `NEXT_PUBLIC_SSE_URL`

### Worker Variables

- `WORKER_QUEUE`
- `DEVICE=cpu|cuda`
- `MODEL_DIR=/models`
- `MAX_CONCURRENCY=1`

### Model Variables

- `SAM3_MODEL_ID`
- `DEPTH_MODEL_ID`
- `MATTING_MODEL_ID`
- `QWEN_MODEL_ID`

## Phase 4 - Define Local Volumes

### Required Volumes

- `postgres-data`
- `minio-data`
- `model-cache`

### Optional Volumes

- `redis-data`
- `worker-scratch`

### Rules

- model weights live outside the image in `/models`
- source bind mounts are separate from model cache volumes
- object storage is the long-term source of truth
- worker-local scratch space should be disposable

## Phase 5 - Compose File Layout

### Base Compose File

This file should always start the minimum useful local stack:

- `postgres`
- `redis`
- `minio`
- `api`
- `web`
- `worker-compose-export`

### Dev Override File

Use this for:

- source bind mounts
- hot reload
- local `.env`
- developer-friendly logging

### GPU Override File

Use this for:

- `worker-segmentation`
- `worker-depth`
- `worker-matting`

### Optional Qwen Override File

Use this only when needed:

- `worker-layer-refine`

### Rule

The local stack must be layered.

The base stack should always work without GPU services.

## Phase 6 - Containerize Infrastructure First

### Use Upstream Images

- `postgres`
- `redis`
- `minio`

### Tasks

1. Create service entries for the three infrastructure services.
2. Attach persistent volumes.
3. Expose local ports.
4. Add health checks.
5. Verify they can communicate on the local Docker network.

### Exit Criteria

- Postgres persists data
- Redis is reachable
- MinIO can store and retrieve a test object

## Phase 7 - Containerize The API

### Image Rules

- use a slim Python runtime
- keep it CPU-only
- do not include model code
- do not include CUDA libraries

### Responsibilities

- scene CRUD
- upload finalization
- signed storage URLs
- job creation
- job polling
- job cancellation

### Health Check Requirements

- DB reachable
- Redis reachable
- MinIO configuration valid

### Exit Criteria

- API boots in Docker
- API can connect to infra services
- API can create and read projects/scenes

## Phase 8 - Containerize The Web App

### Image Rules

- use a multi-stage build
- build Next.js in one stage
- run in a smaller Node runtime stage
- do not include Python or model code

### Responsibilities

- UI shell
- editor routes
- upload flow
- layer UI
- preview UI

### Rule

The web app should only need the API URL to boot.

It must not wait for GPU workers to be healthy.

### Exit Criteria

- web boots in Docker
- web talks to API
- base UI is accessible in browser

## Phase 9 - Containerize The Compose/Export Worker

### Why This Worker Comes First

It is CPU-only and validates the job system without adding GPU complexity.

### Responsibilities

- queue consumption
- scene compilation
- artifact packaging
- export bundle generation

### Exit Criteria

- worker can consume jobs from Redis-backed queue
- worker can read/write artifacts to MinIO
- worker can mark jobs complete or failed

## Phase 10 - Add GPU Workers One At A Time

### Rollout Order

1. `worker-segmentation`
2. `worker-depth`
3. `worker-matting`
4. `worker-layer-refine`

### Per-Worker Rules

- one image per worker
- one queue per worker type
- one model family per worker
- mount `/models`
- pin model IDs by environment variable

### Rule

Do not introduce Qwen until the base segmentation, depth, and matting path is stable.

## Phase 11 - Local CPU Fallback Policy

### Options

1. Real CPU inference for selected workers
2. Mock workers returning placeholder outputs
3. Remote GPU workers for real inference

### Recommended Local Policy

- allow CPU fallback only where acceptable,
- use mocks or remote GPU for the heaviest paths,
- keep Qwen off by default,
- keep the local app usable even without heavy inference.

## Phase 12 - Model Weight Strategy

### Rule

Do not bake large model weights into your normal Docker images.

### Local Strategy

- mount a named volume or bind mount at `/models`
- download weights there as needed
- share that location across relevant workers

### Benefits

- smaller images
- faster rebuilds
- easier model upgrades
- less duplication

### Failure Rule

Workers should fail clearly if required weights are missing.

They should not silently run in a broken state.

## Phase 13 - Health Checks

### `web`

- simple HTTP check

### `api`

- verify DB
- verify Redis
- verify MinIO config

### Workers

- process alive
- queue reachable
- model config present

### Rule

Do not make health checks reload the full model on every probe.

## Phase 14 - Startup Order

### Local Startup Order

1. `postgres`
2. `redis`
3. `minio`
4. `api`
5. `web`
6. `worker-compose-export`
7. `worker-segmentation`
8. `worker-depth`
9. `worker-matting`
10. `worker-layer-refine`

### Dependency Rules

- API waits on Postgres, Redis, and MinIO
- workers wait on Redis and MinIO
- web waits on API
- web must not wait on GPU workers

## Phase 15 - Local Developer Workflow

### Default Startup

Start only the base stack:

- `web`
- `api`
- `postgres`
- `redis`
- `minio`
- `worker-compose-export`

### Optional Startup Profiles

- add segmentation
- add depth
- add matting
- add Qwen

### Benefit

This keeps onboarding simple while still preserving the full architecture.

## Recommended Local Rollout

1. Run `postgres`, `redis`, and `minio`.
2. Run `api`.
3. Run `web`.
4. Run `worker-compose-export`.
5. Verify upload, scene creation, storage, and job creation.
6. Add `worker-segmentation`.
7. Add `worker-depth`.
8. Add `worker-matting`.
9. Add `worker-layer-refine` last.

## What Correct Containerization Means Here

- each service has one clear responsibility,
- images are small and purpose-specific,
- model weights are externalized,
- local dev works without the full GPU stack,
- queues are separated by worker type,
- storage and env conventions are standardized early,
- the same architecture can later move to Kubernetes.

## Recommended First Local Stack

### Always On

- `web`
- `api`
- `postgres`
- `redis`
- `minio`
- `worker-compose-export`

### Opt-In

- `worker-segmentation`
- `worker-depth`
- `worker-matting`
- `worker-layer-refine`

## Biggest Local-First Pitfalls

- trying to run every AI worker on day one,
- using one shared ML container,
- baking model weights into Docker images,
- making the frontend depend on GPU workers to start,
- not separating base compose from optional overlays.

## Final Recommendation

For local development first, build the containerization plan in layers:

1. infrastructure,
2. API,
3. web,
4. CPU export worker,
5. segmentation,
6. depth,
7. matting,
8. optional Qwen.

This gives you a stable local developer experience, preserves clean service boundaries, and keeps the path open for later GPU production deployment without forcing premature infrastructure complexity.
