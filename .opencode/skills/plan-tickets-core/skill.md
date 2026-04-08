---
Skill: plan-tickets-core
Description: Execution skill for generating implementation tickets from slice task lists. Produces paired markdown/json ticket artifacts and updates manifest/state.
---

## Purpose

This skill generates implementation tickets only.

## Inputs

- task list outputs
- metadata from `meta/json`

## Outputs

Markdown:

- `Build Plan/Active Plans/<app_slug>/Implementation Tickets/markdown/Implementation-Tickets-Index.md`
- `Build Plan/Active Plans/<app_slug>/Implementation Tickets/markdown/Slice-<n>-Tickets.md`

JSON:

- paired `.json` files for every markdown artifact above in sibling `json/`
- updated `Build Plan/Active Plans/<app_slug>/meta/json/manifest.json`
- updated `Build Plan/Active Plans/<app_slug>/meta/json/state.json`

## Instructions

- derive execution-ready tickets from task lists
- preserve slice grouping
- set state to `tickets_generated`

