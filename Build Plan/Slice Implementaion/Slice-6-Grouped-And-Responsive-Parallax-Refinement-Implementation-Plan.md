# Slice 6: Grouped And Responsive Parallax Refinement Implementation Plan

## Purpose

This document defines the concrete implementation plan for Slice 6.

Slice 6 completes the intended MVP parallax control model by adding flat groups as runtime motion units, bounded scroll segments, and scene/group responsive behavior across phone, tablet, and desktop.

---

## Slice Goal

By the end of Slice 6, a user should be able to:

1. create and manage groups
2. assign layers to groups
3. configure group-level parallax behavior
4. configure bounded scroll segments for groups
5. preview phone, tablet, and desktop behavior
6. apply group-level responsive overrides while preserving scene defaults

---

## Scope Boundary

### In scope

- group CRUD with real editor integration
- group assignment for real extracted layers
- group-level parallax mapping controls
- group bounded scroll segment controls
- scene-level medium defaults applied in preview
- group-level responsive overrides
- inheritance visibility in the UI
- medium switching with real grouped behavior

### Explicitly out of scope

- nested groups
- layer-level medium-specific responsive overrides
- timeline-based motion editing

---

## Slice Dependency

Slice 6 depends on successful Slice 5 outcomes:

- preview runtime exists
- depth-informed defaults exist
- real layers exist
- scene graph and preview payloads are stable

---

## Slice Outcome

At completion, the system should have:

- first-class group runtime behavior in the editor
- grouped motion participation in preview
- bounded group scroll segments
- responsive medium-aware parallax behavior

This is the slice that completes the core MVP parallax authoring model.

---

## Required Deliverables

### Backend/control-plane deliverables

- group create/update/assignment support
- persistence of group mappings
- persistence of group scroll segments
- persistence of group responsive overrides
- preview payload generation honoring group semantics

### Frontend deliverables

- group panel with real group state
- group inspector
- inheritance indicators
- phone/tablet/desktop preview controls
- group-level responsive override controls

### Integration deliverables

- preview payload reflects scene defaults plus group overrides
- group assignment affects preview semantics

---

## Required Data And State Changes

To complete Slice 6, the implementation must support:

### Group state

- name
- order
- assigned layers
- parallax mapping
- bounded scroll segment
- responsive overrides

### Layer state

- group membership
- inherited mapping visibility
- general layer override support

### Preview state

- medium-aware scene defaults
- group override application

---

## Minimum API Surface Needed

Recommended minimum routes for Slice 6:

- `POST /v1/scenes/{scene_id}/groups`
- `PATCH /v1/groups/{group_id}`
- `POST /v1/groups/{group_id}/layers`
- `PATCH /v1/layers/{layer_id}`
- `GET /v1/scenes/{scene_id}/preview?medium=...`

---

## Backend Task Breakdown

### 1. Group persistence

Implement:

- group create/update
- layer assignment/unassignment
- group order handling

### 2. Group runtime semantics

Implement:

- group parallax mapping persistence
- bounded segment persistence
- responsive override persistence

### 3. Preview payload integration

Implement:

- group mapping inclusion
- inheritance resolution
- medium-specific override application in payload generation

---

## Frontend Task Breakdown

### 1. Group panel

Build:

- create group
- rename group
- reorder group
- show layer membership

### 2. Group inspector

Build:

- parallax mapping controls
- bounded segment controls
- medium override controls

### 3. Inheritance UX

Build:

- layer-level inherited/overridden state indicators
- clear override/reset behavior

### 4. Responsive preview

Build:

- phone/tablet/desktop selection
- visibly different behavior where configured

---

## UX Expectations For Slice 6

The user should understand:

- groups are motion units, not just folders
- scene-level defaults still exist
- group-level overrides refine those defaults
- layers inherit behavior unless overridden

---

## Failure Handling For Slice 6

Must support:

- group mutation failure
- invalid segment configuration
- preview mismatch or bad responsive config

Required behavior:

- invalid changes should be rejected clearly
- existing scene configuration should remain intact
- medium-specific preview should remain usable

---

## QA Checks For Slice 6

Minimum manual checks:

- create and rename groups
- assign and remove layers from groups
- configure bounded scroll segments
- preview grouped motion correctly
- preview phone/tablet/desktop differences correctly
- clear override returns inheritance behavior correctly

---

## Exit Criteria

Slice 6 is complete when:

1. groups are fully usable as runtime motion units
2. grouped motion appears correctly in preview
3. bounded scroll segments work
4. scene-level medium defaults are applied
5. group-level medium overrides are applied
6. inheritance is visible and understandable

---

## What This Slice Proves

If completed successfully, Slice 6 proves:

- the MVP’s full parallax control model is viable
- responsive parallax behavior works across media
- grouping provides meaningful storytelling control

---

## What Comes Next

The next slice after successful completion is:

- export bundle

That slice should package the now-complete scene semantics into a real deliverable artifact.

---

## Final Slice Statement

Slice 6 completes the core parallax authoring model by making groups real runtime motion units with bounded segment participation and medium-aware overrides, allowing the stitched-scene preview to express the intended MVP storytelling behavior across phone, tablet, and desktop.
