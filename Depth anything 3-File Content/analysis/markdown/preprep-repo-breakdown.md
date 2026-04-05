# Repository Breakdown: Depth anything 3-File Content

## Overview

- Total Files Detected: 97
- Total Files Processed: 97
- Processing Mode: Balanced
- Goal: General understanding

## Entry Points

- `README.md`
- `da3_streaming/da3_streaming.py`
- `da3_streaming/fastloop/__init__.py`
- `da3_streaming/loop_utils/__init__.py`
- `da3_streaming/loop_utils/alignment_torch.py`
- `da3_streaming/loop_utils/alignment_triton.py`
- `da3_streaming/loop_utils/loop_detector.py`
- `da3_streaming/loop_utils/sim3loop.py`
- `da3_streaming/npz_output_process.py`
- `src/depth_anything_3/api.py`
- `src/depth_anything_3/app/gradio_app.py`
- `src/depth_anything_3/cli.py`
- `src/depth_anything_3/services/backend.py`
- `src/depth_anything_3/services/gallery.py`
- `src/depth_anything_3/utils/io/input_processor.py`
- `src/depth_anything_3/utils/logger.py`
- `src/depth_anything_3/utils/pose_align.py`
- `src/depth_anything_3/utils/read_write_model.py`

## Tech Stack

- Languages: python (85), markdown (4), yaml (3), text (2), cpp (1), shell (1), toml (1)
- Tools: FastAPI, Gradio, NumPy, OmegaConf, Open3D, OpenCV, Pillow, PyTorch, Typer, Uvicorn, e3nn, einops, huggingface_hub, imageio, matplotlib, moviepy, plyfile, pycolmap, requests, safetensors, torchvision, trimesh, xformers
- Runtime: Python >=3.9, <=3.13, CUDA GPU recommended

## File Breakdown

### README.md

- **Type:** documentation
- **Role:** project-overview
- **Priority:** high
- **Summary:** Documentation covering 📰 News, ✨ Highlights, 🏆 Model Zoo, 🛠️ Codebase Features.
- **Key Elements:** 📰 News, ✨ Highlights, 🏆 Model Zoo, 🛠️ Codebase Features, 🚀 Quick Start, 📦 Installation, 💻 Basic Usage, prediction.processed_images : [N, H, W, 3] uint8   array
- **Dependencies:** No internal dependencies resolved

### da3_streaming/da3_streaming.py

- **Type:** source
- **Role:** streaming-pipeline
- **Priority:** high
- **Summary:** Chunked long-video inference pipeline that extends DA3 with loop handling and memory-aware processing.
- **Key Elements:** depth_to_point_cloud_vectorized, remove_duplicates, DA3_Streaming, copy_file
- **Dependencies:** `src/depth_anything_3/api.py`

### docs/CLI.md

- **Type:** documentation
- **Role:** cli-doc
- **Priority:** high
- **Summary:** Documentation covering 🚀 Depth Anything 3 Command Line Interface, 📋 Table of Contents, 📖 Overview, ⚡ Quick Start.
- **Key Elements:** 🚀 Depth Anything 3 Command Line Interface, 📋 Table of Contents, 📖 Overview, ⚡ Quick Start, 🔧 Start backend service (optional, keeps model resident in GPU memory), 🚀 Use auto mode to process input, ♻️ Reuse backend for next job, 📚 Command Reference
- **Dependencies:** No internal dependencies resolved

### pyproject.toml

- **Type:** config
- **Role:** package-config
- **Priority:** high
- **Summary:** Build and packaging configuration defining dependencies, optional extras, CLI entry point, and Python version support.
- **Key Elements:** [build-system], [project], [project.optional-dependencies], [project.scripts], [project.urls], [tool.hatch.version], [tool.hatch.build.targets.wheel], [tool.hatch.build.targets.sdist]
- **Dependencies:** No internal dependencies resolved

### src/depth_anything_3/api.py

- **Type:** source
- **Role:** public-api
- **Priority:** high
- **Summary:** High-level Python API for loading pretrained Depth Anything 3 models, running inference, and exporting results.
- **Key Elements:** DepthAnything3
- **Dependencies:** `src/depth_anything_3/cfg.py`, `src/depth_anything_3/registry.py`, `src/depth_anything_3/specs.py`, `src/depth_anything_3/utils/export/__init__.py`, `src/depth_anything_3/utils/geometry.py`, `src/depth_anything_3/utils/io/input_processor.py`, `src/depth_anything_3/utils/io/output_processor.py`, `src/depth_anything_3/utils/logger.py`

### src/depth_anything_3/app/gradio_app.py

- **Type:** source
- **Role:** web-app-entry
- **Priority:** high
- **Summary:** Gradio application entry point that assembles the interactive reconstruction UI and wires event handlers.
- **Key Elements:** DepthAnything3App, main
- **Dependencies:** `src/depth_anything_3/app/css_and_html.py`, `src/depth_anything_3/app/modules/__init__.py`, `src/depth_anything_3/app/modules/event_handlers.py`, `src/depth_anything_3/app/modules/ui_components.py`, `src/depth_anything_3/app/modules/utils.py`

### src/depth_anything_3/app/modules/__init__.py

- **Type:** source
- **Role:** ui-layer
- **Priority:** high
- **Summary:** UI-related module with 0 classes and 0 top-level functions supporting the Gradio app.
- **Key Elements:** None extracted
- **Dependencies:** `src/depth_anything_3/app/modules/event_handlers.py`, `src/depth_anything_3/app/modules/file_handlers.py`, `src/depth_anything_3/app/modules/model_inference.py`, `src/depth_anything_3/app/modules/ui_components.py`, `src/depth_anything_3/app/modules/utils.py`, `src/depth_anything_3/app/modules/visualization.py`

### src/depth_anything_3/cli.py

- **Type:** source
- **Role:** cli-entry
- **Priority:** high
- **Summary:** Typer-based command-line interface that routes images, videos, and COLMAP inputs into local or backend inference workflows.
- **Key Elements:** detect_input_type, auto, image, images, colmap, video, backend, gradio
- **Dependencies:** `src/depth_anything_3/app/gradio_app.py`, `src/depth_anything_3/services/__init__.py`, `src/depth_anything_3/services/gallery.py`, `src/depth_anything_3/services/inference_service.py`, `src/depth_anything_3/services/input_handlers.py`, `src/depth_anything_3/utils/constants.py`

### src/depth_anything_3/model/utils/gs_renderer.py

- **Type:** source
- **Role:** utility-module
- **Priority:** high
- **Summary:** Utility module with 0 classes and 2 top-level functions used across inference, export, or visualization flows.
- **Key Elements:** render_3dgs, run_renderer_in_chunk_w_trj_mode
- **Dependencies:** `src/depth_anything_3/specs.py`, `src/depth_anything_3/utils/camera_trj_helpers.py`, `src/depth_anything_3/utils/geometry.py`, `src/depth_anything_3/utils/logger.py`

### src/depth_anything_3/services/__init__.py

- **Type:** source
- **Role:** service-layer
- **Priority:** high
- **Summary:** Service-layer module with 0 classes and 0 top-level functions for execution and I/O orchestration.
- **Key Elements:** None extracted
- **Dependencies:** `src/depth_anything_3/services/backend.py`

### src/depth_anything_3/services/backend.py

- **Type:** source
- **Role:** backend-service
- **Priority:** high
- **Summary:** FastAPI backend that keeps a model loaded in memory, queues inference tasks, and exposes status/result endpoints.
- **Key Elements:** InferenceRequest, InferenceResponse, TaskStatus, ModelBackend, _process_next_task, _run_inference_task, _cleanup_old_tasks, _schedule_task_cleanup
- **Dependencies:** `src/depth_anything_3/api.py`, `src/depth_anything_3/services/gallery.py`, `src/depth_anything_3/utils/memory.py`

### src/depth_anything_3/services/inference_service.py

- **Type:** source
- **Role:** inference-orchestrator
- **Priority:** high
- **Summary:** Unified service layer that runs inference locally or delegates work to the backend API.
- **Key Elements:** InferenceService, run_inference
- **Dependencies:** `src/depth_anything_3/api.py`

### da3_streaming/README.md

- **Type:** documentation
- **Role:** supporting-file
- **Priority:** medium
- **Summary:** Documentation covering **Updates**, Setup, Installation & Running, 📮 1 - Clone this project, 📦 2 - Environment Setup.
- **Key Elements:** **Updates**, Setup, Installation & Running, 📮 1 - Clone this project, 📦 2 - Environment Setup, Step 1: Dependency Installation, Step 2: Weights Download, System dependencies you may encounter., 🚀 3 - Running the code
- **Dependencies:** No internal dependencies resolved

### da3_streaming/configs/base_config.yaml

- **Type:** config
- **Role:** runtime-config
- **Priority:** medium
- **Summary:** Configuration file used by the surrounding pipeline or runtime.
- **Key Elements:** Weights, DA3, DA3_CONFIG, SALAD, Model, chunk_size, overlap, loop_chunk_size
- **Dependencies:** No internal dependencies resolved

### da3_streaming/configs/kitti.yaml

- **Type:** config
- **Role:** runtime-config
- **Priority:** medium
- **Summary:** Configuration file used by the surrounding pipeline or runtime.
- **Key Elements:** Weights, DA3, DA3_CONFIG, SALAD, Model, chunk_size, overlap, loop_chunk_size
- **Dependencies:** No internal dependencies resolved

### da3_streaming/configs/tum.yaml

- **Type:** config
- **Role:** runtime-config
- **Priority:** medium
- **Summary:** Configuration file used by the surrounding pipeline or runtime.
- **Key Elements:** Weights, DA3, DA3_CONFIG, SALAD, Model, chunk_size, overlap, loop_chunk_size
- **Dependencies:** No internal dependencies resolved

### da3_streaming/loop_utils/__init__.py

- **Type:** source
- **Role:** package-export
- **Priority:** medium
- **Summary:** Package initializer that exposes package-level symbols or marks import boundaries.
- **Key Elements:** None extracted
- **Dependencies:** No internal dependencies resolved

### da3_streaming/loop_utils/alignment_torch.py

- **Type:** source
- **Role:** supporting-file
- **Priority:** medium
- **Summary:** Supporting file module with 0 classes and 12 top-level functions.
- **Key Elements:** weighted_estimate_se3_torch, weighted_estimate_sim3_torch, weighted_estimate_sim3_numba_torch, huber_loss_torch, compute_residuals_torch, compute_huber_weights_torch, apply_transformation_torch, robust_weighted_estimate_sim3_torch
- **Dependencies:** No internal dependencies resolved

### da3_streaming/loop_utils/alignment_triton.py

- **Type:** source
- **Role:** supporting-file
- **Priority:** medium
- **Summary:** Supporting file module with 0 classes and 14 top-level functions.
- **Key Elements:** apply_transformation_residual_kernel, weighted_covariance_kernel, compute_huber_weights_kernel, weighted_mean_kernel, apply_transformation_residual_triton, compute_weighted_mean_triton, compute_weighted_covariance_triton, compute_huber_weights_triton
- **Dependencies:** No internal dependencies resolved

### da3_streaming/loop_utils/loop_detector.py

- **Type:** source
- **Role:** supporting-file
- **Priority:** medium
- **Summary:** Supporting file module with 2 classes and 1 top-level functions.
- **Key Elements:** VPRModel, LoopDetector, main
- **Dependencies:** No internal dependencies resolved

### da3_streaming/loop_utils/loop_refinement.py

- **Type:** source
- **Role:** supporting-file
- **Priority:** medium
- **Summary:** Supporting file module with 0 classes and 11 top-level functions.
- **Key Elements:** make_pypose_Sim3, SE3_to_Sim3, _format, reduce_edges, umeyama_alignment, ransac_umeyama, batch_jacobian, _residual
- **Dependencies:** No internal dependencies resolved

### da3_streaming/loop_utils/sim3loop.py

- **Type:** source
- **Role:** supporting-file
- **Priority:** medium
- **Summary:** Supporting file module with 1 classes and 2 top-level functions.
- **Key Elements:** Sim3LoopOptimizer, create_ring_transforms, example_usage
- **Dependencies:** No internal dependencies resolved

### da3_streaming/loop_utils/sim3utils.py

- **Type:** source
- **Role:** supporting-file
- **Priority:** medium
- **Summary:** Supporting file module with 0 classes and 20 top-level functions.
- **Key Elements:** accumulate_sim3_transforms, estimate_sim3, align_point_maps, apply_sim3, apply_sim3_direct, compute_alignment_error, save_confident_pointcloud, save_confident_pointcloud_batch
- **Dependencies:** No internal dependencies resolved

### da3_streaming/requirements.txt

- **Type:** config
- **Role:** dependency-manifest
- **Priority:** medium
- **Summary:** Dependency manifest listing runtime packages needed for inference, services, and export tooling.
- **Key Elements:** None extracted
- **Dependencies:** No internal dependencies resolved

### docs/API.md

- **Type:** documentation
- **Role:** api-doc
- **Priority:** medium
- **Summary:** Documentation covering repository usage and structure.
- **Key Elements:** None extracted
- **Dependencies:** No internal dependencies resolved

### requirements.txt

- **Type:** config
- **Role:** dependency-manifest
- **Priority:** medium
- **Summary:** Dependency manifest listing runtime packages needed for inference, services, and export tooling.
- **Key Elements:** None extracted
- **Dependencies:** No internal dependencies resolved

### src/depth_anything_3/app/css_and_html.py

- **Type:** source
- **Role:** ui-layer
- **Priority:** medium
- **Summary:** UI-related module with 0 classes and 4 top-level functions supporting the Gradio app.
- **Key Elements:** get_header_html, get_description_html, get_acknowledgements_html, get_gradio_theme
- **Dependencies:** No internal dependencies resolved

### src/depth_anything_3/app/modules/event_handlers.py

- **Type:** source
- **Role:** ui-layer
- **Priority:** medium
- **Summary:** UI-related module with 1 classes and 0 top-level functions supporting the Gradio app.
- **Key Elements:** EventHandlers
- **Dependencies:** `src/depth_anything_3/app/modules/__init__.py`, `src/depth_anything_3/app/modules/file_handlers.py`, `src/depth_anything_3/app/modules/model_inference.py`, `src/depth_anything_3/app/modules/utils.py`, `src/depth_anything_3/app/modules/visualization.py`, `src/depth_anything_3/utils/memory.py`

### src/depth_anything_3/app/modules/file_handlers.py

- **Type:** source
- **Role:** ui-layer
- **Priority:** medium
- **Summary:** UI-related module with 1 classes and 0 top-level functions supporting the Gradio app.
- **Key Elements:** FileHandler
- **Dependencies:** `src/depth_anything_3/app/modules/__init__.py`, `src/depth_anything_3/app/modules/utils.py`

### src/depth_anything_3/app/modules/model_inference.py

- **Type:** source
- **Role:** ui-layer
- **Priority:** medium
- **Summary:** UI-related module with 1 classes and 0 top-level functions supporting the Gradio app.
- **Key Elements:** ModelInference
- **Dependencies:** `src/depth_anything_3/api.py`, `src/depth_anything_3/utils/export/__init__.py`, `src/depth_anything_3/utils/export/glb.py`, `src/depth_anything_3/utils/export/gs.py`, `src/depth_anything_3/utils/memory.py`

### src/depth_anything_3/app/modules/ui_components.py

- **Type:** source
- **Role:** ui-layer
- **Priority:** medium
- **Summary:** UI-related module with 1 classes and 0 top-level functions supporting the Gradio app.
- **Key Elements:** UIComponents
- **Dependencies:** `src/depth_anything_3/app/css_and_html.py`, `src/depth_anything_3/app/modules/__init__.py`, `src/depth_anything_3/app/modules/utils.py`

### src/depth_anything_3/app/modules/utils.py

- **Type:** source
- **Role:** ui-layer
- **Priority:** medium
- **Summary:** UI-related module with 0 classes and 4 top-level functions supporting the Gradio app.
- **Key Elements:** create_depth_visualization, save_to_gallery_func, get_scene_info, get_logo_base64
- **Dependencies:** No internal dependencies resolved

### src/depth_anything_3/app/modules/visualization.py

- **Type:** source
- **Role:** ui-layer
- **Priority:** medium
- **Summary:** UI-related module with 1 classes and 0 top-level functions supporting the Gradio app.
- **Key Elements:** VisualizationHandler
- **Dependencies:** No internal dependencies resolved

### src/depth_anything_3/model/__init__.py

- **Type:** source
- **Role:** model-component
- **Priority:** medium
- **Summary:** Model implementation module with 0 classes and 0 top-level functions for geometry or network behavior.
- **Key Elements:** None extracted
- **Dependencies:** `src/depth_anything_3/model/da3.py`

### src/depth_anything_3/model/cam_dec.py

- **Type:** source
- **Role:** model-component
- **Priority:** medium
- **Summary:** Model implementation module with 1 classes and 0 top-level functions for geometry or network behavior.
- **Key Elements:** CameraDec
- **Dependencies:** No internal dependencies resolved

### src/depth_anything_3/model/cam_enc.py

- **Type:** source
- **Role:** model-component
- **Priority:** medium
- **Summary:** Model implementation module with 1 classes and 0 top-level functions for geometry or network behavior.
- **Key Elements:** CameraEnc
- **Dependencies:** `src/depth_anything_3/model/__init__.py`, `src/depth_anything_3/model/utils/attention.py`, `src/depth_anything_3/model/utils/block.py`, `src/depth_anything_3/model/utils/transform.py`, `src/depth_anything_3/utils/geometry.py`

### src/depth_anything_3/model/da3.py

- **Type:** source
- **Role:** model-component
- **Priority:** medium
- **Summary:** Model implementation module with 2 classes and 1 top-level functions for geometry or network behavior.
- **Key Elements:** _wrap_cfg, DepthAnything3Net, NestedDepthAnything3Net
- **Dependencies:** `src/depth_anything_3/cfg.py`, `src/depth_anything_3/model/__init__.py`, `src/depth_anything_3/model/utils/transform.py`, `src/depth_anything_3/utils/alignment.py`, `src/depth_anything_3/utils/geometry.py`, `src/depth_anything_3/utils/ray_utils.py`

### src/depth_anything_3/model/dinov2/dinov2.py

- **Type:** source
- **Role:** model-component
- **Priority:** medium
- **Summary:** Model implementation module with 1 classes and 0 top-level functions for geometry or network behavior.
- **Key Elements:** DinoV2
- **Dependencies:** `src/depth_anything_3/model/__init__.py`, `src/depth_anything_3/model/dinov2/vision_transformer.py`

### src/depth_anything_3/model/dinov2/layers/__init__.py

- **Type:** source
- **Role:** model-component
- **Priority:** medium
- **Summary:** Model implementation module with 0 classes and 0 top-level functions for geometry or network behavior.
- **Key Elements:** None extracted
- **Dependencies:** No internal dependencies resolved

### src/depth_anything_3/model/dinov2/layers/attention.py

- **Type:** source
- **Role:** model-component
- **Priority:** medium
- **Summary:** Model implementation module with 1 classes and 0 top-level functions for geometry or network behavior.
- **Key Elements:** Attention
- **Dependencies:** No internal dependencies resolved

### src/depth_anything_3/model/dinov2/layers/block.py

- **Type:** source
- **Role:** model-component
- **Priority:** medium
- **Summary:** Model implementation module with 1 classes and 2 top-level functions for geometry or network behavior.
- **Key Elements:** Block, drop_add_residual_stochastic_depth, get_branges_scales
- **Dependencies:** `src/depth_anything_3/model/dinov2/layers/attention.py`, `src/depth_anything_3/model/dinov2/layers/drop_path.py`, `src/depth_anything_3/model/dinov2/layers/layer_scale.py`, `src/depth_anything_3/model/dinov2/layers/mlp.py`

### src/depth_anything_3/model/dinov2/layers/drop_path.py

- **Type:** source
- **Role:** model-component
- **Priority:** medium
- **Summary:** Model implementation module with 1 classes and 1 top-level functions for geometry or network behavior.
- **Key Elements:** drop_path, DropPath
- **Dependencies:** No internal dependencies resolved

### src/depth_anything_3/model/dinov2/layers/layer_scale.py

- **Type:** source
- **Role:** model-component
- **Priority:** medium
- **Summary:** Model implementation module with 1 classes and 0 top-level functions for geometry or network behavior.
- **Key Elements:** LayerScale
- **Dependencies:** No internal dependencies resolved

### src/depth_anything_3/model/dinov2/layers/mlp.py

- **Type:** source
- **Role:** model-component
- **Priority:** medium
- **Summary:** Model implementation module with 1 classes and 0 top-level functions for geometry or network behavior.
- **Key Elements:** Mlp
- **Dependencies:** No internal dependencies resolved

### src/depth_anything_3/model/dinov2/layers/patch_embed.py

- **Type:** source
- **Role:** model-component
- **Priority:** medium
- **Summary:** Model implementation module with 1 classes and 1 top-level functions for geometry or network behavior.
- **Key Elements:** make_2tuple, PatchEmbed
- **Dependencies:** No internal dependencies resolved

### src/depth_anything_3/model/dinov2/layers/rope.py

- **Type:** source
- **Role:** model-component
- **Priority:** medium
- **Summary:** Model implementation module with 2 classes and 0 top-level functions for geometry or network behavior.
- **Key Elements:** PositionGetter, RotaryPositionEmbedding2D
- **Dependencies:** No internal dependencies resolved

### src/depth_anything_3/model/dinov2/layers/swiglu_ffn.py

- **Type:** source
- **Role:** model-component
- **Priority:** medium
- **Summary:** Model implementation module with 2 classes and 0 top-level functions for geometry or network behavior.
- **Key Elements:** SwiGLUFFN, SwiGLUFFNFused
- **Dependencies:** No internal dependencies resolved

### src/depth_anything_3/model/dinov2/vision_transformer.py

- **Type:** source
- **Role:** model-component
- **Priority:** medium
- **Summary:** Model implementation module with 2 classes and 6 top-level functions for geometry or network behavior.
- **Key Elements:** get_1d_sincos_pos_embed_from_grid, named_apply, BlockChunk, DinoVisionTransformer, vit_small, vit_base, vit_large, vit_giant2
- **Dependencies:** `src/depth_anything_3/model/__init__.py`, `src/depth_anything_3/model/dinov2/layers/__init__.py`, `src/depth_anything_3/model/reference_view_selector.py`, `src/depth_anything_3/utils/constants.py`, `src/depth_anything_3/utils/logger.py`

### src/depth_anything_3/model/dpt.py

- **Type:** source
- **Role:** model-component
- **Priority:** medium
- **Summary:** Model implementation module with 3 classes and 2 top-level functions for geometry or network behavior.
- **Key Elements:** DPT, _make_fusion_block, _make_scratch, ResidualConvUnit, FeatureFusionBlock
- **Dependencies:** `src/depth_anything_3/model/__init__.py`, `src/depth_anything_3/model/utils/head_utils.py`

### src/depth_anything_3/model/dualdpt.py

- **Type:** source
- **Role:** model-component
- **Priority:** medium
- **Summary:** Model implementation module with 1 classes and 0 top-level functions for geometry or network behavior.
- **Key Elements:** DualDPT
- **Dependencies:** `src/depth_anything_3/model/__init__.py`, `src/depth_anything_3/model/dpt.py`, `src/depth_anything_3/model/utils/head_utils.py`

### src/depth_anything_3/model/gs_adapter.py

- **Type:** source
- **Role:** model-component
- **Priority:** medium
- **Summary:** Model implementation module with 1 classes and 0 top-level functions for geometry or network behavior.
- **Key Elements:** GaussianAdapter
- **Dependencies:** `src/depth_anything_3/model/__init__.py`, `src/depth_anything_3/model/utils/transform.py`, `src/depth_anything_3/specs.py`, `src/depth_anything_3/utils/geometry.py`, `src/depth_anything_3/utils/pose_align.py`, `src/depth_anything_3/utils/sh_helpers.py`

### src/depth_anything_3/model/gsdpt.py

- **Type:** source
- **Role:** model-component
- **Priority:** medium
- **Summary:** Model implementation module with 1 classes and 0 top-level functions for geometry or network behavior.
- **Key Elements:** GSDPT
- **Dependencies:** `src/depth_anything_3/model/__init__.py`, `src/depth_anything_3/model/dpt.py`, `src/depth_anything_3/model/utils/head_utils.py`

### src/depth_anything_3/model/reference_view_selector.py

- **Type:** source
- **Role:** model-component
- **Priority:** medium
- **Summary:** Model implementation module with 0 classes and 3 top-level functions for geometry or network behavior.
- **Key Elements:** select_reference_view, reorder_by_reference, restore_original_order
- **Dependencies:** No internal dependencies resolved

### src/depth_anything_3/model/utils/attention.py

- **Type:** source
- **Role:** utility-module
- **Priority:** medium
- **Summary:** Utility module with 3 classes and 0 top-level functions used across inference, export, or visualization flows.
- **Key Elements:** Attention, LayerScale, Mlp
- **Dependencies:** No internal dependencies resolved

### src/depth_anything_3/model/utils/block.py

- **Type:** source
- **Role:** utility-module
- **Priority:** medium
- **Summary:** Utility module with 1 classes and 0 top-level functions used across inference, export, or visualization flows.
- **Key Elements:** Block
- **Dependencies:** `src/depth_anything_3/model/utils/attention.py`

### src/depth_anything_3/model/utils/head_utils.py

- **Type:** source
- **Role:** utility-module
- **Priority:** medium
- **Summary:** Utility module with 1 classes and 5 top-level functions used across inference, export, or visualization flows.
- **Key Elements:** activate_head_gs, Permute, position_grid_to_embed, make_sincos_pos_embed, create_uv_grid, custom_interpolate
- **Dependencies:** No internal dependencies resolved

### src/depth_anything_3/model/utils/transform.py

- **Type:** source
- **Role:** utility-module
- **Priority:** medium
- **Summary:** Utility module with 0 classes and 7 top-level functions used across inference, export, or visualization flows.
- **Key Elements:** extri_intri_to_pose_encoding, pose_encoding_to_extri_intri, quat_to_mat, mat_to_quat, _sqrt_positive_part, standardize_quaternion, cam_quat_xyzw_to_world_quat_wxyz
- **Dependencies:** No internal dependencies resolved

### src/depth_anything_3/services/gallery.py

- **Type:** source
- **Role:** service-layer
- **Priority:** medium
- **Summary:** Service-layer module with 1 classes and 6 top-level functions for execution and I/O orchestration.
- **Key Elements:** _url_join, _is_plain_name, build_group_list, build_group_manifest, GalleryHandler, gallery, main
- **Dependencies:** No internal dependencies resolved

### src/depth_anything_3/services/input_handlers.py

- **Type:** source
- **Role:** service-layer
- **Priority:** medium
- **Summary:** Service-layer module with 5 classes and 1 top-level functions for execution and I/O orchestration.
- **Key Elements:** InputHandler, ImageHandler, ImagesHandler, ColmapHandler, VideoHandler, parse_export_feat
- **Dependencies:** `src/depth_anything_3/utils/read_write_model.py`

### src/depth_anything_3/utils/camera_trj_helpers.py

- **Type:** source
- **Role:** utility-module
- **Priority:** medium
- **Summary:** Utility module with 0 classes and 17 top-level functions used across inference, export, or visualization flows.
- **Key Elements:** render_stabilization_path, render_wander_path, render_dolly_zoom_path, interpolate_intrinsics, intersect_rays, normalize, generate_coordinate_frame, generate_rotation_coordinate_frame
- **Dependencies:** `src/depth_anything_3/utils/geometry.py`, `src/depth_anything_3/utils/logger.py`

### src/depth_anything_3/utils/export/__init__.py

- **Type:** source
- **Role:** utility-module
- **Priority:** medium
- **Summary:** Utility module with 0 classes and 1 top-level functions used across inference, export, or visualization flows.
- **Key Elements:** export
- **Dependencies:** `src/depth_anything_3/specs.py`, `src/depth_anything_3/utils/export/gs.py`

### src/depth_anything_3/utils/export/glb.py

- **Type:** source
- **Role:** utility-module
- **Priority:** medium
- **Summary:** Utility module with 0 classes and 12 top-level functions used across inference, export, or visualization flows.
- **Key Elements:** set_sky_depth, get_conf_thresh, export_to_glb, _as_homogeneous44, _depths_to_world_points_with_colors, _filter_and_downsample, _estimate_scene_scale, _compute_alignment_transform_first_cam_glTF_center_by_points
- **Dependencies:** `src/depth_anything_3/specs.py`, `src/depth_anything_3/utils/export/depth_vis.py`, `src/depth_anything_3/utils/logger.py`

### src/depth_anything_3/utils/geometry.py

- **Type:** source
- **Role:** utility-module
- **Priority:** medium
- **Summary:** Utility module with 0 classes and 20 top-level functions used across inference, export, or visualization flows.
- **Key Elements:** as_homogeneous, affine_inverse, transpose_last_two_axes, affine_inverse_np, quat_to_mat, mat_to_quat, _sqrt_positive_part, standardize_quaternion
- **Dependencies:** No internal dependencies resolved

### src/depth_anything_3/utils/io/input_processor.py

- **Type:** source
- **Role:** utility-module
- **Priority:** medium
- **Summary:** Utility module with 1 classes and 0 top-level functions used across inference, export, or visualization flows.
- **Key Elements:** InputProcessor
- **Dependencies:** `src/depth_anything_3/utils/logger.py`, `src/depth_anything_3/utils/parallel_utils.py`

### src/depth_anything_3/utils/pose_align.py

- **Type:** source
- **Role:** utility-module
- **Priority:** medium
- **Summary:** Utility module with 0 classes and 14 top-level functions used across inference, export, or visualization flows.
- **Key Elements:** batch_apply_alignment_to_enc, batch_apply_alignment_to_ext, batch_align_poses_umeyama, _to44, _poses_from_ext, _umeyama_sim3_from_paths, _apply_sim3_to_poses, _median_nn_thresh
- **Dependencies:** `src/depth_anything_3/utils/geometry.py`

### src/depth_anything_3/utils/ray_utils.py

- **Type:** source
- **Role:** utility-module
- **Priority:** medium
- **Summary:** Utility module with 0 classes and 10 top-level functions used across inference, export, or visualization flows.
- **Key Elements:** compute_optimal_rotation_intrinsics_batch, ql_decomposition, find_homography_least_squares_weighted_torch, ransac_find_homography_weighted, find_homography_least_squares_weighted_torch_batch, ransac_find_homography_weighted_fast, ransac_find_homography_weighted_fast_batch, get_params_for_ransac
- **Dependencies:** `src/depth_anything_3/utils/geometry.py`

### src/depth_anything_3/utils/read_write_model.py

- **Type:** source
- **Role:** utility-module
- **Priority:** medium
- **Summary:** Utility module with 1 classes and 19 top-level functions used across inference, export, or visualization flows.
- **Key Elements:** Image, read_next_bytes, write_next_bytes, read_cameras_text, read_cameras_binary, write_cameras_text, write_cameras_binary, read_images_text
- **Dependencies:** No internal dependencies resolved

## Relationships

- `da3_streaming/da3_streaming.py` -> `src/depth_anything_3/api.py`
- `src/depth_anything_3/api.py` -> `src/depth_anything_3/cfg.py`
- `src/depth_anything_3/api.py` -> `src/depth_anything_3/registry.py`
- `src/depth_anything_3/api.py` -> `src/depth_anything_3/specs.py`
- `src/depth_anything_3/api.py` -> `src/depth_anything_3/utils/export/__init__.py`
- `src/depth_anything_3/api.py` -> `src/depth_anything_3/utils/geometry.py`
- `src/depth_anything_3/api.py` -> `src/depth_anything_3/utils/io/input_processor.py`
- `src/depth_anything_3/api.py` -> `src/depth_anything_3/utils/io/output_processor.py`
- `src/depth_anything_3/api.py` -> `src/depth_anything_3/utils/logger.py`
- `src/depth_anything_3/api.py` -> `src/depth_anything_3/utils/pose_align.py`
- `src/depth_anything_3/app/gradio_app.py` -> `src/depth_anything_3/app/css_and_html.py`
- `src/depth_anything_3/app/gradio_app.py` -> `src/depth_anything_3/app/modules/__init__.py`
- `src/depth_anything_3/app/gradio_app.py` -> `src/depth_anything_3/app/modules/event_handlers.py`
- `src/depth_anything_3/app/gradio_app.py` -> `src/depth_anything_3/app/modules/ui_components.py`
- `src/depth_anything_3/app/gradio_app.py` -> `src/depth_anything_3/app/modules/utils.py`
- `src/depth_anything_3/app/modules/__init__.py` -> `src/depth_anything_3/app/modules/event_handlers.py`
- `src/depth_anything_3/app/modules/__init__.py` -> `src/depth_anything_3/app/modules/file_handlers.py`
- `src/depth_anything_3/app/modules/__init__.py` -> `src/depth_anything_3/app/modules/model_inference.py`
- `src/depth_anything_3/app/modules/__init__.py` -> `src/depth_anything_3/app/modules/ui_components.py`
- `src/depth_anything_3/app/modules/__init__.py` -> `src/depth_anything_3/app/modules/utils.py`
- `src/depth_anything_3/app/modules/__init__.py` -> `src/depth_anything_3/app/modules/visualization.py`
- `src/depth_anything_3/app/modules/event_handlers.py` -> `src/depth_anything_3/app/modules/__init__.py`
- `src/depth_anything_3/app/modules/event_handlers.py` -> `src/depth_anything_3/app/modules/file_handlers.py`
- `src/depth_anything_3/app/modules/event_handlers.py` -> `src/depth_anything_3/app/modules/model_inference.py`
- `src/depth_anything_3/app/modules/event_handlers.py` -> `src/depth_anything_3/app/modules/utils.py`
- `src/depth_anything_3/app/modules/event_handlers.py` -> `src/depth_anything_3/app/modules/visualization.py`
- `src/depth_anything_3/app/modules/event_handlers.py` -> `src/depth_anything_3/utils/memory.py`
- `src/depth_anything_3/app/modules/file_handlers.py` -> `src/depth_anything_3/app/modules/__init__.py`
- `src/depth_anything_3/app/modules/file_handlers.py` -> `src/depth_anything_3/app/modules/utils.py`
- `src/depth_anything_3/app/modules/model_inference.py` -> `src/depth_anything_3/api.py`
- `src/depth_anything_3/app/modules/model_inference.py` -> `src/depth_anything_3/utils/export/__init__.py`
- `src/depth_anything_3/app/modules/model_inference.py` -> `src/depth_anything_3/utils/export/glb.py`
- `src/depth_anything_3/app/modules/model_inference.py` -> `src/depth_anything_3/utils/export/gs.py`
- `src/depth_anything_3/app/modules/model_inference.py` -> `src/depth_anything_3/utils/memory.py`
- `src/depth_anything_3/app/modules/ui_components.py` -> `src/depth_anything_3/app/css_and_html.py`
- `src/depth_anything_3/app/modules/ui_components.py` -> `src/depth_anything_3/app/modules/__init__.py`
- `src/depth_anything_3/app/modules/ui_components.py` -> `src/depth_anything_3/app/modules/utils.py`
- `src/depth_anything_3/cli.py` -> `src/depth_anything_3/app/gradio_app.py`
- `src/depth_anything_3/cli.py` -> `src/depth_anything_3/services/__init__.py`
- `src/depth_anything_3/cli.py` -> `src/depth_anything_3/services/gallery.py`
- ... plus 82 additional dependency links

## Key Observations

- The repo exposes the core DA3 inference stack through a Python API, a Typer CLI, and a Gradio UI.
- A FastAPI backend keeps models resident in memory and queues inference jobs, which fits long GPU-bound workloads.
- A separate `da3_streaming` subsystem extends the main package for chunked long-video processing and loop-aware alignment.
- Most files live in model and utility layers, indicating a research-style codebase with reusable geometry, export, and visualization helpers.
- Multiple export helpers suggest the project is designed for downstream reconstruction, visualization, and interoperability rather than depth-only output.

## Unknowns / Issues

- No structural validation issues detected from the markdown snapshot.

## Summary

- Depth Anything 3 is a visual geometry toolkit centered on a pretrained PyTorch model that predicts depth, pose, and related 3D outputs from single-view or multi-view imagery.
- The repository is organized around `src/depth_anything_3` for the main package, with separate service/UI layers, model internals, export helpers, and an additional `da3_streaming` pipeline for long video inference.
