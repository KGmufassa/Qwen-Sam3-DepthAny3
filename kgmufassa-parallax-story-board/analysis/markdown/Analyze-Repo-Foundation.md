# Analyze Repo Foundation: kgmufassa-parallax-story-board

## Overview
- Focus: Full Repository Overview
- Total files: 198
- Entry points: 38
- Relationships: 300
- Summary: This repository appears to be a Next.js parallax story composition platform with a layered backend, Prisma-backed persistence, and feature-oriented UI plus API workflows for projects, scenes, uploads, preview, and authentication.

## Repository Shape
- `AGENTS.md`: 1 files
- `docs`: 21 files
- `env.example`: 1 files
- `eslint.config.mjs`: 1 files
- `next-env.d.ts`: 1 files
- `next.config.ts`: 1 files
- `opencode`: 29 files
- `package.json`: 1 files
- `prisma`: 2 files
- `public`: 1 files
- `scripts`: 1 files
- `src`: 120 files
- `tests`: 16 files
- `tsconfig.json`: 1 files
- `vitest.config.ts`: 1 files

## Major Categories
- API routes: 21
- Controllers: 8
- Services: 13
- Repositories: 4
- Components: 14
- Documentation files: 33

## Modules
- `assets`: 5 files
- `auth`: 5 files
- `authorization`: 3 files
- `decomposition`: 3 files
- `feature-flags`: 2 files
- `guest-sessions`: 4 files
- `maintenance`: 2 files
- `motion`: 3 files
- `playback`: 2 files
- `processing`: 2 files
- `projects`: 5 files
- `scenes`: 5 files
- `uploads`: 4 files

## Features
- `auth`: 1 files
- `marketing`: 1 files
- `preview`: 3 files
- `projects`: 6 files
- `scenes`: 1 files
- `settings`: 1 files
- `shared`: 2 files
- `uploads`: 1 files

## Entry Points
- `next.config.ts` - project/bootstrap config
- `package.json` - project/bootstrap config
- `scripts/dev-with-chunk-sync.mjs` - script entry
- `src/app/layout.tsx` - global layout shell
- `src/app/page.tsx` - root app route
- `src/app/api/auth/[...nextauth]/route.ts` - API route handler
- `src/app/api/v1/assets/[...assetPath]/route.ts` - API route handler
- `src/app/api/v1/auth/register/route.ts` - API route handler
- `src/app/api/v1/auth/session/route.ts` - API route handler
- `src/app/api/v1/guest-sessions/route.ts` - API route handler
- `src/app/api/v1/health/live/route.ts` - API route handler
- `src/app/api/v1/health/ready/route.ts` - API route handler
- `src/app/api/v1/internal/maintenance/cleanup/route.ts` - API route handler
- `src/app/api/v1/internal/maintenance/recover-timeouts/route.ts` - API route handler
- `src/app/api/v1/projects/route.ts` - API route handler
- `src/app/api/v1/projects/[projectId]/route.ts` - API route handler
- `src/app/api/v1/projects/[projectId]/claim/route.ts` - API route handler
- `src/app/api/v1/projects/[projectId]/preview/playback/route.ts` - API route handler
- `src/app/api/v1/projects/[projectId]/preview/status/route.ts` - API route handler
- `src/app/api/v1/projects/[projectId]/scenes/reorder/route.ts` - API route handler
- `src/app/api/v1/projects/[projectId]/uploads/finalize/route.ts` - API route handler
- `src/app/api/v1/projects/[projectId]/uploads/init/route.ts` - API route handler
- `src/app/api/v1/scenes/[sceneId]/route.ts` - API route handler
- `src/app/api/v1/scenes/[sceneId]/regenerate/route.ts` - API route handler
- `src/app/api/v1/scenes/[sceneId]/retry/route.ts` - API route handler
- `src/app/api/v1/uploads/[uploadToken]/route.ts` - API route handler
- `src/modules/assets/index.ts` - module index
- `src/modules/auth/index.ts` - module index
- `src/modules/authorization/index.ts` - module index
- `src/modules/feature-flags/index.ts` - module index
- `src/modules/guest-sessions/index.ts` - module index
- `src/modules/maintenance/index.ts` - module index
- `src/modules/motion/index.ts` - module index
- `src/modules/playback/index.ts` - module index
- `src/modules/processing/index.ts` - module index
- `src/modules/projects/index.ts` - module index
- `src/modules/scenes/index.ts` - module index
- `src/modules/uploads/index.ts` - module index

## Known Issues
- 17 local imports could not be resolved from the markdown snapshot.

