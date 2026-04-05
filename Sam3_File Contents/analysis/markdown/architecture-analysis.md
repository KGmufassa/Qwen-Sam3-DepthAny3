# Architecture Analysis

## Inputs

- Repo folder: `./Sam3_File Contents`
- Focus: `Full Repository Overview`
- Mode: `Balanced`

## Architectural Style

Layered research/ML package with factory-driven model construction, runtime predictors, and an optional agent orchestration layer.

## Layers

### Documentation and setup
- Responsibility: README and pyproject describe installation, usage, packaging, and developer tooling.
- Primary files: `README.md`, `pyproject.toml`
### Assembly and configuration
- Responsibility: Factory functions compose model backbones, transformers, text encoders, and predictors.
- Primary files: `sam3/model_builder.py`
### Core modeling
- Responsibility: Encoder, geometry, segmentation, memory, VL fusion, and SAM primitives implement the main architecture.
- Primary files: `sam3/model/encoder.py`, `sam3/model/geometry_encoders.py`, `sam3/model/vl_combiner.py`, `sam3/sam/transformer.py`
### Inference runtimes
- Responsibility: Image and video predictors manage sessions, propagation, and request-oriented inference.
- Primary files: `sam3/model/sam3_image_processor.py`, `sam3/model/sam3_video_predictor.py`, `sam3/model/sam3_base_predictor.py`
### Agent orchestration
- Responsibility: LLM-guided reasoning selects tools and invokes SAM 3 segmentation plus visualization/debug output.
- Primary files: `sam3/agent/agent_core.py`, `sam3/agent/client_llm.py`, `sam3/agent/client_sam3.py`
### Evaluation and examples
- Responsibility: Scripts exercise benchmark, qualitative, speed, and dataset preparation workflows.
- Primary files: `scripts/measure_speed.py`, `scripts/qualitative_test.py`, `scripts/eval/gold/eval_sam3.py`

## Module Groups

- `agent_runtime`: 19 files
- `predictors`: 4 files
- `model_factory`: 1 files
- `model_components`: 6 files
- `model_support`: 22 files
- `sam_core`: 6 files
- `evaluation_and_scripts`: 9 files

## Primary Flows

### Image inference flow
- Client code loads or builds an image model through sam3/model_builder.py.
- sam3/model/sam3_image_processor.py normalizes input images and prompts.
- sam3/model/sam3_image.py executes feature extraction, prompt conditioning, and segmentation outputs.
- Post-processing returns masks, boxes, and scores to the caller.

### Video inference flow
- sam3/model_builder.py constructs video-capable predictor objects.
- sam3/model/sam3_base_predictor.py manages predictor state and request lifecycle.
- sam3/model/sam3_video_predictor.py handles session setup, propagation, and multi-GPU variants.
- sam3/model/io_utils.py loads frames from folders or video files for inference.

### Agent-assisted segmentation flow
- sam3/agent/inference.py or higher-level callers invoke sam3/agent/agent_core.py.
- sam3/agent/client_llm.py sends prompts and images to an OpenAI-compatible model for tool selection.
- sam3/agent/client_sam3.py formats requests to the SAM 3 segmentation service.
- sam3/agent/viz.py and helper modules render overlays and debug artifacts.

## Critical Relationships

- `sam3/model_builder.py` -> `sam3/model/*`: Central construction and wiring of most major components.
- `sam3/model/sam3_image.py` -> `sam3/model/geometry_encoders.py`: Prompt and geometry encoding feed image segmentation behavior.
- `sam3/model/sam3_video_predictor.py` -> `sam3/model/sam3_base_predictor.py`: Video predictor builds on shared predictor/session base logic.
- `sam3/agent/agent_core.py` -> `sam3/agent/client_llm.py`: LLM client determines next reasoning/action steps.
- `sam3/agent/agent_core.py` -> `sam3/agent/client_sam3.py`: Agent loop dispatches segmentation operations through service calls.

## Unknowns

- Several imports in the preprep snapshot reference modules not included in the extracted file set, suggesting partial extraction or missing internal packages.
- The exact runtime boundary between local predictor execution and remote SAM service execution is inferred from filenames and summaries, not validated from full source reading.
- No deployment packaging such as Dockerfiles or service manifests appears in the snapshot.
