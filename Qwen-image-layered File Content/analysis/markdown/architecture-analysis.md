# Architecture Analysis

## Inputs
- Repo folder: `./Qwen-image-layered File Content`
- Focus: `Full Repository Overview`
- Mode: `Balanced`

## Architectural Style
The repository uses a workflow-oriented, multi-app script architecture.
Instead of a deeply modular package, it exposes three focused Gradio entry points that users run separately as stages of one broader image-editing flow.

## Core Components

### `src/app.py`
- Main decomposition app
- Loads `QwenImageLayeredPipeline`
- Produces RGBA layer outputs
- Builds PPTX, ZIP, and PSD exports

### `src/tool/edit_rgba_image.py`
- Companion editing app for one transparent layer at a time
- Uses `QwenImageEditPlusPipeline`
- Restores transparency with segmentation output from RMBG

### `src/tool/combine_layers.py`
- Final recomposition tool
- Alpha-composites multiple transparent layers in stack order

## Execution Flow
1. User runs `src/app.py` and submits an image with prompts and generation settings.
2. The decomposition pipeline generates multiple RGBA layers.
3. The app stores layer outputs and packages them as downloadable files.
4. User optionally opens `src/tool/edit_rgba_image.py` to modify individual layers.
5. Edited layers are passed to `src/tool/combine_layers.py` for final compositing.

## Data Flow
- Input image enters the main app as a PIL-compatible source image.
- Model inference creates layer images and temporary export artifacts.
- Individual layer files become the handoff contract between the three scripts.
- Final outputs are either editable layer packages or one recomposited image.

## Relationship Model
- `README.md` defines the operational path through the repo.
- `src/app.py` is the producer stage.
- `src/tool/edit_rgba_image.py` is the transformation stage.
- `src/tool/combine_layers.py` is the recomposition stage.
- The architecture is coupled by artifacts and user workflow, not by import graphs.

## External Dependencies
- Model pipelines from `diffusers`
- GPU-oriented inference via `torch`
- Web UI delivery through `gradio`
- Image packaging via `python-pptx` and `psd-tools`
- Segmentation support via `transformers` and `torchvision`

## Strengths
- Very legible architecture for operators and demo users
- Narrow component responsibilities
- Useful export formats that extend the workflow into external creative tools

## Risks And Unknowns
- Missing dependency manifest increases setup ambiguity.
- Referenced assets are not fully represented in the snapshot.
- The runtime appears sensitive to CUDA and model availability.
- Because app-to-app transfer is manual, user mistakes in ordering or asset selection are possible.
