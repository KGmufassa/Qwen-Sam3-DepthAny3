---
Skill: Multi-repo-comparison
Description: Efficiently compares multiple analyzed repositories to extract shared patterns, identify best implementations, detect conflicts, and generate a unified system blueprint. Prompts the user to select which repos to scan and uses the .md outputs generated from the full-repo-analysis command. Produces both structured JSON output and a human-readable Markdown comparison report. Fully command-compatible.
---

## Interactive Input Phase (REQUIRED)

### 1. Select Repositories to Compare

Prompt:
- Enter the repo folders you want to compare

Instructions:
- Accept multiple repo folders
- Example:
  - ./repo-A
  - ./repo-B
  - ./repo-C

System resolves for EACH repo:

- foundation:
  `./<repo_name>/analysis/markdown/Analyze-Repo-Foundation.md`

- architecture:
  `./<repo_name>/analysis/markdown/architecture-analysis.md`

- explanation:
  `./<repo_name>/analysis/markdown/explain-repo/repo-explanation.md`

---

### 2. Goal Selection (Multiple Choice)

What is your primary goal?

Options:
1. Build a new application (combine features)
2. Extract best practices
3. Compare architecture patterns
4. Merge specific features
5. Debug differences
6. Optimize system
7. User-defined

IF User-defined:
- Prompt for custom goal

---

### 3. Mode Selection (Multiple Choice)

Options:
1. Fast
2. Balanced (default)
3. Deep
4. User-defined

---

### 4. Comparison Scope (Multiple Choice)

Options:
1. Full
2. Component Only
3. Flow Only
4. User-defined

---

## Inputs

### Primary
- `repo_folders` (array<string>)

### Derived (auto-resolved)
For each repo:
- foundation_md
- architecture_md
- explanation_md

### Optional
- goal
- mode
- comparison_scope

---

## Outputs

### JSON Output
`./synthesized-repo-bluprint/json/repo-comparison.json`

### Markdown Output
`./synthesized-repo-bluprint/markdown/repo-comparison-report.md`

---

## Instructions

### Step 1 — Resolve Inputs

IF repo_folders NOT provided:
- prompt user

FOR each repo:
- load foundation MD
- load architecture JSON
- load explanation JSON

---

## PASS 1 — LIGHTWEIGHT ANALYSIS

### Step 2 — Load Minimal Data

Extract:
- architecture.pattern
- layers
- control_flow
- module_map (names)

---

### Step 3 — Normalize Structures

Map all repos into:
- entry
- control
- logic
- utility

---

### Step 4 — Detect Components

Identify:
- authentication
- API
- CLI
- data layer
- utilities

---

### Step 5 — Similarity Scoring

Compare:
- architecture
- layers
- flow structures

---

### Step 6 — Early Filtering

Remove low similarity pairs

---

### Step 7 — Build Similarity Matrix

---

## PASS 2 — FOCUSED COMPARISON

### Step 8 — Load Detailed Data

Only for:
- relevant repos
- relevant components

---

### Step 9 — Component Comparison

Match:
- auth ↔ auth
- API ↔ API

---

### Step 10 — Deduplicate Components

---

### Step 11 — Build Component Matrix

---

### Step 12 — Flow Matching

Normalize:
ENTRY → CONTROL → LOGIC → OUTPUT

---

### Step 13 — Flow Alignment

---

### Step 14 — Unified Flow

---

### Step 15 — Conflict Detection

Mode-based:
- fast → minimal
- balanced → standard
- deep → full detection

---

### Step 16 — Integration Opportunities

---

### Step 17 — System Blueprint

Construct:
- architecture
- modules
- flows

---

### Step 18 — Apply Goal Filtering

Adjust output based on goal

---

### Step 19 — Confidence Scoring

Evaluate:
- pattern consistency
- flow alignment
- conflicts

---

### Step 20 — Unknown Detection

---

### Step 21 — Build JSON Output

Populate schema

---

## Step 22 — Build Markdown Report

# Multi-Repo Comparison Report

## Overview
- Goal:
- Mode:
- Scope:
- Repos Compared:

---

## Pattern Summary

---

## Similarity Insights

---

## Component Comparison

---

## Flow Alignment

---

## Conflicts

---

## Integration Opportunities

---

## System Blueprint

---

## Key Insights

---

## Unknowns

---

## Summary

---

### Step 23 — Persist Outputs

Save:

JSON:
`./synthesized-repo-bluprint/json/repo-comparison.json`

Markdown:
`./synthesized-repo-bluprint/markdown/repo-comparison-report.md`

---

## Constraints

- DO NOT analyze raw code
- USE only structured outputs from pipeline
- DO NOT merge code
- KEEP deterministic

---

## Notes

- Uses outputs from full-repo-analysis pipeline
- Repo folder is the single source of truth
- Produces both machine + human readable outputs
- Fully compatible with repo-integration-report
