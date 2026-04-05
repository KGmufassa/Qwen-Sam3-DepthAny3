```
Directory structure:
└── facebookresearch-sam3/
    ├── README.md
    ├── CODE_OF_CONDUCT.md
    ├── CONTRIBUTING.md
    ├── LICENSE
    ├── MANIFEST.in
    ├── pyproject.toml
    ├── README_TRAIN.md
    ├── RELEASE_SAM3p1.md
    ├── assets/
    │   └── veval/
    │       └── toy_gt_and_pred/
    │           └── toy_saco_veval_sav_test_eval_res.json
    ├── examples/
    │   ├── saco_gold_silver_vis_example.ipynb
    │   ├── saco_veval_eval_example.ipynb
    │   ├── saco_veval_vis_example.ipynb
    │   ├── sam3.1_video_predictor_example.ipynb
    │   ├── sam3_agent.ipynb
    │   ├── sam3_for_sam1_task_example.ipynb
    │   ├── sam3_for_sam2_video_task_example.ipynb
    │   └── sam3_image_interactive.ipynb
    ├── sam3/
    │   ├── __init__.py
    │   ├── logger.py
    │   ├── model_builder.py
    │   ├── visualization_utils.py
    │   ├── agent/
    │   │   ├── __init__.py
    │   │   ├── agent_core.py
    │   │   ├── client_llm.py
    │   │   ├── client_sam3.py
    │   │   ├── inference.py
    │   │   ├── viz.py
    │   │   ├── helpers/
    │   │   │   ├── __init__.py
    │   │   │   ├── boxes.py
    │   │   │   ├── color_map.py
    │   │   │   ├── keypoints.py
    │   │   │   ├── mask_overlap_removal.py
    │   │   │   ├── masks.py
    │   │   │   ├── memory.py
    │   │   │   ├── rle.py
    │   │   │   ├── roi_align.py
    │   │   │   ├── rotated_boxes.py
    │   │   │   ├── som_utils.py
    │   │   │   └── zoom_in.py
    │   │   └── system_prompts/
    │   │       └── system_prompt_iterative_checking.txt
    │   ├── eval/
    │   │   ├── __init__.py
    │   │   ├── cgf1_eval.py
    │   │   ├── coco_eval.py
    │   │   ├── coco_eval_offline.py
    │   │   ├── coco_reindex.py
    │   │   ├── coco_writer.py
    │   │   ├── conversion_util.py
    │   │   ├── demo_eval.py
    │   │   ├── postprocessors.py
    │   │   ├── saco_veval_eval.py
    │   │   ├── saco_veval_evaluators.py
    │   │   ├── ytvis_coco_wrapper.py
    │   │   ├── ytvis_eval.py
    │   │   ├── hota_eval_toolkit/
    │   │   │   ├── __init__.py
    │   │   │   ├── run_ytvis_eval.py
    │   │   │   └── trackeval/
    │   │   │       ├── __init__.py
    │   │   │       ├── _timing.py
    │   │   │       ├── eval.py
    │   │   │       ├── utils.py
    │   │   │       ├── datasets/
    │   │   │       │   ├── __init__.py
    │   │   │       │   ├── _base_dataset.py
    │   │   │       │   ├── tao_ow.py
    │   │   │       │   └── youtube_vis.py
    │   │   │       └── metrics/
    │   │   │           ├── __init__.py
    │   │   │           ├── _base_metric.py
    │   │   │           ├── count.py
    │   │   │           └── hota.py
    │   │   └── teta_eval_toolkit/
    │   │       ├── __init__.py
    │   │       ├── _timing.py
    │   │       ├── config.py
    │   │       ├── eval.py
    │   │       ├── utils.py
    │   │       ├── datasets/
    │   │       │   ├── __init__.py
    │   │       │   ├── _base_dataset.py
    │   │       │   ├── coco.py
    │   │       │   └── tao.py
    │   │       └── metrics/
    │   │           ├── __init__.py
    │   │           ├── _base_metric.py
    │   │           └── teta.py
    │   ├── model/
    │   │   ├── __init__.py
    │   │   ├── act_ckpt_utils.py
    │   │   ├── box_ops.py
    │   │   ├── data_misc.py
    │   │   ├── edt.py
    │   │   ├── encoder.py
    │   │   ├── geometry_encoders.py
    │   │   ├── io_utils.py
    │   │   ├── maskformer_segmentation.py
    │   │   ├── memory.py
    │   │   ├── model_misc.py
    │   │   ├── multiplex_mask_decoder.py
    │   │   ├── multiplex_utils.py
    │   │   ├── necks.py
    │   │   ├── position_encoding.py
    │   │   ├── sam1_task_predictor.py
    │   │   ├── sam3_base_predictor.py
    │   │   ├── sam3_image.py
    │   │   ├── sam3_image_processor.py
    │   │   ├── sam3_multiplex_detector.py
    │   │   ├── sam3_multiplex_detector_utils.py
    │   │   ├── sam3_multiplex_video_predictor.py
    │   │   ├── sam3_tracker_utils.py
    │   │   ├── sam3_video_predictor.py
    │   │   ├── text_encoder_ve.py
    │   │   ├── tokenizer_ve.py
    │   │   ├── vitdet.py
    │   │   ├── vl_combiner.py
    │   │   └── utils/
    │   │       ├── __init__.py
    │   │       ├── misc.py
    │   │       ├── sam1_utils.py
    │   │       └── sam2_utils.py
    │   ├── perflib/
    │   │   ├── __init__.py
    │   │   ├── associate_det_trk.py
    │   │   ├── compile.py
    │   │   ├── connected_components.py
    │   │   ├── fa3.py
    │   │   ├── fused.py
    │   │   ├── iou.py
    │   │   ├── masks_ops.py
    │   │   ├── nms.py
    │   │   ├── tests/
    │   │   │   └── tests.py
    │   │   └── triton/
    │   │       ├── connected_components.py
    │   │       └── nms.py
    │   ├── sam/
    │   │   ├── __init__.py
    │   │   ├── common.py
    │   │   ├── mask_decoder.py
    │   │   ├── prompt_encoder.py
    │   │   ├── rope.py
    │   │   └── transformer.py
    │   └── train/
    │       ├── __init__.py
    │       ├── masks_ops.py
    │       ├── matcher.py
    │       ├── nms_helper.py
    │       ├── train.py
    │       ├── trainer.py
    │       ├── configs/
    │       │   ├── eval_base.yaml
    │       │   ├── gold_image_evals/
    │       │   │   ├── sam3_gold_image_attributes.yaml
    │       │   │   ├── sam3_gold_image_crowded.yaml
    │       │   │   ├── sam3_gold_image_fg_food.yaml
    │       │   │   ├── sam3_gold_image_fg_sports.yaml
    │       │   │   ├── sam3_gold_image_metaclip_nps.yaml
    │       │   │   ├── sam3_gold_image_sa1b_nps.yaml
    │       │   │   └── sam3_gold_image_wiki_common.yaml
    │       │   ├── odinw13/
    │       │   │   ├── odinw_text_and_visual.yaml
    │       │   │   ├── odinw_text_only.yaml
    │       │   │   ├── odinw_text_only_positive.yaml
    │       │   │   ├── odinw_text_only_train.yaml
    │       │   │   └── odinw_visual_only.yaml
    │       │   ├── roboflow_v100/
    │       │   │   ├── roboflow_v100_eval.yaml
    │       │   │   └── roboflow_v100_full_ft_100_images.yaml
    │       │   ├── saco_video_evals/
    │       │   │   ├── saco_veval_sav_test.yaml
    │       │   │   ├── saco_veval_sav_test_noheur.yaml
    │       │   │   ├── saco_veval_sav_val.yaml
    │       │   │   ├── saco_veval_sav_val_noheur.yaml
    │       │   │   ├── saco_veval_smartglasses_test.yaml
    │       │   │   ├── saco_veval_smartglasses_test_noheur.yaml
    │       │   │   ├── saco_veval_smartglasses_val.yaml
    │       │   │   ├── saco_veval_smartglasses_val_noheur.yaml
    │       │   │   ├── saco_veval_yt1b_test.yaml
    │       │   │   ├── saco_veval_yt1b_test_noheur.yaml
    │       │   │   ├── saco_veval_yt1b_val.yaml
    │       │   │   └── saco_veval_yt1b_val_noheur.yaml
    │       │   └── silver_image_evals/
    │       │       ├── sam3_silver_image_bdd100k.yaml
    │       │       ├── sam3_silver_image_droid.yaml
    │       │       ├── sam3_silver_image_ego4d.yaml
    │       │       ├── sam3_silver_image_fathomnet.yaml
    │       │       ├── sam3_silver_image_food_rec.yaml
    │       │       ├── sam3_silver_image_geode.yaml
    │       │       ├── sam3_silver_image_inaturalist.yaml
    │       │       ├── sam3_silver_image_nga.yaml
    │       │       ├── sam3_silver_image_sav.yaml
    │       │       └── sam3_silver_image_yt1b.yaml
    │       ├── data/
    │       │   ├── __init__.py
    │       │   ├── coco_json_loaders.py
    │       │   ├── collator.py
    │       │   ├── sam3_image_dataset.py
    │       │   ├── sam3_video_dataset.py
    │       │   └── torch_dataset.py
    │       ├── loss/
    │       │   ├── __init__.py
    │       │   ├── mask_sampling.py
    │       │   ├── sam3_loss.py
    │       │   └── sigmoid_focal_loss.py
    │       ├── optim/
    │       │   ├── __init__.py
    │       │   ├── optimizer.py
    │       │   └── schedulers.py
    │       ├── transforms/
    │       │   ├── __init__.py
    │       │   ├── basic.py
    │       │   ├── filter_query_transforms.py
    │       │   ├── point_sampling.py
    │       │   └── segmentation.py
    │       └── utils/
    │           ├── __init__.py
    │           ├── checkpoint_utils.py
    │           ├── distributed.py
    │           ├── logger.py
    │           └── train_utils.py
    ├── scripts/
    │   ├── extract_odinw_results.py
    │   ├── extract_roboflow_vl100_results.py
    │   ├── measure_speed.py
    │   ├── qualitative_test.py
    │   └── eval/
    │       ├── standalone_cgf1.py
    │       ├── gold/
    │       │   ├── README.md
    │       │   └── eval_sam3.py
    │       ├── silver/
    │       │   ├── README.md
    │       │   ├── CONFIG_FRAMES.yaml
    │       │   ├── download_fathomnet.py
    │       │   ├── download_inaturalist.py
    │       │   ├── download_preprocess_nga.py
    │       │   ├── download_videos.py
    │       │   ├── extract_frames.py
    │       │   ├── preprocess_silver_geode_bdd100k_food_rec.py
    │       │   └── utils.py
    │       └── veval/
    │           ├── README.md
    │           ├── __init__.py
    │           ├── saco_yt1b_annot_update.py
    │           ├── saco_yt1b_downloader.py
    │           └── saco_yt1b_frame_prep_util.py
    └── .github/
        └── workflows/
            └── format.yml
```
