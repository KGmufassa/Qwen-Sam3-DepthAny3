---
Command Name: preprep-repo
Description: Processes selectively downloaded repository files and converts them into a structured, token-efficient, LLM-ready dataset. Extracts key metadata, normalizes file content, and prepares both a JSON dataset and a human-readable Markdown breakdown for downstream analysis.
Agent: Build
subtask: false
---

## Interactive Input Phase (REQUIRED)

### 1. Define Source File

Prompt:
- Provide the path to the Markdown file containing the repository

---

### 2. Define Goal (Multiple Choice)

What is your goal for processing this repo?

Options:
- General understanding (default)
- Analyze architecture
- Understand execution flow
- Extract key components
- Prepare for integration
- Debug / identify issues
- User-defined

IF User-defined:
- Prompt: Enter your custom goal

---

### 3. Select Processing Mode (Multiple Choice)

Options:
- Fast (minimal parsing, faster execution)
- Balanced (default, recommended)
- Deep (full analysis, maximum detail)

---

## Inputs

- input_source (string)
- goal (string)
- mode (string)

---

## Outputs

### 1. JSON Output
Saved to:

    ./<repo_name>/analysis/json/preprep-repo-doc.json


### 2. Markdown Output (NEW)
Saved to:

    ./<repo_name>/analysis/markdown/preprep-repo-breakdown.md


---

## Instructions

### Step 0 — Resolve Inputs

IF input_source NOT provided:
- prompt user

IF goal NOT provided:
- default = General understanding

IF mode NOT provided:
- default = Balanced

---

### Step 1 — Detect Repository Name

repo_name = filename(input_source)

---

### Step 2 — Create Output Directory


    ./<repo_name>/analysis/


---

### Step 3 — Validate Markdown Format

Ensure:
- file markers exist
- code blocks exist

IF invalid:
- log errors

---

### Step 4 — Extract Virtual Files

Parse markdown into:
```
{
  "path": "",
  "language": "",
  "content": ""
}
```
---

### Step 5 — Classify + Analyze Files

For each file:
- detect type
- assign role
- assign priority
- extract imports/exports
- extract key elements
- generate summary

---

### Step 6 — Build Relationships

Map dependencies between files

---

### Step 7 — Detect Entry Points

Identify:
- main files
- CLI files
- index files

---

### Step 8 — Detect Config Files

Identify:
- package.json
- requirements.txt
- Dockerfile
- .env

---

### Step 9 — Token Estimation

Estimate total size

---

### Step 10 — Build JSON Output

Populate full schema

---

### Step 11 — Build Markdown Output (NEW)

Create a readable breakdown:

---

# Repository Breakdown: <repo_name>

## Overview
- Total Files Detected: X
- Total Files Processed: X
- Processing Mode: <mode>
- Goal: <goal>

---

## Entry Points
- List detected entry points

---

## Tech Stack
- Languages
- Tools
- Runtime (if detected)

---

## File Breakdown

For each HIGH + MEDIUM priority file:

### <file_path>

- **Type:**  
- **Role:**  
- **Priority:**  

- **Summary:**  
<summary>

- **Key Elements:**
    - functions/classes/etc.

- **Dependencies:**
    - imports

---

## Relationships

- File A → File B
- Module connections

---

## Key Observations

- Patterns detected
- Important architectural hints

---

## Unknowns / Issues

- Missing entry points
- Unclear roles
- Parsing issues

---

## Summary

Short explanation of:
- what the repo appears to do
- how it is structured

---

### Step 12 — Persist Outputs

Save:

JSON:

    ./<repo_name>/analysis/json/preprep-repo-doc.json


Markdown:

    ./<repo_name>/analysis/markdown/preprep-repo-breakdown.md


---

## Constraints

- DO NOT include full raw code for large files
- DO NOT hallucinate missing data
- MUST rely on markdown structure
- KEEP output deterministic

---

## Notes

- Produces BOTH machine-readable + human-readable outputs
- Markdown file is optimized for quick inspection and debugging
- JSON remains the source of truth for downstream skills
- Fully compatible with analysis pipeline (foundation → architecture → explain)
