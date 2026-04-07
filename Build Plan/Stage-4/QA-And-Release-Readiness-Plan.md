# QA And Release Readiness Plan

## Document Purpose

This document defines how the MVP will be validated before release.

It focuses on:

- what must be tested
- what quality risks must be covered
- what manual QA flows matter most
- what conditions must be true before MVP release

---

## QA Principles

- test the real user flow, not isolated happy paths only
- validate both correctness and recoverability
- verify preview/export consistency
- use representative stitched-scene examples
- test medium-aware behavior deliberately

---

## Required Test Categories

The MVP should be validated across:

- upload and stitching
- segmentation
- extraction
- grouping
- depth and normalization
- preview
- export
- retry and recovery
- responsive behavior

---

## Golden Test Scene Set

The MVP should define a small but meaningful set of representative stitched-scene inputs.

Recommended categories:

- simple two-image stitched scene
- multi-image stitched scene with clear foreground/midground/background separation
- difficult segmentation case
- difficult depth case
- scene with multiple groups and bounded scroll segments

This set should be reused for:

- manual QA
- regression checks
- preview/export consistency checks

---

## Functional QA Areas

### Upload and stitch

Verify:

- multiple images upload correctly
- ordering is respected
- stitched scene is created correctly
- source provenance remains intact

### Segmentation

Verify:

- segmentation candidates are returned
- accepted masks commit correctly
- unaccepted masks do not become layers

### Extraction

Verify:

- extracted layers are created correctly
- thumbnails and active versions are correct
- failures do not corrupt unaffected layers

### Grouping

Verify:

- groups can be created
- groups can be renamed and reordered
- layers can be assigned and removed
- a layer cannot belong to more than one group

### Depth

Verify:

- depth outputs are generated
- normalized layer metrics are attached
- manual override remains possible when defaults are poor

### Preview

Verify:

- preview reflects saved scene graph
- medium switching works
- grouped motion behaves as configured
- bounded scroll segments behave as configured

### Export

Verify:

- export succeeds from saved scene state
- export bundle reflects active layer versions
- export preserves group and responsive behavior

---

## Responsive QA Areas

The MVP must be checked for:

- phone preview behavior
- tablet preview behavior
- desktop preview behavior
- scene-level responsive defaults
- group-level medium overrides

The purpose is not perfect visual identity across all devices, but semantic correctness of configured behavior.

---

## Failure And Recovery QA

The MVP must test:

- upload retry
- stitch retry
- segmentation retry
- extraction retry
- depth retry
- export retry
- worker unavailable behavior
- timeout handling

These tests are required because failure handling is part of the MVP promise.

---

## Preview/Export Consistency QA

The MVP must explicitly test:

- same layer order
- same group behavior
- same responsive medium rules
- same active layer versions
- same bounded segment logic

Minor rendering differences are acceptable.

Semantic divergence is not.

---

## Manual QA Checklist Categories

Manual QA should include:

- fresh project flow
- partial-completion flow
- recovery flow
- medium-switch flow
- export flow

Manual QA should not only test ideal clean runs.

---

## Release Blockers

The MVP should not ship if any of these are unresolved:

- stitched scenes cannot be created reliably
- groups do not persist correctly
- preview and export use different semantics
- responsive medium behavior is broken or misleading
- failed stages silently corrupt scene state
- active layer version selection is not respected in export

---

## Suggested Readiness Checklist

Before release, confirm:

- all Stage 1 assumptions remain valid
- all Stage 2 contracts remain valid
- all Stage 3 workflow behavior is implemented consistently
- representative stitched scenes pass end-to-end flow
- retries and failures are visible and recoverable
- preview/export equivalence is acceptable

---

## Out-Of-Scope QA Features

The MVP does not require:

- enterprise certification workflows
- advanced automated visual diff infrastructure
- large-scale device lab coverage

---

## Freeze Criteria

This plan is ready to freeze when:

- required QA categories are accepted
- release blockers are accepted
- preview/export consistency requirements are accepted
- responsive QA requirements are accepted

---

## Final QA Statement

The MVP QA and release readiness strategy validates the stitched-scene workflow end to end, treats failure and retry behavior as release-critical, and requires semantic consistency between preview and export across supported medium profiles before shipment.
