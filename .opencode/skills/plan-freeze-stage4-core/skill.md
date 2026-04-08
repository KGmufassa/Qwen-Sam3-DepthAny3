---
Skill: plan-freeze-stage4-core
Description: Sequential freeze skill for Stage 4. Reconciles delivery artifacts, validates readiness, writes a freeze review artifact, and updates manifest/state to Stage 4 frozen.
---

## Purpose

This skill freezes Stage 4 only.

## Inputs

- Stage 4 outputs
- metadata from `meta/json`

## Outputs

Markdown:

- `Build Plan/Active Plans/<app_slug>/1-4 Stage Planning/Stage-4/markdown/Stage-4-Freeze-Review.md`

JSON:

- `Build Plan/Active Plans/<app_slug>/1-4 Stage Planning/Stage-4/json/Stage-4-Freeze-Review.json`
- updated `Build Plan/Active Plans/<app_slug>/meta/json/manifest.json`
- updated `Build Plan/Active Plans/<app_slug>/meta/json/state.json`

## Instructions

- reconcile infrastructure, QA, slice order, operations, and risk assumptions
- fail on unresolved contradictions
- set state to `stage_4_frozen`

