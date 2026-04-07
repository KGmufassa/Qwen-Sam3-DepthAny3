# Dependency Gate Plan

## Document Purpose

This document defines the mandatory planning and implementation gates that must be passed before downstream work can proceed.

Its purpose is to make sequencing explicit and prevent work from starting on unstable assumptions.

---

## Why Gates Are Needed

This project spans:

- frontend editor work
- API contract work
- stitched scene modeling
- artifact storage
- worker orchestration
- preview rendering
- export generation
- parallax mapping

Without hard gates, teams can easily build on assumptions that later change.

Typical failure patterns include:

- preview built before coordinate math is frozen
- editor history designed before layer and group semantics are defined
- export logic built before artifact rules are agreed
- worker integration started before API contracts are stable
- stitched-scene assumptions drifting across preview and export

Gates prevent those failures.

---

## Gate Philosophy

Each gate exists to answer one question:

- is the next layer of work safe to begin?

A gate is passed only when:

- required inputs are complete
- approval conditions are met
- downstream assumptions are stable enough to build on

---

## Gate Structure

Every gate contains:

- objective
- required inputs
- approval criteria
- blocked work if not passed
- unlocked work once passed

---

## Gate 1: Scope Freeze

### Objective

Freeze the MVP boundary before contract design begins.

### Required inputs

- `MVP Scope Plan`
- `Decision Log Plan`

### Approval criteria

- in-scope features are explicit
- non-goals are explicit
- release boundary is explicit
- Qwen refinement is confirmed optional
- multi-image stitched MVP scope is confirmed
- grouping and parallax capabilities are confirmed as MVP features

### Blocked work if not passed

- final schema design
- final API contract design
- editor UX finalization
- delivery schedule commitments

### Unlocked work

- architecture finalization
- contract planning
- mock integration planning

---

## Gate 2: Strategy Alignment

### Objective

Ensure the project has one coherent architectural direction.

### Required inputs

- `Unified Architecture Plan`
- approved Stage 1 decisions from the decision log

### Approval criteria

- control plane versus worker plane split is explicit
- local app source-of-truth rule is explicit
- worker responsibilities are explicit
- preview and export share a common scene-graph source
- stitched scene is modeled as one continuous scroll canvas
- grouping is a first-class scene and runtime concept
- group inheritance and bounded scroll participation are architecturally accounted for
- responsive parallax strategy for phone, tablet, and desktop is architecturally accounted for

### Blocked work if not passed

- worker contract finalization
- artifact lifecycle finalization
- deployment plan finalization

### Unlocked work

- schema planning
- API/job planning
- runtime contract planning

---

## Gate 3: Contract Freeze

### Objective

Freeze the system contracts that everything else will depend on.

### Required inputs

- `Data Schema And Scene Graph Plan`
- `API And Job Contract Plan`
- `Canonical Math Plan`
- `Worker Runtime Contract Plan`

### Approval criteria

- entity definitions are complete
- stitched scene entity model is complete
- source-image-to-stitched-scene relationships are defined
- layer semantics are frozen
- group semantics are frozen
- group inheritance rules are frozen
- artifact identity model is frozen
- coordinate spaces are frozen
- bounded scroll segment mapping is frozen
- cross-image depth normalization rules are frozen
- parallax data contracts are frozen
- responsive parallax contract is frozen
- request/response patterns are frozen
- worker input/output contracts are frozen

### Blocked work if not passed

- final editor behavior design
- preview implementation
- export implementation
- real worker integration

### Unlocked work

- mock end-to-end workflow
- frontend editor finalization
- persistence implementation
- route/controller implementation

---

## Gate 4: Mock End-To-End Ready

### Objective

Prove the full app workflow with deterministic mocks before real ML integration.

### Required inputs

- mock-first integration plan
- approved API contracts
- approved scene graph shape

### Approval criteria

- multi-image upload flow works to completion
- mock stitch stage returns valid stitched scene metadata
- mock segmentation returns valid candidate structure
- committed masks create valid layer seeds
- mock extraction produces editor-loadable layers
- mock depth produces valid stitched-scene layer metrics
- mock grouping and parallax behavior load correctly
- mock export produces valid bundle metadata
- mock preview demonstrates continuous stitched scroll with bounded group participation
- mock preview demonstrates medium-aware parallax behavior for phone, tablet, and desktop

### Blocked work if not passed

- reliance on real worker integration for user-flow validation
- preview acceptance testing
- export acceptance testing

### Unlocked work

- real worker substitution
- UX iteration with stable flow
- persistence hardening

---

## Gate 5: Base Pipeline Stable

### Objective

Verify that the baseline user flow works with real core integrations.

### Required inputs

- real stitching integration
- real segmentation integration
- real extraction pipeline
- real depth pipeline
- preview path
- export path

### Approval criteria

- multi-image upload works
- stitching or alignment works
- segmentation works
- mask commit works
- layer extraction works
- editor loads real stitched-scene layers
- groups can be created and assigned correctly
- depth outputs support stitched-scene behavior
- group-based parallax behavior works in preview
- continuous stitched scroll works in preview
- responsive parallax behavior works for phone, tablet, and desktop using scene defaults and group overrides
- export preserves grouped parallax behavior and layer overrides

### Blocked work if not passed

- Qwen refinement integration
- matting polish beyond core necessity
- release readiness signoff

### Unlocked work

- reliability hardening
- quality tuning
- optional difficult-layer workflows

---

## Gate 6: Reliability Baseline

### Objective

Ensure the MVP is usable under normal failure and retry conditions.

### Required inputs

- job retry rules
- timeout handling
- health checks
- failure UI
- artifact cleanup policy

### Approval criteria

- failures are visible
- retries do not duplicate final state incorrectly
- late job results are handled safely
- stalled jobs surface meaningful status
- worker unavailability degrades gracefully

### Blocked work if not passed

- release signoff

### Unlocked work

- QA signoff
- release candidate packaging

---

## Gate 7: MVP Release Readiness

### Objective

Confirm the product meets its declared MVP bar.

### Required inputs

- QA and release readiness plan
- acceptance evidence from prior gates

### Approval criteria

- all MVP success criteria are satisfied
- preview/export consistency is acceptable
- grouped parallax behavior is preserved through export
- stitched-scene continuity is preserved through preview and export
- responsive parallax behavior is preserved through preview and export for supported media profiles
- core workflows are documented
- known limitations are explicit
- optional features are not blocking release

### Blocked work if not passed

- MVP release

### Unlocked work

- MVP shipment
- post-MVP planning

---

## Gate Dependency Map

The gates depend on each other in this order:

1. `Scope Freeze`
2. `Strategy Alignment`
3. `Contract Freeze`
4. `Mock End-To-End Ready`
5. `Base Pipeline Stable`
6. `Reliability Baseline`
7. `MVP Release Readiness`

This order is strict.

---

## What Can Run In Parallel

After `Scope Freeze`:

- architecture planning
- decision logging
- draft UX planning
- draft deployment planning

After `Contract Freeze`:

- frontend workflow implementation
- backend route/controller implementation
- mock integration
- artifact registration implementation
- worker adapter development

After `Base Pipeline Stable`:

- reliability hardening
- QA execution
- optional refinement work

---

## Stop-Work Rules

Work must pause and return to the relevant gate if:

- stitched scene continuity assumptions change
- layer semantics change
- source-of-truth ownership changes
- coordinate spaces change
- preview and export diverge structurally
- worker contracts no longer match API assumptions
- group semantics or inheritance rules change
- responsive parallax representation changes

These are gate-breaking events.

---

## Approval Ownership

Each gate must have explicit signoff ownership.

Recommended ownership:

- product owner for `Scope Freeze`
- architecture owner for `Strategy Alignment`
- platform plus product owner for `Contract Freeze`
- engineering owner for `Mock End-To-End Ready`
- engineering plus product owner for `Base Pipeline Stable`
- platform owner for `Reliability Baseline`
- product plus engineering for `MVP Release Readiness`

---

## Success Criteria

This plan is successful when:

- downstream work starts on stable assumptions
- rework from contract churn is reduced
- optional features stop delaying baseline progress
- release readiness is evaluated against explicit gates rather than intuition

---

## Final Gate Policy

No workstream is considered ready to move forward just because implementation has started.

The next phase begins only when the current gate is explicitly passed.
