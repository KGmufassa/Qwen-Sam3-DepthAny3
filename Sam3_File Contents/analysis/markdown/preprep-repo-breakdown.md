# Repository Breakdown: Sam3_File Contents

## Overview

- Total Files Detected: 81
- Total Files Processed: 81
- Processing Mode: Deep
- Goal: General understanding

## Entry Points

- `README.md`
- `sam3/agent/helpers/color_map.py`
- `sam3/model_builder.py`
- `scripts/eval/gold/eval_sam3.py`
- `scripts/eval/standalone_cgf1.py`
- `scripts/eval/veval/README.md`
- `scripts/eval/veval/__init__.py`
- `scripts/eval/veval/saco_yt1b_annot_update.py`
- `scripts/eval/veval/saco_yt1b_downloader.py`
- `scripts/eval/veval/saco_yt1b_frame_prep_util.py`
- `scripts/measure_speed.py`
- `scripts/qualitative_test.py`

## Tech Stack

- Languages: python (76), markdown (2), text (2), toml (1)
- Tools: Jupyter, OpenCV, Pillow, PyTorch, huggingface_hub, iopath, matplotlib, numpy, torchvision
- Runtime: Python >=3.8, CUDA GPU recommended

## File Breakdown

### README.md

- **Type:** documentation
- **Role:** project-overview
- **Priority:** high
- **Summary:** Top-level project documentation describing SAM 3 capabilities, setup, usage, examples, and benchmarks.
- **Key Elements:** SAM 3: Segment Anything with Concepts, Latest updates, Installation, Prerequisites, Getting Started, Basic Usage, Examples, Model
- **Dependencies:** No internal dependencies resolved

### pyproject.toml

- **Type:** config
- **Role:** package-config
- **Priority:** high
- **Summary:** Build and packaging configuration defining dependencies, extras, Python versions, and developer tooling.
- **Key Elements:** [build-system], [project], [project.optional-dependencies], [project.urls], [tool.setuptools.packages.find], [tool.setuptools.package-data], [tool.setuptools.dynamic], [tool.black]
- **Dependencies:** No internal dependencies resolved

### sam3/__init__.py

- **Type:** source
- **Role:** package-export
- **Priority:** high
- **Summary:** Package export module with 0 classes and 0 top-level functions.
- **Key Elements:** None extracted
- **Dependencies:** No internal dependencies resolved

### sam3/agent/agent_core.py

- **Type:** source
- **Role:** agent-runtime
- **Priority:** high
- **Summary:** Agent loop that combines MLLM tool decisions, SAM 3 service calls, debugging output, and visualization.
- **Key Elements:** save_debug_messages, cleanup_debug_files, count_images, _prune_messages_for_next_round, agent_inference
- **Dependencies:** `sam3/agent/client_llm.py`, `sam3/agent/client_sam3.py`, `sam3/agent/viz.py`

### sam3/model/sam3_base_predictor.py

- **Type:** source
- **Role:** predictor
- **Priority:** high
- **Summary:** Predictor module with 1 classes and 0 top-level functions.
- **Key Elements:** Sam3BasePredictor
- **Dependencies:** `sam3/logger.py`

### sam3/model/sam3_image.py

- **Type:** source
- **Role:** model-support
- **Priority:** high
- **Summary:** Model support module with 2 classes and 1 top-level functions.
- **Key Elements:** _update_out, Sam3Image, Sam3ImageOnVideoMultiGPU
- **Dependencies:** `sam3/model/act_ckpt_utils.py`, `sam3/model/box_ops.py`, `sam3/model/data_misc.py`, `sam3/model/geometry_encoders.py`, `sam3/model/model_misc.py`, `sam3/model/sam1_task_predictor.py`, `sam3/model/vl_combiner.py`

### sam3/model/sam3_image_processor.py

- **Type:** source
- **Role:** model-support
- **Priority:** high
- **Summary:** Stateful image inference wrapper for setting inputs, applying prompts, and producing masks, boxes, and scores.
- **Key Elements:** Sam3Processor
- **Dependencies:** `sam3/model/__init__.py`, `sam3/model/box_ops.py`, `sam3/model/data_misc.py`

### sam3/model/sam3_multiplex_video_predictor.py

- **Type:** source
- **Role:** predictor
- **Priority:** high
- **Summary:** Predictor module with 1 classes and 0 top-level functions.
- **Key Elements:** Sam3MultiplexVideoPredictor
- **Dependencies:** `sam3/logger.py`, `sam3/model/sam3_base_predictor.py`

### sam3/model/sam3_video_predictor.py

- **Type:** source
- **Role:** predictor
- **Priority:** high
- **Summary:** Session-oriented video predictor that serves request dispatch, propagation, and optional multi-GPU execution.
- **Key Elements:** Sam3VideoPredictor, Sam3VideoPredictorMultiGPU
- **Dependencies:** `sam3/logger.py`, `sam3/model/sam3_base_predictor.py`

### sam3/model_builder.py

- **Type:** source
- **Role:** model-factory
- **Priority:** high
- **Summary:** Central factory module that constructs image, video, and multiplex model variants and handles checkpoint setup.
- **Key Elements:** _setup_tf32, _create_position_encoding, _create_vit_backbone, _create_vit_neck, _create_vl_backbone, _create_transformer_encoder, _create_transformer_decoder, _create_dot_product_scoring
- **Dependencies:** `sam3/model/encoder.py`, `sam3/model/geometry_encoders.py`, `sam3/model/maskformer_segmentation.py`, `sam3/model/memory.py`, `sam3/model/model_misc.py`, `sam3/model/multiplex_utils.py`, `sam3/model/necks.py`, `sam3/model/position_encoding.py`, `sam3/model/sam1_task_predictor.py`, `sam3/model/sam3_image.py`

### scripts/measure_speed.py

- **Type:** source
- **Role:** utility-script
- **Priority:** high
- **Summary:** Utility script module with 0 classes and 5 top-level functions.
- **Key Elements:** max_memory_allocated, synthesize_video_data, profiler_runner, main_loop, run_test
- **Dependencies:** No internal dependencies resolved

### scripts/qualitative_test.py

- **Type:** source
- **Role:** utility-script
- **Priority:** high
- **Summary:** Utility script module with 0 classes and 7 top-level functions.
- **Key Elements:** extract_frames, synthesize_video, load_frame, render_overlay, save_overlay, collect_propagation, main
- **Dependencies:** No internal dependencies resolved

### sam3/agent/client_llm.py

- **Type:** source
- **Role:** agent-runtime
- **Priority:** medium
- **Summary:** Agent runtime module with 0 classes and 3 top-level functions.
- **Key Elements:** get_image_base64_and_mime, send_generate_request, send_direct_request
- **Dependencies:** No internal dependencies resolved

### sam3/agent/client_sam3.py

- **Type:** source
- **Role:** agent-runtime
- **Priority:** medium
- **Summary:** Agent runtime module with 0 classes and 2 top-level functions.
- **Key Elements:** sam3_inference, call_sam_service
- **Dependencies:** `sam3/agent/helpers/mask_overlap_removal.py`, `sam3/agent/viz.py`, `sam3/model/box_ops.py`

### sam3/agent/helpers/boxes.py

- **Type:** source
- **Role:** agent-runtime
- **Priority:** medium
- **Summary:** Agent runtime module with 2 classes and 5 top-level functions.
- **Key Elements:** BoxMode, Boxes, pairwise_intersection, pairwise_iou, pairwise_ioa, pairwise_point_box_distance, matched_pairwise_iou
- **Dependencies:** No internal dependencies resolved

### sam3/agent/helpers/color_map.py

- **Type:** source
- **Role:** agent-runtime
- **Priority:** medium
- **Summary:** Agent runtime module with 0 classes and 3 top-level functions.
- **Key Elements:** colormap, random_color, random_colors
- **Dependencies:** No internal dependencies resolved

### sam3/agent/helpers/keypoints.py

- **Type:** source
- **Role:** agent-runtime
- **Priority:** medium
- **Summary:** Agent runtime module with 1 classes and 2 top-level functions.
- **Key Elements:** Keypoints, _keypoints_to_heatmap, heatmaps_to_keypoints
- **Dependencies:** No internal dependencies resolved

### sam3/agent/helpers/mask_overlap_removal.py

- **Type:** source
- **Role:** agent-runtime
- **Priority:** medium
- **Summary:** Agent runtime module with 0 classes and 5 top-level functions.
- **Key Elements:** mask_intersection, mask_iom, _decode_single_mask, _decode_masks_to_torch_bool, remove_overlapping_masks
- **Dependencies:** No internal dependencies resolved

### sam3/agent/helpers/masks.py

- **Type:** source
- **Role:** agent-runtime
- **Priority:** medium
- **Summary:** Agent runtime module with 3 classes and 3 top-level functions.
- **Key Elements:** polygon_area, polygons_to_bitmask, rasterize_polygons_within_box, BitMasks, PolygonMasks, ROIMasks
- **Dependencies:** `sam3/agent/helpers/boxes.py`, `sam3/agent/helpers/memory.py`, `sam3/agent/helpers/roi_align.py`

### sam3/agent/helpers/memory.py

- **Type:** source
- **Role:** agent-runtime
- **Priority:** medium
- **Summary:** Agent runtime module with 0 classes and 2 top-level functions.
- **Key Elements:** _ignore_torch_cuda_oom, retry_if_cuda_oom
- **Dependencies:** No internal dependencies resolved

### sam3/agent/helpers/rle.py

- **Type:** source
- **Role:** agent-runtime
- **Priority:** medium
- **Summary:** Agent runtime module with 0 classes and 3 top-level functions.
- **Key Elements:** rle_encode, robust_rle_encode, ann_to_rle
- **Dependencies:** No internal dependencies resolved

### sam3/agent/helpers/roi_align.py

- **Type:** source
- **Role:** agent-runtime
- **Priority:** medium
- **Summary:** Agent runtime module with 1 classes and 0 top-level functions.
- **Key Elements:** ROIAlign
- **Dependencies:** No internal dependencies resolved

### sam3/agent/helpers/rotated_boxes.py

- **Type:** source
- **Role:** agent-runtime
- **Priority:** medium
- **Summary:** Agent runtime module with 1 classes and 2 top-level functions.
- **Key Elements:** pairwise_iou_rotated, RotatedBoxes, pairwise_iou
- **Dependencies:** `sam3/agent/helpers/boxes.py`

### sam3/agent/helpers/som_utils.py

- **Type:** source
- **Role:** agent-runtime
- **Priority:** medium
- **Summary:** Agent runtime module with 2 classes and 6 top-level functions.
- **Key Elements:** rgb_to_hex, _validate_color_hex, Color, ColorPalette, draw_box, draw_text, draw_mask, _change_color_brightness
- **Dependencies:** No internal dependencies resolved

### sam3/agent/helpers/zoom_in.py

- **Type:** source
- **Role:** agent-runtime
- **Priority:** medium
- **Summary:** Agent runtime module with 0 classes and 1 top-level functions.
- **Key Elements:** render_zoom_in
- **Dependencies:** `sam3/agent/helpers/som_utils.py`

### sam3/agent/inference.py

- **Type:** source
- **Role:** agent-runtime
- **Priority:** medium
- **Summary:** Agent runtime module with 0 classes and 1 top-level functions.
- **Key Elements:** run_single_image_inference
- **Dependencies:** `sam3/agent/agent_core.py`

### sam3/agent/viz.py

- **Type:** source
- **Role:** agent-runtime
- **Priority:** medium
- **Summary:** Agent runtime module with 0 classes and 1 top-level functions.
- **Key Elements:** visualize
- **Dependencies:** `sam3/agent/helpers/zoom_in.py`

### sam3/model/act_ckpt_utils.py

- **Type:** source
- **Role:** model-support
- **Priority:** medium
- **Summary:** Model support module with 0 classes and 2 top-level functions.
- **Key Elements:** activation_ckpt_wrapper, clone_output_wrapper
- **Dependencies:** No internal dependencies resolved

### sam3/model/box_ops.py

- **Type:** source
- **Role:** model-support
- **Priority:** medium
- **Summary:** Model support module with 0 classes and 13 top-level functions.
- **Key Elements:** box_cxcywh_to_xyxy, box_cxcywh_to_xywh, box_xywh_to_xyxy, box_xywh_to_cxcywh, box_xyxy_to_xywh, box_xyxy_to_cxcywh, box_area, masks_to_boxes
- **Dependencies:** No internal dependencies resolved

### sam3/model/data_misc.py

- **Type:** source
- **Role:** model-support
- **Priority:** medium
- **Summary:** Model support module with 6 classes and 2 top-level functions.
- **Key Elements:** NestedTensor, interpolate, BatchedPointer, FindStage, BatchedFindTarget, BatchedInferenceMetadata, BatchedDatapoint, convert_my_tensors
- **Dependencies:** No internal dependencies resolved

### sam3/model/edt.py

- **Type:** source
- **Role:** model-support
- **Priority:** medium
- **Summary:** Model support module with 0 classes and 2 top-level functions.
- **Key Elements:** edt_kernel, edt_triton
- **Dependencies:** No internal dependencies resolved

### sam3/model/encoder.py

- **Type:** source
- **Role:** model-component
- **Priority:** medium
- **Summary:** Model component module with 3 classes and 1 top-level functions.
- **Key Elements:** TransformerEncoderLayer, TransformerEncoder, TransformerEncoderFusion, pool_text_feat
- **Dependencies:** `sam3/model/act_ckpt_utils.py`, `sam3/model/model_misc.py`

### sam3/model/geometry_encoders.py

- **Type:** source
- **Role:** model-component
- **Priority:** medium
- **Summary:** Model component module with 4 classes and 2 top-level functions.
- **Key Elements:** is_right_padded, concat_padded_sequences, Prompt, MaskEncoder, FusedMaskEncoder, SequenceGeometryEncoder
- **Dependencies:** `sam3/model/act_ckpt_utils.py`, `sam3/model/box_ops.py`, `sam3/model/model_misc.py`

### sam3/model/io_utils.py

- **Type:** source
- **Role:** model-support
- **Priority:** medium
- **Summary:** Model support module with 4 classes and 8 top-level functions.
- **Key Elements:** load_resource_as_video_frames, load_image_as_single_frame_video, load_video_frames, load_video_frames_from_image_folder, load_video_frames_from_video_file, load_video_frames_from_video_file_using_cv2, load_dummy_video, _load_img_as_tensor
- **Dependencies:** `sam3/logger.py`

### sam3/model/maskformer_segmentation.py

- **Type:** source
- **Role:** model-support
- **Priority:** medium
- **Summary:** Model support module with 5 classes and 0 top-level functions.
- **Key Elements:** LinearPresenceHead, MaskPredictor, SegmentationHead, PixelDecoder, UniversalSegmentationHead
- **Dependencies:** `sam3/model/model_misc.py`

### sam3/model/memory.py

- **Type:** source
- **Role:** model-support
- **Priority:** medium
- **Summary:** Model support module with 4 classes and 0 top-level functions.
- **Key Elements:** SimpleMaskDownSampler, CXBlock, SimpleFuser, SimpleMaskEncoder
- **Dependencies:** `sam3/model/model_misc.py`

### sam3/model/model_misc.py

- **Type:** source
- **Role:** model-support
- **Priority:** medium
- **Summary:** Model support module with 8 classes and 9 top-level functions.
- **Key Elements:** inverse_sigmoid, get_sdpa_settings, AttentionType, multi_head_attention_forward, MultiheadAttention, DotProductScoring, LayerScale, LayerNorm2d
- **Dependencies:** No internal dependencies resolved

### sam3/model/multiplex_mask_decoder.py

- **Type:** source
- **Role:** model-component
- **Priority:** medium
- **Summary:** Model component module with 2 classes and 0 top-level functions.
- **Key Elements:** MultiplexMaskDecoder, MLP
- **Dependencies:** `sam3/sam/common.py`

### sam3/model/multiplex_utils.py

- **Type:** source
- **Role:** model-support
- **Priority:** medium
- **Summary:** Model support module with 2 classes and 0 top-level functions.
- **Key Elements:** MultiplexState, MultiplexController
- **Dependencies:** No internal dependencies resolved

### sam3/model/necks.py

- **Type:** source
- **Role:** model-component
- **Priority:** medium
- **Summary:** Model component module with 2 classes and 0 top-level functions.
- **Key Elements:** Sam3DualViTDetNeck, Sam3TriViTDetNeck
- **Dependencies:** `sam3/model/data_misc.py`

### sam3/model/position_encoding.py

- **Type:** source
- **Role:** model-support
- **Priority:** medium
- **Summary:** Model support module with 1 classes and 0 top-level functions.
- **Key Elements:** PositionEmbeddingSine
- **Dependencies:** No internal dependencies resolved

### sam3/model/sam1_task_predictor.py

- **Type:** source
- **Role:** predictor
- **Priority:** medium
- **Summary:** Predictor module with 1 classes and 0 top-level functions.
- **Key Elements:** SAM3InteractiveImagePredictor
- **Dependencies:** `sam3/model/utils/sam1_utils.py`

### sam3/model/sam3_multiplex_detector.py

- **Type:** source
- **Role:** model-support
- **Priority:** medium
- **Summary:** Model support module with 2 classes and 0 top-level functions.
- **Key Elements:** Sam3MultiplexImageBase, Sam3MultiplexDetector
- **Dependencies:** `sam3/model/data_misc.py`, `sam3/model/geometry_encoders.py`, `sam3/model/model_misc.py`, `sam3/model/sam3_image.py`, `sam3/model/sam3_multiplex_detector_utils.py`, `sam3/model/vl_combiner.py`

### sam3/model/sam3_multiplex_detector_utils.py

- **Type:** source
- **Role:** model-support
- **Priority:** medium
- **Summary:** Model support module with 0 classes and 11 top-level functions.
- **Key Elements:** nms_masks, _nms_masks_core, _nms_masks_core_batched, _batched_mask_iou, _batched_mask_iom, _batched_generic_nms_mask, _nms_masks_core_single, generic_nms_cpu
- **Dependencies:** `sam3/__init__.py`

### sam3/model/sam3_tracker_utils.py

- **Type:** source
- **Role:** model-support
- **Priority:** medium
- **Summary:** Model support module with 0 classes and 11 top-level functions.
- **Key Elements:** sample_box_points, mask_to_box, sample_random_points_from_errors, sample_one_point_from_error_center, sample_one_point_from_error_center_slow, get_next_point, select_closest_cond_frames, get_1d_sine_pe
- **Dependencies:** `sam3/model/edt.py`

### sam3/model/text_encoder_ve.py

- **Type:** source
- **Role:** model-component
- **Priority:** medium
- **Summary:** Model component module with 4 classes and 1 top-level functions.
- **Key Elements:** ResidualAttentionBlock, Transformer, text_global_pool, TextTransformer, VETextEncoder
- **Dependencies:** `sam3/model/model_misc.py`

### sam3/model/tokenizer_ve.py

- **Type:** source
- **Role:** model-support
- **Priority:** medium
- **Summary:** Model support module with 1 classes and 9 top-level functions.
- **Key Elements:** bytes_to_unicode, get_pairs, basic_clean, whitespace_clean, _clean_canonicalize, _clean_lower, _clean_whitespace, get_clean_fn
- **Dependencies:** No internal dependencies resolved

### sam3/model/utils/misc.py

- **Type:** source
- **Role:** model-support
- **Priority:** medium
- **Summary:** Model support module with 1 classes and 2 top-level functions.
- **Key Elements:** _is_named_tuple, _CopyableData, copy_data_to_device
- **Dependencies:** No internal dependencies resolved

### sam3/model/utils/sam1_utils.py

- **Type:** source
- **Role:** model-support
- **Priority:** medium
- **Summary:** Model support module with 1 classes and 0 top-level functions.
- **Key Elements:** SAM2Transforms
- **Dependencies:** No internal dependencies resolved

### sam3/model/utils/sam2_utils.py

- **Type:** source
- **Role:** model-support
- **Priority:** medium
- **Summary:** Model support module with 1 classes and 4 top-level functions.
- **Key Elements:** _load_img_as_tensor, AsyncVideoFrameLoader, load_video_frames, load_video_frames_from_jpg_images, load_video_frames_from_video_file
- **Dependencies:** No internal dependencies resolved

### sam3/model/vitdet.py

- **Type:** source
- **Role:** model-support
- **Priority:** medium
- **Summary:** Model support module with 5 classes and 9 top-level functions.
- **Key Elements:** Mlp, init_t_xy, compute_axial_cis, reshape_for_broadcast, apply_rotary_enc, window_partition, window_unpartition, get_rel_pos
- **Dependencies:** `sam3/model/data_misc.py`, `sam3/model/model_misc.py`, `sam3/sam/rope.py`

### sam3/model/vl_combiner.py

- **Type:** source
- **Role:** model-component
- **Priority:** medium
- **Summary:** Model component module with 4 classes and 0 top-level functions.
- **Key Elements:** SAM3VLBackbone, SAM3VLBackboneTri, VisionOnly, TriHeadVisionOnly
- **Dependencies:** `sam3/model/act_ckpt_utils.py`, `sam3/model/data_misc.py`, `sam3/model/necks.py`

### sam3/sam/common.py

- **Type:** source
- **Role:** sam-core-component
- **Priority:** medium
- **Summary:** Sam core component module with 2 classes and 0 top-level functions.
- **Key Elements:** MLPBlock, LayerNorm2d
- **Dependencies:** No internal dependencies resolved

### sam3/sam/mask_decoder.py

- **Type:** source
- **Role:** sam-core-component
- **Priority:** medium
- **Summary:** Sam core component module with 2 classes and 0 top-level functions.
- **Key Elements:** MaskDecoder, MLP
- **Dependencies:** `sam3/sam/common.py`

### sam3/sam/prompt_encoder.py

- **Type:** source
- **Role:** sam-core-component
- **Priority:** medium
- **Summary:** Sam core component module with 2 classes and 0 top-level functions.
- **Key Elements:** PromptEncoder, PositionEmbeddingRandom
- **Dependencies:** `sam3/sam/common.py`

### sam3/sam/rope.py

- **Type:** source
- **Role:** sam-core-component
- **Priority:** medium
- **Summary:** Sam core component module with 1 classes and 8 top-level functions.
- **Key Elements:** init_t_xy, compute_axial_cis, reshape_for_broadcast, apply_rotary_enc, complex_mult, apply_rotary_enc_real, broadcat, rotate_half
- **Dependencies:** No internal dependencies resolved

### sam3/sam/transformer.py

- **Type:** source
- **Role:** sam-core-component
- **Priority:** medium
- **Summary:** Sam core component module with 4 classes and 0 top-level functions.
- **Key Elements:** TwoWayTransformer, TwoWayAttentionBlock, Attention, RoPEAttention
- **Dependencies:** `sam3/sam/common.py`, `sam3/sam/rope.py`

### scripts/eval/gold/eval_sam3.py

- **Type:** source
- **Role:** evaluation-script
- **Priority:** medium
- **Summary:** Evaluation script module with 0 classes and 1 top-level functions.
- **Key Elements:** main
- **Dependencies:** No internal dependencies resolved

### scripts/eval/standalone_cgf1.py

- **Type:** source
- **Role:** evaluation-script
- **Priority:** medium
- **Summary:** Evaluation script module with 0 classes and 1 top-level functions.
- **Key Elements:** main
- **Dependencies:** No internal dependencies resolved

### scripts/eval/veval/README.md

- **Type:** documentation
- **Role:** evaluation-script
- **Priority:** medium
- **Summary:** Evaluation script module with 0 classes and 0 top-level functions.
- **Key Elements:** SA-Co/VEval Dataset, Environment, Download, The expected folder structure, Download ready-to-use data, Download via preprocessing steps, Download annotations, Download videos or frames
- **Dependencies:** No internal dependencies resolved

### scripts/eval/veval/saco_yt1b_annot_update.py

- **Type:** source
- **Role:** evaluation-script
- **Priority:** medium
- **Summary:** Evaluation script module with 0 classes and 4 top-level functions.
- **Key Elements:** get_available_saco_yt1b_ids, update_yt1b_annot_per_field, update_yt1b_annot, main
- **Dependencies:** No internal dependencies resolved

### scripts/eval/veval/saco_yt1b_downloader.py

- **Type:** source
- **Role:** evaluation-script
- **Priority:** medium
- **Summary:** Evaluation script module with 0 classes and 2 top-level functions.
- **Key Elements:** download_and_extract_frames, main
- **Dependencies:** No internal dependencies resolved

### scripts/eval/veval/saco_yt1b_frame_prep_util.py

- **Type:** source
- **Role:** evaluation-script
- **Priority:** medium
- **Summary:** Evaluation script module with 0 classes and 0 top-level functions.
- **Key Elements:** None extracted
- **Dependencies:** No internal dependencies resolved

## Relationships

- `sam3/agent/agent_core.py` -> `sam3/agent/client_llm.py`
- `sam3/agent/agent_core.py` -> `sam3/agent/client_sam3.py`
- `sam3/agent/agent_core.py` -> `sam3/agent/viz.py`
- `sam3/agent/client_sam3.py` -> `sam3/agent/helpers/mask_overlap_removal.py`
- `sam3/agent/client_sam3.py` -> `sam3/agent/viz.py`
- `sam3/agent/client_sam3.py` -> `sam3/model/box_ops.py`
- `sam3/agent/helpers/masks.py` -> `sam3/agent/helpers/boxes.py`
- `sam3/agent/helpers/masks.py` -> `sam3/agent/helpers/memory.py`
- `sam3/agent/helpers/masks.py` -> `sam3/agent/helpers/roi_align.py`
- `sam3/agent/helpers/rotated_boxes.py` -> `sam3/agent/helpers/boxes.py`
- `sam3/agent/helpers/zoom_in.py` -> `sam3/agent/helpers/som_utils.py`
- `sam3/agent/inference.py` -> `sam3/agent/agent_core.py`
- `sam3/agent/viz.py` -> `sam3/agent/helpers/zoom_in.py`
- `sam3/model/encoder.py` -> `sam3/model/act_ckpt_utils.py`
- `sam3/model/encoder.py` -> `sam3/model/model_misc.py`
- `sam3/model/geometry_encoders.py` -> `sam3/model/act_ckpt_utils.py`
- `sam3/model/geometry_encoders.py` -> `sam3/model/box_ops.py`
- `sam3/model/geometry_encoders.py` -> `sam3/model/model_misc.py`
- `sam3/model/io_utils.py` -> `sam3/logger.py`
- `sam3/model/maskformer_segmentation.py` -> `sam3/model/model_misc.py`
- `sam3/model/memory.py` -> `sam3/model/model_misc.py`
- `sam3/model/multiplex_mask_decoder.py` -> `sam3/sam/common.py`
- `sam3/model/necks.py` -> `sam3/model/data_misc.py`
- `sam3/model/sam1_task_predictor.py` -> `sam3/model/utils/sam1_utils.py`
- `sam3/model/sam3_base_predictor.py` -> `sam3/logger.py`
- `sam3/model/sam3_image.py` -> `sam3/model/act_ckpt_utils.py`
- `sam3/model/sam3_image.py` -> `sam3/model/box_ops.py`
- `sam3/model/sam3_image.py` -> `sam3/model/data_misc.py`
- `sam3/model/sam3_image.py` -> `sam3/model/geometry_encoders.py`
- `sam3/model/sam3_image.py` -> `sam3/model/model_misc.py`
- `sam3/model/sam3_image.py` -> `sam3/model/sam1_task_predictor.py`
- `sam3/model/sam3_image.py` -> `sam3/model/vl_combiner.py`
- `sam3/model/sam3_image_processor.py` -> `sam3/model/__init__.py`
- `sam3/model/sam3_image_processor.py` -> `sam3/model/box_ops.py`
- `sam3/model/sam3_image_processor.py` -> `sam3/model/data_misc.py`
- `sam3/model/sam3_multiplex_detector.py` -> `sam3/model/data_misc.py`
- `sam3/model/sam3_multiplex_detector.py` -> `sam3/model/geometry_encoders.py`
- `sam3/model/sam3_multiplex_detector.py` -> `sam3/model/model_misc.py`
- `sam3/model/sam3_multiplex_detector.py` -> `sam3/model/sam3_image.py`
- `sam3/model/sam3_multiplex_detector.py` -> `sam3/model/sam3_multiplex_detector_utils.py`
- `sam3/model/sam3_multiplex_detector.py` -> `sam3/model/vl_combiner.py`
- `sam3/model/sam3_multiplex_detector_utils.py` -> `sam3/__init__.py`
- `sam3/model/sam3_multiplex_video_predictor.py` -> `sam3/logger.py`
- `sam3/model/sam3_multiplex_video_predictor.py` -> `sam3/model/sam3_base_predictor.py`
- `sam3/model/sam3_tracker_utils.py` -> `sam3/model/edt.py`
- `sam3/model/sam3_video_predictor.py` -> `sam3/logger.py`
- `sam3/model/sam3_video_predictor.py` -> `sam3/model/sam3_base_predictor.py`
- `sam3/model/text_encoder_ve.py` -> `sam3/model/model_misc.py`
- `sam3/model/vitdet.py` -> `sam3/model/data_misc.py`
- `sam3/model/vitdet.py` -> `sam3/model/model_misc.py`
- `sam3/model/vitdet.py` -> `sam3/sam/rope.py`
- `sam3/model/vl_combiner.py` -> `sam3/model/act_ckpt_utils.py`
- `sam3/model/vl_combiner.py` -> `sam3/model/data_misc.py`
- `sam3/model/vl_combiner.py` -> `sam3/model/necks.py`
- `sam3/model_builder.py` -> `sam3/model/encoder.py`
- `sam3/model_builder.py` -> `sam3/model/geometry_encoders.py`
- `sam3/model_builder.py` -> `sam3/model/maskformer_segmentation.py`
- `sam3/model_builder.py` -> `sam3/model/memory.py`
- `sam3/model_builder.py` -> `sam3/model/model_misc.py`
- `sam3/model_builder.py` -> `sam3/model/multiplex_utils.py`
- `sam3/model_builder.py` -> `sam3/model/necks.py`
- `sam3/model_builder.py` -> `sam3/model/position_encoding.py`
- `sam3/model_builder.py` -> `sam3/model/sam1_task_predictor.py`
- `sam3/model_builder.py` -> `sam3/model/sam3_image.py`
- `sam3/model_builder.py` -> `sam3/model/sam3_video_predictor.py`
- `sam3/model_builder.py` -> `sam3/model/text_encoder_ve.py`
- `sam3/model_builder.py` -> `sam3/model/tokenizer_ve.py`
- `sam3/model_builder.py` -> `sam3/model/vitdet.py`
- `sam3/model_builder.py` -> `sam3/model/vl_combiner.py`
- `sam3/model_builder.py` -> `sam3/sam/transformer.py`
- `sam3/sam/mask_decoder.py` -> `sam3/sam/common.py`
- `sam3/sam/prompt_encoder.py` -> `sam3/sam/common.py`
- `sam3/sam/transformer.py` -> `sam3/sam/common.py`
- `sam3/sam/transformer.py` -> `sam3/sam/rope.py`

## Key Observations

- `sam3/model_builder.py` is the assembly hub for the repository's model variants.
- Image inference is exposed through a processor-style API, while video inference uses session/request semantics.
- The codebase separates core SAM blocks (`sam3/sam`) from higher-level SAM 3 orchestration (`sam3/model`).
- An additional `sam3/agent` layer integrates multimodal LLM reasoning with SAM 3 segmentation calls.
- Examples and evaluation scripts are included directly in the snapshot, which makes the repo documentation-heavy and workflow-oriented.

## Unknowns / Issues

- Some internal imports do not resolve within the extracted markdown snapshot, which suggests missing files or stale references: sam3/__init__.py -> .model_builder:build_sam3_image_model,build_sam3_predictor, sam3/agent/client_sam3.py -> sam3.train.masks_ops:rle_encode, sam3/agent/viz.py -> .helpers.visualizer:Visualizer, sam3/model/sam1_task_predictor.py -> sam3.model.sam3_tracker_base:Sam3TrackerBase, sam3/model/sam3_image.py -> sam3.perflib.nms:nms_masks, sam3/model/sam3_image.py -> sam3.train.data.collator:BatchedDatapoint, sam3/model/sam3_multiplex_detector_utils.py -> sam3.perflib.masks_ops:mask_iou, sam3/model/sam3_multiplex_detector_utils.py -> sam3.train.masks_ops:mask_iom ...
- No Dockerfile was detected in the provided markdown snapshot.
- No `.env` file was detected in the provided markdown snapshot.

## Summary

This repository appears to package Meta's SAM 3 segmentation stack as a Python library with image, video, multiplex, and agent-driven workflows. The structure centers on a model factory, core architecture modules, predictor runtimes, and example/evaluation material for demonstration and benchmarking.
