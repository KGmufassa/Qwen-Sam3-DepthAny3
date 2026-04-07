# Repository Breakdown: kgmufassa-parallax-story-board

## Overview
- Total Files Detected: 198
- Total Files Processed: 198
- Processing Mode: Deep
- Goal: General understanding

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

## Tech Stack
- Languages: javascript, json, markdown, prisma, rtf, sql, text, tsx, typescript
- Tools: next, next-auth, pino, prisma, react, typescript, vitest, zod
- Runtime: Node.js, PostgreSQL (via Prisma)

## File Breakdown

### eslint.config.mjs

- **Type:** tool-config
- **Role:** supporting source file
- **Priority:** medium

- **Summary:**
Serves as supporting source file for `eslint.config.mjs`; leading content starts with `import { dirname } from "node:path"`.

- **Key Elements:**
  - const __filename
  - const __dirname
  - const compat
  - const config

- **Dependencies:**
  - @eslint/eslintrc
  - node:path
  - node:url

### next.config.ts

- **Type:** tool-config
- **Role:** supporting source file
- **Priority:** high

- **Summary:**
Serves as supporting source file for `next.config.ts`; leading content starts with `import type { NextConfig } from "next"`.

- **Key Elements:**
  - None detected

- **Dependencies:**
  - next

### package.json

- **Type:** package-manifest
- **Role:** package manifest and scripts
- **Priority:** high

- **Summary:**
Defines project metadata, npm scripts (build, clean, dev, lint, prebuild, predev), and 16 tracked dependencies for the application stack.

- **Key Elements:**
  - None detected

- **Dependencies:**
  - None detected

### tsconfig.json

- **Type:** tool-config
- **Role:** supporting source file
- **Priority:** high

- **Summary:**
Serves as supporting source file for `tsconfig.json`; leading content starts with `{`.

- **Key Elements:**
  - None detected

- **Dependencies:**
  - None detected

### vitest.config.ts

- **Type:** tool-config
- **Role:** supporting source file
- **Priority:** medium

- **Summary:**
Serves as supporting source file for `vitest.config.ts`; leading content starts with `import { defineConfig } from "vitest/config"`.

- **Key Elements:**
  - None detected

- **Dependencies:**
  - node:url
  - vitest/config

### prisma/schema.prisma

- **Type:** database-schema
- **Role:** database schema definition
- **Priority:** high

- **Summary:**
Defines the Prisma data model, enums, and database relationships used throughout the application.

- **Key Elements:**
  - enum AuthProvider
  - enum ProjectStatus
  - enum SceneStatus
  - enum AssetType
  - enum JobType
  - enum JobStatus
  - enum ExportStatus

- **Dependencies:**
  - None detected

### src/auth.ts

- **Type:** source-file
- **Role:** supporting source file
- **Priority:** high

- **Summary:**
Serves as supporting source file for `src/auth.ts`; leading content starts with `import bcrypt from "bcryptjs"`.

- **Key Elements:**
  - const env
  - const user
  - const passwordMatches
  - const dbUser

- **Dependencies:**
  - src/config/env.ts
  - src/modules/auth/repository.ts
  - bcryptjs
  - next-auth
  - next-auth/providers
  - next-auth/providers/credentials
  - next-auth/providers/google

### src/app/layout.tsx

- **Type:** app-layout
- **Role:** application shell layout
- **Priority:** high

- **Summary:**
Defines the shared Next.js application shell and wraps all routed pages with common layout concerns.

- **Key Elements:**
  - function RootLayout

- **Dependencies:**
  - next
  - react

### src/app/page.tsx

- **Type:** app-page
- **Role:** primary landing entry page
- **Priority:** high

- **Summary:**
Renders the `src/app/page.tsx` route in the Next.js App Router and composes feature-level UI for that screen.

- **Key Elements:**
  - function HomePage

- **Dependencies:**
  - src/features/marketing/components/landing-page.tsx

### src/app/api/auth/[...nextauth]/route.ts

- **Type:** api-route
- **Role:** HTTP route handler
- **Priority:** high

- **Summary:**
Implements the route handler for `src/app/api/auth/[...nextauth]/route.ts` and bridges Next.js requests into controller or module logic.

- **Key Elements:**
  - None detected

- **Dependencies:**
  - src/auth.ts

### src/app/api/v1/assets/[...assetPath]/route.ts

- **Type:** api-route
- **Role:** HTTP route handler
- **Priority:** high

- **Summary:**
Implements the route handler for `src/app/api/v1/assets/[...assetPath]/route.ts` and bridges Next.js requests into controller or module logic.

- **Key Elements:**
  - function contentTypeForAssetPath
  - component GET
  - const encodedAssetPath
  - const assetPath
  - const asset

- **Dependencies:**
  - src/core/http/route-handler.ts
  - src/modules/assets/index.ts
  - next/server

### src/app/api/v1/auth/register/route.ts

- **Type:** api-route
- **Role:** HTTP route handler
- **Priority:** high

- **Summary:**
Implements the route handler for `src/app/api/v1/auth/register/route.ts` and bridges Next.js requests into controller or module logic.

- **Key Elements:**
  - component POST
  - const requestId

- **Dependencies:**
  - src/core/http/route-handler.ts
  - src/infrastructure/rate-limit/memory-rate-limiter.ts
  - src/interfaces/http/controllers/auth-controller.ts

### src/app/api/v1/auth/session/route.ts

- **Type:** api-route
- **Role:** HTTP route handler
- **Priority:** high

- **Summary:**
Implements the route handler for `src/app/api/v1/auth/session/route.ts` and bridges Next.js requests into controller or module logic.

- **Key Elements:**
  - component GET

- **Dependencies:**
  - src/core/http/route-handler.ts
  - src/interfaces/http/controllers/auth-controller.ts

### src/app/api/v1/guest-sessions/route.ts

- **Type:** api-route
- **Role:** HTTP route handler
- **Priority:** high

- **Summary:**
Implements the route handler for `src/app/api/v1/guest-sessions/route.ts` and bridges Next.js requests into controller or module logic.

- **Key Elements:**
  - component POST
  - const requestId

- **Dependencies:**
  - src/core/http/route-handler.ts
  - src/infrastructure/rate-limit/memory-rate-limiter.ts
  - src/interfaces/http/controllers/guest-session-controller.ts

### src/app/api/v1/health/live/route.ts

- **Type:** api-route
- **Role:** HTTP route handler
- **Priority:** high

- **Summary:**
Implements the route handler for `src/app/api/v1/health/live/route.ts` and bridges Next.js requests into controller or module logic.

- **Key Elements:**
  - component GET

- **Dependencies:**
  - src/core/http/route-handler.ts
  - src/interfaces/http/controllers/health-controller.ts

### src/app/api/v1/health/ready/route.ts

- **Type:** api-route
- **Role:** HTTP route handler
- **Priority:** high

- **Summary:**
Implements the route handler for `src/app/api/v1/health/ready/route.ts` and bridges Next.js requests into controller or module logic.

- **Key Elements:**
  - component GET

- **Dependencies:**
  - src/core/http/route-handler.ts
  - src/interfaces/http/controllers/health-controller.ts

### src/app/api/v1/internal/maintenance/cleanup/route.ts

- **Type:** api-route
- **Role:** HTTP route handler
- **Priority:** high

- **Summary:**
Implements the route handler for `src/app/api/v1/internal/maintenance/cleanup/route.ts` and bridges Next.js requests into controller or module logic.

- **Key Elements:**
  - component POST

- **Dependencies:**
  - src/core/http/route-handler.ts
  - src/interfaces/http/controllers/maintenance-controller.ts
  - src/interfaces/http/support/internal-maintenance.ts

### src/app/api/v1/internal/maintenance/recover-timeouts/route.ts

- **Type:** api-route
- **Role:** HTTP route handler
- **Priority:** high

- **Summary:**
Implements the route handler for `src/app/api/v1/internal/maintenance/recover-timeouts/route.ts` and bridges Next.js requests into controller or module logic.

- **Key Elements:**
  - component POST

- **Dependencies:**
  - src/core/http/route-handler.ts
  - src/interfaces/http/controllers/maintenance-controller.ts
  - src/interfaces/http/support/internal-maintenance.ts

### src/app/api/v1/projects/route.ts

- **Type:** api-route
- **Role:** HTTP route handler
- **Priority:** high

- **Summary:**
Implements the route handler for `src/app/api/v1/projects/route.ts` and bridges Next.js requests into controller or module logic.

- **Key Elements:**
  - function requestIdentifier
  - component GET
  - component POST

- **Dependencies:**
  - src/core/http/route-handler.ts
  - src/infrastructure/rate-limit/memory-rate-limiter.ts
  - src/interfaces/http/controllers/project-controller.ts

### src/app/api/v1/projects/[projectId]/route.ts

- **Type:** api-route
- **Role:** HTTP route handler
- **Priority:** high

- **Summary:**
Implements the route handler for `src/app/api/v1/projects/[projectId]/route.ts` and bridges Next.js requests into controller or module logic.

- **Key Elements:**
  - component GET
  - component PATCH
  - component DELETE
  - const projectId

- **Dependencies:**
  - src/core/http/route-handler.ts
  - src/infrastructure/rate-limit/memory-rate-limiter.ts
  - src/interfaces/http/controllers/project-controller.ts

### src/app/api/v1/projects/[projectId]/claim/route.ts

- **Type:** api-route
- **Role:** HTTP route handler
- **Priority:** high

- **Summary:**
Implements the route handler for `src/app/api/v1/projects/[projectId]/claim/route.ts` and bridges Next.js requests into controller or module logic.

- **Key Elements:**
  - component POST
  - const segments
  - const projectId

- **Dependencies:**
  - src/core/http/route-handler.ts
  - src/infrastructure/rate-limit/memory-rate-limiter.ts
  - src/interfaces/http/controllers/project-controller.ts

### src/app/api/v1/projects/[projectId]/preview/playback/route.ts

- **Type:** api-route
- **Role:** HTTP route handler
- **Priority:** high

- **Summary:**
Implements the route handler for `src/app/api/v1/projects/[projectId]/preview/playback/route.ts` and bridges Next.js requests into controller or module logic.

- **Key Elements:**
  - component GET
  - const segments
  - const projectId
  - const reducedMotion

- **Dependencies:**
  - src/core/http/route-handler.ts
  - src/infrastructure/rate-limit/memory-rate-limiter.ts
  - src/interfaces/http/controllers/preview-controller.ts

### src/app/api/v1/projects/[projectId]/preview/status/route.ts

- **Type:** api-route
- **Role:** HTTP route handler
- **Priority:** high

- **Summary:**
Implements the route handler for `src/app/api/v1/projects/[projectId]/preview/status/route.ts` and bridges Next.js requests into controller or module logic.

- **Key Elements:**
  - component GET
  - const segments
  - const projectId

- **Dependencies:**
  - src/core/http/route-handler.ts
  - src/infrastructure/rate-limit/memory-rate-limiter.ts
  - src/interfaces/http/controllers/preview-controller.ts

### src/app/api/v1/projects/[projectId]/scenes/reorder/route.ts

- **Type:** api-route
- **Role:** HTTP route handler
- **Priority:** high

- **Summary:**
Implements the route handler for `src/app/api/v1/projects/[projectId]/scenes/reorder/route.ts` and bridges Next.js requests into controller or module logic.

- **Key Elements:**
  - component POST
  - const segments
  - const projectId

- **Dependencies:**
  - src/core/http/route-handler.ts
  - src/infrastructure/rate-limit/memory-rate-limiter.ts
  - src/interfaces/http/controllers/project-controller.ts

### src/app/api/v1/projects/[projectId]/uploads/finalize/route.ts

- **Type:** api-route
- **Role:** HTTP route handler
- **Priority:** high

- **Summary:**
Implements the route handler for `src/app/api/v1/projects/[projectId]/uploads/finalize/route.ts` and bridges Next.js requests into controller or module logic.

- **Key Elements:**
  - component POST
  - const segments
  - const projectId

- **Dependencies:**
  - src/core/http/route-handler.ts
  - src/infrastructure/rate-limit/memory-rate-limiter.ts
  - src/interfaces/http/controllers/scene-controller.ts

### src/app/api/v1/projects/[projectId]/uploads/init/route.ts

- **Type:** api-route
- **Role:** HTTP route handler
- **Priority:** high

- **Summary:**
Implements the route handler for `src/app/api/v1/projects/[projectId]/uploads/init/route.ts` and bridges Next.js requests into controller or module logic.

- **Key Elements:**
  - component POST
  - const segments
  - const projectId

- **Dependencies:**
  - src/core/http/route-handler.ts
  - src/infrastructure/rate-limit/memory-rate-limiter.ts
  - src/interfaces/http/controllers/upload-controller.ts

### src/app/api/v1/scenes/[sceneId]/route.ts

- **Type:** api-route
- **Role:** HTTP route handler
- **Priority:** high

- **Summary:**
Implements the route handler for `src/app/api/v1/scenes/[sceneId]/route.ts` and bridges Next.js requests into controller or module logic.

- **Key Elements:**
  - component PATCH
  - component DELETE
  - const sceneId

- **Dependencies:**
  - src/core/http/route-handler.ts
  - src/infrastructure/rate-limit/memory-rate-limiter.ts
  - src/interfaces/http/controllers/scene-controller.ts

### src/app/api/v1/scenes/[sceneId]/regenerate/route.ts

- **Type:** api-route
- **Role:** HTTP route handler
- **Priority:** high

- **Summary:**
Implements the route handler for `src/app/api/v1/scenes/[sceneId]/regenerate/route.ts` and bridges Next.js requests into controller or module logic.

- **Key Elements:**
  - component POST
  - const sceneId

- **Dependencies:**
  - src/core/http/route-handler.ts
  - src/infrastructure/rate-limit/memory-rate-limiter.ts
  - src/interfaces/http/controllers/scene-controller.ts

### src/app/api/v1/scenes/[sceneId]/retry/route.ts

- **Type:** api-route
- **Role:** HTTP route handler
- **Priority:** high

- **Summary:**
Implements the route handler for `src/app/api/v1/scenes/[sceneId]/retry/route.ts` and bridges Next.js requests into controller or module logic.

- **Key Elements:**
  - component POST
  - const sceneId

- **Dependencies:**
  - src/core/http/route-handler.ts
  - src/infrastructure/rate-limit/memory-rate-limiter.ts
  - src/interfaces/http/controllers/scene-controller.ts

### src/app/api/v1/uploads/[uploadToken]/route.ts

- **Type:** api-route
- **Role:** HTTP route handler
- **Priority:** high

- **Summary:**
Implements the route handler for `src/app/api/v1/uploads/[uploadToken]/route.ts` and bridges Next.js requests into controller or module logic.

- **Key Elements:**
  - component PUT
  - const uploadToken
  - const verified
  - const content

- **Dependencies:**
  - src/core/errors/app-error.ts
  - src/core/http/route-handler.ts
  - src/lib/api-response.ts
  - src/modules/assets/index.ts
  - src/modules/uploads/index.ts

### src/app/login/page.tsx

- **Type:** app-page
- **Role:** supporting source file
- **Priority:** medium

- **Summary:**
Renders the `src/app/login/page.tsx` route in the Next.js App Router and composes feature-level UI for that screen.

- **Key Elements:**
  - function LoginPage
  - type LoginPageProps
  - const env
  - const params

- **Dependencies:**
  - src/config/env.ts
  - src/features/auth/components/auth-page.tsx

### src/app/projects/page.tsx

- **Type:** app-page
- **Role:** supporting source file
- **Priority:** medium

- **Summary:**
Renders the `src/app/projects/page.tsx` route in the Next.js App Router and composes feature-level UI for that screen.

- **Key Elements:**
  - function ProjectsPage

- **Dependencies:**
  - src/features/projects/components/projects-dashboard-page.tsx

### src/app/projects/[projectId]/editor/page.tsx

- **Type:** app-page
- **Role:** supporting source file
- **Priority:** medium

- **Summary:**
Renders the `src/app/projects/[projectId]/editor/page.tsx` route in the Next.js App Router and composes feature-level UI for that screen.

- **Key Elements:**
  - function ProjectEditorRoute
  - type EditorPageProps

- **Dependencies:**
  - src/features/projects/components/project-editor-page.tsx

### src/app/projects/[projectId]/preview/page.tsx

- **Type:** app-page
- **Role:** supporting source file
- **Priority:** medium

- **Summary:**
Renders the `src/app/projects/[projectId]/preview/page.tsx` route in the Next.js App Router and composes feature-level UI for that screen.

- **Key Elements:**
  - function ProjectPreviewRoute
  - type PreviewPageProps

- **Dependencies:**
  - src/features/preview/components/project-preview-page.tsx

### src/app/projects/new/page.tsx

- **Type:** app-page
- **Role:** supporting source file
- **Priority:** medium

- **Summary:**
Renders the `src/app/projects/new/page.tsx` route in the Next.js App Router and composes feature-level UI for that screen.

- **Key Elements:**
  - function NewProjectRoute

- **Dependencies:**
  - src/features/projects/components/new-project-page.tsx

### src/app/settings/page.tsx

- **Type:** app-page
- **Role:** supporting source file
- **Priority:** medium

- **Summary:**
Renders the `src/app/settings/page.tsx` route in the Next.js App Router and composes feature-level UI for that screen.

- **Key Elements:**
  - function SettingsRoute

- **Dependencies:**
  - src/features/settings/components/settings-page.tsx

### src/app/signup/page.tsx

- **Type:** app-page
- **Role:** supporting source file
- **Priority:** medium

- **Summary:**
Renders the `src/app/signup/page.tsx` route in the Next.js App Router and composes feature-level UI for that screen.

- **Key Elements:**
  - function SignupPage
  - type SignupPageProps
  - const env
  - const params

- **Dependencies:**
  - src/config/env.ts
  - src/features/auth/components/auth-page.tsx

### src/config/constants.ts

- **Type:** source-file
- **Role:** runtime configuration
- **Priority:** medium

- **Summary:**
Centralizes runtime configuration and environment-driven application settings.

- **Key Elements:**
  - component API_VERSION
  - component DEFAULT_PROJECT_OUTPUT_FORMAT
  - component UPLOAD_BASE_PATH
  - component DEFAULT_SCENE_LAYER_COUNT
  - component DEFAULT_SCENE_DURATION_MS
  - component DEFAULT_SCENE_OVERLAP_MS

- **Dependencies:**
  - None detected

### src/config/env.ts

- **Type:** source-file
- **Role:** runtime configuration
- **Priority:** medium

- **Summary:**
Centralizes runtime configuration and environment-driven application settings.

- **Key Elements:**
  - function resetEnvCache
  - function getEnv
  - function envIsConfigured
  - function getAuthConfigEnv
  - type AppEnv
  - const envSchema
  - const parsed
  - const issues

- **Dependencies:**
  - zod

### src/core/errors/app-error.ts

- **Type:** source-file
- **Role:** cross-cutting infrastructure
- **Priority:** medium

- **Summary:**
Provides shared cross-cutting behavior used across multiple layers of the application.

- **Key Elements:**
  - function isAppError
  - class AppError

- **Dependencies:**
  - None detected

### src/core/errors/error-response.ts

- **Type:** source-file
- **Role:** cross-cutting infrastructure
- **Priority:** medium

- **Summary:**
Provides shared cross-cutting behavior used across multiple layers of the application.

- **Key Elements:**
  - function toErrorResponse

- **Dependencies:**
  - src/core/errors/app-error.ts
  - src/core/request/context.ts
  - @prisma/client
  - next/server
  - zod

### src/core/http/route-handler.ts

- **Type:** source-file
- **Role:** cross-cutting infrastructure
- **Priority:** medium

- **Summary:**
Provides shared cross-cutting behavior used across multiple layers of the application.

- **Key Elements:**
  - function defineRoute
  - function route
  - type RouteCallback
  - const context
  - const logger
  - const startedAt
  - const response

- **Dependencies:**
  - src/core/errors/error-response.ts
  - src/core/logging/logger.ts
  - src/core/request/context.ts
  - next/server

### src/core/logging/logger.ts

- **Type:** source-file
- **Role:** cross-cutting infrastructure
- **Priority:** medium

- **Summary:**
Provides shared cross-cutting behavior used across multiple layers of the application.

- **Key Elements:**
  - function getLogger
  - const env

- **Dependencies:**
  - src/config/env.ts
  - pino

### src/core/observability/metrics.ts

- **Type:** source-file
- **Role:** cross-cutting infrastructure
- **Priority:** medium

- **Summary:**
Provides shared cross-cutting behavior used across multiple layers of the application.

- **Key Elements:**
  - function ensureMetric
  - type MetricName
  - type MetricEntry
  - const store
  - const existing
  - const initial
  - const metrics
  - const metric

- **Dependencies:**
  - None detected

### src/core/observability/processing-log.ts

- **Type:** source-file
- **Role:** cross-cutting infrastructure
- **Priority:** medium

- **Summary:**
Provides shared cross-cutting behavior used across multiple layers of the application.

- **Key Elements:**
  - function logProcessingEvent
  - type ProcessingLogInput
  - const logger

- **Dependencies:**
  - src/core/logging/logger.ts

### src/core/request/context.ts

- **Type:** source-file
- **Role:** cross-cutting infrastructure
- **Priority:** medium

- **Summary:**
Provides shared cross-cutting behavior used across multiple layers of the application.

- **Key Elements:**
  - function randomId
  - function buildRequestContext
  - type RequestContext
  - const headerStore
  - const correlationId

- **Dependencies:**
  - next/headers

### src/core/security/cookies.ts

- **Type:** source-file
- **Role:** cross-cutting infrastructure
- **Priority:** medium

- **Summary:**
Provides shared cross-cutting behavior used across multiple layers of the application.

- **Key Elements:**
  - component COOKIE_MAX_AGE_SECONDS

- **Dependencies:**
  - None detected

### src/features/auth/components/auth-page.tsx

- **Type:** component
- **Role:** UI component
- **Priority:** medium

- **Summary:**
Provides reusable UI building blocks for the feature or page that owns this component.

- **Key Elements:**
  - function parseJsonResponse
  - function AuthPage
  - function handleSubmit
  - type AuthPageProps
  - type RegisterResponse
  - type ApiErrorEnvelope
  - const payload
  - const router

- **Dependencies:**
  - src/features/shared/components/app-header.tsx
  - src/features/shared/components/app-icon.tsx
  - next
  - next-auth/react
  - next/link
  - next/navigation
  - react

### src/features/marketing/components/landing-page.tsx

- **Type:** component
- **Role:** UI component
- **Priority:** medium

- **Summary:**
Provides reusable UI building blocks for the feature or page that owns this component.

- **Key Elements:**
  - function LandingPage
  - const footerProductLinks
  - const footerResourceLinks

- **Dependencies:**
  - src/features/shared/components/app-header.tsx
  - src/features/shared/components/app-icon.tsx
  - next
  - next/link

### src/features/preview/components/playback-scene-renderer.tsx

- **Type:** component
- **Role:** UI component
- **Priority:** medium

- **Summary:**
Provides reusable UI building blocks for the feature or page that owns this component.

- **Key Elements:**
  - function clampProgress
  - function applyEasing
  - function interpolate
  - function toGroupedProgress
  - function toOffset
  - function toFlatImageTransform
  - function PlaybackSceneRenderer
  - type PlaybackSceneRendererProps

- **Dependencies:**
  - src/features/preview/lib/playback-client.ts
  - react

### src/features/preview/components/project-preview-page.tsx

- **Type:** component
- **Role:** UI component
- **Priority:** medium

- **Summary:**
Provides reusable UI building blocks for the feature or page that owns this component.

- **Key Elements:**
  - function ProjectPreviewPage
  - function loadPreview
  - type ProjectPreviewPageProps
  - type PreviewState
  - const playback
  - const previewCountLabel

- **Dependencies:**
  - src/features/preview/components/playback-scene-renderer.tsx
  - src/features/preview/lib/playback-client.ts
  - src/features/shared/components/app-header.tsx
  - next
  - next/link
  - react

### src/features/preview/lib/playback-client.ts

- **Type:** source-file
- **Role:** supporting source file
- **Priority:** medium

- **Summary:**
Serves as supporting source file for `src/features/preview/lib/playback-client.ts`; leading content starts with `import type { EasingKey, GroupKey, MobileGroupScrollMapping, SceneGroupingConfig } from "@/modules/scenes/types"`.

- **Key Elements:**
  - function isRenderableImageUrl
  - function resolveProjectSceneImage
  - function parseApiResponse
  - function normalizeProject
  - function normalizePlayback
  - function formatSceneTitle
  - function formatSceneDetail
  - function resolveLayerAssets

- **Dependencies:**
  - src/modules/scenes/types.ts

### src/features/projects/mock-projects.ts

- **Type:** source-file
- **Role:** supporting source file
- **Priority:** medium

- **Summary:**
Serves as supporting source file for `src/features/projects/mock-projects.ts`; leading content starts with `export type MockProjectScene = {`.

- **Key Elements:**
  - function getMockProjectById
  - function isMockProjectId
  - type MockProjectScene
  - type MockProject

- **Dependencies:**
  - None detected

### src/features/projects/components/new-project-form.tsx

- **Type:** component
- **Role:** UI component
- **Priority:** medium

- **Summary:**
Provides reusable UI building blocks for the feature or page that owns this component.

- **Key Elements:**
  - function readImageDimensions
  - function parseJsonResponse
  - function reorderItems
  - function NewProjectForm
  - function handleFileSelection
  - function removeQueueItem
  - function ensureGuestSession
  - function createProject

- **Dependencies:**
  - src/features/shared/components/app-icon.tsx
  - next/link
  - next/navigation
  - react

### src/features/projects/components/new-project-page.tsx

- **Type:** component
- **Role:** UI component
- **Priority:** medium

- **Summary:**
Provides reusable UI building blocks for the feature or page that owns this component.

- **Key Elements:**
  - function NewProjectPage

- **Dependencies:**
  - src/features/projects/components/new-project-form.tsx
  - src/features/shared/components/app-header.tsx

### src/features/projects/components/project-card.tsx

- **Type:** component
- **Role:** UI component
- **Priority:** medium

- **Summary:**
Provides reusable UI building blocks for the feature or page that owns this component.

- **Key Elements:**
  - function ProjectCard
  - type ProjectCardProps
  - const cardClassName

- **Dependencies:**
  - src/features/shared/components/app-icon.tsx
  - next
  - next/link

### src/features/projects/components/project-editor-page.tsx

- **Type:** component
- **Role:** UI component
- **Priority:** medium

- **Summary:**
Provides reusable UI building blocks for the feature or page that owns this component.

- **Key Elements:**
  - function cloneGroupingConfig
  - function sortLayerIndexes
  - function buildAutoGroupingFromScene
  - function ensureSceneGrouping
  - function readImageDimensions
  - function parseJsonResponse
  - function ensureGuestSession
  - function ProjectEditorPage

- **Dependencies:**
  - src/features/preview/components/playback-scene-renderer.tsx
  - src/features/preview/lib/playback-client.ts
  - src/features/shared/components/app-header.tsx
  - src/features/shared/components/app-icon.tsx
  - src/modules/scenes/types.ts
  - next
  - next/link
  - react

### src/features/projects/components/projects-dashboard-page.tsx

- **Type:** component
- **Role:** UI component
- **Priority:** medium

- **Summary:**
Provides reusable UI building blocks for the feature or page that owns this component.

- **Key Elements:**
  - function mapProjectToDashboardProject
  - function isRenderableImageUrl
  - function formatUpdatedAt
  - function resolveProjectImage
  - function normalizeProjects
  - function parseJsonResponse
  - function ensureGuestSession
  - function ProjectsDashboardPage

- **Dependencies:**
  - src/features/projects/components/project-card.tsx
  - src/features/shared/components/app-header.tsx
  - src/features/shared/components/app-icon.tsx
  - next
  - next/link
  - react

### src/features/scenes/components/scene-rail.tsx

- **Type:** component
- **Role:** UI component
- **Priority:** medium

- **Summary:**
Provides reusable UI building blocks for the feature or page that owns this component.

- **Key Elements:**
  - function SceneRail
  - const scenes

- **Dependencies:**
  - None detected

### src/features/settings/components/settings-page.tsx

- **Type:** component
- **Role:** UI component
- **Priority:** medium

- **Summary:**
Provides reusable UI building blocks for the feature or page that owns this component.

- **Key Elements:**
  - function SettingsPage

- **Dependencies:**
  - src/features/shared/components/app-header.tsx

### src/features/shared/components/app-header.tsx

- **Type:** component
- **Role:** UI component
- **Priority:** medium

- **Summary:**
Provides reusable UI building blocks for the feature or page that owns this component.

- **Key Elements:**
  - function navClass
  - function AppHeader
  - type AppHeaderProps

- **Dependencies:**
  - src/features/shared/components/app-icon.tsx
  - next
  - next/link

### src/features/shared/components/app-icon.tsx

- **Type:** component
- **Role:** UI component
- **Priority:** medium

- **Summary:**
Provides reusable UI building blocks for the feature or page that owns this component.

- **Key Elements:**
  - function AppIcon
  - type AppIconName
  - type AppIconProps

- **Dependencies:**
  - None detected

### src/features/uploads/components/upload-panel.tsx

- **Type:** component
- **Role:** UI component
- **Priority:** medium

- **Summary:**
Provides reusable UI building blocks for the feature or page that owns this component.

- **Key Elements:**
  - function UploadPanel

- **Dependencies:**
  - None detected

### src/infrastructure/db/prisma.ts

- **Type:** source-file
- **Role:** external integration/infrastructure
- **Priority:** medium

- **Summary:**
Serves as external integration/infrastructure for `src/infrastructure/db/prisma.ts`; leading content starts with `import { PrismaClient } from "@prisma/client"`.

- **Key Elements:**
  - const prisma

- **Dependencies:**
  - @prisma/client

### src/infrastructure/jobs/trigger-dev.ts

- **Type:** source-file
- **Role:** external integration/infrastructure
- **Priority:** medium

- **Summary:**
Serves as external integration/infrastructure for `src/infrastructure/jobs/trigger-dev.ts`; leading content starts with `import { metrics } from "@/core/observability/metrics"`.

- **Key Elements:**
  - type TriggerJobPayload
  - const triggerDevJobRunner
  - const retryJob
  - const message

- **Dependencies:**
  - src/core/observability/metrics.ts
  - src/core/observability/processing-log.ts
  - src/modules/decomposition/service.ts
  - src/modules/decomposition/types.ts
  - src/modules/scenes/index.ts

### src/infrastructure/providers/qwen/client.ts

- **Type:** source-file
- **Role:** external integration/infrastructure
- **Priority:** medium

- **Summary:**
Serves as external integration/infrastructure for `src/infrastructure/providers/qwen/client.ts`; leading content starts with `import { getEnv } from "@/config/env"`.

- **Key Elements:**
  - type SubmitPayload
  - const qwenClient
  - const env
  - const controller
  - const timeout
  - const response
  - const text
  - const isLastAttempt

- **Dependencies:**
  - src/config/env.ts
  - src/modules/decomposition/types.ts

### src/infrastructure/rate-limit/memory-rate-limiter.ts

- **Type:** source-file
- **Role:** external integration/infrastructure
- **Priority:** medium

- **Summary:**
Serves as external integration/infrastructure for `src/infrastructure/rate-limit/memory-rate-limiter.ts`; leading content starts with `import { AppError } from "@/core/errors/app-error"`.

- **Key Elements:**
  - function enforceRateLimit
  - type Bucket
  - const buckets
  - const env
  - const now
  - const current

- **Dependencies:**
  - src/config/env.ts
  - src/core/errors/app-error.ts

### src/interfaces/http/controllers/auth-controller.ts

- **Type:** controller
- **Role:** interface/controller layer
- **Priority:** high

- **Summary:**
Acts as an HTTP-facing controller that validates request context and orchestrates module calls for a route.

- **Key Elements:**
  - const authController
  - const env
  - const session
  - const cookieStore
  - const guestSessionId
  - const guestSession
  - const body
  - const input

- **Dependencies:**
  - src/auth.ts
  - src/config/env.ts
  - src/core/errors/app-error.ts
  - src/core/request/context.ts
  - src/lib/api-response.ts
  - src/modules/auth/index.ts
  - src/modules/auth/validator.ts
  - src/modules/guest-sessions/index.ts
  - next/headers

### src/interfaces/http/controllers/guest-session-controller.ts

- **Type:** controller
- **Role:** interface/controller layer
- **Priority:** high

- **Summary:**
Acts as an HTTP-facing controller that validates request context and orchestrates module calls for a route.

- **Key Elements:**
  - const guestSessionController
  - const env
  - const session
  - const cookieStore

- **Dependencies:**
  - src/config/env.ts
  - src/core/request/context.ts
  - src/core/security/cookies.ts
  - src/lib/api-response.ts
  - src/modules/guest-sessions/index.ts
  - next/headers

### src/interfaces/http/controllers/health-controller.ts

- **Type:** controller
- **Role:** interface/controller layer
- **Priority:** high

- **Summary:**
Acts as an HTTP-facing controller that validates request context and orchestrates module calls for a route.

- **Key Elements:**
  - const healthController

- **Dependencies:**
  - src/config/env.ts
  - src/core/observability/metrics.ts
  - src/core/request/context.ts
  - src/infrastructure/db/prisma.ts
  - src/lib/api-response.ts
  - src/modules/feature-flags/index.ts

### src/interfaces/http/controllers/maintenance-controller.ts

- **Type:** controller
- **Role:** interface/controller layer
- **Priority:** high

- **Summary:**
Acts as an HTTP-facing controller that validates request context and orchestrates module calls for a route.

- **Key Elements:**
  - const maintenanceController
  - const result

- **Dependencies:**
  - src/core/request/context.ts
  - src/lib/api-response.ts
  - src/modules/maintenance/index.ts

### src/interfaces/http/controllers/preview-controller.ts

- **Type:** controller
- **Role:** interface/controller layer
- **Priority:** high

- **Summary:**
Acts as an HTTP-facing controller that validates request context and orchestrates module calls for a route.

- **Key Elements:**
  - const previewController
  - const actor
  - const project
  - const status
  - const playback

- **Dependencies:**
  - src/core/request/context.ts
  - src/interfaces/http/support/authorization.ts
  - src/interfaces/http/support/request-actor.ts
  - src/lib/api-response.ts
  - src/modules/assets/index.ts
  - src/modules/playback/index.ts
  - src/modules/projects/index.ts

### src/interfaces/http/controllers/project-controller.ts

- **Type:** controller
- **Role:** interface/controller layer
- **Priority:** high

- **Summary:**
Acts as an HTTP-facing controller that validates request context and orchestrates module calls for a route.

- **Key Elements:**
  - const projectController
  - const actor
  - const projects
  - const input
  - const project
  - const updatedProject
  - const guestSessionId
  - const claimedProject

- **Dependencies:**
  - src/core/errors/app-error.ts
  - src/core/request/context.ts
  - src/interfaces/http/support/authorization.ts
  - src/interfaces/http/support/json-body.ts
  - src/interfaces/http/support/request-actor.ts
  - src/lib/api-response.ts
  - src/modules/assets/index.ts
  - src/modules/playback/index.ts
  - src/modules/projects/index.ts
  - src/modules/scenes/index.ts

### src/interfaces/http/controllers/scene-controller.ts

- **Type:** controller
- **Role:** interface/controller layer
- **Priority:** high

- **Summary:**
Acts as an HTTP-facing controller that validates request context and orchestrates module calls for a route.

- **Key Elements:**
  - const sceneController
  - const actor
  - const project
  - const input
  - const startIndex
  - const scenes
  - const token
  - const sceneId

- **Dependencies:**
  - src/core/errors/app-error.ts
  - src/core/request/context.ts
  - src/interfaces/http/support/authorization.ts
  - src/interfaces/http/support/json-body.ts
  - src/interfaces/http/support/request-actor.ts
  - src/lib/api-response.ts
  - src/modules/assets/index.ts
  - src/modules/motion/index.ts
  - src/modules/playback/index.ts
  - src/modules/processing/index.ts
  - src/modules/projects/index.ts
  - src/modules/scenes/index.ts
  - src/modules/uploads/index.ts

### src/interfaces/http/controllers/upload-controller.ts

- **Type:** controller
- **Role:** interface/controller layer
- **Priority:** high

- **Summary:**
Acts as an HTTP-facing controller that validates request context and orchestrates module calls for a route.

- **Key Elements:**
  - const uploadController
  - const actor
  - const project
  - const input
  - const uploads

- **Dependencies:**
  - src/core/request/context.ts
  - src/interfaces/http/support/authorization.ts
  - src/interfaces/http/support/json-body.ts
  - src/interfaces/http/support/request-actor.ts
  - src/lib/api-response.ts
  - src/modules/projects/index.ts
  - src/modules/uploads/index.ts

### src/interfaces/http/support/authorization.ts

- **Type:** source-file
- **Role:** supporting source file
- **Priority:** medium

- **Summary:**
Serves as supporting source file for `src/interfaces/http/support/authorization.ts`; leading content starts with `import { AppError } from "@/core/errors/app-error"`.

- **Key Elements:**
  - function ensureProjectAccess
  - const decision

- **Dependencies:**
  - src/core/errors/app-error.ts
  - src/modules/authorization/index.ts

### src/interfaces/http/support/internal-maintenance.ts

- **Type:** source-file
- **Role:** supporting source file
- **Priority:** medium

- **Summary:**
Serves as supporting source file for `src/interfaces/http/support/internal-maintenance.ts`; leading content starts with `import { timingSafeEqual } from "node:crypto"`.

- **Key Elements:**
  - function ensureInternalMaintenanceAccess
  - const env
  - const providedToken

- **Dependencies:**
  - src/config/env.ts
  - src/core/errors/app-error.ts
  - node:crypto

### src/interfaces/http/support/json-body.ts

- **Type:** source-file
- **Role:** supporting source file
- **Priority:** medium

- **Summary:**
Serves as supporting source file for `src/interfaces/http/support/json-body.ts`; leading content starts with `import { ZodSchema } from "zod"`.

- **Key Elements:**
  - function parseJsonBody
  - const body

- **Dependencies:**
  - src/core/errors/app-error.ts
  - zod

### src/interfaces/http/support/request-actor.ts

- **Type:** source-file
- **Role:** supporting source file
- **Priority:** medium

- **Summary:**
Serves as supporting source file for `src/interfaces/http/support/request-actor.ts`; leading content starts with `import { cookies } from "next/headers"`.

- **Key Elements:**
  - function resolveRequestActor
  - const session
  - const env
  - const cookieStore
  - const guestSessionId
  - const guestSession

- **Dependencies:**
  - src/auth.ts
  - src/config/env.ts
  - src/modules/authorization/index.ts
  - src/modules/guest-sessions/index.ts
  - next/headers

### src/modules/assets/index.ts

- **Type:** module-index
- **Role:** module entrypoint
- **Priority:** high

- **Summary:**
Serves as module entrypoint for `src/modules/assets/index.ts`; leading content starts with `export * from "@/modules/assets/pathing"`.

- **Key Elements:**
  - None detected

- **Dependencies:**
  - src/modules/assets/pathing.ts
  - src/modules/assets/serialization.ts
  - src/modules/assets/service.ts
  - src/modules/assets/storage.ts

### src/modules/assets/service.ts

- **Type:** service
- **Role:** domain service
- **Priority:** high

- **Summary:**
Contains domain logic for its module and coordinates validation, persistence, or provider interactions.

- **Key Elements:**
  - function decodeBase64Artifact
  - function persistArtifact
  - type PersistAssetsInput
  - const payload
  - const response
  - const content
  - const assetService
  - const compositePath

- **Dependencies:**
  - src/modules/assets/pathing.ts
  - src/modules/assets/storage.ts
  - src/modules/decomposition/types.ts
  - src/modules/scenes/repository.ts
  - @prisma/client

### src/modules/auth/index.ts

- **Type:** module-index
- **Role:** module entrypoint
- **Priority:** high

- **Summary:**
Serves as module entrypoint for `src/modules/auth/index.ts`; leading content starts with `export * from "@/modules/auth/service"`.

- **Key Elements:**
  - None detected

- **Dependencies:**
  - src/modules/auth/service.ts
  - src/modules/auth/types.ts
  - src/modules/auth/validator.ts

### src/modules/auth/repository.ts

- **Type:** repository
- **Role:** data access layer
- **Priority:** high

- **Summary:**
Handles persistence access and storage-oriented queries for its module.

- **Key Elements:**
  - const authRepository

- **Dependencies:**
  - src/infrastructure/db/prisma.ts
  - @prisma/client

### src/modules/auth/service.ts

- **Type:** service
- **Role:** domain service
- **Priority:** high

- **Summary:**
Contains domain logic for its module and coordinates validation, persistence, or provider interactions.

- **Key Elements:**
  - const authService
  - const existingUser
  - const passwordHash
  - const user

- **Dependencies:**
  - src/core/errors/app-error.ts
  - src/modules/auth/repository.ts
  - src/modules/auth/types.ts
  - @prisma/client
  - bcryptjs

### src/modules/authorization/index.ts

- **Type:** module-index
- **Role:** module entrypoint
- **Priority:** high

- **Summary:**
Serves as module entrypoint for `src/modules/authorization/index.ts`; leading content starts with `export * from "@/modules/authorization/service"`.

- **Key Elements:**
  - None detected

- **Dependencies:**
  - src/modules/authorization/service.ts
  - src/modules/authorization/types.ts

### src/modules/authorization/service.ts

- **Type:** service
- **Role:** domain service
- **Priority:** high

- **Summary:**
Contains domain logic for its module and coordinates validation, persistence, or provider interactions.

- **Key Elements:**
  - function authorizeProjectAction
  - const matchesGuest
  - const sameGuestSession

- **Dependencies:**
  - src/modules/authorization/types.ts

### src/modules/decomposition/service.ts

- **Type:** service
- **Role:** domain service
- **Priority:** high

- **Summary:**
Contains domain logic for its module and coordinates validation, persistence, or provider interactions.

- **Key Elements:**
  - const decompositionService
  - const startedAt
  - const originalAsset
  - const metadata
  - const attemptCount
  - const correlationId
  - const result
  - const refreshedScene

- **Dependencies:**
  - src/config/constants.ts
  - src/core/observability/metrics.ts
  - src/core/observability/processing-log.ts
  - src/modules/assets/index.ts
  - src/modules/decomposition/adapter.ts
  - src/modules/decomposition/types.ts
  - src/modules/feature-flags/index.ts
  - src/modules/motion/index.ts
  - src/modules/playback/index.ts
  - src/modules/scenes/index.ts

### src/modules/feature-flags/index.ts

- **Type:** module-index
- **Role:** module entrypoint
- **Priority:** high

- **Summary:**
Serves as module entrypoint for `src/modules/feature-flags/index.ts`; leading content starts with `export * from "@/modules/feature-flags/service"`.

- **Key Elements:**
  - None detected

- **Dependencies:**
  - src/modules/feature-flags/service.ts

### src/modules/feature-flags/service.ts

- **Type:** service
- **Role:** domain service
- **Priority:** high

- **Summary:**
Contains domain logic for its module and coordinates validation, persistence, or provider interactions.

- **Key Elements:**
  - const featureFlagService
  - const env
  - const percent

- **Dependencies:**
  - src/config/env.ts

### src/modules/guest-sessions/index.ts

- **Type:** module-index
- **Role:** module entrypoint
- **Priority:** high

- **Summary:**
Serves as module entrypoint for `src/modules/guest-sessions/index.ts`; leading content starts with `export * from "@/modules/guest-sessions/service"`.

- **Key Elements:**
  - None detected

- **Dependencies:**
  - src/modules/guest-sessions/service.ts
  - src/modules/guest-sessions/types.ts

### src/modules/guest-sessions/repository.ts

- **Type:** repository
- **Role:** data access layer
- **Priority:** high

- **Summary:**
Handles persistence access and storage-oriented queries for its module.

- **Key Elements:**
  - const guestSessionRepository

- **Dependencies:**
  - src/infrastructure/db/prisma.ts

### src/modules/guest-sessions/service.ts

- **Type:** service
- **Role:** domain service
- **Priority:** high

- **Summary:**
Contains domain logic for its module and coordinates validation, persistence, or provider interactions.

- **Key Elements:**
  - function addHours
  - const guestSessionService
  - const env
  - const expiresAt
  - const guestSession

- **Dependencies:**
  - src/config/env.ts
  - src/core/errors/app-error.ts
  - src/modules/guest-sessions/repository.ts

### src/modules/maintenance/index.ts

- **Type:** module-index
- **Role:** module entrypoint
- **Priority:** high

- **Summary:**
Serves as module entrypoint for `src/modules/maintenance/index.ts`; leading content starts with `export * from "@/modules/maintenance/service"`.

- **Key Elements:**
  - None detected

- **Dependencies:**
  - src/modules/maintenance/service.ts

### src/modules/maintenance/service.ts

- **Type:** service
- **Role:** domain service
- **Priority:** high

- **Summary:**
Contains domain logic for its module and coordinates validation, persistence, or provider interactions.

- **Key Elements:**
  - const maintenanceService
  - const now
  - const deletedProjects
  - const deletedSessions
  - const env
  - const timeoutBefore
  - const jobs

- **Dependencies:**
  - src/config/env.ts
  - src/core/observability/metrics.ts
  - src/core/observability/processing-log.ts
  - src/modules/projects/repository.ts
  - src/modules/scenes/index.ts
  - src/modules/scenes/repository.ts

### src/modules/motion/index.ts

- **Type:** module-index
- **Role:** module entrypoint
- **Priority:** high

- **Summary:**
Serves as module entrypoint for `src/modules/motion/index.ts`; leading content starts with `export * from "@/modules/motion/service"`.

- **Key Elements:**
  - None detected

- **Dependencies:**
  - src/modules/motion/service.ts
  - src/modules/motion/types.ts

### src/modules/motion/service.ts

- **Type:** service
- **Role:** domain service
- **Priority:** high

- **Summary:**
Contains domain logic for its module and coordinates validation, persistence, or provider interactions.

- **Key Elements:**
  - function intensityFromPreset
  - function movementFromPreset
  - function round
  - function asRecord
  - function toFiniteNumber
  - function toLayerIndex
  - function toEasingKey
  - function toGroupKey

- **Dependencies:**
  - src/config/constants.ts
  - src/core/observability/metrics.ts
  - src/core/observability/processing-log.ts
  - src/modules/motion/types.ts
  - src/modules/scenes/index.ts
  - src/modules/scenes/repository.ts
  - @prisma/client

### src/modules/playback/index.ts

- **Type:** module-index
- **Role:** module entrypoint
- **Priority:** high

- **Summary:**
Serves as module entrypoint for `src/modules/playback/index.ts`; leading content starts with `export * from "@/modules/playback/service"`.

- **Key Elements:**
  - None detected

- **Dependencies:**
  - src/modules/playback/service.ts

### src/modules/playback/service.ts

- **Type:** service
- **Role:** domain service
- **Priority:** high

- **Summary:**
Contains domain logic for its module and coordinates validation, persistence, or provider interactions.

- **Key Elements:**
  - function round
  - function applyReducedMotionToLayerBehavior
  - function deriveSceneDuration
  - type StitchOptions
  - const mapping
  - const value
  - const playbackService
  - const reducedMotion

- **Dependencies:**
  - src/config/constants.ts
  - src/core/errors/app-error.ts
  - src/core/observability/metrics.ts
  - src/core/observability/processing-log.ts
  - src/modules/feature-flags/index.ts
  - src/modules/projects/repository.ts
  - src/modules/scenes/repository.ts
  - @prisma/client

### src/modules/processing/index.ts

- **Type:** module-index
- **Role:** module entrypoint
- **Priority:** high

- **Summary:**
Serves as module entrypoint for `src/modules/processing/index.ts`; leading content starts with `export * from "@/modules/processing/service"`.

- **Key Elements:**
  - None detected

- **Dependencies:**
  - src/modules/processing/service.ts

### src/modules/processing/service.ts

- **Type:** service
- **Role:** domain service
- **Priority:** high

- **Summary:**
Contains domain logic for its module and coordinates validation, persistence, or provider interactions.

- **Key Elements:**
  - const processingService
  - const scene
  - const job
  - const latestScene

- **Dependencies:**
  - src/core/errors/app-error.ts
  - src/core/observability/processing-log.ts
  - src/infrastructure/jobs/trigger-dev.ts
  - src/modules/feature-flags/index.ts
  - src/modules/scenes/index.ts

### src/modules/projects/index.ts

- **Type:** module-index
- **Role:** module entrypoint
- **Priority:** high

- **Summary:**
Serves as module entrypoint for `src/modules/projects/index.ts`; leading content starts with `export * from "@/modules/projects/service"`.

- **Key Elements:**
  - None detected

- **Dependencies:**
  - src/modules/projects/service.ts
  - src/modules/projects/types.ts
  - src/modules/projects/validator.ts

### src/modules/projects/repository.ts

- **Type:** repository
- **Role:** data access layer
- **Priority:** high

- **Summary:**
Handles persistence access and storage-oriented queries for its module.

- **Key Elements:**
  - const projectRepository
  - const claimedAt

- **Dependencies:**
  - src/infrastructure/db/prisma.ts
  - @prisma/client

### src/modules/projects/service.ts

- **Type:** service
- **Role:** domain service
- **Priority:** high

- **Summary:**
Contains domain logic for its module and coordinates validation, persistence, or provider interactions.

- **Key Elements:**
  - const projectService
  - const project
  - const env
  - const guestProjectCount

- **Dependencies:**
  - src/config/constants.ts
  - src/config/env.ts
  - src/core/errors/app-error.ts
  - src/modules/projects/repository.ts
  - src/modules/projects/types.ts

### src/modules/scenes/index.ts

- **Type:** module-index
- **Role:** module entrypoint
- **Priority:** high

- **Summary:**
Serves as module entrypoint for `src/modules/scenes/index.ts`; leading content starts with `export * from "@/modules/scenes/service"`.

- **Key Elements:**
  - None detected

- **Dependencies:**
  - src/modules/scenes/service.ts
  - src/modules/scenes/types.ts
  - src/modules/scenes/validator.ts

### src/modules/scenes/repository.ts

- **Type:** repository
- **Role:** data access layer
- **Priority:** high

- **Summary:**
Handles persistence access and storage-oriented queries for its module.

- **Key Elements:**
  - const sceneRepository
  - const result

- **Dependencies:**
  - src/infrastructure/db/prisma.ts
  - @prisma/client

### src/modules/scenes/service.ts

- **Type:** service
- **Role:** domain service
- **Priority:** high

- **Summary:**
Contains domain logic for its module and coordinates validation, persistence, or provider interactions.

- **Key Elements:**
  - const sceneService
  - const scene
  - const env
  - const projectId
  - const existingCount
  - const activeJob

- **Dependencies:**
  - src/config/env.ts
  - src/core/errors/app-error.ts
  - src/modules/scenes/repository.ts
  - src/modules/scenes/types.ts
  - @prisma/client

### src/modules/uploads/index.ts

- **Type:** module-index
- **Role:** module entrypoint
- **Priority:** high

- **Summary:**
Serves as module entrypoint for `src/modules/uploads/index.ts`; leading content starts with `export * from "@/modules/uploads/service"`.

- **Key Elements:**
  - None detected

- **Dependencies:**
  - src/modules/uploads/service.ts
  - src/modules/uploads/types.ts
  - src/modules/uploads/validator.ts

### src/modules/uploads/service.ts

- **Type:** service
- **Role:** domain service
- **Priority:** high

- **Summary:**
Contains domain logic for its module and coordinates validation, persistence, or provider interactions.

- **Key Elements:**
  - function toBase64Url
  - function fromBase64Url
  - function sign
  - type UploadTokenPayload
  - const env
  - const uploadService
  - const expiresAt
  - const safeFilename

- **Dependencies:**
  - src/config/constants.ts
  - src/config/env.ts
  - src/core/errors/app-error.ts
  - src/modules/uploads/types.ts
  - node:crypto

### tests/unit/core/errors/error-response.test.ts

- **Type:** source-file
- **Role:** cross-cutting infrastructure
- **Priority:** medium

- **Summary:**
Provides shared cross-cutting behavior used across multiple layers of the application.

- **Key Elements:**
  - const context
  - const error
  - const response
  - const payload

- **Dependencies:**
  - src/core/errors/app-error.ts
  - src/core/errors/error-response.ts
  - @prisma/client
  - vitest
  - zod

### tests/unit/features/preview/playback-client.test.ts

- **Type:** source-file
- **Role:** supporting source file
- **Priority:** medium

- **Summary:**
Serves as supporting source file for `tests/unit/features/preview/playback-client.test.ts`; leading content starts with `import { describe, expect, it } from "vitest"`.

- **Key Elements:**
  - const state

- **Dependencies:**
  - src/features/preview/lib/playback-client.ts
  - vitest

## Relationships
- src/auth.ts -> src/config/env.ts
- src/auth.ts -> src/modules/auth/repository.ts
- src/app/page.tsx -> src/features/marketing/components/landing-page.tsx
- src/app/api/auth/[...nextauth]/route.ts -> src/auth.ts
- src/app/api/v1/assets/[...assetPath]/route.ts -> src/core/http/route-handler.ts
- src/app/api/v1/assets/[...assetPath]/route.ts -> src/modules/assets/index.ts
- src/app/api/v1/auth/register/route.ts -> src/core/http/route-handler.ts
- src/app/api/v1/auth/register/route.ts -> src/infrastructure/rate-limit/memory-rate-limiter.ts
- src/app/api/v1/auth/register/route.ts -> src/interfaces/http/controllers/auth-controller.ts
- src/app/api/v1/auth/session/route.ts -> src/core/http/route-handler.ts
- src/app/api/v1/auth/session/route.ts -> src/interfaces/http/controllers/auth-controller.ts
- src/app/api/v1/guest-sessions/route.ts -> src/core/http/route-handler.ts
- src/app/api/v1/guest-sessions/route.ts -> src/infrastructure/rate-limit/memory-rate-limiter.ts
- src/app/api/v1/guest-sessions/route.ts -> src/interfaces/http/controllers/guest-session-controller.ts
- src/app/api/v1/health/live/route.ts -> src/core/http/route-handler.ts
- src/app/api/v1/health/live/route.ts -> src/interfaces/http/controllers/health-controller.ts
- src/app/api/v1/health/ready/route.ts -> src/core/http/route-handler.ts
- src/app/api/v1/health/ready/route.ts -> src/interfaces/http/controllers/health-controller.ts
- src/app/api/v1/internal/maintenance/cleanup/route.ts -> src/core/http/route-handler.ts
- src/app/api/v1/internal/maintenance/cleanup/route.ts -> src/interfaces/http/support/internal-maintenance.ts
- src/app/api/v1/internal/maintenance/cleanup/route.ts -> src/interfaces/http/controllers/maintenance-controller.ts
- src/app/api/v1/internal/maintenance/recover-timeouts/route.ts -> src/core/http/route-handler.ts
- src/app/api/v1/internal/maintenance/recover-timeouts/route.ts -> src/interfaces/http/support/internal-maintenance.ts
- src/app/api/v1/internal/maintenance/recover-timeouts/route.ts -> src/interfaces/http/controllers/maintenance-controller.ts
- src/app/api/v1/projects/route.ts -> src/core/http/route-handler.ts
- src/app/api/v1/projects/route.ts -> src/infrastructure/rate-limit/memory-rate-limiter.ts
- src/app/api/v1/projects/route.ts -> src/interfaces/http/controllers/project-controller.ts
- src/app/api/v1/projects/[projectId]/route.ts -> src/core/http/route-handler.ts
- src/app/api/v1/projects/[projectId]/route.ts -> src/infrastructure/rate-limit/memory-rate-limiter.ts
- src/app/api/v1/projects/[projectId]/route.ts -> src/interfaces/http/controllers/project-controller.ts
- src/app/api/v1/projects/[projectId]/claim/route.ts -> src/core/http/route-handler.ts
- src/app/api/v1/projects/[projectId]/claim/route.ts -> src/infrastructure/rate-limit/memory-rate-limiter.ts
- src/app/api/v1/projects/[projectId]/claim/route.ts -> src/interfaces/http/controllers/project-controller.ts
- src/app/api/v1/projects/[projectId]/preview/playback/route.ts -> src/core/http/route-handler.ts
- src/app/api/v1/projects/[projectId]/preview/playback/route.ts -> src/infrastructure/rate-limit/memory-rate-limiter.ts
- src/app/api/v1/projects/[projectId]/preview/playback/route.ts -> src/interfaces/http/controllers/preview-controller.ts
- src/app/api/v1/projects/[projectId]/preview/status/route.ts -> src/core/http/route-handler.ts
- src/app/api/v1/projects/[projectId]/preview/status/route.ts -> src/infrastructure/rate-limit/memory-rate-limiter.ts
- src/app/api/v1/projects/[projectId]/preview/status/route.ts -> src/interfaces/http/controllers/preview-controller.ts
- src/app/api/v1/projects/[projectId]/scenes/reorder/route.ts -> src/core/http/route-handler.ts
- src/app/api/v1/projects/[projectId]/scenes/reorder/route.ts -> src/infrastructure/rate-limit/memory-rate-limiter.ts
- src/app/api/v1/projects/[projectId]/scenes/reorder/route.ts -> src/interfaces/http/controllers/project-controller.ts
- src/app/api/v1/projects/[projectId]/uploads/finalize/route.ts -> src/core/http/route-handler.ts
- src/app/api/v1/projects/[projectId]/uploads/finalize/route.ts -> src/infrastructure/rate-limit/memory-rate-limiter.ts
- src/app/api/v1/projects/[projectId]/uploads/finalize/route.ts -> src/interfaces/http/controllers/scene-controller.ts
- src/app/api/v1/projects/[projectId]/uploads/init/route.ts -> src/core/http/route-handler.ts
- src/app/api/v1/projects/[projectId]/uploads/init/route.ts -> src/infrastructure/rate-limit/memory-rate-limiter.ts
- src/app/api/v1/projects/[projectId]/uploads/init/route.ts -> src/interfaces/http/controllers/upload-controller.ts
- src/app/api/v1/scenes/[sceneId]/route.ts -> src/core/http/route-handler.ts
- src/app/api/v1/scenes/[sceneId]/route.ts -> src/infrastructure/rate-limit/memory-rate-limiter.ts
- src/app/api/v1/scenes/[sceneId]/route.ts -> src/interfaces/http/controllers/scene-controller.ts
- src/app/api/v1/scenes/[sceneId]/regenerate/route.ts -> src/core/http/route-handler.ts
- src/app/api/v1/scenes/[sceneId]/regenerate/route.ts -> src/infrastructure/rate-limit/memory-rate-limiter.ts
- src/app/api/v1/scenes/[sceneId]/regenerate/route.ts -> src/interfaces/http/controllers/scene-controller.ts
- src/app/api/v1/scenes/[sceneId]/retry/route.ts -> src/core/http/route-handler.ts
- src/app/api/v1/scenes/[sceneId]/retry/route.ts -> src/infrastructure/rate-limit/memory-rate-limiter.ts
- src/app/api/v1/scenes/[sceneId]/retry/route.ts -> src/interfaces/http/controllers/scene-controller.ts
- src/app/api/v1/uploads/[uploadToken]/route.ts -> src/core/http/route-handler.ts
- src/app/api/v1/uploads/[uploadToken]/route.ts -> src/core/errors/app-error.ts
- src/app/api/v1/uploads/[uploadToken]/route.ts -> src/lib/api-response.ts
- src/app/api/v1/uploads/[uploadToken]/route.ts -> src/modules/assets/index.ts
- src/app/api/v1/uploads/[uploadToken]/route.ts -> src/modules/uploads/index.ts
- src/app/login/page.tsx -> src/features/auth/components/auth-page.tsx
- src/app/login/page.tsx -> src/config/env.ts
- src/app/projects/page.tsx -> src/features/projects/components/projects-dashboard-page.tsx
- src/app/projects/[projectId]/editor/page.tsx -> src/features/projects/components/project-editor-page.tsx
- src/app/projects/[projectId]/preview/page.tsx -> src/features/preview/components/project-preview-page.tsx
- src/app/projects/new/page.tsx -> src/features/projects/components/new-project-page.tsx
- src/app/settings/page.tsx -> src/features/settings/components/settings-page.tsx
- src/app/signup/page.tsx -> src/features/auth/components/auth-page.tsx
- src/app/signup/page.tsx -> src/config/env.ts
- src/core/errors/error-response.ts -> src/core/errors/app-error.ts
- src/core/errors/error-response.ts -> src/core/request/context.ts
- src/core/http/route-handler.ts -> src/core/errors/error-response.ts
- src/core/http/route-handler.ts -> src/core/logging/logger.ts
- src/core/http/route-handler.ts -> src/core/request/context.ts
- src/core/logging/logger.ts -> src/config/env.ts
- src/core/observability/processing-log.ts -> src/core/logging/logger.ts
- src/features/auth/components/auth-page.tsx -> src/features/shared/components/app-header.tsx
- src/features/auth/components/auth-page.tsx -> src/features/shared/components/app-icon.tsx
- src/features/marketing/components/landing-page.tsx -> src/features/shared/components/app-header.tsx
- src/features/marketing/components/landing-page.tsx -> src/features/shared/components/app-icon.tsx
- src/features/preview/components/playback-scene-renderer.tsx -> src/features/preview/lib/playback-client.ts
- src/features/preview/components/project-preview-page.tsx -> src/features/shared/components/app-header.tsx
- src/features/preview/components/project-preview-page.tsx -> src/features/preview/components/playback-scene-renderer.tsx
- src/features/preview/components/project-preview-page.tsx -> src/features/preview/lib/playback-client.ts
- src/features/preview/lib/playback-client.ts -> src/modules/scenes/types.ts
- src/features/projects/components/new-project-form.tsx -> src/features/shared/components/app-icon.tsx
- src/features/projects/components/new-project-page.tsx -> src/features/shared/components/app-header.tsx
- src/features/projects/components/new-project-page.tsx -> src/features/projects/components/new-project-form.tsx
- src/features/projects/components/project-card.tsx -> src/features/shared/components/app-icon.tsx
- src/features/projects/components/project-editor-page.tsx -> src/features/preview/components/playback-scene-renderer.tsx
- src/features/projects/components/project-editor-page.tsx -> src/features/preview/lib/playback-client.ts
- src/features/projects/components/project-editor-page.tsx -> src/features/shared/components/app-header.tsx
- src/features/projects/components/project-editor-page.tsx -> src/features/shared/components/app-icon.tsx
- src/features/projects/components/project-editor-page.tsx -> src/modules/scenes/types.ts
- src/features/projects/components/projects-dashboard-page.tsx -> src/features/shared/components/app-header.tsx
- src/features/projects/components/projects-dashboard-page.tsx -> src/features/shared/components/app-icon.tsx
- src/features/projects/components/projects-dashboard-page.tsx -> src/features/projects/components/project-card.tsx
- src/features/settings/components/settings-page.tsx -> src/features/shared/components/app-header.tsx
- src/features/shared/components/app-header.tsx -> src/features/shared/components/app-icon.tsx
- src/infrastructure/jobs/trigger-dev.ts -> src/core/observability/metrics.ts
- src/infrastructure/jobs/trigger-dev.ts -> src/core/observability/processing-log.ts
- src/infrastructure/jobs/trigger-dev.ts -> src/modules/decomposition/types.ts
- src/infrastructure/jobs/trigger-dev.ts -> src/modules/decomposition/service.ts
- src/infrastructure/jobs/trigger-dev.ts -> src/modules/scenes/index.ts
- src/infrastructure/providers/qwen/client.ts -> src/config/env.ts
- src/infrastructure/providers/qwen/client.ts -> src/modules/decomposition/types.ts
- src/infrastructure/rate-limit/memory-rate-limiter.ts -> src/core/errors/app-error.ts
- src/infrastructure/rate-limit/memory-rate-limiter.ts -> src/config/env.ts
- src/interfaces/http/controllers/auth-controller.ts -> src/auth.ts
- src/interfaces/http/controllers/auth-controller.ts -> src/core/errors/app-error.ts
- src/interfaces/http/controllers/auth-controller.ts -> src/lib/api-response.ts
- src/interfaces/http/controllers/auth-controller.ts -> src/modules/auth/index.ts
- src/interfaces/http/controllers/auth-controller.ts -> src/modules/auth/validator.ts
- src/interfaces/http/controllers/auth-controller.ts -> src/modules/guest-sessions/index.ts
- src/interfaces/http/controllers/auth-controller.ts -> src/config/env.ts
- src/interfaces/http/controllers/auth-controller.ts -> src/core/request/context.ts
- src/interfaces/http/controllers/guest-session-controller.ts -> src/config/env.ts
- src/interfaces/http/controllers/guest-session-controller.ts -> src/core/security/cookies.ts
- src/interfaces/http/controllers/guest-session-controller.ts -> src/lib/api-response.ts
- src/interfaces/http/controllers/guest-session-controller.ts -> src/modules/guest-sessions/index.ts
- src/interfaces/http/controllers/guest-session-controller.ts -> src/core/request/context.ts
- src/interfaces/http/controllers/health-controller.ts -> src/infrastructure/db/prisma.ts
- src/interfaces/http/controllers/health-controller.ts -> src/config/env.ts
- src/interfaces/http/controllers/health-controller.ts -> src/core/observability/metrics.ts
- src/interfaces/http/controllers/health-controller.ts -> src/lib/api-response.ts
- src/interfaces/http/controllers/health-controller.ts -> src/modules/feature-flags/index.ts
- src/interfaces/http/controllers/health-controller.ts -> src/core/request/context.ts
- src/interfaces/http/controllers/maintenance-controller.ts -> src/lib/api-response.ts
- src/interfaces/http/controllers/maintenance-controller.ts -> src/modules/maintenance/index.ts
- src/interfaces/http/controllers/maintenance-controller.ts -> src/core/request/context.ts
- src/interfaces/http/controllers/preview-controller.ts -> src/lib/api-response.ts
- src/interfaces/http/controllers/preview-controller.ts -> src/interfaces/http/support/authorization.ts
- src/interfaces/http/controllers/preview-controller.ts -> src/interfaces/http/support/request-actor.ts
- src/interfaces/http/controllers/preview-controller.ts -> src/modules/assets/index.ts
- src/interfaces/http/controllers/preview-controller.ts -> src/modules/projects/index.ts
- src/interfaces/http/controllers/preview-controller.ts -> src/modules/playback/index.ts
- src/interfaces/http/controllers/preview-controller.ts -> src/core/request/context.ts
- src/interfaces/http/controllers/project-controller.ts -> src/lib/api-response.ts
- src/interfaces/http/controllers/project-controller.ts -> src/interfaces/http/support/json-body.ts
- src/interfaces/http/controllers/project-controller.ts -> src/interfaces/http/support/request-actor.ts
- src/interfaces/http/controllers/project-controller.ts -> src/interfaces/http/support/authorization.ts
- src/interfaces/http/controllers/project-controller.ts -> src/core/errors/app-error.ts
- src/interfaces/http/controllers/project-controller.ts -> src/modules/assets/index.ts
- src/interfaces/http/controllers/project-controller.ts -> src/modules/projects/index.ts
- src/interfaces/http/controllers/project-controller.ts -> src/modules/scenes/index.ts
- src/interfaces/http/controllers/project-controller.ts -> src/modules/playback/index.ts
- src/interfaces/http/controllers/project-controller.ts -> src/core/request/context.ts
- src/interfaces/http/controllers/scene-controller.ts -> src/lib/api-response.ts
- src/interfaces/http/controllers/scene-controller.ts -> src/interfaces/http/support/json-body.ts
- src/interfaces/http/controllers/scene-controller.ts -> src/interfaces/http/support/request-actor.ts
- src/interfaces/http/controllers/scene-controller.ts -> src/interfaces/http/support/authorization.ts
- src/interfaces/http/controllers/scene-controller.ts -> src/modules/scenes/index.ts
- src/interfaces/http/controllers/scene-controller.ts -> src/modules/projects/index.ts
- src/interfaces/http/controllers/scene-controller.ts -> src/modules/uploads/index.ts
- src/interfaces/http/controllers/scene-controller.ts -> src/modules/assets/index.ts
- src/interfaces/http/controllers/scene-controller.ts -> src/modules/processing/index.ts
- src/interfaces/http/controllers/scene-controller.ts -> src/modules/motion/index.ts
- src/interfaces/http/controllers/scene-controller.ts -> src/modules/playback/index.ts
- src/interfaces/http/controllers/scene-controller.ts -> src/core/errors/app-error.ts
- src/interfaces/http/controllers/scene-controller.ts -> src/core/request/context.ts
- src/interfaces/http/controllers/upload-controller.ts -> src/lib/api-response.ts
- src/interfaces/http/controllers/upload-controller.ts -> src/interfaces/http/support/json-body.ts
- src/interfaces/http/controllers/upload-controller.ts -> src/interfaces/http/support/request-actor.ts
- src/interfaces/http/controllers/upload-controller.ts -> src/interfaces/http/support/authorization.ts
- src/interfaces/http/controllers/upload-controller.ts -> src/modules/uploads/index.ts
- src/interfaces/http/controllers/upload-controller.ts -> src/modules/projects/index.ts
- src/interfaces/http/controllers/upload-controller.ts -> src/core/request/context.ts
- src/interfaces/http/support/authorization.ts -> src/core/errors/app-error.ts
- src/interfaces/http/support/authorization.ts -> src/modules/authorization/index.ts
- src/interfaces/http/support/internal-maintenance.ts -> src/config/env.ts
- src/interfaces/http/support/internal-maintenance.ts -> src/core/errors/app-error.ts
- src/interfaces/http/support/json-body.ts -> src/core/errors/app-error.ts
- src/interfaces/http/support/request-actor.ts -> src/auth.ts
- src/interfaces/http/support/request-actor.ts -> src/config/env.ts
- src/interfaces/http/support/request-actor.ts -> src/modules/guest-sessions/index.ts
- src/interfaces/http/support/request-actor.ts -> src/modules/authorization/index.ts
- src/modules/assets/index.ts -> src/modules/assets/pathing.ts
- src/modules/assets/index.ts -> src/modules/assets/serialization.ts
- src/modules/assets/index.ts -> src/modules/assets/service.ts
- src/modules/assets/index.ts -> src/modules/assets/storage.ts
- src/modules/assets/pathing.ts -> src/config/constants.ts
- src/modules/assets/serialization.ts -> src/modules/assets/storage.ts
- src/modules/assets/service.ts -> src/modules/assets/pathing.ts
- src/modules/assets/service.ts -> src/modules/scenes/repository.ts
- src/modules/assets/service.ts -> src/modules/assets/storage.ts
- src/modules/assets/service.ts -> src/modules/decomposition/types.ts
- src/modules/assets/storage.ts -> src/config/env.ts
- src/modules/assets/storage.ts -> src/core/errors/app-error.ts
- src/modules/auth/index.ts -> src/modules/auth/service.ts
- src/modules/auth/index.ts -> src/modules/auth/types.ts
- src/modules/auth/index.ts -> src/modules/auth/validator.ts
- src/modules/auth/repository.ts -> src/infrastructure/db/prisma.ts
- src/modules/auth/service.ts -> src/core/errors/app-error.ts
- src/modules/auth/service.ts -> src/modules/auth/repository.ts
- src/modules/auth/service.ts -> src/modules/auth/types.ts
- src/modules/authorization/index.ts -> src/modules/authorization/service.ts
- src/modules/authorization/index.ts -> src/modules/authorization/types.ts
- src/modules/authorization/service.ts -> src/modules/authorization/types.ts
- src/modules/decomposition/adapter.ts -> src/config/constants.ts
- src/modules/decomposition/adapter.ts -> src/infrastructure/providers/qwen/client.ts
- src/modules/decomposition/adapter.ts -> src/modules/decomposition/types.ts
- src/modules/decomposition/service.ts -> src/config/constants.ts
- src/modules/decomposition/service.ts -> src/core/observability/metrics.ts
- src/modules/decomposition/service.ts -> src/core/observability/processing-log.ts
- src/modules/decomposition/service.ts -> src/modules/assets/index.ts
- src/modules/decomposition/service.ts -> src/modules/decomposition/adapter.ts
- src/modules/decomposition/service.ts -> src/modules/decomposition/types.ts
- src/modules/decomposition/service.ts -> src/modules/feature-flags/index.ts
- src/modules/decomposition/service.ts -> src/modules/motion/index.ts
- src/modules/decomposition/service.ts -> src/modules/playback/index.ts
- src/modules/decomposition/service.ts -> src/modules/scenes/index.ts
- src/modules/feature-flags/index.ts -> src/modules/feature-flags/service.ts
- src/modules/feature-flags/service.ts -> src/config/env.ts
- src/modules/guest-sessions/index.ts -> src/modules/guest-sessions/service.ts
- src/modules/guest-sessions/index.ts -> src/modules/guest-sessions/types.ts
- src/modules/guest-sessions/repository.ts -> src/infrastructure/db/prisma.ts
- src/modules/guest-sessions/service.ts -> src/core/errors/app-error.ts
- src/modules/guest-sessions/service.ts -> src/config/env.ts
- src/modules/guest-sessions/service.ts -> src/modules/guest-sessions/repository.ts
- src/modules/maintenance/index.ts -> src/modules/maintenance/service.ts
- src/modules/maintenance/service.ts -> src/config/env.ts
- src/modules/maintenance/service.ts -> src/core/observability/metrics.ts
- src/modules/maintenance/service.ts -> src/core/observability/processing-log.ts
- src/modules/maintenance/service.ts -> src/modules/projects/repository.ts
- src/modules/maintenance/service.ts -> src/modules/scenes/repository.ts
- src/modules/maintenance/service.ts -> src/modules/scenes/index.ts
- src/modules/motion/index.ts -> src/modules/motion/service.ts
- src/modules/motion/index.ts -> src/modules/motion/types.ts
- src/modules/motion/service.ts -> src/config/constants.ts
- src/modules/motion/service.ts -> src/core/observability/metrics.ts
- src/modules/motion/service.ts -> src/core/observability/processing-log.ts
- src/modules/motion/service.ts -> src/modules/scenes/repository.ts
- src/modules/motion/service.ts -> src/modules/scenes/index.ts
- src/modules/motion/service.ts -> src/modules/motion/types.ts
- src/modules/motion/types.ts -> src/modules/scenes/index.ts
- src/modules/playback/index.ts -> src/modules/playback/service.ts
- src/modules/playback/service.ts -> src/config/constants.ts
- src/modules/playback/service.ts -> src/core/errors/app-error.ts
- src/modules/playback/service.ts -> src/core/observability/metrics.ts
- src/modules/playback/service.ts -> src/core/observability/processing-log.ts
- src/modules/playback/service.ts -> src/modules/feature-flags/index.ts
- src/modules/playback/service.ts -> src/modules/projects/repository.ts
- src/modules/playback/service.ts -> src/modules/scenes/repository.ts
- src/modules/processing/index.ts -> src/modules/processing/service.ts
- src/modules/processing/service.ts -> src/core/errors/app-error.ts
- src/modules/processing/service.ts -> src/core/observability/processing-log.ts
- src/modules/processing/service.ts -> src/infrastructure/jobs/trigger-dev.ts
- src/modules/processing/service.ts -> src/modules/feature-flags/index.ts

## Key Observations
- The repo uses a versioned API surface under `src/app/api/v1/**`, suggesting explicit external contract management.
- The codebase follows a layered architecture with controllers, modules, core utilities, infrastructure, and feature UI separated by concern.
- Persistence is modeled with Prisma, so database shape is centralized and strongly tied to generated client access patterns.
- A large number of route handlers indicates the repo acts as both a UI app and an API backend for project, scene, upload, auth, and maintenance workflows.
- The repository includes substantial documentation, which likely captures design decisions and implementation planning alongside the code.

## Unknowns / Issues
- 17 local imports could not be resolved from the markdown snapshot.

## Summary
This repository appears to be a Next.js parallax story composition platform with a layered backend, Prisma-backed persistence, and feature-oriented UI plus API workflows for projects, scenes, uploads, preview, and authentication.
