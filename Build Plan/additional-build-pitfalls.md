# Additional Build Pitfalls To Consider

This list focuses on risks and gaps that are not fully covered, or that deserve more explicit handling, in the current build plan.

## Product And UX Pitfalls

- Ambiguous user mental model between `mask`, `layer`, `artifact`, and `refinement` can make the editor feel unpredictable if the UI language is not consistent.
- Users may not understand why a generated segmentation candidate differs from the final committed layer unless approval and commit states are visually distinct.
- If depth suggestions visibly conflict with user expectations, trust in the overall pipeline can drop quickly even when manual override exists.
- Scroll-parallax previews can look good in-editor but feel excessive on real pages unless motion limits are calibrated against real browser scrolling behavior.
- Large uploads with long async processing stages need strong progress messaging, otherwise users will assume the app is stuck.
- Undo/redo expectations will break if async AI actions, manual layer edits, and refinement toggles do not have clearly defined history semantics.
- If layer naming is weak or fully generic, projects become unmanageable once a scene has more than a handful of extracted elements.
- The app may feel destructive unless the UI makes version switching, reverting, and “active asset” state obvious.

## Data Model And State Pitfalls

- Scene versioning can become expensive and hard to reason about if every change snapshots too much state instead of storing small semantic deltas.
- Concurrent edits from multiple browser tabs or sessions can silently overwrite scene graph state if optimistic concurrency or revision checks are missing.
- If artifacts are immutable but references are not validated carefully, scenes can end up pointing to incompatible or stale outputs.
- Bounding boxes, masks, RGBA crops, and depth statistics can drift out of sync when a layer is re-refined but dependent metadata is not recomputed.
- Coordinate-system mismatches between original image space, normalized image space, canvas space, and exported runtime space are a common source of subtle bugs.
- Floating-point drift in transforms and parallax values can accumulate if the editor repeatedly serializes and rehydrates runtime state.
- Cache invalidation will be error-prone if manual edits and AI outputs share identifiers without explicit lineage metadata.

## ML And Image Processing Pitfalls

- SAM-style segmentation often fails on transparent, reflective, hair-like, or low-contrast regions, so the fallback UX needs to be stronger than “try again.”
- Depth estimation on layered scenes can be semantically wrong for mirrors, shadows, sky regions, glass, and overlapping objects.
- Refinement quality can improve edge detail while damaging semantic content if matte/refine stages are applied to the wrong crop or with inconsistent padding.
- Thin structures can be lost during resizing, mask rasterization, or PNG/WebP conversion if intermediate formats are chosen for convenience instead of fidelity.
- Crop padding policy matters: too little padding clips edges, too much padding confuses refinement and increases compute cost.
- Different workers may interpret color channels, premultiplication, alpha conventions, and EXIF orientation differently unless normalization is centralized.
- Model upgrades can silently change output distributions and break cache correctness, quality thresholds, and UI expectations unless version pinning is strict.
- Prompt-driven iterative segmentation can produce non-deterministic outputs, which complicates bug reports and acceptance testing.

## Performance And Cost Pitfalls

- Browser memory pressure may come from thumbnails, preview textures, masks, and undo history together, not just from the base source image.
- Full-resolution assets can be unnecessarily loaded into the editor if preview/full-res selection rules are not enforced aggressively.
- GPU worker autoscaling can look healthy while queue latency is still poor if cold starts dominate runtime.
- The optional Qwen stage can still become a cost sink if “suggested” refinement is over-triggered or if retries are not capped.
- Export generation can become the hidden bottleneck because it touches many artifacts even when inference is offloaded.
- Signed URL churn can add avoidable latency if each pipeline step re-downloads the same inputs instead of reusing cached intermediate artifacts.
- Large-object storage costs can grow quickly if every refinement variant, preview, and export bundle is retained forever without retention rules.

## Reliability And Operations Pitfalls

- Cancellation is harder than marking a job canceled; workers also need to stop work, avoid uploading partial outputs, and avoid committing late results.
- Retry logic can create duplicate artifacts or duplicate layer versions unless writes are idempotent at the artifact-registration boundary.
- Partial pipeline success is easy to mishandle; for example, mask extraction may succeed while artifact registration fails, leaving orphaned files.
- Queue poisoning is possible if malformed jobs keep retrying without dead-letter handling or error bucketing.
- Health checks that only test process liveness will miss bad model mounts, invalid credentials, exhausted disks, and broken signed URL flows.
- Worker startup can race with model downloads or lazy initialization, causing the system to accept jobs before the runtime is truly ready.
- Time synchronization matters when using short-lived signed URLs and request timestamp validation across local services and Runpod.
- Backpressure needs to exist at the API layer, otherwise users can spam expensive jobs faster than queues can absorb them.

## Security And Compliance Pitfalls

- Upload finalization must verify content type, file size, and actual image decodability; trusting client metadata is not enough.
- Image parsing libraries can be a security boundary, especially with malformed or oversized files designed to exhaust memory.
- Signed URLs need narrow scope and short lifetimes, or they become a quiet data-exposure vector.
- Multi-tenant isolation can break if artifact keys, cache keys, or project IDs are guessable or insufficiently namespaced.
- Logs can accidentally capture signed URLs, prompt payloads, or internal storage locations unless explicit redaction rules exist.
- If user images may contain sensitive data, retention, deletion, and export-history rules need to be explicit early rather than retrofitted later.

## Frontend Implementation Pitfalls

- PixiJS and React ownership boundaries can erode over time, leading to duplicated state and hard-to-reproduce rendering bugs.
- Hit-testing, selection bounds, and drag handles can become inaccurate on zoomed or transformed layers if transform math is not centralized.
- Texture disposal bugs may only appear after long editing sessions, especially when switching scenes or toggling refined variants repeatedly.
- SSE-only progress delivery can feel brittle in browsers, proxies, or serverless environments unless reconnection and replay behavior are defined.
- Keyboard shortcuts, accessibility states, and focus management are easy to defer, but the editor will feel broken without them.
- Mobile and touch behavior may be substantially different from desktop even if the layout is responsive; pointer interactions need separate validation.

## Backend And API Pitfalls

- API contracts may look stable while semantic behavior remains underspecified, especially around overwrite rules, retries, and eventual consistency.
- Long-running job status endpoints need pagination or truncation rules for event logs, or payload sizes will become inefficient quickly.
- Webhook or polling behavior from external inference providers can introduce duplicate completion events that must be safely ignored.
- If project deletion is added later, cascading cleanup of scenes, artifacts, cache entries, and storage objects becomes operationally risky.
- Export reproducibility will break if the runtime depends on implicit defaults that are not stored in the scene graph or export manifest.

## Testing And Release Pitfalls

- Happy-path demos can pass while edge cases fail unless the test set includes hair, transparent objects, overlapping subjects, very large images, and low-contrast scenes.
- Visual regression testing is important here; purely functional tests will miss many quality and compositing defects.
- Local development with mocked GPU stages can hide production-only failures in memory usage, timeout behavior, and artifact-size limits.
- End-to-end tests need deterministic fixtures and pinned model/runtime versions, or they will be noisy and hard to trust.
- Manual QA should cover resume/retry/reconnect flows, not just fresh runs from upload to export.

## Decisions To Make Explicit Early

- Define maximum supported source image dimensions, file size, and per-project storage budget.
- Define whether the editor is single-user only for MVP or whether concurrent editing must be prevented explicitly.
- Define artifact retention and cleanup rules for rejected masks, failed jobs, previews, and old exports.
- Define what “cancel,” “retry,” and “revert” mean at both the job level and the scene-version level.
- Define whether export output must be pixel-identical to editor preview or only semantically equivalent.
- Define which failures are user-fixable in the UI versus which should be hidden behind internal retry logic.
