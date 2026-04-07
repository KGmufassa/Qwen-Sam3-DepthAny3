# Caching And Performance Plan

## Document Purpose

This document defines the MVP caching strategy and performance expectations.

It focuses on:

- what should be cached
- what should not be cached
- how repeated expensive work is avoided
- performance budgets for core user flows

---

## Performance Principles

- cache expensive deterministic outputs when safe
- do not cache hidden semantic state
- prioritize responsiveness of the editor and preview
- preserve correctness over aggressive optimization
- use stable keys tied to artifacts, checksums, and model/runtime identity

---

## Cache Targets

The MVP should consider caching for:

- normalized source images
- stitched scene outputs
- segmentation session context or embeddings when available
- canonical depth outputs
- preview derivatives
- export outputs where scene graph state is unchanged

---

## Normalization Caching

If the same source image is reused without changes:

- normalization should not be recomputed unnecessarily

Suggested cache key inputs:

- source image checksum
- normalization options

---

## Stitch Caching

If the same ordered image set and stitch options are reused:

- stitched outputs should be cacheable

Suggested cache key inputs:

- ordered source image checksums
- stitch options
- stitch runtime/version identity

---

## Segmentation Caching

Segmentation outputs themselves may be prompt-dependent, but reusable context may be cached if supported by the runtime.

Recommended MVP posture:

- allow caching of segmentation session context or embeddings when valid
- do not assume final masks are reusable across semantically different prompts

---

## Depth Caching

Depth generation should support deterministic caching.

Suggested cache key inputs:

- stitched scene artifact checksum
- depth model/version
- relevant depth options

Cached depth should include:

- canonical depth artifact
- preview depth artifact
- reusable metadata if valid

---

## Preview Derivative Caching

Preview-supporting derivatives may be cached when based on stable scene state.

Examples:

- thumbnails
- medium-specific derived payloads
- static preview snapshots if introduced later

Preview cache must not become a hidden source of truth.

---

## Export Caching

Export caching may be used when:

- scene graph state is unchanged
- active artifacts are unchanged
- export settings are unchanged

Suggested export cache key inputs:

- scene graph version or equivalent scene state checksum
- active artifact version references
- export settings

---

## What Not To Cache Aggressively

The MVP should avoid overly aggressive caching of:

- transient editor interaction state
- unaccepted segmentation candidates as canonical truth
- failed outputs
- hidden derived semantics not backed by saved scene state

---

## Performance Budget Categories

The MVP should define performance expectations for:

- upload to initial stitched readiness
- segmentation response cadence
- depth turnaround
- editor load
- preview responsiveness
- export turnaround

---

## Recommended MVP Performance Targets

These are planning targets, not yet implementation guarantees.

### Upload and stitch

Goal:

- the user should receive visible progress quickly
- the system should avoid long silent periods

### Segmentation

Goal:

- prompt-to-feedback should feel iterative, not batch-only

### Depth

Goal:

- depth generation should feel like a bounded asynchronous step, not an indefinite background mystery

### Editor load

Goal:

- the editor should open quickly once enough scene state exists

### Preview

Goal:

- preview should remain smooth enough to validate parallax behavior on the target medium

### Export

Goal:

- export should be bounded, visible, and retryable

Exact numeric budgets can be tuned later, but the product must define them before implementation is considered production-ready.

---

## Recommended Concrete Budget Fields

The implementation team should track at least:

- time to stitched-scene availability
- time to first segmentation result
- time to depth completion
- time to editor ready state
- preview frame stability under normal scene size
- time to export bundle availability

---

## Preview Performance Rules

Preview performance should be protected by:

- avoiding unnecessary recomputation on every minor UI event
- deriving runtime payloads from saved state predictably
- selecting medium-specific behavior explicitly

The preview should not require all expensive pipeline stages to rerun to test medium switches if scene state is unchanged.

---

## Responsive Performance Considerations

Because the MVP supports:

- phone
- tablet
- desktop

the system should avoid treating each medium switch as a full recomputation of unrelated expensive work.

Medium switching should ideally reuse:

- scene graph state
- active artifact references
- existing depth outputs

and only change runtime mapping behavior where possible.

---

## Cache Invalidation Principles

Invalidate caches when:

- source images change
- stitched scene source ordering changes
- model/runtime version changes
- relevant scene graph settings change
- export settings change

Avoid broad invalidation when only unrelated UI state changes.

---

## Metrics To Track

The MVP should eventually track:

- cache hit rate for stitched outputs
- cache hit rate for depth outputs
- export cache reuse
- preview load time by medium
- job queue latency by worker family

---

## Out-Of-Scope Performance Features

The MVP does not require:

- advanced distributed cache infrastructure
- predictive prewarming for all workers
- full adaptive autoscaling based on performance telemetry

---

## Freeze Criteria

This plan is ready to freeze when:

- cache targets are accepted
- invalidation principles are accepted
- performance budget categories are accepted
- responsive preview expectations are accepted

---

## Final Performance Statement

The MVP performance strategy relies on caching deterministic expensive outputs such as normalized images, stitched outputs, and depth results while keeping editor and preview responsiveness centered on saved scene state and explicit medium selection rather than recomputation of heavy processing stages.
