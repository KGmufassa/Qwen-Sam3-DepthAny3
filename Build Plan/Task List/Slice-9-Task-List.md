# Slice 9 Task List

## Goal

Add optional difficult-layer enhancement workflows without destabilizing the baseline MVP path.

## Workspace And Shared

- Add alternate layer version types for:
  - matte refine
  - qwen refine
- Add refined-version metadata types

## Frontend

- Build refine-edge action UI
- Build enhance-layer action UI
- Build active-version switch UI
- Build revert-to-base action UI
- Build refinement pending/success/failure UI

## Control Plane

- Implement `POST /v1/layers/{layer_id}/matte`
- Implement `POST /v1/layers/{layer_id}/refine-content`
- Persist alternate layer versions
- Implement active version switching mutation
- Ensure base version remains available

## Worker

- Implement Python matting worker integration
- Implement optional Python Qwen refine worker integration
- Emit alternate RGBA/alpha artifacts as needed
- Return typed metadata for refined versions

## Infrastructure

- Add matting queue
- Add refine queue
- Add worker service configs for matting and refine workers

## QA And Verification

- Verify refined versions can be generated
- Verify active version switching works safely
- Verify revert-to-base works
- Verify failed refinement does not replace the base version
- Verify baseline scene remains usable if refinement services are unavailable

## Exit Checklist

- Optional enhancement workflow exists
- Base path remains stable
- This slice stays non-blocking for MVP completion
