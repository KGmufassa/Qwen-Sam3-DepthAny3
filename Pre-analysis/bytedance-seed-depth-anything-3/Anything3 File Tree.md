```
Directory structure:
└── bytedance-seed-depth-anything-3/
    ├── README.md
    ├── LICENSE
    ├── pyproject.toml
    ├── requirements.txt
    ├── .flake8
    ├── .pre-commit-config.yaml
    ├── da3_streaming/
    │   ├── README.md
    │   ├── da3_streaming.py
    │   ├── npz_output_process.py
    │   ├── requirements.txt
    │   ├── configs/
    │   │   ├── base_config.yaml
    │   │   ├── kitti.yaml
    │   │   └── tum.yaml
    │   ├── fastloop/
    │   │   ├── __init__.py
    │   │   ├── solve.cpp
    │   │   └── solve_python.py
    │   ├── loop_utils/
    │   │   ├── __init__.py
    │   │   ├── alignment_torch.py
    │   │   ├── alignment_triton.py
    │   │   ├── config_utils.py
    │   │   ├── logging_utils.py
    │   │   ├── loop_detector.py
    │   │   ├── loop_refinement.py
    │   │   ├── sim3loop.py
    │   │   └── sim3utils.py
    │   └── scripts/
    │       └── download_weights.sh
    ├── docs/
    │   ├── API.md
    │   ├── BENCHMARK.md
    │   ├── CLI.md
    │   └── funcs/
    │       └── ref_view_strategy.md
    └── src/
        └── depth_anything_3/
            ├── api.py
            ├── cfg.py
            ├── cli.py
            ├── registry.py
            ├── specs.py
            ├── app/
            │   ├── css_and_html.py
            │   ├── gradio_app.py
            │   └── modules/
            │       ├── __init__.py
            │       ├── event_handlers.py
            │       ├── file_handlers.py
            │       ├── model_inference.py
            │       ├── ui_components.py
            │       ├── utils.py
            │       └── visualization.py
            ├── bench/
            │   ├── __init__.py
            │   ├── dataset.py
            │   ├── evaluator.py
            │   ├── print_metrics.py
            │   ├── registries.py
            │   ├── utils.py
            │   ├── configs/
            │   │   └── eval_bench.yaml
            │   └── datasets/
            │       ├── __init__.py
            │       ├── dtu.py
            │       ├── dtu64.py
            │       ├── eth3d.py
            │       ├── hiroom.py
            │       ├── scannetpp.py
            │       └── sevenscenes.py
            ├── configs/
            │   ├── da3-base.yaml
            │   ├── da3-giant.yaml
            │   ├── da3-large.yaml
            │   ├── da3-small.yaml
            │   ├── da3metric-large.yaml
            │   ├── da3mono-large.yaml
            │   └── da3nested-giant-large.yaml
            ├── model/
            │   ├── __init__.py
            │   ├── cam_dec.py
            │   ├── cam_enc.py
            │   ├── da3.py
            │   ├── dpt.py
            │   ├── dualdpt.py
            │   ├── gs_adapter.py
            │   ├── gsdpt.py
            │   ├── reference_view_selector.py
            │   ├── dinov2/
            │   │   ├── dinov2.py
            │   │   ├── vision_transformer.py
            │   │   └── layers/
            │   │       ├── __init__.py
            │   │       ├── attention.py
            │   │       ├── block.py
            │   │       ├── drop_path.py
            │   │       ├── layer_scale.py
            │   │       ├── mlp.py
            │   │       ├── patch_embed.py
            │   │       ├── rope.py
            │   │       └── swiglu_ffn.py
            │   └── utils/
            │       ├── attention.py
            │       ├── block.py
            │       ├── gs_renderer.py
            │       ├── head_utils.py
            │       └── transform.py
            ├── services/
            │   ├── __init__.py
            │   ├── backend.py
            │   ├── gallery.py
            │   ├── inference_service.py
            │   └── input_handlers.py
            └── utils/
                ├── alignment.py
                ├── api_helpers.py
                ├── camera_trj_helpers.py
                ├── constants.py
                ├── geometry.py
                ├── gsply_helpers.py
                ├── layout_helpers.py
                ├── logger.py
                ├── memory.py
                ├── model_loading.py
                ├── parallel_utils.py
                ├── pca_utils.py
                ├── pose_align.py
                ├── ray_utils.py
                ├── read_write_model.py
                ├── registry.py
                ├── sh_helpers.py
                ├── visualize.py
                ├── export/
                │   ├── __init__.py
                │   ├── colmap.py
                │   ├── depth_vis.py
                │   ├── feat_vis.py
                │   ├── glb.py
                │   ├── gs.py
                │   ├── npz.py
                │   └── utils.py
                └── io/
                    ├── input_processor.py
                    └── output_processor.py
```
