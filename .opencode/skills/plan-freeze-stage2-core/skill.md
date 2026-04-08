---
Skill: plan-freeze-stage2-core
Description: Sequential freeze skill for Stage 2. Reconciles contract artifacts, validates readiness, writes a freeze review artifact, and updates manifest/state to Stage 2 frozen.
---

## Purpose

This skill freezes Stage 2 only.

## Inputs

- Stage 2 outputs
- metadata from `meta/json`

## Outputs

Markdown:

- `Build Plan/Active Plans/<app_slug>/1-4 Stage Planning/Stage-2/markdown/Stage-2-Freeze-Review.md`

JSON:

- `Build Plan/Active Plans/<app_slug>/1-4 Stage Planning/Stage-2/json/Stage-2-Freeze-Review.json`
- updated `Build Plan/Active Plans/<app_slug>/meta/json/manifest.json`
- updated `Build Plan/Active Plans/<app_slug>/meta/json/state.json`

## Instructions

- reconcile data model, contract, integration, and security assumptions
- fail on unresolved contradictions
- set state to `stage_2_frozen`

