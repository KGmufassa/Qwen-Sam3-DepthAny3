# Slice 6 Tickets

## Scope

Implement the full MVP parallax control model with groups, bounded scroll segments, and responsive medium-specific behavior.

## Tickets

### S6-001: Add shared group mapping, scroll segment, and responsive override contract types

- Owner area: shared contracts
- Dependencies: Slice 5 complete
- Deliverable: typed contracts for group runtime behavior

### S6-002: Implement group create/update/assignment APIs

- Owner area: control plane
- Dependencies: S6-001
- Deliverable: group CRUD and layer assignment endpoints

### S6-003: Persist group parallax mappings, segments, and responsive overrides

- Owner area: control plane
- Dependencies: S6-002
- Deliverable: durable scene graph support for group runtime behavior

### S6-004: Update preview payload generation for scene defaults, group mappings, and overrides

- Owner area: control plane
- Dependencies: S6-003
- Deliverable: preview payload honors full parallax model

### S6-005: Build group panel UI

- Owner area: frontend
- Dependencies: S6-002
- Deliverable: create/rename/reorder groups and show membership

### S6-006: Build group inspector UI

- Owner area: frontend
- Dependencies: S6-003
- Deliverable: controls for group mapping, bounded segments, and medium overrides

### S6-007: Build inheritance indicators and reset-to-inherited behavior

- Owner area: frontend
- Dependencies: S6-003, S6-006
- Deliverable: clear inherited vs overridden state in the editor

### S6-008: Verify responsive preview behavior for phone/tablet/desktop

- Owner area: frontend
- Dependencies: S6-004, S6-006
- Deliverable: medium switching and visible behavior differences where configured

### S6-009: Validate Slice 6 end-to-end

- Owner area: QA
- Dependencies: S6-002 through S6-008
- Deliverable: verified group-aware and responsive parallax model
