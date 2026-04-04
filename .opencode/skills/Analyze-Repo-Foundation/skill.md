---
Skill: analyze-repo-foundation
Description: Parses a structured LLM-ready repository document to extract foundational intelligence including file structure, detected technology stack, and entry points. Supports both direct use (interactive prompts) and command-driven execution (no prompts if inputs are provided). Produces both JSON and human-readable Markdown outputs.
---

## Inputs

### Primary
- `repo_folder` (string, optional)

### Derived
- `preprep_repo_path` (auto-resolved if repo_folder provided)  
  `./<repo_name>/analysis/json/preprep-repo-doc.json`

### Optional
- `focus` (string)

---

## Input Handling Logic (Command-Compatible)

### Step 0 — Resolve Inputs

IF `repo_folder` is provided:
- Resolve:
  prepared_repo_path = `./<repo_name>/analysis/json/preprep-repo-doc.json`

ELSE:
- Prompt user:
  - Enter repo folder path

---

IF `focus` is NOT provided:
- Prompt user:

### Select Focus Area (Multiple Choice)

Options:
- Full Repository Overview (default)
- Architecture & Flow
- Tech Stack & Dependencies
- Entry Points & Execution Flow
- Key Files & Core Logic
- Relationships Between Modules
- Debug / Unknowns Analysis
- User-defined

IF User-defined:
- Prompt for custom input

---

## Outputs

### JSON Output
`./<repo_name>/analysis/json/Analyze-Repo-Foundation.json`

### Markdown Output
`./<repo_name>/analysis/markdown/Analyze-Repo-Foundation.md`

---

## JSON Schema
```
{
  "repo_summary": {
    "name": "",
    "type": "",
    "primary_language": "",
    "description": ""
  },
  "tech_stack": {
    "languages": [],
    "frameworks": [],
    "runtime": [],
    "tools": []
  },
  "architecture": {
    "pattern": "",
    "modules": [],
    "flow": ""
  },
  "entry_points": [],
  "key_files": [],
  "relationships": [],
  "confidence": {
    "structure": 0.0,
    "tech_stack": 0.0,
    "entry_points": 0.0,
    "architecture": 0.0
  },
  "unknowns": []
}
```
---

## Instructions

### Step 1 — Load Preprocessed Data

Load JSON from:
- prepared_repo_path

Extract:
- files[]
- entry_points[]
- config_files[]
- relationships[]
- unknowns[]

Set:

output_directory = `./<repo_name>/analysis/`

---

### Step 2 — Priority Filtering

- Include:
  - priority = high
  - priority = medium (if needed)
- Ignore low unless required by focus

---

### Step 3 — Determine Repo Type

Classify:
- cli_tool
- backend_api
- frontend_app
- library
- unknown

---

### Step 4 — Detect Tech Stack

Infer:
- languages
- frameworks
- runtime
- tools

---

### Step 5 — Identify Key Files

Select:
- entry_points
- core_logic files

---

### Step 6 — Map Architecture

Group modules:
- entry
- core
- services
- utilities

Flow:
Entry → Handler → Core Logic → Utility → Output

---

### Step 7 — Pattern Recognition

Infer:
- CLI-based
- Layered
- Modular
- Hybrid

---

### Step 8 — Entry Point Validation

- Verify entry_points
- Add missing to unknowns

---

### Step 9 — Relationship Normalization

- Deduplicate
- Keep meaningful connections

---

### Step 10 — Confidence Aggregation

Compute:
- structure
- tech_stack
- entry_points
- architecture

---

### Step 11 — Unknown Propagation

Add unknowns where needed

---

### Step 12 — Apply Focus

Adjust emphasis based on selected focus

---

### Step 13 — Build JSON Output

Populate full schema

---

## Step 14 — Build Markdown Output (NEW)

Create structured readable file:

---

# Repo Foundation Analysis: <repo_name>

## Overview
- Type:
- Primary Language:
- Description:

---

## Tech Stack
- Languages:
- Frameworks:
- Runtime:
- Tools:

---

## Architecture Summary
- Pattern:
- Flow:
- Modules:
  - Entry
  - Core
  - Services
  - Utilities

---

## Entry Points
- List of entry points

---

## Key Files

For each file:

### <file_path>
- Role:
- Priority:
- Summary:

---

## Relationships
- File → File connections

---

## Confidence
- Structure:
- Tech Stack:
- Entry Points:
- Architecture:

---

## Unknowns / Gaps
- Missing elements
- Unclear structure

---

## Summary
- High-level explanation of repo structure and behavior

---

### Step 15 — Persist Outputs

Save:

JSON:
`./<repo_name>/analysis/json/Analyze-Repo-Foundation.json`

Markdown:
`./<repo_name>/analysis/markdown/Analyze-Repo-Foundation.md`

---

## Constraints

- DO NOT parse raw files
- USE only structured data
- DO NOT hallucinate frameworks
- KEEP deterministic output

---

## Notes

- Produces BOTH JSON + Markdown outputs
- Markdown is optimized for readability and debugging
- JSON remains source of truth for downstream skills
- Fully command-compatible
