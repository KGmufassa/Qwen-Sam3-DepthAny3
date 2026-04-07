# Vertical Release Slice Plan

## Document Purpose

This document defines the recommended incremental delivery order for the MVP using vertical slices instead of only horizontal subsystem completion.

It focuses on:

- what slices should be built first
- what each slice proves
- how slices reduce implementation risk
- how to stage work so progress is visible early

---

## Slice Principles

- each slice should produce a testable user-visible outcome
- slices should validate contracts before full complexity is introduced
- mock-first flow should unlock early integration
- optional features should not block baseline value

---

## Recommended Slice Order

The MVP should be built in these slices:

1. upload to mock stitched scene
2. real stitch to scene shell
3. real segmentation to committed layer seeds
4. real extraction to editable layers
5. depth to parallax preview
6. grouped and responsive parallax refinement
7. export bundle
8. reliability and recovery
9. optional difficult-layer enhancements

---

## Slice 1: Upload To Mock Stitched Scene

### Goal

Prove the product shell and scene graph wiring before real ML integration.

### Scope

- create project
- upload multiple images
- mock stitched scene
- load editor shell
- mock groups/layers if needed

### What this proves

- control plane wiring
- editor entry logic
- stitched-scene baseline flow

---

## Slice 2: Real Stitch To Scene Shell

### Goal

Replace mocked stitched scene generation with real stitching/alignment.

### Scope

- real stitch job
- stitched artifact registration
- stitched scene provenance
- editor loading from real stitched scene

### What this proves

- stitch worker integration
- artifact registration
- stitched scene authority

---

## Slice 3: Real Segmentation To Committed Layer Seeds

### Goal

Validate segmentation and commit workflow before extraction complexity fully lands.

### Scope

- segmentation request flow
- candidate mask handling
- mask commit
- seed layer creation

### What this proves

- segmentation worker contract
- scene mutation from accepted masks

---

## Slice 4: Real Extraction To Editable Layers

### Goal

Make committed masks become real editable layers in the scene.

### Scope

- extraction jobs
- layer version creation
- thumbnail creation
- editor layer panel populated from real state

### What this proves

- extraction pipeline
- layer version model
- editor usability with real assets

---

## Slice 5: Depth To Parallax Preview

### Goal

Deliver the first clear expression of the product’s core value.

### Scope

- depth generation
- cross-image depth normalization
- default parallax mapping
- preview playback

### What this proves

- depth contract
- stitched-scene parallax viability
- preview math viability

---

## Slice 6: Grouped And Responsive Parallax Refinement

### Goal

Add the full MVP parallax control model.

### Scope

- group creation and assignment
- group mappings
- bounded scroll segments
- phone/tablet/desktop preview selection
- group-level responsive overrides

### What this proves

- group runtime semantics
- responsive parallax behavior
- richer story composition value

---

## Slice 7: Export Bundle

### Goal

Turn the editable stitched scene into a deliverable artifact.

### Scope

- export job creation
- export manifest generation
- bundle packaging
- download flow

### What this proves

- export parity with scene graph
- artifact/export lifecycle correctness

---

## Slice 8: Reliability And Recovery

### Goal

Ensure the product is usable under normal failure conditions.

### Scope

- retries
- timeout handling
- worker unavailable behavior
- partial completion behavior

### What this proves

- operational resilience
- fallback UX quality

---

## Slice 9: Optional Difficult-Layer Enhancements

### Goal

Add quality improvements without blocking MVP shipment.

### Scope

- matting refinement
- optional Qwen refinement
- alternate version activation flow

### What this proves

- optional enhancement path
- version switching behavior under real worker use

---

## Slice Dependencies

Recommended dependencies:

- Slice 1 before everything else
- Slice 2 before segmentation and depth on real stitched scenes
- Slice 3 before Slice 4
- Slice 4 before Slice 5
- Slice 5 before Slice 6
- Slice 7 after core scene graph and preview semantics are stable
- Slice 8 before release
- Slice 9 only after baseline MVP path is stable

---

## Parallel Work Guidance

Parallel work can happen, but slices should remain the visible delivery model.

Examples:

- while Slice 2 is underway, editor shell refinement can continue
- while Slice 5 is underway, export contract work can progress
- while Slice 7 is underway, reliability work can begin

The key rule:

- do not let optional enhancement work block baseline slices

---

## Freeze Criteria

This plan is ready to freeze when:

- slice order is accepted
- slice outcomes are accepted
- dependencies are accepted
- optional enhancement placement is accepted

---

## Final Slice Statement

The MVP should be delivered through vertical slices that prove stitched-scene creation, segmentation, extraction, parallax behavior, responsive grouping, export, and resilience in sequence, with optional difficult-layer enhancement intentionally delayed until the baseline product value is already working.
