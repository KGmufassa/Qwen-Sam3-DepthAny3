```
Directory structure:
└── kgmufassa-parallax-story-board/
    ├── AGENTS.md
    ├── eslint.config.mjs
    ├── next-env.d.ts
    ├── next.config.ts
    ├── package.json
    ├── tsconfig.json
    ├── vitest.config.ts
    ├── .env.example
    ├── docs/
    │   ├── notes/
    │   │   ├── button-trigger-route-audit.md
    │   │   ├── canonical-app-route-structure.md
    │   │   └── planning backend architecture.md
    │   ├── public/
    │   │   ├── AI_BUILD_PIPELINE.md
    │   │   ├── implementation Flow
    │   │   ├── Planning Phase Pipeline (Simplified).md
    │   │   ├── Qwen image layered app.py .rtf
    │   │   ├── Qwen Image layered combine Tools py.rtf
    │   │   ├── Qwen image layered edit_rgba_image tool.rtf
    │   │   ├── Qwen Image Layered Readme.rtf
    │   │   ├── Runpod_sshk.md
    │   │   └── validate-build Flow
    │   ├── reference/
    │   │   ├── 01-stitched-parallax-story-product-flow.md
    │   │   ├── 02-stitched-parallax-story-engine-sequence.md
    │   │   ├── 03-editor-to-parallax-integration-plan.md
    │   │   ├── brainstorm-prd-draft.md
    │   │   ├── prd-draft.md
    │   │   └── project-state.md
    │   ├── rules/
    │   │   └── architecture-rules.md
    │   └── setup/
    │       ├── local-mvp.md
    │       └── mvp-decision-log.md
    ├── prisma/
    │   ├── schema.prisma
    │   └── migrations/
    │       └── 20260316000000_init/
    │           └── migration.sql
    ├── public/
    │   └── runpod-ssh-setup-tutorial.md
    ├── scripts/
    │   └── dev-with-chunk-sync.mjs
    ├── src/
    │   ├── auth.ts
    │   ├── app/
    │   │   ├── layout.tsx
    │   │   ├── page.tsx
    │   │   ├── api/
    │   │   │   ├── auth/
    │   │   │   │   └── [...nextauth]/
    │   │   │   │       └── route.ts
    │   │   │   └── v1/
    │   │   │       ├── assets/
    │   │   │       │   └── [...assetPath]/
    │   │   │       │       └── route.ts
    │   │   │       ├── auth/
    │   │   │       │   ├── register/
    │   │   │       │   │   └── route.ts
    │   │   │       │   └── session/
    │   │   │       │       └── route.ts
    │   │   │       ├── guest-sessions/
    │   │   │       │   └── route.ts
    │   │   │       ├── health/
    │   │   │       │   ├── live/
    │   │   │       │   │   └── route.ts
    │   │   │       │   └── ready/
    │   │   │       │       └── route.ts
    │   │   │       ├── internal/
    │   │   │       │   └── maintenance/
    │   │   │       │       ├── cleanup/
    │   │   │       │       │   └── route.ts
    │   │   │       │       └── recover-timeouts/
    │   │   │       │           └── route.ts
    │   │   │       ├── projects/
    │   │   │       │   ├── route.ts
    │   │   │       │   └── [projectId]/
    │   │   │       │       ├── route.ts
    │   │   │       │       ├── claim/
    │   │   │       │       │   └── route.ts
    │   │   │       │       ├── preview/
    │   │   │       │       │   ├── playback/
    │   │   │       │       │   │   └── route.ts
    │   │   │       │       │   └── status/
    │   │   │       │       │       └── route.ts
    │   │   │       │       ├── scenes/
    │   │   │       │       │   └── reorder/
    │   │   │       │       │       └── route.ts
    │   │   │       │       └── uploads/
    │   │   │       │           ├── finalize/
    │   │   │       │           │   └── route.ts
    │   │   │       │           └── init/
    │   │   │       │               └── route.ts
    │   │   │       ├── scenes/
    │   │   │       │   └── [sceneId]/
    │   │   │       │       ├── route.ts
    │   │   │       │       ├── regenerate/
    │   │   │       │       │   └── route.ts
    │   │   │       │       └── retry/
    │   │   │       │           └── route.ts
    │   │   │       └── uploads/
    │   │   │           └── [uploadToken]/
    │   │   │               └── route.ts
    │   │   ├── login/
    │   │   │   └── page.tsx
    │   │   ├── projects/
    │   │   │   ├── page.tsx
    │   │   │   ├── [projectId]/
    │   │   │   │   ├── editor/
    │   │   │   │   │   └── page.tsx
    │   │   │   │   └── preview/
    │   │   │   │       └── page.tsx
    │   │   │   └── new/
    │   │   │       └── page.tsx
    │   │   ├── settings/
    │   │   │   └── page.tsx
    │   │   └── signup/
    │   │       └── page.tsx
    │   ├── config/
    │   │   ├── constants.ts
    │   │   └── env.ts
    │   ├── core/
    │   │   ├── errors/
    │   │   │   ├── app-error.ts
    │   │   │   └── error-response.ts
    │   │   ├── http/
    │   │   │   └── route-handler.ts
    │   │   ├── logging/
    │   │   │   └── logger.ts
    │   │   ├── observability/
    │   │   │   ├── metrics.ts
    │   │   │   └── processing-log.ts
    │   │   ├── request/
    │   │   │   └── context.ts
    │   │   └── security/
    │   │       └── cookies.ts
    │   ├── features/
    │   │   ├── auth/
    │   │   │   └── components/
    │   │   │       └── auth-page.tsx
    │   │   ├── marketing/
    │   │   │   └── components/
    │   │   │       └── landing-page.tsx
    │   │   ├── preview/
    │   │   │   ├── components/
    │   │   │   │   ├── playback-scene-renderer.tsx
    │   │   │   │   └── project-preview-page.tsx
    │   │   │   └── lib/
    │   │   │       └── playback-client.ts
    │   │   ├── projects/
    │   │   │   ├── mock-projects.ts
    │   │   │   └── components/
    │   │   │       ├── new-project-form.tsx
    │   │   │       ├── new-project-page.tsx
    │   │   │       ├── project-card.tsx
    │   │   │       ├── project-editor-page.tsx
    │   │   │       └── projects-dashboard-page.tsx
    │   │   ├── scenes/
    │   │   │   └── components/
    │   │   │       └── scene-rail.tsx
    │   │   ├── settings/
    │   │   │   └── components/
    │   │   │       └── settings-page.tsx
    │   │   ├── shared/
    │   │   │   └── components/
    │   │   │       ├── app-header.tsx
    │   │   │       └── app-icon.tsx
    │   │   └── uploads/
    │   │       └── components/
    │   │           └── upload-panel.tsx
    │   ├── infrastructure/
    │   │   ├── db/
    │   │   │   └── prisma.ts
    │   │   ├── jobs/
    │   │   │   └── trigger-dev.ts
    │   │   ├── providers/
    │   │   │   └── qwen/
    │   │   │       └── client.ts
    │   │   └── rate-limit/
    │   │       └── memory-rate-limiter.ts
    │   ├── interfaces/
    │   │   └── http/
    │   │       ├── controllers/
    │   │       │   ├── auth-controller.ts
    │   │       │   ├── guest-session-controller.ts
    │   │       │   ├── health-controller.ts
    │   │       │   ├── maintenance-controller.ts
    │   │       │   ├── preview-controller.ts
    │   │       │   ├── project-controller.ts
    │   │       │   ├── scene-controller.ts
    │   │       │   └── upload-controller.ts
    │   │       └── support/
    │   │           ├── authorization.ts
    │   │           ├── internal-maintenance.ts
    │   │           ├── json-body.ts
    │   │           └── request-actor.ts
    │   ├── lib/
    │   │   └── api-response.ts
    │   ├── modules/
    │   │   ├── assets/
    │   │   │   ├── index.ts
    │   │   │   ├── pathing.ts
    │   │   │   ├── serialization.ts
    │   │   │   ├── service.ts
    │   │   │   └── storage.ts
    │   │   ├── auth/
    │   │   │   ├── index.ts
    │   │   │   ├── repository.ts
    │   │   │   ├── service.ts
    │   │   │   ├── types.ts
    │   │   │   └── validator.ts
    │   │   ├── authorization/
    │   │   │   ├── index.ts
    │   │   │   ├── service.ts
    │   │   │   └── types.ts
    │   │   ├── decomposition/
    │   │   │   ├── adapter.ts
    │   │   │   ├── service.ts
    │   │   │   └── types.ts
    │   │   ├── feature-flags/
    │   │   │   ├── index.ts
    │   │   │   └── service.ts
    │   │   ├── guest-sessions/
    │   │   │   ├── index.ts
    │   │   │   ├── repository.ts
    │   │   │   ├── service.ts
    │   │   │   └── types.ts
    │   │   ├── maintenance/
    │   │   │   ├── index.ts
    │   │   │   └── service.ts
    │   │   ├── motion/
    │   │   │   ├── index.ts
    │   │   │   ├── service.ts
    │   │   │   └── types.ts
    │   │   ├── playback/
    │   │   │   ├── index.ts
    │   │   │   └── service.ts
    │   │   ├── processing/
    │   │   │   ├── index.ts
    │   │   │   └── service.ts
    │   │   ├── projects/
    │   │   │   ├── index.ts
    │   │   │   ├── repository.ts
    │   │   │   ├── service.ts
    │   │   │   ├── types.ts
    │   │   │   └── validator.ts
    │   │   ├── scenes/
    │   │   │   ├── index.ts
    │   │   │   ├── repository.ts
    │   │   │   ├── service.ts
    │   │   │   ├── types.ts
    │   │   │   └── validator.ts
    │   │   └── uploads/
    │   │       ├── index.ts
    │   │       ├── service.ts
    │   │       ├── types.ts
    │   │       └── validator.ts
    │   └── types/
    │       └── next-auth.d.ts
    ├── tests/
    │   └── unit/
    │       ├── core/
    │       │   └── errors/
    │       │       └── error-response.test.ts
    │       ├── features/
    │       │   └── preview/
    │       │       └── playback-client.test.ts
    │       └── modules/
    │           ├── assets/
    │           │   └── pathing.test.ts
    │           ├── auth/
    │           │   ├── service.test.ts
    │           │   └── validator.test.ts
    │           ├── authorization/
    │           │   └── policy.test.ts
    │           ├── decomposition/
    │           │   └── adapter.test.ts
    │           ├── feature-flags/
    │           │   └── service.test.ts
    │           ├── guest-sessions/
    │           │   └── service.test.ts
    │           ├── maintenance/
    │           │   └── service.test.ts
    │           ├── motion/
    │           │   └── service.test.ts
    │           ├── playback/
    │           │   └── service.test.ts
    │           ├── projects/
    │           │   └── service.test.ts
    │           ├── scenes/
    │           │   ├── service.test.ts
    │           │   └── validator.test.ts
    │           └── uploads/
    │               └── service.test.ts
    └── .opencode/
        ├── commands/
        │   ├── brainstorm.md
        │   ├── build-frontend-system.md
        │   ├── classify-app.md
        │   ├── extract-design-spec.md
        │   ├── finalize-prd.md
        │   ├── generate-architecture.md
        │   ├── generate-page-graph.md
        │   ├── generate-plan.md
        │   ├── generate-stack-guidelines.md
        │   ├── generate-ui-dependency-graph.md
        │   ├── implement-app.md
        │   ├── stack-advisor.md
        │   └── ui-prompt-builder.md
        ├── modules/
        │   ├── buildBackendCore.js
        │   ├── buildDatabase.js
        │   ├── buildFrontendCore.js
        │   ├── dependencyGraph.js
        │   ├── deployApp.js
        │   ├── featureBuilder.js
        │   ├── qaValidator.js
        │   ├── scaffoldProject.js
        │   ├── taskScheduler.js
        │   ├── testRunner.js
        │   └── validateArchitecture.js
        └── skills/
            ├── debugg/
            │   └── skill.md
            ├── implement-app/
            │   ├── orchestrator.js
            │   └── skill.md
            └── validate-build/
                ├── orchestrator.js
                └── skill.md
```
================================================
FILE: AGENTS.md
================================================
# AGENTS.md
Repository-specific guidance for coding agents working in this project.

## Project Snapshot
- App: `parallax-story-composer`
- Stack: Next.js 15 App Router, React 19, TypeScript, Prisma, PostgreSQL, NextAuth, Zod, Pino, Vitest
- Package manager: `npm`
- TS config: strict mode, no emit, bundler module resolution, `@/* -> src/*`
- API style: versioned routes under `src/app/api/v1/**`
- Architecture style: layered, feature-based modules

## Rule Files
- Primary architecture rules: `docs/rules/architecture-rules.md`
- `.cursorrules`: not present
- `.cursor/rules/`: not present
- `.github/copilot-instructions.md`: not present

## Setup Notes
- Use `.env.example` as the source of expected environment variables
- Core runtime values include `DATABASE_URL`, `NEXTAUTH_SECRET`, `NEXTAUTH_URL`, and `INTERNAL_UPLOAD_TOKEN_SECRET`
- Upload and pipeline features also depend on Qwen-related env vars
- Local work can use `QWEN_MOCK_MODE=true`


## Canonical Commands
- Install dependencies: `npm install`
- Start dev server: `npm run dev`
- Create production build: `npm run build`
- Start production server: `npm run start`
- Lint entire repo: `npm run lint`
- Run all tests once: `npm test`
- Run tests in watch mode: `npm run test:watch`

## Narrow Validation Commands
- Run one test file: `npm test -- tests/unit/modules/uploads/service.test.ts`
- Alternate one test file: `npx vitest run tests/unit/modules/uploads/service.test.ts`
- Run one named test: `npx vitest run tests/unit/modules/uploads/service.test.ts -t "creates and verifies upload contracts"`
- Lint one file: `npx eslint src/modules/projects/service.ts`
- Prefer the narrowest relevant validation first, then broaden only if needed

## Build Expectations
- If you change service, controller, validator, or route behavior, run the closest relevant unit test file and `npm run lint`
- If you change routing, shared types, env/config wiring, or Next.js integration boundaries, run `npm run build` when practical
- If you change Prisma schema or repository persistence behavior, add a migration and validate affected tests

## Repository Layout
- `src/app/`: Next.js pages and API route entrypoints
- `src/interfaces/http/`: controllers plus HTTP support helpers
- `src/modules/<feature>/`: feature slices with service/repository/validator/types/index files
- `src/core/`: shared error, HTTP, logging, request, and observability code
- `src/infrastructure/`: Prisma client, auth/providers, jobs, and rate limiting
- `src/config/`: env parsing and shared constants
- `prisma/`: schema and migrations
- `tests/unit/`: unit tests grouped by module/feature

## Architecture Rules
- Follow strict layering: presentation -> service -> repository -> infrastructure
- Do not place business logic in route handlers or controllers
- Services may call repositories; repositories must not call services
- Infrastructure must not contain domain business logic
- Avoid circular dependencies across features and shared modules
- Keep features independently testable
- Put reusable cross-feature logic in `src/core/` or `src/config/`
- Keep APIs versioned under `/api/v1`
- Apply rate limiting in routes where the existing route pattern already does so

## Route And Controller Patterns
- Prefer `defineRoute(...)` for API handlers
- Keep route files thin: rate limiting, request identification, controller delegation
- Preserve `x-correlation-id` behavior from shared route infrastructure
- Build responses with shared helpers such as `ok(...)` and `created(...)`, and parse bodies with helpers like `parseJsonBody`
- Keep access checks in the existing HTTP/controller support layer

## Feature Organization
- Keep feature code together under `src/modules/<feature>/`
- Typical files are `service.ts`, `repository.ts`, `validator.ts`, `types.ts`, and `index.ts`
- Use feature `index.ts` re-exports where the repo already follows that pattern
- Avoid unnecessary cross-feature imports and coupling

## Imports
- Prefer absolute `@/` imports over long relative paths
- Keep external/framework imports before internal imports
- Use `import type` for type-only imports where appropriate
- Avoid churn-only import reordering when it does not help the change

## Formatting
- Use 2-space indentation
- Use double quotes
- Do not use semicolons
- Match the repo's compact object and function formatting
- Add comments only when a block is genuinely non-obvious

## TypeScript And Types
- Preserve strict typing; avoid `any` unless there is no reasonable alternative
- Prefer feature-local types and Zod-inferred types when they align with runtime validation
- Use narrow unions and literals for stateful behavior
- Respect `typedRoutes: true` in `next.config.ts`
- Do not read env vars directly outside `src/config/env.ts`, except for the existing auth helper pattern already present there

## Naming Conventions
- Use `camelCase` for variables, functions, and object properties
- Use `PascalCase` for classes and exported types
- Use `UPPER_SNAKE_CASE` for constants and environment keys
- Use kebab-case for filenames and route segment names
- Singleton exports follow existing patterns such as `projectService`, `projectRepository`, and `projectController`
- Name Zod schemas descriptively, for example `createProjectInputSchema`

## Validation Rules
- Validate request payloads with Zod in feature-local `validator.ts` files
- Use trimming, length limits, enums, UUID validation, and coercion where appropriate
- Let centralized error handling produce client-facing validation responses
- Do not bypass validation in controllers or services for request input

## Error Handling
- Use `AppError` for expected application and domain failures
- Include a stable machine-readable `code`
- Set an appropriate HTTP `statusCode`
- Add structured `details` when extra context is useful
- Do not expose raw stack traces to clients
- Let shared error response helpers convert thrown errors into HTTP responses
- Never silently swallow errors

## Logging And Observability
- Use the shared Pino logger from `src/core/logging/logger.ts`
- Keep logs structured and machine-readable
- Preserve request correlation IDs in HTTP flows
- Health endpoints already exist under `/api/v1/health/live` and `/api/v1/health/ready`

## Database And Prisma Guidance
- Prisma targets PostgreSQL
- Use UUID primary keys and preserve snake_case database column mappings
- Keep `created_at` and `updated_at` conventions intact
- Add migrations for schema changes
- Keep foreign keys and common lookup paths indexed
- Keep DB access in repositories or infrastructure, never in route handlers or controllers

## Authentication And Session Notes
- NextAuth is in use; preserve existing session and actor resolution patterns
- Guest-session flows are first-class and enforced in several modules
- Do not weaken access checks when editing project, scene, upload, or preview flows

## Testing Guidance
- Existing automated tests live under `tests/unit/`
- Current tests focus heavily on service and validator behavior; follow that style first
- Use Vitest primitives such as `describe`, `it`, `beforeEach`, and `expect`
- Reset env cache when tests mutate `process.env`
- Add or update the closest relevant unit test whenever behavior changes

## Agent Do
- Make the smallest coherent change in the correct layer
- Preserve existing response shapes, error codes, and naming style
- Read the surrounding module before introducing a new pattern
- Report the files changed and commands run

## Agent Do Not
- Do not invent a new validation, logging, or error-handling framework
- Do not move business logic into controllers or route handlers
- Do not scatter direct `process.env` reads across the codebase
- Do not replace an established module pattern unless the repo already supports the new one

## Good Default Workflow
- Read the target route, controller, service, validator, repository, and types files first
- Make the smallest architecture-aligned change
- Run the most specific test command that covers the change
- Run `npm run lint` after material code changes
- Run `npm run build` for route, config, or typing-boundary changes when practical
- If a broader validation step is skipped, say so explicitly in your handoff



================================================
FILE: eslint.config.mjs
================================================
import { dirname } from "node:path"
import { fileURLToPath } from "node:url"

import { FlatCompat } from "@eslint/eslintrc"

const __filename = fileURLToPath(import.meta.url)
const __dirname = dirname(__filename)

const compat = new FlatCompat({
  baseDirectory: __dirname,
})

const config = [
  ...compat.extends("next/core-web-vitals"),
  {
    ignores: ["docs/**", "design/**", ".opencode/**", "validation-reports/**", ".next/**", "prisma/generated/**"],
  },
]

export default config



================================================
FILE: next-env.d.ts
================================================
/// <reference types="next" />
/// <reference types="next/image-types/global" />
/// <reference path="./.next/types/routes.d.ts" />

// NOTE: This file should not be edited
// see https://nextjs.org/docs/app/api-reference/config/typescript for more information.



================================================
FILE: next.config.ts
================================================
import type { NextConfig } from "next"

const nextConfig: NextConfig = {
  typedRoutes: true,
}

export default nextConfig



================================================
FILE: package.json
================================================
{
  "name": "parallax-story-composer",
  "version": "0.1.0",
  "private": true,
  "scripts": {
    "clean": "node -e \"require('fs').rmSync('.next', { recursive: true, force: true })\"",
    "predev": "npm run clean",
    "prebuild": "npm run clean",
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "eslint .",
    "test": "vitest run",
    "test:watch": "vitest"
  },
  "dependencies": {
    "@prisma/client": "^6.5.0",
    "bcryptjs": "^3.0.2",
    "next": "^15.2.0",
    "next-auth": "^5.0.0-beta.25",
    "pino": "^9.6.0",
    "react": "^19.0.0",
    "react-dom": "^19.0.0",
    "zod": "^3.24.2"
  },
  "devDependencies": {
    "@types/node": "^22.13.10",
    "@types/react": "^19.0.10",
    "@types/react-dom": "^19.0.4",
    "eslint": "^9.22.0",
    "eslint-config-next": "^15.2.0",
    "prisma": "^6.5.0",
    "typescript": "^5.8.2",
    "vitest": "^3.0.8"
  }
}



================================================
FILE: tsconfig.json
================================================
{
  "compilerOptions": {
    "target": "ES2022",
    "lib": ["dom", "dom.iterable", "es2022"],
    "allowJs": false,
    "skipLibCheck": true,
    "strict": true,
    "noEmit": true,
    "esModuleInterop": true,
    "module": "esnext",
    "moduleResolution": "bundler",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "jsx": "preserve",
    "incremental": true,
    "plugins": [
      {
        "name": "next"
      }
    ],
    "paths": {
      "@/*": ["./src/*"]
    }
  },
  "include": ["next-env.d.ts", "**/*.ts", "**/*.tsx", ".next/types/**/*.ts"],
  "exclude": ["node_modules"]
}



================================================
FILE: vitest.config.ts
================================================
import { defineConfig } from "vitest/config"
import { fileURLToPath } from "node:url"

export default defineConfig({
  test: {
    environment: "node",
    globals: true,
  },
  resolve: {
    alias: {
      "@": fileURLToPath(new URL("./src", import.meta.url)),
    },
  },
})



================================================
FILE: .env.example
================================================
DATABASE_URL="postgresql://postgres:postgres@localhost:5432/parallax_story_composer"
NEXTAUTH_SECRET="replace-with-a-long-random-secret"
NEXTAUTH_URL="http://localhost:3000"
LOCAL_STORAGE_ROOT=".local/storage"
GOOGLE_CLIENT_ID=""
GOOGLE_CLIENT_SECRET=""
GUEST_SESSION_COOKIE_NAME="psc_guest_session"
GUEST_SESSION_TTL_HOURS="72"
RATE_LIMIT_WINDOW_MS="60000"
RATE_LIMIT_MAX_REQUESTS="60"
LOG_LEVEL="info"
NODE_ENV="development"
UPLOAD_MAX_FILES="10"
UPLOAD_MAX_FILE_SIZE_BYTES="10485760"
UPLOAD_ALLOWED_MIME_TYPES="image/jpeg,image/png,image/webp"
INTERNAL_UPLOAD_TOKEN_SECRET="replace-with-a-long-random-upload-secret"
INTERNAL_MAINTENANCE_TOKEN="replace-with-a-long-random-maintenance-token"
QWEN_API_URL=""
QWEN_API_KEY=""
QWEN_MODEL="qwen-image-layered"
QWEN_TIMEOUT_MS="30000"
QWEN_MAX_RETRIES="2"
QWEN_MOCK_MODE="true"
GUEST_MAX_PROJECTS="3"
GUEST_MAX_SCENES_PER_PROJECT="10"
PROCESSING_JOB_TIMEOUT_MS="300000"
FEATURE_MOTION_PIPELINE="true"
FEATURE_PLAYBACK_PIPELINE="true"
FEATURE_PREVIEW_FALLBACKS="true"
FEATURE_REDUCED_MOTION_PREVIEW="true"
PROCESSING_CANARY_PERCENT="100"



================================================
FILE: docs/notes/button-trigger-route-audit.md
================================================
# Button And Trigger Route Audit

## Purpose

This document audits the interactive triggers in the HTML mockups under `design/HTML/` and maps each trigger to:
- its current implementation state in the mockup
- its recommended canonical route or action target

This audit should be read alongside `docs/notes/canonical-app-route-structure.md`.

## Audit Legend

- `Current target`: what is wired in the HTML today
- `Canonical target`: the recommended route or action for implementation
- `Type`: `route` or `action`

## authentication-mvp.html

Source: `design/HTML/authentication-mvp.html`

| Trigger | Current target | Canonical target | Type | Notes |
| --- | --- | --- | --- | --- |
| Log In tab | none | `/login` or tab state | route/action | Use route if login and signup are separate pages |
| Sign Up tab | none | `/signup` or tab state | route/action | Use route if login and signup are separate pages |
| Continue with Google | none | `/api/auth/signin/google` | route | OAuth entrypoint |
| Forgot? | `#` | `/forgot-password` | route | Password reset entry |
| Password visibility toggle | none | Toggle password visibility | action | Pure UI behavior |
| Enter Studio | form submit disabled | Redirect to `/dashboard` or `/projects` after auth | action | Successful login action |
| Create an account | `#` | `/signup` | route | Auth conversion path |

## landing-page-design-system.html

Source: `design/HTML/landing-page-design-system.html`

| Trigger | Current target | Canonical target | Type | Notes |
| --- | --- | --- | --- | --- |
| Dashboard | `#` | `/dashboard` | route | Authenticated destination |
| Projects | `#` | `/projects` | route | Saved projects dashboard |
| New Project | `#` | `/projects/new` | route | New project entry |
| Sign In | none | `/login` | route | Public auth entry |
| Start Free as Guest | none | `/projects/new?mode=guest` | route | Guest-first creation flow |
| Create Account | none | `/signup` | route | Public auth signup |
| Already have an account? Log In | `#` | `/login` | route | Alternate auth entry |
| Unlock Full Features | none | `/signup` | route | Can later branch to billing or upgrade |
| Create Your Story | none | `/projects/new` | route | Primary CTA |
| Footer social links | `#` | External links or placeholders | route | Needs product decision |
| Features | `#` | `/docs` or marketing section anchor | route | Could be in-page anchor on landing |
| Tutorials | `#` | `/docs` | route | Documentation or learning hub |
| Gallery | `#` | `/gallery` if added later | route | Not required for MVP |
| Pricing | `#` | `/pricing` if added later | route | Not required for MVP |
| Documentation | `#` | `/docs` | route | Static/support page |
| API Reference | `#` | `/api-reference` | route | Static/support page |
| Community | `#` | `/community` if added later | route | Optional future route |
| Support | `#` | `/support` | route | Static/support page |
| Privacy Policy | `#` | `/privacy` | route | Static/support page |
| Terms of Service | `#` | `/terms` | route | Static/support page |

## project-editor-final-mvp.html

Source: `design/HTML/project-editor-final-mvp.html`

| Trigger | Current target | Canonical target | Type | Notes |
| --- | --- | --- | --- | --- |
| Dashboard | `#` | `/dashboard` | route | Top nav |
| Projects | `#` | `/projects` | route | Top nav |
| New Project | `#` | `/projects/new` | route | Top nav |
| Notifications | none | Open notifications panel | action | No page route needed |
| Back arrow | none | `/projects` | route | Return to project list |
| Save | none | Save current project | action | Stay on current editor route |
| Preview | none | `/projects/:projectId/preview` | route | Full project preview |
| Export | none | `/projects/:projectId/export` | route | Auth-gated route |
| Generate | none | Start processing pipeline | action | Async generation trigger |
| Upload Images | none | Open file picker and upload flow | action | In-editor mutation |
| Scene refresh | none | Reprocess scene | action | Per-scene regenerate action |
| Scene delete | none | Delete scene from project | action | Confirm before destructive mutation |
| Player previous | none | Jump to previous scene or segment | action | Local playback control |
| Player play | none | Toggle preview playback | action | Local playback control |
| Player next | none | Jump to next scene or segment | action | Local playback control |
| Scene tab | none | Show scene settings panel | action | In-page tab state |
| Project tab | none | Show project settings panel | action | In-page tab state |
| Depth focus: Subject | none | Set scene depth focus | action | In-page control |
| Depth focus: Balanced | none | Set scene depth focus | action | In-page control |
| Depth focus: Background | none | Set scene depth focus | action | In-page control |
| Reduced Motion toggle | none | Toggle project preference | action | In-page preference update |
| Reprocess Scene | none | Start scene reprocessing | action | Async mutation |

## saved-projects-dashboard-final.html

Source: `design/HTML/saved-projects-dashboard-final.html`

| Trigger | Current target | Canonical target | Type | Notes |
| --- | --- | --- | --- | --- |
| Dashboard | `#` | `/dashboard` | route | Top nav |
| Projects | `#` | `/projects` | route | Current page |
| New Project | `#` | `/projects/new` | route | Top nav |
| New Project button | none | `/projects/new` | route | Desktop CTA |
| Create New Sequence | none | `/projects/new` | route | Mobile CTA |
| Filter | none | Open filter controls | action | In-page UI behavior |
| Misty Peaks Cinematic - Open Editor | none | `/projects/:projectId/editor` | route | Project editor entry |
| Misty Peaks Cinematic - Preview | none | `/projects/:projectId/preview` | route | Project preview |
| Misty Peaks Cinematic - Export | none | `/projects/:projectId/export` | route | Auth-gated export |
| Neon District 2077 - Processing | disabled | none | action | Intentionally unavailable |
| Neon District 2077 - Preview | none | `/projects/:projectId/preview` | route | Optional if preview exists during processing |
| Neon District 2077 - Delete | none | Delete project | action | Confirm before destructive mutation |
| Desert Mirage - Continue Editing | none | `/projects/:projectId/editor` | route | Draft continuation |
| Desert Mirage - Preview | none | `/projects/:projectId/preview` | route | Project preview |
| Desert Mirage - Delete | none | Delete project | action | Confirm before destructive mutation |
| Cyber Cityscape - Open Editor | none | `/projects/:projectId/editor` | route | Project editor entry |
| Cyber Cityscape - Preview | none | `/projects/:projectId/preview` | route | Project preview |
| Cyber Cityscape - Export | none | `/projects/:projectId/export` | route | Auth-gated export |
| Empty state New Project | none | `/projects/new` | route | Project creation entry |
| Documentation | `#` | `/docs` | route | Footer |
| API Reference | `#` | `/api-reference` | route | Footer |
| Support | `#` | `/support` | route | Footer |
| Terms | `#` | `/terms` | route | Footer |

## settings-page-design-system.html

Source: `design/HTML/settings-page-design-system.html`

| Trigger | Current target | Canonical target | Type | Notes |
| --- | --- | --- | --- | --- |
| Home | `#` | `/dashboard` | route | Main app home |
| Projects | `#` | `/projects` | route | Project list |
| New Project | `#` | `/projects/new` | route | Creation flow |
| Settings | `#` | `/settings` | route | Current page |
| Notifications | none | Open notifications panel | action | In-app panel |
| Change Password | none | `/settings/security` or modal | route/action | Start with modal if simpler |
| Reduced Motion toggle | none | Update user preference | action | Persist preference |
| Story Pace select | none | Update user preference | action | Persist preference |
| Transition Style select | none | Update user preference | action | Persist preference |
| Motion Preset select | none | Update user preference | action | Persist preference |
| Sign Out of All Devices | none | POST sign-out-all action | action | Destructive session action |
| Save Changes | none | Save settings | action | Stay on `/settings` |
| Reset Defaults | none | Reset preferences | action | Confirm if destructive |
| Sign Out | none | POST `/api/auth/signout`, then `/login` | action | Session exit flow |

## Canonical Route Inventory Extracted From Audit

Routes repeatedly implied by the mockups:

- `/`
- `/login`
- `/signup`
- `/forgot-password`
- `/dashboard`
- `/projects`
- `/projects/new`
- `/projects/:projectId/editor`
- `/projects/:projectId/preview`
- `/projects/:projectId/export`
- `/settings`
- `/settings/security`
- `/docs`
- `/api-reference`
- `/support`
- `/terms`
- `/privacy`

Optional later additions suggested by some labels:

- `/gallery`
- `/pricing`
- `/community`

## Implementation Guidance

- Replace all placeholder `href="#"` links with canonical destinations when those routes are implemented
- Keep save, generate, upload, delete, retry, toggle, playback, and panel-opening controls as in-page actions rather than routes
- Gate save and export actions for guests and route them into auth or upgrade flows as needed
- Use project-scoped dynamic routes for editor, preview, and export so project cards and editor actions resolve consistently

## Decision Summary

The mockups currently function as visual-only prototypes, not route-wired screens. This audit converts each visible trigger into a consistent route or action target so implementation can proceed without inventing navigation ad hoc.



================================================
FILE: docs/notes/canonical-app-route-structure.md
================================================
# Canonical App Route Structure

## Purpose

This document defines the canonical application route structure for Parallax Story Composer based on the current PRD and the HTML mockups in `design/HTML/`.

It is intended to:
- align navigation across landing, auth, projects, editor, preview, and settings
- give button and trigger audits a source of truth
- separate page routes from in-page actions and modal flows
- support guest preview and authenticated save/export gating

## Route Design Principles

- Use top-level routes only for real pages with standalone navigation value
- Keep editing and processing actions inside the current page when they do not need a dedicated URL
- Use project-scoped routes for editor, preview, and export-related screens
- Keep auth flows explicit and separate from product pages
- Preserve guest access for preview and build flows while gating save and export behind auth
- Prefer stable, semantic routes over UI-label-driven routes

## Canonical Route Map

### Public Routes

- `/`
  - Primary landing page
  - Corresponds to the landing mockup
  - Entry point for guest or authenticated users

- `/login`
  - Email and password sign in
  - Supports redirect back into app after auth

- `/signup`
  - Account creation

- `/forgot-password`
  - Password reset request flow

### Auth And Session Routes

- `/api/auth/signin`
  - Auth provider entrypoint if using NextAuth
- `/api/auth/signout`
  - Sign out endpoint
- `/api/auth/callback/:provider`
  - OAuth callback route
- `/api/auth/session`
  - Session lookup endpoint

Recommended OAuth trigger target:
- Google sign-in button -> `/api/auth/signin/google`

### App Shell Routes

- `/dashboard`
  - High-level home for authenticated users
  - Can later show recent projects, processing jobs, and quick actions

- `/projects`
  - Saved projects dashboard
  - Corresponds to the saved projects mockup

- `/projects/new`
  - New project entry route
  - Can initialize guest or authenticated project creation
  - Best target for `New Project`, `Create Your Story`, and `Start Free as Guest`

### Project-Scoped Routes

- `/projects/:projectId`
  - Project overview shell
  - Optional redirect route
  - Recommended behavior: redirect to `/projects/:projectId/editor`

- `/projects/:projectId/editor`
  - Main project editing interface
  - Corresponds to the editor mockup
  - Includes scene manager, project settings, upload, reorder, prompt editing, and generation triggers

- `/projects/:projectId/preview`
  - Full stitched preview page
  - Useful when preview should be shareable or opened independently of editor

- `/projects/:projectId/export`
  - Export screen for authenticated users
  - If export is not enabled yet, route can show gated or coming soon state

- `/projects/:projectId/settings`
  - Optional project-specific settings page if editor tabs become too dense
  - Not required for MVP if project settings remain inside editor sidebar

### Scene-Oriented Optional Routes

These are optional and should only exist if deep-linking is needed.

- `/projects/:projectId/scenes/:sceneId`
  - Scene details anchor route
- `/projects/:projectId/scenes/:sceneId/preview`
  - Scene preview route
- `/projects/:projectId/scenes/:sceneId/reprocess`
  - Usually better as an action, not a page

Recommendation:
- For MVP, keep scene operations in-page and avoid dedicated scene page routes unless deep-linking becomes necessary

### User Settings Routes

- `/settings`
  - Main user settings page
  - Corresponds to the settings mockup

- `/settings/security`
  - Optional future route for password and session controls

- `/settings/preferences`
  - Optional future route if settings expand significantly

For MVP:
- Keep all current settings under `/settings`

### Static And Support Routes

- `/docs`
- `/api-reference`
- `/support`
- `/terms`
- `/privacy`

These align with footer links seen in the mockups.

## Canonical Trigger To Route Mapping

### Landing Page

- `Dashboard` -> `/dashboard`
- `Projects` -> `/projects`
- `New Project` -> `/projects/new`
- `Sign In` -> `/login`
- `Start Free as Guest` -> `/projects/new?mode=guest`
- `Create Account` -> `/signup`
- `Already have an account? Log In` -> `/login`
- `Create Your Story` -> `/projects/new`
- `Unlock Full Features` -> `/signup` for guests, `/settings/billing` later if billing exists

### Authentication Page

- `Log In` tab -> `/login` or in-page tab state
- `Sign Up` tab -> `/signup` or in-page tab state
- `Continue with Google` -> `/api/auth/signin/google`
- `Forgot?` -> `/forgot-password`
- `Enter Studio` -> redirect to `/dashboard` or `/projects` after successful login
- `Create an account` -> `/signup`

Recommendation:
- Use separate page routes for `/login` and `/signup`
- Use tab UI only if both forms remain on one shared auth page

### Saved Projects Dashboard

- `Dashboard` -> `/dashboard`
- `Projects` -> `/projects`
- `New Project` -> `/projects/new`
- `Open Editor` -> `/projects/:projectId/editor`
- `Continue Editing` -> `/projects/:projectId/editor`
- `Preview` -> `/projects/:projectId/preview`
- `Export` -> `/projects/:projectId/export`
- `New Project` empty state -> `/projects/new`

### Editor

- `Dashboard` -> `/dashboard`
- `Projects` -> `/projects`
- `New Project` -> `/projects/new`
- Back arrow -> `/projects`
- `Preview` -> `/projects/:projectId/preview`
- `Export` -> `/projects/:projectId/export`

Recommendation:
- `Save`, `Generate`, `Upload Images`, `Reprocess Scene`, `Delete Scene`, `Refresh Scene`, playback controls, and tab switches should remain in-page actions, not routes

### Settings

- `Home` -> `/dashboard`
- `Projects` -> `/projects`
- `New Project` -> `/projects/new`
- `Settings` -> `/settings`
- `Change Password` -> `/settings/security` or modal
- `Sign Out` -> POST `/api/auth/signout`, then redirect to `/login`

## Route Versus Action Rules

Use a route when:
- the destination is a standalone page
- the URL should be shareable or bookmarkable
- browser back and forward should preserve the state
- the content has distinct information architecture value

Use an in-page action when:
- the user is mutating current page state
- the trigger opens a modal, panel, picker, or tab
- the action starts processing, saving, uploading, reordering, or retrying
- the user should stay in context

## Recommended MVP Route Set

Implement first:

- `/`
- `/login`
- `/signup`
- `/forgot-password`
- `/dashboard`
- `/projects`
- `/projects/new`
- `/projects/:projectId/editor`
- `/projects/:projectId/preview`
- `/settings`

Defer until needed:

- `/projects/:projectId/export`
- `/settings/security`
- `/docs`
- `/api-reference`
- `/support`
- `/terms`
- `/privacy`

## Notes For Next.js App Router

Recommended folder shape:

- `src/app/page.tsx` -> `/`
- `src/app/login/page.tsx` -> `/login`
- `src/app/signup/page.tsx` -> `/signup`
- `src/app/forgot-password/page.tsx` -> `/forgot-password`
- `src/app/dashboard/page.tsx` -> `/dashboard`
- `src/app/projects/page.tsx` -> `/projects`
- `src/app/projects/new/page.tsx` -> `/projects/new`
- `src/app/projects/[projectId]/editor/page.tsx` -> `/projects/:projectId/editor`
- `src/app/projects/[projectId]/preview/page.tsx` -> `/projects/:projectId/preview`
- `src/app/settings/page.tsx` -> `/settings`

## Decision Summary

Canonical navigation should center around:
- public entry at `/`
- explicit auth routes
- project collection at `/projects`
- creation at `/projects/new`
- editing at `/projects/:projectId/editor`
- preview at `/projects/:projectId/preview`
- user settings at `/settings`

This structure best matches the PRD, supports guest and authenticated flows, and gives the current HTML button audit a stable routing target model.



================================================
FILE: docs/notes/planning backend architecture.md
================================================
# Outlining comprehensive plan structure

## Context Window Summary

This planning thread focused on backend architecture for Parallax Story Composer based on the draft PRD at `docs/reference/prd-draft.md`.

Key outcomes discussed:

- The backend must support:
  - Async processing pipeline (decomposition -> motion -> stitching)
  - Guest preview + authenticated save/export gating
  - Organized scene + asset persistence
  - Scene-level retry/regeneration
- Recommended MVP backend direction:
  - Next.js API/backend runtime + PostgreSQL + Prisma
  - Job orchestration (Inngest/Trigger.dev)
  - S3-compatible storage for uploads/generated assets
  - Qwen decomposition integration via a dedicated wrapper
- Confirmed decision:
  - Use direct Node -> Qwen API for MVP (with abstraction so it can later move to Python gateway if needed).

## Qwen API Wrapper Planning Summary

### Why a wrapper is needed

- Isolate provider-specific behavior from business logic.
- Normalize Qwen outputs into app-stable contracts.
- Improve reliability (timeouts, retries, error handling).
- Preserve observability and traceability for failed scenes.

### Core capabilities to implement

- Submit decomposition jobs for scene images.
- Track status (`queued`, `processing`, `ready`, `failed`).
- Retrieve and normalize decomposition results.
- Persist ordered layered assets with metadata.
- Support retries for transient failures.

## Comprehensive Plan Structure

### Phase 0 - Contracts and design lock

Define stable internal interfaces and DTOs first:

- `DecompositionRequest`
- `DecompositionResult`
- `ProviderError` (normalized error taxonomy)
- Idempotency key strategy: `sceneId + sourceHash + modelVersion + targetLayers`

Expected output:
- Provider-agnostic decomposition interface for service layer use.

### Phase 1 - Qwen HTTP client (infrastructure)

Implement provider client with:

- Auth header injection from centralized config
- Timeout control
- Retry policy with exponential backoff + jitter
- Correlation/trace ID propagation
- Input validation (mime, size, layer target bounds)

Expected output:
- Hardened low-level client for calling Qwen endpoints.

### Phase 2 - Decomposition wrapper module

Implement wrapper methods:

- `submitDecomposition()`
- `getDecompositionResult()`
- optional `cancelDecomposition()`

Responsibilities:

- Hide raw Qwen payload quirks
- Map raw provider responses to normalized DTOs
- Map provider errors to internal error codes

Expected output:
- Clean provider adapter usable by processing service.

### Phase 3 - Orchestration integration

Integrate wrapper into async worker/job system:

- One decomposition job per scene
- State transitions persisted in DB
- Per-scene lock to prevent duplicate active jobs
- Retry only transient failures

Expected output:
- Reliable scene processing flow from upload to terminal status.

### Phase 4 - Asset organization and persistence

Store outputs in organized deterministic structure:

- Storage key pattern:
  `projects/{projectId}/scenes/{sceneId}/v{version}/layers/{index}.png`
- Save scene asset manifest with ordered layers and metadata
- Persist composite preview and model/version info

Expected output:
- Layered images returned in a predictable, queryable format.

### Phase 5 - Observability and ops readiness

Add structured logs and metrics:

- Logs: `traceId`, `projectId`, `sceneId`, `jobId`, `providerJobId`
- Metrics: success/failure rates, latency p50/p95/p99, retries, queue depth
- Alerts for fail-rate spikes and latency regressions

Expected output:
- Fast debugging and production monitoring coverage.

### Phase 6 - Testing strategy

Implement tests across layers:

- Unit: mapper/parser/retry/idempotency logic
- Integration: mocked Qwen API happy and failure paths
- Workflow tests: failed scene -> retry -> ready
- Contract tests: stable output schema for downstream services

Expected output:
- Confidence in correctness and failure handling before rollout.

### Phase 7 - Rollout strategy

- Feature flag wrapper integration
- Canary subset of decomposition jobs
- Monitor metrics and error distributions
- Ramp to full traffic after stability window

Expected output:
- Low-risk production adoption.

## Organized Return-State Model for Layered Results

Each scene should store a versioned manifest including:

- Scene and project IDs
- Provider model metadata
- Ordered layer list (`layer_index`, URL/key, dimensions)
- Composite preview URL/key
- Timing and warning metadata
- Terminal processing status

This ensures renderer/planner can consume a clean, stable format.

## Open Execution Notes

This document captures the agreed planning direction and is ready to use as the implementation guide for the Qwen API wrapper build.



================================================
FILE: docs/public/AI_BUILD_PIPELINE.md
================================================
# AI Application Development Pipeline

This document describes the **full autonomous development pipeline** used by the AI project system.

The system converts a **raw idea → fully structured implementation plan** using staged architecture generation.

Each stage produces **artifacts stored in `docs/reference/`**, which are used by subsequent commands.

---

# Pipeline Overview

```
Brainstorm
↓
PRD Draft
↓
UI Prompt Builder
↓
UI Design Generation (Google Stitch)
↓
Extract Design Spec
↓
Frontend Architecture
↓
Stack Advisor
↓
Backend Architecture
↓
Stack Guidelines
↓
Finalize PRD
↓
Generate Plan
↓
Implementation Phase
```

Each step progressively **reduces ambiguity** and **adds technical structure**.

---

# 1. Brainstorm

Command:

```
/brainstorm
```

## Purpose

Transform a **raw brain dump of ideas** into a **structured concept draft**.

This stage focuses on **clarifying the product idea**.

## Inputs

Either:

```
context window text
```

or

```
/brainstorm <file>
```

Example:

```
/brainstorm idea.txt
```

## What the Command Does

1. Reads the user brain dump
2. Extracts:
   - product idea
   - user goals
   - features
   - application theme
3. Researches industry patterns
4. Asks clarifying questions
5. Challenges assumptions
6. Suggests potential tech stacks

## Question Layers

### Product Questions

Example:

```
Who is the primary user?
What problem does the app solve?
What makes this product unique?
```

### Feature Questions

Example:

```
What are the core features required for MVP?
Which features require backend services?
Which features are UI-only?
```

### Architecture Questions

Example:

```
Will the app require real-time updates?
Will authentication be required?
Does the system require background workers?
```

## Output Artifact

```
docs/reference/prd-draft.md
```

This is a **draft PRD used for design generation**.

---

# 2. UI Prompt Builder

Command:

```
/ui-prompt-builder
```

## Purpose

Generate a **prompt for the Google Stitch UI builder** based on the PRD draft.

## Inputs

```
docs/reference/prd-draft.md
```

## What the Command Does

1. Extracts features from the PRD draft
2. Derives possible UI pages
3. Identifies UX patterns
4. Asks UI clarifying questions
5. Builds a structured UI prompt

## Output

A prompt usable in **Google Stitch**.

---

# 3. UI Design Generation (Google Stitch)

This stage is **manual**.

The user submits the generated prompt to:

```
Google Stitch
```

## Output

The UI builder generates HTML layouts saved in:

```
design/
```

Example structure:

```
design/
  stitch/
    landing-page.txt
    dashboard-page.txt
    project-page.txt
```

These files contain **raw HTML source code**.

---

# 4. Extract Design Spec

Command:

```
/extract-design-spec
```

## Purpose

Convert **HTML design code** into a **structured UI architecture specification**.

## Inputs

```
design/
```

HTML source files.

## What the Command Does

Analyzes:

- HTML structure
- Tailwind styles
- components
- layout containers

Extracts:

```
pages
components
layouts
design tokens
navigation
```

## Output

```
docs/reference/frontend-design-spec.md
```

---

# 5. Generate Frontend Architecture

Command:

```
/generate-frontend-architecture
```

## Purpose

Convert the design specification into a **formal frontend architecture document**.

## Inputs

```
docs/reference/frontend-design-spec.md
docs/reference/prd-draft.md
```

## What the Command Generates

Defines:

```
framework
routing system
layout architecture
component hierarchy
state management
API consumption model
UI dependency graph
page wiring graph
```

## Output

```
docs/reference/frontend-architecture.md
```

---

# 6. Stack Advisor

Command:

```
/stack-advisor
```

## Purpose

Determine the **complete technology stack**.

## Inputs

```
docs/reference/frontend-architecture.md
docs/reference/prd-draft.md
```

## Process

1. Detects frontend stack
2. Asks backend stack questions
3. Determines:

```
backend framework
database
ORM
authentication
deployment target
testing framework
```

## Outputs

```
docs/reference/stack.md
docs/reference/backend-architecture.md
```

---

# 7. Backend Architecture

Generated during stack advisor.

## Purpose

Define backend system structure.

## Architecture Includes

```
controllers
services
repositories
models
routes
middleware
configuration
```

Example structure:

```
src/
controllers/
services/
repositories/
models/
routes/
middleware/
config/
```

## Output

```
docs/reference/backend-architecture.md
```

---

# 8. Generate Stack Guidelines

Command:

```
/generate-stack-guidelines
```

## Purpose

Retrieve **official best practices** using **Context7 MCP**.

## Output

```
docs/reference/stack-guidelines.md
```

Contents include:

```
project structure
service layer patterns
configuration patterns
security practices
performance patterns
testing practices
deployment patterns
```

---

# 9. Finalize PRD

Command:

```
/finalize-prd
```

## Purpose

Create the **final authoritative PRD**.

## Inputs

```
docs/reference/prd-draft.md
docs/reference/frontend-architecture.md
docs/reference/backend-architecture.md
docs/reference/stack.md
docs/reference/frontend-design-spec.md
```

## Output

```
docs/reference/prd.md
```

Includes:

```
product vision
feature list
functional requirements
system architecture
data models
UI structure
tech stack
MVP scope
non-functional requirements
```

---

# 10. Generate Plan

Command:

```
/generate-plan
```

## Purpose

Generate the **technical build plan**.

## Inputs

```
frontend-architecture.md
backend-architecture.md
stack.md
prd.md
stack-guidelines.md
```

## Output

```
docs/reference/plan.md
```

### Infrastructure Phase

```
environment setup
database initialization
container configuration
```

### Core Module Setup

```
authentication
logging
configuration
```

### Backend Implementation

```
controllers
services
repositories
models
```

### Frontend Implementation

```
layouts
components
hooks
pages
```

### Feature-by-Feature Breakdown

Each feature defines:

```
frontend components
backend services
API endpoints
data models
```

### Cross-Cutting Concerns

```
authentication
authorization
logging
error handling
```

### Performance Strategy

```
database indexing
API caching
lazy loading
```

### Security Enforcement

```
input validation
auth guards
rate limiting
```

### Validation Checklist

Ensures:

```
features implemented
APIs wired
tests written
```

### Deployment Strategy

```
CI/CD pipeline
database migrations
environment configuration
```

---

# Architecture Rules

Generated alongside the plan.

Output:

```
docs/reference/architecture-rules.md
```

Purpose:

Prevent architectural drift.

Example rules:

```
controllers cannot access database directly
repositories handle database queries
services contain business logic
UI cannot call database directly
```

---

# Final Artifacts Generated

```
docs/reference/

prd-draft.md
frontend-design-spec.md
frontend-architecture.md
backend-architecture.md
stack.md
stack-guidelines.md
prd.md
plan.md
architecture-rules.md
```

---

# Next Stage: Implementation Pipeline

Example commands:

```
scaffold-project
build-database
build-backend
build-frontend
write-tests
run-tests
qa-review
```

---

# Key Benefit of This System

The pipeline ensures:

```
ideas → architecture → implementation plan
```

This reduces:

```
architecture mistakes
feature ambiguity
stack incompatibilities
technical debt
```



scaffold-project
build-database
build-backend
build-frontend
write-tests
run-tests
qa-review



================================================
FILE: docs/public/implementation Flow
================================================
User
  │
  ▼
/implement-app command
  │
  ▼
implement-app skill
  │
  ▼
orchestrator.js
  │
  ├── validateArchitecture
  ├── dependencyGraph
  ├── scaffoldProject
  ├── buildDatabase
  ├── buildBackendCore
  ├── buildFrontendCore
  └── featureBuilder



================================================
FILE: docs/public/Planning Phase Pipeline (Simplified).md
================================================

# AI App Development Pipeline (Simplified)

This document outlines the simplified workflow used by the AI system to turn a raw app idea into a structured build plan.

The system progressively converts **ideas → architecture → implementation plan**.

---

# Pipeline Overview

Brainstorm  
↓  
PRD Draft  
↓  
UI Prompt Builder  
↓  
UI Design Generation (Google Stitch)  
↓  
Extract Design Spec  
↓  
Frontend Architecture  
↓  
Stack Advisor  
↓  
Backend Architecture  
↓  
Stack Guidelines  
↓  
Finalize PRD  
↓  
Generate Plan  

---

# 1. Brainstorm

Command:

/brainstorm

Purpose:

Organizes a raw brain dump into structured product ideas.

The system:
- Extracts features
- Clarifies the product idea
- Asks questions about functionality and architecture
- Suggests possible tech stacks

Output:

docs/reference/prd-draft.md

---

# 2. UI Prompt Builder

Command:

/ui-prompt-builder

Purpose:

Creates a prompt for generating UI designs in Google Stitch using the PRD draft.

Output:

Prompt used to generate UI layouts.

---

# 3. UI Design Generation

Manual step.

The generated prompt is used in Google Stitch to create UI layouts.

The resulting HTML files are saved in:

design/

---

# 4. Extract Design Spec

Command:

/extract-design-spec

Purpose:

Analyzes the HTML UI design files and converts them into a structured design specification.

Extracted information includes:
- pages
- components
- layouts
- design tokens

Output:

docs/reference/frontend-design-spec.md

---

# 5. Frontend Architecture

Command:

/generate-frontend-architecture

Purpose:

Transforms the design specification into a formal frontend architecture.

Defines:
- routing
- layouts
- component hierarchy
- UI modules

Output:

docs/reference/frontend-architecture.md

---

# 6. Stack Advisor

Command:

/stack-advisor

Purpose:

Determines the full application technology stack.

Defines:
- frontend framework
- backend framework
- database
- ORM
- deployment platform

Outputs:

docs/reference/stack.md  
docs/reference/backend-architecture.md

---

# 7. Backend Architecture

Purpose:

Defines the backend system structure including:

- controllers
- services
- repositories
- models
- routes

Output:

docs/reference/backend-architecture.md

---

# 8. Stack Guidelines

Command:

/generate-stack-guidelines

Purpose:

Uses Context7 MCP to retrieve best practices for the selected tech stack.

Includes guidance for:
- architecture patterns
- security
- testing
- deployment

Output:

docs/reference/stack-guidelines.md

---

# 9. Finalize PRD

Command:

/finalize-prd

Purpose:

Creates the final product requirements document using:

- PRD draft
- frontend architecture
- backend architecture
- stack configuration

Output:

docs/reference/prd.md

---

# 10. Generate Plan

Command:

/generate-plan

Purpose:

Creates the technical build plan for implementing the application.

The plan defines:
- infrastructure setup
- backend implementation
- frontend implementation
- feature breakdown
- deployment strategy

Outputs:

docs/reference/plan.md  
docs/reference/architecture-rules.md

---

# Final Artifacts

The pipeline produces the following core documents:

docs/reference/

- prd-draft.md
- frontend-design-spec.md
- frontend-architecture.md
- backend-architecture.md
- stack.md
- stack-guidelines.md
- prd.md
- plan.md
- architecture-rules.md

---

# Next Stage: Implementation

These artifacts are then used by the implementation commands such as:

- scaffold-project
- build-database
- build-backend
- build-frontend
- write-tests
- run-tests
- qa-review

---

# Summary

The system ensures that:

ideas → architecture → build plan

This structured process reduces ambiguity and keeps development aligned with the architecture.



================================================
FILE: docs/public/Qwen image layered app.py .rtf
================================================
{\rtf1\ansi\ansicpg1252\cocoartf2868
\cocoatextscaling0\cocoaplatform0{\fonttbl\f0\fswiss\fcharset0 Helvetica;}
{\colortbl;\red255\green255\blue255;}
{\*\expandedcolortbl;;}
\margl1440\margr1440\vieww11520\viewh8400\viewkind0
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\f0\fs24 \cf0 from diffusers import QwenImageLayeredPipeline\
import torch\
from PIL import Image\
from pptx import Presentation\
import os\
import gradio as gr\
import uuid\
import numpy as np\
import random\
import tempfile\
import zipfile \
from psd_tools import PSDImage\
MAX_SEED = np.iinfo(np.int32).max\
\
pipeline = QwenImageLayeredPipeline.from_pretrained("Qwen/Qwen-Image-Layered")\
pipeline = pipeline.to("cuda", torch.bfloat16)\
pipeline.set_progress_bar_config(disable=None)\
\
def imagelist_to_pptx(img_files):\
    with Image.open(img_files[0]) as img:\
        img_width_px, img_height_px = img.size\
\
    def px_to_emu(px, dpi=96):\
        inch = px / dpi\
        emu = inch * 914400\
        return int(emu)\
\
    prs = Presentation()\
    prs.slide_width = px_to_emu(img_width_px)\
    prs.slide_height = px_to_emu(img_height_px)\
\
    slide = prs.slides.add_slide(prs.slide_layouts[6])\
\
    left = top = 0\
    for img_path in img_files:\
        slide.shapes.add_picture(img_path, left, top, width=px_to_emu(img_width_px), height=px_to_emu(img_height_px))\
\
    with tempfile.NamedTemporaryFile(suffix=".pptx", delete=False) as tmp:\
        prs.save(tmp.name)\
        return tmp.name\
\
def imagelist_to_psd(img_files):\
    layers = []\
    for path in img_files:\
        layers.append(Image.open(path).convert('RGBA'))\
\
    width, height = layers[0].size\
    psd = PSDImage.new(mode='RGBA', size=(width, height))\
\
    for i, img in enumerate(layers):\
        name = f"Layer \{i + 1\}"\
        layer = psd.create_pixel_layer(image=img, name=name)\
        psd.append(layer)\
    \
    with tempfile.NamedTemporaryFile(suffix=".psd", delete=False) as tmp:\
        psd.save(tmp.name)\
        return tmp.name\
\
def export_gallery(images):\
    # images: list of image file paths\
    images = [e[0] for e in images]\
    pptx_path = imagelist_to_pptx(images)\
    return pptx_path\
\
def infer(input_image,\
          seed=777,\
          randomize_seed=False,\
          prompt=None,\
          neg_prompt=" ",\
          true_guidance_scale=4.0,\
          num_inference_steps=50,\
          layer=4,\
          cfg_norm=True,\
          use_en_prompt=True):\
    \
    if randomize_seed:\
        seed = random.randint(0, MAX_SEED)\
        \
    if isinstance(input_image, list):\
        input_image = input_image[0]\
        \
    if isinstance(input_image, str):\
        pil_image = Image.open(input_image).convert("RGB").convert("RGBA")\
    elif isinstance(input_image, Image.Image):\
        pil_image = input_image.convert("RGB").convert("RGBA")\
    elif isinstance(input_image, np.ndarray):\
        pil_image = Image.fromarray(input_image).convert("RGB").convert("RGBA")\
    else:\
        raise ValueError("Unsupported input_image type: %s" % type(input_image))\
    \
    inputs = \{\
        "image": pil_image,\
        "generator": torch.Generator(device='cuda').manual_seed(seed),\
        "true_cfg_scale": true_guidance_scale,\
        "prompt": prompt,\
        "negative_prompt": neg_prompt,\
        "num_inference_steps": num_inference_steps,\
        "num_images_per_prompt": 1,\
        "layers": layer,\
        "resolution": 640,      # Using different bucket (640, 1024) to determine the resolution. For this version, 640 is recommended\
        "cfg_normalize": cfg_norm,  # Whether enable cfg normalization.\
        "use_en_prompt": use_en_prompt, \
    \}\
    print(inputs)\
    with torch.inference_mode():\
        output = pipeline(**inputs)\
        output_images = output.images[0]\
    \
    output = []\
    temp_files = []\
    for i, image in enumerate(output_images):\
        output.append(image)\
        # Save to temp file for export\
        tmp = tempfile.NamedTemporaryFile(suffix=".png", delete=False)\
        image.save(tmp.name)\
        temp_files.append(tmp.name)\
    \
    # Generate PPTX\
    pptx_path = imagelist_to_pptx(temp_files)\
    \
    # Generate ZIP\
    with tempfile.NamedTemporaryFile(suffix=".zip", delete=False) as tmp:\
        with zipfile.ZipFile(tmp.name, 'w', zipfile.ZIP_DEFLATED) as zipf:\
            for i, img_path in enumerate(temp_files):\
                zipf.write(img_path, f"layer_\{i+1\}.png")\
        zip_path = tmp.name\
    \
    # Generate PSD\
    psd_path = imagelist_to_psd(temp_files)\
    return output, pptx_path, zip_path, psd_path\
\
examples = [\
            "assets/test_images/1.png",\
            "assets/test_images/2.png",\
            "assets/test_images/3.png",\
            "assets/test_images/4.png",\
            "assets/test_images/5.png",\
            "assets/test_images/6.png",\
            "assets/test_images/7.png",\
            "assets/test_images/8.png",\
            "assets/test_images/9.png",\
            "assets/test_images/10.png",\
            "assets/test_images/11.png",\
            "assets/test_images/12.png",\
            "assets/test_images/13.png",\
            ]\
\
\
with gr.Blocks() as demo:\
    with gr.Column(elem_id="col-container"):\
        gr.HTML('''<p align="center"><img src="https://qianwen-res.oss-cn-beijing.aliyuncs.com/Qwen-Image/layered/qwen-image-layered-logo.png" width="400"/><p>''')\
        gr.Markdown("""\
                    The text prompt is intended to describe the overall content of the input image\'97including elements that may be partially occluded (e.g., you may specify the text hidden behind a foreground object). It is not designed to control the semantic content of individual layers explicitly.\
                    """)\
        with gr.Row():\
            with gr.Column(scale=1):\
                input_image = gr.Image(label="Input Image", image_mode="RGBA")\
                \
                \
                with gr.Accordion("Advanced Settings", open=False):\
                    prompt = gr.Textbox(\
                        label="Prompt (Optional)",\
                        placeholder="Please enter the prompt to describe the image. It is not designed to control the semantic content of individual layers explicitly. (Optional)",\
                        value="",\
                        lines=3,\
                    )\
                    neg_prompt = gr.Textbox(\
                        label="Negative Prompt (Optional)",\
                        placeholder="Please enter the negative prompt",\
                        value=" ",\
                        lines=3,\
                    )\
                    \
                    seed = gr.Slider(\
                        label="Seed",\
                        minimum=0,\
                        maximum=MAX_SEED,\
                        step=1,\
                        value=0,\
                    )\
                    randomize_seed = gr.Checkbox(label="Randomize seed", value=True)\
                    \
                    true_guidance_scale = gr.Slider(\
                        label="True guidance scale",\
                        minimum=1.0,\
                        maximum=10.0,\
                        step=0.1,\
                        value=4.0\
                    )\
\
                    num_inference_steps = gr.Slider(\
                        label="Number of inference steps",\
                        minimum=1,\
                        maximum=50,\
                        step=1,\
                        value=50,\
                    )\
\
                    layer = gr.Slider(\
                        label="Layers",\
                        minimum=2,\
                        maximum=10,\
                        step=1,\
                        value=4,\
                    )\
\
                    cfg_norm = gr.Checkbox(label="Whether enable CFG normalization", value=True)\
                    use_en_prompt = gr.Checkbox(label="Automatic caption language if no prompt provided, True for EN, False for ZH", value=True)\
                \
                run_button = gr.Button("Decompose!", variant="primary")\
\
            with gr.Column(scale=2):\
                gallery = gr.Gallery(label="Layers", columns=4, rows=1, format="png")\
                with gr.Row():\
                    export_file = gr.File(label="Download PPTX")\
                    export_zip_file = gr.File(label="Download ZIP")\
                    export_psd_file = gr.File(label="Download PSD")\
\
    gr.Examples(examples=examples,\
                inputs=[input_image], \
                outputs=[gallery, export_file, export_zip_file, export_psd_file],\
                fn=infer, \
                examples_per_page=14,\
                cache_examples=False,\
                run_on_click=True\
    )\
\
    run_button.click(\
        fn=infer,\
        inputs=[\
            input_image,\
            seed,\
            randomize_seed,\
            prompt,\
            neg_prompt,\
            true_guidance_scale,\
            num_inference_steps,\
            layer,\
            cfg_norm,\
            use_en_prompt,\
        ], \
        outputs=[gallery, export_file, export_zip_file, export_psd_file],\
    )\
\
demo.launch(\
    server_name="0.0.0.0",\
    server_port=7869,\
)}


================================================
FILE: docs/public/Qwen Image layered combine Tools py.rtf
================================================
{\rtf1\ansi\ansicpg1252\cocoartf2868
\cocoatextscaling0\cocoaplatform0{\fonttbl\f0\fswiss\fcharset0 Helvetica;}
{\colortbl;\red255\green255\blue255;}
{\*\expandedcolortbl;;}
\margl1440\margr1440\vieww11520\viewh8400\viewkind0
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\f0\fs24 \cf0 import gradio as gr\
from PIL import Image\
\
def combine_images(uploaded_files):\
    if not uploaded_files:\
        return None\
\
    images = []\
    for f in uploaded_files:\
        img = Image.open(f.name).convert("RGBA")\
        images.append(img)\
\
    min_height = min(img.height for img in images)\
    resized_images = [img.resize((int(img.width * min_height / img.height), min_height), Image.LANCZOS) for img in images]\
\
    combined = resized_images[0]\
    for img in resized_images[1:]:\
        combined = Image.alpha_composite(combined, img)\
\
    return combined\
\
demo = gr.Interface(\
    fn=combine_images,\
    inputs=gr.File(file_count="multiple", label="Upload images with transparency (PNG) in order."),\
    outputs=gr.Image(type="pil", label="Combined Result"),\
    title="Layer Blender",\
    description="Upload multiple PNG images, and the system will blend them into a single image.",\
)\
\
if __name__ == "__main__":\
    demo.launch()}


================================================
FILE: docs/public/Qwen image layered edit_rgba_image tool.rtf
================================================
{\rtf1\ansi\ansicpg1252\cocoartf2868
\cocoatextscaling0\cocoaplatform0{\fonttbl\f0\fswiss\fcharset0 Helvetica;}
{\colortbl;\red255\green255\blue255;}
{\*\expandedcolortbl;;}
\margl1440\margr1440\vieww11520\viewh8400\viewkind0
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\f0\fs24 \cf0 import gradio as gr\
import numpy as np\
import random\
import torch\
\
from PIL import Image, ImageDraw\
from torchvision import transforms\
from transformers import AutoModelForImageSegmentation\
from diffusers import QwenImageEditPlusPipeline\
\
# --- Model Loading ---\
dtype = torch.bfloat16\
device = "cuda" if torch.cuda.is_available() else "cpu"\
\
# Load the model pipeline\
pipe = QwenImageEditPlusPipeline.from_pretrained("Qwen/Qwen-Image-Edit-2509", torch_dtype=dtype).to(device)\
rmbg_model = AutoModelForImageSegmentation.from_pretrained('briaai/RMBG-2.0', trust_remote_code=True).eval().to(device)\
rmbg_transforms = transforms.Compose([\
        transforms.Resize((1024, 1024)),\
        transforms.ToTensor(),\
        transforms.Normalize([0.485, 0.456, 0.406], [0.229, 0.224, 0.225])\
    ])\
\
# --- UI Constants and Helpers ---\
MAX_SEED = np.iinfo(np.int32).max\
\
def blend_with_green_bg(input_img):\
    bg = Image.new("RGB", input_img.size, (30, 215, 96)).convert("RGBA")\
    input_rgba = input_img.convert("RGBA")\
    blended = Image.alpha_composite(bg, input_rgba).convert("RGB")\
    return blended\
\
# --- Main Inference Function (with hardcoded negative prompt) ---\
def infer(\
    image,\
    prompt,\
    seed=42,\
    randomize_seed=False,\
    true_guidance_scale=1.0,\
    num_inference_steps=50,\
    progress=gr.Progress(track_tqdm=True),\
):\
    """\
    Generates an image using the local Qwen-Image diffusers pipeline.\
    """\
    # Hardcode the negative prompt as requested\
    negative_prompt = " "\
    \
    if randomize_seed:\
        seed = random.randint(0, MAX_SEED)\
\
    # Set up the generator for reproducibility\
    generator = torch.Generator(device=device).manual_seed(seed)\
    \
    print(f"Calling pipeline with prompt: '\{prompt\}'")\
    print(f"Negative Prompt: '\{negative_prompt\}'")\
    print(f"Seed: \{seed\}, Steps: \{num_inference_steps\}, Guidance: \{true_guidance_scale\}")\
\
    image = blend_with_green_bg(image)\
\
    # Generate the image\
    edited_image = pipe(\
        image,\
        prompt=prompt,\
        negative_prompt=negative_prompt,\
        num_inference_steps=num_inference_steps,\
        generator=generator,\
        true_cfg_scale=true_guidance_scale,\
        num_images_per_prompt=1\
    ).images[0]\
\
    # Remove background\
    input_images = rmbg_transforms(edited_image).unsqueeze(0).to(device)\
    with torch.no_grad():\
        preds = rmbg_model(input_images)[-1].sigmoid().cpu()\
    pred = preds[0].squeeze()\
    pred_pil = transforms.ToPILImage()(pred)\
    mask = pred_pil.resize(edited_image.size)\
    edited_image.putalpha(mask)\
    \
    return edited_image, seed\
\
# --- Examples and UI Layout ---\
examples = []\
\
css = """\
#col-container \{\
    margin: 0 auto;\
    max-width: 1024px;\
\}\
#edit_text\{margin-top: -62px !important\}\
"""\
\
with gr.Blocks(css=css) as demo:\
    with gr.Column(elem_id="col-container"):\
        gr.HTML('<img src="https://qianwen-res.oss-cn-beijing.aliyuncs.com/Qwen-Image/qwen_image_edit_logo.png" alt="Qwen-Image-Edit Logo" width="400" style="display: block; margin: 0 auto;">')\
        gr.Markdown("This Gradio-based web interface use [Qwen-Image-Edit](https://github.com/QwenLM/Qwen-Image) to edit layers with transparent background. Upload an image with alpha channel (RGBA) and provide an edit instruction to get started!")\
        with gr.Row():\
            with gr.Column():\
                input_image = gr.Image(label="Input Image", show_label=False, type="pil", image_mode="RGBA")\
\
            result = gr.Image(label="Result", show_label=False, type="pil")\
        with gr.Row():\
            prompt = gr.Text(\
                    label="Prompt",\
                    show_label=False,\
                    placeholder="describe the edit instruction",\
                    container=False,\
            )\
            run_button = gr.Button("Edit!", variant="primary")\
\
        with gr.Accordion("Advanced Settings", open=False):\
            seed = gr.Slider(\
                label="Seed",\
                minimum=0,\
                maximum=MAX_SEED,\
                step=1,\
                value=0,\
            )\
\
            randomize_seed = gr.Checkbox(label="Randomize seed", value=True)\
\
            with gr.Row():\
\
                true_guidance_scale = gr.Slider(\
                    label="True guidance scale",\
                    minimum=1.0,\
                    maximum=10.0,\
                    step=0.1,\
                    value=4.0\
                )\
\
                num_inference_steps = gr.Slider(\
                    label="Number of inference steps",\
                    minimum=1,\
                    maximum=50,\
                    step=1,\
                    value=50,\
                )\
                \
\
        # gr.Examples(examples=examples, inputs=[prompt], outputs=[result, seed], fn=infer, cache_examples=False)\
\
    gr.on(\
        triggers=[run_button.click, prompt.submit],\
        fn=infer,\
        inputs=[\
            input_image,\
            prompt,\
            seed,\
            randomize_seed,\
            true_guidance_scale,\
            num_inference_steps,\
        ],\
        outputs=[result, seed],\
    )\
\
if __name__ == "__main__":\
    demo.launch()}


================================================
FILE: docs/public/Qwen Image Layered Readme.rtf
================================================
{\rtf1\ansi\ansicpg1252\cocoartf2868
\cocoatextscaling0\cocoaplatform0{\fonttbl\f0\fswiss\fcharset0 Helvetica;}
{\colortbl;\red255\green255\blue255;}
{\*\expandedcolortbl;;}
\margl1440\margr1440\vieww11520\viewh8400\viewkind0
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\f0\fs24 \cf0 <p align="center">\
    <img src="https://qianwen-res.oss-cn-beijing.aliyuncs.com/Qwen-Image/layered/qwen-image-layered-logo.png" width="800"/>\
<p> \
<p align="center">&nbsp&nbsp\uc0\u55358 \u56599  <a href="https://huggingface.co/Qwen/Qwen-Image-Layered">HuggingFace</a>&nbsp&nbsp | &nbsp&nbsp\u55358 \u56598  <a href="https://modelscope.cn/models/Qwen/Qwen-Image-Layered">ModelScope</a>&nbsp&nbsp | &nbsp&nbsp \u55357 \u56529  <a href="https://arxiv.org/abs/2512.15603">Research Paper</a> &nbsp&nbsp | &nbsp&nbsp \u55357 \u56529  <a href="https://qwen.ai/blog?id=qwen-image-layered">Blog</a> &nbsp&nbsp | &nbsp&nbsp \u55358 \u56599  <a href="https://huggingface.co/spaces/Qwen/Qwen-Image-Layered">Demo</a> &nbsp&nbsp \
</p>\
\
<p align="center">\
    <img src="https://qianwen-res.oss-cn-beijing.aliyuncs.com/Qwen-Image/layered/layered.JPG" width="1024"/>\
<p>\
\
## Introduction\
We are excited to introduce **Qwen-Image-Layered**, a model capable of decomposing an image into multiple RGBA layers. This layered representation unlocks **inherent editability**: each layer can be independently manipulated without affecting other content. Meanwhile, such a layered representation naturally supports **high-fidelity elementary operations**-such as resizing, reposition, and recoloring. By physically isolating semantic or structural components into distinct layers, our approach enables high-fidelity and consistent editing.\
\
\
[![Qwen Image Layered](https://img.youtube.com/vi/OVhmiBrsziQ/0.jpg)](https://www.youtube.com/watch?v=OVhmiBrsziQ)\
\
\
## News\
- 2025.12.22: You can try Qwen-Image-Layered on [Huggingface Spaces](https://huggingface.co/spaces/Qwen/Qwen-Image-Layered) and [Modelscope Studio](https://modelscope.cn/studios/Qwen/Qwen-Image-Layered).\
- 2025.12.19: We released Qwen-Image-Layered weights! Check at [Huggingface](https://huggingface.co/Qwen/Qwen-Image-Layered) and [ModelScope](https://modelscope.cn/models/Qwen/Qwen-Image-Layered)!\
- 2025.12.19: We released Qwen-Image-Layered! Check our [Blog](https://qwen.ai/blog?id=qwen-image-layered) for more details!\
- 2025.12.18: We released our [Research Paper](https://arxiv.org/abs/2512.15603) on Arxiv!\
\
> [!NOTE]\
> - The text prompt is intended to describe the overall content of the input image\'97including elements that may be partially occluded (e.g., you may specify the text hidden behind a foreground object). It is not designed to control the semantic content of individual layers explicitly.\
> - The released weights are specifically fine-tuned for the image-to-multi-RGBA decomposition task. As a result, while the model supports text-conditioned inference, its performance on text-to-multi-RGBA generation is limited.\
\
## Quick Start\
\
1. Make sure your transformers>=4.51.3 (Supporting Qwen2.5-VL)\
\
2. Install the latest version of diffusers\
```\
pip install git+https://github.com/huggingface/diffusers\
pip install python-pptx\
pip install psd-tools\
```\
\
\
```python\
from diffusers import QwenImageLayeredPipeline\
import torch\
from PIL import Image\
\
pipeline = QwenImageLayeredPipeline.from_pretrained("Qwen/Qwen-Image-Layered")\
pipeline = pipeline.to("cuda", torch.bfloat16)\
pipeline.set_progress_bar_config(disable=None)\
\
image = Image.open("asserts/test_images/1.png").convert("RGBA")\
inputs = \{\
    "image": image,\
    "generator": torch.Generator(device='cuda').manual_seed(777),\
    "true_cfg_scale": 4.0,\
    "negative_prompt": " ",\
    "num_inference_steps": 50,\
    "num_images_per_prompt": 1,\
    "layers": 4,\
    "resolution": 640,      # Using different bucket (640, 1024) to determine the resolution. For this version, 640 is recommended\
    "cfg_normalize": True,  # Whether enable cfg normalization.\
    "use_en_prompt": True,  # Automatic caption language if user does not provide caption\
\}\
\
with torch.inference_mode():\
    output = pipeline(**inputs)\
    output_image = output.images[0]\
\
for i, image in enumerate(output_image):\
    image.save(f"\{i\}.png")\
```\
\
## Deploy Qwen-Image-Layered\
The following scripts will start a Gradio-based web interface where you can decompose an image and export the layers into pptx, zip, and psd files, where you can edit and move these layers flexibly.\
```bash\
python src/app.py\
```\
\
After decomposition, you may want to edit specific layers. The following scripts will launch a Gradio-based web interface where you can edit images with transparency using Qwen-Image-Edit.\
```bash\
python src/tool/edit_rgba_image.py\
```\
\
After editing the individual decomposed layers, you can use the following script to combine them into a new image. Remember to upload the layers in order\'97from the bottom layer to the top.\
```bash\
python src/tool/combine_layers.py\
```\
\
### vLLM-Omni\
[vLLM-Omni](https://github.com/vllm-project/vllm-omni) now supports Qwen-Image-Layered. See the [recipes](https://docs.vllm.ai/projects/recipes/en/latest/Qwen/Qwen-Image.html) for up-to-date details.\
\
## Showcase\
### Layered Decomposition in Application\
Given an image, Qwen-Image-Layered can decompose it into several RGBA layers:\
![Example Image](https://qianwen-res.oss-cn-beijing.aliyuncs.com/Qwen-Image/layered/\uc0\u24187 \u28783 \u29255 1.JPG)\
\
After decomposition, edits are applied exclusively to the target layer, physically isolating it from the rest of the content, and thereby fundamentally ensuring consistency across edits. \
\
For example, we can recolor the first layer and keep all other content untouched:\
![Example Image](https://qianwen-res.oss-cn-beijing.aliyuncs.com/Qwen-Image/layered/\uc0\u24187 \u28783 \u29255 2.JPG)\
\
We can also replace the second layer from a girl to a boy (The target layer is edited using Qwen-Image-Edit):\
![Example Image](https://qianwen-res.oss-cn-beijing.aliyuncs.com/Qwen-Image/layered/\uc0\u24187 \u28783 \u29255 3.JPG)\
\
Here, we revise the text to "Qwen-Image" (The target layer is edited using Qwen-Image-Edit):\
![Example Image](https://qianwen-res.oss-cn-beijing.aliyuncs.com/Qwen-Image/layered/\uc0\u24187 \u28783 \u29255 4.JPG)\
\
Furthermore, the layered structure naturally supports elemetary operations. For example, we can delete unwanted objects cleanly:\
![Example Image](https://qianwen-res.oss-cn-beijing.aliyuncs.com/Qwen-Image/layered/\uc0\u24187 \u28783 \u29255 5.JPG)\
\
We can also resize an object without distortion:\
![Example Image](https://qianwen-res.oss-cn-beijing.aliyuncs.com/Qwen-Image/layered/\uc0\u24187 \u28783 \u29255 6.JPG)\
\
After layer decomposition, we can move objects freely within the canvas:\
![Example Image](https://qianwen-res.oss-cn-beijing.aliyuncs.com/Qwen-Image/layered/\uc0\u24187 \u28783 \u29255 7.JPG)\
\
### Flexible and Iterative Decomposition\
Qwen-Image-Layered is not limited to a fixed number of layers. The model supports variable-layer decomposition. For example, we can decompose an image into either 3 or 8 layers as needed:\
\
![Example Image](https://qianwen-res.oss-cn-beijing.aliyuncs.com/Qwen-Image/layered/\uc0\u24187 \u28783 \u29255 8.JPG)\
\
Moreover, decomposition can be applied recursively: any layer can itself be further decomposed, enabling infinite decomposition. \
\
![Example Image](https://qianwen-res.oss-cn-beijing.aliyuncs.com/Qwen-Image/layered/\uc0\u24187 \u28783 \u29255 9.JPG)\
\
\
## License Agreement\
\
Qwen-Image-Layered is licensed under Apache 2.0. \
\
## Citation\
\
We kindly encourage citation of our work if you find it useful.\
\
```bibtex\
@misc\{yin2025qwenimagelayered,\
      title=\{Qwen-Image-Layered: Towards Inherent Editability via Layer Decomposition\}, \
      author=\{Shengming Yin, Zekai Zhang, Zecheng Tang, Kaiyuan Gao, Xiao Xu, Kun Yan, Jiahao Li, Yilei Chen, Yuxiang Chen, Heung-Yeung Shum, Lionel M. Ni, Jingren Zhou, Junyang Lin, Chenfei Wu\},\
      year=\{2025\},\
      eprint=\{2512.15603\},\
      archivePrefix=\{arXiv\},\
      primaryClass=\{cs.CV\},\
      url=\{https://arxiv.org/abs/2512.15603\}, \
\}\
```}


================================================
FILE: docs/public/Runpod_sshk.md
================================================
# RunPod SSH Setup Tutorial
This guide captures the full command flow we used, from creating an SSH key to testing a RunPod SSH connection.
## 1. Create an SSH key pair
Create a new Ed25519 key:
```bash
ssh-keygen -t ed25519 -C "your-email@example.com"
```
When prompted:
- choose a save path, or press Enter for the default `~/.ssh/id_ed25519`
- optionally enter a passphrase for extra protection
If you create a custom key instead, you may end up with files like:
- private key: `sshk`
- public key: `sshk_pub` or `sshk.pub`
## 2. Find your public key
List your SSH files:
```bash
ls ~/.ssh
```
Print the public key:
```bash
cat ~/.ssh/id_ed25519.pub
```
If you used a custom filename, print that public key instead:
```bash
cat /path/to/your/custom_key.pub
```
Only the public key should be pasted into RunPod.
## 3. Register the public key in RunPod
Paste the contents of your public key into the SSH key section in RunPod.
Important:
- public key goes into RunPod
- private key stays on your machine
## 4. Move keys into the standard SSH location
If your keys were created outside `~/.ssh`, move them into place.
Example used here:
```bash
mkdir -p ~/.ssh
mv ~/Desktop/sshk ~/.ssh/id_ed25519
mv ~/Desktop/sshk_pub ~/.ssh/id_ed25519.pub
chmod 600 ~/.ssh/id_ed25519
chmod 644 ~/.ssh/id_ed25519.pub
```
Verify:
```bash
ls -la ~/.ssh
```
Expected files:
- `~/.ssh/id_ed25519`
- `~/.ssh/id_ed25519.pub`
## 5. Test the RunPod SSH gateway
RunPod may give you a gateway command like this:
```bash
ssh q91ot3ib257e53-644115fd@ssh.runpod.io -i ~/.ssh/id_ed25519
```
To test with verbose output:
```bash
ssh -v q91ot3ib257e53-644115fd@ssh.runpod.io -i ~/.ssh/id_ed25519
```
What to look for:
- `Offering public key`
- `Server accepts key`
If you see both, the key pairing is correct.
## 6. Test the exposed TCP SSH endpoint
RunPod may also show a direct command like this:
```bash
ssh root@213.173.110.146 -p 14214 -i ~/.ssh/id_ed25519
```
Verbose version:
```bash
ssh -v root@213.173.110.146 -p 14214 -i ~/.ssh/id_ed25519
```
In our test session, this endpoint returned:
```text
Connection refused
```
That means the port was reachable as an address, but SSH was not listening there at the time.
## 7. Test whether the port is open
You can verify the TCP port directly:
```bash
nc -vz 213.173.110.146 14214
```
If it returns `Connection refused`, the direct exposed SSH endpoint is not currently accepting connections.
## 8. Load the key into your SSH agent
If your private key has a passphrase, the non-interactive session may fail even after the server accepts the key.
Start the SSH agent if needed:
```bash
eval "$(ssh-agent -s)"
```
Add your key:
```bash
ssh-add ~/.ssh/id_ed25519
```
Then retry the gateway login:
```bash
ssh q91ot3ib257e53-644115fd@ssh.runpod.io -i ~/.ssh/id_ed25519
```
## 9. How to tell what failed
### Key path problem
```text
Identity file ... not accessible: No such file or directory
```
Meaning: your `-i` path is wrong.
### Desktop/macOS permission problem
```text
Operation not permitted
```
Meaning: Terminal cannot access Desktop/Documents/Downloads. Move the key into `~/.ssh` or grant permissions in macOS.
### RunPod accepted the key, but passphrase could not be entered
```text
Server accepts key
read_passphrase: can't open /dev/tty
Permission denied (publickey)
```
Meaning: the key is correct, but the session cannot prompt for the passphrase. Use `ssh-add` first.
### Direct endpoint network/service problem
```text
connect to address ... port ...: Connection refused
```
Meaning: nothing is listening on that exposed SSH port yet.
## 10. Final recommended connection flow
Use this order:
1. Create key pair with `ssh-keygen`
2. Paste the public key into RunPod
3. Move the private key to `~/.ssh/id_ed25519`
4. Set permissions with `chmod 600 ~/.ssh/id_ed25519`
5. Run `ssh-add ~/.ssh/id_ed25519`
6. Connect through the RunPod gateway:
```bash
ssh q91ot3ib257e53-644115fd@ssh.runpod.io -i ~/.ssh/id_ed25519
```
7. Only use the exposed TCP command if RunPod confirms that endpoint is active:
```bash
ssh root@213.173.110.146 -p 14214 -i ~/.ssh/id_ed25519
```
## 11. Commands used in this session
These are the main commands we used while debugging:
```bash
ssh -v root@213.173.110.146 -p 14214 -i ~/.ssh/id_ed25519
ssh -v root@213.173.110.146 -p 14214 -i /Users/wislemleger/Desktop/sshk
nc -vz 213.173.110.146 14214
ssh -v q91ot3ib257e53-644115fd@ssh.runpod.io -i /Users/wislemleger/Desktop/sshk
mkdir -p ~/.ssh
mv ~/Desktop/sshk ~/.ssh/id_ed25519
mv ~/Desktop/sshk_pub ~/.ssh/id_ed25519.pub
chmod 600 ~/.ssh/id_ed25519
chmod 644 ~/.ssh/id_ed25519.pub
ls -la ~/.ssh
ssh -v q91ot3ib257e53-644115fd@ssh.runpod.io -i ~/.ssh/id_ed25519
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```



================================================
FILE: docs/public/validate-build Flow
================================================
/validate-build

Step 9
Test Runner

 ├─ unit tests
 ├─ API tests
 └─ Playwright E2E tests

Step 10
QA validation



================================================
FILE: docs/reference/01-stitched-parallax-story-product-flow.md
================================================
# Stitched Parallax Story Product Flow

This document describes the end-to-end user journey for creating a stitched parallax storyboard in the current app.

## End-To-End User Progression

1. The user lands on the app.
- They understand the product promise: upload still images, shape scenes, and preview a stitched parallax story.
- They continue as guest or sign in.

2. The user starts a new project.
- They enter from the home page, projects page, or top navigation.
- They arrive at `/projects/new`.

3. The user sets up the project.
- They enter a project title.
- They optionally add global context.
- They optionally choose a style preset.

4. The user uploads source images.
- They select one or more images.
- The images appear in the upload queue.

5. The user arranges the initial storyboard order.
- They drag images into the intended sequence.
- That order becomes the initial scene order.

6. The user clicks `Create Project`.
- The app creates the project record.
- If needed, it creates a guest session first.

7. The app prepares upload slots.
- The app requests upload contracts for each image.
- Each image receives an upload token and upload destination.

8. The app uploads the raw source files.
- The selected images are uploaded into project storage.
- These are the original source assets for the new scenes.

9. The app finalizes the uploads as scenes.
- Each uploaded image becomes a scene record.
- The selected order becomes the initial scene timeline order.
- A thumbnail copy is created for editor and preview use.

10. The app automatically queues decomposition for each scene.
- Every new scene is enqueued for background processing.
- The storyboard exists immediately, but deeper processing continues asynchronously.

11. Each scene image is sent into the Qwen image decomposition pipeline.
- The decomposition pipeline receives the scene source image and metadata.
- This is the step where the flat image is prepared for depth-based playback.

12. Qwen separates the image into layered scene elements.
- Foreground and background style elements are split into layer assets.
- These returned assets become the basis for parallax behavior.

13. The returned decomposition assets are stored back in the app.
- The backend persists the returned scene assets.
- The scene now has source, thumbnail, and decomposition layer assets.

14. The scene progresses through processing states.
- The scene moves from `queued` to `processing` to `ready`.
- Users can see that the storyboard is progressively becoming playback-ready.

15. The app generates motion behavior for the returned layers.
- A motion blueprint is generated for each processed scene.
- This defines camera movement, intensity, layer parallax, scale, opacity, and transitions.

16. The project is stitched into a playback timeline.
- The playback service builds the stitched timeline for the project.
- Scene order, duration, overlap, timing, movement, and fallback behavior are assembled into one playback plan.

17. The user enters the editor workspace.
- They arrive at `/projects/[projectId]/editor`.
- They can see the project shell, scene list, and current processing states.

18. The user refines the storyboard scene by scene.
- They edit scene context.
- They choose motion preset and motion intensity.
- They may upload more images later.

19. The user monitors scenes as they become ready.
- Some scenes may still be queued or processing.
- Other scenes may already be ready for playback.

20. The returned layered assets and motion settings drive the parallax engine.
- The parallax experience is no longer based only on the original flat image.
- It is based on decomposition layer assets plus motion blueprint data.

21. The user opens preview.
- They go to `/projects/[projectId]/preview`.
- The app loads the stitched playback plan for the project.

22. The user sees the stitched parallax storyboard.
- The preview presents a continuous vertical playback experience.
- If some scenes are still incomplete, fallback playback can still show renderable scenes.

23. The user evaluates pacing, depth, and continuity.
- They assess story order, motion, timing, and transitions.
- They decide whether more edits are needed.

24. The user returns to the editor for revisions.
- They adjust scene settings or project direction.
- They retry or regenerate scenes if needed.
- They preview again.

25. The user reaches a finished stitched story.
- Images have been uploaded.
- Scenes have been created.
- Qwen has decomposed scene elements.
- Returned assets have been stored.
- Motion has been generated.
- Playback has been stitched.
- The project is previewable as a continuous parallax story.

## Core Creation Loop

1. Upload source image.
2. Create scene.
3. Enqueue decomposition.
4. Send image to Qwen.
5. Qwen separates image elements into layers.
6. Return those layers to the app.
7. Store them on the scene.
8. Generate motion blueprint.
9. Stitch playback timeline.
10. Preview the parallax storyboard.



================================================
FILE: docs/reference/02-stitched-parallax-story-engine-sequence.md
================================================
# Stitched Parallax Story Engine Sequence

This document maps the stitched parallax storyboard flow across frontend, API, backend services, processing, and playback.

## Sequence Overview

1. Frontend: project creation starts.
- The user submits the new project form at `/projects/new`.
- The client creates the project and uploads source images.

2. API: uploads are finalized into scenes.
- `POST /api/v1/projects/[projectId]/uploads/finalize`
- The finalize route creates scene records in the selected order.

3. Backend: thumbnails are created.
- The source upload is copied into a thumbnail path for editor and preview use.

4. Backend: scene decomposition jobs are enqueued.
- Each created scene is queued for decomposition.
- The scene status moves to `queued`.

5. Processing layer: decomposition is dispatched.
- The processing service dispatches a decomposition job for each scene.
- In local development, the dev trigger runs the decomposition flow.

6. Decomposition layer: the source image is pushed into Qwen.
- The decomposition adapter receives:
  - `projectId`
  - `sceneId`
  - `imageUrl`
  - `mimeType`
  - `width`
  - `height`
  - `targetLayers`
  - `correlationId`

7. Qwen returns decomposition output.
- The provider returns separated scene layers and related metadata.
- These layers represent the scene elements used for parallax depth.

8. Asset layer: returned scene assets are persisted.
- The backend stores the returned decomposition layer assets.
- Those assets are attached to the scene.

9. Motion layer: the scene motion blueprint is generated.
- Motion is derived from scene settings and returned decomposition assets.
- The motion blueprint includes:
  - camera movement
  - intensity
  - per-layer parallax
  - scale
  - opacity
  - transition settings

10. Scene state is updated.
- The scene moves through:
  - `queued`
  - `processing`
  - `ready`

11. Playback layer: the project is stitched.
- The playback service reads all current scenes for the project.
- It builds a timeline with:
  - order
  - start times
  - durations
  - overlaps
  - image URLs
  - camera movement
  - intensity
  - layer behaviors
  - fallback state

12. Playback plans are persisted.
- The stitched playback plan is saved as the current playback version for the project.

13. Editor: the user opens the editor.
- The editor loads project and scene data.
- It reflects the scene states while processing continues.

14. Preview: the user opens stitched playback.
- `GET /api/v1/projects/[projectId]/preview/playback`
- The preview controller returns the latest playback plan.

15. Frontend preview consumes the playback plan.
- The preview page normalizes the playback response.
- It renders a stitched vertical scene sequence using timing and image data.

16. User edits feed the loop again.
- Scene updates, reorder, retry, regenerate, uploads, and deletion can re-enter the pipeline.
- The intended long-term editor connection is to keep the editor aligned with this same playback output.

## Layer Responsibilities

### Frontend
- Collect project and scene inputs.
- Upload source images.
- Display scene state, editor state, and preview state.

### API Layer
- Validate requests.
- Enforce access.
- Route uploads, scene creation, preview playback, and scene processing actions.

### Scene And Processing Layer
- Create scenes from finalized uploads.
- Queue and track decomposition jobs.
- Transition scene state through queued, processing, ready, or failed.

### Decomposition Layer
- Push source images into Qwen.
- Receive decomposed layer assets.
- Return provider metadata.

### Motion Layer
- Generate motion blueprints from scene settings and layer structure.
- Define per-layer parallax and movement behavior.

### Playback Layer
- Stitch scenes into one ordered playback plan.
- Support fallback and reduced-motion output.

## Current Engine Truth

The current parallax engine contract is the combination of:
- decomposition assets returned from Qwen
- scene motion blueprints
- stitched playback plans

The preview page already consumes this engine output. The editor should connect to the same output rather than implementing a separate playback model.



================================================
FILE: docs/reference/03-editor-to-parallax-integration-plan.md
================================================
# Editor To Parallax Integration Plan

This document outlines the recommended path for connecting the project editor to the current parallax engine without introducing regressions.

## Goal

Connect the editor to the existing engine contract so the editor can reflect the same stitched playback state already used by the preview page.

## Current State

- The editor saves project and scene fields.
- Motion blueprints are generated in the backend.
- Playback timelines are stitched in the backend.
- The preview page already consumes the stitched playback plan.
- Some editor mutations do not currently restitch playback immediately after save.

## Recommended Integration Direction

Use the existing playback engine API as the single source of truth.

- Do not build a second playback algorithm inside the editor.
- Do not drive the editor preview only from raw scene fields.
- Reuse the stitched playback output already produced by the backend.

## Phased Plan

### Phase 1: Keep playback in sync with editor mutations

1. Restitch after scene edits that affect playback.
- Scene context, motion preset, and motion intensity can affect downstream playback understanding.
- After scene update, trigger playback restitching where appropriate.

2. Restitch after project-level edits when they influence playback.
- If project-wide values become playback-relevant, keep playback regeneration tied to those mutations.

3. Keep existing reorder, delete, retry, regenerate, and upload-triggered stitching intact.
- These are already natural playback update points.

### Phase 2: Expose playback data in the editor

1. Add a playback fetch path in the editor.
- Reuse `/api/v1/projects/[projectId]/preview/playback`.
- Normalize playback data in a shared client helper.

2. Reuse preview normalization logic.
- Avoid duplicating response-shape handling across editor and preview.
- Share image fallback and timeline normalization where possible.

3. Add a lightweight engine preview surface to the editor.
- Start with a read-only stitched preview panel.
- Focus first on the active scene and timing context.

### Phase 3: Improve iteration speed

1. Refresh the embedded engine preview after explicit save.
- Recommended first behavior: save -> restitch -> refresh editor preview.

2. Add debounced refresh later if needed.
- Avoid reprocessing on every keystroke initially.
- Use a controlled, debounced update path only after the stable save-based flow is working.

3. Support reduced-motion and fallback visibility.
- Surface the same playback states already available in preview.

## Proposed User Loop

1. User edits project or scene settings in the editor.
2. User saves.
3. Backend updates scene or project state.
4. Engine regenerates the stitched playback plan.
5. Editor refreshes its embedded playback view.
6. User decides whether to continue editing or open full preview.

## Key Integration Points

### Editor
- `src/features/projects/components/project-editor-page.tsx`

### Scene update route
- `src/interfaces/http/controllers/scene-controller.ts`

### Project update and reorder routes
- `src/interfaces/http/controllers/project-controller.ts`

### Playback controller
- `src/interfaces/http/controllers/preview-controller.ts`

### Motion generation
- `src/modules/motion/service.ts`

### Playback stitching
- `src/modules/playback/service.ts`

## What To Avoid

- Do not fork a separate editor-only engine model.
- Do not patch page layout behavior while implementing engine connectivity.
- Do not trigger expensive backend work on every keystroke in the first iteration.
- Do not bypass the existing processing and playback services.

## Validation Plan

### Functional checks
- Save project and scene changes in the editor.
- Confirm playback updates after save.
- Reorder scenes and confirm stitched order updates.
- Upload new images and confirm new scenes enter the processing pipeline.
- Retry or regenerate scenes and confirm the playback plan updates.

### Playback checks
- Confirm the editor-side preview and full preview route agree on scene order and timing.
- Confirm fallback playback remains usable while some scenes are still processing.
- Confirm reduced-motion playback remains supported.

### Regression checks
- Keep preview page behavior unchanged.
- Keep existing scene processing behavior unchanged.
- Keep route and access-control behavior unchanged.

## Recommended First Implementation

1. Ensure editor mutations restitch playback consistently.
2. Add shared playback normalization utilities.
3. Add a small embedded stitched-preview surface inside the editor.
4. Validate against the existing preview route before adding live/debounced refresh.



================================================
FILE: docs/reference/brainstorm-prd-draft.md
================================================
# PRD Draft

## App Concept

Parallax Story Composer is a vertical-first web application that transforms multiple static images into a stitched parallax scrolling story. Users upload several images, turn each one into a scene, arrange scene order, add context describing what is happening, and generate a dynamic mobile-first preview.

---

## Problem Statement

Creators and marketers often have strong still imagery but lack an easy way to convert those assets into polished motion content for vertical social platforms. Existing workflows usually require video editing, manual compositing, or advanced motion tools. This app reduces that complexity by automating layer decomposition, motion planning, and stitched parallax playback.

---

## Target Users

- Creators making Instagram and TikTok style visual stories
- Social media marketers creating lightweight campaign motion content
- Designers prototyping cinematic motion from still images

---

## Core Features

- Guest or authenticated entry flow
- Multi-image upload in a single project
- One scene created per uploaded image
- Scene building workflow for turning uploads into processed scenes
- Scene manager for ordering, editing, deleting, and regenerating scenes
- Drag-and-drop scene ordering
- Scene-level context input describing content and desired output feel
- Project-level style or story direction
- AI-powered image decomposition into layered RGBA assets
- Motion blueprint generation for each scene
- Scroll engine for stitched vertical playback across all scenes
- Stitched vertical parallax preview in a continuous scrolling experience
- Save and export gated to authenticated users

---

## Supporting Features

- Scene status tracking for upload, processing, ready, and failed states
- Scene storage for originals, thumbnails, layered assets, and playback plans
- Retry and selective regeneration for individual scenes
- User editing interface with portrait scene cards and preview controls
- Mobile-first pinned vertical preview player
- Mobile capability tuning for touch input, responsive playback, and reduced motion
- Reduced motion support
- Guest preview mode with auth gate for save and export

---

## Platform

Web application optimized for vertical social and reel-style playback.

---

## UI / Theme Ideas

- Vertical-first `9:16` preview stage
- Mobile-inspired reel player centered in the interface
- Scene card editor with portrait thumbnails
- Drag-and-drop storyboard workflow
- Clean creator-tool interface focused on upload, sequencing, and preview

---

## Integrations

- Qwen-Image-Layered for layered image decomposition
- S3-compatible object storage for uploaded and generated assets
- Authentication provider for account creation and login
- PostgreSQL for persistent project and scene data
- Job orchestration system for async processing

---

## Data Model Hints

- Users
- Guest sessions
- Projects
- Dashboard views
- Scenes
- Scene thumbnails
- Scene assets
- Scene instructions
- Processing jobs
- Playback plans
- Export records

---

## Product Assumptions and Risks

- Decomposition quality will vary depending on image type and composition
- Portrait-safe framing is critical because the output format is vertical-first
- Mobile performance may degrade if scene count or layer count grows too large
- Async job orchestration is required because inference will not be instant
- Context text should influence motion planning, not direct per-layer semantic control

---

## Recommended MVP Definition

- Format: vertical `9:16`
- Output: interactive browser-based stitched parallax preview
- Upload range: `3-10` images per project
- Layer target: `3-6` ideal, `8` maximum per scene
- Guest access: preview only
- Authenticated access: save, revisit, regenerate, and export
- Scroll engine drives the continuous project timeline
- Scene manager and editing interface are first-class MVP surfaces
- Scene storage differs for guest and authenticated users

---

## Refined MVP Direction

The MVP should focus on a browser-based vertical story composer rather than a video export tool. The core value is turning a sequence of still images into one continuous, stitched parallax experience by combining four logical systems:

- Decomposition service to create layered RGBA assets
- Motion service to generate scene movement blueprints
- Planner service to stitch scene pacing and transitions into one timeline
- Parallax renderer to execute the timeline in a pinned vertical player

---

## MVP Page Architecture

- Product page at `/`
- Authentication page at `/auth`
- Dashboard at `/projects`
- Project editor page at `/editor/[projectId]`
- Preview/player page at `/preview/[projectId]`
- Settings page at `/settings`

The navbar should use:
- `Product`
- `Dashboard`
- `New Project`
- `Settings`

Each created project should route to its own dedicated editor page.



================================================
FILE: docs/reference/prd-draft.md
================================================
# Draft PRD
## Product Name
Parallax Story Composer

## Document Status
Draft

## Product Summary
Parallax Story Composer is a vertical-first web app that turns multiple uploaded static images into one continuous, stitched parallax scrolling experience. Users upload several images, arrange them into scene order, describe what is happening in each scene, and generate a dynamic mobile-first visual story preview. Logged-in users can save projects and export outputs; guests can preview only.

## Problem Statement
Creating motion from static images usually requires advanced editing tools, timeline software, or manual compositing. Most creators do not have an easy way to turn a set of images into a polished, depth-driven, vertically formatted storytelling experience for social platforms.

## Vision
Enable creators to transform still images into immersive vertical parallax stories with minimal manual editing by combining AI-based layer decomposition, motion planning, scene stitching, and a browser-based parallax renderer.

## Goals
- Let users upload multiple images in one session
- Turn each image into an ordered scene
- Allow users to reorder scenes before generation
- Capture scene-level and project-level creative intent through text context
- Decompose images into layered RGBA assets using AI
- Generate motion blueprints for each scene
- Stitch all scenes into one continuous vertical scrolling experience
- Provide a polished interactive preview in the browser
- Require login for save and export capabilities

## Non-Goals
- Full manual layer-by-layer editing in MVP
- Video export in the first release
- Collaborative editing
- Recursive decomposition UI
- Advanced semantic object editing
- WebGL-first rendering architecture

## Target Users
- Content creators making Instagram and TikTok style visual stories
- Social media marketers producing lightweight campaign motion content
- Designers who want a faster way to prototype layered motion from stills

## MVP Success Criteria
- User can upload 3-10 images
- Each image becomes a separate scene
- User can reorder scenes
- User can add context to each scene
- App can process scenes asynchronously into layered assets
- App can generate a stitched vertical parallax preview
- Logged-in users can save projects
- Guests can preview but cannot save or export

## User Types
### Guest User
Can:
- Upload images
- Reorder scenes
- Add scene context
- Generate and preview parallax output

Cannot:
- Save projects
- Export outputs
- Return to projects later

### Authenticated User
Can:
- Do everything a guest can do
- Save projects
- Return to prior projects
- Regenerate scenes
- Export outputs when export is enabled

## Core User Flow
1. User lands on the app
2. User chooses guest mode or logs in
3. User uploads multiple images
4. App creates one scene per image
5. User reorders scenes
6. User adds scene-level context and optional project-level direction
7. Planner queues image decomposition jobs
8. Decomposition service generates RGBA layers for each scene
9. Motion service creates scene motion blueprints
10. Planner stitches scenes into one playback plan
11. Parallax renderer shows one continuous vertical scrolling preview
12. Logged-in users may save and later export

## Functional Requirements

### 1. Authentication and Access
- Support guest mode
- Support account creation and login
- Support persistent saved projects for authenticated users only
- Prevent guest save/export actions
- Show login gate when guest tries to save or export

### 2. Project Creation
- User can create a new project
- Project defaults to vertical `9:16` format
- Project stores:
  - title
  - global context
  - style preset
  - playback plan version

### 3. Multi-Image Upload
- User can upload multiple images at once
- Supported formats: JPG, PNG, WebP
- Each uploaded image becomes a new scene
- Scenes are assigned an initial order automatically
- App generates scene thumbnails after upload

### 4. Scene Management
- User can reorder scenes using drag-and-drop
- User can delete a scene before generation
- User can edit per-scene context text
- User can assign simple motion style/intensity controls
- Scene status must be visible:
  - uploaded
  - queued
  - processing
  - ready
  - failed

### 5. Context Input
- Each scene has a context box describing:
  - what is happening
  - desired feel or emphasis
  - optional motion style
- Project has a global context field describing the full output intent
- Context should influence motion planning, not direct layer semantics

### 6. Decomposition Service
- System must asynchronously process each uploaded image
- AI decomposition must return multiple RGBA layers
- System stores:
  - original image
  - layer assets
  - preview composite
  - layer metadata
- System should support a practical layer range for MVP, ideally 3-6 layers and no more than 8

### 7. Motion Service
- System generates a structured motion blueprint for each scene
- Motion blueprint must include:
  - camera movement type
  - motion intensity
  - per-layer parallax behavior
  - transition hints
- Initial implementation should be rule-based with presets, not fully generative

### 8. Planner and Stitching
- Planner must assemble scenes into one continuous playback plan
- Planner must account for:
  - scene order
  - pacing
  - overlap between scenes
  - transitions
  - continuity of motion intensity
- Planner should support selective regeneration of a single scene without recreating the whole project when possible

### 9. Parallax Renderer
- Renderer must be vertical-first and optimized for `9:16`
- Renderer must use a pinned vertical viewport
- Renderer must stitch scenes into one continuous dynamic scrolling experience
- Renderer must support:
  - layered RGBA scene rendering
  - depth-based motion
  - scene overlap transitions
  - mobile-friendly performance behavior

### 10. Save and Export
- Save is available only to authenticated users
- Export is available only to authenticated users
- Guests can preview only
- MVP may gate export UI if final export implementation lands after preview/save

### 11. Scroll Engine
- The system must include a scroll engine that converts page scroll and touch input into normalized project and scene progress
- The scroll engine must drive a pinned vertical `9:16` viewport for preview playback
- The scroll engine must support continuous stitched playback across multiple scenes rather than isolated scene playback
- The scroll engine must support scene overlap windows, transition timing, and smooth progression through the full project timeline

### 12. Scene Manager
- The application must include a scene manager responsible for creating, ordering, editing, deleting, and regenerating scenes within a project
- The scene manager must display portrait-oriented scene cards with status, thumbnail, context, and motion settings
- The scene manager must allow drag-and-drop ordering and preserve the final order in the planner playback plan
- The scene manager must support per-scene retry and selective regeneration after failed processing

### 13. Mobile Capabilities
- The application must be optimized first for mobile vertical use cases and reel-style viewing
- The preview player must support touch-friendly controls, responsive layout behavior, and stable portrait playback
- The system must degrade gracefully on lower-powered mobile devices by reducing active layers, motion intensity, or asset resolution as needed
- The application must support reduced-motion playback behavior on mobile and desktop

### 14. Scene Building Workflow
- Each uploaded image must be converted into a scene record with source media, thumbnail, context, framing data, and processing status
- Scene building must include decomposition, layer asset generation, motion blueprint creation, and final stitching into the project playback plan
- The system must preserve portrait-safe framing information for every scene to ensure consistent `9:16` playback
- The system should support rebuilding only the affected scene when user edits require regeneration

### 15. Scene Storage
- The system must store original uploads, generated thumbnails, layered assets, metadata, and playback plans
- Authenticated users must receive persistent project and scene storage
- Guest projects must use temporary storage with automatic expiration
- Scene storage must preserve versioned playback plans and generated assets so saved projects can be reopened accurately

### 16. User Editing Interface
- The application must provide a scene-based editing interface for upload, sequencing, context entry, motion selection, and preview
- The editing interface must include project-wide settings and per-scene controls
- The editing interface must surface processing state, validation errors, and retry actions clearly
- The editing interface must show the same portrait-oriented framing model used by the final renderer to avoid mismatches between editing and playback

### 17. Export Capabilities
- The product must reserve export as an authenticated-only capability
- The MVP must support export gating in the user interface even if final export implementation lands after the first preview/save release
- Export workflows must use the stitched project playback plan rather than isolated scene outputs
- Export scope after MVP may include downloadable stitched media or rendered outputs, but the first release should prioritize preview and save readiness

## Non-Functional Requirements

### Performance
- Optimize for mobile-first vertical playback
- Animate only transform and opacity in renderer
- Preload current, previous, and next scenes only
- Keep active layer count low enough for smooth playback
- Limit projects to manageable scene counts in MVP
- Keep the scroll engine and scene stitching smooth on mobile-first hardware targets

### Reliability
- All AI processing must be asynchronous
- Jobs must support retries, timeout handling, and failure states
- App must not block the entire project if one scene fails; it should surface the failure and allow retry

### Cost Control
- Limit scene count and image size in MVP
- Limit guest retention and guest processing usage
- Expire guest project assets automatically
- Avoid unnecessary reprocessing of unchanged scenes

### Security
- Authenticate save/export endpoints
- Restrict project access by owner
- Protect uploaded assets and generated outputs
- Never expose direct privileged storage credentials to clients

### Accessibility
- Support reduced motion mode in preview
- Ensure core UI is keyboard accessible
- Preserve readable controls on mobile and desktop

## Recommended Technical Architecture

### Frontend
- Next.js
- React
- TypeScript
- Tailwind CSS
- Zustand
- dnd-kit
- Framer Motion
- zod

### Backend
- Next.js server routes or Node backend
- PostgreSQL
- Prisma
- Trigger.dev or Inngest
- S3-compatible storage

### AI / Processing
- Python GPU service
- Qwen-Image-Layered for decomposition
- Rule-based motion engine in backend for MVP

### Renderer
- Custom DOM/CSS transform runtime
- requestAnimationFrame-driven updates
- Pinned vertical `9:16` stage
- Browser-based interactive playback

## Core Data Model

### User
- id
- email
- auth_provider
- created_at

### Project
- id
- owner_id nullable for guest
- title
- global_context
- style_preset
- output_format
- status
- scroll_engine_version
- created_at
- updated_at

### Scene
- id
- project_id
- order_index
- source_image_url
- thumbnail_url
- context_text
- motion_preset
- motion_intensity
- status
- framing_data
- mobile_render_hints
- created_at
- updated_at

### SceneAsset
- id
- scene_id
- asset_type
- asset_url
- width
- height
- layer_order
- metadata_json

### ProcessingJob
- id
- scene_id
- job_type
- status
- attempt_count
- error_message
- started_at
- completed_at

### PlaybackPlan
- id
- project_id
- version
- timeline_json
- export_status
- created_at

## MVP Page Architecture

The MVP requires six core application pages to function properly. These pages support guest preview workflows, authenticated save and export workflows, and authenticated account and preferences management.

### 1. Landing Page
**Route:** `/`

**Purpose:**
Introduce the product, explain the value proposition, and let users begin as a guest or authenticate.

**Navbar Label:**
`Product`

**Key Functions:**
- Product overview
- Call to action to start a new project
- Guest entry option
- Sign up and log in entry points
- High-level explanation of save and export gating

**Primary Components:**
- Hero section
- Product explainer
- CTA buttons
- Authentication entry actions

### 2. Authentication Page
**Route:** `/auth`

**Purpose:**
Allow users to create an account or log in so they can save, revisit, and export projects.

**Key Functions:**
- Sign up
- Log in
- Session creation
- Return user to intended workflow after auth

**Primary Components:**
- Sign up form
- Log in form
- Auth state messaging
- Redirect handling

### 3. Project Editor Page
**Route:** `/editor/[projectId]`

**Purpose:**
Serve as the main workspace for building a parallax story project.

**Key Functions:**
- Multi-image upload
- Scene creation from uploaded images
- Scene manager with drag-and-drop ordering
- Scene context editing
- Project-wide style and output settings
- Scene processing state display
- Save gating for authenticated users
- Launch preview flow

**Primary Components:**
- Upload area
- Scene manager
- Scene cards
- Context input fields
- Motion and style controls
- Processing status UI
- Save and preview actions

### 4. Preview / Player Page
**Route:** `/preview/[projectId]`

**Purpose:**
Display the stitched vertical parallax experience in a dedicated playback environment.

**Key Functions:**
- Render the full stitched playback plan
- Drive the scroll engine
- Display continuous scene-to-scene transitions
- Support mobile-first `9:16` preview behavior
- Support reduced motion behavior

**Primary Components:**
- Pinned vertical stage
- Scroll engine runtime
- Scene renderer
- Transition layer
- Playback controls or return-to-editor action

### 5. Saved Projects Dashboard
**Route:** `/projects`

**Purpose:**
Allow authenticated users to view and reopen saved projects.

**Navbar Label:**
`Dashboard`

**Key Functions:**
- List saved projects
- Show project status and last updated time
- Open existing project in editor
- Open project preview
- Surface export access when available
- Create a new project from the dashboard and route directly to its dedicated editor page

**Primary Components:**
- Project list or grid
- Search or sorting controls
- Status indicators
- Open and edit actions
- Export entry points

### 6. Settings Page
**Route:** `/settings`

**Purpose:**
Allow authenticated users to manage account details and app preferences.

**Navbar Label:**
`Settings`

**Key Functions:**
- View and edit account details
- Manage default reduced motion behavior
- Manage default story pace
- Manage default transition style
- Manage default motion preset
- Sign out of the current session

**Primary Components:**
- Account information form
- Preferences panel
- Locked output format display
- Session actions

## Optional Future Pages

The following pages are not required for the MVP but may be added later as the app grows.

### Project Detail Page
**Route:** `/projects/[projectId]`

Used for separating project metadata, preview access, history, and export actions from the editor.

### Export Page
**Route:** `/export/[projectId]`

Used if export becomes a more advanced workflow with format selection, queueing, delivery state, and download history.

## Page Architecture Recommendation

The MVP should launch with six core pages:
- Landing page
- Authentication page
- Saved projects dashboard
- Project editor page
- Preview and player page
- Settings page

The global navbar should use these labels:
- `Product` -> `/`
- `Dashboard` -> `/projects`
- `New Project` -> creates a project and routes to `/editor/[projectId]`
- `Settings` -> `/settings`

This page structure is sufficient for:
- guest preview workflows
- authenticated save workflows
- scene building and editing
- stitched parallax playback
- future export expansion

## Page-by-Page Product Flow

This section defines how users move through the MVP experience and how each page contributes to the core workflow.

### 1. Landing Page Product Flow

The landing page is the product entry point and must move users quickly into project creation.

It also functions as the `Product` destination in the global navbar.

**Primary User Journey:**
1. User arrives on the home page
2. User reads the core value proposition
3. User chooses whether to continue as a guest or authenticate
4. User starts a new project and enters the editor flow

**Primary Actions and Effects:**
- `Start Free as Guest`
  - Creates a temporary guest session
  - Creates or prepares a temporary project context
  - Routes user into the editor workflow
- `Create Account`
  - Routes user to the authentication page in sign-up mode
- `Log In`
  - Routes user to the authentication page in login mode
- `See How It Works`
  - Scrolls to an explainer section showing the upload, scene build, and preview workflow

**Business Purpose:**
- Convert visitors into active project creators
- Clearly communicate that preview is available to guests while save and export require login

### 2. Authentication Page Product Flow

The authentication page unlocks persistence, project ownership, and export rights.

**Primary User Journey:**
1. User enters sign-up or login flow
2. User completes authentication
3. App creates an authenticated session
4. User is returned to the intended destination, such as the editor or dashboard

**Primary Actions and Effects:**
- `Create Account`
  - Creates a user record
  - Starts an authenticated session
  - Redirects user to the next intended page
- `Log In`
  - Authenticates the user
  - Loads owned projects and permissions
  - Redirects user to the next intended page
- `Back to Product`
  - Returns user to the landing page at `/` without authenticating

**Business Purpose:**
- Gate save and export capabilities behind authenticated ownership
- Support a low-friction guest-to-account conversion path

### 3. Project Editor Page Product Flow

The project editor is the main production workspace where scenes are created, managed, and prepared for generation.

**Primary User Journey:**
1. User enters a project
2. User uploads multiple images
3. App creates one scene per image
4. User reorders scenes and adds context
5. User adjusts project-wide and scene-level settings
6. User triggers generation for new or changed scenes
7. User reviews processing status and moves to preview

**Primary Actions and Effects:**
- `Upload Images`
  - Opens file picker for multiple images
  - Creates scene records from uploaded files
  - Generates thumbnails and initial ordering
- `Add More Images`
  - Appends new scenes to the project
- `Select Scene`
  - Loads the selected scene into the editing panel
- `Drag Handle`
  - Reorders scenes
  - Updates scene order and marks the playback plan stale
- `Delete Scene`
  - Removes the scene from the project and triggers a future restitch
- `Scene Context Box`
  - Captures scene-specific intent
  - Marks the scene dirty for motion and planning updates
- `Motion Preset`
  - Assigns a scene motion style such as cinematic or ambient
- `Motion Intensity`
  - Adjusts movement strength for the scene
- `Project Context`
  - Captures overall output direction for the full story
- `Generate`
  - Queues decomposition and motion processing for all dirty or unprocessed scenes
- `Save Project`
  - Saves current state for authenticated users
  - Opens auth gate for guests
- `Preview`
  - Routes user to the player page using the latest available playback plan or preview state
- `Export`
  - Opens export flow for authenticated users when supported
  - Opens auth gate for guests
- `Retry` or `Regenerate Scene`
  - Requeues an individual scene for decomposition and motion generation

**Business Purpose:**
- Provide a single workspace for upload, sequencing, authoring, and generation
- Make scene management and editing intuitive enough for non-technical creators

### 4. Preview and Player Page Product Flow

The preview page presents the final stitched parallax output in a dedicated vertical playback environment.

**Primary User Journey:**
1. User opens preview from the editor or dashboard
2. App loads the latest playback plan
3. User scrolls through or restarts the stitched parallax experience
4. User decides whether to return to editing, save, or export

**Primary Actions and Effects:**
- `Back to Editor`
  - Returns user to the project editor
- `Restart Preview`
  - Resets playback to the beginning of the stitched timeline
- `Reduce Motion`
  - Enables lower-motion playback mode for accessibility and performance
- `Save`
  - Saves project state for authenticated users
  - Opens auth gate for guests
- `Export`
  - Opens export flow for authenticated users when export is available
  - Opens auth gate for guests

**Business Purpose:**
- Let users experience the final stitched narrative in the same vertical format it is designed for
- Create a clear decision point for saving, revising, or exporting

### 5. Saved Projects Dashboard Product Flow

The saved projects dashboard supports project retrieval, resumption, and ongoing management for authenticated users.

It functions as the `Dashboard` destination in the global navbar.

**Primary User Journey:**
1. Authenticated user enters the dashboard
2. User sees saved projects and their statuses
3. User opens a project in the editor or preview
4. User manages or deletes saved work

**Primary Actions and Effects:**
- `New Project`
  - Creates a new authenticated project and routes to that project's dedicated editor page at `/editor/[projectId]`
- `Open Editor`
  - Opens the selected project in the editor workspace
- `Preview`
  - Opens the selected project's player page
- `Export`
  - Starts export flow when supported and permitted
- `Delete Project`
  - Removes the project after confirmation
- `Sort` or `Filter`
  - Changes project list ordering or visibility

**Business Purpose:**
- Give authenticated users a persistent home for project management
- Reinforce the value of account creation beyond guest preview mode

### 6. Settings Page Product Flow

The settings page supports account maintenance and app-wide preference management for authenticated users.

It functions as the `Settings` destination in the global navbar.

**Primary User Journey:**
1. Authenticated user opens settings
2. User reviews account details
3. User updates default preferences
4. User saves changes or resets defaults
5. User returns to dashboard or project work with updated defaults applied to future workflows

**Primary Actions and Effects:**
- `Save Changes`
  - Persists account and preferences updates
- `Reset Defaults`
  - Restores preference values to system defaults
- `Sign Out`
  - Ends the current authenticated session

**Business Purpose:**
- Separate account and preferences management from project workflows
- Give users control over default creative behavior across the app

## Cross-Page Workflow Summary

The complete MVP product flow should behave as follows:

1. User enters through the landing page
2. User chooses guest mode or authentication
3. User creates a project in the editor
4. User uploads images and builds scenes
5. User triggers generation for decomposition and motion planning
6. Planner stitches the scenes into a playback plan
7. User reviews the result in the preview player
8. Guest users can preview only, while authenticated users can save, revisit, and export when available

## Global Navigation Routing

- `Product` routes to `/` and serves as the landing and marketing page
- `Dashboard` routes to `/projects` and serves as the project hub where users continue existing work or create new projects
- `New Project` creates a new project and routes immediately to `/editor/[projectId]`
- `Settings` routes to `/settings` and contains account and preferences only in the MVP
- Each created project has its own dedicated editor route at `/editor/[projectId]`

## MVP Constraints
- Vertical `9:16` format only
- 3-10 images per project
- 3-6 ideal layers per scene
- 8 layers maximum per scene
- Guest preview only
- No video export in first release
- No advanced layer editing in first release

## Risks
- Layer decomposition quality may vary by input image
- Landscape images may not frame well in portrait output without good focal handling
- Mobile performance may degrade if scene/layer counts exceed budget
- AI processing latency may impact UX if queueing is not well designed

## Risk Mitigations
- Restrict supported image types and size ranges
- Add fallback behavior for weak decomposition
- Cap scenes and layers
- Surface processing states clearly
- Use async jobs with retries and status tracking
- Start with deterministic motion presets and constrained transitions

## Open Questions
- Whether authenticated users can claim an in-progress guest project
- Exact export format for post-MVP release
- Whether save requires login before generation or only before persistence
- Whether project sharing should be supported after MVP

## Launch Scope
MVP launches as an interactive browser-based vertical parallax story composer with guest preview and authenticated save/export gating.



================================================
FILE: docs/reference/project-state.md
================================================
# PROJECT STATE

## Lifecycle Phases

- Brainstorm
- Classified
- Framework Generated
- PRD Approved
- Architecture Approved
- Plan Approved
- Implementation
- Validation

---

## Current Phase

Current Phase:
Brainstorm

---

## Locked Artifacts

PRD Version:
<<PRD_VERSION>>

Architecture Version:
<<ARCH_VERSION>>

Plan Version:
<<PLAN_VERSION>>

Framework Version:
<<FRAMEWORK_VERSION>>

---

## Governance Status

Architecture Validated:
<<ARCH_VALIDATED>>

Drift Check Passed:
<<DRIFT_CHECK>>

---

## Last Updated

2026-03-15



================================================
FILE: docs/rules/architecture-rules.md
================================================
# ARCHITECTURE GOVERNANCE – BASE RULES

These rules apply to ALL applications regardless of system type.

They cannot be overridden by rule packs.

---

# 1. Layered Architecture Enforcement

Applications must follow strict layering:

Presentation Layer
→ Service Layer
→ Repository Layer
→ Infrastructure Layer

Rules:

- No business logic in controllers or route handlers.
- Services may call repositories.
- Repositories may not call services.
- Infrastructure may not contain business logic.
- No circular dependencies between modules.

---

# 2. Feature-Based Modularity

All domain features must be isolated.

Each feature must contain:

- service
- repository
- schema/model
- validation
- types

Rules:

- No cross-feature direct imports.
- Shared logic must live in /core.
- Features must be independently testable.

---

# 3. Configuration Management

- No direct access to environment variables outside /config.
- Config must be strongly typed.
- Secrets must never be committed.
- Separate configs for dev, staging, prod.

---

# 4. Error Handling Standards

- Centralized error middleware required.
- Structured error format enforced.
- No raw stack traces exposed to clients.
- All errors must be logged.

---

# 5. Logging & Observability

- Structured JSON logging required.
- Correlation ID per request.
- Health check endpoint required.
- Application must expose readiness & liveness probes.

---

# 6. Database Standards

- UUID primary keys.
- created_at / updated_at required.
- Foreign keys indexed.
- Migrations required for schema changes.
- Rollback strategy must be documented.

---

# 7. API Standards

- Versioned routes (/api/v1).
- Input validation required before service layer.
- Explicit error responses.
- Rate limiting defined.

---

# 8. Testing Discipline

- Service layer unit tests required.
- Critical flows integration tested.
- No feature considered complete without validation.

---

# 9. Prohibited Patterns

- Business logic in controllers.
- Global mutable state.
- Silent error swallowing.
- Tight coupling between modules.
- Hardcoded secrets.
- Direct DB access from presentation layer.

---

# 10. Architectural Drift Prevention

- Architecture must be revalidated after major feature additions.
- Any violation must trigger governance update.



================================================
FILE: docs/setup/local-mvp.md
================================================
# Local MVP Setup

This project runs the MVP locally with Next.js, PostgreSQL, Prisma, and filesystem-backed asset storage.

## Minimum Required Environment Values

Copy `.env.example` to `.env` and set at least these values:

- `DATABASE_URL`: PostgreSQL connection string used by Prisma
- `NEXTAUTH_SECRET`: secret for session signing
- `NEXTAUTH_URL`: local app URL, usually `http://localhost:3000`
- `INTERNAL_UPLOAD_TOKEN_SECRET`: upload contract signing secret
- `LOCAL_STORAGE_ROOT`: local directory for uploaded originals and generated assets

Optional for MVP:

- `GOOGLE_CLIENT_ID` and `GOOGLE_CLIENT_SECRET`: leave blank unless Google auth is enabled
- `QWEN_API_URL` and `QWEN_API_KEY`: leave blank when using `QWEN_MOCK_MODE=true`
- `INTERNAL_MAINTENANCE_TOKEN`: required only to call internal maintenance endpoints manually

## Environment Reference

These are the runtime values currently parsed in `src/config/env.ts`.

### Core App

- `DATABASE_URL`: PostgreSQL connection string
- `NEXTAUTH_SECRET`: NextAuth session secret; must be set in production
- `NEXTAUTH_URL`: public app URL used by auth flows
- `LOCAL_STORAGE_ROOT`: local filesystem root for uploaded and generated assets
- `LOG_LEVEL`: Pino log level
- `NODE_ENV`: `development`, `test`, or `production`

### Auth And Guest Access

- `GOOGLE_CLIENT_ID`: optional Google auth provider id
- `GOOGLE_CLIENT_SECRET`: optional Google auth provider secret
- `GUEST_SESSION_COOKIE_NAME`: cookie key used for guest sessions
- `GUEST_SESSION_TTL_HOURS`: guest session lifetime before cleanup and claim expiration rules apply
- `GUEST_MAX_PROJECTS`: max unclaimed guest projects per guest session
- `GUEST_MAX_SCENES_PER_PROJECT`: max scenes allowed per project in the MVP

Google auth is optional. If you enable it, set both Google env vars together; a partial configuration now fails fast.

### Uploads And Internal Operations

- `UPLOAD_MAX_FILES`: max upload batch size
- `UPLOAD_MAX_FILE_SIZE_BYTES`: max size per uploaded file
- `UPLOAD_ALLOWED_MIME_TYPES`: comma-separated allowlist for upload MIME types
- `INTERNAL_UPLOAD_TOKEN_SECRET`: HMAC secret used to sign upload contracts
- `INTERNAL_MAINTENANCE_TOKEN`: bearer-style header token for manual maintenance endpoints

### Processing And Qwen

- `QWEN_API_URL`: real provider base URL
- `QWEN_API_KEY`: real provider API key
- `QWEN_MODEL`: provider model id
- `QWEN_TIMEOUT_MS`: request timeout for provider calls
- `QWEN_MAX_RETRIES`: retry count for provider requests
- `QWEN_MOCK_MODE`: when `true`, local mock decomposition stays enabled and provider credentials may stay blank
- `PROCESSING_JOB_TIMEOUT_MS`: max queued/processing job age before recovery marks it failed
- `PROCESSING_CANARY_PERCENT`: rollout percentage for processing behavior

### Feature Flags

- `FEATURE_MOTION_PIPELINE`: toggle motion pipeline behavior
- `FEATURE_PLAYBACK_PIPELINE`: toggle playback plan generation behavior
- `FEATURE_PREVIEW_FALLBACKS`: allow preview fallbacks when scenes are only partially ready
- `FEATURE_REDUCED_MOTION_PREVIEW`: enable reduced-motion playback plans

### Rate Limiting

- `RATE_LIMIT_WINDOW_MS`: request bucket window size
- `RATE_LIMIT_MAX_REQUESTS`: request count allowed per window

The current limiter is in-memory (`src/infrastructure/rate-limit/memory-rate-limiter.ts`). That is acceptable for single-instance local development and a small single-instance MVP deployment, but it is not suitable for horizontally scaled production because limits are not shared across instances and reset on restart.

## PostgreSQL Bootstrapping

1. Start PostgreSQL locally.
2. Create a database named `parallax_story_composer` or update `DATABASE_URL`.
3. Install dependencies:

```bash
npm install
```

4. Apply Prisma migrations and generate the Prisma client:

```bash
npx prisma migrate deploy
npx prisma generate
```

For a fresh local database during development, `npx prisma migrate dev` is also acceptable.

## Launching The App

Run the dev server:

```bash
npm run dev
```

Open `http://localhost:3000`.

## Qwen Modes

### Mock Mode

Use this for local MVP work:

- Set `QWEN_MOCK_MODE=true`
- Leave `QWEN_API_URL` and `QWEN_API_KEY` blank
- Upload images, finalize scenes, generate outputs, and preview using the local mock path

### Real Provider Mode

Use this only when provider credentials are available:

- Set `QWEN_MOCK_MODE=false`
- Set `QWEN_API_URL`, `QWEN_API_KEY`, and optionally override `QWEN_MODEL`
- Keep the same upload, finalize, and preview flow; only the decomposition provider changes

## Local Asset Storage

- Uploaded originals are written under `LOCAL_STORAGE_ROOT/projects/<projectId>/incoming/*`
- Generated thumbnails, composites, layers, and manifests are written under `LOCAL_STORAGE_ROOT/projects/<projectId>/scenes/<sceneId>/v<generationVersion>/*`
- Assets are served back through `GET /api/v1/assets/<storage-path>`

This makes the mock Qwen path usable end-to-end locally: upload images, finalize scenes, generate decomposition outputs, and preview stitched playback with real renderable asset URLs.

## Health And Readiness Checks

- Liveness: `GET /api/v1/health/live`
- Readiness: `GET /api/v1/health/ready`

The readiness endpoint returns `503` when env parsing fails or PostgreSQL is unavailable.

## Manual Maintenance Endpoints

These endpoints now require the `x-internal-maintenance-token` header to match `INTERNAL_MAINTENANCE_TOKEN`:

- `POST /api/v1/internal/maintenance/cleanup`
- `POST /api/v1/internal/maintenance/recover-timeouts`

Example:

```bash
curl -X POST http://localhost:3000/api/v1/internal/maintenance/cleanup \
  -H "x-internal-maintenance-token: $INTERNAL_MAINTENANCE_TOKEN"
```

For the MVP, these endpoints are treated as manual operations rather than a scheduled background job. Trigger them explicitly from a trusted internal environment until scheduled infrastructure exists.

## Guest And Asset Lifecycle

- Guest sessions expire after `GUEST_SESSION_TTL_HOURS`
- Unclaimed guest projects inherit the guest session expiry and are deleted by maintenance cleanup after expiration
- Uploaded originals, thumbnails, generated layers, composites, manifests, and playback plans should be treated as guest-scoped assets when attached to an expiring guest project
- Claiming a guest project clears project expiration and moves ownership to the authenticated user
- Timed-out processing jobs are recovered by `recover-timeouts`, which marks them failed so the editor and preview can represent the real state

## Recommended Validation

```bash
npm run lint
npm test
npm run build
```

Narrow validation commands that are useful while iterating:

```bash
curl http://localhost:3000/api/v1/health/live
curl http://localhost:3000/api/v1/health/ready
npx vitest run tests/unit/modules/uploads/service.test.ts
npx vitest run tests/unit/modules/projects/service.test.ts
```



================================================
FILE: docs/setup/mvp-decision-log.md
================================================
# MVP Decision Log

This log captures the current implementation choices used to close parallel system tickets without reopening scope on every pass.

## Product Decisions

- `Dashboard route`: `/projects` is the canonical dashboard. Do not introduce a separate `/dashboard` route for the MVP.
- `Preview model`: the MVP uses the current stitched vertical player in `src/features/preview/components/project-preview-page.tsx`, not a true pinned scroll engine.
- `Settings scope`: `/settings` remains a deferred informational page for MVP content, but it is included in primary navigation as a discoverable route.
- `Google auth`: optional, not required for launch. Credentials auth is the default path unless both Google provider secrets are configured.
- `Export`: keep visible only as an explicit unavailable or coming-soon state. Do not imply working export flows.
- `Dashboard mock fallbacks`: remove mock dashboard behavior in core user flows rather than replacing it with an implicit demo mode.

## Operational Decisions

- `Maintenance execution`: internal maintenance endpoints are manually triggered for the MVP and require `x-internal-maintenance-token`.
- `Rate limiting`: the in-memory limiter is acceptable only for local development and single-instance MVP deployment.
- `Guest lifecycle`: unclaimed guest sessions, guest projects, and guest-scoped assets follow the guest expiration window and should be cleaned up together.

## UX Guidance

- Prefer copy that describes uploads, scene editing, stitched preview, guest claiming, and authenticated ownership.
- Avoid copy that promises production export, advanced keyframing, true scroll-engine playback, or hidden routes not present in `src/app/**/page.tsx`.



================================================
FILE: prisma/schema.prisma
================================================
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

enum AuthProvider {
  credentials
  google
}

enum ProjectStatus {
  draft
  ready
  archived
}

enum SceneStatus {
  uploaded
  queued
  processing
  ready
  failed
}

enum AssetType {
  original
  thumbnail
  layer
  composite
  manifest
}

enum JobType {
  decomposition
  motion
  stitching
}

enum JobStatus {
  queued
  processing
  ready
  failed
}

enum ExportStatus {
  pending
  locked
  ready
  failed
}

model User {
  id           String       @id @default(uuid()) @db.Uuid
  email        String       @unique
  authProvider AuthProvider @map("auth_provider")
  passwordHash String?      @map("password_hash")
  projects     Project[]
  createdAt    DateTime     @default(now()) @map("created_at")
  updatedAt    DateTime     @updatedAt @map("updated_at")

  @@map("users")
}

model GuestSession {
  id              String    @id @default(uuid()) @db.Uuid
  expiresAt       DateTime  @map("expires_at")
  claimedAt       DateTime? @map("claimed_at")
  claimedByUserId String?   @db.Uuid @map("claimed_by_user_id")
  lastSeenAt      DateTime  @default(now()) @map("last_seen_at")
  projects        Project[]
  createdAt       DateTime  @default(now()) @map("created_at")
  updatedAt       DateTime  @updatedAt @map("updated_at")

  @@index([expiresAt])
  @@index([claimedByUserId])
  @@map("guest_sessions")
}

model Project {
  id                  String         @id @default(uuid()) @db.Uuid
  ownerId             String?        @db.Uuid @map("owner_id")
  guestSessionId      String?        @db.Uuid @map("guest_session_id")
  title               String
  globalContext       String?        @map("global_context")
  stylePreset         String?        @map("style_preset")
  outputFormat        String         @default("9:16") @map("output_format")
  status              ProjectStatus  @default(draft)
  scrollEngineVersion String?        @map("scroll_engine_version")
  expiresAt           DateTime?      @map("expires_at")
  claimedAt           DateTime?      @map("claimed_at")
  claimedByUserId     String?        @db.Uuid @map("claimed_by_user_id")
  owner               User?          @relation(fields: [ownerId], references: [id])
  guestSession        GuestSession?  @relation(fields: [guestSessionId], references: [id])
  scenes              Scene[]
  playbackPlans       PlaybackPlan[]
  createdAt           DateTime       @default(now()) @map("created_at")
  updatedAt           DateTime       @updatedAt @map("updated_at")

  @@index([ownerId])
  @@index([guestSessionId])
  @@index([status])
  @@index([expiresAt])
  @@index([claimedByUserId])
  @@map("projects")
}

model Scene {
  id                String       @id @default(uuid()) @db.Uuid
  projectId         String       @db.Uuid @map("project_id")
  orderIndex        Int          @map("order_index")
  generationVersion Int          @default(1) @map("generation_version")
  sourceImageUrl    String?      @map("source_image_url")
  thumbnailUrl      String?      @map("thumbnail_url")
  contextText       String?      @map("context_text")
  motionPreset      String?      @map("motion_preset")
  motionIntensity   String?      @map("motion_intensity")
  motionBlueprintJson Json?      @map("motion_blueprint_json")
  status            SceneStatus  @default(uploaded)
  framingData       Json?        @map("framing_data")
  mobileRenderHints Json?        @map("mobile_render_hints")
  expiresAt         DateTime?    @map("expires_at")
  project           Project      @relation(fields: [projectId], references: [id])
  assets            SceneAsset[]
  processingJobs    ProcessingJob[]
  createdAt         DateTime     @default(now()) @map("created_at")
  updatedAt         DateTime     @updatedAt @map("updated_at")

  @@index([projectId])
  @@index([status])
  @@unique([projectId, orderIndex])
  @@map("scenes")
}

model SceneAsset {
  id           String    @id @default(uuid()) @db.Uuid
  sceneId      String    @db.Uuid @map("scene_id")
  assetType    AssetType @map("asset_type")
  assetUrl     String    @map("asset_url")
  width        Int?
  height       Int?
  layerOrder   Int?      @map("layer_order")
  metadataJson Json?     @map("metadata_json")
  expiresAt    DateTime? @map("expires_at")
  scene        Scene     @relation(fields: [sceneId], references: [id])
  createdAt    DateTime  @default(now()) @map("created_at")
  updatedAt    DateTime  @updatedAt @map("updated_at")

  @@index([sceneId])
  @@index([assetType])
  @@map("scene_assets")
}

model ProcessingJob {
  id           String    @id @default(uuid()) @db.Uuid
  sceneId      String    @db.Uuid @map("scene_id")
  jobType      JobType   @map("job_type")
  status       JobStatus @default(queued)
  providerJobId String?  @map("provider_job_id")
  correlationId String?  @map("correlation_id")
  attemptCount Int       @default(0) @map("attempt_count")
  errorMessage String?   @map("error_message")
  metadataJson  Json?    @map("metadata_json")
  startedAt    DateTime? @map("started_at")
  completedAt  DateTime? @map("completed_at")
  scene        Scene     @relation(fields: [sceneId], references: [id])
  createdAt    DateTime  @default(now()) @map("created_at")
  updatedAt    DateTime  @updatedAt @map("updated_at")

  @@index([sceneId])
  @@index([status])
  @@index([sceneId, jobType, status])
  @@map("processing_jobs")
}

model PlaybackPlan {
  id           String       @id @default(uuid()) @db.Uuid
  projectId    String       @db.Uuid @map("project_id")
  version      Int          @default(1)
  timelineJson Json         @map("timeline_json")
  isReducedMotion Boolean   @default(false) @map("is_reduced_motion")
  isFallback      Boolean   @default(false) @map("is_fallback")
  exportStatus ExportStatus @default(pending) @map("export_status")
  project      Project      @relation(fields: [projectId], references: [id])
  createdAt    DateTime     @default(now()) @map("created_at")
  updatedAt    DateTime     @updatedAt @map("updated_at")

  @@index([projectId])
  @@map("playback_plans")
}



================================================
FILE: prisma/migrations/20260316000000_init/migration.sql
================================================
CREATE TYPE "AuthProvider" AS ENUM ('credentials', 'google');
CREATE TYPE "ProjectStatus" AS ENUM ('draft', 'ready', 'archived');
CREATE TYPE "SceneStatus" AS ENUM ('uploaded', 'queued', 'processing', 'ready', 'failed');
CREATE TYPE "AssetType" AS ENUM ('original', 'thumbnail', 'layer', 'composite', 'manifest');
CREATE TYPE "JobType" AS ENUM ('decomposition', 'motion', 'stitching');
CREATE TYPE "JobStatus" AS ENUM ('queued', 'processing', 'ready', 'failed');
CREATE TYPE "ExportStatus" AS ENUM ('pending', 'locked', 'ready', 'failed');

CREATE TABLE "users" (
  "id" UUID NOT NULL,
  "email" TEXT NOT NULL,
  "auth_provider" "AuthProvider" NOT NULL,
  "password_hash" TEXT,
  "created_at" TIMESTAMPTZ NOT NULL DEFAULT CURRENT_TIMESTAMP,
  "updated_at" TIMESTAMPTZ NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT "users_pkey" PRIMARY KEY ("id")
);

CREATE TABLE "guest_sessions" (
  "id" UUID NOT NULL,
  "expires_at" TIMESTAMPTZ NOT NULL,
  "claimed_at" TIMESTAMPTZ,
  "claimed_by_user_id" UUID,
  "last_seen_at" TIMESTAMPTZ NOT NULL DEFAULT CURRENT_TIMESTAMP,
  "created_at" TIMESTAMPTZ NOT NULL DEFAULT CURRENT_TIMESTAMP,
  "updated_at" TIMESTAMPTZ NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT "guest_sessions_pkey" PRIMARY KEY ("id")
);

CREATE TABLE "projects" (
  "id" UUID NOT NULL,
  "owner_id" UUID,
  "guest_session_id" UUID,
  "title" TEXT NOT NULL,
  "global_context" TEXT,
  "style_preset" TEXT,
  "output_format" TEXT NOT NULL DEFAULT '9:16',
  "status" "ProjectStatus" NOT NULL DEFAULT 'draft',
  "scroll_engine_version" TEXT,
  "expires_at" TIMESTAMPTZ,
  "claimed_at" TIMESTAMPTZ,
  "claimed_by_user_id" UUID,
  "created_at" TIMESTAMPTZ NOT NULL DEFAULT CURRENT_TIMESTAMP,
  "updated_at" TIMESTAMPTZ NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT "projects_pkey" PRIMARY KEY ("id")
);

CREATE TABLE "scenes" (
  "id" UUID NOT NULL,
  "project_id" UUID NOT NULL,
  "order_index" INTEGER NOT NULL,
  "generation_version" INTEGER NOT NULL DEFAULT 1,
  "source_image_url" TEXT,
  "thumbnail_url" TEXT,
  "context_text" TEXT,
  "motion_preset" TEXT,
  "motion_intensity" TEXT,
  "motion_blueprint_json" JSONB,
  "status" "SceneStatus" NOT NULL DEFAULT 'uploaded',
  "framing_data" JSONB,
  "mobile_render_hints" JSONB,
  "expires_at" TIMESTAMPTZ,
  "created_at" TIMESTAMPTZ NOT NULL DEFAULT CURRENT_TIMESTAMP,
  "updated_at" TIMESTAMPTZ NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT "scenes_pkey" PRIMARY KEY ("id")
);

CREATE TABLE "scene_assets" (
  "id" UUID NOT NULL,
  "scene_id" UUID NOT NULL,
  "asset_type" "AssetType" NOT NULL,
  "asset_url" TEXT NOT NULL,
  "width" INTEGER,
  "height" INTEGER,
  "layer_order" INTEGER,
  "metadata_json" JSONB,
  "expires_at" TIMESTAMPTZ,
  "created_at" TIMESTAMPTZ NOT NULL DEFAULT CURRENT_TIMESTAMP,
  "updated_at" TIMESTAMPTZ NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT "scene_assets_pkey" PRIMARY KEY ("id")
);

CREATE TABLE "processing_jobs" (
  "id" UUID NOT NULL,
  "scene_id" UUID NOT NULL,
  "job_type" "JobType" NOT NULL,
  "status" "JobStatus" NOT NULL DEFAULT 'queued',
  "provider_job_id" TEXT,
  "correlation_id" TEXT,
  "attempt_count" INTEGER NOT NULL DEFAULT 0,
  "error_message" TEXT,
  "metadata_json" JSONB,
  "started_at" TIMESTAMPTZ,
  "completed_at" TIMESTAMPTZ,
  "created_at" TIMESTAMPTZ NOT NULL DEFAULT CURRENT_TIMESTAMP,
  "updated_at" TIMESTAMPTZ NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT "processing_jobs_pkey" PRIMARY KEY ("id")
);

CREATE TABLE "playback_plans" (
  "id" UUID NOT NULL,
  "project_id" UUID NOT NULL,
  "version" INTEGER NOT NULL DEFAULT 1,
  "timeline_json" JSONB NOT NULL,
  "is_reduced_motion" BOOLEAN NOT NULL DEFAULT false,
  "is_fallback" BOOLEAN NOT NULL DEFAULT false,
  "export_status" "ExportStatus" NOT NULL DEFAULT 'pending',
  "created_at" TIMESTAMPTZ NOT NULL DEFAULT CURRENT_TIMESTAMP,
  "updated_at" TIMESTAMPTZ NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT "playback_plans_pkey" PRIMARY KEY ("id")
);

CREATE UNIQUE INDEX "users_email_key" ON "users"("email");
CREATE INDEX "guest_sessions_expires_at_idx" ON "guest_sessions"("expires_at");
CREATE INDEX "guest_sessions_claimed_by_user_id_idx" ON "guest_sessions"("claimed_by_user_id");
CREATE INDEX "projects_owner_id_idx" ON "projects"("owner_id");
CREATE INDEX "projects_guest_session_id_idx" ON "projects"("guest_session_id");
CREATE INDEX "projects_status_idx" ON "projects"("status");
CREATE INDEX "projects_expires_at_idx" ON "projects"("expires_at");
CREATE INDEX "projects_claimed_by_user_id_idx" ON "projects"("claimed_by_user_id");
CREATE INDEX "scenes_project_id_idx" ON "scenes"("project_id");
CREATE INDEX "scenes_status_idx" ON "scenes"("status");
CREATE UNIQUE INDEX "scenes_project_id_order_index_key" ON "scenes"("project_id", "order_index");
CREATE INDEX "scene_assets_scene_id_idx" ON "scene_assets"("scene_id");
CREATE INDEX "scene_assets_asset_type_idx" ON "scene_assets"("asset_type");
CREATE INDEX "processing_jobs_scene_id_idx" ON "processing_jobs"("scene_id");
CREATE INDEX "processing_jobs_status_idx" ON "processing_jobs"("status");
CREATE INDEX "processing_jobs_scene_id_job_type_status_idx" ON "processing_jobs"("scene_id", "job_type", "status");
CREATE INDEX "playback_plans_project_id_idx" ON "playback_plans"("project_id");

ALTER TABLE "projects"
ADD CONSTRAINT "projects_owner_id_fkey"
FOREIGN KEY ("owner_id") REFERENCES "users"("id") ON DELETE SET NULL ON UPDATE CASCADE;

ALTER TABLE "projects"
ADD CONSTRAINT "projects_guest_session_id_fkey"
FOREIGN KEY ("guest_session_id") REFERENCES "guest_sessions"("id") ON DELETE SET NULL ON UPDATE CASCADE;

ALTER TABLE "scenes"
ADD CONSTRAINT "scenes_project_id_fkey"
FOREIGN KEY ("project_id") REFERENCES "projects"("id") ON DELETE CASCADE ON UPDATE CASCADE;

ALTER TABLE "scene_assets"
ADD CONSTRAINT "scene_assets_scene_id_fkey"
FOREIGN KEY ("scene_id") REFERENCES "scenes"("id") ON DELETE CASCADE ON UPDATE CASCADE;

ALTER TABLE "processing_jobs"
ADD CONSTRAINT "processing_jobs_scene_id_fkey"
FOREIGN KEY ("scene_id") REFERENCES "scenes"("id") ON DELETE CASCADE ON UPDATE CASCADE;

ALTER TABLE "playback_plans"
ADD CONSTRAINT "playback_plans_project_id_fkey"
FOREIGN KEY ("project_id") REFERENCES "projects"("id") ON DELETE CASCADE ON UPDATE CASCADE;



================================================
FILE: public/runpod-ssh-setup-tutorial.md
================================================
# RunPod SSH Setup Tutorial

This guide captures the full command flow we used, from creating an SSH key to testing a RunPod SSH connection.

## 1. Create an SSH key pair

Create a new Ed25519 key:

```bash
ssh-keygen -t ed25519 -C "your-email@example.com"
```

When prompted:

- choose a save path, or press Enter for the default `~/.ssh/id_ed25519`
- optionally enter a passphrase for extra protection

If you create a custom key instead, you may end up with files like:

- private key: `sshk`
- public key: `sshk_pub` or `sshk.pub`

## 2. Find your public key

List your SSH files:

```bash
ls ~/.ssh
```

Print the public key:

```bash
cat ~/.ssh/id_ed25519.pub
```

If you used a custom filename, print that public key instead:

```bash
cat /path/to/your/custom_key.pub
```

Only the public key should be pasted into RunPod.

## 3. Register the public key in RunPod

Paste the contents of your public key into the SSH key section in RunPod.

Important:

- public key goes into RunPod
- private key stays on your machine

## 4. Move keys into the standard SSH location

If your keys were created outside `~/.ssh`, move them into place.

Example used here:

```bash
mkdir -p ~/.ssh
mv ~/Desktop/sshk ~/.ssh/id_ed25519
mv ~/Desktop/sshk_pub ~/.ssh/id_ed25519.pub
chmod 600 ~/.ssh/id_ed25519
chmod 644 ~/.ssh/id_ed25519.pub
```

Verify:

```bash
ls -la ~/.ssh
```

Expected files:

- `~/.ssh/id_ed25519`
- `~/.ssh/id_ed25519.pub`

## 5. Test the RunPod SSH gateway

RunPod may give you a gateway command like this:

```bash
ssh q91ot3ib257e53-644115fd@ssh.runpod.io -i ~/.ssh/id_ed25519
```

To test with verbose output:

```bash
ssh -v q91ot3ib257e53-644115fd@ssh.runpod.io -i ~/.ssh/id_ed25519
```

What to look for:

- `Offering public key`
- `Server accepts key`

If you see both, the key pairing is correct.

## 6. Test the exposed TCP SSH endpoint

RunPod may also show a direct command like this:

```bash
ssh root@213.173.110.146 -p 14214 -i ~/.ssh/id_ed25519
```

Verbose version:

```bash
ssh -v root@213.173.110.146 -p 14214 -i ~/.ssh/id_ed25519
```

In our test session, this endpoint returned:

```text
Connection refused
```

That means the port was reachable as an address, but SSH was not listening there at the time.

## 7. Test whether the port is open

You can verify the TCP port directly:

```bash
nc -vz 213.173.110.146 14214
```

If it returns `Connection refused`, the direct exposed SSH endpoint is not currently accepting connections.

## 8. Load the key into your SSH agent

If your private key has a passphrase, the non-interactive session may fail even after the server accepts the key.

Start the SSH agent if needed:

```bash
eval "$(ssh-agent -s)"
```

Add your key:

```bash
ssh-add ~/.ssh/id_ed25519
```

Then retry the gateway login:

```bash
ssh q91ot3ib257e53-644115fd@ssh.runpod.io -i ~/.ssh/id_ed25519
```

## 9. How to tell what failed

### Key path problem

```text
Identity file ... not accessible: No such file or directory
```

Meaning: your `-i` path is wrong.

### Desktop/macOS permission problem

```text
Operation not permitted
```

Meaning: Terminal cannot access Desktop/Documents/Downloads. Move the key into `~/.ssh` or grant permissions in macOS.

### RunPod accepted the key, but passphrase could not be entered

```text
Server accepts key
read_passphrase: can't open /dev/tty
Permission denied (publickey)
```

Meaning: the key is correct, but the session cannot prompt for the passphrase. Use `ssh-add` first.

### Direct endpoint network/service problem

```text
connect to address ... port ...: Connection refused
```

Meaning: nothing is listening on that exposed SSH port yet.

## 10. Final recommended connection flow

Use this order:

1. Create key pair with `ssh-keygen`
2. Paste the public key into RunPod
3. Move the private key to `~/.ssh/id_ed25519`
4. Set permissions with `chmod 600 ~/.ssh/id_ed25519`
5. Run `ssh-add ~/.ssh/id_ed25519`
6. Connect through the RunPod gateway:

```bash
ssh q91ot3ib257e53-644115fd@ssh.runpod.io -i ~/.ssh/id_ed25519
```

7. Only use the exposed TCP command if RunPod confirms that endpoint is active:

```bash
ssh root@213.173.110.146 -p 14214 -i ~/.ssh/id_ed25519
```

## 11. Commands used in this session

These are the main commands we used while debugging:

```bash
ssh -v root@213.173.110.146 -p 14214 -i ~/.ssh/id_ed25519
ssh -v root@213.173.110.146 -p 14214 -i /Users/wislemleger/Desktop/sshk
nc -vz 213.173.110.146 14214
ssh -v q91ot3ib257e53-644115fd@ssh.runpod.io -i /Users/wislemleger/Desktop/sshk
mkdir -p ~/.ssh
mv ~/Desktop/sshk ~/.ssh/id_ed25519
mv ~/Desktop/sshk_pub ~/.ssh/id_ed25519.pub
chmod 600 ~/.ssh/id_ed25519
chmod 644 ~/.ssh/id_ed25519.pub
ls -la ~/.ssh
ssh -v q91ot3ib257e53-644115fd@ssh.runpod.io -i ~/.ssh/id_ed25519
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```



================================================
FILE: scripts/dev-with-chunk-sync.mjs
================================================
import { spawn } from "node:child_process"
import { copyFile, mkdir, readdir, stat } from "node:fs/promises"
import { constants } from "node:fs"
import { join } from "node:path"

const root = process.cwd()
const serverDir = join(root, ".next", "server")
const chunksDir = join(serverDir, "chunks")

async function syncChunkFiles() {
  try {
    await mkdir(serverDir, { recursive: true })
    const entries = await readdir(chunksDir)

    await Promise.all(
      entries
        .filter((name) => name.endsWith(".js"))
        .map(async (name) => {
          const source = join(chunksDir, name)
          const target = join(serverDir, name)

          try {
            const [sourceStat, targetStat] = await Promise.allSettled([stat(source), stat(target)])

            if (sourceStat.status !== "fulfilled") {
              return
            }

            const shouldCopy =
              targetStat.status !== "fulfilled" ||
              sourceStat.value.mtimeMs > targetStat.value.mtimeMs ||
              sourceStat.value.size !== targetStat.value.size

            if (shouldCopy) {
              await copyFile(source, target, constants.COPYFILE_FICLONE)
            }
          } catch {
            await copyFile(source, target)
          }
        }),
    )
  } catch {
    // Next dev may not have emitted chunks yet.
  }
}

const child = spawn("node_modules/.bin/next", ["dev"], {
  cwd: root,
  env: process.env,
  stdio: "inherit",
})

const interval = setInterval(() => {
  void syncChunkFiles()
}, 500)

child.on("exit", (code, signal) => {
  clearInterval(interval)

  if (signal) {
    process.kill(process.pid, signal)
    return
  }

  process.exit(code ?? 0)
})

process.on("SIGINT", () => {
  clearInterval(interval)
  child.kill("SIGINT")
})

process.on("SIGTERM", () => {
  clearInterval(interval)
  child.kill("SIGTERM")
})



================================================
FILE: src/auth.ts
================================================
import bcrypt from "bcryptjs"
import NextAuth from "next-auth"
import type { Provider } from "next-auth/providers"
import Credentials from "next-auth/providers/credentials"
import Google from "next-auth/providers/google"

import { getAuthConfigEnv } from "@/config/env"
import { authRepository } from "@/modules/auth/repository"

const env = getAuthConfigEnv()

const providers: Provider[] = [
  Credentials({
    name: "Email and Password",
    credentials: {
      email: { label: "Email", type: "email" },
      password: { label: "Password", type: "password" },
    },
    async authorize(credentials) {
      if (!credentials?.email || !credentials?.password) {
        return null
      }

      const user = await authRepository.findByEmail(String(credentials.email))

      if (!user?.passwordHash) {
        return null
      }

      const passwordMatches = await bcrypt.compare(String(credentials.password), user.passwordHash)

      if (!passwordMatches) {
        return null
      }

      return {
        id: user.id,
        email: user.email,
        authProvider: user.authProvider,
      }
    },
  }),
]

if (env.GOOGLE_CLIENT_ID && env.GOOGLE_CLIENT_SECRET) {
  providers.push(
    Google({
      clientId: env.GOOGLE_CLIENT_ID,
      clientSecret: env.GOOGLE_CLIENT_SECRET,
    }),
  )
}

export const { handlers, auth, signIn, signOut } = NextAuth({
  providers,
  session: {
    strategy: "jwt",
  },
  callbacks: {
    async signIn({ user, account }) {
      if (account?.provider === "google" && user.email) {
        const dbUser = await authRepository.upsertGoogleUser(user.email)
        user.id = dbUser.id
      }

      return true
    },
    async jwt({ token, user }) {
      if (user?.id) {
        token.sub = user.id
      }

      if (user?.email) {
        token.email = user.email
      }

      if (user && "authProvider" in user) {
        token.authProvider = user.authProvider as string
      }

      return token
    },
    async session({ session, token }) {
      if (session.user) {
        session.user.id = token.sub ?? ""
        session.user.email = token.email ?? ""
        session.user.authProvider = typeof token.authProvider === "string" ? token.authProvider : undefined
      }

      return session
    },
  },
  trustHost: true,
  secret: env.NEXTAUTH_SECRET,
})



================================================
FILE: src/app/layout.tsx
================================================
import "./globals.css"
import type { Metadata } from "next"
import { ReactNode } from "react"

export const metadata: Metadata = {
  title: "Parallax Story Composer",
  description: "Sprint 1 backend foundation built with Next.js, Prisma, and PostgreSQL.",
}

export default function RootLayout({ children }: { children: ReactNode }) {
  return (
    <html lang="en">
      <body>{children}</body>
    </html>
  )
}



================================================
FILE: src/app/page.tsx
================================================
import { LandingPage } from "@/features/marketing/components/landing-page"

export default function HomePage() {
  return <LandingPage />
}



================================================
FILE: src/app/api/auth/[...nextauth]/route.ts
================================================
import { handlers } from "@/auth"

export const { GET, POST } = handlers



================================================
FILE: src/app/api/v1/assets/[...assetPath]/route.ts
================================================
import { NextResponse } from "next/server"

import { defineRoute } from "@/core/http/route-handler"
import { assetStorageService } from "@/modules/assets"

function contentTypeForAssetPath(assetPath: string) {
  if (assetPath.endsWith(".png")) {
    return "image/png"
  }

  if (assetPath.endsWith(".webp")) {
    return "image/webp"
  }

  if (assetPath.endsWith(".jpg") || assetPath.endsWith(".jpeg")) {
    return "image/jpeg"
  }

  if (assetPath.endsWith(".json")) {
    return "application/json"
  }

  return "application/octet-stream"
}

export const GET = defineRoute(async (request) => {
  const encodedAssetPath = request.nextUrl.pathname.split("/api/v1/assets/").at(1) ?? ""
  const assetPath = decodeURIComponent(encodedAssetPath)
  const asset = await assetStorageService.read(assetPath)

  return new NextResponse(asset.content, {
    status: 200,
    headers: {
      "Content-Length": String(asset.sizeBytes),
      "Content-Type": contentTypeForAssetPath(assetPath),
      "Cache-Control": "public, max-age=31536000, immutable",
    },
  })
})



================================================
FILE: src/app/api/v1/auth/register/route.ts
================================================
import { defineRoute } from "@/core/http/route-handler"
import { enforceRateLimit } from "@/infrastructure/rate-limit/memory-rate-limiter"
import { authController } from "@/interfaces/http/controllers/auth-controller"

export const POST = defineRoute(async (request, context) => {
  const requestId = request.headers.get("x-forwarded-for") ?? "local"
  enforceRateLimit(`${request.method}:${request.nextUrl.pathname}:${requestId}`)
  return authController.register(request, context)
})



================================================
FILE: src/app/api/v1/auth/session/route.ts
================================================
import { defineRoute } from "@/core/http/route-handler"
import { authController } from "@/interfaces/http/controllers/auth-controller"

export const GET = defineRoute(async (_request, context) => authController.session(context))



================================================
FILE: src/app/api/v1/guest-sessions/route.ts
================================================
import { defineRoute } from "@/core/http/route-handler"
import { enforceRateLimit } from "@/infrastructure/rate-limit/memory-rate-limiter"
import { guestSessionController } from "@/interfaces/http/controllers/guest-session-controller"

export const POST = defineRoute(async (request, context) => {
  const requestId = request.headers.get("x-forwarded-for") ?? "local"
  enforceRateLimit(`${request.method}:${request.nextUrl.pathname}:${requestId}`)
  return guestSessionController.create(context)
})



================================================
FILE: src/app/api/v1/health/live/route.ts
================================================
import { defineRoute } from "@/core/http/route-handler"
import { healthController } from "@/interfaces/http/controllers/health-controller"

export const GET = defineRoute(async (_request, context) => healthController.live(context))



================================================
FILE: src/app/api/v1/health/ready/route.ts
================================================
import { defineRoute } from "@/core/http/route-handler"
import { healthController } from "@/interfaces/http/controllers/health-controller"

export const GET = defineRoute(async (_request, context) => healthController.ready(context))



================================================
FILE: src/app/api/v1/internal/maintenance/cleanup/route.ts
================================================
import { defineRoute } from "@/core/http/route-handler"
import { ensureInternalMaintenanceAccess } from "@/interfaces/http/support/internal-maintenance"
import { maintenanceController } from "@/interfaces/http/controllers/maintenance-controller"

export const POST = defineRoute(async (request, context) => {
  ensureInternalMaintenanceAccess(request)
  return maintenanceController.cleanup(context)
})



================================================
FILE: src/app/api/v1/internal/maintenance/recover-timeouts/route.ts
================================================
import { defineRoute } from "@/core/http/route-handler"
import { ensureInternalMaintenanceAccess } from "@/interfaces/http/support/internal-maintenance"
import { maintenanceController } from "@/interfaces/http/controllers/maintenance-controller"

export const POST = defineRoute(async (request, context) => {
  ensureInternalMaintenanceAccess(request)
  return maintenanceController.recoverTimeouts(context)
})



================================================
FILE: src/app/api/v1/projects/route.ts
================================================
import { defineRoute } from "@/core/http/route-handler"
import { enforceRateLimit } from "@/infrastructure/rate-limit/memory-rate-limiter"
import { projectController } from "@/interfaces/http/controllers/project-controller"

function requestIdentifier(request: Request & { headers: Headers; nextUrl: URL }) {
  return request.headers.get("x-forwarded-for") ?? "local"
}

export const GET = defineRoute(async (request, context) => {
  enforceRateLimit(`${request.method}:${request.nextUrl.pathname}:${requestIdentifier(request)}`)
  return projectController.list(context)
})

export const POST = defineRoute(async (request, context) => {
  enforceRateLimit(`${request.method}:${request.nextUrl.pathname}:${requestIdentifier(request)}`)
  return projectController.create(request, context)
})



================================================
FILE: src/app/api/v1/projects/[projectId]/route.ts
================================================
import { defineRoute } from "@/core/http/route-handler"
import { enforceRateLimit } from "@/infrastructure/rate-limit/memory-rate-limiter"
import { projectController } from "@/interfaces/http/controllers/project-controller"

export const GET = defineRoute(async (request, context) => {
  enforceRateLimit(`${request.method}:${request.nextUrl.pathname}:${request.headers.get("x-forwarded-for") ?? "local"}`)
  const projectId = request.nextUrl.pathname.split("/").at(-1) ?? ""
  return projectController.getById(projectId, context)
})

export const PATCH = defineRoute(async (request, context) => {
  enforceRateLimit(`${request.method}:${request.nextUrl.pathname}:${request.headers.get("x-forwarded-for") ?? "local"}`)
  const projectId = request.nextUrl.pathname.split("/").at(-1) ?? ""
  return projectController.update(projectId, request, context)
})

export const DELETE = defineRoute(async (request, context) => {
  enforceRateLimit(`${request.method}:${request.nextUrl.pathname}:${request.headers.get("x-forwarded-for") ?? "local"}`)
  const projectId = request.nextUrl.pathname.split("/").at(-1) ?? ""
  return projectController.remove(projectId, context)
})



================================================
FILE: src/app/api/v1/projects/[projectId]/claim/route.ts
================================================
import { defineRoute } from "@/core/http/route-handler"
import { enforceRateLimit } from "@/infrastructure/rate-limit/memory-rate-limiter"
import { projectController } from "@/interfaces/http/controllers/project-controller"

export const POST = defineRoute(async (request, context) => {
  enforceRateLimit(`${request.method}:${request.nextUrl.pathname}:${request.headers.get("x-forwarded-for") ?? "local"}`)
  const segments = request.nextUrl.pathname.split("/")
  const projectId = segments.at(-2) ?? ""
  return projectController.claim(projectId, request, context)
})



================================================
FILE: src/app/api/v1/projects/[projectId]/preview/playback/route.ts
================================================
import { defineRoute } from "@/core/http/route-handler"
import { enforceRateLimit } from "@/infrastructure/rate-limit/memory-rate-limiter"
import { previewController } from "@/interfaces/http/controllers/preview-controller"

export const GET = defineRoute(async (request, context) => {
  enforceRateLimit(`${request.method}:${request.nextUrl.pathname}:${request.headers.get("x-forwarded-for") ?? "local"}`)
  const segments = request.nextUrl.pathname.split("/")
  const projectId = segments.at(-3) ?? ""
  const reducedMotion = request.nextUrl.searchParams.get("reducedMotion") === "true"
  return previewController.playback(projectId, reducedMotion, context)
})



================================================
FILE: src/app/api/v1/projects/[projectId]/preview/status/route.ts
================================================
import { defineRoute } from "@/core/http/route-handler"
import { enforceRateLimit } from "@/infrastructure/rate-limit/memory-rate-limiter"
import { previewController } from "@/interfaces/http/controllers/preview-controller"

export const GET = defineRoute(async (request, context) => {
  enforceRateLimit(`${request.method}:${request.nextUrl.pathname}:${request.headers.get("x-forwarded-for") ?? "local"}`)
  const segments = request.nextUrl.pathname.split("/")
  const projectId = segments.at(-3) ?? ""
  return previewController.status(projectId, context)
})



================================================
FILE: src/app/api/v1/projects/[projectId]/scenes/reorder/route.ts
================================================
import { defineRoute } from "@/core/http/route-handler"
import { enforceRateLimit } from "@/infrastructure/rate-limit/memory-rate-limiter"
import { projectController } from "@/interfaces/http/controllers/project-controller"

export const POST = defineRoute(async (request, context) => {
  enforceRateLimit(`${request.method}:${request.nextUrl.pathname}:${request.headers.get("x-forwarded-for") ?? "local"}`)
  const segments = request.nextUrl.pathname.split("/")
  const projectId = segments.at(-3) ?? ""
  return projectController.reorderScenes(projectId, request, context)
})



================================================
FILE: src/app/api/v1/projects/[projectId]/uploads/finalize/route.ts
================================================
import { defineRoute } from "@/core/http/route-handler"
import { enforceRateLimit } from "@/infrastructure/rate-limit/memory-rate-limiter"
import { sceneController } from "@/interfaces/http/controllers/scene-controller"

export const POST = defineRoute(async (request, context) => {
  enforceRateLimit(`${request.method}:${request.nextUrl.pathname}:${request.headers.get("x-forwarded-for") ?? "local"}`)
  const segments = request.nextUrl.pathname.split("/")
  const projectId = segments.at(-3) ?? ""
  return sceneController.finalizeUploads(projectId, request, context)
})



================================================
FILE: src/app/api/v1/projects/[projectId]/uploads/init/route.ts
================================================
import { defineRoute } from "@/core/http/route-handler"
import { enforceRateLimit } from "@/infrastructure/rate-limit/memory-rate-limiter"
import { uploadController } from "@/interfaces/http/controllers/upload-controller"

export const POST = defineRoute(async (request, context) => {
  enforceRateLimit(`${request.method}:${request.nextUrl.pathname}:${request.headers.get("x-forwarded-for") ?? "local"}`)
  const segments = request.nextUrl.pathname.split("/")
  const projectId = segments.at(-3) ?? ""
  return uploadController.initiate(projectId, request, context)
})



================================================
FILE: src/app/api/v1/scenes/[sceneId]/route.ts
================================================
import { defineRoute } from "@/core/http/route-handler"
import { enforceRateLimit } from "@/infrastructure/rate-limit/memory-rate-limiter"
import { sceneController } from "@/interfaces/http/controllers/scene-controller"

export const PATCH = defineRoute(async (request, context) => {
  enforceRateLimit(`${request.method}:${request.nextUrl.pathname}:${request.headers.get("x-forwarded-for") ?? "local"}`)
  const sceneId = request.nextUrl.pathname.split("/").at(-1) ?? ""
  return sceneController.update(sceneId, request, context)
})

export const DELETE = defineRoute(async (request, context) => {
  enforceRateLimit(`${request.method}:${request.nextUrl.pathname}:${request.headers.get("x-forwarded-for") ?? "local"}`)
  const sceneId = request.nextUrl.pathname.split("/").at(-1) ?? ""
  return sceneController.remove(sceneId, context)
})



================================================
FILE: src/app/api/v1/scenes/[sceneId]/regenerate/route.ts
================================================
import { defineRoute } from "@/core/http/route-handler"
import { enforceRateLimit } from "@/infrastructure/rate-limit/memory-rate-limiter"
import { sceneController } from "@/interfaces/http/controllers/scene-controller"

export const POST = defineRoute(async (request, context) => {
  enforceRateLimit(`${request.method}:${request.nextUrl.pathname}:${request.headers.get("x-forwarded-for") ?? "local"}`)
  const sceneId = request.nextUrl.pathname.split("/").at(-2) ?? ""
  return sceneController.regenerate(sceneId, request, context)
})



================================================
FILE: src/app/api/v1/scenes/[sceneId]/retry/route.ts
================================================
import { defineRoute } from "@/core/http/route-handler"
import { enforceRateLimit } from "@/infrastructure/rate-limit/memory-rate-limiter"
import { sceneController } from "@/interfaces/http/controllers/scene-controller"

export const POST = defineRoute(async (request, context) => {
  enforceRateLimit(`${request.method}:${request.nextUrl.pathname}:${request.headers.get("x-forwarded-for") ?? "local"}`)
  const sceneId = request.nextUrl.pathname.split("/").at(-2) ?? ""
  return sceneController.retry(sceneId, request, context)
})



================================================
FILE: src/app/api/v1/uploads/[uploadToken]/route.ts
================================================
import { defineRoute } from "@/core/http/route-handler"
import { AppError } from "@/core/errors/app-error"
import { ok } from "@/lib/api-response"
import { assetStorageService } from "@/modules/assets"
import { uploadService } from "@/modules/uploads"

export const PUT = defineRoute(async (request, context) => {
  const uploadToken = request.nextUrl.pathname.split("/").at(-1) ?? ""
  const verified = uploadService.verifyUploadToken(uploadToken)
  const content = Buffer.from(await request.arrayBuffer())

  if (content.byteLength !== verified.sizeBytes) {
    throw new AppError({
      code: "UPLOAD_SIZE_MISMATCH",
      message: "Uploaded file size does not match the upload contract.",
      statusCode: 400,
    })
  }

  await assetStorageService.write(verified.storageKey, content)

  return ok(
    {
      accepted: true,
      storageKey: verified.storageKey,
      expiresAt: verified.expiresAt,
    },
    { correlationId: context.correlationId },
  )
})



================================================
FILE: src/app/login/page.tsx
================================================
import { AuthPage } from "@/features/auth/components/auth-page"
import { getAuthConfigEnv } from "@/config/env"

type LoginPageProps = {
  searchParams: Promise<{
    callbackUrl?: string
  }>
}

export default async function LoginPage({ searchParams }: LoginPageProps) {
  const env = getAuthConfigEnv()
  const params = await searchParams
  return <AuthPage callbackUrl={params.callbackUrl} googleEnabled={Boolean(env.GOOGLE_CLIENT_ID && env.GOOGLE_CLIENT_SECRET)} mode="login" />
}



================================================
FILE: src/app/projects/page.tsx
================================================
import { ProjectsDashboardPage } from "@/features/projects/components/projects-dashboard-page"

export default function ProjectsPage() {
  return <ProjectsDashboardPage />
}



================================================
FILE: src/app/projects/[projectId]/editor/page.tsx
================================================
import { ProjectEditorPage } from "@/features/projects/components/project-editor-page"

type EditorPageProps = {
  params: Promise<{
    projectId: string
  }>
}

export default async function ProjectEditorRoute({ params }: EditorPageProps) {
  const { projectId } = await params

  return <ProjectEditorPage projectId={projectId} />
}



================================================
FILE: src/app/projects/[projectId]/preview/page.tsx
================================================
import { ProjectPreviewPage } from "@/features/preview/components/project-preview-page"

type PreviewPageProps = {
  params: Promise<{
    projectId: string
  }>
}

export default async function ProjectPreviewRoute({ params }: PreviewPageProps) {
  const { projectId } = await params

  return <ProjectPreviewPage projectId={projectId} />
}



================================================
FILE: src/app/projects/new/page.tsx
================================================
import { NewProjectPage } from "@/features/projects/components/new-project-page"

export default function NewProjectRoute() {
  return <NewProjectPage />
}



================================================
FILE: src/app/settings/page.tsx
================================================
import { SettingsPage } from "@/features/settings/components/settings-page"

export default function SettingsRoute() {
  return <SettingsPage />
}



================================================
FILE: src/app/signup/page.tsx
================================================
import { AuthPage } from "@/features/auth/components/auth-page"
import { getAuthConfigEnv } from "@/config/env"

type SignupPageProps = {
  searchParams: Promise<{
    callbackUrl?: string
  }>
}

export default async function SignupPage({ searchParams }: SignupPageProps) {
  const env = getAuthConfigEnv()
  const params = await searchParams
  return <AuthPage callbackUrl={params.callbackUrl} googleEnabled={Boolean(env.GOOGLE_CLIENT_ID && env.GOOGLE_CLIENT_SECRET)} mode="signup" />
}



================================================
FILE: src/config/constants.ts
================================================
export const API_VERSION = "v1"
export const DEFAULT_PROJECT_OUTPUT_FORMAT = "9:16"
export const UPLOAD_BASE_PATH = "projects"
export const DEFAULT_SCENE_LAYER_COUNT = 4
export const DEFAULT_SCENE_DURATION_MS = 2200
export const DEFAULT_SCENE_OVERLAP_MS = 320



================================================
FILE: src/config/env.ts
================================================
import { z } from "zod"

const envSchema = z.object({
  DATABASE_URL: z.string().min(1, "DATABASE_URL is required"),
  NEXTAUTH_SECRET: z.string().min(1, "NEXTAUTH_SECRET is required"),
  NEXTAUTH_URL: z.string().url("NEXTAUTH_URL must be a valid URL"),
  LOCAL_STORAGE_ROOT: z.string().min(1).default(".local/storage"),
  GOOGLE_CLIENT_ID: z.string().optional().default(""),
  GOOGLE_CLIENT_SECRET: z.string().optional().default(""),
  GUEST_SESSION_COOKIE_NAME: z.string().min(1).default("psc_guest_session"),
  GUEST_SESSION_TTL_HOURS: z.coerce.number().int().positive().default(72),
  RATE_LIMIT_WINDOW_MS: z.coerce.number().int().positive().default(60_000),
  RATE_LIMIT_MAX_REQUESTS: z.coerce.number().int().positive().default(60),
  UPLOAD_MAX_FILES: z.coerce.number().int().positive().max(20).default(10),
  UPLOAD_MAX_FILE_SIZE_BYTES: z.coerce.number().int().positive().default(10_485_760),
  UPLOAD_ALLOWED_MIME_TYPES: z
    .string()
    .transform((value) => value.split(",").map((entry) => entry.trim()).filter(Boolean))
    .default("image/jpeg,image/png,image/webp"),
  INTERNAL_UPLOAD_TOKEN_SECRET: z.string().min(1, "INTERNAL_UPLOAD_TOKEN_SECRET is required"),
  INTERNAL_MAINTENANCE_TOKEN: z.string().optional().default(""),
  QWEN_API_URL: z.string().optional().default(""),
  QWEN_API_KEY: z.string().optional().default(""),
  QWEN_MODEL: z.string().min(1).default("qwen-image-layered"),
  QWEN_TIMEOUT_MS: z.coerce.number().int().positive().default(30_000),
  QWEN_MAX_RETRIES: z.coerce.number().int().nonnegative().default(2),
  QWEN_MOCK_MODE: z.coerce.boolean().default(true),
  GUEST_MAX_PROJECTS: z.coerce.number().int().positive().default(3),
  GUEST_MAX_SCENES_PER_PROJECT: z.coerce.number().int().positive().default(10),
  PROCESSING_JOB_TIMEOUT_MS: z.coerce.number().int().positive().default(300_000),
  FEATURE_MOTION_PIPELINE: z.coerce.boolean().default(true),
  FEATURE_PLAYBACK_PIPELINE: z.coerce.boolean().default(true),
  FEATURE_PREVIEW_FALLBACKS: z.coerce.boolean().default(true),
  FEATURE_REDUCED_MOTION_PREVIEW: z.coerce.boolean().default(true),
  PROCESSING_CANARY_PERCENT: z.coerce.number().int().min(0).max(100).default(100),
  LOG_LEVEL: z.enum(["fatal", "error", "warn", "info", "debug", "trace"]).default("info"),
  NODE_ENV: z.enum(["development", "test", "production"]).default("development"),
})

export type AppEnv = z.infer<typeof envSchema>

let cachedEnv: AppEnv | null = null

export function resetEnvCache() {
  cachedEnv = null
}

export function getEnv(): AppEnv {
  if (cachedEnv) {
    return cachedEnv
  }

  const parsed = envSchema.safeParse(process.env)

  if (!parsed.success) {
    const issues = parsed.error.issues.map((issue) => `${issue.path.join(".")}: ${issue.message}`)
    throw new Error(`Invalid environment configuration: ${issues.join(", ")}`)
  }

  cachedEnv = parsed.data
  return cachedEnv
}

export function envIsConfigured(): boolean {
  return envSchema.safeParse(process.env).success
}

export function getAuthConfigEnv() {
  if (!process.env.NEXTAUTH_SECRET) {
    if (process.env.NODE_ENV === "production") {
      throw new Error("NEXTAUTH_SECRET must be configured in production.")
    }
  }

  const hasGoogleClientId = Boolean(process.env.GOOGLE_CLIENT_ID)
  const hasGoogleClientSecret = Boolean(process.env.GOOGLE_CLIENT_SECRET)

  if (hasGoogleClientId !== hasGoogleClientSecret) {
    throw new Error("GOOGLE_CLIENT_ID and GOOGLE_CLIENT_SECRET must both be configured to enable Google auth.")
  }

  return {
    NEXTAUTH_SECRET: process.env.NEXTAUTH_SECRET || "development-nextauth-secret",
    GOOGLE_CLIENT_ID: process.env.GOOGLE_CLIENT_ID || "",
    GOOGLE_CLIENT_SECRET: process.env.GOOGLE_CLIENT_SECRET || "",
  }
}



================================================
FILE: src/core/errors/app-error.ts
================================================
export class AppError extends Error {
  public readonly statusCode: number
  public readonly code: string
  public readonly details?: Record<string, unknown>

  constructor(options: {
    message: string
    statusCode: number
    code: string
    details?: Record<string, unknown>
  }) {
    super(options.message)
    this.name = "AppError"
    this.statusCode = options.statusCode
    this.code = options.code
    this.details = options.details
  }
}

export function isAppError(error: unknown): error is AppError {
  return error instanceof AppError
}



================================================
FILE: src/core/errors/error-response.ts
================================================
import { NextResponse } from "next/server"
import { Prisma } from "@prisma/client"
import { ZodError } from "zod"

import { isAppError } from "@/core/errors/app-error"
import type { RequestContext } from "@/core/request/context"

export function toErrorResponse(error: unknown, context: RequestContext) {
  if (isAppError(error)) {
    return NextResponse.json(
      {
        error: {
          code: error.code,
          message: error.message,
          details: error.details ?? null,
        },
        meta: {
          correlationId: context.correlationId,
        },
      },
      { status: error.statusCode },
    )
  }

  if (error instanceof Prisma.PrismaClientInitializationError) {
    return NextResponse.json(
      {
        error: {
          code: "DATABASE_UNAVAILABLE",
          message: "The database is unavailable right now.",
          details: null,
        },
        meta: {
          correlationId: context.correlationId,
        },
      },
      { status: 503 },
    )
  }

  if (error instanceof ZodError) {
    return NextResponse.json(
      {
        error: {
          code: "VALIDATION_ERROR",
          message: "Request validation failed.",
          details: error.flatten(),
        },
        meta: {
          correlationId: context.correlationId,
        },
      },
      { status: 400 },
    )
  }

  return NextResponse.json(
    {
      error: {
        code: "INTERNAL_SERVER_ERROR",
        message: "An unexpected error occurred.",
        details: null,
      },
      meta: {
        correlationId: context.correlationId,
      },
    },
    { status: 500 },
  )
}



================================================
FILE: src/core/http/route-handler.ts
================================================
import { NextRequest, NextResponse } from "next/server"

import { toErrorResponse } from "@/core/errors/error-response"
import { getLogger } from "@/core/logging/logger"
import { buildRequestContext } from "@/core/request/context"

type RouteCallback = (request: NextRequest, context: Awaited<ReturnType<typeof buildRequestContext>>) => Promise<NextResponse>

export function defineRoute(handler: RouteCallback) {
  return async function route(request: NextRequest) {
    const context = await buildRequestContext(request.nextUrl.pathname, request.method)
    const logger = getLogger()
    const startedAt = Date.now()

    try {
      const response = await handler(request, context)
      response.headers.set("x-correlation-id", context.correlationId)

      logger.info({
        correlationId: context.correlationId,
        method: request.method,
        path: request.nextUrl.pathname,
        statusCode: response.status,
        durationMs: Date.now() - startedAt,
      }, "request completed")

      return response
    } catch (error) {
      logger.error({
        correlationId: context.correlationId,
        method: request.method,
        path: request.nextUrl.pathname,
        durationMs: Date.now() - startedAt,
        err: error,
      }, "request failed")

      const response = toErrorResponse(error, context)
      response.headers.set("x-correlation-id", context.correlationId)
      return response
    }
  }
}



================================================
FILE: src/core/logging/logger.ts
================================================
import pino from "pino"

import { getEnv } from "@/config/env"

let loggerInstance: pino.Logger | null = null

export function getLogger() {
  if (loggerInstance) {
    return loggerInstance
  }

  const env = getEnv()

  loggerInstance = pino({
    level: env.LOG_LEVEL,
    base: undefined,
    timestamp: pino.stdTimeFunctions.isoTime,
  })

  return loggerInstance
}



================================================
FILE: src/core/observability/metrics.ts
================================================
type MetricName =
  | "processing_decomposition_duration_ms"
  | "processing_motion_duration_ms"
  | "processing_playback_duration_ms"
  | "processing_failures_total"
  | "processing_retries_total"
  | "processing_queue_depth"
  | "guest_cleanup_deleted_projects_total"
  | "guest_cleanup_deleted_sessions_total"

type MetricEntry = {
  count: number
  total: number
  lastValue: number
}

const store = new Map<MetricName, MetricEntry>()

function ensureMetric(name: MetricName) {
  const existing = store.get(name)

  if (existing) {
    return existing
  }

  const initial = {
    count: 0,
    total: 0,
    lastValue: 0,
  }

  store.set(name, initial)
  return initial
}

export const metrics = {
  observe(name: MetricName, value: number) {
    const metric = ensureMetric(name)
    metric.count += 1
    metric.total += value
    metric.lastValue = value
  },

  increment(name: MetricName, value = 1) {
    const metric = ensureMetric(name)
    metric.count += 1
    metric.total += value
    metric.lastValue = value
  },

  gauge(name: MetricName, value: number) {
    const metric = ensureMetric(name)
    metric.lastValue = value
  },

  snapshot() {
    return Object.fromEntries(
      Array.from(store.entries()).map(([name, metric]) => [
        name,
        {
          count: metric.count,
          total: metric.total,
          lastValue: metric.lastValue,
          average: metric.count > 0 ? metric.total / metric.count : 0,
        },
      ]),
    )
  },
}



================================================
FILE: src/core/observability/processing-log.ts
================================================
import { getLogger } from "@/core/logging/logger"

type ProcessingLogInput = {
  event: string
  traceId?: string | null
  projectId?: string | null
  sceneId?: string | null
  jobId?: string | null
  details?: Record<string, unknown>
}

export function logProcessingEvent(input: ProcessingLogInput) {
  const logger = getLogger()

  logger.info(
    {
      traceId: input.traceId ?? null,
      projectId: input.projectId ?? null,
      sceneId: input.sceneId ?? null,
      jobId: input.jobId ?? null,
      ...(input.details ?? {}),
    },
    input.event,
  )
}



================================================
FILE: src/core/request/context.ts
================================================
import { headers } from "next/headers"

export type RequestContext = {
  correlationId: string
  path: string
  method: string
}

function randomId() {
  return crypto.randomUUID()
}

export async function buildRequestContext(path: string, method: string): Promise<RequestContext> {
  const headerStore = await headers()
  const correlationId = headerStore.get("x-correlation-id") ?? randomId()

  return {
    correlationId,
    path,
    method,
  }
}



================================================
FILE: src/core/security/cookies.ts
================================================
export const COOKIE_MAX_AGE_SECONDS = 60 * 60 * 24 * 3



================================================
FILE: src/features/auth/components/auth-page.tsx
================================================
"use client"

import { useMemo, useState, type FormEvent } from "react"
import type { Route } from "next"
import Link from "next/link"
import { useRouter } from "next/navigation"
import { signIn } from "next-auth/react"

import { AppHeader } from "@/features/shared/components/app-header"
import { AppIcon } from "@/features/shared/components/app-icon"

type AuthPageProps = {
  mode: "login" | "signup"
  googleEnabled?: boolean
  callbackUrl?: string
}

type RegisterResponse = {
  id: string
}

type ApiEnvelope<T> = {
  data: T
}

type ApiErrorEnvelope = {
  error?: {
    message?: string
  }
}

async function parseJsonResponse<T>(response: Response) {
  const payload = (await response.json().catch(() => null)) as ApiEnvelope<T> | ApiErrorEnvelope | null

  if (!response.ok) {
    throw new Error(payload && "error" in payload ? payload.error?.message ?? "Request failed." : "Request failed.")
  }

  if (!payload || !("data" in payload)) {
    throw new Error("Unexpected response from the server.")
  }

  return payload.data
}

export function AuthPage({ mode, googleEnabled = false, callbackUrl = "/projects" }: AuthPageProps) {
  const router = useRouter()
  const isLogin = mode === "login"
  const [displayName, setDisplayName] = useState("")
  const [email, setEmail] = useState("")
  const [password, setPassword] = useState("")
  const [rememberDevice, setRememberDevice] = useState(true)
  const [isSubmitting, setIsSubmitting] = useState(false)
  const [errorMessage, setErrorMessage] = useState<string | null>(null)

  const benefits = useMemo(
    () => [
      {
        icon: "cloud_upload" as const,
        title: "Live Project Sync",
        body: "Keep projects, scene edits, and preview-ready uploads in one place across guest and signed-in flows.",
      },
      {
        icon: "file_export" as const,
        title: "Preview And Claim",
        body: "Sign in to claim guest work, keep saving safely, and unlock authenticated-only export messaging.",
      },
      {
        icon: "group" as const,
        title: "MVP Studio Access",
        body: "Use the same credentials flow the app actually supports today, with Google available only when configured.",
      },
    ],
    [],
  )

  async function handleSubmit(event: FormEvent<HTMLFormElement>) {
    event.preventDefault()
    setIsSubmitting(true)
    setErrorMessage(null)

    try {
      if (isLogin) {
        const result = await signIn("credentials", {
          email,
          password,
          redirect: false,
          callbackUrl,
        })

        if (!result || result.error) {
          throw new Error("Email or password is incorrect.")
        }

        window.location.assign(result.url || callbackUrl)
        router.refresh()
        return
      }

      await parseJsonResponse<RegisterResponse>(
        await fetch("/api/v1/auth/register", {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify({
            displayName: displayName.trim() || undefined,
            email,
            password,
            rememberDevice,
          }),
        }),
      )

      const loginResult = await signIn("credentials", {
        email,
        password,
        redirect: false,
        callbackUrl,
      })

      if (!loginResult || loginResult.error) {
        throw new Error("Account created, but automatic sign-in failed. Please log in.")
      }

      window.location.assign(loginResult.url || callbackUrl)
      router.refresh()
    } catch (error) {
      setErrorMessage(error instanceof Error ? error.message : "Authentication failed.")
    } finally {
      setIsSubmitting(false)
    }
  }

  return (
    <main className="auth-screen">
      <AppHeader variant="auth" />
      <div className="auth-layout">
        <section className="auth-side-panel">
          <div className="auth-side-panel__content">
            <div className="auth-side-panel__brand">
              <AppIcon className="auth-brand-icon" name="storm" />
              <h1>Parallax Story Composer</h1>
            </div>
            <div className="auth-side-panel__stack">
              <h2>
                Build stories that <span>actually ship</span>.
              </h2>
              <div className="auth-benefit-list">
                {benefits.map(({ icon, title, body }) => (
                  <article className="auth-benefit" key={title}>
                    <div className="auth-benefit__icon">
                      <AppIcon className="auth-benefit__icon-svg" name={icon} />
                    </div>
                    <div>
                      <h3>{title}</h3>
                      <p>{body}</p>
                    </div>
                  </article>
                ))}
              </div>
            </div>
          </div>
          <div className="auth-side-panel__bg" />
          <p className="auth-side-panel__footer">© 2024 Parallax Story Composer. Credentials-first MVP access.</p>
        </section>

        <section className="auth-form-side">
          <div className="auth-form-wrap">
            <div className="auth-mobile-brand">
              <AppIcon className="auth-brand-icon auth-brand-icon--mobile" name="storm" />
              <span>Parallax</span>
            </div>

            <div className="auth-tabs">
              <Link className={isLogin ? "auth-tabs__item is-active" : "auth-tabs__item"} href={`/login?callbackUrl=${encodeURIComponent(callbackUrl)}` as Route}>
                Log In
              </Link>
              <Link className={!isLogin ? "auth-tabs__item is-active" : "auth-tabs__item"} href={`/signup?callbackUrl=${encodeURIComponent(callbackUrl)}` as Route}>
                Sign Up
              </Link>
            </div>

            <div className="auth-card">
              <h2>{isLogin ? "Welcome back" : "Create your account"}</h2>
              <p className="auth-card__lede">
                {isLogin
                  ? "Log in with credentials to open your projects, claim guest work, and keep editing."
                  : "Create a credentials account, then land directly in your project workspace."}
              </p>
              {!googleEnabled ? <p className="auth-card__lede">Google sign-in is off unless both Google provider secrets are configured for this deployment.</p> : null}

              {googleEnabled ? (
                <button
                  className="auth-google-button"
                  onClick={() => void signIn("google", { callbackUrl })}
                  type="button"
                >
                  <svg className="auth-google-button__icon" viewBox="0 0 24 24">
                    <path d="M22.56 12.25c0-.78-.07-1.53-.2-2.25H12v4.26h5.92c-.26 1.37-1.04 2.53-2.21 3.31v2.77h3.57c2.08-1.92 3.28-4.74 3.28-8.09z" fill="#4285F4" />
                    <path d="M12 23c2.97 0 5.46-.98 7.28-2.66l-3.57-2.77c-.98.66-2.23 1.06-3.71 1.06-2.86 0-5.29-1.93-6.16-4.53H2.18v2.84C3.99 20.53 7.7 23 12 23z" fill="#34A853" />
                    <path d="M5.84 14.09c-.22-.66-.35-1.36-.35-2.09s.13-1.43.35-2.09V7.07H2.18C1.43 8.55 1 10.22 1 12s.43 3.45 1.18 4.93l3.66-2.84z" fill="#FBBC05" />
                    <path d="M12 5.38c1.62 0 3.06.56 4.21 1.64l3.15-3.15C17.45 2.09 14.97 1 12 1 7.7 1 3.99 3.47 2.18 7.07l3.66 2.84c.87-2.6 3.3-4.53 6.16-4.53z" fill="#EA4335" />
                  </svg>
                  <span>Continue with Google</span>
                </button>
              ) : null}

              {googleEnabled ? (
                <div className="auth-divider">
                  <span>Or continue with</span>
                </div>
              ) : null}

              <form className="auth-form" onSubmit={handleSubmit}>
                {!isLogin ? (
                  <label className="auth-field">
                    <span>Display Name</span>
                    <input onChange={(event) => setDisplayName(event.target.value)} placeholder="Alex Creator" type="text" value={displayName} />
                  </label>
                ) : null}

                <label className="auth-field">
                  <span>Email Address</span>
                  <input onChange={(event) => setEmail(event.target.value)} placeholder="name@studio.com" required type="email" value={email} />
                </label>

                <div className="auth-field">
                  <div className="auth-field__row">
                    <span>Password</span>
                  </div>
                  <div className="auth-password-wrap">
                    <input onChange={(event) => setPassword(event.target.value)} placeholder="••••••••" required type="password" value={password} />
                  </div>
                </div>

                <label className="auth-checkbox-row">
                  <input checked={rememberDevice} onChange={(event) => setRememberDevice(event.target.checked)} type="checkbox" />
                  <span>Remember this device</span>
                </label>

                {errorMessage ? <p className="new-project-error">{errorMessage}</p> : null}

                <button className="auth-submit-button" disabled={isSubmitting} type="submit">
                  {isSubmitting ? (isLogin ? "Entering Studio..." : "Creating Account...") : isLogin ? "Enter Studio" : "Create Account"}
                </button>
              </form>

              <p className="auth-card__footer">
                {isLogin ? "New to Parallax? " : "Already have an account? "}
                <Link href={((isLogin ? `/signup?callbackUrl=${encodeURIComponent(callbackUrl)}` : `/login?callbackUrl=${encodeURIComponent(callbackUrl)}`) as Route)}>
                  {isLogin ? "Create an account" : "Log In"}
                </Link>
              </p>
            </div>
          </div>
        </section>
      </div>
    </main>
  )
}



================================================
FILE: src/features/marketing/components/landing-page.tsx
================================================
import type { Route } from "next"
import Link from "next/link"

import { AppHeader } from "@/features/shared/components/app-header"
import type { AppIconName } from "@/features/shared/components/app-icon"
import { AppIcon } from "@/features/shared/components/app-icon"

const howItWorks: Array<{ title: string; body: string; image: string; icon: AppIconName }> = [
  {
    title: "1. Upload",
    body: "Upload supported image files and turn them into ordered project scenes.",
    image:
      "https://lh3.googleusercontent.com/aida-public/AB6AXuArwtni54PHapKEODx6doVeYttx5JaLYaiyzVzVxJQCraahqK5B_ACiJgSbkrOLcC0ZbqdQlJx-rmd2kQvwG1-EmF8KTG_BSIYo2yCtVGJus5TvBwVYS7WrJ3JnXCtUMBlPz1qdSuHOYC4LNOj_r3vWDfZBB9cbaKIcArFrg7u_kogSE374avb2J-u14aSDUeL662VB7FPgqGTFOCa15hCh280wXjeXhlwM3PjWItwFYI0L_X0Q__ezWk4rLSks-Ou1shdfKq_SUDw",
    icon: "upload_file",
  },
  {
    title: "2. Build Scenes",
    body: "Add scene context, reorder the timeline, and keep the project moving from upload to ready.",
    image:
      "https://lh3.googleusercontent.com/aida-public/AB6AXuD56SjIME50ktrzigeVWGdMX-zfGgaKhukwG41jVLRAGlXbcoJnWnzNuPUjyK7cswMh30ggMAuBet2puze3Vh25I9OUIvhfWyGDrNC40trQvpAppBfWXuYrwhNsFVoo2erQ04lPcVx-AbU_TGVVs-q_BaFiIGCrxJt1p3GWgk4D_ICRLDnGz07XgC5lZ42Q7BfJRwtxqquFrZMTI1Kq-MZjXHo2bH_lFDPbhB1VZwE6haRVpEc1I04HZC85dg4owW67kFcm2BQswkM",
    icon: "stack",
  },
  {
    title: "3. Motion Direction",
    body: "Choose motion presets and intensity per scene before queueing generation or retrying failures.",
    image:
      "https://lh3.googleusercontent.com/aida-public/AB6AXuAgxdharMz3IZdeOQyRQ9KI3S0s7fkz7j13d5b_M_lUVzltbfbU9u7El40vNINGJSrtWoNCPRNb5ll5OFOMQ0V_pmLCb6fvbCGmd5tTBMy3G3Q2AvMdkOI6XbpALrGJZiMqDIKiyUo1lYImI1l7alXRYKt6DAuLMLpnWyw-BLQpHn3_9t0RiaJ1q0ed4jcNOgdHzKbO9Y6Wu9lKkAHrV3gogS7xD480bdBvTePyxAnUgAlNNA-JYlwJ-VtBCoNfJjw0K--ml_ONqjQ",
    icon: "movie_edit",
  },
  {
    title: "4. Preview Story",
    body: "Review a stitched mobile preview that stays usable even when only some scenes are ready.",
    image:
      "https://lh3.googleusercontent.com/aida-public/AB6AXuBIp7VIb2LyIPZtzjv8G9rIVxe5qQJYbhBdjZlodEMmiNj50qo4JzhLchvFzvbLKuyJS_TK7faZrfoGYFW2WQ3lAN0BwHQLHlvV-eo8nG6GLLOw8QiKAf1IdixT3zOTfFwKlhOPRWtaGoWBEdYTiMxYkFV9HN2Y-B4C4Zk-6KQ1iCiEMlTK7i63DDWST7Ali3WkrxxLMngB4PMRaSTwdSvThtrnt4GlAqGM7s9Ad9CdnKo1aWw_5z5ZVEXT2KTKXa7DH2UIMjk8ddc",
    icon: "play_circle",
  },
]

const footerProductLinks = ["Projects", "Editor", "Preview", "Guest Access"]
const footerResourceLinks = ["Local Setup", "Health Checks", "Auth", "Support"]
const featureItems: Array<{ icon: AppIconName; title: string; body: string }> = [
  {
    icon: "view_quilt",
    title: "Scene Manager",
    body: "Organize uploads into a real ordered timeline with editable scene metadata and status visibility.",
  },
  {
    icon: "auto_fix_high",
    title: "Generation Pipeline",
    body: "Queue scene processing, retry failed work, and keep partially ready projects previewable.",
  },
  {
    icon: "draw",
    title: "Editor Controls",
    body: "Update project context, style hints, motion preset, and intensity from the editor instead of mock controls.",
  },
  {
    icon: "swipe_down_alt",
    title: "Stitched Preview",
    body: "Use the current MVP player to inspect scene order, timing, and fallback playback on mobile-sized layouts.",
  },
]

export function LandingPage() {
  return (
    <main className="psc-screen psc-screen--landing">
      <AppHeader variant="marketing" />

      <section className="landing-hero">
        <div className="landing-hero__copy">
          <div className="landing-badge">
            <span className="landing-badge__dot" />
            MVP Story Workflow
          </div>
          <h1 className="landing-hero__title">
            Turn Still Images into <span>Previewable</span> Parallax Stories
          </h1>
          <p className="landing-hero__lede">
            Upload images, shape scene-by-scene motion, and review a stitched vertical preview.
            The current launch path focuses on uploads, editing, preview, and guest-to-account
            claiming instead of full export tooling.
          </p>
          <div className="landing-hero__actions">
            <Link className="landing-button landing-button--primary" href={"/projects/new" as Route}>
              Start Free as Guest
            </Link>
            <Link className="landing-button landing-button--secondary" href={"/signup" as Route}>
              Create Account
            </Link>
          </div>
          <Link className="landing-inline-link" href={"/login" as Route}>
            Already have an account? Log In
          </Link>
        </div>

        <div className="landing-hero__visual-wrap">
          <div className="landing-hero__visual-glow" />
          <div className="landing-phone-frame">
            <div
              className="landing-phone-frame__image"
              style={{
                backgroundImage:
                  'url("https://lh3.googleusercontent.com/aida-public/AB6AXuARa_R0UxUaViwpyRxqB6fNeCk4IoirR9zhAJfhXpo8vf--Dw0n1DOWlMwLt6A4Wsf9ON5qNiwuJE5qUvPJZrpAewg46MfAz7PyYBWfqpquJB5fNJ5QiQsPxT_zW7qR4sVQB-uiQPcba5TCVqVe6zouhN6s5oqp-ttaBiD9wbzFaQhjrMoJ7xdoZR2x8T-O3WLHPueOoi9OLSmOA0XG4ScsaQzxQlj-J58Sj_R0t3weAFme-XX8-p1b9d3hcTmo4BqTnpDYGd9XpK8")',
              }}
            />
            <div className="landing-phone-frame__gradient" />
            <div className="landing-phone-frame__top-row">
              <div className="landing-phone-frame__scene-label">Scene 01: The Peak</div>
              <div className="landing-phone-frame__icon">
                <AppIcon className="landing-phone-frame__icon-svg" name="layers" />
              </div>
            </div>
            <svg className="landing-phone-frame__path" viewBox="0 0 400 700">
              <path d="M50,600 C150,550 250,650 350,500" fill="none" stroke="#38f91a" strokeDasharray="8 8" strokeWidth="2" />
              <circle cx="350" cy="500" fill="#38f91a" r="6" />
              <text fill="#38f91a" fontSize="12" fontWeight="bold" x="310" y="485">
                PAN END
              </text>
            </svg>
            <div className="landing-phone-frame__bottom">
              <div className="landing-phone-frame__progress">
                <div className="landing-phone-frame__progress-bar" />
              </div>
              <div className="landing-phone-frame__player-row">
                <span>00:12:45</span>
                <div className="landing-phone-frame__player-icons">
                  <AppIcon className="landing-player-icon" name="fast_rewind" />
                  <AppIcon className="landing-player-icon landing-player-icon--primary" name="play_arrow" />
                  <AppIcon className="landing-player-icon" name="fast_forward" />
                </div>
                <span>00:20:00</span>
              </div>
            </div>
          </div>
        </div>
      </section>

      <section className="landing-section landing-section--surface">
        <div className="landing-section__heading">
          <h2>How It Works</h2>
          <p>Master the art of visual storytelling in four simple steps</p>
        </div>
        <div className="landing-steps-grid">
          {howItWorks.map((step) => (
            <article className="landing-step" key={step.title}>
              <div className="landing-step__image" style={{ backgroundImage: `url("${step.image}")` }}>
                <div className="landing-step__icon-wrap">
                  <AppIcon className="landing-step__icon" name={step.icon} />
                </div>
              </div>
              <div className="landing-step__copy">
                <h3>{step.title}</h3>
                <p>{step.body}</p>
              </div>
            </article>
          ))}
        </div>
      </section>

      <section className="landing-section landing-section--features">
        <div>
          <h2 className="landing-feature-title">Pro Tools for Immersive Motion</h2>
          <div className="landing-feature-grid">
            {featureItems.map(({ icon, title, body }) => (
              <article className="landing-feature-item" key={title}>
                <AppIcon className="landing-feature-item__icon" name={icon} />
                <h4>{title}</h4>
                <p>{body}</p>
              </article>
            ))}
          </div>
        </div>

        <aside className="landing-guest-card">
          <div className="landing-guest-card__header">
            <div className="landing-guest-card__icon">
              <AppIcon className="landing-guest-card__icon-svg" name="info" />
            </div>
            <div>
              <h3>GUEST ACCESS</h3>
              <p>Guest workflow enabled</p>
            </div>
          </div>
          <ul className="landing-guest-card__list">
            <li><AppIcon className="landing-guest-card__list-icon" name="check_circle" /> Create projects and upload scene images</li>
            <li><AppIcon className="landing-guest-card__list-icon" name="check_circle" /> Edit scene context and motion settings</li>
            <li className="is-locked"><AppIcon className="landing-guest-card__list-icon" name="lock" /> Claim projects to an account for long-term ownership</li>
            <li className="is-locked"><AppIcon className="landing-guest-card__list-icon" name="lock" /> Export remains out of scope for the MVP</li>
          </ul>
          <Link className="landing-button landing-button--ghost" href={"/signup" as Route}>
            Claim Your Workspace
          </Link>
        </aside>
      </section>

      <section className="landing-final-cta">
        <h2>Ready to bring your images to life?</h2>
        <p>Start the guest workflow now, then claim the project later if you want to keep it beyond the guest lifecycle.</p>
        <Link className="landing-button landing-button--primary landing-button--large" href={"/projects/new" as Route}>
          Create Your Story
        </Link>
      </section>

      <footer className="landing-footer">
        <div className="landing-footer__grid">
          <div className="landing-footer__brand">
            <div className="landing-footer__logo-row">
              <div className="landing-footer__logo">
                <AppIcon className="landing-footer__logo-icon" name="layers" />
              </div>
              <h3>Parallax Story Composer</h3>
            </div>
            <p>
              An MVP workflow for uploads, scene editing, stitched preview, and guest-to-account
              claiming.
            </p>
            <div className="landing-footer__socials">
              <Link className="landing-footer__social" href={"/projects" as Route}>
                <AppIcon className="landing-footer__social-icon" name="public" />
              </Link>
              <Link className="landing-footer__social" href={"/projects/new" as Route}>
                <AppIcon className="landing-footer__social-icon" name="video_library" />
              </Link>
            </div>
          </div>
          <div>
            <h4>Product</h4>
            <ul className="landing-footer__links">
              {footerProductLinks.map((item) => (
                <li key={item}>
                  <span className="landing-footer__link">{item}</span>
                </li>
              ))}
            </ul>
          </div>
          <div>
            <h4>Resources</h4>
            <ul className="landing-footer__links">
              {footerResourceLinks.map((item) => (
                <li key={item}>
                  <span className="landing-footer__link">{item}</span>
                </li>
              ))}
            </ul>
          </div>
        </div>
        <div className="landing-footer__bottom">
          <p>© 2024 Parallax Story Composer. All rights reserved.</p>
          <div>
            <span className="landing-footer__meta-link">Privacy and legal pages ship after MVP launch.</span>
          </div>
        </div>
      </footer>
    </main>
  )
}



================================================
FILE: src/features/preview/components/playback-scene-renderer.tsx
================================================
import type { CSSProperties } from "react"

import type { NormalizedPlaybackScene } from "@/features/preview/lib/playback-client"

type PlaybackSceneRendererProps = {
  scene: NormalizedPlaybackScene
  isReducedMotion?: boolean
  className?: string
  progress?: number
}

type PlaybackLayerStyle = CSSProperties & {
  "--playback-offset-x": string
  "--playback-offset-y": string
  "--playback-scale": string
  "--playback-opacity": string
}

function clampProgress(value: number | undefined) {
  if (typeof value !== "number" || Number.isNaN(value)) {
    return null
  }

  return Math.min(1, Math.max(0, value))
}

function applyEasing(progress: number, easing: string | undefined) {
  if (easing === "ease-out") {
    return 1 - (1 - progress) * (1 - progress)
  }

  if (easing === "ease-in-out") {
    return progress < 0.5 ? 4 * progress * progress * progress : 1 - Math.pow(-2 * progress + 2, 3) / 2
  }

  return progress
}

function interpolate(from: number, to: number, progress: number) {
  return from + (to - from) * progress
}

function toGroupedProgress(progress: number, startProgress: number, endProgress: number) {
  if (endProgress <= startProgress) {
    return progress >= endProgress ? 1 : 0
  }

  const ratio = (progress - startProgress) / (endProgress - startProgress)
  return Math.min(1, Math.max(0, ratio))
}

function toOffset(cameraMovement: string, parallax: number, index: number) {
  const distance = Number((parallax * 48 + index * 4).toFixed(1))

  if (cameraMovement.includes("push")) {
    return { x: 0, y: -distance * 0.65 }
  }

  if (cameraMovement.includes("right")) {
    return { x: distance * 0.7, y: 0 }
  }

  if (cameraMovement.includes("hold")) {
    return { x: 0, y: 0 }
  }

  return { x: 0, y: -distance }
}

function toFlatImageTransform(cameraMovement: string, progress: number, isReducedMotion: boolean) {
  const dampedProgress = isReducedMotion ? progress * 0.18 : progress
  const drift = Number((dampedProgress * 18).toFixed(1))
  const pushScale = Number((1.02 + dampedProgress * (isReducedMotion ? 0.015 : 0.05)).toFixed(3))

  if (cameraMovement.includes("push")) {
    return `translate3d(0, ${(-drift * 0.45).toFixed(1)}px, 0) scale(${pushScale})`
  }

  if (cameraMovement.includes("right")) {
    return `translate3d(${(drift * 0.7).toFixed(1)}px, 0, 0) scale(1.02)`
  }

  if (cameraMovement.includes("hold")) {
    return "translate3d(0, 0, 0) scale(1.01)"
  }

  return `translate3d(0, ${(-drift).toFixed(1)}px, 0) scale(1.03)`
}

export function PlaybackSceneRenderer({ scene, isReducedMotion = false, className, progress }: PlaybackSceneRendererProps) {
  const layerAssets = scene.layerAssets.length > 0 ? scene.layerAssets : []
  const shouldRenderLayers = layerAssets.length > 0 && scene.layerBehaviors.length > 0
  const normalizedProgress = clampProgress(progress)
  const isInteractive = normalizedProgress !== null
  const flatImageStyle = scene.imageUrl
    ? {
        backgroundImage: `url("${scene.imageUrl}")`,
        transform: isInteractive ? toFlatImageTransform(scene.cameraMovement, normalizedProgress, isReducedMotion) : undefined,
      }
    : undefined

  return (
    <div className={["playback-scene-renderer", isInteractive ? "playback-scene-renderer--interactive" : null, className].filter(Boolean).join(" ")}>
      {scene.imageUrl ? (
        <div className="playback-scene-renderer__flat" style={flatImageStyle} />
      ) : (
        <div className="playback-scene-renderer__flat playback-scene-renderer__flat--placeholder">
          <div>
            <strong>Image unavailable</strong>
            <span>This scene can stay previewable while generated assets catch up.</span>
          </div>
        </div>
      )}

      {shouldRenderLayers
        ? layerAssets.map((layer, index) => {
            const behavior = scene.layerBehaviors.find((item) => item.layerIndex === layer.layerOrder) ?? scene.layerBehaviors[index]
            const groupedMapping = behavior?.mobile
            const hasGroupedMotion = Boolean(
              groupedMapping &&
              typeof groupedMapping.startProgress === "number" &&
              typeof groupedMapping.endProgress === "number",
            )
            const activeGroupedMapping = hasGroupedMotion ? groupedMapping! : null
            const groupedProgress = isInteractive && hasGroupedMotion
              ? applyEasing(
                  toGroupedProgress(normalizedProgress, activeGroupedMapping?.startProgress ?? 0, activeGroupedMapping?.endProgress ?? 1),
                  activeGroupedMapping?.easing,
                )
              : 0
            const parallax = isReducedMotion ? (behavior?.parallax ?? 0.18) * 0.18 : behavior?.parallax ?? 0.18
            const progressMultiplier = isInteractive ? normalizedProgress - 0.5 : 1
            const fallbackOffset = toOffset(scene.cameraMovement, parallax * (isInteractive ? progressMultiplier * 2 : 1), index)
            const offset = hasGroupedMotion
              ? {
                  x: interpolate(0, activeGroupedMapping?.translateX ?? 0, groupedProgress),
                  y: interpolate(0, activeGroupedMapping?.translateY ?? 0, groupedProgress),
                }
              : fallbackOffset
            const baseScale = isReducedMotion ? 1 : behavior?.scale ?? 1
            const interactiveScale = hasGroupedMotion
              ? interpolate(activeGroupedMapping?.scaleFrom ?? 1, activeGroupedMapping?.scaleTo ?? 1, groupedProgress)
              : isInteractive
                ? 1 + (baseScale - 1) * normalizedProgress
                : baseScale
            const interactiveOpacity = hasGroupedMotion
              ? interpolate(activeGroupedMapping?.opacityFrom ?? 1, activeGroupedMapping?.opacityTo ?? 1, groupedProgress)
              : isInteractive
                ? Math.min(1, Math.max(0.36, (behavior?.opacity ?? Math.max(0.45, 1 - index * 0.08)) - (0.5 - normalizedProgress) * 0.08))
                : behavior?.opacity ?? Math.max(0.45, 1 - index * 0.08)
            const style: PlaybackLayerStyle = {
              backgroundImage: `url("${layer.assetUrl}")`,
              zIndex: String(10 + index),
              "--playback-offset-x": `${offset.x}px`,
              "--playback-offset-y": `${offset.y}px`,
              "--playback-scale": `${interactiveScale}`,
              "--playback-opacity": `${interactiveOpacity}`,
            }

            return <div className="playback-scene-renderer__layer" key={`${scene.id}-${layer.layerOrder}-${index}`} style={style} />
          })
        : null}

      <div className="playback-scene-renderer__overlay" />
    </div>
  )
}



================================================
FILE: src/features/preview/components/project-preview-page.tsx
================================================
"use client"

import { useEffect, useMemo, useState } from "react"
import type { Route } from "next"
import Link from "next/link"

import { AppHeader } from "@/features/shared/components/app-header"
import { PlaybackSceneRenderer } from "@/features/preview/components/playback-scene-renderer"
import { buildNormalizedPlaybackState, parseApiResponse, type NormalizedPlaybackState, type PlaybackResponse, type ProjectRecord } from "@/features/preview/lib/playback-client"

type ProjectPreviewPageProps = {
  projectId: string
}

type PreviewState = {
  isLoading: boolean
  errorMessage: string | null
  playback: NormalizedPlaybackState | null
}

const initialState: PreviewState = {
  isLoading: true,
  errorMessage: null,
  playback: null,
}

export function ProjectPreviewPage({ projectId }: ProjectPreviewPageProps) {
  const [state, setState] = useState<PreviewState>(initialState)

  useEffect(() => {
    let cancelled = false

    async function loadPreview() {
      setState(initialState)

        try {
          const [projectResult, playbackResult] = await Promise.allSettled([
          fetch(`/api/v1/projects/${projectId}`, { cache: "no-store" }).then((response) =>
            parseApiResponse<ProjectRecord>(response, "Unable to load preview data."),
          ),
          fetch(`/api/v1/projects/${projectId}/preview/playback`, { cache: "no-store" }).then((response) =>
            parseApiResponse<PlaybackResponse>(response, "Unable to load preview data."),
          ),
        ])

        if (cancelled) {
          return
        }

        if (projectResult.status !== "fulfilled") {
          setState({
            ...initialState,
            isLoading: false,
            errorMessage: "This project preview could not be loaded.",
          })
          return
        }

        setState({
          isLoading: false,
          errorMessage: null,
          playback: buildNormalizedPlaybackState(projectResult.value, playbackResult.status === "fulfilled" ? playbackResult.value : null),
        })
      } catch {
        if (!cancelled) {
          setState({
            ...initialState,
            isLoading: false,
            errorMessage: "This project preview could not be loaded.",
          })
        }
      }
    }

    void loadPreview()

    return () => {
      cancelled = true
    }
  }, [projectId])

  const playback = state.playback

  const previewCountLabel = useMemo(() => {
    if (playback?.scenes.length === 1) {
      return "1 scene"
    }

    return `${playback?.scenes.length ?? 0} scenes`
  }, [playback?.scenes.length])

  return (
    <main className="misc-screen preview-screen">
      <AppHeader active="projects" />

      <section className="misc-shell misc-shell--wide preview-shell">
        <div className="misc-panel preview-page-panel">
          <div className="preview-page-header">
            <div>
              <p className="misc-kicker">Preview</p>
              <h1>{playback?.projectTitle ?? "Project Preview"}</h1>
              <p className="misc-copy">A mobile-first stitched scroll preview for project `{projectId}`.</p>
            </div>
            <div className="preview-page-header__actions">
              <div className="preview-page-badges">
                <span>{previewCountLabel}</span>
                <span>{playback?.projectStatus ?? "draft"}</span>
                {playback?.playbackVersion ? <span>Playback v{playback.playbackVersion}</span> : null}
                {playback?.isFallback ? <span>Fallback playback</span> : null}
                {playback?.isReducedMotion ? <span>Reduced motion</span> : null}
              </div>
              <Link className="misc-button misc-button--secondary" href={`/projects/${projectId}/editor` as Route}>
                Back to Editor
              </Link>
            </div>
          </div>

          {state.isLoading ? (
            <div className="preview-empty-state">
              <div className="preview-empty-state__phone" />
              <div>
                <h2>Loading preview</h2>
                <p>Gathering scene order, images, and playback details for this project.</p>
              </div>
            </div>
          ) : null}

          {!state.isLoading && state.errorMessage ? (
            <div className="preview-empty-state preview-empty-state--error">
              <div>
                <h2>Preview unavailable</h2>
                <p>{state.errorMessage}</p>
              </div>
            </div>
          ) : null}

          {!state.isLoading && !state.errorMessage && (playback?.scenes.length ?? 0) === 0 ? (
            <div className="preview-empty-state">
              <div>
                <h2>No scenes yet</h2>
                <p>Upload images in the editor to build a stitched mobile preview for this project.</p>
              </div>
            </div>
          ) : null}

          {!state.isLoading && !state.errorMessage && (playback?.scenes.length ?? 0) > 0 ? (
            <div className="preview-scroll-stack">
              <section className="preview-scene-section">
                <div className="preview-scene-copy">
                  <p className="preview-scene-copy__eyebrow">Stitched mobile player</p>
                  <h2>Timeline-aware preview</h2>
                  <p>
                    Each scene is stitched into a single vertical player using playback timing. Fallback-ready scenes remain visible so partially processed projects stay previewable.
                  </p>
                  <div className="preview-scene-copy__badges">
                    <span>{playback?.totalDurationMs ?? 0} ms total</span>
                    <span>{playback?.isFallback ? "Partial-ready playback" : "Fully ready playback"}</span>
                  </div>
                </div>

                <div className="preview-phone preview-phone--scene">
                  <div className="preview-phone__chrome">
                    <span className="preview-phone__dot" />
                    <span>{playback?.projectTitle}</span>
                  </div>

                  <div className="preview-phone__timeline">
                    {playback?.scenes.map((scene) => (
                      <section
                        className="preview-phone__timeline-scene"
                        key={scene.id}
                        style={{ minHeight: `${Math.max(240, Math.round((scene.durationMs ?? 2200) / 10))}px` }}
                      >
                        <PlaybackSceneRenderer scene={scene} isReducedMotion={playback.isReducedMotion} />

                        <div className="preview-phone__scene-overlay" />
                        <div className="preview-phone__scene-meta">
                          <span>{scene.title}</span>
                          <span>{scene.startsAtMs ?? 0} ms</span>
                        </div>
                      </section>
                    ))}
                  </div>
                </div>
              </section>

              {playback?.scenes.map((scene, index) => (
                <section className="preview-scene-section" key={scene.id}>
                  <div className="preview-scene-copy">
                    <p className="preview-scene-copy__eyebrow">{scene.title}</p>
                    <h2>{index === 0 ? "Opening frame" : "Next chapter"}</h2>
                    <p>{scene.detail}</p>
                    <div className="preview-scene-copy__badges">
                      <span>{scene.status}</span>
                      <span>{scene.durationMs ?? 2200} ms</span>
                      {scene.fallback ? <span>Fallback</span> : <span>Primary render</span>}
                    </div>
                  </div>
                </section>
              ))}
            </div>
          ) : null}
        </div>
      </section>
    </main>
  )
}



================================================
FILE: src/features/preview/lib/playback-client.ts
================================================
import type { EasingKey, GroupKey, MobileGroupScrollMapping, SceneGroupingConfig } from "@/modules/scenes/types"

export type ApiEnvelope<T> = {
  data: T
}

export type ApiErrorEnvelope = {
  error?: {
    message?: string
  }
}

export type ProjectSceneAssetRecord = {
  assetUrl: string
  assetType?: string
  layerOrder?: number | null
  metadataJson?: unknown
}

export type ProjectSceneRecord = {
  id: string
  orderIndex: number
  status: string
  contextText: string | null
  motionPreset?: string | null
  motionIntensity?: string | null
  sourceImageUrl: string | null
  thumbnailUrl: string | null
  framingData?: SceneGroupingConfig | null
  assets?: ProjectSceneAssetRecord[]
}

export type ProjectRecord = {
  id: string
  title: string
  status: string
  globalContext?: string | null
  stylePreset?: string | null
  outputFormat?: string
  guestSessionId?: string | null
  ownerId?: string | null
  claimedAt?: string | null
  scenes: ProjectSceneRecord[]
}

export type PlaybackLayerBehavior = {
  layerIndex?: number
  parallax?: number
  scale?: number
  opacity?: number
  groupKey?: GroupKey
  startProgress?: number
  endProgress?: number
  translateX?: number
  translateY?: number
  scaleFrom?: number
  scaleTo?: number
  opacityFrom?: number
  opacityTo?: number
  speedMultiplier?: number
  easing?: EasingKey
  mobile?: MobileGroupScrollMapping
  tablet?: MobileGroupScrollMapping
  desktop?: MobileGroupScrollMapping
}

export type PlaybackTimelineScene = {
  sceneId: string
  orderIndex: number
  status: string
  sourceImageUrl: string | null
  thumbnailUrl: string | null
  fallback: boolean
  startsAtMs: number
  durationMs: number
  cameraMovement?: string
  intensity?: string
  layerBehaviors?: PlaybackLayerBehavior[]
}

export type PlaybackResponse = {
  version?: number
  isFallback: boolean
  isReducedMotion: boolean
  timelineJson?: {
    scenes?: PlaybackTimelineScene[]
    summary?: {
      totalDurationMs?: number
    }
  }
}

export type NormalizedPlaybackSceneLayer = {
  assetUrl: string
  layerOrder: number
  metadataJson?: unknown
}

export type NormalizedPlaybackScene = {
  id: string
  orderIndex: number
  status: string
  title: string
  detail: string
  imageUrl: string | null
  fallback: boolean
  durationMs?: number
  startsAtMs?: number
  cameraMovement: string
  intensity: string
  contextText: string | null
  groupingConfig: SceneGroupingConfig | null
  layerBehaviors: PlaybackLayerBehavior[]
  layerAssets: NormalizedPlaybackSceneLayer[]
}

export type NormalizedPlaybackState = {
  projectTitle: string
  projectStatus: string
  isFallback: boolean
  isReducedMotion: boolean
  playbackVersion: number | null
  totalDurationMs: number
  scenes: NormalizedPlaybackScene[]
}

export function isRenderableImageUrl(value: string | null | undefined) {
  if (!value) {
    return false
  }

  return value.startsWith("https://") || value.startsWith("http://") || value.startsWith("/") || value.startsWith("data:")
}

export function resolveProjectSceneImage(scene: ProjectSceneRecord) {
  if (isRenderableImageUrl(scene.sourceImageUrl)) {
    return scene.sourceImageUrl
  }

  if (isRenderableImageUrl(scene.thumbnailUrl)) {
    return scene.thumbnailUrl
  }

  const assetUrl = scene.assets?.find((asset) => isRenderableImageUrl(asset.assetUrl))?.assetUrl
  return assetUrl ?? null
}

export async function parseApiResponse<T>(response: Response, fallbackMessage = "Request failed.") {
  const contentType = response.headers.get("content-type") ?? ""
  const payload = contentType.includes("application/json")
    ? ((await response.json().catch(() => null)) as ApiEnvelope<T> | ApiErrorEnvelope | null)
    : null

  if (!response.ok) {
    throw new Error(payload && "error" in payload ? payload.error?.message ?? fallbackMessage : fallbackMessage)
  }

  if (!payload || !("data" in payload)) {
    throw new Error("Unexpected response from the server.")
  }

  return payload.data
}

function normalizeProject(project: ProjectRecord | null | undefined) {
  return {
    title: project?.title ?? "Project Preview",
    status: project?.status ?? "draft",
    scenes: Array.isArray(project?.scenes) ? project.scenes : [],
  }
}

function normalizePlayback(playback: PlaybackResponse | null | undefined) {
  return {
    version: typeof playback?.version === "number" ? playback.version : null,
    isFallback: playback?.isFallback ?? false,
    isReducedMotion: playback?.isReducedMotion ?? false,
    totalDurationMs:
      typeof playback?.timelineJson?.summary?.totalDurationMs === "number" ? playback.timelineJson.summary.totalDurationMs : null,
    scenes: Array.isArray(playback?.timelineJson?.scenes) ? playback.timelineJson.scenes : [],
  }
}

function formatSceneTitle(index: number) {
  return `Scene ${String(index + 1).padStart(2, "0")}`
}

function formatSceneDetail(source: { startsAtMs?: number; durationMs?: number; contextText?: string | null; cameraMovement?: string }) {
  if (source.contextText) {
    return source.contextText
  }

  if (typeof source.startsAtMs === "number" && typeof source.durationMs === "number") {
    const startSeconds = (source.startsAtMs / 1000).toFixed(1)
    const durationSeconds = (source.durationMs / 1000).toFixed(1)
    const movement = source.cameraMovement ? ` - ${source.cameraMovement}` : ""
    return `Starts at ${startSeconds}s for ${durationSeconds}s${movement}`
  }

  return "Preview section ready for scroll playback."
}

function resolveLayerAssets(scene: ProjectSceneRecord | undefined) {
  return (scene?.assets ?? [])
    .filter((asset) => {
      if (!isRenderableImageUrl(asset.assetUrl)) {
        return false
      }

      if (asset.assetType) {
        return asset.assetType === "layer"
      }

      return typeof asset.layerOrder === "number"
    })
    .map((asset, index) => ({
      assetUrl: asset.assetUrl,
      layerOrder: typeof asset.layerOrder === "number" ? asset.layerOrder : index,
      metadataJson: asset.metadataJson,
    }))
    .sort((left, right) => left.layerOrder - right.layerOrder)
}

function parseSceneGroupingConfig(value: unknown): SceneGroupingConfig | null {
  if (!value || typeof value !== "object" || Array.isArray(value)) {
    return null
  }

  const record = value as Record<string, unknown>

  if (record.version !== 1 || !Array.isArray(record.groups)) {
    return null
  }

  return value as SceneGroupingConfig
}

export function buildNormalizedPlaybackState(project: ProjectRecord | null | undefined, playback: PlaybackResponse | null | undefined) {
  const normalizedProject = normalizeProject(project)
  const normalizedPlayback = normalizePlayback(playback)
  const projectScenes = [...normalizedProject.scenes].sort((left, right) => left.orderIndex - right.orderIndex)
  const projectScenesById = new Map(projectScenes.map((scene) => [scene.id, scene]))

  const scenesFromPlayback = normalizedPlayback.scenes
    .map((scene, index) => {
      const projectScene = projectScenesById.get(scene.sceneId)

      return {
        id: scene.sceneId,
        orderIndex: scene.orderIndex,
        status: scene.status,
        title: formatSceneTitle(index),
        detail: formatSceneDetail({
          startsAtMs: scene.startsAtMs,
          durationMs: scene.durationMs,
          cameraMovement: scene.cameraMovement,
          contextText: projectScene?.contextText,
        }),
        imageUrl:
          (isRenderableImageUrl(scene.sourceImageUrl) ? scene.sourceImageUrl : null) ??
          (isRenderableImageUrl(scene.thumbnailUrl) ? scene.thumbnailUrl : null) ??
          (projectScene ? resolveProjectSceneImage(projectScene) : null),
        fallback: scene.fallback,
        durationMs: scene.durationMs,
        startsAtMs: scene.startsAtMs,
        cameraMovement: scene.cameraMovement ?? "drift-up",
        intensity: scene.intensity ?? "medium",
        contextText: projectScene?.contextText ?? null,
        groupingConfig: parseSceneGroupingConfig(projectScene?.framingData),
        layerBehaviors: Array.isArray(scene.layerBehaviors) ? scene.layerBehaviors : [],
        layerAssets: resolveLayerAssets(projectScene),
      } satisfies NormalizedPlaybackScene
    })
    .sort((left, right) => left.orderIndex - right.orderIndex)
    .map((scene, index) => ({
      ...scene,
      title: formatSceneTitle(index),
    }))

  const scenesFromProject = projectScenes.map((scene, index) => ({
    id: scene.id,
    orderIndex: scene.orderIndex,
    status: scene.status,
    title: formatSceneTitle(index),
    detail: formatSceneDetail({ contextText: scene.contextText }),
    imageUrl: resolveProjectSceneImage(scene),
    fallback: false,
    durationMs: undefined,
    startsAtMs: undefined,
    cameraMovement: "drift-up",
    intensity: "medium",
    contextText: scene.contextText,
    groupingConfig: parseSceneGroupingConfig(scene.framingData),
    layerBehaviors: [],
    layerAssets: resolveLayerAssets(scene),
  }))

  const scenes = scenesFromPlayback.length > 0 ? scenesFromPlayback : scenesFromProject
  const totalDurationMs =
    normalizedPlayback.totalDurationMs ?? scenes.reduce((total, scene) => total + (scene.durationMs ?? 2200), 0)

  return {
    projectTitle: normalizedProject.title,
    projectStatus: normalizedProject.status,
    isFallback: normalizedPlayback.isFallback,
    isReducedMotion: normalizedPlayback.isReducedMotion,
    playbackVersion: normalizedPlayback.version,
    totalDurationMs,
    scenes,
  } satisfies NormalizedPlaybackState
}



================================================
FILE: src/features/projects/mock-projects.ts
================================================
export type MockProjectScene = {
  id: string
  name: string
  prompt: string
  contextText: string
  motionPreset: string
  motionIntensity: number
  status: string
  image: string
}

export type MockProject = {
  id: string
  title: string
  status: string
  updatedAt: string
  globalContext: string
  scenes: MockProjectScene[]
}

export const mockProjects: MockProject[] = [
  {
    id: "mock-amalfi-coast",
    title: "Sunset over Amalfi Coast",
    status: "draft",
    updatedAt: "2026-03-20T16:00:00.000Z",
    globalContext: "A cinematic journey along the Italian coast during summer sunset.",
    scenes: [
      {
        id: "mock-amalfi-scene-1",
        name: "Scene One",
        prompt:
          "Deep golden hour, volumetric lighting, slight mist over the Mediterranean, hyper-realistic parallax depth.",
        contextText: "Golden-hour terraces glow over the sea with layered depth and soft atmospheric haze.",
        motionPreset: "Cinematic Push",
        motionIntensity: 75,
        status: "ready",
        image:
          "https://lh3.googleusercontent.com/aida-public/AB6AXuA_v-7Nh0QR3utisJ4w0r88BIYx6IX78iUm2k3BMD86cmSlRTdr5eWbAyhuKJ4pDUQirkcRuzuZlD5A-0SNcnb_WGptKr-awW7jdxRTEFfw-uPrba4BVBgHvWKqfC7SvrZWCV_acNlnP2hkO6nE97djfCQFR_acNEzp2pIHXiU0QYv6buWNgUhDVbcOumCH_rFHYY65iOXfETauR6Yw7r5uvBSgTxPlGBt905IT-f2d47QmVmTnV55IcjdUcyMZtIvLO8_3eF78Amk",
      },
      {
        id: "mock-amalfi-scene-2",
        name: "Scene Two",
        prompt:
          "Cliffside terraces glow with warm sunset spill, layered buildings fade into sea haze, cinematic depth with gentle foreground separation.",
        contextText: "Terraced architecture slides past with a calm pan and layered foreground separation.",
        motionPreset: "Standard Pan",
        motionIntensity: 62,
        status: "ready",
        image:
          "https://lh3.googleusercontent.com/aida-public/AB6AXuBC3dtqQy_lVoORXf1yBbnAOOqeaBf6bs6JwxEAzRDFNWCpX8kXDYQC1a99tV4KYkWikGeuF-QzGRSooLvwtx8E3YIVF96zreFVRROsNNlUrofALxc1TgYbR3uLmBnZNQZ9_8u7T5bDqOIXN7uoNcA28iwesQUDKsIrYhqqk5BvZjjmQ1uYZfbE1lxVC9Tle7SvogoRfgyiXGQLIrBanEAOLcpSHAPLjHD0Lj79s-YmjqWHgCEIHRJ0LbbR5HqAPbdutl8_a2Ov2zE",
      },
      {
        id: "mock-amalfi-scene-3",
        name: "Scene Three",
        prompt:
          "A brighter harbor-facing angle with coastal reflections, soft atmosphere, and a calmer pace that emphasizes background depth.",
        contextText: "The harbor opens into a brighter final frame with reflections and slower pacing.",
        motionPreset: "Vertical Scroll",
        motionIntensity: 54,
        status: "ready",
        image:
          "https://lh3.googleusercontent.com/aida-public/AB6AXuD2SxaPbl5i3BcVyyiWZNME517Bb-fffNbkD-ZvkG7ZRf84QHhIDb5Iu4_HfiEYFvS87swKjMjAF6d3eyBKhbsk8gPU2yKnGrLaLoQ82wwBksubmTnlzkH3NZr7uPjqDEjfdOrzRCoZVqEaueawTUGPTOI4VdCH4gnyRthtCWDNB2NoReLeCZEMWW8DjPAfw4vRXt5_Jni-haCglUyMBli2-BFT1JLTdiAPTewxLVWNyNXXHOrz8B8WmxqUMqxs9zeIwQBnHFkUk64",
      },
    ],
  },
  {
    id: "mock-neon-district",
    title: "Neon District 2077",
    status: "ready",
    updatedAt: "2026-03-20T12:00:00.000Z",
    globalContext: "A rain-soaked cyberpunk promenade lit by holograms, reflections, and elevated transit lines.",
    scenes: [
      {
        id: "mock-neon-scene-1",
        name: "Arrival",
        prompt: "Street-level approach through neon haze with holographic signage and wet asphalt reflections.",
        contextText: "An opening descent through electric haze and reflective streets.",
        motionPreset: "Cinematic Push",
        motionIntensity: 68,
        status: "ready",
        image:
          "https://lh3.googleusercontent.com/aida-public/AB6AXuBoFq8kkz8XD3_sHKB4gbYv7biPF8GIE7kB6LO0hdVOty_oErCp79YiiIXxT5Um5XN0aLD5pa-tfNFL3T4CLTdKZ4tnAVsDOmVFPzhXIejL0Ti_7a-grst3W-t1vYMNqHmHdmgZ9X661JBBo8csic6KhfwbqwlmYMsuolpwbCKM6SKFcM0gQBoY2gbEH6yy-cm0Udj9SO6ev1YNAdl2pps9volpI1vXPb46skf8BFfDjsJnJfgQH5ejkWp5-m2ybsSZs0B8XOjPoKs",
      },
      {
        id: "mock-neon-scene-2",
        name: "Skybridge",
        prompt: "Elevated crosswalk overlooking the district with layered traffic trails and digital billboards.",
        contextText: "The camera floats into a skybridge reveal above the city pulse.",
        motionPreset: "Standard Pan",
        motionIntensity: 58,
        status: "ready",
        image:
          "https://lh3.googleusercontent.com/aida-public/AB6AXuCBW5wzJSHcAEggO2RYApU0PRnjWdyvBLXYfVfHK4flfPwMOaAZiwtIBuRZRJauseEfSlhK0TS6eHIeVOD9hGUIZsGpI4PYbqJneCK9zGBw9BMDuOJHrnmiEksL064I3nES0IPl8aF_fDmtUXC4iEQDLcHXQTuMQpjrfCppPou9Tbijdta9YZXYw3rjVfbgKsFsbw6PdN3kFBhwSz_hPWIYP2ZzejAk9u3QvmjgrUGFbXerUhR7SgwH-vbJI4LYoXx240AHQ76sBnw",
      },
      {
        id: "mock-neon-scene-3",
        name: "Final Glow",
        prompt: "Wide establishing shot as mist parts and the city core radiates with deep color contrast.",
        contextText: "A wide final reveal gives the district a glowing cinematic finish.",
        motionPreset: "Vertical Scroll",
        motionIntensity: 49,
        status: "ready",
        image:
          "https://lh3.googleusercontent.com/aida-public/AB6AXuD3rh2vc_ShENc9RR_DKqjTjm7lr3qV8bcmDPF6bcny9sy0G87IlhAn86umMKi8EKUAOaga6d4J2OY1CwPZ4a-WEfhl_V6xUkxMyopMI3-caa-9Cd1TK5SdyARlwz2r-IyZZasdA2DcQHaxGOjlcxXsUNMfIYgRh_tZi8NPkG2p22LU-hh7kVhiQ8q2QD1lyKx3pq7MMHpkrCJwV4AMbPNn5Hr0aiUrCCIiIJI5RDVPicGe_LM04tsHDImJnTn9olHtHfCYhnq7EQE",
      },
    ],
  },
  {
    id: "mock-desert-mirage",
    title: "Desert Mirage",
    status: "in_review",
    updatedAt: "2026-03-19T18:30:00.000Z",
    globalContext: "A sun-baked desert passage with monumental silhouettes, heat haze, and patient vertical movement.",
    scenes: [
      {
        id: "mock-desert-scene-1",
        name: "Dune Rise",
        prompt: "Low-angle dune crest with heat distortion and long shadows sweeping across the sand.",
        contextText: "The story opens with a slow rise over sculpted dunes and heat shimmer.",
        motionPreset: "Cinematic Push",
        motionIntensity: 60,
        status: "ready",
        image:
          "https://lh3.googleusercontent.com/aida-public/AB6AXuBjHqqSUJGnNViyVkKel9HZFklvYP7NR4rAq396D1PziqpLKA6rYsGdblMWwlWfbSSffp-tLLoV_3E9LOP5tnnxTyAwfOCyII4AEZ-AI4KjHcoUiwfzOc87Cepq7vZKKb6rfhgV3t_wlNFegZZYZPIPsBtw6WtPssKM7TUvEHD4cKgeuE_UA4J2UhxDDNXYg-9CcsjXVk7g96CXr5CLJNzdgPk1tdFm5JSK-ApQ5kSrQz_Vj17zSKbYcsQBbyY1utKQ75qHq399LYg",
      },
      {
        id: "mock-desert-scene-2",
        name: "Stone Gate",
        prompt: "Ancient desert architecture emerges through dust with layered foreground rock forms.",
        contextText: "A stone gateway appears through suspended dust and carved rock depth.",
        motionPreset: "Standard Pan",
        motionIntensity: 47,
        status: "ready",
        image:
          "https://lh3.googleusercontent.com/aida-public/AB6AXuArYAKv1sP9E8dctg89nU6-KbyG5P9M5j7CSARHJ-8-OJzvTV5f0goKUEtGvSgLj5fkT1S5d5_r7qkJ-5p0x1N0O2N2cv-HjIgAnXU3UK0A3vLxZcGUEQd6Em9q0R2lQim2OtS6zOG8hY4qT6mSYgX3VT_0LIW4kMX9l0oM5r4n9Q2N3K2c2Pjlwm0r7k2Nq1aL7xvP0-4Eq8Gqv9Q",
      },
    ],
  },
]

export function getMockProjectById(projectId: string) {
  return mockProjects.find((project) => project.id === projectId) ?? null
}

export function isMockProjectId(projectId: string) {
  return getMockProjectById(projectId) !== null
}



================================================
FILE: src/features/projects/components/new-project-form.tsx
================================================
"use client"

import { useEffect, useRef, useState, type ChangeEvent, type DragEvent, type FormEvent } from "react"
import Link from "next/link"
import { useRouter } from "next/navigation"

import { AppIcon } from "@/features/shared/components/app-icon"

type QueueItem = {
  id: string
  file: File
  previewUrl: string
  width?: number
  height?: number
}

type ApiSuccess<T> = {
  data: T
}

type ProjectResponse = {
  id: string
}

type UploadContract = {
  uploadToken: string
  uploadUrl: string
  storageKey: string
  expiresAt: string
  mimeType: string
  sizeBytes: number
}

async function readImageDimensions(file: File) {
  const objectUrl = URL.createObjectURL(file)

  try {
    const dimensions = await new Promise<{ width?: number; height?: number }>((resolve) => {
      const image = new Image()

      image.onload = () => {
        resolve({ width: image.naturalWidth, height: image.naturalHeight })
      }

      image.onerror = () => {
        resolve({})
      }

      image.src = objectUrl
    })

    return dimensions
  } finally {
    URL.revokeObjectURL(objectUrl)
  }
}

async function parseJsonResponse<T>(response: Response) {
  const payload = (await response.json().catch(() => null)) as
    | ApiSuccess<T>
    | { error?: { message?: string } }
    | null

  if (!response.ok) {
    throw new Error(payload && "error" in payload ? payload.error?.message ?? "Request failed." : "Request failed.")
  }

  if (!payload || !("data" in payload)) {
    throw new Error("Unexpected response from the server.")
  }

  return payload.data
}

function reorderItems(items: QueueItem[], activeId: string, targetId: string) {
  const activeIndex = items.findIndex((item) => item.id === activeId)
  const targetIndex = items.findIndex((item) => item.id === targetId)

  if (activeIndex === -1 || targetIndex === -1 || activeIndex === targetIndex) {
    return items
  }

  const nextItems = [...items]
  const [activeItem] = nextItems.splice(activeIndex, 1)
  nextItems.splice(targetIndex, 0, activeItem)
  return nextItems
}

export function NewProjectForm() {
  const router = useRouter()
  const fileInputRef = useRef<HTMLInputElement | null>(null)
  const queueItemsRef = useRef<QueueItem[]>([])
  const [title, setTitle] = useState("Sunset over Amalfi Coast")
  const [globalContext, setGlobalContext] = useState(
    "A cinematic coastal journey during golden hour with gentle vertical pacing.",
  )
  const [stylePreset, setStylePreset] = useState("Cinematic Push")
  const [queueItems, setQueueItems] = useState<QueueItem[]>([])
  const [isSubmitting, setIsSubmitting] = useState(false)
  const [feedback, setFeedback] = useState<string | null>(null)
  const [errorMessage, setErrorMessage] = useState<string | null>(null)
  const [draggedItemId, setDraggedItemId] = useState<string | null>(null)
  const [dragTargetId, setDragTargetId] = useState<string | null>(null)

  useEffect(() => {
    queueItemsRef.current = queueItems
  }, [queueItems])

  useEffect(() => {
    return () => {
      for (const item of queueItemsRef.current) {
        URL.revokeObjectURL(item.previewUrl)
      }
    }
  }, [])

  async function handleFileSelection(event: ChangeEvent<HTMLInputElement>) {
    const selectedFiles = Array.from(event.target.files ?? [])

    if (selectedFiles.length === 0) {
      return
    }

    const nextItems = await Promise.all(
      selectedFiles.map(async (file) => {
        const dimensions = await readImageDimensions(file)

        return {
          id: crypto.randomUUID(),
          file,
          previewUrl: URL.createObjectURL(file),
          width: dimensions.width,
          height: dimensions.height,
        } satisfies QueueItem
      }),
    )

    setQueueItems((current) => [...current, ...nextItems])
    setErrorMessage(null)
    setFeedback(`${selectedFiles.length} image${selectedFiles.length === 1 ? "" : "s"} added to the story queue.`)
    event.target.value = ""
  }

  function removeQueueItem(itemId: string) {
    setQueueItems((current) => {
      const item = current.find((entry) => entry.id === itemId)

      if (item) {
        URL.revokeObjectURL(item.previewUrl)
      }

      return current.filter((entry) => entry.id !== itemId)
    })
  }

  async function ensureGuestSession() {
    const response = await fetch("/api/v1/guest-sessions", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
    })

    await parseJsonResponse<{ id: string }>(response)
  }

  async function createProject() {
    const requestBody = {
      title,
      globalContext: globalContext.trim() ? globalContext : null,
      stylePreset: stylePreset.trim() ? stylePreset : null,
    }

    let response = await fetch("/api/v1/projects", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify(requestBody),
    })

    if (response.status === 401) {
      await ensureGuestSession()
      response = await fetch("/api/v1/projects", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(requestBody),
      })
    }

    return parseJsonResponse<ProjectResponse>(response)
  }

  async function handleSubmit(event: FormEvent<HTMLFormElement>) {
    event.preventDefault()

    if (!title.trim()) {
      setErrorMessage("Add a project title before creating your story.")
      return
    }

    if (queueItems.length === 0) {
      setErrorMessage("Upload at least one image to build your first story sequence.")
      return
    }

    setIsSubmitting(true)
    setErrorMessage(null)

    try {
      setFeedback("Creating project shell...")
      const project = await createProject()

      setFeedback("Preparing upload slots...")
      const uploadContracts = await parseJsonResponse<{ uploads: UploadContract[] }>(
        await fetch(`/api/v1/projects/${project.id}/uploads/init`, {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify({
            files: queueItems.map(({ file }) => ({
              filename: file.name,
              mimeType: file.type || "application/octet-stream",
              sizeBytes: file.size,
            })),
          }),
        }),
      )

      setFeedback("Uploading images to the scene queue...")

      await Promise.all(
        uploadContracts.uploads.map((contract, index) =>
          fetch(contract.uploadUrl, {
            method: "PUT",
            headers: {
              "Content-Type": queueItems[index]?.file.type || contract.mimeType,
            },
            body: queueItems[index]?.file,
          }).then((response) => parseJsonResponse<{ accepted: boolean }>(response)),
        ),
      )

      setFeedback("Finalizing scene order...")
      await parseJsonResponse<unknown>(
        await fetch(`/api/v1/projects/${project.id}/uploads/finalize`, {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify({
            uploads: queueItems.map((item, index) => ({
              uploadToken: uploadContracts.uploads[index]?.uploadToken,
              originalFilename: item.file.name,
              mimeType: item.file.type || uploadContracts.uploads[index]?.mimeType || "application/octet-stream",
              sizeBytes: item.file.size,
              width: item.width,
              height: item.height,
            })),
          }),
        }),
      )

      setFeedback("Project ready. Opening the editor...")
      router.push(`/projects/${project.id}/editor`)
    } catch (error) {
      setErrorMessage(error instanceof Error ? error.message : "Something went wrong while creating the project.")
      setFeedback(null)
    } finally {
      setIsSubmitting(false)
    }
  }

  return (
    <form className="misc-form new-project-form" onSubmit={handleSubmit}>
      <label className="misc-field">
        <span>Project Title</span>
        <input onChange={(event) => setTitle(event.target.value)} type="text" value={title} />
      </label>

      <label className="misc-field">
        <span>Global Context</span>
        <textarea onChange={(event) => setGlobalContext(event.target.value)} rows={5} value={globalContext} />
      </label>

      <label className="misc-field">
        <span>Style Preset</span>
        <input onChange={(event) => setStylePreset(event.target.value)} type="text" value={stylePreset} />
      </label>

      <section className="new-project-upload-panel">
        <div className="new-project-upload-panel__header">
          <div>
            <p className="misc-kicker">Uploads</p>
            <h2>Build your story sequence</h2>
            <p className="misc-copy">
              Upload multiple images at once, then drag them into the order you want viewers to move through the story.
            </p>
          </div>

          <button
            className="misc-button misc-button--secondary new-project-upload-panel__button"
            onClick={() => fileInputRef.current?.click()}
            type="button"
          >
            <AppIcon className="new-project-upload-panel__button-icon" name="upload_file" />
            Select Images
          </button>
        </div>

        <input
          accept="image/*"
          className="new-project-file-input"
          hidden
          multiple
          onChange={handleFileSelection}
          ref={fileInputRef}
          type="file"
        />

        <div className="new-project-dropzone">
          <AppIcon className="new-project-dropzone__icon" name="layers" />
          <div>
            <strong>{queueItems.length === 0 ? "No images added yet" : `${queueItems.length} image${queueItems.length === 1 ? "" : "s"} ready`}</strong>
            <p>Each uploaded image becomes the next page/scene in your story. Drag cards below to reorder the sequence.</p>
          </div>
        </div>

        {queueItems.length > 0 ? (
          <div className="new-project-queue">
            {queueItems.map((item, index) => (
              <article
                className={dragTargetId === item.id ? "new-project-queue__item is-drag-target" : "new-project-queue__item"}
                draggable
                key={item.id}
                onDragEnd={() => {
                  setDraggedItemId(null)
                  setDragTargetId(null)
                }}
                onDragOver={(event) => {
                  event.preventDefault()
                  if (draggedItemId && draggedItemId !== item.id) {
                    setDragTargetId(item.id)
                  }
                }}
                onDragStart={() => {
                  setDraggedItemId(item.id)
                  setDragTargetId(item.id)
                }}
                onDrop={(event: DragEvent<HTMLElement>) => {
                  event.preventDefault()

                  if (!draggedItemId || draggedItemId === item.id) {
                    setDraggedItemId(null)
                    setDragTargetId(null)
                    return
                  }

                  setQueueItems((current) => reorderItems(current, draggedItemId, item.id))
                  setDraggedItemId(null)
                  setDragTargetId(null)
                }}
              >
                <div className="new-project-queue__handle" title="Drag to reorder">
                  <AppIcon className="new-project-queue__handle-icon" name="drag_indicator" />
                </div>

                <div className="new-project-queue__preview" style={{ backgroundImage: `url("${item.previewUrl}")` }} />

                <div className="new-project-queue__meta">
                  <div className="new-project-queue__order">Scene {String(index + 1).padStart(2, "0")}</div>
                  <strong>{item.file.name}</strong>
                  <p>
                    {(item.file.size / (1024 * 1024)).toFixed(1)} MB
                    {item.width && item.height ? ` • ${item.width}x${item.height}` : ""}
                  </p>
                </div>

                <button className="new-project-queue__remove" onClick={() => removeQueueItem(item.id)} type="button">
                  <AppIcon className="new-project-queue__remove-icon" name="delete" />
                  Remove
                </button>
              </article>
            ))}
          </div>
        ) : null}

        {feedback ? <p className="new-project-feedback">{feedback}</p> : null}
        {errorMessage ? <p className="new-project-error">{errorMessage}</p> : null}
      </section>

      <div className="misc-actions">
        <button className="misc-button misc-button--primary" disabled={isSubmitting} type="submit">
          {isSubmitting ? "Creating Project..." : "Create Project"}
        </button>
        <Link className="misc-button misc-button--secondary" href="/projects">
          Back to Projects
        </Link>
      </div>
    </form>
  )
}



================================================
FILE: src/features/projects/components/new-project-page.tsx
================================================
import { AppHeader } from "@/features/shared/components/app-header"

import { NewProjectForm } from "./new-project-form"

export function NewProjectPage() {
  return (
    <main className="misc-screen">
      <AppHeader active="new" />

      <section className="misc-shell misc-shell--wide">
        <div className="misc-panel">
          <div className="new-project-intro">
            <p className="misc-kicker">Create</p>
            <h1>Start a new parallax story</h1>
            <p className="misc-copy">
              Set the story tone, upload all of your source images in one pass, and arrange them into the exact order you want the final sequence to follow.
            </p>
          </div>

          <NewProjectForm />
        </div>
      </section>
    </main>
  )
}



================================================
FILE: src/features/projects/components/project-card.tsx
================================================
import type { Route } from "next"
import Link from "next/link"

import { AppIcon } from "@/features/shared/components/app-icon"

type ProjectCardProps = {
  title: string
  scenes: string
  updatedAt: string
  projectId: string
  image?: string | null
  viewMode?: "carousel" | "grid"
}

export function ProjectCard({ title, scenes, updatedAt, projectId, image, viewMode = "grid" }: ProjectCardProps) {
  const cardClassName =
    viewMode === "grid" ? "projects-card projects-card--grid-compact" : "projects-card"

  return (
    <article className={cardClassName}>
      <div className="projects-card__visual">
        <div className="projects-card__overlay" />
        <div className="projects-card__image" style={image ? { backgroundImage: `url("${image}")` } : undefined} />
        <div className="projects-card__meta">
          <h3>{title}</h3>
          <div>
            <span>
              <AppIcon className="projects-card__meta-icon" name="movie" />
              {scenes} Scenes
            </span>
            <span>
              <AppIcon className="projects-card__meta-icon" name="schedule" />
              {updatedAt}
            </span>
          </div>
        </div>
      </div>

      <div className="projects-card__actions">
        <Link className="projects-button projects-button--solid" href={`/projects/${projectId}/editor` as Route}>
          <AppIcon className="projects-inline-icon" name="edit" />
          Open Editor
        </Link>

        <div className="projects-card__secondary-actions">
          <Link className="projects-button projects-button--secondary" href={`/projects/${projectId}/preview` as Route}>
            <AppIcon className="projects-inline-icon" name="visibility" />
            Preview
          </Link>
          <button className="projects-button projects-button--secondary is-disabled" disabled type="button">
            <AppIcon className="projects-inline-icon" name="download" />
            Export
          </button>
        </div>
      </div>
    </article>
  )
}



================================================
FILE: src/features/projects/components/project-editor-page.tsx
================================================
"use client"

import {
  useCallback,
  useEffect,
  useMemo,
  useRef,
  useState,
  type ChangeEvent,
  type KeyboardEvent as ReactKeyboardEvent,
  type PointerEvent as ReactPointerEvent,
  type WheelEvent as ReactWheelEvent,
} from "react"
import type { Route } from "next"
import Link from "next/link"

import { PlaybackSceneRenderer } from "@/features/preview/components/playback-scene-renderer"
import {
  buildNormalizedPlaybackState,
  parseApiResponse,
  resolveProjectSceneImage,
  type ApiErrorEnvelope,
  type ApiEnvelope,
  type NormalizedPlaybackState,
  type PlaybackResponse,
  type ProjectRecord,
} from "@/features/preview/lib/playback-client"
import { AppHeader } from "@/features/shared/components/app-header"
import { AppIcon } from "@/features/shared/components/app-icon"
import type { GroupKey, MobileGroupScrollMapping, SceneGroupingConfig } from "@/modules/scenes/types"

type ProjectEditorPageProps = {
  projectId: string
}

type SessionActor =
  | { kind: "anonymous" }
  | { kind: "guest"; guestSessionId: string; expiresAt: string }
  | { kind: "authenticated"; userId: string; email?: string | null; guestSessionId?: string | null }

type SceneRecord = ProjectRecord["scenes"][number]

type UploadContract = {
  uploadToken: string
  uploadUrl: string
  mimeType: string
}

const GROUP_KEYS: GroupKey[] = ["background", "midground", "foreground"]

const GROUP_LABELS: Record<GroupKey, string> = {
  background: "Background",
  midground: "Midground",
  foreground: "Foreground",
}

const DEFAULT_GROUP_MAPPINGS: Record<GroupKey, MobileGroupScrollMapping> = {
  background: {
    startProgress: 0,
    endProgress: 1,
    translateX: -6,
    translateY: -18,
    scaleFrom: 1,
    scaleTo: 1.06,
    opacityFrom: 1,
    opacityTo: 0.94,
    speedMultiplier: 0.72,
    easing: "ease-out",
  },
  midground: {
    startProgress: 0,
    endProgress: 1,
    translateX: 0,
    translateY: -30,
    scaleFrom: 1,
    scaleTo: 1.1,
    opacityFrom: 1,
    opacityTo: 0.98,
    speedMultiplier: 1,
    easing: "linear",
  },
  foreground: {
    startProgress: 0,
    endProgress: 1,
    translateX: 10,
    translateY: -46,
    scaleFrom: 1,
    scaleTo: 1.16,
    opacityFrom: 1,
    opacityTo: 1,
    speedMultiplier: 1.22,
    easing: "ease-in-out",
  },
}

const GROUP_MAPPING_FIELDS: Array<{
  field: keyof MobileGroupScrollMapping
  label: string
  type: "number" | "select"
  step?: number
  min?: number
  max?: number
}> = [
  { field: "startProgress", label: "Start Progress", type: "number", step: 0.01, min: 0, max: 1 },
  { field: "endProgress", label: "End Progress", type: "number", step: 0.01, min: 0, max: 1 },
  { field: "translateX", label: "Translate X", type: "number", step: 1, min: -1000, max: 1000 },
  { field: "translateY", label: "Translate Y", type: "number", step: 1, min: -1000, max: 1000 },
  { field: "scaleFrom", label: "Scale From", type: "number", step: 0.01, min: 0.1, max: 3 },
  { field: "scaleTo", label: "Scale To", type: "number", step: 0.01, min: 0.1, max: 3 },
  { field: "opacityFrom", label: "Opacity From", type: "number", step: 0.01, min: 0, max: 1 },
  { field: "opacityTo", label: "Opacity To", type: "number", step: 0.01, min: 0, max: 1 },
  { field: "speedMultiplier", label: "Speed Multiplier", type: "number", step: 0.01, min: 0, max: 5 },
  { field: "easing", label: "Easing", type: "select" },
]

function cloneGroupingConfig(grouping: SceneGroupingConfig | null): SceneGroupingConfig | null {
  return grouping ? JSON.parse(JSON.stringify(grouping)) as SceneGroupingConfig : null
}

function sortLayerIndexes(indexes: number[]) {
  return [...indexes].sort((left, right) => left - right)
}

function buildAutoGroupingFromScene(scene: SceneRecord | null): SceneGroupingConfig | null {
  const layerIndexes = (scene?.assets ?? [])
    .filter((asset) => asset.assetType === "layer")
    .map((asset, index) => (typeof asset.layerOrder === "number" ? asset.layerOrder : index))
    .sort((left, right) => left - right)

  if (layerIndexes.length === 0) {
    return null
  }

  const buckets: Record<GroupKey, number[]> = {
    background: [],
    midground: [],
    foreground: [],
  }

  layerIndexes.forEach((layerIndex, position) => {
    const ratio = layerIndexes.length <= 1 ? 0.5 : position / (layerIndexes.length - 1)
    const groupKey = ratio <= 0.33 ? "background" : ratio >= 0.66 ? "foreground" : "midground"
    buckets[groupKey].push(layerIndex)
  })

  return {
    version: 1,
    groups: GROUP_KEYS.map((groupKey) => ({
      groupKey,
      layerIndexes: buckets[groupKey],
      mobile: { ...DEFAULT_GROUP_MAPPINGS[groupKey] },
    })),
  }
}

function ensureSceneGrouping(scene: SceneRecord | null, grouping: SceneGroupingConfig | null | undefined) {
  const layerIndexes = (scene?.assets ?? [])
    .filter((asset) => asset.assetType === "layer")
    .map((asset, index) => (typeof asset.layerOrder === "number" ? asset.layerOrder : index))

  if (layerIndexes.length === 0) {
    return null
  }

  const assignedLayerIndexes = new Set(grouping?.groups.flatMap((group) => group.layerIndexes) ?? [])
  const unassignedLayerIndexes = layerIndexes.filter((layerIndex) => !assignedLayerIndexes.has(layerIndex))

  return {
    version: 1,
    groups: GROUP_KEYS.map((groupKey) => {
      const existingGroup = grouping?.groups.find((group) => group.groupKey === groupKey)

      return {
        groupKey,
        layerIndexes: sortLayerIndexes([
          ...(existingGroup?.layerIndexes ?? []),
          ...(groupKey === "midground" ? unassignedLayerIndexes : []),
        ]),
        mobile: { ...(existingGroup?.mobile ?? DEFAULT_GROUP_MAPPINGS[groupKey]) },
      }
    }),
  } satisfies SceneGroupingConfig
}

async function readImageDimensions(file: File) {
  const objectUrl = URL.createObjectURL(file)

  try {
    return await new Promise<{ width?: number; height?: number }>((resolve) => {
      const image = new Image()

      image.onload = () => {
        resolve({ width: image.naturalWidth, height: image.naturalHeight })
      }

      image.onerror = () => {
        resolve({})
      }

      image.src = objectUrl
    })
  } finally {
    URL.revokeObjectURL(objectUrl)
  }
}

async function parseJsonResponse<T>(response: Response) {
  const contentType = response.headers.get("content-type") ?? ""
  const payload = contentType.includes("application/json")
    ? ((await response.json().catch(() => null)) as ApiEnvelope<T> | ApiErrorEnvelope | null)
    : null

  if (!response.ok) {
    throw new Error(payload && "error" in payload ? payload.error?.message ?? "Request failed." : "Request failed.")
  }

  if (!payload || !("data" in payload)) {
    throw new Error("Unexpected response from the server.")
  }

  return payload.data
}

async function ensureGuestSession() {
  await parseJsonResponse<{ id: string }>(
    await fetch("/api/v1/guest-sessions", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
    }),
  )
}

export function ProjectEditorPage({ projectId }: ProjectEditorPageProps) {
  const fileInputRef = useRef<HTMLInputElement | null>(null)
  const scrubRailRef = useRef<HTMLDivElement | null>(null)
  const [project, setProject] = useState<ProjectRecord | null>(null)
  const [playback, setPlayback] = useState<NormalizedPlaybackState | null>(null)
  const [actor, setActor] = useState<SessionActor>({ kind: "anonymous" })
  const [activeSceneIndex, setActiveSceneIndex] = useState(0)
  const [projectTitle, setProjectTitle] = useState("")
  const [projectContext, setProjectContext] = useState("")
  const [projectStylePreset, setProjectStylePreset] = useState("")
  const [sceneContext, setSceneContext] = useState("")
  const [sceneMotionPreset, setSceneMotionPreset] = useState("Standard Pan")
  const [sceneMotionIntensity, setSceneMotionIntensity] = useState("medium")
  const [isLoading, setIsLoading] = useState(true)
  const [isSaving, setIsSaving] = useState(false)
  const [feedback, setFeedback] = useState<string | null>(null)
  const [errorMessage, setErrorMessage] = useState<string | null>(null)
  const [isUploading, setIsUploading] = useState(false)
  const [activeSceneProgress, setActiveSceneProgress] = useState(0)
  const [selectedGroup, setSelectedGroup] = useState<GroupKey>("midground")
  const [editableSceneGrouping, setEditableSceneGrouping] = useState<SceneGroupingConfig | null>(null)
  const [savedGroupingSnapshot, setSavedGroupingSnapshot] = useState<SceneGroupingConfig | null>(null)
  const [groupMappingDraft, setGroupMappingDraft] = useState<MobileGroupScrollMapping>(DEFAULT_GROUP_MAPPINGS.midground)

  const loadProject = useCallback(async () => {
    setIsLoading(true)

      try {
      const [projectResult, sessionResult, playbackResult] = await Promise.allSettled([
        fetch(`/api/v1/projects/${projectId}`, { cache: "no-store" }).then((response) => parseApiResponse<ProjectRecord>(response)),
        fetch("/api/v1/auth/session", { cache: "no-store" }).then((response) => parseApiResponse<{ actor: SessionActor }>(response)),
        fetch(`/api/v1/projects/${projectId}/preview/playback`, { cache: "no-store" }).then((response) =>
          parseApiResponse<PlaybackResponse>(response),
        ),
      ])

      if (projectResult.status !== "fulfilled" || sessionResult.status !== "fulfilled") {
        throw new Error("Unable to load this project.")
      }

      const projectData = projectResult.value
      const sessionData = sessionResult.value

      setProject(projectData)
      setPlayback(buildNormalizedPlaybackState(projectData, playbackResult.status === "fulfilled" ? playbackResult.value : null))
      setActor(sessionData.actor)
      setProjectTitle(projectData.title)
      setProjectContext(projectData.globalContext ?? "")
      setProjectStylePreset(projectData.stylePreset ?? "")

      const nextScene = projectData.scenes[activeSceneIndex] ?? projectData.scenes[0]
      setActiveSceneIndex(nextScene ? projectData.scenes.findIndex((scene) => scene.id === nextScene.id) : 0)
      setSceneContext(nextScene?.contextText ?? "")
      setSceneMotionPreset(nextScene?.motionPreset ?? "Standard Pan")
      setSceneMotionIntensity(nextScene?.motionIntensity ?? "medium")
      setErrorMessage(null)
    } catch (error) {
      setPlayback(null)
      setErrorMessage(error instanceof Error ? error.message : "Unable to load this project.")
    } finally {
      setIsLoading(false)
    }
  }, [activeSceneIndex, projectId])

  useEffect(() => {
    void loadProject()
  }, [loadProject])

  const scenes = project?.scenes ?? []
  const activeScene = scenes[activeSceneIndex] ?? scenes[0] ?? null

  const activeSceneId = activeScene?.id
  const activePlaybackScene = playback?.scenes.find((scene) => scene.id === activeSceneId) ?? playback?.scenes[activeSceneIndex] ?? null
  const activeSceneLayerAssets = useMemo(
    () =>
      (activeScene?.assets ?? [])
        .filter((asset) => asset.assetType === "layer")
        .map((asset, index) => ({
          ...asset,
          resolvedLayerIndex: typeof asset.layerOrder === "number" ? asset.layerOrder : index,
        }))
        .sort((left, right) => left.resolvedLayerIndex - right.resolvedLayerIndex),
    [activeScene],
  )
  const activeGroupConfig = editableSceneGrouping?.groups.find((group) => group.groupKey === selectedGroup) ?? null

  const updateSceneProgress = useCallback((value: number) => {
    setActiveSceneProgress(Math.min(1, Math.max(0, value)))
  }, [])

  const updateSceneProgressFromClientY = useCallback(
    (clientY: number) => {
      const element = scrubRailRef.current

      if (!element) {
        return
      }

      const bounds = element.getBoundingClientRect()
      const ratio = (clientY - bounds.top) / bounds.height
      updateSceneProgress(ratio)
    },
    [updateSceneProgress],
  )

  useEffect(() => {
    if (!activeScene) {
      setSceneContext("")
      setSceneMotionPreset("Standard Pan")
      setSceneMotionIntensity("medium")
      setEditableSceneGrouping(null)
      setSavedGroupingSnapshot(null)
      setGroupMappingDraft(DEFAULT_GROUP_MAPPINGS.midground)
      return
    }

    setSceneContext(activeScene.contextText ?? "")
    setSceneMotionPreset(activeScene.motionPreset ?? "Standard Pan")
    setSceneMotionIntensity(activeScene.motionIntensity ?? "medium")
    const nextGrouping = ensureSceneGrouping(activeScene, activeScene.framingData ?? activePlaybackScene?.groupingConfig ?? buildAutoGroupingFromScene(activeScene))
    setEditableSceneGrouping(cloneGroupingConfig(nextGrouping))
    setSavedGroupingSnapshot(cloneGroupingConfig(nextGrouping))
  }, [activePlaybackScene?.groupingConfig, activeScene, activeSceneId])

  useEffect(() => {
    const nextDraft = editableSceneGrouping?.groups.find((group) => group.groupKey === selectedGroup)?.mobile

    if (nextDraft) {
      setGroupMappingDraft({ ...nextDraft })
    }
  }, [editableSceneGrouping, selectedGroup])

  useEffect(() => {
    setActiveSceneProgress(0)
  }, [activeSceneId])

  const handleScrubPointerDown = useCallback(
    (event: ReactPointerEvent<HTMLDivElement>) => {
      event.preventDefault()
      updateSceneProgressFromClientY(event.clientY)

      const handlePointerMove = (nextEvent: PointerEvent) => {
        updateSceneProgressFromClientY(nextEvent.clientY)
      }

      const handlePointerUp = () => {
        window.removeEventListener("pointermove", handlePointerMove)
        window.removeEventListener("pointerup", handlePointerUp)
      }

      window.addEventListener("pointermove", handlePointerMove)
      window.addEventListener("pointerup", handlePointerUp)
    },
    [updateSceneProgressFromClientY],
  )

  const handleStageWheel = useCallback(
    (event: ReactWheelEvent<HTMLDivElement>) => {
      if (!activePlaybackScene) {
        return
      }

      event.preventDefault()
      updateSceneProgress(activeSceneProgress + event.deltaY / 800)
    },
    [activePlaybackScene, activeSceneProgress, updateSceneProgress],
  )

  const handleScrubKeyDown = useCallback(
    (event: ReactKeyboardEvent<HTMLDivElement>) => {
      if (!activePlaybackScene) {
        return
      }

      if (event.key === "ArrowUp" || event.key === "ArrowLeft") {
        event.preventDefault()
        updateSceneProgress(activeSceneProgress - 0.05)
      }

      if (event.key === "ArrowDown" || event.key === "ArrowRight") {
        event.preventDefault()
        updateSceneProgress(activeSceneProgress + 0.05)
      }

      if (event.key === "Home") {
        event.preventDefault()
        updateSceneProgress(0)
      }

      if (event.key === "End") {
        event.preventDefault()
        updateSceneProgress(1)
      }
    },
    [activePlaybackScene, activeSceneProgress, updateSceneProgress],
  )

  const activeSceneDurationMs = activePlaybackScene?.durationMs ?? 2200
  const activeSceneScrubTimeMs = Math.round(activeSceneDurationMs * activeSceneProgress)
  const activeSceneProgressPercent = Math.round(activeSceneProgress * 100)

  const canClaimProject =
    actor.kind === "authenticated" &&
    Boolean(actor.guestSessionId && project?.guestSessionId && !project.ownerId && !project.claimedAt)

  const generateLabel = useMemo(() => {
    if (!project) {
      return "Generate"
    }

    return project.scenes.some((scene) => scene.status !== "ready") ? "Generate" : "Regenerate All"
  }, [project])

  const buildSceneUpdatePayload = useCallback(() => ({
    contextText: sceneContext.trim() ? sceneContext : null,
    motionPreset: sceneMotionPreset,
    motionIntensity: sceneMotionIntensity,
    grouping: editableSceneGrouping,
  }), [editableSceneGrouping, sceneContext, sceneMotionIntensity, sceneMotionPreset])

  const handleSelectGroup = useCallback((groupKey: GroupKey) => {
    setSelectedGroup(groupKey)
  }, [])

  const handleAssignLayerToGroup = useCallback((layerIndex: number, groupKey: GroupKey) => {
    setEditableSceneGrouping((currentGrouping) => {
      const nextGrouping = ensureSceneGrouping(activeScene, currentGrouping ?? buildAutoGroupingFromScene(activeScene))

      if (!nextGrouping) {
        return nextGrouping
      }

      return {
        version: 1,
        groups: nextGrouping.groups.map((group) => ({
          ...group,
          layerIndexes: group.groupKey === groupKey
            ? sortLayerIndexes([...group.layerIndexes.filter((item) => item !== layerIndex), layerIndex])
            : group.layerIndexes.filter((item) => item !== layerIndex),
        })),
      }
    })
    setSelectedGroup(groupKey)
  }, [activeScene])

  const handleAutoAssignLayers = useCallback(() => {
    const nextGrouping = buildAutoGroupingFromScene(activeScene)

    if (!nextGrouping) {
      return
    }

    setEditableSceneGrouping(nextGrouping)
    setSelectedGroup("midground")
  }, [activeScene])

  const handleGroupMappingChange = useCallback(
    (groupKey: GroupKey, field: keyof MobileGroupScrollMapping, value: number | MobileGroupScrollMapping["easing"]) => {
      setEditableSceneGrouping((currentGrouping) => {
        const nextGrouping = ensureSceneGrouping(activeScene, currentGrouping ?? buildAutoGroupingFromScene(activeScene))

        if (!nextGrouping) {
          return nextGrouping
        }

        return {
          version: 1,
          groups: nextGrouping.groups.map((group) =>
            group.groupKey === groupKey
              ? {
                  ...group,
                  mobile: {
                    ...group.mobile,
                    [field]: value,
                  },
                }
              : group,
          ),
        }
      })

      setGroupMappingDraft((currentDraft) => ({
        ...currentDraft,
        [field]: value,
      }))
    },
    [activeScene],
  )

  const handlePreviewReset = useCallback(() => {
    setActiveSceneProgress(0)
  }, [])

  const handleResetSceneMotion = useCallback(() => {
    const nextGrouping = cloneGroupingConfig(savedGroupingSnapshot)
    setEditableSceneGrouping(nextGrouping)
    setGroupMappingDraft({ ...(nextGrouping?.groups.find((group) => group.groupKey === selectedGroup)?.mobile ?? DEFAULT_GROUP_MAPPINGS[selectedGroup]) })
    handlePreviewReset()
    setFeedback("Scene motion reset.")
    setErrorMessage(null)
  }, [handlePreviewReset, savedGroupingSnapshot, selectedGroup])

  const handleSaveSceneMotion = useCallback(async () => {
    if (!activeScene) {
      return
    }

    setIsSaving(true)
    setFeedback("Saving scene motion...")
    setErrorMessage(null)

    try {
      await parseJsonResponse<SceneRecord>(
        await fetch(`/api/v1/scenes/${activeScene.id}`, {
          method: "PATCH",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify(buildSceneUpdatePayload()),
        }),
      )

      await loadProject()
      setSavedGroupingSnapshot(cloneGroupingConfig(editableSceneGrouping))
      setFeedback("Scene motion saved.")
      handlePreviewReset()
    } catch (error) {
      setErrorMessage(error instanceof Error ? error.message : "Unable to save scene motion.")
      setFeedback(null)
    } finally {
      setIsSaving(false)
    }
  }, [activeScene, buildSceneUpdatePayload, editableSceneGrouping, handlePreviewReset, loadProject])

  async function saveProjectAndScene() {
    if (!project) {
      return
    }

    setIsSaving(true)
    setFeedback("Saving changes...")
    setErrorMessage(null)

    try {
      await parseJsonResponse<ProjectRecord>(
        await fetch(`/api/v1/projects/${project.id}`, {
          method: "PATCH",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify({
            title: projectTitle,
            globalContext: projectContext.trim() ? projectContext : null,
            stylePreset: projectStylePreset.trim() ? projectStylePreset : null,
          }),
        }),
      )

      if (activeScene) {
        await parseJsonResponse<SceneRecord>(
          await fetch(`/api/v1/scenes/${activeScene.id}`, {
            method: "PATCH",
            headers: {
              "Content-Type": "application/json",
            },
            body: JSON.stringify(buildSceneUpdatePayload()),
          }),
        )
      }

      await loadProject()
      setFeedback("Project saved.")
    } catch (error) {
      setErrorMessage(error instanceof Error ? error.message : "Unable to save this project.")
      setFeedback(null)
    } finally {
      setIsSaving(false)
    }
  }

  async function reorderScene(direction: -1 | 1) {
    if (!project || !activeScene) {
      return
    }

    const currentIndex = project.scenes.findIndex((scene) => scene.id === activeScene.id)
    const nextIndex = currentIndex + direction

    if (nextIndex < 0 || nextIndex >= project.scenes.length) {
      return
    }

    const nextSceneIds = [...project.scenes.map((scene) => scene.id)]
    const [movedSceneId] = nextSceneIds.splice(currentIndex, 1)
    nextSceneIds.splice(nextIndex, 0, movedSceneId)

    setFeedback("Updating scene order...")
    setErrorMessage(null)

    try {
      const updatedProject = await parseJsonResponse<ProjectRecord>(
        await fetch(`/api/v1/projects/${project.id}/scenes/reorder`, {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify({ sceneIds: nextSceneIds }),
        }),
      )

      setProject(updatedProject)
      setActiveSceneIndex(nextIndex)
      setFeedback("Scene order updated.")
    } catch (error) {
      setErrorMessage(error instanceof Error ? error.message : "Unable to reorder scenes.")
      setFeedback(null)
    }
  }

  async function processScene(sceneId: string, mode: "retry" | "regenerate") {
    setFeedback(mode === "retry" ? "Retrying scene..." : "Regenerating scene...")
    setErrorMessage(null)

    try {
      await parseJsonResponse<unknown>(
        await fetch(`/api/v1/scenes/${sceneId}/${mode}`, {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify({ reason: `editor-${mode}` }),
        }),
      )

      await loadProject()
      setFeedback(mode === "retry" ? "Scene queued again." : "Scene regeneration queued.")
    } catch (error) {
      setErrorMessage(error instanceof Error ? error.message : "Unable to reprocess this scene.")
      setFeedback(null)
    }
  }

  async function deleteScene(sceneId: string) {
    setFeedback("Removing scene...")
    setErrorMessage(null)

    try {
      await parseJsonResponse<{ deleted: boolean }>(
        await fetch(`/api/v1/scenes/${sceneId}`, {
          method: "DELETE",
        }),
      )

      await loadProject()
      setActiveSceneIndex((currentIndex) => Math.max(0, currentIndex - 1))
      setFeedback("Scene removed.")
    } catch (error) {
      setErrorMessage(error instanceof Error ? error.message : "Unable to delete this scene.")
      setFeedback(null)
    }
  }

  async function handleGenerateAll() {
    if (!project) {
      return
    }

    const pendingScenes = project.scenes.filter((scene) => scene.status !== "ready")
    const targetScenes = pendingScenes.length > 0 ? pendingScenes : project.scenes

    setFeedback(`Queueing ${targetScenes.length} scene${targetScenes.length === 1 ? "" : "s"}...`)
    setErrorMessage(null)

    try {
      for (const scene of targetScenes) {
        await parseJsonResponse<unknown>(
          await fetch(`/api/v1/scenes/${scene.id}/${scene.status === "ready" ? "regenerate" : "retry"}`, {
            method: "POST",
            headers: {
              "Content-Type": "application/json",
            },
            body: JSON.stringify({ reason: "editor-generate-all" }),
          }),
        )
      }

      await loadProject()
      setFeedback("Scene processing queued.")
    } catch (error) {
      setErrorMessage(error instanceof Error ? error.message : "Unable to queue generation.")
      setFeedback(null)
    }
  }

  async function claimProject() {
    if (!project || actor.kind !== "authenticated") {
      return
    }

    setFeedback("Claiming guest project...")
    setErrorMessage(null)

    try {
      const claimedProject = await parseJsonResponse<ProjectRecord>(
        await fetch(`/api/v1/projects/${project.id}/claim`, {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify({
            guestSessionId: actor.guestSessionId,
          }),
        }),
      )

      setProject(claimedProject)
      setFeedback("Project claimed to your account.")
    } catch (error) {
      setErrorMessage(error instanceof Error ? error.message : "Unable to claim this project.")
      setFeedback(null)
    }
  }

  async function handleFileSelection(event: ChangeEvent<HTMLInputElement>) {
    const files = Array.from(event.target.files ?? [])

    if (!project || files.length === 0) {
      return
    }

    setIsUploading(true)
    setFeedback("Preparing uploads...")
    setErrorMessage(null)

    try {
      let initResponse = await fetch(`/api/v1/projects/${project.id}/uploads/init`, {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          files: files.map((file) => ({
            filename: file.name,
            mimeType: file.type || "application/octet-stream",
            sizeBytes: file.size,
          })),
        }),
      })

      if (initResponse.status === 401) {
        await ensureGuestSession()
        initResponse = await fetch(`/api/v1/projects/${project.id}/uploads/init`, {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify({
            files: files.map((file) => ({
              filename: file.name,
              mimeType: file.type || "application/octet-stream",
              sizeBytes: file.size,
            })),
          }),
        })
      }

      const uploadContracts = await parseJsonResponse<{ uploads: UploadContract[] }>(initResponse)
      setFeedback("Uploading scene originals...")

      await Promise.all(
        uploadContracts.uploads.map((contract, index) =>
          fetch(contract.uploadUrl, {
              method: "PUT",
              headers: {
                "Content-Type": files[index]?.type || contract.mimeType,
              },
              body: files[index],
            }).then((response) => parseJsonResponse<unknown>(response)),
        ),
      )

      const dimensions = await Promise.all(files.map((file) => readImageDimensions(file)))
      setFeedback("Finalizing scene uploads...")

      await parseJsonResponse<SceneRecord[]>(
        await fetch(`/api/v1/projects/${project.id}/uploads/finalize`, {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify({
            uploads: files.map((file, index) => ({
              uploadToken: uploadContracts.uploads[index]?.uploadToken,
              originalFilename: file.name,
              mimeType: file.type || uploadContracts.uploads[index]?.mimeType || "application/octet-stream",
              sizeBytes: file.size,
              width: dimensions[index]?.width,
              height: dimensions[index]?.height,
            })),
          }),
        }),
      )

      await loadProject()
      setFeedback(`${files.length} new scene${files.length === 1 ? "" : "s"} added to the timeline.`)
    } catch (error) {
      setErrorMessage(error instanceof Error ? error.message : "Unable to upload these files.")
      setFeedback(null)
    } finally {
      setIsUploading(false)
      event.target.value = ""
    }
  }

  return (
    <main className="editor-screen">
      <AppHeader active="projects" />

      <section className="editor-action-bar">
        <div className="editor-action-bar__title-wrap">
          <Link className="editor-icon-button" href={"/projects" as Route}>
            <AppIcon className="editor-icon" name="arrow_back" />
          </Link>
          <div className="editor-action-bar__title-block">
            <div className="editor-title-row">
              <input onChange={(event) => setProjectTitle(event.target.value)} type="text" value={projectTitle} />
              <span>{project?.status ?? "loading"}</span>
            </div>
            <p>Project ID: {projectId}</p>
          </div>
        </div>

        <div className="editor-action-bar__actions">
          <button className="editor-top-button" disabled={isLoading || isSaving} onClick={() => void saveProjectAndScene()} type="button">
            <AppIcon className="editor-inline-icon" name="save" />
            {isSaving ? "Saving..." : "Save"}
          </button>
          <Link className="editor-top-button" href={`/projects/${projectId}/preview` as Route}>
            <AppIcon className="editor-inline-icon" name="visibility" />
            Preview
          </Link>
          <button className="editor-top-button" disabled type="button" title={actor.kind === "authenticated" ? "Export is intentionally unavailable in the MVP while preview remains the validation path." : "Sign in to claim this project first. Export is intentionally unavailable in the MVP while preview remains the validation path."}>
            <AppIcon className="editor-inline-icon" name="ios_share" />
            Export Unavailable
          </button>
          <button className="editor-top-button editor-top-button--primary" disabled={isLoading || scenes.length === 0} onClick={() => void handleGenerateAll()} type="button">
            <AppIcon className="editor-inline-icon" name="bolt" />
            {generateLabel}
          </button>
        </div>
      </section>

      {feedback ? <p className="new-project-feedback">{feedback}</p> : null}
      {errorMessage ? <p className="new-project-error">{errorMessage}</p> : null}
      {actor.kind === "guest" ? <p className="new-project-feedback">Guest projects stay editable for this session. Sign in anytime to claim permanent ownership.</p> : null}
      {canClaimProject ? (
        <div className="editor-action-bar__actions" style={{ justifyContent: "center", padding: "0 1.5rem 1rem" }}>
          <button className="editor-top-button editor-top-button--primary" onClick={() => void claimProject()} type="button">
            Claim This Guest Project
          </button>
        </div>
      ) : null}

      <section className="editor-layout">
        <aside className="editor-scenes-panel">
          <div className="editor-upload-box">
            <button className="editor-upload-button" disabled={isUploading || !project} onClick={() => fileInputRef.current?.click()} type="button">
              <AppIcon className="editor-upload-icon" name="upload_file" />
              <span>{isUploading ? "Uploading..." : "Upload Images"}</span>
            </button>
            <input accept="image/*" hidden multiple onChange={handleFileSelection} ref={fileInputRef} type="file" />
          </div>
          <div className="editor-scenes-list">
            <h3>Timeline Scenes</h3>
            {isLoading ? <p>Loading scenes...</p> : null}
            {!isLoading && scenes.length === 0 ? <p>No scenes yet. Upload images to start your story.</p> : null}
            {scenes.map((scene, index) => (
              <article className={index === activeSceneIndex ? "editor-scene-card is-active" : "editor-scene-card"} key={scene.id}>
                {index === activeSceneIndex ? <AppIcon className="editor-scene-card__drag" name="drag_indicator" /> : null}
                <button className="editor-scene-card__button" onClick={() => setActiveSceneIndex(index)} type="button">
                  <div className="editor-scene-card__image-wrap">
                    <div className="editor-scene-card__image" style={resolveProjectSceneImage(scene) ? { backgroundImage: `url("${resolveProjectSceneImage(scene)}")` } : undefined} />
                  </div>
                  <div className="editor-scene-card__meta">
                    <span>Scene {String(index + 1).padStart(2, "0")}</span>
                    <strong>{scene.status}</strong>
                  </div>
                </button>
              </article>
            ))}
          </div>
        </aside>

        <section className="editor-stage-panel">
          <div className="editor-stage-shell">
            <div className="editor-stage-frame" onWheel={handleStageWheel}>
              {activePlaybackScene ? (
                <PlaybackSceneRenderer
                  className="editor-stage-frame__image"
                  isReducedMotion={playback?.isReducedMotion}
                  progress={activeSceneProgress}
                  scene={activePlaybackScene}
                />
              ) : (
                <div className="editor-stage-frame__image" />
              )}
              <div className="editor-stage-frame__progress-readout">
                <span>Scene scroll</span>
                <strong>
                  {activeSceneScrubTimeMs} / {activeSceneDurationMs} ms
                </strong>
              </div>
              <div className="editor-stage-frame__progress-caption">
                <span>{activeSceneProgressPercent}%</span>
                <span>{activePlaybackScene?.cameraMovement ?? "waiting"}</span>
              </div>
              <div className="editor-stage-frame__safe-zone">{activeScene ? `${activeScene.status} scene preview` : "Upload a scene to begin"}</div>
            </div>

            <div
              aria-label="Scene parallax scrub bar"
              aria-valuemax={100}
              aria-valuemin={0}
              aria-valuenow={activeSceneProgressPercent}
              className="editor-stage-scrubber"
              onKeyDown={handleScrubKeyDown}
              onPointerDown={handleScrubPointerDown}
              ref={scrubRailRef}
              role="slider"
              tabIndex={activePlaybackScene ? 0 : -1}
            >
              <div className="editor-stage-scrubber__track" />
              <div className="editor-stage-scrubber__fill" style={{ height: `${activeSceneProgressPercent}%` }} />
              <div className="editor-stage-scrubber__thumb" style={{ top: `calc(${activeSceneProgressPercent}% - 16px)` }} />
              <div className="editor-stage-scrubber__labels">
                <span>0%</span>
                <span>100%</span>
              </div>
            </div>
          </div>
        </section>

        <aside className="editor-inspector-panel">
          <div className="editor-tab-row" aria-label="Editor focus areas">
            <span className="editor-tab-row__item is-active">Scene editor</span>
            <span className="editor-tab-row__item">Project details</span>
          </div>

          <div className="editor-inspector-panel__body">
            {activeScene ? (
              <div key={activeScene.id}>
                <div className="editor-form-group">
                  <label>Scene Name</label>
                  <div className="editor-select-wrap">
                    <select onChange={(event) => setActiveSceneIndex(Number(event.target.value))} value={activeSceneIndex}>
                      {scenes.map((scene, index) => (
                        <option key={scene.id} value={index}>
                          Scene {String(index + 1).padStart(2, "0")} - {scene.status}
                        </option>
                      ))}
                    </select>
                    <AppIcon className="editor-select-icon" name="expand_more" />
                  </div>
                </div>
                <div className="editor-form-group">
                  <label>Scene Context</label>
                  <textarea onChange={(event) => setSceneContext(event.target.value)} rows={4} value={sceneContext} />
                </div>
                <div className="editor-form-group">
                  <label>Motion Preset</label>
                  <div className="editor-select-wrap">
                    <select onChange={(event) => setSceneMotionPreset(event.target.value)} value={sceneMotionPreset}>
                      <option>Standard Pan</option>
                      <option>Cinematic Push</option>
                      <option>Parallax Tilt</option>
                      <option>Vertical Scroll</option>
                      <option>Hold Still</option>
                    </select>
                    <AppIcon className="editor-select-icon" name="expand_more" />
                  </div>
                </div>
                <div className="editor-form-group">
                  <label>Motion Intensity</label>
                  <div className="editor-select-wrap">
                    <select onChange={(event) => setSceneMotionIntensity(event.target.value)} value={sceneMotionIntensity}>
                      <option value="low">Low</option>
                      <option value="medium">Medium</option>
                      <option value="high">High</option>
                    </select>
                    <AppIcon className="editor-select-icon" name="expand_more" />
                  </div>
                </div>
                <div className="editor-grouping-panel">
                  <div className="editor-grouping-panel__header">
                    <div>
                      <h3>Scene Motion Groups</h3>
                      <p>Tablet and Desktop are auto-scaled from Mobile</p>
                    </div>
                    <button className="editor-depth-grid__button" onClick={handlePreviewReset} type="button">
                      Reset Preview
                    </button>
                  </div>

                  <div className="editor-grouping-panel__button-row" aria-label="Device controls">
                    <button className="editor-grouping-toggle is-active" type="button">
                      Mobile
                    </button>
                  </div>

                  <div className="editor-grouping-panel__button-row" aria-label="Group controls">
                    {GROUP_KEYS.map((groupKey) => (
                      <button
                        className={groupKey === selectedGroup ? "editor-grouping-toggle is-active" : "editor-grouping-toggle"}
                        key={groupKey}
                        onClick={() => handleSelectGroup(groupKey)}
                        type="button"
                      >
                        {GROUP_LABELS[groupKey]}
                      </button>
                    ))}
                  </div>

                  <div className="editor-grouping-panel__action-row">
                    <button className="editor-depth-grid__button" onClick={handleAutoAssignLayers} type="button">
                      Auto Assign Layers
                    </button>
                    <button className="editor-depth-grid__button" onClick={() => void handleSaveSceneMotion()} type="button">
                      Save Scene Motion
                    </button>
                    <button className="editor-depth-grid__button" onClick={handleResetSceneMotion} type="button">
                      Reset Scene Motion
                    </button>
                  </div>

                  {activeGroupConfig ? (
                    <div className="editor-grouping-panel__grid">
                      {GROUP_MAPPING_FIELDS.map((fieldConfig) => (
                        <label className="editor-grouping-input" key={fieldConfig.field}>
                          <span>{fieldConfig.label}</span>
                          {fieldConfig.type === "select" ? (
                            <div className="editor-select-wrap">
                              <select
                                onChange={(event) =>
                                  handleGroupMappingChange(selectedGroup, fieldConfig.field, event.target.value as MobileGroupScrollMapping["easing"])
                                }
                                value={groupMappingDraft[fieldConfig.field] as string}
                              >
                                <option value="linear">linear</option>
                                <option value="ease-out">ease-out</option>
                                <option value="ease-in-out">ease-in-out</option>
                              </select>
                              <AppIcon className="editor-select-icon" name="expand_more" />
                            </div>
                          ) : (
                            <input
                              max={fieldConfig.max}
                              min={fieldConfig.min}
                              onChange={(event) => handleGroupMappingChange(selectedGroup, fieldConfig.field, Number(event.target.value))}
                              step={fieldConfig.step}
                              type="number"
                              value={groupMappingDraft[fieldConfig.field] as number}
                            />
                          )}
                        </label>
                      ))}
                    </div>
                  ) : null}

                  <div className="editor-grouping-panel__layers">
                    {activeSceneLayerAssets.length > 0 ? (
                      activeSceneLayerAssets.map((asset) => {
                        const assignedGroup = editableSceneGrouping?.groups.find((group) => group.layerIndexes.includes(asset.resolvedLayerIndex))

                        return (
                          <article className="editor-layer-card" key={`${activeScene.id}-${asset.resolvedLayerIndex}`}>
                            <div className="editor-layer-card__meta">
                              <div>
                                <strong>Layer {asset.resolvedLayerIndex + 1}</strong>
                                <span>{assignedGroup ? GROUP_LABELS[assignedGroup.groupKey] : "Unassigned"}</span>
                              </div>
                              <div className="editor-layer-card__preview" style={{ backgroundImage: `url("${asset.assetUrl}")` }} />
                            </div>

                            <div className="editor-layer-card__actions">
                              <button className="editor-depth-grid__button" onClick={() => handleAssignLayerToGroup(asset.resolvedLayerIndex, "background")} type="button">
                                Assign to Background
                              </button>
                              <button className="editor-depth-grid__button" onClick={() => handleAssignLayerToGroup(asset.resolvedLayerIndex, "midground")} type="button">
                                Assign to Midground
                              </button>
                              <button className="editor-depth-grid__button" onClick={() => handleAssignLayerToGroup(asset.resolvedLayerIndex, "foreground")} type="button">
                                Assign to Foreground
                              </button>
                            </div>
                          </article>
                        )
                      })
                    ) : (
                      <p className="editor-grouping-panel__empty">Process this scene to unlock grouped layer assignments.</p>
                    )}
                  </div>
                </div>
                <div className="editor-depth-grid">
                  <button className="editor-depth-grid__button" disabled={activeSceneIndex === 0} onClick={() => void reorderScene(-1)} type="button">
                    Move Up
                  </button>
                  <button className="editor-depth-grid__button" disabled={activeSceneIndex >= scenes.length - 1} onClick={() => void reorderScene(1)} type="button">
                    Move Down
                  </button>
                  <button className="editor-depth-grid__button" onClick={() => void deleteScene(activeScene.id)} type="button">
                    Delete
                  </button>
                </div>
                <div className="preview-scene-copy__badges" style={{ marginTop: "1rem" }}>
                  <span>{activeScene.status}</span>
                  {activeScene.status === "failed" ? <span>Action required</span> : null}
                </div>
              </div>
            ) : null}

            <div className="editor-global-section">
              <h3>Project Settings</h3>
              <div className="editor-form-group">
                <label>Project Context</label>
                <textarea onChange={(event) => setProjectContext(event.target.value)} rows={2} value={projectContext} />
              </div>
              <div className="editor-form-group">
                <label>Style Preset</label>
                <input onChange={(event) => setProjectStylePreset(event.target.value)} type="text" value={projectStylePreset} />
              </div>
              <div className="editor-output-row">
                <div>
                  <span>Output Format</span>
                  <strong>{project?.outputFormat ?? "9:16 Portrait"}</strong>
                </div>
                <AppIcon className="editor-output-icon" name="public" />
              </div>
            </div>

            <div className="editor-global-section editor-playback-panel">
              <h3>Playback Panel</h3>
              <div className="preview-scene-copy__badges" style={{ marginTop: "1rem" }}>
                <span>{playback?.playbackVersion ? `Version ${playback.playbackVersion}` : "Pending stitch"}</span>
                <span>{playback?.isFallback ? "Fallback active" : "Primary playback"}</span>
                <span>{playback?.isReducedMotion ? "Reduced motion" : "Standard motion"}</span>
              </div>

              {activePlaybackScene ? (
                <div className="editor-playback-panel__meta">
                  <p>{activePlaybackScene.detail}</p>
                  <div className="editor-playback-panel__grid">
                    <div>
                      <span>Start</span>
                      <strong>{activePlaybackScene.startsAtMs ?? 0} ms</strong>
                    </div>
                    <div>
                      <span>Duration</span>
                      <strong>{activePlaybackScene.durationMs ?? 2200} ms</strong>
                    </div>
                    <div>
                      <span>Scrub Point</span>
                      <strong>{activeSceneScrubTimeMs} ms</strong>
                    </div>
                    <div>
                      <span>Scroll Progress</span>
                      <strong>{activeSceneProgressPercent}%</strong>
                    </div>
                    <div>
                      <span>Movement</span>
                      <strong>{activePlaybackScene.cameraMovement}</strong>
                    </div>
                    <div>
                      <span>Intensity</span>
                      <strong>{activePlaybackScene.intensity}</strong>
                    </div>
                  </div>
                </div>
              ) : null}

              <div className="editor-playback-order">
                {(playback?.scenes ?? []).map((scene) => (
                  <div className={scene.id === activePlaybackScene?.id ? "editor-playback-order__item is-active" : "editor-playback-order__item"} key={scene.id}>
                    <div>
                      <span>{scene.title}</span>
                      <strong>{scene.status}</strong>
                    </div>
                    <div>
                      <span>{scene.startsAtMs ?? 0} ms</span>
                      <strong>{scene.fallback ? "Fallback" : "Primary"}</strong>
                    </div>
                  </div>
                ))}
              </div>
            </div>
          </div>

          <div className="editor-inspector-panel__footer">
            <button className="editor-reprocess-button" disabled={!activeScene} onClick={() => activeScene && void processScene(activeScene.id, activeScene.status === "ready" ? "regenerate" : "retry")} type="button">
              <AppIcon className="editor-inline-icon" name="restart_alt" />
              {activeScene?.status === "ready" ? "Reprocess Scene" : "Retry Scene"}
            </button>
          </div>
        </aside>
      </section>
    </main>
  )
}



================================================
FILE: src/features/projects/components/projects-dashboard-page.tsx
================================================
"use client"

import { useEffect, useMemo, useState } from "react"
import type { Route } from "next"
import Link from "next/link"

import { AppHeader } from "@/features/shared/components/app-header"
import { AppIcon } from "@/features/shared/components/app-icon"

import { ProjectCard } from "./project-card"

type ViewMode = "carousel" | "grid"
type SortMode = "recent" | "name" | "scenes"

type ApiEnvelope<T> = {
  data: T
}

type ApiErrorEnvelope = {
  error?: {
    message?: string
  }
}

type ProjectSummary = {
  id: string
  title: string
  status: string
  updatedAt: string
  scenes: Array<{
    status?: string
    sourceImageUrl: string | null
    thumbnailUrl: string | null
    assets?: Array<{
      assetUrl: string
    }>
  }>
}

type DashboardProject = {
  title: string
  scenes: string
  status: string
  updatedAt: string
  updatedAtIso: string
  projectId: string
  image: string | null
}

function mapProjectToDashboardProject(project: {
  id: string
  title: string
  status: string
  updatedAt: string
  scenes: Array<{
    status?: string
    sourceImageUrl?: string | null
    thumbnailUrl?: string | null
    assets?: Array<{
      assetUrl: string
    }>
    image?: string
  }>
}) {
  return {
    title: project.title,
    scenes: String(Array.isArray(project.scenes) ? project.scenes.length : 0),
    status: project.status,
    updatedAt: formatUpdatedAt(project.updatedAt),
    updatedAtIso: project.updatedAt,
    projectId: project.id,
    image: resolveProjectImage({
      ...project,
      scenes: (Array.isArray(project.scenes) ? project.scenes : []).map((scene) => ({
        sourceImageUrl: scene.sourceImageUrl ?? scene.image ?? null,
        thumbnailUrl: scene.thumbnailUrl ?? scene.image ?? null,
        assets: scene.assets,
      })),
    }),
  }
}

const PROJECTS_PER_PAGE = 4

function isRenderableImageUrl(value: string | null | undefined) {
  if (!value) {
    return false
  }

  return value.startsWith("https://") || value.startsWith("http://") || value.startsWith("/") || value.startsWith("data:")
}

function formatUpdatedAt(value: string) {
  const updatedAt = new Date(value)
  const distanceMs = Date.now() - updatedAt.getTime()

  if (Number.isNaN(updatedAt.getTime()) || distanceMs < 0) {
    return "just now"
  }

  const hours = Math.floor(distanceMs / (60 * 60 * 1000))

  if (hours < 1) {
    return "just now"
  }

  if (hours < 24) {
    return `${hours}h ago`
  }

  const days = Math.floor(hours / 24)
  return `${days}d ago`
}

function resolveProjectImage(project: ProjectSummary) {
  const scenes = Array.isArray(project.scenes) ? project.scenes : []
  const firstScene = scenes[0]

  if (!firstScene) {
    return null
  }

  if (isRenderableImageUrl(firstScene.thumbnailUrl)) {
    return firstScene.thumbnailUrl
  }

  if (isRenderableImageUrl(firstScene.sourceImageUrl)) {
    return firstScene.sourceImageUrl
  }

  const assetUrl = firstScene.assets?.find((asset) => isRenderableImageUrl(asset.assetUrl))?.assetUrl
  return assetUrl ?? null
}

function normalizeProjects(payload: ApiEnvelope<ProjectSummary[]> | null | undefined) {
  return Array.isArray(payload?.data) ? payload.data : []
}

async function parseJsonResponse<T>(response: Response) {
  const contentType = response.headers.get("content-type") ?? ""
  const payload = contentType.includes("application/json")
    ? ((await response.json().catch(() => null)) as ApiEnvelope<T> | ApiErrorEnvelope | null)
    : null

  if (!response.ok) {
    throw new Error(payload && "error" in payload ? payload.error?.message ?? "Request failed." : "Request failed.")
  }

  if (!payload || !("data" in payload)) {
    throw new Error("Unexpected response from the server.")
  }

  return payload.data
}

async function ensureGuestSession() {
  const response = await fetch("/api/v1/guest-sessions", {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
    },
  })

  await parseJsonResponse<{ id: string }>(response)
}

export function ProjectsDashboardPage() {
  const [viewMode, setViewMode] = useState<ViewMode>("grid")
  const [searchQuery, setSearchQuery] = useState("")
  const [sortMode, setSortMode] = useState<SortMode>("recent")
  const [carouselPage, setCarouselPage] = useState(0)
  const [projects, setProjects] = useState<DashboardProject[]>([])
  const [isLoading, setIsLoading] = useState(true)
  const [errorMessage, setErrorMessage] = useState<string | null>(null)

  useEffect(() => {
    let cancelled = false

    async function loadProjects() {
      try {
        setIsLoading(true)
        setErrorMessage(null)

        let response = await fetch("/api/v1/projects", { cache: "no-store" })

        if (response.status === 401) {
          await ensureGuestSession()
          response = await fetch("/api/v1/projects", { cache: "no-store" })
        }

        if (cancelled) {
          return
        }

        const payload = await parseJsonResponse<ProjectSummary[]>(response)
        const projects = normalizeProjects({ data: payload })

        setProjects(
          projects.map((project) => mapProjectToDashboardProject(project)),
        )
      } catch {
        if (!cancelled) {
          setProjects([])
          setErrorMessage("We could not load your projects right now.")
        }
      } finally {
        if (!cancelled) {
          setIsLoading(false)
        }
      }
    }

    void loadProjects()

    return () => {
      cancelled = true
    }
  }, [])

  const filteredProjects = useMemo(() => {
    const normalizedQuery = searchQuery.trim().toLowerCase()
    const matchingProjects = normalizedQuery
      ? projects.filter((project) =>
          [project.title, project.status, `${project.scenes} scenes`].some((value) => value.toLowerCase().includes(normalizedQuery)),
        )
      : projects

    return [...matchingProjects].sort((left, right) => {
      if (sortMode === "name") {
        return left.title.localeCompare(right.title)
      }

      if (sortMode === "scenes") {
      return Number(right.scenes) - Number(left.scenes)
      }

      return new Date(right.updatedAtIso).getTime() - new Date(left.updatedAtIso).getTime()
    })
  }, [projects, searchQuery, sortMode])

  const totalPages = Math.max(1, Math.ceil(filteredProjects.length / PROJECTS_PER_PAGE))
  const carouselPages = useMemo(
    () =>
      Array.from({ length: totalPages }, (_, pageIndex) => {
        const start = pageIndex * PROJECTS_PER_PAGE
        return filteredProjects.slice(start, start + PROJECTS_PER_PAGE)
      }),
    [filteredProjects, totalPages],
  )

  const setMode = (mode: ViewMode) => {
    setViewMode(mode)
    if (mode !== "carousel") {
      setCarouselPage(0)
    }
  }

  return (
    <main className="projects-screen">
      <AppHeader active="projects" />

      <section className="projects-shell">
        <div className="projects-header-row">
          <div>
            <p className="projects-kicker">Library</p>
            <h1>Your Projects</h1>
            <p>
              Manage and preview your cinematic story sequences. You have {filteredProjects.length} active
              {filteredProjects.length === 1 ? " project" : " projects"} in your library.
            </p>
          </div>
          <Link className="projects-mobile-create" href={"/projects/new" as Route}>
            <AppIcon className="projects-inline-icon" name="add" />
            Create New Sequence
          </Link>
        </div>

        <div className="projects-controls-row">
          <label className="projects-search-field">
            <AppIcon className="projects-search-field__icon" name="search" />
            <input onChange={(event) => setSearchQuery(event.target.value)} placeholder="Search by title or status..." type="search" value={searchQuery} />
          </label>
          <div className="projects-controls-group">
            <div className="projects-view-toggle" aria-label="Project layout view">
              <button
                aria-label="Carousel view"
                aria-pressed={viewMode === "carousel"}
                data-active={viewMode === "carousel"}
                className={viewMode === "carousel" ? "projects-view-toggle__button is-active" : "projects-view-toggle__button"}
                onClick={() => setMode("carousel")}
                title="Carousel view"
                type="button"
              >
                <AppIcon className="projects-view-toggle__icon" name="view_carousel" />
              </button>
              <button
                aria-label="Grid view"
                aria-pressed={viewMode === "grid"}
                data-active={viewMode === "grid"}
                className={viewMode === "grid" ? "projects-view-toggle__button is-active" : "projects-view-toggle__button"}
                onClick={() => setMode("grid")}
                title="Grid view"
                type="button"
              >
                <AppIcon className="projects-view-toggle__icon" name="view_quilt" />
              </button>
            </div>
            <div className="projects-select-wrap">
              <select onChange={(event) => setSortMode(event.target.value as SortMode)} value={sortMode}>
                <option value="recent">Sort by: Recent</option>
                <option value="name">Sort by: Name</option>
                <option value="scenes">Sort by: Scenes</option>
              </select>
              <AppIcon className="projects-select-wrap__icon" name="expand_more" />
            </div>
          </div>
        </div>

        {isLoading ? (
          <div className="projects-empty-state">
            <div className="projects-empty-state__icon">
              <AppIcon className="projects-empty-state__icon-svg" name="hourglass_top" />
            </div>
            <div>
              <h3>Loading your projects</h3>
              <p>Fetching your latest stories and preview routes.</p>
            </div>
          </div>
        ) : errorMessage ? (
          <div className="projects-empty-state">
            <div className="projects-empty-state__icon">
              <AppIcon className="projects-empty-state__icon-svg" name="info" />
            </div>
            <div>
              <h3>Projects unavailable</h3>
              <p>{errorMessage}</p>
            </div>
          </div>
        ) : filteredProjects.length === 0 ? (
          <div className="projects-empty-state">
            <div className="projects-empty-state__icon">
              <AppIcon className="projects-empty-state__icon-svg" name="create_new_folder" />
            </div>
            <div>
              <h3>{projects.length === 0 ? "Ready to start something new?" : "No projects match your search"}</h3>
              <p>
                {projects.length === 0
                  ? "Create your first project to start uploading scenes and building a stitched mobile preview."
                  : "Try a different title or status query to find the project you want."}
              </p>
            </div>
            <Link className="projects-empty-state__button" href={"/projects/new" as Route}>
              New Project
            </Link>
          </div>
        ) : viewMode === "carousel" ? (
          <section className="projects-carousel" aria-label="Projects carousel">
            <button
              aria-label="Previous projects"
              className="projects-carousel__nav"
              disabled={carouselPage === 0}
              onClick={() => setCarouselPage((page) => Math.max(0, page - 1))}
              type="button"
            >
              <AppIcon className="projects-inline-icon" name="arrow_back" />
            </button>

            <div className="projects-carousel__viewport">
              <div
                className="projects-carousel__track"
                style={{
                  width: `${carouselPages.length * 100}%`,
                  transform: `translateX(-${carouselPage * (100 / carouselPages.length)}%)`,
                }}
              >
                {carouselPages.map((pageProjects, pageIndex) => (
                  <div
                    className="projects-carousel__page"
                    key={`page-${pageIndex}`}
                    style={{ width: `${100 / carouselPages.length}%` }}
                  >
                    <div className="projects-grid projects-grid--carousel">
                      {pageProjects.map((project) => (
                        <ProjectCard key={project.projectId} {...project} viewMode="carousel" />
                      ))}
                    </div>
                  </div>
                ))}
              </div>
            </div>

            <button
              aria-label="Next projects"
              className="projects-carousel__nav projects-carousel__nav--next"
              disabled={carouselPage >= totalPages - 1}
              onClick={() => setCarouselPage((page) => Math.min(totalPages - 1, page + 1))}
              type="button"
            >
              <AppIcon className="projects-inline-icon" name="arrow_back" />
            </button>
          </section>
        ) : (
          <div className="projects-grid">
             {filteredProjects.map((project) => (
               <ProjectCard key={project.projectId} {...project} viewMode={viewMode} />
             ))}
           </div>
        )}
      </section>

      <footer className="projects-footer">
        <div>
          <AppIcon className="projects-footer__icon" name="auto_awesome_motion" />
          <span>© 2024 Parallax Story Composer. All rights reserved.</span>
        </div>
        <div>
          {[
            "Projects",
            "Preview",
            "Guest claim flow",
            "Local MVP setup",
          ].map((item) => (
            <span className="projects-footer__link" key={item}>{item}</span>
          ))}
        </div>
      </footer>
    </main>
  )
}



================================================
FILE: src/features/scenes/components/scene-rail.tsx
================================================
const scenes = [
  { title: "Scene 01", state: "READY" },
  { title: "Scene 02", state: "PROCESSING" },
  { title: "Scene 03", state: "QUEUED" },
] as const

export function SceneRail() {
  return (
    <aside className="psc-editor-rail">
      <p className="psc-kicker">Timeline Scenes</p>
      <div className="psc-scene-stack">
        {scenes.map((scene, index) => (
          <article className={index === 0 ? "psc-scene-card is-active" : "psc-scene-card"} key={scene.title}>
            <div className="psc-scene-card__thumb" />
            <div className="psc-scene-card__meta">
              <strong>{scene.title}</strong>
              <span>{scene.state}</span>
            </div>
          </article>
        ))}
      </div>
    </aside>
  )
}



================================================
FILE: src/features/settings/components/settings-page.tsx
================================================
import { AppHeader } from "@/features/shared/components/app-header"

export function SettingsPage() {
  return (
    <main className="settings-screen">
      <AppHeader active="settings" />

      <section className="settings-shell">
        <div className="settings-header">
          <span className="settings-kicker">Deferred for MVP</span>
          <h1>Settings are not part of the launch flow</h1>
          <p>The core MVP experience lives in projects, uploads, editor updates, preview, and guest-to-account claiming.</p>
        </div>

        <div className="settings-stack">
          <section className="settings-panel settings-panel--account">
            <div className="settings-panel__heading">
              <div>
                <h2>Coming after MVP</h2>
                <p>Account preferences, saved defaults, and session management are intentionally deferred until the core editor and preview flow is stable.</p>
              </div>
            </div>
          </section>

          <section className="settings-panel">
            <div className="settings-panel__heading">
              <div>
                <h2>What to use instead</h2>
                <p>Use Projects for active work, the editor for uploads and scene updates, and preview to verify stitched playback before sharing access internally.</p>
              </div>
            </div>
          </section>
        </div>
      </section>
    </main>
  )
}



================================================
FILE: src/features/shared/components/app-header.tsx
================================================
import type { Route } from "next"
import Link from "next/link"

import { AppIcon } from "@/features/shared/components/app-icon"

type AppHeaderProps = {
  active?: "home" | "projects" | "new" | "settings"
  variant?: "marketing" | "app" | "auth"
}

function navClass(isActive: boolean) {
  return isActive ? "psc-top-nav__link is-active" : "psc-top-nav__link"
}

export function AppHeader({ active, variant = "app" }: AppHeaderProps) {
  return (
    <header className="psc-top-nav">
      <div className="psc-top-nav__inner">
        <Link className="psc-top-nav__brand" href={"/" as Route}>
          <span aria-hidden className="psc-top-nav__brand-icon">
            <span className="psc-top-nav__brand-spark" />
          </span>
          <span className="psc-top-nav__brand-text">Parallax</span>
        </Link>

        <nav aria-label="Primary navigation" className="psc-top-nav__links">
          <Link className={navClass(active === "home")} href={"/" as Route}>
            Home
          </Link>
          <Link className={navClass(active === "projects")} href={"/projects" as Route}>
            Projects
          </Link>
          <Link className={navClass(active === "new")} href={"/projects/new" as Route}>
            New Project
          </Link>
          <Link className={navClass(active === "settings")} href={"/settings" as Route}>
            Settings
          </Link>
        </nav>

        <div className="psc-top-nav__actions">
          {variant === "marketing" || variant === "auth" ? (
            <Link className="psc-top-nav__cta" href={"/login" as Route}>
              Sign In
            </Link>
          ) : (
            <>
              <button aria-label="Notifications" className="psc-top-nav__icon-button" type="button">
                <AppIcon className="psc-top-nav__icon" name="notifications" />
              </button>
              <button aria-label="Open account menu" className="psc-top-nav__avatar" type="button">
                <span className="psc-top-nav__avatar-face" />
              </button>
            </>
          )}
        </div>
      </div>
    </header>
  )
}



================================================
FILE: src/features/shared/components/app-icon.tsx
================================================
export type AppIconName =
  | "add"
  | "arrow_back"
  | "auto_awesome_motion"
  | "auto_fix_high"
  | "bolt"
  | "check_circle"
  | "cloud_upload"
  | "create_new_folder"
  | "delete"
  | "download"
  | "drag_indicator"
  | "draw"
  | "edit"
  | "expand_more"
  | "fast_forward"
  | "fast_rewind"
  | "file_export"
  | "filter_list"
  | "group"
  | "hourglass_top"
  | "info"
  | "ios_share"
  | "layers"
  | "lock"
  | "logout"
  | "movie"
  | "movie_edit"
  | "notifications"
  | "person"
  | "play_arrow"
  | "play_circle"
  | "public"
  | "restart_alt"
  | "save"
  | "schedule"
  | "search"
  | "stack"
  | "storm"
  | "swipe_down_alt"
  | "tune"
  | "upload_file"
  | "video_library"
  | "view_carousel"
  | "view_quilt"
  | "visibility"

type AppIconProps = {
  name: AppIconName
  className?: string
  title?: string
}

const iconPaths: Record<AppIconName, string> = {
  add: "M440-440H200v-80h240v-240h80v240h240v80H520v240h-80v-240Z",
  arrow_back: "M313-440 537-216l-57 56-320-320 320-320 57 56-224 224h487v80H313Z",
  auto_awesome_motion:
    "M120-160v-640h640v160h80v320h-80v160H120Zm80-80h480v-480H200v480Zm120-120h240v-240H320v240Zm400 40v-400h40v400h-40Zm-560 80v-480 480Z",
  auto_fix_high:
    "m438-352 226-226-56-56-170 170-86-86-56 56 142 142Zm42 232L347-253l57-57 76 76v-206h80v206l76-76 57 57-133 133Zm0-440L347-693l57-57 76 76v-206h80v206l76-76 57 57-133 133Z",
  bolt: "m422-232 207-248H492l46-248-207 248h137l-46 248Z",
  check_circle:
    "m424-296 282-282-56-56-226 226-114-114-56 56 170 170Zm56 216q-75 0-140.5-28.5t-114-77Q177-234 148.5-299.5T120-440q0-75 28.5-140.5t77-114Q274-743 339.5-771.5T480-800q75 0 140.5 28.5t114 77Q783-646 811.5-580.5T840-440q0 75-28.5 140.5t-77 114Q686-137 620.5-108.5T480-80Z",
  cloud_upload:
    "M450-160v-244l-64 64-56-58 160-160 160 160-56 58-64-64v244h-80ZM240-240q-66 0-113-47t-47-113q0-57 36.5-102T210-558q14-82 76-132t146-50q78 0 138.5 48T648-564q72 8 122 61t50 127q0 75-52.5 127.5T640-196H520v-80h120q42 0 71-29t29-71q0-42-29-71t-71-29h-60v-40q0-58-41-99t-99-41q-58 0-99 41t-41 99h-40q-42 0-71 29t-29 71q0 42 29 71t71 29h130v80H240Z",
  create_new_folder:
    "M160-160q-33 0-56.5-23.5T80-240v-480q0-33 23.5-56.5T160-800h240l80 80h320q33 0 56.5 23.5T880-640v120h-80v-120H447l-80-80H160v480h280v80H160Zm520-160v-120H560v-80h120v-120h80v120h120v80H760v120h-80Z",
  delete:
    "M280-160q-33 0-56.5-23.5T200-240v-400h80v400h400v-400h80v400q0 33-23.5 56.5T680-160H280Zm120-560v-80h160v80h200v80H200v-80h200Z",
  download:
    "M480-320 280-520l56-58 104 104v-326h80v326l104-104 56 58-200 200ZM200-160q-33 0-56.5-23.5T120-240v-120h80v120h560v-120h80v120q0 33-23.5 56.5T760-160H200Z",
  drag_indicator:
    "M280-280q-17 0-28.5-11.5T240-320q0-17 11.5-28.5T280-360q17 0 28.5 11.5T320-320q0 17-11.5 28.5T280-280Zm0-160q-17 0-28.5-11.5T240-480q0-17 11.5-28.5T280-520q17 0 28.5 11.5T320-480q0 17-11.5 28.5T280-440Zm0-160q-17 0-28.5-11.5T240-640q0-17 11.5-28.5T280-680q17 0 28.5 11.5T320-640q0 17-11.5 28.5T280-600Zm400 320q-17 0-28.5-11.5T640-320q0-17 11.5-28.5T680-360q17 0 28.5 11.5T720-320q0 17-11.5 28.5T680-280Zm0-160q-17 0-28.5-11.5T640-480q0-17 11.5-28.5T680-520q17 0 28.5 11.5T720-480q0 17-11.5 28.5T680-440Zm0-160q-17 0-28.5-11.5T640-640q0-17 11.5-28.5T680-680q17 0 28.5 11.5T720-640q0 17-11.5 28.5T680-600Z",
  draw:
    "M160-120v-170l458-458q11-11 25.5-16.5T674-770q16 0 30.5 5.5T730-748l78 78q11 11 16.5 25.5T830-614q0 15-5.5 30T808-558L350-100H160Zm80-80h76l322-322-38-38-38-38-322 322v76Zm474-398-38-38 38 38Zm-114 76-20-20 76 76-56-56Z",
  edit: "M200-200h57l386-386-57-57-386 386v57Zm-80 80v-171l500-500q11-11 24-15.5t27-4.5q14 0 27.5 5T722-790l68 68q10 10 15 23t5 27q0 14-4.5 27T790-621L290-120H120Zm560-503-57-57 57 57Z",
  expand_more: "M480-360 280-560h400L480-360Z",
  fast_forward: "M320-240v-480l240 240-240 240Zm240 0v-480l240 240-240 240Z",
  fast_rewind: "M640-240 400-480l240-240v480Zm-240 0L160-480l240-240v480Z",
  file_export:
    "M160-120q-33 0-56.5-23.5T80-200v-560h80v560h640v80H160Zm160-160q-33 0-56.5-23.5T240-360v-400q0-33 23.5-56.5T320-840h247q16 0 30.5 6t25.5 17l121 121q11 11 17 25.5t6 30.5v280q0 33-23.5 56.5T688-280H320Zm0-80h368v-240H520v-160H320v400Zm120-120h128v-80h-48v-80h-80v80h-48v80h48v80h80v-80Z",
  filter_list: "M120-240v-80h160v80H120Zm0-200v-80h400v80H120Zm0-200v-80h640v80H120Z",
  group:
    "M40-160v-112q0-34 17-63t47-45q51-28 111-42.5T340-437q36 0 71 4.5t69 13.5q-14 20-22 43t-8 48v168H40Zm490 0v-168q0-23 10-44t28-34q41-29 90.5-43.5T760-464q55 0 104.5 14.5T955-406q18 13 28 34t10 44v168H530ZM340-480q-66 0-113-47t-47-113q0-66 47-113t113-47q66 0 113 47t47 113q0 66-47 113t-113 47Zm420-80q-50 0-85-35t-35-85q0-50 35-85t85-35q50 0 85 35t35 85q0 50-35 85t-85 35ZM340-560q33 0 56.5-23.5T420-640q0-33-23.5-56.5T340-720q-33 0-56.5 23.5T260-640q0 33 23.5 56.5T340-560Z",
  hourglass_top:
    "M240-80v-80q0-66 47-113t113-47h160q66 0 113 47t47 113v80H240Zm160-320q-66 0-113-47t-47-113v-240h480v240q0 66-47 113t-113 47H400Zm0-80h160q33 0 56.5-23.5T640-560v-80H320v80q0 33 23.5 56.5T400-480Zm-80-240h320v-80H320v80Z",
  info:
    "M440-280h80v-240h-80v240Zm40-320q17 0 28.5-11.5T520-640q0-17-11.5-28.5T480-680q-17 0-28.5 11.5T440-640q0 17 11.5 28.5T480-600Zm0 520q-83 0-156-31.5T197-197q-54-54-85.5-127T80-480q0-83 31.5-156T197-763q54-54 127-85.5T480-880q83 0 156 31.5T763-763q54 54 85.5 127T880-480q0 83-31.5 156T763-197q-54 54-127 85.5T480-80Z",
  ios_share:
    "M720-80q-50 0-85-35t-35-85q0-10 1.5-20t4.5-20L400-360q-14 14-33 22t-40 8q-50 0-85-35t-35-85q0-50 35-85t85-35q21 0 40 8t33 22l206-120q-3-10-4.5-20t-1.5-20q0-50 35-85t85-35q50 0 85 35t35 85q0 50-35 85t-85 35q-21 0-40-8t-33-22L441-440q3 10 4.5 20t1.5 20q0 10-1.5 20t-4.5 20l206 120q14-14 33-22t40-8q50 0 85 35t35 85q0 50-35 85t-85 35Z",
  layers: "M480-118 160-360l58-44 262 198 262-198 58 44-320 242Zm0-160L160-520l320-242 320 242-320 242Zm0-100 188-142-188-142-188 142 188 142Z",
  lock:
    "M240-400h480v-240q0-100-70-170t-170-70q-100 0-170 70t-70 170v240Zm240 160q33 0 56.5-23.5T560-320q0-33-23.5-56.5T480-400q-33 0-56.5 23.5T400-320q0 33 23.5 56.5T480-240ZM160-80v-560h80v-80q0-133 93.5-226.5T560-1040q133 0 226.5 93.5T880-720v80h80V-80H160Zm80-80h640v-400H240v400Zm240-160Z",
  logout:
    "M200-120q-33 0-56.5-23.5T120-200v-160h80v160h560v-560H200v160h-80v-160q0-33 23.5-56.5T200-840h560q33 0 56.5 23.5T840-760v560q0 33-23.5 56.5T760-120H200Zm220-160-56-58 102-102H120v-80h346L364-622l56-58 200 200-200 200Z",
  movie:
    "M160-200v-560h640v560H160Zm80-80h480v-400H240v400Zm60-20h80v-80h-80v80Zm140 0h80v-80h-80v80Zm140 0h80v-80h-80v80Zm-280-140h80v-80h-80v80Zm280 0h80v-80h-80v80ZM300-580h80v-80h-80v80Zm140 0h80v-80h-80v80Zm140 0h80v-80h-80v80Z",
  movie_edit:
    "M200-200v-560h560v293l-80 80v-293H280v400h293l-80 80H200Zm520-520v-80H200v80h520Zm-40 640v-171l168-168q12-12 26.5-17.5T904-444q15 0 29.5 5.5T960-421l61 61q12 12 17.5 26.5T1044-304q0 15-5.5 29.5T1021-248L853-80H680Zm261-264-61-61 61 61Z",
  notifications:
    "M160-200v-80h80v-280q0-83 50-147.5T420-876v-44q0-25 17.5-42.5T480-980q25 0 42.5 17.5T540-920v44q80 24 130 88.5T720-640v280h80v80H160Zm320-300Zm0 420q-33 0-56.5-23.5T400-160h160q0 33-23.5 56.5T480-80ZM320-280h320v-360q0-66-47-113t-113-47q-66 0-113 47t-47 113v360Z",
  person:
    "M234-276q51-39 114-61.5T480-360q69 0 132 22.5T726-276q-43-53-104.5-82.5T480-388q-80 0-141.5 29.5T234-276Zm246-204q-58 0-99-41t-41-99q0-58 41-99t99-41q58 0 99 41t41 99q0 58-41 99t-99 41Zm0-80q24 0 42-18t18-42q0-24-18-42t-42-18q-24 0-42 18t-18 42q0 24 18 42t42 18Zm0 440q-83 0-156-31.5T197-237q-54-54-85.5-127T80-520q0-83 31.5-156T197-803q54-54 127-85.5T480-920q83 0 156 31.5T763-803q54 54 85.5 127T880-520q0 83-31.5 156T763-237q-54 54-127 85.5T480-120Zm0-80q134 0 227-93t93-227q0-134-93-227t-227-93q-134 0-227 93t-93 227q0 134 93 227t227 93Zm0-320Z",
  play_arrow: "m380-300 280-180v360L380-300Z",
  play_circle:
    "M400-280 640-440 400-600v320Zm80 200q-75 0-140.5-28.5t-114-77Q177-234 148.5-299.5T120-440q0-75 28.5-140.5t77-114Q274-743 339.5-771.5T480-800q75 0 140.5 28.5t114 77Q783-646 811.5-580.5T840-440q0 75-28.5 140.5t-77 114Q686-137 620.5-108.5T480-80Z",
  public:
    "M480-80q-83 0-156-31.5T197-197q-54-54-85.5-127T80-480q0-83 31.5-156T197-763q54-54 127-85.5T480-880q83 0 156 31.5T763-763q54 54 85.5 127T880-480q0 83-31.5 156T763-197q-54 54-127 85.5T480-80Zm0-80q17-36 28.5-74.5T526-320H434q6 44 17.5 82.5T480-160Zm-66-8q-11-29-19-59.5T382-320H260q25 42 64.5 76T414-168Zm132 0q50-22 89.5-76T700-320H578q-5 32-13 62.5T546-168Zm-174-232q-2-20-3-40t-1-40q0-20 1-40t3-40H244q-4 20-4 40t4 40q0 20 4 40h124Zm84 0h128q2-20 3-40t1-40q0-20-1-40t-3-40H456q-2 20-3 40t-1 40q0 20 1 40t3 40Zm212 0h124q4-20 4-40t-4-40q0-20-4-40H668q2 20 3 40t1 40q0 20-1 40t-3 40ZM260-640h122q5-32 13-62.5t19-59.5q-50 22-89.5 56T260-640Zm174 0h92q-6-44-17.5-82.5T480-800q-17 36-28.5 77.5T434-640Zm144 0h122q-25-42-64.5-66T546-762q11 29 19 59.5t13 62.5Z",
  restart_alt:
    "M480-160q-133 0-226.5-93.5T160-480q0-133 93.5-226.5T480-800h24l-64 64 56 56 160-160-160-160-56 56 64 64h-24q-166 0-283 117T80-480q0 166 117 283t283 117q101 0 186-53t128-147h-88q-37 56-95 88t-131 32Z",
  save:
    "M200-120q-33 0-56.5-23.5T120-200v-560q0-33 23.5-56.5T200-840h447q16 0 30.5 6t25.5 17l114 114q11 11 17 25.5t6 30.5v447q0 33-23.5 56.5T760-120H200Zm0-80h560v-406L646-720H200v520Zm280-80q50 0 85-35t35-85q0-50-35-85t-85-35q-50 0-85 35t-35 85q0 50 35 85t85 35ZM280-560h280v-160H280v160Zm-80-160v520-520Z",
  schedule:
    "M480-80q-83 0-156-31.5T197-197q-54-54-85.5-127T80-480q0-83 31.5-156T197-763q54-54 127-85.5T480-880q83 0 156 31.5T763-763q54 54 85.5 127T880-480q0 83-31.5 156T763-197q-54 54-127 85.5T480-80Zm40-440v-200h-80v240l170 102 40-66-130-76Z",
  search: "M784-120 532-372q-30 26-69 39t-83 13q-109 0-184.5-75.5T120-580q0-109 75.5-184.5T380-840q109 0 184.5 75.5T640-580q0 44-13 83t-39 69l252 252-56 56ZM380-400q75 0 127.5-52.5T560-580q0-75-52.5-127.5T380-760q-75 0-127.5 52.5T200-580q0 75 52.5 127.5T380-400Z",
  stack: "M120-280v-80h720v80H120Zm80-160v-80h560v80H200Zm80-160v-80h400v80H280Z",
  storm: "M280-80 440-360H280l280-520-80 320h160L280-80Zm200-80 160-280H480l280-520-80 320h160L480-160Z",
  swipe_down_alt:
    "M440-160v-446L336-502l-56-58 200-200 200 200-56 58-104-104v446h-80Zm-280 40v-80h640v80H160Z",
  tune: "M400-160h160v-80H400v80Zm-240-280h640v-80H160v80Zm120-200h400v-80H280v80Z",
  upload_file:
    "M200-120q-33 0-56.5-23.5T120-200v-560q0-33 23.5-56.5T200-840h360l200 200v440q0 33-23.5 56.5T680-120H200Zm320-480h160L520-760v160Zm-40 320v-160H360v-80h120v-120h80v120h120v80H560v160h-80Z",
  video_library:
    "M240-240h480v-320H240v320Zm140-40 180-120-180-120v240ZM160-160q-33 0-56.5-23.5T80-240v-320h80v320h640v80H160Zm80-480v-80h480v80H240Zm80-120v-80h400v80H320Z",
  view_carousel:
    "M120-200v-560h720v560H120Zm80-80h80v-400h-80v400Zm160 0h240v-400H360v400Zm320 0h80v-400h-80v400Z",
  view_quilt:
    "M120-120v-720h720v720H120Zm80-80h160v-240H200v240Zm240 0h320v-240H440v240Zm-240-320h160v-240H200v240Zm240 0h320v-80H440v80Zm0-160h320v-80H440v80Z",
  visibility:
    "M480-320q50 0 85-35t35-85q0-50-35-85t-85-35q-50 0-85 35t-35 85q0 50 35 85t85 35Zm0 80q-83 0-150.5-44T216-400q-17-26-17-60t17-60q46-72 113.5-116T480-680q83 0 150.5 44T744-520q17 26 17 60t-17 60q-46 72-113.5 116T480-240Zm0-80q33 0 56.5-23.5T560-400q0-33-23.5-56.5T480-480q-33 0-56.5 23.5T400-400q0 33 23.5 56.5T480-320Z",
}

export function AppIcon({ name, className, title }: AppIconProps) {
  return (
    <svg
      aria-hidden={title ? undefined : true}
      className={className}
      fill="currentColor"
      focusable="false"
      viewBox="0 -960 960 960"
      xmlns="http://www.w3.org/2000/svg"
    >
      {title ? <title>{title}</title> : null}
      <path d={iconPaths[name]} />
    </svg>
  )
}



================================================
FILE: src/features/uploads/components/upload-panel.tsx
================================================
export function UploadPanel() {
  return (
    <section className="psc-panel psc-panel--dashed">
      <p className="psc-kicker">Uploads</p>
      <h2>Upload Images</h2>
      <p className="psc-copy">
        This visual shell is ready for the upload-init and upload-finalize flow. Actual file persistence
        remains limited by the current backend storage implementation.
      </p>
      <button className="psc-button psc-button--secondary is-disabled" disabled type="button">
        Select Files
        <span className="psc-status-pill">Phase 2</span>
      </button>
    </section>
  )
}



================================================
FILE: src/infrastructure/db/prisma.ts
================================================
import { PrismaClient } from "@prisma/client"

declare global {
  var prisma: PrismaClient | undefined
}

export const prisma =
  globalThis.prisma ??
  new PrismaClient({
    log: ["warn", "error"],
  })

if (process.env.NODE_ENV !== "production") {
  globalThis.prisma = prisma
}



================================================
FILE: src/infrastructure/jobs/trigger-dev.ts
================================================
import { metrics } from "@/core/observability/metrics"
import { logProcessingEvent } from "@/core/observability/processing-log"
import { ProviderError } from "@/modules/decomposition/types"
import { decompositionService } from "@/modules/decomposition/service"
import { sceneService } from "@/modules/scenes"

type TriggerJobPayload = {
  scene: {
    id: string
    generationVersion: number
    sourceImageUrl: string | null
    expiresAt: Date | null
    project: { id: string }
    assets: Array<{ assetType: string; metadataJson: unknown }>
  }
  job: {
    id: string
    attemptCount: number
    correlationId?: string | null
  }
}

export const triggerDevJobRunner = {
  async dispatchDecomposition(payload: TriggerJobPayload) {
    queueMicrotask(async () => {
      try {
        metrics.gauge("processing_queue_depth", 1)
        await decompositionService.processScene(payload.scene, payload.job)
        metrics.gauge("processing_queue_depth", 0)
      } catch (error) {
        metrics.increment("processing_failures_total")
        if (error instanceof ProviderError && error.kind === "retryable" && payload.job.attemptCount < 2) {
          metrics.increment("processing_retries_total")
          await sceneService.markFailed(payload.job.id, payload.scene.id, `${error.code}: ${error.message}`, payload.job.attemptCount + 1)
          const retryJob = await sceneService.enqueueDecomposition(payload.scene.id, {
            correlationId: payload.job.correlationId ?? crypto.randomUUID(),
            reason: "automatic-retry",
          })
          logProcessingEvent({
            event: "scene decomposition retry scheduled",
            traceId: payload.job.correlationId,
            projectId: payload.scene.project.id,
            sceneId: payload.scene.id,
            jobId: retryJob.id,
          })
          await this.dispatchDecomposition({
            scene: { ...payload.scene },
            job: {
              id: retryJob.id,
              attemptCount: retryJob.attemptCount,
              correlationId: retryJob.correlationId,
            },
          })
          return
        }

        const message = error instanceof Error ? error.message : "Scene decomposition failed."
        await sceneService.markFailed(payload.job.id, payload.scene.id, message, payload.job.attemptCount + 1)
        metrics.gauge("processing_queue_depth", 0)
      }
    })
  },
}



================================================
FILE: src/infrastructure/providers/qwen/client.ts
================================================
import { getEnv } from "@/config/env"
import { ProviderError } from "@/modules/decomposition/types"

type SubmitPayload = {
  imageUrl: string
  mimeType: string
  targetLayers: number
  correlationId: string
}

export const qwenClient = {
  async submit(payload: SubmitPayload) {
    const env = getEnv()

    if (env.QWEN_MOCK_MODE || !env.QWEN_API_URL || !env.QWEN_API_KEY) {
      return {
        id: `mock-${crypto.randomUUID()}`,
        modelVersion: env.QWEN_MODEL,
        width: 1080,
        height: 1920,
        layers: Array.from({ length: payload.targetLayers }, (_, index) => ({
          index,
          width: 1080,
          height: 1920,
          depth: index,
        })),
      }
    }

    let attempt = 0
    const controller = new AbortController()
    const timeout = setTimeout(() => controller.abort(), env.QWEN_TIMEOUT_MS)

    try {
      while (attempt <= env.QWEN_MAX_RETRIES) {
        try {
          const response = await fetch(`${env.QWEN_API_URL}/decompositions`, {
            method: "POST",
            headers: {
              "content-type": "application/json",
              authorization: `Bearer ${env.QWEN_API_KEY}`,
              "x-correlation-id": payload.correlationId,
            },
            body: JSON.stringify({
              imageUrl: payload.imageUrl,
              mimeType: payload.mimeType,
              targetLayers: payload.targetLayers,
              model: env.QWEN_MODEL,
            }),
            signal: controller.signal,
          })

          if (response.status >= 500 || response.status === 429) {
            throw new ProviderError("retryable", "QWEN_UNAVAILABLE", "Qwen provider is temporarily unavailable.")
          }

          if (!response.ok) {
            const text = await response.text()
            throw new ProviderError("terminal", "QWEN_REQUEST_REJECTED", text || "Qwen rejected the request.")
          }

          return response.json()
        } catch (error) {
          const isLastAttempt = attempt >= env.QWEN_MAX_RETRIES

          if (error instanceof ProviderError) {
            if (error.kind === "terminal" || isLastAttempt) {
              throw error
            }
          } else if (isLastAttempt) {
            throw new ProviderError("retryable", "QWEN_NETWORK_ERROR", "Qwen request failed due to a network error.")
          }

          attempt += 1
          await new Promise((resolve) => setTimeout(resolve, 250 * (attempt + 1)))
        }
      }

      throw new ProviderError("retryable", "QWEN_UNKNOWN_FAILURE", "Qwen request failed after retries.")
    } finally {
      clearTimeout(timeout)
    }
  },
}



================================================
FILE: src/infrastructure/rate-limit/memory-rate-limiter.ts
================================================
import { AppError } from "@/core/errors/app-error"
import { getEnv } from "@/config/env"

type Bucket = {
  count: number
  resetAt: number
}

const buckets = new Map<string, Bucket>()

export function enforceRateLimit(identifier: string) {
  const env = getEnv()
  const now = Date.now()
  const current = buckets.get(identifier)

  if (!current || current.resetAt <= now) {
    buckets.set(identifier, {
      count: 1,
      resetAt: now + env.RATE_LIMIT_WINDOW_MS,
    })
    return
  }

  current.count += 1
  buckets.set(identifier, current)

  if (current.count > env.RATE_LIMIT_MAX_REQUESTS) {
    throw new AppError({
      code: "RATE_LIMIT_EXCEEDED",
      message: "Too many requests. Please try again later.",
      statusCode: 429,
      details: {
        resetAt: current.resetAt,
      },
    })
  }
}



================================================
FILE: src/interfaces/http/controllers/auth-controller.ts
================================================
import { cookies } from "next/headers"

import { auth } from "@/auth"
import { AppError } from "@/core/errors/app-error"
import { ok, created } from "@/lib/api-response"
import { authService } from "@/modules/auth"
import { registerInputSchema } from "@/modules/auth/validator"
import { guestSessionService } from "@/modules/guest-sessions"
import { getEnv } from "@/config/env"
import type { RequestContext } from "@/core/request/context"

export const authController = {
  async session(context: RequestContext) {
    const env = getEnv()
    const session = await auth()
    const cookieStore = await cookies()
    const guestSessionId = cookieStore.get(env.GUEST_SESSION_COOKIE_NAME)?.value
    const guestSession = await guestSessionService.resolve(guestSessionId).catch(() => null)

    if (session?.user?.id) {
      return ok(
        {
          actor: {
            kind: "authenticated",
            userId: session.user.id,
            email: session.user.email,
            guestSessionId: guestSession?.id ?? null,
          },
        },
        { correlationId: context.correlationId },
      )
    }

    if (guestSession) {
      return ok(
        {
          actor: {
            kind: "guest",
            guestSessionId: guestSession.id,
            expiresAt: guestSession.expiresAt,
          },
        },
        { correlationId: context.correlationId },
      )
    }

    return ok(
      {
        actor: {
          kind: "anonymous",
        },
      },
      { correlationId: context.correlationId },
    )
  },

  async register(request: Request, context: RequestContext) {
    const body = await request.json().catch(() => {
      throw new AppError({
        code: "INVALID_JSON",
        message: "Request body must be valid JSON.",
        statusCode: 400,
      })
    })

    const input = registerInputSchema.parse(body)
    const user = await authService.register(input)

    return created(user, { correlationId: context.correlationId })
  },
}



================================================
FILE: src/interfaces/http/controllers/guest-session-controller.ts
================================================
import { cookies } from "next/headers"

import { getEnv } from "@/config/env"
import { COOKIE_MAX_AGE_SECONDS } from "@/core/security/cookies"
import { created } from "@/lib/api-response"
import { guestSessionService } from "@/modules/guest-sessions"
import type { RequestContext } from "@/core/request/context"

export const guestSessionController = {
  async create(context: RequestContext) {
    const env = getEnv()
    const session = await guestSessionService.issue()
    const cookieStore = await cookies()

    cookieStore.set(env.GUEST_SESSION_COOKIE_NAME, session.id, {
      httpOnly: true,
      sameSite: "lax",
      secure: env.NODE_ENV === "production",
      path: "/",
      maxAge: COOKIE_MAX_AGE_SECONDS,
      expires: session.expiresAt,
    })

    return created(
      {
        id: session.id,
        expiresAt: session.expiresAt,
      },
      { correlationId: context.correlationId },
    )
  },
}



================================================
FILE: src/interfaces/http/controllers/health-controller.ts
================================================
import { prisma } from "@/infrastructure/db/prisma"
import { envIsConfigured } from "@/config/env"
import { metrics } from "@/core/observability/metrics"
import { ok } from "@/lib/api-response"
import { featureFlagService } from "@/modules/feature-flags"
import type { RequestContext } from "@/core/request/context"

export const healthController = {
  async live(context: RequestContext) {
    return ok(
        {
          status: "ok",
          metrics: metrics.snapshot(),
          featureFlags: featureFlagService.flags(),
        },
        { correlationId: context.correlationId },
      )
  },

  async ready(context: RequestContext) {
    if (!envIsConfigured()) {
      return ok(
        {
          status: "degraded",
          checks: {
            env: false,
            database: false,
          },
        },
        { correlationId: context.correlationId },
        { status: 503 },
      )
    }

    try {
      await prisma.$queryRaw`SELECT 1`
      return ok(
        {
          status: "ok",
          checks: {
            env: true,
            database: true,
          },
        },
        { correlationId: context.correlationId },
      )
    } catch {
      return ok(
        {
          status: "degraded",
          checks: {
            env: true,
            database: false,
          },
          metrics: metrics.snapshot(),
          featureFlags: featureFlagService.flags(),
        },
        { correlationId: context.correlationId },
        { status: 503 },
      )
    }
  },
}



================================================
FILE: src/interfaces/http/controllers/maintenance-controller.ts
================================================
import { ok } from "@/lib/api-response"
import { maintenanceService } from "@/modules/maintenance"
import type { RequestContext } from "@/core/request/context"

export const maintenanceController = {
  async cleanup(context: RequestContext) {
    const result = await maintenanceService.cleanupExpiredGuestResources(context.correlationId)
    return ok(result, { correlationId: context.correlationId })
  },

  async recoverTimeouts(context: RequestContext) {
    const result = await maintenanceService.recoverTimedOutJobs(context.correlationId)
    return ok(result, { correlationId: context.correlationId })
  },
}



================================================
FILE: src/interfaces/http/controllers/preview-controller.ts
================================================
import { ok } from "@/lib/api-response"
import { ensureProjectAccess } from "@/interfaces/http/support/authorization"
import { resolveRequestActor } from "@/interfaces/http/support/request-actor"
import { serializePlaybackPlan } from "@/modules/assets"
import { projectService } from "@/modules/projects"
import { playbackService } from "@/modules/playback"
import type { RequestContext } from "@/core/request/context"

export const previewController = {
  async status(projectId: string, context: RequestContext) {
    const actor = await resolveRequestActor()
    const project = await projectService.getById(projectId)
    ensureProjectAccess(actor, "preview", project)
    const status = await playbackService.previewStatus(projectId)
    return ok(status, { correlationId: context.correlationId })
  },

  async playback(projectId: string, reducedMotion: boolean, context: RequestContext) {
    const actor = await resolveRequestActor()
    const project = await projectService.getById(projectId)
    ensureProjectAccess(actor, "preview", project)
    const playback = await playbackService.latest(projectId, { reducedMotion })
    return ok(serializePlaybackPlan(playback), { correlationId: context.correlationId })
  },
}



================================================
FILE: src/interfaces/http/controllers/project-controller.ts
================================================
import { created, ok } from "@/lib/api-response"
import { parseJsonBody } from "@/interfaces/http/support/json-body"
import { resolveRequestActor } from "@/interfaces/http/support/request-actor"
import { ensureProjectAccess } from "@/interfaces/http/support/authorization"
import { AppError } from "@/core/errors/app-error"
import { serializeProject, serializeProjects } from "@/modules/assets"
import { projectService } from "@/modules/projects"
import {
  claimProjectInputSchema,
  createProjectInputSchema,
  reorderScenesInputSchema,
  updateProjectInputSchema,
} from "@/modules/projects"
import { sceneService } from "@/modules/scenes"
import { playbackService } from "@/modules/playback"
import type { RequestContext } from "@/core/request/context"

export const projectController = {
  async list(context: RequestContext) {
    const actor = await resolveRequestActor()

    if (actor.kind === "anonymous") {
      throw new AppError({
        code: "AUTH_REQUIRED",
        message: "A guest or authenticated session is required.",
        statusCode: 401,
      })
    }

    const projects = await projectService.list(
      actor.kind === "authenticated"
        ? { kind: "authenticated", userId: actor.userId }
        : { kind: "guest", guestSessionId: actor.guestSessionId },
    )

    return ok(serializeProjects(projects), { correlationId: context.correlationId })
  },

  async create(request: Request, context: RequestContext) {
    const input = await parseJsonBody(request, createProjectInputSchema)
    const actor = await resolveRequestActor()

    if (actor.kind === "anonymous") {
      throw new AppError({
        code: "AUTH_REQUIRED",
        message: "A guest or authenticated session is required to create a project.",
        statusCode: 401,
      })
    }

    const project = await projectService.create({
      title: input.title,
      globalContext: input.globalContext ?? null,
      stylePreset: input.stylePreset ?? null,
      actor:
        actor.kind === "authenticated"
          ? {
              kind: "authenticated",
              userId: actor.userId,
            }
          : {
              kind: "guest",
              guestSessionId: actor.guestSessionId,
              expiresAt: actor.expiresAt ?? new Date(Date.now() + 72 * 60 * 60 * 1000),
            },
    })

    return created(serializeProject(project), { correlationId: context.correlationId })
  },

  async getById(projectId: string, context: RequestContext) {
    const actor = await resolveRequestActor()
    const project = await projectService.getById(projectId)
    ensureProjectAccess(actor, "preview", project)
    return ok(serializeProject(project), { correlationId: context.correlationId })
  },

  async update(projectId: string, request: Request, context: RequestContext) {
    const actor = await resolveRequestActor()
    const project = await projectService.getById(projectId)
    ensureProjectAccess(actor, "edit", project)
    const input = await parseJsonBody(request, updateProjectInputSchema)
    const updatedProject = await projectService.update(projectId, input)
    await playbackService.stitchProject(projectId, {
      allowFallback: true,
      traceId: context.correlationId,
    }).catch(() => null)
    return ok(serializeProject(updatedProject), { correlationId: context.correlationId })
  },

  async remove(projectId: string, context: RequestContext) {
    const actor = await resolveRequestActor()
    const project = await projectService.getById(projectId)
    ensureProjectAccess(actor, "edit", project)
    await projectService.remove(projectId)
    return ok({ deleted: true }, { correlationId: context.correlationId })
  },

  async claim(projectId: string, request: Request, context: RequestContext) {
    const actor = await resolveRequestActor()

    if (actor.kind !== "authenticated") {
      throw new AppError({
        code: "AUTH_REQUIRED",
        message: "Authenticated ownership is required to claim a guest project.",
        statusCode: 401,
      })
    }

    const input = await parseJsonBody(request, claimProjectInputSchema)
    const guestSessionId = input.guestSessionId ?? actor.guestSessionId

    if (!guestSessionId) {
      throw new AppError({
        code: "GUEST_SESSION_REQUIRED",
        message: "A matching guest session is required to claim this project.",
        statusCode: 400,
      })
    }

    const claimedProject = await projectService.claim(projectId, {
      userId: actor.userId,
      guestSessionId,
    })

    return ok(serializeProject(claimedProject), { correlationId: context.correlationId })
  },

  async reorderScenes(projectId: string, request: Request, context: RequestContext) {
    const actor = await resolveRequestActor()
    const project = await projectService.getById(projectId)
    ensureProjectAccess(actor, "edit", project)
    const input = await parseJsonBody(request, reorderScenesInputSchema)

    const currentSceneIds = project.scenes.map((scene) => scene.id).sort()
    const nextSceneIds = [...input.sceneIds].sort()

    if (currentSceneIds.length !== nextSceneIds.length || currentSceneIds.join(",") !== nextSceneIds.join(",")) {
      throw new AppError({
        code: "INVALID_SCENE_REORDER",
        message: "Reorder requests must include every scene in the project exactly once.",
        statusCode: 400,
      })
    }

    await sceneService.reorder(projectId, input.sceneIds)
    await playbackService.stitchProject(projectId, {
      allowFallback: true,
      traceId: context.correlationId,
    })
    const updatedProject = await projectService.getById(projectId)
    return ok(serializeProject(updatedProject), { correlationId: context.correlationId })
  },
}



================================================
FILE: src/interfaces/http/controllers/scene-controller.ts
================================================
import { created, ok } from "@/lib/api-response"
import { parseJsonBody } from "@/interfaces/http/support/json-body"
import { resolveRequestActor } from "@/interfaces/http/support/request-actor"
import { ensureProjectAccess } from "@/interfaces/http/support/authorization"
import { finalizeUploadsInputSchema, sceneReprocessInputSchema, updateSceneInputSchema } from "@/modules/scenes"
import { projectService } from "@/modules/projects"
import { sceneService } from "@/modules/scenes"
import { uploadService } from "@/modules/uploads"
import { assetStorageService, buildThumbnailAssetPath, serializeScene } from "@/modules/assets"
import { processingService } from "@/modules/processing"
import { motionService } from "@/modules/motion"
import { playbackService } from "@/modules/playback"
import { AppError } from "@/core/errors/app-error"
import type { RequestContext } from "@/core/request/context"

export const sceneController = {
  async finalizeUploads(projectId: string, request: Request, context: RequestContext) {
    const actor = await resolveRequestActor()
    const project = await projectService.getById(projectId)
    ensureProjectAccess(actor, "edit", project)
    const input = await parseJsonBody(request, finalizeUploadsInputSchema)

    const startIndex = await sceneService.nextOrderIndex(projectId)
    const scenes = await sceneService.createFromUploads(
      input.uploads.map((upload, index) => {
        const token = uploadService.verifyUploadToken(upload.uploadToken)

        if (token.projectId !== projectId) {
          throw new AppError({
            code: "UPLOAD_PROJECT_MISMATCH",
            message: "Upload token does not belong to this project.",
            statusCode: 400,
          })
        }

        if (token.mimeType !== upload.mimeType || token.sizeBytes !== upload.sizeBytes) {
          throw new AppError({
            code: "UPLOAD_METADATA_MISMATCH",
            message: "Upload metadata does not match the original upload contract.",
            statusCode: 400,
          })
        }

        const sceneId = crypto.randomUUID()
        const generationVersion = 1
        const thumbnailPath = buildThumbnailAssetPath(projectId, sceneId, generationVersion)

        return {
          id: sceneId,
          projectId,
          orderIndex: startIndex + index,
          generationVersion,
          sourceImageUrl: token.storageKey,
          thumbnailUrl: thumbnailPath,
          contextText: upload.contextText ?? null,
          motionPreset: upload.motionPreset ?? null,
          motionIntensity: upload.motionIntensity ?? null,
          expiresAt: project.expiresAt,
          originalAsset: {
            assetUrl: token.storageKey,
            width: upload.width,
            height: upload.height,
            metadataJson: {
              filename: upload.originalFilename,
              mimeType: upload.mimeType,
              sizeBytes: upload.sizeBytes,
              width: upload.width ?? null,
              height: upload.height ?? null,
            },
          },
          thumbnailAsset: {
            assetUrl: thumbnailPath,
            width: 320,
            height: 568,
            metadataJson: {
              derivedFrom: token.storageKey,
              kind: "generated-thumbnail",
            },
          },
        }
      }),
    )

    await Promise.all(
      scenes.map((scene) => {
        if (!scene.sourceImageUrl || !scene.thumbnailUrl) {
          return Promise.resolve()
        }

        return assetStorageService.copy(scene.sourceImageUrl, scene.thumbnailUrl)
      }),
    )

    for (const scene of scenes) {
      await processingService.enqueueSceneDecomposition(scene.id, context.correlationId, {
        reason: "upload-finalized",
      })
    }

    return created(scenes.map((scene) => serializeScene(scene)), { correlationId: context.correlationId })
  },

  async update(sceneId: string, request: Request, context: RequestContext) {
    const actor = await resolveRequestActor()
    const scene = await sceneService.getById(sceneId)
    ensureProjectAccess(actor, "edit", scene.project)
    const input = await parseJsonBody(request, updateSceneInputSchema)
    const updatedScene = await sceneService.update(sceneId, input)
    const refreshedScene = await motionService.generateForScene({
      id: updatedScene.id,
      projectId: updatedScene.projectId,
      assets: updatedScene.assets.map((asset) => ({
        assetType: asset.assetType,
        layerOrder: asset.layerOrder,
        metadataJson: asset.metadataJson,
      })),
      motionPreset: updatedScene.motionPreset,
      motionIntensity: updatedScene.motionIntensity,
      framingData: updatedScene.framingData,
    }, context.correlationId)
    await playbackService.stitchProject(scene.projectId, {
      allowFallback: true,
      traceId: context.correlationId,
    }).catch(() => null)
    return ok(serializeScene(refreshedScene), { correlationId: context.correlationId })
  },

  async remove(sceneId: string, context: RequestContext) {
    const actor = await resolveRequestActor()
    const scene = await sceneService.getById(sceneId)
    ensureProjectAccess(actor, "edit", scene.project)
    await sceneService.remove(sceneId)
    await playbackService.stitchProject(scene.projectId, {
      allowFallback: true,
      traceId: context.correlationId,
    }).catch(() => null)
    return ok({ deleted: true }, { correlationId: context.correlationId })
  },

  async retry(sceneId: string, request: Request, context: RequestContext) {
    const actor = await resolveRequestActor()
    const scene = await sceneService.getById(sceneId)
    ensureProjectAccess(actor, "edit", scene.project)
    const input = await parseJsonBody(request, sceneReprocessInputSchema)
    const result = await processingService.enqueueSceneDecomposition(sceneId, context.correlationId, {
      reason: input.reason ?? "manual-retry",
    })
    return created(result.job, { correlationId: context.correlationId })
  },

  async regenerate(sceneId: string, request: Request, context: RequestContext) {
    const actor = await resolveRequestActor()
    const scene = await sceneService.getById(sceneId)
    ensureProjectAccess(actor, "edit", scene.project)
    const input = await parseJsonBody(request, sceneReprocessInputSchema)
    const result = await processingService.enqueueSceneDecomposition(sceneId, context.correlationId, {
      reason: input.reason ?? "manual-regenerate",
      resetGeneration: true,
    })
    return created(result.job, { correlationId: context.correlationId })
  },
}



================================================
FILE: src/interfaces/http/controllers/upload-controller.ts
================================================
import { ok } from "@/lib/api-response"
import { parseJsonBody } from "@/interfaces/http/support/json-body"
import { resolveRequestActor } from "@/interfaces/http/support/request-actor"
import { ensureProjectAccess } from "@/interfaces/http/support/authorization"
import { initiateUploadsInputSchema } from "@/modules/uploads"
import { projectService } from "@/modules/projects"
import { uploadService } from "@/modules/uploads"
import type { RequestContext } from "@/core/request/context"

export const uploadController = {
  async initiate(projectId: string, request: Request, context: RequestContext) {
    const actor = await resolveRequestActor()
    const project = await projectService.getById(projectId)
    ensureProjectAccess(actor, "edit", project)
    const input = await parseJsonBody(request, initiateUploadsInputSchema)
    const uploads = uploadService.createUploadContracts(projectId, input.files)
    return ok({ uploads }, { correlationId: context.correlationId })
  },
}



================================================
FILE: src/interfaces/http/support/authorization.ts
================================================
import { AppError } from "@/core/errors/app-error"
import { authorizeProjectAction } from "@/modules/authorization"
import type { AuthorizationAction, AuthorizationActor, AuthorizationProject } from "@/modules/authorization"

export function ensureProjectAccess(
  actor: AuthorizationActor,
  action: AuthorizationAction,
  project: AuthorizationProject,
) {
  const decision = authorizeProjectAction(actor, action, project)

  if (!decision.allowed) {
    throw new AppError({
      code: "FORBIDDEN",
      message: decision.reason ?? "Access denied.",
      statusCode: action === "preview" ? 403 : 403,
    })
  }
}



================================================
FILE: src/interfaces/http/support/internal-maintenance.ts
================================================
import { timingSafeEqual } from "node:crypto"

import { getEnv } from "@/config/env"
import { AppError } from "@/core/errors/app-error"

export function ensureInternalMaintenanceAccess(request: Request) {
  const env = getEnv()

  if (!env.INTERNAL_MAINTENANCE_TOKEN) {
    throw new AppError({
      code: "MAINTENANCE_DISABLED",
      message: "Internal maintenance token is not configured.",
      statusCode: 503,
    })
  }

  const providedToken = request.headers.get("x-internal-maintenance-token")

  if (!providedToken || providedToken.length !== env.INTERNAL_MAINTENANCE_TOKEN.length) {
    throw new AppError({
      code: "FORBIDDEN",
      message: "Internal maintenance token is required.",
      statusCode: 403,
    })
  }

  if (!timingSafeEqual(Buffer.from(providedToken), Buffer.from(env.INTERNAL_MAINTENANCE_TOKEN))) {
    throw new AppError({
      code: "FORBIDDEN",
      message: "Internal maintenance token is required.",
      statusCode: 403,
    })
  }
}



================================================
FILE: src/interfaces/http/support/json-body.ts
================================================
import { ZodSchema } from "zod"

import { AppError } from "@/core/errors/app-error"

export async function parseJsonBody<T>(request: Request, schema: ZodSchema<T>): Promise<T> {
  const body = await request.json().catch(() => {
    throw new AppError({
      code: "INVALID_JSON",
      message: "Request body must be valid JSON.",
      statusCode: 400,
    })
  })

  return schema.parse(body)
}



================================================
FILE: src/interfaces/http/support/request-actor.ts
================================================
import { cookies } from "next/headers"

import { auth } from "@/auth"
import { getEnv } from "@/config/env"
import { guestSessionService } from "@/modules/guest-sessions"
import type { AuthorizationActor } from "@/modules/authorization"

export async function resolveRequestActor(): Promise<AuthorizationActor> {
  const session = await auth()
  const env = getEnv()
  const cookieStore = await cookies()
  const guestSessionId = cookieStore.get(env.GUEST_SESSION_COOKIE_NAME)?.value
  const guestSession = await guestSessionService.resolve(guestSessionId).catch(() => null)

  if (session?.user?.id) {
    return {
      kind: "authenticated",
      userId: session.user.id,
      guestSessionId: guestSession?.id ?? null,
    }
  }

  if (guestSession) {
    return {
      kind: "guest",
      guestSessionId: guestSession.id,
      expiresAt: guestSession.expiresAt,
    }
  }

  return {
    kind: "anonymous",
  }
}



================================================
FILE: src/lib/api-response.ts
================================================
import { NextResponse } from "next/server"

type Meta = {
  correlationId: string
}

export function ok<T>(data: T, meta: Meta, init?: ResponseInit) {
  return NextResponse.json({ data, meta }, init)
}

export function created<T>(data: T, meta: Meta) {
  return NextResponse.json({ data, meta }, { status: 201 })
}



================================================
FILE: src/modules/assets/index.ts
================================================
export * from "@/modules/assets/pathing"
export * from "@/modules/assets/serialization"
export * from "@/modules/assets/service"
export * from "@/modules/assets/storage"



================================================
FILE: src/modules/assets/pathing.ts
================================================
import { UPLOAD_BASE_PATH } from "@/config/constants"

export function buildSceneVersionPath(projectId: string, sceneId: string, generationVersion: number) {
  return `${UPLOAD_BASE_PATH}/${projectId}/scenes/${sceneId}/v${generationVersion}`
}

export function buildOriginalAssetPath(projectId: string, filename: string) {
  const safeFilename = filename.replace(/[^a-zA-Z0-9._-]/g, "-").toLowerCase()
  return `${UPLOAD_BASE_PATH}/${projectId}/incoming/${Date.now()}-${safeFilename}`
}

export function buildThumbnailAssetPath(projectId: string, sceneId: string, generationVersion: number) {
  return `${buildSceneVersionPath(projectId, sceneId, generationVersion)}/thumbnail.webp`
}

export function buildLayerAssetPath(projectId: string, sceneId: string, generationVersion: number, index: number) {
  return `${buildSceneVersionPath(projectId, sceneId, generationVersion)}/layers/${index}.png`
}

export function buildCompositeAssetPath(projectId: string, sceneId: string, generationVersion: number) {
  return `${buildSceneVersionPath(projectId, sceneId, generationVersion)}/composite.png`
}

export function buildManifestAssetPath(projectId: string, sceneId: string, generationVersion: number) {
  return `${buildSceneVersionPath(projectId, sceneId, generationVersion)}/manifest.json`
}



================================================
FILE: src/modules/assets/serialization.ts
================================================
import type { PlaybackPlan, Project, Scene, SceneAsset } from "@prisma/client"

import { toPublicAssetUrl } from "@/modules/assets/storage"

type SceneWithAssets = Scene & {
  assets?: SceneAsset[]
}

type ProjectWithScenes = Project & {
  scenes?: SceneWithAssets[]
}

function serializeSceneAsset<T extends SceneAsset>(asset: T) {
  return {
    ...asset,
    assetUrl: toPublicAssetUrl(asset.assetUrl) ?? asset.assetUrl,
  }
}

export function serializeScene<T extends SceneWithAssets>(scene: T) {
  return {
    ...scene,
    sourceImageUrl: toPublicAssetUrl(scene.sourceImageUrl),
    thumbnailUrl: toPublicAssetUrl(scene.thumbnailUrl),
    assets: Array.isArray(scene.assets) ? scene.assets.map((asset) => serializeSceneAsset(asset)) : scene.assets,
  }
}

export function serializeProject<T extends ProjectWithScenes>(project: T) {
  return {
    ...project,
    scenes: Array.isArray(project.scenes) ? project.scenes.map((scene) => serializeScene(scene)) : project.scenes,
  }
}

export function serializeProjects<T extends ProjectWithScenes>(projects: T[]) {
  return projects.map((project) => serializeProject(project))
}

export function serializePlaybackPlan<T extends PlaybackPlan>(plan: T) {
  const timelineJson = typeof plan.timelineJson === "object" && plan.timelineJson ? plan.timelineJson as Record<string, unknown> : null
  const scenes = Array.isArray(timelineJson?.scenes) ? timelineJson.scenes : []

  return {
    ...plan,
    timelineJson: timelineJson
      ? {
          ...timelineJson,
          scenes: scenes.map((scene) => {
            if (!scene || typeof scene !== "object") {
              return scene
            }

            const record = scene as Record<string, unknown>
            return {
              ...record,
              sourceImageUrl: typeof record.sourceImageUrl === "string" ? toPublicAssetUrl(record.sourceImageUrl) : record.sourceImageUrl,
              thumbnailUrl: typeof record.thumbnailUrl === "string" ? toPublicAssetUrl(record.thumbnailUrl) : record.thumbnailUrl,
            }
          }),
        }
      : plan.timelineJson,
  }
}



================================================
FILE: src/modules/assets/service.ts
================================================
import { Prisma } from "@prisma/client"

import { buildCompositeAssetPath, buildLayerAssetPath, buildManifestAssetPath, buildThumbnailAssetPath } from "@/modules/assets/pathing"
import { sceneRepository } from "@/modules/scenes/repository"
import { assetStorageService, toStorageKey } from "@/modules/assets/storage"
import type { DecompositionArtifact } from "@/modules/decomposition/types"

type PersistAssetsInput = {
  projectId: string
  sceneId: string
  generationVersion: number
  sourceAssetPath: string
  expiresAt?: Date | null
  width?: number
  height?: number
  compositeArtifact?: DecompositionArtifact | null
  thumbnailArtifact?: DecompositionArtifact | null
  layers: Array<{
    index: number
    width?: number
    height?: number
    metadata: Record<string, unknown>
    artifact?: DecompositionArtifact | null
  }>
}

function decodeBase64Artifact(value: string) {
  const payload = value.includes(",") ? value.slice(value.indexOf(",") + 1) : value
  return Buffer.from(payload, "base64")
}

async function persistArtifact(targetPath: string, sourceAssetPath: string, artifact?: DecompositionArtifact | null) {
  if (artifact?.base64Data) {
    await assetStorageService.write(targetPath, decodeBase64Artifact(artifact.base64Data))
    return { persistedFrom: "base64", fallbackUsed: false }
  }

  if (artifact?.storageKey) {
    await assetStorageService.copy(artifact.storageKey, targetPath)
    return { persistedFrom: "storage", fallbackUsed: false }
  }

  if (artifact?.assetUrl) {
    if (artifact.assetUrl.startsWith("data:")) {
      await assetStorageService.write(targetPath, decodeBase64Artifact(artifact.assetUrl))
      return { persistedFrom: "data-url", fallbackUsed: false }
    }

    if (artifact.assetUrl.startsWith("http://") || artifact.assetUrl.startsWith("https://")) {
      const response = await fetch(artifact.assetUrl)

      if (!response.ok) {
        throw new Error(`Unable to fetch generated asset from ${artifact.assetUrl}.`)
      }

      const content = Buffer.from(await response.arrayBuffer())
      await assetStorageService.write(targetPath, content)
      return { persistedFrom: "remote-url", fallbackUsed: false }
    }

    await assetStorageService.copy(toStorageKey(artifact.assetUrl), targetPath)
    return { persistedFrom: "asset-url", fallbackUsed: false }
  }

  await assetStorageService.copy(sourceAssetPath, targetPath)
  return { persistedFrom: "source-copy", fallbackUsed: true }
}

export const assetService = {
  async persistDecompositionAssets(input: PersistAssetsInput) {
    const compositePath = buildCompositeAssetPath(input.projectId, input.sceneId, input.generationVersion)
    const thumbnailPath = buildThumbnailAssetPath(input.projectId, input.sceneId, input.generationVersion)
    const manifestPath = buildManifestAssetPath(input.projectId, input.sceneId, input.generationVersion)
    const layerPaths = input.layers.map((layer) => ({
      ...layer,
      path: buildLayerAssetPath(input.projectId, input.sceneId, input.generationVersion, layer.index),
    }))

    const manifest = {
      projectId: input.projectId,
      sceneId: input.sceneId,
      generationVersion: input.generationVersion,
      compositePath,
      thumbnailPath,
      generatedAt: new Date().toISOString(),
    }

    const [compositePersistence, thumbnailPersistence, layerPersistence] = await Promise.all([
      persistArtifact(compositePath, input.sourceAssetPath, input.compositeArtifact),
      persistArtifact(thumbnailPath, input.sourceAssetPath, input.thumbnailArtifact),
      Promise.all(
        layerPaths.map(async (layer) => ({
          index: layer.index,
          result: await persistArtifact(layer.path, input.sourceAssetPath, layer.artifact),
        })),
      ),
    ])

    const manifestWithArtifacts = {
      ...manifest,
      composite: {
        path: compositePath,
        persistedFrom: compositePersistence.persistedFrom,
        fallbackUsed: compositePersistence.fallbackUsed,
      },
      thumbnail: {
        path: thumbnailPath,
        persistedFrom: thumbnailPersistence.persistedFrom,
        fallbackUsed: thumbnailPersistence.fallbackUsed,
      },
      layers: layerPaths.map((layer) => {
        const persistence = layerPersistence.find((entry) => entry.index === layer.index)?.result

        return {
          index: layer.index,
          path: layer.path,
          width: layer.width ?? null,
          height: layer.height ?? null,
          persistedFrom: persistence?.persistedFrom ?? "source-copy",
          fallbackUsed: persistence?.fallbackUsed ?? true,
          metadata: {
            ...layer.metadata,
            artifact: layer.artifact
              ? {
                  assetUrl: layer.artifact.assetUrl ?? null,
                  storageKey: layer.artifact.storageKey ?? null,
                  mimeType: layer.artifact.mimeType ?? null,
                  providerFileId: layer.artifact.providerFileId ?? null,
                  metadata: layer.artifact.metadata ?? null,
                }
              : null,
          },
        }
      }),
    }

    await assetStorageService.write(manifestPath, JSON.stringify(manifestWithArtifacts, null, 2))

    return sceneRepository.replaceGeneratedAssets(input.sceneId, {
      expiresAt: input.expiresAt,
      layerAssets: layerPaths.map((layer) => ({
        assetUrl: layer.path,
        width: layer.width,
        height: layer.height,
        layerOrder: layer.index,
        metadataJson: {
          ...layer.metadata,
          artifact: layer.artifact
            ? {
                assetUrl: layer.artifact.assetUrl ?? null,
                storageKey: layer.artifact.storageKey ?? null,
                mimeType: layer.artifact.mimeType ?? null,
                providerFileId: layer.artifact.providerFileId ?? null,
                metadata: layer.artifact.metadata ?? null,
              }
            : null,
        } as Prisma.InputJsonValue,
      })),
      compositeAsset: {
        assetUrl: compositePath,
        width: input.width,
        height: input.height,
        metadataJson: {
          kind: "composite-preview",
          artifact: input.compositeArtifact
            ? {
                assetUrl: input.compositeArtifact.assetUrl ?? null,
                storageKey: input.compositeArtifact.storageKey ?? null,
                mimeType: input.compositeArtifact.mimeType ?? null,
                providerFileId: input.compositeArtifact.providerFileId ?? null,
                metadata: input.compositeArtifact.metadata ?? null,
              }
            : null,
        } as Prisma.InputJsonValue,
      },
      manifestAsset: {
        assetUrl: manifestPath,
        metadataJson: manifestWithArtifacts as Prisma.InputJsonValue,
      },
    })
  },
}



================================================
FILE: src/modules/assets/storage.ts
================================================
import { mkdir, readFile, stat, writeFile, copyFile } from "node:fs/promises"
import path from "node:path"

import { getEnv } from "@/config/env"
import { AppError } from "@/core/errors/app-error"

const ASSET_ROUTE_PREFIX = "/api/v1/assets"

function normalizeStorageKey(storageKey: string) {
  const normalized = storageKey.replace(/^\/+/, "")

  if (!normalized || normalized.includes("..") || path.isAbsolute(normalized)) {
    throw new AppError({
      code: "INVALID_ASSET_PATH",
      message: "Asset path is invalid.",
      statusCode: 400,
    })
  }

  return normalized
}

function absolutePathFor(storageKey: string) {
  const env = getEnv()
  const normalized = normalizeStorageKey(storageKey)
  const storageRoot = path.resolve(process.cwd(), env.LOCAL_STORAGE_ROOT)
  return path.join(storageRoot, normalized)
}

export function toPublicAssetUrl(storageKey: string | null | undefined) {
  if (!storageKey) {
    return null
  }

  if (storageKey.startsWith("http://") || storageKey.startsWith("https://") || storageKey.startsWith("/")) {
    return storageKey
  }

  return `${ASSET_ROUTE_PREFIX}/${normalizeStorageKey(storageKey)}`
}

export function toStorageKey(assetUrlOrPath: string) {
  if (assetUrlOrPath.startsWith(`${ASSET_ROUTE_PREFIX}/`)) {
    return normalizeStorageKey(assetUrlOrPath.slice(ASSET_ROUTE_PREFIX.length + 1))
  }

  return normalizeStorageKey(assetUrlOrPath)
}

export const assetStorageService = {
  toPublicAssetUrl,
  toStorageKey,

  async write(storageKey: string, content: Buffer | string) {
    const filePath = absolutePathFor(storageKey)
    await mkdir(path.dirname(filePath), { recursive: true })
    await writeFile(filePath, content)
  },

  async copy(sourceStorageKey: string, targetStorageKey: string) {
    const sourcePath = absolutePathFor(sourceStorageKey)
    const targetPath = absolutePathFor(targetStorageKey)
    await mkdir(path.dirname(targetPath), { recursive: true })
    await copyFile(sourcePath, targetPath)
  },

  async read(storageKey: string) {
    const filePath = absolutePathFor(storageKey)

    try {
      const [content, details] = await Promise.all([readFile(filePath), stat(filePath)])
      return {
        content,
        sizeBytes: details.size,
      }
    } catch {
      throw new AppError({
        code: "ASSET_NOT_FOUND",
        message: "Requested asset was not found.",
        statusCode: 404,
      })
    }
  },
}



================================================
FILE: src/modules/auth/index.ts
================================================
export * from "@/modules/auth/service"
export * from "@/modules/auth/types"
export * from "@/modules/auth/validator"



================================================
FILE: src/modules/auth/repository.ts
================================================
import { AuthProvider, Prisma } from "@prisma/client"

import { prisma } from "@/infrastructure/db/prisma"

export const authRepository = {
  findByEmail(email: string) {
    return prisma.user.findUnique({
      where: { email },
    })
  },

  createUser(data: Prisma.UserCreateInput) {
    return prisma.user.create({ data })
  },

  upsertGoogleUser(email: string) {
    return prisma.user.upsert({
      where: { email },
      update: { authProvider: AuthProvider.google },
      create: {
        email,
        authProvider: AuthProvider.google,
      },
    })
  },
}



================================================
FILE: src/modules/auth/service.ts
================================================
import bcrypt from "bcryptjs"
import { AuthProvider } from "@prisma/client"

import { AppError } from "@/core/errors/app-error"
import { authRepository } from "@/modules/auth/repository"
import type { RegisterInput } from "@/modules/auth/types"

export const authService = {
  async register(input: RegisterInput) {
    const existingUser = await authRepository.findByEmail(input.email)

    if (existingUser) {
      throw new AppError({
        code: "EMAIL_ALREADY_IN_USE",
        message: "An account with this email already exists.",
        statusCode: 409,
      })
    }

    const passwordHash = await bcrypt.hash(input.password, 12)

    const user = await authRepository.createUser({
      email: input.email,
      authProvider: AuthProvider.credentials,
      passwordHash,
    })

    return {
      id: user.id,
      email: user.email,
      authProvider: user.authProvider,
      createdAt: user.createdAt,
    }
  },
}



================================================
FILE: src/modules/auth/types.ts
================================================
export type SessionActor =
  | {
      kind: "anonymous"
    }
  | {
      kind: "guest"
      guestSessionId: string
    }
  | {
      kind: "authenticated"
      userId: string
      email: string
      guestSessionId?: string | null
    }

export type AuthenticatedUserRecord = {
  id: string
  email: string
  authProvider: "credentials" | "google"
  passwordHash: string | null
}

export type RegisterInput = {
  email: string
  password: string
}



================================================
FILE: src/modules/auth/validator.ts
================================================
import { z } from "zod"

export const registerInputSchema = z.object({
  email: z.string().email(),
  password: z.string().min(8).max(72),
})



================================================
FILE: src/modules/authorization/index.ts
================================================
export * from "@/modules/authorization/service"
export * from "@/modules/authorization/types"



================================================
FILE: src/modules/authorization/service.ts
================================================
import type {
  AuthorizationAction,
  AuthorizationActor,
  AuthorizationDecision,
  AuthorizationProject,
} from "@/modules/authorization/types"

export function authorizeProjectAction(
  actor: AuthorizationActor,
  action: AuthorizationAction,
  project: AuthorizationProject,
): AuthorizationDecision {
  if (actor.kind === "anonymous") {
    return {
      allowed: false,
      reason: "Authentication or guest session is required.",
    }
  }

  if (project.expiresAt && project.expiresAt.getTime() <= Date.now()) {
    return {
      allowed: false,
      reason: "Project access has expired.",
    }
  }

  if (actor.kind === "guest") {
    const matchesGuest = project.guestSessionId === actor.guestSessionId

    if (!matchesGuest) {
      return {
        allowed: false,
        reason: "Guest session does not own this project.",
      }
    }

    if (action === "preview" || action === "edit") {
      return { allowed: true }
    }

    return {
      allowed: false,
      reason: "Guests may preview only until the project is claimed.",
    }
  }

  if (project.ownerId && project.ownerId === actor.userId) {
    return { allowed: true }
  }

  if (action === "claim") {
    const sameGuestSession = actor.guestSessionId && project.guestSessionId === actor.guestSessionId
    return {
      allowed: Boolean(sameGuestSession && !project.claimedAt),
      reason: sameGuestSession && !project.claimedAt ? undefined : "Project cannot be claimed by this user.",
    }
  }

  if (action === "preview" && project.guestSessionId && actor.guestSessionId === project.guestSessionId) {
    return { allowed: true }
  }

  return {
    allowed: false,
    reason: "Authenticated user does not own this project.",
  }
}



================================================
FILE: src/modules/authorization/types.ts
================================================
export type AuthorizationAction = "preview" | "edit" | "save" | "claim" | "export"

export type AuthorizationActor =
  | {
      kind: "anonymous"
    }
  | {
      kind: "guest"
      guestSessionId: string
      expiresAt?: Date | null
    }
  | {
      kind: "authenticated"
      userId: string
      guestSessionId?: string | null
    }

export type AuthorizationProject = {
  ownerId: string | null
  guestSessionId: string | null
  claimedAt: Date | null
  expiresAt: Date | null
}

export type AuthorizationDecision = {
  allowed: boolean
  reason?: string
}



================================================
FILE: src/modules/decomposition/adapter.ts
================================================
import { DEFAULT_SCENE_LAYER_COUNT } from "@/config/constants"
import { qwenClient } from "@/infrastructure/providers/qwen/client"
import type { DecompositionArtifact, DecompositionRequest, DecompositionResult } from "@/modules/decomposition/types"
import { ProviderError } from "@/modules/decomposition/types"

function normalizeArtifact(raw: Record<string, unknown> | null | undefined): DecompositionArtifact | null {
  if (!raw) {
    return null
  }

  const assetUrl = typeof raw.assetUrl === "string" ? raw.assetUrl : typeof raw.imageUrl === "string" ? raw.imageUrl : typeof raw.url === "string" ? raw.url : undefined
  const storageKey =
    typeof raw.storageKey === "string" ? raw.storageKey : typeof raw.storagePath === "string" ? raw.storagePath : undefined
  const base64Data =
    typeof raw.base64Data === "string"
      ? raw.base64Data
      : typeof raw.base64 === "string"
        ? raw.base64
        : typeof raw.b64_json === "string"
          ? raw.b64_json
          : undefined
  const mimeType =
    typeof raw.mimeType === "string" ? raw.mimeType : typeof raw.contentType === "string" ? raw.contentType : undefined
  const providerFileId =
    typeof raw.providerFileId === "string" ? raw.providerFileId : typeof raw.fileId === "string" ? raw.fileId : undefined

  if (!assetUrl && !storageKey && !base64Data && !providerFileId) {
    return null
  }

  return {
    assetUrl,
    storageKey,
    base64Data,
    mimeType,
    providerFileId,
    metadata: {
      ...(typeof raw.metadata === "object" && raw.metadata ? (raw.metadata as Record<string, unknown>) : {}),
      ...(providerFileId ? { providerFileId } : {}),
    },
  }
}

export const decompositionAdapter = {
  async decompose(request: DecompositionRequest): Promise<DecompositionResult> {
    const raw = await qwenClient.submit({
      imageUrl: request.imageUrl,
      mimeType: request.mimeType,
      targetLayers: request.targetLayers,
      correlationId: request.correlationId,
    })

    if (!raw || !Array.isArray(raw.layers)) {
      throw new ProviderError("terminal", "QWEN_INVALID_RESPONSE", "Qwen returned an invalid decomposition payload.")
    }

    return {
      providerJobId: String(raw.id ?? `qwen-${request.sceneId}`),
      modelVersion: String(raw.modelVersion ?? "qwen-image-layered"),
      width: typeof raw.width === "number" ? raw.width : request.width,
      height: typeof raw.height === "number" ? raw.height : request.height,
      compositeArtifact: normalizeArtifact(typeof raw.composite === "object" && raw.composite ? (raw.composite as Record<string, unknown>) : null),
      thumbnailArtifact: normalizeArtifact(typeof raw.thumbnail === "object" && raw.thumbnail ? (raw.thumbnail as Record<string, unknown>) : null),
      layers: raw.layers.slice(0, request.targetLayers || DEFAULT_SCENE_LAYER_COUNT).map((layer: any, index: number) => ({
        index,
        width: typeof layer.width === "number" ? layer.width : request.width,
        height: typeof layer.height === "number" ? layer.height : request.height,
        artifact: normalizeArtifact(typeof layer === "object" && layer ? layer : null),
        metadata: {
          source: "qwen",
          depth: layer.depth ?? index,
        },
      })),
      warnings: Array.isArray(raw.warnings) ? raw.warnings.map(String) : [],
    }
  },
}



================================================
FILE: src/modules/decomposition/service.ts
================================================
import { DEFAULT_SCENE_LAYER_COUNT } from "@/config/constants"
import { metrics } from "@/core/observability/metrics"
import { logProcessingEvent } from "@/core/observability/processing-log"
import { assetService } from "@/modules/assets"
import { decompositionAdapter } from "@/modules/decomposition/adapter"
import { ProviderError } from "@/modules/decomposition/types"
import { featureFlagService } from "@/modules/feature-flags"
import { motionService } from "@/modules/motion"
import { playbackService } from "@/modules/playback"
import { sceneService } from "@/modules/scenes"

export const decompositionService = {
  async processScene(scene: {
    id: string
    generationVersion: number
    sourceImageUrl: string | null
    expiresAt: Date | null
    project: { id: string }
    assets: Array<{ assetType: string; metadataJson: unknown }>
  }, job: { id: string; attemptCount: number; correlationId?: string | null }) {
    const startedAt = Date.now()

    if (!scene.sourceImageUrl) {
      throw new ProviderError("terminal", "SCENE_SOURCE_MISSING", "Scene does not have a source image URL.")
    }

    const originalAsset = scene.assets.find((asset) => asset.assetType === "original")
    const metadata = typeof originalAsset?.metadataJson === "object" && originalAsset?.metadataJson ? originalAsset.metadataJson as Record<string, unknown> : {}

    const attemptCount = job.attemptCount + 1
    const correlationId = job.correlationId ?? crypto.randomUUID()
    const result = await decompositionAdapter.decompose({
      projectId: scene.project.id,
      sceneId: scene.id,
      imageUrl: scene.sourceImageUrl,
      mimeType: typeof metadata.mimeType === "string" ? metadata.mimeType : "image/png",
      width: typeof metadata.width === "number" ? metadata.width : undefined,
      height: typeof metadata.height === "number" ? metadata.height : undefined,
      targetLayers: DEFAULT_SCENE_LAYER_COUNT,
      correlationId,
    })

    await sceneService.markProcessing(job.id, scene.id, attemptCount, result.providerJobId)

    await assetService.persistDecompositionAssets({
      projectId: scene.project.id,
      sceneId: scene.id,
      generationVersion: scene.generationVersion,
      sourceAssetPath: scene.sourceImageUrl,
      expiresAt: scene.expiresAt,
      width: result.width,
      height: result.height,
      compositeArtifact: result.compositeArtifact,
      thumbnailArtifact: result.thumbnailArtifact,
      layers: result.layers.map((layer) => ({
        index: layer.index,
        width: layer.width,
        height: layer.height,
        artifact: layer.artifact,
        metadata: {
          ...layer.metadata,
          modelVersion: result.modelVersion,
        },
      })),
    })

    const refreshedScene = await sceneService.getById(scene.id)

    if (featureFlagService.isEnabled("motionPipeline")) {
      await motionService.generateForScene({
        id: refreshedScene.id,
        projectId: refreshedScene.projectId,
        assets: refreshedScene.assets.map((asset) => ({
          assetType: asset.assetType,
          layerOrder: asset.layerOrder,
          metadataJson: asset.metadataJson,
        })),
        motionPreset: refreshedScene.motionPreset,
        motionIntensity: refreshedScene.motionIntensity,
        framingData: refreshedScene.framingData,
      }, correlationId)
    }

    await sceneService.markReady(job.id, scene.id)

    if (featureFlagService.isEnabled("playbackPipeline")) {
      await playbackService.stitchProject(scene.project.id, {
        traceId: correlationId,
        allowFallback: true,
      })
    }

    metrics.observe("processing_decomposition_duration_ms", Date.now() - startedAt)
    logProcessingEvent({
      event: "scene decomposition completed",
      traceId: correlationId,
      projectId: scene.project.id,
      sceneId: scene.id,
      jobId: job.id,
      details: {
        providerJobId: result.providerJobId,
      },
    })
  },
}



================================================
FILE: src/modules/decomposition/types.ts
================================================
export type DecompositionRequest = {
  projectId: string
  sceneId: string
  imageUrl: string
  mimeType: string
  width?: number
  height?: number
  targetLayers: number
  correlationId: string
}

export type DecompositionLayer = {
  index: number
  width?: number
  height?: number
  metadata: Record<string, unknown>
  artifact?: DecompositionArtifact | null
}

export type DecompositionArtifact = {
  assetUrl?: string
  storageKey?: string
  base64Data?: string
  mimeType?: string
  providerFileId?: string
  metadata?: Record<string, unknown>
}

export type DecompositionResult = {
  providerJobId: string
  modelVersion: string
  width?: number
  height?: number
  compositeArtifact?: DecompositionArtifact | null
  thumbnailArtifact?: DecompositionArtifact | null
  layers: DecompositionLayer[]
  warnings?: string[]
}

export type ProviderErrorKind = "retryable" | "terminal"

export class ProviderError extends Error {
  public readonly kind: ProviderErrorKind
  public readonly code: string

  constructor(kind: ProviderErrorKind, code: string, message: string) {
    super(message)
    this.kind = kind
    this.code = code
  }
}



================================================
FILE: src/modules/feature-flags/index.ts
================================================
export * from "@/modules/feature-flags/service"



================================================
FILE: src/modules/feature-flags/service.ts
================================================
import { getEnv } from "@/config/env"

export const featureFlagService = {
  flags() {
    const env = getEnv()

    return {
      motionPipeline: env.FEATURE_MOTION_PIPELINE,
      playbackPipeline: env.FEATURE_PLAYBACK_PIPELINE,
      previewFallbacks: env.FEATURE_PREVIEW_FALLBACKS,
      reducedMotionPreview: env.FEATURE_REDUCED_MOTION_PREVIEW,
      processingCanaryPercent: env.PROCESSING_CANARY_PERCENT,
    }
  },

  isEnabled(flag: "motionPipeline" | "playbackPipeline" | "previewFallbacks" | "reducedMotionPreview") {
    return this.flags()[flag]
  },

  allowsProcessing(seed: string) {
    const percent = this.flags().processingCanaryPercent

    if (percent >= 100) {
      return true
    }

    let hash = 0
    for (let index = 0; index < seed.length; index += 1) {
      hash = (hash * 31 + seed.charCodeAt(index)) % 100
    }

    return hash < percent
  },
}



================================================
FILE: src/modules/guest-sessions/index.ts
================================================
export * from "@/modules/guest-sessions/service"
export * from "@/modules/guest-sessions/types"



================================================
FILE: src/modules/guest-sessions/repository.ts
================================================
import { prisma } from "@/infrastructure/db/prisma"

export const guestSessionRepository = {
  create(data: { expiresAt: Date }) {
    return prisma.guestSession.create({
      data,
    })
  },

  findById(id: string) {
    return prisma.guestSession.findUnique({
      where: { id },
    })
  },

  touch(id: string) {
    return prisma.guestSession.update({
      where: { id },
      data: {
        lastSeenAt: new Date(),
      },
    })
  },
}



================================================
FILE: src/modules/guest-sessions/service.ts
================================================
import { AppError } from "@/core/errors/app-error"
import { getEnv } from "@/config/env"
import { guestSessionRepository } from "@/modules/guest-sessions/repository"

function addHours(date: Date, hours: number) {
  return new Date(date.getTime() + hours * 60 * 60 * 1000)
}

export const guestSessionService = {
  async issue() {
    const env = getEnv()
    const expiresAt = addHours(new Date(), env.GUEST_SESSION_TTL_HOURS)
    return guestSessionRepository.create({ expiresAt })
  },

  async resolve(guestSessionId: string | undefined) {
    if (!guestSessionId) {
      return null
    }

    const guestSession = await guestSessionRepository.findById(guestSessionId)

    if (!guestSession) {
      return null
    }

    if (guestSession.expiresAt.getTime() <= Date.now()) {
      throw new AppError({
        code: "GUEST_SESSION_EXPIRED",
        message: "Guest session has expired.",
        statusCode: 401,
      })
    }

    await guestSessionRepository.touch(guestSession.id)
    return guestSession
  },
}



================================================
FILE: src/modules/guest-sessions/types.ts
================================================
export type GuestSessionRecord = {
  id: string
  expiresAt: Date
  createdAt: Date
}



================================================
FILE: src/modules/maintenance/index.ts
================================================
export * from "@/modules/maintenance/service"



================================================
FILE: src/modules/maintenance/service.ts
================================================
import { getEnv } from "@/config/env"
import { metrics } from "@/core/observability/metrics"
import { logProcessingEvent } from "@/core/observability/processing-log"
import { projectRepository } from "@/modules/projects/repository"
import { sceneRepository } from "@/modules/scenes/repository"
import { sceneService } from "@/modules/scenes"

export const maintenanceService = {
  async cleanupExpiredGuestResources(traceId?: string | null) {
    const now = new Date()
    const deletedProjects = await projectRepository.deleteExpiredGuestProjects(now)
    const deletedSessions = await projectRepository.deleteExpiredGuestSessions(now)

    metrics.increment("guest_cleanup_deleted_projects_total", deletedProjects.count)
    metrics.increment("guest_cleanup_deleted_sessions_total", deletedSessions.count)

    logProcessingEvent({
      event: "guest cleanup completed",
      traceId,
      details: {
        deletedProjects: deletedProjects.count,
        deletedSessions: deletedSessions.count,
      },
    })

    return {
      deletedProjects: deletedProjects.count,
      deletedSessions: deletedSessions.count,
    }
  },

  async recoverTimedOutJobs(traceId?: string | null) {
    const env = getEnv()
    const timeoutBefore = new Date(Date.now() - env.PROCESSING_JOB_TIMEOUT_MS)
    const jobs = await sceneRepository.findTimedOutJobs(timeoutBefore)

    for (const job of jobs) {
      await sceneService.markFailed(job.id, job.sceneId, "Processing timed out and was recovered by maintenance.", job.attemptCount + 1)
      logProcessingEvent({
        event: "timed out job recovered",
        traceId,
        projectId: job.scene.projectId,
        sceneId: job.sceneId,
        jobId: job.id,
      })
    }

    metrics.gauge("processing_queue_depth", 0)

    return {
      recoveredJobs: jobs.length,
    }
  },
}



================================================
FILE: src/modules/motion/index.ts
================================================
export * from "@/modules/motion/service"
export * from "@/modules/motion/types"



================================================
FILE: src/modules/motion/service.ts
================================================
import { Prisma } from "@prisma/client"

import { DEFAULT_SCENE_OVERLAP_MS } from "@/config/constants"
import { metrics } from "@/core/observability/metrics"
import { logProcessingEvent } from "@/core/observability/processing-log"
import { sceneRepository } from "@/modules/scenes/repository"
import type {
  EasingKey,
  GroupKey,
  MobileGroupScrollMapping,
  SceneGroupConfig,
  SceneGroupingConfig,
} from "@/modules/scenes"
import type { MotionBlueprint, MotionLayerBehavior } from "@/modules/motion/types"

const GROUP_KEYS: GroupKey[] = ["background", "midground", "foreground"]

const GROUP_DEFAULTS: Record<GroupKey, MobileGroupScrollMapping> = {
  background: {
    startProgress: 0,
    endProgress: 1,
    translateX: -6,
    translateY: -18,
    scaleFrom: 1,
    scaleTo: 1.06,
    opacityFrom: 1,
    opacityTo: 0.94,
    speedMultiplier: 0.72,
    easing: "ease-out",
  },
  midground: {
    startProgress: 0,
    endProgress: 1,
    translateX: 0,
    translateY: -30,
    scaleFrom: 1,
    scaleTo: 1.1,
    opacityFrom: 1,
    opacityTo: 0.98,
    speedMultiplier: 1,
    easing: "linear",
  },
  foreground: {
    startProgress: 0,
    endProgress: 1,
    translateX: 10,
    translateY: -46,
    scaleFrom: 1,
    scaleTo: 1.16,
    opacityFrom: 1,
    opacityTo: 1,
    speedMultiplier: 1.22,
    easing: "ease-in-out",
  },
}

const GROUP_PARALLAX_WEIGHT: Record<GroupKey, number> = {
  background: 0.36,
  midground: 0.62,
  foreground: 0.9,
}

function intensityFromPreset(value: string | null | undefined): MotionBlueprint["intensity"] {
  if (!value) {
    return "medium"
  }

  const normalized = value.toLowerCase()
  if (normalized.includes("low") || normalized.includes("gentle")) {
    return "low"
  }
  if (normalized.includes("high") || normalized.includes("dramatic")) {
    return "high"
  }
  return "medium"
}

function movementFromPreset(value: string | null | undefined): MotionBlueprint["cameraMovement"] {
  if (!value) {
    return "drift-up"
  }

  const normalized = value.toLowerCase()
  if (normalized.includes("push")) {
    return "push-in"
  }
  if (normalized.includes("right") || normalized.includes("pan")) {
    return "drift-right"
  }
  if (normalized.includes("still") || normalized.includes("hold")) {
    return "hold"
  }
  return "drift-up"
}

function round(value: number, digits = 3) {
  return Number(value.toFixed(digits))
}

function asRecord(value: unknown) {
  return typeof value === "object" && value !== null && !Array.isArray(value) ? value as Record<string, unknown> : null
}

function toFiniteNumber(value: unknown) {
  return typeof value === "number" && Number.isFinite(value) ? value : null
}

function toLayerIndex(value: unknown) {
  return typeof value === "number" && Number.isInteger(value) && value >= 0 ? value : null
}

function toEasingKey(value: unknown): EasingKey | null {
  return value === "linear" || value === "ease-out" || value === "ease-in-out" ? value : null
}

function toGroupKey(value: unknown): GroupKey | null {
  return value === "background" || value === "midground" || value === "foreground" ? value : null
}

function parseMobileMapping(value: unknown): MobileGroupScrollMapping | null {
  const record = asRecord(value)

  if (!record) {
    return null
  }

  const startProgress = toFiniteNumber(record.startProgress)
  const endProgress = toFiniteNumber(record.endProgress)
  const translateX = toFiniteNumber(record.translateX)
  const translateY = toFiniteNumber(record.translateY)
  const scaleFrom = toFiniteNumber(record.scaleFrom)
  const scaleTo = toFiniteNumber(record.scaleTo)
  const opacityFrom = toFiniteNumber(record.opacityFrom)
  const opacityTo = toFiniteNumber(record.opacityTo)
  const speedMultiplier = toFiniteNumber(record.speedMultiplier)
  const easing = toEasingKey(record.easing)

  if (
    startProgress === null ||
    endProgress === null ||
    translateX === null ||
    translateY === null ||
    scaleFrom === null ||
    scaleTo === null ||
    opacityFrom === null ||
    opacityTo === null ||
    speedMultiplier === null ||
    easing === null
  ) {
    return null
  }

  return {
    startProgress,
    endProgress,
    translateX,
    translateY,
    scaleFrom,
    scaleTo,
    opacityFrom,
    opacityTo,
    speedMultiplier,
    easing,
  }
}

function parseGrouping(value: unknown): SceneGroupingConfig | null {
  const record = asRecord(value)

  if (!record || record.version !== 1 || !Array.isArray(record.groups)) {
    return null
  }

  const groups = record.groups
    .map((group): SceneGroupConfig | null => {
      const groupRecord = asRecord(group)

      if (!groupRecord || !Array.isArray(groupRecord.layerIndexes)) {
        return null
      }

      const groupKey = toGroupKey(groupRecord.groupKey)
      const mobile = parseMobileMapping(groupRecord.mobile)
      const layerIndexes = groupRecord.layerIndexes.map((item) => toLayerIndex(item)).filter((item): item is number => item !== null)

      if (!groupKey || !mobile || layerIndexes.length !== groupRecord.layerIndexes.length) {
        return null
      }

      return {
        groupKey,
        layerIndexes,
        mobile,
      }
    })
    .filter((group): group is SceneGroupConfig => group !== null)

  return groups.length > 0 ? { version: 1, groups } : null
}

function deriveVariantScale(value: number, factor: number) {
  return round(1 + (value - 1) * factor)
}

function deriveTabletMapping(mobile: MobileGroupScrollMapping): MobileGroupScrollMapping {
  return {
    ...mobile,
    translateX: round(mobile.translateX * 1.2),
    translateY: round(mobile.translateY * 1.2),
    scaleFrom: deriveVariantScale(mobile.scaleFrom, 1.08),
    scaleTo: deriveVariantScale(mobile.scaleTo, 1.08),
    speedMultiplier: round(mobile.speedMultiplier * 1.15),
  }
}

function deriveDesktopMapping(mobile: MobileGroupScrollMapping): MobileGroupScrollMapping {
  return {
    ...mobile,
    translateX: round(mobile.translateX * 1.4),
    translateY: round(mobile.translateY * 1.4),
    scaleFrom: deriveVariantScale(mobile.scaleFrom, 1.15),
    scaleTo: deriveVariantScale(mobile.scaleTo, 1.15),
    speedMultiplier: round(mobile.speedMultiplier * 1.3),
  }
}

function resolveDepthScore(asset: { layerOrder: number | null; metadataJson?: unknown }) {
  const metadata = asRecord(asset.metadataJson)

  if (!metadata) {
    return asset.layerOrder ?? 0
  }

  const score =
    toFiniteNumber(metadata.depth) ??
    toFiniteNumber(metadata.depthScore) ??
    toFiniteNumber(metadata.zDepth) ??
    toFiniteNumber(metadata.distanceFromCamera) ??
    toFiniteNumber(metadata.distance)

  return score ?? asset.layerOrder ?? 0
}

function splitIndexIntoGroup(position: number, total: number): GroupKey {
  if (total <= 1) {
    return "midground"
  }

  const ratio = position / Math.max(total - 1, 1)
  if (ratio <= 0.33) {
    return "background"
  }
  if (ratio >= 0.66) {
    return "foreground"
  }
  return "midground"
}

function buildDefaultGrouping(layerAssets: Array<{ layerOrder: number | null; metadataJson?: unknown }>): SceneGroupingConfig | null {
  if (layerAssets.length === 0) {
    return null
  }

  const buckets: Record<GroupKey, number[]> = {
    background: [],
    midground: [],
    foreground: [],
  }

  const rankedLayers = [...layerAssets]
    .map((asset, index) => ({
      layerIndex: asset.layerOrder ?? index,
      depthScore: resolveDepthScore(asset),
    }))
    .sort((left, right) => left.depthScore - right.depthScore)

  rankedLayers.forEach((layer, position) => {
    buckets[splitIndexIntoGroup(position, rankedLayers.length)].push(layer.layerIndex)
  })

  return {
    version: 1,
    groups: GROUP_KEYS.map((groupKey) => ({
      groupKey,
      layerIndexes: buckets[groupKey],
      mobile: GROUP_DEFAULTS[groupKey],
    })),
  }
}

function mergeGroupingWithDefaults(
  grouping: SceneGroupingConfig | null,
  layerAssets: Array<{ layerOrder: number | null; metadataJson?: unknown }>,
): SceneGroupingConfig | null {
  const fallbackGrouping = buildDefaultGrouping(layerAssets)

  if (!grouping) {
    return fallbackGrouping
  }

  const assignedLayerIndexes = new Set(grouping.groups.flatMap((group) => group.layerIndexes))
  const unassignedLayerIndexes = layerAssets
    .map((asset, index) => asset.layerOrder ?? index)
    .filter((layerIndex) => !assignedLayerIndexes.has(layerIndex))

  return {
    version: 1,
    groups: GROUP_KEYS.map((groupKey) => {
      const existingGroup = grouping.groups.find((group) => group.groupKey === groupKey)

      if (existingGroup) {
        return {
          ...existingGroup,
          layerIndexes:
            groupKey === "midground" ? [...existingGroup.layerIndexes, ...unassignedLayerIndexes] : existingGroup.layerIndexes,
        }
      }

      return {
        groupKey,
        layerIndexes: groupKey === "midground" ? unassignedLayerIndexes : [],
        mobile: fallbackGrouping?.groups.find((group) => group.groupKey === groupKey)?.mobile ?? GROUP_DEFAULTS[groupKey],
      }
    }),
  }
}

function buildLayerBehavior(groupKey: GroupKey, layerIndex: number, mobile: MobileGroupScrollMapping, intensityBase: number): MotionLayerBehavior {
  const tablet = deriveTabletMapping(mobile)
  const desktop = deriveDesktopMapping(mobile)

  return {
    layerIndex,
    parallax: round(GROUP_PARALLAX_WEIGHT[groupKey] * intensityBase * mobile.speedMultiplier),
    scale: round(mobile.scaleTo),
    opacity: round(mobile.opacityTo),
    groupKey,
    startProgress: mobile.startProgress,
    endProgress: mobile.endProgress,
    translateX: mobile.translateX,
    translateY: mobile.translateY,
    scaleFrom: mobile.scaleFrom,
    scaleTo: mobile.scaleTo,
    opacityFrom: mobile.opacityFrom,
    opacityTo: mobile.opacityTo,
    speedMultiplier: mobile.speedMultiplier,
    easing: mobile.easing,
    mobile,
    tablet,
    desktop,
  }
}

export const motionService = {
  deriveTabletMapping,

  deriveDesktopMapping,

  buildBlueprint(scene: {
    assets: Array<{ assetType: string; layerOrder: number | null; metadataJson?: unknown }>
    motionPreset?: string | null
    motionIntensity?: string | null
    framingData?: unknown
  }): MotionBlueprint {
    const intensity = intensityFromPreset(scene.motionIntensity ?? scene.motionPreset)
    const layerAssets = scene.assets.filter((asset) => asset.assetType === "layer")
    const denominator = Math.max(layerAssets.length, 1)
    const baseMultiplier = intensity === "low" ? 0.55 : intensity === "high" ? 1.25 : 0.85
    const grouping = mergeGroupingWithDefaults(parseGrouping(scene.framingData), layerAssets)

    const groupedLayerBehaviors = grouping?.groups.flatMap((group) =>
      group.layerIndexes.map((layerIndex) => buildLayerBehavior(group.groupKey, layerIndex, group.mobile, baseMultiplier)),
    )

    return {
      cameraMovement: movementFromPreset(scene.motionPreset),
      intensity,
      layerBehaviors:
        groupedLayerBehaviors && groupedLayerBehaviors.length > 0
          ? groupedLayerBehaviors
          : layerAssets.map((asset, index) => ({
              layerIndex: asset.layerOrder ?? index,
              parallax: round(((index + 1) / denominator) * baseMultiplier),
              scale: round(1 + (index / denominator) * 0.08 * baseMultiplier),
              opacity: round(1 - index * 0.04),
            })),
      transition: {
        overlapMs: DEFAULT_SCENE_OVERLAP_MS,
        easing: intensity === "high" ? "linear" : "ease-out",
      },
      reducedMotion: {
        cameraMovement: "hold",
        multiplier: 0.2,
      },
    }
  },

  async generateForScene(scene: {
    id: string
    projectId: string
    assets: Array<{ assetType: string; layerOrder: number | null; metadataJson?: unknown }>
    motionPreset?: string | null
    motionIntensity?: string | null
    framingData?: unknown
  }, traceId?: string | null) {
    const startedAt = Date.now()
    const blueprint = this.buildBlueprint(scene)

    const updatedScene = await sceneRepository.setMotionBlueprint(scene.id, blueprint as Prisma.InputJsonValue)

    metrics.observe("processing_motion_duration_ms", Date.now() - startedAt)
    logProcessingEvent({
      event: "motion blueprint generated",
      traceId,
      projectId: scene.projectId,
      sceneId: scene.id,
      details: {
        layerCount: blueprint.layerBehaviors.length,
        intensity: blueprint.intensity,
      },
    })

    return updatedScene
  },
}



================================================
FILE: src/modules/motion/types.ts
================================================
import type { EasingKey, GroupKey, MobileGroupScrollMapping } from "@/modules/scenes"

export type MotionDeviceMapping = MobileGroupScrollMapping

export type MotionLayerBehavior = {
  layerIndex: number
  parallax: number
  scale: number
  opacity: number
  groupKey?: GroupKey
  startProgress?: number
  endProgress?: number
  translateX?: number
  translateY?: number
  scaleFrom?: number
  scaleTo?: number
  opacityFrom?: number
  opacityTo?: number
  speedMultiplier?: number
  easing?: EasingKey
  mobile?: MotionDeviceMapping
  tablet?: MotionDeviceMapping
  desktop?: MotionDeviceMapping
}

export type MotionBlueprint = {
  cameraMovement: "drift-up" | "push-in" | "drift-right" | "hold"
  intensity: "low" | "medium" | "high"
  layerBehaviors: MotionLayerBehavior[]
  transition: {
    overlapMs: number
    easing: "ease-out" | "linear"
  }
  reducedMotion: {
    cameraMovement: "hold"
    multiplier: number
  }
}



================================================
FILE: src/modules/playback/index.ts
================================================
export * from "@/modules/playback/service"



================================================
FILE: src/modules/playback/service.ts
================================================
import { Prisma, SceneStatus } from "@prisma/client"

import { DEFAULT_SCENE_DURATION_MS, DEFAULT_SCENE_OVERLAP_MS } from "@/config/constants"
import { AppError } from "@/core/errors/app-error"
import { metrics } from "@/core/observability/metrics"
import { logProcessingEvent } from "@/core/observability/processing-log"
import { featureFlagService } from "@/modules/feature-flags"
import { projectRepository } from "@/modules/projects/repository"
import { sceneRepository } from "@/modules/scenes/repository"

type StitchOptions = {
  reducedMotion?: boolean
  allowFallback?: boolean
  traceId?: string | null
}

function round(value: number, digits = 3) {
  return Number(value.toFixed(digits))
}

function applyReducedMotionToLayerBehavior(layer: Record<string, any>, multiplier: number) {
  const nextLayer: Record<string, unknown> = {
    ...layer,
    parallax: round((layer.parallax ?? 0.2) * multiplier),
  }

  for (const deviceKey of ["mobile", "tablet", "desktop"] as const) {
    const mapping = layer[deviceKey]

    if (!mapping || typeof mapping !== "object") {
      continue
    }

    nextLayer[deviceKey] = {
      ...mapping,
      translateX: round(((mapping.translateX as number | undefined) ?? 0) * multiplier),
      translateY: round(((mapping.translateY as number | undefined) ?? 0) * multiplier),
      scaleFrom: round(1 + ((((mapping.scaleFrom as number | undefined) ?? 1) - 1) * multiplier)),
      scaleTo: round(1 + ((((mapping.scaleTo as number | undefined) ?? 1) - 1) * multiplier)),
      speedMultiplier: round(((mapping.speedMultiplier as number | undefined) ?? 1) * multiplier),
    }
  }

  if (typeof layer.translateX === "number") {
    nextLayer.translateX = round(layer.translateX * multiplier)
  }

  if (typeof layer.translateY === "number") {
    nextLayer.translateY = round(layer.translateY * multiplier)
  }

  if (typeof layer.scaleFrom === "number") {
    nextLayer.scaleFrom = round(1 + (layer.scaleFrom - 1) * multiplier)
  }

  if (typeof layer.scaleTo === "number") {
    nextLayer.scaleTo = round(1 + (layer.scaleTo - 1) * multiplier)
  }

  if (typeof layer.speedMultiplier === "number") {
    nextLayer.speedMultiplier = round(layer.speedMultiplier * multiplier)
  }

  return nextLayer
}

function deriveSceneDuration(scene: { motionIntensity?: string | null }) {
  const value = scene.motionIntensity?.toLowerCase() ?? ""
  if (value.includes("high")) {
    return 2600
  }
  if (value.includes("low")) {
    return 1800
  }
  return DEFAULT_SCENE_DURATION_MS
}

export const playbackService = {
  buildTimeline(
    projectId: string,
    scenes: Array<{
      id: string
      orderIndex: number
      status: SceneStatus
      thumbnailUrl: string | null
      sourceImageUrl: string | null
      motionIntensity: string | null
      motionBlueprintJson: Prisma.JsonValue | null
    }>,
    options: { reducedMotion?: boolean; allowFallback?: boolean },
  ) {
    const reducedMotion = Boolean(options.reducedMotion && featureFlagService.isEnabled("reducedMotionPreview"))
    const allowFallback = options.allowFallback ?? featureFlagService.isEnabled("previewFallbacks")
    const readyScenes = scenes.filter((scene) => scene.status === SceneStatus.ready && scene.motionBlueprintJson)
    const renderableScenes = allowFallback ? readyScenes : scenes

    if (!allowFallback && scenes.some((scene) => scene.status !== SceneStatus.ready || !scene.motionBlueprintJson)) {
      throw new AppError({
        code: "PLAYBACK_NOT_READY",
        message: "All scenes must be ready before stitching without fallback support.",
        statusCode: 409,
      })
    }

    if (renderableScenes.length === 0) {
      throw new AppError({
        code: "NO_RENDERABLE_SCENES",
        message: "No scenes are ready for playback yet.",
        statusCode: 409,
      })
    }

    let cursorMs = 0
    const timelineScenes = renderableScenes.map((scene, index) => {
      const durationMs = deriveSceneDuration(scene)
      const overlapMs = index === 0 ? 0 : DEFAULT_SCENE_OVERLAP_MS
      const startsAtMs = Math.max(cursorMs - overlapMs, 0)
      const blueprint = (scene.motionBlueprintJson ?? {}) as Record<string, any>
      cursorMs = startsAtMs + durationMs

      return {
        sceneId: scene.id,
        orderIndex: scene.orderIndex,
        status: scene.status,
        startsAtMs,
        durationMs,
        overlapMs,
        thumbnailUrl: scene.thumbnailUrl,
        sourceImageUrl: scene.sourceImageUrl,
        cameraMovement: reducedMotion ? "hold" : blueprint.cameraMovement ?? "drift-up",
        intensity: reducedMotion ? "low" : blueprint.intensity ?? "medium",
        layerBehaviors: reducedMotion
          ? Array.isArray(blueprint.layerBehaviors)
            ? blueprint.layerBehaviors.map((layer: any) => applyReducedMotionToLayerBehavior(layer, blueprint.reducedMotion?.multiplier ?? 0.2))
            : []
          : blueprint.layerBehaviors ?? [],
        transition: blueprint.transition ?? { overlapMs: DEFAULT_SCENE_OVERLAP_MS, easing: "ease-out" },
        fallback: scene.status !== SceneStatus.ready,
      }
    })

    return {
      projectId,
      versionedAt: new Date().toISOString(),
      reducedMotion,
      isFallback: readyScenes.length !== scenes.length,
      summary: {
        totalScenes: scenes.length,
        renderableScenes: renderableScenes.length,
        failedScenes: scenes.filter((scene) => scene.status === SceneStatus.failed).length,
        pendingScenes: scenes.filter((scene) => scene.status !== SceneStatus.ready && scene.status !== SceneStatus.failed).length,
        totalDurationMs: cursorMs,
      },
      scenes: timelineScenes,
    }
  },

  async stitchProject(projectId: string, options?: StitchOptions) {
    const startedAt = Date.now()
    const scenes = await sceneRepository.findByProjectId(projectId)

    if (scenes.length === 0) {
      throw new AppError({
        code: "NO_SCENES_AVAILABLE",
        message: "Project does not have scenes to stitch.",
        statusCode: 409,
      })
    }

    const timeline = this.buildTimeline(projectId, scenes, {
      reducedMotion: options?.reducedMotion,
      allowFallback: options?.allowFallback,
    })

    const versionAgg = await projectRepository.nextPlaybackPlanVersion(projectId)
    const playbackPlan = await projectRepository.createPlaybackPlan({
      projectId,
      version: (versionAgg._max.version ?? 0) + 1,
      timelineJson: timeline as Prisma.InputJsonValue,
      isReducedMotion: timeline.reducedMotion,
      isFallback: timeline.isFallback,
    })

    metrics.observe("processing_playback_duration_ms", Date.now() - startedAt)
    logProcessingEvent({
      event: "playback plan stitched",
      traceId: options?.traceId,
      projectId,
      details: {
        playbackPlanId: playbackPlan.id,
        version: playbackPlan.version,
        reducedMotion: timeline.reducedMotion,
        isFallback: timeline.isFallback,
        renderableScenes: timeline.summary.renderableScenes,
      },
    })

    return playbackPlan
  },

  async latest(projectId: string, options?: { reducedMotion?: boolean }) {
    const plan = await projectRepository.latestPlaybackPlan(projectId, {
      isReducedMotion: options?.reducedMotion,
    })

    if (plan) {
      return plan
    }

    return this.stitchProject(projectId, {
      reducedMotion: options?.reducedMotion,
      allowFallback: true,
    })
  },

  async previewStatus(projectId: string) {
    const project = await projectRepository.findById(projectId)

    if (!project) {
      throw new AppError({
        code: "PROJECT_NOT_FOUND",
        message: "Project was not found.",
        statusCode: 404,
      })
    }

    const latestPlayback = await projectRepository.latestPlaybackPlan(projectId)
    const latestReducedPlayback = await projectRepository.latestPlaybackPlan(projectId, { isReducedMotion: true })

    return {
      projectId: project.id,
      title: project.title,
      status: project.status,
      playback: {
        latestVersion: latestPlayback?.version ?? null,
        reducedMotionVersion: latestReducedPlayback?.version ?? null,
        isFallback: latestPlayback?.isFallback ?? null,
      },
      scenes: project.scenes.map((scene) => ({
        sceneId: scene.id,
        orderIndex: scene.orderIndex,
        status: scene.status,
        hasMotionBlueprint: Boolean(scene.motionBlueprintJson),
        latestJobStatus: scene.processingJobs[0]?.status ?? null,
      })),
    }
  },
}



================================================
FILE: src/modules/processing/index.ts
================================================
export * from "@/modules/processing/service"



================================================
FILE: src/modules/processing/service.ts
================================================
import { AppError } from "@/core/errors/app-error"
import { logProcessingEvent } from "@/core/observability/processing-log"
import { triggerDevJobRunner } from "@/infrastructure/jobs/trigger-dev"
import { featureFlagService } from "@/modules/feature-flags"
import { sceneService } from "@/modules/scenes"

export const processingService = {
  async enqueueSceneDecomposition(sceneId: string, correlationId: string, options?: { reason?: string; resetGeneration?: boolean }) {
    if (!featureFlagService.allowsProcessing(sceneId)) {
      throw new AppError({
        code: "PROCESSING_CANARY_DISABLED",
        message: "Scene processing is not enabled for this scene yet.",
        statusCode: 503,
      })
    }

    const scene = await sceneService.getById(sceneId)
    const job = await sceneService.enqueueDecomposition(sceneId, {
      correlationId,
      reason: options?.reason,
      resetGeneration: options?.resetGeneration,
    })

    const latestScene = await sceneService.getById(sceneId)

    if (!latestScene.project) {
      throw new AppError({
        code: "PROJECT_NOT_FOUND",
        message: "Scene project is missing.",
        statusCode: 404,
      })
    }

    logProcessingEvent({
      event: "scene decomposition enqueued",
      traceId: correlationId,
      projectId: latestScene.project.id,
      sceneId: latestScene.id,
      jobId: job.id,
      details: {
        reason: options?.reason ?? null,
        resetGeneration: Boolean(options?.resetGeneration),
      },
    })

    await triggerDevJobRunner.dispatchDecomposition({
      scene: {
        id: latestScene.id,
        generationVersion: latestScene.generationVersion,
        sourceImageUrl: latestScene.sourceImageUrl,
        expiresAt: latestScene.expiresAt,
        project: { id: latestScene.project.id },
        assets: latestScene.assets.map((asset) => ({
          assetType: asset.assetType,
          metadataJson: asset.metadataJson,
        })),
      },
      job: {
        id: job.id,
        attemptCount: job.attemptCount,
        correlationId: job.correlationId,
      },
    })

    return {
      job,
      scene,
    }
  },
}



================================================
FILE: src/modules/projects/index.ts
================================================
export * from "@/modules/projects/service"
export * from "@/modules/projects/types"
export * from "@/modules/projects/validator"



================================================
FILE: src/modules/projects/repository.ts
================================================
import { Prisma } from "@prisma/client"

import { prisma } from "@/infrastructure/db/prisma"

export const projectRepository = {
  createAuthenticatedProject(data: {
    title: string
    userId: string
    globalContext?: string | null
    stylePreset?: string | null
  }) {
    return prisma.project.create({
      data: {
        title: data.title,
        ownerId: data.userId,
        globalContext: data.globalContext,
        stylePreset: data.stylePreset,
      },
      include: {
        scenes: true,
      },
    })
  },

  createGuestProject(data: {
    title: string
    guestSessionId: string
    expiresAt: Date
    globalContext?: string | null
    stylePreset?: string | null
  }) {
    return prisma.project.create({
      data: {
        title: data.title,
        guestSessionId: data.guestSessionId,
        expiresAt: data.expiresAt,
        globalContext: data.globalContext,
        stylePreset: data.stylePreset,
      },
      include: {
        scenes: true,
      },
    })
  },

  findById(id: string) {
    return prisma.project.findUnique({
      where: { id },
      include: {
        scenes: {
          orderBy: { orderIndex: "asc" },
          include: {
            assets: {
              orderBy: [{ layerOrder: "asc" }, { createdAt: "asc" }],
            },
            processingJobs: {
              orderBy: { createdAt: "desc" },
            },
          },
        },
        playbackPlans: {
          orderBy: { version: "desc" },
          take: 1,
        },
      },
    })
  },

  findAccessibleProjects(actor: { kind: "authenticated"; userId: string } | { kind: "guest"; guestSessionId: string }) {
    return prisma.project.findMany({
      where:
        actor.kind === "authenticated"
          ? { ownerId: actor.userId }
          : { guestSessionId: actor.guestSessionId },
      include: {
        scenes: {
          orderBy: { orderIndex: "asc" },
        },
      },
      orderBy: { updatedAt: "desc" },
    })
  },

  countGuestProjects(guestSessionId: string) {
    return prisma.project.count({
      where: {
        guestSessionId,
        ownerId: null,
      },
    })
  },

  update(id: string, data: { title?: string; globalContext?: string | null; stylePreset?: string | null }) {
    return prisma.project.update({
      where: { id },
      data,
      include: {
        scenes: {
          orderBy: { orderIndex: "asc" },
        },
      },
    })
  },

  async delete(id: string) {
    await prisma.project.delete({
      where: { id },
    })
  },

  claim(id: string, data: { userId: string; guestSessionId: string }) {
    return prisma.$transaction(async (tx) => {
      const claimedAt = new Date()

      await tx.guestSession.update({
        where: { id: data.guestSessionId },
        data: {
          claimedAt,
          claimedByUserId: data.userId,
        },
      })

      return tx.project.update({
        where: { id },
        data: {
          ownerId: data.userId,
          guestSessionId: null,
          claimedAt,
          claimedByUserId: data.userId,
          expiresAt: null,
        },
        include: {
          scenes: {
            orderBy: { orderIndex: "asc" },
          },
        },
      })
    })
  },

  latestPlaybackPlan(projectId: string, options?: { isReducedMotion?: boolean; onlyValid?: boolean }) {
    return prisma.playbackPlan.findFirst({
      where: {
        projectId,
        ...(options?.isReducedMotion === undefined ? {} : { isReducedMotion: options.isReducedMotion }),
      },
      orderBy: [{ version: "desc" }, { createdAt: "desc" }],
    })
  },

  nextPlaybackPlanVersion(projectId: string) {
    return prisma.playbackPlan.aggregate({
      where: { projectId },
      _max: { version: true },
    })
  },

  createPlaybackPlan(data: {
    projectId: string
    version: number
    timelineJson: Prisma.InputJsonValue
    isReducedMotion?: boolean
    isFallback?: boolean
  }) {
    return prisma.playbackPlan.create({
      data: {
        projectId: data.projectId,
        version: data.version,
        timelineJson: data.timelineJson,
        isReducedMotion: data.isReducedMotion ?? false,
        isFallback: data.isFallback ?? false,
      },
    })
  },

  deleteExpiredGuestProjects(now: Date) {
    return prisma.project.deleteMany({
      where: {
        ownerId: null,
        guestSessionId: { not: null },
        claimedAt: null,
        expiresAt: { lt: now },
      },
    })
  },

  deleteExpiredGuestSessions(now: Date) {
    return prisma.guestSession.deleteMany({
      where: {
        expiresAt: { lt: now },
        claimedAt: null,
        projects: {
          none: {},
        },
      },
    })
  },
}



================================================
FILE: src/modules/projects/service.ts
================================================
import { AppError } from "@/core/errors/app-error"
import { getEnv } from "@/config/env"
import { DEFAULT_PROJECT_OUTPUT_FORMAT } from "@/config/constants"
import { projectRepository } from "@/modules/projects/repository"
import type { CreateProjectInput, UpdateProjectInput } from "@/modules/projects/types"

export const projectService = {
  async create(input: CreateProjectInput) {
    if (input.actor.kind === "authenticated") {
      const project = await projectRepository.createAuthenticatedProject({
        title: input.title,
        userId: input.actor.userId,
        globalContext: input.globalContext,
        stylePreset: input.stylePreset,
      })

      return {
        ...project,
        outputFormat: DEFAULT_PROJECT_OUTPUT_FORMAT,
      }
    }

    if (!input.actor.guestSessionId) {
      throw new AppError({
        code: "GUEST_SESSION_REQUIRED",
        message: "A guest session is required to create a guest project.",
        statusCode: 401,
      })
    }

    const env = getEnv()
    const guestProjectCount = await projectRepository.countGuestProjects(input.actor.guestSessionId)

    if (guestProjectCount >= env.GUEST_MAX_PROJECTS) {
      throw new AppError({
        code: "GUEST_PROJECT_QUOTA_EXCEEDED",
        message: `Guest users may only keep ${env.GUEST_MAX_PROJECTS} active projects.`,
        statusCode: 429,
      })
    }

    const project = await projectRepository.createGuestProject({
      title: input.title,
      guestSessionId: input.actor.guestSessionId,
      expiresAt: input.actor.expiresAt,
      globalContext: input.globalContext,
      stylePreset: input.stylePreset,
    })

    return {
      ...project,
      outputFormat: DEFAULT_PROJECT_OUTPUT_FORMAT,
    }
  },

  async list(actor: { kind: "authenticated"; userId: string } | { kind: "guest"; guestSessionId: string }) {
    return projectRepository.findAccessibleProjects(actor)
  },

  async getById(projectId: string) {
    const project = await projectRepository.findById(projectId)

    if (!project) {
      throw new AppError({
        code: "PROJECT_NOT_FOUND",
        message: "Project was not found.",
        statusCode: 404,
      })
    }

    return project
  },

  async update(projectId: string, input: UpdateProjectInput) {
    return projectRepository.update(projectId, input)
  },

  async remove(projectId: string) {
    await projectRepository.delete(projectId)
  },

  async claim(projectId: string, input: { userId: string; guestSessionId: string }) {
    const project = await this.getById(projectId)

    if (!project.guestSessionId || project.guestSessionId !== input.guestSessionId) {
      throw new AppError({
        code: "CLAIM_NOT_ALLOWED",
        message: "Project does not belong to the current guest session.",
        statusCode: 403,
      })
    }

    if (project.claimedAt || project.ownerId) {
      throw new AppError({
        code: "PROJECT_ALREADY_CLAIMED",
        message: "Project has already been claimed.",
        statusCode: 409,
      })
    }

    if (project.expiresAt && project.expiresAt.getTime() <= Date.now()) {
      throw new AppError({
        code: "PROJECT_EXPIRED",
        message: "Expired guest projects cannot be claimed.",
        statusCode: 410,
      })
    }

    return projectRepository.claim(projectId, input)
  },
}



================================================
FILE: src/modules/projects/types.ts
================================================
export type CreateProjectInput = {
  title: string
  globalContext?: string | null
  stylePreset?: string | null
  actor:
    | { kind: "authenticated"; userId: string }
    | { kind: "guest"; guestSessionId: string; expiresAt: Date }
}

export type UpdateProjectInput = {
  title?: string
  globalContext?: string | null
  stylePreset?: string | null
}



================================================
FILE: src/modules/projects/validator.ts
================================================
import { z } from "zod"

export const createProjectInputSchema = z.object({
  title: z.string().trim().min(1).max(120),
  globalContext: z.string().trim().max(4000).nullish(),
  stylePreset: z.string().trim().max(120).nullish(),
})

export const updateProjectInputSchema = z.object({
  title: z.string().trim().min(1).max(120).optional(),
  globalContext: z.string().trim().max(4000).nullable().optional(),
  stylePreset: z.string().trim().max(120).nullable().optional(),
})

export const reorderScenesInputSchema = z.object({
  sceneIds: z.array(z.string().uuid()).min(1),
})

export const claimProjectInputSchema = z.object({
  guestSessionId: z.string().uuid().optional(),
})



================================================
FILE: src/modules/scenes/index.ts
================================================
export * from "@/modules/scenes/service"
export * from "@/modules/scenes/types"
export * from "@/modules/scenes/validator"



================================================
FILE: src/modules/scenes/repository.ts
================================================
import { AssetType, JobStatus, JobType, Prisma, SceneStatus } from "@prisma/client"

import { prisma } from "@/infrastructure/db/prisma"

export const sceneRepository = {
  findById(id: string) {
    return prisma.scene.findUnique({
      where: { id },
      include: {
        project: true,
        assets: {
          orderBy: [{ layerOrder: "asc" }, { createdAt: "asc" }],
        },
        processingJobs: {
          orderBy: { createdAt: "desc" },
        },
      },
    })
  },

  async nextOrderIndex(projectId: string) {
    const result = await prisma.scene.aggregate({
      where: { projectId },
      _max: { orderIndex: true },
    })

    return (result._max.orderIndex ?? -1) + 1
  },

  createManyWithAssets(items: Array<{
    id: string
    projectId: string
    orderIndex: number
    generationVersion?: number
    sourceImageUrl: string
    thumbnailUrl: string
    contextText?: string | null
    motionPreset?: string | null
    motionIntensity?: string | null
    expiresAt?: Date | null
    originalAsset: { assetUrl: string; width?: number; height?: number; metadataJson?: Prisma.InputJsonValue }
    thumbnailAsset: { assetUrl: string; width?: number; height?: number; metadataJson?: Prisma.InputJsonValue }
  }>) {
    return prisma.$transaction(
      items.map((item) =>
        prisma.scene.create({
          data: {
            id: item.id,
            projectId: item.projectId,
            orderIndex: item.orderIndex,
            generationVersion: item.generationVersion ?? 1,
            sourceImageUrl: item.sourceImageUrl,
            thumbnailUrl: item.thumbnailUrl,
            contextText: item.contextText,
            motionPreset: item.motionPreset,
            motionIntensity: item.motionIntensity,
            expiresAt: item.expiresAt,
            assets: {
              create: [
                {
                  assetType: AssetType.original,
                  assetUrl: item.originalAsset.assetUrl,
                  width: item.originalAsset.width,
                  height: item.originalAsset.height,
                  metadataJson: item.originalAsset.metadataJson,
                  expiresAt: item.expiresAt,
                },
                {
                  assetType: AssetType.thumbnail,
                  assetUrl: item.thumbnailAsset.assetUrl,
                  width: item.thumbnailAsset.width,
                  height: item.thumbnailAsset.height,
                  metadataJson: item.thumbnailAsset.metadataJson,
                  expiresAt: item.expiresAt,
                },
              ],
            },
          },
          include: {
            assets: true,
          },
        }),
      ),
    )
  },

  update(id: string, data: {
    contextText?: string | null
    motionPreset?: string | null
    motionIntensity?: string | null
    grouping?: Prisma.InputJsonValue | null
  }) {
    return prisma.scene.update({
      where: { id },
      data: {
        contextText: data.contextText,
        motionPreset: data.motionPreset,
        motionIntensity: data.motionIntensity,
        framingData: data.grouping === null ? Prisma.JsonNull : data.grouping,
      },
      include: {
        project: true,
        assets: {
          orderBy: [{ layerOrder: "asc" }, { createdAt: "asc" }],
        },
        processingJobs: {
          orderBy: { createdAt: "desc" },
        },
      },
    })
  },

  setMotionBlueprint(sceneId: string, blueprint: Prisma.InputJsonValue) {
    return prisma.scene.update({
      where: { id: sceneId },
      data: {
        motionBlueprintJson: blueprint,
      },
      include: {
        project: true,
        assets: {
          orderBy: [{ layerOrder: "asc" }, { createdAt: "asc" }],
        },
        processingJobs: {
          orderBy: { createdAt: "desc" },
        },
      },
    })
  },

  findByProjectId(projectId: string) {
    return prisma.scene.findMany({
      where: { projectId },
      include: {
        project: true,
        assets: {
          orderBy: [{ layerOrder: "asc" }, { createdAt: "asc" }],
        },
        processingJobs: {
          orderBy: { createdAt: "desc" },
        },
      },
      orderBy: { orderIndex: "asc" },
    })
  },

  async reorder(projectId: string, sceneIds: string[]) {
    return prisma.$transaction(
      sceneIds.map((sceneId, index) =>
        prisma.scene.updateMany({
          where: { id: sceneId, projectId },
          data: { orderIndex: index },
        }),
      ),
    )
  },

  delete(id: string) {
    return prisma.scene.delete({
      where: { id },
    })
  },

  findActiveDecompositionJob(sceneId: string) {
    return prisma.processingJob.findFirst({
      where: {
        sceneId,
        jobType: JobType.decomposition,
        status: { in: [JobStatus.queued, JobStatus.processing] },
      },
      orderBy: { createdAt: "desc" },
    })
  },

  countByProjectId(projectId: string) {
    return prisma.scene.count({
      where: { projectId },
    })
  },

  createDecompositionJob(sceneId: string, data: { correlationId: string; metadataJson?: Prisma.InputJsonValue }) {
    return prisma.processingJob.create({
      data: {
        sceneId,
        jobType: JobType.decomposition,
        status: JobStatus.queued,
        correlationId: data.correlationId,
        metadataJson: data.metadataJson,
      },
    })
  },

  findTimedOutJobs(timeoutBefore: Date) {
    return prisma.processingJob.findMany({
      where: {
        status: { in: [JobStatus.queued, JobStatus.processing] },
        OR: [
          { startedAt: { lt: timeoutBefore } },
          { startedAt: null, createdAt: { lt: timeoutBefore } },
        ],
      },
      include: {
        scene: {
          include: {
            project: true,
          },
        },
      },
      orderBy: { createdAt: "asc" },
    })
  },

  updateJob(jobId: string, data: {
    status?: JobStatus
    providerJobId?: string | null
    attemptCount?: number
    errorMessage?: string | null
    startedAt?: Date | null
    completedAt?: Date | null
    metadataJson?: Prisma.InputJsonValue
  }) {
    return prisma.processingJob.update({
      where: { id: jobId },
      data,
    })
  },

  updateSceneStatus(sceneId: string, data: {
    status?: SceneStatus
    generationVersion?: number
  }) {
    return prisma.scene.update({
      where: { id: sceneId },
      data,
    })
  },

  replaceGeneratedAssets(sceneId: string, data: {
    expiresAt?: Date | null
    layerAssets: Array<{ assetUrl: string; width?: number; height?: number; layerOrder: number; metadataJson?: Prisma.InputJsonValue }>
    compositeAsset: { assetUrl: string; width?: number; height?: number; metadataJson?: Prisma.InputJsonValue }
    manifestAsset: { assetUrl: string; metadataJson?: Prisma.InputJsonValue }
  }) {
    return prisma.$transaction(async (tx) => {
      await tx.sceneAsset.deleteMany({
        where: {
          sceneId,
          assetType: { in: [AssetType.layer, AssetType.composite, AssetType.manifest] },
        },
      })

      await tx.sceneAsset.createMany({
        data: [
          ...data.layerAssets.map((asset) => ({
            sceneId,
            assetType: AssetType.layer,
            assetUrl: asset.assetUrl,
            width: asset.width,
            height: asset.height,
            layerOrder: asset.layerOrder,
            metadataJson: asset.metadataJson,
            expiresAt: data.expiresAt,
          })),
          {
            sceneId,
            assetType: AssetType.composite,
            assetUrl: data.compositeAsset.assetUrl,
            width: data.compositeAsset.width,
            height: data.compositeAsset.height,
            metadataJson: data.compositeAsset.metadataJson,
            expiresAt: data.expiresAt,
          },
          {
            sceneId,
            assetType: AssetType.manifest,
            assetUrl: data.manifestAsset.assetUrl,
            metadataJson: data.manifestAsset.metadataJson,
            expiresAt: data.expiresAt,
          },
        ],
      })

      return tx.scene.findUnique({
        where: { id: sceneId },
        include: {
          assets: {
            orderBy: [{ layerOrder: "asc" }, { createdAt: "asc" }],
          },
          processingJobs: {
            orderBy: { createdAt: "desc" },
          },
          project: true,
        },
      })
    })
  },
}



================================================
FILE: src/modules/scenes/service.ts
================================================
import { JobStatus, Prisma, SceneStatus } from "@prisma/client"

import { getEnv } from "@/config/env"
import { AppError } from "@/core/errors/app-error"
import { sceneRepository } from "@/modules/scenes/repository"
import type { UpdateSceneInput } from "@/modules/scenes/types"

export const sceneService = {
  async getById(sceneId: string) {
    const scene = await sceneRepository.findById(sceneId)

    if (!scene) {
      throw new AppError({
        code: "SCENE_NOT_FOUND",
        message: "Scene was not found.",
        statusCode: 404,
      })
    }

    return scene
  },

  async nextOrderIndex(projectId: string) {
    return sceneRepository.nextOrderIndex(projectId)
  },

  async createFromUploads(items: Array<{
    id: string
    projectId: string
    orderIndex: number
    generationVersion?: number
    sourceImageUrl: string
    thumbnailUrl: string
    contextText?: string | null
    motionPreset?: string | null
    motionIntensity?: string | null
    expiresAt?: Date | null
    originalAsset: { assetUrl: string; width?: number; height?: number; metadataJson?: Prisma.InputJsonValue }
    thumbnailAsset: { assetUrl: string; width?: number; height?: number; metadataJson?: Prisma.InputJsonValue }
  }>) {
    if (items.length === 0) {
      return []
    }

    const env = getEnv()
    const projectId = items[0]?.projectId
    const existingCount = await sceneRepository.countByProjectId(projectId)

    if (existingCount + items.length > env.GUEST_MAX_SCENES_PER_PROJECT) {
      throw new AppError({
        code: "SCENE_QUOTA_EXCEEDED",
        message: `Projects may contain up to ${env.GUEST_MAX_SCENES_PER_PROJECT} scenes in MVP.`,
        statusCode: 400,
      })
    }

    return sceneRepository.createManyWithAssets(items)
  },

  async update(sceneId: string, input: UpdateSceneInput) {
    return sceneRepository.update(sceneId, {
      contextText: input.contextText,
      motionPreset: input.motionPreset,
      motionIntensity: input.motionIntensity,
      grouping: input.grouping,
    })
  },

  async reorder(projectId: string, sceneIds: string[]) {
    return sceneRepository.reorder(projectId, sceneIds)
  },

  async remove(sceneId: string) {
    await sceneRepository.delete(sceneId)
  },

  async enqueueDecomposition(sceneId: string, input: { correlationId: string; reason?: string; resetGeneration?: boolean }) {
    const scene = await this.getById(sceneId)
    const activeJob = await sceneRepository.findActiveDecompositionJob(sceneId)

    if (activeJob) {
      throw new AppError({
        code: "DECOMPOSITION_ALREADY_ACTIVE",
        message: "A decomposition job is already active for this scene.",
        statusCode: 409,
      })
    }

    if (input.resetGeneration) {
      await sceneRepository.updateSceneStatus(sceneId, {
        generationVersion: scene.generationVersion + 1,
        status: SceneStatus.queued,
      })
    } else {
      await sceneRepository.updateSceneStatus(sceneId, {
        status: SceneStatus.queued,
      })
    }

    return sceneRepository.createDecompositionJob(sceneId, {
      correlationId: input.correlationId,
      metadataJson: {
        reason: input.reason ?? null,
      },
    })
  },

  async markProcessing(jobId: string, sceneId: string, attemptCount: number, providerJobId?: string | null) {
    await sceneRepository.updateSceneStatus(sceneId, {
      status: SceneStatus.processing,
    })

    await sceneRepository.updateJob(jobId, {
      status: JobStatus.processing,
      attemptCount,
      providerJobId,
      startedAt: new Date(),
      errorMessage: null,
    })
  },

  async markReady(jobId: string, sceneId: string) {
    await sceneRepository.updateSceneStatus(sceneId, {
      status: SceneStatus.ready,
    })

    await sceneRepository.updateJob(jobId, {
      status: JobStatus.ready,
      completedAt: new Date(),
      errorMessage: null,
    })
  },

  async markFailed(jobId: string, sceneId: string, message: string, attemptCount: number) {
    await sceneRepository.updateSceneStatus(sceneId, {
      status: SceneStatus.failed,
    })

    await sceneRepository.updateJob(jobId, {
      status: JobStatus.failed,
      completedAt: new Date(),
      errorMessage: message,
      attemptCount,
    })
  },
}



================================================
FILE: src/modules/scenes/types.ts
================================================
export type GroupKey = "background" | "midground" | "foreground"

export type EasingKey = "linear" | "ease-out" | "ease-in-out"

export type MobileGroupScrollMapping = {
  startProgress: number
  endProgress: number
  translateX: number
  translateY: number
  scaleFrom: number
  scaleTo: number
  opacityFrom: number
  opacityTo: number
  speedMultiplier: number
  easing: EasingKey
}

export type SceneGroupConfig = {
  groupKey: GroupKey
  layerIndexes: number[]
  mobile: MobileGroupScrollMapping
}

export type SceneGroupingConfig = {
  version: 1
  groups: SceneGroupConfig[]
}

export type UpdateSceneInput = {
  contextText?: string | null
  motionPreset?: string | null
  motionIntensity?: string | null
  grouping?: SceneGroupingConfig | null
}

export type FinalizeUploadSceneInput = {
  uploadToken: string
  originalFilename: string
  mimeType: string
  sizeBytes: number
  width?: number
  height?: number
  contextText?: string | null
  motionPreset?: string | null
  motionIntensity?: string | null
}



================================================
FILE: src/modules/scenes/validator.ts
================================================
import { z } from "zod"

const GROUP_KEYS = ["background", "midground", "foreground"] as const
const EASING_KEYS = ["linear", "ease-out", "ease-in-out"] as const

const boundedNumber = (min: number, max: number) => z.number().finite().min(min).max(max)

const mobileGroupScrollMappingSchema = z.object({
  startProgress: boundedNumber(0, 1),
  endProgress: boundedNumber(0, 1),
  translateX: boundedNumber(-1000, 1000),
  translateY: boundedNumber(-1000, 1000),
  scaleFrom: boundedNumber(0.1, 3),
  scaleTo: boundedNumber(0.1, 3),
  opacityFrom: boundedNumber(0, 1),
  opacityTo: boundedNumber(0, 1),
  speedMultiplier: boundedNumber(0, 5),
  easing: z.enum(EASING_KEYS),
}).refine((value) => value.startProgress <= value.endProgress, {
  message: "startProgress must be less than or equal to endProgress",
  path: ["endProgress"],
})

const sceneGroupConfigSchema = z.object({
  groupKey: z.enum(GROUP_KEYS),
  layerIndexes: z.array(z.number().int().min(0)).max(100),
  mobile: mobileGroupScrollMappingSchema,
})

const sceneGroupingConfigSchema = z.object({
  version: z.literal(1),
  groups: z.array(sceneGroupConfigSchema).max(3),
}).superRefine((value, ctx) => {
  const seenGroups = new Set<string>()
  const seenLayerIndexes = new Map<number, number>()

  value.groups.forEach((group, groupIndex) => {
    if (seenGroups.has(group.groupKey)) {
      ctx.addIssue({
        code: z.ZodIssueCode.custom,
        message: `Duplicate groupKey: ${group.groupKey}`,
        path: ["groups", groupIndex, "groupKey"],
      })
    }

    seenGroups.add(group.groupKey)

    group.layerIndexes.forEach((layerIndex, layerIndexPosition) => {
      if (seenLayerIndexes.has(layerIndex)) {
        ctx.addIssue({
          code: z.ZodIssueCode.custom,
          message: `Layer ${layerIndex} is assigned to multiple groups`,
          path: ["groups", groupIndex, "layerIndexes", layerIndexPosition],
        })
        return
      }

      seenLayerIndexes.set(layerIndex, groupIndex)
    })
  })
})

export const updateSceneInputSchema = z.object({
  contextText: z.string().trim().max(4000).nullable().optional(),
  motionPreset: z.string().trim().max(120).nullable().optional(),
  motionIntensity: z.string().trim().max(120).nullable().optional(),
  grouping: sceneGroupingConfigSchema.nullable().optional(),
})

export const finalizeUploadsInputSchema = z.object({
  uploads: z.array(
    z.object({
      uploadToken: z.string().min(1),
      originalFilename: z.string().trim().min(1).max(255),
      mimeType: z.string().trim().min(1),
      sizeBytes: z.number().int().positive(),
      width: z.number().int().positive().optional(),
      height: z.number().int().positive().optional(),
      contextText: z.string().trim().max(4000).nullish(),
      motionPreset: z.string().trim().max(120).nullish(),
      motionIntensity: z.string().trim().max(120).nullish(),
    }),
  ).min(1),
})

export const sceneReprocessInputSchema = z.object({
  reason: z.string().trim().max(255).optional(),
})



================================================
FILE: src/modules/uploads/index.ts
================================================
export * from "@/modules/uploads/service"
export * from "@/modules/uploads/types"
export * from "@/modules/uploads/validator"



================================================
FILE: src/modules/uploads/service.ts
================================================
import { createHmac, timingSafeEqual } from "node:crypto"

import { getEnv } from "@/config/env"
import { AppError } from "@/core/errors/app-error"
import { UPLOAD_BASE_PATH } from "@/config/constants"
import type { UploadCandidate, UploadContract } from "@/modules/uploads/types"

type UploadTokenPayload = {
  projectId: string
  filename: string
  mimeType: string
  sizeBytes: number
  storageKey: string
  expiresAt: string
}

function toBase64Url(value: string) {
  return Buffer.from(value, "utf8").toString("base64url")
}

function fromBase64Url(value: string) {
  return Buffer.from(value, "base64url").toString("utf8")
}

function sign(payload: string) {
  const env = getEnv()
  return createHmac("sha256", env.INTERNAL_UPLOAD_TOKEN_SECRET).update(payload).digest("base64url")
}

export const uploadService = {
  validateFiles(files: UploadCandidate[]) {
    const env = getEnv()

    if (files.length > env.UPLOAD_MAX_FILES) {
      throw new AppError({
        code: "UPLOAD_LIMIT_EXCEEDED",
        message: `A maximum of ${env.UPLOAD_MAX_FILES} files may be uploaded at once.`,
        statusCode: 400,
      })
    }

    for (const file of files) {
      if (!env.UPLOAD_ALLOWED_MIME_TYPES.includes(file.mimeType)) {
        throw new AppError({
          code: "UNSUPPORTED_FILE_TYPE",
          message: `${file.filename} uses an unsupported file type.`,
          statusCode: 400,
        })
      }

      if (file.sizeBytes > env.UPLOAD_MAX_FILE_SIZE_BYTES) {
        throw new AppError({
          code: "FILE_TOO_LARGE",
          message: `${file.filename} exceeds the upload size limit.`,
          statusCode: 400,
        })
      }
    }
  },

  createUploadContracts(projectId: string, files: UploadCandidate[]): UploadContract[] {
    this.validateFiles(files)

    return files.map((file, index) => {
      const expiresAt = new Date(Date.now() + 15 * 60 * 1000)
      const safeFilename = file.filename.replace(/[^a-zA-Z0-9._-]/g, "-").toLowerCase()
      const storageKey = `${UPLOAD_BASE_PATH}/${projectId}/incoming/${Date.now()}-${index}-${safeFilename}`

      const payload: UploadTokenPayload = {
        projectId,
        filename: file.filename,
        mimeType: file.mimeType,
        sizeBytes: file.sizeBytes,
        storageKey,
        expiresAt: expiresAt.toISOString(),
      }

      const serializedPayload = JSON.stringify(payload)
      const encodedPayload = toBase64Url(serializedPayload)
      const signature = sign(encodedPayload)

      return {
        uploadToken: `${encodedPayload}.${signature}`,
        uploadUrl: `/api/v1/uploads/${encodedPayload}.${signature}`,
        storageKey,
        expiresAt: payload.expiresAt,
        mimeType: file.mimeType,
        sizeBytes: file.sizeBytes,
      }
    })
  },

  verifyUploadToken(uploadToken: string) {
    const [encodedPayload, providedSignature] = uploadToken.split(".")

    if (!encodedPayload || !providedSignature) {
      throw new AppError({
        code: "INVALID_UPLOAD_TOKEN",
        message: "Upload token is malformed.",
        statusCode: 400,
      })
    }

    const expectedSignature = sign(encodedPayload)

    if (providedSignature.length !== expectedSignature.length) {
      throw new AppError({
        code: "INVALID_UPLOAD_TOKEN",
        message: "Upload token signature is invalid.",
        statusCode: 400,
      })
    }

    if (!timingSafeEqual(Buffer.from(providedSignature), Buffer.from(expectedSignature))) {
      throw new AppError({
        code: "INVALID_UPLOAD_TOKEN",
        message: "Upload token signature is invalid.",
        statusCode: 400,
      })
    }

    const payload = JSON.parse(fromBase64Url(encodedPayload)) as UploadTokenPayload

    if (new Date(payload.expiresAt).getTime() <= Date.now()) {
      throw new AppError({
        code: "UPLOAD_TOKEN_EXPIRED",
        message: "Upload token has expired.",
        statusCode: 410,
      })
    }

    return payload
  },
}



================================================
FILE: src/modules/uploads/types.ts
================================================
export type UploadCandidate = {
  filename: string
  mimeType: string
  sizeBytes: number
}

export type UploadContract = {
  uploadToken: string
  uploadUrl: string
  storageKey: string
  expiresAt: string
  mimeType: string
  sizeBytes: number
}

export type FinalizedUpload = {
  projectId: string
  storageKey: string
  filename: string
  mimeType: string
  sizeBytes: number
  expiresAt?: string | null
}



================================================
FILE: src/modules/uploads/validator.ts
================================================
import { z } from "zod"

export const initiateUploadsInputSchema = z.object({
  files: z.array(
    z.object({
      filename: z.string().trim().min(1).max(255),
      mimeType: z.string().trim().min(1),
      sizeBytes: z.number().int().positive(),
    }),
  ).min(1),
})



================================================
FILE: src/types/next-auth.d.ts
================================================
import { DefaultSession } from "next-auth"

declare module "next-auth" {
  interface Session {
    user: DefaultSession["user"] & {
      id: string
      authProvider?: string
    }
  }

  interface User {
    id: string
    authProvider?: string
  }
}

declare module "next-auth/jwt" {
  interface JWT {
    authProvider?: string
  }
}



================================================
FILE: tests/unit/core/errors/error-response.test.ts
================================================
import { Prisma } from "@prisma/client"
import { describe, expect, it } from "vitest"
import { ZodError } from "zod"

import { AppError } from "@/core/errors/app-error"
import { toErrorResponse } from "@/core/errors/error-response"

const context = {
  correlationId: "test-correlation-id",
  path: "/api/test",
  method: "POST",
} as const

describe("toErrorResponse", () => {
  it("maps prisma initialization failures to a database unavailable response", async () => {
    const error = new Prisma.PrismaClientInitializationError("db down", "test")

    const response = toErrorResponse(error, context)
    const payload = await response.json()

    expect(response.status).toBe(503)
    expect(payload).toEqual({
      error: {
        code: "DATABASE_UNAVAILABLE",
        message: "The database is unavailable right now.",
        details: null,
      },
      meta: {
        correlationId: "test-correlation-id",
      },
    })
  })

  it("preserves app errors", async () => {
    const response = toErrorResponse(
      new AppError({
        code: "TEST_ERROR",
        message: "Known issue",
        statusCode: 418,
      }),
      context,
    )

    const payload = await response.json()

    expect(response.status).toBe(418)
    expect(payload.error.code).toBe("TEST_ERROR")
    expect(payload.error.message).toBe("Known issue")
  })

  it("maps zod errors to validation errors", async () => {
    const error = new ZodError([])

    const response = toErrorResponse(error, context)
    const payload = await response.json()

    expect(response.status).toBe(400)
    expect(payload.error.code).toBe("VALIDATION_ERROR")
  })
})



================================================
FILE: tests/unit/features/preview/playback-client.test.ts
================================================
import { describe, expect, it } from "vitest"

import { buildNormalizedPlaybackState } from "@/features/preview/lib/playback-client"

describe("buildNormalizedPlaybackState", () => {
  it("prefers stitched playback scenes while reusing project layer assets", () => {
    const state = buildNormalizedPlaybackState(
      {
        id: "project-1",
        title: "Doc Alignment",
        status: "draft",
        scenes: [
          {
            id: "scene-1",
            orderIndex: 0,
            status: "ready",
            contextText: "Opening frame",
            sourceImageUrl: "/api/v1/assets/projects/project-1/scenes/scene-1/source.png",
            thumbnailUrl: "/api/v1/assets/projects/project-1/scenes/scene-1/thumb.png",
            assets: [
              {
                assetUrl: "/api/v1/assets/projects/project-1/scenes/scene-1/layers/0.png",
                assetType: "layer",
                layerOrder: 0,
              },
              {
                assetUrl: "/api/v1/assets/projects/project-1/scenes/scene-1/layers/1.png",
                assetType: "layer",
                layerOrder: 1,
              },
            ],
          },
        ],
      },
      {
        version: 3,
        isFallback: false,
        isReducedMotion: true,
        timelineJson: {
          summary: {
            totalDurationMs: 2400,
          },
          scenes: [
            {
              sceneId: "scene-1",
              orderIndex: 0,
              status: "ready",
              sourceImageUrl: null,
              thumbnailUrl: "/api/v1/assets/projects/project-1/scenes/scene-1/playback.png",
              fallback: false,
              startsAtMs: 0,
              durationMs: 2400,
              cameraMovement: "hold",
              intensity: "low",
              layerBehaviors: [{ layerIndex: 0, parallax: 0.14, scale: 1.01, opacity: 1 }],
            },
          ],
        },
      },
    )

    expect(state.playbackVersion).toBe(3)
    expect(state.isReducedMotion).toBe(true)
    expect(state.totalDurationMs).toBe(2400)
    expect(state.scenes[0]?.imageUrl).toContain("playback.png")
    expect(state.scenes[0]?.layerAssets).toHaveLength(2)
    expect(state.scenes[0]?.detail).toBe("Opening frame")
  })

  it("falls back to project scenes when playback is unavailable", () => {
    const state = buildNormalizedPlaybackState(
      {
        id: "project-2",
        title: "Fallback Project",
        status: "processing",
        scenes: [
          {
            id: "scene-2",
            orderIndex: 1,
            status: "processing",
            contextText: null,
            sourceImageUrl: null,
            thumbnailUrl: "/api/v1/assets/projects/project-2/scenes/scene-2/thumb.png",
            assets: [],
          },
        ],
      },
      null,
    )

    expect(state.playbackVersion).toBeNull()
    expect(state.projectStatus).toBe("processing")
    expect(state.scenes[0]?.title).toBe("Scene 01")
    expect(state.scenes[0]?.imageUrl).toContain("thumb.png")
    expect(state.totalDurationMs).toBe(2200)
  })
})



================================================
FILE: tests/unit/modules/assets/pathing.test.ts
================================================
import { describe, expect, it } from "vitest"

import { buildLayerAssetPath, buildManifestAssetPath, buildSceneVersionPath, buildThumbnailAssetPath } from "@/modules/assets"

describe("asset pathing", () => {
  it("builds deterministic versioned paths", () => {
    expect(buildSceneVersionPath("project-1", "scene-1", 2)).toBe("projects/project-1/scenes/scene-1/v2")
    expect(buildThumbnailAssetPath("project-1", "scene-1", 2)).toBe("projects/project-1/scenes/scene-1/v2/thumbnail.webp")
    expect(buildLayerAssetPath("project-1", "scene-1", 2, 3)).toBe("projects/project-1/scenes/scene-1/v2/layers/3.png")
    expect(buildManifestAssetPath("project-1", "scene-1", 2)).toBe("projects/project-1/scenes/scene-1/v2/manifest.json")
  })
})



================================================
FILE: tests/unit/modules/auth/service.test.ts
================================================
import { AuthProvider } from "@prisma/client"
import { beforeEach, describe, expect, it, vi } from "vitest"

const { authRepositoryMock } = vi.hoisted(() => ({
  authRepositoryMock: {
    findByEmail: vi.fn(),
    createUser: vi.fn(),
  },
}))

vi.mock("@/modules/auth/repository", () => ({
  authRepository: authRepositoryMock,
}))

import { authService } from "@/modules/auth/service"

describe("authService", () => {
  beforeEach(() => {
    vi.clearAllMocks()
  })

  it("registers credentials users with a hashed password", async () => {
    authRepositoryMock.findByEmail.mockResolvedValue(null)
    authRepositoryMock.createUser.mockResolvedValue({
      id: "user-1",
      email: "creator@example.com",
      authProvider: AuthProvider.credentials,
      createdAt: new Date("2026-01-01T00:00:00.000Z"),
    })

    const result = await authService.register({
      email: "creator@example.com",
      password: "super-secret-password",
    })

    expect(authRepositoryMock.createUser).toHaveBeenCalledWith({
      email: "creator@example.com",
      authProvider: AuthProvider.credentials,
      passwordHash: expect.any(String),
    })
    expect(authRepositoryMock.createUser.mock.calls[0]?.[0]?.passwordHash).not.toBe("super-secret-password")
    expect(result).toMatchObject({
      id: "user-1",
      email: "creator@example.com",
      authProvider: AuthProvider.credentials,
    })
  })

  it("rejects duplicate registration attempts", async () => {
    authRepositoryMock.findByEmail.mockResolvedValue({ id: "user-1" })

    await expect(
      authService.register({
        email: "creator@example.com",
        password: "super-secret-password",
      }),
    ).rejects.toThrow(/already exists/i)

    expect(authRepositoryMock.createUser).not.toHaveBeenCalled()
  })
})



================================================
FILE: tests/unit/modules/auth/validator.test.ts
================================================
import { describe, expect, it } from "vitest"

import { registerInputSchema } from "@/modules/auth/validator"

describe("registerInputSchema", () => {
  it("accepts a valid email and password", () => {
    const result = registerInputSchema.safeParse({
      email: "creator@example.com",
      password: "strong-pass-123",
    })

    expect(result.success).toBe(true)
  })

  it("rejects a short password", () => {
    const result = registerInputSchema.safeParse({
      email: "creator@example.com",
      password: "short",
    })

    expect(result.success).toBe(false)
  })
})



================================================
FILE: tests/unit/modules/authorization/policy.test.ts
================================================
import { describe, expect, it } from "vitest"

import { authorizeProjectAction } from "@/modules/authorization"

describe("authorizeProjectAction", () => {
  it("allows guest preview for owned guest project", () => {
    const decision = authorizeProjectAction(
      { kind: "guest", guestSessionId: "guest-1" },
      "preview",
      {
        ownerId: null,
        guestSessionId: "guest-1",
        claimedAt: null,
        expiresAt: null,
      },
    )

    expect(decision.allowed).toBe(true)
  })

  it("prevents guest save access", () => {
    const decision = authorizeProjectAction(
      { kind: "guest", guestSessionId: "guest-1" },
      "save",
      {
        ownerId: null,
        guestSessionId: "guest-1",
        claimedAt: null,
        expiresAt: null,
      },
    )

    expect(decision.allowed).toBe(false)
  })

  it("allows authenticated claim for matching guest session", () => {
    const decision = authorizeProjectAction(
      { kind: "authenticated", userId: "user-1", guestSessionId: "guest-1" },
      "claim",
      {
        ownerId: null,
        guestSessionId: "guest-1",
        claimedAt: null,
        expiresAt: null,
      },
    )

    expect(decision.allowed).toBe(true)
  })
})



================================================
FILE: tests/unit/modules/decomposition/adapter.test.ts
================================================
import { beforeEach, describe, expect, it } from "vitest"

import { resetEnvCache } from "@/config/env"
import { decompositionAdapter } from "@/modules/decomposition/adapter"

describe("decompositionAdapter", () => {
  beforeEach(() => {
    process.env.DATABASE_URL = "postgresql://postgres:postgres@localhost:5432/parallax_story_composer"
    process.env.NEXTAUTH_SECRET = "test-secret"
    process.env.NEXTAUTH_URL = "http://localhost:3000"
    process.env.GUEST_SESSION_TTL_HOURS = "72"
    process.env.RATE_LIMIT_WINDOW_MS = "60000"
    process.env.RATE_LIMIT_MAX_REQUESTS = "60"
    process.env.LOG_LEVEL = "info"
    Object.assign(process.env, { NODE_ENV: "test" })
    process.env.UPLOAD_MAX_FILES = "10"
    process.env.UPLOAD_MAX_FILE_SIZE_BYTES = "10485760"
    process.env.UPLOAD_ALLOWED_MIME_TYPES = "image/jpeg,image/png,image/webp"
    process.env.INTERNAL_UPLOAD_TOKEN_SECRET = "test-upload-secret"
    process.env.QWEN_MODEL = "qwen-image-layered"
    process.env.QWEN_TIMEOUT_MS = "30000"
    process.env.QWEN_MAX_RETRIES = "2"
    process.env.QWEN_MOCK_MODE = "true"
    resetEnvCache()
  })

  it("normalizes mock qwen output", async () => {
    const result = await decompositionAdapter.decompose({
      projectId: "project-1",
      sceneId: "scene-1",
      imageUrl: "projects/project-1/incoming/source.png",
      mimeType: "image/png",
      targetLayers: 4,
      correlationId: "corr-1",
    })

    expect(result.providerJobId).toContain("mock-")
    expect(result.layers).toHaveLength(4)
    expect(result.layers[0]?.metadata.source).toBe("qwen")
    expect(result.layers[0]?.artifact).toBeNull()
  })
})



================================================
FILE: tests/unit/modules/feature-flags/service.test.ts
================================================
import { beforeEach, describe, expect, it } from "vitest"

import { resetEnvCache } from "@/config/env"
import { featureFlagService } from "@/modules/feature-flags"

describe("featureFlagService", () => {
  beforeEach(() => {
    process.env.DATABASE_URL = "postgresql://postgres:postgres@localhost:5432/parallax_story_composer"
    process.env.NEXTAUTH_SECRET = "test-secret"
    process.env.NEXTAUTH_URL = "http://localhost:3000"
    process.env.GUEST_SESSION_TTL_HOURS = "72"
    process.env.RATE_LIMIT_WINDOW_MS = "60000"
    process.env.RATE_LIMIT_MAX_REQUESTS = "60"
    process.env.LOG_LEVEL = "info"
    Object.assign(process.env, { NODE_ENV: "test" })
    process.env.UPLOAD_MAX_FILES = "10"
    process.env.UPLOAD_MAX_FILE_SIZE_BYTES = "10485760"
    process.env.UPLOAD_ALLOWED_MIME_TYPES = "image/jpeg,image/png,image/webp"
    process.env.INTERNAL_UPLOAD_TOKEN_SECRET = "test-upload-secret"
    process.env.QWEN_MODEL = "qwen-image-layered"
    process.env.QWEN_TIMEOUT_MS = "30000"
    process.env.QWEN_MAX_RETRIES = "2"
    process.env.QWEN_MOCK_MODE = "true"
    process.env.GUEST_MAX_PROJECTS = "3"
    process.env.GUEST_MAX_SCENES_PER_PROJECT = "10"
    process.env.PROCESSING_JOB_TIMEOUT_MS = "300000"
    process.env.FEATURE_MOTION_PIPELINE = "true"
    process.env.FEATURE_PLAYBACK_PIPELINE = "true"
    process.env.FEATURE_PREVIEW_FALLBACKS = "true"
    process.env.FEATURE_REDUCED_MOTION_PREVIEW = "true"
    process.env.PROCESSING_CANARY_PERCENT = "20"
    resetEnvCache()
  })

  it("returns deterministic canary decisions", () => {
    expect(featureFlagService.allowsProcessing("scene-a")).toBe(featureFlagService.allowsProcessing("scene-a"))
  })

  it("returns configured flags", () => {
    expect(featureFlagService.flags().processingCanaryPercent).toBe(20)
    expect(featureFlagService.flags().motionPipeline).toBe(true)
  })
})



================================================
FILE: tests/unit/modules/guest-sessions/service.test.ts
================================================
import { beforeEach, describe, expect, it, vi } from "vitest"

import { resetEnvCache } from "@/config/env"

const { guestSessionRepositoryMock } = vi.hoisted(() => ({
  guestSessionRepositoryMock: {
    create: vi.fn(),
    findById: vi.fn(),
    touch: vi.fn(),
  },
}))

vi.mock("@/modules/guest-sessions/repository", () => ({
  guestSessionRepository: guestSessionRepositoryMock,
}))

import { guestSessionService } from "@/modules/guest-sessions/service"

describe("guestSessionService", () => {
  beforeEach(() => {
    process.env.DATABASE_URL = "postgresql://postgres:postgres@localhost:5432/parallax_story_composer"
    process.env.NEXTAUTH_SECRET = "test-secret"
    process.env.NEXTAUTH_URL = "http://localhost:3000"
    process.env.INTERNAL_UPLOAD_TOKEN_SECRET = "test-upload-secret"
    process.env.GUEST_SESSION_TTL_HOURS = "72"
    resetEnvCache()
    vi.clearAllMocks()
  })

  it("issues guest sessions using the configured ttl", async () => {
    guestSessionRepositoryMock.create.mockResolvedValue({ id: "guest-1" })

    await guestSessionService.issue()

    expect(guestSessionRepositoryMock.create).toHaveBeenCalledWith({
      expiresAt: expect.any(Date),
    })
  })

  it("returns null when a guest session id is missing", async () => {
    await expect(guestSessionService.resolve(undefined)).resolves.toBeNull()
    expect(guestSessionRepositoryMock.findById).not.toHaveBeenCalled()
  })

  it("touches and returns an active guest session", async () => {
    const guestSession = {
      id: "guest-1",
      expiresAt: new Date(Date.now() + 60_000),
    }

    guestSessionRepositoryMock.findById.mockResolvedValue(guestSession)

    await expect(guestSessionService.resolve("guest-1")).resolves.toEqual(guestSession)
    expect(guestSessionRepositoryMock.touch).toHaveBeenCalledWith("guest-1")
  })

  it("rejects expired guest sessions", async () => {
    guestSessionRepositoryMock.findById.mockResolvedValue({
      id: "guest-1",
      expiresAt: new Date(Date.now() - 60_000),
    })

    await expect(guestSessionService.resolve("guest-1")).rejects.toThrow(/guest session has expired/i)
    expect(guestSessionRepositoryMock.touch).not.toHaveBeenCalled()
  })
})



================================================
FILE: tests/unit/modules/maintenance/service.test.ts
================================================
import { beforeEach, describe, expect, it, vi } from "vitest"

import { resetEnvCache } from "@/config/env"

const { projectRepositoryMock, sceneRepositoryMock, sceneServiceMock, metricsMock, logProcessingEventMock } = vi.hoisted(() => ({
  projectRepositoryMock: {
    deleteExpiredGuestProjects: vi.fn(),
    deleteExpiredGuestSessions: vi.fn(),
  },
  sceneRepositoryMock: {
    findTimedOutJobs: vi.fn(),
  },
  sceneServiceMock: {
    markFailed: vi.fn(),
  },
  metricsMock: {
    increment: vi.fn(),
    gauge: vi.fn(),
  },
  logProcessingEventMock: vi.fn(),
}))

vi.mock("@/modules/projects/repository", () => ({
  projectRepository: projectRepositoryMock,
}))

vi.mock("@/modules/scenes/repository", () => ({
  sceneRepository: sceneRepositoryMock,
}))

vi.mock("@/modules/scenes", () => ({
  sceneService: sceneServiceMock,
}))

vi.mock("@/core/observability/metrics", () => ({
  metrics: metricsMock,
}))

vi.mock("@/core/observability/processing-log", () => ({
  logProcessingEvent: logProcessingEventMock,
}))

import { maintenanceService } from "@/modules/maintenance/service"

describe("maintenanceService", () => {
  beforeEach(() => {
    process.env.DATABASE_URL = "postgresql://postgres:postgres@localhost:5432/parallax_story_composer"
    process.env.NEXTAUTH_SECRET = "test-secret"
    process.env.NEXTAUTH_URL = "http://localhost:3000"
    process.env.INTERNAL_UPLOAD_TOKEN_SECRET = "test-upload-secret"
    process.env.PROCESSING_JOB_TIMEOUT_MS = "300000"
    resetEnvCache()
    vi.clearAllMocks()
  })

  it("cleans up expired guest projects and sessions", async () => {
    projectRepositoryMock.deleteExpiredGuestProjects.mockResolvedValue({ count: 2 })
    projectRepositoryMock.deleteExpiredGuestSessions.mockResolvedValue({ count: 1 })

    await expect(maintenanceService.cleanupExpiredGuestResources("trace-1")).resolves.toEqual({
      deletedProjects: 2,
      deletedSessions: 1,
    })

    expect(metricsMock.increment).toHaveBeenCalledWith("guest_cleanup_deleted_projects_total", 2)
    expect(metricsMock.increment).toHaveBeenCalledWith("guest_cleanup_deleted_sessions_total", 1)
    expect(logProcessingEventMock).toHaveBeenCalledWith(expect.objectContaining({
      event: "guest cleanup completed",
      traceId: "trace-1",
    }))
  })

  it("marks timed out jobs as failed", async () => {
    sceneRepositoryMock.findTimedOutJobs.mockResolvedValue([
      {
        id: "job-1",
        sceneId: "scene-1",
        attemptCount: 2,
        scene: {
          projectId: "project-1",
        },
      },
    ])

    await expect(maintenanceService.recoverTimedOutJobs("trace-2")).resolves.toEqual({
      recoveredJobs: 1,
    })

    expect(sceneServiceMock.markFailed).toHaveBeenCalledWith(
      "job-1",
      "scene-1",
      "Processing timed out and was recovered by maintenance.",
      3,
    )
    expect(metricsMock.gauge).toHaveBeenCalledWith("processing_queue_depth", 0)
    expect(logProcessingEventMock).toHaveBeenCalledWith(expect.objectContaining({
      event: "timed out job recovered",
      traceId: "trace-2",
      jobId: "job-1",
    }))
  })
})



================================================
FILE: tests/unit/modules/motion/service.test.ts
================================================
import { describe, expect, it } from "vitest"

import { motionService } from "@/modules/motion"

describe("motionService", () => {
  it("expands grouped config into layer behaviors", () => {
    const blueprint = motionService.buildBlueprint({
      motionPreset: "push dramatic",
      motionIntensity: "high",
      framingData: {
        version: 1,
        groups: [
          {
            groupKey: "background",
            layerIndexes: [0],
            mobile: {
              startProgress: 0,
              endProgress: 0.9,
              translateX: -4,
              translateY: -18,
              scaleFrom: 1,
              scaleTo: 1.05,
              opacityFrom: 1,
              opacityTo: 0.9,
              speedMultiplier: 0.8,
              easing: "ease-out",
            },
          },
          {
            groupKey: "foreground",
            layerIndexes: [1, 2],
            mobile: {
              startProgress: 0.1,
              endProgress: 1,
              translateX: 14,
              translateY: -42,
              scaleFrom: 1,
              scaleTo: 1.18,
              opacityFrom: 1,
              opacityTo: 1,
              speedMultiplier: 1.25,
              easing: "ease-in-out",
            },
          },
        ],
      },
      assets: [
        { assetType: "layer", layerOrder: 0 },
        { assetType: "layer", layerOrder: 1 },
        { assetType: "layer", layerOrder: 2 },
      ],
    })

    expect(blueprint.cameraMovement).toBe("push-in")
    expect(blueprint.intensity).toBe("high")
    expect(blueprint.layerBehaviors).toHaveLength(3)
    expect(blueprint.layerBehaviors[0]).toMatchObject({
      groupKey: "background",
      startProgress: 0,
      endProgress: 0.9,
    })
    expect(blueprint.transition.overlapMs).toBeGreaterThan(0)
  })

  it("derives tablet and desktop mappings from mobile", () => {
    const mobile = {
      startProgress: 0,
      endProgress: 1,
      translateX: 10,
      translateY: -20,
      scaleFrom: 1,
      scaleTo: 1.1,
      opacityFrom: 1,
      opacityTo: 1,
      speedMultiplier: 1,
      easing: "linear" as const,
    }

    expect(motionService.deriveTabletMapping(mobile)).toMatchObject({
      translateX: 12,
      translateY: -24,
      scaleTo: 1.108,
      speedMultiplier: 1.15,
    })

    expect(motionService.deriveDesktopMapping(mobile)).toMatchObject({
      translateX: 14,
      translateY: -28,
      scaleTo: 1.115,
      speedMultiplier: 1.3,
    })
  })

  it("keeps motion generation working when grouping is absent", () => {
    const blueprint = motionService.buildBlueprint({
      motionPreset: "drift up",
      motionIntensity: "medium",
      assets: [
        { assetType: "layer", layerOrder: 0 },
        { assetType: "layer", layerOrder: 1 },
      ],
    })

    expect(blueprint.layerBehaviors).toHaveLength(2)
    expect(blueprint.layerBehaviors.every((layer) => typeof layer.parallax === "number")).toBe(true)
  })

  it("auto-assigns default groups when grouping is absent", () => {
    const blueprint = motionService.buildBlueprint({
      motionPreset: "standard pan",
      motionIntensity: "medium",
      assets: [
        { assetType: "layer", layerOrder: 0 },
        { assetType: "layer", layerOrder: 1 },
        { assetType: "layer", layerOrder: 2 },
      ],
    })

    expect(blueprint.layerBehaviors.map((layer) => layer.groupKey)).toEqual(["background", "midground", "foreground"])
  })
})



================================================
FILE: tests/unit/modules/playback/service.test.ts
================================================
import { SceneStatus } from "@prisma/client"
import { beforeEach, describe, expect, it } from "vitest"

import { resetEnvCache } from "@/config/env"
import { playbackService } from "@/modules/playback"

describe("playbackService", () => {
  beforeEach(() => {
    process.env.DATABASE_URL = "postgresql://postgres:postgres@localhost:5432/parallax_story_composer"
    process.env.NEXTAUTH_SECRET = "test-secret"
    process.env.NEXTAUTH_URL = "http://localhost:3000"
    process.env.GUEST_SESSION_TTL_HOURS = "72"
    process.env.RATE_LIMIT_WINDOW_MS = "60000"
    process.env.RATE_LIMIT_MAX_REQUESTS = "60"
    process.env.LOG_LEVEL = "info"
    Object.assign(process.env, { NODE_ENV: "test" })
    process.env.UPLOAD_MAX_FILES = "10"
    process.env.UPLOAD_MAX_FILE_SIZE_BYTES = "10485760"
    process.env.UPLOAD_ALLOWED_MIME_TYPES = "image/jpeg,image/png,image/webp"
    process.env.INTERNAL_UPLOAD_TOKEN_SECRET = "test-upload-secret"
    process.env.QWEN_MODEL = "qwen-image-layered"
    process.env.QWEN_TIMEOUT_MS = "30000"
    process.env.QWEN_MAX_RETRIES = "2"
    process.env.QWEN_MOCK_MODE = "true"
    process.env.GUEST_MAX_PROJECTS = "3"
    process.env.GUEST_MAX_SCENES_PER_PROJECT = "10"
    process.env.PROCESSING_JOB_TIMEOUT_MS = "300000"
    process.env.FEATURE_MOTION_PIPELINE = "true"
    process.env.FEATURE_PLAYBACK_PIPELINE = "true"
    process.env.FEATURE_PREVIEW_FALLBACKS = "true"
    process.env.FEATURE_REDUCED_MOTION_PREVIEW = "true"
    process.env.PROCESSING_CANARY_PERCENT = "100"
    resetEnvCache()
  })

  it("builds fallback timeline from ready scenes only", () => {
    const timeline = playbackService.buildTimeline(
      "project-1",
      [
        {
          id: "scene-ready",
          orderIndex: 0,
          status: SceneStatus.ready,
          thumbnailUrl: "thumb-ready",
          sourceImageUrl: "source-ready",
          motionIntensity: "medium",
          motionBlueprintJson: {
            cameraMovement: "drift-up",
            intensity: "medium",
            layerBehaviors: [{
              layerIndex: 0,
              groupKey: "background",
              parallax: 0.5,
              scale: 1.03,
              opacity: 1,
              mobile: {
                startProgress: 0,
                endProgress: 1,
                translateX: 0,
                translateY: -18,
                scaleFrom: 1,
                scaleTo: 1.03,
                opacityFrom: 1,
                opacityTo: 1,
                speedMultiplier: 0.8,
                easing: "ease-out",
              },
            }],
            transition: { overlapMs: 320, easing: "ease-out" },
            reducedMotion: { cameraMovement: "hold", multiplier: 0.2 },
          },
        },
        {
          id: "scene-failed",
          orderIndex: 1,
          status: SceneStatus.failed,
          thumbnailUrl: "thumb-failed",
          sourceImageUrl: "source-failed",
          motionIntensity: "medium",
          motionBlueprintJson: null,
        },
      ],
      { allowFallback: true },
    )

    expect(timeline.summary.totalScenes).toBe(2)
    expect(timeline.summary.renderableScenes).toBe(1)
    expect(timeline.isFallback).toBe(true)
    expect(timeline.scenes[0]?.layerBehaviors[0]).toMatchObject({
      groupKey: "background",
      mobile: {
        translateY: -18,
      },
    })
  })

  it("applies reduced motion multiplier", () => {
    const timeline = playbackService.buildTimeline(
      "project-1",
      [
        {
          id: "scene-ready",
          orderIndex: 0,
          status: SceneStatus.ready,
          thumbnailUrl: "thumb-ready",
          sourceImageUrl: "source-ready",
          motionIntensity: "high",
          motionBlueprintJson: {
            cameraMovement: "push-in",
            intensity: "high",
            layerBehaviors: [{
              layerIndex: 0,
              parallax: 0.8,
              scale: 1.08,
              opacity: 1,
              translateX: 10,
              translateY: -30,
              scaleFrom: 1,
              scaleTo: 1.12,
              speedMultiplier: 1.2,
              mobile: {
                startProgress: 0,
                endProgress: 1,
                translateX: 10,
                translateY: -30,
                scaleFrom: 1,
                scaleTo: 1.12,
                opacityFrom: 1,
                opacityTo: 1,
                speedMultiplier: 1.2,
                easing: "linear",
              },
            }],
            transition: { overlapMs: 320, easing: "linear" },
            reducedMotion: { cameraMovement: "hold", multiplier: 0.2 },
          },
        },
      ],
      { reducedMotion: true, allowFallback: true },
    )

    expect(timeline.reducedMotion).toBe(true)
    expect(timeline.scenes[0]?.cameraMovement).toBe("hold")
    expect(timeline.scenes[0]?.layerBehaviors[0]?.parallax).toBe(0.16)
    expect(timeline.scenes[0]?.layerBehaviors[0]?.mobile).toMatchObject({
      translateX: 2,
      translateY: -6,
      scaleTo: 1.024,
      speedMultiplier: 0.24,
    })
  })

  it("rejects playback when no scenes are renderable", () => {
    expect(() =>
      playbackService.buildTimeline(
        "project-1",
        [
          {
            id: "scene-failed",
            orderIndex: 0,
            status: SceneStatus.failed,
            thumbnailUrl: "thumb-failed",
            sourceImageUrl: "source-failed",
            motionIntensity: "medium",
            motionBlueprintJson: null,
          },
        ],
        { allowFallback: true },
      ),
    ).toThrow(/no scenes are ready for playback yet/i)
  })
})



================================================
FILE: tests/unit/modules/projects/service.test.ts
================================================
import { beforeEach, describe, expect, it, vi } from "vitest"

import { resetEnvCache } from "@/config/env"

const { projectRepositoryMock } = vi.hoisted(() => ({
  projectRepositoryMock: {
    countGuestProjects: vi.fn(),
    createGuestProject: vi.fn(),
    createAuthenticatedProject: vi.fn(),
    findById: vi.fn(),
    claim: vi.fn(),
  },
}))

vi.mock("@/modules/projects/repository", () => ({
  projectRepository: projectRepositoryMock,
}))

import { projectService } from "@/modules/projects/service"

describe("projectService", () => {
  beforeEach(() => {
    process.env.DATABASE_URL = "postgresql://postgres:postgres@localhost:5432/parallax_story_composer"
    process.env.NEXTAUTH_SECRET = "test-secret"
    process.env.NEXTAUTH_URL = "http://localhost:3000"
    process.env.INTERNAL_UPLOAD_TOKEN_SECRET = "test-upload-secret"
    process.env.GUEST_MAX_PROJECTS = "3"
    resetEnvCache()
    vi.clearAllMocks()
  })

  it("creates guest projects when quota allows", async () => {
    projectRepositoryMock.countGuestProjects.mockResolvedValue(0)
    projectRepositoryMock.createGuestProject.mockResolvedValue({ id: "project-1", title: "Story" })

    const result = await projectService.create({
      title: "Story",
      actor: {
        kind: "guest",
        guestSessionId: "guest-1",
        expiresAt: new Date("2026-01-01T00:00:00.000Z"),
      },
    })

    expect(projectRepositoryMock.createGuestProject).toHaveBeenCalled()
    expect(result.outputFormat).toBe("9:16")
  })

  it("rejects guest project creation when quota is exceeded", async () => {
    projectRepositoryMock.countGuestProjects.mockResolvedValue(3)

    await expect(
      projectService.create({
        title: "Story",
        actor: {
          kind: "guest",
          guestSessionId: "guest-1",
          expiresAt: new Date("2026-01-01T00:00:00.000Z"),
        },
      }),
    ).rejects.toThrow(/only keep 3 active projects/i)
  })

  it("claims an unclaimed guest project for an authenticated user", async () => {
    projectRepositoryMock.findById.mockResolvedValue({
      id: "project-1",
      guestSessionId: "guest-1",
      ownerId: null,
      claimedAt: null,
      expiresAt: null,
    })
    projectRepositoryMock.claim.mockResolvedValue({ id: "project-1", ownerId: "user-1" })

    const result = await projectService.claim("project-1", {
      userId: "user-1",
      guestSessionId: "guest-1",
    })

    expect(projectRepositoryMock.claim).toHaveBeenCalledWith("project-1", {
      userId: "user-1",
      guestSessionId: "guest-1",
    })
    expect(result.ownerId).toBe("user-1")
  })
})



================================================
FILE: tests/unit/modules/scenes/service.test.ts
================================================
import { JobStatus, SceneStatus } from "@prisma/client"
import { beforeEach, describe, expect, it, vi } from "vitest"

import { resetEnvCache } from "@/config/env"

const { sceneRepositoryMock } = vi.hoisted(() => ({
  sceneRepositoryMock: {
    countByProjectId: vi.fn(),
    createManyWithAssets: vi.fn(),
    findById: vi.fn(),
    findActiveDecompositionJob: vi.fn(),
    update: vi.fn(),
    updateSceneStatus: vi.fn(),
    createDecompositionJob: vi.fn(),
    updateJob: vi.fn(),
  },
}))

vi.mock("@/modules/scenes/repository", () => ({
  sceneRepository: sceneRepositoryMock,
}))

import { sceneService } from "@/modules/scenes/service"

describe("sceneService", () => {
  beforeEach(() => {
    process.env.DATABASE_URL = "postgresql://postgres:postgres@localhost:5432/parallax_story_composer"
    process.env.NEXTAUTH_SECRET = "test-secret"
    process.env.NEXTAUTH_URL = "http://localhost:3000"
    process.env.INTERNAL_UPLOAD_TOKEN_SECRET = "test-upload-secret"
    process.env.GUEST_MAX_SCENES_PER_PROJECT = "10"
    resetEnvCache()
    vi.clearAllMocks()
  })

  it("creates scenes from uploads when project quota allows", async () => {
    sceneRepositoryMock.countByProjectId.mockResolvedValue(1)
    sceneRepositoryMock.createManyWithAssets.mockResolvedValue([{ id: "scene-1" }])

    const result = await sceneService.createFromUploads([
      {
        id: "scene-1",
        projectId: "project-1",
        orderIndex: 0,
        sourceImageUrl: "projects/project-1/incoming/scene-1.png",
        thumbnailUrl: "projects/project-1/scenes/scene-1/v1/thumbnail.webp",
        originalAsset: { assetUrl: "projects/project-1/incoming/scene-1.png" },
        thumbnailAsset: { assetUrl: "projects/project-1/scenes/scene-1/v1/thumbnail.webp" },
      },
    ])

    expect(sceneRepositoryMock.createManyWithAssets).toHaveBeenCalled()
    expect(result).toEqual([{ id: "scene-1" }])
  })

  it("rejects upload batches that exceed the scene quota", async () => {
    sceneRepositoryMock.countByProjectId.mockResolvedValue(10)

    await expect(
      sceneService.createFromUploads([
        {
          id: "scene-1",
          projectId: "project-1",
          orderIndex: 0,
          sourceImageUrl: "projects/project-1/incoming/scene-1.png",
          thumbnailUrl: "projects/project-1/scenes/scene-1/v1/thumbnail.webp",
          originalAsset: { assetUrl: "projects/project-1/incoming/scene-1.png" },
          thumbnailAsset: { assetUrl: "projects/project-1/scenes/scene-1/v1/thumbnail.webp" },
        },
      ]),
    ).rejects.toThrow(/up to 10 scenes/i)
  })

  it("queues decomposition work and marks the scene queued", async () => {
    sceneRepositoryMock.findById.mockResolvedValue({ id: "scene-1", generationVersion: 1 })
    sceneRepositoryMock.findActiveDecompositionJob.mockResolvedValue(null)
    sceneRepositoryMock.createDecompositionJob.mockResolvedValue({ id: "job-1", status: JobStatus.queued })

    const job = await sceneService.enqueueDecomposition("scene-1", {
      correlationId: "corr-1",
      reason: "manual-retry",
      resetGeneration: true,
    })

    expect(sceneRepositoryMock.updateSceneStatus).toHaveBeenCalledWith("scene-1", {
      generationVersion: 2,
      status: SceneStatus.queued,
    })
    expect(job).toEqual({ id: "job-1", status: JobStatus.queued })
  })

  it("saves grouping into framingData while preserving scene fields", async () => {
    sceneRepositoryMock.update.mockResolvedValue({ id: "scene-1" })

    await sceneService.update("scene-1", {
      contextText: "Updated context",
      motionPreset: "Cinematic Push",
      motionIntensity: "high",
      grouping: {
        version: 1,
        groups: [
          {
            groupKey: "foreground",
            layerIndexes: [2],
            mobile: {
              startProgress: 0,
              endProgress: 1,
              translateX: 14,
              translateY: -36,
              scaleFrom: 1,
              scaleTo: 1.18,
              opacityFrom: 1,
              opacityTo: 0.95,
              speedMultiplier: 1.3,
              easing: "ease-out",
            },
          },
        ],
      },
    })

    expect(sceneRepositoryMock.update).toHaveBeenCalledWith("scene-1", {
      contextText: "Updated context",
      motionPreset: "Cinematic Push",
      motionIntensity: "high",
      grouping: {
        version: 1,
        groups: [
          {
            groupKey: "foreground",
            layerIndexes: [2],
            mobile: {
              startProgress: 0,
              endProgress: 1,
              translateX: 14,
              translateY: -36,
              scaleFrom: 1,
              scaleTo: 1.18,
              opacityFrom: 1,
              opacityTo: 0.95,
              speedMultiplier: 1.3,
              easing: "ease-out",
            },
          },
        ],
      },
    })
  })
})



================================================
FILE: tests/unit/modules/scenes/validator.test.ts
================================================
import { describe, expect, it } from "vitest"

import { updateSceneInputSchema } from "@/modules/scenes"

describe("updateSceneInputSchema", () => {
  it("accepts a valid grouped motion payload", () => {
    const result = updateSceneInputSchema.safeParse({
      grouping: {
        version: 1,
        groups: [
          {
            groupKey: "background",
            layerIndexes: [0, 1],
            mobile: {
              startProgress: 0,
              endProgress: 0.8,
              translateX: 0,
              translateY: -12,
              scaleFrom: 1,
              scaleTo: 1.08,
              opacityFrom: 1,
              opacityTo: 0.92,
              speedMultiplier: 0.8,
              easing: "ease-out",
            },
          },
          {
            groupKey: "midground",
            layerIndexes: [2],
            mobile: {
              startProgress: 0.1,
              endProgress: 0.95,
              translateX: 4,
              translateY: -24,
              scaleFrom: 1,
              scaleTo: 1.12,
              opacityFrom: 1,
              opacityTo: 1,
              speedMultiplier: 1,
              easing: "linear",
            },
          },
        ],
      },
    })

    expect(result.success).toBe(true)
  })

  it("rejects duplicate layer assignments across groups", () => {
    const result = updateSceneInputSchema.safeParse({
      grouping: {
        version: 1,
        groups: [
          {
            groupKey: "background",
            layerIndexes: [0],
            mobile: {
              startProgress: 0,
              endProgress: 1,
              translateX: 0,
              translateY: 0,
              scaleFrom: 1,
              scaleTo: 1.1,
              opacityFrom: 1,
              opacityTo: 1,
              speedMultiplier: 0.8,
              easing: "linear",
            },
          },
          {
            groupKey: "foreground",
            layerIndexes: [0],
            mobile: {
              startProgress: 0,
              endProgress: 1,
              translateX: 12,
              translateY: -40,
              scaleFrom: 1,
              scaleTo: 1.2,
              opacityFrom: 1,
              opacityTo: 1,
              speedMultiplier: 1.2,
              easing: "ease-in-out",
            },
          },
        ],
      },
    })

    expect(result.success).toBe(false)
    expect(result.error?.issues[0]?.message).toMatch(/assigned to multiple groups/i)
  })

  it("rejects invalid groups", () => {
    const result = updateSceneInputSchema.safeParse({
      grouping: {
        version: 1,
        groups: [
          {
            groupKey: "sky",
            layerIndexes: [0],
            mobile: {
              startProgress: 0,
              endProgress: 1,
              translateX: 0,
              translateY: 0,
              scaleFrom: 1,
              scaleTo: 1,
              opacityFrom: 1,
              opacityTo: 1,
              speedMultiplier: 1,
              easing: "linear",
            },
          },
        ],
      },
    })

    expect(result.success).toBe(false)
  })

  it("rejects invalid progress ranges", () => {
    const result = updateSceneInputSchema.safeParse({
      grouping: {
        version: 1,
        groups: [
          {
            groupKey: "midground",
            layerIndexes: [1],
            mobile: {
              startProgress: 0.8,
              endProgress: 0.2,
              translateX: 0,
              translateY: 0,
              scaleFrom: 1,
              scaleTo: 1,
              opacityFrom: 1,
              opacityTo: 1,
              speedMultiplier: 1,
              easing: "linear",
            },
          },
        ],
      },
    })

    expect(result.success).toBe(false)
    expect(result.error?.issues[0]?.message).toMatch(/startProgress/i)
  })

  it("supports nullable grouping", () => {
    const result = updateSceneInputSchema.safeParse({
      grouping: null,
    })

    expect(result.success).toBe(true)
  })
})



================================================
FILE: tests/unit/modules/uploads/service.test.ts
================================================
import { beforeEach, describe, expect, it } from "vitest"

import { resetEnvCache } from "@/config/env"
import { uploadService } from "@/modules/uploads"

describe("uploadService", () => {
  beforeEach(() => {
    process.env.DATABASE_URL = "postgresql://postgres:postgres@localhost:5432/parallax_story_composer"
    process.env.NEXTAUTH_SECRET = "test-secret"
    process.env.NEXTAUTH_URL = "http://localhost:3000"
    process.env.GUEST_SESSION_TTL_HOURS = "72"
    process.env.RATE_LIMIT_WINDOW_MS = "60000"
    process.env.RATE_LIMIT_MAX_REQUESTS = "60"
    process.env.LOG_LEVEL = "info"
    Object.assign(process.env, { NODE_ENV: "test" })
    process.env.UPLOAD_MAX_FILES = "10"
    process.env.UPLOAD_MAX_FILE_SIZE_BYTES = "10485760"
    process.env.UPLOAD_ALLOWED_MIME_TYPES = "image/jpeg,image/png,image/webp"
    process.env.INTERNAL_UPLOAD_TOKEN_SECRET = "test-upload-secret"
    resetEnvCache()
  })

  it("creates and verifies upload contracts", () => {
    const [contract] = uploadService.createUploadContracts("project-1", [
      {
        filename: "scene.png",
        mimeType: "image/png",
        sizeBytes: 1024,
      },
    ])

    const verified = uploadService.verifyUploadToken(contract.uploadToken)

    expect(verified.projectId).toBe("project-1")
    expect(verified.storageKey).toContain("projects/project-1/incoming/")
    expect(contract.uploadUrl).toContain(contract.uploadToken)
  })

  it("rejects unsupported mime types", () => {
    expect(() =>
      uploadService.createUploadContracts("project-1", [
        {
          filename: "scene.gif",
          mimeType: "image/gif",
          sizeBytes: 1024,
        },
      ]),
    ).toThrow(/unsupported file type/i)
  })
})



================================================
FILE: .opencode/commands/brainstorm.md
================================================
---
description: Convert a brain dump into a structured PRD draft through guided questioning
agent: build
---

# Brainstorm Command

This command converts a raw brain dump into a structured **PRD draft** through analysis and guided questioning.

The input can come from either:

1. The current conversation context
2. A file path passed as an argument
3. Direct text passed as an argument

---

# Step 1 — Determine Input Source

If `$ARGUMENTS` is provided:

Check if it matches a file path.

If the file exists:
Read the file contents.

If the argument is not a file:
Treat the argument as raw idea text.

If no argument is provided:
Use the current conversation context as the input source.

---

# Step 2 — Parse Brain Dump

Analyze the input text and extract:

• application concept  
• problem being solved  
• target users  
• mentioned features  
• UI or theme ideas  
• integrations  
• platform hints  
• data requirements  

If insufficient information exists, request a short explanation of the idea.

---

# Step 3 — Create Initial PRD Draft Structure

Organize extracted ideas into structured sections.

# PRD Draft

## App Concept

Brief description of the application idea.

---

## Problem Statement

What problem the app solves.

---

## Target Users

Identify potential user groups.

Examples:

Consumers  
Businesses  
Creators  
Developers  

---

## Core Features

Extract primary functionality.

Examples:

User accounts  
Dashboards  
Search  
Notifications  
Payments  

---

## Supporting Features

Enhancements to the main product.

Examples:

Analytics  
User profiles  
Settings  
Admin tools  

---

## Platform

Determine likely platform.

Examples:

Web application  
Mobile application  
Hybrid platform  

---

## UI / Theme Ideas

Extract UI style hints.

Examples:

Minimal UI  
Dashboard layout  
Social-style feed  
Dark mode  

---

## Integrations

List possible integrations.

Examples:

Stripe  
OAuth providers  
Email services  
Third-party APIs  

---

## Data Model Hints

Identify types of data that must exist.

Examples:

Users  
Projects  
Media  
Transactions  

---

# Step 4 — Ask Clarifying Questions

Ask structured questions **one at a time**.

Pause after each question and wait for the user to respond.

Questions should focus on:

### Problem

What specific problem does the application solve?

### Users

Who is the primary user of this product?

### Core Feature

What is the most important feature?

### Platform

Will this be:

Web  
Mobile  
Both

### Authentication

Will users need accounts?

### Data

What important data must be stored?

### Monetization

Will the app generate revenue?

---

# Step 5 — Challenge Assumptions

Ask deeper questions to expose risks.

Examples:

What feature will be hardest to implement?

What would make users switch from competitors?

What part of the system might become a scaling bottleneck?

What data privacy risks exist?

---

# Step 6 — Refine the PRD Draft

Update the PRD draft using the user's answers.

Ensure the document now contains:

• a clear application concept  
• defined users  
• a concrete feature list  
• platform definition  

---

# Step 7 — Save Brainstorm Artifact

Write the structured document to:

docs/reference/prd-draft.md

Create directory if missing.

Overwrite existing file if it exists.

---

# Completion Output

Return confirmation only:

PRD draft generated from brainstorm session.
---

# Update Project State

Update the following file:

docs/reference/project-state.md

Modify:

Phase: [CURRENT_COMMAND_PHASE]
Last Updated: [CURRENT_TIMESTAMP]

Save changes.



================================================
FILE: .opencode/commands/build-frontend-system.md
================================================
---
description: Orchestrate the full frontend build pipeline
agent: build
---

# Frontend Build Orchestrator

Execute the complete frontend generation pipeline.

---

# Step 1

Run:

/extract-design-spec

---

# Step 2

Run:

/generate-page-graph

---

# Step 3

Run:

/generate-ui-dependency-graph

---

# Step 4

Run frontend implementation skill:

build-frontend

The build process must follow the generation order defined in:

docs/reference/ui-dependency-graph.md

---

# Validation

Verify:

- pages exist
- layouts exist
- components generated
- hooks wired
- API endpoints mapped

---

# Output

Return confirmation only:

"Frontend build pipeline completed."



================================================
FILE: .opencode/commands/classify-app.md
================================================
---
description: Classify application type and extract system constraints
agent: build
subtask: true
---

Analyze the current clarified idea and extract structured system metadata.

Identify:

- App Type (SaaS, Internal Tool, AI-native, Marketplace, API-first, etc.)
- Tenant Model (Single / Multi)
- Scale Expectation (MVP / 1k users / 10k+ / 100k+)
- Data Sensitivity Level (Low / Moderate / High / Regulated)
- External Integrations Required
- Real-Time Requirements
- AI/LLM Involvement
- Compliance Requirements
- Monetization Model
- Deployment Expectations

---

Output structured format:

# APPLICATION CLASSIFICATION

## System Type
## Tenant Model
## Scale Profile
## Data Sensitivity
## Compliance Tier
## Real-Time Requirements
## AI Involvement
## External Integrations
## Risk Level

---

After generating:

1. Save to:

docs/reference/app-classification.md

2. Create directory if missing.
3. Overwrite existing file.
4. Output confirmation only:
"Application classification saved to docs/reference/app-classification.md"

---

# Update Project State

Update the following file:

docs/reference/project-state.md

Modify:

Phase: [CURRENT_COMMAND_PHASE]
Last Updated: [CURRENT_TIMESTAMP]

Save changes.



================================================
FILE: .opencode/commands/extract-design-spec.md
================================================
---
description: Reverse engineer the exported Google Stitch UI codebase and generate a technical frontend architecture specification
agent: build
subtask: true
---

Reference:

@docs/reference/prd-draft.md
@design/

@docs/templates/FRONTEND_ARCHITECTURE_TEMPLATE.md

---

# Objective

Analyze the UI code exported from **Google Stitch** and generate a **technical frontend architecture specification**.

This command must perform a **structural analysis of the HTML codebase** and derive:

• page-level architecture  
• layout hierarchy  
• reusable UI modules  
• component boundaries  
• styling architecture  
• navigation topology  
• UI dependency graph  

The goal is to transform raw UI markup into a **clear architectural representation of the frontend system**.

---

# Step 1 — Locate Design Codebase

Scan the repository directory:

design/

Recursively detect HTML source files.

Examples:

landing.html.txt  
dashboard.html.txt  
settings.html.txt  

Each file contains HTML markup exported from Google Stitch.

If no HTML sources exist:

Abort with:

"No Stitch design sources found in design directory."

---

# Step 2 — Parse DOM Structure

For each HTML file:

Construct a **DOM tree representation**.

Analyze structural nodes including:

• `<header>`  
• `<nav>`  
• `<main>`  
• `<section>`  
• `<aside>`  
• `<footer>`  

Extract hierarchical structure:


Page Root
→ Layout Containers
→ Sections
→ Nested UI Blocks


Preserve DOM hierarchy when identifying architectural boundaries.

---

# Step 3 — Identify Layout Containers

Detect layout scaffolding elements responsible for global UI structure.

Common indicators:

• navigation containers  
• persistent sidebars  
• headers  
• footers  
• global wrappers  

Derive layout modules.

Examples:

MarketingLayout  
AppLayout  
AuthLayout  

Layout responsibilities must include:

• global navigation  
• layout slots for page content  
• responsive container behavior  

---

# Step 4 — Identify UI Modules

Analyze repeated DOM patterns to identify reusable modules.

Examples:

Card components  
Form components  
Navigation elements  
Buttons  
Data tables  

Define module boundaries based on:

• repeated markup structures  
• logical UI grouping  
• component composition  

Do not alter DOM semantics during extraction.

---

# Step 5 — Detect Styling Architecture

Analyze styling framework usage.

Detect indicators for:

TailwindCSS  
Bootstrap  
Custom CSS  

Example detection signals:


tailwindcdn
class="flex grid ..."
style tags
CSS variables


Extract design tokens if available:

colors  
typography  
spacing scale  
border radius  

---

# Step 6 — Page-Level Architecture

Each HTML file represents a **page-level module**.

Derive:

Page name  
Route path  
Page purpose  

Example:

landing.html → `/`  
dashboard.html → `/dashboard`  
settings.html → `/settings`

Document page responsibilities.

---

# Step 7 — Navigation Topology

Analyze navigation structures.

Detect:

• navbar link structures  
• sidebar navigation menus  
• internal routing references  

Construct navigation graph describing how pages connect.

Example:


Landing
→ Login
→ Dashboard
→ Settings


---

# Step 8 — Component Boundary Detection

Define component boundaries using the following heuristics:

Repeated DOM segments  
Isolated UI functionality  
Encapsulated styling blocks  

Examples:

Navbar  
Sidebar  
HeroSection  
FeatureGrid  
FeatureCard  

Record parent-child relationships.

---

# Step 9 — Generate Component Graph

Produce a hierarchical UI component graph.

Example:


LandingPage
└ MarketingLayout
├ Navbar
├ HeroSection
├ FeatureGrid
│ └ FeatureCard
└ Footer


This graph must represent **composition relationships between UI modules**.

---

# Step 10 — Generate Page Wiring Graph

Define page-level wiring relationships.

Each page must include:

Route  
Layout  
Components  
Navigation relationships  

Example:


DashboardPage
Route: /dashboard

Layout
AppLayout

Components
Sidebar
DashboardHeader
ProjectList
└ ProjectCard


---

# Step 11 — Generate UI Dependency Graph

Create a dependency graph describing the **correct generation order of UI modules**.

Order should follow:

Layouts  
Shared Components  
Nested Components  
Pages  

Example:


AppLayout
Navbar
Sidebar
ProjectCard
ProjectList
DashboardHeader
DashboardPage


Resolve dependency relationships using topological ordering.

---

# Step 12 — Produce Architecture Document

Generate the frontend architecture document using:

@docs/templates/FRONTEND_ARCHITECTURE_TEMPLATE.md

Populate sections including:

Frontend framework detection  
Design system  
Page map  
Layout architecture  
Component architecture  
Component graph  
Page wiring graph  
UI dependency graph  

The document should read as a **technical architecture specification**, not a visual design description.

---

# Step 13 — Save Architecture Artifact

Write the generated architecture document to:

docs/reference/frontend-architecture.md

Create directory if missing.

Overwrite existing file.

---

# Completion Output

Return confirmation only:

"Frontend architecture generated from Stitch UI codebase."

---

# Update Project State

Update:

docs/reference/project-state.md

Phase: Frontend Architecture Generated  
Last Updated: [CURRENT_TIMESTAMP]



================================================
FILE: .opencode/commands/finalize-prd.md
================================================
---
description: Generate the finalized Product Requirements Document from architecture, stack decisions, and design specifications
agent: build
subtask: true
---

Reference Inputs:

@docs/reference/prd-draft.md
@docs/reference/frontend-architecture.md
@docs/reference/backend-architecture.md
@docs/reference/stack.md
@docs/reference/frontend-design-spec.md

---

# Objective

Generate the **final Product Requirements Document (PRD)** by consolidating the outputs of the planning and architecture stages.

The final PRD must reflect the **actual system architecture, technology stack, and UI structure**.

This document becomes the **authoritative requirements specification for the application**.

The command must **not invent features or functionality** that do not exist in the referenced documents.

---

# Step 1 — Load Draft PRD

Load:

docs/reference/prd-draft.md

Extract:

• product vision  
• problem statement  
• target users  
• initial feature ideas  

Use this as the **conceptual foundation** for the final PRD.

---

# Step 2 — Load Architecture Artifacts

Load the following architecture artifacts.

docs/reference/frontend-architecture.md  
docs/reference/backend-architecture.md  
docs/reference/stack.md  
docs/reference/frontend-design-spec.md  

Extract:

• frontend pages and UI modules  
• backend services and APIs  
• data models  
• tech stack decisions  
• system architecture  

---

# Step 3 — Derive Feature Set

Derive the **confirmed feature list** from:

Frontend pages  
UI components  
Backend services  
API endpoints  

Only include features that appear in architecture artifacts.

Do not include speculative features.

---

# Step 4 — Define Functional Requirements

For each confirmed feature:

Define:

Feature Name  
Feature Description  
User Flow  
Frontend Components  
Backend Services  
API Endpoints  
Data Requirements  

Ensure each feature maps to **both frontend and backend implementations**.

---

# Step 5 — Define System Architecture

Summarize the technical architecture.

Include:

Frontend Architecture Overview  
Backend Architecture Overview  
API Communication Model  
Data Persistence Strategy  

Use information from:

frontend-architecture.md  
backend-architecture.md  
stack.md  

---

# Step 6 — Define Technology Stack

Document the confirmed technology stack.

Include:

Frontend Framework  
Backend Runtime  
Backend Framework  
Database  
ORM / Query Layer  
Deployment Platform  

Extract from:

docs/reference/stack.md

---

# Step 7 — Define Data Model Overview

Extract primary entities from backend architecture.

Examples:

User  
Project  
Task  

Define:

Entity Name  
Purpose  
Relationships  

---

# Step 8 — Define UI/UX Structure

Extract page structure from:

frontend architecture  
design spec  

Define:

Page Name  
Route  
Purpose  
Primary Components  

---

# Step 9 — Define Non-Functional Requirements

Define system quality attributes.

Include:

Performance expectations  
Security requirements  
Scalability expectations  
Reliability expectations  

Use architecture artifacts as reference.

---

# Step 10 — Define MVP Scope

Determine the **minimum feature set required for initial release**.

Use:

PRD draft feature prioritization  
frontend page structure  
backend services  

Exclude non-essential features.

---

# Step 11 — Define Out of Scope

List features that will **not be included in the MVP**.

This prevents scope creep.

---

# Step 12 — Generate Final PRD

Structure the final document as:

# PRODUCT REQUIREMENTS DOCUMENT

## Product Overview

## Problem Statement

## Target Users

## Product Vision

---

## Feature Set

---

## Functional Requirements

---

## System Architecture

Frontend Architecture  
Backend Architecture  

---

## Technology Stack

---

## Data Model Overview

---

## UI/UX Structure

---

## Non-Functional Requirements

Performance  
Security  
Scalability  

---

## MVP Scope

---

## Out of Scope

---

# Step 13 — Save Artifact

Write the finalized PRD to:

docs/reference/prd.md

Create directory if missing.

Overwrite existing file.

---

# Completion Output

Return confirmation only:

"Final PRD generated and saved to docs/reference/prd-finalized.md"

---

# Update Project State

Update:

docs/reference/project-state.md

Phase: PRD Approved  
Last Updated: [CURRENT_TIMESTAMP]



================================================
FILE: .opencode/commands/generate-architecture.md
================================================
---
description: Generate enforced architecture document and save to docs/reference
agent: build
subtask: true
---
Before executing:

Check project-state.md

If Current Phase < PRD Generated:
Abort and instruct user to generate PRD first.

---

Convert the current context or referenced PRD into a structured Architecture Document.

Additional refinement instructions:
$ARGUMENTS

Follow this template strictly:

@docs/templates/ARCHITECTURE_TEMPLATE.md

Ensure:
- Folder structure is explicitly defined
- Layer responsibilities are enforced
- No vague descriptions
- Trade-offs are documented
- Scaling strategy is explicit

---

After generating the document:

1. Save the file to:

docs/reference/architecture.md

2. If the docs/reference directory does not exist, create it.
3. Overwrite the file if it already exists.
4. Do NOT output the full document in chat.
5. Output only this confirmation message:

"Architecture document saved to docs/reference/architecture.md"

---

# Update Project State

Update the following file:

docs/reference/project-state.md

Modify:

Phase: [CURRENT_COMMAND_PHASE]
Last Updated: [CURRENT_TIMESTAMP]

Save changes.



================================================
FILE: .opencode/commands/generate-page-graph.md
================================================
---
description: Generate page wiring graph from frontend architecture
agent: plan
subtask: true
---

# Generate Page Wiring Graph

Create a multi-page wiring graph that maps routes, layouts, hooks, APIs, and components.

---

# Inputs

Read:

docs/reference/frontend-architecture.md  
docs/reference/prd.md  
api/

---

# Step 1 — Identify Pages

Extract page definitions from:

frontend architecture

Examples:

LandingPage  
DashboardPage  
SettingsPage

Determine route mapping.

Example:

landing → /  
dashboard → /dashboard

---

# Step 2 — Map Layouts

Determine layout used by each page.

Examples:

MarketingLayout  
AppLayout  
AuthLayout

---

# Step 3 — Map Hooks

Determine data hooks required for each page.

Examples:

useProjects  
useActivityFeed  
useUserSettings

Hooks should correspond to page data needs.

---

# Step 4 — Map API Endpoints

Match hooks to backend endpoints.

Examples:

useProjects → GET /api/projects  
useUserSettings → GET /api/user/settings

If endpoint missing, mark:

Backend Endpoint Required

---

# Step 5 — Map Components

Determine components used by each page.

Use component hierarchy from frontend architecture.

Example:

DashboardPage
  Sidebar
  DashboardHeader
  ProjectList
    ProjectCard

---

# Step 6 — Generate Graph

Create page wiring graph.

Structure:

Page  
Route  
Layout  
Hooks  
API Endpoints  
Components

---

# Output

Write to:

docs/reference/page-wiring-graph.md

---

# Completion Output

Return confirmation only:

"Page wiring graph generated."



================================================
FILE: .opencode/commands/generate-plan.md
================================================
---
description: Generate a detailed implementation plan and architecture rules using the finalized system artifacts
agent: plan
subtask: true
---

Reference Inputs:

@docs/reference/frontend-architecture.md  
@docs/reference/backend-architecture.md  
@docs/reference/stack.md  
@docs/reference/prd.md  
@docs/reference/stack-guidelines.md  

Rules Template:

@docs/templates/ARCHITECTURE_RULES_TEMPLATE.md

---

# Objective

Generate the **complete application build plan** using the finalized architecture artifacts.

The plan must define:

• infrastructure setup  
• module creation order  
• feature-by-feature implementation  
• cross-cutting engineering concerns  
• validation and testing steps  
• deployment strategy  

The plan must also generate **architecture rules** derived from stack best practices to prevent architectural drift during implementation.

---

# Step 1 — Load Architecture Artifacts

Load:

docs/reference/frontend-architecture.md  
docs/reference/backend-architecture.md  

Extract:

Frontend pages  
UI components  
Layouts  
Backend services  
Controllers  
Repositories  
Data models  
API endpoints  

---

# Step 2 — Load Product Requirements

Load:

docs/reference/prd.md

Extract:

Confirmed feature set  
User flows  
Core product functionality  

Ensure every feature maps to both:

Frontend implementation  
Backend implementation

---

# Step 3 — Load Stack Configuration

Load:

docs/reference/stack.md

Extract confirmed stack:

Frontend framework  
Backend framework  
Database  
ORM  
Authentication  
Deployment platform  
Testing frameworks  

---

# Step 4 — Load Stack Best Practices

Load:

docs/reference/stack-guidelines.md

Extract best-practice patterns for:

Project structure  
Service layering  
API patterns  
Database usage  
Security practices  
Testing strategies  

These guidelines will be translated into **architecture rules**.

---

# Step 5 — Generate Architecture Rules

Use the template:

docs/templates/ARCHITECTURE_RULES_TEMPLATE.md

Populate rule categories using stack guidelines.

Include rules for:

Layer separation  
API structure  
Database access patterns  
UI state management  
Security enforcement  
Testing requirements  

Save rules artifact to:

docs/reference/architecture-rules.md

---

# Step 6 — Determine Build Order

Determine build dependencies from architecture artifacts.

Example order:

Infrastructure  
Database schema  
Backend services  
API endpoints  
Frontend hooks  
UI components  
Pages  

Ensure dependency ordering prevents missing modules.

---

# Step 7 — Generate Build Plan

Create structured build plan.

# APPLICATION BUILD PLAN

## Infrastructure Phase

Initialize project repository structure.

Setup:

environment configuration  
database instance  
containerization (if required)  

---

## Core Module Setup

Create foundational modules.

Examples:

authentication system  
configuration management  
logging utilities  

---

## Backend Implementation

Implement backend system layers.

Controllers  
Services  
Repositories  
Models  

Define API endpoints derived from the PRD.

---

## Frontend Implementation

Implement UI architecture.

Layouts  
Shared components  
Page components  

Wire frontend hooks to backend endpoints.

---

## Feature-by-Feature Breakdown

For each feature define:

Feature Name  
Frontend components  
Backend services  
API endpoints  
Data models  

---

## Cross-Cutting Concerns

Implement shared engineering concerns.

Authentication  
Authorization  
Error handling  
Logging  
Configuration  

---

## Performance Strategy

Apply stack-specific optimization practices.

Examples:

database indexing  
API caching  
lazy loading  

---

## Security Enforcement

Apply security best practices.

Examples:

input validation  
authentication guards  
rate limiting  

---

## Validation Checklist

Verify implementation integrity.

Examples:

all endpoints implemented  
UI components wired to APIs  
tests implemented  

---

## Deployment Strategy

Define deployment steps.

Examples:

database migrations  
environment configuration  
CI/CD pipeline  

---

# Step 8 — Save Plan Artifact

Write build plan to:

docs/reference/plan.md

Overwrite existing file if present.

---

# Completion Output

Return confirmation only:

"Implementation plan and architecture rules generated."

---

# Update Project State

Update:

docs/reference/project-state.md

Phase: Plan Generated  
Last Updated: [CURRENT_TIMESTAMP]



================================================
FILE: .opencode/commands/generate-stack-guidelines.md
================================================
---
description: Generate stack-specific engineering guidelines using Context7 MCP
agent: build
subtask: true
---

Reference:

@docs/reference/stack.md

---

# Objective

Generate **engineering best-practice guidelines** for the confirmed technology stack.

These guidelines will later be used by the **architecture rule generator** to enforce correct implementation patterns.

Guidelines must be derived from:

• official documentation  
• stable best practices  
• Context7 MCP sources  

The command must **not invent practices** that are not supported by official documentation.

---

# Step 1 — Load Confirmed Stack

Load:

docs/reference/stack.md

Extract the following technologies:

Frontend Framework  
Styling Framework  
State Management System  

Backend Runtime  
Backend Framework  
API Architecture  

Database  
ORM  

Authentication System  
Deployment Platform  
Testing Framework  

---

# Step 2 — Query Context7 MCP

For each detected technology:

Query **Context7 MCP** to retrieve official best practices.

Retrieve guidance for:

• project structure  
• dependency management  
• configuration patterns  
• security considerations  
• performance recommendations  
• testing practices  
• production deployment patterns  

Important rules:

Use **stable documentation patterns only**  
Ignore experimental or deprecated features  
Focus on **current major version practices**

Do NOT include raw MCP responses.

Summarize the results into concise engineering guidelines.

---

# Step 3 — Generate Guidelines

Produce a structured guideline section for each confirmed technology.

Example structure:

## Technology

Technology Name

### Recommended Usage

Brief description of recommended usage patterns.

### Architecture Patterns

Common structural patterns recommended by official documentation.

### Configuration Guidelines

Environment configuration practices.

### Security Practices

Security recommendations.

### Performance Practices

Optimization recommendations.

### Testing Guidelines

Recommended testing approaches.

---

# Step 4 — Consolidate Guidelines

Combine all technology sections into a single artifact.

Document structure:

# STACK BEST PRACTICE GUIDELINES

## Confirmed Technology Stack

Frontend  
Backend  
Database  
ORM  
Authentication  
Deployment  

---

## Frontend Guidelines

---

## Backend Guidelines

---

## Database Guidelines

---

## API Design Guidelines

---

## Security Guidelines

---

## Testing Guidelines

---

## Deployment Guidelines

---

# Step 5 — Save Artifact

Write the generated document to:

docs/reference/stack-guidelines.md

Create directory if missing.

Overwrite existing file.

---

# Completion Output

Return confirmation only:

"Stack best practice guidelines generated."



================================================
FILE: .opencode/commands/generate-ui-dependency-graph.md
================================================
---
description: Generate UI dependency graph for deterministic frontend build order
agent: plan
subtask: true
---

# Generate UI Dependency Graph

Create a dependency graph describing the correct order to generate frontend UI elements.

---

# Inputs

Read:

docs/reference/frontend-architecture.md  
docs/reference/page-wiring-graph.md

---

# Step 1 — Extract UI Elements

Identify:

Layouts  
Components  
Hooks  
Pages

---

# Step 2 — Detect Dependencies

Determine relationships.

Examples:

Layout → Page  
Component → Component  
Hook → Component  
Hook → Page

---

# Step 3 — Build Dependency Graph

Create graph structure.

Example:

Navbar  
Sidebar  
MainLayout  
ProjectCard  
ProjectList  
DashboardHeader  
DashboardPage

---

# Step 4 — Resolve Generation Order

Topologically sort the graph.

Correct order must satisfy all dependencies.

Example order:

Layouts  
Shared Components  
Nested Components  
Hooks  
Pages

---

# Output

Write dependency graph to:

docs/reference/ui-dependency-graph.md

---

# Completion Output

Return confirmation only:

"UI dependency graph generated."



================================================
FILE: .opencode/commands/implement-app.md
================================================
# /implement-app

Implements the application based on the finalized architecture and implementation plan.

This command executes the `implement-app skill`, which performs the following pipeline:

1. Validate architecture
2. Generate dependency graph
3. Initialize task scheduler
4. Scaffold project structure
5. Build database layer
6. Build backend core
7. Build frontend core
8. Generate application features

Execute the `implement-app skill` to perform the implementation phase.



================================================
FILE: .opencode/commands/stack-advisor.md
================================================
---
description: Confirm frontend stack and derive backend architecture aligned with the PRD draft and frontend architecture
agent: build
subtask: true
---

Reference:

@docs/reference/prd-draft.md
@docs/reference/frontend-architecture.md

---

# Objective

Determine the **complete full-stack architecture** of the application.

This command must:

1. Analyze the **PRD draft**
2. Analyze the **frontend architecture**
3. Infer backend requirements
4. Ask **targeted architecture questions**
5. Finalize the **technology stack**
6. Generate the **backend architecture specification**

The goal is to ensure the **backend architecture directly supports the product requirements and UI structure**.

---

# Step 1 — Load PRD Draft

Load:

docs/reference/prd-draft.md

Extract:

Product features  
User workflows  
Data entities  
Authentication needs  
Integration requirements  

Identify backend implications such as:

Persistent data storage  
User account systems  
File uploads  
Real-time features  
External integrations  

---

# Step 2 — Load Frontend Architecture

Load:

docs/reference/frontend-architecture.md

Extract:

Frontend framework  
Routing structure  
API interaction patterns  
State management approach  

Identify:

Frontend hooks  
API endpoints required  
Frontend data dependencies  

---

# Step 3 — Extract design specs 

Load:

docs/reference/frontend-design-spec.md

Extract:

Pages  
Components  
Layouts  
User interaction flows  

Use this to identify backend needs such as:

Data fetching requirements  
Search/filter operations  
User dashboards  
Content creation features  

---

# Step 4 — Infer Backend Requirements

Using the PRD and UI architecture, determine backend needs.

Example detections:

User authentication system  
CRUD APIs for entities  
File storage  
Notification systems  
Real-time communication  
Background job processing  

These inferred requirements should guide the backend stack selection.

---

# Step 5 — Confirm Frontend Stack

Display detected frontend stack.

Example:

Frontend Framework: Next.js  
Styling: TailwindCSS  
Routing: App Router  
State Management: React Hooks  

Ask the user to confirm or correct the frontend stack.

---

# Step 6 — Backend Architecture Questionnaire

Using the PRD and frontend architecture, ask targeted questions about backend design.

Ask all questions **in one output** so the user can respond in a single reply.

---

## Backend Runtime

Based on the product requirements, which runtime should power the backend?

Examples:

Node.js  
Python  
Go  
Java  

---

## Backend Framework

Which framework should be used?

Examples:

Express  
NestJS  
FastAPI  
Django  

---

## API Style

Based on the frontend data needs, which API architecture should be used?

Options:

REST  
GraphQL  
tRPC  

---

## Database

What database is best suited for the application's data model?

Examples:

PostgreSQL  
MySQL  
MongoDB  

---

## ORM / Query Layer

Which database abstraction layer should be used?

Examples:

Prisma  
Drizzle  
SQLAlchemy  

---

## Authentication Strategy

How should authentication be implemented?

Examples:

JWT tokens  
Session cookies  
OAuth providers  

---

## File Storage

Does the application require file uploads or media storage?

Examples:

S3  
Cloud storage  
Local storage  

---

## Real-Time Features

Does the application require real-time updates?

Examples:

WebSockets  
Server-Sent Events  

---

## Background Processing

Does the application require background jobs?

Examples:

Queue workers  
Task schedulers  

---

## Deployment Target

Where will the backend be deployed?

Examples:

AWS  
Vercel serverless  
Fly.io  
Docker containers  

---

## Testing Framework

Which testing framework should be used?

Examples:

Jest  
Vitest  
Pytest  

---

# Step 7 — Validate Stack Compatibility

Ensure backend choices are compatible with the frontend architecture.

Example validations:

Next.js frontend → REST or GraphQL APIs  
Serverless frontend → stateless backend services  

Flag incompatibilities and suggest alternatives.

---

# Step 8 — Generate Backend Architecture

Create a backend architecture aligned with the application requirements.

Include:

Controller layer  
Service layer  
Repository layer  
Data models  
API routing  

Example structure:
src/

controllers/
services/
repositories/
models/
routes/
middleware/
config/


---

# Step 9 — Define API Contract

Derive API endpoints from:

PRD features  
Frontend page data needs  

Example:

GET /api/projects  
POST /api/projects  
GET /api/users  

Map these endpoints to frontend hooks.

---

# Step 10 — Produce Stack Definition

Output structured architecture:

# FULL STACK ARCHITECTURE

## Frontend Stack

Framework  
Styling  
Routing  
State Management  

---

## Backend Stack

Runtime  
Framework  
Database  
ORM  
Authentication  

---

## Backend Architecture

Controllers  
Services  
Repositories  
Models  

---

## API Contract

List required endpoints.

---

## Deployment Strategy

Define infrastructure approach.

---

# Step 11 — Save Artifacts

Save stack definition:

docs/reference/stack.md

Save backend architecture:

docs/reference/backend-architecture.md

Create directories if missing.

Overwrite existing files.

---

# Completion Output

Return confirmation only:

"Stack confirmed and backend architecture generated."



================================================
FILE: .opencode/commands/ui-prompt-builder.md
================================================
---
description: Generate a UI prompt for Google Stitch using the PRD draft
agent: plan
---

Reference:

@docs/reference/prd-draft.md

---

# Objective

Generate a structured prompt that can be used with **Google Stitch UI builder** to create the application's frontend design.

The prompt must be derived from:

- PRD draft features
- user flows
- UI theme ideas
- platform constraints

The goal is to produce a **high-quality UI prompt** that results in realistic and usable UI prototypes.

---

# Step 1 — Load PRD Draft

Read:

docs/reference/prd-draft.md

Extract:

Application concept  
Target users  
Core features  
Supporting features  
Platform  
UI theme ideas  

---

# Step 2 — Determine UI Scope

Identify what type of interface the application requires.

Possible interface types:

Marketing site  
Dashboard application  
Mobile interface  
Admin panel  
Consumer product  

If unclear, ask the user.

Pause and wait for response.

---

# Step 3 — Ask UI Clarifying Questions

Ask questions one at a time.

Pause after each question.

Questions should include:

### Visual Style

What UI style should the app follow?

Examples:

Minimal SaaS  
Material design  
Glassmorphism  
Dark dashboard  

---

### Color Theme

Does the product have a brand color?

Example:

Green tech theme  
Blue enterprise theme  

---

### Navigation Style

How should users navigate the product?

Examples:

Sidebar navigation  
Top navigation  
Mobile tab navigation  

---

### Page Layout

Should the product be:

Card-based  
Table-based  
Feed-based  
Form-heavy  

---

### Primary User Flow

What is the most common action users perform?

Examples:

Create projects  
Upload content  
Search data  

---

### Mobile Considerations

Should the UI be optimized for mobile as well?

---

# Step 4 — Generate Page List

Using the PRD features, derive the required pages.

Example:

Landing page  
Login / Register  
Dashboard  
Projects  
Settings  

Each page should have:

Purpose  
Key components  

---

# Step 5 — Generate Component Suggestions

Derive reusable components.

Examples:

Navbar  
Sidebar  
Cards  
Tables  
Forms  
Modals  

---

# Step 6 — Construct Stitch Prompt

Build a structured prompt optimized for UI generation.

Format:

APP DESCRIPTION

USER TYPES

CORE FEATURES

PAGES

UI STYLE

NAVIGATION MODEL

COMPONENTS

DESIGN SYSTEM HINTS

---

# Step 7 — Save Prompt Artifact

Write prompt to:

docs/reference/stitch-ui-prompt.md

Overwrite if file exists.

---

# Completion Output

Return confirmation only:

"Stitch UI prompt generated."



================================================
FILE: .opencode/modules/buildBackendCore.js
================================================
import fs from "fs";

const ARCH_PATH = "docs/reference/backend-architecture.md";

function loadArchitecture() {
  if (!fs.existsSync(ARCH_PATH)) {
    throw new Error("backend-architecture.md missing");
  }

  return fs.readFileSync(ARCH_PATH, "utf8");
}

function extractServices(text) {
  const services = [];

  const lines = text.split("\n");

  for (const line of lines) {
    if (line.startsWith("Service:")) {
      const name = line.replace("Service:", "").trim();

      services.push(name);
    }
  }

  return services;
}

function createController(service) {
  const code = `
import ${service}Service from "../services/${service}Service.js"

export async function ${service}Controller(req, res) {

  const result = await ${service}Service(req.body)

  res.json(result)

}
`;

  fs.writeFileSync(`backend/controllers/${service}Controller.js`, code);
}

function createService(service) {
  const code = `
import ${service}Repository from "../repositories/${service}Repository.js"

export default async function ${service}Service(data) {

  return await ${service}Repository(data)

}
`;

  fs.writeFileSync(`backend/services/${service}Service.js`, code);
}

function createRepository(service) {
  const code = `
export default async function ${service}Repository(data) {

  // database logic placeholder

  return { status: "ok", service: "${service}" }

}
`;

  fs.writeFileSync(`backend/repositories/${service}Repository.js`, code);
}

function createRoute(service) {
  const code = `
import express from "express"
import { ${service}Controller } from "../controllers/${service}Controller.js"

const router = express.Router()

router.post("/", ${service}Controller)

export default router
`;

  fs.writeFileSync(`backend/routes/${service}.js`, code);
}

function createServer(services) {
  let imports = "";
  let routes = "";

  services.forEach((service) => {
    imports += `import ${service}Route from "./routes/${service}.js"\n`;
    routes += `app.use("/${service}", ${service}Route)\n`;
  });

  const code = `
import express from "express"

${imports}

const app = express()

app.use(express.json())

${routes}

app.listen(3000, () => {
  console.log("API running on port 3000")
})
`;

  fs.writeFileSync("backend/server.js", code);
}

export default async function buildBackendCore() {
  console.log("Building backend core");

  const architecture = loadArchitecture();

  const services = extractServices(architecture);

  if (services.length === 0) {
    throw new Error("No services found in backend architecture");
  }

  for (const service of services) {
    createController(service);
    createService(service);
    createRepository(service);
    createRoute(service);
  }

  createServer(services);

  console.log(`Backend core created (${services.length} services)`);
}



================================================
FILE: .opencode/modules/buildDatabase.js
================================================
import fs from "fs"
import path from "path"

const ARCH_PATH = "docs/reference/backend-architecture.md"

function loadArchitecture() {

  if (!fs.existsSync(ARCH_PATH)) {
    throw new Error("backend-architecture.md missing")
  }

  return fs.readFileSync(ARCH_PATH, "utf8")

}

function parseEntities(text) {

  const entities = []
  const lines = text.split("\n")

  let current = null

  for (const line of lines) {

    if (line.startsWith("Entity:")) {

      if (current) entities.push(current)

      current = {
        name: line.replace("Entity:", "").trim(),
        fields: []
      }

    }

    if (line.trim().startsWith("-")) {

      const field = line.replace("-", "").trim()
      const parts = field.split(" ")

      current.fields.push({
        name: parts[0],
        type: parts[1] || "TEXT"
      })

    }

  }

  if (current) entities.push(current)

  return entities

}

function generateSQL(entities) {

  let sql = ""

  for (const entity of entities) {

    sql += `CREATE TABLE ${entity.name} (\n`
    sql += `  id SERIAL PRIMARY KEY,\n`

    const fields = entity.fields.map(
      f => `  ${f.name} ${f.type}`
    )

    sql += fields.join(",\n")

    sql += `,\n  created_at TIMESTAMP\n`

    sql += ");\n\n"

  }

  return sql

}

function writeSchema(sql) {

  fs.writeFileSync("database/schema.sql", sql)

}

function writeMigration(sql) {

  const file = "database/migrations/001_initial_schema.sql"

  fs.writeFileSync(file, sql)

}

function generateModels(entities) {

  fs.mkdirSync("backend/models", { recursive: true })

  for (const entity of entities) {

    const model = `
class ${entity.name} {

  constructor(data) {
    Object.assign(this, data)
  }

}

export default ${entity.name}
`

    fs.writeFileSync(
      `backend/models/${entity.name}.js`,
      model
    )

  }

}

function writeBuildLog(count) {

  const log = `
# Database Build Log

Tables Generated: ${count}

Build Time:
${new Date().toISOString()}
`

  fs.writeFileSync(
    "docs/reference/database-build-log.md",
    log
  )

}

export default async function buildDatabase() {

  console.log("Building database layer")

  const architecture = loadArchitecture()

  const entities = parseEntities(architecture)

  if (entities.length === 0) {
    throw new Error("No entities detected in backend architecture")
  }

  const sql = generateSQL(entities)

  writeSchema(sql)

  writeMigration(sql)

  generateModels(entities)

  writeBuildLog(entities.length)

  console.log(`Database build complete (${entities.length} tables)`)

}



================================================
FILE: .opencode/modules/buildFrontendCore.js
================================================
import fs from "fs"

const FRONTEND_ARCH_PATH = "docs/reference/frontend-architecture.md"

function loadArchitecture() {

  if (!fs.existsSync(FRONTEND_ARCH_PATH)) {
    throw new Error("frontend-architecture.md missing")
  }

  return fs.readFileSync(FRONTEND_ARCH_PATH, "utf8")

}

function extractRoutes(text) {

  const routes = []
  const lines = text.split("\n")

  for (const line of lines) {

    if (line.startsWith("Route:")) {

      const route = line.replace("Route:", "").trim()

      routes.push(route)

    }

  }

  return routes

}

function routeToFile(route) {

  if (route === "/") return "index"

  return route.replace("/", "")

}

function createPage(route) {

  const name = routeToFile(route)

  const code = `
export default function ${name}Page() {

  return (
    <div>
      <h1>${name} page</h1>
    </div>
  )

}
`

  fs.writeFileSync(
    `frontend/pages/${name}.jsx`,
    code
  )

}

function createLayout() {

  const code = `
export default function MainLayout({ children }) {

  return (
    <div>

      <header>
        <h2>App</h2>
      </header>

      <main>
        {children}
      </main>

    </div>
  )

}
`

  fs.writeFileSync(
    "frontend/layouts/MainLayout.jsx",
    code
  )

}

function createComponent() {

  const code = `
export default function Button({ label, onClick }) {

  return (
    <button onClick={onClick}>
      {label}
    </button>
  )

}
`

  fs.writeFileSync(
    "frontend/components/Button.jsx",
    code
  )

}

function createHook() {

  const code = `
import { useState } from "react"

export default function useFetch(url) {

  const [data, setData] = useState(null)

  async function fetchData() {

    const res = await fetch(url)

    const json = await res.json()

    setData(json)

  }

  return { data, fetchData }

}
`

  fs.writeFileSync(
    "frontend/hooks/useFetch.js",
    code
  )

}

function createApp(routes) {

  let imports = ""
  let routeMap = ""

  routes.forEach(route => {

    const name = routeToFile(route)

    imports += `import ${name}Page from "./pages/${name}.jsx"\n`

    routeMap += `
if (path === "${route}") return <${name}Page />
`

  })

  const code = `
import React from "react"
${imports}

export default function App() {

  const path = window.location.pathname

  ${routeMap}

  return <div>404</div>

}
`

  fs.writeFileSync(
    "frontend/app.js",
    code
  )

}

export default async function buildFrontendCore() {

  console.log("Building frontend core")

  const architecture = loadArchitecture()

  const routes = extractRoutes(architecture)

  if (routes.length === 0) {
    throw new Error("No routes found in frontend architecture")
  }

  for (const route of routes) {

    createPage(route)

  }

  createLayout()

  createComponent()

  createHook()

  createApp(routes)

  console.log(`Frontend core created (${routes.length} pages)`)

}



================================================
FILE: .opencode/modules/dependencyGraph.js
================================================
import fs from "fs"

const PLAN_PATH = "docs/reference/plan.md"
const OUTPUT_PATH = "docs/reference/dependency-graph.json"

function loadPlan() {

  if (!fs.existsSync(PLAN_PATH)) {
    throw new Error("plan.md not found")
  }

  return fs.readFileSync(PLAN_PATH, "utf8")
}

function extractFeatures(planText) {

  const features = []

  const lines = planText.split("\n")

  for (const line of lines) {

    if (line.trim().startsWith("Feature")) {

      const name = line
        .replace("Feature:", "")
        .replace("Feature", "")
        .trim()

      features.push(name.toLowerCase().replace(/\s+/g, "-"))

    }

  }

  return features
}

function buildCoreTasks() {

  return [
    { id: "database", depends: [] },
    { id: "backend-core", depends: ["database"] },
    { id: "frontend-core", depends: [] }
  ]

}

function buildFeatureTasks(features) {

  const tasks = []

  for (const feature of features) {

    tasks.push({
      id: `feature-${feature}`,
      depends: ["backend-core", "frontend-core"]
    })

  }

  return tasks

}

function writeGraph(graph) {

  fs.writeFileSync(
    OUTPUT_PATH,
    JSON.stringify(graph, null, 2)
  )

}

export default async function dependencyGraph() {

  console.log("Generating dependency graph")

  const plan = loadPlan()

  const features = extractFeatures(plan)

  if (features.length === 0) {
    throw new Error("No features detected in plan.md")
  }

  const coreTasks = buildCoreTasks()

  const featureTasks = buildFeatureTasks(features)

  const graph = {
    tasks: [...coreTasks, ...featureTasks]
  }

  writeGraph(graph)

  console.log(`Dependency graph created (${graph.tasks.length} tasks)`)

  return graph

}



================================================
FILE: .opencode/modules/deployApp.js
================================================
import fs from "fs"
import { execSync } from "child_process"

const STACK_PATH = "docs/reference/stack.md"

function loadStack() {

  if (!fs.existsSync(STACK_PATH)) {
    throw new Error("stack.md missing")
  }

  return fs.readFileSync(STACK_PATH,"utf8")

}

function createDeploymentDir() {

  fs.mkdirSync("deployment",{recursive:true})

}

function createDockerfile() {

  const dockerfile = `
FROM node:20

WORKDIR /app

COPY . .

RUN npm install

EXPOSE 3000

CMD ["node","backend/server.js"]
`

  fs.writeFileSync("deployment/Dockerfile",dockerfile)

}

function createCompose() {

  const compose = `
version: "3"

services:

  app:
    build: .
    ports:
      - "3000:3000"

  database:
    image: postgres
    environment:
      POSTGRES_USER: app
      POSTGRES_PASSWORD: password
      POSTGRES_DB: app_db
    ports:
      - "5432:5432"
`

  fs.writeFileSync(
    "deployment/docker-compose.yml",
    compose
  )

}

function buildFrontend() {

  if (fs.existsSync("frontend")) {

    try {

      execSync("npm run build",{stdio:"inherit"})

    } catch {

      console.log("Frontend build skipped")

    }

  }

}

function packageApp() {

  try {

    execSync(
      "docker compose build",
      {stdio:"inherit"}
    )

  } catch {

    console.log("Docker build skipped")

  }

}

function deployApp() {

  try {

    execSync(
      "docker compose up -d",
      {stdio:"inherit"}
    )

  } catch {

    console.log("Deployment skipped")

  }

}

function writeDeploymentReport() {

  const report = `
# Deployment Report

Status: Deployment Attempted

Time:
${new Date().toISOString()}

Deployment Method:
Docker Compose
`

  fs.writeFileSync(
    "docs/reference/deployment-report.md",
    report
  )

}

export default async function deployAppModule() {

  console.log("Starting deployment process")

  loadStack()

  createDeploymentDir()

  createDockerfile()

  createCompose()

  buildFrontend()

  packageApp()

  deployApp()

  writeDeploymentReport()

  console.log("Deployment process finished")

}



================================================
FILE: .opencode/modules/featureBuilder.js
================================================
import fs from "fs"

const PLAN_PATH = "docs/reference/plan.md"

function loadPlan() {

  if (!fs.existsSync(PLAN_PATH)) {
    throw new Error("plan.md missing")
  }

  return fs.readFileSync(PLAN_PATH, "utf8")

}

function extractFeatures(planText) {

  const features = []
  const lines = planText.split("\n")

  for (const line of lines) {

    if (line.startsWith("Feature")) {

      const name = line
        .replace("Feature:", "")
        .replace("Feature", "")
        .trim()

      features.push(name)

    }

  }

  return features

}

function createBackendFeature(feature) {

  const controller = `
export async function ${feature}Feature(req,res){

  res.json({
    feature:"${feature}",
    status:"active"
  })

}
`

  fs.writeFileSync(
    `backend/controllers/${feature}FeatureController.js`,
    controller
  )

  const route = `
import express from "express"
import { ${feature}Feature } from "../controllers/${feature}FeatureController.js"

const router = express.Router()

router.get("/", ${feature}Feature)

export default router
`

  fs.writeFileSync(
    `backend/routes/${feature}Feature.js`,
    route
  )

}

function createFrontendFeature(feature) {

  const component = `
export default function ${feature}Feature(){

  async function load(){

    const res = await fetch("/api/${feature}")

    const data = await res.json()

    console.log(data)

  }

  return(

    <div>

      <h2>${feature} Feature</h2>

      <button onClick={load}>
        Load ${feature}
      </button>

    </div>

  )

}
`

  fs.writeFileSync(
    `frontend/pages/${feature}.jsx`,
    component
  )

}

function writeFeatureLog(features) {

  const log = `
# Feature Build Log

Features Built:
${features.join("\n")}

Time:
${new Date().toISOString()}
`

  fs.writeFileSync(
    "docs/reference/feature-build-log.md",
    log
  )

}

export default async function featureBuilder() {

  console.log("Building application features")

  const plan = loadPlan()

  const features = extractFeatures(plan)

  if (features.length === 0) {
    throw new Error("No features detected in plan")
  }

  for (const feature of features) {

    createBackendFeature(feature)

    createFrontendFeature(feature)

    console.log(`Feature created: ${feature}`)

  }

  writeFeatureLog(features)

  console.log(`Feature generation complete (${features.length} features)`)

}



================================================
FILE: .opencode/modules/qaValidator.js
================================================
import fs from "fs"

const PLAN_PATH = "docs/reference/plan.md"

function loadPlan() {

  if (!fs.existsSync(PLAN_PATH)) {
    throw new Error("plan.md missing")
  }

  return fs.readFileSync(PLAN_PATH,"utf8")

}

function extractFeatures(text) {

  const features = []

  const lines = text.split("\n")

  for (const line of lines) {

    if (line.startsWith("Feature")) {

      const name = line
        .replace("Feature:","")
        .replace("Feature","")
        .trim()

      features.push(name)

    }

  }

  return features

}

function getBackendRoutes() {

  if (!fs.existsSync("backend/routes")) return []

  return fs.readdirSync("backend/routes")
    .map(f => f.replace(".js",""))

}

function getFrontendPages() {

  if (!fs.existsSync("frontend/pages")) return []

  return fs.readdirSync("frontend/pages")
    .map(f => f.replace(".jsx",""))

}

function validateFeatures(features, routes, pages) {

  const missingBackend = []
  const missingFrontend = []

  for (const feature of features) {

    if (!routes.includes(feature) && !routes.includes(feature+"Feature")) {
      missingBackend.push(feature)
    }

    if (!pages.includes(feature)) {
      missingFrontend.push(feature)
    }

  }

  return {
    missingBackend,
    missingFrontend
  }

}

function writeReport(features, routes, pages, validation) {

  const status =
    validation.missingBackend.length === 0 &&
    validation.missingFrontend.length === 0
      ? "PASSED"
      : "FAILED"

  const report = `
# QA Report

Features Expected
${features.join("\n")}

Backend Routes Found
${routes.join("\n")}

Frontend Pages Found
${pages.join("\n")}

Missing Backend Routes
${validation.missingBackend.join("\n") || "None"}

Missing Frontend Pages
${validation.missingFrontend.join("\n") || "None"}

Status
${status}

Time
${new Date().toISOString()}
`

  fs.writeFileSync(
    "docs/reference/qa-report.md",
    report
  )

  return status

}

export default async function qaValidator() {

  console.log("Running QA validation")

  const plan = loadPlan()

  const features = extractFeatures(plan)

  const routes = getBackendRoutes()

  const pages = getFrontendPages()

  const validation = validateFeatures(features, routes, pages)

  const status = writeReport(
    features,
    routes,
    pages,
    validation
  )

  if (status === "FAILED") {
    throw new Error("QA validation failed")
  }

  console.log("QA validation passed")

}



================================================
FILE: .opencode/modules/scaffoldProject.js
================================================
import fs from "fs"
import path from "path"

const STACK_PATH = "docs/reference/stack.md"

function loadStack() {

  if (!fs.existsSync(STACK_PATH)) {
    throw new Error("stack.md not found")
  }

  return fs.readFileSync(STACK_PATH, "utf8")

}

function createDirectory(dir) {

  fs.mkdirSync(dir, { recursive: true })

}

function createBackendStructure() {

  const dirs = [
    "backend/controllers",
    "backend/services",
    "backend/repositories",
    "backend/routes",
    "backend/models",
    "backend/config"
  ]

  dirs.forEach(createDirectory)

}

function createFrontendStructure() {

  const dirs = [
    "frontend/pages",
    "frontend/components",
    "frontend/layouts",
    "frontend/hooks"
  ]

  dirs.forEach(createDirectory)

}

function createDatabaseStructure() {

  const dirs = [
    "database/migrations",
    "database/seeds"
  ]

  dirs.forEach(createDirectory)

}

function createTestStructure() {

  const dirs = [
    "tests/backend",
    "tests/frontend"
  ]

  dirs.forEach(createDirectory)

}

function createBaseFiles() {

  const files = {
    "backend/app.js": "// backend entry point\n",
    "frontend/app.js": "// frontend entry point\n",
    "database/README.md": "# Database Layer\n",
    "tests/README.md": "# Test Suite\n"
  }

  for (const file in files) {

    const dir = path.dirname(file)

    createDirectory(dir)

    fs.writeFileSync(file, files[file])

  }

}

export default async function scaffoldProject() {

  console.log("Scaffolding project structure")

  const stack = loadStack()

  console.log("Detected stack configuration")

  createBackendStructure()

  createFrontendStructure()

  createDatabaseStructure()

  createTestStructure()

  createBaseFiles()

  console.log("Project scaffold created")

}



================================================
FILE: .opencode/modules/taskScheduler.js
================================================
import fs from "fs"

const GRAPH_PATH = "docs/reference/dependency-graph.json"

function loadGraph() {

  if (!fs.existsSync(GRAPH_PATH)) {
    throw new Error("Dependency graph not found")
  }

  return JSON.parse(
    fs.readFileSync(GRAPH_PATH, "utf8")
  )

}

function getRunnableTasks(tasks, completed) {

  return tasks.filter(task => {

    if (completed.has(task.id)) return false

    return task.depends.every(dep => completed.has(dep))

  })

}

export default function taskScheduler(taskRegistry) {

  const graph = loadGraph()

  const completed = new Set()

  async function runTask(taskId) {

    if (!taskRegistry[taskId]) {
      throw new Error(`Task handler missing: ${taskId}`)
    }

    console.log(`Running task: ${taskId}`)

    await taskRegistry[taskId]()

    completed.add(taskId)

    console.log(`Completed: ${taskId}`)

  }

  async function run() {

    const tasks = graph.tasks

    while (completed.size < tasks.length) {

      const runnable = getRunnableTasks(tasks, completed)

      if (runnable.length === 0) {
        throw new Error("Deadlock detected in dependency graph")
      }

      await Promise.all(
        runnable.map(task => runTask(task.id))
      )

    }

    console.log("All tasks completed")

  }

  return { run }

}



================================================
FILE: .opencode/modules/testRunner.js
================================================
import fs from "fs"
import { execSync } from "child_process"

const PACKAGE_FILE = "package.json"

function run(cmd) {
  execSync(cmd, { stdio: "inherit" })
}

function ensurePackageJson() {

  if (!fs.existsSync(PACKAGE_FILE)) {

    console.log("Initializing package.json")

    run("npm init -y")

  }

}

function ensurePlaywrightInstalled() {

  const pkg = JSON.parse(fs.readFileSync(PACKAGE_FILE))

  const devDeps = pkg.devDependencies || {}

  if (!devDeps["@playwright/test"]) {

    console.log("Installing Playwright")

    run("npm install -D @playwright/test")

    run("npx playwright install")

  }

}

function ensurePlaywrightConfig() {

  if (!fs.existsSync("playwright.config.js")) {

    console.log("Creating Playwright config")

    const config = `
import { defineConfig } from '@playwright/test'

export default defineConfig({
  testDir: './tests/e2e',
  timeout: 30000,
  use: {
    baseURL: 'http://localhost:3000',
    headless: true
  }
})
`

    fs.writeFileSync("playwright.config.js", config)

  }

}

function ensureE2EDirectory() {

  fs.mkdirSync("tests/e2e", { recursive: true })

}

function updatePackageScripts() {

  const pkg = JSON.parse(fs.readFileSync(PACKAGE_FILE))

  if (!pkg.scripts) pkg.scripts = {}

  if (!pkg.scripts["test:e2e"]) {

    console.log("Adding Playwright script to package.json")

    pkg.scripts["test:e2e"] = "playwright test"

    fs.writeFileSync(
      PACKAGE_FILE,
      JSON.stringify(pkg, null, 2)
    )

  }

}

function runUnitTests() {

  if (!fs.existsSync(PACKAGE_FILE)) return

  const pkg = JSON.parse(fs.readFileSync(PACKAGE_FILE))

  if (pkg.scripts && pkg.scripts.test) {

    console.log("Running unit tests")

    run("npm test")

  }

}

function runPlaywrightTests() {

  console.log("Running Playwright E2E tests")

  run("npx playwright test")

}

export default async function testRunner() {

  console.log("Preparing test environment")

  ensurePackageJson()

  ensurePlaywrightInstalled()

  ensurePlaywrightConfig()

  ensureE2EDirectory()

  updatePackageScripts()

  console.log("Running tests")

  runUnitTests()

  runPlaywrightTests()

}



================================================
FILE: .opencode/modules/validateArchitecture.js
================================================
import fs from "fs"

const REQUIRED_FILES = [
  "docs/reference/prd.md",
  "docs/reference/plan.md",
  "docs/reference/backend-architecture.md",
  "docs/reference/frontend-architecture.md",
  "docs/reference/frontend-design-spec.md",
  "docs/reference/stack.md",
  "docs/reference/architecture-rules.md"
]

function fileExists(path) {
  return fs.existsSync(path)
}

function readFile(path) {
  return fs.readFileSync(path, "utf8")
}

function validateRequiredFiles() {

  const missing = []

  for (const file of REQUIRED_FILES) {

    if (!fileExists(file)) {
      missing.push(file)
    }

  }

  return missing

}

function validateBackendArchitecture(content) {

  const result = {
    hasEntities: false,
    hasServices: false
  }

  if (content.includes("Entity")) {
    result.hasEntities = true
  }

  if (content.includes("Service")) {
    result.hasServices = true
  }

  return result

}

function validateFrontendArchitecture(content) {

  const result = {
    hasRoutes: false,
    hasComponents: false
  }

  if (content.includes("Route")) {
    result.hasRoutes = true
  }

  if (content.includes("Component")) {
    result.hasComponents = true
  }

  return result

}

function validatePlan(content) {

  const result = {
    hasFeatures: false
  }

  if (content.includes("Feature")) {
    result.hasFeatures = true
  }

  return result

}

function writeValidationReport(report) {

  const output = `
# Architecture Validation Report

Validation Time:
${new Date().toISOString()}

## Missing Files
${report.missingFiles.length === 0 ? "None" : report.missingFiles.join("\n")}

## Backend Architecture
Entities: ${report.backend.hasEntities}
Services: ${report.backend.hasServices}

## Frontend Architecture
Routes: ${report.frontend.hasRoutes}
Components: ${report.frontend.hasComponents}

## Plan
Features Present: ${report.plan.hasFeatures}

Validation Status:
${report.status}
`

  fs.writeFileSync(
    "docs/reference/architecture-validation.md",
    output
  )

}

export default async function validateArchitecture() {

  console.log("Running architecture validation")

  const missingFiles = validateRequiredFiles()

  if (missingFiles.length > 0) {

    writeValidationReport({
      missingFiles,
      backend: {},
      frontend: {},
      plan: {},
      status: "FAILED"
    })

    throw new Error("Architecture validation failed: missing files")

  }

  const backendContent = readFile("docs/reference/backend-architecture.md")
  const frontendContent = readFile("docs/reference/frontend-architecture.md")
  const planContent = readFile("docs/reference/plan.md")

  const backend = validateBackendArchitecture(backendContent)
  const frontend = validateFrontendArchitecture(frontendContent)
  const plan = validatePlan(planContent)

  const status =
    backend.hasEntities &&
    backend.hasServices &&
    frontend.hasRoutes &&
    frontend.hasComponents &&
    plan.hasFeatures
      ? "PASSED"
      : "FAILED"

  const report = {
    missingFiles: [],
    backend,
    frontend,
    plan,
    status
  }

  writeValidationReport(report)

  if (status === "FAILED") {
    throw new Error("Architecture validation failed")
  }

  console.log("Architecture validation passed")

}



================================================
FILE: .opencode/skills/debugg/skill.md
================================================
---
name: debugger
description: |
  Systematic debugging and root cause analysis for identifying and fixing software issues.
  Use when: debugging errors, troubleshooting bugs, investigating crashes, analyzing stack traces,
  fixing broken code, or when user mentions debugging, error, bug, crash, or "not working".
---

# Debugger

You are an expert debugger who uses systematic approaches to identify and resolve software issues efficiently.

## When to Apply

Use this skill when:
- Investigating bugs or unexpected behavior
- Analyzing error messages and stack traces
- Troubleshooting performance issues
- Debugging production incidents
- Finding root causes of failures
- Analyzing crash dumps or logs
- Resolving intermittent issues

## Debugging Process

Follow this systematic approach:

### 1. **Understand the Problem**
- What is the expected behavior?
- What is the actual behavior?
- Can you reproduce it consistently?
- When did it start happening?
- What changed recently?

### 2. **Gather Information**
- Error messages and stack traces
- Log files and error logs
- Environment details (OS, versions, config)
- Input data that triggers the issue
- System state before/during/after

### 3. **Form Hypotheses**
- What are the most likely causes?
- List hypotheses from most to least probable
- Consider: logic errors, data issues, environment, timing, dependencies

### 4. **Test Hypotheses**
- Use binary search to narrow down location
- Add logging/print statements strategically
- Use debugger breakpoints
- Isolate components
- Test with minimal reproduction case

### 5. **Identify Root Cause**
- Don't stop at symptoms - find the real cause
- Verify with evidence
- Understand why it wasn't caught earlier

### 6. **Fix and Verify**
- Implement fix
- Test the fix thoroughly
- Ensure no regressions
- Add tests to prevent recurrence

## Debugging Strategies

### Binary Search
```
1. Identify code region (start → end)
2. Check middle point
3. If bug present → search left half
4. If bug absent → search right half
5. Repeat until isolated
```

### Rubber Duck Debugging
- Explain the code line by line
- Often reveals the issue through verbalization
- Clarifies assumptions

### Add Strategic Logging
```python
# At function entry
print(f"[DEBUG] function_name called with: {args}")

# At decision points
print(f"[DEBUG] Condition X is {condition_result}")

# Before/after state changes
print(f"[DEBUG] Before: {state}, After: {new_state}")
```

### Bisect Method (for regressions)
```bash
# Find which commit introduced the bug
git bisect start
git bisect bad HEAD
git bisect good <last-known-good-commit>
# Test each revision until found
```

## Common Bug Patterns

### Off-by-One Errors
- Loop indices (`i < n` vs `i <= n`)
- Array bounds (`arr[len(arr)]` instead of `arr[len(arr)-1]`)

### Null/Undefined References
- Check variables before use
- Verify API responses have expected fields

### Race Conditions
- Async operations completing in unexpected order
- Shared state without proper locking

### Type Mismatches
- String vs number comparisons
- Implicit type coercion issues

### Stale State
- Cached values not updated
- Closure capturing old variables

## Output Format

Structure debugging analysis as:

```markdown
## Problem Statement
[Clear description of the issue]

## Environment
- [Relevant version/config info]

## Error Analysis
[Error message/stack trace analysis]

## Hypotheses (Priority Order)
1. **[Most Likely]**: [Reasoning]
2. **[Second Most Likely]**: [Reasoning]
3. **[Less Likely]**: [Reasoning]

## Investigation Steps
1. [What to check first]
2. [How to verify hypothesis]
3. [Next steps based on results]

## Root Cause
[Once identified, explain the underlying issue]

## Fix
[Specific code changes needed]

## Prevention
[How to avoid this in the future]
```

## Example

**User Report:** "My API returns 500 errors randomly"

**Debugging Response:**

## Problem Statement
API endpoint returns HTTP 500 errors intermittently. Not all requests fail - some succeed.

## Environment
- Node.js version? 
- Database type?
- Request rate/concurrency?

## Error Analysis
Need to see:
1. Full error stack trace
2. Server logs around failure time
3. Example request that fails

## Hypotheses (Priority Order)

1. **Database Connection Pool Exhausted**: Intermittent nature suggests resource contention
   - Check if failures correlate with high traffic
   - Verify connection pool size vs concurrent requests

2. **Async Operation Not Awaited**: Race condition in code
   - Review async/await usage
   - Check for missing await keywords

3. **Unhandled Promise Rejection**: Some error paths not caught
   - Search for promises without .catch() or try/catch

## Investigation Steps

1. **Add Detailed Logging**
   ```javascript
   app.post('/api/endpoint', async (req, res) => {
     console.log('[DEBUG] Request received:', req.body);
     try {
       const result = await someOperation();
       console.log('[DEBUG] Operation succeeded');
       res.json(result);
     } catch (error) {
       console.error('[ERROR] Operation failed:', error.stack);
       res.status(500).json({ error: error.message });
     }
   });
   ```

2. **Monitor Connection Pool**
   ```javascript
   db.on('acquire', () => {
     console.log(`[POOL] Connection acquired (${db.pool.size}/${db.pool.max})`);
   });
   ```

3. **Check for Unhandled Rejections**
   ```javascript
   process.on('unhandledRejection', (reason, promise) => {
     console.error('[FATAL] Unhandled Promise Rejection:', reason);
   });
   ```

## Next Steps
Deploy logging changes and monitor for patterns in:
- Time of day
- Specific user data
- Server resource usage (CPU, memory, connections)



================================================
FILE: .opencode/skills/implement-app/orchestrator.js
================================================
import validateArchitecture from "./modules/validateArchitecture.js"
import dependencyGraph from "./modules/dependencyGraph.js"
import taskScheduler from "./modules/taskScheduler.js"

import scaffoldProject from "./modules/scaffoldProject.js"
import buildDatabase from "./modules/buildDatabase.js"
import buildBackendCore from "./modules/buildBackendCore.js"
import buildFrontendCore from "./modules/buildFrontendCore.js"
import featureBuilder from "./modules/featureBuilder.js"

export default async function runImplementApp() {

  console.log("Starting implement-app skill")

  // STEP 1
  await validateArchitecture()

  // STEP 2
  await dependencyGraph()

  // STEP 3
  const taskRegistry = {
    database: buildDatabase,
    "backend-core": buildBackendCore,
    "frontend-core": buildFrontendCore,
    features: featureBuilder
  }

  const scheduler = taskScheduler(taskRegistry)

  // STEP 4
  await scaffoldProject()

  // STEP 5–8
  await scheduler.run()

  console.log("Implementation pipeline complete")

}



================================================
FILE: .opencode/skills/implement-app/skill.md
================================================
# implement-app

Implements the application using the finalized architecture and implementation plan.

The skill orchestrates the following pipeline:

1. validateArchitecture
2. dependencyGraph
3. taskScheduler
4. scaffoldProject
5. buildDatabase
6. buildBackendCore
7. buildFrontendCore
8. featureBuilder

Execution is handled by the orchestrator.



================================================
FILE: .opencode/skills/validate-build/orchestrator.js
================================================
import testRunner from "./modules/testRunner.js"
import qaValidator from "./modules/qaValidator.js"

export default async function runValidation() {

  console.log("Starting validation pipeline")

  console.log("Step 9: Running test suite")
  await testRunner()

  console.log("Step 10: Running QA validation")
  await qaValidator()

  console.log("Validation pipeline complete")

}



================================================
FILE: .opencode/skills/validate-build/skill.md
================================================
# validate-build

Runs the validation phase after application implementation.

This skill performs the following pipeline:

1. testRunner  
2. qaValidator  

Purpose:

- generate automated backend and frontend tests
- execute the test suite
- validate that generated features match the implementation plan
- ensure architecture rules are satisfied before deployment

The skill uses an orchestrator to run the modules responsible for each step.
