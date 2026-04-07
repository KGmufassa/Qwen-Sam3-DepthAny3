# State And History Plan

## Document Purpose

This document defines how mutable editor state, persisted scene state, and undo/redo history behave in the MVP.

It answers:

- what state is temporary versus persisted
- what counts as an undoable action
- how async jobs affect history
- how layer version changes behave
- how inheritance changes are represented

---

## State Principles

- stitched scene graph state is the source of truth
- editor interaction state is derived and temporary
- persisted changes must be reproducible
- undo/redo must operate on user-meaningful actions
- async worker completion must not silently corrupt history expectations

---

## State Categories

### Persisted scene state

This includes:

- stitched scene metadata
- group definitions
- layer definitions
- transform values
- depth settings
- parallax mappings
- responsive defaults
- group overrides
- active layer version

### Session UI state

This includes:

- current selection
- current inspector tab
- current preview medium
- current viewport zoom/pan
- open panels

This state does not need to be treated as export-relevant scene truth.

### Async job state

This includes:

- job pending/running/completed/failed
- result availability
- retryable status

### Derived state

This includes:

- inherited values shown in UI
- computed preview payloads
- readiness summaries

Derived state should not be stored as authoritative scene truth unless it becomes export-relevant.

---

## Undo/Redo Principles

Undo/redo should operate on user-intent actions, not low-level rendering events.

Examples of good undo units:

- rename layer
- move layer
- change group assignment
- edit group scroll segment
- toggle layer visibility
- switch active layer version

Examples of poor undo units:

- every mousemove during drag as separate history item
- transient selection changes
- preview scrubbing position

---

## Required Undoable Actions

The MVP should support undo/redo for:

- create group
- rename group
- assign layer to group
- remove layer from group
- rename layer
- reorder layer
- change layer visibility
- move/scale/rotate layer
- edit group mapping
- edit group responsive override
- edit layer general parallax override
- switch active layer version

---

## Non-Undoable Or Session-Only Actions

The following do not need to be undoable in MVP:

- selection changes
- panel open/close state
- viewport pan/zoom
- medium switch in preview
- reading job status

---

## Drag Interaction History Rule

Drag-based transforms should create one undo entry per completed interaction, not one per frame.

Recommended model:

- on drag start: begin draft
- during drag: update ephemeral state
- on drag end: commit one history action

This applies to:

- move
- scale
- rotate

---

## Async Job History Rules

Async jobs need special treatment.

### User-triggered async jobs

If the user explicitly triggers:

- matte refine
- layer refine
- export

the trigger action itself may be recorded in UI state, but the final history-relevant change should only be committed when the result is accepted into scene state.

### Auto-completing async jobs

For jobs such as:

- stitch
- extraction
- depth generation

the history model should avoid pretending the user manually edited values that were system-generated.

Recommended rule:

- job completion updates state
- state mutation is recorded as a system event
- undo should target user-accepted scene mutations, not raw job execution metadata

---

## Version Switching Rules

Layer version switching is a meaningful scene mutation and should be undoable.

Required behavior:

- switching active version creates one history entry
- reverting to base version creates one history entry
- failed worker outputs do not become history entries unless accepted into scene state

---

## Inheritance State Rules

Inherited values should not be stored as independent explicit layer overrides unless the user intentionally sets them.

### Required behavior

- inherited state is derived from group and scene state
- explicit override creates stored override state
- clearing override removes stored override state and restores inheritance

History must distinguish:

- “set override”
- “clear override”

These are meaningful undo units.

---

## Save Model

The MVP should use explicit persistence for scene mutations.

Recommended model:

- user action changes local UI state
- change is validated
- persisted mutation updates scene graph
- history entry is finalized when persistence succeeds

This prevents history from diverging from saved truth.

---

## Conflict Model

The MVP assumes single-user editing for one scene at a time.

Therefore:

- no real-time merge logic is required
- no collaborative conflict-resolution model is required

If future concurrency is added, this plan will need revision.

---

## Autosave Rules

The MVP should assume scene edits are saved explicitly or near-immediately through the control plane.

The plan should preserve:

- one authoritative saved scene graph
- no hidden unsaved export state

If draft buffering is used, it must eventually reconcile into explicit scene mutations.

---

## History Entry Shape

Each history entry should conceptually include:

- action type
- target entity
- previous value
- next value
- timestamp
- actor

This does not require a public API shape yet, but implementation should follow the concept.

---

## Out-Of-Scope History Features

The MVP does not require:

- collaborative edit history
- timeline scrubbing history
- per-frame transform history
- branchable history trees

---

## Freeze Criteria

This plan is ready to freeze when:

- undoable actions are accepted
- drag history behavior is accepted
- async job history treatment is accepted
- version switching behavior is accepted
- inheritance state rules are accepted

---

## Final State Statement

The MVP state model separates persisted stitched scene truth from session UI state and system job state, while undo/redo tracks user-meaningful scene mutations such as layer transforms, group assignments, parallax edits, and active version changes without treating transient UI events or raw worker execution as equivalent user edits.
