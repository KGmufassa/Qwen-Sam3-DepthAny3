# Slice 6 Task List

## Goal

Implement the full MVP parallax control model with groups, bounded scroll segments, and responsive medium-specific behavior at scene and group levels.

## Workspace And Shared

- Add shared `Group` parallax mapping types
- Add bounded scroll segment types
- Add responsive override types for:
  - phone
  - tablet
  - desktop

## Frontend

- Build create/rename/reorder group UI
- Build assign/remove layer to group UI
- Build group inspector
- Build bounded scroll segment controls
- Build scene-level responsive settings inspection UI
- Build group-level responsive override controls
- Make inheritance visible in layer inspector

## Control Plane

- Implement `POST /v1/scenes/{scene_id}/groups`
- Implement `PATCH /v1/groups/{group_id}`
- Implement `POST /v1/groups/{group_id}/layers`
- Persist group mappings and scroll segments
- Persist group responsive overrides
- Update preview payload generation to apply:
  - scene defaults
  - group mappings
  - group overrides
  - layer overrides

## Worker

- No new worker family required
- Ensure preview/export runtime consumers understand updated payloads

## Infrastructure

- No major new infra required
- Validate that existing control-plane and preview runtime deployment supports added config volume

## QA And Verification

- Verify groups can be created and renamed
- Verify layer assignment/removal works
- Verify bounded segments affect preview correctly
- Verify phone/tablet/desktop preview behavior differs where configured
- Verify clearing overrides restores inheritance

## Exit Checklist

- Groups function as runtime motion units
- Responsive parallax works using the frozen model
- The full MVP parallax authoring model is complete
