# Repository Breakdown: Qwen-image-layered File Content

## Overview
- Total Files Detected: 5
- Total Files Processed: 5
- Processing Mode: Balanced
- Goal: General understanding

---

## Entry Points
- `src/app.py` - Launches the primary Gradio decomposition service.
- `src/tool/combine_layers.py` - Launches the Gradio layer recomposition tool.
- `src/tool/edit_rgba_image.py` - Launches the Gradio layer editor for RGBA images.

---

## Tech Stack
- Languages: markdown, python, text
- Tools: diffusers, gradio, torch, Pillow, python-pptx, psd-tools, transformers, torchvision, numpy
- Runtime: Python, CUDA-capable GPU preferred

---

## File Breakdown

### src/app.py

- **Type:** application  
- **Role:** Primary Gradio application for layer decomposition and export  
- **Priority:** HIGH  

- **Summary:**  
Loads the Qwen-Image-Layered diffusion pipeline, decomposes an RGBA image into multiple layers, and packages outputs as gallery images plus PPTX, ZIP, and PSD downloads through a Gradio UI.

- **Key Elements:**
    - imagelist_to_pptx, imagelist_to_psd, export_gallery, infer

- **Dependencies:**
    - diffusers.QwenImageLayeredPipeline, torch, PIL.Image, pptx.Presentation, os, gradio, uuid, numpy, random, tempfile, zipfile, psd_tools.PSDImage

### src/tool/edit_rgba_image.py

- **Type:** tool  
- **Role:** Auxiliary editing app for transparent layers  
- **Priority:** HIGH  

- **Summary:**  
Runs a second Gradio app that edits a single RGBA layer with Qwen-Image-Edit, then removes the background again with RMBG so the result stays transparent.

- **Key Elements:**
    - blend_with_green_bg, infer

- **Dependencies:**
    - gradio, numpy, random, torch, PIL.Image, PIL.ImageDraw, torchvision.transforms, transformers.AutoModelForImageSegmentation, diffusers.QwenImageEditPlusPipeline

### README.md

- **Type:** documentation  
- **Role:** Project guide and operator entry documentation  
- **Priority:** MEDIUM  

- **Summary:**  
Explains the layered image decomposition concept, installation flow, Python usage, and how to launch the decomposition, editing, and recomposition apps.

- **Key Elements:**
    - Introduction, News, Quick Start, Deploy Qwen-Image-Layered, vLLM-Omni, Showcase, Layered Decomposition in Application, Flexible and Iterative Decomposition

- **Dependencies:**
    - No direct code imports

### src/tool/combine_layers.py

- **Type:** tool  
- **Role:** Layer recomposition utility  
- **Priority:** MEDIUM  

- **Summary:**  
Provides a lightweight Gradio interface that alpha-composites uploaded transparent PNG layers back into one image in stack order.

- **Key Elements:**
    - combine_images

- **Dependencies:**
    - gradio, PIL.Image

---

## Relationships
- `README.md` -> `src/app.py` (documents_entry_point)
- `README.md` -> `src/tool/edit_rgba_image.py` (documents_entry_point)
- `README.md` -> `src/tool/combine_layers.py` (documents_entry_point)
- `src/app.py` -> `src/tool/edit_rgba_image.py` (workflow_handoff)
- `src/tool/edit_rgba_image.py` -> `src/tool/combine_layers.py` (workflow_handoff)

---

## Key Observations
- The repository is a small demo-oriented Python project centered on Gradio interfaces rather than a reusable package layout.
- The three Python scripts are linked by user workflow more than by direct internal imports.
- Model execution depends on external pretrained Hugging Face assets and is likely GPU-oriented because the main pipeline is moved directly to CUDA with bfloat16.
- The main app includes export paths for PPTX, ZIP, and PSD, which positions the repo as an editing workflow bridge rather than only a model demo.

---

## Unknowns / Issues
- No dependency manifest such as `requirements.txt` or `pyproject.toml` is present in the markdown snapshot, so install requirements are inferred from imports and README commands.
- The directory snapshot shown in the markdown does not include `assets/`, but `src/app.py` references `assets/test_images/*.png`, so the capture appears incomplete.
- Runtime environment details such as model cache setup, CUDA version, and launch hardware are not encoded in the repository snapshot.

---

## Summary
This repository appears to package Qwen-Image-Layered as a compact Python demo suite: one app decomposes images into editable RGBA layers, one tool edits individual transparent layers, and one tool recombines the stack into a final image.
The structure is shallow and workflow-driven, with most logic concentrated in `src/app.py` and the two helper scripts under `src/tool/`, while the README serves as the main operational guide.

---

## Token Estimate
- Total Characters: 33817
- Estimated Tokens: 8454
