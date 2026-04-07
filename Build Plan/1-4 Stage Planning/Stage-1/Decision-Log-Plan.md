# Decision Log Plan

## Document Purpose

This document defines how architectural and product decisions will be recorded, classified, approved, and frozen throughout MVP planning and implementation.

The goal is to avoid silent drift in foundational assumptions.

This document does not make every decision itself. It defines:

- which decisions must be logged
- how decisions are categorized
- when decisions become frozen
- which decisions can be revisited
- what downstream plans depend on them

---

## Why This Exists

This project has several high-cost decision areas:

- stitched scene structure
- scene graph structure
- coordinate systems
- artifact identity and storage rules
- preview versus export fidelity
- worker boundaries
- synchronous versus async behavior
- where state ownership lives
- grouping semantics
- parallax mapping behavior

If these are not captured formally, the same questions will be answered differently across:

- frontend implementation
- API design
- worker integration
- export logic
- QA expectations

That leads to rework.

---

## Decision Log Goals

The decision log must:

- create one authoritative record of foundational decisions
- expose whether a decision is provisional or frozen
- make downstream impact explicit
- reduce contradictory assumptions across plans
- support fast planning without hidden redesign risk

---

## Decision Categories

Every logged decision must belong to one of the following categories.

### Product scope

Examples:

- multi-image stitched MVP
- Qwen refinement optional versus required
- export bundle required versus deferred

### Domain model

Examples:

- what counts as a `Layer`
- what counts as a `Group`
- what counts as an `Artifact`
- whether a committed mask is a layer seed or a layer itself

### System architecture

Examples:

- local app as source of truth
- worker responsibilities
- control plane versus worker plane split
- stitch stage ownership

### API contract

Examples:

- async job contract shape
- idempotency rules
- status polling versus push

### Data and storage

Examples:

- artifact registration requirements
- canonical checksum usage
- object storage structure
- stitched source-image provenance rules

### Math and rendering

Examples:

- canonical coordinate spaces
- transform ordering
- depth-to-motion mapping
- preview versus export equivalence
- cross-image depth normalization
- group-level scroll segment mapping

### Reliability and operations

Examples:

- timeout rules
- retry rules
- cancellation semantics
- retention rules

### UX behavior

Examples:

- what is undoable
- what happens when segmentation fails
- whether export must block on unresolved warnings
- how groups behave in the editor

---

## Decision States

Every decision must have one of these states.

### Proposed

The idea exists but is not yet agreed.

### Drafted

The preferred direction is identified, but downstream work should not treat it as final.

### Approved

The decision is accepted for active planning and implementation.

### Frozen

The decision is now treated as a contract boundary. Changing it requires explicit review because downstream work already depends on it.

### Superseded

The decision was previously active but has been replaced.

---

## Required Decision Fields

Every decision entry must include:

- decision id
- title
- category
- current state
- date opened
- owner
- summary
- rationale
- options considered
- chosen option
- downstream impact
- dependent plans
- reopen conditions

---

## Decision Priority Levels

Each decision must be labeled by impact level.

### Critical

Changing this would force rework across multiple plans or code areas.

Examples:

- stitched scene structure
- scene graph structure
- group semantics
- source-of-truth ownership
- canonical coordinate spaces

### High

Changing this would affect a major subsystem but not the full platform.

Examples:

- export manifest shape
- retry model
- job lifecycle semantics
- parallax inheritance rules

### Medium

Changing this affects workflow details but does not reshape major contracts.

Examples:

- layer naming defaults
- preview control labels
- default worker timeout values

### Low

Changing this has minimal architectural cost.

Examples:

- document naming conventions
- non-critical UI wording

---

## Decisions That Must Be Logged Before Contract Freeze

The following decisions are mandatory before Stage 2 finalization.

### MVP boundary decisions

- MVP supports multi-image stitched scenes
- export bundle is required for MVP
- Qwen refinement is optional and not baseline

### Ownership decisions

- local app is source of truth for scene state
- workers are pure execution services
- preview and export both derive from saved scene graph state

### Domain decisions

- stitched scene is one continuous scroll canvas
- layer is a versioned scene object, not just a mask file
- group is both an organizational and runtime scene concept
- committed masks create layer seeds
- artifacts are first-class registered entities

### Grouping and parallax decisions

- parallax mappings apply at both group and layer level
- layers inherit group behavior by default
- one layer belongs to zero or one group
- groups are flat only
- groups can map to bounded scroll segments within the continuous stitched scene
- responsive parallax must support phone, tablet, and desktop
- scene-level medium-aware defaults are required
- group-level medium-specific overrides are supported
- layer-level medium-specific overrides are not part of baseline MVP

### Math decisions

- canonical coordinate spaces
- transform composition order
- normalized image rules
- cross-image depth normalization rules
- depth metric storage rules

### Runtime decisions

- core processing stages are async jobs
- retryable versus terminal failures
- health/readiness expectations for workers
- stitch stage ownership and outputs

---

## Decisions That Can Stay Draft Until Workflow Plans

These may remain drafted until later planning stages:

- exact editor undo granularity
- exact fallback copy in UI
- non-critical preview interaction defaults
- optional low-cost refinement heuristics

---

## Freeze Policy

### Stage 1 freeze

The following can be frozen at Stage 1:

- MVP boundary
- source-of-truth rule
- worker role rule
- Qwen optionality rule
- stitched scene continuity rule
- grouping and inheritance rules

### Stage 2 freeze

The following must be frozen at Stage 2:

- scene graph shape
- artifact registration rules
- coordinate space rules
- API/job contract patterns
- cross-image depth normalization rules
- group scroll segment model

### Stage 3 freeze

The following can be frozen at Stage 3:

- editor behavior semantics
- history semantics
- fallback behaviors

### Stage 4 freeze

The following can be frozen at Stage 4:

- deployment defaults
- performance targets
- release readiness checklists

---

## Reopen Rules

A frozen decision may only be reopened if:

- a higher-priority decision conflicts with it
- implementation proves the decision impossible within MVP constraints
- the decision creates unacceptable UX or reliability failure
- the MVP boundary itself changes

Reopening must document:

- why the original decision failed
- what changed
- what downstream plans must be updated

---

## Downstream Dependency Mapping

The decision log must be referenced by these documents:

- MVP Scope Plan
- Unified Architecture Plan
- Data Schema And Scene Graph Plan
- API And Job Contract Plan
- Canonical Math Plan
- Worker Runtime Contract Plan
- Editor UX And Interaction Plan
- Artifact And Export Lifecycle Plan

If any of these plans contain assumptions not reflected in the decision log, the log wins.

---

## Required Initial Decisions

The following entries should be created immediately.

### D-001: MVP supports multi-image stitched scenes

- category: product scope
- priority: critical
- state: approved

### D-002: Local app is the source of truth

- category: system architecture
- priority: critical
- state: approved

### D-003: Workers are pure inference/execution services

- category: system architecture
- priority: critical
- state: approved

### D-004: Qwen refinement is optional for MVP

- category: product scope
- priority: critical
- state: approved

### D-005: Preview and export must derive from the same scene graph

- category: math and rendering
- priority: critical
- state: approved

### D-006: Stitched scene is one continuous scroll canvas

- category: domain model
- priority: critical
- state: approved

### D-007: Layers are versioned scene objects, not raw files

- category: domain model
- priority: critical
- state: approved

### D-008: Artifacts are registered first-class entities

- category: data and storage
- priority: critical
- state: approved

### D-009: Groups are both organizational and runtime scene entities

- category: domain model
- priority: critical
- state: approved

### D-010: Parallax mappings apply at both group and layer level

- category: math and rendering
- priority: high
- state: approved

### D-011: Layers inherit group behavior by default

- category: UX behavior
- priority: high
- state: approved

### D-012: One layer belongs to at most one group

- category: domain model
- priority: high
- state: approved

### D-013: Groups are flat only for MVP

- category: domain model
- priority: high
- state: approved

### D-014: Groups can map to bounded scroll segments within the continuous stitched scene

- category: math and rendering
- priority: high
- state: approved

### D-015: Cross-image depth normalization is required for stitched-scene behavior

- category: math and rendering
- priority: critical
- state: approved

### D-016: Responsive parallax supports phone, tablet, and desktop

- category: math and rendering
- priority: critical
- state: approved

### D-017: Scene-level medium-aware defaults define baseline responsive parallax behavior

- category: math and rendering
- priority: high
- state: approved

### D-018: Group-level medium-specific overrides are supported for MVP

- category: UX behavior
- priority: high
- state: approved

### D-019: Layer-level medium-specific overrides are not required for baseline MVP

- category: product scope
- priority: medium
- state: approved

### D-020: All heavy processing stages are modeled as async jobs

- category: API contract
- priority: high
- state: approved

### D-021: Previous single-image-only MVP assumption is superseded

- category: product scope
- priority: critical
- state: superseded

---

## Operating Rule

No dependency-sensitive plan may be finalized unless all critical decisions it depends on are either:

- approved, or
- frozen

---

## Success Criteria

This plan is successful when:

- foundational assumptions stop moving silently
- planning documents reference common decisions
- dependency-sensitive plans can freeze cleanly
- rework caused by contradictory assumptions is reduced

---

## Final Policy Statement

The decision log is the control surface for architectural certainty.

If a foundational choice affects multiple plans or multiple implementation areas, it must be recorded here before downstream work is allowed to treat it as settled.
