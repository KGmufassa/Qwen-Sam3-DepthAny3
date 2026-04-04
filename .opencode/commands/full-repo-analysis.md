---
Command: full-repo-analysis
Description: Orchestrates a full repository intelligence workflow by sequentially executing Analyze-Repo-Foundation, Analyze-Architecture, and Explain-Repo. Collects user input once and ensures ALL skills output both JSON and Markdown files.
agent: build
subtask: false
---

## Interactive Input Phase (REQUIRED)

### 1. Select Repository Folder

Prompt:
- Select the repo folder you want to analyze

Instructions:
- This is the SINGLE source of truth
- Assumes `preprep-repo` has already been executed

Auto-resolved paths:
- preprep_json → `./<repo_name>/analysis/json/preprep-repo-doc.json`

---

### 2. Select Focus (Optional — Global)

Options:
- Full Repository Overview (default)
- Architecture & Flow
- Execution Flow
- Data Flow
- Tech Stack
- Module Relationships
- Debug / Unknowns
- User-defined

---

### 3. Select Analysis Mode (Optional — Architecture Only)

Options:
- Fast
- Balanced (default)
- Deep

---

## Normalized Command Inputs
```

{
"repo_folder": "./<repo_name>",
"focus": "<selected_focus>",
"mode": "<selected_mode>"
}

```
---

## Execution Flow

### Step 1 — Analyze-Repo-Foundation

Skill:
- analyze-repo-foundation

Inputs:
```
{
"repo_folder": "./<repo_name>",
"focus": "<selected_focus>"
}
```

Outputs:

JSON:
`./<repo_name>/analysis/json/Analyze-Repo-Foundation.json`

Markdown:
`./<repo_name>/analysis/markdown/Analyze-Repo-Foundation.md`

---

### Step 2 — Analyze-Architecture

Skill:
- analyze-architecture

Inputs:
```
{
"repo_folder": "./<repo_name>",
"focus": "<selected_focus>",
"mode": "<selected_mode>"
}
```

Outputs:

JSON:
`./<repo_name>/analysis/json/architecture-analysis.json`

Markdown:
`./<repo_name>/analysis/markdown/architecture-analysis.md`

---

### Step 3 — Explain-Repo

Skill:
- explain-repo

Inputs:
```
{
"repo_folder": "./<repo_name>",
"focus": "<selected_focus>"
}

```
Outputs:

JSON:
`./<repo_name>/analysis/json/repo-explanation.json`

Markdown:
`./<repo_name>/analysis/markdown/repo-explanation.md`

---

## Output Summary

After execution, the following files are generated:

### Foundation
- JSON:
  `./<repo_name>/analysis/json/Analyze-Repo-Foundation.json`
- Markdown:
  `./<repo_name>/analysis/markdown/Analyze-Repo-Foundation.md`

---

### Architecture
- JSON:
  `./<repo_name>/analysis/json/architecture-analysis.json`
- Markdown:
  `./<repo_name>/analysis/markdown/architecture-analysis.md`

---

### Explanation
- JSON:
  `./<repo_name>/analysis/json/repo-explanation.json`
- Markdown:
  `./<repo_name>/analysis/markdown/repo-explanation.md`

---

## Command Behavior

- Prompts user ONCE
- Passes inputs to all skills
- Ensures ALL skills output BOTH:
  - machine-readable JSON
  - human-readable Markdown
- Maintains strict sequential execution:
  1. Foundation
  2. Architecture
  3. Explanation

---

## Validation Rules (NEW)

After each step:

- VERIFY JSON file exists
- VERIFY Markdown file exists

IF either is missing:
- mark step as FAILED
- STOP execution

---

## Constraints

- DO NOT allow skills to override inputs
- DO NOT skip steps
- DO NOT proceed if validation fails
- MUST maintain JSON + Markdown output consistency

---

## Failure Handling

- Step 1 fails → STOP
- Step 2 fails → STOP
- Step 3 fails → return partial outputs + error

---

## Notes

- Fully aligned with dual-output pipeline design
- Ensures consistency across all analysis layers
- Markdown = human insight layer
- JSON = automation + downstream processing layer
- Compatible with:
  - Multi-repo-comparison
  - repo-integration-report
