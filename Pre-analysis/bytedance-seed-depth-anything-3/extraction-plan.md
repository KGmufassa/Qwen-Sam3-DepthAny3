# File Tree Extraction Plan: bytedance-seed-depth-anything-3

## Overview
- Project Type: python_depth_estimation_application_library
- Goal: how the app works, how can I apply to other apps
- Total Items: 123
- Included: 97
- Excluded: 26

---

## Included Paths
- README.md
- da3_streaming/README.md
- da3_streaming/configs/base_config.yaml
- da3_streaming/configs/kitti.yaml
- da3_streaming/configs/tum.yaml
- da3_streaming/da3_streaming.py
- da3_streaming/fastloop/__init__.py
- da3_streaming/fastloop/solve.cpp
- da3_streaming/fastloop/solve_python.py
- da3_streaming/loop_utils/__init__.py
- da3_streaming/loop_utils/alignment_torch.py
- da3_streaming/loop_utils/alignment_triton.py
- da3_streaming/loop_utils/config_utils.py
- da3_streaming/loop_utils/logging_utils.py
- da3_streaming/loop_utils/loop_detector.py
- da3_streaming/loop_utils/loop_refinement.py
- da3_streaming/loop_utils/sim3loop.py
- da3_streaming/loop_utils/sim3utils.py
- da3_streaming/npz_output_process.py
- da3_streaming/requirements.txt
- da3_streaming/scripts/download_weights.sh
- docs/API.md
- docs/CLI.md
- pyproject.toml
- requirements.txt
- src/depth_anything_3/api.py
- src/depth_anything_3/app/css_and_html.py
- src/depth_anything_3/app/gradio_app.py
- src/depth_anything_3/app/modules/__init__.py
- src/depth_anything_3/app/modules/event_handlers.py
- src/depth_anything_3/app/modules/file_handlers.py
- src/depth_anything_3/app/modules/model_inference.py
- src/depth_anything_3/app/modules/ui_components.py
- src/depth_anything_3/app/modules/utils.py
- src/depth_anything_3/app/modules/visualization.py
- src/depth_anything_3/cfg.py
- src/depth_anything_3/cli.py
- src/depth_anything_3/model/__init__.py
- src/depth_anything_3/model/cam_dec.py
- src/depth_anything_3/model/cam_enc.py
- src/depth_anything_3/model/da3.py
- src/depth_anything_3/model/dinov2/dinov2.py
- src/depth_anything_3/model/dinov2/layers/__init__.py
- src/depth_anything_3/model/dinov2/layers/attention.py
- src/depth_anything_3/model/dinov2/layers/block.py
- src/depth_anything_3/model/dinov2/layers/drop_path.py
- src/depth_anything_3/model/dinov2/layers/layer_scale.py
- src/depth_anything_3/model/dinov2/layers/mlp.py
- src/depth_anything_3/model/dinov2/layers/patch_embed.py
- src/depth_anything_3/model/dinov2/layers/rope.py
- src/depth_anything_3/model/dinov2/layers/swiglu_ffn.py
- src/depth_anything_3/model/dinov2/vision_transformer.py
- src/depth_anything_3/model/dpt.py
- src/depth_anything_3/model/dualdpt.py
- src/depth_anything_3/model/gs_adapter.py
- src/depth_anything_3/model/gsdpt.py
- src/depth_anything_3/model/reference_view_selector.py
- src/depth_anything_3/model/utils/attention.py
- src/depth_anything_3/model/utils/block.py
- src/depth_anything_3/model/utils/gs_renderer.py
- src/depth_anything_3/model/utils/head_utils.py
- src/depth_anything_3/model/utils/transform.py
- src/depth_anything_3/registry.py
- src/depth_anything_3/services/__init__.py
- src/depth_anything_3/services/backend.py
- src/depth_anything_3/services/gallery.py
- src/depth_anything_3/services/inference_service.py
- src/depth_anything_3/services/input_handlers.py
- src/depth_anything_3/specs.py
- src/depth_anything_3/utils/alignment.py
- src/depth_anything_3/utils/api_helpers.py
- src/depth_anything_3/utils/camera_trj_helpers.py
- src/depth_anything_3/utils/constants.py
- src/depth_anything_3/utils/export/__init__.py
- src/depth_anything_3/utils/export/colmap.py
- src/depth_anything_3/utils/export/depth_vis.py
- src/depth_anything_3/utils/export/feat_vis.py
- src/depth_anything_3/utils/export/glb.py
- src/depth_anything_3/utils/export/gs.py
- src/depth_anything_3/utils/export/npz.py
- src/depth_anything_3/utils/export/utils.py
- src/depth_anything_3/utils/geometry.py
- src/depth_anything_3/utils/gsply_helpers.py
- src/depth_anything_3/utils/io/input_processor.py
- src/depth_anything_3/utils/io/output_processor.py
- src/depth_anything_3/utils/layout_helpers.py
- src/depth_anything_3/utils/logger.py
- src/depth_anything_3/utils/memory.py
- src/depth_anything_3/utils/model_loading.py
- src/depth_anything_3/utils/parallel_utils.py
- src/depth_anything_3/utils/pca_utils.py
- src/depth_anything_3/utils/pose_align.py
- src/depth_anything_3/utils/ray_utils.py
- src/depth_anything_3/utils/read_write_model.py
- src/depth_anything_3/utils/registry.py
- src/depth_anything_3/utils/sh_helpers.py
- src/depth_anything_3/utils/visualize.py

---

## Excluded Paths (Detailed)
- .flake8
- .pre-commit-config.yaml
- LICENSE
- docs/BENCHMARK.md
- docs/funcs/ref_view_strategy.md
- src/depth_anything_3/bench/__init__.py
- src/depth_anything_3/bench/configs/eval_bench.yaml
- src/depth_anything_3/bench/dataset.py
- src/depth_anything_3/bench/datasets/__init__.py
- src/depth_anything_3/bench/datasets/dtu.py
- src/depth_anything_3/bench/datasets/dtu64.py
- src/depth_anything_3/bench/datasets/eth3d.py
- src/depth_anything_3/bench/datasets/hiroom.py
- src/depth_anything_3/bench/datasets/scannetpp.py
- src/depth_anything_3/bench/datasets/sevenscenes.py
- src/depth_anything_3/bench/evaluator.py
- src/depth_anything_3/bench/print_metrics.py
- src/depth_anything_3/bench/registries.py
- src/depth_anything_3/bench/utils.py
- src/depth_anything_3/configs/da3-base.yaml
- src/depth_anything_3/configs/da3-giant.yaml
- src/depth_anything_3/configs/da3-large.yaml
- src/depth_anything_3/configs/da3-small.yaml
- src/depth_anything_3/configs/da3metric-large.yaml
- src/depth_anything_3/configs/da3mono-large.yaml
- src/depth_anything_3/configs/da3nested-giant-large.yaml

---

## Simplified Exclusion List (KEY SECTION)

```text
docs/funcs, src/depth_anything_3/bench, src/depth_anything_3/configs, .flake8, .pre-commit-config.yaml, LICENSE, docs/BENCHMARK.md
```
id="simple-exclude-list"

---

## Representative Selections
- README.md
- pyproject.toml
- src/depth_anything_3/api.py
- src/depth_anything_3/cli.py
- src/depth_anything_3/services/inference_service.py
- src/depth_anything_3/services/backend.py
- src/depth_anything_3/app/gradio_app.py
- src/depth_anything_3/app/modules/model_inference.py
- src/depth_anything_3/model/da3.py
- src/depth_anything_3/model/reference_view_selector.py
- src/depth_anything_3/utils/model_loading.py
- da3_streaming/da3_streaming.py
- docs/API.md
- docs/CLI.md

---

## Patterns Detected
- Python package layout under `src/depth_anything_3/`
- Public integration surfaces exposed via `api.py`, `cli.py`, and `services/`
- Interactive app UI implemented under `src/depth_anything_3/app/`
- Core depth/model logic isolated under `src/depth_anything_3/model/`
- Reusable utilities and export/io helpers grouped under `src/depth_anything_3/utils/`
- Separate streaming pipeline provided in `da3_streaming/`
- Benchmark-only code isolated under `src/depth_anything_3/bench/`
- Additional user-facing documentation under `docs/`

---

## Selection Rules Applied
- Include packaging files plus API and CLI surfaces that frame installation and invocation.
- Include app, service, model, streaming, util, export, and io paths that reveal runtime flow and reuse boundaries.
- Include `docs/API.md` and `docs/CLI.md` because they likely describe integration surfaces without needing broad documentation review.
- Exclude benchmark modules, benchmark dataset adapters, secondary docs, and repo hygiene files for a first-pass integration analysis.
- Collapse simplified exclusions only when an entire directory is excluded.

---

## Reasoning
- The goal is to understand how the application works and how it can be reused in other apps.
- The most valuable paths are the ones defining public entry points, inference services, UI orchestration, model construction, and input/output conversion.
- Benchmark and evaluation code can matter later, but it is not necessary for identifying integration seams or application flow.

---

## Key Observations
- `src/depth_anything_3/api.py` and `src/depth_anything_3/services/` likely define the cleanest embedding points for another application.
- `src/depth_anything_3/app/gradio_app.py` suggests there is already a user-facing app layer separable from the core backend.
- `da3_streaming/` appears to provide a distinct streaming pipeline that may be useful for real-time or multi-app scenarios.
- `src/depth_anything_3/utils/export/` and `src/depth_anything_3/utils/io/` suggest the project already formalizes data interchange boundaries.

---

## Summary
- This plan keeps the files most likely to explain execution flow and application reuse.
- It excludes benchmarking, broad auxiliary docs, and repo maintenance files to reduce noise.
- Outputs are persisted under `./bytedance-seed-depth-anything-3/pre-analysis/` in both JSON and Markdown formats.
