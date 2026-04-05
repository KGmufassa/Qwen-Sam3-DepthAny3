# File Tree Extraction Plan: facebookresearch-sam3

## Overview
- Project Type: python_computer_vision_ml_library
- Goal: understand how the app works and assess integration into another app or multiple apps
- Total Items: 217
- Included: 81
- Excluded: 136

---

## Included Paths
- MANIFEST.in
- README.md
- examples/saco_gold_silver_vis_example.ipynb
- examples/saco_veval_eval_example.ipynb
- examples/saco_veval_vis_example.ipynb
- examples/sam3.1_video_predictor_example.ipynb
- examples/sam3_agent.ipynb
- examples/sam3_for_sam1_task_example.ipynb
- examples/sam3_for_sam2_video_task_example.ipynb
- examples/sam3_image_interactive.ipynb
- pyproject.toml
- sam3/__init__.py
- sam3/agent/__init__.py
- sam3/agent/agent_core.py
- sam3/agent/client_llm.py
- sam3/agent/client_sam3.py
- sam3/agent/helpers/__init__.py
- sam3/agent/helpers/boxes.py
- sam3/agent/helpers/color_map.py
- sam3/agent/helpers/keypoints.py
- sam3/agent/helpers/mask_overlap_removal.py
- sam3/agent/helpers/masks.py
- sam3/agent/helpers/memory.py
- sam3/agent/helpers/rle.py
- sam3/agent/helpers/roi_align.py
- sam3/agent/helpers/rotated_boxes.py
- sam3/agent/helpers/som_utils.py
- sam3/agent/helpers/zoom_in.py
- sam3/agent/inference.py
- sam3/agent/system_prompts/system_prompt_iterative_checking.txt
- sam3/agent/viz.py
- sam3/logger.py
- sam3/model/__init__.py
- sam3/model/act_ckpt_utils.py
- sam3/model/box_ops.py
- sam3/model/data_misc.py
- sam3/model/edt.py
- sam3/model/encoder.py
- sam3/model/geometry_encoders.py
- sam3/model/io_utils.py
- sam3/model/maskformer_segmentation.py
- sam3/model/memory.py
- sam3/model/model_misc.py
- sam3/model/multiplex_mask_decoder.py
- sam3/model/multiplex_utils.py
- sam3/model/necks.py
- sam3/model/position_encoding.py
- sam3/model/sam1_task_predictor.py
- sam3/model/sam3_base_predictor.py
- sam3/model/sam3_image.py
- sam3/model/sam3_image_processor.py
- sam3/model/sam3_multiplex_detector.py
- sam3/model/sam3_multiplex_detector_utils.py
- sam3/model/sam3_multiplex_video_predictor.py
- sam3/model/sam3_tracker_utils.py
- sam3/model/sam3_video_predictor.py
- sam3/model/text_encoder_ve.py
- sam3/model/tokenizer_ve.py
- sam3/model/utils/__init__.py
- sam3/model/utils/misc.py
- sam3/model/utils/sam1_utils.py
- sam3/model/utils/sam2_utils.py
- sam3/model/vitdet.py
- sam3/model/vl_combiner.py
- sam3/model_builder.py
- sam3/sam/__init__.py
- sam3/sam/common.py
- sam3/sam/mask_decoder.py
- sam3/sam/prompt_encoder.py
- sam3/sam/rope.py
- sam3/sam/transformer.py
- sam3/visualization_utils.py
- scripts/eval/gold/eval_sam3.py
- scripts/eval/standalone_cgf1.py
- scripts/eval/veval/README.md
- scripts/eval/veval/__init__.py
- scripts/eval/veval/saco_yt1b_annot_update.py
- scripts/eval/veval/saco_yt1b_downloader.py
- scripts/eval/veval/saco_yt1b_frame_prep_util.py
- scripts/measure_speed.py
- scripts/qualitative_test.py

---

## Excluded Paths (Detailed)
- .github/workflows/format.yml
- CODE_OF_CONDUCT.md
- CONTRIBUTING.md
- LICENSE
- README_TRAIN.md
- RELEASE_SAM3p1.md
- assets/veval/toy_gt_and_pred/toy_saco_veval_sav_test_eval_res.json
- sam3/eval/__init__.py
- sam3/eval/cgf1_eval.py
- sam3/eval/coco_eval.py
- sam3/eval/coco_eval_offline.py
- sam3/eval/coco_reindex.py
- sam3/eval/coco_writer.py
- sam3/eval/conversion_util.py
- sam3/eval/demo_eval.py
- sam3/eval/hota_eval_toolkit/__init__.py
- sam3/eval/hota_eval_toolkit/run_ytvis_eval.py
- sam3/eval/hota_eval_toolkit/trackeval/__init__.py
- sam3/eval/hota_eval_toolkit/trackeval/_timing.py
- sam3/eval/hota_eval_toolkit/trackeval/datasets/__init__.py
- sam3/eval/hota_eval_toolkit/trackeval/datasets/_base_dataset.py
- sam3/eval/hota_eval_toolkit/trackeval/datasets/tao_ow.py
- sam3/eval/hota_eval_toolkit/trackeval/datasets/youtube_vis.py
- sam3/eval/hota_eval_toolkit/trackeval/eval.py
- sam3/eval/hota_eval_toolkit/trackeval/metrics/__init__.py
- sam3/eval/hota_eval_toolkit/trackeval/metrics/_base_metric.py
- sam3/eval/hota_eval_toolkit/trackeval/metrics/count.py
- sam3/eval/hota_eval_toolkit/trackeval/metrics/hota.py
- sam3/eval/hota_eval_toolkit/trackeval/utils.py
- sam3/eval/postprocessors.py
- sam3/eval/saco_veval_eval.py
- sam3/eval/saco_veval_evaluators.py
- sam3/eval/teta_eval_toolkit/__init__.py
- sam3/eval/teta_eval_toolkit/_timing.py
- sam3/eval/teta_eval_toolkit/config.py
- sam3/eval/teta_eval_toolkit/datasets/__init__.py
- sam3/eval/teta_eval_toolkit/datasets/_base_dataset.py
- sam3/eval/teta_eval_toolkit/datasets/coco.py
- sam3/eval/teta_eval_toolkit/datasets/tao.py
- sam3/eval/teta_eval_toolkit/eval.py
- sam3/eval/teta_eval_toolkit/metrics/__init__.py
- sam3/eval/teta_eval_toolkit/metrics/_base_metric.py
- sam3/eval/teta_eval_toolkit/metrics/teta.py
- sam3/eval/teta_eval_toolkit/utils.py
- sam3/eval/ytvis_coco_wrapper.py
- sam3/eval/ytvis_eval.py
- sam3/perflib/__init__.py
- sam3/perflib/associate_det_trk.py
- sam3/perflib/compile.py
- sam3/perflib/connected_components.py
- sam3/perflib/fa3.py
- sam3/perflib/fused.py
- sam3/perflib/iou.py
- sam3/perflib/masks_ops.py
- sam3/perflib/nms.py
- sam3/perflib/tests/tests.py
- sam3/perflib/triton/connected_components.py
- sam3/perflib/triton/nms.py
- sam3/train/__init__.py
- sam3/train/configs/eval_base.yaml
- sam3/train/configs/gold_image_evals/sam3_gold_image_attributes.yaml
- sam3/train/configs/gold_image_evals/sam3_gold_image_crowded.yaml
- sam3/train/configs/gold_image_evals/sam3_gold_image_fg_food.yaml
- sam3/train/configs/gold_image_evals/sam3_gold_image_fg_sports.yaml
- sam3/train/configs/gold_image_evals/sam3_gold_image_metaclip_nps.yaml
- sam3/train/configs/gold_image_evals/sam3_gold_image_sa1b_nps.yaml
- sam3/train/configs/gold_image_evals/sam3_gold_image_wiki_common.yaml
- sam3/train/configs/odinw13/odinw_text_and_visual.yaml
- sam3/train/configs/odinw13/odinw_text_only.yaml
- sam3/train/configs/odinw13/odinw_text_only_positive.yaml
- sam3/train/configs/odinw13/odinw_text_only_train.yaml
- sam3/train/configs/odinw13/odinw_visual_only.yaml
- sam3/train/configs/roboflow_v100/roboflow_v100_eval.yaml
- sam3/train/configs/roboflow_v100/roboflow_v100_full_ft_100_images.yaml
- sam3/train/configs/saco_video_evals/saco_veval_sav_test.yaml
- sam3/train/configs/saco_video_evals/saco_veval_sav_test_noheur.yaml
- sam3/train/configs/saco_video_evals/saco_veval_sav_val.yaml
- sam3/train/configs/saco_video_evals/saco_veval_sav_val_noheur.yaml
- sam3/train/configs/saco_video_evals/saco_veval_smartglasses_test.yaml
- sam3/train/configs/saco_video_evals/saco_veval_smartglasses_test_noheur.yaml
- sam3/train/configs/saco_video_evals/saco_veval_smartglasses_val.yaml
- sam3/train/configs/saco_video_evals/saco_veval_smartglasses_val_noheur.yaml
- sam3/train/configs/saco_video_evals/saco_veval_yt1b_test.yaml
- sam3/train/configs/saco_video_evals/saco_veval_yt1b_test_noheur.yaml
- sam3/train/configs/saco_video_evals/saco_veval_yt1b_val.yaml
- sam3/train/configs/saco_video_evals/saco_veval_yt1b_val_noheur.yaml
- sam3/train/configs/silver_image_evals/sam3_silver_image_bdd100k.yaml
- sam3/train/configs/silver_image_evals/sam3_silver_image_droid.yaml
- sam3/train/configs/silver_image_evals/sam3_silver_image_ego4d.yaml
- sam3/train/configs/silver_image_evals/sam3_silver_image_fathomnet.yaml
- sam3/train/configs/silver_image_evals/sam3_silver_image_food_rec.yaml
- sam3/train/configs/silver_image_evals/sam3_silver_image_geode.yaml
- sam3/train/configs/silver_image_evals/sam3_silver_image_inaturalist.yaml
- sam3/train/configs/silver_image_evals/sam3_silver_image_nga.yaml
- sam3/train/configs/silver_image_evals/sam3_silver_image_sav.yaml
- sam3/train/configs/silver_image_evals/sam3_silver_image_yt1b.yaml
- sam3/train/data/__init__.py
- sam3/train/data/coco_json_loaders.py
- sam3/train/data/collator.py
- sam3/train/data/sam3_image_dataset.py
- sam3/train/data/sam3_video_dataset.py
- sam3/train/data/torch_dataset.py
- sam3/train/loss/__init__.py
- sam3/train/loss/mask_sampling.py
- sam3/train/loss/sam3_loss.py
- sam3/train/loss/sigmoid_focal_loss.py
- sam3/train/masks_ops.py
- sam3/train/matcher.py
- sam3/train/nms_helper.py
- sam3/train/optim/__init__.py
- sam3/train/optim/optimizer.py
- sam3/train/optim/schedulers.py
- sam3/train/train.py
- sam3/train/trainer.py
- sam3/train/transforms/__init__.py
- sam3/train/transforms/basic.py
- sam3/train/transforms/filter_query_transforms.py
- sam3/train/transforms/point_sampling.py
- sam3/train/transforms/segmentation.py
- sam3/train/utils/__init__.py
- sam3/train/utils/checkpoint_utils.py
- sam3/train/utils/distributed.py
- sam3/train/utils/logger.py
- sam3/train/utils/train_utils.py
- scripts/eval/gold/README.md
- scripts/eval/silver/CONFIG_FRAMES.yaml
- scripts/eval/silver/README.md
- scripts/eval/silver/download_fathomnet.py
- scripts/eval/silver/download_inaturalist.py
- scripts/eval/silver/download_preprocess_nga.py
- scripts/eval/silver/download_videos.py
- scripts/eval/silver/extract_frames.py
- scripts/eval/silver/preprocess_silver_geode_bdd100k_food_rec.py
- scripts/eval/silver/utils.py
- scripts/extract_odinw_results.py
- scripts/extract_roboflow_vl100_results.py

---

## Simplified Exclusion List (KEY SECTION)

```text
.github, assets, sam3/eval, sam3/perflib, sam3/train, scripts/eval/silver, CODE_OF_CONDUCT.md, CONTRIBUTING.md, LICENSE, README_TRAIN.md, RELEASE_SAM3p1.md, scripts/eval/gold/README.md, scripts/extract_odinw_results.py, scripts/extract_roboflow_vl100_results.py
```
id="simple-exclude-list"

---

## Representative Selections
- README.md
- pyproject.toml
- sam3/model_builder.py
- sam3/model/sam3_base_predictor.py
- sam3/model/sam3_image.py
- sam3/model/sam3_video_predictor.py
- sam3/model/sam3_image_processor.py
- sam3/sam/prompt_encoder.py
- sam3/sam/mask_decoder.py
- sam3/sam/transformer.py
- sam3/agent/agent_core.py
- sam3/agent/client_sam3.py
- examples/sam3_image_interactive.ipynb
- examples/sam3.1_video_predictor_example.ipynb
- scripts/qualitative_test.py

---

## Patterns Detected
- Python package layout centered on the `sam3/` module
- Inference-oriented predictor files in `sam3/model/`
- Core segmentation transformer components in `sam3/sam/`
- App-like orchestration layer in `sam3/agent/`
- Notebook examples showing usage flows in `examples/`
- Training and benchmark material separated into `sam3/train/` and `sam3/eval/`
- Operational scripts grouped under `scripts/`

---

## Selection Rules Applied
- Include packaging and top-level entry metadata needed to frame installation and execution.
- Include core inference and architecture paths under `sam3/model/`, `sam3/sam/`, and `sam3/agent/`.
- Include notebooks and a narrow script subset that demonstrate integration and runtime usage.
- Exclude training, broad evaluation, CI, policy, release, and asset-heavy paths that are not required for initial integration analysis.
- Collapse simplified exclusions only when an entire directory is excluded.

---

## Reasoning
- The goal is not full repository comprehension; it is understanding runtime behavior and possible integration points.
- Predictor, builder, prompt, decoder, and agent files are most useful for mapping how another app would call into this project.
- Examples and selected scripts are retained because they likely show request shape, initialization, and output handling patterns.

---

## Key Observations
- `sam3/model_builder.py` is a probable integration choke point for model construction.
- `sam3/model/` appears to contain the main inference surfaces for image, video, and multiplex use cases.
- `sam3/agent/` suggests an orchestration layer that could be embedded into multi-app or assistant-driven workflows.
- `sam3/train/` and most of `sam3/eval/` are structurally useful later, but not necessary for first-pass integration planning.

---

## Summary
- This plan keeps the files most likely to explain how the app runs and how to embed it elsewhere.
- It excludes training, benchmarking, CI, docs collateral, and static assets to reduce noise.
- Outputs are persisted under `./facebookresearch-sam3/pre-analysis/` in both JSON and Markdown formats.
