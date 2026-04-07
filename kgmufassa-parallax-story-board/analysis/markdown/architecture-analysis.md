# Architecture Analysis: kgmufassa-parallax-story-board

## Overview
- Focus: Full Repository Overview
- Mode: Deep
- Foundation source: `./kgmufassa-parallax-story-board/analysis/json/Analyze-Repo-Foundation.json`

## Layers
- `app_routes`: 30 files
- `config`: 2 files
- `core`: 8 files
- `data`: 2 files
- `docs`: 21 files
- `feature_ui`: 16 files
- `infrastructure`: 4 files
- `interfaces`: 12 files
- `modules`: 45 files
- `other`: 42 files
- `tests`: 16 files

## Dominant Layer Flows
- `modules` -> `modules`: 60 relationships
- `interfaces` -> `modules`: 25 relationships
- `app_routes` -> `core`: 21 relationships
- `feature_ui` -> `feature_ui`: 21 relationships
- `app_routes` -> `interfaces`: 20 relationships
- `modules` -> `core`: 17 relationships
- `interfaces` -> `core`: 16 relationships
- `modules` -> `config`: 14 relationships
- `tests` -> `modules`: 14 relationships
- `app_routes` -> `infrastructure`: 13 relationships
- `interfaces` -> `interfaces`: 11 relationships
- `interfaces` -> `other`: 10 relationships
- `app_routes` -> `feature_ui`: 8 relationships
- `tests` -> `config`: 8 relationships
- `core` -> `core`: 6 relationships
- `modules` -> `infrastructure`: 6 relationships
- `interfaces` -> `config`: 5 relationships
- `infrastructure` -> `modules`: 4 relationships
- `app_routes` -> `modules`: 3 relationships
- `infrastructure` -> `core`: 3 relationships

## Architectural Patterns
- Request handling appears to flow from Next.js route files into controller files and then into module services, matching a layered application design.
- UI concerns are separated into `src/features/**`, while reusable business logic lives in `src/modules/**`, reducing coupling between presentation and domain logic.
- Persistence and provider integrations are isolated under infrastructure and Prisma layers, suggesting deliberate boundaries around external systems.
- The versioned API surface under `src/app/api/v1/**` indicates an intentional external contract rather than ad hoc route growth.

## Module Architecture
- `assets`: 5 files; services=1; repositories=0; cross-module deps=scenes (1), decomposition (1)
- `auth`: 5 files; services=1; repositories=1; cross-module deps=none detected
- `authorization`: 3 files; services=1; repositories=0; cross-module deps=none detected
- `decomposition`: 3 files; services=1; repositories=0; cross-module deps=assets (1), feature-flags (1), motion (1), playback (1), scenes (1)
- `feature-flags`: 2 files; services=1; repositories=0; cross-module deps=none detected
- `guest-sessions`: 4 files; services=1; repositories=1; cross-module deps=none detected
- `maintenance`: 2 files; services=1; repositories=0; cross-module deps=scenes (2), projects (1)
- `motion`: 3 files; services=1; repositories=0; cross-module deps=scenes (3)
- `playback`: 2 files; services=1; repositories=0; cross-module deps=feature-flags (1), projects (1), scenes (1)
- `processing`: 2 files; services=1; repositories=0; cross-module deps=feature-flags (1), scenes (1)
- `projects`: 5 files; services=1; repositories=1; cross-module deps=none detected
- `scenes`: 5 files; services=1; repositories=1; cross-module deps=none detected
- `uploads`: 4 files; services=1; repositories=0; cross-module deps=none detected

## Critical Flows
- Authentication flow: Auth requests enter through NextAuth routes, rely on auth setup, and likely resolve users through the auth repository and Prisma client.
  Path: src/app/api/auth/[...nextauth]/route.ts -> src/auth.ts -> src/modules/auth/repository.ts -> src/infrastructure/db/prisma.ts
- Project management flow: Project CRUD and orchestration likely move from API route to controller, through project service logic, into repository-backed persistence.
  Path: src/app/api/v1/projects/route.ts -> src/interfaces/http/controllers/project-controller.ts -> src/modules/projects/service.ts -> src/modules/projects/repository.ts -> src/infrastructure/db/prisma.ts
- Scene processing flow: Scene regeneration appears to combine scene orchestration, processing logic, and Qwen provider integration.
  Path: src/app/api/v1/scenes/[sceneId]/regenerate/route.ts -> src/interfaces/http/controllers/scene-controller.ts -> src/modules/scenes/service.ts -> src/modules/processing/service.ts -> src/infrastructure/providers/qwen/client.ts
- Preview playback flow: The preview UI likely requests playback data from the API, which is then composed by preview and playback services.
  Path: src/app/projects/[projectId]/preview/page.tsx -> src/features/preview/components/project-preview-page.tsx -> src/features/preview/lib/playback-client.ts -> src/app/api/v1/projects/[projectId]/preview/playback/route.ts -> src/interfaces/http/controllers/preview-controller.ts -> src/modules/playback/service.ts

## Dependency Hubs
- `src/config/env.ts` - layer=config, type=source-file, incoming=26, outgoing=0
- `src/core/http/route-handler.ts` - layer=core, type=source-file, incoming=20, outgoing=3
- `src/core/errors/app-error.ts` - layer=core, type=source-file, incoming=18, outgoing=0
- `src/interfaces/http/controllers/scene-controller.ts` - layer=interfaces, type=controller, incoming=4, outgoing=13
- `src/infrastructure/rate-limit/memory-rate-limiter.ts` - layer=infrastructure, type=source-file, incoming=13, outgoing=2
- `src/interfaces/http/controllers/project-controller.ts` - layer=interfaces, type=controller, incoming=4, outgoing=10
- `src/modules/scenes/index.ts` - layer=modules, type=module-index, incoming=9, outgoing=3
- `src/modules/assets/index.ts` - layer=modules, type=module-index, incoming=7, outgoing=4
- `src/modules/decomposition/service.ts` - layer=modules, type=service, incoming=1, outgoing=10
- `src/core/request/context.ts` - layer=core, type=source-file, incoming=10, outgoing=0
- `src/interfaces/http/controllers/auth-controller.ts` - layer=interfaces, type=controller, incoming=2, outgoing=8
- `src/lib/api-response.ts` - layer=other, type=source-file, incoming=9, outgoing=0
- `src/interfaces/http/controllers/preview-controller.ts` - layer=interfaces, type=controller, incoming=2, outgoing=7
- `src/features/shared/components/app-header.tsx` - layer=feature_ui, type=component, incoming=7, outgoing=1
- `src/interfaces/http/support/request-actor.ts` - layer=interfaces, type=source-file, incoming=4, outgoing=4
- `src/interfaces/http/controllers/health-controller.ts` - layer=interfaces, type=controller, incoming=2, outgoing=6
- `src/modules/maintenance/service.ts` - layer=modules, type=service, incoming=2, outgoing=6
- `src/interfaces/http/controllers/upload-controller.ts` - layer=interfaces, type=controller, incoming=1, outgoing=7
- `src/modules/playback/service.ts` - layer=modules, type=service, incoming=1, outgoing=7
- `src/config/constants.ts` - layer=config, type=source-file, incoming=7, outgoing=0

## Risks And Unknowns
- 17 local imports could not be resolved from the markdown snapshot.
- Several modules do not expose an obvious repository file, so persistence responsibilities may be unevenly distributed.

