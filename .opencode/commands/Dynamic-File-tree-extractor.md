---
Command Name: Dynamic-File-tree-extractor
Description: Analyzes a repository file tree (no code) and dynamically determines which files and directories to include or exclude based on detected project type and structural patterns. Produces both JSON and Markdown outputs, including a simplified exclusion list with intelligent folder collapsing.
Agent: Build
Subtask: true
---

## Inputs

- file_tree_path (string, required)  
- goal:
   - I want to only extract files that help do the following:
        1. How to use the app
        2. How to apply or wrap the app withing an exsiting app
        3. How to run the app in tandem with other exsiting apps
        4. How to make changes to the code base to increase productivity when applicable
---

## Outputs

### JSON Output
`./pre-analysis/<repo_name>/json/extraction-plan.json`

### Markdown Output
`./pre-analysis/<repo_name>/markdown/extraction-plan.md`

---

## JSON Schema (Updated)
```
{
  "project_type": "",
  "include": [],
  "exclude": [],
  "excluded_simple_list": [],
  "representative_selection": [],
  "selection_strategy": {
    "type": "rule_based",
    "constraints": []
  },
  "reasoning": {
    "patterns_detected": [],
    "selection_strategy": "",
    "type_specific_rules": []
  },
  "stats": {
    "total_items": 0,
    "included_items": 0,
    "excluded_items": 0
  },
  "output_directory": ""
}
```
---

## Instructions

### Step 1 — Detect Repository Name

Extract repo name from root

---

### Step 2 — Create Output Directory

`./pre-analysis/<repo_name>`

---

### Step 3 — Detect Project Type

---

### Step 4 — Parse File Tree

---

### Step 5 — Detect Patterns

---

### Step 6 — Classify Files

---

### Step 7 — Apply Inclusion Rules

---

### Step 8 — Apply Exclusion Rules

Build full exclusion list first:
- all excluded file paths

---

## Step 9 — Build Simplified Exclusion List (CRITICAL NEW LOGIC)

### Goal:
Produce a flattened, human-readable exclusion list with intelligent folder collapsing.

### Rules:

1. IF all files inside a directory are excluded:
   → include ONLY the directory path  
   Example:

`assets`


2. IF only specific files are excluded:
→ include FULL relative paths  
Example:

`assets/veval/toy_gt_and_pred/toy_saco_veval_sav_test_eval_res.json`


3. Root-level files:
→ include filename only  
Example:

`LICENSE`

`CONTRIBUTING.md`


4. DO NOT include redundant nested paths if parent folder is already excluded

---

### Example Output:

Given:

- LICENSE (excluded)
- CONTRIBUTING.md (excluded)
- assets/veval/toy_gt_and_pred/toy_saco_veval_sav_test_eval_res.json (excluded)

Output:


LICENSE,
CONTRIBUTING.md,
assets/veval/toy_gt_and_pred/toy_saco_veval_sav_test_eval_res.json


---

### Step 10 — Representative Selection

---

### Step 11 — Goal Optimization

---

### Step 12 — Apply Constraints

---

### Step 13 — Build JSON Output

Include:
- full exclude list
- excluded_simple_list (NEW structured list)

---

## Step 14 — Build Markdown Output

---

# File Tree Extraction Plan: <repo_name>

## Overview
- Project Type:
- Goal:
- Total Items:
- Included:
- Excluded:

---

## Included Paths
- list

---

## Excluded Paths (Detailed)
- full raw excluded list

---

## Simplified Exclusion List (KEY SECTION)

```text
LICENSE, CONTRIBUTING.md, assets/veval/toy_gt_and_pred/toy_saco_veval_sav_test_eval_res.json
``` 
id="simple-exclude-list"
---

## Representative Selections

---

## Patterns Detected

---

## Selection Rules Applied

---

## Reasoning

---

## Key Observations

---

## Summary

---

### Step 15 — Persist Outputs

JSON:
`./pre-analysis/<repo_name>/json/extraction-plan.json`

Markdown:
`./pre-analysis/<repo_name>/markdown/extraction-plan.md`

---

## Constraints

- DO NOT analyze file contents
- DO NOT hallucinate files
- MUST correctly collapse folder exclusions
- MUST output simplified exclusion list in code block
- KEEP deterministic

---

## Notes

- Introduces intelligent exclusion summarization
- Simplified list improves readability and debugging
- JSON retains full detail, Markdown provides clarity
- Fully aligned with downstream pipeline
