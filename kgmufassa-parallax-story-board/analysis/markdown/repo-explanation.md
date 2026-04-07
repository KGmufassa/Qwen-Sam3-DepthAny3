# Repo Explanation: kgmufassa-parallax-story-board

## What This Repo Appears To Do
- This repository appears to be a Next.js parallax story composition platform with a layered backend, Prisma-backed persistence, and feature-oriented UI plus API workflows for projects, scenes, uploads, preview, and authentication.
- It looks like a product for building parallax story projects, handling auth, uploads, scene processing, and preview playback in one app.

## How It Is Organized
- `src/app/**` contains the Next.js routes and pages.
- `src/features/**` contains page-facing UI and reusable feature components.
- `src/interfaces/http/**` contains controllers and request support helpers.
- `src/modules/**` contains domain logic, service orchestration, repositories, validators, and types.
- `src/core/**`, `src/config/**`, and `src/infrastructure/**` hold shared plumbing, runtime config, and external integrations.
- `prisma/**` defines database shape and migrations.

## How Requests And Data Likely Move
- Requests enter from UI pages or API route handlers in `src/app/**`.
- API routes usually delegate into controllers in `src/interfaces/http/controllers/**`.
- Controllers call module services in `src/modules/**` to run business logic.
- Services either use repositories for persistence or infrastructure clients/providers for external work.
- Shared concerns such as env access, route handling, errors, and request context live in `src/config/**` and `src/core/**`.

## Important Modules
- `assets`
- `auth`
- `authorization`
- `decomposition`
- `feature-flags`
- `guest-sessions`
- `maintenance`
- `motion`
- `playback`
- `processing`
- `projects`
- `scenes`
- `uploads`

## Important Features
- `auth`
- `marketing`
- `preview`
- `projects`
- `scenes`
- `settings`
- `shared`
- `uploads`

## Critical Flows
- Authentication flow: Auth requests enter through NextAuth routes, rely on auth setup, and likely resolve users through the auth repository and Prisma client.
- Project management flow: Project CRUD and orchestration likely move from API route to controller, through project service logic, into repository-backed persistence.
- Scene processing flow: Scene regeneration appears to combine scene orchestration, processing logic, and Qwen provider integration.
- Preview playback flow: The preview UI likely requests playback data from the API, which is then composed by preview and playback services.

## Best Starting Points
- `src/app/page.tsx`
- `src/app/layout.tsx`
- `src/interfaces/http/controllers/project-controller.ts`
- `src/modules/projects/service.ts`
- `prisma/schema.prisma`

## Known Unknowns
- 17 local imports could not be resolved from the markdown snapshot.
- Several modules do not expose an obvious repository file, so persistence responsibilities may be unevenly distributed.

