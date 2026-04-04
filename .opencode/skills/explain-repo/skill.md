---
Skill: explain-repo
Description: Generates a clear, human-readable explanation of a repository using structured outputs from analyze-repo-foundation and analyze-architecture. Supports both direct use (interactive prompts) and command-driven execution (no prompts if inputs are provided). Produces both JSON and Markdown outputs.
---

## Inputs

### Primary
- repo_folder (string, optional)

### Derived
- foundation_analysis_path → `./<repo_name>/analysis/markdown/Analyze-Repo-Foundation.md`
- architecture_analysis_path → `./<repo_name>/analysis/markdown/architecture-analysis.md`

### Optional
- focus (string)
- mode (string)

---

## Input Handling Logic (Command-Compatible)

IF repo_folder provided:
- auto-resolve paths

ELSE:
- prompt user

IF focus missing:
- prompt (multiple choice)

IF mode missing:
- prompt (multiple choice)

---

## Outputs

### JSON Output
`./<repo_name>/analysis/json/repo-explanation.json`

### Markdown Output
`./<repo_name>/analysis/markdown/repo-explanation.md`

---

## JSON Schema
```
{
  "overview": "",
  "how_it_works": "",
  "key_components": [],
  "execution_flow": "",
  "data_flow": "",
  "integration_points": [],
  "important_files": [],
  "modification_guide": [],
  "summary": "",
  "confidence": {},
  "unknowns": [],
  "output_directory": ""
}
```
---

## Instructions

### Step 1 — Load Required Data

From foundation:
- repo_summary
- tech_stack
- key_files

From architecture:
- architecture.pattern
- layers
- module_map
- control_flow
- data_flow
- integration_points
- unknowns

---

### Step 2 — Apply Focus

Filter:
- modules
- flows
- components

---

### Step 3 — Identify Active Components

- include active modules
- exclude passive unless needed

---

### Step 4 — Generate Overview

"This repository is a {type} system designed to {purpose}..."

---

### Step 5 — Explain System Behavior

Describe:
- layers
- structure
- interactions

---

### Step 6 — Key Components

List:
- module name
- description
- importance

---

### Step 7 — Execution Flow

Simplified:
Input → Processing → Output

---

### Step 8 — Data Flow

Simplified:
Input → Transform → Output

---

### Step 9 — Integration Points

Describe:
- APIs
- DBs
- external systems

---

### Step 10 — Important Files

Select:
- entry points
- core files

---

### Step 11 — Modification Guide

Provide structured recommendations:

- what to change
- where
- why

---

### Step 12 — Mode Adjustment

- Quick → minimal
- Standard → balanced
- Detailed → deep explanation

---

### Step 13 — Compression

- remove redundancy
- merge similar ideas

---

### Step 14 — Confidence Scoring

Evaluate:
- clarity
- completeness
- unknown impact

---

### Step 15 — Unknown Propagation

Include gaps and uncertainties

---

### Step 16 — Build JSON Output

Populate schema

---

## Step 17 — Build Markdown Output (NEW)

Create structured report:

---

# Repository Explanation: <repo_name>

## Overview
- System Type:
- Purpose:
- Architecture Pattern:

---

## How It Works
- High-level explanation of system behavior

---

## Execution Flow
- Entry → Processing → Output

---

## Data Flow
- Input → Transformation → Output

---

## Key Components

### <Component Name>
- Description:
- Importance:

---

## Architecture Summary

### Layers
- Entry Layer
- Control Layer
- Logic Layer
- Utility Layer

---

## Integration Points
- APIs
- Databases
- External systems

---

## Important Files
- List of key files with roles

---

## Modification Guide

### Suggested Changes

- Action:
- Location:
- Reason:

---

## Confidence
- Explanation Quality:
- Architecture Clarity:
- Flow Completeness:

---

## Unknowns / Gaps
- Missing details
- Unclear behavior

---

## Summary
- What the system does
- How it works
- Key takeaway

---

### Step 18 — Persist Outputs

Save:

JSON:
`./<repo_name>/analysis/json/repo-explanation.json`

Markdown:
`./<repo_name>/analysis/markdown/repo-explanation.md`

---

## Constraints

- DO NOT analyze raw code
- USE structured inputs only
- DO NOT hallucinate
- KEEP deterministic

---

## Notes

- Produces BOTH JSON + Markdown outputs :contentReference[oaicite:0]{index=0}  
- Markdown is optimized for readability and explanation  
- JSON is optimized for downstream automation  
- Final human-facing layer of pipeline
