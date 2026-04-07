# Editor UX And Interaction Plan

## Document Purpose

This document defines the MVP editor experience for stitched-scene authoring.

It focuses on:

- how users enter the editor
- what the editor must display
- how layers and groups are managed
- how parallax is configured
- how responsive preview selection works
- what interaction patterns are required for MVP

This plan is workflow-facing and must remain aligned with the frozen Stage 1 and Stage 2 contracts.

---

## UX Principles

- the stitched scene should feel like one coherent workspace
- the editor should expose structure without overwhelming the user
- the most important controls must be understandable without backend knowledge
- preview behavior should be understandable from saved scene state
- grouping should feel like both organization and motion control
- responsive medium behavior should be inspectable and testable

---

## Primary Editor Goals

The editor must let a user:

- inspect the stitched scene
- manage extracted layers
- create and manage groups
- tune parallax behavior
- preview by target medium
- prepare the scene for export

---

## Entry Into The Editor

The user should enter the editor only after the system has enough scene state to make the experience meaningful.

### Minimum editor-ready state

- stitched scene exists
- source images are registered
- at least one layer can exist or be created
- scene graph payload is fetchable

### Recommended entry moments

- after stitching completes
- after first committed masks are extracted into layers

The editor may load before all jobs are complete, but incomplete states must be explicit.

---

## Editor Layout

The MVP editor should have these core regions:

- scene canvas
- layer/group panel
- inspector panel
- preview controls
- status/processing area

### Scene canvas

Used for:

- visual composition
- selection
- transform editing
- stitched scene inspection

### Layer/group panel

Used for:

- viewing order
- renaming
- visibility toggles
- group creation and assignment

### Inspector panel

Used for:

- layer transform settings
- depth settings
- parallax settings
- group mappings
- responsive behavior controls

### Preview controls

Used for:

- selecting medium profile
- previewing scroll behavior
- toggling reduced motion if supported

### Status/processing area

Used for:

- job progress
- warnings
- failed stage visibility
- retry entry points

---

## Required Editor Capabilities

### Layer management

Users must be able to:

- select a layer
- rename a layer
- reorder layers
- show and hide layers
- inspect active version state

### Group management

Users must be able to:

- create a group
- rename a group
- reorder groups
- assign layers to groups
- remove layers from groups

Constraints:

- groups are flat
- a layer belongs to zero or one group

### Transform editing

Users must be able to edit:

- position
- scale
- rotation

These edits must persist in stitched scene space.

### Parallax editing

Users must be able to:

- inspect scene-level parallax defaults
- inspect group-level parallax mappings
- edit group scroll segment participation
- inspect layer inheritance
- apply layer-level general override when needed

### Responsive preview selection

Users must be able to preview the scene as:

- phone
- tablet
- desktop

The selected medium should affect the preview and inspector context.

---

## Group Interaction Model

Groups should be visible in the editor as motion-aware containers.

The UI should communicate that groups are:

- organizational
- runtime motion units

### Group panel behavior

A group row should expose:

- name
- order
- layer count
- enabled/visible state if supported
- current scroll segment summary
- current responsive override summary

### Group inspector behavior

The group inspector should expose:

- shared parallax mapping
- scroll segment bounds
- medium-specific overrides

---

## Layer Interaction Model

Layer rows should expose:

- name
- visibility
- group membership
- active version indicator
- selection state

The layer inspector should expose:

- transform
- depth settings
- inherited group mapping summary
- layer-level override controls

The UI should make inheritance visible so users understand whether a value is:

- inherited
- overridden

---

## Inheritance UX Rules

The editor must make group inheritance obvious.

Recommended behaviors:

- inherited values display as inherited, not as if they were directly set on the layer
- overriding a value should be explicit
- clearing an override should return the layer to inherited behavior

For MVP, inheritance clarity matters more than visual polish.

---

## Responsive UX Rules

Responsive behavior should be represented simply.

### Scene-level responsive UX

The editor should allow inspection of:

- phone defaults
- tablet defaults
- desktop defaults

### Group-level responsive UX

The editor should allow group-specific overrides for:

- phone
- tablet
- desktop

### Layer-level responsive UX

Not required for baseline MVP.

The editor should avoid exposing per-layer responsive controls unless needed later.

---

## Preview UX

The preview experience must be integrated with the editor, not treated as a separate product.

Users should be able to:

- switch medium profile
- enter preview mode
- inspect how group scroll segments behave
- verify that exported behavior will match the preview semantics

The preview should clearly communicate which medium profile is active.

---

## Processing UX

The editor must remain usable during asynchronous work where possible.

It should surface:

- pending stitch status
- pending extraction status
- pending depth status
- pending refinement status

If parts of the editor depend on unfinished work, those controls should explain why they are unavailable.

---

## Version UX

Where layer versions exist, users should be able to:

- know which version is active
- revert to base version
- switch versions intentionally

The MVP does not require a full version browser, but it does require clear active-version behavior.

---

## Export UX

The export entry point should:

- show export readiness
- surface blocking failures
- use the saved scene graph state

The editor should never imply that export will include unpublished or unstored implicit state.

---

## Accessibility And Clarity Requirements

The MVP editor should aim for:

- clear labels for group inheritance
- clear labels for medium profile selection
- no hidden motion rules
- no ambiguity between “grouping for organization” and “grouping for parallax”

---

## Out-Of-Scope Editor Features

The MVP editor does not require:

- nested groups
- per-layer medium-specific responsive UI
- timeline/keyframe editing
- advanced paint tools
- multi-user collaboration tools

---

## Freeze Criteria

This plan is ready to freeze when:

- required editor regions are accepted
- layer and group behaviors are accepted
- inheritance behavior is accepted
- responsive preview model is accepted
- export UX expectations are accepted

---

## Final UX Statement

The MVP editor is a stitched-scene workspace that exposes layers, flat groups, inherited parallax behavior, medium-aware preview selection, and export readiness in one coherent interface, with the scene graph remaining the source of truth for everything the user sees and configures.
