---
Skill: plan-slices-core
Description: Execution skill for generating slice implementation plans from the fully frozen planning stack. Produces paired markdown/json slice artifacts and updates manifest/state.
---

## Purpose

This skill generates slice implementation plans only.

## Inputs

- frozen Stage 1 through Stage 4 outputs
- metadata from `meta/json`

## Outputs

Markdown:

- `Build Plan/Active Plans/<app_slug>/Slice Implementaion/markdown/Slice-Implementation-Index.md`
- `Build Plan/Active Plans/<app_slug>/Slice Implementaion/markdown/Slice-<n>-<Outcome>-Implementation-Plan.md`

JSON:

- paired `.json` files for every markdown artifact above in sibling `json/`
- updated `Build Plan/Active Plans/<app_slug>/meta/json/manifest.json`
- updated `Build Plan/Active Plans/<app_slug>/meta/json/state.json`

## Instructions

- derive slice order from the frozen planning stack
- create one index and one paired markdown/json artifact per slice
- set state to `slice_plans_generated`

