---
Skill: analyze-architecture
Description: Analyzes structured repository intelligence directly from `preprep-repo` output to identify system architecture patterns, module interactions, data flow, and structural design principles. Supports both direct use (interactive prompts) and command-driven execution (no prompts if inputs are provided). Produces both JSON and human-readable Markdown outputs.
---

## Inputs

### Primary
- repo_folder (string, optional)

### Derived
- preprep_repo_path  
  `./<repo_name>/analysis/json/preprep-repo-doc.json`

### Optional
- focus (string)
- mode (string: fast | balanced | deep)

---

## Input Handling Logic (Command-Compatible)

IF repo_folder provided:
- resolve path automatically

ELSE:
- prompt user

IF focus missing:
- prompt (multiple choice)

IF mode missing:
- prompt (multiple choice)

---

## Outputs

### JSON Output
`./<repo_name>/analysis/json/architecture-analysis.json`

### Markdown Output
`./<repo_name>/analysis/markdown/architecture-analysis.md`

---

## JSON Schema
```
{
  "architecture": {},
  "graph": {},
  "module_map": [],
  "data_flow": [],
  "control_flow": [],
  "integration_points": [],
  "anti_patterns": [],
  "cycles": [],
  "unused_modules": [],
  "confidence": {},
  "unknowns": [],
  "analysis_limits": {},
  "normalized": true,
  "analysis_version": "3.2",
  "output_directory": ""
}
```
---

## Instructions

### Step 1 — Load Data

Extract:
- files
- relationships
- entry_points
- config_files

---

### Step 2 — Lightweight Foundation

- detect repo type
- detect tech stack
- validate entry points

---

### Step 3 — Mode Settings

- Fast → depth 2  
- Balanced → depth 3  
- Deep → depth 5  

---

### Step 4 — Build Graph

- nodes = modules  
- edges = relationships  

---

### Step 5 — Traverse System

- start at entry points  
- BFS/DFS traversal  

---

### Step 6 — Classify Modules

- entry_point  
- core_logic  
- utility  

---

### Step 7 — Layer Mapping

- entry  
- control  
- logic  
- utility  

---

### Step 8 — Build Flows

Control Flow:
Entry → Handler → Logic → Output  

Data Flow:
Input → Transform → Output  

---

### Step 9 — Detect Patterns

- CLI  
- Layered  
- Modular  
- Hybrid  

---

### Step 10 — Detect Risks

- cycles  
- tight coupling  
- unused modules  

---

### Step 11 — Build Module Map

---

### Step 12 — Confidence Scoring

---

### Step 13 — Apply Focus

Adjust output emphasis

---

### Step 14 — Build JSON Output

Populate schema

---

## Step 15 — Build Markdown Output (NEW)

Create structured report:

---

# Architecture Analysis: <repo_name>

## Overview
- Architecture Pattern:
- System Type:
- Layers:

---

## System Flow

### Execution Flow
- Entry → Control → Logic → Output

### Data Flow
- Input → Processing → Output

---

## Architecture Breakdown

### Layers

#### Entry Layer
- modules

#### Control Layer
- modules

#### Logic Layer
- modules

#### Utility Layer
- modules

---

## Module Map

For each module:

### <module_name>
- Role:
- Type:
- Connected To:

---

## Integration Points
- APIs
- Databases
- External systems

---

## Graph Summary
- Total Nodes:
- Total Edges:

---

## Risks & Anti-Patterns

- Cycles:
- Tight Coupling:
- Misplaced Logic:

---

## Unused Modules
- List

---

## Confidence

- Pattern:
- Flow:
- Relationships:

---

## Unknowns / Gaps

- Missing structure
- Unclear relationships

---

## Summary

- High-level explanation of how the system is structured
- Key architectural insight

---

### Step 16 — Persist Outputs

Save:

JSON:
`./<repo_name>/analysis/json/architecture-analysis.json`

Markdown:
`./<repo_name>/analysis/markdown/architecture-analysis.md`

---

## Constraints

- DO NOT parse raw code
- USE structured input only
- DO NOT hallucinate
- KEEP deterministic

---

## Notes

- Produces BOTH JSON + Markdown outputs :contentReference[oaicite:0]{index=0}  
- Markdown is optimized for readability and architectural understanding  
- JSON is optimized for downstream skills  
- Fully command-compatible
