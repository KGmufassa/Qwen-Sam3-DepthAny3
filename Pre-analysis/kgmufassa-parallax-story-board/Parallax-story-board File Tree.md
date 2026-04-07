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
    ├── apps/
    │   └── web/
    │       └── .next-dev/
    │           └── trace
    ├── design/
    │   ├── HTML/
    │   │   ├── authentication-mvp.html
    │   │   ├── landing-page-design-system.html
    │   │   ├── project-editor-final-mvp.html
    │   │   ├── saved-projects-dashboard-final.html
    │   │   └── settings-page-design-system.html
    │   └── webpages/
    │       ├── 00-shared-design-system.md
    │       ├── 01-landing-page.md
    │       ├── 02-auth-page.md
    │       ├── 03-project-editor-page.md
    │       ├── 04-preview-player-page.md
    │       ├── 05-projects-dashboard-page.md
    │       ├── 06-settings-page.md
    │       ├── 07-component-map.md
    │       └── Create-new-project-progression.md
    ├── docs/
    │   ├── Logs/
    │   │   ├── runtime-error-2026-03-24_00-54-37.md
    │   │   ├── runtime-error-2026-03-24_00-57-59.md
    │   │   ├── sprint-1-changelog-2026-03-16_01-05-32.md
    │   │   ├── UI-UX-logs-2026-03-17_22-41-59.md
    │   │   ├── UI-UX-logs-2026-03-17_22-56-02.md
    │   │   ├── UI-UX-logs-2026-03-17_23-45-12.md
    │   │   ├── UI-UX-logs-2026-03-17_23-53-50.md
    │   │   ├── UI-UX-logs-2026-03-18_23-31-47.md
    │   │   ├── UI-UX-logs-2026-03-18_23-50-59.md
    │   │   ├── UI-UX-logs-2026-03-18_23-55-13.md
    │   │   ├── UI-UX-logs-2026-03-20_00-00-00.md
    │   │   ├── UI-UX-logs-2026-03-22_12-00-00.md
    │   │   ├── UI-UX-logs-2026-03-22_13-00-00.md
    │   │   ├── UI-UX-logs-2026-03-22_14-00-00.md
    │   │   ├── UI-UX-logs-2026-03-22_14-20-00.md
    │   │   └── UI-UX-logs-2026-03-22_15-00-00.md
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
    │   ├── rule-packs/
    │   │   ├── ai-native.md
    │   │   ├── compliance.md
    │   │   ├── high-scale.md
    │   │   ├── multi-tenant.md
    │   │   ├── real-time.md
    │   │   └── saas.md
    │   ├── rules/
    │   │   └── architecture-rules.md
    │   ├── setup/
    │   │   ├── local-mvp.md
    │   │   └── mvp-decision-log.md
    │   ├── task/
    │   │   ├── Backendplan/
    │   │   │   ├── index.md
    │   │   │   ├── sprint-1/
    │   │   │   │   ├── check-build-list.md
    │   │   │   │   └── plan.md
    │   │   │   ├── sprint-2/
    │   │   │   │   ├── check-build-list.md
    │   │   │   │   └── plan.md
    │   │   │   └── sprint-3/
    │   │   │       ├── check-build-list.md
    │   │   │       └── plan.md
    │   │   ├── Frontendplan/
    │   │   │   ├── frontend-build-task-list.md
    │   │   │   ├── index.md
    │   │   │   ├── missing-route-report.md
    │   │   │   └── Webpage-errors.txt
    │   │   └── system/
    │   │       ├── core-system-tickets.md
    │   │       ├── mvp-system-task-list.md
    │   │       ├── parallel-system-tickets.md
    │   │       ├── project-editor-doc-alignment-checklist.md
    │   │       ├── project-editor-doc-alignment-implementation-plan.md
    │   │       ├── project-editor-element-parallax-mvp-execution-plan.md
    │   │       └── project-editor-grouped-parallax-mobile-first-execution-checklist.md
    │   └── templates/
    │       ├── ARCHITECTURE_TEMPLATE.md
    │       ├── FEATURES_BUILD_PLAN.md
    │       ├── FRONTEND_ARCHITECTURE_TEMPLATE.md
    │       └── TECHNICAL_PRD_TEMPLATE.md
    ├── log/
    │   └── visual-audit-2026-03-20.md
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
    ├── validation-reports/
    │   └── blank.md
    ├── .local/
    │   └── storage/
    │       └── projects/
    │           └── 57dbb5da-9823-4961-96b6-27e80a97662b/
    │               └── scenes/
    │                   ├── 05bc7602-fce3-48c9-9bca-7b2d24e28f51/
    │                   │   ├── v1/
    │                   │   │   └── manifest.json
    │                   │   ├── v2/
    │                   │   │   └── manifest.json
    │                   │   ├── v3/
    │                   │   │   └── manifest.json
    │                   │   └── v4/
    │                   │       └── manifest.json
    │                   ├── 6c28396e-0082-47d0-b0ad-8673189b2c6c/
    │                   │   ├── v1/
    │                   │   │   └── manifest.json
    │                   │   ├── v2/
    │                   │   │   └── manifest.json
    │                   │   ├── v3/
    │                   │   │   └── manifest.json
    │                   │   └── v4/
    │                   │       └── manifest.json
    │                   ├── 6e338340-6f10-4bb8-88c3-7971f1d04dd2/
    │                   │   ├── v1/
    │                   │   │   └── manifest.json
    │                   │   ├── v2/
    │                   │   │   └── manifest.json
    │                   │   ├── v3/
    │                   │   │   └── manifest.json
    │                   │   ├── v4/
    │                   │   │   └── manifest.json
    │                   │   ├── v5/
    │                   │   │   └── manifest.json
    │                   │   └── v6/
    │                   │       └── manifest.json
    │                   └── ab4452ac-8d76-4ec7-8200-5d3f0ab2124a/
    │                       ├── v1/
    │                       │   └── manifest.json
    │                       ├── v2/
    │                       │   └── manifest.json
    │                       ├── v3/
    │                       │   └── manifest.json
    │                       └── v4/
    │                           └── manifest.json
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
