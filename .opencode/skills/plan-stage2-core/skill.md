---
Skill: plan-stage2-core
Description: Draft Stage 2 planning skill. Uses frozen Stage 1 context to generate only Stage 2 contract artifacts in paired markdown/json outputs, then updates manifest/state without freezing the stage.
---

## Purpose

This skill drafts Stage 2 only.

## Inputs

- Stage 1 frozen workspace
- PRD/intake outputs
- manifest/state from `meta/json`
- Stage 2 planning templates

## Outputs

Markdown:

- `Build Plan/Active Plans/<app_slug>/1-4 Stage Planning/Stage-2/markdown/Data-Schema-And-Domain-Model-Plan.md`
- `Build Plan/Active Plans/<app_slug>/1-4 Stage Planning/Stage-2/markdown/Canonical-State-And-Math-Plan.md`
- `Build Plan/Active Plans/<app_slug>/1-4 Stage Planning/Stage-2/markdown/API-And-Job-Contract-Plan.md`
- `Build Plan/Active Plans/<app_slug>/1-4 Stage Planning/Stage-2/markdown/Runtime-Contract-Plan.md`

Conditional markdown:

- `Build Plan/Active Plans/<app_slug>/1-4 Stage Planning/Stage-2/markdown/User-Personas-And-Jobs-To-Be-Done-Plan.md`
- `Build Plan/Active Plans/<app_slug>/1-4 Stage Planning/Stage-2/markdown/Integration-And-External-Dependency-Plan.md`
- `Build Plan/Active Plans/<app_slug>/1-4 Stage Planning/Stage-2/markdown/Security-And-Compliance-Plan.md`

JSON:

- paired `.json` files for every markdown artifact above in sibling `json/`
- updated `Build Plan/Active Plans/<app_slug>/meta/json/manifest.json`
- updated `Build Plan/Active Plans/<app_slug>/meta/json/state.json`

## Instructions

- keep outputs limited to Stage 2 contracts and constraints
- activate conditional documents only when present in manifest
- set manifest/state to `stage_2_drafting`

## Constraints

- no Stage 3 or Stage 4 content
- no freeze here

