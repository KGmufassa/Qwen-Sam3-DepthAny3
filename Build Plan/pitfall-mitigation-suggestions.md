# Suggestions To Fix Or Reduce Common Pitfalls

This file gives simple ways to fix or reduce the risks listed in the pitfalls document.

## Product And UX

- Use the same words everywhere in the app.
  Example: always use `Mask`, `Layer`, `Refined Layer`, and `Export`.
- Make AI steps easy to see.
  Show clear states like `Generating`, `Ready for Review`, `Accepted`, and `Rejected`.
- Let users override AI choices.
  Depth order, layer names, and refinement should always be editable by hand.
- Keep motion gentle by default.
  Start with small parallax movement so the preview does not feel too strong.
- Show progress for long jobs.
  Use progress bars, status text, and estimated wait messages.
- Make undo rules simple.
  Treat each meaningful user action as one undo step.

## Data And State

- Keep one source of truth.
  The scene graph should be the main record for what the project currently is.
- Store small changes instead of full copies when possible.
  This keeps version history easier to manage.
- Add revision numbers or version checks.
  This helps stop one browser tab from overwriting another by mistake.
- Recompute related metadata after important changes.
  If a layer changes, refresh its box, mask stats, and depth stats.
- Pick one coordinate system policy and document it.
  Every service should know how image space, canvas space, and export space relate.

## AI And Image Processing

- Do not trust one model result too much.
  Give users tools to fix hard cases like hair, glass, shadows, and transparent objects.
- Normalize images once at the start.
  Fix orientation, color format, alpha handling, and image size in one shared pipeline.
- Use safe crop padding rules.
  Add enough padding to protect edges, but keep it consistent across workers.
- Pin model versions.
  If a model changes, treat it as a new version and update cache keys.
- Keep hard AI steps optional.
  Expensive refinement should stay user-invoked, not automatic.

## Performance And Cost

- Use smaller preview assets in the editor.
  Save full-resolution files for extraction and export only.
- Free memory aggressively.
  Dispose old textures, thumbnails, and temporary masks when they are no longer needed.
- Cache expensive outputs.
  Reuse normalized images, depth maps, and masks when the inputs have not changed.
- Add limits to expensive features.
  Cap retries, job size, and how often heavy refinement can run.
- Set storage cleanup rules early.
  Remove failed outputs, rejected masks, and old previews after a set time.

## Reliability And Operations

- Make jobs idempotent.
  Retrying the same job should not create duplicate artifacts or duplicate scene updates.
- Support true cancellation.
  Workers should stop work, skip uploads, and avoid saving late results after cancel.
- Add dead-letter handling.
  Bad jobs should move aside instead of retrying forever.
- Use stronger health checks.
  Check storage, queue access, model config, and ready state, not just “process is alive.”
- Add backpressure.
  Slow or reject new expensive jobs when the system is overloaded.

## Security

- Validate uploads on the server.
  Check file type, file size, and whether the file can actually be decoded as an image.
- Keep signed URLs short-lived.
  Give them only the access they need, for only as long as needed.
- Redact sensitive logs.
  Do not store signed URLs, private prompts, or secret storage paths in logs.
- Namespace all project data carefully.
  Artifact keys, cache keys, and project IDs should not collide across users.
- Define deletion rules early.
  Decide how users can delete projects, exports, and sensitive image data.

## Frontend

- Keep React and Pixi responsibilities separate.
  React should manage UI state, and Pixi should manage drawing.
- Centralize transform math.
  Selection boxes, dragging, zooming, and exporting should all use the same math rules.
- Plan for reconnects.
  SSE progress should recover cleanly if the browser refreshes or loses connection.
- Add keyboard and accessibility support early.
  This is much easier now than later.
- Test touch behavior separately.
  Mobile support needs more than a responsive layout.

## Backend And API

- Write down exact API behavior.
  Define what happens on retry, duplicate completion, overwrite, and partial failure.
- Keep event logs small and paginated.
  Large job histories should not produce huge API responses.
- Save enough data to reproduce exports.
  Export settings should live in the scene graph or export manifest, not in hidden defaults.
- Plan deletion carefully.
  Removing a project should safely clean up scenes, artifacts, cache entries, and storage objects.

## Testing

- Build a real test image set.
  Include hair, glass, overlap, low contrast, large files, and transparent objects.
- Add visual regression tests.
  Many bugs here will be visual, not just functional.
- Test with real worker behavior when possible.
  Mocked GPU flows can hide production problems.
- Make end-to-end tests stable.
  Use fixed fixtures, pinned model versions, and predictable settings.
- Test failure paths on purpose.
  Practice cancel, retry, reconnect, timeout, and partial-failure cases.

## Good Early Decisions

- Set clear limits for upload size, image dimensions, and project storage.
- Decide whether MVP supports one editor at a time or blocks concurrent editing.
- Define what `Cancel`, `Retry`, `Revert`, and `Delete` mean in exact terms.
- Decide how long artifacts, previews, and exports should be kept.
- Decide whether export output must match the editor preview exactly or just closely enough.
