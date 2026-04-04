---
Skill: repo-integration-report
Description: Consumes the output from the Multi-repo-comparison skill and generates a tailored integration report based on user-defined goals. Produces a hybrid output (JSON + Markdown) focused on how to effectively combine, adapt, or reuse code across repositories. No code is modified—this is a planning and strategy layer.
---

## Interactive Input Phase (REQUIRED)

### 1. Project Goal (Multiple Choice)

What are you trying to accomplish?

Options:
- Build a new app using these repos
- Combine features across repos
- Reuse logic from one repo in another
- Improve or refactor an existing system
- Learn how these repos can work together
- User-defined

IF User-defined:
- Prompt: Describe your goal

---

### 2. Desired Output Type (CRITICAL)

What type of report do you want?

Options:
- Full Integration Plan (default)
- Code Adaptation Guide (how to move logic between repos)
- Architecture Merge Strategy
- Feature Mapping (which repo handles what)
- Conflict Resolution Plan
- Step-by-step Build Guide
- User-defined

IF User-defined:
- Prompt: Describe desired output

---

### 3. Integration Strategy Preference

Options:
- Wrap (use repos as-is)
- Extract (reuse specific parts)
- Extend (build on top)
- Hybrid (recommended)
- Not sure

---

### 4. Priority

Options:
- Speed
- Maintainability
- Flexibility
- Performance
- Balanced

---

### 5. Constraints (Optional)

- Tech stack limits
- Time constraints
- Complexity tolerance

---

## Inputs

- comparison_file  
  `./synthesized-repo-bluprint/json/repo-comparison.json`

- user_responses

---

## Outputs

### Markdown Output (PRIMARY)
`./synthesized-repo-bluprint/markdown/repo-integration-report.md`

### JSON Output (SECONDARY)
`./synthesized-repo-bluprint/json/repo-integration-report.json`

---

## Execution Logic

### Step 1 — Load Comparison Data

Extract:
- component_matrix
- system_blueprint
- conflicts
- integration_opportunities
- flows

---

### Step 2 — Interpret User Intent

Map:
- goal → strategy
- output_type → report structure
- priority → decision weighting

---

### Step 3 — Build Repo Roles

For each repo:
- determine role:
  - core
  - feature provider
  - utility
  - reference

---

### Step 4 — Cross-Repo Mapping

Identify:
- which repo owns which components
- overlapping functionality
- best implementation sources

---

### Step 5 — Code Reuse Mapping (CRITICAL)

IF output_type includes adaptation:

Generate:

- Source repo → Target repo mapping
- What logic can be reused
- Required transformations

Example:

Repo A auth → Repo B integration:
- extract auth service
- adapt API interface
- align data schema

---

### Step 6 — Conflict Resolution

For conflicts:
- identify cause
- propose resolution
- recommend dominant implementation

---

### Step 7 — Integration Strategy

Define:
- how repos connect
- boundaries
- coupling level

---

### Step 8 — Build Implementation Plan

Generate phases:

Phase 1 — Setup  
Phase 2 — Extraction  
Phase 3 — Integration  
Phase 4 — Alignment  
Phase 5 — Testing  

---

## JSON Output
```
{
  "project_name": "",
  "intent": {},
  "repo_roles": [],
  "integration_strategy": {},
  "code_reuse_map": [],
  "conflicts": [],
  "implementation_plan": []
}
```
---

## Markdown Output (PRIMARY)

# Repo Integration Report

## Overview
- Goal:
- Output Type:
- Strategy:
- Priority:

---

## Repo Roles

- Repo A → Core
- Repo B → Feature (Auth)
- Repo C → Utility

---

## How These Repos Fit Together

- High-level explanation of system integration

---

## Component Mapping

### Authentication
- Best Source: Repo A
- Used In: Repo B

---

## Code Reuse Guide (KEY SECTION)

### Example:

#### Auth System Migration
- Source: Repo A
- Target: Repo B
- Steps:
  - Extract auth module
  - Replace API endpoints
  - Align database schema

---

## Integration Strategy

- How repos connect
- API boundaries
- Data flow

---

## Conflict Resolution

- Conflict:
- Resolution:
- Recommended Source:

---

## Build Plan

### Phase 1 — Setup
### Phase 2 — Extraction
### Phase 3 — Integration
### Phase 4 — Testing

---

## Key Insights

- Best patterns
- Reusable logic
- Design decisions

---

## Risks

- Integration complexity
- Dependency conflicts

---

## Summary

- What to build
- How to build it
- Key takeaway

---

## Constraints

- DO NOT modify code
- USE only comparison output
- KEEP deterministic
- MUST follow user-defined output type

---

## Notes

- Designed to work directly after Multi-repo-comparison :contentReference[oaicite:0]{index=0}  
- Markdown output is the PRIMARY deliverable  
- Focused on real-world integration + code reuse strategy  
- Acts as final decision + planning layer before actual development
