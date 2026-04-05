```
Directory structure:
└── bytedance-seed-depth-anything-3/
    ├── README.md
    ├── pyproject.toml
    ├── requirements.txt
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
    │   └── CLI.md
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
================================================
FILE: README.md
================================================
<div align="center">
<h1 style="border-bottom: none; margin-bottom: 0px ">Depth Anything 3: Recovering the Visual Space from Any Views</h1>
<!-- <h2 style="border-top: none; margin-top: 3px;">Recovering the Visual Space from Any Views</h2> -->


[**Haotong Lin**](https://haotongl.github.io/)<sup>&ast;</sup> · [**Sili Chen**](https://github.com/SiliChen321)<sup>&ast;</sup> · [**Jun Hao Liew**](https://liewjunhao.github.io/)<sup>&ast;</sup> · [**Donny Y. Chen**](https://donydchen.github.io)<sup>&ast;</sup> · [**Zhenyu Li**](https://zhyever.github.io/) · [**Guang Shi**](https://scholar.google.com/citations?user=MjXxWbUAAAAJ&hl=en) · [**Jiashi Feng**](https://scholar.google.com.sg/citations?user=Q8iay0gAAAAJ&hl=en)
<br>
[**Bingyi Kang**](https://bingyikang.com/)<sup>&ast;&dagger;</sup>

&dagger;project lead&emsp;&ast;Equal Contribution

<a href="https://arxiv.org/abs/2511.10647"><img src='https://img.shields.io/badge/arXiv-Depth Anything 3-red' alt='Paper PDF'></a>
<a href='https://depth-anything-3.github.io'><img src='https://img.shields.io/badge/Project_Page-Depth Anything 3-green' alt='Project Page'></a>
<a href='https://huggingface.co/spaces/depth-anything/Depth-Anything-3'><img src='https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Demo-blue'></a>
<!-- <a href='https://huggingface.co/datasets/depth-anything/VGB'><img src='https://img.shields.io/badge/Benchmark-VisGeo-yellow' alt='Benchmark'></a> -->
<!-- <a href='https://huggingface.co/datasets/depth-anything/data'><img src='https://img.shields.io/badge/Benchmark-xxx-yellow' alt='Data'></a> -->

</div>

This work presents **Depth Anything 3 (DA3)**, a model that predicts spatially consistent geometry from
arbitrary visual inputs, with or without known camera poses.
In pursuit of minimal modeling, DA3 yields two key insights:
- 💎 A **single plain transformer** (e.g., vanilla DINO encoder) is sufficient as a backbone without architectural specialization,
- ✨ A singular **depth-ray representation** obviates the need for complex multi-task learning.

🏆 DA3 significantly outperforms
[DA2](https://github.com/DepthAnything/Depth-Anything-V2) for monocular depth estimation,
and [VGGT](https://github.com/facebookresearch/vggt) for multi-view depth estimation and pose estimation.
All models are trained exclusively on **public academic datasets**.

<!-- <p align="center">
  <img src="assets/images/da3_teaser.png" alt="Depth Anything 3" width="100%">
</p> -->
<p align="center">
  <img src="assets/images/demo320-2.gif" alt="Depth Anything 3 - Left" width="70%">
</p>
<p align="center">
  <img src="assets/images/da3_radar.png" alt="Depth Anything 3" width="100%">
</p>


## 📰 News
- **11-12-2025:** 🚀 New models and [**DA3-Streaming**](da3_streaming/README.md) released! Handle ultra-long video sequence inference with less than 12GB GPU memory via sliding-window streaming inference. Special thanks to [Kai Deng](https://github.com/DengKaiCQ) for his contribution to DA3-Streaming!
- **08-12-2025:** 📊 [Benchmark evaluation pipeline](docs/BENCHMARK.md) released! Evaluate pose estimation & 3D reconstruction on 5 datasets.
- **30-11-2025:** Add [`use_ray_pose`](#use-ray-pose) and [`ref_view_strategy`](docs/funcs/ref_view_strategy.md) (reference view selection for multi-view inputs).   
- **25-11-2025:** Add [Awesome DA3 Projects](#-awesome-da3-projects), a community-driven section featuring DA3-based applications.
- **14-11-2025:** Paper, project page, code and models are all released.

## ✨ Highlights

### 🏆 Model Zoo
We release three series of models, each tailored for specific use cases in visual geometry.

- 🌟 **DA3 Main Series** (`DA3-Giant`, `DA3-Large`, `DA3-Base`, `DA3-Small`) These are our flagship foundation models, trained with a unified depth-ray representation. By varying the input configuration, a single model can perform a wide range of tasks:
  + 🌊 **Monocular Depth Estimation**: Predicts a depth map from a single RGB image.
  + 🌊 **Multi-View Depth Estimation**: Generates consistent depth maps from multiple images for high-quality fusion.
  + 🎯 **Pose-Conditioned Depth Estimation**: Achieves superior depth consistency when camera poses are provided as input.
  + 📷 **Camera Pose Estimation**:  Estimates camera extrinsics and intrinsics from one or more images.
  + 🟡 **3D Gaussian Estimation**: Directly predicts 3D Gaussians, enabling high-fidelity novel view synthesis.

- 📐 **DA3 Metric Series** (`DA3Metric-Large`) A specialized model fine-tuned for metric depth estimation in monocular settings, ideal for applications requiring real-world scale.

- 🔍 **DA3 Monocular Series** (`DA3Mono-Large`). A dedicated model for high-quality relative monocular depth estimation. Unlike disparity-based models (e.g.,  [Depth Anything 2](https://github.com/DepthAnything/Depth-Anything-V2)), it directly predicts depth, resulting in superior geometric accuracy.

🔗 Leveraging these available models, we developed a **nested series** (`DA3Nested-Giant-Large`). This series combines a any-view giant model with a metric model to reconstruct visual geometry at a real-world metric scale.

### 🛠️ Codebase Features
Our repository is designed to be a powerful and user-friendly toolkit for both practical application and future research.
- 🎨 **Interactive Web UI & Gallery**: Visualize model outputs and compare results with an easy-to-use Gradio-based web interface.
- ⚡ **Flexible Command-Line Interface (CLI)**: Powerful and scriptable CLI for batch processing and integration into custom workflows.
- 💾 **Multiple Export Formats**: Save your results in various formats, including `glb`, `npz`, depth images, `ply`, 3DGS videos, etc, to seamlessly connect with other tools.
- 🔧 **Extensible and Modular Design**: The codebase is structured to facilitate future research and the integration of new models or functionalities.


<!-- ### 🎯 Visual Geometry Benchmark
We introduce a new benchmark to rigorously evaluate geometry prediction models on three key tasks: pose estimation, 3D reconstruction, and visual rendering (novel view synthesis) quality.

- 🔄 **Broad Model Compatibility**: Our benchmark is designed to be versatile, supporting the evaluation of various models, including both monocular and multi-view depth estimation approaches.
- 🔬 **Robust Evaluation Pipeline**: We provide a standardized pipeline featuring RANSAC-based pose alignment, TSDF fusion for dense reconstruction, and a principled view selection strategy for novel view synthesis.
- 📊 **Standardized Metrics**: Performance is measured using established metrics: AUC for pose accuracy, F1-score and Chamfer Distance for reconstruction, and PSNR/SSIM/LPIPS for rendering quality.
- 🌍 **Diverse and Challenging Datasets**: The benchmark spans a wide range of scenes from datasets like HiRoom, ETH3D, DTU, 7Scenes, ScanNet++, DL3DV, Tanks and Temples, and MegaDepth. -->


## 🚀 Quick Start

### 📦 Installation

```bash
pip install xformers torch\>=2 torchvision
pip install -e . # Basic
pip install --no-build-isolation git+https://github.com/nerfstudio-project/gsplat.git@0b4dddf04cb687367602c01196913cde6a743d70 # for gaussian head
pip install -e ".[app]" # Gradio, python>=3.10
pip install -e ".[all]" # ALL
```

For detailed model information, please refer to the [Model Cards](#-model-cards) section below.

### 💻 Basic Usage

```python
import glob, os, torch
from depth_anything_3.api import DepthAnything3
device = torch.device("cuda")
model = DepthAnything3.from_pretrained("depth-anything/DA3NESTED-GIANT-LARGE")
model = model.to(device=device)
example_path = "assets/examples/SOH"
images = sorted(glob.glob(os.path.join(example_path, "*.png")))
prediction = model.inference(
    images,
)
# prediction.processed_images : [N, H, W, 3] uint8   array
print(prediction.processed_images.shape)
# prediction.depth            : [N, H, W]    float32 array
print(prediction.depth.shape)  
# prediction.conf             : [N, H, W]    float32 array
print(prediction.conf.shape)  
# prediction.extrinsics       : [N, 3, 4]    float32 array # opencv w2c or colmap format
print(prediction.extrinsics.shape)
# prediction.intrinsics       : [N, 3, 3]    float32 array
print(prediction.intrinsics.shape)
```

```bash

export MODEL_DIR=depth-anything/DA3NESTED-GIANT-LARGE
# This can be a Hugging Face repository or a local directory
# If you encounter network issues, consider using the following mirror: export HF_ENDPOINT=https://hf-mirror.com
# Alternatively, you can download the model directly from Hugging Face
export GALLERY_DIR=workspace/gallery
mkdir -p $GALLERY_DIR

# CLI auto mode with backend reuse
da3 backend --model-dir ${MODEL_DIR} --gallery-dir ${GALLERY_DIR} # Cache model to gpu
da3 auto assets/examples/SOH \
    --export-format glb \
    --export-dir ${GALLERY_DIR}/TEST_BACKEND/SOH \
    --use-backend

# CLI video processing with feature visualization
da3 video assets/examples/robot_unitree.mp4 \
    --fps 15 \
    --use-backend \
    --export-dir ${GALLERY_DIR}/TEST_BACKEND/robo \
    --export-format glb-feat_vis \
    --feat-vis-fps 15 \
    --process-res-method lower_bound_resize \
    --export-feat "11,21,31"

# CLI auto mode without backend reuse
da3 auto assets/examples/SOH \
    --export-format glb \
    --export-dir ${GALLERY_DIR}/TEST_CLI/SOH \
    --model-dir ${MODEL_DIR}

```

The model architecture is defined in [`DepthAnything3Net`](src/depth_anything_3/model/da3.py), and specified with a Yaml config file located at [`src/depth_anything_3/configs`](src/depth_anything_3/configs). The input and output processing are handled by [`DepthAnything3`](src/depth_anything_3/api.py). To customize the model architecture, simply create a new config file (*e.g.*, `path/to/new/config`) as:

```yaml
__object__:
  path: depth_anything_3.model.da3
  name: DepthAnything3Net
  args: as_params

net:
  __object__:
    path: depth_anything_3.model.dinov2.dinov2
    name: DinoV2
    args: as_params

  name: vitb
  out_layers: [5, 7, 9, 11]
  alt_start: 4
  qknorm_start: 4
  rope_start: 4
  cat_token: True

head:
  __object__:
    path: depth_anything_3.model.dualdpt
    name: DualDPT
    args: as_params

  dim_in: &head_dim_in 1536
  output_dim: 2
  features: &head_features 128
  out_channels: &head_out_channels [96, 192, 384, 768]
```

Then, the model can be created with the following code snippet.
```python
from depth_anything_3.cfg import create_object, load_config

Model = create_object(load_config("path/to/new/config"))
```



## 📚 Useful Documentation

- 🖥️ [Command Line Interface](docs/CLI.md)
- 📑 [Python API](docs/API.md)
- 📊 [Benchmark Evaluation](docs/BENCHMARK.md)

## 🗂️ Model Cards

Generally, you should observe that DA3-LARGE achieves comparable results to VGGT.

The Nested series uses an Any-view model to estimate pose and depth, and a monocular metric depth estimator for scaling. 

⚠️ Models with the `-1.1` suffix are retrained after fixing a training bug; prefer these refreshed checkpoints. The original `DA3NESTED-GIANT-LARGE`, `DA3-GIANT`, and `DA3-LARGE` remain available but are deprecated. You could expect much better performance for street scenes with the `-1.1` models.

| 🗃️ Model Name                  | 📏 Params | 📊 Rel. Depth | 📷 Pose Est. | 🧭 Pose Cond. | 🎨 GS | 📐 Met. Depth | ☁️ Sky Seg | 📄 License     |
|-------------------------------|-----------|---------------|--------------|---------------|-------|---------------|-----------|----------------|
| **Nested** | | | | | | | | |
| [DA3NESTED-GIANT-LARGE-1.1](https://huggingface.co/depth-anything/DA3NESTED-GIANT-LARGE-1.1)  | 1.40B     | ✅             | ✅            | ✅             | ✅     | ✅             | ✅         | CC BY-NC 4.0   |
| [DA3NESTED-GIANT-LARGE](https://huggingface.co/depth-anything/DA3NESTED-GIANT-LARGE)  | 1.40B     | ✅             | ✅            | ✅             | ✅     | ✅             | ✅         | CC BY-NC 4.0   |
| **Any-view Model** | | | | | | | | |
| [DA3-GIANT-1.1](https://huggingface.co/depth-anything/DA3-GIANT-1.1)                     | 1.15B     | ✅             | ✅            | ✅             | ✅     |               |           | CC BY-NC 4.0   |
| [DA3-GIANT](https://huggingface.co/depth-anything/DA3-GIANT)                     | 1.15B     | ✅             | ✅            | ✅             | ✅     |               |           | CC BY-NC 4.0   |
| [DA3-LARGE-1.1](https://huggingface.co/depth-anything/DA3-LARGE-1.1)                     | 0.35B     | ✅             | ✅            | ✅             |       |               |           | CC BY-NC 4.0     |
| [DA3-LARGE](https://huggingface.co/depth-anything/DA3-LARGE)                     | 0.35B     | ✅             | ✅            | ✅             |       |               |           | CC BY-NC 4.0     |
| [DA3-BASE](https://huggingface.co/depth-anything/DA3-BASE)                     | 0.12B     | ✅             | ✅            | ✅             |       |               |           | Apache 2.0     |
| [DA3-SMALL](https://huggingface.co/depth-anything/DA3-SMALL)                     | 0.08B     | ✅             | ✅            | ✅             |       |               |           | Apache 2.0     |
|                               |           |               |              |               |               |       |           |                |
| **Monocular Metric Depth** | | | | | | | | |
| [DA3METRIC-LARGE](https://huggingface.co/depth-anything/DA3METRIC-LARGE)              | 0.35B     | ✅             |              |               |       | ✅             | ✅         | Apache 2.0     |
|                               |           |               |              |               |               |       |           |                |
| **Monocular Depth** | | | | | | | | |
| [DA3MONO-LARGE](https://huggingface.co/depth-anything/DA3MONO-LARGE)                | 0.35B     | ✅             |              |               |               |       | ✅         | Apache 2.0     |


## ❓ FAQ

- **Monocular Metric Depth**: To obtain metric depth in meters from `DA3METRIC-LARGE`, use `metric_depth = focal * net_output / 300.`, where `focal` is the focal length in pixels (typically the average of fx and fy from the camera intrinsic matrix K). Note that the output from `DA3NESTED-GIANT-LARGE` is already in meters.

- <a id="use-ray-pose"></a>**Ray Head (`use_ray_pose`)**:  Our API and CLI support `use_ray_pose` arg, which means that the model will derive camera pose from ray head, which is generally slightly slower, but more accurate. Note that the default is `False` for faster inference speed. 
  <details>
  <summary>AUC3 Results for DA3NESTED-GIANT-LARGE</summary>
  
  | Model | HiRoom | ETH3D | DTU | 7Scenes | ScanNet++ | 
  |-------|------|-------|-----|---------|-----------|
  | `ray_head` | 84.4 | 52.6 | 93.9 | 29.5 | 89.4 |
  | `cam_head` | 80.3 | 48.4 | 94.1 | 28.5 | 85.0 |

  </details>




- **Older GPUs without XFormers support**: See [Issue #11](https://github.com/ByteDance-Seed/Depth-Anything-3/issues/11). Thanks to [@S-Mahoney](https://github.com/S-Mahoney) for the solution!


## 🏢 Awesome DA3 Projects

A community-curated list of Depth Anything 3 integrations across 3D tools, creative pipelines, robotics, and web/VR viewers, including but not limited to these. You are welcome to submit your DA3-based project via PR, and we will review and feature it if applicable.

- [DA3-blender](https://github.com/xy-gao/DA3-blender): Blender addon for DA3-based 3D reconstruction from a set of images. 

- [ComfyUI-DepthAnythingV3](https://github.com/PozzettiAndrea/ComfyUI-DepthAnythingV3): ComfyUI nodes for Depth Anything 3, supporting single/multi-view and video-consistent depth with optional point‑cloud export.

- [DA3-ROS2-Wrapper](https://github.com/GerdsenAI/GerdsenAI-Depth-Anything-3-ROS2-Wrapper): Real-time DA3 depth in ROS2 with multi-camera support. 

- [DA3-ROS2-CPP-TensorRT](https://github.com/ika-rwth-aachen/ros2-depth-anything-v3-trt): DA3 ROS2 C++ TensorRT Inference Node: a ROS2 node for DA3 depth estimation using TensorRT for real-time inference.

- [VideoDepthViewer3D](https://github.com/amariichi/VideoDepthViewer3D): Streaming videos with DA3 metric depth to a Three.js/WebXR 3D viewer for VR/stereo playback.


## 🧑‍💻 Official Codebase Core Contributors and Maintainers

<table>
  <tr>
    <td align="center">
      <a href="https://bingykang.github.io/">
        <img src="https://images.weserv.nl/?url=https://bingykang.github.io/images/bykang_homepage.jpeg?h=100&w=100&fit=cover&mask=circle&maxage=7d" width="100px;" alt=""/>
      </a>
        <br />
        <sub><b>Bingyi Kang</b></sub>
    </td>
    <td align="center">
      <a href="https://haotongl.github.io/">
        <img src="https://images.weserv.nl/?url=https://haotongl.github.io/assets/img/prof_pic.jpg?h=100&w=100&fit=cover&mask=circle&maxage=7d" width="100px;" alt=""/>
      </a>
        <br />
        <sub>Haotong Lin</sub>
    </td>
    <td align="center">
      <a href="https://github.com/SiliChen321">
        <img src="https://images.weserv.nl/?url=https://avatars.githubusercontent.com/u/195901058?v=4&h=100&w=100&fit=cover&mask=circle&maxage=7d" width="100px;" alt=""/>
      </a>
        <br />
        <sub>Sili Chen</sub>
    </td>
    <td align="center">
      <a href="https://liewjunhao.github.io/">
        <img src="https://images.weserv.nl/?url=https://liewjunhao.github.io/images/liewjunhao.png?h=100&w=100&fit=cover&mask=circle&maxage=7d" width="100px;" alt=""/>
       </a>
        <br />
        <sub>Jun Hao Liew</sub>
    </td>
    <td align="center">
      <a href="https://donydchen.github.io/">
        <img src="https://images.weserv.nl/?url=https://donydchen.github.io/assets/img/profile.jpg?h=100&w=100&fit=cover&mask=circle&maxage=7d" width="100px;" alt=""/>
      </a>
        <br />
        <sub>Donny Y. Chen</sub>
    </td>
    <td align="center">
      <a href="https://github.com/DengKaiCQ">
        <img src="https://images.weserv.nl/?url=https://avatars.githubusercontent.com/u/59907452?v=4&h=100&w=100&fit=cover&mask=circle&maxage=7d" width="100px;" alt=""/>
      </a>
        <br />
        <sub>Kai Deng</sub>
    </td>
  </tr>
</table>

## 📝 Citations
If you find Depth Anything 3 useful in your research or projects, please cite our work:

```
@article{depthanything3,
  title={Depth Anything 3: Recovering the visual space from any views},
  author={Haotong Lin and Sili Chen and Jun Hao Liew and Donny Y. Chen and Zhenyu Li and Guang Shi and Jiashi Feng and Bingyi Kang},
  journal={arXiv preprint arXiv:2511.10647},
  year={2025}
}
```



================================================
FILE: pyproject.toml
================================================
[build-system]
requires = ["hatchling>=1.25", "hatch-vcs>=0.4"]
build-backend = "hatchling.build"

[project]
name = "depth-anything-3"
version = "0.0.0"
description = "Depth Anything 3"
readme = "README.md"
requires-python = ">=3.9, <=3.13"
license = { text = "Apache-2.0" }
authors = [{ name = "Your Name" }]

dependencies = [
    "pre-commit",
    "trimesh",
    "torch>=2",
    "torchvision",
    "einops",
    "huggingface_hub",
    "imageio",
    "numpy<2",
    "opencv-python",
    "xformers",
    "open3d",
    "fastapi",
    "uvicorn",
    "requests",
    "typer",
    "pillow",
    "omegaconf",
    "evo",
    "e3nn",
    "moviepy",
    "plyfile",
    "pillow_heif",
    "safetensors",
    "uvicorn",
    "moviepy==1.0.3",
    "typer>=0.9.0",
    "pycolmap",
]

[project.optional-dependencies]
app = ["gradio>=5", "pillow>=9.0"] # requires that python3>=3.10
gs = ["gsplat @ git+https://github.com/nerfstudio-project/gsplat.git@0b4dddf04cb687367602c01196913cde6a743d70"]
all = ["depth-anything-3[app,gs]"]


[project.scripts]
da3 = "depth_anything_3.cli:app"

[project.urls]
Homepage = "https://github.com/ByteDance-Seed/Depth-Anything-3"

[tool.hatch.version]
source = "vcs"

[tool.hatch.build.targets.wheel]
packages = ["src/depth_anything_3"]

[tool.hatch.build.targets.sdist]
include = [
  "/README.md",
  "/pyproject.toml",
  "/src/depth_anything_3",
]

[tool.hatch.metadata]
allow-direct-references = true

[tool.mypy]
plugins = ["jaxtyping.mypy_plugin"]

[tool.black]
line-length = 99
target-version = ['py37', 'py38', 'py39', 'py310', 'py311']
include = '\.pyi?$'
exclude = '''
/(
  | \.git
)/
'''

[tool.isort]
profile = "black"
multi_line_output = 3
include_trailing_comma = true
known_third_party = ["bson","cruise","cv2","dataloader","diffusers","omegaconf","tensorflow","torch","torchvision","transformers","gsplat"]
known_first_party = ["common", "data", "models", "projects"]
sections = ["FUTURE","STDLIB","THIRDPARTY","FIRSTPARTY","LOCALFOLDER"]
skip_gitignore = true
line_length = 99
no_lines_before="THIRDPARTY"



================================================
FILE: requirements.txt
================================================
pre-commit
trimesh
torch>=2
torchvision
einops
huggingface_hub
imageio
numpy<2
opencv-python
xformers
open3d
fastapi
uvicorn
requests
typer
pillow
omegaconf
evo
e3nn
moviepy
plyfile
pillow_heif
safetensors
pycolmap


================================================
FILE: da3_streaming/README.md
================================================
<p align="center">
<p align="center">
<h1 align="center">DA3-Streaming: Memory-Efficient Inference for Videos via Chunk Streaming</h1>
</p>


This repo introduces a streaming pipeline that enables `Depth Anything 3` to process ⭐ **`long video sequences`** and **`super-large scale scenes`** ⭐ under tight CPU/GPU memory budgets by chunking frames and managing state across chunks.
Built on the ideas of `VGGT-Long`, it focuses on memory efficiency and stable online inference for near-real-time video processing.

`DA3-Streaming` is built on the [VGGT-Long](https://github.com/DengKaiCQ/VGGT-Long) and [Depth Anything 3](https://github.com/ByteDance-Seed/Depth-Anything-3).

### **Updates**

`[11 Nov 2025]` Code of `DA3-Streaming` release.

##  Setup, Installation & Running

### 📮 1 - Clone this project

Clone the repo using the `--recursive` flag

```cmd
git clone --recursive https://github.com/ByteDance-Seed/Depth-Anything-3.git

```

If you forgot `--recursive`

```cmd
cd <your_dir>/Depth-Anything-3/
git submodule update --init --recursive .
```

### 📦 2 - Environment Setup

#### Step 1: Dependency Installation

Install `Depth-Anything-3` first.

```cmd
pip install -r requirements.txt
```

#### Step 2: Weights Download

Download all the pre-trained weights needed:

```cmd
bash ./scripts/download_weights.sh
```


#### System dependencies you may encounter.

If you encounter an error about `libGL.so.1` (the error comes from `opencv-python`), please run the following cmd to install the system dependencies.

```cmd
sudo apt-get install -y libgl1-mesa-glx
```


### 🚀 3 - Running the code


```cmd
python da3_streaming.py --image_dir ./path_of_images
```

or

```cmd
python da3_streaming.py --image_dir ./path_of_images --config ./configs/base_config.yaml --output_dir ${OUTPUT_DIR}
```

You may run the following cmd if you got videos before `python da3_streaming.py`.

```
mkdir ./extract_images
ffmpeg -i your_video.mp4 -vf "fps=5,scale=640:-1" ./extract_images/frame_%06d.png
```


### 4 - Outputs

#### Basic Outputs

After running the code, you will get the following outputs:

- `${OUTPUT_DIR}/camera_poses.txt`: The camera poses file. Each line contains the extrinsic matrix parameters of a frame.
- `${OUTPUT_DIR}/intrinsic.txt`: The intrinsic parameters of the camera. Each line contains fx, fy, cx, cy of a frame.
- `${OUTPUT_DIR}/pcd/combined_pcd.ply`: The combined point cloud file. It contains the 3D points from all frames.

#### Additional Outputs

If setting `save_depth_conf_result` in config to `True`, you will get outputs for each frame:

- `${OUTPUT_DIR}/results_output`: The folder that contains the rgb, depth, confidence and intrinsic results for each frame. Note that the minimum value of confidence is 0.

To verify the results, you can use the following cmd to fuse point cloud from `./results_output`. The fused point cloud file will be saved as `${OUTPUT_DIR}/output.ply`.

```cmd
python npz_output_process.py --npz_folder ${OUTPUT_DIR}/results_output --pose_file ${OUTPUT_DIR}/camera_poses.txt --output_file ${OUTPUT_DIR}/output.ply
```


**Note on Space Requirements**: Please ensure your machine has sufficient disk space before running the code for `DA3-Streaming`. When finishing, the code will delete these intermediate results to prevent excessive disk usage.

## Experiment Results

We conducted some additional experiments to compare the performance differences among different architectures. Below is the comparison of `ATE RMSE [m]` on KITTI Odometry between `DA3-Streaming`, `VGGT-Long` and `Pi-Long`. All methods are evaluated with overlap equal to half chunk size, comparable resolution (~500px-width), and loop closure with similarity threshold 0.85.


| **Method**                      | **chunk size**| **AVG**  | **AVG (w/o 01)** | **00**   | **01**   | **02**   | **03** | **04** | **05**  | **06**  | **07**  | **08**  | **09**   | **10**  |
|:-------------------------------:|:--------:|:--------:|:----------------:|:--------:|:--------:|:--------:|:------:|:------:|:-------:|:-------:|:-------:|:-------:|:--------:|:-------:|
| **Num. of Frames**             |      | 2109     | 2210             | 4542     | 1101     | 4661     | 801    | 271    | 2761    | 1101    | 1101    | 4071    | 1591     | 1201    |
| **VGGT-Long**            |120| 25.60  | 22.81          | 16.13   | 53.43   | 51.98   | 4.37  | 2.15  | 12.69  | 11.33  | 3.60   | 70.29  | 34.55   | 21.05  |
| **Pi-Long**              |120| 21.17  | 11.81          | 5.55    | 114.83  | 50.29   | 1.63  | 1.11  | 3.48   | 2.88   | 3.92   | 24.25  | 7.38    | 17.61  |
| **DA3-Streaming**        |120| <span style="text-decoration: underline;">18.63</span>  | **10.42**          | 4.48    | 100.77  | 33.41   | 3.58  | 2.39  | 3.95   | 7.59   | 2.09   | 31.20  | 8.06    | 7.44   |
| **VGGT-Long**            |60| 26.36 |	19.30           | 8.06 | 	96.96 |	34.16 |	6.83  |	4.16 |	9.15 |	4.68 |	2.68 |	63.15 |	32.24 |	27.87  |
| **Pi-Long**              |60| 30.63 |	17.10           | 7.82 |	165.92 |	73.59 |	3.67 |	0.91 |	5.16 |	3.89 |	3.57 |	33.97 |	17.01 |	21.41  |
| **DA3-Streaming**        |60| **16.83**  | <span style="text-decoration: underline;">10.64</span>          | 5.13 | 78.76 | 35.64 | 5.38 | 3.18 | 3.04 | 2.83 | 2.32 | 26.55 | 8.86 | 13.42   |


In `DA3-Streaming`, we restructured the code and accelerated it using GPU technology. Currently, our method achieves a running speed of nearly `10 FPS` without the Keyframe strategy (the test time has excluded warm-up, model loading and ply result saving). Following results are evaluated on KITTI sequences 00, 05, and 08, totaling 11,373 frames, using an NVIDIA A100 GPU.

| **Method**         | **Time** | **FPS** |
|:------------------:|:------------------------:|:------------------------:|
| **VGGT-Long** | 65min 08sec               | 2.91   |
| **Pi-long**   | 60min 09sec               | 3.15   |
| **DA3-Streaming**  | 22min 17sec                |**8.51**   |



Although the current pipeline is not an SLAM system, `DA3-Streaming` still has a certain degree of accuracy compared to the uncalibrated SLAM method on TUM RGB-D. `DA3-Streaming`, `VGGT-Long` and `Pi-Long` are evaluated with chunk size 120, overlap 60, comparable resolution (~500px-width) and with loop closure.

| **Methods**                  | **AVG** | **360** | **desk** | **desk2** | **floor** | **plant** | **room** | **rpy** | **teddy** | **xyz** |
|:----------------------------:|:-------:|:--------:|:---------:|:---------:|:---------:|:--------:|:-------:|:---------:|:-------:|:-------:|
| **Droid-SLAM Uncalibrated**  | 0.163  | 0.202  | 0.032   | 0.091    | 0.064    | 0.045    | 0.918   | 0.056  | 0.045    | 0.012  |
| **Mast3r-SLAM Uncalibrated** | **0.060**  | 0.070  | 0.035   | 0.055    | 0.056    | 0.035    | 0.118   | 0.041  | 0.114    | 0.020  |
| **VGGT-Long**                | 0.110  | 0.118  |	0.058  |	0.111 	| 0.118 	 | 0.071 	  | 0.155 	| 0.140  | 0.120 	  | 0.099  |
| **Pi-long**                  | 0.094  | 0.115  | 0.047   | 0.052    | 0.160 	 | 0.085 	  | 0.114 	| 0.143  | 0.081 	  | 0.052  |
| **DA3-Streaming**            | <span style="text-decoration: underline;">0.087</span>  | 0.059  | 0.034   | 0.042    | 0.107    | 0.060    | 0.105   | 0.206  | 0.126    | 0.044  |


We also evaluate `DA3-Streaming` with different chunk sizes on KITTI (w/o 01) with resolution 504x154 and TUM RGB-D with resolution 504x378. Overlap is set to half of chunk size.

| | **Chunk size** | **120** | **90** | **60** | **30** |
|:-------:|:---------:|:--------:|:-----:|:------:|:------:|
| **KITTI (504x154)** | **Peak VRAM [GB]** | 15.9 | 14.3 | 12.7 | 11.5 |
|| **ATE RMSE [m]** | 10.42 | 9.38 | 10.64 | 19.39 |
| **TUM RGB-D (504x378)** |  **Peak VRAM [GB]** | 28.3 | 25.1 | 21.2 | 18.7 |
|| **ATE RMSE [m]** | 0.087 | 0.091 | 0.127 | 0.227 |

## Acknowledgements

Our project is based on [VGGT-Long](https://github.com/DengKaiCQ/VGGT-Long) and [Depth Anything 3](https://github.com/ByteDance-Seed/Depth-Anything-3).



================================================
FILE: da3_streaming/da3_streaming.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
# Adapted from [VGGT-Long](https://github.com/DengKaiCQ/VGGT-Long)

import argparse
import gc
import glob
import json
import os
import shutil
import sys
from datetime import datetime
import matplotlib
import matplotlib.pyplot as plt
import numpy as np
import torch
from loop_utils.alignment_torch import (
    apply_sim3_direct_torch,
    depth_to_point_cloud_optimized_torch,
)
from loop_utils.config_utils import load_config
from loop_utils.loop_detector import LoopDetector
from loop_utils.sim3loop import Sim3LoopOptimizer
from loop_utils.sim3utils import (
    accumulate_sim3_transforms,
    compute_sim3_ab,
    merge_ply_files,
    precompute_scale_chunks_with_depth,
    process_loop_list,
    save_confident_pointcloud_batch,
    warmup_numba,
    weighted_align_point_maps,
)
from safetensors.torch import load_file

from depth_anything_3.api import DepthAnything3

matplotlib.use("Agg")


def depth_to_point_cloud_vectorized(depth, intrinsics, extrinsics, device=None):
    """
    depth: [N, H, W] numpy array or torch tensor
    intrinsics: [N, 3, 3] numpy array or torch tensor
    extrinsics: [N, 3, 4] (w2c) numpy array or torch tensor
    Returns: point_cloud_world: [N, H, W, 3] same type as input
    """
    input_is_numpy = False
    if isinstance(depth, np.ndarray):
        input_is_numpy = True

        depth_tensor = torch.tensor(depth, dtype=torch.float32)
        intrinsics_tensor = torch.tensor(intrinsics, dtype=torch.float32)
        extrinsics_tensor = torch.tensor(extrinsics, dtype=torch.float32)

        if device is not None:
            depth_tensor = depth_tensor.to(device)
            intrinsics_tensor = intrinsics_tensor.to(device)
            extrinsics_tensor = extrinsics_tensor.to(device)
    else:
        depth_tensor = depth
        intrinsics_tensor = intrinsics
        extrinsics_tensor = extrinsics

    if device is not None:
        depth_tensor = depth_tensor.to(device)
        intrinsics_tensor = intrinsics_tensor.to(device)
        extrinsics_tensor = extrinsics_tensor.to(device)

    # main logic

    N, H, W = depth_tensor.shape

    device = depth_tensor.device

    u = torch.arange(W, device=device).float().view(1, 1, W, 1).expand(N, H, W, 1)
    v = torch.arange(H, device=device).float().view(1, H, 1, 1).expand(N, H, W, 1)
    ones = torch.ones((N, H, W, 1), device=device)
    pixel_coords = torch.cat([u, v, ones], dim=-1)

    intrinsics_inv = torch.inverse(intrinsics_tensor)  # [N, 3, 3]
    camera_coords = torch.einsum("nij,nhwj->nhwi", intrinsics_inv, pixel_coords)
    camera_coords = camera_coords * depth_tensor.unsqueeze(-1)
    camera_coords_homo = torch.cat([camera_coords, ones], dim=-1)

    extrinsics_4x4 = torch.zeros(N, 4, 4, device=device)
    extrinsics_4x4[:, :3, :4] = extrinsics_tensor
    extrinsics_4x4[:, 3, 3] = 1.0

    c2w = torch.inverse(extrinsics_4x4)
    world_coords_homo = torch.einsum("nij,nhwj->nhwi", c2w, camera_coords_homo)
    point_cloud_world = world_coords_homo[..., :3]

    if input_is_numpy:
        point_cloud_world = point_cloud_world.cpu().numpy()

    return point_cloud_world


def remove_duplicates(data_list):
    """
    data_list: [(67, (3386, 3406), 48, (2435, 2455)), ...]
    """
    seen = {}
    result = []

    for item in data_list:
        if item[0] == item[2]:
            continue

        key = (item[0], item[2])

        if key not in seen.keys():
            seen[key] = True
            result.append(item)

    return result


class DA3_Streaming:
    def __init__(self, image_dir, save_dir, config):
        self.config = config

        self.chunk_size = self.config["Model"]["chunk_size"]
        self.overlap = self.config["Model"]["overlap"]
        self.overlap_s = 0
        self.overlap_e = self.overlap - self.overlap_s
        self.conf_threshold = 1.5
        self.seed = 42
        self.device = "cuda" if torch.cuda.is_available() else "cpu"
        self.dtype = (
            torch.bfloat16 if torch.cuda.get_device_capability()[0] >= 8 else torch.float16
        )

        self.img_dir = image_dir
        self.img_list = None
        self.output_dir = save_dir

        self.result_unaligned_dir = os.path.join(save_dir, "_tmp_results_unaligned")
        self.result_aligned_dir = os.path.join(save_dir, "_tmp_results_aligned")
        self.result_loop_dir = os.path.join(save_dir, "_tmp_results_loop")
        self.result_output_dir = os.path.join(save_dir, "results_output")
        self.pcd_dir = os.path.join(save_dir, "pcd")
        os.makedirs(self.result_unaligned_dir, exist_ok=True)
        os.makedirs(self.result_aligned_dir, exist_ok=True)
        os.makedirs(self.result_loop_dir, exist_ok=True)
        os.makedirs(self.pcd_dir, exist_ok=True)

        self.all_camera_poses = []
        self.all_camera_intrinsics = []

        self.delete_temp_files = self.config["Model"]["delete_temp_files"]

        print("Loading model...")

        with open(self.config["Weights"]["DA3_CONFIG"]) as f:
            config = json.load(f)
        self.model = DepthAnything3(**config)
        weight = load_file(self.config["Weights"]["DA3"])
        self.model.load_state_dict(weight, strict=False)

        self.model.eval()
        self.model = self.model.to(self.device)

        self.skyseg_session = None

        self.chunk_indices = None  # [(begin_idx, end_idx), ...]

        self.loop_list = []  # e.g. [(1584, 139), ...]

        self.loop_optimizer = Sim3LoopOptimizer(self.config)

        self.sim3_list = []  # [(s [1,], R [3,3], T [3,]), ...]

        self.loop_sim3_list = []  # [(chunk_idx_a, chunk_idx_b, s [1,], R [3,3], T [3,]), ...]

        self.loop_predict_list = []

        self.loop_enable = self.config["Model"]["loop_enable"]

        if self.loop_enable:
            loop_info_save_path = os.path.join(save_dir, "loop_closures.txt")
            self.loop_detector = LoopDetector(
                image_dir=image_dir, output=loop_info_save_path, config=self.config
            )
            self.loop_detector.load_model()

        print("init done.")

    def get_loop_pairs(self):
        self.loop_detector.run()
        loop_list = self.loop_detector.get_loop_list()
        return loop_list

    def save_depth_conf_result(self, predictions, chunk_idx, s, R, T):
        if not self.config["Model"]["save_depth_conf_result"]:
            return
        os.makedirs(self.result_output_dir, exist_ok=True)

        chunk_start, chunk_end = self.chunk_indices[chunk_idx]

        if chunk_idx == 0:
            save_indices = list(range(0, chunk_end - chunk_start - self.overlap_e))
        elif chunk_idx == len(self.chunk_indices) - 1:
            save_indices = list(range(self.overlap_s, chunk_end - chunk_start))
        else:
            save_indices = list(range(self.overlap_s, chunk_end - chunk_start - self.overlap_e))

        print("[save_depth_conf_result] save_indices:")

        for local_idx in save_indices:
            global_idx = chunk_start + local_idx
            print(f"{global_idx}, ", end="")

            image = predictions.processed_images[local_idx]  # [H, W, 3] uint8
            depth = predictions.depth[local_idx]  # [H, W] float32
            conf = predictions.conf[local_idx]  # [H, W] float32
            intrinsics = predictions.intrinsics[local_idx]  # [3, 3] float32

            filename = f"frame_{global_idx}.npz"
            filepath = os.path.join(self.result_output_dir, filename)

            if self.config["Model"]["save_debug_info"]:
                np.savez_compressed(
                    filepath,
                    image=image,
                    depth=depth,
                    conf=conf,
                    intrinsics=intrinsics,
                    extrinsics=predictions.extrinsics[local_idx],
                    s=s,
                    R=R,
                    T=T,
                )
            else:
                np.savez_compressed(
                    filepath, image=image, depth=depth, conf=conf, intrinsics=intrinsics
                )
        print("")

    def process_single_chunk(self, range_1, chunk_idx=None, range_2=None, is_loop=False):
        start_idx, end_idx = range_1
        chunk_image_paths = self.img_list[start_idx:end_idx]
        if range_2 is not None:
            start_idx, end_idx = range_2
            chunk_image_paths += self.img_list[start_idx:end_idx]

        # images = load_and_preprocess_images(chunk_image_paths).to(self.device)
        print(f"Loaded {len(chunk_image_paths)} images")

        ref_view_strategy = self.config["Model"][
            "ref_view_strategy" if not is_loop else "ref_view_strategy_loop"
        ]

        torch.cuda.empty_cache()
        with torch.no_grad():
            with torch.cuda.amp.autocast(dtype=self.dtype):
                images = chunk_image_paths
                # images: ['xxx.png', 'xxx.png', ...]

                predictions = self.model.inference(images, ref_view_strategy=ref_view_strategy)

                predictions.depth = np.squeeze(predictions.depth)
                predictions.conf -= 1.0

                print(predictions.processed_images.shape)  # [N, H, W, 3] uint8
                print(predictions.depth.shape)  # [N, H, W] float32
                print(predictions.conf.shape)  # [N, H, W] float32
                print(predictions.extrinsics.shape)  # [N, 3, 4] float32 (w2c)
                print(predictions.intrinsics.shape)  # [N, 3, 3] float32
        torch.cuda.empty_cache()

        # Save predictions to disk instead of keeping in memory
        if is_loop:
            save_dir = self.result_loop_dir
            filename = f"loop_{range_1[0]}_{range_1[1]}_{range_2[0]}_{range_2[1]}.npy"
        else:
            if chunk_idx is None:
                raise ValueError("chunk_idx must be provided when is_loop is False")
            save_dir = self.result_unaligned_dir
            filename = f"chunk_{chunk_idx}.npy"

        save_path = os.path.join(save_dir, filename)

        if not is_loop and range_2 is None:
            extrinsics = predictions.extrinsics
            intrinsics = predictions.intrinsics
            chunk_range = self.chunk_indices[chunk_idx]
            self.all_camera_poses.append((chunk_range, extrinsics))
            self.all_camera_intrinsics.append((chunk_range, intrinsics))

        np.save(save_path, predictions)

        return predictions

    def get_chunk_indices(self):
        if len(self.img_list) <= self.chunk_size:
            num_chunks = 1
            chunk_indices = [(0, len(self.img_list))]
        else:
            step = self.chunk_size - self.overlap
            num_chunks = (len(self.img_list) - self.overlap + step - 1) // step
            chunk_indices = []
            for i in range(num_chunks):
                start_idx = i * step
                end_idx = min(start_idx + self.chunk_size, len(self.img_list))
                chunk_indices.append((start_idx, end_idx))
        return chunk_indices, num_chunks

    def align_2pcds(
        self,
        point_map1,
        conf1,
        point_map2,
        conf2,
        chunk1_depth,
        chunk2_depth,
        chunk1_depth_conf,
        chunk2_depth_conf,
    ):

        conf_threshold = min(np.median(conf1), np.median(conf2)) * 0.1

        scale_factor = None
        if self.config["Model"]["align_method"] == "scale+se3":
            scale_factor_return, quality_score, method_used = precompute_scale_chunks_with_depth(
                chunk1_depth,
                chunk1_depth_conf,
                chunk2_depth,
                chunk2_depth_conf,
                method=self.config["Model"]["scale_compute_method"],
            )
            print(
                f"[Depth Scale Precompute] scale: {scale_factor_return}, \
                    quality_score: {quality_score}, method_used: {method_used}"
            )
            scale_factor = scale_factor_return

        s, R, t = weighted_align_point_maps(
            point_map1,
            conf1,
            point_map2,
            conf2,
            conf_threshold=conf_threshold,
            config=self.config,
            precompute_scale=scale_factor,
        )
        print("Estimated Scale:", s)
        print("Estimated Rotation:\n", R)
        print("Estimated Translation:", t)

        return s, R, t

    def get_loop_sim3_from_loop_predict(self, loop_predict_list):
        loop_sim3_list = []
        for item in loop_predict_list:
            chunk_idx_a = item[0][0]
            chunk_idx_b = item[0][2]
            chunk_a_range = item[0][1]
            chunk_b_range = item[0][3]

            point_map_loop_org = depth_to_point_cloud_vectorized(
                item[1].depth, item[1].intrinsics, item[1].extrinsics
            )

            chunk_a_s = 0
            chunk_a_e = chunk_a_len = chunk_a_range[1] - chunk_a_range[0]
            chunk_b_s = -chunk_b_range[1] + chunk_b_range[0]
            chunk_b_e = point_map_loop_org.shape[0]
            chunk_b_len = chunk_b_range[1] - chunk_b_range[0]

            chunk_a_rela_begin = chunk_a_range[0] - self.chunk_indices[chunk_idx_a][0]
            chunk_a_rela_end = chunk_a_rela_begin + chunk_a_len
            chunk_b_rela_begin = chunk_b_range[0] - self.chunk_indices[chunk_idx_b][0]
            chunk_b_rela_end = chunk_b_rela_begin + chunk_b_len

            print("chunk_a align")

            point_map_loop_a = point_map_loop_org[chunk_a_s:chunk_a_e]
            conf_loop = item[1].conf[chunk_a_s:chunk_a_e]
            print(self.chunk_indices[chunk_idx_a])
            print(chunk_a_range)
            print(chunk_a_rela_begin, chunk_a_rela_end)
            chunk_data_a = np.load(
                os.path.join(self.result_unaligned_dir, f"chunk_{chunk_idx_a}.npy"),
                allow_pickle=True,
            ).item()

            point_map_a = depth_to_point_cloud_vectorized(
                chunk_data_a.depth, chunk_data_a.intrinsics, chunk_data_a.extrinsics
            )
            point_map_a = point_map_a[chunk_a_rela_begin:chunk_a_rela_end]
            conf_a = chunk_data_a.conf[chunk_a_rela_begin:chunk_a_rela_end]

            if self.config["Model"]["align_method"] == "scale+se3":
                chunk_a_depth = np.squeeze(chunk_data_a.depth[chunk_a_rela_begin:chunk_a_rela_end])
                chunk_a_depth_conf = np.squeeze(
                    chunk_data_a.conf[chunk_a_rela_begin:chunk_a_rela_end]
                )
                chunk_a_loop_depth = np.squeeze(item[1].depth[chunk_a_s:chunk_a_e])
                chunk_a_loop_depth_conf = np.squeeze(item[1].conf[chunk_a_s:chunk_a_e])
            else:
                chunk_a_depth = None
                chunk_a_loop_depth = None
                chunk_a_depth_conf = None
                chunk_a_loop_depth_conf = None

            s_a, R_a, t_a = self.align_2pcds(
                point_map_a,
                conf_a,
                point_map_loop_a,
                conf_loop,
                chunk_a_depth,
                chunk_a_loop_depth,
                chunk_a_depth_conf,
                chunk_a_loop_depth_conf,
            )

            print("chunk_b align")

            point_map_loop_b = point_map_loop_org[chunk_b_s:chunk_b_e]
            conf_loop = item[1].conf[chunk_b_s:chunk_b_e]
            print(self.chunk_indices[chunk_idx_b])
            print(chunk_b_range)
            print(chunk_b_rela_begin, chunk_b_rela_end)
            chunk_data_b = np.load(
                os.path.join(self.result_unaligned_dir, f"chunk_{chunk_idx_b}.npy"),
                allow_pickle=True,
            ).item()

            point_map_b = depth_to_point_cloud_vectorized(
                chunk_data_b.depth, chunk_data_b.intrinsics, chunk_data_b.extrinsics
            )
            point_map_b = point_map_b[chunk_b_rela_begin:chunk_b_rela_end]
            conf_b = chunk_data_b.conf[chunk_b_rela_begin:chunk_b_rela_end]

            if self.config["Model"]["align_method"] == "scale+se3":
                chunk_b_depth = np.squeeze(chunk_data_b.depth[chunk_b_rela_begin:chunk_b_rela_end])
                chunk_b_depth_conf = np.squeeze(
                    chunk_data_b.conf[chunk_b_rela_begin:chunk_b_rela_end]
                )
                chunk_b_loop_depth = np.squeeze(item[1].depth[chunk_b_s:chunk_b_e])
                chunk_b_loop_depth_conf = np.squeeze(item[1].conf[chunk_b_s:chunk_b_e])
            else:
                chunk_b_depth = None
                chunk_b_loop_depth = None
                chunk_b_depth_conf = None
                chunk_b_loop_depth_conf = None

            s_b, R_b, t_b = self.align_2pcds(
                point_map_b,
                conf_b,
                point_map_loop_b,
                conf_loop,
                chunk_b_depth,
                chunk_b_loop_depth,
                chunk_b_depth_conf,
                chunk_b_loop_depth_conf,
            )

            print("a -> b SIM 3")
            s_ab, R_ab, t_ab = compute_sim3_ab((s_a, R_a, t_a), (s_b, R_b, t_b))
            print("Estimated Scale:", s_ab)
            print("Estimated Rotation:\n", R_ab)
            print("Estimated Translation:", t_ab)

            loop_sim3_list.append((chunk_idx_a, chunk_idx_b, (s_ab, R_ab, t_ab)))

        return loop_sim3_list

    def plot_loop_closure(
        self, input_abs_poses, optimized_abs_poses, save_name="sim3_opt_result.png"
    ):
        def extract_xyz(pose_tensor):
            poses = pose_tensor.cpu().numpy()
            return poses[:, 0], poses[:, 1], poses[:, 2]

        x0, _, y0 = extract_xyz(input_abs_poses)
        x1, _, y1 = extract_xyz(optimized_abs_poses)

        # Visual in png format
        plt.figure(figsize=(8, 6))
        plt.plot(x0, y0, "o--", alpha=0.45, label="Before Optimization")
        plt.plot(x1, y1, "o-", label="After Optimization")
        for i, j, _ in self.loop_sim3_list:
            plt.plot(
                [x0[i], x0[j]],
                [y0[i], y0[j]],
                "r--",
                alpha=0.25,
                label="Loop (Before)" if i == 5 else "",
            )
            plt.plot(
                [x1[i], x1[j]],
                [y1[i], y1[j]],
                "g-",
                alpha=0.25,
                label="Loop (After)" if i == 5 else "",
            )
        plt.gca().set_aspect("equal")
        plt.title("Sim3 Loop Closure Optimization")
        plt.xlabel("x")
        plt.ylabel("z")
        plt.legend()
        plt.grid(True)
        plt.axis("equal")
        save_path = os.path.join(self.output_dir, save_name)
        plt.savefig(save_path, dpi=300, bbox_inches="tight")
        plt.close()

    def process_long_sequence(self):
        if self.overlap >= self.chunk_size:
            raise ValueError(
                f"[SETTING ERROR] Overlap ({self.overlap}) \
                    must be less than chunk size ({self.chunk_size})"
            )

        self.chunk_indices, num_chunks = self.get_chunk_indices()

        print(
            f"Processing {len(self.img_list)} images in {num_chunks} \
                chunks of size {self.chunk_size} with {self.overlap} overlap"
        )

        pre_predictions = None
        for chunk_idx in range(len(self.chunk_indices)):
            print(f"[Progress]: {chunk_idx}/{len(self.chunk_indices)}")
            cur_predictions = self.process_single_chunk(
                self.chunk_indices[chunk_idx], chunk_idx=chunk_idx
            )
            torch.cuda.empty_cache()

            if chunk_idx > 0:
                print(
                    f"Aligning {chunk_idx-1} and {chunk_idx} (Total {len(self.chunk_indices)-1})"
                )
                chunk_data1 = pre_predictions
                chunk_data2 = cur_predictions

                point_map1 = depth_to_point_cloud_vectorized(
                    chunk_data1.depth, chunk_data1.intrinsics, chunk_data1.extrinsics
                )
                point_map2 = depth_to_point_cloud_vectorized(
                    chunk_data2.depth, chunk_data2.intrinsics, chunk_data2.extrinsics
                )

                point_map1 = point_map1[-self.overlap :]
                point_map2 = point_map2[: self.overlap]
                conf1 = chunk_data1.conf[-self.overlap :]
                conf2 = chunk_data2.conf[: self.overlap]

                if self.config["Model"]["align_method"] == "scale+se3":
                    chunk1_depth = np.squeeze(chunk_data1.depth[-self.overlap :])
                    chunk2_depth = np.squeeze(chunk_data2.depth[: self.overlap])
                    chunk1_depth_conf = np.squeeze(chunk_data1.conf[-self.overlap :])
                    chunk2_depth_conf = np.squeeze(chunk_data2.conf[: self.overlap])
                else:
                    chunk1_depth = None
                    chunk2_depth = None
                    chunk1_depth_conf = None
                    chunk2_depth_conf = None

                s, R, t = self.align_2pcds(
                    point_map1,
                    conf1,
                    point_map2,
                    conf2,
                    chunk1_depth,
                    chunk2_depth,
                    chunk1_depth_conf,
                    chunk2_depth_conf,
                )
                self.sim3_list.append((s, R, t))

            pre_predictions = cur_predictions

        if self.loop_enable:
            self.loop_list = self.get_loop_pairs()
            del self.loop_detector  # Save GPU Memory

            torch.cuda.empty_cache()

            print("Loop SIM(3) estimating...")
            loop_results = process_loop_list(
                self.chunk_indices,
                self.loop_list,
                half_window=int(self.config["Model"]["loop_chunk_size"] / 2),
            )
            loop_results = remove_duplicates(loop_results)
            print(loop_results)
            # return e.g. (31, (1574, 1594), 2, (129, 149))
            for item in loop_results:
                single_chunk_predictions = self.process_single_chunk(
                    item[1], range_2=item[3], is_loop=True
                )

                self.loop_predict_list.append((item, single_chunk_predictions))
                print(item)

            self.loop_sim3_list = self.get_loop_sim3_from_loop_predict(self.loop_predict_list)

            input_abs_poses = self.loop_optimizer.sequential_to_absolute_poses(
                self.sim3_list
            )  # just for plot
            self.sim3_list = self.loop_optimizer.optimize(self.sim3_list, self.loop_sim3_list)
            optimized_abs_poses = self.loop_optimizer.sequential_to_absolute_poses(
                self.sim3_list
            )  # just for plot

            self.plot_loop_closure(
                input_abs_poses, optimized_abs_poses, save_name="sim3_opt_result.png"
            )

        print("Apply alignment")
        self.sim3_list = accumulate_sim3_transforms(self.sim3_list)
        for chunk_idx in range(len(self.chunk_indices) - 1):
            print(f"Applying {chunk_idx+1} -> {chunk_idx} (Total {len(self.chunk_indices)-1})")
            s, R, t = self.sim3_list[chunk_idx]

            chunk_data = np.load(
                os.path.join(self.result_unaligned_dir, f"chunk_{chunk_idx+1}.npy"),
                allow_pickle=True,
            ).item()

            aligned_chunk_data = {}

            aligned_chunk_data["world_points"] = depth_to_point_cloud_optimized_torch(
                chunk_data.depth, chunk_data.intrinsics, chunk_data.extrinsics
            )
            aligned_chunk_data["world_points"] = apply_sim3_direct_torch(
                aligned_chunk_data["world_points"], s, R, t
            )

            aligned_chunk_data["conf"] = chunk_data.conf
            aligned_chunk_data["images"] = chunk_data.processed_images

            aligned_path = os.path.join(self.result_aligned_dir, f"chunk_{chunk_idx+1}.npy")
            np.save(aligned_path, aligned_chunk_data)

            if chunk_idx == 0:
                chunk_data_first = np.load(
                    os.path.join(self.result_unaligned_dir, "chunk_0.npy"), allow_pickle=True
                ).item()
                np.save(os.path.join(self.result_aligned_dir, "chunk_0.npy"), chunk_data_first)
                points_first = depth_to_point_cloud_vectorized(
                    chunk_data_first.depth,
                    chunk_data_first.intrinsics,
                    chunk_data_first.extrinsics,
                )
                colors_first = chunk_data_first.processed_images
                confs_first = chunk_data_first.conf
                ply_path_first = os.path.join(self.pcd_dir, "0_pcd.ply")
                save_confident_pointcloud_batch(
                    points=points_first,  # shape: (H, W, 3)
                    colors=colors_first,  # shape: (H, W, 3)
                    confs=confs_first,  # shape: (H, W)
                    output_path=ply_path_first,
                    conf_threshold=np.mean(confs_first)
                    * self.config["Model"]["Pointcloud_Save"]["conf_threshold_coef"],
                    sample_ratio=self.config["Model"]["Pointcloud_Save"]["sample_ratio"],
                )
                if self.config["Model"]["save_depth_conf_result"]:
                    predictions = chunk_data_first
                    self.save_depth_conf_result(predictions, 0, 1, np.eye(3), np.array([0, 0, 0]))

            points = aligned_chunk_data["world_points"].reshape(-1, 3)
            colors = (aligned_chunk_data["images"].reshape(-1, 3)).astype(np.uint8)
            confs = aligned_chunk_data["conf"].reshape(-1)
            ply_path = os.path.join(self.pcd_dir, f"{chunk_idx+1}_pcd.ply")
            save_confident_pointcloud_batch(
                points=points,  # shape: (H, W, 3)
                colors=colors,  # shape: (H, W, 3)
                confs=confs,  # shape: (H, W)
                output_path=ply_path,
                conf_threshold=np.mean(confs)
                * self.config["Model"]["Pointcloud_Save"]["conf_threshold_coef"],
                sample_ratio=self.config["Model"]["Pointcloud_Save"]["sample_ratio"],
            )

            if self.config["Model"]["save_depth_conf_result"]:
                predictions = chunk_data
                predictions.depth *= s
                self.save_depth_conf_result(predictions, chunk_idx + 1, s, R, t)

        self.save_camera_poses()

        print("Done.")

    def run(self):
        print(f"Loading images from {self.img_dir}...")
        self.img_list = sorted(
            glob.glob(os.path.join(self.img_dir, "*.jpg"))
            + glob.glob(os.path.join(self.img_dir, "*.png"))
        )
        # print(self.img_list)
        if len(self.img_list) == 0:
            raise ValueError(f"[DIR EMPTY] No images found in {self.img_dir}!")
        print(f"Found {len(self.img_list)} images")

        self.process_long_sequence()

    def save_camera_poses(self):
        """
        Save camera poses from all chunks to txt and ply files
        - txt file: Each line contains a 4x4 C2W matrix flattened into 16 numbers
        - ply file: Camera poses visualized as points with different colors for each chunk
        """
        chunk_colors = [
            [255, 0, 0],  # Red
            [0, 255, 0],  # Green
            [0, 0, 255],  # Blue
            [255, 255, 0],  # Yellow
            [255, 0, 255],  # Magenta
            [0, 255, 255],  # Cyan
            [128, 0, 0],  # Dark Red
            [0, 128, 0],  # Dark Green
            [0, 0, 128],  # Dark Blue
            [128, 128, 0],  # Olive
        ]
        print("Saving all camera poses to txt file...")

        all_poses = [None] * len(self.img_list)
        all_intrinsics = [None] * len(self.img_list)

        first_chunk_range, first_chunk_extrinsics = self.all_camera_poses[0]
        _, first_chunk_intrinsics = self.all_camera_intrinsics[0]

        for i, idx in enumerate(
            range(first_chunk_range[0], first_chunk_range[1] - self.overlap_e)
        ):
            w2c = np.eye(4)
            w2c[:3, :] = first_chunk_extrinsics[i]
            c2w = np.linalg.inv(w2c)
            all_poses[idx] = c2w
            all_intrinsics[idx] = first_chunk_intrinsics[i]

        for chunk_idx in range(1, len(self.all_camera_poses)):
            chunk_range, chunk_extrinsics = self.all_camera_poses[chunk_idx]
            _, chunk_intrinsics = self.all_camera_intrinsics[chunk_idx]
            s, R, t = self.sim3_list[
                chunk_idx - 1
            ]  # When call self.save_camera_poses(), all the sim3 are aligned to the first chunk.

            S = np.eye(4)
            S[:3, :3] = s * R
            S[:3, 3] = t

            chunk_range_end = (
                chunk_range[1] - self.overlap_e
                if chunk_idx < len(self.all_camera_poses) - 1
                else chunk_range[1]
            )

            for i, idx in enumerate(range(chunk_range[0] + self.overlap_s, chunk_range_end)):
                w2c = np.eye(4)
                w2c[:3, :] = chunk_extrinsics[i + self.overlap_s]
                c2w = np.linalg.inv(w2c)

                transformed_c2w = S @ c2w  # Be aware of the left multiplication!
                transformed_c2w[:3, :3] /= s  # Normalize rotation

                all_poses[idx] = transformed_c2w
                all_intrinsics[idx] = chunk_intrinsics[i + self.overlap_s]

        poses_path = os.path.join(self.output_dir, "camera_poses.txt")
        with open(poses_path, "w") as f:
            for pose in all_poses:
                flat_pose = pose.flatten()
                f.write(" ".join([str(x) for x in flat_pose]) + "\n")

        print(f"Camera poses saved to {poses_path}")

        intrinsics_path = os.path.join(self.output_dir, "intrinsic.txt")
        with open(intrinsics_path, "w") as f:
            for intrinsic in all_intrinsics:
                fx = intrinsic[0, 0]
                fy = intrinsic[1, 1]
                cx = intrinsic[0, 2]
                cy = intrinsic[1, 2]
                f.write(f"{fx} {fy} {cx} {cy}\n")

        print(f"Camera intrinsics saved to {intrinsics_path}")

        ply_path = os.path.join(self.output_dir, "camera_poses.ply")
        with open(ply_path, "w") as f:
            # Write PLY header
            f.write("ply\n")
            f.write("format ascii 1.0\n")
            f.write(f"element vertex {len(all_poses)}\n")
            f.write("property float x\n")
            f.write("property float y\n")
            f.write("property float z\n")
            f.write("property uchar red\n")
            f.write("property uchar green\n")
            f.write("property uchar blue\n")
            f.write("end_header\n")

            color = chunk_colors[0]
            for pose in all_poses:
                position = pose[:3, 3]
                f.write(
                    f"{position[0]} {position[1]} {position[2]} {color[0]} {color[1]} {color[2]}\n"
                )

        print(f"Camera poses visualization saved to {ply_path}")

    def close(self):
        """
        Clean up temporary files and calculate reclaimed disk space.

        This method deletes all temporary files generated during processing from three directories:
        - Unaligned results
        - Aligned results
        - Loop results

        ~50 GiB for 4500-frame KITTI 00,
        ~35 GiB for 2700-frame KITTI 05,
        or ~5 GiB for 300-frame short seq.
        """
        if not self.delete_temp_files:
            return

        total_space = 0

        print(f"Deleting the temp files under {self.result_unaligned_dir}")
        for filename in os.listdir(self.result_unaligned_dir):
            file_path = os.path.join(self.result_unaligned_dir, filename)
            if os.path.isfile(file_path):
                total_space += os.path.getsize(file_path)
                os.remove(file_path)

        print(f"Deleting the temp files under {self.result_aligned_dir}")
        for filename in os.listdir(self.result_aligned_dir):
            file_path = os.path.join(self.result_aligned_dir, filename)
            if os.path.isfile(file_path):
                total_space += os.path.getsize(file_path)
                os.remove(file_path)

        print(f"Deleting the temp files under {self.result_loop_dir}")
        for filename in os.listdir(self.result_loop_dir):
            file_path = os.path.join(self.result_loop_dir, filename)
            if os.path.isfile(file_path):
                total_space += os.path.getsize(file_path)
                os.remove(file_path)
        print("Deleting temp files done.")

        print(f"Saved disk space: {total_space/1024/1024/1024:.4f} GiB")


def copy_file(src_path, dst_dir):
    try:
        os.makedirs(dst_dir, exist_ok=True)

        dst_path = os.path.join(dst_dir, os.path.basename(src_path))

        shutil.copy2(src_path, dst_path)
        print(f"config yaml file has been copied to: {dst_path}")
        return dst_path

    except FileNotFoundError:
        print("File Not Found")
    except PermissionError:
        print("Permission Error")
    except Exception as e:
        print(f"Copy Error: {e}")


if __name__ == "__main__":

    parser = argparse.ArgumentParser(description="DA3-Streaming")
    parser.add_argument("--image_dir", type=str, required=True, help="Image path")
    parser.add_argument(
        "--config",
        type=str,
        required=False,
        default="./configs/base_config.yaml",
        help="Image path",
    )
    parser.add_argument("--output_dir", type=str, required=False, default=None, help="Output path")
    args = parser.parse_args()

    config = load_config(args.config)

    image_dir = args.image_dir
    path = image_dir.split("/")

    if args.output_dir is not None:
        save_dir = args.output_dir
    else:
        current_datetime = datetime.now().strftime("%Y-%m-%d-%H-%M-%S")
        exp_dir = "./exps"
        save_dir = os.path.join(exp_dir, image_dir.replace("/", "_"), current_datetime)

    if not os.path.exists(save_dir):
        os.makedirs(save_dir)
        print(f"The exp will be saved under dir: {save_dir}")
        copy_file(args.config, save_dir)

    if config["Model"]["align_lib"] == "numba":
        warmup_numba()

    da3_streaming = DA3_Streaming(image_dir, save_dir, config)
    da3_streaming.run()
    da3_streaming.close()

    del da3_streaming
    torch.cuda.empty_cache()
    gc.collect()

    all_ply_path = os.path.join(save_dir, "pcd/combined_pcd.ply")
    input_dir = os.path.join(save_dir, "pcd")
    print("Saving all the point clouds")
    merge_ply_files(input_dir, all_ply_path)
    print("DA3-Streaming done.")
    sys.exit()



================================================
FILE: da3_streaming/npz_output_process.py
================================================
import argparse
import os
from glob import glob
import numpy as np
from loop_utils.sim3utils import save_confident_pointcloud_batch

from da3_streaming import depth_to_point_cloud_vectorized


def read_camera_poses(pose_file):
    poses = []
    with open(pose_file) as f:
        for line in f:
            if line.strip():
                numbers = list(map(float, line.strip().split()))
                if len(numbers) == 16:
                    pose = np.array(numbers).reshape(4, 4)
                    poses.append(pose)
    return poses


def create_point_cloud(npz_folder, pose_file, output_ply, conf_threshold_coef, sample_ratio=1.0):

    poses = read_camera_poses(pose_file)
    print(f"Read {len(poses)} camera poses")

    npz_files = sorted(glob(os.path.join(npz_folder, "frame_*.npz")))
    npz_files = [f for f in npz_files if os.path.basename(f).startswith("frame_")]

    npz_files.sort(key=lambda x: int(os.path.basename(x).split("_")[1].split(".")[0]))

    print(f"Found {len(npz_files)} .npz files")

    assert len(poses) == len(
        npz_files
    ), f"Pose file has {len(poses)} lines, but npz folder has {len(npz_files)} files"

    all_points = []
    all_colors = []
    all_confs = []

    for idx, (npz_path, c2w) in enumerate(zip(npz_files, poses)):
        if idx % 50 == 0:
            print(f"Processing frame {idx}/{len(npz_files)}...")

        data = np.load(npz_path)

        image = data["image"]  # [H, W, 3] uint8
        depth = data["depth"]  # [H, W] float32
        conf = data["conf"]  # [H, W] float32
        intrinsics = data["intrinsics"]  # [3, 3] float32

        depth_reshaped = depth[np.newaxis, :, :]  # [1, H, W]
        intrinsics_reshaped = intrinsics[np.newaxis, :, :]  # [1, 3, 3]

        w2c = np.linalg.inv(c2w)
        extrinsics = w2c[:3, :]  # [3, 4]
        extrinsics_reshaped = extrinsics[np.newaxis, :, :]  # [1, 3, 4]

        points_world = depth_to_point_cloud_vectorized(
            depth_reshaped, intrinsics_reshaped, extrinsics_reshaped
        )
        points_world = points_world[0]  # [H, W, 3]

        all_points.append(points_world)
        all_colors.append(image)
        all_confs.append(conf)

    if not all_points:
        print("No valid point cloud data found!")
        return

    points_combined = np.stack(all_points, axis=0)  # [b, H, W, 3]
    colors_combined = np.stack(all_colors, axis=0)  # [b, H, W, 3]
    confs_combined = np.stack(all_confs, axis=0)  # [b, H, W]

    conf_threshold = np.mean(confs_combined) * conf_threshold_coef

    print(
        f"Original point cloud contains \
            {points_combined.shape[0] * points_combined.shape[1] * points_combined.shape[2]} points"
    )

    save_confident_pointcloud_batch(
        points=points_combined,
        colors=colors_combined,
        confs=confs_combined,
        output_path=output_ply,
        conf_threshold=conf_threshold,
        sample_ratio=sample_ratio,
        batch_size=1000000,
    )

    print(f"Downsampled point cloud saved to: {output_ply}")


def main():
    parser = argparse.ArgumentParser(description="Create point cloud from DA3-Long output")
    parser.add_argument("--npz_folder", type=str, required=True, help="Path to npz folder")
    parser.add_argument("--pose_file", type=str, required=True, help="Path to pose file")
    parser.add_argument(
        "--output_file", type=str, default="output.ply", help="Path to output PLY file"
    )
    parser.add_argument(
        "--conf_threshold_coef", type=float, default=0.5, help="Confidence threshold coefficient"
    )
    parser.add_argument(
        "--sample_ratio", type=float, default=0.015, help="Sample ratio for downsampling"
    )

    args = parser.parse_args()

    npz_folder = args.npz_folder
    pose_file = args.pose_file
    output_file = args.output_file

    conf_threshold_coef = (
        args.conf_threshold_coef
    )  # conf_threshold = np.mean(confs) * conf_threshold_coef
    sample_ratio = args.sample_ratio

    if not os.path.exists(npz_folder):
        print(f"Error: Folder {npz_folder} does not exist")
        return

    if not os.path.exists(pose_file):
        print(f"Error: File {pose_file} does not exist")
        return

    output_dir = os.path.dirname(output_file)
    if not os.path.exists(output_dir):
        os.makedirs(output_dir)

    create_point_cloud(
        npz_folder=npz_folder,
        pose_file=pose_file,
        output_ply=output_file,
        conf_threshold_coef=conf_threshold_coef,
        sample_ratio=sample_ratio,
    )


if __name__ == "__main__":
    main()



================================================
FILE: da3_streaming/requirements.txt
================================================
faiss-gpu
pandas
prettytable
einops
safetensors
numba
pypose



================================================
FILE: da3_streaming/configs/base_config.yaml
================================================
Weights:
  DA3: './weights/model.safetensors'
  DA3_CONFIG: './weights/config.json'
  SALAD: './weights/dino_salad.ckpt'

Model:
  chunk_size: 120
  overlap: 60
  loop_chunk_size: 20 # imgs of loop chunk = 2 * loop_chunk_size
  loop_enable: True
  useDBoW: False
  delete_temp_files: True
  align_lib: 'triton' # choose among 'triton' (GPU), 'torch' (GPU), 'numba' (CPU) or 'numpy' (CPU)
  align_method: 'sim3' # choose among 'sim3', 'se3' or 'scale+se3'
  scale_compute_method: 'auto' # choose among 'auto', 'ransac' or 'weighted'. It is used when align_method == 'scale+se3'
  align_type: 'dense' # choose between 'dense' or 'sparse'. Sparse align is constructing, not avaible for now

  ref_view_strategy: 'saddle_balanced' # 'middle', 'saddle_balanced', 'first' or 'saddle_sim_range'
  ref_view_strategy_loop: 'saddle_balanced' # 'middle', 'saddle_balanced', 'first' or 'saddle_sim_range'
  depth_threshold: 15.0

  save_depth_conf_result: True
  save_debug_info: False

  Sparse_Align:
    keypoint_select: 'orb' # choose among 'orb', 'fast' or 'disk'
    keypoint_num: 5000

  IRLS:
    delta: 0.1
    max_iters: 5
    tol: 1e-9

  Pointcloud_Save:
    sample_ratio: 0.015
    conf_threshold_coef: 0.75 # conf_threshold = np.mean(confs) * conf_threshold_coef

Loop:
  SALAD:
    image_size: [336, 336]
    batch_size: 32
    similarity_threshold: 0.85
    top_k: 5
    use_nms: True
    nms_threshold: 25

  SIM3_Optimizer:
    lang_version: 'cpp'
    # choose between 'cpp' or 'python'. will auto set 'python' if c++ version has not installed
    max_iterations: 30
    lambda_init: 1e-6



================================================
FILE: da3_streaming/configs/kitti.yaml
================================================
Weights:
  DA3: './weights/model.safetensors'
  DA3_CONFIG: './weights/config.json'
  SALAD: './weights/dino_salad.ckpt'

Model:
  chunk_size: 120
  overlap: 60
  loop_chunk_size: 20 # imgs of loop chunk = 2 * loop_chunk_size
  loop_enable: True
  useDBoW: False
  delete_temp_files: True
  align_lib: 'triton' # choose among 'triton' (GPU), 'torch' (GPU), 'numba' (CPU) or 'numpy' (CPU)
  align_method: 'sim3' # choose among 'sim3', 'se3' or 'scale+se3'
  scale_compute_method: 'auto' # choose among 'auto', 'ransac' or 'weighted'. It is used when align_method == 'scale+se3'
  align_type: 'dense' # choose between 'dense' or 'sparse'. Sparse align is constructing, not avaible for now

  ref_view_strategy: 'middle' # 'middle', 'saddle_balanced', 'first' or 'saddle_sim_range'
  ref_view_strategy_loop: 'saddle_balanced' # 'middle', 'saddle_balanced', 'first' or 'saddle_sim_range'
  depth_threshold: 15.0

  save_depth_conf_result: True
  save_debug_info: False

  Sparse_Align:
    keypoint_select: 'orb' # choose among 'orb', 'fast' or 'disk'
    keypoint_num: 5000

  IRLS:
    delta: 0.1
    max_iters: 5
    tol: 1e-9

  Pointcloud_Save:
    sample_ratio: 0.015
    conf_threshold_coef: 0.75 # conf_threshold = np.mean(confs) * conf_threshold_coef

Loop:
  SALAD:
    image_size: [336, 336]
    batch_size: 32
    similarity_threshold: 0.85
    top_k: 5
    use_nms: True
    nms_threshold: 25

  SIM3_Optimizer:
    lang_version: 'cpp'
    # choose between 'cpp' or 'python'. will auto set 'python' if c++ version has not installed
    max_iterations: 30
    lambda_init: 1e-6



================================================
FILE: da3_streaming/configs/tum.yaml
================================================
Weights:
  DA3: './weights/model.safetensors'
  DA3_CONFIG: './weights/config.json'
  SALAD: './weights/dino_salad.ckpt'

Model:
  chunk_size: 120
  overlap: 60
  loop_chunk_size: 20 # imgs of loop chunk = 2 * loop_chunk_size
  loop_enable: True
  useDBoW: False
  delete_temp_files: True
  align_lib: 'triton' # choose among 'triton' (GPU), 'torch' (GPU), 'numba' (CPU) or 'numpy' (CPU)
  align_method: 'sim3' # choose among 'sim3', 'se3' or 'scale+se3'
  scale_compute_method: 'auto' # choose among 'auto', 'ransac' or 'weighted'. It is used when align_method == 'scale+se3'
  align_type: 'dense' # choose between 'dense' or 'sparse'. Sparse align is constructing, not avaible for now

  ref_view_strategy: 'saddle_balanced' # 'middle', 'saddle_balanced', 'first' or 'saddle_sim_range'
  ref_view_strategy_loop: 'saddle_balanced' # 'middle', 'saddle_balanced', 'first' or 'saddle_sim_range'
  depth_threshold: 15.0

  save_depth_conf_result: True
  save_debug_info: False

  Sparse_Align:
    keypoint_select: 'orb' # choose among 'orb', 'fast' or 'disk'
    keypoint_num: 5000

  IRLS:
    delta: 0.1
    max_iters: 5
    tol: 1e-9

  Pointcloud_Save:
    sample_ratio: 0.015
    conf_threshold_coef: 0.75 # conf_threshold = np.mean(confs) * conf_threshold_coef

Loop:
  SALAD:
    image_size: [336, 336]
    batch_size: 32
    similarity_threshold: 0.85
    top_k: 5
    use_nms: True
    nms_threshold: 25

  SIM3_Optimizer:
    lang_version: 'cpp'
    # choose between 'cpp' or 'python'. will auto set 'python' if c++ version has not installed
    max_iterations: 30
    lambda_init: 1e-6



================================================
FILE: da3_streaming/fastloop/__init__.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
# Adapted from [VGGT-Long](https://github.com/DengKaiCQ/VGGT-Long)



================================================
FILE: da3_streaming/fastloop/solve.cpp
================================================
// Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
//
// Licensed under the Apache License, Version 2.0 (the "License");
// you may not use this file except in compliance with the License.
// You may obtain a copy of the License at
//
//   http://www.apache.org/licenses/LICENSE-2.0
//
// Unless required by applicable law or agreed to in writing, software
// distributed under the License is distributed on an "AS IS" BASIS,
// WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
// See the License for the specific language governing permissions and
// limitations under the License.
//
// Adapted from [VGGT-Long](https://github.com/DengKaiCQ/VGGT-Long)

#include <torch/extension.h>
#include <vector>
#include <unordered_map>
#include <algorithm>
#include <iostream>
#include <Eigen/Core>
#include <Eigen/Sparse>

typedef Eigen::SparseMatrix<double> SpMat;
typedef Eigen::Triplet<double> T;

Eigen::VectorXd solve(const SpMat &A, const Eigen::VectorXd &b, int freen){

  if (freen < 0){
    const Eigen::SimplicialCholesky<SpMat> chol(A);
    return chol.solve(b); // n x 1
  }

  const SpMat A_sub = A.topLeftCorner(freen, freen);
  const Eigen::VectorXd b_sub = b.topRows(freen);
  const Eigen::VectorXd delta = solve(A_sub, b_sub, -7);

  Eigen::VectorXd delta2(b.rows());
  delta2.setZero();
  delta2.topRows(freen) = delta;

  return delta2;
}

std::vector<torch::Tensor> solve_system(torch::Tensor J_Ginv_i, torch::Tensor J_Ginv_j, torch::Tensor ii, torch::Tensor jj, torch::Tensor res, float ep, float lm, int freen)
{

  const torch::Device device = res.device();
  J_Ginv_i = J_Ginv_i.to(torch::kCPU);
  J_Ginv_j = J_Ginv_j.to(torch::kCPU);
  ii = ii.to(torch::kCPU);
  jj = jj.to(torch::kCPU);
  res = res.clone().to(torch::kCPU);

  const int r = res.size(0);
  const int n = std::max(ii.max().item<long>(), jj.max().item<long>()) + 1;

  res.resize_({r*7});
  float *res_ptr = res.data_ptr<float>();
  Eigen::Map<Eigen::VectorXf> v(res_ptr, r*7);

  SpMat J(r*7, n*7);
  std::vector<T> tripletList;
  tripletList.reserve(r*7*7*2);

  auto ii_acc = ii.accessor<long,1>();
  auto jj_acc = jj.accessor<long,1>();
  auto J_Ginv_i_acc = J_Ginv_i.accessor<float,3>();
  auto J_Ginv_j_acc = J_Ginv_j.accessor<float,3>();

  for (int x=0; x<r; x++){
    const int i = ii_acc[x];
    const int j = jj_acc[x];
    for (int k=0; k<7; k++){
      for (int l=0; l<7; l++){
        if (i == j)
          exit(1);
        const float val_i = J_Ginv_i_acc[x][k][l];
        tripletList.emplace_back(x*7 + k, i*7 + l, val_i);
        const float val_j = J_Ginv_j_acc[x][k][l];
        tripletList.emplace_back(x*7 + k, j*7 + l, val_j);
      }
    }
  }

  J.setFromTriplets(tripletList.begin(), tripletList.end());
  const SpMat Jt = J.transpose();
  Eigen::VectorXd b = -(Jt * v.cast<double>());
  SpMat A = Jt * J;

  A.diagonal() += (A.diagonal() * lm);
  A.diagonal().array() += ep;
  Eigen::VectorXf delta = solve(A, b, freen*7).cast<float>();

  torch::Tensor delta_tensor = torch::from_blob(delta.data(), {n*7}).clone().to(device);
  delta_tensor.resize_({n, 7});
  return {delta_tensor};

  Eigen::Matrix<float, -1, -1, Eigen::RowMajor> dense_J(J.cast<float>());
  torch::Tensor dense_J_tensor = torch::from_blob(dense_J.data(), {r*7, n*7}).clone().to(device);
  dense_J_tensor.resize_({r, 7, n, 7});

  return {delta_tensor, dense_J_tensor};

}


PYBIND11_MODULE(TORCH_EXTENSION_NAME, m) {
  m.def("solve_system", &solve_system, "temporal neighboor indicies");
}



================================================
FILE: da3_streaming/fastloop/solve_python.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
# Adapted from [VGGT-Long](https://github.com/DengKaiCQ/VGGT-Long)

import numpy as np
import torch
from scipy.sparse import coo_matrix, csc_matrix
from scipy.sparse.linalg import spsolve


def solve_sparse(A: csc_matrix, b: np.ndarray, freen: int) -> np.ndarray:
    """Solve linear system A * delta = b, supports submatrix solving"""
    if freen < 0:
        return spsolve(A, b)
    else:
        A_sub = A[:freen, :freen].tocsc()
        b_sub = b[:freen]
        delta_sub = spsolve(A_sub, b_sub)
        delta = np.zeros_like(b)
        delta[:freen] = delta_sub
        return delta


def solve_system_py(
    J_Ginv_i: torch.Tensor,
    J_Ginv_j: torch.Tensor,
    ii: torch.Tensor,
    jj: torch.Tensor,
    res: torch.Tensor,
    ep: float,
    lm: float,
    freen: int,
) -> torch.Tensor:
    # Ensure all tensors are on CPU
    device = res.device
    J_Ginv_i = J_Ginv_i.cpu()
    J_Ginv_j = J_Ginv_j.cpu()
    ii = ii.cpu()
    jj = jj.cpu()
    res = res.clone().cpu()

    r = res.size(0)  # Number of edges
    n = max(ii.max().item(), jj.max().item()) + 1  # Number of nodes

    res_vec = res.view(-1).numpy().astype(np.float64)

    rows, cols, data = [], [], []
    ii_np = ii.numpy()
    jj_np = jj.numpy()
    J_Ginv_i_np = J_Ginv_i.numpy()
    J_Ginv_j_np = J_Ginv_j.numpy()

    for x in range(r):
        i = ii_np[x]
        j = jj_np[x]
        if i == j:
            raise ValueError("Self-edges are not allowed")

        for k in range(7):
            for l in range(7):
                row_idx = x * 7 + k
                col_idx_i = i * 7 + l
                val_i = J_Ginv_i_np[x, k, l]
                rows.append(row_idx)
                cols.append(col_idx_i)
                data.append(val_i)

                col_idx_j = j * 7 + l
                val_j = J_Ginv_j_np[x, k, l]
                rows.append(row_idx)
                cols.append(col_idx_j)
                data.append(val_j)

    J = coo_matrix((data, (rows, cols)), shape=(r * 7, n * 7)).tocsc()

    b_vec = -J.T @ res_vec

    A_mat = J.T @ J

    diag = A_mat.diagonal()
    new_diag = diag * (1.0 + lm) + ep
    A_mat.setdiag(new_diag)

    freen_total = freen * 7
    delta = solve_sparse(A_mat.tocsc(), b_vec, freen_total)

    delta_tensor = torch.from_numpy(delta.astype(np.float32)).view(n, 7).to(device)
    return delta_tensor



================================================
FILE: da3_streaming/loop_utils/__init__.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
# Adapted from [VGGT-Long](https://github.com/DengKaiCQ/VGGT-Long)



================================================
FILE: da3_streaming/loop_utils/alignment_torch.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
# Adapted from [VGGT-Long](https://github.com/DengKaiCQ/VGGT-Long)

import numpy as np
import torch


def weighted_estimate_se3_torch(source_points, target_points, weights):
    source_points = torch.from_numpy(source_points).cuda().float()
    target_points = torch.from_numpy(target_points).cuda().float()
    weights = torch.from_numpy(weights).cuda().float()

    total_weight = torch.sum(weights)
    if total_weight < 1e-6:
        return (
            1.0,
            np.zeros(3, dtype=np.float32),
            np.zeros(3, dtype=np.float32),
            np.zeros((3, 3), dtype=np.float32),
        )

    normalized_weights = weights / total_weight

    mu_src = torch.sum(normalized_weights[:, None] * source_points, dim=0)
    mu_tgt = torch.sum(normalized_weights[:, None] * target_points, dim=0)

    src_centered = source_points - mu_src
    tgt_centered = target_points - mu_tgt

    weighted_src = src_centered * torch.sqrt(normalized_weights)[:, None]
    weighted_tgt = tgt_centered * torch.sqrt(normalized_weights)[:, None]

    H = weighted_src.T @ weighted_tgt

    return 1.0, mu_src.cpu().numpy(), mu_tgt.cpu().numpy(), H.cpu().numpy()


def weighted_estimate_sim3_torch(source_points, target_points, weights):

    source_points = torch.from_numpy(source_points).cuda().float()
    target_points = torch.from_numpy(target_points).cuda().float()
    weights = torch.from_numpy(weights).cuda().float()

    total_weight = torch.sum(weights)
    if total_weight < 1e-6:
        return (
            -1.0,
            np.zeros(3, dtype=np.float32),
            np.zeros(3, dtype=np.float32),
            np.zeros((3, 3), dtype=np.float32),
        )

    normalized_weights = weights / total_weight

    mu_src = torch.sum(normalized_weights[:, None] * source_points, dim=0)
    mu_tgt = torch.sum(normalized_weights[:, None] * target_points, dim=0)

    src_centered = source_points - mu_src
    tgt_centered = target_points - mu_tgt

    scale_src = torch.sqrt(torch.sum(normalized_weights * torch.sum(src_centered**2, dim=1)))
    scale_tgt = torch.sqrt(torch.sum(normalized_weights * torch.sum(tgt_centered**2, dim=1)))
    s = scale_tgt / scale_src

    weighted_src = (s * src_centered) * torch.sqrt(normalized_weights)[:, None]
    weighted_tgt = tgt_centered * torch.sqrt(normalized_weights)[:, None]

    H = weighted_src.T @ weighted_tgt

    return s.cpu().numpy(), mu_src.cpu().numpy(), mu_tgt.cpu().numpy(), H.cpu().numpy()


def weighted_estimate_sim3_numba_torch(source_points, target_points, weights, align_method="sim3"):

    if align_method == "sim3":
        s, mu_src, mu_tgt, H = weighted_estimate_sim3_torch(source_points, target_points, weights)
    elif align_method == "se3" or align_method == "scale+se3":
        s, mu_src, mu_tgt, H = weighted_estimate_se3_torch(source_points, target_points, weights)

    if s < 0:
        raise ValueError("Total weight too small for meaningful estimation")

    H_torch = torch.from_numpy(H).cuda().float()
    U, _, Vt = torch.linalg.svd(H_torch)

    U = U.cpu().numpy()
    Vt = Vt.cpu().numpy()

    R = Vt.T @ U.T
    if np.linalg.det(R) < 0:
        Vt[2, :] *= -1
        R = Vt.T @ U.T

    mu_src = mu_src.astype(np.float32)
    mu_tgt = mu_tgt.astype(np.float32)
    R = R.astype(np.float32)

    if align_method == "se3" or align_method == "scale+se3":
        t = mu_tgt - R @ mu_src
    else:
        t = mu_tgt - s * R @ mu_src

    return s, R, t.astype(np.float32)


def huber_loss_torch(r, delta):

    r_torch = torch.from_numpy(r).cuda().float()
    delta_torch = torch.tensor(delta, device="cuda", dtype=torch.float32)

    abs_r = torch.abs(r_torch)
    result = torch.where(
        abs_r <= delta_torch, 0.5 * r_torch**2, delta_torch * (abs_r - 0.5 * delta_torch)
    )

    return result.cpu().numpy()


def compute_residuals_torch(tgt, transformed):

    tgt_torch = torch.from_numpy(tgt).cuda().float()
    transformed_torch = torch.from_numpy(transformed).cuda().float()

    residuals = torch.sqrt(torch.sum((tgt_torch - transformed_torch) ** 2, dim=1))
    return residuals.cpu().numpy()


def compute_huber_weights_torch(residuals, delta):

    residuals_torch = torch.from_numpy(residuals).cuda().float()
    delta_torch = torch.tensor(delta, device="cuda", dtype=torch.float32)

    weights = torch.ones_like(residuals_torch)
    mask = residuals_torch > delta_torch
    weights[mask] = delta_torch / residuals_torch[mask]

    return weights.cpu().numpy()


def apply_transformation_torch(src, s, R, t):

    src_torch = torch.from_numpy(src).cuda().float()
    R_torch = torch.from_numpy(R).cuda().float()
    t_torch = torch.from_numpy(t).cuda().float()
    s_torch = torch.tensor(s, device="cuda", dtype=torch.float32)

    transformed = s_torch * (src_torch @ R_torch.T) + t_torch
    return transformed.cpu().numpy()


def robust_weighted_estimate_sim3_torch(
    src, tgt, init_weights, delta=0.1, max_iters=20, tol=1e-9, align_method="sim3"
):

    src = src.astype(np.float32)
    tgt = tgt.astype(np.float32)
    init_weights = init_weights.astype(np.float32)

    s, R, t = weighted_estimate_sim3_numba_torch(src, tgt, init_weights, align_method=align_method)

    prev_error = float("inf")

    for iter in range(max_iters):
        transformed = apply_transformation_torch(src, s, R, t)
        residuals = compute_residuals_torch(tgt, transformed)

        print(f"Iter {iter}: Mean residual = {np.mean(residuals):.6f}")

        huber_weights = compute_huber_weights_torch(residuals, delta)
        combined_weights = init_weights * huber_weights
        combined_weights /= np.sum(combined_weights) + 1e-12

        s_new, R_new, t_new = weighted_estimate_sim3_numba_torch(
            src, tgt, combined_weights, align_method=align_method
        )

        param_change = np.abs(s_new - s) + np.linalg.norm(t_new - t)
        rot_angle = np.arccos(min(1.0, max(-1.0, (np.trace(R_new @ R.T) - 1) / 2)))

        current_error = np.sum(huber_loss_torch(residuals, delta) * init_weights)

        if (param_change < tol and rot_angle < np.radians(0.1)) or (
            abs(prev_error - current_error) < tol * prev_error
        ):
            print(f"Converged at iteration {iter}")
            break

        s, R, t = s_new, R_new, t_new
        prev_error = current_error

    return s, R, t


def apply_sim3_direct_torch(point_maps, s, R, t, device=None):
    """
    PyTorch SIM3
    point_maps: (b, h, w, 3) numpy array
    s: scalar or (b,) array
    R: (3, 3) or (b, 3, 3) numpy array
    t: (3,) or (b, 3) numpy array
    """
    if isinstance(point_maps, np.ndarray):
        point_maps_torch = torch.from_numpy(point_maps).float()
        R_torch = torch.from_numpy(R).float()
        t_torch = torch.from_numpy(t).float()
        s_torch = torch.tensor(s).float() if np.isscalar(s) else torch.from_numpy(s).float()
    else:
        point_maps_torch = point_maps
        R_torch = R
        t_torch = t
        s_torch = s

    if device is not None:
        point_maps_torch = point_maps_torch.to(device)
        R_torch = R_torch.to(device)
        t_torch = t_torch.to(device)
        s_torch = s_torch.to(device)

    b, h, w, c = point_maps_torch.shape

    points_flat = point_maps_torch.reshape(b, -1, 3)  # (b, h*w, 3)

    if R_torch.dim() == 2:
        R_torch = R_torch.unsqueeze(0).expand(b, 3, 3)  # (b, 3, 3)

    if t_torch.dim() == 1:
        t_torch = t_torch.unsqueeze(0).expand(b, 3)  # (b, 3)

    if s_torch.dim() == 0:
        s_torch = s_torch.unsqueeze(0).expand(b)  # (b,)

    rotated_flat = torch.bmm(points_flat, R_torch.transpose(1, 2))  # (b, h*w, 3)

    transformed_flat = s_torch[:, None, None] * rotated_flat + t_torch[:, None, :]

    transformed = transformed_flat.reshape(b, h, w, 3)

    if isinstance(point_maps, np.ndarray):
        return transformed.cpu().numpy()
    return transformed


def depth_to_point_cloud_optimized_torch(depth, intrinsics, extrinsics, device=None):

    input_is_numpy = isinstance(depth, np.ndarray)

    if input_is_numpy:
        depth_tensor = torch.from_numpy(depth).float()
        intrinsics_tensor = torch.from_numpy(intrinsics).float()
        extrinsics_tensor = torch.from_numpy(extrinsics).float()
    else:
        depth_tensor = depth
        intrinsics_tensor = intrinsics
        extrinsics_tensor = extrinsics

    if device is not None:
        depth_tensor = depth_tensor.to(device)
        intrinsics_tensor = intrinsics_tensor.to(device)
        extrinsics_tensor = extrinsics_tensor.to(device)

    N, H, W = depth_tensor.shape
    device = depth_tensor.device

    u = torch.arange(W, device=device, dtype=torch.float32).view(1, 1, W)
    v = torch.arange(H, device=device, dtype=torch.float32).view(1, H, 1)

    u_expanded = u.expand(N, H, W)
    v_expanded = v.expand(N, H, W)

    ones = torch.ones((N, H, W), device=device)
    pixel_coords = torch.stack([u_expanded, v_expanded, ones], dim=-1)  # [N, H, W, 3]

    intrinsics_inv = torch.inverse(intrinsics_tensor)  # [N, 3, 3]

    camera_coords = torch.einsum("nij,nhwj->nhwi", intrinsics_inv, pixel_coords)

    camera_coords = camera_coords * depth_tensor.unsqueeze(-1)  # [N, H, W, 3]

    camera_coords_homo = torch.cat(
        [camera_coords, torch.ones((N, H, W, 1), device=device)], dim=-1
    )

    extrinsics_4x4 = torch.zeros(N, 4, 4, device=device)
    extrinsics_4x4[:, :3, :4] = extrinsics_tensor
    extrinsics_4x4[:, 3, 3] = 1.0

    c2w = torch.inverse(extrinsics_4x4)  # [N, 4, 4]

    world_coords_homo = torch.einsum("nij,nhwj->nhwi", c2w, camera_coords_homo)
    point_cloud_world = world_coords_homo[..., :3]  # [N, H, W, 3]

    if input_is_numpy:
        return point_cloud_world.cpu().numpy()
    return point_cloud_world


def warmup_torch():

    print("\nWarming up PyTorch alignment...")

    src = np.random.randn(100000, 3).astype(np.float32)
    tgt = np.random.randn(100000, 3).astype(np.float32)
    weights = np.ones(100000, dtype=np.float32)
    residuals = np.abs(np.random.randn(100000).astype(np.float32))
    R = np.eye(3, dtype=np.float32)
    t = np.zeros(3, dtype=np.float32)
    s = np.float32(1.0)
    delta = np.float32(1.0)

    try:
        _ = weighted_estimate_sim3_torch(src, tgt, weights)
        print(" - weighted_estimate_sim3_torch warmed up.")
    except Exception as e:
        print(" ! Failed to warm up weighted_estimate_sim3_torch:", e)

    try:
        _ = weighted_estimate_se3_torch(src, tgt, weights)
        print(" - weighted_estimate_se3_torch warmed up.")
    except Exception as e:
        print(" ! Failed to warm up weighted_estimate_se3_torch:", e)

    try:
        _ = huber_loss_torch(residuals, delta)
        print(" - huber_loss_torch warmed up.")
    except Exception as e:
        print(" ! Failed to warm up huber_loss_torch:", e)

    try:
        _ = compute_huber_weights_torch(residuals, delta)
        print(" - compute_huber_weights_torch warmed up.")
    except Exception as e:
        print(" ! Failed to warm up compute_huber_weights_torch:", e)

    try:
        _ = compute_residuals_torch(tgt, src)
        print(" - compute_residuals_torch warmed up.")
    except Exception as e:
        print(" ! Failed to warm up compute_residuals_torch:", e)

    try:
        _ = apply_transformation_torch(src, s, R, t)
        print(" - apply_transformation_torch warmed up.")
    except Exception as e:
        print(" ! Failed to warm up apply_transformation_torch:", e)

    print("PyTorch warm-up complete.\n")


def print_gpu_memory():
    if torch.cuda.is_available():
        allocated = torch.cuda.memory_allocated() / 1024**3  # GB
        cached = torch.cuda.memory_reserved() / 1024**3  # GB
        print(f"GPU Memory Allocated: {allocated:.2f} GB, Cached: {cached:.2f} GB")


if __name__ == "__main__":

    warmup_torch()

    n_points = 7_500_000
    src = np.random.randn(n_points, 3).astype(np.float32)

    true_R = np.array([[0.866, -0.5, 0], [0.5, 0.866, 0], [0, 0, 1]], dtype=np.float32)
    true_t = np.array([1.0, 2.0, 0.5], dtype=np.float32)
    true_s = 1.2

    tgt = true_s * (src @ true_R.T) + true_t
    tgt += 0.01 * np.random.randn(*tgt.shape).astype(np.float32)

    weights = np.ones(n_points, dtype=np.float32)

    print_gpu_memory()

    s, R, t = robust_weighted_estimate_sim3_torch(
        src, tgt, weights, delta=0.1, max_iters=5, align_method="sim3"
    )

    print(f"\nEstimated scale: {s:.6f}")
    print(f"Estimated rotation:\n{R}")
    print(f"Estimated translation: {t}")

    print_gpu_memory()



================================================
FILE: da3_streaming/loop_utils/alignment_triton.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
# Adapted from [VGGT-Long](https://github.com/DengKaiCQ/VGGT-Long)

import numpy as np
import torch
import triton
import triton.language as tl


@triton.jit
def apply_transformation_residual_kernel(
    src_ptr,  # [n, 3]
    tgt_ptr,  # [n, 3]
    transformed_ptr,  # [n, 3]
    residuals_ptr,  # [n]
    s,
    R00,
    R01,
    R02,
    R10,
    R11,
    R12,
    R20,
    R21,
    R22,
    t0,
    t1,
    t2,
    n_points,
    BLOCK_SIZE: tl.constexpr,
):
    pid = tl.program_id(0)
    offsets = pid * BLOCK_SIZE + tl.arange(0, BLOCK_SIZE)
    mask = offsets < n_points

    src_x = tl.load(src_ptr + offsets * 3 + 0, mask=mask)
    src_y = tl.load(src_ptr + offsets * 3 + 1, mask=mask)
    src_z = tl.load(src_ptr + offsets * 3 + 2, mask=mask)

    tgt_x = tl.load(tgt_ptr + offsets * 3 + 0, mask=mask)
    tgt_y = tl.load(tgt_ptr + offsets * 3 + 1, mask=mask)
    tgt_z = tl.load(tgt_ptr + offsets * 3 + 2, mask=mask)

    # transformed = s * (R @ p) + t
    transformed_x = s * (R00 * src_x + R01 * src_y + R02 * src_z) + t0
    transformed_y = s * (R10 * src_x + R11 * src_y + R12 * src_z) + t1
    transformed_z = s * (R20 * src_x + R21 * src_y + R22 * src_z) + t2

    tl.store(transformed_ptr + offsets * 3 + 0, transformed_x, mask=mask)
    tl.store(transformed_ptr + offsets * 3 + 1, transformed_y, mask=mask)
    tl.store(transformed_ptr + offsets * 3 + 2, transformed_z, mask=mask)

    dx = tgt_x - transformed_x
    dy = tgt_y - transformed_y
    dz = tgt_z - transformed_z
    residual = tl.sqrt(dx * dx + dy * dy + dz * dz)
    tl.store(residuals_ptr + offsets, residual, mask=mask)


@triton.jit
def weighted_covariance_kernel(
    src_ptr,  # [n, 3]
    tgt_ptr,  # [n, 3]
    weights_ptr,  # [n]
    mu_src0,
    mu_src1,
    mu_src2,
    mu_tgt0,
    mu_tgt1,
    mu_tgt2,
    H_ptr,  # [3, 3]
    n_points,
    BLOCK_SIZE: tl.constexpr,
):
    pid = tl.program_id(0)
    offsets = pid * BLOCK_SIZE + tl.arange(0, BLOCK_SIZE)
    mask = offsets < n_points

    w = tl.load(weights_ptr + offsets, mask=mask)
    src_x = tl.load(src_ptr + offsets * 3 + 0, mask=mask)
    src_y = tl.load(src_ptr + offsets * 3 + 1, mask=mask)
    src_z = tl.load(src_ptr + offsets * 3 + 2, mask=mask)
    tgt_x = tl.load(tgt_ptr + offsets * 3 + 0, mask=mask)
    tgt_y = tl.load(tgt_ptr + offsets * 3 + 1, mask=mask)
    tgt_z = tl.load(tgt_ptr + offsets * 3 + 2, mask=mask)

    src_centered_x = src_x - mu_src0
    src_centered_y = src_y - mu_src1
    src_centered_z = src_z - mu_src2

    tgt_centered_x = tgt_x - mu_tgt0
    tgt_centered_y = tgt_y - mu_tgt1
    tgt_centered_z = tgt_z - mu_tgt2

    sqrt_w = tl.sqrt(w)
    weighted_src_x = src_centered_x * sqrt_w
    weighted_src_y = src_centered_y * sqrt_w
    weighted_src_z = src_centered_z * sqrt_w

    weighted_tgt_x = tgt_centered_x * sqrt_w
    weighted_tgt_y = tgt_centered_y * sqrt_w
    weighted_tgt_z = tgt_centered_z * sqrt_w

    h00 = weighted_src_x * weighted_tgt_x
    h01 = weighted_src_x * weighted_tgt_y
    h02 = weighted_src_x * weighted_tgt_z

    h10 = weighted_src_y * weighted_tgt_x
    h11 = weighted_src_y * weighted_tgt_y
    h12 = weighted_src_y * weighted_tgt_z

    h20 = weighted_src_z * weighted_tgt_x
    h21 = weighted_src_z * weighted_tgt_y
    h22 = weighted_src_z * weighted_tgt_z

    tl.atomic_add(H_ptr + 0, tl.sum(h00, axis=0))
    tl.atomic_add(H_ptr + 1, tl.sum(h01, axis=0))
    tl.atomic_add(H_ptr + 2, tl.sum(h02, axis=0))

    tl.atomic_add(H_ptr + 3, tl.sum(h10, axis=0))
    tl.atomic_add(H_ptr + 4, tl.sum(h11, axis=0))
    tl.atomic_add(H_ptr + 5, tl.sum(h12, axis=0))

    tl.atomic_add(H_ptr + 6, tl.sum(h20, axis=0))
    tl.atomic_add(H_ptr + 7, tl.sum(h21, axis=0))
    tl.atomic_add(H_ptr + 8, tl.sum(h22, axis=0))


@triton.jit
def compute_huber_weights_kernel(
    residuals_ptr,
    weights_ptr,
    delta,
    n_points,
    BLOCK_SIZE: tl.constexpr,
):
    pid = tl.program_id(0)
    offsets = pid * BLOCK_SIZE + tl.arange(0, BLOCK_SIZE)
    mask = offsets < n_points

    r = tl.load(residuals_ptr + offsets, mask=mask)

    weight = tl.where(r > delta, delta / r, 1.0)

    tl.store(weights_ptr + offsets, weight, mask=mask)


@triton.jit
def weighted_mean_kernel(
    points_ptr,  # [n, 3]
    weights_ptr,  # [n]
    mean_ptr,  # [sum(w*x), sum(w*y), sum(w*z), sum(w)]
    n_points,
    BLOCK_SIZE: tl.constexpr,
):
    pid = tl.program_id(0)
    offsets = pid * BLOCK_SIZE + tl.arange(0, BLOCK_SIZE)
    mask = offsets < n_points

    w = tl.load(weights_ptr + offsets, mask=mask)
    x = tl.load(points_ptr + offsets * 3 + 0, mask=mask)
    y = tl.load(points_ptr + offsets * 3 + 1, mask=mask)
    z = tl.load(points_ptr + offsets * 3 + 2, mask=mask)

    wx = w * x
    wy = w * y
    wz = w * z

    tl.atomic_add(mean_ptr + 0, tl.sum(wx, axis=0))
    tl.atomic_add(mean_ptr + 1, tl.sum(wy, axis=0))
    tl.atomic_add(mean_ptr + 2, tl.sum(wz, axis=0))
    tl.atomic_add(mean_ptr + 3, tl.sum(w, axis=0))


def apply_transformation_residual_triton(src, tgt, s, R, t):
    n_points = src.shape[0]

    transformed = torch.empty_like(src)
    residuals = torch.empty(n_points, device=src.device, dtype=src.dtype)

    BLOCK_SIZE = 256
    grid = (triton.cdiv(n_points, BLOCK_SIZE),)

    R_flat = R.contiguous().view(-1)
    t_flat = t.contiguous().view(-1)

    apply_transformation_residual_kernel[grid](
        src,
        tgt,
        transformed,
        residuals,
        float(s),
        float(R_flat[0]),
        float(R_flat[1]),
        float(R_flat[2]),
        float(R_flat[3]),
        float(R_flat[4]),
        float(R_flat[5]),
        float(R_flat[6]),
        float(R_flat[7]),
        float(R_flat[8]),
        float(t_flat[0]),
        float(t_flat[1]),
        float(t_flat[2]),
        n_points,
        BLOCK_SIZE=BLOCK_SIZE,
    )

    return transformed, residuals


def compute_weighted_mean_triton(points, weights):
    n_points = points.shape[0]

    # [sum(w*x), sum(w*y), sum(w*z), sum(w)]
    mean_buffer = torch.zeros(4, device=points.device, dtype=points.dtype)

    BLOCK_SIZE = 256
    grid = (triton.cdiv(n_points, BLOCK_SIZE),)

    weighted_mean_kernel[grid](points, weights, mean_buffer, n_points, BLOCK_SIZE=BLOCK_SIZE)

    total_weight = mean_buffer[3]
    if total_weight > 1e-12:
        mean = mean_buffer[:3] / total_weight
    else:
        mean = torch.zeros(3, device=points.device, dtype=points.dtype)

    return mean, total_weight


def compute_weighted_covariance_triton(src, tgt, weights, mu_src, mu_tgt):
    n_points = src.shape[0]

    H = torch.zeros(9, device=src.device, dtype=src.dtype)

    BLOCK_SIZE = 256
    grid = (triton.cdiv(n_points, BLOCK_SIZE),)

    mu_src_flat = mu_src.contiguous().view(-1)
    mu_tgt_flat = mu_tgt.contiguous().view(-1)

    weighted_covariance_kernel[grid](
        src,
        tgt,
        weights,
        float(mu_src_flat[0]),
        float(mu_src_flat[1]),
        float(mu_src_flat[2]),
        float(mu_tgt_flat[0]),
        float(mu_tgt_flat[1]),
        float(mu_tgt_flat[2]),
        H,
        n_points,
        BLOCK_SIZE=BLOCK_SIZE,
    )

    return H.reshape(3, 3)


def compute_huber_weights_triton(residuals, delta):
    n_points = residuals.shape[0]
    weights = torch.empty_like(residuals)

    BLOCK_SIZE = 256
    grid = (triton.cdiv(n_points, BLOCK_SIZE),)

    compute_huber_weights_kernel[grid](
        residuals, weights, float(delta), n_points, BLOCK_SIZE=BLOCK_SIZE
    )

    return weights


def weighted_estimate_se3_triton(source_points, target_points, weights):

    source_points = torch.from_numpy(source_points).cuda().float()
    target_points = torch.from_numpy(target_points).cuda().float()
    weights = torch.from_numpy(weights).cuda().float()

    total_weight = torch.sum(weights)
    if total_weight < 1e-6:
        return (
            1.0,
            np.zeros(3, dtype=np.float32),
            np.zeros(3, dtype=np.float32),
            np.zeros((3, 3), dtype=np.float32),
        )

    normalized_weights = weights / total_weight

    mu_src, _ = compute_weighted_mean_triton(source_points, normalized_weights)
    mu_tgt, _ = compute_weighted_mean_triton(target_points, normalized_weights)

    H = compute_weighted_covariance_triton(
        source_points, target_points, normalized_weights, mu_src, mu_tgt
    )

    return 1.0, mu_src.cpu().numpy(), mu_tgt.cpu().numpy(), H.cpu().numpy()


def weighted_estimate_sim3_triton(source_points, target_points, weights):

    source_points = torch.from_numpy(source_points).cuda().float()
    target_points = torch.from_numpy(target_points).cuda().float()
    weights = torch.from_numpy(weights).cuda().float()

    total_weight = torch.sum(weights)
    if total_weight < 1e-6:
        return (
            -1.0,
            np.zeros(3, dtype=np.float32),
            np.zeros(3, dtype=np.float32),
            np.zeros((3, 3), dtype=np.float32),
        )

    normalized_weights = weights / total_weight

    mu_src, _ = compute_weighted_mean_triton(source_points, normalized_weights)
    mu_tgt, _ = compute_weighted_mean_triton(target_points, normalized_weights)

    src_centered = source_points - mu_src
    tgt_centered = target_points - mu_tgt

    scale_src = torch.sqrt(torch.sum(normalized_weights * torch.sum(src_centered**2, dim=1)))
    scale_tgt = torch.sqrt(torch.sum(normalized_weights * torch.sum(tgt_centered**2, dim=1)))
    s = scale_tgt / scale_src

    weighted_src = s * src_centered
    H = compute_weighted_covariance_triton(
        weighted_src,
        tgt_centered,
        normalized_weights,
        torch.zeros_like(mu_src),
        torch.zeros_like(mu_tgt),
    )

    return s.cpu().numpy(), mu_src.cpu().numpy(), mu_tgt.cpu().numpy(), H.cpu().numpy()


def weighted_estimate_sim3_numba_triton(
    source_points, target_points, weights, align_method="sim3"
):

    if align_method == "sim3":
        s, mu_src, mu_tgt, H = weighted_estimate_sim3_triton(source_points, target_points, weights)
    elif align_method == "se3" or align_method == "scale+se3":
        s, mu_src, mu_tgt, H = weighted_estimate_se3_triton(source_points, target_points, weights)

    if s < 0:
        raise ValueError("Total weight too small for meaningful estimation")

    H_torch = torch.from_numpy(H).cuda().float()
    U, _, Vt = torch.linalg.svd(H_torch)

    U = U.cpu().numpy()
    Vt = Vt.cpu().numpy()

    R = Vt.T @ U.T
    if np.linalg.det(R) < 0:
        Vt[2, :] *= -1
        R = Vt.T @ U.T

    mu_src = mu_src.astype(np.float32)
    mu_tgt = mu_tgt.astype(np.float32)
    R = R.astype(np.float32)

    if align_method == "se3" or align_method == "scale+se3":
        t = mu_tgt - R @ mu_src
    else:
        t = mu_tgt - s * R @ mu_src

    return s, R, t.astype(np.float32)


def robust_weighted_estimate_sim3_triton(
    src, tgt, init_weights, delta=0.1, max_iters=20, tol=1e-9, align_method="sim3"
):

    src = src.astype(np.float32)
    tgt = tgt.astype(np.float32)
    init_weights = init_weights.astype(np.float32)

    src_torch = torch.from_numpy(src).cuda().float()
    tgt_torch = torch.from_numpy(tgt).cuda().float()
    init_weights_torch = torch.from_numpy(init_weights).cuda().float()

    s, R, t = weighted_estimate_sim3_numba_triton(
        src, tgt, init_weights, align_method=align_method
    )

    R_torch = torch.from_numpy(R).cuda().float()
    t_torch = torch.from_numpy(t).cuda().float()
    s_torch = torch.tensor(s, device="cuda", dtype=torch.float32)

    prev_error = float("inf")

    for iter in range(max_iters):
        transformed, residuals = apply_transformation_residual_triton(
            src_torch, tgt_torch, s_torch, R_torch, t_torch
        )

        mean_residual = torch.mean(residuals).cpu().numpy()
        print(f"Iter {iter}: Mean residual = {mean_residual:.6f}")

        huber_weights = compute_huber_weights_triton(residuals, delta)

        combined_weights = init_weights_torch * huber_weights
        combined_weights_sum = torch.sum(combined_weights)
        if combined_weights_sum > 1e-12:
            combined_weights /= combined_weights_sum
        else:
            combined_weights = init_weights_torch / torch.sum(init_weights_torch)

        combined_weights_np = combined_weights.cpu().numpy()
        s_new, R_new, t_new = weighted_estimate_sim3_numba_triton(
            src, tgt, combined_weights_np, align_method=align_method
        )

        param_change = np.abs(s_new - s) + np.linalg.norm(t_new - t)
        rot_angle = np.arccos(min(1.0, max(-1.0, (np.trace(R_new @ R.T) - 1) / 2)))

        residuals_np = residuals.cpu().numpy()
        huber_loss_values = np.where(
            residuals_np <= delta, 0.5 * residuals_np**2, delta * (residuals_np - 0.5 * delta)
        )
        current_error = np.sum(huber_loss_values * init_weights)

        if (param_change < tol and rot_angle < np.radians(0.1)) or (
            abs(prev_error - current_error) < tol * prev_error
        ):
            print(f"Converged at iteration {iter}")
            break

        s, R, t = s_new, R_new, t_new
        s_torch = torch.tensor(s, device="cuda", dtype=torch.float32)
        R_torch = torch.from_numpy(R).cuda().float()
        t_torch = torch.from_numpy(t).cuda().float()
        prev_error = current_error

    return s, R, t


def warmup_triton():
    print("\nWarming up Triton functions...")

    n_points = 10000
    src = np.random.randn(n_points, 3).astype(np.float32)
    tgt = np.random.randn(n_points, 3).astype(np.float32)
    weights = np.ones(n_points, dtype=np.float32)

    src_torch = torch.from_numpy(src).cuda().float()
    tgt_torch = torch.from_numpy(tgt).cuda().float()
    weights_torch = torch.from_numpy(weights).cuda().float()

    R = np.eye(3, dtype=np.float32)
    t = np.zeros(3, dtype=np.float32)
    s = np.float32(1.0)
    delta = np.float32(0.1)

    R_torch = torch.from_numpy(R).cuda().float()
    t_torch = torch.from_numpy(t).cuda().float()
    s_torch = torch.tensor(s, device="cuda", dtype=torch.float32)

    try:
        _, _ = apply_transformation_residual_triton(
            src_torch, tgt_torch, s_torch, R_torch, t_torch
        )
        print(" - apply_transformation_residual_triton warmed up.")
    except Exception as e:
        print(f" ! Failed to warm up apply_transformation_residual_triton: {e}")

    try:
        _, _ = compute_weighted_mean_triton(src_torch, weights_torch)
        print(" - compute_weighted_mean_triton warmed up.")
    except Exception as e:
        print(f" ! Failed to warm up compute_weighted_mean_triton: {e}")

    try:
        mu_src, _ = compute_weighted_mean_triton(src_torch, weights_torch)
        mu_tgt, _ = compute_weighted_mean_triton(tgt_torch, weights_torch)
        _ = compute_weighted_covariance_triton(src_torch, tgt_torch, weights_torch, mu_src, mu_tgt)
        print(" - compute_weighted_covariance_triton warmed up.")
    except Exception as e:
        print(f" ! Failed to warm up compute_weighted_covariance_triton: {e}")

    try:
        residuals = torch.abs(torch.randn(n_points, device="cuda", dtype=torch.float32))
        _ = compute_huber_weights_triton(residuals, delta)
        print(" - compute_huber_weights_triton warmed up.")
    except Exception as e:
        print(f" ! Failed to warm up compute_huber_weights_triton: {e}")

    print("Triton warm-up complete.\n")


def print_gpu_memory():
    if torch.cuda.is_available():
        allocated = torch.cuda.memory_allocated() / 1024**3  # GB
        cached = torch.cuda.memory_reserved() / 1024**3  # GB
        print(f"GPU Memory Allocated: {allocated:.2f} GB, Cached: {cached:.2f} GB")


if __name__ == "__main__":

    warmup_triton()

    n_points = 7_500_000
    src = np.random.randn(n_points, 3).astype(np.float32)

    true_R = np.array([[0.866, -0.5, 0], [0.5, 0.866, 0], [0, 0, 1]], dtype=np.float32)
    true_t = np.array([1.0, 2.0, 0.5], dtype=np.float32)
    true_s = 1.2

    tgt = true_s * (src @ true_R.T) + true_t
    tgt += 0.01 * np.random.randn(*tgt.shape).astype(np.float32)

    weights = np.ones(n_points, dtype=np.float32)

    print_gpu_memory()

    s, R, t = robust_weighted_estimate_sim3_triton(
        src, tgt, weights, delta=0.1, max_iters=5, align_method="sim3"
    )

    print(f"\nEstimated scale: {s:.6f}")
    print(f"Estimated rotation:\n{R}")
    print(f"Estimated translation: {t}")

    print_gpu_memory()



================================================
FILE: da3_streaming/loop_utils/config_utils.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
# Adapted from [VGGT-Long](https://github.com/DengKaiCQ/VGGT-Long)

import yaml


def load_config(path, default_path=None):
    """
    Loads config file.

    Args:
        path (str): path to config file.
        default_path (str, optional): whether to use default path. Defaults to None.

    Returns:
        cfg (dict): config dict.

    """
    # load configuration from per scene/dataset cfg.
    with open(path) as f:
        cfg_special = yaml.full_load(f)

    inherit_from = cfg_special.get("inherit_from")

    if inherit_from is not None:
        cfg = load_config(inherit_from, default_path)
    elif default_path is not None:
        with open(default_path) as f:
            cfg = yaml.full_load(f)
    else:
        cfg = dict()

    # merge per dataset cfg. and main cfg.
    update_recursive(cfg, cfg_special)

    return cfg


def update_recursive(dict1, dict2):
    """
    Update two config dictionaries recursively. dict1 get masked by dict2, and we retuen dict1.

    Args:
        dict1 (dict): first dictionary to be updated.
        dict2 (dict): second dictionary which entries should be used.
    """
    for k, v in dict2.items():
        if k not in dict1:
            dict1[k] = dict()
        if isinstance(v, dict):
            update_recursive(dict1[k], v)
        else:
            dict1[k] = v



================================================
FILE: da3_streaming/loop_utils/logging_utils.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
# Adapted from [VGGT-Long](https://github.com/DengKaiCQ/VGGT-Long)

import rich

_log_styles = {
    "DA3-Streaming": "bold green",
}


def get_style(tag):
    if tag in _log_styles.keys():
        return _log_styles[tag]
    return "bold blue"


def Log(*args, tag="DA3-Streaming"):
    style = get_style(tag)
    rich.print(f"[{style}]{tag}:[/{style}]", *args)



================================================
FILE: da3_streaming/loop_utils/loop_detector.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
# Adapted from [VGGT-Long](https://github.com/DengKaiCQ/VGGT-Long)

import argparse
import os
import sys
from pathlib import Path
import faiss
import torch
import torchvision.transforms as T
from PIL import Image
from torch import nn
from tqdm import tqdm

CURRENT_DIR = os.path.dirname(os.path.abspath(__file__))
SALAD_ROOT = os.path.join(CURRENT_DIR, "salad")
if SALAD_ROOT not in sys.path:
    sys.path.insert(0, SALAD_ROOT)
from loop_utils.salad.models import helper


class VPRModel(nn.Module):
    """This is the main model for Visual Place Recognition
    we use Pytorch Lightning for modularity purposes.

    Args:
        pl (_type_): _description_
    """

    def __init__(
        self,
        # ---- Backbone
        backbone_arch="resnet50",
        backbone_config={},
        # ---- Aggregator
        agg_arch="ConvAP",
        agg_config={},
    ):
        super().__init__()

        # Backbone
        self.encoder_arch = backbone_arch
        self.backbone_config = backbone_config

        # Aggregator
        self.agg_arch = agg_arch
        self.agg_config = agg_config

        # ----------------------------------
        # get the backbone and the aggregator
        self.backbone = helper.get_backbone(backbone_arch, backbone_config)
        self.aggregator = helper.get_aggregator(agg_arch, agg_config)

    # the forward pass of the lightning model
    def forward(self, x):
        x = self.backbone(x)
        x = self.aggregator(x)
        return x


class LoopDetector:
    """Loop detector class for detecting loop closures in image sequences"""

    def __init__(self, image_dir, output="loop_closures.txt", config=None):
        """Initialize the loop detector

        Args:
            image_dir: Directory path containing images
            ckpt_path: Model checkpoint path
            image_size: Image resize dimensions [height width]
            batch_size: Batch size for processing
            similarity_threshold: Similarity threshold for loop closure
            top_k: Number of nearest neighbors to check for each image
            use_nms: Whether to use Non-Maximum Suppression (NMS) filtering
            nms_threshold: NMS threshold for minimum frame difference between loop pairs
            output: Output file path
        """
        self.config = config
        self.image_dir = image_dir
        self.ckpt_path = self.config["Weights"]["SALAD"]
        self.image_size = self.config["Loop"]["SALAD"]["image_size"]
        self.batch_size = self.config["Loop"]["SALAD"]["batch_size"]
        self.similarity_threshold = self.config["Loop"]["SALAD"]["similarity_threshold"]
        self.top_k = self.config["Loop"]["SALAD"]["top_k"]
        self.use_nms = self.config["Loop"]["SALAD"]["use_nms"]
        self.nms_threshold = self.config["Loop"]["SALAD"]["nms_threshold"]
        self.output = output

        self.model = None
        self.device = None
        self.image_paths = None
        self.descriptors = None
        self.loop_closures = None

    def _input_transform(self, image_size=None):
        """Create image transformation function"""
        MEAN = [0.485, 0.456, 0.406]
        STD = [0.229, 0.224, 0.225]
        if image_size:
            return T.Compose(
                [
                    T.Resize(image_size, interpolation=T.InterpolationMode.BILINEAR),
                    T.ToTensor(),
                    T.Normalize(mean=MEAN, std=STD),
                ]
            )
        else:
            return T.Compose([T.ToTensor(), T.Normalize(mean=MEAN, std=STD)])

    def load_model(self):
        """Load model"""
        model = VPRModel(
            backbone_arch="dinov2_vitb14",
            backbone_config={
                "num_trainable_blocks": 4,
                "return_token": True,
                "norm_layer": True,
            },
            agg_arch="SALAD",
            agg_config={
                "num_channels": 768,
                "num_clusters": 64,
                "cluster_dim": 128,
                "token_dim": 256,
            },
        )

        model.load_state_dict(torch.load(self.ckpt_path))
        model = model.eval()
        device = torch.device("cuda" if torch.cuda.is_available() else "cpu")
        model = model.to(device)
        print(f"Model loaded: {self.ckpt_path}")

        self.model = model
        self.device = device
        return model, device

    def get_image_paths(self):
        """Get paths of all image files in directory"""
        image_extensions = [".jpg", ".jpeg", ".png"]
        image_paths = []

        for ext in image_extensions:
            image_paths.extend(list(Path(self.image_dir).glob(f"*{ext}")))
            image_paths.extend(list(Path(self.image_dir).glob(f"*{ext.upper()}")))

        image_paths = sorted(image_paths)
        self.image_paths = image_paths
        return image_paths

    def extract_descriptors(self):
        """Extract image feature descriptors"""
        if self.model is None or self.device is None:
            self.load_model()

        if self.image_paths is None:
            self.get_image_paths()

        transform = self._input_transform(self.image_size)
        descriptors = []

        for i in tqdm(
            range(0, len(self.image_paths), self.batch_size), desc="Extracting features"
        ):
            batch_paths = self.image_paths[i : i + self.batch_size]
            batch_imgs = []

            for path in batch_paths:
                try:
                    img = Image.open(path).convert("RGB")
                    img = transform(img)
                    batch_imgs.append(img)
                except Exception as e:
                    print(f"Error processing image {path}: {e}")
                    img = (
                        torch.zeros(3, 224, 224)
                        if self.image_size is None
                        else torch.zeros(3, self.image_size[0], self.image_size[1])
                    )
                    batch_imgs.append(img)

            batch_tensor = torch.stack(batch_imgs).to(self.device)

            with torch.no_grad():
                with torch.autocast(
                    device_type="cuda" if torch.cuda.is_available() else "cpu", dtype=torch.float16
                ):
                    batch_descriptors = self.model(batch_tensor).cpu()

            descriptors.append(batch_descriptors)

        self.descriptors = torch.cat(descriptors)
        return self.descriptors

    def _apply_nms_filter(self, loop_closures, nms_threshold):
        """Apply Non-Maximum Suppression (NMS) filtering to loop pairs"""
        if not loop_closures or nms_threshold <= 0:
            return loop_closures

        sorted_loops = sorted(loop_closures, key=lambda x: x[2], reverse=True)
        filtered_loops = []
        suppressed = set()

        max_frame = max(max(idx1, idx2) for idx1, idx2, _ in loop_closures)

        for idx1, idx2, sim in sorted_loops:
            if idx1 in suppressed or idx2 in suppressed:
                continue

            filtered_loops.append((idx1, idx2, sim))

            suppress_range = set()

            start1 = max(0, idx1 - nms_threshold)
            end1 = min(idx1 + nms_threshold + 1, idx2)
            suppress_range.update(range(start1, end1))

            start2 = max(idx1 + 1, idx2 - nms_threshold)
            end2 = min(idx2 + nms_threshold + 1, max_frame + 1)
            suppress_range.update(range(start2, end2))

            suppressed.update(suppress_range)

        return filtered_loops

    def _ensure_decending_order(self, tuples_list):
        return [(max(a, b), min(a, b), score) for a, b, score in tuples_list]

    def find_loop_closures(self):
        """Find loop closures"""
        if self.descriptors is None:
            self.extract_descriptors()

        embed_size = self.descriptors.shape[1]
        faiss_index = faiss.IndexFlatIP(embed_size)

        normalized_descriptors = self.descriptors.numpy()
        faiss_index.add(normalized_descriptors)

        similarities, indices = faiss_index.search(
            normalized_descriptors, self.top_k + 1
        )  # +1 because self is most similar

        loop_closures = []
        for i in range(len(self.descriptors)):
            # Skip first result (self)
            for j in range(1, self.top_k + 1):
                neighbor_idx = indices[i, j]
                similarity = similarities[i, j]

                if similarity > self.similarity_threshold and abs(i - neighbor_idx) > 10:
                    if i < neighbor_idx:
                        loop_closures.append((i, neighbor_idx, similarity))
                    else:
                        loop_closures.append((neighbor_idx, i, similarity))

        loop_closures = list(set(loop_closures))
        loop_closures.sort(key=lambda x: x[2], reverse=True)

        if self.use_nms and self.nms_threshold > 0:
            loop_closures = self._apply_nms_filter(loop_closures, self.nms_threshold)

        self.loop_closures = self._ensure_decending_order(loop_closures)
        return self.loop_closures

    def save_results(self):
        """Save loop detection results to file"""
        if self.loop_closures is None:
            self.find_loop_closures()

        with open(self.output, "w") as f:
            f.write("# Loop Detection Results (index1, index2, similarity)\n")
            if self.use_nms:
                f.write(f"# NMS filtering applied, threshold: {self.nms_threshold}\n")
            f.write("\n# Loop pairs:\n")
            for i, j, sim in self.loop_closures:
                f.write(f"{i}, {j}, {sim:.4f}\n")
            f.write("\n# Image path list:\n")
            for i, path in enumerate(self.image_paths):
                f.write(f"# {i}: {path}\n")

        print(f"Found {len(self.loop_closures)} loop pairs, results saved to {self.output}")
        if self.use_nms:
            print(f"NMS filtering applied, threshold: {self.nms_threshold}")

        if self.loop_closures:
            print("\nTop 10 loop pairs:")
            for i, (idx1, idx2, sim) in enumerate(self.loop_closures[:10]):
                print(f"{idx1}, {idx2}, similarity: {sim:.4f}")
                if i >= 9:
                    break

    def get_loop_list(self):
        return [(idx1, idx2) for idx1, idx2, _ in self.loop_closures]

    def run(self):
        """Run complete loop detection pipeline"""
        print("Loading model...")
        if self.model is None:
            self.load_model()

        self.get_image_paths()
        if not self.image_paths:
            print(f"No image files found in {self.image_dir}")
            return

        print(f"Found {len(self.image_paths)} image files")

        self.extract_descriptors()

        self.find_loop_closures()

        self.save_results()

        return self.loop_closures


def main():
    parser = argparse.ArgumentParser(description="Loop detection using SALAD model")
    parser.add_argument(
        "--image_dir",
        type=str,
        default="/media/deng/Data/KITTIdataset/data_odometry_color/dataset/sequences/00/image_2",
        help="Directory path containing images",
    )
    parser.add_argument(
        "--ckpt_path", type=str, default="./weights/dino_salad.ckpt", help="Model checkpoint path"
    )
    parser.add_argument(
        "--image_size",
        nargs=2,
        type=int,
        default=[336, 336],
        help="Image resize dimensions [height width]",
    )
    parser.add_argument("--batch_size", type=int, default=32, help="Batch size for processing")
    parser.add_argument(
        "--similarity_threshold",
        type=float,
        default=0.7,
        help="Similarity threshold for loop closure",
    )
    parser.add_argument(
        "--top_k", type=int, default=5, help="Number of nearest neighbors to check for each image"
    )
    parser.add_argument("--output", type=str, default="loop_closures.txt", help="Output file path")
    parser.add_argument(
        "--use_nms",
        action="store_true",
        default=True,
        help="Whether to use Non-Maximum Suppression (NMS) filtering",
    )
    parser.add_argument(
        "--nms_threshold",
        type=int,
        default=25,
        help="NMS threshold for minimum frame difference between loop pairs",
    )

    args = parser.parse_args()

    detector = LoopDetector(
        image_dir=args.image_dir,
        ckpt_path=args.ckpt_path,
        image_size=args.image_size,
        batch_size=args.batch_size,
        similarity_threshold=args.similarity_threshold,
        top_k=args.top_k,
        use_nms=args.use_nms,
        nms_threshold=args.nms_threshold,
        output=args.output,
    )

    detector.run()


if __name__ == "__main__":
    main()



================================================
FILE: da3_streaming/loop_utils/loop_refinement.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
# Adapted from [VGGT-Long](https://github.com/DengKaiCQ/VGGT-Long)

import numba as nb
import numpy as np
import pypose as pp
import sim3solve
import torch
from einops import parse_shape, rearrange
from scipy.spatial.transform import Rotation as R


def make_pypose_Sim3(rot, t, s):
    q = R.from_matrix(rot).as_quat()
    data = np.concatenate([t, q, np.array(s).reshape((1,))])
    return pp.Sim3(data)


def SE3_to_Sim3(x: pp.SE3):
    out = torch.cat((x.data, torch.ones_like(x.data[..., :1])), dim=-1)
    return pp.Sim3(out)


@nb.njit(cache=True)
def _format(es):
    return np.asarray(es, dtype=np.int64).reshape((-1, 2))[1:]


@nb.njit(cache=True)
def reduce_edges(flow_mag, ii, jj, max_num_edges, nms):
    es = [(-1, -1)]

    if ii.size == 0:
        return _format(es)

    Ni, Nj = (ii.max() + 1), (jj.max() + 1)
    ignore_lookup = np.zeros((Ni, Nj), dtype=nb.bool_)

    idxs = np.argsort(flow_mag)
    for idx in idxs:  # edge index

        if len(es) > max_num_edges:
            break

        i = ii[idx]
        j = jj[idx]
        mag = flow_mag[idx]

        if (j - i) < 30:
            continue

        if mag >= 1000:  # i.e., inf
            continue

        if ignore_lookup[i, j]:
            continue

        es.append((i, j))

        for di in range(-nms, nms + 1):
            i1 = i + di

            if 0 <= i1 < Ni:
                ignore_lookup[i1, j] = True

    return _format(es)


@nb.njit(cache=True)
def umeyama_alignment(x: np.ndarray, y: np.ndarray):
    """
    The following function was copied from:
    https://github.com/MichaelGrupp/evo/blob/3067541b350528fe46375423e5bc3a7c42c06c63/evo/core/geometry.py#L35

    Computes the least squares solution parameters of an Sim(m) matrix
    that minimizes the distance between a set of registered points.
    Umeyama, Shinji: Least-squares estimation of transformation parameters
                     between two point patterns. IEEE PAMI, 1991
    :param x: mxn matrix of points, m = dimension, n = nr. of data points
    :param y: mxn matrix of points, m = dimension, n = nr. of data points
    :param with_scale: set to True to align also the scale (default: 1.0 scale)
    :return: r, t, c - rotation matrix, translation vector and scale factor
    """

    # m = dimension, n = nr. of data points
    m, n = x.shape

    # means, eq. 34 and 35
    mean_x = x.sum(axis=1) / n
    mean_y = y.sum(axis=1) / n

    # variance, eq. 36
    # "transpose" for column subtraction
    sigma_x = 1.0 / n * (np.linalg.norm(x - mean_x[:, np.newaxis]) ** 2)

    # covariance matrix, eq. 38
    outer_sum = np.zeros((m, m))
    for i in range(n):
        outer_sum += np.outer((y[:, i] - mean_y), (x[:, i] - mean_x))
    cov_xy = np.multiply(1.0 / n, outer_sum)

    # SVD (text betw. eq. 38 and 39)
    u, d, v = np.linalg.svd(cov_xy)
    if np.count_nonzero(d > np.finfo(d.dtype).eps) < m - 1:
        return None, None, None  # Degenerate covariance rank, Umeyama alignment is not possible

    # S matrix, eq. 43
    s = np.eye(m)
    if np.linalg.det(u) * np.linalg.det(v) < 0.0:
        # Ensure a RHS coordinate system (Kabsch algorithm).
        s[m - 1, m - 1] = -1

    # rotation, eq. 40
    r = u.dot(s).dot(v)

    # scale & translation, eq. 42 and 41
    c = 1 / sigma_x * np.trace(np.diag(d).dot(s))
    t = mean_y - np.multiply(c, r.dot(mean_x))

    return r, t, c


@nb.njit(cache=True)
def ransac_umeyama(src_points, dst_points, iterations=1, threshold=0.1):
    best_inliers = 0
    best_R = None
    best_t = None
    best_s = None
    for _ in range(iterations):
        # Randomly select three points
        indices = np.random.choice(src_points.shape[0], 3, replace=False)
        src_sample = src_points[indices]
        dst_sample = dst_points[indices]

        # Estimate transformation
        R, t, s = umeyama_alignment(src_sample.T, dst_sample.T)
        if t is None:
            continue

        # Apply transformation
        transformed = (src_points @ (R * s).T) + t

        # Count inliers (not ideal because depends on scene scale)
        distances = np.sum((transformed - dst_points) ** 2, axis=1) ** 0.5
        inlier_mask = distances < threshold
        inliers = np.sum(inlier_mask)

        # Update best transformation
        if inliers > best_inliers:
            best_inliers = inliers
            best_R, best_t, best_s = umeyama_alignment(
                src_points[inlier_mask].T, dst_points[inlier_mask].T
            )

    return best_R, best_t, best_s, best_inliers


def batch_jacobian(func, x):
    def _func_sum(*x):
        return func(*x).sum(dim=0)

    _, b, c = torch.autograd.functional.jacobian(_func_sum, x, vectorize=True)
    return rearrange(torch.stack((b, c)), "N O B I -> N B O I", N=2)


def _residual(C, Gi, Gj):
    assert parse_shape(C, "N _") == parse_shape(Gi, "N _") == parse_shape(Gj, "N _")
    out = C @ pp.Exp(Gi) @ pp.Exp(Gj).Inv()
    return out.Log().tensor()


def residual(Ginv, input_poses, dSloop, ii, jj, jacobian=False):

    # prep
    device = Ginv.device
    assert parse_shape(input_poses, "_ d") == dict(d=7)
    pred_inv_poses = SE3_to_Sim3(input_poses).Inv()

    # free variables
    n, _ = pred_inv_poses.shape
    kk = torch.arange(1, n, device=device)
    ll = kk - 1

    # constants
    Ti = pred_inv_poses[kk]
    Tj = pred_inv_poses[ll]
    dSij = Tj @ Ti.Inv()

    constants = torch.cat((dSij, dSloop), dim=0)
    iii = torch.cat((kk, ii))
    jjj = torch.cat((ll, jj))
    resid = _residual(constants, Ginv[iii], Ginv[jjj])

    if not jacobian:
        return resid

    J_Ginv_i, J_Ginv_j = batch_jacobian(_residual, (constants, Ginv[iii], Ginv[jjj]))
    return resid, (J_Ginv_i, J_Ginv_j, iii, jjj)


def perform_updates(
    input_poses, dSloop, ii_loop, jj_loop, iters=30, ep=0.0, lmbda=1e-6, fix_opt_window=False
):
    """Run the Levenberg Marquardt algorithm"""

    input_poses = input_poses.clone()

    if fix_opt_window:
        freen = torch.cat((ii_loop, jj_loop)).max().item() + 1
    else:
        freen = -1

    Ginv = SE3_to_Sim3(input_poses).Inv().Log()

    residual_history = []

    for itr in range(iters):
        resid, (J_Ginv_i, J_Ginv_j, iii, jjj) = residual(
            Ginv, input_poses, dSloop, ii_loop, jj_loop, jacobian=True
        )
        residual_history.append(resid.square().mean().item())
        print(f"resid: {resid.square().mean().item()}")
        (delta_pose,) = sim3solve.solve_system(
            J_Ginv_i, J_Ginv_j, iii, jjj, resid, ep, lmbda, freen
        )
        assert Ginv.shape == delta_pose.shape
        Ginv_tmp = Ginv + delta_pose

        new_resid = residual(Ginv_tmp, input_poses, dSloop, ii_loop, jj_loop)
        if new_resid.square().mean() < residual_history[-1]:
            Ginv = Ginv_tmp
            lmbda /= 2
        else:
            lmbda *= 2

        if (
            (residual_history[-1] < 1e-5)
            and (itr >= 4)
            and ((residual_history[-5] / residual_history[-1]) < 1.5)
        ):
            break

    return pp.Exp(Ginv).Inv()


def pose_refinement(pred_poses, loop_poses, loop_ii, loop_jj):

    final_est = perform_updates(pred_poses, loop_poses, loop_ii, loop_jj, iters=30)

    safe_i = loop_ii.max().item() + 1
    aa = SE3_to_Sim3(pred_poses.cpu())
    final_est = (aa[[safe_i]] * final_est[[safe_i]].Inv()) * final_est
    output = final_est[:safe_i]

    return output



================================================
FILE: da3_streaming/loop_utils/sim3loop.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
# Adapted from [VGGT-Long](https://github.com/DengKaiCQ/VGGT-Long)

import time
from typing import List, Tuple
import numpy as np
import pypose as pp
import torch
from fastloop.solve_python import solve_system_py
from scipy.spatial.transform import Rotation as R

cpp_version = False
try:
    import sim3solve

    cpp_version = True
except Exception:
    print("Sim3solve of C++ Version failed, Will using Python Version.")


class Sim3LoopOptimizer:
    """
    Loop closure optimizer for sequences of Sim3 transformations

    Input:
    - sequential_transforms: List[Tuple[float, np.ndarray, np.ndarray]]
      Each element is (s, R, t), where s is scalar scale, R is [3,3] rotation matrix,
      t is [3,] translation vector
    - loop_constraints: List[Tuple[int, int, Tuple[float, np.ndarray, np.ndarray]]]
      Each element is (i, j, (s, R, t)), representing a loop closure constraint
      from frame i to frame j

    Output:
    - Optimized sequential_transforms
    """

    def __init__(self, config, device="cpu"):
        self.device = device
        self.config = config
        self.solve_system_version = self.config["Loop"]["SIM3_Optimizer"][
            "lang_version"
        ]  # choose between 'python' and 'cpp'

        if not cpp_version:
            self.solve_system_version = "python"

    def numpy_to_pypose_sim3(self, s: float, R_mat: np.ndarray, t_vec: np.ndarray) -> pp.Sim3:
        """Convert numpy s,R,t to pypose Sim3"""
        q = R.from_matrix(R_mat).as_quat()  # [x,y,z,w]
        # pypose requires [t, q, s] format
        data = np.concatenate([t_vec, q, np.array([s])])
        return pp.Sim3(torch.from_numpy(data).float().to(self.device))

    def pypose_sim3_to_numpy(self, sim3: pp.Sim3) -> Tuple[float, np.ndarray, np.ndarray]:
        """Convert pypose Sim3 to numpy s,R,t"""
        data = sim3.data.cpu().numpy()
        t = data[:3]
        q = data[3:7]  # [x,y,z,w]
        s = data[7]
        R_mat = R.from_quat(q).as_matrix()
        return s, R_mat, t

    def sequential_to_absolute_poses(
        self, sequential_transforms: List[Tuple[float, np.ndarray, np.ndarray]]
    ) -> torch.Tensor:
        """
        Convert sequential relative transforms to absolute pose sequence
        S_01, S_12, S_23, ... -> T_0, T_1, T_2, T_3, ...
        Where T_i is the transform from world coordinate to frame i
        """
        len(sequential_transforms) + 1
        poses = []

        identity = pp.Sim3(
            torch.tensor([0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 1.0, 1.0], device=self.device)
        )
        poses.append(identity)

        current_pose = identity
        for s, R_mat, t_vec in sequential_transforms:
            rel_transform = self.numpy_to_pypose_sim3(s, R_mat, t_vec)
            current_pose = current_pose @ rel_transform
            poses.append(current_pose)

        return torch.stack(poses)

    def absolute_to_sequential_transforms(
        self, absolute_poses: pp.Sim3
    ) -> List[Tuple[float, np.ndarray, np.ndarray]]:
        """
        Convert absolute pose sequence back to sequential relative transforms
        T_0, T_1, T_2, ... -> S_01, S_12, S_23, ...
        """
        sequential_transforms = []
        n = absolute_poses.shape[0]

        for i in range(n - 1):
            rel_transform = absolute_poses[i].Inv() @ absolute_poses[i + 1]
            s, R_mat, t_vec = self.pypose_sim3_to_numpy(rel_transform)
            sequential_transforms.append((s, R_mat, t_vec))

        return sequential_transforms

    def SE3_to_Sim3(self, x: torch.Tensor) -> pp.Sim3:
        """Convert SE3 to Sim3 (add unit scale)"""
        ones = torch.ones_like(x[..., :1])
        out = torch.cat((x, ones), dim=-1)
        return pp.Sim3(out)

    def build_loop_constraints(
        self, loop_constraints: List[Tuple[int, int, Tuple[float, np.ndarray, np.ndarray]]]
    ) -> Tuple[torch.Tensor, torch.Tensor, torch.Tensor]:
        """Build loop closure constraints"""
        if not loop_constraints:
            return (
                torch.empty(0, 8, device=self.device),
                torch.empty(0, dtype=torch.long),
                torch.empty(0, dtype=torch.long),
            )

        loop_transforms = []
        ii_loop = []
        jj_loop = []

        for i, j, (s, R_mat, t_vec) in loop_constraints:
            loop_sim3 = self.numpy_to_pypose_sim3(s, R_mat, t_vec)
            loop_transforms.append(loop_sim3.data)
            ii_loop.append(i)
            jj_loop.append(j)

        dSloop = pp.Sim3(torch.stack(loop_transforms))
        ii_loop = torch.tensor(ii_loop, dtype=torch.long, device=self.device)
        jj_loop = torch.tensor(jj_loop, dtype=torch.long, device=self.device)

        return dSloop, ii_loop, jj_loop

    def residual(self, Ginv, input_poses, dSloop, ii, jj, jacobian=False):
        """Compute residuals (modified from original code)"""

        def _residual(C, Gi, Gj):
            out = C @ pp.Exp(Gi) @ pp.Exp(Gj).Inv()
            return out.Log().tensor()

        pred_inv_poses = pp.Sim3(input_poses).Inv()

        n, _ = pred_inv_poses.shape
        if n > 1:
            kk = torch.arange(1, n, device=self.device)
            ll = kk - 1
            Ti = pred_inv_poses[kk]
            Tj = pred_inv_poses[ll]
            dSij = Tj @ Ti.Inv()
        else:
            kk = torch.empty(0, dtype=torch.long, device=self.device)
            ll = torch.empty(0, dtype=torch.long, device=self.device)
            dSij = pp.Sim3(torch.empty(0, 8, device=self.device))

        constants = (
            torch.cat((dSij.data, dSloop.data), dim=0) if dSloop.shape[0] > 0 else dSij.data
        )
        if constants.shape[0] > 0:
            constants = pp.Sim3(constants)
            iii = torch.cat((kk, ii))
            jjj = torch.cat((ll, jj))
            resid = _residual(constants, Ginv[iii], Ginv[jjj])
        else:
            iii = torch.empty(0, dtype=torch.long, device=self.device)
            jjj = torch.empty(0, dtype=torch.long, device=self.device)
            resid = torch.empty(0, device=self.device)

        if not jacobian:
            return resid

        if constants.shape[0] > 0:

            def batch_jacobian(func, x):
                def _func_sum(*x):
                    return func(*x).sum(dim=0)

                _, b, c = torch.autograd.functional.jacobian(_func_sum, x, vectorize=True)
                from einops import rearrange

                return rearrange(torch.stack((b, c)), "N O B I -> N B O I", N=2)

            J_Ginv_i, J_Ginv_j = batch_jacobian(_residual, (constants, Ginv[iii], Ginv[jjj]))
        else:
            J_Ginv_i = torch.empty(0, device=self.device)
            J_Ginv_j = torch.empty(0, device=self.device)

        return resid, (J_Ginv_i, J_Ginv_j, iii, jjj)

    def optimize(
        self,
        sequential_transforms: List[Tuple[float, np.ndarray, np.ndarray]],
        loop_constraints: List[Tuple[int, int, Tuple[float, np.ndarray, np.ndarray]]],
        max_iterations: int = None,
        lambda_init: float = None,
    ) -> List[Tuple[float, np.ndarray, np.ndarray]]:
        """
        Main optimization function

        Args:
            sequential_transforms: Input sequence of transforms
            loop_constraints: List of loop closure constraints
            max_iterations: Maximum iterations
            lambda_init: Initial lambda for L-M algorithm

        Returns:
            Optimized sequence of transforms
        """
        if max_iterations is None:
            max_iterations = self.config["Loop"]["SIM3_Optimizer"]["max_iterations"]
        if lambda_init is None:
            lambda_init = eval(self.config["Loop"]["SIM3_Optimizer"]["lambda_init"])

        input_poses = self.sequential_to_absolute_poses(sequential_transforms)

        dSloop, ii_loop, jj_loop = self.build_loop_constraints(loop_constraints)

        if len(loop_constraints) == 0:
            print("Warning: No loop constraints provided, returning original transforms")
            return sequential_transforms

        Ginv = pp.Sim3(input_poses).Inv().Log()
        lmbda = lambda_init
        residual_history = []

        print(
            f"Starting optimization with {len(sequential_transforms)} poses \
                and {len(loop_constraints)} loop constraints"
        )

        # L-M loop
        for itr in range(max_iterations):
            resid, (J_Ginv_i, J_Ginv_j, iii, jjj) = self.residual(
                Ginv, input_poses, dSloop, ii_loop, jj_loop, jacobian=True
            )

            if resid.numel() == 0:
                print("No residuals to optimize")
                break

            current_cost = resid.square().mean().item()
            residual_history.append(current_cost)

            try:  # Solve linear system
                begin_time = time.time()
                if self.solve_system_version == "cpp":
                    (delta_pose,) = sim3solve.solve_system(
                        J_Ginv_i, J_Ginv_j, iii, jjj, resid, 0.0, lmbda, -1
                    )
                elif self.solve_system_version == "python":
                    delta_pose = solve_system_py(
                        J_Ginv_i, J_Ginv_j, iii, jjj, resid, 0.0, lmbda, -1
                    )
                else:
                    print("Solver version has not been chosen! ('python' or 'cpp')")
                end_time = time.time()
            except Exception as e:
                print(f"Solver failed at iteration {itr}: {e}")
                break

            Ginv_tmp = Ginv + delta_pose

            new_resid = self.residual(Ginv_tmp, input_poses, dSloop, ii_loop, jj_loop)
            new_cost = new_resid.square().mean().item() if new_resid.numel() > 0 else float("inf")

            # L-M
            if new_cost < current_cost:
                Ginv = Ginv_tmp
                lmbda /= 2
                print(
                    f"Iteration {itr}: cost {current_cost:.14f} -> {new_cost:.14f} (accepted)",
                    end=" | ",
                )
            else:
                lmbda *= 2
                print(
                    f"Iteration {itr}: cost {current_cost:.14f} -> {new_cost:.14f} (rej)     ",
                    end=" | ",
                )  # more readible to accepted

            print(
                f"Time of solver ({self.solve_system_version}): \
                    {(end_time - begin_time)*1000:.4f} ms"
            )

            if (current_cost < 1e-5) and (itr >= 4):
                if len(residual_history) >= 5:
                    improvement_ratio = residual_history[-5] / residual_history[-1]
                    if improvement_ratio < 1.5:
                        print(f"Converged at iteration {itr}")
                        break

        optimized_absolute_poses = pp.Exp(Ginv).Inv()

        optimized_sequential = self.absolute_to_sequential_transforms(optimized_absolute_poses)

        print(
            f"Optimization completed. Final cost: \
                {residual_history[-1] if residual_history else 'N/A'}"
        )

        return optimized_sequential


# ======== TEST CODE ========


def create_ring_transforms(num_poses=6, radius=5.0, rot_noise_deg=2.0):
    """Generate a ring of Sim3 transforms with rotation, adding slight rotational noise"""
    transforms = []
    angle_step = 2 * np.pi / num_poses

    for i in range(num_poses):
        angle = angle_step

        # Main rotation (around Z-axis)
        R_z = R.from_euler("z", angle, degrees=False)

        # Add slight rotational noise (Gaussian noise in degrees)
        noise_angles_deg = np.random.normal(loc=0.0, scale=rot_noise_deg, size=3)
        R_noise = R.from_euler("xyz", noise_angles_deg, degrees=True)

        # Combine rotations
        R_mat = (R_noise * R_z).as_matrix()

        # Translation: simulate a circular trajectory
        t = np.array([radius * np.sin(angle), radius * (1 - np.cos(angle)), 0.0])

        s = np.random.uniform(0.8, 1.2)

        transforms.append((s, R_mat, t))

    return transforms


def example_usage():
    optimizer = Sim3LoopOptimizer(solve_system_version="cpp")

    # Build rotating ring
    sequential_transforms = create_ring_transforms(num_poses=20, radius=3.0)

    # Add loop closure constraint: from frame 5 back to frame 0
    loop_constraints = [
        (20, 0, (1.0, np.eye(3), np.zeros(3)))  # Temporary unit loop for simulation
    ]

    # Trajectory before/after optimization
    input_abs_poses = optimizer.sequential_to_absolute_poses(sequential_transforms)
    optimized_transforms = optimizer.optimize(sequential_transforms, loop_constraints)
    optimized_abs_poses = optimizer.sequential_to_absolute_poses(optimized_transforms)

    def extract_xyz(pose_tensor):
        poses = pose_tensor.cpu().numpy()
        return poses[:, 0], poses[:, 1], poses[:, 2]

    x0, y0, z0 = extract_xyz(input_abs_poses)
    x1, y1, z1 = extract_xyz(optimized_abs_poses)

    # Visualize trajectory
    import matplotlib
    import matplotlib.pyplot as plt

    matplotlib.use("Agg")

    plt.figure(figsize=(8, 6))
    plt.plot(x0, y0, "o--", label="Before Optimization")
    plt.plot(x1, y1, "o-", label="After Optimization")
    for i, j, _ in loop_constraints:
        plt.plot([x0[i], x0[j]], [y0[i], y0[j]], "r--", label="Loop (Before)" if i == 5 else "")
        plt.plot([x1[i], x1[j]], [y1[i], y1[j]], "g-", label="Loop (After)" if i == 5 else "")
    plt.gca().set_aspect("equal")
    plt.title("Sim3 Loop Closure Optimization (Rotating Ring)")
    plt.xlabel("x")
    plt.ylabel("y")
    plt.legend()
    plt.grid(True)
    plt.axis("equal")
    plt.show()

    return optimized_transforms


if __name__ == "__main__":
    example_usage()



================================================
FILE: da3_streaming/loop_utils/sim3utils.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
# Adapted from [VGGT-Long](https://github.com/DengKaiCQ/VGGT-Long)

import bisect
import glob
import os
import numpy as np
import trimesh
from loop_utils.alignment_torch import robust_weighted_estimate_sim3_torch
from loop_utils.alignment_triton import robust_weighted_estimate_sim3_triton
from numba import njit
from sklearn.linear_model import LinearRegression, RANSACRegressor


def accumulate_sim3_transforms(transforms):
    """
    Accumulate adjacent SIM(3) transforms into transforms
    from the initial frame to each subsequent frame.

    Args:
    transforms: list, each element is a tuple (R, s, t)
        R: 3x3 rotation matrix (np.array)
        s: scale factor (scalar)
        t: 3x1 translation vector (np.array)

    Returns:
    Cumulative transforms list, each element is (R_cum, s_cum, t_cum)
        representing the transform from frame 0 to frame k
    """
    if not transforms:
        return []

    cumulative_transforms = [transforms[0]]

    for i in range(1, len(transforms)):
        s_cum_prev, R_cum_prev, t_cum_prev = cumulative_transforms[i - 1]
        s_next, R_next, t_next = transforms[i]
        R_cum_new = R_cum_prev @ R_next
        s_cum_new = s_cum_prev * s_next
        t_cum_new = s_cum_prev * (R_cum_prev @ t_next) + t_cum_prev
        cumulative_transforms.append((s_cum_new, R_cum_new, t_cum_new))

    return cumulative_transforms


def estimate_sim3(source_points, target_points):
    mu_src = np.mean(source_points, axis=0)
    mu_tgt = np.mean(target_points, axis=0)

    src_centered = source_points - mu_src
    tgt_centered = target_points - mu_tgt

    scale_src = np.sqrt((src_centered**2).sum(axis=1).mean())
    scale_tgt = np.sqrt((tgt_centered**2).sum(axis=1).mean())
    s = scale_tgt / scale_src

    src_scaled = src_centered * s

    H = src_scaled.T @ tgt_centered
    U, _, Vt = np.linalg.svd(H)
    R = Vt.T @ U.T
    if np.linalg.det(R) < 0:
        Vt[2, :] *= -1
        R = Vt.T @ U.T

    t = mu_tgt - s * R @ mu_src
    return s, R, t


def align_point_maps(point_map1, conf1, point_map2, conf2, conf_threshold):
    """point_map2 -> point_map1"""
    b1, _, _, _ = point_map1.shape
    b2, _, _, _ = point_map2.shape
    b = min(b1, b2)

    aligned_points1 = []
    aligned_points2 = []

    for i in range(b):
        mask1 = conf1[i] > conf_threshold
        mask2 = conf2[i] > conf_threshold
        valid_mask = mask1 & mask2

        idx = np.where(valid_mask)
        if len(idx[0]) == 0:
            continue

        pts1 = point_map1[i][idx]
        pts2 = point_map2[i][idx]

        aligned_points1.append(pts1)
        aligned_points2.append(pts2)

    if len(aligned_points1) == 0:
        raise ValueError("No matching point pairs were found!")

    all_pts1 = np.concatenate(aligned_points1, axis=0)
    all_pts2 = np.concatenate(aligned_points2, axis=0)

    print(f"The number of corresponding points matched: {all_pts1.shape[0]}")
    s, R, t = estimate_sim3(all_pts2, all_pts1)

    mean_error = compute_alignment_error(
        point_map1, conf1, point_map2, conf2, conf_threshold, s, R, t
    )
    print(f"Mean error: {mean_error}")

    return s, R, t


def apply_sim3(points, s, R, t):
    return (s * (R @ points.T)).T + t


def apply_sim3_direct(point_maps, s, R, t):
    # point_maps: (b, h, w, 3) -> (b, h, w, 3, 1)
    point_maps_expanded = point_maps[..., np.newaxis]  # (b, h, w, 3, 1)

    # R: (3, 3) -> (b, h, w, 3, 1) = (3, 3) @ (3, 1)
    rotated = np.matmul(R, point_maps_expanded)  # (b, h, w, 3, 1)
    rotated = rotated.squeeze(-1)  # (b, h, w, 3)
    transformed = s * rotated + t  # (b, h, w, 3)

    return transformed


def compute_alignment_error(point_map1, conf1, point_map2, conf2, conf_threshold, s, R, t):
    """
    Compute the average point alignment error (using only original inputs)

    Args:
    point_map1: target point map (b, h, w, 3)
    conf1: target confidence map (b, h, w)
    point_map2: source point map (b, h, w, 3)
    conf2: source confidence map (b, h, w)
    conf_threshold: confidence threshold
    s, R, t: transformation parameters
    """
    b1, h1, w1, _ = point_map1.shape
    b2, h2, w2, _ = point_map2.shape
    b = min(b1, b2)
    h = min(h1, h2)
    w = min(w1, w2)

    target_points = []
    source_points = []

    for i in range(b):
        mask1 = conf1[i, :h, :w] > conf_threshold
        mask2 = conf2[i, :h, :w] > conf_threshold
        valid_mask = mask1 & mask2

        idx = np.where(valid_mask)
        if len(idx[0]) == 0:
            continue

        t_pts = point_map1[i, :h, :w][idx]
        s_pts = point_map2[i, :h, :w][idx]

        target_points.append(t_pts)
        source_points.append(s_pts)

    if len(target_points) == 0:
        print("Warning: No matching point pairs found for error calculation")
        return np.nan

    all_target = np.concatenate(target_points, axis=0)
    all_source = np.concatenate(source_points, axis=0)

    transformed = (s * (R @ all_source.T)).T + t

    errors = np.linalg.norm(transformed - all_target, axis=1)

    mean_error = np.mean(errors)
    std_error = np.std(errors)
    median_error = np.median(errors)
    max_error = np.max(errors)

    print(
        f"Alignment error statistics [using {len(errors)} points]: "
        f"mean={mean_error:.4f}, std={std_error:.4f}, "
        f"median={median_error:.4f}, max={max_error:.4f}"
    )

    return mean_error


def save_confident_pointcloud(
    points, colors, confs, output_path, conf_threshold, sample_ratio=1.0
):
    """
    Filter points based on confidence threshold
    and save as PLY file, with optional random sampling ratio.

    Args:
    - points: np.ndarray, shape (H, W, 3) or (N, 3)
    - colors: np.ndarray, shape (H, W, 3) or (N, 3)
    - confs: np.ndarray, shape (H, W) or (N,)
    - output_path: str, output PLY file path
    - conf_threshold: float, confidence threshold for point filtering
    - sample_ratio: float, sampling ratio (0 < sample_ratio <= 1.0)
    """
    points = points.reshape(-1, 3).astype(np.float32, copy=False)
    colors = colors.reshape(-1, 3).astype(np.uint8, copy=False)
    confs = confs.reshape(-1).astype(np.float32, copy=False)

    conf_mask = (confs >= conf_threshold) & (confs > 1e-5)
    points = points[conf_mask]
    colors = colors[conf_mask]

    if 0 < sample_ratio < 1.0 and len(points) > 0:
        num_samples = int(len(points) * sample_ratio)
        indices = np.random.choice(len(points), num_samples, replace=False)
        points = points[indices]
        colors = colors[indices]

    os.makedirs(os.path.dirname(os.path.abspath(output_path)), exist_ok=True)

    print(f"shape of sampled point: {points.shape}")
    trimesh.PointCloud(points, colors=colors).export(output_path)
    print(f"Saved point cloud with {len(points)} points to {output_path}")


def save_confident_pointcloud_batch(
    points, colors, confs, output_path, conf_threshold, sample_ratio=1.0, batch_size=1000000
):
    """
    - points: np.ndarray,  (b, H, W, 3) / (N, 3)
    - colors: np.ndarray,  (b, H, W, 3) / (N, 3)
    - confs: np.ndarray,  (b, H, W) / (N,)
    - output_path: str
    - conf_threshold: float,
    - sample_ratio: float (0 < sample_ratio <= 1.0)
    - batch_size: int
    """
    if points.ndim == 2:
        b = 1
        points = points[np.newaxis, ...]
        colors = colors[np.newaxis, ...]
        confs = confs[np.newaxis, ...]
    elif points.ndim == 4:
        b = points.shape[0]
    else:
        raise ValueError("Unsupported points dimension. Must be 2 (N,3) or 4 (b,H,W,3)")

    total_valid = 0
    for i in range(b):
        cfs = confs[i].reshape(-1)
        total_valid += np.count_nonzero((cfs >= conf_threshold) & (cfs > 1e-5))

    num_samples = int(total_valid * sample_ratio) if sample_ratio < 1.0 else total_valid

    if num_samples == 0:
        save_ply(np.zeros((0, 3), dtype=np.float32), np.zeros((0, 3), dtype=np.uint8), output_path)
        return

    if sample_ratio == 1.0:
        with open(output_path, "wb") as f:
            write_ply_header(f, num_samples)

            for i in range(b):
                pts = points[i].reshape(-1, 3).astype(np.float32)
                cls = colors[i].reshape(-1, 3).astype(np.uint8)
                cfs = confs[i].reshape(-1).astype(np.float32)

                mask = (cfs >= conf_threshold) & (cfs > 1e-5)
                valid_pts = pts[mask]
                valid_cls = cls[mask]

                for j in range(0, len(valid_pts), batch_size):
                    batch_pts = valid_pts[j : j + batch_size]
                    batch_cls = valid_cls[j : j + batch_size]
                    write_ply_batch(f, batch_pts, batch_cls)

    else:
        reservoir_pts = np.zeros((num_samples, 3), dtype=np.float32)
        reservoir_clr = np.zeros((num_samples, 3), dtype=np.uint8)
        count = 0

        for i in range(b):
            pts = points[i].reshape(-1, 3).astype(np.float32)
            cls = colors[i].reshape(-1, 3).astype(np.uint8)
            cfs = confs[i].reshape(-1).astype(np.float32)

            mask = (cfs >= conf_threshold) & (cfs > 1e-5)
            valid_pts = pts[mask]
            valid_cls = cls[mask]
            n_valid = len(valid_pts)

            if count < num_samples:
                fill_count = min(num_samples - count, n_valid)

                reservoir_pts[count : count + fill_count] = valid_pts[:fill_count]
                reservoir_clr[count : count + fill_count] = valid_cls[:fill_count]
                count += fill_count

                if fill_count < n_valid:
                    remaining_pts = valid_pts[fill_count:]
                    remaining_cls = valid_cls[fill_count:]

                    count, reservoir_pts, reservoir_clr = optimized_vectorized_reservoir_sampling(
                        remaining_pts, remaining_cls, count, reservoir_pts, reservoir_clr
                    )
            else:
                count, reservoir_pts, reservoir_clr = optimized_vectorized_reservoir_sampling(
                    valid_pts, valid_cls, count, reservoir_pts, reservoir_clr
                )

        save_ply(reservoir_pts, reservoir_clr, output_path)


""" The following function is deprecated"""

# def vectorized_reservoir_sampling(new_pts, new_cls, current_count, reservoir_pts, reservoir_clr):
#     """
#     - new_pts:  (M, 3)
#     - new_cls:  (M, 3)
#     - current_count
#     - reservoir_pts:  (K, 3)
#     - reservoir_clr:  (K, 3)

#     """
#     k = len(reservoir_pts)
#     n_new = len(new_pts)

#     rand_indices = np.random.randint(0, current_count + n_new, size=n_new)

#     replace_mask = rand_indices < k
#     replace_indices = rand_indices[replace_mask]
#     replace_pts = new_pts[replace_mask]
#     replace_cls = new_cls[replace_mask]

#     reservoir_pts[replace_indices] = replace_pts
#     reservoir_clr[replace_indices] = replace_cls

#     return current_count + n_new, reservoir_pts, reservoir_clr


"""
    Function `vectorized_reservoir_sampling`  is not mathematically accurate in sampling.
    This leads to inconsistent density in the downsampled point clouds.
    The `optimized_vectorized_reservoir_sampling` function has fixed this bug.

    Special thanks to @Horace89 for the detailed analysis and code assistance.

    See https://github.com/DengKaiCQ/VGGT-Long/issues/28 for details
"""


def optimized_vectorized_reservoir_sampling(
    new_points: np.ndarray,
    new_colors: np.ndarray,
    current_count: int,
    reservoir_points: np.ndarray,
    reservoir_colors: np.ndarray,
) -> tuple[int, np.ndarray, np.ndarray]:
    """
    Optimized vectorized reservoir sampling with batch probability calculations.

    This maintains mathematical correctness while improving performance through
    vectorized operations where possible.

    Args:
        new_points: New point coordinates to consider, shape (M, 3)
        new_colors: New point colors to consider, shape (M, 3)
        current_count: Number of elements seen so far
        reservoir_points: Current reservoir of sampled points, shape (K, 3)
        reservoir_colors: Current reservoir of sampled colors, shape (K, 3)

    Returns:
        Tuple of (updated_count, updated_reservoir_points, updated_reservoir_colors)
    """
    random_gen = np.random

    reservoir_size = len(reservoir_points)
    num_new_points = len(new_points)

    if num_new_points == 0:
        return current_count, reservoir_points, reservoir_colors

    # Calculate sequential indices for each new point
    point_indices = np.arange(current_count + 1, current_count + num_new_points + 1)

    # Generate random numbers for each point
    random_values = random_gen.randint(0, point_indices, size=num_new_points)

    # Determine which points should replace reservoir elements
    replacement_mask = random_values < reservoir_size
    replacement_positions = random_values[replacement_mask]

    # Apply replacements
    if np.any(replacement_mask):
        points_to_replace = new_points[replacement_mask]
        colors_to_replace = new_colors[replacement_mask]

        reservoir_points[replacement_positions] = points_to_replace
        reservoir_colors[replacement_positions] = colors_to_replace

    return current_count + num_new_points, reservoir_points, reservoir_colors


def write_ply_header(f, num_vertices):
    header = [
        "ply",
        "format binary_little_endian 1.0",
        f"element vertex {num_vertices}",
        "property float x",
        "property float y",
        "property float z",
        "property uchar red",
        "property uchar green",
        "property uchar blue",
        "end_header",
    ]
    f.write("\n".join(header).encode() + b"\n")


def write_ply_batch(f, points, colors):
    structured = np.zeros(
        len(points),
        dtype=[
            ("x", np.float32),
            ("y", np.float32),
            ("z", np.float32),
            ("red", np.uint8),
            ("green", np.uint8),
            ("blue", np.uint8),
        ],
    )

    structured["x"] = points[:, 0]
    structured["y"] = points[:, 1]
    structured["z"] = points[:, 2]
    structured["red"] = colors[:, 0]
    structured["green"] = colors[:, 1]
    structured["blue"] = colors[:, 2]

    f.write(structured.tobytes())


def save_ply(points, colors, filename):
    with open(filename, "wb") as f:
        write_ply_header(f, len(points))
        write_ply_batch(f, points, colors)


def find_chunk_index(chunks, idx):
    """
    Find the 0-based chunk index that contains the given index idx.
    chunks: List of (begin_idx, end_idx).
    idx: The index to search for.
    Returns the 0-based chunk index.
    """
    starts = [chunk[0] for chunk in chunks]
    pos = bisect.bisect_right(starts, idx) - 1  # Find position of idx in starts
    if pos < 0 or pos >= len(chunks):
        raise ValueError(f"Index {idx} not found in any chunk")
    chunk_begin, chunk_end = chunks[pos]
    if idx < chunk_begin or idx > chunk_end:
        raise ValueError(f"Index {idx} not found in any chunk")
    return pos


def get_frame_range(chunk, idx, half_window=10):
    """
    Calculate the frame range centered at idx with half_window
    frames on each side within chunk boundaries.
    If near boundaries, take 2 * half_window frames starting from the boundary.
    chunk: (begin_idx, end_idx).
    idx: Center index.
    half_window: Number of frames to take on each side of center index.
    Returns (start, end).
    """
    begin, end = chunk
    window_size = 2 * half_window

    if idx - half_window < begin:
        start = begin
        end_candidate = begin + window_size
        end = min(end, end_candidate)

    elif idx + half_window > end:
        end_candidate = end
        start_candidate = end - window_size
        start = max(begin, start_candidate)

    else:
        start = idx - half_window
        end = idx + half_window
    return (start, end)


def process_loop_list(chunk_index, loop_list, half_window=10):
    """
    Process loop_list and return chunk indices and frame ranges for each (idx1, idx2) pair.
    chunk_index: List of (begin_idx, end_idx) tuples.
    loop_list: List of (idx1, idx2) tuples.
    half_window: Number of frames to take on each side of center index (default 10).
    Returns list of (chunk_idx1, range1, chunk_idx2, range2) tuples where:
      - chunk_idx1, chunk_idx2: Chunk indices (1-based).
      - range1, range2: Frame range tuples (start, end).
    """
    results = []
    for idx1, idx2 in loop_list:
        try:
            chunk_idx1_0based = find_chunk_index(chunk_index, idx1)
            chunk1 = chunk_index[chunk_idx1_0based]
            range1 = get_frame_range(chunk1, idx1, half_window)

            chunk_idx2_0based = find_chunk_index(chunk_index, idx2)
            chunk2 = chunk_index[chunk_idx2_0based]
            range2 = get_frame_range(chunk2, idx2, half_window)

            result = (chunk_idx1_0based, range1, chunk_idx2_0based, range2)
            results.append(result)
        except ValueError as e:
            print(f"Skipping pair ({idx1}, {idx2}): {e}")
    return results


def compute_sim3_ab(S_a, S_b):

    s_a, R_a, T_a = S_a
    s_b, R_b, T_b = S_b

    s_ab = s_b / s_a
    R_ab = R_b @ R_a.T
    T_ab = T_b - s_ab * (R_ab @ T_a)

    return (s_ab, R_ab, T_ab)


def merge_ply_files(input_dir, output_path):
    """
    Merge all PLY files in a directory into one file (without loading into memory)

    Args:
    - input_dir: Input directory containing multiple '{idx}_pcd.ply' files
    - output_path: Output file path (e.g., 'combined.ply')
    """

    print("Merging PLY files...")

    input_files = sorted(glob.glob(os.path.join(input_dir, "*_pcd.ply")))

    if not input_files:
        print("No PLY files found")
        return

    idx_file = 0
    len(input_files)

    total_vertices = 0
    for file in input_files:  # Count total vertices
        with open(file, "rb") as f:
            for line in f:
                if line.startswith(b"element vertex"):
                    vertex_count = int(line.split()[-1])
                    total_vertices += vertex_count
                elif line.startswith(b"end_header"):
                    break

    with open(output_path, "wb") as out_f:
        # Write new header
        out_f.write(b"ply\n")
        out_f.write(b"format binary_little_endian 1.0\n")
        out_f.write(f"element vertex {total_vertices}\n".encode())
        out_f.write(b"property float x\n")
        out_f.write(b"property float y\n")
        out_f.write(b"property float z\n")
        out_f.write(b"property uchar red\n")
        out_f.write(b"property uchar green\n")
        out_f.write(b"property uchar blue\n")
        out_f.write(b"end_header\n")

        for file in input_files:
            print(f"Processing {idx_file}/{len(input_files)}: {file}")
            idx_file += 1
            with open(file, "rb") as in_f:
                # Skip the head
                in_header = True
                while in_header:
                    line = in_f.readline()
                    if line.startswith(b"end_header"):
                        in_header = False
                data = in_f.read()
                out_f.write(data)

    print(f"Merge completed! Total points: {total_vertices}")
    print(f"Output file: {output_path}")


def weighted_estimate_se3(source_points, target_points, weights):
    """
    source_points:  (Nx3)
    target_points:  (Nx3)
    :weights:  (N,) [0,1]
    """
    total_weight = np.sum(weights)
    if total_weight < 1e-6:
        raise ValueError("Total weight too small for meaningful estimation")

    normalized_weights = weights / total_weight

    mu_src = np.sum(normalized_weights[:, None] * source_points, axis=0)
    mu_tgt = np.sum(normalized_weights[:, None] * target_points, axis=0)

    src_centered = source_points - mu_src
    tgt_centered = target_points - mu_tgt

    weighted_src = src_centered * np.sqrt(normalized_weights)[:, None]
    weighted_tgt = tgt_centered * np.sqrt(normalized_weights)[:, None]

    H = weighted_src.T @ weighted_tgt

    U, _, Vt = np.linalg.svd(H)
    R = Vt.T @ U.T

    if np.linalg.det(R) < 0:
        Vt[2, :] *= -1
        R = Vt.T @ U.T

    t = mu_tgt - R @ mu_src

    return 1.0, R, t


def weighted_estimate_sim3(source_points, target_points, weights):
    """
    source_points:  (Nx3)
    target_points:  (Nx3)
    :weights:  (N,) [0,1]
    """
    total_weight = np.sum(weights)
    if total_weight < 1e-6:
        raise ValueError("Total weight too small for meaningful estimation")

    normalized_weights = weights / total_weight

    mu_src = np.sum(normalized_weights[:, None] * source_points, axis=0)
    mu_tgt = np.sum(normalized_weights[:, None] * target_points, axis=0)

    src_centered = source_points - mu_src
    tgt_centered = target_points - mu_tgt

    scale_src = np.sqrt(np.sum(normalized_weights * np.sum(src_centered**2, axis=1)))
    scale_tgt = np.sqrt(np.sum(normalized_weights * np.sum(tgt_centered**2, axis=1)))
    s = scale_tgt / scale_src

    weighted_src = (s * src_centered) * np.sqrt(normalized_weights)[:, None]
    weighted_tgt = tgt_centered * np.sqrt(normalized_weights)[:, None]

    H = weighted_src.T @ weighted_tgt

    U, _, Vt = np.linalg.svd(H)
    R = Vt.T @ U.T

    if np.linalg.det(R) < 0:
        Vt[2, :] *= -1
        R = Vt.T @ U.T

    t = mu_tgt - s * R @ mu_src
    return s, R, t


def huber_loss(r, delta):
    abs_r = np.abs(r)
    return np.where(abs_r <= delta, 0.5 * r**2, delta * (abs_r - 0.5 * delta))


def robust_weighted_estimate_sim3(
    src, tgt, init_weights, delta=0.1, max_iters=20, tol=1e-9, align_method="sim3"
):
    """
    src:  (Nx3)
    tgt:  (Nx3)
    init_weights:  (N,)
    """
    if align_method == "sim3":
        s, R, t = weighted_estimate_sim3(src, tgt, init_weights)
    elif align_method == "se3" or align_method == "scale+se3":
        s, R, t = weighted_estimate_se3(src, tgt, init_weights)

    prev_error = float("inf")

    for iter in range(max_iters):

        transformed = s * (src @ R.T) + t
        residuals = np.linalg.norm(tgt - transformed, axis=1)  # (N,)
        print(f"Residuals: {np.mean(residuals)}")

        abs_res = np.abs(residuals)
        huber_weights = np.ones_like(residuals)
        large_res_mask = abs_res > delta
        huber_weights[large_res_mask] = delta / abs_res[large_res_mask]

        combined_weights = init_weights * huber_weights

        combined_weights /= np.sum(combined_weights) + 1e-12

        if align_method == "se3":
            s_new, R_new, t_new = weighted_estimate_se3(src, tgt, combined_weights)
        elif align_method == "sim3" or align_method == "scale+se3":
            s_new, R_new, t_new = weighted_estimate_sim3(src, tgt, combined_weights)

        param_change = np.abs(s_new - s) + np.linalg.norm(t_new - t)
        rot_angle = np.arccos(min(1.0, max(-1.0, (np.trace(R_new @ R.T) - 1) / 2)))
        current_error = np.sum(huber_loss(residuals, delta) * init_weights)

        if (param_change < tol and rot_angle < np.radians(0.1)) or (
            abs(prev_error - current_error) < tol * prev_error
        ):
            break

        s, R, t = s_new, R_new, t_new
        prev_error = current_error

    return s, R, t


# ===== Speed Up Begin =====


@njit(cache=True)
def _weighted_estimate_se3_numba(source_points, target_points, weights):
    # Ensure float32
    source_points = source_points.astype(np.float32)
    target_points = target_points.astype(np.float32)
    weights = weights.astype(np.float32)

    total_weight = np.sum(weights)
    if total_weight < 1e-6:
        return (
            1.0,
            np.zeros(3, dtype=np.float32),
            np.zeros(3, dtype=np.float32),
            np.zeros((3, 3), dtype=np.float32),
        )

    normalized_weights = weights / total_weight

    mu_src = np.sum(normalized_weights[:, None] * source_points, axis=0)
    mu_tgt = np.sum(normalized_weights[:, None] * target_points, axis=0)

    src_centered = source_points - mu_src
    tgt_centered = target_points - mu_tgt

    weighted_src = src_centered * np.sqrt(normalized_weights)[:, None]
    weighted_tgt = tgt_centered * np.sqrt(normalized_weights)[:, None]

    H = weighted_src.T @ weighted_tgt

    return 1.0, mu_src, mu_tgt, H


@njit(cache=True)
def _weighted_estimate_sim3_numba(source_points, target_points, weights):
    # Ensure float32
    source_points = source_points.astype(np.float32)
    target_points = target_points.astype(np.float32)
    weights = weights.astype(np.float32)

    total_weight = np.sum(weights)
    if total_weight < 1e-6:
        return (
            -1.0,
            np.zeros(3, dtype=np.float32),
            np.zeros(3, dtype=np.float32),
            np.zeros((3, 3), dtype=np.float32),
        )

    normalized_weights = weights / total_weight

    mu_src = np.sum(normalized_weights[:, None] * source_points, axis=0)
    mu_tgt = np.sum(normalized_weights[:, None] * target_points, axis=0)

    src_centered = source_points - mu_src
    tgt_centered = target_points - mu_tgt

    scale_src = np.sqrt(np.sum(normalized_weights * np.sum(src_centered**2, axis=1)))
    scale_tgt = np.sqrt(np.sum(normalized_weights * np.sum(tgt_centered**2, axis=1)))
    s = scale_tgt / scale_src

    weighted_src = (s * src_centered) * np.sqrt(normalized_weights)[:, None]
    weighted_tgt = tgt_centered * np.sqrt(normalized_weights)[:, None]

    H = weighted_src.T @ weighted_tgt

    return s, mu_src, mu_tgt, H


def weighted_estimate_sim3_numba(source_points, target_points, weights, align_method="sim3"):
    if align_method == "sim3":
        s, mu_src, mu_tgt, H = _weighted_estimate_sim3_numba(source_points, target_points, weights)
    elif align_method == "se3" or align_method == "scale+se3":
        s, mu_src, mu_tgt, H = _weighted_estimate_se3_numba(source_points, target_points, weights)

    if s < 0:
        raise ValueError("Total weight too small for meaningful estimation")

    # Ensure float32
    H = H.astype(np.float32)
    U, _, Vt = np.linalg.svd(H.astype(np.float32))  # float32 SVD

    R = Vt.T @ U.T
    if np.linalg.det(R) < 0:
        Vt[2, :] *= -1
        R = Vt.T @ U.T

    if align_method == "se3" or align_method == "scale+se3":
        t = mu_tgt - R @ mu_src
    else:
        t = mu_tgt - s * R @ mu_src

    return s, R, t


@njit(cache=True)
def huber_loss_numba(r, delta):
    r = r.astype(np.float32)
    delta = np.float32(delta)
    abs_r = np.abs(r)
    result = np.where(abs_r <= delta, 0.5 * r**2, delta * (abs_r - 0.5 * delta))
    return result.astype(np.float32)


@njit(cache=True)
def compute_residuals_numba(tgt, transformed):
    residuals = np.empty(tgt.shape[0], dtype=np.float32)
    for i in range(tgt.shape[0]):
        diff = tgt[i] - transformed[i]
        residuals[i] = np.sqrt(np.sum(diff**2))
    return residuals


@njit(cache=True)
def compute_huber_weights_numba(residuals, delta):
    weights = np.ones(residuals.shape, dtype=np.float32)
    for i in range(residuals.shape[0]):
        r = residuals[i]
        if r > delta:
            weights[i] = delta / r
    return weights


@njit(cache=True)
def apply_transformation_numba(src, s, R, t):
    transformed = np.empty_like(src)
    for i in range(src.shape[0]):
        p = src[i]
        transformed[i] = s * (R @ p) + t
    return transformed


def robust_weighted_estimate_sim3_numba(
    src, tgt, init_weights, delta=0.1, max_iters=20, tol=1e-9, align_method="sim3"
):
    src = src.astype(np.float32)
    tgt = tgt.astype(np.float32)
    init_weights = init_weights.astype(np.float32)

    s, R, t = weighted_estimate_sim3_numba(src, tgt, init_weights, align_method=align_method)

    prev_error = float("inf")

    for iter in range(max_iters):
        transformed = apply_transformation_numba(src, s, R, t)
        residuals = compute_residuals_numba(tgt, transformed)

        print(f"Residuals: {np.mean(residuals)}")

        huber_weights = compute_huber_weights_numba(residuals, delta)
        combined_weights = init_weights * huber_weights
        combined_weights /= np.sum(combined_weights) + 1e-12

        s_new, R_new, t_new = weighted_estimate_sim3_numba(
            src, tgt, combined_weights, align_method=align_method
        )

        param_change = np.abs(s_new - s) + np.linalg.norm(t_new - t)
        rot_angle = np.arccos(min(1.0, max(-1.0, (np.trace(R_new @ R.T) - 1) / 2)))

        current_error = np.sum(huber_loss_numba(residuals, delta) * init_weights)

        if (param_change < tol and rot_angle < np.radians(0.1)) or (
            abs(prev_error - current_error) < tol * prev_error
        ):
            break

        s, R, t = s_new, R_new, t_new
        prev_error = current_error

    return s, R, t


def warmup_numba():

    print("\nWarming up Numba JIT-compiled functions...")

    src = np.random.randn(50000, 3).astype(np.float32)
    tgt = np.random.randn(50000, 3).astype(np.float32)
    weights = np.ones(50000, dtype=np.float32)
    residuals = np.abs(np.random.randn(50000).astype(np.float32))
    R = np.eye(3, dtype=np.float32)
    t = np.zeros(3, dtype=np.float32)
    s = np.float32(1.0)
    delta = np.float32(1.0)

    try:
        _ = _weighted_estimate_sim3_numba(src, tgt, weights)
        print(" - _weighted_estimate_sim3_numba warmed up.")
    except Exception as e:
        print(" ! Failed to warm up _weighted_estimate_sim3_numba:", e)

    try:
        _ = _weighted_estimate_se3_numba(src, tgt, weights)
        print(" - _weighted_estimate_se3_numba warmed up.")
    except Exception as e:
        print(" ! Failed to warm up _weighted_estimate_se3_numba:", e)

    try:
        _ = huber_loss_numba(residuals, delta)
        print(" - huber_loss_numba warmed up.")
    except Exception as e:
        print(" ! Failed to warm up huber_loss_numba:", e)

    try:
        _ = compute_huber_weights_numba(residuals, delta)
        print(" - compute_huber_weights_numba warmed up.")
    except Exception as e:
        print(" ! Failed to warm up compute_huber_weights_numba:", e)

    try:
        _ = compute_residuals_numba(tgt, src)
        print(" - compute_residuals_numba warmed up.")
    except Exception as e:
        print(" ! Failed to warm up compute_residuals_numba:", e)

    try:
        _ = apply_transformation_numba(src, s, R, t)
        print(" - apply_transformation_numba warmed up.")
    except Exception as e:
        print(" ! Failed to warm up apply_transformation_numba:", e)

    print("Numba warm-up complete.\n")


# ===== Speed Up End =====

# ===== Scale precompute begin =====


def compute_scale_ransac(
    depth1, depth2, conf1, conf2, conf_threshold_ratio=0.1, max_samples=10000
):
    """
    Args:
        depth1: (n1, h, w)
        depth2: (n2, h, w)
        conf1: (n1, h, w)
        conf2: (n2, h, w)

    """

    depth1_flat = depth1.reshape(-1)
    depth2_flat = depth2.reshape(-1)
    conf1_flat = conf1.reshape(-1)
    conf2_flat = conf2.reshape(-1)

    conf_threshold = max(
        np.median(conf1_flat) * conf_threshold_ratio,
        np.median(conf2_flat) * conf_threshold_ratio,
        1e-6,
    )

    valid_mask = (
        (conf1_flat > conf_threshold)
        & (conf2_flat > conf_threshold)
        & (depth1_flat > 1e-3)
        & (depth2_flat > 1e-3)
        & (depth1_flat < 100)
        & (depth2_flat < 100)
    )

    if np.sum(valid_mask) < 100:
        print(f"Warning: Only {np.sum(valid_mask)} valid points, using default scale 1.0")
        return 1.0, 0.0

    valid_depth1 = depth1_flat[valid_mask]
    valid_depth2 = depth2_flat[valid_mask]

    if len(valid_depth1) > max_samples:
        indices = np.random.choice(len(valid_depth1), max_samples, replace=False)
        valid_depth1 = valid_depth1[indices]
        valid_depth2 = valid_depth2[indices]

    X = valid_depth2.reshape(-1, 1)
    y = valid_depth1

    base_estimator = LinearRegression(fit_intercept=False)
    ransac = RANSACRegressor(
        estimator=base_estimator,
        max_trials=1000,
        min_samples=max(10, len(X) // 100),
        residual_threshold=0.1,
        random_state=42,
    )

    ransac.fit(X, y)
    scale_factor = ransac.estimator_.coef_[0]
    inlier_mask = ransac.inlier_mask_
    inlier_ratio = np.sum(inlier_mask) / len(inlier_mask)

    print(f"RANSAC scale: {scale_factor:.6f}, inlier ratio: {inlier_ratio:.4f}")

    if 0.1 < scale_factor < 10.0:
        return scale_factor, inlier_ratio
    else:
        print(f"Warning: Unreasonable scale {scale_factor}, using 1.0")
        return 1.0, inlier_ratio


def compute_scale_weighted(
    depth1, depth2, conf1, conf2, conf_threshold_ratio=0.1, weight_power=2.0, robust_quantile=0.9
):
    """
    Args:
        depth1: (n1, h, w)
        depth2: (n2, h, w)
        conf1: (n1, h, w)
        conf2: (n2, h, w)
    """
    depth1_flat = depth1.reshape(-1)
    depth2_flat = depth2.reshape(-1)
    conf1_flat = conf1.reshape(-1)
    conf2_flat = conf2.reshape(-1)

    conf_threshold = max(
        np.median(conf1_flat) * conf_threshold_ratio,
        np.median(conf2_flat) * conf_threshold_ratio,
        1e-6,
    )

    valid_mask = (
        (conf1_flat > conf_threshold)
        & (conf2_flat > conf_threshold)
        & (depth1_flat > 1e-3)
        & (depth2_flat > 1e-3)
        & (depth1_flat < 100)
        & (depth2_flat < 100)
    )

    if np.sum(valid_mask) < 100:
        print(f"Warning: Only {np.sum(valid_mask)} valid points, using default scale 1.0")
        return 1.0, 0.0

    valid_depth1 = depth1_flat[valid_mask]
    valid_depth2 = depth2_flat[valid_mask]
    valid_conf1 = conf1_flat[valid_mask]
    valid_conf2 = conf2_flat[valid_mask]

    combined_weights = (valid_conf1 * valid_conf2) ** weight_power

    combined_weights = combined_weights / (np.sum(combined_weights) + 1e-8)

    ratios = valid_depth1 / (valid_depth2 + 1e-8)

    sorted_indices = np.argsort(ratios)
    sorted_ratios = ratios[sorted_indices]
    sorted_weights = combined_weights[sorted_indices]

    cumulative_weights = np.cumsum(sorted_weights)
    median_idx = np.searchsorted(cumulative_weights, 0.5)
    scale_median = sorted_ratios[median_idx] if median_idx < len(sorted_ratios) else 1.0

    quantile_idx = np.searchsorted(cumulative_weights, robust_quantile)
    scale_quantile = (
        sorted_ratios[quantile_idx] if quantile_idx < len(sorted_ratios) else scale_median
    )

    weight_entropy = -np.sum(combined_weights * np.log(combined_weights + 1e-8))
    max_entropy = np.log(len(combined_weights))
    confidence_score = 1.0 - (weight_entropy / max_entropy) if max_entropy > 0 else 0.0

    print(f"Weighted scale: {scale_quantile:.6f}, confidence: {confidence_score:.4f}")

    if 0.1 < scale_quantile < 10.0:
        return scale_quantile, confidence_score
    else:
        print(f"Warning: Unreasonable scale {scale_quantile}, using 1.0")
        return 1.0, confidence_score


def compute_chunk_scale_advanced(depth1, depth2, conf1, conf2, method="auto"):
    """
    method: 'auto', 'ransac', 'weighted'
    """
    if method == "ransac":
        scale, score = compute_scale_ransac(depth1, depth2, conf1, conf2)
        return scale, score, "ransac"

    elif method == "weighted":
        scale, score = compute_scale_weighted(depth1, depth2, conf1, conf2)
        return scale, score, "weighted"

    elif method == "auto":
        scale_ransac, inlier_ratio = compute_scale_ransac(depth1, depth2, conf1, conf2)
        scale_weighted, conf_score = compute_scale_weighted(depth1, depth2, conf1, conf2)

        ransac_quality = inlier_ratio
        weighted_quality = conf_score

        print(f"RANSAC quality: {ransac_quality:.4f}, Weighted quality: {weighted_quality:.4f}")

        if ransac_quality > 0.7 and weighted_quality > 0.7:
            # both method are good, we take both of them by average
            final_scale = (scale_ransac + scale_weighted) / 2
            final_method = "average"
        elif ransac_quality > weighted_quality:
            final_scale = scale_ransac
            final_method = "ransac"
        else:
            final_scale = scale_weighted
            final_method = "weighted"

        final_quality = max(ransac_quality, weighted_quality)
        return final_scale, final_quality, final_method


def precompute_scale_chunks_with_depth(
    chunk1_depth, chunk1_conf, chunk2_depth, chunk2_conf, method="auto"
):
    """
    Args:
        chunk1_depth: (n1, h, w)
        chunk1_conf: (n1, h, w)
        chunk2_depth: (n2, h, w)
        chunk2_conf: (n2, h, w)
        method: 'auto', 'ransac', 'weighted'
    """

    scale_factor, quality_score, method_used = compute_chunk_scale_advanced(
        chunk1_depth, chunk2_depth, chunk1_conf, chunk2_conf, method
    )

    print(f"Final scale: {scale_factor:.6f}, quality: {quality_score:.4f}, method: {method_used}")

    return scale_factor, quality_score, method_used


# ===== Scale precompute end =====


def weighted_align_point_maps(
    point_map1, conf1, point_map2, conf2, conf_threshold, config, precompute_scale=None
):
    """point_map2 -> point_map1"""
    b1, _, _, _ = point_map1.shape
    b2, _, _, _ = point_map2.shape
    b = min(b1, b2)

    if precompute_scale is not None:  # meaning we are using align method 'scale+se3'
        point_map2 *= precompute_scale

    aligned_points1 = []
    aligned_points2 = []
    confidence_weights = []

    for i in range(b):
        mask1 = conf1[i] > conf_threshold
        mask2 = conf2[i] > conf_threshold
        valid_mask = mask1 & mask2

        idx = np.where(valid_mask)
        if len(idx[0]) == 0:
            continue

        pts1 = point_map1[i][idx]
        pts2 = point_map2[i][idx]

        combined_conf = np.sqrt(conf1[i][idx] * conf2[i][idx])

        aligned_points1.append(pts1)
        aligned_points2.append(pts2)
        confidence_weights.append(combined_conf)

    if len(aligned_points1) == 0:
        raise ValueError("No matching point pairs were found!")

    all_pts1 = np.concatenate(aligned_points1, axis=0)
    all_pts2 = np.concatenate(aligned_points2, axis=0)
    all_weights = np.concatenate(confidence_weights, axis=0)

    print(f"The number of corresponding points matched: {all_pts1.shape[0]}")

    if config["Model"]["align_lib"] == "numba":
        s, R, t = robust_weighted_estimate_sim3_numba(
            all_pts2,
            all_pts1,
            all_weights,
            delta=config["Model"]["IRLS"]["delta"],
            max_iters=config["Model"]["IRLS"]["max_iters"],
            tol=eval(config["Model"]["IRLS"]["tol"]),
            align_method=config["Model"]["align_method"],
        )
    elif config["Model"]["align_lib"] == "numpy":  # numpy
        s, R, t = robust_weighted_estimate_sim3(
            all_pts2,
            all_pts1,
            all_weights,
            delta=config["Model"]["IRLS"]["delta"],
            max_iters=config["Model"]["IRLS"]["max_iters"],
            tol=eval(config["Model"]["IRLS"]["tol"]),
            align_method=config["Model"]["align_method"],
        )
    elif config["Model"]["align_lib"] == "torch":  # torch
        s, R, t = robust_weighted_estimate_sim3_torch(
            all_pts2,
            all_pts1,
            all_weights,
            delta=config["Model"]["IRLS"]["delta"],
            max_iters=config["Model"]["IRLS"]["max_iters"],
            tol=eval(config["Model"]["IRLS"]["tol"]),
            align_method=config["Model"]["align_method"],
        )
    elif config["Model"]["align_lib"] == "triton":  # triton
        s, R, t = robust_weighted_estimate_sim3_triton(
            all_pts2,
            all_pts1,
            all_weights,
            delta=config["Model"]["IRLS"]["delta"],
            max_iters=config["Model"]["IRLS"]["max_iters"],
            tol=eval(config["Model"]["IRLS"]["tol"]),
            align_method=config["Model"]["align_method"],
        )
    else:
        raise ValueError(f"Unknown align_lib: {config['Model']['align_lib']}")

    if precompute_scale is not None:  # meaning we are using align method 'scale+se3'
        # we need this precompute_scale for loop align
        s = precompute_scale

    mean_error = compute_alignment_error(
        point_map1, conf1, point_map2, conf2, conf_threshold, s, R, t
    )
    print(f"Mean error: {mean_error}")

    return s, R, t



================================================
FILE: da3_streaming/scripts/download_weights.sh
================================================
#!/bin/bash

mkdir weights
cd ./weights

# SALAD (~ 340 MiB)
echo "Downloading SALAD weights (~ 340 MiB) ..."
SALAD_URL="https://github.com/serizba/salad/releases/download/v1.0.0/dino_salad.ckpt"
curl -L "$SALAD_URL" -o "./dino_salad.ckpt"


# DA3NESTED-GIANT-LARGE-1.1
echo "Downloading DA3NESTED-GIANT-LARGE-1.1 weights and config (~ 6.76 GiB)..."
BASE_URL="https://huggingface.co/depth-anything/DA3NESTED-GIANT-LARGE-1.1/resolve/main"

# download config.json (~ 3.1 KiB)
curl -L "$BASE_URL/config.json" -o "./config.json"

# download model.safetensors (~ 6.76 GiB)
curl -L "$BASE_URL/model.safetensors" -o "./model.safetensors"



================================================
FILE: docs/API.md
================================================
[Binary file]


================================================
FILE: docs/CLI.md
================================================
# 🚀 Depth Anything 3 Command Line Interface

## 📋 Table of Contents

- [📖 Overview](#overview)
- [⚡ Quick Start](#quick-start)
- [📚 Command Reference](#command-reference)
  - [🤖 auto - Auto Mode](#auto---auto-mode)
  - [🖼️ image - Single Image Processing](#image---single-image-processing)
  - [🗂️ images - Image Directory Processing](#images---image-directory-processing)
  - [🎬 video - Video Processing](#video---video-processing)
  - [📐 colmap - COLMAP Dataset Processing](#colmap---colmap-dataset-processing)
  - [🔧 backend - Backend Service](#backend---backend-service)
  - [🎨 gradio - Gradio Application](#gradio---gradio-application)
  - [🖼️ gallery - Gallery Server](#gallery---gallery-server)
- [⚙️ Parameter Details](#parameter-details)
- [💡 Usage Examples](#usage-examples)

## 📖 Overview

The Depth Anything 3 CLI provides a comprehensive command-line toolkit supporting image depth estimation, video processing, COLMAP dataset handling, and web applications.

The backend service enables cache model to GPU so that we do not need to reload model for each command.

## ⚡ Quick Start

The CLI can run fully offline or connect to the backend for cached weights and task scheduling:

```bash
# 🔧 Start backend service (optional, keeps model resident in GPU memory)
da3 backend --model-dir depth-anything/DA3NESTED-GIANT-LARGE

# 🚀 Use auto mode to process input
da3 auto path/to/input --export-dir ./workspace/scene001

# ♻️ Reuse backend for next job
da3 auto path/to/video.mp4 \
    --export-dir ./workspace/scene002 \
    --use-backend \
    --backend-url http://localhost:8008
```

Each export directory contains `scene.glb`, `scene.jpg`, and optional extras such as `depth_vis/` or `gs_video/` depending on the requested format.

## 📚 Command Reference

### 🤖 auto - Auto Mode

Automatically detect input type and dispatch to the appropriate handler.

**Usage:**

```bash
da3 auto INPUT_PATH [OPTIONS]
```

**Input Type Detection:**
- 🖼️ Single image file (.jpg, .png, .jpeg, .webp, .bmp, .tiff, .tif)
- 📁 Image directory
- 🎬 Video file (.mp4, .avi, .mov, .mkv, .flv, .wmv, .webm, .m4v)
- 📐 COLMAP directory (containing `images/` and `sparse/` subdirectories)

**Parameters:**

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `INPUT_PATH` | str | Required | Input path (image, directory, video, or COLMAP) |
| `--model-dir` | str | Default model | Model directory path |
| `--export-dir` | str | `debug` | Export directory |
| `--export-format` | str | `glb` | Export format (supports `mini_npz`, `glb`, `feat_vis`, etc., can be combined with hyphens) |
| `--device` | str | `cuda` | Device to use |
| `--use-backend` | bool | `False` | Use backend service for inference |
| `--backend-url` | str | `http://localhost:8008` | Backend service URL |
| `--process-res` | int | `504` | Processing resolution |
| `--process-res-method` | str | `upper_bound_resize` | Processing resolution method |
| `--export-feat` | str | `""` | Export features from specified layers, comma-separated (e.g., `"0,1,2"`) |
| `--auto-cleanup` | bool | `False` | Automatically clean export directory without confirmation |
| `--fps` | float | `1.0` | [Video] Frame sampling FPS |
| `--sparse-subdir` | str | `""` | [COLMAP] Sparse reconstruction subdirectory (e.g., `"0"` for `sparse/0/`) |
| `--align-to-input-ext-scale` | bool | `True` | [COLMAP] Align prediction to input extrinsics scale |
| `--use-ray-pose` | bool | `False` | Use ray-based pose estimation instead of camera decoder |
| `--ref-view-strategy` | str | `saddle_balanced` | Reference view selection strategy: `first`, `middle`, `saddle_balanced`, `saddle_sim_range`. See [docs](funcs/ref_view_strategy.md) |
| `--conf-thresh-percentile` | float | `40.0` | [GLB] Lower percentile for adaptive confidence threshold |
| `--num-max-points` | int | `1000000` | [GLB] Maximum number of points in the point cloud |
| `--show-cameras` | bool | `True` | [GLB] Show camera wireframes in the exported scene |
| `--feat-vis-fps` | int | `15` | [FEAT_VIS] Frame rate for output video |

**Examples:**

```bash
# 🖼️ Auto-process an image
da3 auto path/to/image.jpg --export-dir ./output

# 🎬 Auto-process a video
da3 auto path/to/video.mp4 --fps 2.0 --export-dir ./output

# 🔧 Use backend service
da3 auto path/to/input \
    --export-format mini_npz-glb \
    --use-backend \
    --backend-url http://localhost:8008 \
    --export-dir ./output
```

---

### 🖼️ image - Single Image Processing

Process a single image for camera pose and depth estimation.

**Usage:**

```bash
da3 image IMAGE_PATH [OPTIONS]
```

**Parameters:**

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `IMAGE_PATH` | str | Required | Input image file path |
| `--model-dir` | str | Default model | Model directory path |
| `--export-dir` | str | `debug` | Export directory |
| `--export-format` | str | `glb` | Export format |
| `--device` | str | `cuda` | Device to use |
| `--use-backend` | bool | `False` | Use backend service for inference |
| `--backend-url` | str | `http://localhost:8008` | Backend service URL |
| `--process-res` | int | `504` | Processing resolution |
| `--process-res-method` | str | `upper_bound_resize` | Processing resolution method |
| `--export-feat` | str | `""` | Export feature layer indices (comma-separated) |
| `--auto-cleanup` | bool | `False` | Automatically clean export directory |
| `--use-ray-pose` | bool | `False` | Use ray-based pose estimation instead of camera decoder |
| `--ref-view-strategy` | str | `saddle_balanced` | Reference view selection strategy. See [docs](funcs/ref_view_strategy.md) |
| `--conf-thresh-percentile` | float | `40.0` | [GLB] Confidence threshold percentile |
| `--num-max-points` | int | `1000000` | [GLB] Maximum number of points |
| `--show-cameras` | bool | `True` | [GLB] Show cameras |
| `--feat-vis-fps` | int | `15` | [FEAT_VIS] Video frame rate |

**Examples:**

```bash
# ✨ Basic usage
da3 image path/to/image.png --export-dir ./output

# ⚡ With backend acceleration
da3 image path/to/image.png \
    --use-backend \
    --backend-url http://localhost:8008 \
    --export-dir ./output

# 🔍 Export feature visualization
da3 image image.jpg \
    --export-format feat_vis \
    --export-feat "9,19,29,39" \
    --export-dir ./results
```

---

### 🗂️ images - Image Directory Processing

Process a directory of images for batch depth estimation.

**Usage:**

```bash
da3 images IMAGES_DIR [OPTIONS]
```

**Parameters:**

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `IMAGES_DIR` | str | Required | Directory path containing images |
| `--image-extensions` | str | `png,jpg,jpeg` | Image file extensions to process (comma-separated) |
| `--model-dir` | str | Default model | Model directory path |
| `--export-dir` | str | `debug` | Export directory |
| `--export-format` | str | `glb` | Export format |
| `--device` | str | `cuda` | Device to use |
| `--use-backend` | bool | `False` | Use backend service for inference |
| `--backend-url` | str | `http://localhost:8008` | Backend service URL |
| `--process-res` | int | `504` | Processing resolution |
| `--process-res-method` | str | `upper_bound_resize` | Processing resolution method |
| `--export-feat` | str | `""` | Export feature layer indices |
| `--auto-cleanup` | bool | `False` | Automatically clean export directory |
| `--use-ray-pose` | bool | `False` | Use ray-based pose estimation instead of camera decoder |
| `--ref-view-strategy` | str | `saddle_balanced` | Reference view selection strategy. See [docs](funcs/ref_view_strategy.md) |
| `--conf-thresh-percentile` | float | `40.0` | [GLB] Confidence threshold percentile |
| `--num-max-points` | int | `1000000` | [GLB] Maximum number of points |
| `--show-cameras` | bool | `True` | [GLB] Show cameras |
| `--feat-vis-fps` | int | `15` | [FEAT_VIS] Video frame rate |

**Examples:**

```bash
# 📁 Process directory (defaults to png/jpg/jpeg)
da3 images ./image_folder --export-dir ./output

# 🎯 Custom extensions
da3 images ./dataset --image-extensions "png,jpg,webp" --export-dir ./output

# 🔧 Use backend service
da3 images ./dataset \
    --use-backend \
    --backend-url http://localhost:8008 \
    --export-dir ./output
```

---

### 🎬 video - Video Processing

Process video by extracting frames for depth estimation.

**Usage:**

```bash
da3 video VIDEO_PATH [OPTIONS]
```

**Parameters:**

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `VIDEO_PATH` | str | Required | Input video file path |
| `--fps` | float | `1.0` | Frame extraction sampling FPS |
| `--model-dir` | str | Default model | Model directory path |
| `--export-dir` | str | `debug` | Export directory |
| `--export-format` | str | `glb` | Export format |
| `--device` | str | `cuda` | Device to use |
| `--use-backend` | bool | `False` | Use backend service for inference |
| `--backend-url` | str | `http://localhost:8008` | Backend service URL |
| `--process-res` | int | `504` | Processing resolution |
| `--process-res-method` | str | `upper_bound_resize` | Processing resolution method |
| `--export-feat` | str | `""` | Export feature layer indices |
| `--auto-cleanup` | bool | `False` | Automatically clean export directory |
| `--use-ray-pose` | bool | `False` | Use ray-based pose estimation instead of camera decoder |
| `--ref-view-strategy` | str | `saddle_balanced` | Reference view selection strategy. See [docs](funcs/ref_view_strategy.md) |
| `--conf-thresh-percentile` | float | `40.0` | [GLB] Confidence threshold percentile |
| `--num-max-points` | int | `1000000` | [GLB] Maximum number of points |
| `--show-cameras` | bool | `True` | [GLB] Show cameras |
| `--feat-vis-fps` | int | `15` | [FEAT_VIS] Video frame rate |

**Examples:**

```bash
# ✨ Basic video processing
da3 video path/to/video.mp4 --export-dir ./output

# ⚙️ Control frame sampling and resolution
da3 video path/to/video.mp4 \
    --fps 2.0 \
    --process-res 1024 \
    --export-dir ./output

# 🔧 Use backend service
da3 video path/to/video.mp4 \
    --use-backend \
    --backend-url http://localhost:8008 \
    --export-dir ./output
```

---

### 📐 colmap - COLMAP Dataset Processing

Run pose-conditioned depth estimation on COLMAP data.

**Usage:**

```bash
da3 colmap COLMAP_DIR [OPTIONS]
```

**Parameters:**

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `COLMAP_DIR` | str | Required | COLMAP directory containing `images/` and `sparse/` subdirectories |
| `--sparse-subdir` | str | `""` | Sparse reconstruction subdirectory (e.g., `"0"` for `sparse/0/`) |
| `--align-to-input-ext-scale` | bool | `True` | Align prediction to input extrinsics scale |
| `--model-dir` | str | Default model | Model directory path |
| `--export-dir` | str | `debug` | Export directory |
| `--export-format` | str | `glb` | Export format |
| `--device` | str | `cuda` | Device to use |
| `--use-backend` | bool | `False` | Use backend service for inference |
| `--backend-url` | str | `http://localhost:8008` | Backend service URL |
| `--process-res` | int | `504` | Processing resolution |
| `--process-res-method` | str | `upper_bound_resize` | Processing resolution method |
| `--export-feat` | str | `""` | Export feature layer indices |
| `--auto-cleanup` | bool | `False` | Automatically clean export directory |
| `--use-ray-pose` | bool | `False` | Use ray-based pose estimation instead of camera decoder |
| `--ref-view-strategy` | str | `saddle_balanced` | Reference view selection strategy. See [docs](funcs/ref_view_strategy.md) |
| `--conf-thresh-percentile` | float | `40.0` | [GLB] Confidence threshold percentile |
| `--num-max-points` | int | `1000000` | [GLB] Maximum number of points |
| `--show-cameras` | bool | `True` | [GLB] Show cameras |
| `--feat-vis-fps` | int | `15` | [FEAT_VIS] Video frame rate |

**Examples:**

```bash
# 📐 Process COLMAP dataset
da3 colmap ./colmap_dataset --export-dir ./output

# 🎯 Use specific sparse subdirectory and align scale
da3 colmap ./colmap_dataset \
    --sparse-subdir 0 \
    --align-to-input-ext-scale \
    --export-dir ./output

# 🔧 Use backend service
da3 colmap ./colmap_dataset \
    --use-backend \
    --backend-url http://localhost:8008 \
    --export-dir ./output
```

---

### 🔧 backend - Backend Service

Start model backend service with integrated gallery.

**Usage:**

```bash
da3 backend [OPTIONS]
```

**Parameters:**

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `--model-dir` | str | Default model | Model directory path |
| `--device` | str | `cuda` | Device to use |
| `--host` | str | `127.0.0.1` | Host address to bind to |
| `--port` | int | `8008` | Port number to bind to |
| `--gallery-dir` | str | Default gallery dir | Gallery directory path (optional) |

**Features:**
- 🎯 Keeps model resident in GPU memory
- 🔌 Provides REST inference API
- 📊 Integrated dashboard and status monitoring
- 🖼️ Optional gallery browser (if `--gallery-dir` is provided)

**Available Endpoints:**
- 🏠 `/` - Home page
- 📊 `/dashboard` - Dashboard
- ✅ `/status` - API status
- 🖼️ `/gallery/` - Gallery browser (if enabled)

**Examples:**

```bash
# 🚀 Basic backend service
da3 backend --model-dir depth-anything/DA3NESTED-GIANT-LARGE

# 🖼️ Backend with gallery
da3 backend \
    --model-dir depth-anything/DA3NESTED-GIANT-LARGE \
    --device cuda \
    --host 0.0.0.0 \
    --port 8008 \
    --gallery-dir ./workspace

# 💻 Use CPU
da3 backend --model-dir depth-anything/DA3NESTED-GIANT-LARGE --device cpu
```

---

### 🎨 gradio - Gradio Application

Launch Depth Anything 3 Gradio interactive web application.

**Usage:**

```bash
da3 gradio [OPTIONS]
```

**Parameters:**

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `--model-dir` | str | Required | Model directory path |
| `--workspace-dir` | str | Required | Workspace directory path |
| `--gallery-dir` | str | Required | Gallery directory path |
| `--host` | str | `127.0.0.1` | Host address to bind to |
| `--port` | int | `7860` | Port number to bind to |
| `--share` | bool | `False` | Create a public link |
| `--debug` | bool | `False` | Enable debug mode |
| `--cache-examples` | bool | `False` | Pre-cache all example scenes at startup |
| `--cache-gs-tag` | str | `""` | Tag to match scene names for high-res+3DGS caching |

**Examples:**

```bash
# 🎨 Basic Gradio application
da3 gradio \
    --model-dir depth-anything/DA3NESTED-GIANT-LARGE \
    --workspace-dir ./workspace \
    --gallery-dir ./gallery

# 🌐 Enable sharing and debug
da3 gradio \
    --model-dir depth-anything/DA3NESTED-GIANT-LARGE \
    --workspace-dir ./workspace \
    --gallery-dir ./gallery \
    --share \
    --debug

# ⚡ Pre-cache examples
da3 gradio \
    --model-dir depth-anything/DA3NESTED-GIANT-LARGE \
    --workspace-dir ./workspace \
    --gallery-dir ./gallery \
    --cache-examples \
    --cache-gs-tag "dl3dv"
```

---

### 🖼️ gallery - Gallery Server

Launch standalone Depth Anything 3 Gallery server.

**Usage:**

```bash
da3 gallery [OPTIONS]
```

**Parameters:**

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `--gallery-dir` | str | Default gallery dir | Gallery root directory |
| `--host` | str | `127.0.0.1` | Host address to bind to |
| `--port` | int | `8007` | Port number to bind to |
| `--open-browser` | bool | `False` | Open browser after launch |

**Note:**
The gallery expects each scene folder to contain at least `scene.glb` and `scene.jpg`, with optional subfolders such as `depth_vis/` or `gs_video/`.

**Examples:**

```bash
# 🖼️ Basic gallery server
da3 gallery --gallery-dir ./workspace

# 🌐 Custom host and port
da3 gallery \
    --gallery-dir ./workspace \
    --host 0.0.0.0 \
    --port 8007

# 🚀 Auto-open browser
da3 gallery --gallery-dir ./workspace --open-browser
```

---

## ⚙️ Parameter Details

### 🔧 Common Parameters

- **`--export-dir`**: Output directory, defaults to `debug`
- **`--export-format`**: Export format, supports combining multiple formats with hyphens:
  - 📦 `mini_npz`: Compressed NumPy format
  - 🎨 `glb`: glTF binary format (3D scene)
  - 🔍 `feat_vis`: Feature visualization
  - Example: `mini_npz-glb` exports both formats

- **`--process-res`** / **`--process-res-method`**: Control preprocessing resolution strategy
  - `process-res`: Target resolution (default 504)
  - `process-res-method`: Resize method (default `upper_bound_resize`)

- **`--auto-cleanup`**: Remove existing export directory without confirmation

- **`--use-backend`** / **`--backend-url`**: Reuse running backend service
  - ⚡ Reduces model loading time
  - 🌐 Supports distributed processing

- **`--export-feat`**: Layer indices for exporting intermediate features (comma-separated)
  - Example: `"9,19,29,39"`

### 🎨 GLB Export Parameters

- **`--conf-thresh-percentile`**: Lower percentile for adaptive confidence threshold (default 40.0)
  - Used to filter low-confidence points

- **`--num-max-points`**: Maximum number of points in point cloud (default 1,000,000)
  - Controls output file size and performance

- **`--show-cameras`**: Show camera wireframes in exported scene (default True)

### 🔍 Feature Visualization Parameters

- **`--feat-vis-fps`**: Frame rate for feature visualization output video (default 15)

### 🎬 Video-Specific Parameters

- **`--fps`**: Video frame extraction sampling rate (default 1.0 FPS)
  - Higher values extract more frames

### 📐 COLMAP-Specific Parameters

- **`--sparse-subdir`**: Sparse reconstruction subdirectory
  - Empty string uses `sparse/` directory
  - `"0"` uses `sparse/0/` directory

- **`--align-to-input-ext-scale`**: Align prediction to input extrinsics scale (default True)
  - Ensures depth estimation is consistent with COLMAP scale

---

## 💡 Usage Examples

### 1️⃣ Basic Workflow

```bash
# 🔧 Start backend service
da3 backend --model-dir depth-anything/DA3NESTED-GIANT-LARGE --host 0.0.0.0 --port 8008

# 🖼️ Process single image
da3 image image.jpg --export-dir ./output1 --use-backend

# 🎬 Process video
da3 video video.mp4 --fps 2.0 --export-dir ./output2 --use-backend

# 📐 Process COLMAP dataset
da3 colmap ./colmap_data --export-dir ./output3 --use-backend
```

### 2️⃣ Using Auto Mode

```bash
# 🤖 Auto-detect and process
da3 auto ./unknown_input --export-dir ./output

# ⚡ With backend acceleration
da3 auto ./unknown_input \
    --use-backend \
    --backend-url http://localhost:8008 \
    --export-dir ./output
```

### 3️⃣ Multi-Format Export

```bash
# 📦 Export both NPZ and GLB formats
da3 auto assets/examples/SOH \
    --export-format mini_npz-glb \
    --export-dir ./workspace/soh

# 🔍 Export feature visualization
da3 image image.jpg \
    --export-format feat_vis \
    --export-feat "9,19,29,39" \
    --export-dir ./results
```

### 4️⃣ Advanced Configuration

```bash
# ⚙️ Custom resolution and point cloud density
da3 image image.jpg \
    --process-res 1024 \
    --num-max-points 2000000 \
    --conf-thresh-percentile 30.0 \
    --export-dir ./output

# 📐 COLMAP advanced options
da3 colmap ./colmap_data \
    --sparse-subdir 0 \
    --align-to-input-ext-scale \
    --process-res 756 \
    --export-dir ./output
```

### 5️⃣ Batch Processing Workflow

```bash
# 🔧 Start backend
da3 backend \
    --model-dir depth-anything/DA3NESTED-GIANT-LARGE \
    --device cuda \
    --host 0.0.0.0 \
    --port 8008 \
    --gallery-dir ./workspace

# 🔄 Batch process multiple scenes
for scene in scene1 scene2 scene3; do
    da3 auto ./data/$scene \
        --export-dir ./workspace/$scene \
        --use-backend \
        --auto-cleanup
done

# 🖼️ Launch gallery to view results
da3 gallery --gallery-dir ./workspace --open-browser
```

### 6️⃣ Web Applications

```bash
# 🎨 Launch Gradio application
da3 gradio \
    --model-dir depth-anything/DA3NESTED-GIANT-LARGE \
    --workspace-dir workspace/gradio \
    --gallery-dir ./gallery \
    --host 0.0.0.0 \
    --port 7860 \
    --share
```

### 7️⃣ Transformer Feature Visualization

```bash
# 🔍 Export Transformer features
# 📦 Combined with numerical output
da3 auto video.mp4 \
    --export-format glb-feat_vis \
    --export-feat "11,21,31" \
    --export-dir ./debug \
    --use-backend
```

---

## 📝 Notes

1. **🔧 Backend Service**: Recommended for processing multiple tasks to improve efficiency
2. **💾 GPU Memory**: Be mindful of GPU memory usage when processing high-resolution inputs
3. **📁 Export Directory**: Use `--auto-cleanup` to avoid manual confirmation for deletion
4. **🔀 Format Combination**: Multiple export formats can be combined with hyphens (e.g., `mini_npz-glb-feat_vis`)
5. **📐 COLMAP Data**: Ensure COLMAP directory structure is correct (contains `images/` and `sparse/` subdirectories)

---

## ❓ Getting Help

View detailed help for any command:

```bash
# 📖 View main help
da3 --help

# 🔍 View specific command help
da3 auto --help
da3 image --help
da3 backend --help
```



================================================
FILE: src/depth_anything_3/api.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
"""
Depth Anything 3 API module.

This module provides the main API for Depth Anything 3, including model loading,
inference, and export capabilities. It supports both single and nested model architectures.
"""

from __future__ import annotations

import time
from typing import Optional, Sequence
import numpy as np
import torch
import torch.nn as nn
from huggingface_hub import PyTorchModelHubMixin
from PIL import Image

from depth_anything_3.cfg import create_object, load_config
from depth_anything_3.registry import MODEL_REGISTRY
from depth_anything_3.specs import Prediction
from depth_anything_3.utils.export import export
from depth_anything_3.utils.geometry import affine_inverse
from depth_anything_3.utils.io.input_processor import InputProcessor
from depth_anything_3.utils.io.output_processor import OutputProcessor
from depth_anything_3.utils.logger import logger
from depth_anything_3.utils.pose_align import align_poses_umeyama

torch.backends.cudnn.benchmark = False
# logger.info("CUDNN Benchmark Disabled")

SAFETENSORS_NAME = "model.safetensors"
CONFIG_NAME = "config.json"


class DepthAnything3(nn.Module, PyTorchModelHubMixin):
    """
    Depth Anything 3 main API class.

    This class provides a high-level interface for depth estimation using Depth Anything 3.
    It supports both single and nested model architectures with metric scaling capabilities.

    Features:
    - Hugging Face Hub integration via PyTorchModelHubMixin
    - Support for multiple model presets (vitb, vitg, nested variants)
    - Automatic mixed precision inference
    - Export capabilities for various formats (GLB, PLY, NPZ, etc.)
    - Camera pose estimation and metric depth scaling

    Usage:
        # Load from Hugging Face Hub
        model = DepthAnything3.from_pretrained("huggingface/model-name")

        # Or create with specific preset
        model = DepthAnything3(preset="vitg")

        # Run inference
        prediction = model.inference(images, export_dir="output", export_format="glb")
    """

    _commit_hash: str | None = None  # Set by mixin when loading from Hub

    def __init__(self, model_name: str = "da3-large", **kwargs):
        """
        Initialize DepthAnything3 with specified preset.

        Args:
        model_name: The name of the model preset to use.
                    Examples: 'da3-giant', 'da3-large', 'da3metric-large', 'da3nested-giant-large'.
        **kwargs: Additional keyword arguments (currently unused).
        """
        super().__init__()
        self.model_name = model_name

        # Build the underlying network
        self.config = load_config(MODEL_REGISTRY[self.model_name])
        self.model = create_object(self.config)
        self.model.eval()

        # Initialize processors
        self.input_processor = InputProcessor()
        self.output_processor = OutputProcessor()

        # Device management (set by user)
        self.device = None

    @torch.inference_mode()
    def forward(
        self,
        image: torch.Tensor,
        extrinsics: torch.Tensor | None = None,
        intrinsics: torch.Tensor | None = None,
        export_feat_layers: list[int] | None = None,
        infer_gs: bool = False,
        use_ray_pose: bool = False,
        ref_view_strategy: str = "saddle_balanced",
    ) -> dict[str, torch.Tensor]:
        """
        Forward pass through the model.

        Args:
            image: Input batch with shape ``(B, N, 3, H, W)`` on the model device.
            extrinsics: Optional camera extrinsics with shape ``(B, N, 4, 4)``.
            intrinsics: Optional camera intrinsics with shape ``(B, N, 3, 3)``.
            export_feat_layers: Layer indices to return intermediate features for.
            infer_gs: Enable Gaussian Splatting branch.
            use_ray_pose: Use ray-based pose estimation instead of camera decoder.
            ref_view_strategy: Strategy for selecting reference view from multiple views.

        Returns:
            Dictionary containing model predictions
        """
        # Determine optimal autocast dtype
        autocast_dtype = torch.bfloat16 if torch.cuda.is_bf16_supported() else torch.float16
        with torch.no_grad():
            with torch.autocast(device_type=image.device.type, dtype=autocast_dtype):
                return self.model(
                    image, extrinsics, intrinsics, export_feat_layers, infer_gs, use_ray_pose, ref_view_strategy
                )

    def inference(
        self,
        image: list[np.ndarray | Image.Image | str],
        extrinsics: np.ndarray | None = None,
        intrinsics: np.ndarray | None = None,
        align_to_input_ext_scale: bool = True,
        infer_gs: bool = False,
        use_ray_pose: bool = False,
        ref_view_strategy: str = "saddle_balanced",
        render_exts: np.ndarray | None = None,
        render_ixts: np.ndarray | None = None,
        render_hw: tuple[int, int] | None = None,
        process_res: int = 504,
        process_res_method: str = "upper_bound_resize",
        export_dir: str | None = None,
        export_format: str = "mini_npz",
        export_feat_layers: Sequence[int] | None = None,
        # GLB export parameters
        conf_thresh_percentile: float = 40.0,
        num_max_points: int = 1_000_000,
        show_cameras: bool = True,
        # Feat_vis export parameters
        feat_vis_fps: int = 15,
        # Other export parameters, e.g., gs_ply, gs_video
        export_kwargs: Optional[dict] = {},
    ) -> Prediction:
        """
        Run inference on input images.

        Args:
            image: List of input images (numpy arrays, PIL Images, or file paths)
            extrinsics: Camera extrinsics (N, 4, 4)
            intrinsics: Camera intrinsics (N, 3, 3)
            align_to_input_ext_scale: whether to align the input pose scale to the prediction
            infer_gs: Enable the 3D Gaussian branch (needed for `gs_ply`/`gs_video` exports)
            use_ray_pose: Use ray-based pose estimation instead of camera decoder (default: False)
            ref_view_strategy: Strategy for selecting reference view from multiple views.
                Options: "first", "middle", "saddle_balanced", "saddle_sim_range".
                Default: "saddle_balanced". For single view input (S ≤ 2), no reordering is performed.
            render_exts: Optional render extrinsics for Gaussian video export
            render_ixts: Optional render intrinsics for Gaussian video export
            render_hw: Optional render resolution for Gaussian video export
            process_res: Processing resolution
            process_res_method: Resize method for processing
            export_dir: Directory to export results
            export_format: Export format (mini_npz, npz, glb, ply, gs, gs_video)
            export_feat_layers: Layer indices to export intermediate features from
            conf_thresh_percentile: [GLB] Lower percentile for adaptive confidence threshold (default: 40.0) # noqa: E501
            num_max_points: [GLB] Maximum number of points in the point cloud (default: 1,000,000)
            show_cameras: [GLB] Show camera wireframes in the exported scene (default: True)
            feat_vis_fps: [FEAT_VIS] Frame rate for output video (default: 15)
            export_kwargs: additional arguments to export functions.

        Returns:
            Prediction object containing depth maps and camera parameters
        """
        if "gs" in export_format:
            assert infer_gs, "must set `infer_gs=True` to perform gs-related export."

        if "colmap" in export_format:
            assert isinstance(image[0], str), "`image` must be image paths for COLMAP export."

        # Preprocess images
        imgs_cpu, extrinsics, intrinsics = self._preprocess_inputs(
            image, extrinsics, intrinsics, process_res, process_res_method
        )

        # Prepare tensors for model
        imgs, ex_t, in_t = self._prepare_model_inputs(imgs_cpu, extrinsics, intrinsics)

        # Normalize extrinsics
        ex_t_norm = self._normalize_extrinsics(ex_t.clone() if ex_t is not None else None)

        # Run model forward pass
        export_feat_layers = list(export_feat_layers) if export_feat_layers is not None else []

        raw_output = self._run_model_forward(
            imgs, ex_t_norm, in_t, export_feat_layers, infer_gs, use_ray_pose, ref_view_strategy
        )

        # Convert raw output to prediction
        prediction = self._convert_to_prediction(raw_output)

        # Align prediction to extrinsincs
        prediction = self._align_to_input_extrinsics_intrinsics(
            extrinsics, intrinsics, prediction, align_to_input_ext_scale
        )

        # Add processed images for visualization
        prediction = self._add_processed_images(prediction, imgs_cpu)

        # Export if requested
        if export_dir is not None:

            if "gs" in export_format:
                if infer_gs and "gs_video" not in export_format:
                    export_format = f"{export_format}-gs_video"
                if "gs_video" in export_format:
                    if "gs_video" not in export_kwargs:
                        export_kwargs["gs_video"] = {}
                    export_kwargs["gs_video"].update(
                        {
                            "extrinsics": render_exts,
                            "intrinsics": render_ixts,
                            "out_image_hw": render_hw,
                        }
                    )
            # Add GLB export parameters
            if "glb" in export_format:
                if "glb" not in export_kwargs:
                    export_kwargs["glb"] = {}
                export_kwargs["glb"].update(
                    {
                        "conf_thresh_percentile": conf_thresh_percentile,
                        "num_max_points": num_max_points,
                        "show_cameras": show_cameras,
                    }
                )
            # Add Feat_vis export parameters
            if "feat_vis" in export_format:
                if "feat_vis" not in export_kwargs:
                    export_kwargs["feat_vis"] = {}
                export_kwargs["feat_vis"].update(
                    {
                        "fps": feat_vis_fps,
                    }
                )
            # Add COLMAP export parameters
            if "colmap" in export_format:
                if "colmap" not in export_kwargs:
                    export_kwargs["colmap"] = {}
                export_kwargs["colmap"].update(
                    {
                        "image_paths": image,
                        "conf_thresh_percentile": conf_thresh_percentile,
                        "process_res_method": process_res_method,
                    }
                )
            self._export_results(prediction, export_format, export_dir, **export_kwargs)

        return prediction

    def _preprocess_inputs(
        self,
        image: list[np.ndarray | Image.Image | str],
        extrinsics: np.ndarray | None = None,
        intrinsics: np.ndarray | None = None,
        process_res: int = 504,
        process_res_method: str = "upper_bound_resize",
    ) -> tuple[torch.Tensor, torch.Tensor | None, torch.Tensor | None]:
        """Preprocess input images using input processor."""
        start_time = time.time()
        imgs_cpu, extrinsics, intrinsics = self.input_processor(
            image,
            extrinsics.copy() if extrinsics is not None else None,
            intrinsics.copy() if intrinsics is not None else None,
            process_res,
            process_res_method,
        )
        end_time = time.time()
        logger.info(
            "Processed Images Done taking",
            end_time - start_time,
            "seconds. Shape: ",
            imgs_cpu.shape,
        )
        return imgs_cpu, extrinsics, intrinsics

    def _prepare_model_inputs(
        self,
        imgs_cpu: torch.Tensor,
        extrinsics: torch.Tensor | None,
        intrinsics: torch.Tensor | None,
    ) -> tuple[torch.Tensor, torch.Tensor | None, torch.Tensor | None]:
        """Prepare tensors for model input."""
        device = self._get_model_device()

        # Move images to model device
        imgs = imgs_cpu.to(device, non_blocking=True)[None].float()

        # Convert camera parameters to tensors
        ex_t = (
            extrinsics.to(device, non_blocking=True)[None].float()
            if extrinsics is not None
            else None
        )
        in_t = (
            intrinsics.to(device, non_blocking=True)[None].float()
            if intrinsics is not None
            else None
        )

        return imgs, ex_t, in_t

    def _normalize_extrinsics(self, ex_t: torch.Tensor | None) -> torch.Tensor | None:
        """Normalize extrinsics"""
        if ex_t is None:
            return None
        transform = affine_inverse(ex_t[:, :1])
        ex_t_norm = ex_t @ transform
        c2ws = affine_inverse(ex_t_norm)
        translations = c2ws[..., :3, 3]
        dists = translations.norm(dim=-1)
        median_dist = torch.median(dists)
        median_dist = torch.clamp(median_dist, min=1e-1)
        ex_t_norm[..., :3, 3] = ex_t_norm[..., :3, 3] / median_dist
        return ex_t_norm

    def _align_to_input_extrinsics_intrinsics(
        self,
        extrinsics: torch.Tensor | None,
        intrinsics: torch.Tensor | None,
        prediction: Prediction,
        align_to_input_ext_scale: bool = True,
        ransac_view_thresh: int = 10,
    ) -> Prediction:
        """Align depth map to input extrinsics"""
        if extrinsics is None:
            return prediction
        prediction.intrinsics = intrinsics.numpy()
        _, _, scale, aligned_extrinsics = align_poses_umeyama(
            prediction.extrinsics,
            extrinsics.numpy(),
            ransac=len(extrinsics) >= ransac_view_thresh,
            return_aligned=True,
            random_state=42,
        )
        if align_to_input_ext_scale:
            prediction.extrinsics = extrinsics[..., :3, :].numpy()
            prediction.depth /= scale
        else:
            prediction.extrinsics = aligned_extrinsics
        return prediction

    def _run_model_forward(
        self,
        imgs: torch.Tensor,
        ex_t: torch.Tensor | None,
        in_t: torch.Tensor | None,
        export_feat_layers: Sequence[int] | None = None,
        infer_gs: bool = False,
        use_ray_pose: bool = False,
        ref_view_strategy: str = "saddle_balanced",
    ) -> dict[str, torch.Tensor]:
        """Run model forward pass."""
        device = imgs.device
        need_sync = device.type == "cuda"
        if need_sync:
            torch.cuda.synchronize(device)
        start_time = time.time()
        feat_layers = list(export_feat_layers) if export_feat_layers is not None else None
        output = self.forward(imgs, ex_t, in_t, feat_layers, infer_gs, use_ray_pose, ref_view_strategy)
        if need_sync:
            torch.cuda.synchronize(device)
        end_time = time.time()
        logger.info(f"Model Forward Pass Done. Time: {end_time - start_time} seconds")
        return output

    def _convert_to_prediction(self, raw_output: dict[str, torch.Tensor]) -> Prediction:
        """Convert raw model output to Prediction object."""
        start_time = time.time()
        output = self.output_processor(raw_output)
        end_time = time.time()
        logger.info(f"Conversion to Prediction Done. Time: {end_time - start_time} seconds")
        return output

    def _add_processed_images(self, prediction: Prediction, imgs_cpu: torch.Tensor) -> Prediction:
        """Add processed images to prediction for visualization."""
        # Convert from (N, 3, H, W) to (N, H, W, 3) and denormalize
        processed_imgs = imgs_cpu.permute(0, 2, 3, 1).cpu().numpy()  # (N, H, W, 3)

        # Denormalize from ImageNet normalization
        mean = np.array([0.485, 0.456, 0.406])
        std = np.array([0.229, 0.224, 0.225])
        processed_imgs = processed_imgs * std + mean
        processed_imgs = np.clip(processed_imgs, 0, 1)
        processed_imgs = (processed_imgs * 255).astype(np.uint8)

        prediction.processed_images = processed_imgs
        return prediction

    def _export_results(
        self, prediction: Prediction, export_format: str, export_dir: str, **kwargs
    ) -> None:
        """Export results to specified format and directory."""
        start_time = time.time()
        export(prediction, export_format, export_dir, **kwargs)
        end_time = time.time()
        logger.info(f"Export Results Done. Time: {end_time - start_time} seconds")

    def _get_model_device(self) -> torch.device:
        """
        Get the device where the model is located.

        Returns:
            Device where the model parameters are located

        Raises:
            ValueError: If no tensors are found in the model
        """
        if self.device is not None:
            return self.device

        # Find device from parameters
        for param in self.parameters():
            self.device = param.device
            return param.device

        # Find device from buffers
        for buffer in self.buffers():
            self.device = buffer.device
            return buffer.device

        raise ValueError("No tensor found in model")



================================================
FILE: src/depth_anything_3/cfg.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

"""
Configuration utility functions
"""

import importlib
from pathlib import Path
from typing import Any, Callable, List, Union
from omegaconf import DictConfig, ListConfig, OmegaConf

try:
    OmegaConf.register_new_resolver("eval", eval)
except Exception as e:
    # if eval is not available, we can just pass
    print(f"Error registering eval resolver: {e}")


def load_config(path: str, argv: List[str] = None) -> Union[DictConfig, ListConfig]:
    """
    Load a configuration. Will resolve inheritance.
    Supports both file paths and module paths (e.g., depth_anything_3.configs.giant).
    """
    # Check if path is a module path (contains dots but no slashes and doesn't end with .yaml)
    if "." in path and "/" not in path and not path.endswith(".yaml"):
        # It's a module path, load from package resources
        path_parts = path.split(".")[1:]
        config_path = Path(__file__).resolve().parent
        for part in path_parts:
            config_path = config_path.joinpath(part)
        config_path = config_path.with_suffix(".yaml")
        config = OmegaConf.load(str(config_path))
    else:
        # It's a file path (absolute, relative, or with .yaml extension)
        config = OmegaConf.load(path)

    if argv is not None:
        config_argv = OmegaConf.from_dotlist(argv)
        config = OmegaConf.merge(config, config_argv)
    config = resolve_recursive(config, resolve_inheritance)
    return config


def resolve_recursive(
    config: Any,
    resolver: Callable[[Union[DictConfig, ListConfig]], Union[DictConfig, ListConfig]],
) -> Any:
    config = resolver(config)
    if isinstance(config, DictConfig):
        for k in config.keys():
            v = config.get(k)
            if isinstance(v, (DictConfig, ListConfig)):
                config[k] = resolve_recursive(v, resolver)
    if isinstance(config, ListConfig):
        for i in range(len(config)):
            v = config.get(i)
            if isinstance(v, (DictConfig, ListConfig)):
                config[i] = resolve_recursive(v, resolver)
    return config


def resolve_inheritance(config: Union[DictConfig, ListConfig]) -> Any:
    """
    Recursively resolve inheritance if the config contains:
    __inherit__: path/to/parent.yaml or a ListConfig of such paths.
    """
    if isinstance(config, DictConfig):
        inherit = config.pop("__inherit__", None)

        if inherit:
            inherit_list = inherit if isinstance(inherit, ListConfig) else [inherit]

            parent_config = None
            for parent_path in inherit_list:
                assert isinstance(parent_path, str)
                parent_config = (
                    load_config(parent_path)
                    if parent_config is None
                    else OmegaConf.merge(parent_config, load_config(parent_path))
                )

            if len(config.keys()) > 0:
                config = OmegaConf.merge(parent_config, config)
            else:
                config = parent_config
    return config


def import_item(path: str, name: str) -> Any:
    """
    Import a python item. Example: import_item("path.to.file", "MyClass") -> MyClass
    """
    return getattr(importlib.import_module(path), name)


def create_object(config: DictConfig) -> Any:
    """
    Create an object from config.
    The config is expected to contains the following:
    __object__:
      path: path.to.module
      name: MyClass
      args: as_config | as_params (default to as_config)
    """
    config = DictConfig(config)
    item = import_item(
        path=config.__object__.path,
        name=config.__object__.name,
    )
    args = config.__object__.get("args", "as_config")
    if args == "as_config":
        return item(config)
    if args == "as_params":
        config = OmegaConf.to_object(config)
        config.pop("__object__")
        return item(**config)
    raise NotImplementedError(f"Unknown args type: {args}")


def create_dataset(path: str, *args, **kwargs) -> Any:
    """
    Create a dataset. Requires the file to contain a "create_dataset" function.
    """
    return import_item(path, "create_dataset")(*args, **kwargs)


def to_dict_recursive(config_obj):
    if isinstance(config_obj, DictConfig):
        return {k: to_dict_recursive(v) for k, v in config_obj.items()}
    elif isinstance(config_obj, ListConfig):
        return [to_dict_recursive(item) for item in config_obj]
    return config_obj



================================================
FILE: src/depth_anything_3/cli.py
================================================
# flake8: noqa: E402
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
"""
Refactored Depth Anything 3 CLI
Clean, modular command-line interface
"""

from __future__ import annotations

import os
import typer

from depth_anything_3.services import start_server
from depth_anything_3.services.gallery import gallery as gallery_main
from depth_anything_3.services.inference_service import run_inference
from depth_anything_3.services.input_handlers import (
    ColmapHandler,
    ImageHandler,
    ImagesHandler,
    InputHandler,
    VideoHandler,
    parse_export_feat,
)
from depth_anything_3.utils.constants import (
    DEFAULT_EXPORT_DIR,
    DEFAULT_GALLERY_DIR,
    DEFAULT_GRADIO_DIR,
    DEFAULT_MODEL,
)

os.environ["PYTORCH_CUDA_ALLOC_CONF"] = "expandable_segments:True"

app = typer.Typer(help="Depth Anything 3 - Video depth estimation CLI", add_completion=False)


# ============================================================================
# Input type detection utilities
# ============================================================================

# Supported file extensions
IMAGE_EXTENSIONS = {".png", ".jpg", ".jpeg", ".webp", ".bmp", ".tiff", ".tif"}
VIDEO_EXTENSIONS = {".mp4", ".avi", ".mov", ".mkv", ".flv", ".wmv", ".webm", ".m4v"}


def detect_input_type(input_path: str) -> str:
    """
    Detect input type from path.

    Returns:
        - "image": Single image file
        - "images": Directory containing images
        - "video": Video file
        - "colmap": COLMAP directory structure
        - "unknown": Cannot determine type
    """
    if not os.path.exists(input_path):
        return "unknown"

    # Check if it's a file
    if os.path.isfile(input_path):
        ext = os.path.splitext(input_path)[1].lower()
        if ext in IMAGE_EXTENSIONS:
            return "image"
        elif ext in VIDEO_EXTENSIONS:
            return "video"
        return "unknown"

    # Check if it's a directory
    if os.path.isdir(input_path):
        # Check for COLMAP structure
        images_dir = os.path.join(input_path, "images")
        sparse_dir = os.path.join(input_path, "sparse")

        if os.path.isdir(images_dir) and os.path.isdir(sparse_dir):
            return "colmap"

        # Check if directory contains image files
        for item in os.listdir(input_path):
            item_path = os.path.join(input_path, item)
            if os.path.isfile(item_path):
                ext = os.path.splitext(item)[1].lower()
                if ext in IMAGE_EXTENSIONS:
                    return "images"

        return "unknown"

    return "unknown"


# ============================================================================
# Common parameters and configuration
# ============================================================================

# ============================================================================
# Inference commands
# ============================================================================


@app.command()
def auto(
    input_path: str = typer.Argument(
        ..., help="Path to input (image, directory, video, or COLMAP)"
    ),
    model_dir: str = typer.Option(DEFAULT_MODEL, help="Model directory path"),
    export_dir: str = typer.Option(DEFAULT_EXPORT_DIR, help="Export directory"),
    export_format: str = typer.Option("glb", help="Export format"),
    device: str = typer.Option("cuda", help="Device to use"),
    use_backend: bool = typer.Option(False, help="Use backend service for inference"),
    backend_url: str = typer.Option(
        "http://localhost:8008", help="Backend URL (default: http://localhost:8008)"
    ),
    process_res: int = typer.Option(504, help="Processing resolution"),
    process_res_method: str = typer.Option(
        "upper_bound_resize", help="Processing resolution method"
    ),
    export_feat: str = typer.Option(
        "",
        help="[FEAT_VIS]Export features from specified layers using comma-separated indices (e.g., '0,1,2').",
    ),
    auto_cleanup: bool = typer.Option(
        False, help="Automatically clean export directory if it exists (no prompt)"
    ),
    # Video-specific options
    fps: float = typer.Option(1.0, help="[Video] Sampling FPS for frame extraction"),
    # COLMAP-specific options
    sparse_subdir: str = typer.Option(
        "", help="[COLMAP] Sparse reconstruction subdirectory (e.g., '0' for sparse/0/)"
    ),
    align_to_input_ext_scale: bool = typer.Option(
        True, help="[COLMAP] Align prediction to input extrinsics scale"
    ),
    # Pose estimation options
    use_ray_pose: bool = typer.Option(
        False, help="Use ray-based pose estimation instead of camera decoder"
    ),
    ref_view_strategy: str = typer.Option(
        "saddle_balanced",
        help="Reference view selection strategy: empty, first, middle, saddle_balanced, saddle_sim_range",
    ),
    # GLB export options
    conf_thresh_percentile: float = typer.Option(
        40.0, help="[GLB] Lower percentile for adaptive confidence threshold"
    ),
    num_max_points: int = typer.Option(
        1_000_000, help="[GLB] Maximum number of points in the point cloud"
    ),
    show_cameras: bool = typer.Option(
        True, help="[GLB] Show camera wireframes in the exported scene"
    ),
    # Feat_vis export options
    feat_vis_fps: int = typer.Option(15, help="[FEAT_VIS] Frame rate for output video"),
):
    """
    Automatically detect input type and run appropriate processing.

    Supports:
    - Single image file (.jpg, .png, etc.)
    - Directory of images
    - Video file (.mp4, .avi, etc.)
    - COLMAP directory (with 'images' and 'sparse' subdirectories)
    """
    # Detect input type
    input_type = detect_input_type(input_path)

    if input_type == "unknown":
        typer.echo(f"❌ Error: Cannot determine input type for: {input_path}", err=True)
        typer.echo("Supported inputs:", err=True)
        typer.echo("  - Single image file (.jpg, .png, etc.)", err=True)
        typer.echo("  - Directory containing images", err=True)
        typer.echo("  - Video file (.mp4, .avi, etc.)", err=True)
        typer.echo("  - COLMAP directory (with 'images/' and 'sparse/' subdirectories)", err=True)
        raise typer.Exit(1)

    # Display detected type
    typer.echo(f"🔍 Detected input type: {input_type.upper()}")
    typer.echo(f"📁 Input path: {input_path}")
    typer.echo()

    # Determine backend URL based on use_backend flag
    final_backend_url = backend_url if use_backend else None

    # Parse export_feat parameter
    export_feat_layers = parse_export_feat(export_feat)

    # Route to appropriate handler
    if input_type == "image":
        typer.echo("Processing single image...")
        # Process input
        image_files = ImageHandler.process(input_path)

        # Handle export directory
        export_dir = InputHandler.handle_export_dir(export_dir, auto_cleanup)

        # Run inference
        run_inference(
            image_paths=image_files,
            export_dir=export_dir,
            model_dir=model_dir,
            device=device,
            backend_url=final_backend_url,
            export_format=export_format,
            process_res=process_res,
            process_res_method=process_res_method,
            export_feat_layers=export_feat_layers,
            use_ray_pose=use_ray_pose,
            ref_view_strategy=ref_view_strategy,
            conf_thresh_percentile=conf_thresh_percentile,
            num_max_points=num_max_points,
            show_cameras=show_cameras,
            feat_vis_fps=feat_vis_fps,
        )

    elif input_type == "images":
        typer.echo("Processing directory of images...")
        # Process input - use default extensions
        image_files = ImagesHandler.process(input_path, "png,jpg,jpeg")

        # Handle export directory
        export_dir = InputHandler.handle_export_dir(export_dir, auto_cleanup)

        # Run inference
        run_inference(
            image_paths=image_files,
            export_dir=export_dir,
            model_dir=model_dir,
            device=device,
            backend_url=final_backend_url,
            export_format=export_format,
            process_res=process_res,
            process_res_method=process_res_method,
            export_feat_layers=export_feat_layers,
            use_ray_pose=use_ray_pose,
            ref_view_strategy=ref_view_strategy,
            conf_thresh_percentile=conf_thresh_percentile,
            num_max_points=num_max_points,
            show_cameras=show_cameras,
            feat_vis_fps=feat_vis_fps,
        )

    elif input_type == "video":
        typer.echo(f"Processing video with FPS={fps}...")
        # Handle export directory
        export_dir = InputHandler.handle_export_dir(export_dir, auto_cleanup)

        # Process input
        image_files = VideoHandler.process(input_path, export_dir, fps)

        # Run inference
        run_inference(
            image_paths=image_files,
            export_dir=export_dir,
            model_dir=model_dir,
            device=device,
            backend_url=final_backend_url,
            export_format=export_format,
            process_res=process_res,
            process_res_method=process_res_method,
            export_feat_layers=export_feat_layers,
            use_ray_pose=use_ray_pose,
            ref_view_strategy=ref_view_strategy,
            conf_thresh_percentile=conf_thresh_percentile,
            num_max_points=num_max_points,
            show_cameras=show_cameras,
            feat_vis_fps=feat_vis_fps,
        )

    elif input_type == "colmap":
        typer.echo(
            f"Processing COLMAP directory (sparse subdirectory: '{sparse_subdir or 'default'}')..."
        )
        # Process input
        image_files, extrinsics, intrinsics = ColmapHandler.process(input_path, sparse_subdir)

        # Handle export directory
        export_dir = InputHandler.handle_export_dir(export_dir, auto_cleanup)

        # Run inference
        run_inference(
            image_paths=image_files,
            export_dir=export_dir,
            model_dir=model_dir,
            device=device,
            backend_url=final_backend_url,
            export_format=export_format,
            process_res=process_res,
            process_res_method=process_res_method,
            export_feat_layers=export_feat_layers,
            extrinsics=extrinsics,
            intrinsics=intrinsics,
            align_to_input_ext_scale=align_to_input_ext_scale,
            use_ray_pose=use_ray_pose,
            ref_view_strategy=ref_view_strategy,
            conf_thresh_percentile=conf_thresh_percentile,
            num_max_points=num_max_points,
            show_cameras=show_cameras,
            feat_vis_fps=feat_vis_fps,
        )

    typer.echo()
    typer.echo("✅ Processing completed successfully!")


@app.command()
def image(
    image_path: str = typer.Argument(..., help="Path to input image file"),
    model_dir: str = typer.Option(DEFAULT_MODEL, help="Model directory path"),
    export_dir: str = typer.Option(DEFAULT_EXPORT_DIR, help="Export directory"),
    export_format: str = typer.Option("glb", help="Export format"),
    device: str = typer.Option("cuda", help="Device to use"),
    use_backend: bool = typer.Option(False, help="Use backend service for inference"),
    backend_url: str = typer.Option(
        "http://localhost:8008", help="Backend URL (default: http://localhost:8008)"
    ),
    process_res: int = typer.Option(504, help="Processing resolution"),
    process_res_method: str = typer.Option(
        "upper_bound_resize", help="Processing resolution method"
    ),
    export_feat: str = typer.Option(
        "",
        help="[FEAT_VIS] Export features from specified layers using comma-separated indices (e.g., '0,1,2').",
    ),
    auto_cleanup: bool = typer.Option(
        False, help="Automatically clean export directory if it exists (no prompt)"
    ),
    # Pose estimation options
    use_ray_pose: bool = typer.Option(
        False, help="Use ray-based pose estimation instead of camera decoder"
    ),
    ref_view_strategy: str = typer.Option(
        "saddle_balanced",
        help="Reference view selection strategy: empty, first, middle, saddle_balanced, saddle_sim_range",
    ),
    # GLB export options
    conf_thresh_percentile: float = typer.Option(
        40.0, help="[GLB] Lower percentile for adaptive confidence threshold"
    ),
    num_max_points: int = typer.Option(
        1_000_000, help="[GLB] Maximum number of points in the point cloud"
    ),
    show_cameras: bool = typer.Option(
        True, help="[GLB] Show camera wireframes in the exported scene"
    ),
    # Feat_vis export options
    feat_vis_fps: int = typer.Option(15, help="[FEAT_VIS] Frame rate for output video"),
):
    """Run camera pose and depth estimation on a single image."""
    # Process input
    image_files = ImageHandler.process(image_path)

    # Handle export directory
    export_dir = InputHandler.handle_export_dir(export_dir, auto_cleanup)

    # Parse export_feat parameter
    export_feat_layers = parse_export_feat(export_feat)

    # Determine backend URL based on use_backend flag
    final_backend_url = backend_url if use_backend else None

    # Run inference
    run_inference(
        image_paths=image_files,
        export_dir=export_dir,
        model_dir=model_dir,
        device=device,
        backend_url=final_backend_url,
        export_format=export_format,
        process_res=process_res,
        process_res_method=process_res_method,
        export_feat_layers=export_feat_layers,
        use_ray_pose=use_ray_pose,
        reference_view_strategy=reference_view_strategy,
        conf_thresh_percentile=conf_thresh_percentile,
        num_max_points=num_max_points,
        show_cameras=show_cameras,
        feat_vis_fps=feat_vis_fps,
    )


@app.command()
def images(
    images_dir: str = typer.Argument(..., help="Path to directory containing input images"),
    image_extensions: str = typer.Option(
        "png,jpg,jpeg", help="Comma-separated image file extensions to process"
    ),
    model_dir: str = typer.Option(DEFAULT_MODEL, help="Model directory path"),
    export_dir: str = typer.Option(DEFAULT_EXPORT_DIR, help="Export directory"),
    export_format: str = typer.Option("glb", help="Export format"),
    device: str = typer.Option("cuda", help="Device to use"),
    use_backend: bool = typer.Option(False, help="Use backend service for inference"),
    backend_url: str = typer.Option(
        "http://localhost:8008", help="Backend URL (default: http://localhost:8008)"
    ),
    process_res: int = typer.Option(504, help="Processing resolution"),
    process_res_method: str = typer.Option(
        "upper_bound_resize", help="Processing resolution method"
    ),
    export_feat: str = typer.Option(
        "",
        help="[FEAT_VIS] Export features from specified layers using comma-separated indices (e.g., '0,1,2').",
    ),
    auto_cleanup: bool = typer.Option(
        False, help="Automatically clean export directory if it exists (no prompt)"
    ),
    # Pose estimation options
    use_ray_pose: bool = typer.Option(
        False, help="Use ray-based pose estimation instead of camera decoder"
    ),
    ref_view_strategy: str = typer.Option(
        "saddle_balanced",
        help="Reference view selection strategy: empty, first, middle, saddle_balanced, saddle_sim_range",
    ),
    # GLB export options
    conf_thresh_percentile: float = typer.Option(
        40.0, help="[GLB] Lower percentile for adaptive confidence threshold"
    ),
    num_max_points: int = typer.Option(
        1_000_000, help="[GLB] Maximum number of points in the point cloud"
    ),
    show_cameras: bool = typer.Option(
        True, help="[GLB] Show camera wireframes in the exported scene"
    ),
    # Feat_vis export options
    feat_vis_fps: int = typer.Option(15, help="[FEAT_VIS] Frame rate for output video"),
):
    """Run camera pose and depth estimation on a directory of images."""
    # Process input
    image_files = ImagesHandler.process(images_dir, image_extensions)

    # Handle export directory
    export_dir = InputHandler.handle_export_dir(export_dir, auto_cleanup)

    # Parse export_feat parameter
    export_feat_layers = parse_export_feat(export_feat)

    # Determine backend URL based on use_backend flag
    final_backend_url = backend_url if use_backend else None

    # Run inference
    run_inference(
        image_paths=image_files,
        export_dir=export_dir,
        model_dir=model_dir,
        device=device,
        backend_url=final_backend_url,
        export_format=export_format,
        process_res=process_res,
        process_res_method=process_res_method,
        export_feat_layers=export_feat_layers,
        use_ray_pose=use_ray_pose,
        reference_view_strategy=reference_view_strategy,
        conf_thresh_percentile=conf_thresh_percentile,
        num_max_points=num_max_points,
        show_cameras=show_cameras,
        feat_vis_fps=feat_vis_fps,
    )


@app.command()
def colmap(
    colmap_dir: str = typer.Argument(
        ..., help="Path to COLMAP directory containing 'images' and 'sparse' subdirectories"
    ),
    sparse_subdir: str = typer.Option(
        "", help="Sparse reconstruction subdirectory (e.g., '0' for sparse/0/, empty for sparse/)"
    ),
    align_to_input_ext_scale: bool = typer.Option(
        True, help="Align prediction to input extrinsics scale"
    ),
    model_dir: str = typer.Option(DEFAULT_MODEL, help="Model directory path"),
    export_dir: str = typer.Option(DEFAULT_EXPORT_DIR, help="Export directory"),
    export_format: str = typer.Option("glb", help="Export format"),
    device: str = typer.Option("cuda", help="Device to use"),
    use_backend: bool = typer.Option(False, help="Use backend service for inference"),
    backend_url: str = typer.Option(
        "http://localhost:8008", help="Backend URL (default: http://localhost:8008)"
    ),
    process_res: int = typer.Option(504, help="Processing resolution"),
    process_res_method: str = typer.Option(
        "upper_bound_resize", help="Processing resolution method"
    ),
    export_feat: str = typer.Option(
        "",
        help="Export features from specified layers using comma-separated indices (e.g., '0,1,2').",
    ),
    auto_cleanup: bool = typer.Option(
        False, help="Automatically clean export directory if it exists (no prompt)"
    ),
    # Pose estimation options
    use_ray_pose: bool = typer.Option(
        False, help="Use ray-based pose estimation instead of camera decoder"
    ),
    ref_view_strategy: str = typer.Option(
        "saddle_balanced",
        help="Reference view selection strategy: empty, first, middle, saddle_balanced, saddle_sim_range",
    ),
    # GLB export options
    conf_thresh_percentile: float = typer.Option(
        40.0, help="[GLB] Lower percentile for adaptive confidence threshold"
    ),
    num_max_points: int = typer.Option(
        1_000_000, help="[GLB] Maximum number of points in the point cloud"
    ),
    show_cameras: bool = typer.Option(
        True, help="[GLB] Show camera wireframes in the exported scene"
    ),
    # Feat_vis export options
    feat_vis_fps: int = typer.Option(15, help="[FEAT_VIS] Frame rate for output video"),
):
    """Run pose conditioned depth estimation on COLMAP data."""
    # Process input
    image_files, extrinsics, intrinsics = ColmapHandler.process(colmap_dir, sparse_subdir)

    # Handle export directory
    export_dir = InputHandler.handle_export_dir(export_dir, auto_cleanup)

    # Parse export_feat parameter
    export_feat_layers = parse_export_feat(export_feat)

    # Determine backend URL based on use_backend flag
    final_backend_url = backend_url if use_backend else None

    # Run inference
    run_inference(
        image_paths=image_files,
        export_dir=export_dir,
        model_dir=model_dir,
        device=device,
        backend_url=final_backend_url,
        export_format=export_format,
        process_res=process_res,
        process_res_method=process_res_method,
        export_feat_layers=export_feat_layers,
        extrinsics=extrinsics,
        intrinsics=intrinsics,
        align_to_input_ext_scale=align_to_input_ext_scale,
        use_ray_pose=use_ray_pose,
        reference_view_strategy=reference_view_strategy,
        conf_thresh_percentile=conf_thresh_percentile,
        num_max_points=num_max_points,
        show_cameras=show_cameras,
        feat_vis_fps=feat_vis_fps,
    )


@app.command()
def video(
    video_path: str = typer.Argument(..., help="Path to input video file"),
    fps: float = typer.Option(1.0, help="Sampling FPS for frame extraction"),
    model_dir: str = typer.Option(DEFAULT_MODEL, help="Model directory path"),
    export_dir: str = typer.Option(DEFAULT_EXPORT_DIR, help="Export directory"),
    export_format: str = typer.Option("glb", help="Export format"),
    device: str = typer.Option("cuda", help="Device to use"),
    use_backend: bool = typer.Option(False, help="Use backend service for inference"),
    backend_url: str = typer.Option(
        "http://localhost:8008", help="Backend URL (default: http://localhost:8008)"
    ),
    process_res: int = typer.Option(504, help="Processing resolution"),
    process_res_method: str = typer.Option(
        "upper_bound_resize", help="Processing resolution method"
    ),
    export_feat: str = typer.Option(
        "",
        help="[FEAT_VIS] Export features from specified layers using comma-separated indices (e.g., '0,1,2').",
    ),
    auto_cleanup: bool = typer.Option(
        False, help="Automatically clean export directory if it exists (no prompt)"
    ),
    # Pose estimation options
    use_ray_pose: bool = typer.Option(
        False, help="Use ray-based pose estimation instead of camera decoder"
    ),
    ref_view_strategy: str = typer.Option(
        "saddle_balanced",
        help="Reference view selection strategy: empty, first, middle, saddle_balanced, saddle_sim_range",
    ),
    # GLB export options
    conf_thresh_percentile: float = typer.Option(
        40.0, help="[GLB] Lower percentile for adaptive confidence threshold"
    ),
    num_max_points: int = typer.Option(
        1_000_000, help="[GLB] Maximum number of points in the point cloud"
    ),
    show_cameras: bool = typer.Option(
        True, help="[GLB] Show camera wireframes in the exported scene"
    ),
    # Feat_vis export options
    feat_vis_fps: int = typer.Option(15, help="[FEAT_VIS] Frame rate for output video"),
):
    """Run depth estimation on video by extracting frames and processing them."""
    # Handle export directory
    export_dir = InputHandler.handle_export_dir(export_dir, auto_cleanup)

    # Process input
    image_files = VideoHandler.process(video_path, export_dir, fps)

    # Parse export_feat parameter
    export_feat_layers = parse_export_feat(export_feat)

    # Determine backend URL based on use_backend flag
    final_backend_url = backend_url if use_backend else None

    # Run inference
    run_inference(
        image_paths=image_files,
        export_dir=export_dir,
        model_dir=model_dir,
        device=device,
        backend_url=final_backend_url,
        export_format=export_format,
        process_res=process_res,
        process_res_method=process_res_method,
        export_feat_layers=export_feat_layers,
        use_ray_pose=use_ray_pose,
        reference_view_strategy=reference_view_strategy,
        conf_thresh_percentile=conf_thresh_percentile,
        num_max_points=num_max_points,
        show_cameras=show_cameras,
        feat_vis_fps=feat_vis_fps,
    )


# ============================================================================
# Service management commands
# ============================================================================


@app.command()
def backend(
    model_dir: str = typer.Option(DEFAULT_MODEL, help="Model directory path"),
    device: str = typer.Option("cuda", help="Device to use"),
    host: str = typer.Option("127.0.0.1", help="Host to bind to"),
    port: int = typer.Option(8008, help="Port to bind to"),
    gallery_dir: str = typer.Option(DEFAULT_GALLERY_DIR, help="Gallery directory path (optional)"),
):
    """Start model backend service with integrated gallery."""
    typer.echo("=" * 60)
    typer.echo("🚀 Starting Depth Anything 3 Backend Server")
    typer.echo("=" * 60)
    typer.echo(f"Model directory: {model_dir}")
    typer.echo(f"Device: {device}")

    # Check if gallery directory exists
    if gallery_dir and os.path.exists(gallery_dir):
        typer.echo(f"Gallery directory: {gallery_dir}")
    else:
        gallery_dir = None  # Disable gallery if directory doesn't exist

    typer.echo()
    typer.echo("📡 Server URLs (Ctrl/CMD+Click to open):")
    typer.echo(f"  🏠 Home:      http://{host}:{port}")
    typer.echo(f"  📊 Dashboard: http://{host}:{port}/dashboard")
    typer.echo(f"  📈 API Status: http://{host}:{port}/status")

    if gallery_dir:
        typer.echo(f"  🎨 Gallery:   http://{host}:{port}/gallery/")

    typer.echo("=" * 60)

    try:
        start_server(model_dir, device, host, port, gallery_dir)
    except KeyboardInterrupt:
        typer.echo("\n👋 Backend server stopped.")
    except Exception as e:
        typer.echo(f"❌ Failed to start backend: {e}")
        raise typer.Exit(1)


# ============================================================================
# Application launch commands
# ============================================================================


@app.command()
def gradio(
    model_dir: str = typer.Option(DEFAULT_MODEL, help="Model directory path"),
    workspace_dir: str = typer.Option(DEFAULT_GRADIO_DIR, help="Workspace directory path"),
    gallery_dir: str = typer.Option(DEFAULT_GALLERY_DIR, help="Gallery directory path"),
    host: str = typer.Option("127.0.0.1", help="Host address to bind to"),
    port: int = typer.Option(7860, help="Port number to bind to"),
    share: bool = typer.Option(False, help="Create a public link for the app"),
    debug: bool = typer.Option(False, help="Enable debug mode"),
    cache_examples: bool = typer.Option(
        False, help="Pre-cache all example scenes at startup for faster loading"
    ),
    cache_gs_tag: str = typer.Option(
        "",
        help="Tag to match scene names for high-res+3DGS caching (e.g., 'dl3dv'). Scenes containing this tag will use high_res and infer_gs=True; others will use low_res only.",
    ),
):
    """Launch Depth Anything 3 Gradio interactive web application"""
    from depth_anything_3.app.gradio_app import DepthAnything3App

    # Create necessary directories
    os.makedirs(workspace_dir, exist_ok=True)
    os.makedirs(gallery_dir, exist_ok=True)

    typer.echo("Launching Depth Anything 3 Gradio application...")
    typer.echo(f"Model directory: {model_dir}")
    typer.echo(f"Workspace directory: {workspace_dir}")
    typer.echo(f"Gallery directory: {gallery_dir}")
    typer.echo(f"Host: {host}")
    typer.echo(f"Port: {port}")
    typer.echo(f"Share: {share}")
    typer.echo(f"Debug mode: {debug}")
    typer.echo(f"Cache examples: {cache_examples}")
    if cache_examples:
        if cache_gs_tag:
            typer.echo(
                f"Cache GS Tag: '{cache_gs_tag}' (scenes matching this tag will use high-res + 3DGS)"
            )
        else:
            typer.echo(f"Cache GS Tag: None (all scenes will use low-res only)")

    try:
        # Initialize and launch application
        app = DepthAnything3App(
            model_dir=model_dir, workspace_dir=workspace_dir, gallery_dir=gallery_dir
        )

        # Pre-cache examples if requested
        if cache_examples:
            typer.echo("\n" + "=" * 60)
            typer.echo("Pre-caching mode enabled")
            if cache_gs_tag:
                typer.echo(f"Scenes containing '{cache_gs_tag}' will use HIGH-RES + 3DGS")
                typer.echo(f"Other scenes will use LOW-RES only")
            else:
                typer.echo(f"All scenes will use LOW-RES only")
            typer.echo("=" * 60)
            app.cache_examples(
                show_cam=True,
                filter_black_bg=False,
                filter_white_bg=False,
                save_percentage=20.0,
                num_max_points=1000,
                cache_gs_tag=cache_gs_tag,
                gs_trj_mode="smooth",
                gs_video_quality="low",
            )

        # Prepare launch arguments
        launch_kwargs = {"share": share, "debug": debug}

        app.launch(host=host, port=port, **launch_kwargs)

    except KeyboardInterrupt:
        typer.echo("\nGradio application stopped.")
    except Exception as e:
        typer.echo(f"Failed to launch Gradio application: {e}")
        raise typer.Exit(1)


@app.command()
def gallery(
    gallery_dir: str = typer.Option(DEFAULT_GALLERY_DIR, help="Gallery root directory"),
    host: str = typer.Option("127.0.0.1", help="Host address to bind to"),
    port: int = typer.Option(8007, help="Port number to bind to"),
    open_browser: bool = typer.Option(False, help="Open browser after launch"),
):
    """Launch Depth Anything 3 Gallery server"""

    # Validate gallery directory
    if not os.path.exists(gallery_dir):
        raise typer.BadParameter(f"Gallery directory not found: {gallery_dir}")

    typer.echo("Launching Depth Anything 3 Gallery server...")
    typer.echo(f"Gallery directory: {gallery_dir}")
    typer.echo(f"Host: {host}")
    typer.echo(f"Port: {port}")
    typer.echo(f"Auto-open browser: {open_browser}")

    try:
        # Set command line arguments
        import sys

        sys.argv = ["gallery", "--dir", gallery_dir, "--host", host, "--port", str(port)]
        if open_browser:
            sys.argv.append("--open")

        # Launch gallery server
        gallery_main()

    except KeyboardInterrupt:
        typer.echo("\nGallery server stopped.")
    except Exception as e:
        typer.echo(f"Failed to launch Gallery server: {e}")
        raise typer.Exit(1)


if __name__ == "__main__":
    app()



================================================
FILE: src/depth_anything_3/registry.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

from collections import OrderedDict
from pathlib import Path


def get_all_models() -> OrderedDict:
    """
    Scans all YAML files in the configs directory and returns a sorted dictionary where:
    - Keys are model names (YAML filenames without the .yaml extension)
    - Values are absolute paths to the corresponding YAML files
    """
    # Get path to the configs directory within the da3 package
    # Works both in development and after pip installation
    # configs_dir = files("depth_anything_3").joinpath("configs")
    configs_dir = Path(__file__).resolve().parent / "configs"

    # Ensure path is a Path object for consistent cross-platform handling
    configs_dir = Path(configs_dir)

    model_entries = []
    # Iterate through all items in the configs directory
    for item in configs_dir.iterdir():
        # Filter for YAML files (excluding directories)
        if item.is_file() and item.suffix == ".yaml":
            # Extract model name (filename without .yaml extension)
            model_name = item.stem
            # Get absolute path (resolve() handles symlinks)
            file_abs_path = str(item.resolve())
            model_entries.append((model_name, file_abs_path))

    # Sort entries by model name and convert to OrderedDict
    sorted_entries = sorted(model_entries, key=lambda x: x[0])
    return OrderedDict(sorted_entries)


# Global registry for external imports
MODEL_REGISTRY = get_all_models()



================================================
FILE: src/depth_anything_3/specs.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

from __future__ import annotations

from dataclasses import dataclass
from typing import Any, Optional
import numpy as np
import torch


@dataclass
class Gaussians:
    """3DGS parameters, all in world space"""

    means: torch.Tensor  # world points, "batch gaussian dim"
    scales: torch.Tensor  # scales_std, "batch gaussian 3"
    rotations: torch.Tensor  # world_quat_wxyz, "batch gaussian 4"
    harmonics: torch.Tensor  # world SH, "batch gaussian 3 d_sh"
    opacities: torch.Tensor  # opacity | opacity SH, "batch gaussian" | "batch gaussian 1 d_sh"


@dataclass
class Prediction:
    depth: np.ndarray  # N, H, W
    is_metric: int
    sky: np.ndarray | None = None  # N, H, W
    conf: np.ndarray | None = None  # N, H, W
    extrinsics: np.ndarray | None = None  # N, 4, 4
    intrinsics: np.ndarray | None = None  # N, 3, 3
    processed_images: np.ndarray | None = None  # N, H, W, 3 - processed images for visualization
    gaussians: Gaussians | None = None  # 3D gaussians
    aux: dict[str, Any] = None  #
    scale_factor: Optional[float] = None  # metric scale



================================================
FILE: src/depth_anything_3/app/css_and_html.py
================================================
# flake8: noqa: E501

# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

"""
CSS and HTML content for the Depth Anything 3 Gradio application.
This module contains all the CSS styles and HTML content blocks
used in the Gradio interface.
"""

# CSS Styles for the Gradio interface
GRADIO_CSS = """
/* Add Font Awesome CDN with all styles including brands and colors */
@import url('https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css');

/* Add custom styles for colored icons */
.fa-color-blue {
    color: #3b82f6;
}

.fa-color-purple {
    color: #8b5cf6;
}

.fa-color-cyan {
    color: #06b6d4;
}

.fa-color-green {
    color: #10b981;
}

.fa-color-yellow {
    color: #f59e0b;
}

.fa-color-red {
    color: #ef4444;
}

.link-btn {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    text-decoration: none;
    padding: 12px 24px;
    border-radius: 50px;
    font-weight: 500;
    transition: all 0.3s ease;
}

/* Dark mode tech theme */
@media (prefers-color-scheme: dark) {
    html, body {
        background: #1e293b;
        color: #ffffff;
    }

    .gradio-container {
        background: #1e293b;
        color: #ffffff;
    }

    .link-btn {
        background: rgba(255, 255, 255, 0.2);
        color: white;
        backdrop-filter: blur(10px);
        border: 1px solid rgba(255, 255, 255, 0.3);
    }

    .link-btn:hover {
        background: rgba(255, 255, 255, 0.3);
        transform: translateY(-2px);
        box-shadow: 0 8px 25px rgba(0, 0, 0, 0.2);
    }

    .tech-bg {
        background: linear-gradient(135deg, #0f172a, #1e293b); /* Darker colors */
        position: relative;
        overflow: hidden;
    }

    .tech-bg::before {
        content: '';
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        background:
            radial-gradient(circle at 20% 80%, rgba(59, 130, 246, 0.15) 0%, transparent 50%), /* Reduced opacity */
            radial-gradient(circle at 80% 20%, rgba(139, 92, 246, 0.15) 0%, transparent 50%), /* Reduced opacity */
            radial-gradient(circle at 40% 40%, rgba(18, 194, 233, 0.1) 0%, transparent 50%); /* Reduced opacity */
        animation: techPulse 8s ease-in-out infinite;
    }

    .gradio-container .panel,
    .gradio-container .block,
    .gradio-container .form {
        background: rgba(0, 0, 0, 0.3);
        border: 1px solid rgba(59, 130, 246, 0.2);
        border-radius: 10px;
    }

    .gradio-container * {
        color: #ffffff;
    }

    .gradio-container label {
        color: #e0e0e0;
    }

    .gradio-container .markdown {
        color: #e0e0e0;
    }
}

/* Light mode tech theme */
@media (prefers-color-scheme: light) {
    html, body {
        background: #ffffff;
        color: #1e293b;
    }

    .gradio-container {
        background: #ffffff;
        color: #1e293b;
    }

    .tech-bg {
        background: linear-gradient(135deg, #ffffff, #f1f5f9);
        position: relative;
        overflow: hidden;
    }

    .link-btn {
        background: rgba(59, 130, 246, 0.15);
        color: var(--body-text-color);
        border: 1px solid rgba(59, 130, 246, 0.3);
    }

    .link-btn:hover {
        background: rgba(59, 130, 246, 0.25);
        transform: translateY(-2px);
        box-shadow: 0 8px 25px rgba(59, 130, 246, 0.2);
    }

    .tech-bg::before {
        content: '';
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        background:
            radial-gradient(circle at 20% 80%, rgba(59, 130, 246, 0.1) 0%, transparent 50%),
            radial-gradient(circle at 80% 20%, rgba(139, 92, 246, 0.1) 0%, transparent 50%),
            radial-gradient(circle at 40% 40%, rgba(18, 194, 233, 0.08) 0%, transparent 50%);
        animation: techPulse 8s ease-in-out infinite;
    }

    .gradio-container .panel,
    .gradio-container .block,
    .gradio-container .form {
        background: rgba(255, 255, 255, 0.8);
        border: 1px solid rgba(59, 130, 246, 0.3);
        border-radius: 10px;
        box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    }

    .gradio-container * {
        color: #1e293b;
    }

    .gradio-container label {
        color: #334155;
    }

    .gradio-container .markdown {
        color: #334155;
    }
}




@keyframes techPulse {
    0%, 100% { opacity: 0.5; }
    50% { opacity: 0.8; }
}

/* Custom log with tech gradient */
.custom-log * {
    font-style: italic;
    font-size: 22px !important;
    background: linear-gradient(135deg, #3b82f6, #8b5cf6);
    background-size: 400% 400%;
    -webkit-background-clip: text;
    background-clip: text;
    font-weight: bold !important;
    color: transparent !important;
    text-align: center !important;
    animation: techGradient 3s ease infinite;
}

@keyframes techGradient {
    0% { background-position: 0% 50%; }
    50% { background-position: 100% 50%; }
    100% { background-position: 0% 50%; }
}

@keyframes metricPulse {
    0%, 100% { background-position: 0% 50%; }
    50% { background-position: 100% 50%; }
}

@keyframes pointcloudPulse {
    0%, 100% { background-position: 0% 50%; }
    50% { background-position: 100% 50%; }
}

@keyframes camerasPulse {
    0%, 100% { background-position: 0% 50%; }
    50% { background-position: 100% 50%; }
}

@keyframes gaussiansPulse {
    0%, 100% { background-position: 0% 50%; }
    50% { background-position: 100% 50%; }
}

/* Special colors for key terms - Global styles */
.metric-text {
    background: linear-gradient(45deg, #ff6b6b, #ff8e53, #ff6b6b);
    background-size: 200% 200%;
    -webkit-background-clip: text;
    background-clip: text;
    color: transparent !important;
    animation: metricPulse 2s ease-in-out infinite;
    font-weight: 700;
    text-shadow: 0 0 10px rgba(255, 107, 107, 0.5);
}

.pointcloud-text {
    background: linear-gradient(45deg, #4ecdc4, #44a08d, #4ecdc4);
    background-size: 200% 200%;
    -webkit-background-clip: text;
    background-clip: text;
    color: transparent !important;
    animation: pointcloudPulse 2.5s ease-in-out infinite;
    font-weight: 700;
    text-shadow: 0 0 10px rgba(78, 205, 196, 0.5);
}

.cameras-text {
    background: linear-gradient(45deg, #667eea, #764ba2, #667eea);
    background-size: 200% 200%;
    -webkit-background-clip: text;
    background-clip: text;
    color: transparent !important;
    animation: camerasPulse 3s ease-in-out infinite;
    font-weight: 700;
    text-shadow: 0 0 10px rgba(102, 126, 234, 0.5);
}

.gaussians-text {
    background: linear-gradient(45deg, #f093fb, #f5576c, #f093fb);
    background-size: 200% 200%;
    -webkit-background-clip: text;
    background-clip: text;
    color: transparent !important;
    animation: gaussiansPulse 2.2s ease-in-out infinite;
    font-weight: 700;
    text-shadow: 0 0 10px rgba(240, 147, 251, 0.5);
}

.example-log * {
    font-style: italic;
    font-size: 16px !important;
    background: linear-gradient(135deg, #3b82f6, #8b5cf6);
    -webkit-background-clip: text;
    background-clip: text;
    color: transparent !important;
}

#my_radio .wrap {
    display: flex;
    flex-wrap: nowrap;
    justify-content: center;
    align-items: center;
}

#my_radio .wrap label {
    display: flex;
    width: 50%;
    justify-content: center;
    align-items: center;
    margin: 0;
    padding: 10px 0;
    box-sizing: border-box;
}

/* Align navigation buttons with dropdown bottom */
.navigation-row {
    display: flex !important;
    align-items: flex-end !important;
    gap: 8px !important;
}

.navigation-row > div:nth-child(1),
.navigation-row > div:nth-child(3) {
    align-self: flex-end !important;
}

.navigation-row > div:nth-child(2) {
    flex: 1 !important;
}

/* Make thumbnails clickable with pointer cursor */
.clickable-thumbnail img {
    cursor: pointer !important;
}

.clickable-thumbnail:hover img {
    cursor: pointer !important;
    opacity: 0.8;
    transition: opacity 0.3s ease;
}

/* Make thumbnail containers narrower horizontally */
.clickable-thumbnail {
    padding: 5px 2px !important;
    margin: 0 2px !important;
}

.clickable-thumbnail .image-container {
    margin: 0 !important;
    padding: 0 !important;
}

.scene-info {
    text-align: center !important;
    padding: 5px 2px !important;
    margin: 0 !important;
}
"""


def get_header_html(logo_base64=None):
    """
    Generate the main header HTML with logo and title.

    Args:
        logo_base64 (str, optional): Base64 encoded logo image

    Returns:
        str: HTML string for the header
    """
    return """
    <div class="tech-bg" style="text-align: center; margin-bottom: 5px; padding: 40px 20px; border-radius: 15px; position: relative; overflow: hidden;">
        <div style="position: relative; z-index: 2;">
            <h1 style="margin: 0; font-size: 3.5em; font-weight: 700;
                background: linear-gradient(135deg, #3b82f6, #8b5cf6);
                background-size: 400% 400%;
                -webkit-background-clip: text;
                background-clip: text;
                color: transparent;
                animation: techGradient 3s ease infinite;
                text-shadow: 0 0 30px rgba(59, 130, 246, 0.5);
                letter-spacing: 2px;">
                Depth Anything 3
            </h1>
            <p style="margin: 15px 0 0 0; font-size: 2.16em; font-weight: 300;" class="header-subtitle">
                Recovering the Visual Space from Any Views
            </p>
            <div style="margin-top: 20px;">
                <!-- Revert buttons to original inline styles -->
                <a href="https://depth-anything-3.github.io" target="_blank" class="link-btn">
                    <i class="fas fa-globe" style="margin-right: 8px;"></i> Project Page
                </a>
                <a href="https://arxiv.org/abs/2406.09414" target="_blank" class="link-btn">
                    <i class="fas fa-file-pdf" style="margin-right: 8px;"></i> Paper
                </a>
                <a href="https://github.com/ByteDance-Seed/Depth-Anything-3" target="_blank" class="link-btn">
                    <i class="fab fa-github" style="margin-right: 8px;"></i> Code
                </a>
            </div>
        </div>
    </div>

    <style>
        /* Ensure tech-bg class is properly applied in dark mode */
        @media (prefers-color-scheme: dark) {
            .header-subtitle {
                color: #cbd5e1;
            }
            /* Increase priority to ensure background color is properly applied */
            .tech-bg {
                background: linear-gradient(135deg, #0f172a, #1e293b) !important;
            }
        }

        @media (prefers-color-scheme: light) {
            .header-subtitle {
                color: #475569;
            }
            /* Also add explicit background color for light mode */
            .tech-bg {
                background: linear-gradient(135deg, rgba(59, 130, 246, 0.1) 0%, rgba(139, 92, 246, 0.1) 100%) !important;
            }
        }
    </style>
    """


def get_description_html():
    """
    Generate the main description and getting started HTML.

    Returns:
        str: HTML string for the description
    """
    return """
    <div class="description-container" style="padding: 25px; border-radius: 15px; margin: 0 0 20px 0;">
        <h2 class="description-title" style="margin-top: 0; font-size: 1.6em; text-align: center;">
            <i class="fas fa-bullseye fa-color-red" style="margin-right: 8px;"></i> What This Demo Does
        </h2>
        <div class="description-content" style="padding: 20px; border-radius: 10px; margin: 15px 0; text-align: center;">
            <p class="description-main" style="line-height: 1.6; margin: 0; font-size: 1.45em;">
                <strong>Upload images or videos</strong> → <strong>Get <span class="metric-text">Metric</span> <span class="pointcloud-text">Point Clouds</span>, <span class="cameras-text">Cameras</span> and <span class="gaussians-text">Novel Views</span></strong> → <strong>Explore in 3D</strong>
            </p>
        </div>

        <div style="text-align: center; margin-top: 15px;">
            <p class="description-tip" style="font-style: italic; margin: 0;">
                <i class="fas fa-lightbulb fa-color-yellow" style="margin-right: 8px;"></i> <strong>Tip:</strong> Landscape-oriented images or videos are preferred for best 3D recovering.
            </p>
        </div>
    </div>

    <style>
        @media (prefers-color-scheme: dark) {
            .description-container {
                background: linear-gradient(135deg, rgba(59, 130, 246, 0.1) 0%, rgba(139, 92, 246, 0.1) 100%);
                border: 1px solid rgba(59, 130, 246, 0.2);
            }
            .description-title { color: #3b82f6; }
            .description-content { background: rgba(0, 0, 0, 0.3); }
            .description-main { color: #e0e0e0; }
            .description-text { color: #cbd5e1; }
            .description-tip { color: #cbd5e1; }
        }

        @media (prefers-color-scheme: light) {
            .description-container {
                background: linear-gradient(135deg, rgba(59, 130, 246, 0.05) 0%, rgba(139, 92, 246, 0.05) 100%);
                border: 1px solid rgba(59, 130, 246, 0.3);
            }
            .description-title { color: #3b82f6; }
            .description-content { background: transparent; }
            .description-main { color: #1e293b; }
            .description-text { color: #475569; }
            .description-tip { color: #475569; }
        }
    </style>
    """


def get_acknowledgements_html():
    """
    Generate the acknowledgements section HTML.

    Returns:
        str: HTML string for the acknowledgements
    """
    return """
    <div style="background: linear-gradient(135deg, rgba(59, 130, 246, 0.1) 0%, rgba(139, 92, 246, 0.1) 100%);
                padding: 25px; border-radius: 15px; margin: 20px 0; border: 1px solid rgba(59, 130, 246, 0.2);">
        <h3 style="color: #3b82f6; margin-top: 0; text-align: center; font-size: 1.4em;">
            <i class="fas fa-trophy fa-color-yellow" style="margin-right: 8px;"></i> Research Credits & Acknowledgments
        </h3>

        <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin: 15px 0;">
            <!-- Original Research Section (Left) -->
            <div style="text-align: center;">
                <h4 style="color: #8b5cf6; margin: 10px 0;"><i class="fas fa-flask fa-color-green" style="margin-right: 8px;"></i> Original Research</h4>
                <p style="color: #e0e0e0; margin: 5px 0;">
                    <a href="https://depth-anything-3.github.io" target="_blank"
                       style="color: #3b82f6; text-decoration: none; font-weight: 600;">
                        Depth Anything 3
                    </a>
                </p>
            </div>

            <!-- Previous Versions Section (Right) -->
            <div style="text-align: center;">
                <h4 style="color: #8b5cf6; margin: 10px 0;"><i class="fas fa-history fa-color-blue" style="margin-right: 8px;"></i> Previous Versions</h4>
                <div style="display: flex; flex-direction: row; gap: 15px; justify-content: center; align-items: center;">
                    <p style="color: #e0e0e0; margin: 0;">
                        <a href="https://huggingface.co/spaces/LiheYoung/Depth-Anything" target="_blank"
                           style="color: #3b82f6; text-decoration: none; font-weight: 600;">
                            Depth-Anything
                        </a>
                    </p>
                    <span style="color: #e0e0e0;">•</span>
                    <p style="color: #e0e0e0; margin: 0;">
                        <a href="https://huggingface.co/spaces/depth-anything/Depth-Anything-V2" target="_blank"
                           style="color: #3b82f6; text-decoration: none; font-weight: 600;">
                            Depth-Anything-V2
                        </a>
                    </p>
                </div>
            </div>
        </div>

        <!-- HF Demo Adapted from - Centered at the bottom of the whole block -->
        <div style="margin-top: 20px; padding-top: 15px; border-top: 1px solid rgba(59, 130, 246, 0.3); text-align: center;">
            <p style="color: #a0a0a0; font-size: 0.9em; margin: 0;">
                <i class="fas fa-code-branch fa-color-gray" style="margin-right: 5px;"></i> HF demo adapted from <a href="https://huggingface.co/spaces/facebook/map-anything" target="_blank" style="color: inherit; text-decoration: none;">Map Anything</a>
            </p>
        </div>
    </div>
    """


def get_gradio_theme():
    """
    Get the configured Gradio theme with adaptive tech colors.

    Returns:
        gr.themes.Base: Configured Gradio theme
    """
    import gradio as gr

    return gr.themes.Base(
        primary_hue=gr.themes.Color(
            c50="#eff6ff",
            c100="#dbeafe",
            c200="#bfdbfe",
            c300="#93c5fd",
            c400="#60a5fa",
            c500="#3b82f6",
            c600="#2563eb",
            c700="#1d4ed8",
            c800="#1e40af",
            c900="#1e3a8a",
            c950="#172554",
        ),
        secondary_hue=gr.themes.Color(
            c50="#f5f3ff",
            c100="#ede9fe",
            c200="#ddd6fe",
            c300="#c4b5fd",
            c400="#a78bfa",
            c500="#8b5cf6",
            c600="#7c3aed",
            c700="#6d28d9",
            c800="#5b21b6",
            c900="#4c1d95",
            c950="#2e1065",
        ),
        neutral_hue=gr.themes.Color(
            c50="#f8fafc",
            c100="#f1f5f9",
            c200="#e2e8f0",
            c300="#cbd5e1",
            c400="#94a3b8",
            c500="#64748b",
            c600="#475569",
            c700="#334155",
            c800="#1e293b",
            c900="#0f172a",
            c950="#020617",
        ),
    )


# Measure tab instructions HTML
MEASURE_INSTRUCTIONS_HTML = """
### Click points on the image to compute distance.
> <i class="fas fa-triangle-exclamation fa-color-red" style="margin-right: 5px;"></i> Metric scale estimation is difficult on aerial/drone images.
"""



================================================
FILE: src/depth_anything_3/app/gradio_app.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

"""
Refactored Gradio App for Depth Anything 3.

This is the main application file that orchestrates all components.
The original functionality has been split into modular components for better maintainability.
"""

import argparse
import os
from typing import Any, Dict, List
import gradio as gr

from depth_anything_3.app.css_and_html import GRADIO_CSS, get_gradio_theme
from depth_anything_3.app.modules.event_handlers import EventHandlers
from depth_anything_3.app.modules.ui_components import UIComponents

# Set environment variables
os.environ["PYTORCH_CUDA_ALLOC_CONF"] = "expandable_segments:True"


class DepthAnything3App:
    """
    Main application class for Depth Anything 3 Gradio app.
    """

    def __init__(self, model_dir: str = None, workspace_dir: str = None, gallery_dir: str = None):
        """
        Initialize the application.

        Args:
            model_dir: Path to the model directory
            workspace_dir: Path to the workspace directory
            gallery_dir: Path to the gallery directory
        """
        self.model_dir = model_dir
        self.workspace_dir = workspace_dir
        self.gallery_dir = gallery_dir

        # Set environment variables for directories
        if self.model_dir:
            os.environ["DA3_MODEL_DIR"] = self.model_dir
        if self.workspace_dir:
            os.environ["DA3_WORKSPACE_DIR"] = self.workspace_dir
        if self.gallery_dir:
            os.environ["DA3_GALLERY_DIR"] = self.gallery_dir

        self.event_handlers = EventHandlers()
        self.ui_components = UIComponents()

    def cache_examples(
        self,
        show_cam: bool = True,
        filter_black_bg: bool = False,
        filter_white_bg: bool = False,
        save_percentage: float = 20.0,
        num_max_points: int = 1000,
        cache_gs_tag: str = "",
        gs_trj_mode: str = "smooth",
        gs_video_quality: str = "low",
    ) -> None:
        """
        Pre-cache all example scenes at startup.

        Args:
            show_cam: Whether to show camera in visualization
            filter_black_bg: Whether to filter black background
            filter_white_bg: Whether to filter white background
            save_percentage: Filter percentage for point cloud
            num_max_points: Maximum number of points
            cache_gs_tag: Tag to match scene names for high-res+3DGS caching (e.g., "dl3dv")
            gs_trj_mode: Trajectory mode for 3DGS
            gs_video_quality: Video quality for 3DGS
        """
        from depth_anything_3.app.modules.utils import get_scene_info

        examples_dir = os.path.join(self.workspace_dir, "examples")
        if not os.path.exists(examples_dir):
            print(f"Examples directory not found: {examples_dir}")
            return

        scenes = get_scene_info(examples_dir)
        if not scenes:
            print("No example scenes found to cache.")
            return

        print(f"\n{'='*60}")
        print(f"Caching {len(scenes)} example scenes...")
        print(f"{'='*60}\n")

        for i, scene in enumerate(scenes, 1):
            scene_name = scene["name"]

            # Check if scene name matches the gs tag for high-res+3DGS caching
            use_high_res_gs = cache_gs_tag and cache_gs_tag.lower() in scene_name.lower()

            if use_high_res_gs:
                print(f"[{i}/{len(scenes)}] Caching scene: {scene_name} (HIGH-RES + 3DGS)")
                print(f"  - Number of images: {scene['num_images']}")
                print(f"  - Matched tag: '{cache_gs_tag}' - using high_res + 3DGS")
            else:
                print(f"[{i}/{len(scenes)}] Caching scene: {scene_name} (LOW-RES)")
                print(f"  - Number of images: {scene['num_images']}")

            try:
                # Load example scene
                _, target_dir, _, _, _, _, _, _, _ = self.event_handlers.load_example_scene(
                    scene_name
                )

                if target_dir and target_dir != "None":
                    # Run reconstruction with appropriate settings
                    print("  - Running reconstruction...")
                    result = self.event_handlers.gradio_demo(
                        target_dir=target_dir,
                        show_cam=show_cam,
                        filter_black_bg=filter_black_bg,
                        filter_white_bg=filter_white_bg,
                        process_res_method="high_res" if use_high_res_gs else "low_res",
                        save_percentage=save_percentage,
                        num_max_points=num_max_points,
                        infer_gs=use_high_res_gs,
                        ref_view_strategy="saddle_balanced",
                        gs_trj_mode=gs_trj_mode,
                        gs_video_quality=gs_video_quality,
                    )

                    # Check if successful
                    if result[0] is not None:  # reconstruction_output
                        print(f"  ✓ Scene '{scene_name}' cached successfully")
                    else:
                        print(f"  ✗ Scene '{scene_name}' caching failed: {result[1]}")
                else:
                    print(f"  ✗ Scene '{scene_name}' loading failed")

            except Exception as e:
                print(f"  ✗ Error caching scene '{scene_name}': {str(e)}")

            print()

        print("=" * 60)
        print("Example scene caching completed!")
        print("=" * 60 + "\n")

    def create_app(self) -> gr.Blocks:
        """
        Create and configure the Gradio application.

        Returns:
            Configured Gradio Blocks interface
        """

        # Initialize theme
        def get_theme():
            return get_gradio_theme()

        with gr.Blocks(theme=get_theme(), css=GRADIO_CSS) as demo:
            # State variables for the tabbed interface
            is_example = gr.Textbox(label="is_example", visible=False, value="None")
            processed_data_state = gr.State(value=None)
            measure_points_state = gr.State(value=[])
            selected_image_index_state = gr.State(value=0)  # Track selected image index
            # current_view_index = gr.State(value=0)  # noqa: F841 Track current view index

            # Header and description
            self.ui_components.create_header_section()
            self.ui_components.create_description_section()

            target_dir_output = gr.Textbox(label="Target Dir", visible=False, value="None")

            # Main content area
            with gr.Row():
                with gr.Column(scale=2):
                    # Upload section
                    (
                        input_video,
                        s_time_interval,
                        input_images,
                        image_gallery,
                    ) = self.ui_components.create_upload_section()

                with gr.Column(scale=4):
                    with gr.Column():
                        # gr.Markdown("**Metric 3D Reconstruction (Point Cloud and Camera Poses)**")
                        # Reconstruction control section (buttons) - moved below tabs

                        log_output = gr.Markdown(
                            "Please upload a video or images, then click Reconstruct.",
                            elem_classes=["custom-log"],
                        )

                        # Tabbed interface
                        with gr.Tabs():
                            with gr.Tab("Point Cloud & Cameras"):
                                reconstruction_output = (
                                    self.ui_components.create_3d_viewer_section()
                                )

                            with gr.Tab("Metric Depth"):
                                (
                                    prev_measure_btn,
                                    measure_view_selector,
                                    next_measure_btn,
                                    measure_image,
                                    measure_depth_image,
                                    measure_text,
                                ) = self.ui_components.create_measure_section()

                            with gr.Tab("3DGS Rendered Novel Views"):
                                gs_video, gs_info = self.ui_components.create_nvs_video()

                        # Inference control section (before inference)
                        (process_res_method_dropdown, infer_gs, ref_view_strategy_dropdown) = (
                            self.ui_components.create_inference_control_section()
                        )

                        # Display control section - includes 3DGS options, buttons, and Visualization Options  # noqa: E501
                        (
                            show_cam,
                            filter_black_bg,
                            filter_white_bg,
                            save_percentage,
                            num_max_points,
                            gs_trj_mode,
                            gs_video_quality,
                            submit_btn,
                            clear_btn,
                        ) = self.ui_components.create_display_control_section()

                        # bind visibility of gs_trj_mode to infer_gs
                        infer_gs.change(
                            fn=lambda checked: (
                                gr.update(visible=checked),
                                gr.update(visible=checked),
                                gr.update(visible=checked),
                                gr.update(visible=(not checked)),
                            ),
                            inputs=infer_gs,
                            outputs=[gs_trj_mode, gs_video_quality, gs_video, gs_info],
                        )

            # Example scenes section
            gr.Markdown("## Example Scenes")

            scenes = self.ui_components.create_example_scenes_section()
            scene_components = self.ui_components.create_example_scene_grid(scenes)

            # Set up event handlers
            self._setup_event_handlers(
                demo,
                is_example,
                processed_data_state,
                measure_points_state,
                target_dir_output,
                input_video,
                input_images,
                s_time_interval,
                image_gallery,
                reconstruction_output,
                log_output,
                show_cam,
                filter_black_bg,
                filter_white_bg,
                process_res_method_dropdown,
                save_percentage,
                submit_btn,
                clear_btn,
                num_max_points,
                infer_gs,
                ref_view_strategy_dropdown,
                selected_image_index_state,
                measure_view_selector,
                measure_image,
                measure_depth_image,
                measure_text,
                prev_measure_btn,
                next_measure_btn,
                scenes,
                scene_components,
                gs_video,
                gs_info,
                gs_trj_mode,
                gs_video_quality,
            )

            # Acknowledgements
            self.ui_components.create_acknowledgements_section()

        return demo

    def _setup_event_handlers(
        self,
        demo: gr.Blocks,
        is_example: gr.Textbox,
        processed_data_state: gr.State,
        measure_points_state: gr.State,
        target_dir_output: gr.Textbox,
        input_video: gr.Video,
        input_images: gr.File,
        s_time_interval: gr.Slider,
        image_gallery: gr.Gallery,
        reconstruction_output: gr.Model3D,
        log_output: gr.Markdown,
        show_cam: gr.Checkbox,
        filter_black_bg: gr.Checkbox,
        filter_white_bg: gr.Checkbox,
        process_res_method_dropdown: gr.Dropdown,
        save_percentage: gr.Slider,
        submit_btn: gr.Button,
        clear_btn: gr.ClearButton,
        num_max_points: gr.Slider,
        infer_gs: gr.Checkbox,
        ref_view_strategy_dropdown: gr.Dropdown,
        selected_image_index_state: gr.State,
        measure_view_selector: gr.Dropdown,
        measure_image: gr.Image,
        measure_depth_image: gr.Image,
        measure_text: gr.Markdown,
        prev_measure_btn: gr.Button,
        next_measure_btn: gr.Button,
        scenes: List[Dict[str, Any]],
        scene_components: List[gr.Image],
        gs_video: gr.Video,
        gs_info: gr.Markdown,
        gs_trj_mode: gr.Dropdown,
        gs_video_quality: gr.Dropdown,
    ) -> None:
        """
        Set up all event handlers for the application.

        Args:
            demo: Gradio Blocks interface
            All other arguments: Gradio components to connect
        """
        # Configure clear button
        clear_btn.add(
            [
                input_video,
                input_images,
                reconstruction_output,
                log_output,
                target_dir_output,
                image_gallery,
                gs_video,
            ]
        )

        # Main reconstruction button
        submit_btn.click(
            fn=self.event_handlers.clear_fields, inputs=[], outputs=[reconstruction_output]
        ).then(fn=self.event_handlers.update_log, inputs=[], outputs=[log_output]).then(
            fn=self.event_handlers.gradio_demo,
            inputs=[
                target_dir_output,
                show_cam,
                filter_black_bg,
                filter_white_bg,
                process_res_method_dropdown,
                save_percentage,
                # pass num_max_points
                num_max_points,
                infer_gs,
                ref_view_strategy_dropdown,
                gs_trj_mode,
                gs_video_quality,
            ],
            outputs=[
                reconstruction_output,
                log_output,
                processed_data_state,
                measure_image,
                measure_depth_image,
                measure_text,
                measure_view_selector,
                gs_video,
                gs_video,  # gs_video visibility
                gs_info,  # gs_info visibility
            ],
        ).then(
            fn=lambda: "False",
            inputs=[],
            outputs=[is_example],  # set is_example to "False"
        )

        # Real-time visualization updates
        self._setup_visualization_handlers(
            show_cam,
            filter_black_bg,
            filter_white_bg,
            process_res_method_dropdown,
            target_dir_output,
            is_example,
            reconstruction_output,
            log_output,
        )

        # File upload handlers
        input_video.change(
            fn=self.event_handlers.handle_uploads,
            inputs=[input_video, input_images, s_time_interval],
            outputs=[reconstruction_output, target_dir_output, image_gallery, log_output],
        )
        input_images.change(
            fn=self.event_handlers.handle_uploads,
            inputs=[input_video, input_images, s_time_interval],
            outputs=[reconstruction_output, target_dir_output, image_gallery, log_output],
        )

        # Navigation handlers
        self._setup_navigation_handlers(
            prev_measure_btn,
            next_measure_btn,
            measure_view_selector,
            measure_image,
            measure_depth_image,
            measure_points_state,
            processed_data_state,
        )

        # Measurement handler
        measure_image.select(
            fn=self.event_handlers.measure,
            inputs=[processed_data_state, measure_points_state, measure_view_selector],
            outputs=[measure_image, measure_depth_image, measure_points_state, measure_text],
        )

        # Example scene handlers
        self._setup_example_scene_handlers(
            scenes,
            scene_components,
            reconstruction_output,
            target_dir_output,
            image_gallery,
            log_output,
            is_example,
            processed_data_state,
            measure_view_selector,
            measure_image,
            measure_depth_image,
            gs_video,
            gs_info,
        )

    def _setup_visualization_handlers(
        self,
        show_cam: gr.Checkbox,
        filter_black_bg: gr.Checkbox,
        filter_white_bg: gr.Checkbox,
        process_res_method_dropdown: gr.Dropdown,
        target_dir_output: gr.Textbox,
        is_example: gr.Textbox,
        reconstruction_output: gr.Model3D,
        log_output: gr.Markdown,
    ) -> None:
        """Set up visualization update handlers."""
        # Common inputs for visualization updates
        viz_inputs = [
            target_dir_output,
            show_cam,
            is_example,
            filter_black_bg,
            filter_white_bg,
            process_res_method_dropdown,
        ]

        # Set up change handlers for all visualization controls
        for component in [show_cam, filter_black_bg, filter_white_bg]:
            component.change(
                fn=self.event_handlers.update_visualization,
                inputs=viz_inputs,
                outputs=[reconstruction_output, log_output],
            )

    def _setup_navigation_handlers(
        self,
        prev_measure_btn: gr.Button,
        next_measure_btn: gr.Button,
        measure_view_selector: gr.Dropdown,
        measure_image: gr.Image,
        measure_depth_image: gr.Image,
        measure_points_state: gr.State,
        processed_data_state: gr.State,
    ) -> None:
        """Set up navigation handlers for measure tab."""
        # Measure tab navigation
        prev_measure_btn.click(
            fn=lambda processed_data, current_selector: self.event_handlers.navigate_measure_view(
                processed_data, current_selector, -1
            ),
            inputs=[processed_data_state, measure_view_selector],
            outputs=[
                measure_view_selector,
                measure_image,
                measure_depth_image,
                measure_points_state,
            ],
        )

        next_measure_btn.click(
            fn=lambda processed_data, current_selector: self.event_handlers.navigate_measure_view(
                processed_data, current_selector, 1
            ),
            inputs=[processed_data_state, measure_view_selector],
            outputs=[
                measure_view_selector,
                measure_image,
                measure_depth_image,
                measure_points_state,
            ],
        )

        measure_view_selector.change(
            fn=lambda processed_data, selector_value: (
                self.event_handlers.update_measure_view(
                    processed_data, int(selector_value.split()[1]) - 1
                )
                if selector_value
                else (None, None, [])
            ),
            inputs=[processed_data_state, measure_view_selector],
            outputs=[measure_image, measure_depth_image, measure_points_state],
        )

    def _setup_example_scene_handlers(
        self,
        scenes: List[Dict[str, Any]],
        scene_components: List[gr.Image],
        reconstruction_output: gr.Model3D,
        target_dir_output: gr.Textbox,
        image_gallery: gr.Gallery,
        log_output: gr.Markdown,
        is_example: gr.Textbox,
        processed_data_state: gr.State,
        measure_view_selector: gr.Dropdown,
        measure_image: gr.Image,
        measure_depth_image: gr.Image,
        gs_video: gr.Video,
        gs_info: gr.Markdown,
    ) -> None:
        """Set up example scene handlers."""

        def load_and_update_measure(name):
            result = self.event_handlers.load_example_scene(name)
            # result = (reconstruction_output, target_dir, image_paths, log_message, processed_data, measure_view_selector, gs_video, gs_video_vis, gs_info_vis)  # noqa: E501

            # Update measure view if processed_data is available
            measure_img = None
            measure_depth = None
            if result[4] is not None:  # processed_data exists
                measure_img, measure_depth, _ = (
                    self.event_handlers.visualization_handler.update_measure_view(result[4], 0)
                )

            return result + ("True", measure_img, measure_depth)

        for i, scene in enumerate(scenes):
            if i < len(scene_components):
                scene_components[i].select(
                    fn=lambda name=scene["name"]: load_and_update_measure(name),
                    outputs=[
                        reconstruction_output,
                        target_dir_output,
                        image_gallery,
                        log_output,
                        processed_data_state,
                        measure_view_selector,
                        gs_video,
                        gs_video,  # gs_video_visibility
                        gs_info,  # gs_info_visibility
                        is_example,
                        measure_image,
                        measure_depth_image,
                    ],
                )

    def launch(self, host: str = "127.0.0.1", port: int = 7860, **kwargs) -> None:
        """
        Launch the application.

        Args:
            host: Host address to bind to
            port: Port number to bind to
            **kwargs: Additional arguments for demo.launch()
        """
        demo = self.create_app()
        demo.queue(max_size=20).launch(
            show_error=True, ssr_mode=False, server_name=host, server_port=port, **kwargs
        )


def main():
    """Main function to run the application."""
    parser = argparse.ArgumentParser(
        description="Depth Anything 3 Gradio Application",
        formatter_class=argparse.RawDescriptionHelpFormatter,
        epilog="""
Examples:
  # Basic usage
  python gradio_app.py --help
  python gradio_app.py --host 0.0.0.0 --port 8080
  python gradio_app.py --model-dir /path/to/model --workspace-dir /path/to/workspace

  # Cache examples at startup (all low-res)
  python gradio_app.py --cache-examples

  # Cache with selective high-res+3DGS for scenes matching tag
  python gradio_app.py --cache-examples --cache-gs-tag dl3dv
  # This will use high-res + 3DGS for scenes containing "dl3dv" in their name,
  # and low-res only for other scenes
        """,
    )

    # Server configuration
    parser.add_argument(
        "--host", default="127.0.0.1", help="Host address to bind to (default: 127.0.0.1)"
    )
    parser.add_argument(
        "--port", type=int, default=7860, help="Port number to bind to (default: 7860)"
    )

    # Directory configuration
    parser.add_argument(
        "--model-dir",
        default="depth-anything/DA3NESTED-GIANT-LARGE",
        help="Path to the model directory (default: depth-anything/DA3NESTED-GIANT-LARGE)",
    )
    parser.add_argument(
        "--workspace-dir",
        default="workspace/gradio",  # noqa: E501
        help="Path to the workspace directory (default: workspace/gradio)",  # noqa: E501
    )
    parser.add_argument(
        "--gallery-dir",
        default="workspace/gallery",
        help="Path to the gallery directory (default: workspace/gallery)",  # noqa: E501
    )

    # Additional Gradio options
    parser.add_argument("--share", action="store_true", help="Create a public link for the app")
    parser.add_argument("--debug", action="store_true", help="Enable debug mode")

    # Example caching options
    parser.add_argument(
        "--cache-examples",
        action="store_true",
        help="Pre-cache all example scenes at startup for faster loading",
    )
    parser.add_argument(
        "--cache-gs-tag",
        type=str,
        default="",
        help="Tag to match scene names for high-res+3DGS caching (e.g., 'dl3dv'). Scenes containing this tag will use high_res and infer_gs=True; others will use low_res only.",  # noqa: E501
    )

    args = parser.parse_args()

    # Create directories if they don't exist
    os.makedirs(args.workspace_dir, exist_ok=True)
    os.makedirs(args.gallery_dir, exist_ok=True)

    # Initialize and launch the application
    app = DepthAnything3App(
        model_dir=args.model_dir, workspace_dir=args.workspace_dir, gallery_dir=args.gallery_dir
    )

    # Prepare launch arguments
    launch_kwargs = {"share": args.share, "debug": args.debug}

    print("Starting Depth Anything 3 Gradio App...")
    print(f"Host: {args.host}")
    print(f"Port: {args.port}")
    print(f"Model Directory: {args.model_dir}")
    print(f"Workspace Directory: {args.workspace_dir}")
    print(f"Gallery Directory: {args.gallery_dir}")
    print(f"Share: {args.share}")
    print(f"Debug: {args.debug}")
    print(f"Cache Examples: {args.cache_examples}")
    if args.cache_examples:
        if args.cache_gs_tag:
            print(
                f"Cache GS Tag: '{args.cache_gs_tag}' (scenes matching this tag will use high-res + 3DGS)"  # noqa: E501
            )  # noqa: E501
        else:
            print("Cache GS Tag: None (all scenes will use low-res only)")

    # Pre-cache examples if requested
    if args.cache_examples:
        print("\n" + "=" * 60)
        print("Pre-caching mode enabled")
        if args.cache_gs_tag:
            print(f"Scenes containing '{args.cache_gs_tag}' will use HIGH-RES + 3DGS")
            print("Other scenes will use LOW-RES only")
        else:
            print("All scenes will use LOW-RES only")
        print("=" * 60)
        app.cache_examples(
            show_cam=True,
            filter_black_bg=False,
            filter_white_bg=False,
            save_percentage=5.0,
            num_max_points=1000,
            cache_gs_tag=args.cache_gs_tag,
            gs_trj_mode="smooth",
            gs_video_quality="low",
        )

    app.launch(host=args.host, port=args.port, **launch_kwargs)


if __name__ == "__main__":
    main()



================================================
FILE: src/depth_anything_3/app/modules/__init__.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

"""
Modules package for Depth Anything 3 Gradio app.

This package contains all the modular components for the Gradio application.
"""

from depth_anything_3.app.modules.event_handlers import EventHandlers
from depth_anything_3.app.modules.file_handlers import FileHandler
from depth_anything_3.app.modules.model_inference import ModelInference
from depth_anything_3.app.modules.ui_components import UIComponents
from depth_anything_3.app.modules.utils import (
    create_depth_visualization,
    get_logo_base64,
    get_scene_info,
    save_to_gallery_func,
)
from depth_anything_3.app.modules.visualization import VisualizationHandler

__all__ = [
    "ModelInference",
    "FileHandler",
    "VisualizationHandler",
    "EventHandlers",
    "UIComponents",
    "create_depth_visualization",
    "save_to_gallery_func",
    "get_scene_info",
    "get_logo_base64",
]



================================================
FILE: src/depth_anything_3/app/modules/event_handlers.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

"""
Event handling module for Depth Anything 3 Gradio app.

This module handles all event callbacks and user interactions.
"""

import os
import time
from glob import glob
from typing import Any, Dict, List, Optional, Tuple
import gradio as gr
import numpy as np
import torch

from depth_anything_3.app.modules.file_handlers import FileHandler
from depth_anything_3.app.modules.model_inference import ModelInference
from depth_anything_3.utils.memory import cleanup_cuda_memory
from depth_anything_3.app.modules.visualization import VisualizationHandler


class EventHandlers:
    """
    Handles all event callbacks and user interactions for the Gradio app.
    """

    def __init__(self):
        """Initialize the event handlers."""
        self.model_inference = ModelInference()
        self.file_handler = FileHandler()
        self.visualization_handler = VisualizationHandler()

    def clear_fields(self) -> None:
        """
        Clears the 3D viewer, the stored target_dir, and empties the gallery.
        """
        return None

    def update_log(self) -> str:
        """
        Display a quick log message while waiting.
        """
        return "Loading and Reconstructing..."

    def save_current_visualization(
        self,
        target_dir: str,
        save_percentage: float,
        show_cam: bool,
        filter_black_bg: bool,
        filter_white_bg: bool,
        processed_data: Optional[Dict],
        scene_name: str = "",
    ) -> str:
        """
        Save current visualization results to gallery with specified save percentage.

        Args:
            target_dir: Directory containing results
            save_percentage: Percentage of points to save (0-100)
            show_cam: Whether to show cameras
            filter_black_bg: Whether to filter black background
            filter_white_bg: Whether to filter white background
            processed_data: Processed data from reconstruction

        Returns:
            Status message
        """
        if not target_dir or target_dir == "None" or not os.path.isdir(target_dir):
            return "No reconstruction available. Please run 'Reconstruct' first."

        if processed_data is None:
            return "No processed data available. Please run 'Reconstruct' first."

        try:
            # Add debug information
            print("[DEBUG] save_current_visualization called with:")
            print(f"  target_dir: {target_dir}")
            print(f"  save_percentage: {save_percentage}")
            print(f"  show_cam: {show_cam}")
            print(f"  filter_black_bg: {filter_black_bg}")
            print(f"  filter_white_bg: {filter_white_bg}")
            print(f"  processed_data: {processed_data is not None}")

            # Import the gallery save function
            # Create gallery name with user input or auto-generated
            import datetime

            from .utils import save_to_gallery_func

            timestamp = datetime.datetime.now().strftime("%Y%m%d_%H%M%S")
            if scene_name and scene_name.strip():
                gallery_name = f"{scene_name.strip()}_{timestamp}_pct{save_percentage:.0f}"
            else:
                gallery_name = f"save_{timestamp}_pct{save_percentage:.0f}"

            print(f"[DEBUG] Saving to gallery with name: {gallery_name}")

            # Save entire process folder to gallery
            success, message = save_to_gallery_func(
                target_dir=target_dir, processed_data=processed_data, gallery_name=gallery_name
            )

            if success:
                print(f"[DEBUG] Gallery save completed successfully: {message}")
                return (
                    "Successfully saved to gallery!\n"
                    f"Gallery name: {gallery_name}\n"
                    f"Save percentage: {save_percentage}%\n"
                    f"Show cameras: {show_cam}\n"
                    f"Filter black bg: {filter_black_bg}\n"
                    f"Filter white bg: {filter_white_bg}\n\n"
                    f"{message}"
                )
            else:
                print(f"[DEBUG] Gallery save failed: {message}")
                return f"Failed to save to gallery: {message}"

        except Exception as e:
            return f"Error saving visualization: {str(e)}"

    def gradio_demo(
        self,
        target_dir: str,
        show_cam: bool = True,
        filter_black_bg: bool = False,
        filter_white_bg: bool = False,
        process_res_method: str = "upper_bound_resize",
        save_percentage: float = 30.0,
        num_max_points: int = 1_000_000,
        infer_gs: bool = False,
        ref_view_strategy: str = "saddle_balanced",
        gs_trj_mode: str = "extend",
        gs_video_quality: str = "high",
    ) -> Tuple[
        Optional[str],
        str,
        Optional[Dict],
        Optional[np.ndarray],
        Optional[np.ndarray],
        str,
        gr.Dropdown,
        Optional[str],  # gs video path
        gr.update,  # gs video visibility update
        gr.update,  # gs info visibility update
    ]:
        """
        Perform reconstruction using the already-created target_dir/images.

        Args:
            target_dir: Directory containing images
            show_cam: Whether to show camera
            filter_black_bg: Whether to filter black background
            filter_white_bg: Whether to filter white background
            process_res_method: Method for resizing input images
            save_percentage: Filter percentage for point cloud
            num_max_points: Maximum number of points
            infer_gs: Whether to infer 3D Gaussian Splatting
            ref_view_strategy: Reference view selection strategy

        Returns:
            Tuple of reconstruction results
        """
        if not os.path.isdir(target_dir) or target_dir == "None":
            return (
                None,
                "No valid target directory found. Please upload first.",
                None,
                None,
                None,
                "",
                None,
                None,
                gr.update(visible=False),  # gs_video
                gr.update(visible=True),  # gs_info
            )

        start_time = time.time()
        cleanup_cuda_memory()

        # Get image files for logging
        target_dir_images = os.path.join(target_dir, "images")
        all_files = (
            sorted(os.listdir(target_dir_images)) if os.path.isdir(target_dir_images) else []
        )

        print("Running DepthAnything3 model...")
        print(f"Reference view strategy: {ref_view_strategy}")

        with torch.no_grad():
            prediction, processed_data = self.model_inference.run_inference(
                target_dir,
                process_res_method=process_res_method,
                show_camera=show_cam,
                save_percentage=save_percentage,
                num_max_points=int(num_max_points * 1000),  # Convert K to actual count
                infer_gs=infer_gs,
                ref_view_strategy=ref_view_strategy,
                gs_trj_mode=gs_trj_mode,
                gs_video_quality=gs_video_quality,
            )

        # The GLB file is already generated by the API
        glbfile = os.path.join(target_dir, "scene.glb")

        # Handle 3DGS video based on infer_gs flag
        gsvideo_path = None
        gs_video_visible = False
        gs_info_visible = True

        if infer_gs:
            try:
                gsvideo_path = sorted(glob(os.path.join(target_dir, "gs_video", "*.mp4")))[-1]
                gs_video_visible = True
                gs_info_visible = False
            except IndexError:
                gsvideo_path = None
                print("3DGS video not found, but infer_gs was enabled")

        # Cleanup
        cleanup_cuda_memory()

        end_time = time.time()
        print(f"Total time: {end_time - start_time:.2f} seconds")
        log_msg = f"Reconstruction Success ({len(all_files)} frames). Waiting for visualization."

        # Populate visualization tabs with processed data
        depth_vis, measure_img, measure_depth_vis, measure_pts = (
            self.visualization_handler.populate_visualization_tabs(processed_data)
        )

        # Update view selectors based on available views
        depth_selector, measure_selector = self.visualization_handler.update_view_selectors(
            processed_data
        )

        return (
            glbfile,
            log_msg,
            processed_data,
            measure_img,  # measure_image
            measure_depth_vis,  # measure_depth_image
            "",  # measure_text (empty initially)
            measure_selector,  # measure_view_selector
            gsvideo_path,
            gr.update(visible=gs_video_visible),  # gs_video visibility
            gr.update(visible=gs_info_visible),  # gs_info visibility
        )

    def update_visualization(
        self,
        target_dir: str,
        show_cam: bool,
        is_example: str,
        filter_black_bg: bool = False,
        filter_white_bg: bool = False,
        process_res_method: str = "upper_bound_resize",
    ) -> Tuple[gr.update, str]:
        """
        Reload saved predictions from npz, create (or reuse) the GLB for new parameters,
        and return it for the 3D viewer.

        Args:
            target_dir: Directory containing results
            show_cam: Whether to show camera
            is_example: Whether this is an example scene
            filter_black_bg: Whether to filter black background
            filter_white_bg: Whether to filter white background
            process_res_method: Method for resizing input images

        Returns:
            Tuple of (glb_file, log_message)
        """
        if not target_dir or target_dir == "None" or not os.path.isdir(target_dir):
            return (
                gr.update(),
                "No reconstruction available. Please click the Reconstruct button first.",
            )

        # Check if GLB exists (could be cached example or reconstructed scene)
        glbfile = os.path.join(target_dir, "scene.glb")
        if os.path.exists(glbfile):
            return (
                glbfile,
                (
                    "Visualization loaded from cache."
                    if is_example == "True"
                    else "Visualization updated."
                ),
            )

        # If no GLB but it's an example that hasn't been reconstructed yet
        if is_example == "True":
            return (
                gr.update(),
                "No reconstruction available. Please click the Reconstruct button first.",
            )

        # For non-examples, check predictions.npz
        predictions_path = os.path.join(target_dir, "predictions.npz")
        if not os.path.exists(predictions_path):
            error_message = (
                f"No reconstruction available at {predictions_path}. "
                "Please run 'Reconstruct' first."
            )
            return gr.update(), error_message

        loaded = np.load(predictions_path, allow_pickle=True)
        predictions = {key: loaded[key] for key in loaded.keys()}  # noqa: F841

        return (
            glbfile,
            "Visualization updated.",
        )

    def handle_uploads(
        self,
        input_video: Optional[str],
        input_images: Optional[List],
        s_time_interval: float = 10.0,
    ) -> Tuple[Optional[str], Optional[str], Optional[List], Optional[str]]:
        """
        Handle file uploads and update gallery.

        Args:
            input_video: Path to input video file
            input_images: List of input image files
            s_time_interval: Sampling FPS (frames per second) for frame extraction

        Returns:
            Tuple of (reconstruction_output, target_dir, image_paths, log_message)
        """
        return self.file_handler.update_gallery_on_upload(
            input_video, input_images, s_time_interval
        )

    def load_example_scene(self, scene_name: str, examples_dir: str = None) -> Tuple[
        Optional[str],
        Optional[str],
        Optional[List],
        str,
        Optional[Dict],
        gr.Dropdown,
        Optional[str],
        gr.update,
        gr.update,
    ]:
        """
        Load a scene from examples directory.

        Args:
            scene_name: Name of the scene to load
            examples_dir: Path to examples directory (if None, uses workspace_dir/examples)

        Returns:
            Tuple of (reconstruction_output, target_dir, image_paths, log_message, processed_data, measure_view_selector, gs_video, gs_video_vis, gs_info_vis)  # noqa: E501
        """
        if examples_dir is None:
            # Get workspace directory from environment variable
            workspace_dir = os.environ.get("DA3_WORKSPACE_DIR", "gradio_workspace")
            examples_dir = os.path.join(workspace_dir, "examples")

        reconstruction_output, target_dir, image_paths, log_message = (
            self.file_handler.load_example_scene(scene_name, examples_dir)
        )

        # Try to load cached processed data if available
        processed_data = None
        measure_view_selector = gr.Dropdown(choices=["View 1"], value="View 1")
        gs_video_path = None
        gs_video_visible = False
        gs_info_visible = True

        if target_dir and target_dir != "None":
            predictions_path = os.path.join(target_dir, "predictions.npz")
            if os.path.exists(predictions_path):
                try:
                    # Load predictions from cache
                    loaded = np.load(predictions_path, allow_pickle=True)
                    predictions = {key: loaded[key] for key in loaded.keys()}

                    # Reconstruct processed_data structure
                    num_images = len(predictions.get("images", []))
                    processed_data = {}

                    for i in range(num_images):
                        processed_data[i] = {
                            "image": predictions["images"][i] if "images" in predictions else None,
                            "depth": predictions["depths"][i] if "depths" in predictions else None,
                            "depth_image": os.path.join(
                                target_dir, "depth_vis", f"{i:04d}.jpg"  # Fixed: use .jpg not .png
                            ),
                            "intrinsics": (
                                predictions["intrinsics"][i]
                                if "intrinsics" in predictions
                                and i < len(predictions["intrinsics"])
                                else None
                            ),
                            "mask": None,
                        }

                    # Update measure view selector
                    choices = [f"View {i + 1}" for i in range(num_images)]
                    measure_view_selector = gr.Dropdown(choices=choices, value=choices[0])

                except Exception as e:
                    print(f"Error loading cached data: {e}")

            # Check for cached 3DGS video
            gs_video_dir = os.path.join(target_dir, "gs_video")
            if os.path.exists(gs_video_dir):
                try:
                    from glob import glob

                    gs_videos = sorted(glob(os.path.join(gs_video_dir, "*.mp4")))
                    if gs_videos:
                        gs_video_path = gs_videos[-1]
                        gs_video_visible = True
                        gs_info_visible = False
                        print(f"Loaded cached 3DGS video: {gs_video_path}")
                except Exception as e:
                    print(f"Error loading cached 3DGS video: {e}")

        return (
            reconstruction_output,
            target_dir,
            image_paths,
            log_message,
            processed_data,
            measure_view_selector,
            gs_video_path,
            gr.update(visible=gs_video_visible),
            gr.update(visible=gs_info_visible),
        )

    def navigate_depth_view(
        self,
        processed_data: Optional[Dict[int, Dict[str, Any]]],
        current_selector: str,
        direction: int,
    ) -> Tuple[str, Optional[str]]:
        """
        Navigate depth view.

        Args:
            processed_data: Processed data dictionary
            current_selector: Current selector value
            direction: Direction to navigate

        Returns:
            Tuple of (new_selector_value, depth_vis)
        """
        return self.visualization_handler.navigate_depth_view(
            processed_data, current_selector, direction
        )

    def update_depth_view(
        self, processed_data: Optional[Dict[int, Dict[str, Any]]], view_index: int
    ) -> Optional[str]:
        """
        Update depth view for a specific view index.

        Args:
            processed_data: Processed data dictionary
            view_index: Index of the view to update

        Returns:
            Path to depth visualization image or None
        """
        return self.visualization_handler.update_depth_view(processed_data, view_index)

    def navigate_measure_view(
        self,
        processed_data: Optional[Dict[int, Dict[str, Any]]],
        current_selector: str,
        direction: int,
    ) -> Tuple[str, Optional[np.ndarray], Optional[np.ndarray], List]:
        """
        Navigate measure view.

        Args:
            processed_data: Processed data dictionary
            current_selector: Current selector value
            direction: Direction to navigate

        Returns:
            Tuple of (new_selector_value, measure_image, depth_right_half, measure_points)
        """
        return self.visualization_handler.navigate_measure_view(
            processed_data, current_selector, direction
        )

    def update_measure_view(
        self, processed_data: Optional[Dict[int, Dict[str, Any]]], view_index: int
    ) -> Tuple[Optional[np.ndarray], Optional[np.ndarray], List]:
        """
        Update measure view for a specific view index.

        Args:
            processed_data: Processed data dictionary
            view_index: Index of the view to update

        Returns:
            Tuple of (measure_image, depth_right_half, measure_points)
        """
        return self.visualization_handler.update_measure_view(processed_data, view_index)

    def measure(
        self,
        processed_data: Optional[Dict[int, Dict[str, Any]]],
        measure_points: List,
        current_view_selector: str,
        event: gr.SelectData,
    ) -> List:
        """
        Handle measurement on images.

        Args:
            processed_data: Processed data dictionary
            measure_points: List of current measure points
            current_view_selector: Current view selector value
            event: Gradio select event

        Returns:
            List of [image, depth_right_half, measure_points, text]
        """
        return self.visualization_handler.measure(
            processed_data, measure_points, current_view_selector, event
        )

    def select_first_frame(
        self, image_gallery: List, selected_index: int = 0
    ) -> Tuple[List, str, str]:
        """
        Select the first frame from the image gallery.

        Args:
            image_gallery: List of images in the gallery
            selected_index: Index of the selected image (default: 0)

        Returns:
            Tuple of (updated_image_gallery, log_message, selected_frame_path)
        """
        try:
            if not image_gallery or len(image_gallery) == 0:
                return image_gallery, "No images available to select as first frame.", ""

            # Handle None or invalid selected_index
            if (
                selected_index is None
                or selected_index < 0
                or selected_index >= len(image_gallery)
            ):
                selected_index = 0
                print(f"Invalid selected_index: {selected_index}, using default: 0")

            # Get the selected image based on index
            selected_image = image_gallery[selected_index]
            print(f"Selected image index: {selected_index}")
            print(f"Total images: {len(image_gallery)}")

            # Extract the file path from the selected image
            selected_frame_path = ""
            print(f"Selected image type: {type(selected_image)}")
            print(f"Selected image: {selected_image}")

            if isinstance(selected_image, tuple):
                # Gradio Gallery returns tuple (path, None)
                selected_frame_path = selected_image[0]
            elif isinstance(selected_image, str):
                selected_frame_path = selected_image
            elif hasattr(selected_image, "name"):
                selected_frame_path = selected_image.name
            elif isinstance(selected_image, dict):
                if "name" in selected_image:
                    selected_frame_path = selected_image["name"]
                elif "path" in selected_image:
                    selected_frame_path = selected_image["path"]
                elif "src" in selected_image:
                    selected_frame_path = selected_image["src"]
            else:
                # Try to convert to string
                selected_frame_path = str(selected_image)

            print(f"Extracted path: {selected_frame_path}")

            # Extract filename from the path for matching
            import os

            selected_filename = os.path.basename(selected_frame_path)
            print(f"Selected filename: {selected_filename}")

            # Move the selected image to the front
            updated_gallery = [selected_image] + [
                img for img in image_gallery if img != selected_image
            ]

            log_message = (
                f"Selected frame: {selected_filename}. "
                f"Moved to first position. Total frames: {len(updated_gallery)}"
            )
            return updated_gallery, log_message, selected_filename

        except Exception as e:
            print(f"Error selecting first frame: {e}")
            return image_gallery, f"Error selecting first frame: {e}", ""



================================================
FILE: src/depth_anything_3/app/modules/file_handlers.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

"""
File handling module for Depth Anything 3 Gradio app.

This module handles file uploads, video processing, and file operations.
"""

import os
import shutil
import time
from datetime import datetime
from typing import List, Optional, Tuple
import cv2
from PIL import Image
from pillow_heif import register_heif_opener

register_heif_opener()


class FileHandler:
    """
    Handles file uploads and processing for the Gradio app.
    """

    def __init__(self):
        """Initialize the file handler."""

    def handle_uploads(
        self,
        input_video: Optional[str],
        input_images: Optional[List],
        s_time_interval: float = 10.0,
    ) -> Tuple[str, List[str]]:
        """
        Create a new 'target_dir' + 'images' subfolder, and place user-uploaded
        images or extracted frames from video into it.

        Args:
            input_video: Path to input video file
            input_images: List of input image files
            s_time_interval: Sampling FPS (frames per second) for frame extraction

        Returns:
            Tuple of (target_dir, image_paths)
        """
        start_time = time.time()

        # Get workspace directory from environment variable or use default
        workspace_dir = os.environ.get("DA3_WORKSPACE_DIR", "gradio_workspace")
        if not os.path.exists(workspace_dir):
            os.makedirs(workspace_dir)

        # Create input_images subdirectory
        input_images_dir = os.path.join(workspace_dir, "input_images")
        if not os.path.exists(input_images_dir):
            os.makedirs(input_images_dir)

        # Create a unique folder name within input_images
        timestamp = datetime.now().strftime("%Y%m%d_%H%M%S_%f")
        target_dir = os.path.join(input_images_dir, f"session_{timestamp}")
        target_dir_images = os.path.join(target_dir, "images")

        # Clean up if somehow that folder already exists
        if os.path.exists(target_dir):
            shutil.rmtree(target_dir)
        os.makedirs(target_dir)
        os.makedirs(target_dir_images)

        image_paths = []

        # Handle images
        if input_images is not None:
            image_paths.extend(self._process_images(input_images, target_dir_images))

        # Handle video
        if input_video is not None:
            image_paths.extend(
                self._process_video(input_video, target_dir_images, s_time_interval)
            )

        # Sort final images for gallery
        image_paths = sorted(image_paths)

        end_time = time.time()
        print(f"Files copied to {target_dir_images}; took {end_time - start_time:.3f} seconds")
        return target_dir, image_paths

    def _process_images(self, input_images: List, target_dir_images: str) -> List[str]:
        """
        Process uploaded images.

        Args:
            input_images: List of input image files
            target_dir_images: Target directory for images

        Returns:
            List of processed image paths
        """
        image_paths = []

        for file_data in input_images:
            if isinstance(file_data, dict) and "name" in file_data:
                file_path = file_data["name"]
            else:
                file_path = file_data

            # Check if the file is a HEIC image
            file_ext = os.path.splitext(file_path)[1].lower()
            if file_ext in [".heic", ".heif"]:
                # Convert HEIC to JPEG for better gallery compatibility
                try:
                    with Image.open(file_path) as img:
                        # Convert to RGB if necessary (HEIC can have different color modes)
                        if img.mode not in ("RGB", "L"):
                            img = img.convert("RGB")

                        # Create JPEG filename
                        base_name = os.path.splitext(os.path.basename(file_path))[0]
                        dst_path = os.path.join(target_dir_images, f"{base_name}.jpg")

                        # Save as JPEG with high quality
                        img.save(dst_path, "JPEG", quality=95)
                        image_paths.append(dst_path)
                        print(
                            f"Converted HEIC to JPEG: {os.path.basename(file_path)} -> "
                            f"{os.path.basename(dst_path)}"
                        )
                except Exception as e:
                    print(f"Error converting HEIC file {file_path}: {e}")
                    # Fall back to copying as is
                    dst_path = os.path.join(target_dir_images, os.path.basename(file_path))
                    shutil.copy(file_path, dst_path)
                    image_paths.append(dst_path)
            else:
                # Regular image files - copy as is
                dst_path = os.path.join(target_dir_images, os.path.basename(file_path))
                shutil.copy(file_path, dst_path)
                image_paths.append(dst_path)

        return image_paths

    def _process_video(
        self, input_video: str, target_dir_images: str, s_time_interval: float
    ) -> List[str]:
        """
        Process video file and extract frames.

        Args:
            input_video: Path to input video file
            target_dir_images: Target directory for extracted frames
            s_time_interval: Sampling FPS (frames per second) for frame extraction

        Returns:
            List of extracted frame paths
        """
        image_paths = []

        if isinstance(input_video, dict) and "name" in input_video:
            video_path = input_video["name"]
        else:
            video_path = input_video

        vs = cv2.VideoCapture(video_path)
        fps = vs.get(cv2.CAP_PROP_FPS)
        frame_interval = max(1, int(fps / s_time_interval))  # Convert FPS to frame interval

        count = 0
        video_frame_num = 0
        while True:
            gotit, frame = vs.read()
            if not gotit:
                break
            count += 1
            if count % frame_interval == 0:
                image_path = os.path.join(target_dir_images, f"{video_frame_num:06}.png")
                cv2.imwrite(image_path, frame)
                image_paths.append(image_path)
                video_frame_num += 1

        return image_paths

    def update_gallery_on_upload(
        self,
        input_video: Optional[str],
        input_images: Optional[List],
        s_time_interval: float = 10.0,
    ) -> Tuple[Optional[str], Optional[str], Optional[List], Optional[str]]:
        """
        Handle file uploads and update gallery.

        Args:
            input_video: Path to input video file
            input_images: List of input image files
            s_time_interval: Sampling FPS (frames per second) for frame extraction

        Returns:
            Tuple of (reconstruction_output, target_dir, image_paths, log_message)
        """
        if not input_video and not input_images:
            return None, None, None, None

        target_dir, image_paths = self.handle_uploads(input_video, input_images, s_time_interval)
        return (
            None,
            target_dir,
            image_paths,
            "Upload complete. Click 'Reconstruct' to begin 3D processing.",
        )

    def load_example_scene(
        self, scene_name: str, examples_dir: str = "examples"
    ) -> Tuple[Optional[str], Optional[str], Optional[List], str]:
        """
        Load a scene from examples directory.

        Args:
            scene_name: Name of the scene to load
            examples_dir: Path to examples directory

        Returns:
            Tuple of (reconstruction_output, target_dir, image_paths, log_message)
        """
        from depth_anything_3.app.modules.utils import get_scene_info

        scenes = get_scene_info(examples_dir)

        # Find the selected scene
        selected_scene = None
        for scene in scenes:
            if scene["name"] == scene_name:
                selected_scene = scene
                break

        if selected_scene is None:
            return None, None, None, "Scene not found"

        # Use fixed directory name for examples (not timestamp-based)
        workspace_dir = os.environ.get("DA3_WORKSPACE_DIR", "gradio_workspace")
        input_images_dir = os.path.join(workspace_dir, "input_images")
        if not os.path.exists(input_images_dir):
            os.makedirs(input_images_dir)

        # Create a fixed folder name based on scene name
        target_dir = os.path.join(input_images_dir, f"example_{scene_name}")
        target_dir_images = os.path.join(target_dir, "images")

        # Check if already cached (GLB file exists)
        glb_path = os.path.join(target_dir, "scene.glb")
        is_cached = os.path.exists(glb_path)

        # Create directory if it doesn't exist
        if not os.path.exists(target_dir):
            os.makedirs(target_dir)
            os.makedirs(target_dir_images)

        # Copy images if directory is new or empty
        if not os.path.exists(target_dir_images) or len(os.listdir(target_dir_images)) == 0:
            os.makedirs(target_dir_images, exist_ok=True)
            image_paths = []
            for file_path in selected_scene["image_files"]:
                dst_path = os.path.join(target_dir_images, os.path.basename(file_path))
                shutil.copy(file_path, dst_path)
                image_paths.append(dst_path)
        else:
            # Use existing images
            image_paths = sorted(
                [
                    os.path.join(target_dir_images, f)
                    for f in os.listdir(target_dir_images)
                    if f.lower().endswith((".png", ".jpg", ".jpeg", ".bmp", ".tiff", ".tif"))
                ]
            )

        # Return cached GLB if available
        if is_cached:
            return (
                glb_path,  # Return cached reconstruction
                target_dir,  # Set target directory
                image_paths,  # Set gallery
                f"Loaded cached scene '{scene_name}' with {selected_scene['num_images']} images.",
            )
        else:
            return (
                None,  # No cached reconstruction
                target_dir,  # Set target directory
                image_paths,  # Set gallery
                (
                    f"Loaded scene '{scene_name}' with {selected_scene['num_images']} images. "
                    "Click 'Reconstruct' to begin 3D processing."
                ),
            )



================================================
FILE: src/depth_anything_3/app/modules/model_inference.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

"""
Model inference module for Depth Anything 3 Gradio app.

This module handles all model-related operations including inference,
data processing, and result preparation.
"""

import glob
import os
from typing import Any, Dict, Optional, Tuple
import numpy as np
import torch

from depth_anything_3.api import DepthAnything3
from depth_anything_3.utils.memory import cleanup_cuda_memory
from depth_anything_3.utils.export.glb import export_to_glb
from depth_anything_3.utils.export.gs import export_to_gs_video


class ModelInference:
    """
    Handles model inference and data processing for Depth Anything 3.
    """

    def __init__(self):
        """Initialize the model inference handler."""
        self.model = None

    def initialize_model(self, device: str = "cuda") -> None:
        """
        Initialize the DepthAnything3 model.

        Args:
            device: Device to load the model on
        """
        if self.model is None:
            # Get model directory from environment variable or use default
            model_dir = os.environ.get(
                "DA3_MODEL_DIR", "/dev/shm/da3_models/DA3HF-VITG-METRIC_VITL"
            )
            self.model = DepthAnything3.from_pretrained(model_dir)
            self.model = self.model.to(device)
        else:
            self.model = self.model.to(device)

        self.model.eval()

    def run_inference(
        self,
        target_dir: str,
        filter_black_bg: bool = False,
        filter_white_bg: bool = False,
        process_res_method: str = "upper_bound_resize",
        show_camera: bool = True,
        save_percentage: float = 30.0,
        num_max_points: int = 1_000_000,
        infer_gs: bool = False,
        ref_view_strategy: str = "saddle_balanced",
        gs_trj_mode: str = "extend",
        gs_video_quality: str = "high",
    ) -> Tuple[Any, Dict[int, Dict[str, Any]]]:
        """
        Run DepthAnything3 model inference on images.

        Args:
            target_dir: Directory containing images
            filter_black_bg: Whether to filter black background
            filter_white_bg: Whether to filter white background
            process_res_method: Method for resizing input images
            show_camera: Whether to show camera in 3D view
            save_percentage: Percentage of points to save (0-100)
            num_max_points: Maximum number of points in point cloud
            infer_gs: Whether to infer 3D Gaussian Splatting
            ref_view_strategy: Reference view selection strategy
            gs_trj_mode: Trajectory mode for 3DGS
            gs_video_quality: Video quality for 3DGS

        Returns:
            Tuple of (prediction, processed_data)
        """
        print(f"Processing images from {target_dir}")

        # Device check
        device = "cuda" if torch.cuda.is_available() else "cpu"
        device = torch.device(device)

        # Initialize model if needed
        self.initialize_model(device)

        # Get image paths
        print("Loading images...")
        image_folder_path = os.path.join(target_dir, "images")
        all_image_paths = sorted(glob.glob(os.path.join(image_folder_path, "*")))

        # Filter for image files
        image_extensions = [".jpg", ".jpeg", ".png", ".bmp", ".tiff", ".tif"]
        all_image_paths = [
            path
            for path in all_image_paths
            if any(path.lower().endswith(ext) for ext in image_extensions)
        ]

        print(f"Found {len(all_image_paths)} images")
        print(f"All image paths: {all_image_paths}")

        # Use sorted image order (reference view will be selected automatically)
        image_paths = all_image_paths
        print(f"Reference view selection strategy: {ref_view_strategy}")

        if len(image_paths) == 0:
            raise ValueError("No images found. Check your upload.")

        # Map UI options to actual method names
        method_mapping = {"high_res": "lower_bound_resize", "low_res": "upper_bound_resize"}
        actual_method = method_mapping.get(process_res_method, "upper_bound_crop")

        # Run model inference
        print(f"Running inference with method: {actual_method}")
        with torch.no_grad():
            prediction = self.model.inference(
                image_paths,
                export_dir=None,
                process_res_method=actual_method,
                infer_gs=infer_gs,
                ref_view_strategy=ref_view_strategy,
            )
        # num_max_points: int = 1_000_000,
        export_to_glb(
            prediction,
            filter_black_bg=filter_black_bg,
            filter_white_bg=filter_white_bg,
            export_dir=target_dir,
            show_cameras=show_camera,
            conf_thresh_percentile=save_percentage,
            num_max_points=int(num_max_points),
        )

        # export to gs video if needed
        if infer_gs:
            mode_mapping = {"extend": "extend", "smooth": "interpolate_smooth"}
            print(f"GS mode: {gs_trj_mode}; Backend mode: {mode_mapping[gs_trj_mode]}")
            export_to_gs_video(
                prediction,
                export_dir=target_dir,
                chunk_size=4,
                trj_mode=mode_mapping.get(gs_trj_mode, "extend"),
                enable_tqdm=True,
                vis_depth="hcat",
                video_quality=gs_video_quality,
            )

        # Save predictions.npz for caching metric depth data
        self._save_predictions_cache(target_dir, prediction)

        # Process results
        processed_data = self._process_results(target_dir, prediction, image_paths)

        # Clean up using centralized memory utilities for consistency with backend
        cleanup_cuda_memory()

        return prediction, processed_data

    def _save_predictions_cache(self, target_dir: str, prediction: Any) -> None:
        """
        Save predictions data to predictions.npz for caching.

        Args:
            target_dir: Directory to save the cache
            prediction: Model prediction object
        """
        try:
            output_file = os.path.join(target_dir, "predictions.npz")

            # Build save dict with prediction data
            save_dict = {}

            # Save processed images if available
            if prediction.processed_images is not None:
                save_dict["images"] = prediction.processed_images

            # Save depth data
            if prediction.depth is not None:
                save_dict["depths"] = np.round(prediction.depth, 6)

            # Save confidence if available
            if prediction.conf is not None:
                save_dict["conf"] = np.round(prediction.conf, 2)

            # Save camera parameters
            if prediction.extrinsics is not None:
                save_dict["extrinsics"] = prediction.extrinsics
            if prediction.intrinsics is not None:
                save_dict["intrinsics"] = prediction.intrinsics

            # Save to file
            np.savez_compressed(output_file, **save_dict)
            print(f"Saved predictions cache to: {output_file}")

        except Exception as e:
            print(f"Warning: Failed to save predictions cache: {e}")

    def _process_results(
        self, target_dir: str, prediction: Any, image_paths: list
    ) -> Dict[int, Dict[str, Any]]:
        """
        Process model results into structured data.

        Args:
            target_dir: Directory containing results
            prediction: Model prediction object
            image_paths: List of input image paths

        Returns:
            Dictionary containing processed data for each view
        """
        processed_data = {}

        # Read generated depth visualization files
        depth_vis_dir = os.path.join(target_dir, "depth_vis")

        if os.path.exists(depth_vis_dir):
            depth_files = sorted(glob.glob(os.path.join(depth_vis_dir, "*.jpg")))
            for i, depth_file in enumerate(depth_files):
                # Use processed images directly from API
                processed_image = None
                if prediction.processed_images is not None and i < len(
                    prediction.processed_images
                ):
                    processed_image = prediction.processed_images[i]

                processed_data[i] = {
                    "depth_image": depth_file,
                    "image": processed_image,
                    "original_image_path": image_paths[i] if i < len(image_paths) else None,
                    "depth": prediction.depth[i] if i < len(prediction.depth) else None,
                    "intrinsics": (
                        prediction.intrinsics[i]
                        if prediction.intrinsics is not None and i < len(prediction.intrinsics)
                        else None
                    ),
                    "mask": None,  # No mask information available
                }

        return processed_data

    # cleanup() removed: call cleanup_cuda_memory() directly where needed.



================================================
FILE: src/depth_anything_3/app/modules/ui_components.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

"""
UI components module for Depth Anything 3 Gradio app.

This module contains UI component definitions and layout functions.
"""

import os
from typing import Any, Dict, List, Tuple
import gradio as gr

from depth_anything_3.app.modules.utils import get_logo_base64, get_scene_info


class UIComponents:
    """
    Handles UI component creation and layout for the Gradio app.
    """

    def __init__(self):
        """Initialize the UI components handler."""

    def create_upload_section(self) -> Tuple[gr.Video, gr.Slider, gr.File, gr.Gallery]:
        """
        Create the upload section with video, images, and gallery components.

        Returns:
            A tuple of Gradio components: (input_video, s_time_interval, input_images, image_gallery).
        """
        input_video = gr.Video(label="Upload Video", interactive=True)
        s_time_interval = gr.Slider(
            minimum=0.1,
            maximum=60,
            value=10,
            step=0.1,
            label="Sampling FPS (Frames Per Second)",
            interactive=True,
            visible=True,
        )
        input_images = gr.File(file_count="multiple", label="Upload Images", interactive=True)
        image_gallery = gr.Gallery(
            label="Preview",
            columns=4,
            height="300px",
            show_download_button=True,
            object_fit="contain",
            preview=True,
            interactive=False,
        )

        return input_video, s_time_interval, input_images, image_gallery

    def create_3d_viewer_section(self) -> gr.Model3D:
        """
        Create the 3D viewer component.

        Returns:
            3D model viewer component
        """
        return gr.Model3D(
            height=520,
            zoom_speed=0.5,
            pan_speed=0.5,
            clear_color=[0.0, 0.0, 0.0, 0.0],
            key="persistent_3d_viewer",
            elem_id="reconstruction_3d_viewer",
        )

    def create_nvs_video(self) -> Tuple[gr.Video, gr.Markdown]:
        """
        Create the 3DGS rendered video display component and info message.

        Returns:
            Tuple of (video component, info message component)
        """
        with gr.Column():
            gs_info = gr.Markdown(
                (
                    "‼️ **3D Gaussian Splatting rendering is currently DISABLED.** <br><br><br>"
                    "To render novel views from 3DGS, "
                    "enable **Infer 3D Gaussian Splatting** below. <br>"
                    "Next, in **Visualization Options**, "
                    "*optionally* configure the **rendering trajectory** (default: smooth) "
                    "and **video quality** (default: low), "
                    "then click **Reconstruct**."
                ),
                visible=True,
                height=520,
            )
            gs_video = gr.Video(
                height=520,
                label="3DGS Rendered NVS Video (depth shown for reference only)",
                interactive=False,
                visible=False,
            )
        return gs_video, gs_info

    def create_depth_section(self) -> Tuple[gr.Button, gr.Dropdown, gr.Button, gr.Image]:
        """
        Create the depth visualization section.

        Returns:
            A tuple of (prev_depth_btn, depth_view_selector, next_depth_btn, depth_map)
        """
        with gr.Row(elem_classes=["navigation-row"]):
            prev_depth_btn = gr.Button("◀ Previous", size="sm", scale=1)
            depth_view_selector = gr.Dropdown(
                choices=["View 1"],
                value="View 1",
                label="Select View",
                scale=2,
                interactive=True,
                allow_custom_value=True,
            )
            next_depth_btn = gr.Button("Next ▶", size="sm", scale=1)
        depth_map = gr.Image(
            type="numpy",
            label="Colorized Depth Map",
            format="png",
            interactive=False,
        )

        return prev_depth_btn, depth_view_selector, next_depth_btn, depth_map

    def create_measure_section(
        self,
    ) -> Tuple[gr.Button, gr.Dropdown, gr.Button, gr.Image, gr.Image, gr.Markdown]:
        """
        Create the measurement section.

        Returns:
            A tuple of (prev_measure_btn, measure_view_selector, next_measure_btn, measure_image,
            measure_depth_image, measure_text)
        """
        from depth_anything_3.app.css_and_html import MEASURE_INSTRUCTIONS_HTML

        gr.Markdown(MEASURE_INSTRUCTIONS_HTML)
        with gr.Row(elem_classes=["navigation-row"]):
            prev_measure_btn = gr.Button("◀ Previous", size="sm", scale=1)
            measure_view_selector = gr.Dropdown(
                choices=["View 1"],
                value="View 1",
                label="Select View",
                scale=2,
                interactive=True,
                allow_custom_value=True,
            )
            next_measure_btn = gr.Button("Next ▶", size="sm", scale=1)
        with gr.Row():
            measure_image = gr.Image(
                type="numpy",
                show_label=False,
                format="webp",
                interactive=False,
                sources=[],
                label="RGB Image",
                scale=1,
                height=275,
            )
            measure_depth_image = gr.Image(
                type="numpy",
                show_label=False,
                format="webp",
                interactive=False,
                sources=[],
                label="Depth Visualization (Right Half)",
                scale=1,
                height=275,
            )
        gr.Markdown(
            "**Note:** Images have been adjusted to model processing size. "
            "Click two points on the RGB image to measure distance."
        )
        measure_text = gr.Markdown("")

        return (
            prev_measure_btn,
            measure_view_selector,
            next_measure_btn,
            measure_image,
            measure_depth_image,
            measure_text,
        )

    def create_inference_control_section(self) -> Tuple[gr.Dropdown, gr.Checkbox, gr.Dropdown]:
        """
        Create the inference control section (before inference).

        Returns:
            Tuple of (process_res_method_dropdown, infer_gs, ref_view_strategy)
        """
        with gr.Row():
            process_res_method_dropdown = gr.Dropdown(
                choices=["high_res", "low_res"],
                value="low_res",
                label="Image Processing Method",
                info="low_res for much more images",
                scale=1,
            )
            # Modify line 220, add color class
            infer_gs = gr.Checkbox(
                label="Infer 3D Gaussian Splatting",
                value=False,
                info=(
                    'Enable novel view rendering from 3DGS (<i class="fas fa-triangle-exclamation '
                    'fa-color-red"></i> requires extra processing time)'
                ),
                scale=1,
            )
            ref_view_strategy = gr.Dropdown(
                choices=["saddle_balanced", "saddle_sim_range", "first", "middle"],
                value="saddle_balanced",
                label="Reference View Strategy",
                info="Strategy for selecting reference view from multiple inputs",
                scale=1,
            )

        return (process_res_method_dropdown, infer_gs, ref_view_strategy)

    def create_display_control_section(
        self,
    ) -> Tuple[
        gr.Checkbox,
        gr.Checkbox,
        gr.Checkbox,
        gr.Slider,
        gr.Slider,
        gr.Dropdown,
        gr.Dropdown,
        gr.Button,
        gr.ClearButton,
    ]:
        """
        Create the display control section (options for visualization).

        Returns:
            Tuple of display control components including buttons
        """
        with gr.Column():
            # 3DGS options at the top
            with gr.Row():
                gs_trj_mode = gr.Dropdown(
                    choices=["smooth", "extend"],
                    value="smooth",
                    label=("Rendering trajectory for 3DGS viewpoints (requires n_views ≥ 2)"),
                    info=("'smooth' for view interpolation; 'extend' for longer trajectory"),
                    visible=False,  # initially hidden
                )
                gs_video_quality = gr.Dropdown(
                    choices=["low", "medium", "high"],
                    value="low",
                    label=("Video quality for 3DGS rendered outputs"),
                    info=("'low' for faster loading speed; 'high' for better visual quality"),
                    visible=False,  # initially hidden
                )

            # Reconstruct and Clear buttons (before Visualization Options)
            with gr.Row():
                submit_btn = gr.Button("Reconstruct", scale=1, variant="primary")
                clear_btn = gr.ClearButton(scale=1)

            gr.Markdown("### Visualization Options: (Click Reconstruct to update)")
            show_cam = gr.Checkbox(label="Show Camera", value=True)
            filter_black_bg = gr.Checkbox(label="Filter Black Background", value=False)
            filter_white_bg = gr.Checkbox(label="Filter White Background", value=False)
            save_percentage = gr.Slider(
                minimum=0,
                maximum=100,
                value=10,
                step=1,
                label="Filter Percentage",
                info="Confidence Threshold (%): Higher values filter more points.",
            )
            num_max_points = gr.Slider(
                minimum=1000,
                maximum=100000,
                value=1000,
                step=1000,
                label="Max Points (K points)",
                info="Maximum number of points to export to GLB (in thousands)",
            )

        return (
            show_cam,
            filter_black_bg,
            filter_white_bg,
            save_percentage,
            num_max_points,
            gs_trj_mode,
            gs_video_quality,
            submit_btn,
            clear_btn,
        )

    def create_control_section(
        self,
    ) -> Tuple[
        gr.Button,
        gr.ClearButton,
        gr.Dropdown,
        gr.Checkbox,
        gr.Checkbox,
        gr.Checkbox,
        gr.Checkbox,
        gr.Checkbox,
        gr.Dropdown,
        gr.Checkbox,
        gr.Textbox,
    ]:
        """
        Create the control section with buttons and options.

        Returns:
            Tuple of control components
        """
        with gr.Row():
            submit_btn = gr.Button("Reconstruct", scale=1, variant="primary")
            clear_btn = gr.ClearButton(
                scale=1,
            )

        with gr.Row():
            frame_filter = gr.Dropdown(
                choices=["All"], value="All", label="Show Points from Frame"
            )
            with gr.Column():
                gr.Markdown("### Visualization Option: (Click Reconstruct to update)")
                show_cam = gr.Checkbox(label="Show Camera", value=True)
                show_mesh = gr.Checkbox(label="Show Mesh", value=True)
                filter_black_bg = gr.Checkbox(label="Filter Black Background", value=False)
                filter_white_bg = gr.Checkbox(label="Filter White Background", value=False)
                gr.Markdown("### Reconstruction Options: (updated on next run)")
                apply_mask_checkbox = gr.Checkbox(
                    label="Apply mask for predicted ambiguous depth classes & edges",
                    value=True,
                )
                process_res_method_dropdown = gr.Dropdown(
                    choices=[
                        "upper_bound_resize",
                        "upper_bound_crop",
                        "lower_bound_resize",
                        "lower_bound_crop",
                    ],
                    value="upper_bound_resize",
                    label="Image Processing Method",
                    info="Method for resizing input images",
                )
                save_to_gallery_checkbox = gr.Checkbox(
                    label="Save to Gallery",
                    value=False,
                    info="Save current reconstruction results to gallery directory",
                )
                gallery_name_input = gr.Textbox(
                    label="Gallery Name",
                    placeholder="Enter a name for the gallery folder",
                    value="",
                    info="Leave empty for auto-generated name with timestamp",
                )

        return (
            submit_btn,
            clear_btn,
            frame_filter,
            show_cam,
            show_mesh,
            filter_black_bg,
            filter_white_bg,
            apply_mask_checkbox,
            process_res_method_dropdown,
            save_to_gallery_checkbox,
            gallery_name_input,
        )

    def create_example_scenes_section(self) -> List[Dict[str, Any]]:
        """
        Create the example scenes section.

        Returns:
            List of scene information dictionaries
        """
        # Get workspace directory from environment variable
        workspace_dir = os.environ.get("DA3_WORKSPACE_DIR", "gradio_workspace")
        examples_dir = os.path.join(workspace_dir, "examples")

        # Get scene information
        scenes = get_scene_info(examples_dir)

        return scenes

    def create_example_scene_grid(self, scenes: List[Dict[str, Any]]) -> List[gr.Image]:
        """
        Create the example scene grid.

        Args:
            scenes: List of scene information dictionaries

        Returns:
            List of scene image components
        """
        scene_components = []

        if scenes:
            for i in range(0, len(scenes), 4):  # Process 4 scenes per row
                with gr.Row():
                    for j in range(4):
                        scene_idx = i + j
                        if scene_idx < len(scenes):
                            scene = scenes[scene_idx]
                            with gr.Column(scale=1, elem_classes=["clickable-thumbnail"]):
                                # Clickable thumbnail
                                scene_img = gr.Image(
                                    value=scene["thumbnail"],
                                    height=150,
                                    interactive=False,
                                    show_label=False,
                                    elem_id=f"scene_thumb_{scene['name']}",
                                    sources=[],
                                )
                                scene_components.append(scene_img)

                                # Scene name and image count as text below thumbnail
                                gr.Markdown(
                                    f"**{scene['name']}** \n {scene['num_images']} images",
                                    elem_classes=["scene-info"],
                                )
                        else:
                            # Empty column to maintain grid structure
                            with gr.Column(scale=1):
                                pass

        return scene_components

    def create_header_section(self) -> gr.HTML:
        """
        Create the header section with logo and title.

        Returns:
            Header HTML component
        """
        from depth_anything_3.app.css_and_html import get_header_html

        return gr.HTML(get_header_html(get_logo_base64()))

    def create_description_section(self) -> gr.HTML:
        """
        Create the description section.

        Returns:
            Description HTML component
        """
        from depth_anything_3.app.css_and_html import get_description_html

        return gr.HTML(get_description_html())

    def create_acknowledgements_section(self) -> gr.HTML:
        """
        Create the acknowledgements section.

        Returns:
            Acknowledgements HTML component
        """
        from depth_anything_3.app.css_and_html import get_acknowledgements_html

        return gr.HTML(get_acknowledgements_html())



================================================
FILE: src/depth_anything_3/app/modules/utils.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

"""
Utility functions for Depth Anything 3 Gradio app.

This module contains helper functions for data processing, visualization,
and file operations.
"""


import json
import os
import shutil
from datetime import datetime
from typing import Any, Dict, List, Optional, Tuple
import numpy as np

def create_depth_visualization(depth: np.ndarray) -> Optional[np.ndarray]:
    """
    Create a colored depth visualization.

    Args:
        depth: Depth array

    Returns:
        Colored depth visualization or None
    """
    if depth is None:
        return None

    # Normalize depth to 0-1 range
    depth_min = depth[depth > 0].min() if (depth > 0).any() else 0
    depth_max = depth.max()

    if depth_max <= depth_min:
        return None

    # Normalize depth
    depth_norm = (depth - depth_min) / (depth_max - depth_min)
    depth_norm = np.clip(depth_norm, 0, 1)

    # Apply colormap (using matplotlib's viridis colormap)
    import matplotlib.cm as cm

    # Convert to colored image
    depth_colored = cm.viridis(depth_norm)[:, :, :3]  # Remove alpha channel
    depth_colored = (depth_colored * 255).astype(np.uint8)

    return depth_colored


def save_to_gallery_func(
    target_dir: str, processed_data: Dict[int, Dict[str, Any]], gallery_name: Optional[str] = None
) -> Tuple[bool, str]:
    """
    Save the current reconstruction results to the gallery directory.

    Args:
        target_dir: Source directory containing reconstruction results
        processed_data: Processed data dictionary
        gallery_name: Name for the gallery folder

    Returns:
        Tuple of (success, message)
    """
    try:
        # Get gallery directory from environment variable or use default
        gallery_dir = os.environ.get(
            "DA3_GALLERY_DIR",
            "workspace/gallery",
        )
        if not os.path.exists(gallery_dir):
            os.makedirs(gallery_dir)

        # Use provided name or create a unique name
        if gallery_name is None or gallery_name.strip() == "":
            timestamp = datetime.now().strftime("%Y%m%d_%H%M%S")
            gallery_name = f"reconstruction_{timestamp}"

        gallery_path = os.path.join(gallery_dir, gallery_name)

        # Check if directory already exists
        if os.path.exists(gallery_path):
            return False, f"Save failed: folder '{gallery_name}' already exists"

        # Create the gallery directory
        os.makedirs(gallery_path, exist_ok=True)

        # Copy GLB file
        glb_source = os.path.join(target_dir, "scene.glb")
        glb_dest = os.path.join(gallery_path, "scene.glb")
        if os.path.exists(glb_source):
            shutil.copy2(glb_source, glb_dest)

        # Copy depth visualization images
        depth_vis_dir = os.path.join(target_dir, "depth_vis")
        if os.path.exists(depth_vis_dir):
            gallery_depth_vis = os.path.join(gallery_path, "depth_vis")
            shutil.copytree(depth_vis_dir, gallery_depth_vis)

        # Copy original images
        images_source = os.path.join(target_dir, "images")
        if os.path.exists(images_source):
            gallery_images = os.path.join(gallery_path, "images")
            shutil.copytree(images_source, gallery_images)

        scene_preview_source = os.path.join(target_dir, "scene.jpg")
        scene_preview_dest = os.path.join(gallery_path, "scene.jpg")
        shutil.copy2(scene_preview_source, scene_preview_dest)

        # Save metadata
        metadata = {
            "timestamp": datetime.now().strftime("%Y%m%d_%H%M%S"),
            "num_images": len(processed_data) if processed_data else 0,
            "gallery_name": gallery_name,
        }

        with open(os.path.join(gallery_path, "metadata.json"), "w") as f:
            json.dump(metadata, f, indent=2)

        print(f"Saved reconstruction to gallery: {gallery_path}")
        return True, f"Save successful: saved to {gallery_path}"

    except Exception as e:
        print(f"Error saving to gallery: {e}")
        return False, f"Save failed: {str(e)}"


def get_scene_info(examples_dir: str) -> List[Dict[str, Any]]:
    """
    Get information about scenes in the examples directory.

    Args:
        examples_dir: Path to examples directory

    Returns:
        List of scene information dictionaries
    """
    import glob

    scenes = []
    if not os.path.exists(examples_dir):
        return scenes

    for scene_folder in sorted(os.listdir(examples_dir)):
        scene_path = os.path.join(examples_dir, scene_folder)
        if os.path.isdir(scene_path):
            # Find all image files in the scene folder
            image_extensions = ["*.jpg", "*.jpeg", "*.png", "*.bmp", "*.tiff", "*.tif"]
            image_files = []
            for ext in image_extensions:
                image_files.extend(glob.glob(os.path.join(scene_path, ext)))
                image_files.extend(glob.glob(os.path.join(scene_path, ext.upper())))

            if image_files:
                # Sort images and get the first one for thumbnail
                image_files = sorted(image_files)
                first_image = image_files[0]
                num_images = len(image_files)

                scenes.append(
                    {
                        "name": scene_folder,
                        "path": scene_path,
                        "thumbnail": first_image,
                        "num_images": num_images,
                        "image_files": image_files,
                    }
                )

    return scenes


# NOTE: cleanup was moved to a single canonical helper in
# `depth_anything_3.utils.memory.cleanup_cuda_memory`.
# Callers should import and call that directly instead of using this module.


def get_logo_base64() -> Optional[str]:
    """
    Convert WAI logo to base64 for embedding in HTML.

    Returns:
        Base64 encoded logo string or None
    """
    import base64

    logo_path = "examples/WAI-Logo/wai_logo.png"
    try:
        with open(logo_path, "rb") as img_file:
            img_data = img_file.read()
            base64_str = base64.b64encode(img_data).decode()
            return f"data:image/png;base64,{base64_str}"
    except FileNotFoundError:
        return None



================================================
FILE: src/depth_anything_3/app/modules/visualization.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

"""
Visualization module for Depth Anything 3 Gradio app.

This module handles visualization updates, navigation, and measurement functionality.
"""

import os
from typing import Any, Dict, List, Optional, Tuple
import cv2
import gradio as gr
import numpy as np


class VisualizationHandler:
    """
    Handles visualization updates and navigation for the Gradio app.
    """

    def __init__(self):
        """Initialize the visualization handler."""

    def update_view_selectors(
        self, processed_data: Optional[Dict[int, Dict[str, Any]]]
    ) -> Tuple[gr.Dropdown, gr.Dropdown]:
        """
        Update view selector dropdowns based on available views.

        Args:
            processed_data: Processed data dictionary

        Returns:
            Tuple of (depth_view_selector, measure_view_selector)
        """
        if processed_data is None or len(processed_data) == 0:
            choices = ["View 1"]
        else:
            num_views = len(processed_data)
            choices = [f"View {i + 1}" for i in range(num_views)]

        return (
            gr.Dropdown(choices=choices, value=choices[0]),  # depth_view_selector
            gr.Dropdown(choices=choices, value=choices[0]),  # measure_view_selector
        )

    def get_view_data_by_index(
        self, processed_data: Optional[Dict[int, Dict[str, Any]]], view_index: int
    ) -> Optional[Dict[str, Any]]:
        """
        Get view data by index, handling bounds.

        Args:
            processed_data: Processed data dictionary
            view_index: Index of the view to get

        Returns:
            View data dictionary or None
        """
        if processed_data is None or len(processed_data) == 0:
            return None

        view_keys = list(processed_data.keys())
        if view_index < 0 or view_index >= len(view_keys):
            view_index = 0

        return processed_data[view_keys[view_index]]

    def update_depth_view(
        self, processed_data: Optional[Dict[int, Dict[str, Any]]], view_index: int
    ) -> Optional[str]:
        """
        Update depth view for a specific view index.

        Args:
            processed_data: Processed data dictionary
            view_index: Index of the view to update

        Returns:
            Path to depth visualization image or None
        """
        view_data = self.get_view_data_by_index(processed_data, view_index)
        if view_data is None or view_data.get("depth_image") is None:
            return None

        # Return the depth visualization image directly
        return view_data["depth_image"]

    def navigate_depth_view(
        self,
        processed_data: Optional[Dict[int, Dict[str, Any]]],
        current_selector_value: str,
        direction: int,
    ) -> Tuple[str, Optional[str]]:
        """
        Navigate depth view (direction: -1 for previous, +1 for next).

        Args:
            processed_data: Processed data dictionary
            current_selector_value: Current selector value
            direction: Direction to navigate (-1 for previous, +1 for next)

        Returns:
            Tuple of (new_selector_value, depth_vis)
        """
        if processed_data is None or len(processed_data) == 0:
            return "View 1", None

        # Parse current view number
        try:
            current_view = int(current_selector_value.split()[1]) - 1
        except:  # noqa
            current_view = 0

        num_views = len(processed_data)
        new_view = (current_view + direction) % num_views

        new_selector_value = f"View {new_view + 1}"
        depth_vis = self.update_depth_view(processed_data, new_view)

        return new_selector_value, depth_vis

    def update_measure_view(
        self, processed_data: Optional[Dict[int, Dict[str, Any]]], view_index: int
    ) -> Tuple[Optional[np.ndarray], Optional[np.ndarray], List]:
        """
        Update measure view for a specific view index.

        Args:
            processed_data: Processed data dictionary
            view_index: Index of the view to update

        Returns:
            Tuple of (measure_image, depth_right_half, measure_points)
        """
        view_data = self.get_view_data_by_index(processed_data, view_index)
        if view_data is None:
            return None, None, []  # image, depth_right_half, measure_points

        # Get the processed (resized) image
        if "image" in view_data and view_data["image"] is not None:
            image = view_data["image"].copy()
        else:
            return None, None, []

        # Ensure image is in uint8 format
        if image.dtype != np.uint8:
            if image.max() <= 1.0:
                image = (image * 255).astype(np.uint8)
            else:
                image = image.astype(np.uint8)

        # Extract right half of the depth visualization (pure depth part)
        depth_image_path = view_data.get("depth_image", None)
        depth_right_half = None

        if depth_image_path and os.path.exists(depth_image_path):
            try:
                # Load the combined depth visualization image
                depth_combined = cv2.imread(depth_image_path)
                depth_combined = cv2.cvtColor(depth_combined, cv2.COLOR_BGR2RGB)
                if depth_combined is not None:
                    height, width = depth_combined.shape[:2]
                    # Extract right half (depth visualization part)
                    depth_right_half = depth_combined[:, width // 2 :]
            except Exception as e:
                print(f"Error extracting depth right half: {e}")

        return image, depth_right_half, []

    def navigate_measure_view(
        self,
        processed_data: Optional[Dict[int, Dict[str, Any]]],
        current_selector_value: str,
        direction: int,
    ) -> Tuple[str, Optional[np.ndarray], Optional[str], List]:
        """
        Navigate measure view (direction: -1 for previous, +1 for next).

        Args:
            processed_data: Processed data dictionary
            current_selector_value: Current selector value
            direction: Direction to navigate (-1 for previous, +1 for next)

        Returns:
            Tuple of (new_selector_value, measure_image, depth_image_path, measure_points)
        """
        if processed_data is None or len(processed_data) == 0:
            return "View 1", None, None, []

        # Parse current view number
        try:
            current_view = int(current_selector_value.split()[1]) - 1
        except:  # noqa
            current_view = 0

        num_views = len(processed_data)
        new_view = (current_view + direction) % num_views

        new_selector_value = f"View {new_view + 1}"
        measure_image, depth_right_half, measure_points = self.update_measure_view(
            processed_data, new_view
        )

        return new_selector_value, measure_image, depth_right_half, measure_points

    def populate_visualization_tabs(
        self, processed_data: Optional[Dict[int, Dict[str, Any]]]
    ) -> Tuple[Optional[str], Optional[np.ndarray], Optional[str], List]:
        """
        Populate the depth and measure tabs with processed data.

        Args:
            processed_data: Processed data dictionary

        Returns:
            Tuple of (depth_vis, measure_img, depth_image_path, measure_points)
        """
        if processed_data is None or len(processed_data) == 0:
            return None, None, None, []

        # Use update function to get depth visualization
        depth_vis = self.update_depth_view(processed_data, 0)
        measure_img, depth_right_half, _ = self.update_measure_view(processed_data, 0)

        return depth_vis, measure_img, depth_right_half, []

    def reset_measure(
        self, processed_data: Optional[Dict[int, Dict[str, Any]]]
    ) -> Tuple[Optional[np.ndarray], List, str]:
        """
        Reset measure points.

        Args:
            processed_data: Processed data dictionary

        Returns:
            Tuple of (image, measure_points, text)
        """
        if processed_data is None or len(processed_data) == 0:
            return None, [], ""

        # Return the first view image
        first_view = list(processed_data.values())[0]
        return first_view["image"], [], ""

    def measure(
        self,
        processed_data: Optional[Dict[int, Dict[str, Any]]],
        measure_points: List,
        current_view_selector: str,
        event: gr.SelectData,
    ) -> List:
        """
        Handle measurement on images.

        Args:
            processed_data: Processed data dictionary
            measure_points: List of current measure points
            current_view_selector: Current view selector value
            event: Gradio select event

        Returns:
            List of [image, depth_right_half, measure_points, text]
        """
        try:
            print(f"Measure function called with selector: {current_view_selector}")

            if processed_data is None or len(processed_data) == 0:
                return [None, [], "No data available"]

            # Use the currently selected view instead of always using the first view
            try:
                current_view_index = int(current_view_selector.split()[1]) - 1
            except:  # noqa
                current_view_index = 0

            print(f"Using view index: {current_view_index}")

            # Get view data safely
            if current_view_index < 0 or current_view_index >= len(processed_data):
                current_view_index = 0

            view_keys = list(processed_data.keys())
            current_view = processed_data[view_keys[current_view_index]]

            if current_view is None:
                return [None, [], "No view data available"]

            point2d = event.index[0], event.index[1]
            print(f"Clicked point: {point2d}")

            measure_points.append(point2d)

            # Get image and depth visualization
            image, depth_right_half, _ = self.update_measure_view(
                processed_data, current_view_index
            )
            if image is None:
                return [None, [], "No image available"]

            image = image.copy()

            # Ensure image is in uint8 format for proper cv2 operations
            try:
                if image.dtype != np.uint8:
                    if image.max() <= 1.0:
                        # Image is in [0, 1] range, convert to [0, 255]
                        image = (image * 255).astype(np.uint8)
                    else:
                        # Image is already in [0, 255] range
                        image = image.astype(np.uint8)
            except Exception as e:
                print(f"Image conversion error: {e}")
                return [None, [], f"Image conversion error: {e}"]

            # Draw circles for points
            try:
                for p in measure_points:
                    if 0 <= p[0] < image.shape[1] and 0 <= p[1] < image.shape[0]:
                        image = cv2.circle(image, p, radius=5, color=(255, 0, 0), thickness=2)
            except Exception as e:
                print(f"Drawing error: {e}")
                return [None, [], f"Drawing error: {e}"]

            # Get depth information from processed_data
            depth_text = ""
            try:
                for i, p in enumerate(measure_points):
                    if (
                        current_view["depth"] is not None
                        and 0 <= p[1] < current_view["depth"].shape[0]
                        and 0 <= p[0] < current_view["depth"].shape[1]
                    ):
                        d = current_view["depth"][p[1], p[0]]
                        depth_text += f"- **P{i + 1} depth: {d:.2f}m**\n"
                    else:
                        depth_text += f"- **P{i + 1}: Click position ({p[0]}, {p[1]}) - No depth information**\n"  # noqa: E501
            except Exception as e:
                print(f"Depth text error: {e}")
                depth_text = f"Error computing depth: {e}\n"

            if len(measure_points) == 2:
                try:
                    point1, point2 = measure_points
                    # Draw line
                    if (
                        0 <= point1[0] < image.shape[1]
                        and 0 <= point1[1] < image.shape[0]
                        and 0 <= point2[0] < image.shape[1]
                        and 0 <= point2[1] < image.shape[0]
                    ):
                        image = cv2.line(image, point1, point2, color=(255, 0, 0), thickness=2)

                    # Compute 3D distance using depth information and camera intrinsics
                    distance_text = "- **Distance: Unable to calculate 3D distance**"
                    if (
                        current_view["depth"] is not None
                        and 0 <= point1[1] < current_view["depth"].shape[0]
                        and 0 <= point1[0] < current_view["depth"].shape[1]
                        and 0 <= point2[1] < current_view["depth"].shape[0]
                        and 0 <= point2[0] < current_view["depth"].shape[1]
                    ):
                        try:
                            # Get depth values at the two points
                            d1 = current_view["depth"][point1[1], point1[0]]
                            d2 = current_view["depth"][point2[1], point2[0]]

                            # Convert 2D pixel coordinates to 3D world coordinates
                            if current_view["intrinsics"] is not None:
                                # Get camera intrinsics
                                K = current_view["intrinsics"]  # 3x3 intrinsic matrix
                                fx, fy = K[0, 0], K[1, 1]  # focal lengths
                                cx, cy = K[0, 2], K[1, 2]  # principal point

                                # Convert pixel coordinates to normalized camera coordinates
                                # Point 1: (u1, v1) -> (x1, y1, z1)
                                u1, v1 = point1[0], point1[1]
                                x1 = (u1 - cx) * d1 / fx
                                y1 = (v1 - cy) * d1 / fy
                                z1 = d1

                                # Point 2: (u2, v2) -> (x2, y2, z2)
                                u2, v2 = point2[0], point2[1]
                                x2 = (u2 - cx) * d2 / fx
                                y2 = (v2 - cy) * d2 / fy
                                z2 = d2

                                # Calculate 3D Euclidean distance
                                p1_3d = np.array([x1, y1, z1])
                                p2_3d = np.array([x2, y2, z2])
                                distance_3d = np.linalg.norm(p1_3d - p2_3d)

                                distance_text = f"- **Distance: {distance_3d:.2f}m**"
                            else:
                                # Fallback to simplified calculation if no intrinsics
                                pixel_distance = np.sqrt(
                                    (point1[0] - point2[0]) ** 2 + (point1[1] - point2[1]) ** 2
                                )
                                avg_depth = (d1 + d2) / 2
                                scale_factor = avg_depth / 1000  # Rough scaling factor
                                estimated_3d_distance = pixel_distance * scale_factor
                                distance_text = f"- **Distance: {estimated_3d_distance:.2f}m (estimated, no intrinsics)**"  # noqa: E501

                        except Exception as e:
                            print(f"Distance computation error: {e}")
                            distance_text = f"- **Distance computation error: {e}**"

                    measure_points = []
                    text = depth_text + distance_text
                    print(f"Measurement complete: {text}")
                    return [image, depth_right_half, measure_points, text]
                except Exception as e:
                    print(f"Final measurement error: {e}")
                    return [None, [], f"Measurement error: {e}"]
            else:
                print(f"Single point measurement: {depth_text}")
                return [image, depth_right_half, measure_points, depth_text]

        except Exception as e:
            print(f"Overall measure function error: {e}")
            return [None, [], f"Measure function error: {e}"]



================================================
FILE: src/depth_anything_3/model/__init__.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

from depth_anything_3.model.da3 import DepthAnything3Net, NestedDepthAnything3Net

__export__ = [
    NestedDepthAnything3Net,
    DepthAnything3Net,
]



================================================
FILE: src/depth_anything_3/model/cam_dec.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

import torch
import torch.nn as nn


class CameraDec(nn.Module):
    def __init__(self, dim_in=1536):
        super().__init__()
        output_dim = dim_in
        self.backbone = nn.Sequential(
            nn.Linear(output_dim, output_dim),
            nn.ReLU(),
            nn.Linear(output_dim, output_dim),
            nn.ReLU(),
        )
        self.fc_t = nn.Linear(output_dim, 3)
        self.fc_qvec = nn.Linear(output_dim, 4)
        self.fc_fov = nn.Sequential(nn.Linear(output_dim, 2), nn.ReLU())

    def forward(self, feat, camera_encoding=None, *args, **kwargs):
        B, N = feat.shape[:2]
        feat = feat.reshape(B * N, -1)
        feat = self.backbone(feat)
        out_t = self.fc_t(feat.float()).reshape(B, N, 3)
        if camera_encoding is None:
            out_qvec = self.fc_qvec(feat.float()).reshape(B, N, 4)
            out_fov = self.fc_fov(feat.float()).reshape(B, N, 2)
        else:
            out_qvec = camera_encoding[..., 3:7]
            out_fov = camera_encoding[..., -2:]
        pose_enc = torch.cat([out_t, out_qvec, out_fov], dim=-1)
        return pose_enc



================================================
FILE: src/depth_anything_3/model/cam_enc.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

import torch.nn as nn

from depth_anything_3.model.utils.attention import Mlp
from depth_anything_3.model.utils.block import Block
from depth_anything_3.model.utils.transform import extri_intri_to_pose_encoding
from depth_anything_3.utils.geometry import affine_inverse


class CameraEnc(nn.Module):
    """
    CameraHead predicts camera parameters from token representations using iterative refinement.

    It applies a series of transformer blocks (the "trunk") to dedicated camera tokens.
    """

    def __init__(
        self,
        dim_out: int = 1024,
        dim_in: int = 9,
        trunk_depth: int = 4,
        target_dim: int = 9,
        num_heads: int = 16,
        mlp_ratio: int = 4,
        init_values: float = 0.01,
        **kwargs,
    ):
        super().__init__()
        self.target_dim = target_dim
        self.trunk_depth = trunk_depth
        self.trunk = nn.Sequential(
            *[
                Block(
                    dim=dim_out,
                    num_heads=num_heads,
                    mlp_ratio=mlp_ratio,
                    init_values=init_values,
                )
                for _ in range(trunk_depth)
            ]
        )
        self.token_norm = nn.LayerNorm(dim_out)
        self.trunk_norm = nn.LayerNorm(dim_out)
        self.pose_branch = Mlp(
            in_features=dim_in,
            hidden_features=dim_out // 2,
            out_features=dim_out,
            drop=0,
        )

    def forward(
        self,
        ext,
        ixt,
        image_size,
    ) -> tuple:
        c2ws = affine_inverse(ext)
        pose_encoding = extri_intri_to_pose_encoding(
            c2ws,
            ixt,
            image_size,
        )
        pose_tokens = self.pose_branch(pose_encoding)
        pose_tokens = self.token_norm(pose_tokens)
        pose_tokens = self.trunk(pose_tokens)
        pose_tokens = self.trunk_norm(pose_tokens)
        return pose_tokens



================================================
FILE: src/depth_anything_3/model/da3.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

from __future__ import annotations

import torch
import torch.nn as nn
from addict import Dict
from omegaconf import DictConfig, OmegaConf

from depth_anything_3.cfg import create_object
from depth_anything_3.model.utils.transform import pose_encoding_to_extri_intri
from depth_anything_3.utils.alignment import (
    apply_metric_scaling,
    compute_alignment_mask,
    compute_sky_mask,
    least_squares_scale_scalar,
    sample_tensor_for_quantile,
    set_sky_regions_to_max_depth,
)
from depth_anything_3.utils.geometry import affine_inverse, as_homogeneous, map_pdf_to_opacity
from depth_anything_3.utils.ray_utils import get_extrinsic_from_camray


def _wrap_cfg(cfg_obj):
    return OmegaConf.create(cfg_obj)


class DepthAnything3Net(nn.Module):
    """
    Depth Anything 3 network for depth estimation and camera pose estimation.

    This network consists of:
    - Backbone: DinoV2 feature extractor
    - Head: DPT or DualDPT for depth prediction
    - Optional camera decoders for pose estimation
    - Optional GSDPT for 3DGS prediction

    Args:
        preset: Configuration preset containing network dimensions and settings

    Returns:
        Dictionary containing:
        - depth: Predicted depth map (B, H, W)
        - depth_conf: Depth confidence map (B, H, W)
        - extrinsics: Camera extrinsics (B, N, 4, 4)
        - intrinsics: Camera intrinsics (B, N, 3, 3)
        - gaussians: 3D Gaussian Splats (world space), type: model.gs_adapter.Gaussians
        - aux: Auxiliary features for specified layers
    """

    # Patch size for feature extraction
    PATCH_SIZE = 14

    def __init__(self, net, head, cam_dec=None, cam_enc=None, gs_head=None, gs_adapter=None):
        """
        Initialize DepthAnything3Net with given yaml-initialized configuration.
        """
        super().__init__()
        self.backbone = net if isinstance(net, nn.Module) else create_object(_wrap_cfg(net))
        self.head = head if isinstance(head, nn.Module) else create_object(_wrap_cfg(head))
        self.cam_dec, self.cam_enc = None, None
        if cam_dec is not None:
            self.cam_dec = (
                cam_dec if isinstance(cam_dec, nn.Module) else create_object(_wrap_cfg(cam_dec))
            )
            self.cam_enc = (
                cam_enc if isinstance(cam_enc, nn.Module) else create_object(_wrap_cfg(cam_enc))
            )
        self.gs_adapter, self.gs_head = None, None
        if gs_head is not None and gs_adapter is not None:
            self.gs_adapter = (
                gs_adapter
                if isinstance(gs_adapter, nn.Module)
                else create_object(_wrap_cfg(gs_adapter))
            )
            gs_out_dim = self.gs_adapter.d_in + 1
            if isinstance(gs_head, nn.Module):
                assert (
                    gs_head.out_dim == gs_out_dim
                ), f"gs_head.out_dim should be {gs_out_dim}, got {gs_head.out_dim}"
                self.gs_head = gs_head
            else:
                assert (
                    gs_head["output_dim"] == gs_out_dim
                ), f"gs_head output_dim should set to {gs_out_dim}, got {gs_head['output_dim']}"
                self.gs_head = create_object(_wrap_cfg(gs_head))

    def forward(
        self,
        x: torch.Tensor,
        extrinsics: torch.Tensor | None = None,
        intrinsics: torch.Tensor | None = None,
        export_feat_layers: list[int] | None = [],
        infer_gs: bool = False,
        use_ray_pose: bool = False,
        ref_view_strategy: str = "saddle_balanced",
    ) -> Dict[str, torch.Tensor]:
        """
        Forward pass through the network.

        Args:
            x: Input images (B, N, 3, H, W)
            extrinsics: Camera extrinsics (B, N, 4, 4) 
            intrinsics: Camera intrinsics (B, N, 3, 3) 
            feat_layers: List of layer indices to extract features from
            infer_gs: Enable Gaussian Splatting branch
            use_ray_pose: Use ray-based pose estimation
            ref_view_strategy: Strategy for selecting reference view

        Returns:
            Dictionary containing predictions and auxiliary features
        """
        # Extract features using backbone
        if extrinsics is not None:
            with torch.autocast(device_type=x.device.type, enabled=False):
                cam_token = self.cam_enc(extrinsics, intrinsics, x.shape[-2:])
        else:
            cam_token = None

        feats, aux_feats = self.backbone(
            x, cam_token=cam_token, export_feat_layers=export_feat_layers, ref_view_strategy=ref_view_strategy
        )
        # feats = [[item for item in feat] for feat in feats]
        H, W = x.shape[-2], x.shape[-1]

        # Process features through depth head
        with torch.autocast(device_type=x.device.type, enabled=False):
            output = self._process_depth_head(feats, H, W)
            if use_ray_pose:
                output = self._process_ray_pose_estimation(output, H, W)
            else:
                output = self._process_camera_estimation(feats, H, W, output)
            if infer_gs:
                output = self._process_gs_head(feats, H, W, output, x, extrinsics, intrinsics)
        
        output = self._process_mono_sky_estimation(output)    

        # Extract auxiliary features if requested
        output.aux = self._extract_auxiliary_features(aux_feats, export_feat_layers, H, W)

        return output

    def _process_mono_sky_estimation(
        self, output: Dict[str, torch.Tensor]
    ) -> Dict[str, torch.Tensor]:
        """Process mono sky estimation."""
        if "sky" not in output:
            return output
        non_sky_mask = compute_sky_mask(output.sky, threshold=0.3)
        if non_sky_mask.sum() <= 10:
            return output
        if (~non_sky_mask).sum() <= 10:
            return output
        
        non_sky_depth = output.depth[non_sky_mask]
        if non_sky_depth.numel() > 100000:
            idx = torch.randint(0, non_sky_depth.numel(), (100000,), device=non_sky_depth.device)
            sampled_depth = non_sky_depth[idx]
        else:
            sampled_depth = non_sky_depth
        non_sky_max = torch.quantile(sampled_depth, 0.99)

        # Set sky regions to maximum depth and high confidence
        output.depth, _ = set_sky_regions_to_max_depth(
            output.depth, None, non_sky_mask, max_depth=non_sky_max
        )
        return output

    def _process_ray_pose_estimation(
        self, output: Dict[str, torch.Tensor], height: int, width: int
    ) -> Dict[str, torch.Tensor]:
        """Process ray pose estimation if ray pose decoder is available."""
        if "ray" in output and "ray_conf" in output:
            pred_extrinsic, pred_focal_lengths, pred_principal_points = get_extrinsic_from_camray(
                output.ray,
                output.ray_conf,
                output.ray.shape[-3],
                output.ray.shape[-2],
            )
            pred_extrinsic = affine_inverse(pred_extrinsic) # w2c -> c2w
            pred_extrinsic = pred_extrinsic[:, :, :3, :]
            pred_intrinsic = torch.eye(3, 3)[None, None].repeat(pred_extrinsic.shape[0], pred_extrinsic.shape[1], 1, 1).clone().to(pred_extrinsic.device)
            pred_intrinsic[:, :, 0, 0] = pred_focal_lengths[:, :, 0] / 2 * width
            pred_intrinsic[:, :, 1, 1] = pred_focal_lengths[:, :, 1] / 2 * height
            pred_intrinsic[:, :, 0, 2] = pred_principal_points[:, :, 0] * width * 0.5
            pred_intrinsic[:, :, 1, 2] = pred_principal_points[:, :, 1] * height * 0.5
            del output.ray
            del output.ray_conf
            output.extrinsics = pred_extrinsic
            output.intrinsics = pred_intrinsic
        return output

    def _process_depth_head(
        self, feats: list[torch.Tensor], H: int, W: int
    ) -> Dict[str, torch.Tensor]:
        """Process features through the depth prediction head."""
        return self.head(feats, H, W, patch_start_idx=0)

    def _process_camera_estimation(
        self, feats: list[torch.Tensor], H: int, W: int, output: Dict[str, torch.Tensor]
    ) -> Dict[str, torch.Tensor]:
        """Process camera pose estimation if camera decoder is available."""
        if self.cam_dec is not None:
            pose_enc = self.cam_dec(feats[-1][1])
            # Remove ray information as it's not needed for pose estimation
            if "ray" in output:
                del output.ray
            if "ray_conf" in output:
                del output.ray_conf

            # Convert pose encoding to extrinsics and intrinsics
            c2w, ixt = pose_encoding_to_extri_intri(pose_enc, (H, W))
            output.extrinsics = affine_inverse(c2w)
            output.intrinsics = ixt

        return output

    def _process_gs_head(
        self,
        feats: list[torch.Tensor],
        H: int,
        W: int,
        output: Dict[str, torch.Tensor],
        in_images: torch.Tensor,
        extrinsics: torch.Tensor | None = None,
        intrinsics: torch.Tensor | None = None,
    ) -> Dict[str, torch.Tensor]:
        """Process 3DGS parameters estimation if 3DGS head is available."""
        if self.gs_head is None or self.gs_adapter is None:
            return output
        assert output.get("depth", None) is not None, "must provide MV depth for the GS head."

        # The depth is defined in the DA3 model's camera space,
        # so even with provided GT camera poses,
        # we instead use the predicted camera poses for better alignment.
        ctx_extr = output.get("extrinsics", None)
        ctx_intr = output.get("intrinsics", None)
        assert (
            ctx_extr is not None and ctx_intr is not None
        ), "must process camera info first if GT is not available"

        gt_extr = extrinsics
        # homo the extr if needed
        ctx_extr = as_homogeneous(ctx_extr)
        if gt_extr is not None:
            gt_extr = as_homogeneous(gt_extr)

        # forward through the gs_dpt head to get 'camera space' parameters
        gs_outs = self.gs_head(
            feats=feats,
            H=H,
            W=W,
            patch_start_idx=0,
            images=in_images,
        )
        raw_gaussians = gs_outs.raw_gs
        densities = gs_outs.raw_gs_conf

        # convert to 'world space' 3DGS parameters; ready to export and render
        # gt_extr could be None, and will be used to align the pose scale if available
        gs_world = self.gs_adapter(
            extrinsics=ctx_extr,
            intrinsics=ctx_intr,
            depths=output.depth,
            opacities=map_pdf_to_opacity(densities),
            raw_gaussians=raw_gaussians,
            image_shape=(H, W),
            gt_extrinsics=gt_extr,
        )
        output.gaussians = gs_world

        return output

    def _extract_auxiliary_features(
        self, feats: list[torch.Tensor], feat_layers: list[int], H: int, W: int
    ) -> Dict[str, torch.Tensor]:
        """Extract auxiliary features from specified layers."""
        aux_features = Dict()
        assert len(feats) == len(feat_layers)
        for feat, feat_layer in zip(feats, feat_layers):
            # Reshape features to spatial dimensions
            feat_reshaped = feat.reshape(
                [
                    feat.shape[0],
                    feat.shape[1],
                    H // self.PATCH_SIZE,
                    W // self.PATCH_SIZE,
                    feat.shape[-1],
                ]
            )
            aux_features[f"feat_layer_{feat_layer}"] = feat_reshaped

        return aux_features


class NestedDepthAnything3Net(nn.Module):
    """
    Nested Depth Anything 3 network with metric scaling capabilities.

    This network combines two DepthAnything3Net branches:
    - Main branch: Standard depth estimation
    - Metric branch: Metric depth estimation for scaling alignment

    The network performs depth alignment using least squares scaling
    and handles sky region masking for improved depth estimation.

    Args:
        preset: Configuration for the main depth estimation branch
        second_preset: Configuration for the metric depth branch
    """

    def __init__(self, anyview: DictConfig, metric: DictConfig):
        """
        Initialize NestedDepthAnything3Net with two branches.

        Args:
            preset: Configuration for main depth estimation branch
            second_preset: Configuration for metric depth branch
        """
        super().__init__()
        self.da3 = create_object(anyview)
        self.da3_metric = create_object(metric)

    def forward(
        self,
        x: torch.Tensor,
        extrinsics: torch.Tensor | None = None,
        intrinsics: torch.Tensor | None = None,
        export_feat_layers: list[int] | None = [],
        infer_gs: bool = False,
        use_ray_pose: bool = False,
        ref_view_strategy: str = "saddle_balanced",
    ) -> Dict[str, torch.Tensor]:
        """
        Forward pass through both branches with metric scaling alignment.

        Args:
            x: Input images (B, N, 3, H, W)
            extrinsics: Camera extrinsics (B, N, 4, 4) - unused
            intrinsics: Camera intrinsics (B, N, 3, 3) - unused
            feat_layers: List of layer indices to extract features from
            infer_gs: Enable Gaussian Splatting branch
            use_ray_pose: Use ray-based pose estimation
            ref_view_strategy: Strategy for selecting reference view

        Returns:
            Dictionary containing aligned depth predictions and camera parameters
        """
        # Get predictions from both branches
        output = self.da3(
            x, extrinsics, intrinsics, export_feat_layers=export_feat_layers, infer_gs=infer_gs, use_ray_pose=use_ray_pose, ref_view_strategy=ref_view_strategy
        )
        metric_output = self.da3_metric(x)

        # Apply metric scaling and alignment
        output = self._apply_metric_scaling(output, metric_output)
        output = self._apply_depth_alignment(output, metric_output)
        output = self._handle_sky_regions(output, metric_output)

        return output

    def _apply_metric_scaling(
        self, output: Dict[str, torch.Tensor], metric_output: Dict[str, torch.Tensor]
    ) -> Dict[str, torch.Tensor]:
        """Apply metric scaling to the metric depth output."""
        # Scale metric depth based on camera intrinsics
        metric_output.depth = apply_metric_scaling(
            metric_output.depth,
            output.intrinsics,
        )
        return output

    def _apply_depth_alignment(
        self, output: Dict[str, torch.Tensor], metric_output: Dict[str, torch.Tensor]
    ) -> Dict[str, torch.Tensor]:
        """Apply depth alignment using least squares scaling."""
        # Compute non-sky mask
        non_sky_mask = compute_sky_mask(metric_output.sky, threshold=0.3)

        # Ensure we have enough non-sky pixels
        assert non_sky_mask.sum() > 10, "Insufficient non-sky pixels for alignment"

        # Sample depth confidence for quantile computation
        depth_conf_ns = output.depth_conf[non_sky_mask]
        depth_conf_sampled = sample_tensor_for_quantile(depth_conf_ns, max_samples=100000)
        median_conf = torch.quantile(depth_conf_sampled, 0.5)

        # Compute alignment mask
        align_mask = compute_alignment_mask(
            output.depth_conf, non_sky_mask, output.depth, metric_output.depth, median_conf
        )

        # Compute scale factor using least squares
        valid_depth = output.depth[align_mask]
        valid_metric_depth = metric_output.depth[align_mask]
        scale_factor = least_squares_scale_scalar(valid_metric_depth, valid_depth)

        # Apply scaling to depth and extrinsics
        output.depth *= scale_factor
        output.extrinsics[:, :, :3, 3] *= scale_factor
        output.is_metric = 1
        output.scale_factor = scale_factor.item()

        return output

    def _handle_sky_regions(
        self,
        output: Dict[str, torch.Tensor],
        metric_output: Dict[str, torch.Tensor],
        sky_depth_def: float = 200.0,
    ) -> Dict[str, torch.Tensor]:
        """Handle sky regions by setting them to maximum depth."""
        non_sky_mask = compute_sky_mask(metric_output.sky, threshold=0.3)

        # Compute maximum depth for non-sky regions
        # Use sampling to safely compute quantile on large tensors
        non_sky_depth = output.depth[non_sky_mask]
        if non_sky_depth.numel() > 100000:
            idx = torch.randint(0, non_sky_depth.numel(), (100000,), device=non_sky_depth.device)
            sampled_depth = non_sky_depth[idx]
        else:
            sampled_depth = non_sky_depth
        non_sky_max = min(torch.quantile(sampled_depth, 0.99), sky_depth_def)

        # Set sky regions to maximum depth and high confidence
        output.depth, output.depth_conf = set_sky_regions_to_max_depth(
            output.depth, output.depth_conf, non_sky_mask, max_depth=non_sky_max
        )

        return output



================================================
FILE: src/depth_anything_3/model/dpt.py
================================================
# flake8: noqa E501
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

from typing import Dict as TyDict
from typing import List, Sequence, Tuple
import torch
import torch.nn as nn
from addict import Dict
from einops import rearrange

from depth_anything_3.model.utils.head_utils import (
    Permute,
    create_uv_grid,
    custom_interpolate,
    position_grid_to_embed,
)


class DPT(nn.Module):
    """
    DPT for dense prediction (main head + optional sky head, sky always 1 channel).

    Returns:
      - Main head:
        * If output_dim>1: { head_name, f"{head_name}_conf" }
        * If output_dim==1: { head_name }
      - Sky head (if use_sky_head=True): { sky_name }  # [B, S, 1, H/down_ratio, W/down_ratio]
    """

    def __init__(
        self,
        dim_in: int,
        *,
        patch_size: int = 14,
        output_dim: int = 1,
        activation: str = "exp",
        conf_activation: str = "expp1",
        features: int = 256,
        out_channels: Sequence[int] = (256, 512, 1024, 1024),
        pos_embed: bool = False,
        down_ratio: int = 1,
        head_name: str = "depth",
        # ---- sky head (fixed 1 channel) ----
        use_sky_head: bool = True,
        sky_name: str = "sky",
        sky_activation: str = "relu",  # 'sigmoid' / 'relu' / 'linear'
        use_ln_for_heads: bool = False,  # If needed, apply LayerNorm on intermediate features of both heads
        norm_type: str = "idt",  # use to match legacy GS-DPT head, "idt" / "layer"
        fusion_block_inplace: bool = False,
    ) -> None:
        super().__init__()

        # -------------------- configuration --------------------
        self.patch_size = patch_size
        self.activation = activation
        self.conf_activation = conf_activation
        self.pos_embed = pos_embed
        self.down_ratio = down_ratio

        # Names
        self.head_main = head_name
        self.sky_name = sky_name

        # Main head: output dimension and confidence switch
        self.out_dim = output_dim
        self.has_conf = output_dim > 1

        # Sky head parameters (always 1 channel)
        self.use_sky_head = use_sky_head
        self.sky_activation = sky_activation

        # Fixed 4 intermediate outputs
        self.intermediate_layer_idx: Tuple[int, int, int, int] = (0, 1, 2, 3)

        # -------------------- token pre-norm + per-stage projection --------------------
        if norm_type == "layer":
            self.norm = nn.LayerNorm(dim_in)
        elif norm_type == "idt":
            self.norm = nn.Identity()
        else:
            raise Exception(f"Unknown norm_type {norm_type}, should be 'layer' or 'idt'.")
        self.projects = nn.ModuleList(
            [nn.Conv2d(dim_in, oc, kernel_size=1, stride=1, padding=0) for oc in out_channels]
        )

        # -------------------- Spatial re-size (align to common scale before fusion) --------------------
        # Design consistent with original: relative to patch grid (x4, x2, x1, /2)
        self.resize_layers = nn.ModuleList(
            [
                nn.ConvTranspose2d(
                    out_channels[0], out_channels[0], kernel_size=4, stride=4, padding=0
                ),
                nn.ConvTranspose2d(
                    out_channels[1], out_channels[1], kernel_size=2, stride=2, padding=0
                ),
                nn.Identity(),
                nn.Conv2d(out_channels[3], out_channels[3], kernel_size=3, stride=2, padding=1),
            ]
        )

        # -------------------- scratch: stage adapters + main fusion chain --------------------
        self.scratch = _make_scratch(list(out_channels), features, expand=False)

        # Main fusion chain
        self.scratch.refinenet1 = _make_fusion_block(features, inplace=fusion_block_inplace)
        self.scratch.refinenet2 = _make_fusion_block(features, inplace=fusion_block_inplace)
        self.scratch.refinenet3 = _make_fusion_block(features, inplace=fusion_block_inplace)
        self.scratch.refinenet4 = _make_fusion_block(
            features, has_residual=False, inplace=fusion_block_inplace
        )

        # Heads (shared neck1; then split into two heads)
        head_features_1 = features
        head_features_2 = 32
        self.scratch.output_conv1 = nn.Conv2d(
            head_features_1, head_features_1 // 2, kernel_size=3, stride=1, padding=1
        )

        ln_seq = (
            [Permute((0, 2, 3, 1)), nn.LayerNorm(head_features_2), Permute((0, 3, 1, 2))]
            if use_ln_for_heads
            else []
        )

        # Main head
        self.scratch.output_conv2 = nn.Sequential(
            nn.Conv2d(head_features_1 // 2, head_features_2, kernel_size=3, stride=1, padding=1),
            *ln_seq,
            nn.ReLU(inplace=True),
            nn.Conv2d(head_features_2, output_dim, kernel_size=1, stride=1, padding=0),
        )

        # Sky head (fixed 1 channel)
        if self.use_sky_head:
            self.scratch.sky_output_conv2 = nn.Sequential(
                nn.Conv2d(
                    head_features_1 // 2, head_features_2, kernel_size=3, stride=1, padding=1
                ),
                *ln_seq,
                nn.ReLU(inplace=True),
                nn.Conv2d(head_features_2, 1, kernel_size=1, stride=1, padding=0),
            )

    # -------------------------------------------------------------------------
    # Public forward (supports frame chunking to save memory)
    # -------------------------------------------------------------------------
    def forward(
        self,
        feats: List[torch.Tensor],
        H: int,
        W: int,
        patch_start_idx: int,
        chunk_size: int = 8,
        **kwargs,
    ) -> Dict:
        """
        Args:
            feats: List of 4 entries, each entry is a tensor like [B, S, T, C] (or the 0th element of tuple/list is that tensor).
            H, W:  Original image dimensions
            patch_start_idx: Starting index of patch tokens in sequence (for cropping non-patch tokens)
            chunk_size:      Chunk size along time dimension S

        Returns:
            Dict[str, Tensor]
        """
        B, S, N, C = feats[0][0].shape
        feats = [feat[0].reshape(B * S, N, C) for feat in feats]

        # update image info, used by the GS-DPT head
        extra_kwargs = {}
        if "images" in kwargs:
            extra_kwargs.update({"images": rearrange(kwargs["images"], "B S ... -> (B S) ...")})

        if chunk_size is None or chunk_size >= S:
            out_dict = self._forward_impl(feats, H, W, patch_start_idx, **extra_kwargs)
            out_dict = {k: v.view(B, S, *v.shape[1:]) for k, v in out_dict.items()}
            return Dict(out_dict)

        out_dicts: List[TyDict[str, torch.Tensor]] = []
        for s0 in range(0, S, chunk_size):
            s1 = min(s0 + chunk_size, S)
            kw = {}
            if "images" in extra_kwargs:
                kw.update({"images": extra_kwargs["images"][s0:s1]})
            out_dicts.append(
                self._forward_impl([f[s0:s1] for f in feats], H, W, patch_start_idx, **kw)
            )
        out_dict = {k: torch.cat([od[k] for od in out_dicts], dim=0) for k in out_dicts[0].keys()}
        out_dict = {k: v.view(B, S, *v.shape[1:]) for k, v in out_dict.items()}
        return Dict(out_dict)

    # -------------------------------------------------------------------------
    # Internal forward (single chunk)
    # -------------------------------------------------------------------------
    def _forward_impl(
        self,
        feats: List[torch.Tensor],
        H: int,
        W: int,
        patch_start_idx: int,
    ) -> TyDict[str, torch.Tensor]:
        B, _, C = feats[0].shape
        ph, pw = H // self.patch_size, W // self.patch_size
        resized_feats = []
        for stage_idx, take_idx in enumerate(self.intermediate_layer_idx):
            x = feats[take_idx][:, patch_start_idx:]  # [B*S, N_patch, C]
            x = self.norm(x)
            # permute -> contiguous before reshape to keep conv input contiguous
            x = x.permute(0, 2, 1).contiguous().reshape(B, C, ph, pw)  # [B*S, C, ph, pw]

            x = self.projects[stage_idx](x)
            if self.pos_embed:
                x = self._add_pos_embed(x, W, H)
            x = self.resize_layers[stage_idx](x)  # Align scale
            resized_feats.append(x)

        # 2) Fusion pyramid (main branch only)
        fused = self._fuse(resized_feats)

        # 3) Upsample to target resolution, optionally add position encoding again
        h_out = int(ph * self.patch_size / self.down_ratio)
        w_out = int(pw * self.patch_size / self.down_ratio)

        fused = self.scratch.output_conv1(fused)
        fused = custom_interpolate(fused, (h_out, w_out), mode="bilinear", align_corners=True)
        if self.pos_embed:
            fused = self._add_pos_embed(fused, W, H)

        # 4) Shared neck1
        feat = fused

        # 5) Main head: logits -> activation
        main_logits = self.scratch.output_conv2(feat)
        outs: TyDict[str, torch.Tensor] = {}
        if self.has_conf:
            fmap = main_logits.permute(0, 2, 3, 1)
            pred = self._apply_activation_single(fmap[..., :-1], self.activation)
            conf = self._apply_activation_single(fmap[..., -1], self.conf_activation)
            outs[self.head_main] = pred.squeeze(1)
            outs[f"{self.head_main}_conf"] = conf.squeeze(1)
        else:
            outs[self.head_main] = self._apply_activation_single(
                main_logits, self.activation
            ).squeeze(1)

        # 6) Sky head (fixed 1 channel)
        if self.use_sky_head:
            sky_logits = self.scratch.sky_output_conv2(feat)
            outs[self.sky_name] = self._apply_sky_activation(sky_logits).squeeze(1)

        return outs

    # -------------------------------------------------------------------------
    # Subroutines
    # -------------------------------------------------------------------------
    def _fuse(self, feats: List[torch.Tensor]) -> torch.Tensor:
        """
        4-layer top-down fusion, returns finest scale features (after fusion, before neck1).
        """
        l1, l2, l3, l4 = feats

        l1_rn = self.scratch.layer1_rn(l1)
        l2_rn = self.scratch.layer2_rn(l2)
        l3_rn = self.scratch.layer3_rn(l3)
        l4_rn = self.scratch.layer4_rn(l4)

        # 4 -> 3 -> 2 -> 1
        out = self.scratch.refinenet4(l4_rn, size=l3_rn.shape[2:])
        out = self.scratch.refinenet3(out, l3_rn, size=l2_rn.shape[2:])
        out = self.scratch.refinenet2(out, l2_rn, size=l1_rn.shape[2:])
        out = self.scratch.refinenet1(out, l1_rn)
        return out

    def _apply_activation_single(
        self, x: torch.Tensor, activation: str = "linear"
    ) -> torch.Tensor:
        """
        Apply activation to single channel output, maintaining semantic consistency with value branch in multi-channel case.
        Supports: exp / relu / sigmoid / softplus / tanh / linear / expp1
        """
        act = activation.lower() if isinstance(activation, str) else activation
        if act == "exp":
            return torch.exp(x)
        if act == "expp1":
            return torch.exp(x) + 1
        if act == "expm1":
            return torch.expm1(x)
        if act == "relu":
            return torch.relu(x)
        if act == "sigmoid":
            return torch.sigmoid(x)
        if act == "softplus":
            return torch.nn.functional.softplus(x)
        if act == "tanh":
            return torch.tanh(x)
        # Default linear
        return x

    def _apply_sky_activation(self, x: torch.Tensor) -> torch.Tensor:
        """
        Sky head activation (fixed 1 channel):
          * 'sigmoid' -> Sigmoid probability map
          * 'relu'    -> ReLU positive domain output
          * 'linear'  -> Original value (logits)
        """
        act = (
            self.sky_activation.lower()
            if isinstance(self.sky_activation, str)
            else self.sky_activation
        )
        if act == "sigmoid":
            return torch.sigmoid(x)
        if act == "relu":
            return torch.relu(x)
        # 'linear'
        return x

    def _add_pos_embed(self, x: torch.Tensor, W: int, H: int, ratio: float = 0.1) -> torch.Tensor:
        """Simple UV position encoding directly added to feature map."""
        pw, ph = x.shape[-1], x.shape[-2]
        pe = create_uv_grid(pw, ph, aspect_ratio=W / H, dtype=x.dtype, device=x.device)
        pe = position_grid_to_embed(pe, x.shape[1]) * ratio
        pe = pe.permute(2, 0, 1)[None].expand(x.shape[0], -1, -1, -1)
        return x + pe


# -----------------------------------------------------------------------------
# Building blocks (preserved, consistent with original)
# -----------------------------------------------------------------------------
def _make_fusion_block(
    features: int,
    size: Tuple[int, int] = None,
    has_residual: bool = True,
    groups: int = 1,
    inplace: bool = False,
) -> nn.Module:
    return FeatureFusionBlock(
        features=features,
        activation=nn.ReLU(inplace=inplace),
        deconv=False,
        bn=False,
        expand=False,
        align_corners=True,
        size=size,
        has_residual=has_residual,
        groups=groups,
    )


def _make_scratch(
    in_shape: List[int], out_shape: int, groups: int = 1, expand: bool = False
) -> nn.Module:
    scratch = nn.Module()
    # Optional expansion by stage
    c1 = out_shape
    c2 = out_shape * (2 if expand else 1)
    c3 = out_shape * (4 if expand else 1)
    c4 = out_shape * (8 if expand else 1)

    scratch.layer1_rn = nn.Conv2d(in_shape[0], c1, 3, 1, 1, bias=False, groups=groups)
    scratch.layer2_rn = nn.Conv2d(in_shape[1], c2, 3, 1, 1, bias=False, groups=groups)
    scratch.layer3_rn = nn.Conv2d(in_shape[2], c3, 3, 1, 1, bias=False, groups=groups)
    scratch.layer4_rn = nn.Conv2d(in_shape[3], c4, 3, 1, 1, bias=False, groups=groups)
    return scratch


class ResidualConvUnit(nn.Module):
    """Lightweight residual convolution block for fusion"""

    def __init__(self, features: int, activation: nn.Module, bn: bool, groups: int = 1) -> None:
        super().__init__()
        self.bn = bn
        self.groups = groups
        self.conv1 = nn.Conv2d(features, features, 3, 1, 1, bias=True, groups=groups)
        self.conv2 = nn.Conv2d(features, features, 3, 1, 1, bias=True, groups=groups)
        self.norm1 = None
        self.norm2 = None
        self.activation = activation
        self.skip_add = nn.quantized.FloatFunctional()

    def forward(self, x: torch.Tensor) -> torch.Tensor:  # type: ignore[override]
        out = self.activation(x)
        out = self.conv1(out)
        if self.norm1 is not None:
            out = self.norm1(out)

        out = self.activation(out)
        out = self.conv2(out)
        if self.norm2 is not None:
            out = self.norm2(out)

        return self.skip_add.add(out, x)


class FeatureFusionBlock(nn.Module):
    """Top-down fusion block: (optional) residual merge + upsampling + 1x1 contraction"""

    def __init__(
        self,
        features: int,
        activation: nn.Module,
        deconv: bool = False,
        bn: bool = False,
        expand: bool = False,
        align_corners: bool = True,
        size: Tuple[int, int] = None,
        has_residual: bool = True,
        groups: int = 1,
    ) -> None:
        super().__init__()
        self.align_corners = align_corners
        self.size = size
        self.has_residual = has_residual

        self.resConfUnit1 = (
            ResidualConvUnit(features, activation, bn, groups=groups) if has_residual else None
        )
        self.resConfUnit2 = ResidualConvUnit(features, activation, bn, groups=groups)

        out_features = (features // 2) if expand else features
        self.out_conv = nn.Conv2d(features, out_features, 1, 1, 0, bias=True, groups=groups)
        self.skip_add = nn.quantized.FloatFunctional()

    def forward(self, *xs: torch.Tensor, size: Tuple[int, int] = None) -> torch.Tensor:  # type: ignore[override]
        """
        xs:
          - xs[0]: Top branch input
          - xs[1]: Lateral input (can do residual addition with top branch)
        """
        y = xs[0]
        if self.has_residual and len(xs) > 1 and self.resConfUnit1 is not None:
            y = self.skip_add.add(y, self.resConfUnit1(xs[1]))

        y = self.resConfUnit2(y)

        # Upsampling
        if (size is None) and (self.size is None):
            up_kwargs = {"scale_factor": 2}
        elif size is None:
            up_kwargs = {"size": self.size}
        else:
            up_kwargs = {"size": size}

        y = custom_interpolate(y, **up_kwargs, mode="bilinear", align_corners=self.align_corners)
        y = self.out_conv(y)
        return y



================================================
FILE: src/depth_anything_3/model/dualdpt.py
================================================
# flake8: noqa E501
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

from typing import List, Sequence, Tuple
import torch
import torch.nn as nn
from addict import Dict

from depth_anything_3.model.dpt import _make_fusion_block, _make_scratch
from depth_anything_3.model.utils.head_utils import (
    Permute,
    create_uv_grid,
    custom_interpolate,
    position_grid_to_embed,
)


class DualDPT(nn.Module):
    """
    Dual-head DPT for dense prediction with an always-on auxiliary head.

    Architectural notes:
      - Sky/object branches are removed.
      - `intermediate_layer_idx` is fixed to (0, 1, 2, 3).
      - Auxiliary head has its **own** fusion blocks (no fusion_inplace / no sharing).
      - Auxiliary head is internally multi-level; **only the final level** is returned.
      - Returns a **dict** with keys from `head_names`, e.g.:
          { main_name, f"{main_name}_conf", aux_name, f"{aux_name}_conf" }
      - `feature_only` is fixed to False.
    """

    def __init__(
        self,
        dim_in: int,
        *,
        patch_size: int = 14,
        output_dim: int = 2,
        activation: str = "exp",
        conf_activation: str = "expp1",
        features: int = 256,
        out_channels: Sequence[int] = (256, 512, 1024, 1024),
        pos_embed: bool = True,
        down_ratio: int = 1,
        aux_pyramid_levels: int = 4,
        aux_out1_conv_num: int = 5,
        head_names: Tuple[str, str] = ("depth", "ray"),
    ) -> None:
        super().__init__()

        # -------------------- configuration --------------------
        self.patch_size = patch_size
        self.activation = activation
        self.conf_activation = conf_activation
        self.pos_embed = pos_embed
        self.down_ratio = down_ratio

        self.aux_levels = aux_pyramid_levels
        self.aux_out1_conv_num = aux_out1_conv_num

        # names ONLY come from config (no hard-coded strings elsewhere)
        self.head_main, self.head_aux = head_names

        # Always expect 4 scales; enforce intermediate idx = (0, 1, 2, 3)
        self.intermediate_layer_idx: Tuple[int, int, int, int] = (0, 1, 2, 3)

        # -------------------- token pre-norm + per-stage projection --------------------
        self.norm = nn.LayerNorm(dim_in)
        self.projects = nn.ModuleList(
            [nn.Conv2d(dim_in, oc, kernel_size=1, stride=1, padding=0) for oc in out_channels]
        )

        # -------------------- spatial re-sizers (align to common scale before fusion) --------------------
        # design: stage strides (x4, x2, x1, /2) relative to patch grid to align to a common pivot scale
        self.resize_layers = nn.ModuleList(
            [
                nn.ConvTranspose2d(
                    out_channels[0], out_channels[0], kernel_size=4, stride=4, padding=0
                ),
                nn.ConvTranspose2d(
                    out_channels[1], out_channels[1], kernel_size=2, stride=2, padding=0
                ),
                nn.Identity(),
                nn.Conv2d(out_channels[3], out_channels[3], kernel_size=3, stride=2, padding=1),
            ]
        )

        # -------------------- scratch: stage adapters + fusion (main & aux are separate) --------------------
        self.scratch = _make_scratch(list(out_channels), features, expand=False)

        # Main fusion chain (independent)
        self.scratch.refinenet1 = _make_fusion_block(features)
        self.scratch.refinenet2 = _make_fusion_block(features)
        self.scratch.refinenet3 = _make_fusion_block(features)
        self.scratch.refinenet4 = _make_fusion_block(features, has_residual=False)

        # Primary head neck + head (independent)
        head_features_1 = features
        head_features_2 = 32
        self.scratch.output_conv1 = nn.Conv2d(
            head_features_1, head_features_1 // 2, kernel_size=3, stride=1, padding=1
        )
        self.scratch.output_conv2 = nn.Sequential(
            nn.Conv2d(head_features_1 // 2, head_features_2, kernel_size=3, stride=1, padding=1),
            nn.ReLU(inplace=True),
            nn.Conv2d(head_features_2, output_dim, kernel_size=1, stride=1, padding=0),
        )

        # Auxiliary fusion chain (completely separate; no sharing, i.e., "fusion_inplace=False")
        self.scratch.refinenet1_aux = _make_fusion_block(features)
        self.scratch.refinenet2_aux = _make_fusion_block(features)
        self.scratch.refinenet3_aux = _make_fusion_block(features)
        self.scratch.refinenet4_aux = _make_fusion_block(features, has_residual=False)

        # Aux pre-head per level (we will only *return final level*)
        self.scratch.output_conv1_aux = nn.ModuleList(
            [self._make_aux_out1_block(head_features_1) for _ in range(self.aux_levels)]
        )

        # Aux final projection per level
        use_ln = True
        ln_seq = (
            [Permute((0, 2, 3, 1)), nn.LayerNorm(head_features_2), Permute((0, 3, 1, 2))]
            if use_ln
            else []
        )
        self.scratch.output_conv2_aux = nn.ModuleList(
            [
                nn.Sequential(
                    nn.Conv2d(
                        head_features_1 // 2, head_features_2, kernel_size=3, stride=1, padding=1
                    ),
                    *ln_seq,
                    nn.ReLU(inplace=True),
                    nn.Conv2d(head_features_2, 7, kernel_size=1, stride=1, padding=0),
                )
                for _ in range(self.aux_levels)
            ]
        )

    # -------------------------------------------------------------------------
    # Public forward (supports frame chunking for memory)
    # -------------------------------------------------------------------------

    def forward(
        self,
        feats: List[torch.Tensor],
        H: int,
        W: int,
        patch_start_idx: int,
        chunk_size: int = 8,
    ) -> Dict[str, torch.Tensor]:
        """
        Args:
            aggregated_tokens_list: List of 4 tensors [B, S, T, C] from transformer.
            images:                [B, S, 3, H, W], in [0, 1].
            patch_start_idx:       Patch-token start in the token sequence (to drop non-patch tokens).
            frames_chunk_size:     Optional chunking along S for memory.

        Returns:
            Dict[str, Tensor] with keys based on `head_names`, e.g.:
                self.head_main, f"{self.head_main}_conf",
                self.head_aux,  f"{self.head_aux}_conf"
            Shapes:
              main:    [B, S, out_dim, H/down_ratio, W/down_ratio]
              main_cf: [B, S, 1,       H/down_ratio, W/down_ratio]
              aux:     [B, S, 7,       H/down_ratio, W/down_ratio]
              aux_cf:  [B, S, 1,       H/down_ratio, W/down_ratio]
        """
        B, S, N, C = feats[0][0].shape
        feats = [feat[0].reshape(B * S, N, C) for feat in feats]
        if chunk_size is None or chunk_size >= S:
            out_dict = self._forward_impl(feats, H, W, patch_start_idx)
            out_dict = {k: v.reshape(B, S, *v.shape[1:]) for k, v in out_dict.items()}
            return Dict(out_dict)
        out_dicts = []
        for s0 in range(0, B * S, chunk_size):
            s1 = min(s0 + chunk_size, B * S)
            out_dict = self._forward_impl(
                [feat[s0:s1] for feat in feats],
                H,
                W,
                patch_start_idx,
            )
            out_dicts.append(out_dict)
        out_dict = {
            k: torch.cat([out_dict[k] for out_dict in out_dicts], dim=0)
            for k in out_dicts[0].keys()
        }
        out_dict = {k: v.view(B, S, *v.shape[1:]) for k, v in out_dict.items()}
        return Dict(out_dict)

    # -------------------------------------------------------------------------
    # Internal forward (single chunk)
    # -------------------------------------------------------------------------

    def _forward_impl(
        self,
        feats: List[torch.Tensor],
        H: int,
        W: int,
        patch_start_idx: int,
    ) -> Dict[str, torch.Tensor]:
        B, _, C = feats[0].shape
        ph, pw = H // self.patch_size, W // self.patch_size
        resized_feats = []
        for stage_idx, take_idx in enumerate(self.intermediate_layer_idx):
            x = feats[take_idx][:, patch_start_idx:]
            x = self.norm(x)
            x = x.permute(0, 2, 1).reshape(B, C, ph, pw)  # [B*S, C, ph, pw]

            x = self.projects[stage_idx](x)
            if self.pos_embed:
                x = self._add_pos_embed(x, W, H)
            x = self.resize_layers[stage_idx](x)  # align scales
            resized_feats.append(x)

        # 2) Fuse pyramid (main & aux are completely independent)
        fused_main, fused_aux_pyr = self._fuse(resized_feats)

        # 3) Upsample to target resolution and (optional) add pos-embed again
        h_out = int(ph * self.patch_size / self.down_ratio)
        w_out = int(pw * self.patch_size / self.down_ratio)

        fused_main = custom_interpolate(
            fused_main, (h_out, w_out), mode="bilinear", align_corners=True
        )
        if self.pos_embed:
            fused_main = self._add_pos_embed(fused_main, W, H)

        # Primary head: conv1 -> conv2 -> activate
        # fused_main = self.scratch.output_conv1(fused_main)
        main_logits = self.scratch.output_conv2(fused_main)
        fmap = main_logits.permute(0, 2, 3, 1)
        main_pred = self._apply_activation_single(fmap[..., :-1], self.activation)
        main_conf = self._apply_activation_single(fmap[..., -1], self.conf_activation)

        # Auxiliary head (multi-level inside) -> only last level returned (after activation)
        last_aux = fused_aux_pyr[-1]
        if self.pos_embed:
            last_aux = self._add_pos_embed(last_aux, W, H)
        # neck (per-level pre-conv) then final projection (only for last level)
        # last_aux = self.scratch.output_conv1_aux[-1](last_aux)
        last_aux_logits = self.scratch.output_conv2_aux[-1](last_aux)
        fmap_last = last_aux_logits.permute(0, 2, 3, 1)
        aux_pred = self._apply_activation_single(fmap_last[..., :-1], "linear")
        aux_conf = self._apply_activation_single(fmap_last[..., -1], self.conf_activation)
        return {
            self.head_main: main_pred.squeeze(-1),
            f"{self.head_main}_conf": main_conf,
            self.head_aux: aux_pred,
            f"{self.head_aux}_conf": aux_conf,
        }

    # -------------------------------------------------------------------------
    # Subroutines
    # -------------------------------------------------------------------------

    def _fuse(self, feats: List[torch.Tensor]) -> Tuple[torch.Tensor, List[torch.Tensor]]:
        """
        Feature pyramid fusion.
        Returns:
            fused_main: Tensor at finest scale (after refinenet1)
            aux_pyr:    List of aux tensors at each level (pre out_conv1_aux)
        """
        l1, l2, l3, l4 = feats

        l1_rn = self.scratch.layer1_rn(l1)
        l2_rn = self.scratch.layer2_rn(l2)
        l3_rn = self.scratch.layer3_rn(l3)
        l4_rn = self.scratch.layer4_rn(l4)

        # level 4 -> 3
        out = self.scratch.refinenet4(l4_rn, size=l3_rn.shape[2:])
        aux_out = self.scratch.refinenet4_aux(l4_rn, size=l3_rn.shape[2:])
        aux_list: List[torch.Tensor] = []
        if self.aux_levels >= 4:
            aux_list.append(aux_out)

        # level 3 -> 2
        out = self.scratch.refinenet3(out, l3_rn, size=l2_rn.shape[2:])
        aux_out = self.scratch.refinenet3_aux(aux_out, l3_rn, size=l2_rn.shape[2:])
        if self.aux_levels >= 3:
            aux_list.append(aux_out)

        # level 2 -> 1
        out = self.scratch.refinenet2(out, l2_rn, size=l1_rn.shape[2:])
        aux_out = self.scratch.refinenet2_aux(aux_out, l2_rn, size=l1_rn.shape[2:])
        if self.aux_levels >= 2:
            aux_list.append(aux_out)

        # level 1 (final)
        out = self.scratch.refinenet1(out, l1_rn)
        aux_out = self.scratch.refinenet1_aux(aux_out, l1_rn)
        aux_list.append(aux_out)

        out = self.scratch.output_conv1(out)
        aux_list = [self.scratch.output_conv1_aux[i](aux) for i, aux in enumerate(aux_list)]

        return out, aux_list

    def _add_pos_embed(self, x: torch.Tensor, W: int, H: int, ratio: float = 0.1) -> torch.Tensor:
        """Simple UV positional embedding added to feature maps."""
        pw, ph = x.shape[-1], x.shape[-2]
        pe = create_uv_grid(pw, ph, aspect_ratio=W / H, dtype=x.dtype, device=x.device)
        pe = position_grid_to_embed(pe, x.shape[1]) * ratio
        pe = pe.permute(2, 0, 1)[None].expand(x.shape[0], -1, -1, -1)
        return x + pe

    def _make_aux_out1_block(self, in_ch: int) -> nn.Sequential:
        """Factory for the aux pre-head stack before the final 1x1 projection."""
        if self.aux_out1_conv_num == 5:
            return nn.Sequential(
                nn.Conv2d(in_ch, in_ch // 2, 3, 1, 1),
                nn.Conv2d(in_ch // 2, in_ch, 3, 1, 1),
                nn.Conv2d(in_ch, in_ch // 2, 3, 1, 1),
                nn.Conv2d(in_ch // 2, in_ch, 3, 1, 1),
                nn.Conv2d(in_ch, in_ch // 2, 3, 1, 1),
            )
        if self.aux_out1_conv_num == 3:
            return nn.Sequential(
                nn.Conv2d(in_ch, in_ch // 2, 3, 1, 1),
                nn.Conv2d(in_ch // 2, in_ch, 3, 1, 1),
                nn.Conv2d(in_ch, in_ch // 2, 3, 1, 1),
            )
        if self.aux_out1_conv_num == 1:
            return nn.Sequential(nn.Conv2d(in_ch, in_ch // 2, 3, 1, 1))
        raise ValueError(f"aux_out1_conv_num {self.aux_out1_conv_num} not supported")

    def _apply_activation_single(
        self, x: torch.Tensor, activation: str = "linear"
    ) -> torch.Tensor:
        """
        Apply activation to single channel output, maintaining semantic consistency with value branch in multi-channel case.
        Supports: exp / relu / sigmoid / softplus / tanh / linear / expp1
        """
        act = activation.lower() if isinstance(activation, str) else activation
        if act == "exp":
            return torch.exp(x)
        if act == "expm1":
            return torch.expm1(x)
        if act == "expp1":
            return torch.exp(x) + 1
        if act == "relu":
            return torch.relu(x)
        if act == "sigmoid":
            return torch.sigmoid(x)
        if act == "softplus":
            return torch.nn.functional.softplus(x)
        if act == "tanh":
            return torch.tanh(x)
        # Default linear
        return x


# # -----------------------------------------------------------------------------
# # Building blocks (tidy)
# # -----------------------------------------------------------------------------


# def _make_fusion_block(
#     features: int,
#     size: Tuple[int, int] = None,
#     has_residual: bool = True,
#     groups: int = 1,
#     inplace: bool = False,  # <- activation uses inplace=True by default; not related to "fusion_inplace"
# ) -> nn.Module:
#     return FeatureFusionBlock(
#         features=features,
#         activation=nn.ReLU(inplace=inplace),
#         deconv=False,
#         bn=False,
#         expand=False,
#         align_corners=True,
#         size=size,
#         has_residual=has_residual,
#         groups=groups,
#     )


# def _make_scratch(
#     in_shape: List[int], out_shape: int, groups: int = 1, expand: bool = False
# ) -> nn.Module:
#     scratch = nn.Module()
#     # optionally expand widths by stage
#     c1 = out_shape
#     c2 = out_shape * (2 if expand else 1)
#     c3 = out_shape * (4 if expand else 1)
#     c4 = out_shape * (8 if expand else 1)

#     scratch.layer1_rn = nn.Conv2d(in_shape[0], c1, 3, 1, 1, bias=False, groups=groups)
#     scratch.layer2_rn = nn.Conv2d(in_shape[1], c2, 3, 1, 1, bias=False, groups=groups)
#     scratch.layer3_rn = nn.Conv2d(in_shape[2], c3, 3, 1, 1, bias=False, groups=groups)
#     scratch.layer4_rn = nn.Conv2d(in_shape[3], c4, 3, 1, 1, bias=False, groups=groups)
#     return scratch


# class ResidualConvUnit(nn.Module):
#     """Lightweight residual conv block used within fusion."""

#     def __init__(self, features: int, activation: nn.Module, bn: bool, groups: int = 1) -> None:
#         super().__init__()
#         self.bn = bn
#         self.groups = groups
#         self.conv1 = nn.Conv2d(features, features, 3, 1, 1, bias=True, groups=groups)
#         self.conv2 = nn.Conv2d(features, features, 3, 1, 1, bias=True, groups=groups)
#         self.norm1 = None
#         self.norm2 = None
#         self.activation = activation
#         self.skip_add = nn.quantized.FloatFunctional()

#     def forward(self, x: torch.Tensor) -> torch.Tensor:  # type: ignore[override]
#         out = self.activation(x)
#         out = self.conv1(out)
#         if self.norm1 is not None:
#             out = self.norm1(out)

#         out = self.activation(out)
#         out = self.conv2(out)
#         if self.norm2 is not None:
#             out = self.norm2(out)

#         return self.skip_add.add(out, x)


# class FeatureFusionBlock(nn.Module):
#     """Top-down fusion block: (optional) residual merge + upsample + 1x1 shrink."""

#     def __init__(
#         self,
#         features: int,
#         activation: nn.Module,
#         deconv: bool = False,
#         bn: bool = False,
#         expand: bool = False,
#         align_corners: bool = True,
#         size: Tuple[int, int] = None,
#         has_residual: bool = True,
#         groups: int = 1,
#     ) -> None:
#         super().__init__()
#         self.align_corners = align_corners
#         self.size = size
#         self.has_residual = has_residual

#         self.resConfUnit1 = (
#             ResidualConvUnit(features, activation, bn, groups=groups) if has_residual else None
#         )
#         self.resConfUnit2 = ResidualConvUnit(features, activation, bn, groups=groups)

#         out_features = (features // 2) if expand else features
#         self.out_conv = nn.Conv2d(features, out_features, 1, 1, 0, bias=True, groups=groups)
#         self.skip_add = nn.quantized.FloatFunctional()

#     def forward(self, *xs: torch.Tensor, size: Tuple[int, int] = None) -> torch.Tensor:  # type: ignore[override]
#         """
#         xs:
#           - xs[0]: top input
#           - xs[1]: (optional) lateral (to be added with residual)
#         """
#         y = xs[0]
#         if self.has_residual and len(xs) > 1 and self.resConfUnit1 is not None:
#             y = self.skip_add.add(y, self.resConfUnit1(xs[1]))

#         y = self.resConfUnit2(y)

#         # upsample
#         if (size is None) and (self.size is None):
#             up_kwargs = {"scale_factor": 2}
#         elif size is None:
#             up_kwargs = {"size": self.size}
#         else:
#             up_kwargs = {"size": size}

#         y = custom_interpolate(y, **up_kwargs, mode="bilinear", align_corners=self.align_corners)
#         y = self.out_conv(y)
#         return y



================================================
FILE: src/depth_anything_3/model/gs_adapter.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

from typing import Optional
import torch
from einops import einsum, rearrange, repeat
from torch import nn

from depth_anything_3.model.utils.transform import cam_quat_xyzw_to_world_quat_wxyz
from depth_anything_3.specs import Gaussians
from depth_anything_3.utils.geometry import affine_inverse, get_world_rays, sample_image_grid
from depth_anything_3.utils.pose_align import batch_align_poses_umeyama
from depth_anything_3.utils.sh_helpers import rotate_sh


class GaussianAdapter(nn.Module):

    def __init__(
        self,
        sh_degree: int = 0,
        pred_color: bool = False,
        pred_offset_depth: bool = False,
        pred_offset_xy: bool = True,
        gaussian_scale_min: float = 1e-5,
        gaussian_scale_max: float = 30.0,
    ):
        super().__init__()
        self.sh_degree = sh_degree
        self.pred_color = pred_color
        self.pred_offset_depth = pred_offset_depth
        self.pred_offset_xy = pred_offset_xy
        self.gaussian_scale_min = gaussian_scale_min
        self.gaussian_scale_max = gaussian_scale_max

        # Create a mask for the spherical harmonics coefficients. This ensures that at
        # initialization, the coefficients are biased towards having a large DC
        # component and small view-dependent components.
        if not pred_color:
            self.register_buffer(
                "sh_mask",
                torch.ones((self.d_sh,), dtype=torch.float32),
                persistent=False,
            )
            for degree in range(1, sh_degree + 1):
                self.sh_mask[degree**2 : (degree + 1) ** 2] = 0.1 * 0.25**degree

    def forward(
        self,
        extrinsics: torch.Tensor,  # "*#batch 4 4"
        intrinsics: torch.Tensor,  # "*#batch 3 3"
        depths: torch.Tensor,  # "*#batch"
        opacities: torch.Tensor,  # "*#batch" | "*#batch _"
        raw_gaussians: torch.Tensor,  # "*#batch _"
        image_shape: tuple[int, int],
        eps: float = 1e-8,
        gt_extrinsics: Optional[torch.Tensor] = None,  # "*#batch 4 4"
        **kwargs,
    ) -> Gaussians:
        device = extrinsics.device
        dtype = raw_gaussians.dtype
        H, W = image_shape
        b, v = raw_gaussians.shape[:2]

        # get cam2worlds and intr_normed to adapt to 3DGS codebase
        cam2worlds = affine_inverse(extrinsics)
        intr_normed = intrinsics.clone().detach()
        intr_normed[..., 0, :] /= W
        intr_normed[..., 1, :] /= H

        # 1. compute 3DGS means
        # 1.1) offset the predicted depth if needed
        if self.pred_offset_depth:
            gs_depths = depths + raw_gaussians[..., -1]
            raw_gaussians = raw_gaussians[..., :-1]
        else:
            gs_depths = depths
        # 1.2) align predicted poses with GT if needed
        if gt_extrinsics is not None and not torch.equal(extrinsics, gt_extrinsics):
            try:
                _, _, pose_scales = batch_align_poses_umeyama(
                    gt_extrinsics.detach().float(),
                    extrinsics.detach().float(),
                )
            except Exception:
                pose_scales = torch.ones_like(extrinsics[:, 0, 0, 0])
            pose_scales = torch.clamp(pose_scales, min=1 / 3.0, max=3.0)
            cam2worlds[:, :, :3, 3] = cam2worlds[:, :, :3, 3] * rearrange(
                pose_scales, "b -> b () ()"
            )  # [b, i, j]
            gs_depths = gs_depths * rearrange(pose_scales, "b -> b () () ()")  # [b, v, h, w]
        # 1.3) casting xy in image space
        xy_ray, _ = sample_image_grid((H, W), device)
        xy_ray = xy_ray[None, None, ...].expand(b, v, -1, -1, -1)  # b v h w xy
        # offset xy if needed
        if self.pred_offset_xy:
            pixel_size = 1 / torch.tensor((W, H), dtype=xy_ray.dtype, device=device)
            offset_xy = raw_gaussians[..., :2]
            xy_ray = xy_ray + offset_xy * pixel_size
            raw_gaussians = raw_gaussians[..., 2:]  # skip the offset_xy
        # 1.4) unproject depth + xy to world ray
        origins, directions = get_world_rays(
            xy_ray,
            repeat(cam2worlds, "b v i j -> b v h w i j", h=H, w=W),
            repeat(intr_normed, "b v i j -> b v h w i j", h=H, w=W),
        )
        gs_means_world = origins + directions * gs_depths[..., None]
        gs_means_world = rearrange(gs_means_world, "b v h w d -> b (v h w) d")

        # 2. compute other GS attributes
        scales, rotations, sh = raw_gaussians.split((3, 4, 3 * self.d_sh), dim=-1)

        # 2.1) 3DGS scales
        # make the scale invarient to resolution
        scale_min = self.gaussian_scale_min
        scale_max = self.gaussian_scale_max
        scales = scale_min + (scale_max - scale_min) * scales.sigmoid()
        pixel_size = 1 / torch.tensor((W, H), dtype=dtype, device=device)
        multiplier = self.get_scale_multiplier(intr_normed, pixel_size)
        gs_scales = scales * gs_depths[..., None] * multiplier[..., None, None, None]
        gs_scales = rearrange(gs_scales, "b v h w d -> b (v h w) d")

        # 2.2) 3DGS quaternion (world space)
        # due to historical issue, assume quaternion in order xyzw, not wxyz
        # Normalize the quaternion features to yield a valid quaternion.
        rotations = rotations / (rotations.norm(dim=-1, keepdim=True) + eps)
        # rotate them to world space
        cam_quat_xyzw = rearrange(rotations, "b v h w c -> b (v h w) c")
        c2w_mat = repeat(
            cam2worlds,
            "b v i j -> b (v h w) i j",
            h=H,
            w=W,
        )
        world_quat_wxyz = cam_quat_xyzw_to_world_quat_wxyz(cam_quat_xyzw, c2w_mat)
        gs_rotations_world = world_quat_wxyz  # b (v h w) c

        # 2.3) 3DGS color / SH coefficient (world space)
        sh = rearrange(sh, "... (xyz d_sh) -> ... xyz d_sh", xyz=3)
        if not self.pred_color:
            sh = sh * self.sh_mask

        if self.pred_color or self.sh_degree == 0:
            # predict pre-computed color or predict only DC band, no need to transform
            gs_sh_world = sh
        else:
            gs_sh_world = rotate_sh(sh, cam2worlds[:, :, None, None, None, :3, :3])
        gs_sh_world = rearrange(gs_sh_world, "b v h w xyz d_sh -> b (v h w) xyz d_sh")

        # 2.4) 3DGS opacity
        gs_opacities = rearrange(opacities, "b v h w ... -> b (v h w) ...")

        return Gaussians(
            means=gs_means_world,
            harmonics=gs_sh_world,
            opacities=gs_opacities,
            scales=gs_scales,
            rotations=gs_rotations_world,
        )

    def get_scale_multiplier(
        self,
        intrinsics: torch.Tensor,  # "*#batch 3 3"
        pixel_size: torch.Tensor,  # "*#batch 2"
        multiplier: float = 0.1,
    ) -> torch.Tensor:  # " *batch"
        xy_multipliers = multiplier * einsum(
            intrinsics[..., :2, :2].float().inverse().to(intrinsics),
            pixel_size,
            "... i j, j -> ... i",
        )
        return xy_multipliers.sum(dim=-1)

    @property
    def d_sh(self) -> int:
        return 1 if self.pred_color else (self.sh_degree + 1) ** 2

    @property
    def d_in(self) -> int:
        # provided as reference to the gs_dpt output dim
        raw_gs_dim = 0
        if self.pred_offset_xy:
            raw_gs_dim += 2
        raw_gs_dim += 3  # scales
        raw_gs_dim += 4  # quaternion
        raw_gs_dim += 3 * self.d_sh  # color
        if self.pred_offset_depth:
            raw_gs_dim += 1

        return raw_gs_dim



================================================
FILE: src/depth_anything_3/model/gsdpt.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

from typing import Dict as TyDict
from typing import List, Sequence
import torch
import torch.nn as nn

from depth_anything_3.model.dpt import DPT
from depth_anything_3.model.utils.head_utils import activate_head_gs, custom_interpolate


class GSDPT(DPT):

    def __init__(
        self,
        dim_in: int,
        patch_size: int = 14,
        output_dim: int = 4,
        activation: str = "linear",
        conf_activation: str = "sigmoid",
        features: int = 256,
        out_channels: Sequence[int] = (256, 512, 1024, 1024),
        pos_embed: bool = True,
        feature_only: bool = False,
        down_ratio: int = 1,
        conf_dim: int = 1,
        norm_type: str = "idt",  # use to match legacy GS-DPT head, "idt" / "layer"
        fusion_block_inplace: bool = False,
    ) -> None:
        super().__init__(
            dim_in=dim_in,
            patch_size=patch_size,
            output_dim=output_dim,
            activation=activation,
            conf_activation=conf_activation,
            features=features,
            out_channels=out_channels,
            pos_embed=pos_embed,
            down_ratio=down_ratio,
            head_name="raw_gs",
            use_sky_head=False,
            norm_type=norm_type,
            fusion_block_inplace=fusion_block_inplace,
        )
        self.conf_dim = conf_dim
        if conf_dim and conf_dim > 1:
            assert (
                conf_activation == "linear"
            ), "use linear prediction when using view-dependent opacity"

        merger_out_dim = features if feature_only else features // 2
        self.images_merger = nn.Sequential(
            nn.Conv2d(3, merger_out_dim // 4, 3, 1, 1),  # fewer channels first
            nn.GELU(),
            nn.Conv2d(merger_out_dim // 4, merger_out_dim // 2, 3, 1, 1),
            nn.GELU(),
            nn.Conv2d(merger_out_dim // 2, merger_out_dim, 3, 1, 1),
            nn.GELU(),
        )

    # -------------------------------------------------------------------------
    # Internal forward (single chunk)
    # -------------------------------------------------------------------------
    def _forward_impl(
        self,
        feats: List[torch.Tensor],
        H: int,
        W: int,
        patch_start_idx: int,
        images: torch.Tensor,
    ) -> TyDict[str, torch.Tensor]:
        B, _, C = feats[0].shape
        ph, pw = H // self.patch_size, W // self.patch_size
        resized_feats = []
        for stage_idx, take_idx in enumerate(self.intermediate_layer_idx):
            x = feats[take_idx][:, patch_start_idx:]  # [B*S, N_patch, C]
            x = self.norm(x)
            x = x.permute(0, 2, 1).reshape(B, C, ph, pw)  # [B*S, C, ph, pw]

            x = self.projects[stage_idx](x)
            if self.pos_embed:
                x = self._add_pos_embed(x, W, H)
            x = self.resize_layers[stage_idx](x)  # Align scale
            resized_feats.append(x)

        # 2) Fusion pyramid (main branch only)
        fused = self._fuse(resized_feats)
        fused = self.scratch.output_conv1(fused)

        # 3) Upsample to target resolution, optionally add position encoding again
        h_out = int(ph * self.patch_size / self.down_ratio)
        w_out = int(pw * self.patch_size / self.down_ratio)

        fused = custom_interpolate(fused, (h_out, w_out), mode="bilinear", align_corners=True)

        # inject the image information here
        fused = fused + self.images_merger(images)

        if self.pos_embed:
            fused = self._add_pos_embed(fused, W, H)

        # 4) Shared neck1
        # feat = self.scratch.output_conv1(fused)
        feat = fused

        # 5) Main head: logits -> activate_head or single channel activation
        main_logits = self.scratch.output_conv2(feat)
        outs: TyDict[str, torch.Tensor] = {}
        if self.has_conf:
            pred, conf = activate_head_gs(
                main_logits,
                activation=self.activation,
                conf_activation=self.conf_activation,
                conf_dim=self.conf_dim,
            )
            outs[self.head_main] = pred.squeeze(1)
            outs[f"{self.head_main}_conf"] = conf.squeeze(1)
        else:
            outs[self.head_main] = self._apply_activation_single(main_logits).squeeze(1)

        return outs



================================================
FILE: src/depth_anything_3/model/reference_view_selector.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

"""
Reference View Selection Strategies

This module provides different strategies for selecting a reference view
from multiple input views in multi-view depth estimation.
"""

import torch
from typing import Literal


RefViewStrategy = Literal["first", "middle", "saddle_balanced", "saddle_sim_range"]


def select_reference_view(
    x: torch.Tensor,
    strategy: RefViewStrategy = "saddle_balanced",
) -> torch.Tensor:
    """
    Select a reference view from multiple views using the specified strategy.
    
    Args:
        x: Input tensor of shape (B, S, N, C) where
           B = batch size
           S = number of views
           N = number of tokens
           C = channel dimension
        strategy: Selection strategy, one of:
            - "first": Always select the first view
            - "middle": Select the middle view
            - "saddle_balanced": Select view with balanced features across multiple metrics
            - "saddle_sim_range": Select view with largest similarity range
    
    Returns:
        b_idx: Tensor of shape (B,) containing the selected view index for each batch
    """
    B, S, N, C = x.shape
    
    # For single view, no reordering needed
    if S <= 1:
        return torch.zeros(B, dtype=torch.long, device=x.device)
    
    # Simple position-based strategies
    if strategy == "first":
        return torch.zeros(B, dtype=torch.long, device=x.device)
    
    elif strategy == "middle":
        return torch.full((B,), S // 2, dtype=torch.long, device=x.device)
    
    # Feature-based strategies require normalized class tokens
    # Extract and normalize class tokens (first token of each view)
    img_class_feat = x[:, :, 0] / x[:, :, 0].norm(dim=-1, keepdim=True)  # B S C
    
    if strategy == "saddle_balanced":
        # Select view with balanced features across multiple metrics
        # Compute similarity matrix
        sim = torch.matmul(img_class_feat, img_class_feat.transpose(1, 2))  # B S S
        sim_no_diag = sim - torch.eye(S, device=sim.device).unsqueeze(0)
        sim_score = sim_no_diag.sum(dim=-1) / (S - 1)  # B S
        
        feat_norm = x[:, :, 0].norm(dim=-1)  # B S
        feat_var = img_class_feat.var(dim=-1)  # B S
        
        # Normalize all metrics to [0, 1]
        def normalize_metric(metric):
            min_val = metric.min(dim=1, keepdim=True).values
            max_val = metric.max(dim=1, keepdim=True).values
            return (metric - min_val) / (max_val - min_val + 1e-8)
        
        sim_score_norm = normalize_metric(sim_score)
        norm_norm = normalize_metric(feat_norm)
        var_norm = normalize_metric(feat_var)
        
        # Select view closest to the median (0.5) across all metrics
        balance_score = (
            (sim_score_norm - 0.5).abs() +
            (norm_norm - 0.5).abs() +
            (var_norm - 0.5).abs()
        )
        b_idx = balance_score.argmin(dim=1)
        
    elif strategy == "saddle_sim_range":
        # Select view with largest similarity range (max - min)
        sim = torch.matmul(img_class_feat, img_class_feat.transpose(1, 2))  # B S S
        sim_no_diag = sim - torch.eye(S, device=sim.device).unsqueeze(0)
        
        sim_max = sim_no_diag.max(dim=-1).values  # B S
        sim_min = sim_no_diag.min(dim=-1).values  # B S
        sim_range = sim_max - sim_min
        b_idx = sim_range.argmax(dim=1)
    
    else:
        raise ValueError(
            f"Unknown reference view selection strategy: {strategy}. "
            f"Must be one of: 'first', 'middle', 'saddle_balanced', 'saddle_sim_range'"
        )
    
    return b_idx


def reorder_by_reference(
    x: torch.Tensor,
    b_idx: torch.Tensor,
) -> torch.Tensor:
    """
    Reorder views to place the selected reference view first.
    
    Args:
        x: Input tensor of shape (B, S, N, C)
        b_idx: Reference view indices of shape (B,)
    
    Returns:
        Reordered tensor with reference view at position 0
    
    Example:
        If b_idx = [2] and S = 5 (views [0,1,2,3,4]),
        result order is [2,0,1,3,4] (ref_idx first, then others in order)
    """
    B, S = x.shape[0], x.shape[1]
    
    # For single view, no reordering needed
    if S <= 1:
        return x
    
    # Create position indices: (B, S) where each row is [0, 1, 2, ..., S-1]
    positions = torch.arange(S, device=x.device).unsqueeze(0).expand(B, -1)  # B S
    
    # For each position, determine which original index it should take
    # Position 0 gets ref_idx
    # Position 1 to ref_idx gets indices 0 to ref_idx-1
    # Position ref_idx+1 to S-1 gets indices ref_idx+1 to S-1
    
    b_idx_expanded = b_idx.unsqueeze(1)  # B 1
    
    # Create the reordering indices
    # For positions 1 to ref_idx: map to indices 0 to ref_idx-1 (shift by -1)
    # For positions > ref_idx: keep the same
    reorder_indices = positions.clone()
    reorder_indices = torch.where(
        (positions > 0) & (positions <= b_idx_expanded),
        positions - 1,
        positions
    )
    # Set position 0 to ref_idx
    reorder_indices[:, 0] = b_idx
    
    # Gather using advanced indexing
    batch_indices = torch.arange(B, device=x.device).unsqueeze(1)  # B 1
    x_reordered = x[batch_indices, reorder_indices]
    
    return x_reordered


def restore_original_order(
    x: torch.Tensor,
    b_idx: torch.Tensor,
) -> torch.Tensor:
    """
    Restore original view order after processing.
    
    Args:
        x: Reordered tensor of shape (B, S, ...)
        b_idx: Original reference view indices of shape (B,)
    
    Returns:
        Tensor with original view order restored
    
    Example:
        If original order was [0, 1, 2, 3, 4] and b_idx=2,
        reordered becomes [2, 0, 1, 3, 4] (reference at position 0),
        restore should return [0, 1, 2, 3, 4] (original order).
    """
    B, S = x.shape[0], x.shape[1]
    
    # For single view, no restoration needed
    if S <= 1:
        return x
    
    # Create target position indices: (B, S) where each row is [0, 1, 2, ..., S-1]
    target_positions = torch.arange(S, device=x.device).unsqueeze(0).expand(B, -1)  # B S
    
    # For each target position, determine which current position it comes from
    # Target position 0 to ref_idx-1 <- Current position 1 to ref_idx (shift by +1)
    # Target position ref_idx <- Current position 0
    # Target position ref_idx+1 to S-1 <- Current position ref_idx+1 to S-1 (no change)
    
    b_idx_expanded = b_idx.unsqueeze(1)  # B 1
    
    # Create the restore indices
    restore_indices = torch.where(
        target_positions < b_idx_expanded,
        target_positions + 1,  # Positions before ref_idx come from current position + 1
        target_positions        # Positions after ref_idx stay the same
    )
    # Target position = ref_idx comes from current position 0
    # Use scatter to set specific positions
    restore_indices = torch.scatter(
        restore_indices,
        dim=1,
        index=b_idx_expanded,
        src=torch.zeros_like(b_idx_expanded)
    )
    
    # Gather using advanced indexing
    batch_indices = torch.arange(B, device=x.device).unsqueeze(1)  # B 1
    x_restored = x[batch_indices, restore_indices]
    
    return x_restored




================================================
FILE: src/depth_anything_3/model/dinov2/dinov2.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates.
#
# This source code is licensed under the Apache License, Version 2.0
# found in the LICENSE file in the root directory of this source tree.

# References:
#   https://github.com/facebookresearch/dino/blob/main/vision_transformer.py
#   https://github.com/rwightman/pytorch-image-models/tree/master/timm/models/vision_transformer.py


from typing import List
import torch.nn as nn

from depth_anything_3.model.dinov2.vision_transformer import (
    vit_base,
    vit_giant2,
    vit_large,
    vit_small,
)


class DinoV2(nn.Module):
    def __init__(
        self,
        name: str,
        out_layers: List[int],
        alt_start: int = -1,
        qknorm_start: int = -1,
        rope_start: int = -1,
        cat_token: bool = True,
        **kwargs,
    ):
        super().__init__()
        assert name in {"vits", "vitb", "vitl", "vitg"}
        self.name = name
        self.out_layers = out_layers
        self.alt_start = alt_start
        self.qknorm_start = qknorm_start
        self.rope_start = rope_start
        self.cat_token = cat_token
        encoder_map = {
            "vits": vit_small,
            "vitb": vit_base,
            "vitl": vit_large,
            "vitg": vit_giant2,
        }
        encoder_fn = encoder_map[self.name]
        ffn_layer = "swiglufused" if self.name == "vitg" else "mlp"
        self.pretrained = encoder_fn(
            img_size=518,
            patch_size=14,
            ffn_layer=ffn_layer,
            alt_start=alt_start,
            qknorm_start=qknorm_start,
            rope_start=rope_start,
            cat_token=cat_token,
        )

    def forward(self, x, **kwargs):
        return self.pretrained.get_intermediate_layers(
            x,
            self.out_layers,
            **kwargs,
        )



================================================
FILE: src/depth_anything_3/model/dinov2/vision_transformer.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates.
#
# This source code is licensed under the Apache License, Version 2.0
# found in the LICENSE file in the root directory of this source tree.

# References:
#   https://github.com/facebookresearch/dino/blob/main/vision_transformer.py
#   https://github.com/rwightman/pytorch-image-models/tree/master/timm/models/vision_transformer.py

import math
from typing import Callable, List, Sequence, Tuple, Union
import numpy as np
import torch
import torch.nn as nn
import torch.utils.checkpoint
from einops import rearrange

from depth_anything_3.utils.logger import logger

from .layers import LayerScale  # noqa: F401
from .layers import Mlp  # noqa: F401
from .layers import (  # noqa: F401
    Block,
    PatchEmbed,
    PositionGetter,
    RotaryPositionEmbedding2D,
    SwiGLUFFNFused,
)
from depth_anything_3.model.reference_view_selector import (
    RefViewStrategy,
    select_reference_view,
    reorder_by_reference,
    restore_original_order,
)
from depth_anything_3.utils.constants import THRESH_FOR_REF_SELECTION

# logger = logging.getLogger("dinov2")


def get_1d_sincos_pos_embed_from_grid(embed_dim, pos):
    """
    embed_dim: output dimension for each position
    pos: a list of positions to be encoded: size (M,)
    out: (M, D)
    """
    assert embed_dim % 2 == 0
    omega = np.arange(embed_dim // 2, dtype=float)
    omega /= embed_dim / 2.0
    omega = 1.0 / 10000**omega  # (D/2,)

    pos = pos.reshape(-1)  # (M,)
    out = np.einsum("m,d->md", pos, omega)  # (M, D/2), outer product

    emb_sin = np.sin(out)  # (M, D/2)
    emb_cos = np.cos(out)  # (M, D/2)

    emb = np.concatenate([emb_sin, emb_cos], axis=1)  # (M, D)
    return emb


def named_apply(
    fn: Callable, module: nn.Module, name="", depth_first=True, include_root=False
) -> nn.Module:
    if not depth_first and include_root:
        fn(module=module, name=name)
    for child_name, child_module in module.named_children():
        child_name = ".".join((name, child_name)) if name else child_name
        named_apply(
            fn=fn, module=child_module, name=child_name, depth_first=depth_first, include_root=True
        )
    if depth_first and include_root:
        fn(module=module, name=name)
    return module


class BlockChunk(nn.ModuleList):
    def forward(self, x):
        for b in self:
            x = b(x)
        return x


class DinoVisionTransformer(nn.Module):
    def __init__(
        self,
        img_size=224,
        patch_size=16,
        in_chans=3,
        embed_dim=768,
        depth=12,
        num_heads=12,
        mlp_ratio=4.0,
        qkv_bias=True,
        ffn_bias=True,
        proj_bias=True,
        drop_path_rate=0.0,
        drop_path_uniform=False,
        init_values=1.0,  # for layerscale: None or 0 => no layerscale
        embed_layer=PatchEmbed,
        act_layer=nn.GELU,
        block_fn=Block,
        ffn_layer="mlp",
        block_chunks=1,
        num_register_tokens=0,
        interpolate_antialias=False,
        interpolate_offset=0.1,
        alt_start=-1,
        qknorm_start=-1,
        rope_start=-1,
        rope_freq=100,
        plus_cam_token=False,
        cat_token=True,
    ):
        """
        Args:
            img_size (int, tuple): input image size
            patch_size (int, tuple): patch size
            in_chans (int): number of input channels
            embed_dim (int): embedding dimension
            depth (int): depth of transformer
            num_heads (int): number of attention heads
            mlp_ratio (int): ratio of mlp hidden dim to embedding dim
            qkv_bias (bool): enable bias for qkv if True
            proj_bias (bool): enable bias for proj in attn if True
            ffn_bias (bool): enable bias for ffn if True
            weight_init (str): weight init scheme
            init_values (float): layer-scale init values
            embed_layer (nn.Module): patch embedding layer
            act_layer (nn.Module): MLP activation layer
            block_fn (nn.Module): transformer block class
            ffn_layer (str): "mlp", "swiglu", "swiglufused" or "identity"
            block_chunks: (int) split block sequence into block_chunks units for FSDP wrap
            num_register_tokens: (int) number of extra cls tokens (so-called "registers")
            interpolate_antialias: (str) flag to apply anti-aliasing when interpolating
                positional embeddings
            interpolate_offset: (float) work-around offset to apply when interpolating
                positional embeddings
        """
        super().__init__()
        self.patch_start_idx = 1
        norm_layer = nn.LayerNorm
        self.num_features = self.embed_dim = (
            embed_dim  # num_features for consistency with other models
        )
        self.alt_start = alt_start
        self.qknorm_start = qknorm_start
        self.rope_start = rope_start
        self.cat_token = cat_token
        self.num_tokens = 1
        self.n_blocks = depth
        self.num_heads = num_heads
        self.patch_size = patch_size
        self.num_register_tokens = num_register_tokens
        self.interpolate_antialias = interpolate_antialias
        self.interpolate_offset = interpolate_offset

        self.patch_embed = embed_layer(
            img_size=img_size, patch_size=patch_size, in_chans=in_chans, embed_dim=embed_dim
        )
        num_patches = self.patch_embed.num_patches
        self.cls_token = nn.Parameter(torch.zeros(1, 1, embed_dim))
        if self.alt_start != -1:
            self.camera_token = nn.Parameter(torch.randn(1, 2, embed_dim))
        self.pos_embed = nn.Parameter(torch.zeros(1, num_patches + self.num_tokens, embed_dim))
        assert num_register_tokens >= 0
        self.register_tokens = (
            nn.Parameter(torch.zeros(1, num_register_tokens, embed_dim))
            if num_register_tokens
            else None
        )

        if drop_path_uniform is True:
            dpr = [drop_path_rate] * depth
        else:
            dpr = [
                x.item() for x in torch.linspace(0, drop_path_rate, depth)
            ]  # stochastic depth decay rule
        if ffn_layer == "mlp":
            logger.info("using MLP layer as FFN")
            ffn_layer = Mlp
        elif ffn_layer == "swiglufused" or ffn_layer == "swiglu":
            logger.info("using SwiGLU layer as FFN")
            ffn_layer = SwiGLUFFNFused
        elif ffn_layer == "identity":
            logger.info("using Identity layer as FFN")

            def f(*args, **kwargs):
                return nn.Identity()

            ffn_layer = f
        else:
            raise NotImplementedError

        if self.rope_start != -1:
            self.rope = RotaryPositionEmbedding2D(frequency=rope_freq) if rope_freq > 0 else None
            self.position_getter = PositionGetter() if self.rope is not None else None
        else:
            self.rope = None
        blocks_list = [
            block_fn(
                dim=embed_dim,
                num_heads=num_heads,
                mlp_ratio=mlp_ratio,
                qkv_bias=qkv_bias,
                proj_bias=proj_bias,
                ffn_bias=ffn_bias,
                drop_path=dpr[i],
                norm_layer=norm_layer,
                act_layer=act_layer,
                ffn_layer=ffn_layer,
                init_values=init_values,
                qk_norm=i >= qknorm_start if qknorm_start != -1 else False,
                rope=self.rope if i >= rope_start and rope_start != -1 else None,
            )
            for i in range(depth)
        ]
        self.blocks = nn.ModuleList(blocks_list)
        self.norm = norm_layer(embed_dim)

    def interpolate_pos_encoding(self, x, w, h):
        previous_dtype = x.dtype
        npatch = x.shape[1] - 1
        N = self.pos_embed.shape[1] - 1
        if npatch == N and w == h:
            return self.pos_embed
        pos_embed = self.pos_embed.float()
        class_pos_embed = pos_embed[:, 0]
        patch_pos_embed = pos_embed[:, 1:]
        dim = x.shape[-1]
        w0 = w // self.patch_size
        h0 = h // self.patch_size
        M = int(math.sqrt(N))  # Recover the number of patches in each dimension
        assert N == M * M
        kwargs = {}
        if self.interpolate_offset:
            # Historical kludge: add a small number to avoid floating point error in the
            # interpolation, see https://github.com/facebookresearch/dino/issues/8
            # Note: still needed for backward-compatibility, the underlying operators are using
            # both output size and scale factors
            sx = float(w0 + self.interpolate_offset) / M
            sy = float(h0 + self.interpolate_offset) / M
            kwargs["scale_factor"] = (sx, sy)
        else:
            # Simply specify an output size instead of a scale factor
            kwargs["size"] = (w0, h0)
        patch_pos_embed = nn.functional.interpolate(
            patch_pos_embed.reshape(1, M, M, dim).permute(0, 3, 1, 2),
            mode="bicubic",
            antialias=self.interpolate_antialias,
            **kwargs,
        )
        assert (w0, h0) == patch_pos_embed.shape[-2:]
        patch_pos_embed = patch_pos_embed.permute(0, 2, 3, 1).view(1, -1, dim)
        return torch.cat((class_pos_embed.unsqueeze(0), patch_pos_embed), dim=1).to(previous_dtype)

    def prepare_cls_token(self, B, S):
        cls_token = self.cls_token.expand(B, S, -1)
        cls_token = cls_token.reshape(B * S, -1, self.embed_dim)
        return cls_token

    def prepare_tokens_with_masks(self, x, masks=None, cls_token=None, **kwargs):
        B, S, nc, w, h = x.shape
        x = rearrange(x, "b s c h w -> (b s) c h w")
        x = self.patch_embed(x)
        if masks is not None:
            x = torch.where(masks.unsqueeze(-1), self.mask_token.to(x.dtype).unsqueeze(0), x)
        cls_token = self.prepare_cls_token(B, S)
        x = torch.cat((cls_token, x), dim=1)
        x = x + self.interpolate_pos_encoding(x, w, h)
        if self.register_tokens is not None:
            x = torch.cat(
                (
                    x[:, :1],
                    self.register_tokens.expand(x.shape[0], -1, -1),
                    x[:, 1:],
                ),
                dim=1,
            )
        x = rearrange(x, "(b s) n c -> b s n c", b=B, s=S)
        return x

    def _prepare_rope(self, B, S, H, W, device):
        pos = None
        pos_nodiff = None
        if self.rope is not None:
            pos = self.position_getter(
                B * S, H // self.patch_size, W // self.patch_size, device=device
            )
            pos = rearrange(pos, "(b s) n c -> b s n c", b=B)
            pos_nodiff = torch.zeros_like(pos).to(pos.dtype)
            if self.patch_start_idx > 0:
                pos = pos + 1
                pos_special = torch.zeros(B * S, self.patch_start_idx, 2).to(device).to(pos.dtype)
                pos_special = rearrange(pos_special, "(b s) n c -> b s n c", b=B)
                pos = torch.cat([pos_special, pos], dim=2)
                pos_nodiff = pos_nodiff + 1
                pos_nodiff = torch.cat([pos_special, pos_nodiff], dim=2)
        return pos, pos_nodiff

    def _get_intermediate_layers_not_chunked(self, x, n=1, export_feat_layers=[], **kwargs):
        B, S, _, H, W = x.shape
        x = self.prepare_tokens_with_masks(x)
        output, total_block_len, aux_output = [], len(self.blocks), []
        blocks_to_take = range(total_block_len - n, total_block_len) if isinstance(n, int) else n
        pos, pos_nodiff = self._prepare_rope(B, S, H, W, x.device)

        for i, blk in enumerate(self.blocks):
            if i < self.rope_start or self.rope is None:
                g_pos, l_pos = None, None
            else:
                g_pos = pos_nodiff
                l_pos = pos

            if self.alt_start != -1 and (i == self.alt_start - 1) and x.shape[1] >= THRESH_FOR_REF_SELECTION and kwargs.get("cam_token", None) is None:
                # Select reference view using configured strategy
                strategy = kwargs.get("ref_view_strategy", "saddle_balanced")
                logger.info(f"Selecting reference view using strategy: {strategy}")
                b_idx = select_reference_view(x, strategy=strategy)
                # Reorder views to place reference view first
                x = reorder_by_reference(x, b_idx)
                local_x = reorder_by_reference(local_x, b_idx)

            if self.alt_start != -1 and i == self.alt_start:
                if kwargs.get("cam_token", None) is not None:
                    logger.info("Using camera conditions provided by the user")
                    cam_token = kwargs.get("cam_token")
                else:
                    ref_token = self.camera_token[:, :1].expand(B, -1, -1)
                    src_token = self.camera_token[:, 1:].expand(B, S - 1, -1)
                    cam_token = torch.cat([ref_token, src_token], dim=1)
                x[:, :, 0] = cam_token

            if self.alt_start != -1 and i >= self.alt_start and i % 2 == 1:
                x = self.process_attention(
                    x, blk, "global", pos=g_pos, attn_mask=kwargs.get("attn_mask", None)
                )
            else:
                x = self.process_attention(x, blk, "local", pos=l_pos)
                local_x = x

            if i in blocks_to_take:
                out_x = torch.cat([local_x, x], dim=-1) if self.cat_token else x
                # Restore original view order if reordering was applied
                if x.shape[1] >= THRESH_FOR_REF_SELECTION and self.alt_start != -1 and 'b_idx' in locals():
                    out_x = restore_original_order(out_x, b_idx)
                output.append((out_x[:, :, 0], out_x))
            if i in export_feat_layers:
                aux_output.append(x)
        return output, aux_output

    def process_attention(self, x, block, attn_type="global", pos=None, attn_mask=None):
        b, s, n = x.shape[:3]
        if attn_type == "local":
            x = rearrange(x, "b s n c -> (b s) n c")
            if pos is not None:
                pos = rearrange(pos, "b s n c -> (b s) n c")
        elif attn_type == "global":
            x = rearrange(x, "b s n c -> b (s n) c")
            if pos is not None:
                pos = rearrange(pos, "b s n c -> b (s n) c")
        else:
            raise ValueError(f"Invalid attention type: {attn_type}")

        x = block(x, pos=pos, attn_mask=attn_mask)

        if attn_type == "local":
            x = rearrange(x, "(b s) n c -> b s n c", b=b, s=s)
        elif attn_type == "global":
            x = rearrange(x, "b (s n) c -> b s n c", b=b, s=s)
        return x

    def get_intermediate_layers(
        self,
        x: torch.Tensor,
        n: Union[int, Sequence] = 1,  # Layers or n last layers to take
        export_feat_layers: List[int] = [],
        **kwargs,
    ) -> Tuple[Union[torch.Tensor, Tuple[torch.Tensor]]]:
        outputs, aux_outputs = self._get_intermediate_layers_not_chunked(
            x, n, export_feat_layers=export_feat_layers, **kwargs
        )
        camera_tokens = [out[0] for out in outputs]
        if outputs[0][1].shape[-1] == self.embed_dim:
            outputs = [self.norm(out[1]) for out in outputs]
        elif outputs[0][1].shape[-1] == (self.embed_dim * 2):
            outputs = [
                torch.cat(
                    [out[1][..., : self.embed_dim], self.norm(out[1][..., self.embed_dim :])],
                    dim=-1,
                )
                for out in outputs
            ]
        else:
            raise ValueError(f"Invalid output shape: {outputs[0][1].shape}")
        aux_outputs = [self.norm(out) for out in aux_outputs]
        outputs = [out[..., 1 + self.num_register_tokens :, :] for out in outputs]
        aux_outputs = [out[..., 1 + self.num_register_tokens :, :] for out in aux_outputs]
        return tuple(zip(outputs, camera_tokens)), aux_outputs


def vit_small(patch_size=16, num_register_tokens=0, depth=12, **kwargs):
    model = DinoVisionTransformer(
        patch_size=patch_size,
        embed_dim=384,
        depth=depth,
        num_heads=6,
        mlp_ratio=4,
        # block_fn=partial(Block, attn_class=MemEffAttention),
        num_register_tokens=num_register_tokens,
        **kwargs,
    )
    return model


def vit_base(patch_size=16, num_register_tokens=0, depth=12, **kwargs):
    model = DinoVisionTransformer(
        patch_size=patch_size,
        embed_dim=768,
        depth=depth,
        num_heads=12,
        mlp_ratio=4,
        # block_fn=partial(Block, attn_class=MemEffAttention),
        num_register_tokens=num_register_tokens,
        **kwargs,
    )
    return model


def vit_large(patch_size=16, num_register_tokens=0, depth=24, **kwargs):
    model = DinoVisionTransformer(
        patch_size=patch_size,
        embed_dim=1024,
        depth=depth,
        num_heads=16,
        mlp_ratio=4,
        # block_fn=partial(Block, attn_class=MemEffAttention),
        num_register_tokens=num_register_tokens,
        **kwargs,
    )
    return model


def vit_giant2(patch_size=16, num_register_tokens=0, depth=40, **kwargs):
    """
    Close to ViT-giant, with embed-dim 1536 and 24 heads => embed-dim per head 64
    """
    model = DinoVisionTransformer(
        patch_size=patch_size,
        embed_dim=1536,
        depth=depth,
        num_heads=24,
        mlp_ratio=4,
        num_register_tokens=num_register_tokens,
        **kwargs,
    )
    return model



================================================
FILE: src/depth_anything_3/model/dinov2/layers/__init__.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates.
# All rights reserved.
#
# This source code is licensed under the license found in the
# LICENSE file in the root directory of this source tree.

# from .attention import MemEffAttention
from .block import Block
from .layer_scale import LayerScale
from .mlp import Mlp
from .patch_embed import PatchEmbed
from .rope import PositionGetter, RotaryPositionEmbedding2D
from .swiglu_ffn import SwiGLUFFN, SwiGLUFFNFused

__all__ = [
    Mlp,
    PatchEmbed,
    SwiGLUFFN,
    SwiGLUFFNFused,
    Block,
    # MemEffAttention,
    LayerScale,
    PositionGetter,
    RotaryPositionEmbedding2D,
]



================================================
FILE: src/depth_anything_3/model/dinov2/layers/attention.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates.
# All rights reserved.
#
# This source code is licensed under the license found in the
# LICENSE file in the root directory of this source tree.

# References:
#   https://github.com/facebookresearch/dino/blob/master/vision_transformer.py
#   https://github.com/rwightman/pytorch-image-models/tree/master/timm/models/vision_transformer.py

import logging
import torch.nn.functional as F
from torch import Tensor, nn

logger = logging.getLogger("dinov2")


class Attention(nn.Module):
    def __init__(
        self,
        dim: int,
        num_heads: int = 8,
        qkv_bias: bool = False,
        proj_bias: bool = True,
        attn_drop: float = 0.0,
        proj_drop: float = 0.0,
        norm_layer: nn.Module = nn.LayerNorm,
        qk_norm: bool = False,
        fused_attn: bool = True,  # use F.scaled_dot_product_attention or not
        rope=None,
    ) -> None:
        super().__init__()
        assert dim % num_heads == 0, "dim should be divisible by num_heads"
        self.num_heads = num_heads
        head_dim = dim // num_heads
        self.scale = head_dim**-0.5
        self.fused_attn = fused_attn

        self.qkv = nn.Linear(dim, dim * 3, bias=qkv_bias)
        self.q_norm = norm_layer(head_dim) if qk_norm else nn.Identity()
        self.k_norm = norm_layer(head_dim) if qk_norm else nn.Identity()
        self.attn_drop = nn.Dropout(attn_drop)
        self.proj = nn.Linear(dim, dim, bias=proj_bias)
        self.proj_drop = nn.Dropout(proj_drop)
        self.rope = rope

    def forward(self, x: Tensor, pos=None, attn_mask=None) -> Tensor:
        B, N, C = x.shape
        qkv = (
            self.qkv(x)
            .reshape(B, N, 3, self.num_heads, C // self.num_heads)
            .permute(2, 0, 3, 1, 4)
        )
        q, k, v = qkv[0], qkv[1], qkv[2]
        q, k = self.q_norm(q), self.k_norm(k)
        if self.rope is not None and pos is not None:
            q = self.rope(q, pos)
            k = self.rope(k, pos)
        if self.fused_attn:
            x = F.scaled_dot_product_attention(
                q,
                k,
                v,
                dropout_p=self.attn_drop.p if self.training else 0.0,
                attn_mask=(
                    (attn_mask)[:, None].repeat(1, self.num_heads, 1, 1)
                    if attn_mask is not None
                    else None
                ),
            )
        else:
            q = q * self.scale
            attn = q @ k.transpose(-2, -1)
            attn = attn.softmax(dim=-1)
            attn = self.attn_drop(attn)
            x = attn @ v

        x = x.transpose(1, 2).reshape(B, N, C)
        x = self.proj(x)
        x = self.proj_drop(x)
        return x

    def _forward(self, x: Tensor) -> Tensor:
        B, N, C = x.shape
        qkv = (
            self.qkv(x)
            .reshape(B, N, 3, self.num_heads, C // self.num_heads)
            .permute(2, 0, 3, 1, 4)
        )

        q, k, v = qkv[0] * self.scale, qkv[1], qkv[2]
        attn = q @ k.transpose(-2, -1)

        attn = attn.softmax(dim=-1)
        attn = self.attn_drop(attn)

        x = (attn @ v).transpose(1, 2).reshape(B, N, C)
        x = self.proj(x)
        x = self.proj_drop(x)
        return x



================================================
FILE: src/depth_anything_3/model/dinov2/layers/block.py
================================================
# flake8: noqa: F821
# Copyright (c) Meta Platforms, Inc. and affiliates.
# All rights reserved.
#
# This source code is licensed under the license found in the
# LICENSE file in the root directory of this source tree.

# References:
#   https://github.com/facebookresearch/dino/blob/master/vision_transformer.py
#   https://github.com/rwightman/pytorch-image-models/tree/master/timm/layers/patch_embed.py

import logging
from typing import Callable, Optional
import torch
from torch import Tensor, nn

from .attention import Attention
from .drop_path import DropPath
from .layer_scale import LayerScale
from .mlp import Mlp

logger = logging.getLogger("dinov2")
XFORMERS_AVAILABLE = True


class Block(nn.Module):
    def __init__(
        self,
        dim: int,
        num_heads: int,
        mlp_ratio: float = 4.0,
        qkv_bias: bool = False,
        proj_bias: bool = True,
        ffn_bias: bool = True,
        drop: float = 0.0,
        attn_drop: float = 0.0,
        init_values=None,
        drop_path: float = 0.0,
        act_layer: Callable[..., nn.Module] = nn.GELU,
        norm_layer: Callable[..., nn.Module] = nn.LayerNorm,
        attn_class: Callable[..., nn.Module] = Attention,
        ffn_layer: Callable[..., nn.Module] = Mlp,
        qk_norm: bool = False,
        rope=None,
        ln_eps: float = 1e-6,
    ) -> None:
        super().__init__()
        # print(f"biases: qkv: {qkv_bias}, proj: {proj_bias}, ffn: {ffn_bias}")
        self.norm1 = norm_layer(dim, eps=ln_eps)
        self.attn = attn_class(
            dim,
            num_heads=num_heads,
            qkv_bias=qkv_bias,
            proj_bias=proj_bias,
            attn_drop=attn_drop,
            proj_drop=drop,
            qk_norm=qk_norm,
            rope=rope,
        )
        self.ls1 = LayerScale(dim, init_values=init_values) if init_values else nn.Identity()
        self.drop_path1 = DropPath(drop_path) if drop_path > 0.0 else nn.Identity()

        self.norm2 = norm_layer(dim, eps=ln_eps)
        mlp_hidden_dim = int(dim * mlp_ratio)
        self.mlp = ffn_layer(
            in_features=dim,
            hidden_features=mlp_hidden_dim,
            act_layer=act_layer,
            drop=drop,
            bias=ffn_bias,
        )
        self.ls2 = LayerScale(dim, init_values=init_values) if init_values else nn.Identity()
        self.drop_path2 = DropPath(drop_path) if drop_path > 0.0 else nn.Identity()

        self.sample_drop_ratio = drop_path

    def forward(self, x: Tensor, pos=None, attn_mask=None) -> Tensor:
        def attn_residual_func(x: Tensor, pos=None, attn_mask=None) -> Tensor:
            return self.ls1(self.attn(self.norm1(x), pos=pos, attn_mask=attn_mask))

        def ffn_residual_func(x: Tensor) -> Tensor:
            return self.ls2(self.mlp(self.norm2(x)))

        if self.training and self.sample_drop_ratio > 0.1:
            # the overhead is compensated only for a drop path rate larger than 0.1
            x = drop_add_residual_stochastic_depth(
                x,
                residual_func=attn_residual_func,
                sample_drop_ratio=self.sample_drop_ratio,
                pos=pos,
            )
            x = drop_add_residual_stochastic_depth(
                x,
                residual_func=ffn_residual_func,
                sample_drop_ratio=self.sample_drop_ratio,
            )
        elif self.training and self.sample_drop_ratio > 0.0:
            x = x + self.drop_path1(attn_residual_func(x, pos=pos, attn_mask=attn_mask))
            x = x + self.drop_path1(ffn_residual_func(x))  # FIXME: drop_path2
        else:
            x = x + attn_residual_func(x, pos=pos, attn_mask=attn_mask)
            x = x + ffn_residual_func(x)
        return x


def drop_add_residual_stochastic_depth(
    x: Tensor,
    residual_func: Callable[[Tensor], Tensor],
    sample_drop_ratio: float = 0.0,
    pos: Optional[Tensor] = None,
) -> Tensor:
    # 1) extract subset using permutation
    b, n, d = x.shape
    sample_subset_size = max(int(b * (1 - sample_drop_ratio)), 1)
    brange = (torch.randperm(b, device=x.device))[:sample_subset_size]
    x_subset = x[brange]

    # 2) apply residual_func to get residual
    if pos is not None:
        # if necessary, apply rope to the subset
        pos = pos[brange]
        residual = residual_func(x_subset, pos=pos)
    else:
        residual = residual_func(x_subset)

    x_flat = x.flatten(1)
    residual = residual.flatten(1)

    residual_scale_factor = b / sample_subset_size

    # 3) add the residual
    x_plus_residual = torch.index_add(
        x_flat, 0, brange, residual.to(dtype=x.dtype), alpha=residual_scale_factor
    )
    return x_plus_residual.view_as(x)


def get_branges_scales(x, sample_drop_ratio=0.0):
    b, n, d = x.shape
    sample_subset_size = max(int(b * (1 - sample_drop_ratio)), 1)
    brange = (torch.randperm(b, device=x.device))[:sample_subset_size]
    residual_scale_factor = b / sample_subset_size
    return brange, residual_scale_factor



================================================
FILE: src/depth_anything_3/model/dinov2/layers/drop_path.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates.
# All rights reserved.
#
# This source code is licensed under the license found in the
# LICENSE file in the root directory of this source tree.

# References:
#   https://github.com/facebookresearch/dino/blob/master/vision_transformer.py
#   https://github.com/rwightman/pytorch-image-models/tree/master/timm/layers/drop.py


from torch import nn


def drop_path(x, drop_prob: float = 0.0, training: bool = False):
    if drop_prob == 0.0 or not training:
        return x
    keep_prob = 1 - drop_prob
    shape = (x.shape[0],) + (1,) * (x.ndim - 1)  # work with diff dim tensors, not just 2D ConvNets
    random_tensor = x.new_empty(shape).bernoulli_(keep_prob)
    if keep_prob > 0.0:
        random_tensor.div_(keep_prob)
    output = x * random_tensor
    return output


class DropPath(nn.Module):
    """Drop paths (Stochastic Depth) per sample (when applied in main path of residual blocks)."""

    def __init__(self, drop_prob=None):
        super().__init__()
        self.drop_prob = drop_prob

    def forward(self, x):
        return drop_path(x, self.drop_prob, self.training)



================================================
FILE: src/depth_anything_3/model/dinov2/layers/layer_scale.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates.
# All rights reserved.
#
# This source code is licensed under the license found in the
# LICENSE file in the root directory of this source tree.

# Modified from: https://github.com/huggingface/pytorch-image-models/blob/main/timm/models/vision_transformer.py#L103-L110  # noqa: E501

from typing import Union
import torch
from torch import Tensor, nn


class LayerScale(nn.Module):
    def __init__(
        self,
        dim: int,
        init_values: Union[float, Tensor] = 1e-5,
        inplace: bool = False,
    ) -> None:
        super().__init__()
        self.dim = dim
        self.inplace = inplace
        self.init_values = init_values
        self.gamma = nn.Parameter(init_values * torch.ones(dim))

    def forward(self, x: Tensor) -> Tensor:
        return x.mul_(self.gamma) if self.inplace else x * self.gamma

    def extra_repr(self) -> str:
        return f"{self.dim}, init_values={self.init_values}, inplace={self.inplace}"



================================================
FILE: src/depth_anything_3/model/dinov2/layers/mlp.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates.
# All rights reserved.
#
# This source code is licensed under the license found in the
# LICENSE file in the root directory of this source tree.

# References:
#   https://github.com/facebookresearch/dino/blob/master/vision_transformer.py
#   https://github.com/rwightman/pytorch-image-models/tree/master/timm/layers/mlp.py


from typing import Callable, Optional
from torch import Tensor, nn


class Mlp(nn.Module):
    def __init__(
        self,
        in_features: int,
        hidden_features: Optional[int] = None,
        out_features: Optional[int] = None,
        act_layer: Callable[..., nn.Module] = nn.GELU,
        drop: float = 0.0,
        bias: bool = True,
    ) -> None:
        super().__init__()
        out_features = out_features or in_features
        hidden_features = hidden_features or in_features
        self.fc1 = nn.Linear(in_features, hidden_features, bias=bias)
        self.act = act_layer()
        self.fc2 = nn.Linear(hidden_features, out_features, bias=bias)
        self.drop = nn.Dropout(drop)

    def forward(self, x: Tensor) -> Tensor:
        x = self.fc1(x)
        x = self.act(x)
        x = self.drop(x)
        x = self.fc2(x)
        x = self.drop(x)
        return x



================================================
FILE: src/depth_anything_3/model/dinov2/layers/patch_embed.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates.
# All rights reserved.
#
# This source code is licensed under the license found in the
# LICENSE file in the root directory of this source tree.

# References:
#   https://github.com/facebookresearch/dino/blob/master/vision_transformer.py
#   https://github.com/rwightman/pytorch-image-models/tree/master/timm/layers/patch_embed.py

from typing import Callable, Optional, Tuple, Union
import torch.nn as nn
from torch import Tensor


def make_2tuple(x):
    if isinstance(x, tuple):
        assert len(x) == 2
        return x

    assert isinstance(x, int)
    return (x, x)


class PatchEmbed(nn.Module):
    """
    2D image to patch embedding: (B,C,H,W) -> (B,N,D)

    Args:
        img_size: Image size.
        patch_size: Patch token size.
        in_chans: Number of input image channels.
        embed_dim: Number of linear projection output channels.
        norm_layer: Normalization layer.
    """

    def __init__(
        self,
        img_size: Union[int, Tuple[int, int]] = 224,
        patch_size: Union[int, Tuple[int, int]] = 16,
        in_chans: int = 3,
        embed_dim: int = 768,
        norm_layer: Optional[Callable] = None,
        flatten_embedding: bool = True,
    ) -> None:
        super().__init__()

        image_HW = make_2tuple(img_size)
        patch_HW = make_2tuple(patch_size)
        patch_grid_size = (
            image_HW[0] // patch_HW[0],
            image_HW[1] // patch_HW[1],
        )

        self.img_size = image_HW
        self.patch_size = patch_HW
        self.patches_resolution = patch_grid_size
        self.num_patches = patch_grid_size[0] * patch_grid_size[1]

        self.in_chans = in_chans
        self.embed_dim = embed_dim

        self.flatten_embedding = flatten_embedding

        self.proj = nn.Conv2d(in_chans, embed_dim, kernel_size=patch_HW, stride=patch_HW)
        self.norm = norm_layer(embed_dim) if norm_layer else nn.Identity()

    def forward(self, x: Tensor) -> Tensor:
        _, _, H, W = x.shape
        patch_H, patch_W = self.patch_size

        assert (
            H % patch_H == 0
        ), f"Input image height {H} is not a multiple of patch height {patch_H}"
        assert (
            W % patch_W == 0
        ), f"Input image width {W} is not a multiple of patch width: {patch_W}"

        x = self.proj(x)  # B C H W
        H, W = x.size(2), x.size(3)
        x = x.flatten(2).transpose(1, 2)  # B HW C
        x = self.norm(x)
        if not self.flatten_embedding:
            x = x.reshape(-1, H, W, self.embed_dim)  # B H W C
        return x

    def flops(self) -> float:
        Ho, Wo = self.patches_resolution
        flops = (
            Ho * Wo * self.embed_dim * self.in_chans * (self.patch_size[0] * self.patch_size[1])
        )
        if self.norm is not None:
            flops += Ho * Wo * self.embed_dim
        return flops



================================================
FILE: src/depth_anything_3/model/dinov2/layers/rope.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates.
#
# This source code is licensed under the Apache License, Version 2.0
# found in the LICENSE file in the root directory of this source tree.


# Implementation of 2D Rotary Position Embeddings (RoPE).

# This module provides a clean implementation of 2D Rotary Position Embeddings,
# which extends the original RoPE concept to handle 2D spatial positions.

# Inspired by:
#         https://github.com/meta-llama/codellama/blob/main/llama/model.py
#         https://github.com/naver-ai/rope-vit


from typing import Dict, Tuple
import torch
import torch.nn as nn
import torch.nn.functional as F


class PositionGetter:
    """Generates and caches 2D spatial positions for patches in a grid.

    This class efficiently manages the generation of spatial coordinates for patches
    in a 2D grid, caching results to avoid redundant computations.

    Attributes:
        position_cache: Dictionary storing precomputed position tensors for different
            grid dimensions.
    """

    def __init__(self):
        """Initializes the position generator with an empty cache."""
        self.position_cache: Dict[Tuple[int, int], torch.Tensor] = {}

    def __call__(
        self, batch_size: int, height: int, width: int, device: torch.device
    ) -> torch.Tensor:
        """Generates spatial positions for a batch of patches.

        Args:
            batch_size: Number of samples in the batch.
            height: Height of the grid in patches.
            width: Width of the grid in patches.
            device: Target device for the position tensor.

        Returns:
            Tensor of shape (batch_size, height*width, 2) containing y,x coordinates
            for each position in the grid, repeated for each batch item.
        """
        if (height, width) not in self.position_cache:
            y_coords = torch.arange(height, device=device)
            x_coords = torch.arange(width, device=device)
            positions = torch.cartesian_prod(y_coords, x_coords)
            self.position_cache[height, width] = positions

        cached_positions = self.position_cache[height, width]
        return cached_positions.view(1, height * width, 2).expand(batch_size, -1, -1).clone()


class RotaryPositionEmbedding2D(nn.Module):
    """2D Rotary Position Embedding implementation.

    This module applies rotary position embeddings to input tokens based on their
    2D spatial positions. It handles the position-dependent rotation of features
    separately for vertical and horizontal dimensions.

    Args:
        frequency: Base frequency for the position embeddings. Default: 100.0
        scaling_factor: Scaling factor for frequency computation. Default: 1.0

    Attributes:
        base_frequency: Base frequency for computing position embeddings.
        scaling_factor: Factor to scale the computed frequencies.
        frequency_cache: Cache for storing precomputed frequency components.
    """

    def __init__(self, frequency: float = 100.0, scaling_factor: float = 1.0):
        """Initializes the 2D RoPE module."""
        super().__init__()
        self.base_frequency = frequency
        self.scaling_factor = scaling_factor
        self.frequency_cache: Dict[Tuple, Tuple[torch.Tensor, torch.Tensor]] = {}

    def _compute_frequency_components(
        self, dim: int, seq_len: int, device: torch.device, dtype: torch.dtype
    ) -> Tuple[torch.Tensor, torch.Tensor]:
        """Computes frequency components for rotary embeddings.

        Args:
            dim: Feature dimension (must be even).
            seq_len: Maximum sequence length.
            device: Target device for computations.
            dtype: Data type for the computed tensors.

        Returns:
            Tuple of (cosine, sine) tensors for frequency components.
        """
        cache_key = (dim, seq_len, device, dtype)
        if cache_key not in self.frequency_cache:
            # Compute frequency bands
            exponents = torch.arange(0, dim, 2, device=device).float() / dim
            inv_freq = 1.0 / (self.base_frequency**exponents)

            # Generate position-dependent frequencies
            positions = torch.arange(seq_len, device=device, dtype=inv_freq.dtype)
            angles = torch.einsum("i,j->ij", positions, inv_freq)

            # Compute and cache frequency components
            angles = angles.to(dtype)
            angles = torch.cat((angles, angles), dim=-1)
            cos_components = angles.cos().to(dtype)
            sin_components = angles.sin().to(dtype)
            self.frequency_cache[cache_key] = (cos_components, sin_components)

        return self.frequency_cache[cache_key]

    @staticmethod
    def _rotate_features(x: torch.Tensor) -> torch.Tensor:
        """Performs feature rotation by splitting and recombining feature dimensions.

        Args:
            x: Input tensor to rotate.

        Returns:
            Rotated feature tensor.
        """
        feature_dim = x.shape[-1]
        x1, x2 = x[..., : feature_dim // 2], x[..., feature_dim // 2 :]
        return torch.cat((-x2, x1), dim=-1)

    def _apply_1d_rope(
        self,
        tokens: torch.Tensor,
        positions: torch.Tensor,
        cos_comp: torch.Tensor,
        sin_comp: torch.Tensor,
    ) -> torch.Tensor:
        """Applies 1D rotary position embeddings along one dimension.

        Args:
            tokens: Input token features.
            positions: Position indices.
            cos_comp: Cosine components for rotation.
            sin_comp: Sine components for rotation.

        Returns:
            Tokens with applied rotary position embeddings.
        """
        # Embed positions with frequency components
        cos = F.embedding(positions, cos_comp)[:, None, :, :]
        sin = F.embedding(positions, sin_comp)[:, None, :, :]
        # Apply rotation
        return (tokens * cos) + (self._rotate_features(tokens) * sin)

    def forward(self, tokens: torch.Tensor, positions: torch.Tensor) -> torch.Tensor:
        """Applies 2D rotary position embeddings to input tokens.

        Args:
            tokens: Input tensor of shape (batch_size, n_heads, n_tokens, dim).
                   The feature dimension (dim) must be divisible by 4.
            positions: Position tensor of shape (batch_size, n_tokens, 2) containing
                      the y and x coordinates for each token.

        Returns:
            Tensor of same shape as input with applied 2D rotary position embeddings.

        Raises:
            AssertionError: If input dimensions are invalid or positions are malformed.
        """
        # Validate inputs
        assert tokens.size(-1) % 2 == 0, "Feature dimension must be even"
        assert (
            positions.ndim == 3 and positions.shape[-1] == 2
        ), "Positions must have shape (batch_size, n_tokens, 2)"

        # Compute feature dimension for each spatial direction
        feature_dim = tokens.size(-1) // 2

        # Get frequency components
        max_position = int(positions.max()) + 1
        cos_comp, sin_comp = self._compute_frequency_components(
            feature_dim, max_position, tokens.device, tokens.dtype
        )

        # Split features for vertical and horizontal processing
        vertical_features, horizontal_features = tokens.chunk(2, dim=-1)

        # Apply RoPE separately for each dimension
        vertical_features = self._apply_1d_rope(
            vertical_features, positions[..., 0], cos_comp, sin_comp
        )
        horizontal_features = self._apply_1d_rope(
            horizontal_features, positions[..., 1], cos_comp, sin_comp
        )

        # Combine processed features
        return torch.cat((vertical_features, horizontal_features), dim=-1)



================================================
FILE: src/depth_anything_3/model/dinov2/layers/swiglu_ffn.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates.
# All rights reserved.
#
# This source code is licensed under the license found in the
# LICENSE file in the root directory of this source tree.

from typing import Callable, Optional
import torch.nn.functional as F
from torch import Tensor, nn


class SwiGLUFFN(nn.Module):
    def __init__(
        self,
        in_features: int,
        hidden_features: Optional[int] = None,
        out_features: Optional[int] = None,
        act_layer: Callable[..., nn.Module] = None,
        drop: float = 0.0,
        bias: bool = True,
    ) -> None:
        super().__init__()
        out_features = out_features or in_features
        hidden_features = hidden_features or in_features
        self.w12 = nn.Linear(in_features, 2 * hidden_features, bias=bias)
        self.w3 = nn.Linear(hidden_features, out_features, bias=bias)

    def forward(self, x: Tensor) -> Tensor:
        x12 = self.w12(x)
        x1, x2 = x12.chunk(2, dim=-1)
        hidden = F.silu(x1) * x2
        return self.w3(hidden)


try:
    from xformers.ops import SwiGLU

    XFORMERS_AVAILABLE = True
except ImportError:
    SwiGLU = SwiGLUFFN
    XFORMERS_AVAILABLE = False


class SwiGLUFFNFused(SwiGLU):
    def __init__(
        self,
        in_features: int,
        hidden_features: Optional[int] = None,
        out_features: Optional[int] = None,
        act_layer: Callable[..., nn.Module] = None,
        drop: float = 0.0,
        bias: bool = True,
    ) -> None:
        out_features = out_features or in_features
        hidden_features = hidden_features or in_features
        hidden_features = (int(hidden_features * 2 / 3) + 7) // 8 * 8
        super().__init__(
            in_features=in_features,
            hidden_features=hidden_features,
            out_features=out_features,
            bias=bias,
        )



================================================
FILE: src/depth_anything_3/model/utils/attention.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

# Modified from: https://github.com/huggingface/pytorch-image-models/blob/main/timm/models/vision_transformer.py#L103-L110 # noqa

from typing import Callable, Optional, Union
import torch
import torch.nn.functional as F
from torch import Tensor, nn


class Attention(nn.Module):
    def __init__(
        self,
        dim: int,
        num_heads: int = 8,
        qkv_bias: bool = True,
        proj_bias: bool = True,
        attn_drop: float = 0.0,
        proj_drop: float = 0.0,
        norm_layer: nn.Module = nn.LayerNorm,
        qk_norm: bool = False,
        rope=None,
    ) -> None:
        super().__init__()
        assert dim % num_heads == 0, "dim should be divisible by num_heads"
        self.num_heads = num_heads
        self.head_dim = dim // num_heads
        self.scale = self.head_dim**-0.5
        self.qkv = nn.Linear(dim, dim * 3, bias=qkv_bias)
        self.q_norm = norm_layer(self.head_dim) if qk_norm else nn.Identity()
        self.k_norm = norm_layer(self.head_dim) if qk_norm else nn.Identity()
        self.attn_drop = nn.Dropout(attn_drop)
        self.proj = nn.Linear(dim, dim, bias=proj_bias)
        self.proj_drop = nn.Dropout(proj_drop)
        self.rope = rope

    def forward(self, x: Tensor, pos=None, attn_mask=None) -> Tensor:
        # Debug breakpoint removed for production
        B, N, C = x.shape
        qkv = self.qkv(x).reshape(B, N, 3, self.num_heads, self.head_dim).permute(2, 0, 3, 1, 4)
        q, k, v = qkv.unbind(0)
        q, k = self.q_norm(q), self.k_norm(k)
        q = self.rope(q, pos) if self.rope is not None else q
        k = self.rope(k, pos) if self.rope is not None else k
        x = F.scaled_dot_product_attention(
            q,
            k,
            v,
            dropout_p=self.attn_drop.p if self.training else 0.0,
            attn_mask=attn_mask,
        )
        x = x.transpose(1, 2).reshape(B, N, C)
        x = self.proj(x)
        x = self.proj_drop(x)
        return x


class LayerScale(nn.Module):
    def __init__(
        self,
        dim: int,
        init_values: Union[float, Tensor] = 1e-5,
        inplace: bool = False,
    ) -> None:
        super().__init__()
        self.inplace = inplace
        self.gamma = nn.Parameter(init_values * torch.ones(dim))

    def forward(self, x: Tensor) -> Tensor:
        return x.mul_(self.gamma) if self.inplace else x * self.gamma


class Mlp(nn.Module):
    def __init__(
        self,
        in_features: int,
        hidden_features: Optional[int] = None,
        out_features: Optional[int] = None,
        act_layer: Callable[..., nn.Module] = nn.GELU,
        drop: float = 0.0,
        bias: bool = True,
    ) -> None:
        super().__init__()
        out_features = out_features or in_features
        hidden_features = hidden_features or in_features
        self.fc1 = nn.Linear(in_features, hidden_features, bias=bias)
        self.act = act_layer()
        self.fc2 = nn.Linear(hidden_features, out_features, bias=bias)
        self.drop = nn.Dropout(drop)

    def forward(self, x: Tensor) -> Tensor:
        x = self.fc1(x)
        x = self.act(x)
        x = self.drop(x)
        x = self.fc2(x)
        x = self.drop(x)
        return x



================================================
FILE: src/depth_anything_3/model/utils/block.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.


from typing import Callable
from torch import Tensor, nn

from .attention import Attention, LayerScale, Mlp


class Block(nn.Module):
    def __init__(
        self,
        dim: int,
        num_heads: int,
        mlp_ratio: float = 4.0,
        qkv_bias: bool = True,
        proj_bias: bool = True,
        ffn_bias: bool = True,
        drop: float = 0.0,
        attn_drop: float = 0.0,
        init_values=None,
        drop_path: float = 0.0,
        act_layer: Callable[..., nn.Module] = nn.GELU,
        norm_layer: Callable[..., nn.Module] = nn.LayerNorm,
        attn_class: Callable[..., nn.Module] = Attention,
        ffn_layer: Callable[..., nn.Module] = Mlp,
        qk_norm: bool = False,
        rope=None,
    ) -> None:
        super().__init__()

        self.norm1 = norm_layer(dim)

        self.attn = attn_class(
            dim,
            num_heads=num_heads,
            qkv_bias=qkv_bias,
            proj_bias=proj_bias,
            attn_drop=attn_drop,
            proj_drop=drop,
            qk_norm=qk_norm,
            rope=rope,
        )

        self.ls1 = LayerScale(dim, init_values=init_values) if init_values else nn.Identity()
        self.norm2 = norm_layer(dim)
        mlp_hidden_dim = int(dim * mlp_ratio)
        self.mlp = ffn_layer(
            in_features=dim,
            hidden_features=mlp_hidden_dim,
            act_layer=act_layer,
            drop=drop,
            bias=ffn_bias,
        )
        self.ls2 = LayerScale(dim, init_values=init_values) if init_values else nn.Identity()

        self.sample_drop_ratio = 0.0  # Equivalent to always having drop_path=0

    def forward(self, x: Tensor, pos=None, attn_mask=None) -> Tensor:
        def attn_residual_func(x: Tensor, pos=None, attn_mask=None) -> Tensor:
            return self.ls1(self.attn(self.norm1(x), pos=pos, attn_mask=attn_mask))

        def ffn_residual_func(x: Tensor) -> Tensor:
            return self.ls2(self.mlp(self.norm2(x)))

        # drop_path is always 0, so always take the else branch
        x = x + attn_residual_func(x, pos=pos, attn_mask=attn_mask)
        x = x + ffn_residual_func(x)
        return x



================================================
FILE: src/depth_anything_3/model/utils/gs_renderer.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

import math
from math import isqrt
from typing import Literal, Optional
import torch
from einops import rearrange, repeat
from tqdm import tqdm

from depth_anything_3.specs import Gaussians
from depth_anything_3.utils.camera_trj_helpers import (
    interpolate_extrinsics,
    interpolate_intrinsics,
    render_dolly_zoom_path,
    render_stabilization_path,
    render_wander_path,
    render_wobble_inter_path,
)
from depth_anything_3.utils.geometry import affine_inverse, as_homogeneous, get_fov
from depth_anything_3.utils.logger import logger

try:
    from gsplat import rasterization
except ImportError:
    logger.warn(
        "Dependency `gsplat` is required for rendering 3DGS. "
        "Install via: pip install git+https://github.com/nerfstudio-project/"
        "gsplat.git@0b4dddf04cb687367602c01196913cde6a743d70"
    )


def render_3dgs(
    extrinsics: torch.Tensor,  # "batch_views 4 4", w2c
    intrinsics: torch.Tensor,  # "batch_views 3 3", normalized
    image_shape: tuple[int, int],
    gaussian: Gaussians,
    background_color: Optional[torch.Tensor] = None,  # "batch_views 3"
    use_sh: bool = True,
    num_view: int = 1,
    color_mode: Literal["RGB+D", "RGB+ED"] = "RGB+D",
    **kwargs,
) -> tuple[
    torch.Tensor,  # "batch_views 3 height width"
    torch.Tensor,  # "batch_views height width"
]:
    # extract gaussian params
    gaussian_means = gaussian.means
    gaussian_scales = gaussian.scales
    gaussian_quats = gaussian.rotations
    gaussian_opacities = gaussian.opacities
    gaussian_sh_coefficients = gaussian.harmonics
    b, _, _ = extrinsics.shape

    if background_color is None:
        background_color = repeat(torch.tensor([0.0, 0.0, 0.0]), "c -> b c", b=b).to(
            gaussian_sh_coefficients
        )

    if use_sh:
        _, _, _, n = gaussian_sh_coefficients.shape
        degree = isqrt(n) - 1
        shs = rearrange(gaussian_sh_coefficients, "b g xyz n -> b g n xyz").contiguous()
    else:  # use color
        shs = (
            gaussian_sh_coefficients.squeeze(-1).sigmoid().contiguous()
        )  # (b, g, c), normed to (0, 1)

    h, w = image_shape

    fov_x, fov_y = get_fov(intrinsics).unbind(dim=-1)
    tan_fov_x = (0.5 * fov_x).tan()
    tan_fov_y = (0.5 * fov_y).tan()
    focal_length_x = w / (2 * tan_fov_x)
    focal_length_y = h / (2 * tan_fov_y)

    view_matrix = extrinsics.float()

    all_images = []
    all_radii = []
    all_depths = []
    # render view in a batch based, each batch contains one scene
    # assume the Gaussian parameters are originally repeated along the view dim
    batch_scene = b // num_view

    def index_i_gs_attr(full_attr, idx):
        # return rearrange(full_attr, "(b v) ... -> b v ...", v=num_view)[idx, 0]
        return full_attr[idx]

    for i in range(batch_scene):
        K = repeat(
            torch.tensor(
                [
                    [0, 0, w / 2.0],
                    [0, 0, h / 2.0],
                    [0, 0, 1],
                ]
            ),
            "i j -> v i j",
            v=num_view,
        ).to(gaussian_means)
        K[:, 0, 0] = focal_length_x.reshape(batch_scene, num_view)[i]
        K[:, 1, 1] = focal_length_y.reshape(batch_scene, num_view)[i]

        i_means = index_i_gs_attr(gaussian_means, i)  # [N, 3]
        i_scales = index_i_gs_attr(gaussian_scales, i)
        i_quats = index_i_gs_attr(gaussian_quats, i)
        i_opacities = index_i_gs_attr(gaussian_opacities, i)  # [N,]
        i_colors = index_i_gs_attr(shs, i)  # [N, K, 3]
        i_viewmats = rearrange(view_matrix, "(b v) ... -> b v ...", v=num_view)[i]  # [v, 4, 4]
        i_backgrounds = rearrange(background_color, "(b v) ... -> b v ...", v=num_view)[
            i
        ]  # [v, 3]

        render_colors, render_alphas, info = rasterization(
            means=i_means,
            quats=i_quats,  # [N, 4]
            scales=i_scales,  # [N, 3]
            opacities=i_opacities,
            colors=i_colors,
            viewmats=i_viewmats,  # [v, 4, 4]
            Ks=K,  # [v, 3, 3]
            backgrounds=i_backgrounds,
            render_mode=color_mode,
            width=w,
            height=h,
            packed=False,
            sh_degree=degree if use_sh else None,
        )
        depth = render_colors[..., -1].unbind(dim=0)

        image = rearrange(render_colors[..., :3], "v h w c -> v c h w").unbind(dim=0)
        radii = info["radii"].unbind(dim=0)
        try:
            info["means2d"].retain_grad()  # [1, N, 2]
        except Exception:
            pass
        all_images.extend(image)
        all_depths.extend(depth)
        all_radii.extend(radii)

    return torch.stack(all_images), torch.stack(all_depths)


def run_renderer_in_chunk_w_trj_mode(
    gaussians: Gaussians,
    extrinsics: torch.Tensor,  # world2cam, "batch view 4 4" | "batch view 3 4"
    intrinsics: torch.Tensor,  # unnormed intrinsics, "batch view 3 3"
    image_shape: tuple[int, int],
    chunk_size: Optional[int] = 8,
    trj_mode: Literal[
        "original",
        "smooth",
        "interpolate",
        "interpolate_smooth",
        "wander",
        "dolly_zoom",
        "extend",
        "wobble_inter",
    ] = "smooth",
    input_shape: Optional[tuple[int, int]] = None,
    enable_tqdm: Optional[bool] = False,
    **kwargs,
) -> tuple[
    torch.Tensor,  # color, "batch view 3 height width"
    torch.Tensor,  # depth, "batch view height width"
]:
    cam2world = affine_inverse(as_homogeneous(extrinsics))
    if input_shape is not None:
        in_h, in_w = input_shape
    else:
        in_h, in_w = image_shape
    intr_normed = intrinsics.clone().detach()
    intr_normed[..., 0, :] /= in_w
    intr_normed[..., 1, :] /= in_h
    if extrinsics.shape[1] <= 1:
        assert trj_mode in [
            "wander",
            "dolly_zoom",
        ], "Please set trj_mode to 'wander' or 'dolly_zoom' when n_views=1"

    def _smooth_trj_fn_batch(raw_c2ws, k_size=50):
        try:
            smooth_c2ws = torch.stack(
                [render_stabilization_path(c2w_i, k_size) for c2w_i in raw_c2ws],
                dim=0,
            )
        except Exception as e:
            print(f"[DEBUG] Path smoothing failed with error: {e}.")
            smooth_c2ws = raw_c2ws
        return smooth_c2ws

    # get rendered trj
    if trj_mode == "original":
        tgt_c2w = cam2world
        tgt_intr = intr_normed
    elif trj_mode == "smooth":
        tgt_c2w = _smooth_trj_fn_batch(cam2world)
        tgt_intr = intr_normed
    elif trj_mode in ["interpolate", "interpolate_smooth", "extend"]:
        inter_len = 8
        total_len = (cam2world.shape[1] - 1) * inter_len
        if total_len > 24 * 18:  # no more than 18s
            inter_len = max(1, 24 * 10 // (cam2world.shape[1] - 1))
        if total_len < 24 * 2:  # no less than 2s
            inter_len = max(1, 24 * 2 // (cam2world.shape[1] - 1))

        if inter_len > 2:
            t = torch.linspace(0, 1, inter_len, dtype=torch.float32, device=cam2world.device)
            t = (torch.cos(torch.pi * (t + 1)) + 1) / 2
            tgt_c2w_b = []
            tgt_intr_b = []
            for b_idx in range(cam2world.shape[0]):
                tgt_c2w = []
                tgt_intr = []
                for cur_idx in range(cam2world.shape[1] - 1):
                    tgt_c2w.append(
                        interpolate_extrinsics(
                            cam2world[b_idx, cur_idx], cam2world[b_idx, cur_idx + 1], t
                        )[(0 if cur_idx == 0 else 1) :]
                    )
                    tgt_intr.append(
                        interpolate_intrinsics(
                            intr_normed[b_idx, cur_idx], intr_normed[b_idx, cur_idx + 1], t
                        )[(0 if cur_idx == 0 else 1) :]
                    )
                tgt_c2w_b.append(torch.cat(tgt_c2w))
                tgt_intr_b.append(torch.cat(tgt_intr))
            tgt_c2w = torch.stack(tgt_c2w_b)  # b v 4 4
            tgt_intr = torch.stack(tgt_intr_b)  # b v 3 3
        else:
            tgt_c2w = cam2world
            tgt_intr = intr_normed
        if trj_mode in ["interpolate_smooth", "extend"]:
            tgt_c2w = _smooth_trj_fn_batch(tgt_c2w)
        if trj_mode == "extend":
            # apply dolly_zoom and wander in the middle frame
            assert cam2world.shape[0] == 1, "extend only supports for batch_size=1 currently."
            mid_idx = tgt_c2w.shape[1] // 2
            c2w_wd, intr_wd = render_wander_path(
                tgt_c2w[0, mid_idx],
                tgt_intr[0, mid_idx],
                h=in_h,
                w=in_w,
                num_frames=max(36, min(60, mid_idx // 2)),
                max_disp=24.0,
            )
            c2w_dz, intr_dz = render_dolly_zoom_path(
                tgt_c2w[0, mid_idx],
                tgt_intr[0, mid_idx],
                h=in_h,
                w=in_w,
                num_frames=max(36, min(60, mid_idx // 2)),
            )
            tgt_c2w = torch.cat(
                [
                    tgt_c2w[:, :mid_idx],
                    c2w_wd.unsqueeze(0),
                    c2w_dz.unsqueeze(0),
                    tgt_c2w[:, mid_idx:],
                ],
                dim=1,
            )
            tgt_intr = torch.cat(
                [
                    tgt_intr[:, :mid_idx],
                    intr_wd.unsqueeze(0),
                    intr_dz.unsqueeze(0),
                    tgt_intr[:, mid_idx:],
                ],
                dim=1,
            )
    elif trj_mode in ["wander", "dolly_zoom"]:
        if trj_mode == "wander":
            render_fn = render_wander_path
            extra_kwargs = {"max_disp": 24.0}
        else:
            render_fn = render_dolly_zoom_path
            extra_kwargs = {"D_focus": 30.0, "max_disp": 2.0}
        tgt_c2w = []
        tgt_intr = []
        for b_idx in range(cam2world.shape[0]):
            c2w_i, intr_i = render_fn(
                cam2world[b_idx, 0], intr_normed[b_idx, 0], h=in_h, w=in_w, **extra_kwargs
            )
            tgt_c2w.append(c2w_i)
            tgt_intr.append(intr_i)
        tgt_c2w = torch.stack(tgt_c2w)
        tgt_intr = torch.stack(tgt_intr)
    elif trj_mode == "wobble_inter":
        tgt_c2w, tgt_intr = render_wobble_inter_path(
            cam2world=cam2world,
            intr_normed=intr_normed,
            inter_len=10,
            n_skip=3,
        )
    else:
        raise Exception(f"trj mode [{trj_mode}] is not implemented.")

    _, v = tgt_c2w.shape[:2]
    tgt_extr = affine_inverse(tgt_c2w)
    if chunk_size is None:
        chunk_size = v
    chunk_size = min(v, chunk_size)
    all_colors = []
    all_depths = []
    for chunk_idx in tqdm(
        range(math.ceil(v / chunk_size)),
        desc="Rendering novel views",
        disable=(not enable_tqdm),
        leave=False,
    ):
        s = int(chunk_idx * chunk_size)
        e = int((chunk_idx + 1) * chunk_size)
        cur_n_view = tgt_extr[:, s:e].shape[1]
        color, depth = render_3dgs(
            extrinsics=rearrange(tgt_extr[:, s:e], "b v ... -> (b v) ..."),  # w2c
            intrinsics=rearrange(tgt_intr[:, s:e], "b v ... -> (b v) ..."),  # normed
            image_shape=image_shape,
            gaussian=gaussians,
            num_view=cur_n_view,
            **kwargs,
        )
        all_colors.append(rearrange(color, "(b v) ... -> b v ...", v=cur_n_view))
        all_depths.append(rearrange(depth, "(b v) ... -> b v ...", v=cur_n_view))
    all_colors = torch.cat(all_colors, dim=1)
    all_depths = torch.cat(all_depths, dim=1)

    return all_colors, all_depths



================================================
FILE: src/depth_anything_3/model/utils/head_utils.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

from typing import Tuple, Union
import torch
import torch.nn as nn
import torch.nn.functional as F

# -----------------------------------------------------------------------------
# Activation functions
# -----------------------------------------------------------------------------


def activate_head_gs(out, activation="norm_exp", conf_activation="expp1", conf_dim=None):
    """
    Process network output to extract GS params and density values.
    Density could be view-dependent as SH coefficient


    Args:
        out: Network output tensor (B, C, H, W)
        activation: Activation type for 3D points
        conf_activation: Activation type for confidence values

    Returns:
        Tuple of (3D points tensor, confidence tensor)
    """
    # Move channels from last dim to the 4th dimension => (B, H, W, C)
    fmap = out.permute(0, 2, 3, 1)  # B,H,W,C expected

    # Split into xyz (first C-1 channels) and confidence (last channel)
    conf_dim = 1 if conf_dim is None else conf_dim
    xyz = fmap[:, :, :, :-conf_dim]
    conf = fmap[:, :, :, -1] if conf_dim == 1 else fmap[:, :, :, -conf_dim:]

    if activation == "norm_exp":
        d = xyz.norm(dim=-1, keepdim=True).clamp(min=1e-8)
        xyz_normed = xyz / d
        pts3d = xyz_normed * torch.expm1(d)
    elif activation == "norm":
        pts3d = xyz / xyz.norm(dim=-1, keepdim=True)
    elif activation == "exp":
        pts3d = torch.exp(xyz)
    elif activation == "relu":
        pts3d = F.relu(xyz)
    elif activation == "sigmoid":
        pts3d = torch.sigmoid(xyz)
    elif activation == "linear":
        pts3d = xyz
    else:
        raise ValueError(f"Unknown activation: {activation}")

    if conf_activation == "expp1":
        conf_out = 1 + conf.exp()
    elif conf_activation == "expp0":
        conf_out = conf.exp()
    elif conf_activation == "sigmoid":
        conf_out = torch.sigmoid(conf)
    elif conf_activation == "linear":
        conf_out = conf
    else:
        raise ValueError(f"Unknown conf_activation: {conf_activation}")

    return pts3d, conf_out


# -----------------------------------------------------------------------------
# Other utilities
# -----------------------------------------------------------------------------


class Permute(nn.Module):
    """nn.Module wrapper around Tensor.permute for cleaner nn.Sequential usage."""

    dims: Tuple[int, ...]

    def __init__(self, dims: Tuple[int, ...]) -> None:
        super().__init__()
        self.dims = dims

    def forward(self, x: torch.Tensor) -> torch.Tensor:  # type: ignore[override]
        return x.permute(*self.dims)


def position_grid_to_embed(
    pos_grid: torch.Tensor, embed_dim: int, omega_0: float = 100
) -> torch.Tensor:
    """
    Convert 2D position grid (HxWx2) to sinusoidal embeddings (HxWxC)

    Args:
        pos_grid: Tensor of shape (H, W, 2) containing 2D coordinates
        embed_dim: Output channel dimension for embeddings

    Returns:
        Tensor of shape (H, W, embed_dim) with positional embeddings
    """
    H, W, grid_dim = pos_grid.shape
    assert grid_dim == 2
    pos_flat = pos_grid.reshape(-1, grid_dim)  # Flatten to (H*W, 2)

    # Process x and y coordinates separately
    emb_x = make_sincos_pos_embed(embed_dim // 2, pos_flat[:, 0], omega_0=omega_0)  # [1, H*W, D/2]
    emb_y = make_sincos_pos_embed(embed_dim // 2, pos_flat[:, 1], omega_0=omega_0)  # [1, H*W, D/2]

    # Combine and reshape
    emb = torch.cat([emb_x, emb_y], dim=-1)  # [1, H*W, D]

    return emb.view(H, W, embed_dim)  # [H, W, D]


def make_sincos_pos_embed(embed_dim: int, pos: torch.Tensor, omega_0: float = 100) -> torch.Tensor:
    """
    This function generates a 1D positional embedding from a given grid using sine and cosine functions. # noqa

    Args:
    - embed_dim: The embedding dimension.
    - pos: The position to generate the embedding from.

    Returns:
    - emb: The generated 1D positional embedding.
    """
    assert embed_dim % 2 == 0
    omega = torch.arange(embed_dim // 2, dtype=torch.float32, device=pos.device)
    omega /= embed_dim / 2.0
    omega = 1.0 / omega_0**omega  # (D/2,)

    pos = pos.reshape(-1)  # (M,)
    out = torch.einsum("m,d->md", pos, omega)  # (M, D/2), outer product

    emb_sin = torch.sin(out)  # (M, D/2)
    emb_cos = torch.cos(out)  # (M, D/2)

    emb = torch.cat([emb_sin, emb_cos], dim=1)  # (M, D)
    return emb.float()


# Inspired by https://github.com/microsoft/moge


def create_uv_grid(
    width: int,
    height: int,
    aspect_ratio: float = None,
    dtype: torch.dtype = None,
    device: torch.device = None,
) -> torch.Tensor:
    """
    Create a normalized UV grid of shape (width, height, 2).

    The grid spans horizontally and vertically according to an aspect ratio,
    ensuring the top-left corner is at (-x_span, -y_span) and the bottom-right
    corner is at (x_span, y_span), normalized by the diagonal of the plane.

    Args:
        width (int): Number of points horizontally.
        height (int): Number of points vertically.
        aspect_ratio (float, optional): Width-to-height ratio. Defaults to width/height.
        dtype (torch.dtype, optional): Data type of the resulting tensor.
        device (torch.device, optional): Device on which the tensor is created.

    Returns:
        torch.Tensor: A (width, height, 2) tensor of UV coordinates.
    """
    # Derive aspect ratio if not explicitly provided
    if aspect_ratio is None:
        aspect_ratio = float(width) / float(height)

    # Compute normalized spans for X and Y
    diag_factor = (aspect_ratio**2 + 1.0) ** 0.5
    span_x = aspect_ratio / diag_factor
    span_y = 1.0 / diag_factor

    # Establish the linspace boundaries
    left_x = -span_x * (width - 1) / width
    right_x = span_x * (width - 1) / width
    top_y = -span_y * (height - 1) / height
    bottom_y = span_y * (height - 1) / height

    # Generate 1D coordinates
    x_coords = torch.linspace(left_x, right_x, steps=width, dtype=dtype, device=device)
    y_coords = torch.linspace(top_y, bottom_y, steps=height, dtype=dtype, device=device)

    # Create 2D meshgrid (width x height) and stack into UV
    uu, vv = torch.meshgrid(x_coords, y_coords, indexing="xy")
    uv_grid = torch.stack((uu, vv), dim=-1)

    return uv_grid


# -----------------------------------------------------------------------------
# Interpolation (safe interpolation, avoid INT_MAX overflow)
# -----------------------------------------------------------------------------
def custom_interpolate(
    x: torch.Tensor,
    size: Union[Tuple[int, int], None] = None,
    scale_factor: Union[float, None] = None,
    mode: str = "bilinear",
    align_corners: bool = True,
) -> torch.Tensor:
    """
    Safe interpolation implementation to avoid INT_MAX overflow in torch.nn.functional.interpolate.
    """
    if size is None:
        assert scale_factor is not None, "Either size or scale_factor must be provided."
        size = (int(x.shape[-2] * scale_factor), int(x.shape[-1] * scale_factor))

    INT_MAX = 1610612736
    total = size[0] * size[1] * x.shape[0] * x.shape[1]

    if total > INT_MAX:
        chunks = torch.chunk(x, chunks=(total // INT_MAX) + 1, dim=0)
        outs = [
            nn.functional.interpolate(c, size=size, mode=mode, align_corners=align_corners)
            for c in chunks
        ]
        return torch.cat(outs, dim=0).contiguous()

    return nn.functional.interpolate(x, size=size, mode=mode, align_corners=align_corners)



================================================
FILE: src/depth_anything_3/model/utils/transform.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

import torch
import torch.nn.functional as F


def extri_intri_to_pose_encoding(
    extrinsics,
    intrinsics,
    image_size_hw=None,
):
    """Convert camera extrinsics and intrinsics to a compact pose encoding."""

    # extrinsics: BxSx3x4
    # intrinsics: BxSx3x3
    R = extrinsics[:, :, :3, :3]  # BxSx3x3
    T = extrinsics[:, :, :3, 3]  # BxSx3

    quat = mat_to_quat(R)
    # Note the order of h and w here
    H, W = image_size_hw
    fov_h = 2 * torch.atan((H / 2) / intrinsics[..., 1, 1])
    fov_w = 2 * torch.atan((W / 2) / intrinsics[..., 0, 0])
    pose_encoding = torch.cat([T, quat, fov_h[..., None], fov_w[..., None]], dim=-1).float()

    return pose_encoding


def pose_encoding_to_extri_intri(
    pose_encoding,
    image_size_hw=None,
):
    """Convert a pose encoding back to camera extrinsics and intrinsics."""

    T = pose_encoding[..., :3]
    quat = pose_encoding[..., 3:7]
    fov_h = pose_encoding[..., 7]
    fov_w = pose_encoding[..., 8]

    R = quat_to_mat(quat)
    extrinsics = torch.cat([R, T[..., None]], dim=-1)

    H, W = image_size_hw
    fy = (H / 2.0) / torch.clamp(torch.tan(fov_h / 2.0), 1e-6)
    fx = (W / 2.0) / torch.clamp(torch.tan(fov_w / 2.0), 1e-6)
    intrinsics = torch.zeros(pose_encoding.shape[:2] + (3, 3), device=pose_encoding.device)
    intrinsics[..., 0, 0] = fx
    intrinsics[..., 1, 1] = fy
    intrinsics[..., 0, 2] = W / 2
    intrinsics[..., 1, 2] = H / 2
    intrinsics[..., 2, 2] = 1.0  # Set the homogeneous coordinate to 1

    return extrinsics, intrinsics


def quat_to_mat(quaternions: torch.Tensor) -> torch.Tensor:
    """
    Quaternion Order: XYZW or say ijkr, scalar-last

    Convert rotations given as quaternions to rotation matrices.
    Args:
        quaternions: quaternions with real part last,
            as tensor of shape (..., 4).

    Returns:
        Rotation matrices as tensor of shape (..., 3, 3).
    """
    i, j, k, r = torch.unbind(quaternions, -1)
    two_s = 2.0 / (quaternions * quaternions).sum(-1)

    o = torch.stack(
        (
            1 - two_s * (j * j + k * k),
            two_s * (i * j - k * r),
            two_s * (i * k + j * r),
            two_s * (i * j + k * r),
            1 - two_s * (i * i + k * k),
            two_s * (j * k - i * r),
            two_s * (i * k - j * r),
            two_s * (j * k + i * r),
            1 - two_s * (i * i + j * j),
        ),
        -1,
    )
    return o.reshape(quaternions.shape[:-1] + (3, 3))


def mat_to_quat(matrix: torch.Tensor) -> torch.Tensor:
    """
    Convert rotations given as rotation matrices to quaternions.

    Args:
        matrix: Rotation matrices as tensor of shape (..., 3, 3).

    Returns:
        quaternions with real part last, as tensor of shape (..., 4).
        Quaternion Order: XYZW or say ijkr, scalar-last
    """
    if matrix.size(-1) != 3 or matrix.size(-2) != 3:
        raise ValueError(f"Invalid rotation matrix shape {matrix.shape}.")

    batch_dim = matrix.shape[:-2]
    m00, m01, m02, m10, m11, m12, m20, m21, m22 = torch.unbind(
        matrix.reshape(batch_dim + (9,)), dim=-1
    )

    q_abs = _sqrt_positive_part(
        torch.stack(
            [
                1.0 + m00 + m11 + m22,
                1.0 + m00 - m11 - m22,
                1.0 - m00 + m11 - m22,
                1.0 - m00 - m11 + m22,
            ],
            dim=-1,
        )
    )

    quat_by_rijk = torch.stack(
        [
            torch.stack([q_abs[..., 0] ** 2, m21 - m12, m02 - m20, m10 - m01], dim=-1),
            torch.stack([m21 - m12, q_abs[..., 1] ** 2, m10 + m01, m02 + m20], dim=-1),
            torch.stack([m02 - m20, m10 + m01, q_abs[..., 2] ** 2, m12 + m21], dim=-1),
            torch.stack([m10 - m01, m20 + m02, m21 + m12, q_abs[..., 3] ** 2], dim=-1),
        ],
        dim=-2,
    )

    flr = torch.tensor(0.1).to(dtype=q_abs.dtype, device=q_abs.device)
    quat_candidates = quat_by_rijk / (2.0 * q_abs[..., None].max(flr))

    out = quat_candidates[F.one_hot(q_abs.argmax(dim=-1), num_classes=4) > 0.5, :].reshape(
        batch_dim + (4,)
    )

    out = out[..., [1, 2, 3, 0]]

    out = standardize_quaternion(out)

    return out


def _sqrt_positive_part(x: torch.Tensor) -> torch.Tensor:
    """
    Returns torch.sqrt(torch.max(0, x))
    but with a zero subgradient where x is 0.
    """
    ret = torch.zeros_like(x)
    positive_mask = x > 0
    if torch.is_grad_enabled():
        ret[positive_mask] = torch.sqrt(x[positive_mask])
    else:
        ret = torch.where(positive_mask, torch.sqrt(x), ret)
    return ret


def standardize_quaternion(quaternions: torch.Tensor) -> torch.Tensor:
    """
    Convert a unit quaternion to a standard form: one in which the real
    part is non negative.

    Args:
        quaternions: Quaternions with real part last,
            as tensor of shape (..., 4).

    Returns:
        Standardized quaternions as tensor of shape (..., 4).
    """
    return torch.where(quaternions[..., 3:4] < 0, -quaternions, quaternions)


def cam_quat_xyzw_to_world_quat_wxyz(cam_quat_xyzw, c2w):
    # cam_quat_xyzw: (b, n, 4) in xyzw
    # c2w: (b, n, 4, 4)
    b, n = cam_quat_xyzw.shape[:2]
    # 1. xyzw -> wxyz
    cam_quat_wxyz = torch.cat(
        [
            cam_quat_xyzw[..., 3:4],  # w
            cam_quat_xyzw[..., 0:1],  # x
            cam_quat_xyzw[..., 1:2],  # y
            cam_quat_xyzw[..., 2:3],  # z
        ],
        dim=-1,
    )
    # 2. Quaternion to matrix
    cam_quat_wxyz_flat = cam_quat_wxyz.reshape(-1, 4)
    rotmat_cam = quat_to_mat(cam_quat_wxyz_flat).reshape(b, n, 3, 3)
    # 3. Transform to world space
    rotmat_c2w = c2w[..., :3, :3]
    rotmat_world = torch.matmul(rotmat_c2w, rotmat_cam)
    # 4. Matrix to quaternion (wxyz)
    rotmat_world_flat = rotmat_world.reshape(-1, 3, 3)
    world_quat_wxyz_flat = mat_to_quat(rotmat_world_flat)
    world_quat_wxyz = world_quat_wxyz_flat.reshape(b, n, 4)
    return world_quat_wxyz



================================================
FILE: src/depth_anything_3/services/__init__.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

"""
Services module for Depth Anything 3.
"""

from depth_anything_3.services.backend import create_app, start_server

__all__ = [
    start_server,
    create_app,
]



================================================
FILE: src/depth_anything_3/services/backend.py
================================================
# flake8: noqa: E501
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

"""
Model backend service for Depth Anything 3.
Provides HTTP API for model inference with persistent model loading.
"""

import os
import posixpath
import time
import uuid

from concurrent.futures import ThreadPoolExecutor
from typing import Any, Dict, List, Optional
from urllib.parse import quote
import numpy as np

import uvicorn
from fastapi import FastAPI, HTTPException
from fastapi.responses import FileResponse, HTMLResponse
from pydantic import BaseModel

from ..api import DepthAnything3
from ..utils.memory import (
    get_gpu_memory_info,
    cleanup_cuda_memory,
    check_memory_availability,
    estimate_memory_requirement,
)


class InferenceRequest(BaseModel):
    """Request model for inference API."""

    image_paths: List[str]
    export_dir: Optional[str] = None
    export_format: str = "mini_npz-glb"
    extrinsics: Optional[List[List[List[float]]]] = None
    intrinsics: Optional[List[List[List[float]]]] = None
    process_res: int = 504
    process_res_method: str = "upper_bound_resize"
    export_feat_layers: List[int] = []
    align_to_input_ext_scale: bool = True
    # GLB export parameters
    conf_thresh_percentile: float = 40.0
    num_max_points: int = 1_000_000
    show_cameras: bool = True
    # Feat_vis export parameters
    feat_vis_fps: int = 15


class InferenceResponse(BaseModel):
    """Response model for inference API."""

    success: bool
    message: str
    task_id: Optional[str] = None
    export_dir: Optional[str] = None
    export_format: str = "mini_npz-glb"
    processing_time: Optional[float] = None


class TaskStatus(BaseModel):
    """Task status model."""

    task_id: str
    status: str  # "pending", "running", "completed", "failed"
    message: str
    progress: Optional[float] = None  # 0.0 to 1.0
    created_at: float
    started_at: Optional[float] = None
    completed_at: Optional[float] = None
    export_dir: Optional[str] = None
    request: Optional[InferenceRequest] = None  # Store the original request

    # Essential task parameters
    num_images: Optional[int] = None  # Number of input images
    export_format: Optional[str] = None  # Export format
    process_res_method: Optional[str] = None  # Processing resolution method
    video_path: Optional[str] = None  # Source video path


class ModelBackend:
    """Model backend service with persistent model loading."""

    def __init__(self, model_dir: str, device: str = "cuda"):
        self.model_dir = model_dir
        self.device = device
        self.model = None
        self.model_loaded = False
        self.load_time = None
        self.load_start_time = None  # Time when model loading started
        self.load_completed_time = None  # Time when model loading completed
        self.last_used = None

    def load_model(self):
        """Load model if not already loaded."""
        if self.model_loaded and self.model is not None:
            self.last_used = time.time()
            return self.model

        try:
            print(f"Loading model from {self.model_dir}...")
            self.load_start_time = time.time()
            start_time = time.time()

            self.model = DepthAnything3.from_pretrained(self.model_dir).to(self.device)
            self.model.eval()

            self.model_loaded = True
            self.load_time = time.time() - start_time
            self.load_completed_time = time.time()
            self.last_used = time.time()

            print(f"Model loaded successfully in {self.load_time:.2f}s")
            return self.model

        except Exception as e:
            print(f"Failed to load model: {e}")
            raise e

    def get_model(self):
        """Get model, loading if necessary."""
        if not self.model_loaded:
            return self.load_model()
        self.last_used = time.time()
        return self.model

    def get_status(self) -> Dict[str, Any]:
        """Get backend status information."""
        # Calculate uptime from when model loading completed
        uptime = 0
        if self.model_loaded and self.load_completed_time:
            uptime = time.time() - self.load_completed_time

        return {
            "model_loaded": self.model_loaded,
            "model_dir": self.model_dir,
            "device": self.device,
            "load_time": self.load_time,
            "last_used": self.last_used,
            "uptime": uptime,
        }


# Global backend instance
_backend: Optional[ModelBackend] = None
_app: Optional[FastAPI] = None
_tasks: Dict[str, TaskStatus] = {}
_executor = ThreadPoolExecutor(max_workers=1)  # Restrict to single-task execution
_running_task_id: Optional[str] = None  # Currently running task ID
_task_queue: List[str] = []  # Pending task queue

# Task cleanup configuration
MAX_TASK_HISTORY = 100  # Maximum number of tasks to keep in memory
CLEANUP_INTERVAL = 300  # Cleanup interval in seconds (5 minutes)


def _process_next_task():
    """Process the next task in the queue."""
    global _task_queue, _running_task_id

    if not _task_queue or _running_task_id is not None:
        return

    # Get next task from queue
    task_id = _task_queue.pop(0)

    # Get task request from tasks dict (we need to store the request)
    if task_id not in _tasks:
        return

    # Submit task to executor
    _executor.submit(_run_inference_task, task_id)


# get_gpu_memory_info imported from depth_anything_3.utils.memory


# cleanup_cuda_memory imported from depth_anything_3.utils.memory


# check_memory_availability imported from depth_anything_3.utils.memory


# estimate_memory_requirement imported from depth_anything_3.utils.memory


def _run_inference_task(task_id: str):
    """Run inference task in background thread with OOM protection."""
    global _tasks, _backend, _running_task_id, _task_queue

    model = None
    inference_started = False
    start_time = time.time()

    try:
        # Get task request
        if task_id not in _tasks or _tasks[task_id].request is None:
            print(f"[{task_id}] Task not found or request missing")
            return

        request = _tasks[task_id].request
        num_images = len(request.image_paths)

        # Set current running task
        _running_task_id = task_id

        # Update task status to running
        _tasks[task_id].status = "running"
        _tasks[task_id].started_at = start_time
        _tasks[task_id].message = f"[{task_id}] Starting inference on {num_images} frames..."
        print(f"[{task_id}] Starting inference on {num_images} frames")

        # Pre-inference cleanup to ensure maximum available memory
        print(f"[{task_id}] Pre-inference cleanup...")
        cleanup_cuda_memory()

        # Check memory availability
        estimated_memory = estimate_memory_requirement(num_images, request.process_res)
        mem_available, mem_msg = check_memory_availability(estimated_memory)
        print(f"[{task_id}] {mem_msg}")

        if not mem_available:
            # Try aggressive cleanup
            print(f"[{task_id}] Insufficient memory, attempting aggressive cleanup...")
            cleanup_cuda_memory()
            time.sleep(0.5)  # Give system time to reclaim memory

            # Check again
            mem_available, mem_msg = check_memory_availability(estimated_memory)
            if not mem_available:
                raise RuntimeError(
                    f"Insufficient GPU memory after cleanup. {mem_msg}\n"
                    f"Suggestions:\n"
                    f"  1. Reduce process_res (current: {request.process_res})\n"
                    f"  2. Process fewer images at once (current: {num_images})\n"
                    f"  3. Clear other GPU processes"
                )

        # Get model (with error handling)
        print(f"[{task_id}] Loading model...")
        _tasks[task_id].message = f"[{task_id}] Loading model..."
        _tasks[task_id].progress = 0.1

        try:
            model = _backend.get_model()
        except RuntimeError as e:
            if "out of memory" in str(e).lower():
                cleanup_cuda_memory()
                raise RuntimeError(
                    f"OOM during model loading: {str(e)}\n"
                    f"Try reducing the batch size or resolution."
                )
            raise

        print(f"[{task_id}] Model loaded successfully")
        _tasks[task_id].progress = 0.2

        # Prepare inference parameters
        inference_kwargs = {
            "image": request.image_paths,
            "export_format": request.export_format,
            "process_res": request.process_res,
            "process_res_method": request.process_res_method,
            "export_feat_layers": request.export_feat_layers,
            "align_to_input_ext_scale": request.align_to_input_ext_scale,
            "conf_thresh_percentile": request.conf_thresh_percentile,
            "num_max_points": request.num_max_points,
            "show_cameras": request.show_cameras,
            "feat_vis_fps": request.feat_vis_fps,
        }

        if request.export_dir:
            inference_kwargs["export_dir"] = request.export_dir

        if request.extrinsics:
            inference_kwargs["extrinsics"] = np.array(request.extrinsics, dtype=np.float32)

        if request.intrinsics:
            inference_kwargs["intrinsics"] = np.array(request.intrinsics, dtype=np.float32)

        # Run inference with timing
        inference_start_time = time.time()
        print(f"[{task_id}] Running model inference...")
        _tasks[task_id].message = f"[{task_id}] Running model inference on {num_images} images..."
        _tasks[task_id].progress = 0.3

        inference_started = True

        try:
            model.inference(**inference_kwargs)
            inference_time = time.time() - inference_start_time
            avg_time_per_image = inference_time / num_images if num_images > 0 else 0

            print(
                f"[{task_id}] Inference completed in {inference_time:.2f}s "
                f"({avg_time_per_image:.2f}s per image)"
            )

        except RuntimeError as e:
            if "out of memory" in str(e).lower():
                cleanup_cuda_memory()
                raise RuntimeError(
                    f"OOM during inference: {str(e)}\n"
                    f"Settings: {num_images} images, resolution={request.process_res}\n"
                    f"Suggestions:\n"
                    f"  1. Reduce process_res to {int(request.process_res * 0.75)}\n"
                    f"  2. Process images in smaller batches\n"
                    f"  3. Use process_res_method='resize' instead of 'upper_bound_resize'"
                )
            raise

        _tasks[task_id].progress = 0.9

        # Post-inference cleanup
        print(f"[{task_id}] Post-inference cleanup...")
        cleanup_cuda_memory()

        # Calculate total processing time
        total_time = time.time() - start_time

        # Update task status to completed
        _tasks[task_id].status = "completed"
        _tasks[task_id].completed_at = time.time()
        _tasks[task_id].message = (
            f"[{task_id}] Completed in {total_time:.2f}s " f"({avg_time_per_image:.2f}s per image)"
        )
        _tasks[task_id].progress = 1.0
        _tasks[task_id].export_dir = request.export_dir

        # Clear running state
        _running_task_id = None

        # Process next task in queue
        _process_next_task()

        print(f"[{task_id}] Task completed successfully")
        print(
            f"[{task_id}] Total time: {total_time:.2f}s, "
            f"Inference time: {inference_time:.2f}s, "
            f"Avg per image: {avg_time_per_image:.2f}s"
        )

    except Exception as e:
        # Update task status to failed
        error_msg = str(e)
        total_time = time.time() - start_time

        print(f"[{task_id}] Task failed after {total_time:.2f}s: {error_msg}")

        # Always attempt cleanup on failure
        cleanup_cuda_memory()

        _tasks[task_id].status = "failed"
        _tasks[task_id].completed_at = time.time()
        _tasks[task_id].message = f"[{task_id}] Failed after {total_time:.2f}s: {error_msg}"

        # Clear running state
        _running_task_id = None

        # Process next task in queue
        _process_next_task()

    finally:
        # Final cleanup in finally block to ensure it always runs
        # This is critical for releasing resources even if unexpected errors occur
        try:
            if inference_started:
                print(f"[{task_id}] Final cleanup in finally block...")
                cleanup_cuda_memory()
        except Exception as e:
            print(f"[{task_id}] Warning: Finally block cleanup failed: {e}")

        # Schedule cleanup after task completion
        _schedule_task_cleanup()


def _cleanup_old_tasks():
    """Clean up old completed/failed tasks to prevent memory buildup."""
    global _tasks

    current_time = time.time()
    tasks_to_remove = []

    # Find tasks to remove - more aggressive cleanup
    for task_id, task in _tasks.items():
        # Remove completed/failed tasks older than 10 minutes (instead of 1 hour)
        if (
            task.status in ["completed", "failed"]
            and task.completed_at
            and current_time - task.completed_at > 600
        ):  # 10 minutes
            tasks_to_remove.append(task_id)

    # Remove old tasks
    for task_id in tasks_to_remove:
        del _tasks[task_id]
        print(f"[CLEANUP] Removed old task: {task_id}")

    # If still too many tasks, remove oldest completed/failed tasks
    if len(_tasks) > MAX_TASK_HISTORY:
        completed_tasks = [
            (task_id, task)
            for task_id, task in _tasks.items()
            if task.status in ["completed", "failed"]
        ]
        completed_tasks.sort(key=lambda x: x[1].completed_at or 0)

        excess_count = len(_tasks) - MAX_TASK_HISTORY
        for i in range(min(excess_count, len(completed_tasks))):
            task_id = completed_tasks[i][0]
            del _tasks[task_id]
            print(f"[CLEANUP] Removed excess task: {task_id}")

    # Count active tasks (only pending and running)
    active_count = sum(1 for task in _tasks.values() if task.status in ["pending", "running"])
    print(
        "[CLEANUP] Task cleanup completed. "
        f"Total tasks: {len(_tasks)}, Active tasks: {active_count}"
    )


def _schedule_task_cleanup():
    """Schedule task cleanup in background."""

    def cleanup_worker():
        try:
            time.sleep(2)  # Small delay to ensure task status is updated
            _cleanup_old_tasks()
        except Exception as e:
            print(f"[CLEANUP] Cleanup worker failed: {e}")

    # Run cleanup in background thread
    _executor.submit(cleanup_worker)


# ============================================================================
# Gallery utilities (extracted from gallery.py)
# ============================================================================

GALLERY_IMAGE_EXTS = (".png", ".jpg", ".jpeg", ".webp", ".bmp")


def _load_gallery_html() -> str:
    """
    Load and modify gallery HTML to work under /gallery/ subdirectory.
    Replaces API paths from root to /gallery/ prefix.
    """
    from ..services.gallery import HTML_PAGE

    # Replace API paths to be under /gallery/ subdirectory
    html = (
        HTML_PAGE.replace("fetch('/manifest.json'", "fetch('/gallery/manifest.json'")
        .replace("fetch('/manifest/'+", "fetch('/gallery/manifest/'+")
        .replace(
            "if(location.pathname!=\"/\")history.replaceState(null,'','/'+location.search)",
            "if(!location.pathname.startsWith(\"/gallery\"))history.replaceState(null,'','/gallery/'+location.search)",
        )
    )

    return html


def _gallery_url_join(*parts: str) -> str:
    """Join URL parts safely."""
    norm = posixpath.join(*[p.replace("\\", "/") for p in parts])
    segs = [s for s in norm.split("/") if s not in ("", ".")]
    return "/".join(quote(s) for s in segs)


def _is_plain_name(name: str) -> bool:
    """Check if name is safe for use in paths."""
    return all(c not in name for c in ("/", "\\")) and name not in (".", "..")


def build_group_list(root_dir: str) -> dict:
    """Build list of groups from gallery directory."""
    groups = []
    try:
        for gname in sorted(os.listdir(root_dir)):
            gpath = os.path.join(root_dir, gname)
            if not os.path.isdir(gpath):
                continue
            has_scene = False
            try:
                for sname in os.listdir(gpath):
                    spath = os.path.join(gpath, sname)
                    if not os.path.isdir(spath):
                        continue
                    if os.path.exists(os.path.join(spath, "scene.glb")) and os.path.exists(
                        os.path.join(spath, "scene.jpg")
                    ):
                        has_scene = True
                        break
            except Exception:
                pass
            if has_scene:
                groups.append({"id": gname, "title": gname})
    except Exception as e:
        print(f"[warn] build_group_list failed: {e}")
    return {"groups": groups}


def build_group_manifest(root_dir: str, group: str) -> dict:
    """Build manifest for a specific group."""
    items = []
    gpath = os.path.join(root_dir, group)
    try:
        if not os.path.isdir(gpath):
            return {"group": group, "items": []}
        for sname in sorted(os.listdir(gpath)):
            spath = os.path.join(gpath, sname)
            if not os.path.isdir(spath):
                continue
            glb_fs = os.path.join(spath, "scene.glb")
            jpg_fs = os.path.join(spath, "scene.jpg")
            if not (os.path.exists(glb_fs) and os.path.exists(jpg_fs)):
                continue
            depth_images = []
            dpath = os.path.join(spath, "depth_vis")
            if os.path.isdir(dpath):
                files = [
                    f
                    for f in os.listdir(dpath)
                    if os.path.splitext(f)[1].lower() in GALLERY_IMAGE_EXTS
                ]
                for fn in sorted(files):
                    depth_images.append(
                        "/gallery/" + _gallery_url_join(group, sname, "depth_vis", fn)
                    )
            items.append(
                {
                    "id": sname,
                    "title": sname,
                    "model": "/gallery/" + _gallery_url_join(group, sname, "scene.glb"),
                    "thumbnail": "/gallery/" + _gallery_url_join(group, sname, "scene.jpg"),
                    "depth_images": depth_images,
                }
            )
    except Exception as e:
        print(f"[warn] build_group_manifest failed for {group}: {e}")
    return {"group": group, "items": items}


def create_app(model_dir: str, device: str = "cuda", gallery_dir: Optional[str] = None) -> FastAPI:
    """Create FastAPI application with model backend."""
    global _backend, _app

    _backend = ModelBackend(model_dir, device)
    _app = FastAPI(
        title="Depth Anything 3 Backend",
        description="Model inference service for Depth Anything 3",
        version="1.0.0",
    )

    # Store gallery directory globally for use in routes
    _gallery_dir = gallery_dir

    @_app.get("/", response_class=HTMLResponse)
    async def root():
        """Home page with navigation to dashboard and gallery."""
        html_content = (
            """
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Depth Anything 3 Backend</title>
    <style>
        :root {
            --tech-blue: #00d4ff;
            --tech-cyan: #00ffcc;
            --tech-purple: #7877c6;
        }

        * {
            box-sizing: border-box;
        }

        /* Dark mode styles */
        @media (prefers-color-scheme: dark) {
            body {
                margin: 0;
                font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
                background: linear-gradient(135deg, #0a0a0a 0%, #1a1a2e 50%, #16213e 100%);
                color: #e8eaed;
                min-height: 100vh;
                display: flex;
                align-items: center;
                justify-content: center;
                position: relative;
                overflow-x: hidden;
            }

            body::before {
                content: '';
                position: fixed;
                top: 0;
                left: 0;
                right: 0;
                bottom: 0;
                background:
                    radial-gradient(circle at 20% 80%, rgba(120, 119, 198, 0.3) 0%, transparent 50%),
                    radial-gradient(circle at 80% 20%, rgba(255, 119, 198, 0.3) 0%, transparent 50%),
                    radial-gradient(circle at 40% 40%, rgba(120, 219, 255, 0.2) 0%, transparent 50%);
                animation: techPulse 8s ease-in-out infinite;
                z-index: -1;
            }

            .container {
                max-width: 800px;
                padding: 40px;
                text-align: center;
                z-index: 1;
            }

            h1 {
                font-size: 3em;
                margin: 0 0 20px 0;
                background: linear-gradient(45deg, var(--tech-blue), var(--tech-cyan), var(--tech-purple));
                background-size: 400% 400%;
                -webkit-background-clip: text;
                background-clip: text;
                color: transparent;
                animation: techGradient 3s ease infinite;
                text-shadow: 0 0 30px rgba(0, 212, 255, 0.5);
            }

            .subtitle {
                font-size: 1.2em;
                opacity: 0.8;
                margin-bottom: 50px;
                color: #a0a0a0;
            }

            .nav-grid {
                display: grid;
                grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
                gap: 24px;
                margin-top: 40px;
            }

            .nav-card {
                background: rgba(0, 0, 0, 0.3);
                border: 1px solid rgba(0, 212, 255, 0.2);
                border-radius: 16px;
                padding: 30px;
                text-decoration: none;
                color: inherit;
                transition: all 0.3s ease;
                backdrop-filter: blur(10px);
            }

            .nav-card:hover {
                transform: translateY(-4px);
                border-color: var(--tech-blue);
                box-shadow: 0 8px 25px rgba(0, 212, 255, 0.2);
            }

            .nav-card h2 {
                margin: 0 0 15px 0;
                font-size: 1.8em;
                color: var(--tech-blue);
            }

            .nav-card p {
                margin: 0;
                opacity: 0.8;
                line-height: 1.6;
            }
        }

        /* Light mode styles */
        @media (prefers-color-scheme: light) {
            body {
                margin: 0;
                font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
                background: linear-gradient(135deg, #f8fafc 0%, #e2e8f0 50%, #cbd5e1 100%);
                color: #1e293b;
                min-height: 100vh;
                display: flex;
                align-items: center;
                justify-content: center;
                position: relative;
                overflow-x: hidden;
            }

            body::before {
                content: '';
                position: fixed;
                top: 0;
                left: 0;
                right: 0;
                bottom: 0;
                background:
                    radial-gradient(circle at 20% 80%, rgba(0, 212, 255, 0.1) 0%, transparent 50%),
                    radial-gradient(circle at 80% 20%, rgba(0, 102, 255, 0.1) 0%, transparent 50%),
                    radial-gradient(circle at 40% 40%, rgba(0, 255, 204, 0.08) 0%, transparent 50%);
                animation: techPulse 8s ease-in-out infinite;
                z-index: -1;
            }

            .container {
                max-width: 800px;
                padding: 40px;
                text-align: center;
                z-index: 1;
            }

            h1 {
                font-size: 3em;
                margin: 0 0 20px 0;
                background: linear-gradient(45deg, #0066ff, #00d4ff, #00ffcc);
                background-size: 400% 400%;
                -webkit-background-clip: text;
                background-clip: text;
                color: transparent;
                animation: techGradient 3s ease infinite;
                text-shadow: 0 0 20px rgba(0, 102, 255, 0.3);
            }

            .subtitle {
                font-size: 1.2em;
                opacity: 0.8;
                margin-bottom: 50px;
                color: #64748b;
            }

            .nav-grid {
                display: grid;
                grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
                gap: 24px;
                margin-top: 40px;
            }

            .nav-card {
                background: rgba(255, 255, 255, 0.8);
                border: 1px solid rgba(0, 212, 255, 0.3);
                border-radius: 16px;
                padding: 30px;
                text-decoration: none;
                color: inherit;
                transition: all 0.3s ease;
                backdrop-filter: blur(10px);
                box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            }

            .nav-card:hover {
                transform: translateY(-4px);
                border-color: #0066ff;
                box-shadow: 0 8px 25px rgba(0, 102, 255, 0.2);
            }

            .nav-card h2 {
                margin: 0 0 15px 0;
                font-size: 1.8em;
                color: #0066ff;
            }

            .nav-card p {
                margin: 0;
                opacity: 0.8;
                line-height: 1.6;
            }
        }

        @keyframes techPulse {
            0%, 100% { opacity: 0.5; }
            50% { opacity: 0.8; }
        }

        @keyframes techGradient {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        .footer {
            margin-top: 50px;
            opacity: 0.6;
            font-size: 0.9em;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Depth Anything 3</h1>
        <p class="subtitle">Model Backend Service</p>
        <div class="nav-grid">
            <a href="/dashboard" class="nav-card">
                <h2>📊 Dashboard</h2>
                <p>Monitor backend status, model information, and inference tasks in real-time.</p>
            </a>
            """
            + (
                '<a href="/gallery/" class="nav-card">'
                "<h2>🎨 Gallery</h2>"
                "<p>Browse 3D reconstructions and depth visualizations from processed scenes.</p>"
                "</a>"
                if _gallery_dir and os.path.exists(_gallery_dir)
                else ""
            )
            + """
        </div>
        <div class="footer">
            <p>Depth Anything 3 Backend API</p>
        </div>
    </div>
</body>
</html>
        """
        )
        return HTMLResponse(html_content)

    @_app.get("/dashboard", response_class=HTMLResponse)
    async def dashboard():
        """HTML dashboard for monitoring backend status and tasks."""
        if _backend is None:
            return HTMLResponse("<h1>Backend not initialized</h1>", status_code=500)

        # Get backend status
        status = _backend.get_status()

        # Safely format status values
        if status["load_time"] is not None:
            load_time_str = f"{status['load_time']:.2f}s"
        else:
            load_time_str = "Not loaded"

        if status["uptime"] is not None:
            uptime_str = f"{status['uptime']:.2f}s"
        else:
            uptime_str = "Not running"

        # Get tasks information
        active_tasks = [task for task in _tasks.values() if task.status in ["pending", "running"]]
        completed_tasks = [
            task for task in _tasks.values() if task.status in ["completed", "failed"]
        ]

        # Generate task HTML
        active_tasks_html = ""
        if active_tasks:
            for task in active_tasks:
                task_details = f"""
                <div class="task-item running">
                    <div class="task-header">
                        <span class="task-id">{task.task_id}</span>
                        <span class="task-status status-{task.status}">{task.status}</span>
                    </div>
                    <div class="task-message">{task.message}</div>
                    <div class="task-params">
                        <small>
                            Images: {task.num_images or 'N/A'} |
                            Format: {task.export_format or 'N/A'} |
                            Method: {task.process_res_method or 'N/A'} |
                            Export Dir: {task.export_dir or 'N/A'}
                        </small>
                        {f'<br><small>Video: {task.video_path}</small>' if task.video_path else ''}
                    </div>
                </div>
                """
                active_tasks_html += task_details
        else:
            active_tasks_html = "<p>No active tasks</p>"

        completed_tasks_html = ""
        if completed_tasks:
            for task in completed_tasks[-10:]:
                task_details = f"""
                <div class="task-item completed">
                    <div class="task-header">
                        <span class="task-id">{task.task_id}</span>
                        <span class="task-status status-{task.status}">{task.status}</span>
                    </div>
                    <div class="task-message">{task.message}</div>
                    <div class="task-params">
                        <small>
                            Images: {task.num_images or 'N/A'} |
                            Format: {task.export_format or 'N/A'} |
                            Method: {task.process_res_method or 'N/A'} |
                            Export Dir: {task.export_dir or 'N/A'}
                        </small>
                        {f'<br><small>Video: {task.video_path}</small>' if task.video_path else ''}
                    </div>
                </div>
                """
                completed_tasks_html += task_details
        else:
            completed_tasks_html = "<p>No completed tasks</p>"

        # Generate HTML
        html_content = f"""
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Depth Anything 3 Backend Dashboard</title>
    <style>
        body {{
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            margin: 0;
            padding: 20px;
            background-color: #f5f5f5;
        }}
        .container {{
            max-width: 1200px;
            margin: 0 auto;
        }}
        .header {{
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 20px;
            text-align: center;
        }}
        .status-grid {{
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }}
        .status-card {{
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }}
        .status-card h3 {{
            margin-top: 0;
            color: #333;
        }}
        .status-item {{
            display: flex;
            justify-content: space-between;
            margin: 10px 0;
            padding: 8px 0;
            border-bottom: 1px solid #eee;
        }}
        .status-item:last-child {{
            border-bottom: none;
        }}
        .status-value {{
            font-weight: bold;
            color: #666;
        }}
        .status-online {{
            color: #28a745;
        }}
        .status-offline {{
            color: #dc3545;
        }}
        .tasks-section {{
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            margin-bottom: 20px;
        }}
        .task-item {{
            background: #f8f9fa;
            padding: 15px;
            margin: 10px 0;
            border-radius: 8px;
            border-left: 4px solid #007bff;
        }}
        .task-item.completed {{
            border-left-color: #28a745;
        }}
        .task-item.failed {{
            border-left-color: #dc3545;
        }}
        .task-item.running {{
            border-left-color: #ffc107;
        }}
        .task-header {{
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 8px;
        }}
        .task-id {{
            font-family: monospace;
            font-size: 12px;
            color: #666;
        }}
        .task-status {{
            padding: 4px 8px;
            border-radius: 4px;
            font-size: 12px;
            font-weight: bold;
        }}
        .status-pending {{
            background: #fff3cd;
            color: #856404;
        }}
        .status-running {{
            background: #d4edda;
            color: #155724;
        }}
        .status-completed {{
            background: #d1ecf1;
            color: #0c5460;
        }}
        .status-failed {{
            background: #f8d7da;
            color: #721c24;
        }}
        .refresh-btn {{
            background: #007bff;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 14px;
        }}
        .refresh-btn:hover {{
            background: #0056b3;
        }}
        .auto-refresh {{
            margin-left: 10px;
        }}
        .timestamp {{
            font-size: 12px;
            color: #666;
            margin-top: 10px;
        }}
        .task-message {{
            font-size: 14px;
            color: #333;
            margin-bottom: 8px;
        }}
        .task-params {{
            font-size: 12px;
            color: #666;
            background: #f8f9fa;
            padding: 6px 8px;
            border-radius: 4px;
            margin-top: 8px;
        }}
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>Depth Anything 3 Backend Dashboard</h1>
            <p>Real-time monitoring of model status and inference tasks</p>
        </div>

        <div class="status-grid">
            <div class="status-card">
                <h3>Model Status</h3>
                <div class="status-item">
                    <span>Status:</span>
                    <span class="status-value {'status-online' if status['model_loaded'] else 'status-offline'}">
                        {'Online' if status['model_loaded'] else 'Offline'}
                    </span>
                </div>
                <div class="status-item">
                    <span>Model Directory:</span>
                    <span class="status-value">{status['model_dir']}</span>
                </div>
                <div class="status-item">
                    <span>Device:</span>
                    <span class="status-value">{status['device']}</span>
                </div>
                <div class="status-item">
                    <span>Load Time:</span>
                    <span class="status-value">{load_time_str}</span>
                </div>
                <div class="status-item">
                    <span>Uptime:</span>
                    <span class="status-value">{uptime_str}</span>
                </div>
            </div>

            <div class="status-card">
                <h3>Task Summary</h3>
                <div class="status-item">
                    <span>Active Tasks:</span>
                    <span class="status-value">{len(active_tasks)}</span>
                </div>
                <div class="status-item">
                    <span>Completed Tasks:</span>
                    <span class="status-value">{len(completed_tasks)}</span>
                </div>
                <div class="status-item">
                    <span>Total Tasks:</span>
                    <span class="status-value">{len(_tasks)}</span>
                </div>
            </div>
        </div>

        <div class="tasks-section">
            <h3>Active Tasks</h3>
            <button class="refresh-btn" onclick="location.reload()">Refresh</button>
            <label class="auto-refresh">
                <input type="checkbox" id="autoRefresh" onchange="toggleAutoRefresh()"> Auto-refresh (5s)
            </label>
            <div class="timestamp">Last updated: <span id="lastUpdate">{time.strftime('%Y-%m-%d %H:%M:%S')}</span></div>

            {active_tasks_html}
        </div>

        <div class="tasks-section">
            <h3>Recent Completed Tasks</h3>
            {completed_tasks_html}
        </div>
    </div>

    <script>
        let autoRefreshInterval;

        function toggleAutoRefresh() {{
            const checkbox = document.getElementById('autoRefresh');
            if (checkbox.checked) {{
                autoRefreshInterval = setInterval(() => {{
                    location.reload();
                }}, 5000);
            }} else {{
                clearInterval(autoRefreshInterval);
            }}
        }}

        // Update timestamp every second
        setInterval(() => {{
            const now = new Date();
            document.getElementById('lastUpdate').textContent = now.toLocaleString();
        }}, 1000);
    </script>
</body>
</html>
        """

        return HTMLResponse(html_content)

    @_app.get("/status")
    async def get_status():
        """Get backend status with GPU memory information."""
        if _backend is None:
            raise HTTPException(status_code=500, detail="Backend not initialized")

        status = _backend.get_status()

        # Add GPU memory information
        gpu_memory = get_gpu_memory_info()
        if gpu_memory:
            status["gpu_memory"] = {
                "total_gb": round(gpu_memory["total_gb"], 2),
                "allocated_gb": round(gpu_memory["allocated_gb"], 2),
                "reserved_gb": round(gpu_memory["reserved_gb"], 2),
                "free_gb": round(gpu_memory["free_gb"], 2),
                "utilization_percent": round(gpu_memory["utilization"], 1),
            }
        else:
            status["gpu_memory"] = None

        return status

    @_app.post("/inference", response_model=InferenceResponse)
    async def run_inference(request: InferenceRequest):
        """Submit inference task and return task ID."""
        global _running_task_id

        if _backend is None:
            raise HTTPException(status_code=500, detail="Backend not initialized")

        # Generate unique task ID
        task_id = str(uuid.uuid4())

        # Create task status
        if _running_task_id is not None:
            status_msg = f"[{task_id}] Task queued (waiting for {_running_task_id} to complete)"
        else:
            status_msg = f"[{task_id}] Task submitted"

        _tasks[task_id] = TaskStatus(
            task_id=task_id,
            status="pending",
            message=status_msg,
            created_at=time.time(),
            export_dir=request.export_dir,
            request=request,
            # Record essential parameters
            num_images=len(request.image_paths),
            export_format=request.export_format,
            process_res_method=request.process_res_method,
            video_path=(
                request.image_paths[0] if request.image_paths else None
            ),  # Use first image path as video reference
        )

        # Add task to queue
        _task_queue.append(task_id)

        # If no task is running, start processing the queue
        if _running_task_id is None:
            _process_next_task()

        return InferenceResponse(
            success=True,
            message="Task submitted successfully",
            task_id=task_id,
            export_dir=request.export_dir,
            export_format=request.export_format,
        )

    @_app.get("/task/{task_id}", response_model=TaskStatus)
    async def get_task_status(task_id: str):
        """Get task status by task ID."""
        if task_id not in _tasks:
            raise HTTPException(status_code=404, detail="Task not found")

        return _tasks[task_id]

    @_app.get("/gpu-memory")
    async def get_gpu_memory():
        """Get detailed GPU memory information."""
        gpu_memory = get_gpu_memory_info()
        if gpu_memory is None:
            return {
                "available": False,
                "message": "CUDA not available or memory info cannot be retrieved",
            }

        return {
            "available": True,
            "total_gb": round(gpu_memory["total_gb"], 2),
            "allocated_gb": round(gpu_memory["allocated_gb"], 2),
            "reserved_gb": round(gpu_memory["reserved_gb"], 2),
            "free_gb": round(gpu_memory["free_gb"], 2),
            "utilization_percent": round(gpu_memory["utilization"], 1),
            "status": (
                "healthy"
                if gpu_memory["utilization"] < 80
                else "warning" if gpu_memory["utilization"] < 95 else "critical"
            ),
        }

    @_app.get("/tasks")
    async def list_tasks():
        """List all tasks."""
        # Separate active and completed tasks
        active_tasks = [task for task in _tasks.values() if task.status in ["pending", "running"]]
        completed_tasks = [
            task for task in _tasks.values() if task.status in ["completed", "failed"]
        ]

        return {
            "tasks": list(_tasks.values()),
            "active_tasks": active_tasks,
            "completed_tasks": completed_tasks,
            "active_count": len(active_tasks),
            "total_count": len(_tasks),
        }

    @_app.post("/cleanup")
    async def manual_cleanup():
        """Manually trigger task cleanup."""
        try:
            _cleanup_old_tasks()
            return {"message": "Cleanup completed", "active_tasks": len(_tasks)}
        except Exception as e:
            raise HTTPException(status_code=500, detail=f"Cleanup failed: {str(e)}")

    @_app.delete("/task/{task_id}")
    async def delete_task(task_id: str):
        """Delete a specific task."""
        if task_id not in _tasks:
            raise HTTPException(status_code=404, detail="Task not found")

        # Only allow deletion of completed/failed tasks
        if _tasks[task_id].status not in ["completed", "failed"]:
            raise HTTPException(status_code=400, detail="Cannot delete running or pending tasks")

        del _tasks[task_id]
        return {"message": f"Task {task_id} deleted successfully"}

    @_app.post("/reload")
    async def reload_model():
        """Reload the model."""
        if _backend is None:
            raise HTTPException(status_code=500, detail="Backend not initialized")

        try:
            _backend.model = None
            _backend.model_loaded = False
            _backend.load_model()
            return {"message": "Model reloaded successfully"}
        except Exception as e:
            raise HTTPException(status_code=500, detail=f"Failed to reload model: {str(e)}")

    # ============================================================================
    # Gallery routes
    # ============================================================================

    if _gallery_dir and os.path.exists(_gallery_dir):
        # Load gallery HTML page (with modified paths for /gallery/ subdirectory)
        _gallery_html = _load_gallery_html()

        @_app.get("/gallery/", response_class=HTMLResponse)
        @_app.get("/gallery", response_class=HTMLResponse)
        async def gallery_home():
            """Gallery home page."""
            return HTMLResponse(_gallery_html)

        @_app.get("/gallery/manifest.json")
        async def gallery_manifest():
            """Get gallery group list."""
            try:
                return build_group_list(_gallery_dir)
            except Exception as e:
                raise HTTPException(
                    status_code=500, detail=f"Failed to build group list: {str(e)}"
                )

        @_app.get("/gallery/manifest/{group}.json")
        async def gallery_group_manifest(group: str):
            """Get manifest for a specific group."""
            if not _is_plain_name(group):
                raise HTTPException(status_code=400, detail="Invalid group name")
            try:
                return build_group_manifest(_gallery_dir, group)
            except Exception as e:
                raise HTTPException(
                    status_code=500, detail=f"Failed to build group manifest: {str(e)}"
                )

        @_app.get("/gallery/{path:path}")
        async def gallery_files(path: str):
            """Serve gallery static files (GLB, JPG, etc.)."""
            # Security check: prevent directory traversal
            path_parts = path.split("/")
            if any(not _is_plain_name(part) for part in path_parts if part):
                raise HTTPException(status_code=400, detail="Invalid path")

            file_path = os.path.join(_gallery_dir, *path_parts)

            # Ensure the file is within gallery directory
            real_file_path = os.path.realpath(file_path)
            real_gallery_dir = os.path.realpath(_gallery_dir)
            if not real_file_path.startswith(real_gallery_dir):
                raise HTTPException(status_code=403, detail="Access denied")

            if not os.path.exists(file_path) or not os.path.isfile(file_path):
                raise HTTPException(status_code=404, detail="File not found")

            return FileResponse(file_path)

    return _app


def start_server(
    model_dir: str,
    device: str = "cuda",
    host: str = "127.0.0.1",
    port: int = 8000,
    gallery_dir: Optional[str] = None,
):
    """Start the backend server."""
    app = create_app(model_dir, device, gallery_dir)

    print("Starting Depth Anything 3 Backend...")
    print(f"Model directory: {model_dir}")
    print(f"Device: {device}")
    print(f"Server: http://{host}:{port}")
    print(f"Dashboard: http://{host}:{port}/dashboard")
    print(f"API Status: http://{host}:{port}/status")

    if gallery_dir and os.path.exists(gallery_dir):
        print(f"Gallery: http://{host}:{port}/gallery/")

    print("=" * 60)
    print("Backend is running! You can now:")
    print(f"  • Open home page: http://{host}:{port}")
    print(f"  • Open dashboard: http://{host}:{port}/dashboard")
    print(f"  • Check API status: http://{host}:{port}/status")

    if gallery_dir and os.path.exists(gallery_dir):
        print(f"  • Browse gallery: http://{host}:{port}/gallery/")

    print("  • Submit inference tasks via API")
    print("=" * 60)

    uvicorn.run(app, host=host, port=port, log_level="info")


if __name__ == "__main__":
    import argparse

    parser = argparse.ArgumentParser(description="Depth Anything 3 Backend Server")
    parser.add_argument("--model-dir", required=True, help="Model directory path")
    parser.add_argument("--device", default="cuda", help="Device to use")
    parser.add_argument("--host", default="127.0.0.1", help="Host to bind to")
    parser.add_argument("--port", type=int, default=8000, help="Port to bind to")
    parser.add_argument("--gallery-dir", help="Gallery directory path (optional)")

    args = parser.parse_args()
    start_server(args.model_dir, args.device, args.host, args.port, args.gallery_dir)



================================================
FILE: src/depth_anything_3/services/gallery.py
================================================
#!/usr/bin/env python3
# flake8: noqa: E501
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

"""
Depth Anything 3 Gallery Server (two-level, single-file)
Now supports paginated depth preview (4 per page).
"""

import argparse
import json
import mimetypes
import os
import posixpath
import sys
from functools import partial
from http import HTTPStatus
from http.server import SimpleHTTPRequestHandler, ThreadingHTTPServer
from urllib.parse import quote, unquote

# ------------------------------ Embedded HTML ------------------------------ #

HTML_PAGE = r"""<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <title>Depth Anything 3 Gallery</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <link rel="icon" href="https://i.postimg.cc/rFSzGJ7J/light-icon.jpg" media="(prefers-color-scheme: light)">
  <link rel="icon" href="https://i.postimg.cc/P5gZfJsf/dark-icon.jpg" media="(prefers-color-scheme: dark)">
  <script type="module" src="https://unpkg.com/@google/model-viewer/dist/model-viewer.min.js"></script>
  <style>
    :root {
      --gap:16px; --card-radius:16px; --shadow:0 8px 24px rgba(0,0,0,.12);
      --maxW:1036px; --maxH:518px;
      --tech-blue: #00d4ff;
      --tech-cyan: #00ffcc;
      --tech-purple: #7877c6;
    }

    *{ box-sizing:border-box }

    /* Dark mode tech theme */
    @media (prefers-color-scheme: dark) {
      body{
        margin:0; font:16px/1.5 system-ui,-apple-system,Segoe UI,Roboto,sans-serif;
        background: linear-gradient(135deg, #0a0a0a 0%, #1a1a2e 50%, #16213e 100%);
        color:#e8eaed;
        position: relative;
        overflow-x: hidden;
      }

      body::before {
        content: '';
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        background:
          radial-gradient(circle at 20% 80%, rgba(120, 119, 198, 0.3) 0%, transparent 50%),
          radial-gradient(circle at 80% 20%, rgba(255, 119, 198, 0.3) 0%, transparent 50%),
          radial-gradient(circle at 40% 40%, rgba(120, 219, 255, 0.2) 0%, transparent 50%);
        animation: techPulse 8s ease-in-out infinite;
        z-index: -1;
      }
    }

    /* Light mode tech theme */
    @media (prefers-color-scheme: light) {
      body{
        margin:0; font:16px/1.5 system-ui,-apple-system,Segoe UI,Roboto,sans-serif;
        background: linear-gradient(135deg, #f8fafc 0%, #e2e8f0 50%, #cbd5e1 100%);
        color:#1e293b;
        position: relative;
        overflow-x: hidden;
      }

      body::before {
        content: '';
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        background:
          radial-gradient(circle at 20% 80%, rgba(0, 212, 255, 0.1) 0%, transparent 50%),
          radial-gradient(circle at 80% 20%, rgba(0, 102, 255, 0.1) 0%, transparent 50%),
          radial-gradient(circle at 40% 40%, rgba(0, 255, 204, 0.08) 0%, transparent 50%);
        animation: techPulse 8s ease-in-out infinite;
        z-index: -1;
      }
    }

    @keyframes techPulse {
      0%, 100% { opacity: 0.5; }
      50% { opacity: 0.8; }
    }

    @keyframes techGradient {
      0% { background-position: 0% 50%; }
      50% { background-position: 100% 50%; }
      100% { background-position: 0% 50%; }
    }

    /* Dark mode header */
    @media (prefers-color-scheme: dark) {
      header{
        padding:20px 24px; position:sticky; top:0;
        background:linear-gradient(180deg,rgba(10,10,10,0.9) 60%,rgba(10,10,10,0));
        z-index:2; border-bottom:1px solid rgba(0, 212, 255, 0.2);
        backdrop-filter: blur(10px);
      }

      h1{
        margin:0; font-size:22px;
        background: linear-gradient(45deg, var(--tech-blue), var(--tech-cyan), var(--tech-purple));
        background-size: 400% 400%;
        -webkit-background-clip: text;
        background-clip: text;
        color: transparent;
        animation: techGradient 3s ease infinite;
        text-shadow: 0 0 30px rgba(0, 212, 255, 0.5);
      }

      .muted{ opacity:.7; font-size:13px; color: #a0a0a0; }

      #backBtn{
        display:none; padding:6px 10px; border-radius:10px;
        border:1px solid rgba(0, 212, 255, 0.3);
        background:rgba(0, 0, 0, 0.3);
        color:#e8eaed; cursor:pointer;
        transition: all 0.3s ease;
      }

      #backBtn:hover {
        border-color: var(--tech-blue);
        box-shadow: 0 0 10px rgba(0, 212, 255, 0.3);
      }

      #search{
        flex:1 1 260px; min-width:240px; max-width:520px;
        padding:10px 14px; border-radius:12px;
        border:1px solid rgba(0, 212, 255, 0.3);
        background:rgba(0, 0, 0, 0.3);
        color:#e8eaed; outline:none;
        transition: all 0.3s ease;
      }

      #search:focus {
        border-color: var(--tech-blue);
        box-shadow: 0 0 10px rgba(0, 212, 255, 0.3);
      }
    }

    /* Light mode header */
    @media (prefers-color-scheme: light) {
      header{
        padding:20px 24px; position:sticky; top:0;
        background:linear-gradient(180deg,rgba(248,250,252,0.9) 60%,rgba(248,250,252,0));
        z-index:2; border-bottom:1px solid rgba(0, 212, 255, 0.3);
        backdrop-filter: blur(10px);
      }

      h1{
        margin:0; font-size:22px;
        background: linear-gradient(45deg, #0066ff, #00d4ff, #00ffcc);
        background-size: 400% 400%;
        -webkit-background-clip: text;
        background-clip: text;
        color: transparent;
        animation: techGradient 3s ease infinite;
        text-shadow: 0 0 20px rgba(0, 102, 255, 0.3);
      }

      .muted{ opacity:.7; font-size:13px; color: #64748b; }

      #backBtn{
        display:none; padding:6px 10px; border-radius:10px;
        border:1px solid rgba(0, 212, 255, 0.4);
        background:rgba(255, 255, 255, 0.8);
        color:#1e293b; cursor:pointer;
        transition: all 0.3s ease;
      }

      #backBtn:hover {
        border-color: #0066ff;
        box-shadow: 0 0 10px rgba(0, 102, 255, 0.3);
      }

      #search{
        flex:1 1 260px; min-width:240px; max-width:520px;
        padding:10px 14px; border-radius:12px;
        border:1px solid rgba(0, 212, 255, 0.4);
        background:rgba(255, 255, 255, 0.8);
        color:#1e293b; outline:none;
        transition: all 0.3s ease;
      }

      #search:focus {
        border-color: #0066ff;
        box-shadow: 0 0 10px rgba(0, 102, 255, 0.3);
      }
    }

    .row{ display:flex; gap:12px; align-items:center; flex-wrap:wrap; justify-content:center; }

    main{ padding:16px 24px 24px; display:grid; place-items:center; }

    .group-wrap{ width:min(900px,100%); }
    .group-list{ list-style:none; margin:0; padding:0; display:grid; gap:10px; }

    /* Dark mode cards */
    @media (prefers-color-scheme: dark) {
      .group-item{
        display:flex; align-items:center; gap:12px; padding:12px 14px;
        background:rgba(0, 0, 0, 0.3); border:1px solid rgba(0, 212, 255, 0.2); border-radius:14px; cursor:pointer;
        transition: all 0.3s ease;
        backdrop-filter: blur(10px);
      }
      .group-item:hover{
        transform: translateY(-1px);
        border-color:var(--tech-blue);
        box-shadow: 0 4px 15px rgba(0, 212, 255, 0.2);
      }

      .card{
        background:rgba(0, 0, 0, 0.3); border:1px solid rgba(0, 212, 255, 0.2); border-radius:var(--card-radius);
        overflow:hidden; box-shadow:var(--shadow);
        transition:all 0.3s ease; cursor:pointer; display:flex; flex-direction:column; max-width:var(--maxW);
        backdrop-filter: blur(10px);
      }
      .card:hover{
        transform:translateY(-2px);
        border-color:var(--tech-blue);
        box-shadow: 0 8px 25px rgba(0, 212, 255, 0.2);
      }
      .thumb-box{
        position:relative; width:100%; aspect-ratio:2/1;
        background:linear-gradient(135deg, #0e121b 0%, #1a1a2e 100%);
        display:grid; place-items:center; overflow:hidden;
        border-bottom: 1px solid rgba(0, 212, 255, 0.1);
      }
      .open{
        font-size:12px; opacity:.7; padding:6px 8px;
        border:1px solid rgba(0, 212, 255, 0.3);
        border-radius:10px;
        background:rgba(0, 212, 255, 0.1);
        transition: all 0.3s ease;
      }
      .open:hover {
        background:rgba(0, 212, 255, 0.2);
        border-color: var(--tech-blue);
      }
    }

    /* Light mode cards */
    @media (prefers-color-scheme: light) {
      .group-item{
        display:flex; align-items:center; gap:12px; padding:12px 14px;
        background:rgba(255, 255, 255, 0.8); border:1px solid rgba(0, 212, 255, 0.3); border-radius:14px; cursor:pointer;
        transition: all 0.3s ease;
        backdrop-filter: blur(10px);
        box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
      }
      .group-item:hover{
        transform: translateY(-1px);
        border-color:#0066ff;
        box-shadow: 0 4px 15px rgba(0, 102, 255, 0.2);
      }

      .card{
        background:rgba(255, 255, 255, 0.8); border:1px solid rgba(0, 212, 255, 0.3); border-radius:var(--card-radius);
        overflow:hidden; box-shadow:0 4px 6px rgba(0, 0, 0, 0.1);
        transition:all 0.3s ease; cursor:pointer; display:flex; flex-direction:column; max-width:var(--maxW);
        backdrop-filter: blur(10px);
      }
      .card:hover{
        transform:translateY(-2px);
        border-color:#0066ff;
        box-shadow: 0 8px 25px rgba(0, 102, 255, 0.2);
      }
      .thumb-box{
        position:relative; width:100%; aspect-ratio:2/1;
        background:linear-gradient(135deg, #f8fafc 0%, #e2e8f0 100%);
        display:grid; place-items:center; overflow:hidden;
        border-bottom: 1px solid rgba(0, 212, 255, 0.2);
      }
      .open{
        font-size:12px; opacity:.7; padding:6px 8px;
        border:1px solid rgba(0, 212, 255, 0.4);
        border-radius:10px;
        background:rgba(0, 212, 255, 0.1);
        transition: all 0.3s ease;
      }
      .open:hover {
        background:rgba(0, 212, 255, 0.2);
        border-color: #0066ff;
      }
    }

    .gname{ font-weight:600; overflow:hidden; text-overflow:ellipsis; white-space:nowrap; width:100%; }
    .grid{
      width:min(1200px,100%);
      display:grid;
      grid-template-columns:repeat(auto-fill,minmax(260px,1fr));
      gap:var(--gap);
      align-items:start;
      justify-items:stretch;
      margin: 0 auto;
      padding: 0 20px;
    }
    .thumb{ max-width:100%; max-height:100%; object-fit:contain; display:block; }
    .meta{ padding:12px 14px; display:flex; justify-content:space-between; align-items:center; gap:8px; }
    .title{ font-weight:600; font-size:14px; overflow:hidden; text-overflow:ellipsis; white-space:nowrap; }
    .empty{ opacity:.6; padding:40px 0; text-align:center; }
    .crumb{ font-size:13px; opacity:.8; }

    .overlay{ position:fixed; inset:0; background:rgba(0,0,0,.6); display:none; place-items:center; padding:20px; z-index:10; }
    .overlay.show{ display:grid; }

    /* Dark mode viewer */
    @media (prefers-color-scheme: dark) {
      .viewer{
        inline-size:min(92vw,var(--maxW));
        block-size:min(82vh,var(--maxH));
        background:#0e121b; border:1px solid rgba(0, 212, 255, 0.3); border-radius:18px; overflow:hidden; position:relative; box-shadow:0 12px 36px rgba(0,0,0,.35);
        display:grid;
      }
      .chip{ background:rgba(0,0,0,.45); border:1px solid rgba(0, 212, 255, 0.3); color:#e8eaed; padding:6px 10px; border-radius:12px; font-size:12px; max-width:60%; overflow:hidden; text-overflow:ellipsis; white-space:nowrap; }
      .btn{ margin-left:auto; background:rgba(0, 0, 0, 0.3); color:#e8eaed; border:1px solid rgba(0, 212, 255, 0.3); border-radius:10px; padding:6px 10px; cursor:pointer; transition: all 0.3s ease; }
      .btn:hover { border-color: var(--tech-blue); box-shadow: 0 0 10px rgba(0, 212, 255, 0.3); }
      .mv-box{ width:100%; aspect-ratio:1036/518; background:#0b0d12; border:1px solid rgba(0, 212, 255, 0.2); border-radius:12px; overflow:hidden; }
      .mv-box model-viewer{ width:100%; height:100%; background:#0b0d12; }
      .res-cell{ position:relative; width:100%; aspect-ratio:2/1; background:#0e121b; border:1px solid rgba(0, 212, 255, 0.2); border-radius:12px; overflow:hidden; display:grid; place-items:center; }
      .res-empty{ position:absolute; inset:0; display:grid; place-items:center; opacity:.55; font-size:12px; color:#9aa0a6; }
      .download-icon{ background:rgba(0, 0, 0, 0.6); border:1px solid rgba(0, 212, 255, 0.3); color:#e8eaed; box-shadow:0 4px 12px rgba(0,0,0,0.3); }
      .download-icon:hover{ background:rgba(0, 212, 255, 0.2); border-color:var(--tech-blue); box-shadow:0 0 20px rgba(0, 212, 255, 0.4); transform:scale(1.05); }
    }

    /* Light mode viewer */
    @media (prefers-color-scheme: light) {
      .viewer{
        inline-size:min(92vw,var(--maxW));
        block-size:min(82vh,var(--maxH));
        background:#f8fafc; border:1px solid rgba(0, 212, 255, 0.4); border-radius:18px; overflow:hidden; position:relative; box-shadow:0 12px 36px rgba(0,0,0,.15);
        display:grid;
      }
      .chip{ background:rgba(255,255,255,0.8); border:1px solid rgba(0, 212, 255, 0.4); color:#1e293b; padding:6px 10px; border-radius:12px; font-size:12px; max-width:60%; overflow:hidden; text-overflow:ellipsis; white-space:nowrap; }
      .btn{ margin-left:auto; background:rgba(255, 255, 255, 0.8); color:#1e293b; border:1px solid rgba(0, 212, 255, 0.4); border-radius:10px; padding:6px 10px; cursor:pointer; transition: all 0.3s ease; }
      .btn:hover { border-color: #0066ff; box-shadow: 0 0 10px rgba(0, 102, 255, 0.3); }
      .mv-box{ width:100%; aspect-ratio:1036/518; background:#f8fafc; border:1px solid rgba(0, 212, 255, 0.3); border-radius:12px; overflow:hidden; }
      .mv-box model-viewer{ width:100%; height:100%; background:#f8fafc; }
      .res-cell{ position:relative; width:100%; aspect-ratio:2/1; background:#f8fafc; border:1px solid rgba(0, 212, 255, 0.3); border-radius:12px; overflow:hidden; display:grid; place-items:center; }
      .res-empty{ position:absolute; inset:0; display:grid; place-items:center; opacity:.55; font-size:12px; color:#64748b; }
      .download-icon{ background:rgba(255, 255, 255, 0.9); border:1px solid rgba(0, 212, 255, 0.4); color:#1e293b; box-shadow:0 4px 12px rgba(0,0,0,0.15); }
      .download-icon:hover{ background:rgba(0, 212, 255, 0.2); border-color:#0066ff; box-shadow:0 0 20px rgba(0, 102, 255, 0.4); transform:scale(1.05); }
    }

    .viewer-header{ position:absolute; top:8px; left:8px; right:8px; display:flex; gap:8px; align-items:center; z-index:2; }
    .viewer-body{ height:100%; display:grid; grid-template-rows:auto auto; gap:12px; padding:36px 8px 8px 8px; overflow:auto; }
    .res-grid{ display:grid; grid-template-columns:1fr 1fr; gap:8px; }
    .res-img{ max-width:100%; max-height:100%; object-fit:contain; display:block; }
    .download-icon{ position:absolute; bottom:16px; right:16px; width:44px; height:44px; border-radius:50%; display:grid; place-items:center; font-size:20px; cursor:pointer; z-index:3; transition:all 0.3s ease; }

    /* Pagination controls */
    .pager {
      grid-column: 1 / -1;
      justify-content: center;
      align-items: center;
      display: flex;
      gap: 16px;
      margin-top: 8px;
      font-size: 13px;
      text-align: center;
    }

    /* Dark mode pagination */
    @media (prefers-color-scheme: dark) {
      .pager {
        color: #ccc;
      }
      .pager button {
        padding: 4px 10px;
        border-radius: 8px;
        border: 1px solid rgba(0, 212, 255, 0.3);
        background: rgba(0, 0, 0, 0.3);
        color: #e8eaed;
        cursor: pointer;
        transition: all 0.3s ease;
      }
      .pager button:hover:not(:disabled) {
        border-color: var(--tech-blue);
        box-shadow: 0 0 8px rgba(0, 212, 255, 0.2);
      }
      .pager button:disabled {
        opacity: 0.4;
        cursor: not-allowed;
      }
    }

    /* Light mode pagination */
    @media (prefers-color-scheme: light) {
      .pager {
        color: #64748b;
      }
      .pager button {
        padding: 4px 10px;
        border-radius: 8px;
        border: 1px solid rgba(0, 212, 255, 0.4);
        background: rgba(255, 255, 255, 0.8);
        color: #1e293b;
        cursor: pointer;
        transition: all 0.3s ease;
      }
      .pager button:hover:not(:disabled) {
        border-color: #0066ff;
        box-shadow: 0 0 8px rgba(0, 102, 255, 0.2);
      }
      .pager button:disabled {
        opacity: 0.4;
        cursor: not-allowed;
      }
    }

    /* Intro card styles */
    @media (prefers-color-scheme: dark) {
      .intro-card {
        background: linear-gradient(135deg, rgba(0, 212, 255, 0.1) 0%, rgba(0, 102, 255, 0.1) 100%);
        border: 1px solid rgba(0, 212, 255, 0.2);
        backdrop-filter: blur(10px);
      }
      .intro-title {
        background: linear-gradient(45deg, var(--tech-blue), var(--tech-cyan), var(--tech-purple));
        background-size: 400% 400%;
        -webkit-background-clip: text;
        background-clip: text;
        color: transparent;
        animation: techGradient 3s ease infinite;
        text-shadow: 0 0 20px rgba(0, 212, 255, 0.3);
      }
      .intro-description {
        color: #e0e0e0;
      }
    }

    @media (prefers-color-scheme: light) {
      .intro-card {
        background: linear-gradient(135deg, rgba(0, 212, 255, 0.05) 0%, rgba(0, 102, 255, 0.05) 100%);
        border: 1px solid rgba(0, 212, 255, 0.3);
        backdrop-filter: blur(10px);
        box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
      }
      .intro-title {
        background: linear-gradient(45deg, #0066ff, #00d4ff, #00ffcc);
        background-size: 400% 400%;
        -webkit-background-clip: text;
        background-clip: text;
        color: transparent;
        animation: techGradient 3s ease infinite;
        text-shadow: 0 0 15px rgba(0, 102, 255, 0.2);
      }
      .intro-description {
        color: #334155;
      }
    }

    footer{
      opacity:.55;
      font-size:12px;
      padding:12px 24px 24px;
      text-align:center;
      display:flex;
      justify-content:center;
      align-items:center;
      width:100%;
    }
  </style>
</head>
<body>
  <header>
    <div class="row">
      <button id="backBtn">← Back</button>
      <h1 id="pageTitle">Depth Anything 3 Gallery</h1>
      <span id="crumb" class="crumb"></span>
      <input id="search" placeholder="Search…" />
    </div>
    <div class="muted" id="hint" style="text-align: center;">Level 1 shows groups only; click a group to browse scenes and previews.</div>
  </header>

  <main>
    <!-- Tech intro card -->
    <div class="intro-card" style="margin-bottom: 30px; padding: 25px; border-radius: 15px; text-align: center; max-width: 800px;">
      <h2 class="intro-title" style="margin: 0 0 15px 0; font-size: 1.8em; font-weight: 700;">
        🎯 Depth Anything 3 Gallery
      </h2>
      <p class="intro-description" style="margin: 0; font-size: 1.1em; line-height: 1.6;">
        Explore 3D reconstructions and depth visualizations from Depth Anything 3.
        Browse through groups of scenes, preview 3D models, and examine depth maps interactively.
      </p>
    </div>

    <div id="level1" class="group-wrap" aria-live="polite">
      <ul id="groupList" class="group-list"></ul>
      <div id="groupEmpty" class="empty" style="display:none;">No available groups</div>
    </div>

    <div id="level2" style="display:none; width:100%;" aria-live="polite">
      <div id="topPager" class="pager" style="margin-bottom: 16px;"></div>
      <div id="grid" class="grid"></div>
      <div id="sceneEmpty" class="empty" style="display:none;">No available scenes in this group</div>
    </div>
  </main>

  <div id="overlay" class="overlay" role="dialog" aria-modal="true" aria-label="3D Preview">
    <div class="viewer" id="viewer">
      <div class="viewer-header">
        <div id="viewerTitle" class="chip">Loading…</div>
        <button id="toggleView" class="btn" title="Toggle between 3D-only and resource view">Resource View</button>
        <button id="closeBtn" class="btn">Close</button>
      </div>
      <div id="downloadBtn" class="download-icon" title="Download GLB model">⬇</div>
      <div class="viewer-body">
        <div class="mv-box"><model-viewer id="mv"
          src=""
          ar
          camera-controls
          auto-rotate
          interaction-prompt="auto"
          shadow-intensity="0.7"
          exposure="1.0"
          alt="GLB Preview"></model-viewer></div>
        <div class="res-grid" id="resGrid" hidden></div>
      </div>
    </div>
  </div>

  <footer>Depth Anything 3 Gallery. Copyright 2025 Depth Anything 3 authors.</footer>

<script>
const level1=document.getElementById('level1'),level2=document.getElementById('level2'),pageTitle=document.getElementById('pageTitle'),crumb=document.getElementById('crumb'),backBtn=document.getElementById('backBtn'),hint=document.getElementById('hint'),searchInput=document.getElementById('search'),groupList=document.getElementById('groupList'),groupEmpty=document.getElementById('groupEmpty'),topPager=document.getElementById('topPager'),grid=document.getElementById('grid'),sceneEmpty=document.getElementById('sceneEmpty'),overlay=document.getElementById('overlay'),viewer=document.getElementById('viewer'),mv=document.getElementById('mv'),viewerTitle=document.getElementById('viewerTitle'),downloadBtn=document.getElementById('downloadBtn'),toggleViewBtn=document.getElementById('toggleView'),closeBtn=document.getElementById('closeBtn'),resGrid=document.getElementById('resGrid');
let GROUPS=[],SCENES=[],currentGroup=null,currentScene=null,currentPage=1,currentScenePage=1;

const qs=()=>new URLSearchParams(location.search);
async function loadGroups(){const r=await fetch('/manifest.json',{cache:'no-store'});if(!r.ok)throw new Error(r.status+' '+r.statusText);const j=await r.json();GROUPS=j.groups||[];renderGroups(GROUPS);}
async function loadScenes(g){const r=await fetch('/manifest/'+encodeURIComponent(g)+'.json',{cache:'no-store'});if(!r.ok)throw new Error(r.status+' '+r.statusText);const j=await r.json();SCENES=j.items||[];const p=parseInt(qs().get('page'))||1;renderScenes(SCENES,p);}
function renderGroups(list){groupList.innerHTML='';const q=searchInput.value.trim().toLowerCase();const f=list.filter(g=>(g.title||g.id||'').toLowerCase().includes(q));if(!f.length){groupEmpty.style.display='';return;}groupEmpty.style.display='none';for(const g of f){const li=document.createElement('li');li.className='group-item';li.title=g.title||g.id;li.onclick=()=>enterLevel2(g.id,{push:true});const name=document.createElement('div');name.className='gname';name.textContent=g.title||g.id;li.appendChild(name);groupList.appendChild(li);}}
function renderScenes(list,page=1){topPager.innerHTML='';grid.innerHTML='';const q=searchInput.value.trim().toLowerCase();const f=list.filter(x=>(x.title||'').toLowerCase().includes(q)||(x.id||'').toLowerCase().includes(q));if(!f.length){sceneEmpty.style.display='';topPager.style.display='none';return;}sceneEmpty.style.display='none';topPager.style.display='flex';const perPage=16;const total=f.length;const totalPages=Math.max(1,Math.ceil(total/perPage));currentScenePage=page;const u=new URL(location.href);u.searchParams.set('page',page);history.replaceState(null,'',u);const subset=f.slice((page-1)*perPage,page*perPage);for(const i of subset){const c=document.createElement('div');c.className='card';c.title=i.title;const b=document.createElement('div');b.className='thumb-box';const img=document.createElement('img');img.className='thumb';img.loading='lazy';img.alt=i.title;img.src=i.thumbnail;b.appendChild(img);const m=document.createElement('div');m.className='meta';const t=document.createElement('div');t.className='title';t.textContent=i.title;const o=document.createElement('div');o.className='open';o.textContent='Preview';m.appendChild(t);m.appendChild(o);c.appendChild(b);c.appendChild(m);c.onclick=()=>openViewer(i,{push:true});grid.appendChild(c);}function buildPager(){const pg=document.createElement('div');pg.className='pager';const prev=document.createElement('button');prev.textContent='← Prev';prev.disabled=page<=1;prev.onclick=()=>renderScenes(list,page-1);const info=document.createElement('span');info.textContent=`${page} / ${totalPages}`;const next=document.createElement('button');next.textContent='Next →';next.disabled=page>=totalPages;next.onclick=()=>renderScenes(list,page+1);pg.appendChild(prev);pg.appendChild(info);pg.appendChild(next);return pg;}topPager.innerHTML='';topPager.appendChild(buildPager());grid.appendChild(buildPager());}
function enterLevel1({push=false}={}){currentGroup=null;pageTitle.textContent='Depth Anything 3 Gallery';crumb.textContent='';backBtn.style.display='none';hint.style.display='';level1.style.display='';level2.style.display='none';overlay.classList.remove('show');mv.src='';const u=new URL(location.href);u.searchParams.delete('group');u.searchParams.delete('id');u.searchParams.delete('page');push?history.pushState(null,'',u):history.replaceState(null,'',u);searchInput.value='';loadGroups().catch(e=>{groupList.innerHTML='';groupEmpty.style.display='';groupEmpty.textContent='Failed to load groups: '+e;});}
async function enterLevel2(g,{push=false}={}){currentGroup=g;pageTitle.textContent=g;crumb.textContent='(group)';backBtn.style.display='';hint.style.display='none';level1.style.display='none';level2.style.display='';overlay.classList.remove('show');mv.src='';const u=new URL(location.href);u.searchParams.set('group',g);u.searchParams.delete('id');push?history.pushState(null,'',u):history.replaceState(null,'',u);searchInput.value='';try{await loadScenes(g);const id=qs().get('id');if(id){const hit=SCENES.find(x=>x.id===id);if(hit)openViewer(hit,{push:false});}}catch(e){grid.innerHTML='';sceneEmpty.style.display='';sceneEmpty.textContent='Failed to load scenes: '+e;}}
function buildResGrid(i,page=1){
  resGrid.innerHTML='';
  const imgs=i.depth_images||[];
  const perPage=4;
  const total=imgs.length;
  const totalPages=Math.max(1, Math.ceil(total/perPage));
  currentPage=page;

  const subset=imgs.slice((page-1)*perPage,(page-1)*perPage+perPage);
  for(let k=0;k<4;k++){
    const cell=document.createElement('div');
    cell.className='res-cell';
    if(subset[k]){
      const im=document.createElement('img');
      im.className='res-img';
      im.src=subset[k];
      im.alt=(i.title||'scene')+' depth '+(k+1+(page-1)*perPage);
      im.loading='lazy';
      cell.appendChild(im);
    } else {
      const ph=document.createElement('div');
      ph.className='res-empty';
      ph.textContent='N/A';
      cell.appendChild(ph);
    }
    resGrid.appendChild(cell);
  }

  // pagination bar (always rebuilt)
  const pager=document.createElement('div');
  pager.className='pager';

  const prev=document.createElement('button');
  prev.textContent='← Prev';
  prev.disabled=page<=1;
  prev.onclick=()=>buildResGrid(i,page-1);

  const info=document.createElement('span');
  info.textContent=`${page} / ${totalPages}`;

  const next=document.createElement('button');
  next.textContent='Next →';
  next.disabled=page>=totalPages;
  next.onclick=()=>buildResGrid(i,page+1);

  pager.appendChild(prev);
  pager.appendChild(info);
  pager.appendChild(next);
  resGrid.appendChild(pager);
}
function openViewer(i,{push=false}={}){currentScene=i;viewerTitle.textContent=i.title;mv.src=i.model;overlay.classList.add('show');resGrid.hidden=true;toggleViewBtn.textContent='Resource View';viewer.style.blockSize='min(82vh,var(--maxH))';buildResGrid(i,1);downloadBtn.onclick=()=>{const a=document.createElement('a');a.href=i.model;a.download=i.title+'.glb';a.click();};if(push){const u=new URL(location.href);if(!u.searchParams.get('group'))u.searchParams.set('group',currentGroup||'');u.searchParams.set('id',i.id);history.pushState(null,'',u);}}
function toggleView(){const hidden=!resGrid.hidden;resGrid.hidden=hidden;toggleViewBtn.textContent=hidden?'Resource View':'3D Only';viewer.style.blockSize=hidden?'min(82vh,var(--maxH))':'min(92vh,900px)';}
function closeViewer(){const hasId=!!qs().get('id');if(hasId&&history.length>1){history.back();return;}const u=new URL(location.href);u.searchParams.delete('id');history.replaceState(null,'',u);overlay.classList.remove('show');mv.src='';}
overlay.onclick=e=>{if(e.target===overlay)closeViewer();};closeBtn.onclick=closeViewer;toggleViewBtn.onclick=toggleView;backBtn.onclick=()=>history.back();
searchInput.oninput=()=>{!qs().get('group')?renderGroups(GROUPS):renderScenes(SCENES,1);};
window.onpopstate=()=>routeFromURL();
async function routeFromURL(){if(location.pathname!="/")history.replaceState(null,'','/'+location.search);const g=qs().get('group');const id=qs().get('id');if(!g){enterLevel1({push:false});return;}await enterLevel2(g,{push:false});if(id){const hit=SCENES.find(x=>x.id===id);if(hit)openViewer(hit,{push:false});else{overlay.classList.remove('show');mv.src='';}}else{overlay.classList.remove('show');mv.src='';}}
routeFromURL();
</script>
</body>
</html>
"""

# ------------------------------ Utilities ------------------------------ #

IMAGE_EXTS = (".png", ".jpg", ".jpeg", ".webp", ".bmp")


def _url_join(*parts: str) -> str:
    norm = posixpath.join(*[p.replace("\\", "/") for p in parts])
    segs = [s for s in norm.split("/") if s not in ("", ".")]
    return "/".join(quote(s) for s in segs)


def _is_plain_name(name: str) -> bool:
    return all(c not in name for c in ("/", "\\")) and name not in (".", "..")


def build_group_list(root_dir: str) -> dict:
    groups = []
    try:
        for gname in sorted(os.listdir(root_dir)):
            gpath = os.path.join(root_dir, gname)
            if not os.path.isdir(gpath):
                continue
            has_scene = False
            try:
                for sname in os.listdir(gpath):
                    spath = os.path.join(gpath, sname)
                    if not os.path.isdir(spath):
                        continue
                    if os.path.exists(os.path.join(spath, "scene.glb")) and os.path.exists(
                        os.path.join(spath, "scene.jpg")
                    ):
                        has_scene = True
                        break
            except Exception:
                pass
            if has_scene:
                groups.append({"id": gname, "title": gname})
    except Exception as e:
        print(f"[warn] build_group_list failed: {e}", file=sys.stderr)
    return {"groups": groups}


def build_group_manifest(root_dir: str, group: str) -> dict:
    items = []
    gpath = os.path.join(root_dir, group)
    try:
        if not os.path.isdir(gpath):
            return {"group": group, "items": []}
        for sname in sorted(os.listdir(gpath)):
            spath = os.path.join(gpath, sname)
            if not os.path.isdir(spath):
                continue
            glb_fs = os.path.join(spath, "scene.glb")
            jpg_fs = os.path.join(spath, "scene.jpg")
            if not (os.path.exists(glb_fs) and os.path.exists(jpg_fs)):
                continue
            depth_images = []
            dpath = os.path.join(spath, "depth_vis")
            if os.path.isdir(dpath):
                files = [
                    f for f in os.listdir(dpath) if os.path.splitext(f)[1].lower() in IMAGE_EXTS
                ]
                for fn in sorted(files):
                    depth_images.append("/" + _url_join(group, sname, "depth_vis", fn))
            items.append(
                {
                    "id": sname,
                    "title": sname,
                    "model": "/" + _url_join(group, sname, "scene.glb"),
                    "thumbnail": "/" + _url_join(group, sname, "scene.jpg"),
                    "depth_images": depth_images,
                }
            )
    except Exception as e:
        print(f"[warn] build_group_manifest failed for {group}: {e}", file=sys.stderr)
    return {"group": group, "items": items}


class GalleryHandler(SimpleHTTPRequestHandler):
    def __init__(self, *args, directory=None, **kwargs):
        super().__init__(*args, directory=directory, **kwargs)

    def do_GET(self):
        if self.path in ("/", "/index.html") or self.path.startswith("/?"):
            content = HTML_PAGE.encode("utf-8")
            self.send_response(HTTPStatus.OK)
            self.send_header("Content-Type", "text/html; charset=utf-8")
            self.send_header("Content-Length", str(len(content)))
            self.send_header("Cache-Control", "no-store")
            self.end_headers()
            self.wfile.write(content)
            return
        if self.path == "/manifest.json":
            data = json.dumps(
                build_group_list(self.directory), ensure_ascii=False, indent=2
            ).encode("utf-8")
            self.send_response(HTTPStatus.OK)
            self.send_header("Content-Type", "application/json; charset=utf-8")
            self.send_header("Content-Length", str(len(data)))
            self.send_header("Cache-Control", "no-store")
            self.end_headers()
            self.wfile.write(data)
            return
        if self.path.startswith("/manifest/") and self.path.endswith(".json"):
            group_enc = self.path[len("/manifest/") : -len(".json")]
            try:
                group = unquote(group_enc)
            except Exception:
                group = group_enc
            if not _is_plain_name(group):
                self.send_error(HTTPStatus.BAD_REQUEST, "Invalid group name")
                return
            data = json.dumps(
                build_group_manifest(self.directory, group), ensure_ascii=False, indent=2
            ).encode("utf-8")
            self.send_response(HTTPStatus.OK)
            self.send_header("Content-Type", "application/json; charset=utf-8")
            self.send_header("Content-Length", str(len(data)))
            self.send_header("Cache-Control", "no-store")
            self.end_headers()
            self.wfile.write(data)
            return
        if self.path == "/favicon.ico":
            self.send_response(HTTPStatus.NO_CONTENT)
            self.end_headers()
            return
        return super().do_GET()

    def list_directory(self, path):
        self.send_error(HTTPStatus.NOT_FOUND, "Directory listing disabled")
        return None


def gallery():
    parser = argparse.ArgumentParser(
        description="Depth Anything 3 Gallery Server (two-level, with pagination)"
    )
    parser.add_argument(
        "-d", "--dir", required=True, help="Gallery root directory (two-level: group/scene)"
    )
    parser.add_argument("-p", "--port", type=int, default=8000, help="Port (default 8000)")
    parser.add_argument("--host", default="127.0.0.1", help="Host address (default 127.0.0.1)")
    parser.add_argument("--open", action="store_true", help="Open browser after launch")
    args = parser.parse_args()

    root_dir = os.path.abspath(args.dir)
    if not os.path.isdir(root_dir):
        print(f"[error] Directory not found: {root_dir}", file=sys.stderr)
        sys.exit(1)

    Handler = partial(GalleryHandler, directory=root_dir)
    server = ThreadingHTTPServer((args.host, args.port), Handler)

    addr = f"http://{args.host}:{args.port}/"
    print(f"[info] Serving gallery from: {root_dir}")
    print(f"[info] Open: {addr}")

    if args.open:
        try:
            import webbrowser

            webbrowser.open(addr)
        except Exception as e:
            print(f"[warn] Failed to open browser: {e}", file=sys.stderr)

    try:
        server.serve_forever()
    except KeyboardInterrupt:
        print("\n[info] Shutting down...")
    finally:
        server.server_close()


def main():
    """Main entry point for gallery server."""
    mimetypes.add_type("model/gltf-binary", ".glb")
    gallery()


if __name__ == "__main__":
    main()



================================================
FILE: src/depth_anything_3/services/inference_service.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

"""
Unified Inference Service
Provides unified interface for local and remote inference
"""

from typing import Any, Dict, List, Optional, Union
import numpy as np
import requests
import typer

from ..api import DepthAnything3


class InferenceService:
    """Unified inference service class"""

    def __init__(self, model_dir: str, device: str = "cuda"):
        self.model_dir = model_dir
        self.device = device
        self.model = None

    def load_model(self):
        """Load model"""
        if self.model is None:
            typer.echo(f"Loading model from {self.model_dir}...")
            self.model = DepthAnything3.from_pretrained(self.model_dir).to(self.device)
        return self.model

    def run_local_inference(
        self,
        image_paths: List[str],
        export_dir: str,
        export_format: str = "mini_npz-glb",
        process_res: int = 504,
        process_res_method: str = "upper_bound_resize",
        export_feat_layers: List[int] = None,
        extrinsics: Optional[np.ndarray] = None,
        intrinsics: Optional[np.ndarray] = None,
        align_to_input_ext_scale: bool = True,
        use_ray_pose: bool = False,
        ref_view_strategy: str = "saddle_balanced",
        conf_thresh_percentile: float = 40.0,
        num_max_points: int = 1_000_000,
        show_cameras: bool = True,
        feat_vis_fps: int = 15,
    ) -> Any:
        """Run local inference"""
        if export_feat_layers is None:
            export_feat_layers = []

        model = self.load_model()

        # Prepare inference parameters
        inference_kwargs = {
            "image": image_paths,
            "export_dir": export_dir,
            "export_format": export_format,
            "process_res": process_res,
            "process_res_method": process_res_method,
            "export_feat_layers": export_feat_layers,
            "align_to_input_ext_scale": align_to_input_ext_scale,
            "use_ray_pose": use_ray_pose,
            "ref_view_strategy": ref_view_strategy,
            "conf_thresh_percentile": conf_thresh_percentile,
            "num_max_points": num_max_points,
            "show_cameras": show_cameras,
            "feat_vis_fps": feat_vis_fps,
        }

        # Add pose data (if exists)
        if extrinsics is not None:
            inference_kwargs["extrinsics"] = extrinsics
        if intrinsics is not None:
            inference_kwargs["intrinsics"] = intrinsics

        # Run inference
        typer.echo(f"Running inference on {len(image_paths)} images...")
        prediction = model.inference(**inference_kwargs)

        typer.echo(f"Results saved to {export_dir}")
        typer.echo(f"Export format: {export_format}")

        return prediction

    def run_backend_inference(
        self,
        image_paths: List[str],
        export_dir: str,
        backend_url: str,
        export_format: str = "mini_npz-glb",
        process_res: int = 504,
        process_res_method: str = "upper_bound_resize",
        export_feat_layers: List[int] = None,
        extrinsics: Optional[np.ndarray] = None,
        intrinsics: Optional[np.ndarray] = None,
        align_to_input_ext_scale: bool = True,
        use_ray_pose: bool = False,
        ref_view_strategy: str = "saddle_balanced",
        conf_thresh_percentile: float = 40.0,
        num_max_points: int = 1_000_000,
        show_cameras: bool = True,
        feat_vis_fps: int = 15,
    ) -> Dict[str, Any]:
        """Run backend inference"""
        if export_feat_layers is None:
            export_feat_layers = []

        # Check backend status
        if not self._check_backend_status(backend_url):
            raise typer.BadParameter(f"Backend service is not running at {backend_url}")

        # Prepare payload
        payload = {
            "image_paths": image_paths,
            "export_dir": export_dir,
            "export_format": export_format,
            "process_res": process_res,
            "process_res_method": process_res_method,
            "export_feat_layers": export_feat_layers,
            "align_to_input_ext_scale": align_to_input_ext_scale,
            "use_ray_pose": use_ray_pose,
            "ref_view_strategy": ref_view_strategy,
            "conf_thresh_percentile": conf_thresh_percentile,
            "num_max_points": num_max_points,
            "show_cameras": show_cameras,
            "feat_vis_fps": feat_vis_fps,
        }

        # Add pose data (if exists)
        if extrinsics is not None:
            payload["extrinsics"] = [ext.astype(np.float64).tolist() for ext in extrinsics]
        if intrinsics is not None:
            payload["intrinsics"] = [intr.astype(np.float64).tolist() for intr in intrinsics]

        # Submit task
        typer.echo("Submitting inference task to backend...")
        try:
            response = requests.post(f"{backend_url}/inference", json=payload, timeout=30)
            response.raise_for_status()
            result = response.json()

            if result["success"]:
                task_id = result["task_id"]
                typer.echo("Task submitted successfully!")
                typer.echo(f"Task ID: {task_id}")
                typer.echo(f"Results will be saved to: {export_dir}")
                typer.echo(f"Check backend logs for progress updates with task ID: {task_id}")
                return result
            else:
                raise typer.BadParameter(
                    f"Backend inference submission failed: {result['message']}"
                )
        except requests.exceptions.RequestException as e:
            raise typer.BadParameter(f"Backend inference submission failed: {e}")

    def _check_backend_status(self, backend_url: str) -> bool:
        """Check backend status"""
        try:
            response = requests.get(f"{backend_url}/status", timeout=5)
            return response.status_code == 200
        except Exception:
            return False


def run_inference(
    image_paths: List[str],
    export_dir: str,
    model_dir: str,
    device: str = "cuda",
    backend_url: Optional[str] = None,
    export_format: str = "mini_npz-glb",
    process_res: int = 504,
    process_res_method: str = "upper_bound_resize",
    export_feat_layers: List[int] = None,
    extrinsics: Optional[np.ndarray] = None,
    intrinsics: Optional[np.ndarray] = None,
    align_to_input_ext_scale: bool = True,
    use_ray_pose: bool = False,
    ref_view_strategy: str = "saddle_balanced",
    conf_thresh_percentile: float = 40.0,
    num_max_points: int = 1_000_000,
    show_cameras: bool = True,
    feat_vis_fps: int = 15,
) -> Union[Any, Dict[str, Any]]:
    """Unified inference interface"""

    service = InferenceService(model_dir, device)

    if backend_url:
        return service.run_backend_inference(
            image_paths=image_paths,
            export_dir=export_dir,
            backend_url=backend_url,
            export_format=export_format,
            process_res=process_res,
            process_res_method=process_res_method,
            export_feat_layers=export_feat_layers,
            extrinsics=extrinsics,
            intrinsics=intrinsics,
            align_to_input_ext_scale=align_to_input_ext_scale,
            use_ray_pose=use_ray_pose,
            ref_view_strategy=ref_view_strategy,
            conf_thresh_percentile=conf_thresh_percentile,
            num_max_points=num_max_points,
            show_cameras=show_cameras,
            feat_vis_fps=feat_vis_fps,
        )
    else:
        return service.run_local_inference(
            image_paths=image_paths,
            export_dir=export_dir,
            export_format=export_format,
            process_res=process_res,
            process_res_method=process_res_method,
            export_feat_layers=export_feat_layers,
            extrinsics=extrinsics,
            intrinsics=intrinsics,
            align_to_input_ext_scale=align_to_input_ext_scale,
            use_ray_pose=use_ray_pose,
            ref_view_strategy=ref_view_strategy,
            conf_thresh_percentile=conf_thresh_percentile,
            num_max_points=num_max_points,
            show_cameras=show_cameras,
            feat_vis_fps=feat_vis_fps,
        )



================================================
FILE: src/depth_anything_3/services/input_handlers.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

"""
Input Processing Service
Handles different types of inputs (image, images, colmap, video)
"""

import glob
import os
from typing import List, Tuple
import cv2
import numpy as np
import typer

from ..utils.read_write_model import read_model


class InputHandler:
    """Base input handler class"""

    @staticmethod
    def validate_path(path: str, path_type: str = "file") -> str:
        """Validate path"""
        if not os.path.exists(path):
            raise typer.BadParameter(f"{path_type} not found: {path}")
        return path

    @staticmethod
    def handle_export_dir(export_dir: str, auto_cleanup: bool = False) -> str:
        """Handle export directory"""
        if os.path.exists(export_dir):
            if auto_cleanup:
                typer.echo(f"Auto-cleaning existing export directory: {export_dir}")
                import shutil

                shutil.rmtree(export_dir)
                os.makedirs(export_dir, exist_ok=True)
            else:
                typer.echo(f"Export directory '{export_dir}' already exists.")
                if typer.confirm("Do you want to clean it and continue?"):
                    import shutil

                    shutil.rmtree(export_dir)
                    os.makedirs(export_dir, exist_ok=True)
                    typer.echo(f"Cleaned export directory: {export_dir}")
                else:
                    typer.echo("Operation cancelled.")
                    raise typer.Exit(0)
        else:
            os.makedirs(export_dir, exist_ok=True)
        return export_dir


class ImageHandler(InputHandler):
    """Single image handler"""

    @staticmethod
    def process(image_path: str) -> List[str]:
        """Process single image"""
        InputHandler.validate_path(image_path, "Image file")
        return [image_path]


class ImagesHandler(InputHandler):
    """Image directory handler"""

    @staticmethod
    def process(images_dir: str, image_extensions: str = "png,jpg,jpeg") -> List[str]:
        """Process image directory"""
        InputHandler.validate_path(images_dir, "Images directory")

        # Parse extensions
        extensions = [ext.strip().lower() for ext in image_extensions.split(",")]
        extensions = [ext if ext.startswith(".") else f".{ext}" for ext in extensions]

        # Find image files
        image_files = []
        for ext in extensions:
            pattern = f"*{ext}"
            image_files.extend(glob.glob(os.path.join(images_dir, pattern)))
            image_files.extend(glob.glob(os.path.join(images_dir, pattern.upper())))

        image_files = sorted(list(set(image_files)))  # Remove duplicates and sort

        if not image_files:
            raise typer.BadParameter(
                f"No image files found in {images_dir} with extensions: {extensions}"
            )

        typer.echo(f"Found {len(image_files)} images to process")
        return image_files


class ColmapHandler(InputHandler):
    """COLMAP data handler"""

    @staticmethod
    def process(
        colmap_dir: str, sparse_subdir: str = ""
    ) -> Tuple[List[str], np.ndarray, np.ndarray]:
        """Process COLMAP data"""
        InputHandler.validate_path(colmap_dir, "COLMAP directory")

        # Build paths
        images_dir = os.path.join(colmap_dir, "images")
        if sparse_subdir:
            sparse_dir = os.path.join(colmap_dir, "sparse", sparse_subdir)
        else:
            sparse_dir = os.path.join(colmap_dir, "sparse")

        InputHandler.validate_path(images_dir, "Images directory")
        InputHandler.validate_path(sparse_dir, "Sparse reconstruction directory")

        # Load COLMAP data
        typer.echo("Loading COLMAP reconstruction data...")
        try:
            cameras, images, points3D = read_model(sparse_dir)

            typer.echo(
                f"Loaded COLMAP data: {len(cameras)} cameras, {len(images)} images, "
                f"{len(points3D)} 3D points."
            )

            # Get image files and pose data
            image_files = []
            extrinsics = []
            intrinsics = []

            for image_id, image_data in images.items():
                image_name = image_data.name
                image_path = os.path.join(images_dir, image_name)

                if os.path.exists(image_path):
                    image_files.append(image_path)

                    # Get camera parameters
                    camera = cameras[image_data.camera_id]

                    # Convert quaternion to rotation matrix
                    R = image_data.qvec2rotmat()
                    t = image_data.tvec

                    # Create extrinsic matrix (world to camera)
                    extrinsic = np.eye(4)
                    extrinsic[:3, :3] = R
                    extrinsic[:3, 3] = t
                    extrinsics.append(extrinsic)

                    # Create intrinsic matrix
                    if camera.model == "PINHOLE":
                        fx, fy, cx, cy = camera.params
                    elif camera.model == "SIMPLE_PINHOLE":
                        f, cx, cy = camera.params
                        fx = fy = f
                    else:
                        # For other models, use basic pinhole approximation
                        fx = fy = camera.params[0] if len(camera.params) > 0 else 1000
                        cx = camera.width / 2
                        cy = camera.height / 2

                    intrinsic = np.array([[fx, 0, cx], [0, fy, cy], [0, 0, 1]])
                    intrinsics.append(intrinsic)

            if not image_files:
                raise typer.BadParameter("No valid images found in COLMAP data")

            typer.echo(f"Found {len(image_files)} valid images with pose data")

            return image_files, np.array(extrinsics), np.array(intrinsics)

        except Exception as e:
            raise typer.BadParameter(f"Failed to load COLMAP data: {e}")


class VideoHandler(InputHandler):
    """Video handler"""

    @staticmethod
    def process(video_path: str, output_dir: str, fps: float = 1.0) -> List[str]:
        """Process video, extract frames"""
        InputHandler.validate_path(video_path, "Video file")

        cap = cv2.VideoCapture(video_path)
        if not cap.isOpened():
            raise typer.BadParameter(f"Cannot open video: {video_path}")

        # Get video properties
        video_fps = cap.get(cv2.CAP_PROP_FPS)
        total_frames = int(cap.get(cv2.CAP_PROP_FRAME_COUNT))
        duration = total_frames / video_fps

        # Calculate frame interval (ensure at least 1)
        frame_interval = max(1, int(video_fps / fps))
        actual_fps = video_fps / frame_interval

        typer.echo(f"Video FPS: {video_fps:.2f}, Duration: {duration:.2f}s")

        # Warn if requested FPS is higher than video FPS
        if fps > video_fps:
            typer.echo(
                f"⚠️  Warning: Requested sampling FPS ({fps:.2f}) exceeds video FPS ({video_fps:.2f})",  # noqa: E501
                err=True,
            )
            typer.echo(
                f"⚠️  Using maximum available FPS: {actual_fps:.2f} (extracting every frame)",
                err=True,
            )

        typer.echo(f"Extracting frames at {actual_fps:.2f} FPS (every {frame_interval} frame(s))")

        # Create output directory
        frames_dir = os.path.join(output_dir, "input_images")
        os.makedirs(frames_dir, exist_ok=True)

        frame_count = 0
        saved_count = 0

        while True:
            ret, frame = cap.read()
            if not ret:
                break

            if frame_count % frame_interval == 0:
                frame_path = os.path.join(frames_dir, f"{saved_count:06d}.png")
                cv2.imwrite(frame_path, frame)
                saved_count += 1

            frame_count += 1

        cap.release()
        typer.echo(f"Extracted {saved_count} frames to {frames_dir}")

        # Get frame file list
        frame_files = sorted(
            [f for f in os.listdir(frames_dir) if f.endswith((".png", ".jpg", ".jpeg"))]
        )
        if not frame_files:
            raise typer.BadParameter("No frames extracted from video")

        return [os.path.join(frames_dir, f) for f in frame_files]


def parse_export_feat(export_feat_str: str) -> List[int]:
    """Parse export_feat parameter"""
    if not export_feat_str:
        return []

    try:
        return [int(x.strip()) for x in export_feat_str.split(",") if x.strip()]
    except ValueError:
        raise typer.BadParameter(
            f"Invalid export_feat format: {export_feat_str}. "
            "Use comma-separated integers like '0,1,2'"
        )



================================================
FILE: src/depth_anything_3/utils/alignment.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

"""
Alignment utilities for depth estimation and metric scaling.
"""

from typing import Tuple
import torch


def least_squares_scale_scalar(
    a: torch.Tensor, b: torch.Tensor, eps: float = 1e-12
) -> torch.Tensor:
    """
    Compute least squares scale factor s such that a ≈ s * b.

    Args:
        a: First tensor
        b: Second tensor
        eps: Small epsilon for numerical stability

    Returns:
        Scalar tensor containing the scale factor

    Raises:
        ValueError: If tensors have mismatched shapes or devices
        TypeError: If tensors are not floating point
    """
    if a.shape != b.shape:
        raise ValueError(f"Shape mismatch: {a.shape} vs {b.shape}")
    if a.device != b.device:
        raise ValueError(f"Device mismatch: {a.device} vs {b.device}")
    if not a.is_floating_point() or not b.is_floating_point():
        raise TypeError("Tensors must be floating point type")

    # Compute dot products for least squares solution
    num = torch.dot(a.reshape(-1), b.reshape(-1))
    den = torch.dot(b.reshape(-1), b.reshape(-1)).clamp_min(eps)
    return num / den


def compute_sky_mask(sky_prediction: torch.Tensor, threshold: float = 0.3) -> torch.Tensor:
    """
    Compute non-sky mask from sky prediction.

    Args:
        sky_prediction: Sky prediction tensor
        threshold: Threshold for sky classification

    Returns:
        Boolean mask where True indicates non-sky regions
    """
    return sky_prediction < threshold


def compute_alignment_mask(
    depth_conf: torch.Tensor,
    non_sky_mask: torch.Tensor,
    depth: torch.Tensor,
    metric_depth: torch.Tensor,
    median_conf: torch.Tensor,
    min_depth_threshold: float = 1e-3,
    min_metric_depth_threshold: float = 1e-2,
) -> torch.Tensor:
    """
    Compute mask for depth alignment based on confidence and depth thresholds.

    Args:
        depth_conf: Depth confidence tensor
        non_sky_mask: Non-sky region mask
        depth: Predicted depth tensor
        metric_depth: Metric depth tensor
        median_conf: Median confidence threshold
        min_depth_threshold: Minimum depth threshold
        min_metric_depth_threshold: Minimum metric depth threshold

    Returns:
        Boolean mask for valid alignment regions
    """
    return (
        (depth_conf >= median_conf)
        & non_sky_mask
        & (metric_depth > min_metric_depth_threshold)
        & (depth > min_depth_threshold)
    )


def sample_tensor_for_quantile(tensor: torch.Tensor, max_samples: int = 100000) -> torch.Tensor:
    """
    Sample tensor elements for quantile computation to reduce memory usage.

    Args:
        tensor: Input tensor to sample
        max_samples: Maximum number of samples to take

    Returns:
        Sampled tensor
    """
    if tensor.numel() <= max_samples:
        return tensor

    idx = torch.randperm(tensor.numel(), device=tensor.device)[:max_samples]
    return tensor.flatten()[idx]


def apply_metric_scaling(
    depth: torch.Tensor, intrinsics: torch.Tensor, scale_factor: float = 300.0
) -> torch.Tensor:
    """
    Apply metric scaling to depth based on camera intrinsics.

    Args:
        depth: Input depth tensor
        intrinsics: Camera intrinsics tensor
        scale_factor: Scaling factor for metric conversion

    Returns:
        Scaled depth tensor
    """
    focal_length = (intrinsics[:, :, 0, 0] + intrinsics[:, :, 1, 1]) / 2
    return depth * (focal_length[:, :, None, None] / scale_factor)


def set_sky_regions_to_max_depth(
    depth: torch.Tensor,
    depth_conf: torch.Tensor,
    non_sky_mask: torch.Tensor,
    max_depth: float = 200.0,
) -> Tuple[torch.Tensor, torch.Tensor]:
    """
    Set sky regions to maximum depth and high confidence.

    Args:
        depth: Depth tensor
        depth_conf: Depth confidence tensor
        non_sky_mask: Non-sky region mask
        max_depth: Maximum depth value for sky regions

    Returns:
        Tuple of (updated_depth, updated_depth_conf)
    """
    depth = depth.clone()

    # Set sky regions to max depth and high confidence
    depth[~non_sky_mask] = max_depth
    if depth_conf is not None:
        depth_conf = depth_conf.clone()
        depth_conf[~non_sky_mask] = 1.0
        return depth, depth_conf
    else:
        return depth, None



================================================
FILE: src/depth_anything_3/utils/api_helpers.py
================================================
import argparse


def parse_scalar(s):
    if not isinstance(s, str):
        return s
    t = s.strip()
    l = t.lower()
    if l == "true":
        return True
    if l == "false":
        return False
    if l in ("none", "null"):
        return None
    try:
        return int(t, 10)
    except Exception:
        pass
    try:
        return float(t)
    except Exception:
        return s


def fn_kv_csv(s: str) -> dict[str, dict[str, object]]:
    """
    Parse a string of comma-separated triplets: fn:key:value

    Returns:
        dict[fn_name] -> dict[key] = parsed_value

    Example:
        "fn1:width:1920,fn1:height:1080,fn2:quality:0.8"
        -> {"fn1": {"width": 1920, "height": 1080}, "fn2": {"quality": 0.8}}
    """
    result: dict[str, dict[str, object]] = {}
    if not s:
        return result

    for item in s.split(","):
        if not item:
            continue
        parts = item.split(":", 2)  # allow value to contain ":" beyond first two separators
        if len(parts) < 3:
            raise argparse.ArgumentTypeError(f"Bad item '{item}', expected FN:KEY:VALUE")
        fn, key, raw_val = parts[0], parts[1], parts[2]
        # If you need to allow colons in values, join leftover parts:
        # fn, key, raw_val = parts[0], parts[1], ":".join(parts[2:])

        if not fn:
            raise argparse.ArgumentTypeError(f"Bad item '{item}': empty function name")
        if not key:
            raise argparse.ArgumentTypeError(f"Bad item '{item}': empty key")

        val = parse_scalar(raw_val)
        bucket = result.setdefault(fn, {})
        bucket[key] = val
    return result



================================================
FILE: src/depth_anything_3/utils/camera_trj_helpers.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

import cv2
import numpy as np
import torch
import torch.nn.functional as F
from einops import einsum, rearrange, reduce

try:
    from scipy.spatial.transform import Rotation as R
except ImportError:
    from depth_anything_3.utils.logger import logger

    logger.warn("Dependency 'scipy' not found. Required for interpolating camera trajectory.")

from depth_anything_3.utils.geometry import as_homogeneous


@torch.no_grad()
def render_stabilization_path(poses, k_size=45):
    """Rendering stabilized camera path.
    poses: [batch, 4, 4] or [batch, 3, 4],
    return:
        smooth path: [batch 4 4]"""
    num_frames = poses.shape[0]
    device = poses.device
    dtype = poses.dtype

    # Early exit for trivial cases
    if num_frames <= 1:
        return as_homogeneous(poses)

    # Make k_size safe: positive odd and not larger than num_frames
    # 1) Ensure odd
    if k_size < 1:
        k_size = 1
    if k_size % 2 == 0:
        k_size += 1
    # 2) Cap to num_frames (keep odd)
    max_odd = num_frames if (num_frames % 2 == 1) else (num_frames - 1)
    if max_odd < 1:
        max_odd = 1  # covers num_frames == 0 theoretically
    k_size = min(k_size, max_odd)
    # 3) enforce a minimum of 3 when possible (for better smoothing)
    if num_frames >= 3 and k_size < 3:
        k_size = 3

    input_poses = []
    for i in range(num_frames):
        input_poses.append(
            torch.cat([poses[i, :3, 0:1], poses[i, :3, 1:2], poses[i, :3, 3:4]], dim=-1)
        )
    input_poses = torch.stack(input_poses)  # (num_frames, 3, 3)

    # Prepare Gaussian kernel
    gaussian_kernel = cv2.getGaussianKernel(ksize=k_size, sigma=-1).astype(np.float32).squeeze()
    gaussian_kernel = torch.tensor(gaussian_kernel, dtype=dtype, device=device).view(1, 1, -1)
    pad = k_size // 2

    output_vectors = []
    for idx in range(3):  # For r1, r2, t
        vec = (
            input_poses[:, :, idx].T.unsqueeze(0).unsqueeze(0)
        )  # (1, 1, 3, num_frames) -> (1, 1, 3, num_frames)
        # But actually, we want (batch=3, channel=1, width=num_frames)
        # So:
        vec = input_poses[:, :, idx].T.unsqueeze(1)  # (3, 1, num_frames)
        vec_padded = F.pad(vec, (pad, pad), mode="reflect")
        filtered = F.conv1d(vec_padded, gaussian_kernel)
        output_vectors.append(filtered.squeeze(1).T)  # (num_frames, 3)

    output_r1, output_r2, output_t = output_vectors  # Each is (num_frames, 3)

    # Normalize r1 and r2
    output_r1 = output_r1 / output_r1.norm(dim=-1, keepdim=True)
    output_r2 = output_r2 / output_r2.norm(dim=-1, keepdim=True)

    output_poses = []
    for i in range(num_frames):
        output_r3 = torch.linalg.cross(output_r1[i], output_r2[i])
        render_pose = torch.cat(
            [
                output_r1[i].unsqueeze(-1),
                output_r2[i].unsqueeze(-1),
                output_r3.unsqueeze(-1),
                output_t[i].unsqueeze(-1),
            ],
            dim=-1,
        )
        output_poses.append(render_pose[:3, :])
    output_poses = as_homogeneous(torch.stack(output_poses, dim=0))

    return output_poses


@torch.no_grad()
def render_wander_path(
    cam2world: torch.Tensor,
    intrinsic: torch.Tensor,
    h: int,
    w: int,
    num_frames: int = 120,
    max_disp: float = 48.0,
):
    device, dtype = cam2world.device, cam2world.dtype
    fx = intrinsic[0, 0] * w
    r = max_disp / fx
    th = torch.linspace(0, 2.0 * torch.pi, steps=num_frames, device=device, dtype=dtype)
    x = r * torch.sin(th)
    yz = r * torch.cos(th) / 3.0
    T = torch.eye(4, device=device, dtype=dtype).unsqueeze(0).repeat(num_frames, 1, 1)
    T[:, :3, 3] = torch.stack([x, yz, yz], dim=-1) * -1.0
    c2ws = cam2world.unsqueeze(0) @ T
    # Start at reference pose and end back at reference pose
    c2ws = torch.cat([cam2world.unsqueeze(0), c2ws, cam2world.unsqueeze(0)], dim=0)
    Ks = intrinsic.unsqueeze(0).repeat(c2ws.shape[0], 1, 1)
    return c2ws, Ks


@torch.no_grad()
def render_dolly_zoom_path(
    cam2world: torch.Tensor,
    intrinsic: torch.Tensor,
    h: int,
    w: int,
    num_frames: int = 120,
    max_disp: float = 0.1,
    D_focus: float = 10.0,
):
    device, dtype = cam2world.device, cam2world.dtype
    fx0, fy0 = intrinsic[0, 0] * w, intrinsic[1, 1] * h
    t = torch.linspace(0.0, 2.0, steps=num_frames, device=device, dtype=dtype)
    z = 0.5 * (1.0 - torch.cos(torch.pi * t)) * max_disp
    T = torch.eye(4, device=device, dtype=dtype).unsqueeze(0).repeat(num_frames, 1, 1)
    T[:, 2, 3] = -z
    c2ws = cam2world.unsqueeze(0) @ T
    Df = torch.as_tensor(D_focus, device=device, dtype=dtype)
    scale = (Df / (Df + z)).clamp(min=1e-6)
    Ks = intrinsic.unsqueeze(0).repeat(num_frames, 1, 1)
    Ks[:, 0, 0] = (fx0 * scale) / w
    Ks[:, 1, 1] = (fy0 * scale) / h
    return c2ws, Ks


@torch.no_grad()
def interpolate_intrinsics(
    initial: torch.Tensor,  # "*#batch 3 3"
    final: torch.Tensor,  # "*#batch 3 3"
    t: torch.Tensor,  # " time_step"
) -> torch.Tensor:  # "*batch time_step 3 3"
    initial = rearrange(initial, "... i j -> ... () i j")
    final = rearrange(final, "... i j -> ... () i j")
    t = rearrange(t, "t -> t () ()")
    return initial + (final - initial) * t


def intersect_rays(
    a_origins: torch.Tensor,  # "*#batch dim"
    a_directions: torch.Tensor,  # "*#batch dim"
    b_origins: torch.Tensor,  # "*#batch dim"
    b_directions: torch.Tensor,  # "*#batch dim"
) -> torch.Tensor:  # "*batch dim"
    """Compute the least-squares intersection of rays. Uses the math from here:
    https://math.stackexchange.com/a/1762491/286022
    """

    # Broadcast and stack the tensors.
    a_origins, a_directions, b_origins, b_directions = torch.broadcast_tensors(
        a_origins, a_directions, b_origins, b_directions
    )
    origins = torch.stack((a_origins, b_origins), dim=-2)
    directions = torch.stack((a_directions, b_directions), dim=-2)

    # Compute n_i * n_i^T - eye(3) from the equation.
    n = einsum(directions, directions, "... n i, ... n j -> ... n i j")
    n = n - torch.eye(3, dtype=origins.dtype, device=origins.device)

    # Compute the left-hand side of the equation.
    lhs = reduce(n, "... n i j -> ... i j", "sum")

    # Compute the right-hand side of the equation.
    rhs = einsum(n, origins, "... n i j, ... n j -> ... n i")
    rhs = reduce(rhs, "... n i -> ... i", "sum")

    # Left-matrix-multiply both sides by the inverse of lhs to find p.
    return torch.linalg.lstsq(lhs, rhs).solution


def normalize(a: torch.Tensor) -> torch.Tensor:  # "*#batch dim" -> "*#batch dim"
    return a / a.norm(dim=-1, keepdim=True)


def generate_coordinate_frame(
    y: torch.Tensor,  # "*#batch 3"
    z: torch.Tensor,  # "*#batch 3"
) -> torch.Tensor:  # "*batch 3 3"
    """Generate a coordinate frame given perpendicular, unit-length Y and Z vectors."""
    y, z = torch.broadcast_tensors(y, z)
    return torch.stack([y.cross(z, dim=-1), y, z], dim=-1)


def generate_rotation_coordinate_frame(
    a: torch.Tensor,  # "*#batch 3"
    b: torch.Tensor,  # "*#batch 3"
    eps: float = 1e-4,
) -> torch.Tensor:  # "*batch 3 3"
    """Generate a coordinate frame where the Y direction is normal to the plane defined
    by unit vectors a and b. The other axes are arbitrary."""
    device = a.device

    # Replace every entry in b that's parallel to the corresponding entry in a with an
    # arbitrary vector.
    b = b.detach().clone()
    parallel = (einsum(a, b, "... i, ... i -> ...").abs() - 1).abs() < eps
    b[parallel] = torch.tensor([0, 0, 1], dtype=b.dtype, device=device)
    parallel = (einsum(a, b, "... i, ... i -> ...").abs() - 1).abs() < eps
    b[parallel] = torch.tensor([0, 1, 0], dtype=b.dtype, device=device)

    # Generate the coordinate frame. The initial cross product defines the plane.
    return generate_coordinate_frame(normalize(torch.linalg.cross(a, b)), a)


def matrix_to_euler(
    rotations: torch.Tensor,  # "*batch 3 3"
    pattern: str,
) -> torch.Tensor:  # "*batch 3"
    *batch, _, _ = rotations.shape
    rotations = rotations.reshape(-1, 3, 3)
    angles_np = R.from_matrix(rotations.detach().cpu().numpy()).as_euler(pattern)
    rotations = torch.tensor(angles_np, dtype=rotations.dtype, device=rotations.device)
    return rotations.reshape(*batch, 3)


def euler_to_matrix(
    rotations: torch.Tensor,  # "*batch 3"
    pattern: str,
) -> torch.Tensor:  # "*batch 3 3"
    *batch, _ = rotations.shape
    rotations = rotations.reshape(-1, 3)
    matrix_np = R.from_euler(pattern, rotations.detach().cpu().numpy()).as_matrix()
    rotations = torch.tensor(matrix_np, dtype=rotations.dtype, device=rotations.device)
    return rotations.reshape(*batch, 3, 3)


def extrinsics_to_pivot_parameters(
    extrinsics: torch.Tensor,  # "*#batch 4 4"
    pivot_coordinate_frame: torch.Tensor,  # "*#batch 3 3"
    pivot_point: torch.Tensor,  # "*#batch 3"
) -> torch.Tensor:  # "*batch 5"
    """Convert the extrinsics to a representation with 5 degrees of freedom:
    1. Distance from pivot point in the "X" (look cross pivot axis) direction.
    2. Distance from pivot point in the "Y" (pivot axis) direction.
    3. Distance from pivot point in the Z (look) direction
    4. Angle in plane
    5. Twist (rotation not in plane)
    """

    # The pivot coordinate frame's Z axis is normal to the plane.
    pivot_axis = pivot_coordinate_frame[..., :, 1]

    # Compute the translation elements of the pivot parametrization.
    translation_frame = generate_coordinate_frame(pivot_axis, extrinsics[..., :3, 2])
    origin = extrinsics[..., :3, 3]
    delta = pivot_point - origin
    translation = einsum(translation_frame, delta, "... i j, ... i -> ... j")

    # Add the rotation elements of the pivot parametrization.
    inverted = pivot_coordinate_frame.inverse() @ extrinsics[..., :3, :3]
    y, _, z = matrix_to_euler(inverted, "YXZ").unbind(dim=-1)

    return torch.cat([translation, y[..., None], z[..., None]], dim=-1)


def pivot_parameters_to_extrinsics(
    parameters: torch.Tensor,  # "*#batch 5"
    pivot_coordinate_frame: torch.Tensor,  # "*#batch 3 3"
    pivot_point: torch.Tensor,  # "*#batch 3"
) -> torch.Tensor:  # "*batch 4 4"
    translation, y, z = parameters.split((3, 1, 1), dim=-1)

    euler = torch.cat((y, torch.zeros_like(y), z), dim=-1)
    rotation = pivot_coordinate_frame @ euler_to_matrix(euler, "YXZ")

    # The pivot coordinate frame's Z axis is normal to the plane.
    pivot_axis = pivot_coordinate_frame[..., :, 1]

    translation_frame = generate_coordinate_frame(pivot_axis, rotation[..., :3, 2])
    delta = einsum(translation_frame, translation, "... i j, ... j -> ... i")
    origin = pivot_point - delta

    *batch, _ = origin.shape
    extrinsics = torch.eye(4, dtype=parameters.dtype, device=parameters.device)
    extrinsics = extrinsics.broadcast_to((*batch, 4, 4)).clone()
    extrinsics[..., 3, 3] = 1
    extrinsics[..., :3, :3] = rotation
    extrinsics[..., :3, 3] = origin
    return extrinsics


def interpolate_circular(
    a: torch.Tensor,  # "*#batch"
    b: torch.Tensor,  # "*#batch"
    t: torch.Tensor,  # "*#batch"
) -> torch.Tensor:  # " *batch"
    a, b, t = torch.broadcast_tensors(a, b, t)

    tau = 2 * torch.pi
    a = a % tau
    b = b % tau

    # Consider piecewise edge cases.
    d = (b - a).abs()
    a_left = a - tau
    d_left = (b - a_left).abs()
    a_right = a + tau
    d_right = (b - a_right).abs()
    use_d = (d < d_left) & (d < d_right)
    use_d_left = (d_left < d_right) & (~use_d)
    use_d_right = (~use_d) & (~use_d_left)

    result = a + (b - a) * t
    result[use_d_left] = (a_left + (b - a_left) * t)[use_d_left]
    result[use_d_right] = (a_right + (b - a_right) * t)[use_d_right]

    return result


def interpolate_pivot_parameters(
    initial: torch.Tensor,  # "*#batch 5"
    final: torch.Tensor,  # "*#batch 5"
    t: torch.Tensor,  # " time_step"
) -> torch.Tensor:  # "*batch time_step 5"
    initial = rearrange(initial, "... d -> ... () d")
    final = rearrange(final, "... d -> ... () d")
    t = rearrange(t, "t -> t ()")
    ti, ri = initial.split((3, 2), dim=-1)
    tf, rf = final.split((3, 2), dim=-1)

    t_lerp = ti + (tf - ti) * t
    r_lerp = interpolate_circular(ri, rf, t)

    return torch.cat((t_lerp, r_lerp), dim=-1)


@torch.no_grad()
def interpolate_extrinsics(
    initial: torch.Tensor,  # "*#batch 4 4"
    final: torch.Tensor,  # "*#batch 4 4"
    t: torch.Tensor,  # " time_step"
    eps: float = 1e-4,
) -> torch.Tensor:  # "*batch time_step 4 4"
    """Interpolate extrinsics by rotating around their "focus point," which is the
    least-squares intersection between the look vectors of the initial and final
    extrinsics.
    """

    initial = initial.type(torch.float64)
    final = final.type(torch.float64)
    t = t.type(torch.float64)

    # Based on the dot product between the look vectors, pick from one of two cases:
    # 1. Look vectors are parallel: interpolate about their origins' midpoint.
    # 3. Look vectors aren't parallel: interpolate about their focus point.
    initial_look = initial[..., :3, 2]
    final_look = final[..., :3, 2]
    dot_products = einsum(initial_look, final_look, "... i, ... i -> ...")
    parallel_mask = (dot_products.abs() - 1).abs() < eps

    # Pick focus points.
    initial_origin = initial[..., :3, 3]
    final_origin = final[..., :3, 3]
    pivot_point = 0.5 * (initial_origin + final_origin)
    pivot_point[~parallel_mask] = intersect_rays(
        initial_origin[~parallel_mask],
        initial_look[~parallel_mask],
        final_origin[~parallel_mask],
        final_look[~parallel_mask],
    )

    # Convert to pivot parameters.
    pivot_frame = generate_rotation_coordinate_frame(initial_look, final_look, eps=eps)
    initial_params = extrinsics_to_pivot_parameters(initial, pivot_frame, pivot_point)
    final_params = extrinsics_to_pivot_parameters(final, pivot_frame, pivot_point)

    # Interpolate the pivot parameters.
    interpolated_params = interpolate_pivot_parameters(initial_params, final_params, t)

    # Convert back.
    return pivot_parameters_to_extrinsics(
        interpolated_params.type(torch.float32),
        rearrange(pivot_frame, "... i j -> ... () i j").type(torch.float32),
        rearrange(pivot_point, "... xyz -> ... () xyz").type(torch.float32),
    )


@torch.no_grad()
def generate_wobble_transformation(
    radius: torch.Tensor,  # "*#batch"
    t: torch.Tensor,  # " time_step"
    num_rotations: int = 1,
    scale_radius_with_t: bool = True,
) -> torch.Tensor:  # "*batch time_step 4 4"]:
    # Generate a translation in the image plane.
    tf = torch.eye(4, dtype=torch.float32, device=t.device)
    tf = tf.broadcast_to((*radius.shape, t.shape[0], 4, 4)).clone()
    radius = radius[..., None]
    if scale_radius_with_t:
        radius = radius * t
    tf[..., 0, 3] = torch.sin(2 * torch.pi * num_rotations * t) * radius
    tf[..., 1, 3] = -torch.cos(2 * torch.pi * num_rotations * t) * radius
    return tf


@torch.no_grad()
def render_wobble_inter_path(
    cam2world: torch.Tensor, intr_normed: torch.Tensor, inter_len: int, n_skip: int = 3
):
    """
    cam2world: [batch, 4, 4],
    intr_normed: [batch, 3, 3]
    """
    frame_per_round = n_skip * inter_len
    num_rotations = 1

    t = torch.linspace(0, 1, frame_per_round, dtype=torch.float32, device=cam2world.device)
    # t = (torch.cos(torch.pi * (t + 1)) + 1) / 2
    tgt_c2w_b = []
    tgt_intr_b = []
    for b_idx in range(cam2world.shape[0]):
        tgt_c2w = []
        tgt_intr = []
        for cur_idx in range(0, cam2world.shape[1] - n_skip, n_skip):
            origin_a = cam2world[b_idx, cur_idx, :3, 3]
            origin_b = cam2world[b_idx, cur_idx + n_skip, :3, 3]
            delta = (origin_a - origin_b).norm(dim=-1)
            if cur_idx == 0:
                delta_prev = delta
            else:
                delta = (delta_prev + delta) / 2
                delta_prev = delta
            tf = generate_wobble_transformation(
                radius=delta * 0.5,
                t=t,
                num_rotations=num_rotations,
                scale_radius_with_t=False,
            )
            cur_extrs = (
                interpolate_extrinsics(
                    cam2world[b_idx, cur_idx],
                    cam2world[b_idx, cur_idx + n_skip],
                    t,
                )
                @ tf
            )
            tgt_c2w.append(cur_extrs[(0 if cur_idx == 0 else 1) :])
            tgt_intr.append(
                interpolate_intrinsics(
                    intr_normed[b_idx, cur_idx],
                    intr_normed[b_idx, cur_idx + n_skip],
                    t,
                )[(0 if cur_idx == 0 else 1) :]
            )
        tgt_c2w_b.append(torch.cat(tgt_c2w))
        tgt_intr_b.append(torch.cat(tgt_intr))
    tgt_c2w = torch.stack(tgt_c2w_b)  # b v 4 4
    tgt_intr = torch.stack(tgt_intr_b)  # b v 3 3
    return tgt_c2w, tgt_intr



================================================
FILE: src/depth_anything_3/utils/constants.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

DEFAULT_MODEL = "depth-anything/DA3NESTED-GIANT-LARGE-1.1"
DEFAULT_EXPORT_DIR = "workspace/gallery/scene"
DEFAULT_GALLERY_DIR = "workspace/gallery"
DEFAULT_GRADIO_DIR = "workspace/gradio"
THRESH_FOR_REF_SELECTION = 3

# =============================================================================
# Benchmark Evaluation Constants
# =============================================================================

# Default evaluation workspace directory
DEFAULT_EVAL_WORKSPACE = "workspace/evaluation"

# Default reference view selection strategy for evaluation
# Use "first" for consistent and reproducible evaluation results
# Other options: "saddle_balanced", "auto", "mid"
EVAL_REF_VIEW_STRATEGY = "first"

# -----------------------------------------------------------------------------
# DTU Dataset Configuration
# Reference: https://roboimagedata.compute.dtu.dk/
# Note: DepthAnything3 was never trained on any images from DTU.
# -----------------------------------------------------------------------------

# Root directory for DTU evaluation data (MVSNet format)
# Download from: https://drive.google.com/file/d/1rX0EXlUL4prRxrRu2DgLJv2j7-tpUD4D/view
DTU_EVAL_DATA_ROOT = "workspace/benchmark_dataset/dtu"

# List of DTU evaluation scenes
DTU_SCENES = [
    "scan1",
    "scan4",
    "scan9",
    "scan10",
    "scan11",
    "scan12",
    "scan13",
    "scan15",
    "scan23",
    "scan24",
    "scan29",
    "scan32",
    "scan33",
    "scan34",
    "scan48",
    "scan49",
    "scan62",
    "scan75",
    "scan77",
    "scan110",
    "scan114",
    "scan118",
]

# Point cloud fusion hyperparameters
DTU_DIST_THRESH = 0.2  # Distance threshold for geometric consistency (mm)
DTU_NUM_CONSIST = 4  # Minimum number of consistent views for a point
DTU_MAX_POINTS = 4_000_000  # Maximum points in fused point cloud

# 3D reconstruction evaluation hyperparameters
DTU_DOWN_DENSE = 0.2  # Downsample density for evaluation (mm)
DTU_PATCH_SIZE = 60  # Patch size for boundary handling
DTU_MAX_DIST = 20  # Outlier threshold for accuracy/completeness (mm)

# -----------------------------------------------------------------------------
# DTU-64 Dataset Configuration (Pose Evaluation Only)
# This is a subset of DTU with 64 images per scene for pose evaluation.
# Note: This dataset is ONLY for pose evaluation, not 3D reconstruction.
# -----------------------------------------------------------------------------

# Root directory for DTU-64 evaluation data
DTU64_EVAL_DATA_ROOT = "workspace/benchmark_dataset/dtu64"
DTU64_CAMERA_ROOT = "workspace/benchmark_dataset/dtu64/Cameras"

# List of DTU-64 evaluation scenes (13 scenes)
DTU64_SCENES = [
    "scan105",
    "scan114",
    "scan118",
    "scan122",
    "scan24",
    "scan37",
    "scan40",
    "scan55",
    "scan63",
    "scan65",
    "scan69",
    "scan83",
    "scan97",
]

# -----------------------------------------------------------------------------
# ETH3D Dataset Configuration
# Reference: https://www.eth3d.net/
# High-resolution multi-view stereo benchmark with laser-scanned ground truth.
# Note: DepthAnything3 was never trained on any images from ETH3D.
# -----------------------------------------------------------------------------

# Root directory for ETH3D evaluation data
ETH3D_EVAL_DATA_ROOT = "workspace/benchmark_dataset/eth3d"

# List of ETH3D evaluation scenes (indoor and outdoor)
ETH3D_SCENES = [
    "courtyard",
    "electro",
    "kicker",
    "pipes",
    "relief",
    # "terrace",  # Excluded: known issues
    "delivery_area",
    "facade",
    # "meadow",   # Excluded: known issues
    "office",
    "playground",
    "relief_2",
    "terrains",
]

# Images to filter out (known problematic views per scene)
ETH3D_FILTER_KEYS = {
    "delivery_area": ["711.JPG", "712.JPG", "713.JPG", "714.JPG"],
    "electro": ["9289.JPG", "9290.JPG", "9291.JPG", "9292.JPG", "9293.JPG", "9298.JPG"],
    "playground": ["587.JPG", "588.JPG", "589.JPG", "590.JPG", "591.JPG", "592.JPG"],
    "relief": [
        "427.JPG", "428.JPG", "429.JPG", "430.JPG", "431.JPG", "432.JPG",
        "433.JPG", "434.JPG", "435.JPG", "436.JPG", "437.JPG", "438.JPG",
    ],
    "relief_2": [
        "458.JPG", "459.JPG", "460.JPG", "461.JPG", "462.JPG", "463.JPG",
        "464.JPG", "465.JPG", "466.JPG", "467.JPG", "468.JPG",
    ],
}

# TSDF fusion hyperparameters (scaled for outdoor scenes)
ETH3D_VOXEL_LENGTH = 4.0 / 512.0 * 5  # Voxel size for TSDF (meters)
ETH3D_SDF_TRUNC = 0.04 * 5  # SDF truncation distance (meters)
ETH3D_MAX_DEPTH = 100000.0  # Maximum depth for integration (effectively no truncation)

# Point cloud sampling
ETH3D_SAMPLING_NUMBER = 1_000_000  # Number of points to sample from mesh

# 3D reconstruction evaluation hyperparameters
ETH3D_EVAL_THRESHOLD = 0.05 * 5  # Distance threshold for precision/recall (meters)
ETH3D_DOWN_SAMPLE = 4.0 / 512.0 * 5  # Voxel size for evaluation downsampling (meters)


# ==============================================================================
# 7Scenes Dataset Configuration
# ==============================================================================
# Reference: https://www.microsoft.com/en-us/research/project/rgb-d-dataset-7-scenes/
# Note: Indoor RGB-D dataset with ground truth poses and meshes.

# Root directory for 7Scenes evaluation data
SEVENSCENES_EVAL_DATA_ROOT = "workspace/benchmark_dataset/7scenes"

# List of 7Scenes evaluation scenes
SEVENSCENES_SCENES = [
    "chess",
    "fire",
    "heads",
    "office",
    "pumpkin",
    "redkitchen",
    "stairs",
]

# Fixed camera intrinsics for 7Scenes (all images share same intrinsics)
SEVENSCENES_FX = 585.0
SEVENSCENES_FY = 585.0
SEVENSCENES_CX = 320.0
SEVENSCENES_CY = 240.0

# TSDF fusion hyperparameters (indoor scenes, smaller voxels)
SEVENSCENES_VOXEL_LENGTH = 4.0 / 512.0  # Voxel size for TSDF (meters)
SEVENSCENES_SDF_TRUNC = 0.04  # SDF truncation distance (meters)
SEVENSCENES_MAX_DEPTH = 1000000.0  # Maximum depth for integration (no truncation)

# Point cloud sampling
SEVENSCENES_SAMPLING_NUMBER = 1_000_000  # Number of points to sample from mesh

# 3D reconstruction evaluation hyperparameters
SEVENSCENES_EVAL_THRESHOLD = 0.05  # Distance threshold for precision/recall (meters)
SEVENSCENES_DOWN_SAMPLE = 4.0 / 512.0  # Voxel size for evaluation downsampling (meters)


# ==============================================================================
# ScanNet++ Dataset Configuration
# ==============================================================================
# Reference: https://kaldir.vc.in.tum.de/scannetpp/
# Note: High-quality indoor RGB-D dataset with iPhone and DSLR images.

# Root directory for ScanNet++ evaluation data
SCANNETPP_EVAL_DATA_ROOT = "workspace/benchmark_dataset/scannetpp"

# List of ScanNet++ evaluation scenes
SCANNETPP_SCENES = [
    "09c1414f1b",
    "1ada7a0617",
    "40aec5fffa",
    "3e8bba0176",
    "acd95847c5",
    "578511c8a9",
    "5f99900f09",
    "c4c04e6d6c",
    "f3d64c30f8",
    "7bc286c1b6",
    "c5439f4607",
    "286b55a2bf",
    "fb5a96b1a2",
    "7831862f02",
    "38d58a7a31",
    "bde1e479ad",
    "9071e139d9",
    "21d970d8de",
    "bcd2436daf",
    "cc5237fd77",
]

# Input resolution for ScanNet++ (after undistortion and resize)
SCANNETPP_INPUT_H = 768
SCANNETPP_INPUT_W = 1024

# TSDF fusion hyperparameters (indoor scenes)
SCANNETPP_VOXEL_LENGTH = 0.02  # Voxel size for TSDF (meters)
SCANNETPP_SDF_TRUNC = 0.15  # SDF truncation distance (meters)
SCANNETPP_MAX_DEPTH = 5.0  # Maximum depth for integration (meters)

# Point cloud sampling
SCANNETPP_SAMPLING_NUMBER = 1_000_000  # Number of points to sample from mesh

# 3D reconstruction evaluation hyperparameters
SCANNETPP_EVAL_THRESHOLD = 0.05  # Distance threshold for precision/recall (meters)
SCANNETPP_DOWN_SAMPLE = 0.02  # Voxel size for evaluation downsampling (meters)


# ==============================================================================
# HiRoom Dataset Configuration
# ==============================================================================
# Note: Indoor RGB-D dataset.

# Root directory for HiRoom evaluation data
HIROOM_EVAL_DATA_ROOT = "workspace/benchmark_dataset/hiroom/data"
HIROOM_GT_ROOT_PATH = "workspace/benchmark_dataset/hiroom/fused_pcd"
HIROOM_SCENE_LIST_PATH = "workspace/benchmark_dataset/hiroom/selected_scene_list_val.txt"

# TSDF fusion hyperparameters (indoor scenes)
HIROOM_VOXEL_LENGTH = 4.0 / 512.0  # Voxel size for TSDF (meters)
HIROOM_SDF_TRUNC = 0.04  # SDF truncation distance (meters)
HIROOM_MAX_DEPTH = 10000.0  # Maximum depth for integration (no truncation)

# Point cloud sampling
HIROOM_SAMPLING_NUMBER = 1_000_000  # Number of points to sample from mesh

# 3D reconstruction evaluation hyperparameters
HIROOM_EVAL_THRESHOLD = 0.05  # Distance threshold for precision/recall (meters)
HIROOM_DOWN_SAMPLE = 4.0 / 512.0  # Voxel size for evaluation downsampling (meters)



================================================
FILE: src/depth_anything_3/utils/geometry.py
================================================
# flake8: noqa: F722
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
from types import SimpleNamespace
from typing import Optional
import numpy as np
import torch
import torch.nn.functional as F
from einops import einsum


def as_homogeneous(ext):
    """
    Accept (..., 3,4) or (..., 4,4) extrinsics, return (...,4,4) homogeneous matrix.
    Supports torch.Tensor or np.ndarray.
    """
    if isinstance(ext, torch.Tensor):
        # If already in homogeneous form
        if ext.shape[-2:] == (4, 4):
            return ext
        elif ext.shape[-2:] == (3, 4):
            # Create a new homogeneous matrix
            ones = torch.zeros_like(ext[..., :1, :4])
            ones[..., 0, 3] = 1.0
            return torch.cat([ext, ones], dim=-2)
        else:
            raise ValueError(f"Invalid shape for torch.Tensor: {ext.shape}")

    elif isinstance(ext, np.ndarray):
        if ext.shape[-2:] == (4, 4):
            return ext
        elif ext.shape[-2:] == (3, 4):
            ones = np.zeros_like(ext[..., :1, :4])
            ones[..., 0, 3] = 1.0
            return np.concatenate([ext, ones], axis=-2)
        else:
            raise ValueError(f"Invalid shape for np.ndarray: {ext.shape}")

    else:
        raise TypeError("Input must be a torch.Tensor or np.ndarray.")


@torch.jit.script
def affine_inverse(A: torch.Tensor):
    R = A[..., :3, :3]  # ..., 3, 3
    T = A[..., :3, 3:]  # ..., 3, 1
    P = A[..., 3:, :]  # ..., 1, 4
    return torch.cat([torch.cat([R.mT, -R.mT @ T], dim=-1), P], dim=-2)


def transpose_last_two_axes(arr):
    """
    for np < 2
    """
    if arr.ndim < 2:
        return arr
    axes = list(range(arr.ndim))
    # swap the last two
    axes[-2], axes[-1] = axes[-1], axes[-2]
    return arr.transpose(axes)


def affine_inverse_np(A: np.ndarray):
    R = A[..., :3, :3]
    T = A[..., :3, 3:]
    P = A[..., 3:, :]
    return np.concatenate(
        [
            np.concatenate([transpose_last_two_axes(R), -transpose_last_two_axes(R) @ T], axis=-1),
            P,
        ],
        axis=-2,
    )


def quat_to_mat(quaternions: torch.Tensor) -> torch.Tensor:
    """
    Quaternion Order: XYZW or say ijkr, scalar-last

    Convert rotations given as quaternions to rotation matrices.
    Args:
        quaternions: quaternions with real part last,
            as tensor of shape (..., 4).

    Returns:
        Rotation matrices as tensor of shape (..., 3, 3).
    """
    i, j, k, r = torch.unbind(quaternions, -1)
    # pyre-fixme[58]: `/` is not supported for operand types `float` and `Tensor`.
    two_s = 2.0 / (quaternions * quaternions).sum(-1)

    o = torch.stack(
        (
            1 - two_s * (j * j + k * k),
            two_s * (i * j - k * r),
            two_s * (i * k + j * r),
            two_s * (i * j + k * r),
            1 - two_s * (i * i + k * k),
            two_s * (j * k - i * r),
            two_s * (i * k - j * r),
            two_s * (j * k + i * r),
            1 - two_s * (i * i + j * j),
        ),
        -1,
    )
    return o.reshape(quaternions.shape[:-1] + (3, 3))


def mat_to_quat(matrix: torch.Tensor) -> torch.Tensor:
    """
    Convert rotations given as rotation matrices to quaternions.

    Args:
        matrix: Rotation matrices as tensor of shape (..., 3, 3).

    Returns:
        quaternions with real part last, as tensor of shape (..., 4).
        Quaternion Order: XYZW or say ijkr, scalar-last
    """
    if matrix.size(-1) != 3 or matrix.size(-2) != 3:
        raise ValueError(f"Invalid rotation matrix shape {matrix.shape}.")

    batch_dim = matrix.shape[:-2]
    m00, m01, m02, m10, m11, m12, m20, m21, m22 = torch.unbind(
        matrix.reshape(batch_dim + (9,)), dim=-1
    )

    q_abs = _sqrt_positive_part(
        torch.stack(
            [
                1.0 + m00 + m11 + m22,
                1.0 + m00 - m11 - m22,
                1.0 - m00 + m11 - m22,
                1.0 - m00 - m11 + m22,
            ],
            dim=-1,
        )
    )

    # we produce the desired quaternion multiplied by each of r, i, j, k
    quat_by_rijk = torch.stack(
        [
            # pyre-fixme[58]: `**` is not supported for operand types `Tensor` and
            #  `int`.
            torch.stack([q_abs[..., 0] ** 2, m21 - m12, m02 - m20, m10 - m01], dim=-1),
            # pyre-fixme[58]: `**` is not supported for operand types `Tensor` and
            #  `int`.
            torch.stack([m21 - m12, q_abs[..., 1] ** 2, m10 + m01, m02 + m20], dim=-1),
            # pyre-fixme[58]: `**` is not supported for operand types `Tensor` and
            #  `int`.
            torch.stack([m02 - m20, m10 + m01, q_abs[..., 2] ** 2, m12 + m21], dim=-1),
            # pyre-fixme[58]: `**` is not supported for operand types `Tensor` and
            #  `int`.
            torch.stack([m10 - m01, m20 + m02, m21 + m12, q_abs[..., 3] ** 2], dim=-1),
        ],
        dim=-2,
    )

    # We floor here at 0.1 but the exact level is not important; if q_abs is small,
    # the candidate won't be picked.
    flr = torch.tensor(0.1).to(dtype=q_abs.dtype, device=q_abs.device)
    quat_candidates = quat_by_rijk / (2.0 * q_abs[..., None].max(flr))

    # if not for numerical problems, quat_candidates[i] should be same (up to a sign),
    # forall i; we pick the best-conditioned one (with the largest denominator)
    out = quat_candidates[F.one_hot(q_abs.argmax(dim=-1), num_classes=4) > 0.5, :].reshape(
        batch_dim + (4,)
    )

    # Convert from rijk to ijkr
    out = out[..., [1, 2, 3, 0]]

    out = standardize_quaternion(out)

    return out


def _sqrt_positive_part(x: torch.Tensor) -> torch.Tensor:
    """
    Returns torch.sqrt(torch.max(0, x))
    but with a zero subgradient where x is 0.
    """
    ret = torch.zeros_like(x)
    positive_mask = x > 0
    if torch.is_grad_enabled():
        ret[positive_mask] = torch.sqrt(x[positive_mask])
    else:
        ret = torch.where(positive_mask, torch.sqrt(x), ret)
    return ret


def standardize_quaternion(quaternions: torch.Tensor) -> torch.Tensor:
    """
    Convert a unit quaternion to a standard form: one in which the real
    part is non negative.

    Args:
        quaternions: Quaternions with real part last,
            as tensor of shape (..., 4).

    Returns:
        Standardized quaternions as tensor of shape (..., 4).
    """
    return torch.where(quaternions[..., 3:4] < 0, -quaternions, quaternions)


def sample_image_grid(
    shape: tuple[int, ...],
    device: torch.device = torch.device("cpu"),
) -> tuple[
    torch.Tensor,  # float coordinates (xy indexing), "*shape dim"
    torch.Tensor,  # integer indices (ij indexing), "*shape dim"
]:
    """Get normalized (range 0 to 1) coordinates and integer indices for an image."""

    # Each entry is a pixel-wise integer coordinate. In the 2D case, each entry is a
    # (row, col) coordinate.
    indices = [torch.arange(length, device=device) for length in shape]
    stacked_indices = torch.stack(torch.meshgrid(*indices, indexing="ij"), dim=-1)

    # Each entry is a floating-point coordinate in the range (0, 1). In the 2D case,
    # each entry is an (x, y) coordinate.
    coordinates = [(idx + 0.5) / length for idx, length in zip(indices, shape)]
    coordinates = reversed(coordinates)
    coordinates = torch.stack(torch.meshgrid(*coordinates, indexing="xy"), dim=-1)

    return coordinates, stacked_indices


def homogenize_points(points: torch.Tensor) -> torch.Tensor:  # "*batch dim"  # "*batch dim+1"
    """Convert batched points (xyz) to (xyz1)."""
    return torch.cat([points, torch.ones_like(points[..., :1])], dim=-1)


def homogenize_vectors(vectors: torch.Tensor) -> torch.Tensor:  #  "*batch dim"  # "*batch dim+1"
    """Convert batched vectors (xyz) to (xyz0)."""
    return torch.cat([vectors, torch.zeros_like(vectors[..., :1])], dim=-1)


def transform_rigid(
    homogeneous_coordinates: torch.Tensor,  # "*#batch dim"
    transformation: torch.Tensor,  # "*#batch dim dim"
) -> torch.Tensor:  # "*batch dim"
    """Apply a rigid-body transformation to points or vectors."""
    return einsum(
        transformation,
        homogeneous_coordinates.to(transformation.dtype),
        "... i j, ... j -> ... i",
    )


def transform_cam2world(
    homogeneous_coordinates: torch.Tensor,  # "*#batch dim"
    extrinsics: torch.Tensor,  # "*#batch dim dim"
) -> torch.Tensor:  # "*batch dim"
    """Transform points from 3D camera coordinates to 3D world coordinates."""
    return transform_rigid(homogeneous_coordinates, extrinsics)


def unproject(
    coordinates: torch.Tensor,  # "*#batch dim"
    z: torch.Tensor,  # "*#batch"
    intrinsics: torch.Tensor,  # "*#batch dim+1 dim+1"
) -> torch.Tensor:  # "*batch dim+1"
    """Unproject 2D camera coordinates with the given Z values."""

    # Apply the inverse intrinsics to the coordinates.
    coordinates = homogenize_points(coordinates)
    ray_directions = einsum(
        intrinsics.float().inverse().to(intrinsics),
        coordinates.to(intrinsics.dtype),
        "... i j, ... j -> ... i",
    )

    # Apply the supplied depth values.
    return ray_directions * z[..., None]


def get_world_rays(
    coordinates: torch.Tensor,  # "*#batch dim"
    extrinsics: torch.Tensor,  # "*#batch dim+2 dim+2"
    intrinsics: torch.Tensor,  # "*#batch dim+1 dim+1"
) -> tuple[
    torch.Tensor,  # origins, "*batch dim+1"
    torch.Tensor,  # directions, "*batch dim+1"
]:
    # Get camera-space ray directions.
    directions = unproject(
        coordinates,
        torch.ones_like(coordinates[..., 0]),
        intrinsics,
    )
    directions = directions / directions.norm(dim=-1, keepdim=True)

    # Transform ray directions to world coordinates.
    directions = homogenize_vectors(directions)
    directions = transform_cam2world(directions, extrinsics)[..., :-1]

    # Tile the ray origins to have the same shape as the ray directions.
    origins = extrinsics[..., :-1, -1].broadcast_to(directions.shape)

    return origins, directions


def get_fov(intrinsics: torch.Tensor) -> torch.Tensor:  # "batch 3 3" -> "batch 2"
    intrinsics_inv = intrinsics.float().inverse().to(intrinsics)

    def process_vector(vector):
        vector = torch.tensor(vector, dtype=intrinsics.dtype, device=intrinsics.device)
        vector = einsum(intrinsics_inv, vector, "b i j, j -> b i")
        return vector / vector.norm(dim=-1, keepdim=True)

    left = process_vector([0, 0.5, 1])
    right = process_vector([1, 0.5, 1])
    top = process_vector([0.5, 0, 1])
    bottom = process_vector([0.5, 1, 1])
    fov_x = (left * right).sum(dim=-1).acos()
    fov_y = (top * bottom).sum(dim=-1).acos()
    return torch.stack((fov_x, fov_y), dim=-1)


def map_pdf_to_opacity(
    pdf: torch.Tensor,  # " *batch"
    global_step: int = 0,
    opacity_mapping: Optional[dict] = None,
) -> torch.Tensor:  # " *batch"
    # https://www.desmos.com/calculator/opvwti3ba9

    # Figure out the exponent.
    if opacity_mapping is not None:
        cfg = SimpleNamespace(**opacity_mapping)
        x = cfg.initial + min(global_step / cfg.warm_up, 1) * (cfg.final - cfg.initial)
    else:
        x = 0.0
    exponent = 2**x

    # Map the probability density to an opacity.
    return 0.5 * (1 - (1 - pdf) ** exponent + pdf ** (1 / exponent))

def normalize_homogenous_points(points):
    """Normalize the point vectors"""
    return points / points[..., -1:]

def inverse_intrinsic_matrix(ixts):
    """ """
    return torch.inverse(ixts)

def pixel_space_to_camera_space(pixel_space_points, depth, intrinsics):
    """
    Convert pixel space points to camera space points.

    Args:
        pixel_space_points (torch.Tensor): Pixel space points with shape (h, w, 2)
        depth (torch.Tensor): Depth map with shape (b, v, h, w, 1)
        intrinsics (torch.Tensor): Camera intrinsics with shape (b, v, 3, 3)

    Returns:
        torch.Tensor: Camera space points with shape (b, v, h, w, 3).
    """
    pixel_space_points = homogenize_points(pixel_space_points)
    # camera_space_points = torch.einsum(
    #     "b v i j , h w j -> b v h w i", intrinsics.inverse(), pixel_space_points
    # )
    camera_space_points = torch.einsum(
        "b v i j , h w j -> b v h w i", inverse_intrinsic_matrix(intrinsics), pixel_space_points
    )
    camera_space_points = camera_space_points * depth
    return camera_space_points


def camera_space_to_world_space(camera_space_points, c2w):
    """
    Convert camera space points to world space points.

    Args:
        camera_space_points (torch.Tensor): Camera space points with shape (b, v, h, w, 3)
        c2w (torch.Tensor): Camera to world extrinsics matrix with shape (b, v, 4, 4)

    Returns:
        torch.Tensor: World space points with shape (b, v, h, w, 3).
    """
    camera_space_points = homogenize_points(camera_space_points)
    world_space_points = torch.einsum("b v i j , b v h w j -> b v h w i", c2w, camera_space_points)
    return world_space_points[..., :3]


def camera_space_to_pixel_space(camera_space_points, intrinsics):
    """
    Convert camera space points to pixel space points.

    Args:
        camera_space_points (torch.Tensor): Camera space points with shape (b, v1, v2, h, w, 3)
        c2w (torch.Tensor): Camera to world extrinsics matrix with shape (b, v2, 3, 3)

    Returns:
        torch.Tensor: World space points with shape (b, v1, v2, h, w, 2).
    """
    camera_space_points = normalize_homogenous_points(camera_space_points)
    pixel_space_points = torch.einsum(
        "b u i j , b v u h w j -> b v u h w i", intrinsics, camera_space_points
    )
    return pixel_space_points[..., :2]


def world_space_to_camera_space(world_space_points, c2w):
    """
    Convert world space points to pixel space points.

    Args:
        world_space_points (torch.Tensor): World space points with shape (b, v1, h, w, 3)
        c2w (torch.Tensor): Camera to world extrinsics matrix with shape (b, v2, 4, 4)

    Returns:
        torch.Tensor: Camera space points with shape (b, v1, v2, h, w, 3).
    """
    world_space_points = homogenize_points(world_space_points)
    camera_space_points = torch.einsum(
        "b u i j , b v h w j -> b v u h w i", c2w.inverse(), world_space_points
    )
    return camera_space_points[..., :3]


def unproject_depth(
    depth, intrinsics, c2w=None, ixt_normalized=False, num_patches_x=None, num_patches_y=None
):
    """
    Turn the depth map into a 3D point cloud in world space

    Args:
        depth: (b, v, h, w, 1)
        intrinsics: (b, v, 3, 3)
        c2w: (b, v, 4, 4)

    Returns:
        torch.Tensor: World space points with shape (b, v, h, w, 3).
    """
    if c2w is None:
        c2w = torch.eye(4, device=depth.device, dtype=depth.dtype)
        c2w = c2w[None, None].repeat(depth.shape[0], depth.shape[1], 1, 1)

    if not ixt_normalized:
        # Compute indices of pixels
        h, w = depth.shape[-3], depth.shape[-2]
        x_grid, y_grid = torch.meshgrid(
            torch.arange(w, device=depth.device, dtype=depth.dtype),
            torch.arange(h, device=depth.device, dtype=depth.dtype),
            indexing="xy",
        )  # (h, w), (h, w)
    else:
        # ixt_normalized: h=w=2.0. cx, cy, fx, fy are normalized according to h=w=2.0
        assert num_patches_x is not None and num_patches_y is not None
        dx = 1 / num_patches_x
        dy = 1 / num_patches_y
        max_y = 1 - dy
        min_y = -max_y
        max_x = 1 - dx
        min_x = -max_x

        grid_shift = 1.0
        y_grid, x_grid = torch.meshgrid(
            torch.linspace(
                min_y + grid_shift,
                max_y + grid_shift,
                num_patches_y,
                dtype=torch.float32,
                device=depth.device,
            ),
            torch.linspace(
                min_x + grid_shift,
                max_x + grid_shift,
                num_patches_x,
                dtype=torch.float32,
                device=depth.device,
            ),
            indexing="ij",
        )

    # Compute coordinates of pixels in camera space
    pixel_space_points = torch.stack((x_grid, y_grid), dim=-1)  # (..., h, w, 2)
    camera_points = pixel_space_to_camera_space(
        pixel_space_points, depth, intrinsics
    )  # (..., h, w, 3)

    # Convert points to world space
    world_points = camera_space_to_world_space(camera_points, c2w)  # (..., h, w, 3)

    return world_points


================================================
FILE: src/depth_anything_3/utils/gsply_helpers.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
from pathlib import Path
from typing import Optional
import numpy as np
import torch
from einops import rearrange, repeat
from plyfile import PlyData, PlyElement
from torch import Tensor

from depth_anything_3.specs import Gaussians


def construct_list_of_attributes(num_rest: int) -> list[str]:
    attributes = ["x", "y", "z", "nx", "ny", "nz"]
    for i in range(3):
        attributes.append(f"f_dc_{i}")
    for i in range(num_rest):
        attributes.append(f"f_rest_{i}")
    attributes.append("opacity")
    for i in range(3):
        attributes.append(f"scale_{i}")
    for i in range(4):
        attributes.append(f"rot_{i}")
    return attributes


def export_ply(
    means: Tensor,  # "gaussian 3"
    scales: Tensor,  # "gaussian 3"
    rotations: Tensor,  # "gaussian 4"
    harmonics: Tensor,  # "gaussian 3 d_sh"
    opacities: Tensor,  # "gaussian"
    path: Path,
    shift_and_scale: bool = False,
    save_sh_dc_only: bool = True,
    match_3dgs_mcmc_dev: Optional[bool] = False,
):
    if shift_and_scale:
        # Shift the scene so that the median Gaussian is at the origin.
        means = means - means.median(dim=0).values

        # Rescale the scene so that most Gaussians are within range [-1, 1].
        scale_factor = means.abs().quantile(0.95, dim=0).max()
        means = means / scale_factor
        scales = scales / scale_factor

    rotations = rotations.detach().cpu().numpy()

    # Since current model use SH_degree = 4,
    # which require large memory to store, we can only save the DC band to save memory.
    f_dc = harmonics[..., 0]
    f_rest = harmonics[..., 1:].flatten(start_dim=1)

    if match_3dgs_mcmc_dev:
        sh_degree = 3
        n_rest = 3 * (sh_degree + 1) ** 2 - 3
        f_rest = repeat(
            torch.zeros_like(harmonics[..., :1]), "... i -> ... (n i)", n=(n_rest // 3)
        ).flatten(start_dim=1)
        dtype_full = [
            (attribute, "f4")
            for attribute in construct_list_of_attributes(num_rest=n_rest)
            if attribute not in ("nx", "ny", "nz")
        ]
    else:
        dtype_full = [
            (attribute, "f4")
            for attribute in construct_list_of_attributes(
                0 if save_sh_dc_only else f_rest.shape[1]
            )
        ]
    elements = np.empty(means.shape[0], dtype=dtype_full)
    attributes = [
        means.detach().cpu().numpy(),
        torch.zeros_like(means).detach().cpu().numpy(),
        f_dc.detach().cpu().contiguous().numpy(),
        f_rest.detach().cpu().contiguous().numpy(),
        opacities[..., None].detach().cpu().numpy(),
        scales.log().detach().cpu().numpy(),
        rotations,
    ]
    if match_3dgs_mcmc_dev:
        attributes.pop(1)  # dummy normal is not needed
    elif save_sh_dc_only:
        attributes.pop(3)  # remove f_rest from attributes

    attributes = np.concatenate(attributes, axis=1)
    elements[:] = list(map(tuple, attributes))
    path.parent.mkdir(exist_ok=True, parents=True)
    PlyData([PlyElement.describe(elements, "vertex")]).write(path)


def inverse_sigmoid(x):
    return torch.log(x / (1 - x))


def save_gaussian_ply(
    gaussians: Gaussians,
    save_path: str,
    ctx_depth: torch.Tensor,  # depth of input views; for getting shape and filtering, "v h w 1"
    shift_and_scale: bool = False,
    save_sh_dc_only: bool = True,
    gs_views_interval: int = 1,
    inv_opacity: Optional[bool] = True,
    prune_by_depth_percent: Optional[float] = 1.0,
    prune_border_gs: Optional[bool] = True,
    match_3dgs_mcmc_dev: Optional[bool] = False,
):
    b = gaussians.means.shape[0]
    assert b == 1, "must set batch_size=1 when exporting 3D gaussians"
    src_v, out_h, out_w, _ = ctx_depth.shape

    # extract gs params
    world_means = gaussians.means
    world_shs = gaussians.harmonics
    world_rotations = gaussians.rotations
    gs_scales = gaussians.scales
    gs_opacities = inverse_sigmoid(gaussians.opacities) if inv_opacity else gaussians.opacities

    # Create a mask to filter the Gaussians.

    # TODO: prune the sky region here

    # throw away Gaussians at the borders, since they're generally of lower quality.
    if prune_border_gs:
        mask = torch.zeros_like(ctx_depth, dtype=torch.bool)
        gstrim_h = int(8 / 256 * out_h)
        gstrim_w = int(8 / 256 * out_w)
        mask[:, gstrim_h:-gstrim_h, gstrim_w:-gstrim_w, :] = 1
    else:
        mask = torch.ones_like(ctx_depth, dtype=torch.bool)

    # trim the far away point based on depth;
    if prune_by_depth_percent is not None and prune_by_depth_percent < 1:
        in_depths = ctx_depth
        d_percentile = torch.quantile(
            in_depths.view(in_depths.shape[0], -1), q=prune_by_depth_percent, dim=1
        ).view(-1, 1, 1)
        d_mask = (in_depths[..., 0] <= d_percentile).unsqueeze(-1)
        mask = mask & d_mask
    mask = mask.squeeze(-1)  # v h w

    # helper fn, must place after mask
    def trim_select_reshape(element):
        selected_element = rearrange(
            element[0], "(v h w) ... -> v h w ...", v=src_v, h=out_h, w=out_w
        )
        selected_element = selected_element[::gs_views_interval][mask[::gs_views_interval]]
        return selected_element

    export_ply(
        means=trim_select_reshape(world_means),
        scales=trim_select_reshape(gs_scales),
        rotations=trim_select_reshape(world_rotations),
        harmonics=trim_select_reshape(world_shs),
        opacities=trim_select_reshape(gs_opacities),
        path=Path(save_path),
        shift_and_scale=shift_and_scale,
        save_sh_dc_only=save_sh_dc_only,
        match_3dgs_mcmc_dev=match_3dgs_mcmc_dev,
    )



================================================
FILE: src/depth_anything_3/utils/layout_helpers.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

"""This file contains useful layout utilities for images. They are:

- add_border: Add a border to an image.
- cat/hcat/vcat: Join images by arranging them in a line. If the images have different
  sizes, they are aligned as specified (start, end, center). Allows you to specify a gap
  between images.

Images are assumed to be float32 tensors with shape (channel, height, width).
"""

from typing import Any, Generator, Iterable, Literal, Union
import torch
from torch import Tensor

Alignment = Literal["start", "center", "end"]
Axis = Literal["horizontal", "vertical"]
Color = Union[
    int,
    float,
    Iterable[int],
    Iterable[float],
    Tensor,
    Tensor,
]


def _sanitize_color(color: Color) -> Tensor:  # "#channel"
    # Convert tensor to list (or individual item).
    if isinstance(color, torch.Tensor):
        color = color.tolist()

    # Turn iterators and individual items into lists.
    if isinstance(color, Iterable):
        color = list(color)
    else:
        color = [color]

    return torch.tensor(color, dtype=torch.float32)


def _intersperse(iterable: Iterable, delimiter: Any) -> Generator[Any, None, None]:
    it = iter(iterable)
    yield next(it)
    for item in it:
        yield delimiter
        yield item


def _get_main_dim(main_axis: Axis) -> int:
    return {
        "horizontal": 2,
        "vertical": 1,
    }[main_axis]


def _get_cross_dim(main_axis: Axis) -> int:
    return {
        "horizontal": 1,
        "vertical": 2,
    }[main_axis]


def _compute_offset(base: int, overlay: int, align: Alignment) -> slice:
    assert base >= overlay
    offset = {
        "start": 0,
        "center": (base - overlay) // 2,
        "end": base - overlay,
    }[align]
    return slice(offset, offset + overlay)


def overlay(
    base: Tensor,  # "channel base_height base_width"
    overlay: Tensor,  # "channel overlay_height overlay_width"
    main_axis: Axis,
    main_axis_alignment: Alignment,
    cross_axis_alignment: Alignment,
) -> Tensor:  # "channel base_height base_width"
    # The overlay must be smaller than the base.
    _, base_height, base_width = base.shape
    _, overlay_height, overlay_width = overlay.shape
    assert base_height >= overlay_height and base_width >= overlay_width

    # Compute spacing on the main dimension.
    main_dim = _get_main_dim(main_axis)
    main_slice = _compute_offset(
        base.shape[main_dim], overlay.shape[main_dim], main_axis_alignment
    )

    # Compute spacing on the cross dimension.
    cross_dim = _get_cross_dim(main_axis)
    cross_slice = _compute_offset(
        base.shape[cross_dim], overlay.shape[cross_dim], cross_axis_alignment
    )

    # Combine the slices and paste the overlay onto the base accordingly.
    selector = [..., None, None]
    selector[main_dim] = main_slice
    selector[cross_dim] = cross_slice
    result = base.clone()
    result[selector] = overlay
    return result


def cat(
    main_axis: Axis,
    *images: Iterable[Tensor],  # "channel _ _"
    align: Alignment = "center",
    gap: int = 8,
    gap_color: Color = 1,
) -> Tensor:  # "channel height width"
    """Arrange images in a line. The interface resembles a CSS div with flexbox."""
    device = images[0].device
    gap_color = _sanitize_color(gap_color).to(device)

    # Find the maximum image side length in the cross axis dimension.
    cross_dim = _get_cross_dim(main_axis)
    cross_axis_length = max(image.shape[cross_dim] for image in images)

    # Pad the images.
    padded_images = []
    for image in images:
        # Create an empty image with the correct size.
        padded_shape = list(image.shape)
        padded_shape[cross_dim] = cross_axis_length
        base = torch.ones(padded_shape, dtype=torch.float32, device=device)
        base = base * gap_color[:, None, None]
        padded_images.append(overlay(base, image, main_axis, "start", align))

    # Intersperse separators if necessary.
    if gap > 0:
        # Generate a separator.
        c, _, _ = images[0].shape
        separator_size = [gap, gap]
        separator_size[cross_dim - 1] = cross_axis_length
        separator = torch.ones((c, *separator_size), dtype=torch.float32, device=device)
        separator = separator * gap_color[:, None, None]

        # Intersperse the separator between the images.
        padded_images = list(_intersperse(padded_images, separator))

    return torch.cat(padded_images, dim=_get_main_dim(main_axis))


def hcat(
    *images: Iterable[Tensor],  # "channel _ _"
    align: Literal["start", "center", "end", "top", "bottom"] = "start",
    gap: int = 8,
    gap_color: Color = 1,
):
    """Shorthand for a horizontal linear concatenation."""
    return cat(
        "horizontal",
        *images,
        align={
            "start": "start",
            "center": "center",
            "end": "end",
            "top": "start",
            "bottom": "end",
        }[align],
        gap=gap,
        gap_color=gap_color,
    )


def vcat(
    *images: Iterable[Tensor],  # "channel _ _"
    align: Literal["start", "center", "end", "left", "right"] = "start",
    gap: int = 8,
    gap_color: Color = 1,
):
    """Shorthand for a horizontal linear concatenation."""
    return cat(
        "vertical",
        *images,
        align={
            "start": "start",
            "center": "center",
            "end": "end",
            "left": "start",
            "right": "end",
        }[align],
        gap=gap,
        gap_color=gap_color,
    )


def add_border(
    image: Tensor,  # "channel height width"
    border: int = 8,
    color: Color = 1,
) -> Tensor:  # "channel new_height new_width"
    color = _sanitize_color(color).to(image)
    c, h, w = image.shape
    result = torch.empty(
        (c, h + 2 * border, w + 2 * border), dtype=torch.float32, device=image.device
    )
    result[:] = color[:, None, None]
    result[:, border : h + border, border : w + border] = image
    return result



================================================
FILE: src/depth_anything_3/utils/logger.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

import os
import sys


class Color:
    RED = "\033[91m"
    YELLOW = "\033[93m"
    WHITE = "\033[97m"
    GREEN = "\033[92m"
    RESET = "\033[0m"


LOG_LEVELS = {"ERROR": 0, "WARN": 1, "INFO": 2, "DEBUG": 3}

COLOR_MAP = {"ERROR": Color.RED, "WARN": Color.YELLOW, "INFO": Color.WHITE, "DEBUG": Color.GREEN}


def get_env_log_level():
    level = os.environ.get("DA3_LOG_LEVEL", "INFO").upper()
    return LOG_LEVELS.get(level, LOG_LEVELS["INFO"])


class Logger:
    def __init__(self):
        self.level = get_env_log_level()

    def log(self, level_str, *args, **kwargs):
        level_key = level_str.split(":")[0].strip()
        level_val = LOG_LEVELS.get(level_key)
        if level_val is None:
            raise ValueError(f"Unknown log level: {level_str}")
        if self.level >= level_val:
            color = COLOR_MAP[level_key]
            msg = " ".join(str(arg) for arg in args)

            # Align log level output in square brackets
            # ERROR and DEBUG are 5 characters, INFO and WARN have an extra space for alignment
            tag = level_key
            if tag in ("INFO", "WARN"):
                tag += " "
            print(
                f"{color}[{tag}] {msg}{Color.RESET}",
                file=sys.stderr if level_key == "ERROR" else sys.stdout,
                **kwargs,
            )

    def error(self, *args, **kwargs):
        self.log("ERROR:", *args, **kwargs)

    def warn(self, *args, **kwargs):
        self.log("WARN:", *args, **kwargs)

    def info(self, *args, **kwargs):
        self.log("INFO:", *args, **kwargs)

    def debug(self, *args, **kwargs):
        self.log("DEBUG:", *args, **kwargs)


logger = Logger()

__all__ = ["logger"]

if __name__ == "__main__":
    logger.info("This is an info message")
    logger.warn("This is a warning message")
    logger.error("This is an error message")
    logger.debug("This is a debug message")



================================================
FILE: src/depth_anything_3/utils/memory.py
================================================
"""
GPU memory utility helpers.

Shared cleanup and memory checking logic used by both the backend API and
the Gradio UI to keep memory-management behavior consistent.
"""
from __future__ import annotations

import gc

from typing import Any, Dict, Optional

import torch


def get_gpu_memory_info() -> Optional[Dict[str, Any]]:
    """Return a snapshot of current GPU memory usage or None if CUDA not available.

    Keys in returned dict: total_gb, allocated_gb, reserved_gb, free_gb, utilization
    """
    if not torch.cuda.is_available():
        return None

    try:
        device = torch.cuda.current_device()
        total_memory = torch.cuda.get_device_properties(device).total_memory
        allocated_memory = torch.cuda.memory_allocated(device)
        reserved_memory = torch.cuda.memory_reserved(device)
        free_memory = total_memory - reserved_memory

        return {
            "total_gb": total_memory / 1024 ** 3,
            "allocated_gb": allocated_memory / 1024 ** 3,
            "reserved_gb": reserved_memory / 1024 ** 3,
            "free_gb": free_memory / 1024 ** 3,
            "utilization": (reserved_memory / total_memory) * 100,
        }
    except Exception:
        return None


def cleanup_cuda_memory() -> None:
    """Perform a robust GPU cleanup sequence.

    This includes synchronizing, emptying caches, collecting IPC handles and
    running the Python garbage collector. Use this instead of a raw
    ``torch.cuda.empty_cache()`` where you need reliable freeing of GPU memory
    between model loads or in error handling paths.
    """
    try:
        if torch.cuda.is_available():
            mem_before = get_gpu_memory_info()

            torch.cuda.synchronize()
            torch.cuda.empty_cache()
            # Collect cross-process cuda resources
            try:
                torch.cuda.ipc_collect()
            except Exception:
                # Older PyTorch versions or non-cuda devices may not support
                # ipc_collect (no-op if not available)
                pass
            gc.collect()

            mem_after = get_gpu_memory_info()
            if mem_before and mem_after:
                freed = mem_before["reserved_gb"] - mem_after["reserved_gb"]
                print(
                    f"CUDA cleanup: freed {freed:.2f}GB, "
                    f"available: {mem_after['free_gb']:.2f}GB/{mem_after['total_gb']:.2f}GB"
                )
            else:
                print("CUDA memory cleanup completed")
    except Exception as e:
        print(f"Warning: CUDA cleanup failed: {e}")


def check_memory_availability(required_gb: float = 2.0) -> tuple[bool, str]:
    """Return whether at least ``required_gb`` seems available on the current GPU.

    The returned tuple is (is_available, message) with a human-friendly message.
    """
    try:
        if not torch.cuda.is_available():
            return False, "CUDA is not available"

        mem_info = get_gpu_memory_info()
        if mem_info is None:
            return True, "Cannot check memory, proceeding anyway"

        if mem_info["free_gb"] < required_gb:
            return (
                False,
                (
                    f"Insufficient GPU memory: {mem_info['free_gb']:.2f}GB available, "
                    f"{required_gb:.2f}GB required. Total: {mem_info['total_gb']:.2f}GB, "
                    f"Used: {mem_info['reserved_gb']:.2f}GB ({mem_info['utilization']:.1f}%)"
                ),
            )

        return (
            True,
            (
                f"Memory check passed: {mem_info['free_gb']:.2f}GB available, "
                f"{required_gb:.2f}GB required"
            ),
        )
    except Exception as e:
        return True, f"Memory check failed: {e}, proceeding anyway"
def estimate_memory_requirement(num_images: int, process_res: int) -> float:
    """Heuristic estimate for memory usage (GB) based on image count and resolution.

    This mirrors the simple policy used by the backend service so other code
    (e.g., Gradio UI) can make consistent decisions when checking available
    memory before loading a model or running inference.

    Args:
        num_images: Number of images to process.
        process_res: Processing resolution.

    Returns:
        Estimated memory requirement in GB.
    """
    base_memory = 2.0
    per_image_memory = (process_res / 504) ** 2 * 0.5
    total_memory = base_memory + (num_images * per_image_memory * 0.1)
    return total_memory



================================================
FILE: src/depth_anything_3/utils/model_loading.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

"""
Model loading and state dict conversion utilities.
"""

from typing import Dict, Tuple
import torch

from depth_anything_3.utils.logger import logger


def convert_general_state_dict(state_dict: Dict[str, torch.Tensor]) -> Dict[str, torch.Tensor]:
    """
    Convert general model state dict to match current model architecture.

    Args:
        state_dict: Original state dictionary

    Returns:
        Converted state dictionary
    """
    # Replace module prefixes
    state_dict = {k.replace("module.", "model."): v for k, v in state_dict.items()}
    state_dict = {k.replace(".net.", ".backbone."): v for k, v in state_dict.items()}

    # Remove camera token if present
    if "model.backbone.pretrained.camera_token" in state_dict:
        del state_dict["model.backbone.pretrained.camera_token"]

    # Replace camera token naming
    state_dict = {
        k.replace(".camera_token_extra", ".camera_token"): v for k, v in state_dict.items()
    }

    # Replace head naming
    state_dict = {
        k.replace("model.all_heads.camera_cond_head", "model.cam_enc"): v
        for k, v in state_dict.items()
    }
    state_dict = {
        k.replace("model.all_heads.camera_head", "model.cam_dec"): v for k, v in state_dict.items()
    }
    state_dict = {k.replace(".more_mlps.", ".backbone."): v for k, v in state_dict.items()}
    state_dict = {k.replace(".fc_rot.", ".fc_qvec."): v for k, v in state_dict.items()}
    state_dict = {
        k.replace("model.all_heads.head", "model.head"): v for k, v in state_dict.items()
    }

    # Replace output naming
    state_dict = {
        k.replace("output_conv2_additional.sky_mask", "sky_output_conv2"): v
        for k, v in state_dict.items()
    }
    state_dict = {k.replace("_ray.", "_aux."): v for k, v in state_dict.items()}

    # Update GS-DPT head naming and value
    state_dict = {k.replace("gaussian_param_head.", "gs_head."): v for k, v in state_dict.items()}

    return state_dict


def convert_metric_state_dict(state_dict: Dict[str, torch.Tensor]) -> Dict[str, torch.Tensor]:
    """
    Convert metric model state dict to match current model architecture.

    Args:
        state_dict: Original metric state dictionary

    Returns:
        Converted state dictionary
    """
    # Add module prefix for metric models
    state_dict = {"module." + k: v for k, v in state_dict.items()}
    return convert_general_state_dict(state_dict)


def load_pretrained_weights(model, model_path: str, is_metric: bool = False) -> Tuple[list, list]:
    """
    Load pretrained weights for a single model.

    Args:
        model: Model instance to load weights into
        model_path: Path to the pretrained weights
        is_metric: Whether this is a metric model

    Returns:
        Tuple of (missed_keys, unexpected_keys)
    """
    state_dict = torch.load(model_path, map_location="cpu")

    if is_metric:
        state_dict = convert_metric_state_dict(state_dict)
    else:
        state_dict = convert_general_state_dict(state_dict)

    missed, unexpected = model.load_state_dict(state_dict, strict=False)
    logger.info("Missed keys:", missed)
    logger.info("Unexpected keys:", unexpected)

    return missed, unexpected


def load_pretrained_nested_weights(
    model, main_model_path: str, metric_model_path: str
) -> Tuple[list, list]:
    """
    Load pretrained weights for a nested model with both main and metric branches.

    Args:
        model: Nested model instance
        main_model_path: Path to main model weights
        metric_model_path: Path to metric model weights

    Returns:
        Tuple of (missed_keys, unexpected_keys)
    """
    # Load main model weights
    state_dict0 = torch.load(main_model_path, map_location="cpu")
    state_dict0 = convert_general_state_dict(state_dict0)
    state_dict0 = {k.replace("model.", "model.da3."): v for k, v in state_dict0.items()}

    # Load metric model weights
    state_dict1 = torch.load(metric_model_path, map_location="cpu")
    state_dict1 = convert_metric_state_dict(state_dict1)
    state_dict1 = {k.replace("model.", "model.da3_metric."): v for k, v in state_dict1.items()}

    # Combine state dictionaries
    combined_state_dict = state_dict0.copy()
    combined_state_dict.update(state_dict1)

    missed, unexpected = model.load_state_dict(combined_state_dict, strict=False)

    print("Missed keys:", missed)
    print("Unexpected keys:", unexpected)

    return missed, unexpected



================================================
FILE: src/depth_anything_3/utils/parallel_utils.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

import asyncio
import os
from functools import wraps
from multiprocessing.pool import ThreadPool
from threading import Thread
from typing import Callable, Dict, List
import imageio
from tqdm import tqdm


def async_call_func(func):
    @wraps(func)
    async def wrapper(*args, **kwargs):
        loop = asyncio.get_event_loop()
        # Use run_in_executor to run the blocking function in a separate thread
        return await loop.run_in_executor(None, func, *args, **kwargs)

    return wrapper


slice_func = lambda chunk_index, chunk_dim, chunk_size: [slice(None)] * chunk_dim + [
    slice(chunk_index, chunk_index + chunk_size)
]


def async_call(fn):
    def wrapper(*args, **kwargs):
        Thread(target=fn, args=args, kwargs=kwargs).start()

    return wrapper


def _save_image_impl(save_img, save_path):
    """Common implementation for saving images synchronously or asynchronously"""
    os.makedirs(os.path.dirname(save_path), exist_ok=True)
    imageio.imwrite(save_path, save_img)


@async_call
def save_image_async(save_img, save_path):
    """Save image asynchronously"""
    _save_image_impl(save_img, save_path)


def save_image(save_img, save_path):
    """Save image synchronously"""
    _save_image_impl(save_img, save_path)


def parallel_execution(
    *args,
    action: Callable,
    num_processes=32,
    print_progress=False,
    sequential=False,
    async_return=False,
    desc=None,
    **kwargs,
):
    # Partially copy from EasyVolumetricVideo (parallel_execution)
    # NOTE: we expect first arg / or kwargs to be distributed
    # NOTE: print_progress arg is reserved.
    # `*args` packs all positional arguments passed to the function into a tuple
    args = list(args)

    def get_length(args: List, kwargs: Dict):
        for a in args:
            if isinstance(a, list):
                return len(a)
        for v in kwargs.values():
            if isinstance(v, list):
                return len(v)
        raise NotImplementedError

    def get_action_args(length: int, args: List, kwargs: Dict, i: int):
        action_args = [
            (arg[i] if isinstance(arg, list) and len(arg) == length else arg) for arg in args
        ]
        # TODO: Support all types of iterable
        action_kwargs = {
            key: (
                kwargs[key][i]
                if isinstance(kwargs[key], list) and len(kwargs[key]) == length
                else kwargs[key]
            )
            for key in kwargs
        }
        return action_args, action_kwargs

    if not sequential:
        # Create ThreadPool
        pool = ThreadPool(processes=num_processes)

        # Spawn threads
        results = []
        asyncs = []
        length = get_length(args, kwargs)
        for i in range(length):
            action_args, action_kwargs = get_action_args(length, args, kwargs, i)
            async_result = pool.apply_async(action, action_args, action_kwargs)
            asyncs.append(async_result)

        # Join threads and get return values
        if not async_return:
            for async_result in tqdm(asyncs, desc=desc, disable=not print_progress):
                results.append(async_result.get())  # will sync the corresponding thread
            pool.close()
            pool.join()
            return results
        else:
            return pool
    else:
        results = []
        length = get_length(args, kwargs)
        for i in tqdm(range(length), desc=desc, disable=not print_progress):
            action_args, action_kwargs = get_action_args(length, args, kwargs, i)
            async_result = action(*action_args, **action_kwargs)
            results.append(async_result)
        return results



================================================
FILE: src/depth_anything_3/utils/pca_utils.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

"""
PCA utilities for feature visualization and dimensionality reduction (video-friendly).
- Support frame-by-frame: transform_frame / transform_video
- Support one-time global PCA fitting and reuse (mean, V3) for stable colors
- Support Procrustes alignment (solving principal component order/sign/rotation jumps)
- Support global fixed or temporal EMA for percentiles (time dimension only, no spatial)
"""

import numpy as np
import torch


def pca_to_rgb_4d_bf16_percentile(
    x_np: np.ndarray,
    device=None,
    q_oversample: int = 6,
    clip_percent: float = 10.0,  # Percentage to clip from top and bottom (0~49.9)
    return_uint8: bool = False,
    enable_autocast_bf16: bool = True,
):
    """
    Reduce numpy array of shape (49, 27, 36, 3072) to 3D via PCA and visualize as (49, 27, 36, 3).
    - PCA uses torch.pca_lowrank (randomized SVD), defaults to GPU.
    - Uses CUDA bf16 autocast in computation (if available),
      then per-channel percentile clipping and normalization.
    - Default removes 5% outliers from top and bottom (adjustable via clip_percent) to
      improve visualization contrast.

    Parameters
    ----------
    x_np : np.ndarray
        Shape must be (49, 27, 36, 3072). dtype recommended float32/float64.
    device : str | None
        Specify 'cuda' or 'cpu'. Auto-select if None (prefer cuda).
    q_oversample : int
        Oversampling q for pca_lowrank, must be >= 3.
        Slightly larger than target dim (3) is more stable, default 6.
    clip_percent : float
        Percentage to clip from top and bottom (0~49.9),
        e.g. 5.0 means clip lowest 5% and highest 5% per channel.
    return_uint8 : bool
        True returns uint8(0~255), otherwise returns float32(0~1).
    enable_autocast_bf16 : bool
        Enable bf16 autocast on CUDA.

    Returns
    -------
    np.ndarray
        Array of shape (49, 27, 36, 3), float32[0,1] or uint8[0,255].
    """
    assert (
        x_np.ndim == 4
    )  # and x_np.shape[-1] == 3072, f"expect (49,27,36,3072), got {x_np.shape}"
    B1, B2, B3, D = x_np.shape
    N = B1 * B2 * B3

    # Device selection
    if device is None:
        device = "cuda" if torch.cuda.is_available() else "cpu"

    # Convert input to torch, unified float32
    X = torch.from_numpy(x_np.reshape(N, D)).to(device=device, dtype=torch.float32)

    # Parameter and safety checks
    k = 3
    q = max(int(q_oversample), k)
    clip_percent = float(clip_percent)
    if not (0.0 <= clip_percent < 50.0):
        raise ValueError(
            "clip_percent must be in [0, 50), e.g. 5.0 means clip 5% from top and bottom"
        )
    low = clip_percent / 100.0
    high = 1.0 - low

    with torch.no_grad():
        # Zero mean
        mean = X.mean(dim=0, keepdim=True)
        Xc = X - mean

        # Main computation: PCA + projection, try to use bf16
        # (auto-fallback if operator not supported)
        device.startswith("cuda") and enable_autocast_bf16
        U, S, V = torch.pca_lowrank(Xc, q=q, center=False)  # V: (D, q)
        V3 = V[:, :k]  # (3072, 3)
        PCs = Xc @ V3  # (N, 3)

        # === Per-channel percentile clipping and normalization to [0,1] ===
        # Vectorized one-time calculation of low/high percentiles for each channel
        qs = torch.tensor([low, high], device=PCs.device, dtype=PCs.dtype)
        qvals = torch.quantile(PCs, q=qs, dim=0)  # Shape (2, 3)
        lo = qvals[0]  # (3,)
        hi = qvals[1]  # (3,)

        # Avoid degenerate case where hi==lo
        denom = torch.clamp(hi - lo, min=1e-8)

        # Broadcast clipping + normalization
        PCs = torch.clamp(PCs, lo, hi)
        PCs = (PCs - lo) / denom  # (N, 3) in [0,1]

        # Restore 4D
        PCs = PCs.reshape(B1, B2, B3, k)

        # Output
        if return_uint8:
            out = (PCs * 255.0).round().clamp(0, 255).to(torch.uint8).cpu().numpy()
        else:
            out = PCs.clamp(0, 1).to(torch.float32).cpu().numpy()

    return out


class PCARGBVisualizer:
    """
    Stable PCA→RGB for video features shaped (T, H, W, D) or a single frame (H, W, D).
    - Global mean/V3 reference for stable colors
    - Per-frame PCA with Procrustes alignment to V3_ref (basis_mode='procrustes')
    - Percentile normalization with global or EMA stats (time-only, no spatial smoothing)
    """

    def __init__(
        self,
        device=None,
        q_oversample: int = 16,
        clip_percent: float = 10.0,
        return_uint8: bool = False,
        enable_autocast_bf16: bool = True,
        basis_mode: str = "procrustes",  # 'fixed' | 'procrustes'
        percentile_mode: str = "ema",  # 'global' | 'ema'
        ema_alpha: float = 0.1,
        denom_eps: float = 1e-4,
    ):
        assert 0.0 <= clip_percent < 50.0
        assert basis_mode in ("fixed", "procrustes")
        assert percentile_mode in ("global", "ema")
        self.device = device or ("cuda" if torch.cuda.is_available() else "cpu")
        self.q = max(int(q_oversample), 6)
        self.clip_percent = float(clip_percent)
        self.return_uint8 = return_uint8
        self.enable_autocast_bf16 = enable_autocast_bf16
        self.basis_mode = basis_mode
        self.percentile_mode = percentile_mode
        self.ema_alpha = float(ema_alpha)
        self.denom_eps = float(denom_eps)

        # reference state
        self.mean_ref = None  # (1, D)
        self.V3_ref = None  # (D, 3)
        self.lo_ref = None  # (3,)
        self.hi_ref = None  # (3,)

    @torch.no_grad()
    def fit_reference(self, frames):
        """
        Fit global mean/V3 and initialize percentiles from a reference set.
        frames: ndarray (T,H,W,D) or list of (H,W,D)
        """
        if isinstance(frames, np.ndarray):
            if frames.ndim != 4:
                raise ValueError("fit_reference expects (T,H,W,D) ndarray.")
            T, H, W, D = frames.shape
            X = torch.from_numpy(frames.reshape(T * H * W, D))
        else:  # list of (H,W,D)
            xs = [torch.from_numpy(x.reshape(-1, x.shape[-1])) for x in frames]
            D = xs[0].shape[-1]
            X = torch.cat(xs, dim=0)

        X = X.to(self.device, dtype=torch.float32)
        X = torch.nan_to_num(X, nan=0.0, posinf=1e6, neginf=-1e6)

        mean = X.mean(0, keepdim=True)
        Xc = X - mean

        U, S, V = torch.pca_lowrank(Xc, q=max(self.q, 8), center=False)
        V3 = V[:, :3]  # (D,3)

        PCs = Xc @ V3
        low = self.clip_percent / 100.0
        high = 1.0 - low
        qs = torch.tensor([low, high], device=PCs.device, dtype=PCs.dtype)
        qvals = torch.quantile(PCs, q=qs, dim=0)
        lo, hi = qvals[0], qvals[1]

        self.mean_ref = mean
        self.V3_ref = V3
        if self.percentile_mode == "global":
            self.lo_ref, self.hi_ref = lo, hi
        else:
            self.lo_ref = lo.clone()
            self.hi_ref = hi.clone()

    @torch.no_grad()
    def _project_with_stable_colors(self, X: torch.Tensor) -> torch.Tensor:
        """
        X: (N,D) where N = H*W
        Returns PCs_raw: (N,3) using stable basis (fixed or Procrustes-aligned)
        """
        assert self.mean_ref is not None and self.V3_ref is not None, "Call fit_reference() first."
        X = torch.nan_to_num(X, nan=0.0, posinf=1e6, neginf=-1e6)
        Xc = X - self.mean_ref

        if self.basis_mode == "fixed":
            V3_used = self.V3_ref
        else:
            U, S, V = torch.pca_lowrank(Xc, q=max(self.q, 6), center=False)
            V3 = V[:, :3]  # (D,3)
            M = V3.T @ self.V3_ref
            Uo, So, Vh = torch.linalg.svd(M)
            R = Uo @ Vh
            V3_used = V3 @ R
            # Optional polarity fix via anchor
            a = self.V3_ref.mean(0, keepdim=True)
            sign = torch.sign((V3_used * a).sum(0, keepdim=True)).clamp(min=-1)
            V3_used = V3_used * sign

        return Xc @ V3_used

    @torch.no_grad()
    def _normalize_rgb(self, PCs_raw: torch.Tensor) -> torch.Tensor:
        assert self.lo_ref is not None and self.hi_ref is not None
        if self.percentile_mode == "global":
            lo, hi = self.lo_ref, self.hi_ref
        else:
            low = self.clip_percent / 100.0
            high = 1.0 - low
            qs = torch.tensor([low, high], device=PCs_raw.device, dtype=PCs_raw.dtype)
            qvals = torch.quantile(PCs_raw, q=qs, dim=0)
            lo_now, hi_now = qvals[0], qvals[1]
            a = self.ema_alpha
            self.lo_ref = (1 - a) * self.lo_ref + a * lo_now
            self.hi_ref = (1 - a) * self.hi_ref + a * hi_now
            lo, hi = self.lo_ref, self.hi_ref

        denom = torch.clamp(hi - lo, min=self.denom_eps)
        PCs = torch.clamp(PCs_raw, lo, hi)
        PCs = (PCs - lo) / denom
        return PCs.clamp_(0, 1)

    @torch.no_grad()
    def transform_frame(self, frame: np.ndarray) -> np.ndarray:
        """
        frame: (H,W,D) -> (H,W,3)
        """
        if frame.ndim != 3:
            raise ValueError("transform_frame expects (H,W,D).")
        H, W, D = frame.shape
        X = torch.from_numpy(frame.reshape(H * W, D)).to(self.device, dtype=torch.float32)
        PCs_raw = self._project_with_stable_colors(X)
        PCs = self._normalize_rgb(PCs_raw).reshape(H, W, 3)
        if self.return_uint8:
            return (PCs * 255.0).round().clamp(0, 255).to(torch.uint8).cpu().numpy()
        return PCs.to(torch.float32).cpu().numpy()

    @torch.no_grad()
    def transform_video(self, frames) -> np.ndarray:
        """
        frames: (T,H,W,D) or list of (H,W,D)
        returns: (T,H,W,3)
        """
        outs = []
        if isinstance(frames, np.ndarray):
            if frames.ndim != 4:
                raise ValueError("transform_video expects (T,H,W,D).")
            T, H, W, D = frames.shape
            for t in range(T):
                outs.append(self.transform_frame(frames[t]))
        else:
            for f in frames:
                outs.append(self.transform_frame(f))
        return np.stack(outs, axis=0)



================================================
FILE: src/depth_anything_3/utils/pose_align.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

from typing import List
import numpy as np
import torch
from evo.core.trajectory import PosePath3D

from depth_anything_3.utils.geometry import affine_inverse, affine_inverse_np


def batch_apply_alignment_to_enc(
    rots: torch.Tensor, trans: torch.Tensor, scales: torch.Tensor, enc_list: List[torch.Tensor]
):
    pass


def batch_apply_alignment_to_ext(
    rots: torch.Tensor, trans: torch.Tensor, scales: torch.Tensor, ext: torch.Tensor
):
    device, _ = ext.device, ext.dtype
    if ext.shape[-2:] == (3, 4):
        pad = torch.zeros((*ext.shape[:-2], 4, 4), dtype=ext.dtype, device=device)
        pad[..., :3, :4] = ext
        pad[..., 3, 3] = 1.0
        ext = pad
    pose_est = affine_inverse(ext)
    pose_new_align_rot = rots[:, None] @ pose_est[..., :3, :3]
    pose_new_align_trans = (
        scales[:, None, None] * (rots[:, None] @ pose_est[..., :3, 3:])[..., 0] + trans[:, None]
    )
    pose_new_align = torch.zeros_like(ext)
    pose_new_align[..., :3, :3] = pose_new_align_rot
    pose_new_align[..., :3, 3] = pose_new_align_trans
    pose_new_align[..., 3, 3] = 1.0
    return affine_inverse(pose_new_align)[:, :3]


def batch_align_poses_umeyama(ext_ref: torch.Tensor, ext_est: torch.Tensor):
    device, dtype = ext_ref.device, ext_ref.dtype
    assert ext_ref.dtype in [torch.float32, torch.float64]
    assert ext_est.dtype in [torch.float32, torch.float64]
    assert ext_ref.requires_grad is False
    assert ext_est.requires_grad is False
    rots, trans, scales = [], [], []
    for b in range(ext_ref.shape[0]):
        r, t, s = align_poses_umeyama(ext_ref[b].cpu().numpy(), ext_est[b].cpu().numpy())
        rots.append(torch.from_numpy(r).to(device=device, dtype=dtype))
        trans.append(torch.from_numpy(t).to(device=device, dtype=dtype))
        scales.append(torch.tensor(s, device=device, dtype=dtype))
    return torch.stack(rots), torch.stack(trans), torch.stack(scales)


# Dependencies: affine_inverse_np, PosePath3D (maintain consistency with your existing project)


def _to44(ext):
    if ext.shape[1] == 3:
        out = np.eye(4)[None].repeat(len(ext), 0)
        out[:, :3, :4] = ext
        return out
    return ext


def _poses_from_ext(ext_ref, ext_est):
    ext_ref = _to44(ext_ref)
    ext_est = _to44(ext_est)
    pose_ref = affine_inverse_np(ext_ref)
    pose_est = affine_inverse_np(ext_est)
    return pose_ref, pose_est


def _umeyama_sim3_from_paths(pose_ref, pose_est):
    path_ref = PosePath3D(poses_se3=pose_ref.copy())
    path_est = PosePath3D(poses_se3=pose_est.copy())
    r, t, s = path_est.align(path_ref, correct_scale=True)
    pose_est_aligned = np.stack(path_est.poses_se3)
    return r, t, s, pose_est_aligned


def _apply_sim3_to_poses(poses, r, t, s):
    out = poses.copy()
    Ri = poses[:, :3, :3]
    ti = poses[:, :3, 3]
    out[:, :3, :3] = r @ Ri
    out[:, :3, 3] = (r @ (s * ti.T)).T + t
    return out


def _median_nn_thresh(pose_ref, pose_est_aligned):
    P_ref = pose_ref[:, :3, 3]
    P_est = pose_est_aligned[:, :3, 3]
    dists = []
    for p in P_est:
        dd = np.linalg.norm(P_ref - p[None, :], axis=1)
        dists.append(dd.min())
    return float(np.median(dists)) if dists else 0.0


def _ransac_align_sim3(
    pose_ref, pose_est, sub_n=None, inlier_thresh=None, max_iters=10, random_state=None
):
    rng = np.random.default_rng(random_state)
    N = pose_ref.shape[0]
    idx_all = np.arange(N)
    if sub_n is None:
        sub_n = max(3, (N + 1) // 2)
    else:
        sub_n = max(3, min(sub_n, N))

    # Pre-alignment + default threshold
    r0, t0, s0, pose_est0 = _umeyama_sim3_from_paths(pose_ref, pose_est)
    if inlier_thresh is None:
        inlier_thresh = _median_nn_thresh(pose_ref, pose_est0)

    P_ref_all = pose_ref[:, :3, 3]

    best_model = (r0, t0, s0)
    best_inliers = None
    best_score = (-1, np.inf)  # (num_inliers, mean_err)

    for _ in range(max_iters):
        sample = rng.choice(idx_all, size=sub_n, replace=False)
        try:
            r, t, s, _ = _umeyama_sim3_from_paths(pose_ref[sample], pose_est[sample])
        except Exception:
            continue
        pose_h = _apply_sim3_to_poses(pose_est, r, t, s)
        P_h = pose_h[:, :3, 3]
        errs = np.linalg.norm(P_h - P_ref_all, axis=1)  # Match by same index
        inliers = errs <= inlier_thresh
        k = int(inliers.sum())
        mean_err = float(errs[inliers].mean()) if k > 0 else np.inf
        if (k > best_score[0]) or (k == best_score[0] and mean_err < best_score[1]):
            best_score = (k, mean_err)
            best_model = (r, t, s)
            best_inliers = inliers

    # Fit again with best inliers
    if best_inliers is not None and best_inliers.sum() >= 3:
        r, t, s, _ = _umeyama_sim3_from_paths(pose_ref[best_inliers], pose_est[best_inliers])
    else:
        r, t, s = best_model
    return r, t, s


def align_poses_umeyama(
    ext_ref: np.ndarray,
    ext_est: np.ndarray,
    return_aligned=False,
    ransac=False,
    sub_n=None,
    inlier_thresh=None,
    ransac_max_iters=10,
    random_state=None,
):
    """
    Align estimated trajectory to reference using Umeyama Sim(3).
    Default no RANSAC; if ransac=True, use RANSAC (max iterations default 10).
    - sub_n defaults to half the number of frames (rounded up, at least 3)
    - inlier_thresh defaults to median of "distance from each estimated pose to
      nearest reference pose after pre-alignment"
    Returns rotation (3x3), translation (3,), scale; optionally returns aligned extrinsics (4x4).
    """
    pose_ref, pose_est = _poses_from_ext(ext_ref, ext_est)

    if not ransac:
        r, t, s, pose_est_aligned = _umeyama_sim3_from_paths(pose_ref, pose_est)
    else:
        r, t, s = _ransac_align_sim3(
            pose_ref,
            pose_est,
            sub_n=sub_n,
            inlier_thresh=inlier_thresh,
            max_iters=ransac_max_iters,
            random_state=random_state,
        )
        pose_est_aligned = _apply_sim3_to_poses(pose_est, r, t, s)

    if return_aligned:
        ext_est_aligned = affine_inverse_np(pose_est_aligned)
        return r, t, s, ext_est_aligned
    return r, t, s


# def align_poses_umeyama(ext_ref: np.ndarray, ext_est: np.ndarray, return_aligned=False):
#     """
#     Align estimated trajectory to reference trajectory using Umeyama Sim(3)
#     alignment (via evo PosePath3D). # noqa
#     Returns rotation, translation, and scale.
#     """
#     # If input extrinsics are 3x4, convert to 4x4 by padding
#     if ext_ref.shape[1] == 3:
#         ext_ref_ = np.eye(4)[None].repeat(len(ext_ref), 0)
#         ext_ref_[:, :3] = ext_ref
#         ext_ref = ext_ref_
#     if ext_est.shape[1] == 3:
#         ext_est_ = np.eye(4)[None].repeat(len(ext_est), 0)
#         ext_est_[:, :3] = ext_est
#         ext_est = ext_est_

#     # Convert to camera poses (inverse extrinsics)
#     pose_ref = affine_inverse_np(ext_ref)
#     pose_est = affine_inverse_np(ext_est)

#     # Create evo PosePath3D objects
#     path_ref = PosePath3D(poses_se3=pose_ref)
#     path_est = PosePath3D(poses_se3=pose_est)
#     r, t, s = path_est.align(path_ref, correct_scale=True)
#     if return_aligned:
#         return r, t, s, affine_inverse_np(np.stack(path_est.poses_se3))
#     else:
#         return r, t, s


def apply_umeyama_alignment_to_ext(
    rot: np.ndarray,  # (3,3)
    trans: np.ndarray,  # (3,) or (1,3)
    scale: float,
    ext_est: np.ndarray,  # (...,4,4) or (...,3,4)
) -> np.ndarray:
    """
    Apply Sim(3) (R, t, s) to a batch of world-to-camera extrinsics ext_est.
    Returns the aligned extrinsics, with the same shape as input.
    """

    # Allow 3x4 extrinsics: pad to 4x4
    if ext_est.shape[-2:] == (3, 4):
        pad = np.zeros((*ext_est.shape[:-2], 4, 4), dtype=ext_est.dtype)
        pad[..., :3, :4] = ext_est
        pad[..., 3, 3] = 1.0
        ext_est = pad

    # Convert world-to-camera to camera-to-world
    pose_est = affine_inverse_np(ext_est)  # (...,4,4)
    R_e = pose_est[..., :3, :3]  # (...,3,3)
    t_e = pose_est[..., :3, 3]  # (...,3)

    # Apply Sim(3) transformation
    R_a = np.einsum("ij,...jk->...ik", rot, R_e)  # (...,3,3)
    t_a = scale * np.einsum("ij,...j->...i", rot, t_e) + trans  # (...,3)

    # Assemble the transformed pose
    pose_a = np.zeros_like(pose_est)
    pose_a[..., :3, :3] = R_a
    pose_a[..., :3, 3] = t_a
    pose_a[..., 3, 3] = 1.0

    # Convert back to world-to-camera
    return affine_inverse_np(pose_a)


def transform_points_sim3(points, rot, trans, scale, inverse=False):
    """
    Sim(3) transform point cloud
    points: (N, 3)
    rot: (3, 3)
    trans: (3,) or (1, 3)
    scale: float
    inverse: Whether to do inverse transform (ref->est)
    Returns: (N, 3)
    """
    if not inverse:
        # Forward: est -> ref
        return scale * (points @ rot.T) + trans
    else:
        # Inverse: ref -> est
        return ((points - trans) @ rot) / scale


def _rand_rot():
    u1, u2, u3 = np.random.rand(3)
    q = np.array(
        [
            np.sqrt(1 - u1) * np.sin(2 * np.math.pi * u2),
            np.sqrt(1 - u1) * np.cos(2 * np.math.pi * u2),
            np.sqrt(u1) * np.sin(2 * np.math.pi * u3),
            np.sqrt(u1) * np.cos(2 * np.math.pi * u3),
        ]
    )
    w, x, y, z = q
    return np.array(
        [
            [1 - 2 * (y * y + z * z), 2 * (x * y - z * w), 2 * (x * z + y * w)],
            [2 * (x * y + z * w), 1 - 2 * (x * x + z * z), 2 * (y * z - x * w)],
            [2 * (x * z - y * w), 2 * (y * z + x * w), 1 - 2 * (x * x + y * y)],
        ]
    )


def _rand_pose():
    R, t = _rand_rot(), np.random.randn(3)
    P = np.eye(4)
    P[:3, :3] = R
    P[:3, 3] = t
    return P


if __name__ == "__main__":
    np.random.seed(42)
    # 1. Randomly generate reference trajectory and Sim(3)
    N = 8
    pose_ref = np.stack([_rand_pose() for _ in range(N)])  # (N,4,4)  cam→world
    rot_gt = _rand_rot()
    scale_gt = 2.3
    trans_gt = np.random.randn(3)
    # 2. Generate estimated trajectory (apply Sim(3))
    pose_est = np.zeros_like(pose_ref)
    for i in range(N):
        R = pose_ref[i][:3, :3]
        t = pose_ref[i][:3, 3]
        pose_est[i][:3, :3] = rot_gt @ R
        pose_est[i][:3, 3] = scale_gt * (rot_gt @ t) + trans_gt
        pose_est[i][3, 3] = 1.0
    # 3. Get extrinsics (world->cam)
    ext_ref = affine_inverse_np(pose_ref)
    ext_est = affine_inverse_np(pose_est)
    # 4. Use umeyama alignment, estimate Sim(3)
    r_est, t_est, s_est = align_poses_umeyama(ext_ref, ext_est)
    print("GT scale:", scale_gt, "Estimated:", s_est)
    print("GT trans:", trans_gt, "Estimated:", t_est)
    print("GT rot:\n", rot_gt, "\nEstimated:\n", r_est)
    # 5. Random point cloud, in ref frame
    num_points = 100
    points_ref = np.random.randn(num_points, 3)
    # 6. Use GT Sim(3) inverse transform to est frame
    points_est = transform_points_sim3(points_ref, rot_gt, trans_gt, scale_gt, inverse=True)
    # 7. Use estimated Sim(3) forward transform back to ref frame
    points_ref_recovered = transform_points_sim3(points_est, r_est, t_est, s_est, inverse=False)
    # 8. Check error
    err = np.abs(points_ref_recovered - points_ref)
    print("Point cloud sim3 transform error (mean abs):", err.mean())
    print("Point cloud sim3 transform error (max abs):", err.max())
    assert err.mean() < 1e-6, "Mean sim3 transform error too large!"
    assert err.max() < 1e-5, "Max sim3 transform error too large!"
    print("Sim(3) point cloud transform & alignment test passed!")



================================================
FILE: src/depth_anything_3/utils/ray_utils.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

import torch
from einops import repeat
from .geometry import unproject_depth


def compute_optimal_rotation_intrinsics_batch(
    rays_origin, rays_target, z_threshold=1e-4, reproj_threshold=0.2, weights=None,
    n_sample = None,
    n_iter=100,
    num_sample_for_ransac=8,
    rand_sample_iters_idx=None,
):
    """
    Args:
        rays_origin (torch.Tensor): (B, N, 3)
        rays_target (torch.Tensor): (B, N, 3)
        z_threshold (float): Threshold for z value to be considered valid.

    Returns:
        R (torch.tensor): (3, 3)
        focal_length (torch.tensor): (2,)
        principal_point (torch.tensor): (2,)
    """
    device = rays_origin.device
    B, N, _ = rays_origin.shape
    z_mask = torch.logical_and(
        torch.abs(rays_target[:, :, 2]) > z_threshold, torch.abs(rays_origin[:, :, 2]) > z_threshold
    ) # (B, N, 1)
    rays_origin = rays_origin.clone()
    rays_target = rays_target.clone()
    rays_origin[:, :, 0][z_mask] /= rays_origin[:, :, 2][z_mask]
    rays_origin[:, :, 1][z_mask] /= rays_origin[:, :, 2][z_mask]
    rays_target[:, :, 0][z_mask] /= rays_target[:, :, 2][z_mask]
    rays_target[:, :, 1][z_mask] /= rays_target[:, :, 2][z_mask]

    rays_origin = rays_origin[:, :, :2]
    rays_target = rays_target[:, :, :2]
    assert weights is not None, "weights must be provided"
    weights[~z_mask] = 0 

    A_list = []
    max_chunk_size = 2
    for i in range(0, rays_origin.shape[0], max_chunk_size):
        A = ransac_find_homography_weighted_fast_batch(
            rays_origin[i:i+max_chunk_size],
            rays_target[i:i+max_chunk_size],
            weights[i:i+max_chunk_size],
            n_iter=n_iter,
            n_sample = n_sample,
            num_sample_for_ransac=num_sample_for_ransac,
            reproj_threshold=reproj_threshold,
            rand_sample_iters_idx=rand_sample_iters_idx,
            max_inlier_num=8000,
        )
        A = A.to(device)
        A_need_inv_mask = torch.linalg.det(A) < 0
        A[A_need_inv_mask] = -A[A_need_inv_mask]
        A_list.append(A)

    A = torch.cat(A_list, dim=0)

    R_list = []
    f_list = []
    pp_list = []
    for i in range(A.shape[0]):
        R, L = ql_decomposition(A[i])
        L = L / L[2][2]

        f = torch.stack((L[0][0], L[1][1]))
        pp = torch.stack((L[2][0], L[2][1]))
        R_list.append(R)
        f_list.append(f)
        pp_list.append(pp)
        
    R = torch.stack(R_list)
    f = torch.stack(f_list)
    pp = torch.stack(pp_list)

    return R, f, pp


# https://www.reddit.com/r/learnmath/comments/v1crd7/linear_algebra_qr_to_ql_decomposition/
def ql_decomposition(A):
    P = torch.tensor([[0, 0, 1], [0, 1, 0], [1, 0, 0]], device=A.device).float()
    A_tilde = torch.matmul(A, P)
    Q_tilde, R_tilde = torch.linalg.qr(A_tilde)
    Q = torch.matmul(Q_tilde, P)
    L = torch.matmul(torch.matmul(P, R_tilde), P)
    d = torch.diag(L)
    Q[:, 0] *= torch.sign(d[0])
    Q[:, 1] *= torch.sign(d[1])
    Q[:, 2] *= torch.sign(d[2])
    L[0] *= torch.sign(d[0])
    L[1] *= torch.sign(d[1])
    L[2] *= torch.sign(d[2])
    return Q, L

def find_homography_least_squares_weighted_torch(src_pts, dst_pts, confident_weight):
    """
    src_pts: (N,2) source points (torch.Tensor, float32/float64)
    dst_pts: (N,2) target points (torch.Tensor, float32/float64)
    confident_weight: (N,) weights (torch.Tensor)
    Returns: (3,3) homography matrix H (torch.Tensor)
    """
    assert src_pts.shape == dst_pts.shape
    N = src_pts.shape[0]
    if N < 4:
        raise ValueError("At least 4 points are required to compute homography.")
    assert confident_weight.shape == (N,)

    w = confident_weight.sqrt().unsqueeze(1)  # (N,1)

    x = src_pts[:, 0:1]  # (N,1)
    y = src_pts[:, 1:2]  # (N,1)
    u = dst_pts[:, 0:1]
    v = dst_pts[:, 1:2]

    zeros = torch.zeros_like(x)

    # Construct A matrix (2N, 9)
    A1 = torch.cat([-x * w, -y * w, -w, zeros, zeros, zeros, x * u * w, y * u * w, u * w], dim=1)
    A2 = torch.cat([zeros, zeros, zeros, -x * w, -y * w, -w, x * v * w, y * v * w, v * w], dim=1)
    A = torch.cat([A1, A2], dim=0)  # (2N, 9)

    # SVD
    # Note: torch.linalg.svd returns U, S, Vh, where Vh is the transpose of V
    _, _, Vh = torch.linalg.svd(A)
    H = Vh[-1].reshape(3, 3)
    H = H / H[-1, -1]
    return H


def ransac_find_homography_weighted(
    src_pts,
    dst_pts,
    confident_weight,
    n_iter=100,
    sample_ratio=0.2,
    reproj_threshold=3.0,
    num_sample_for_ransac=16,
    random_seed=None,
):
    """
    RANSAC version of weighted Homography estimation.
    Sample 4 points from the top 50% weighted points each time.
    reproj_threshold: points with reprojection error less than this value are inliers
    Returns: best_H
    """
    if random_seed is not None:
        torch.manual_seed(random_seed)
    N = src_pts.shape[0]
    assert N >= 4
    # 1. Select top 50% weighted points
    sorted_idx = torch.argsort(confident_weight, descending=True)
    n_sample = max(num_sample_for_ransac, int(N * sample_ratio))
    candidate_idx = sorted_idx[:n_sample]
    best_inlier_mask = None
    best_score = 0
    for _ in range(n_iter):
        # 2. Randomly sample 4 points
        idx = candidate_idx[torch.randperm(n_sample)[:num_sample_for_ransac]]
        # 3. Compute Homography
        try:
            H = find_homography_least_squares_weighted_torch(
                src_pts[idx], dst_pts[idx], confident_weight[idx]
            )
        except Exception:
            H = torch.eye(3, dtype=src_pts.dtype, device=src_pts.device)
        # 4. Compute reprojection error for all points
        src_homo = torch.cat(
            [src_pts, torch.ones(N, 1, dtype=src_pts.dtype, device=src_pts.device)], dim=1
        )
        proj = (H @ src_homo.T).T
        proj = proj[:, :2] / proj[:, 2:3]
        error = ((proj - dst_pts) ** 2).sum(dim=1).sqrt()  # Euclidean distance
        inlier_mask = error < reproj_threshold
        total_score = (inlier_mask * confident_weight).sum().item()
        n_inlier = inlier_mask.sum().item()
        if n_inlier < 4:
            continue  # At least 4 inliers required for fitting

        if total_score > best_score:
            best_score = total_score
            best_inlier_mask = inlier_mask

    # 5. Refit Homography using inliers
    H_inlier = find_homography_least_squares_weighted_torch(
        src_pts[best_inlier_mask], dst_pts[best_inlier_mask], confident_weight[best_inlier_mask]
    )

    return H_inlier


def find_homography_least_squares_weighted_torch_batch(
    src_pts_batch, dst_pts_batch, confident_weight_batch
):
    """
    Batch version of weighted least squares Homography
    src_pts_batch: (B, K, 2)
    dst_pts_batch: (B, K, 2)
    confident_weight_batch: (B, K)
    Returns: (B, 3, 3)
    """
    B, K, _ = src_pts_batch.shape
    w = confident_weight_batch.sqrt().unsqueeze(2)  # (B,K,1)
    x = src_pts_batch[:, :, 0:1]
    y = src_pts_batch[:, :, 1:2]
    u = dst_pts_batch[:, :, 0:1]
    v = dst_pts_batch[:, :, 1:2]
    zeros = torch.zeros_like(x)
    A1 = torch.cat([-x * w, -y * w, -w, zeros, zeros, zeros, x * u * w, y * u * w, u * w], dim=2)
    A2 = torch.cat([zeros, zeros, zeros, -x * w, -y * w, -w, x * v * w, y * v * w, v * w], dim=2)
    A = torch.cat([A1, A2], dim=1)  # (B, 2K, 9)
    # SVD: torch.linalg.svd supports batch
    _, _, Vh = torch.linalg.svd(A)
    H = Vh[:, -1].reshape(B, 3, 3)
    H = H / H[:, 2:3, 2:3]
    return H


def ransac_find_homography_weighted_fast(
    src_pts,
    dst_pts,
    confident_weight,
    n_sample,
    n_iter=100,
    reproj_threshold=3.0,
    num_sample_for_ransac=8,
    random_seed=None,
    rand_sample_iters_idx=None,
):
    """
    Batch version of RANSAC weighted Homography estimation.
    Returns: H_inlier
    """
    if random_seed is not None:
        torch.manual_seed(random_seed)
    N = src_pts.shape[0]
    device = src_pts.device
    assert N >= 4
    # 1. Select top weighted points by sample_ratio
    sorted_idx = torch.argsort(confident_weight, descending=True)
    candidate_idx = sorted_idx[:n_sample]  # (n_sample,)
    if rand_sample_iters_idx is None:
        rand_sample_iters_idx = torch.stack(
            [torch.randperm(n_sample, device=device)[:num_sample_for_ransac] for _ in range(n_iter)],
            dim=0,
        )  # (n_iter, num_sample_for_ransac)
    # 2. Generate all sampling groups at once
    # shape: (n_iter, num_sample_for_ransac)
    rand_idx = candidate_idx[rand_sample_iters_idx]  # (n_iter, num_sample_for_ransac)
    # 3. Construct batch input
    src_pts_batch = src_pts[rand_idx]  # (n_iter, num_sample_for_ransac, 2)
    dst_pts_batch = dst_pts[rand_idx]  # (n_iter, num_sample_for_ransac, 2)
    confident_weight_batch = confident_weight[rand_idx]  # (n_iter, num_sample_for_ransac)
    # 4. Batch fit Homography
    H_batch = find_homography_least_squares_weighted_torch_batch(
        src_pts_batch, dst_pts_batch, confident_weight_batch
    )  # (n_iter, 3, 3)
    # 5. Batch evaluate inliers for all H
    src_homo = torch.cat(
        [src_pts, torch.ones(N, 1, dtype=src_pts.dtype, device=src_pts.device)], dim=1
    )  # (N,3)
    src_homo_expand = src_homo.unsqueeze(0).expand(n_iter, N, 3)  # (n_iter, N, 3)
    dst_pts_expand = dst_pts.unsqueeze(0).expand(n_iter, N, 2)  # (n_iter, N, 2)
    confident_weight_expand = confident_weight.unsqueeze(0).expand(n_iter, N)  # (n_iter, N)
    # H_batch: (n_iter, 3, 3)
    proj = torch.bmm(src_homo_expand, H_batch.transpose(1, 2))  # (n_iter, N, 3)
    proj_xy = proj[:, :, :2] / proj[:, :, 2:3]  # (n_iter, N, 2)
    error = ((proj_xy - dst_pts_expand) ** 2).sum(dim=2).sqrt()  # (n_iter, N)
    inlier_mask = error < reproj_threshold  # (n_iter, N)
    total_score = (inlier_mask * confident_weight_expand).sum(dim=1)  # (n_iter,)
    # 6. Select the sampling group with the highest score
    best_idx = torch.argmax(total_score)
    best_inlier_mask = inlier_mask[best_idx]  # (N,)
    inlier_src_pts = src_pts[best_inlier_mask]
    inlier_dst_pts = dst_pts[best_inlier_mask]
    inlier_confident_weight = confident_weight[best_inlier_mask]

    max_inlier_num = 10000
    sorted_idx = torch.argsort(inlier_confident_weight, descending=True)

    # method 1: sort according to confident_weight, and only keep max_inlier_num pts
    # sorted_idx = sorted_idx[:max_inlier_num]

    # method 2: random choose max_inlier_num pts
    sorted_idx = sorted_idx[torch.randperm(len(sorted_idx))[:max_inlier_num]]

    inlier_src_pts = inlier_src_pts[sorted_idx]
    inlier_dst_pts = inlier_dst_pts[sorted_idx]
    inlier_confident_weight = inlier_confident_weight[sorted_idx]
    # 7. Refit Homography using inliers
    H_inlier = find_homography_least_squares_weighted_torch(
        inlier_src_pts, inlier_dst_pts, inlier_confident_weight
    )
    return H_inlier


def ransac_find_homography_weighted_fast_batch(
    src_pts,  # (B, N, 3)
    dst_pts,  # (B, N, 2)
    confident_weight,  # (B, N)
    n_sample,
    n_iter=100,
    reproj_threshold=3.0,
    num_sample_for_ransac=8,
    max_inlier_num=10000,
    random_seed=None,
    rand_sample_iters_idx=None,
):
    """
    Batch version of RANSAC weighted Homography estimation (supports batch).
    Input:
        src_pts: (B, N, 2)
        dst_pts: (B, N, 2)
        confident_weight: (B, N)
    Returns:
        H_inlier: (B, 3, 3)
    """
    if random_seed is not None:
        torch.manual_seed(random_seed)
    B, N, _ = src_pts.shape
    assert N >= 4

    device = src_pts.device

    # 1. Select top weighted points by sample_ratio
    sorted_idx = torch.argsort(confident_weight, descending=True, dim=1)  # (B, N)
    candidate_idx = sorted_idx[:, :n_sample]  # (B, n_sample)

    # 2. Generate all sampling groups at once
    # rand_idx: (B, n_iter, num_sample_for_ransac)
    if rand_sample_iters_idx is None:
        rand_sample_iters_idx = torch.stack(
            [torch.randperm(n_sample, device=device)[:num_sample_for_ransac] for _ in range(n_iter)],
            dim=0,
        )  # (n_iter, num_sample_for_ransac)
    
    rand_idx = candidate_idx[:, rand_sample_iters_idx]  # (B, n_iter, num_sample_for_ransac)

    # 3. Construct batch input
    # Indexing method below: (B, n_iter, num_sample_for_ransac, ...)
    b_idx = torch.arange(B, device=device).view(B, 1, 1).expand(B, n_iter, num_sample_for_ransac)
    src_pts_batch = src_pts[b_idx, rand_idx]  # (B, n_iter, num_sample_for_ransac, 2)
    dst_pts_batch = dst_pts[b_idx, rand_idx]  # (B, n_iter, num_sample_for_ransac, 2)
    confident_weight_batch = confident_weight[b_idx, rand_idx]  # (B, n_iter, num_sample_for_ransac)

    # 4. Batch fit Homography
    # Need to implement batch version that supports (B, n_iter, num_sample_for_ransac, ...) input
    # Output H_batch: (B, n_iter, 3, 3)
    cB, cN = src_pts_batch.shape[:2]
    H_batch = find_homography_least_squares_weighted_torch_batch(
        src_pts_batch.flatten(0, 1), dst_pts_batch.flatten(0, 1), confident_weight_batch.flatten(0, 1)
    )  # (B, n_iter, 3, 3)
    H_batch = H_batch.unflatten(0, (cB, cN))

    # 5. Batch evaluate inliers for all H
    src_homo = torch.cat(
        [src_pts, torch.ones(B, N, 1, dtype=src_pts.dtype, device=src_pts.device)], dim=2
    )  # (B, N, 3)
    src_homo_expand = src_homo.unsqueeze(1).expand(B, n_iter, N, 3)  # (B, n_iter, N, 3)
    dst_pts_expand = dst_pts.unsqueeze(1).expand(B, n_iter, N, 2)  # (B, n_iter, N, 2)
    confident_weight_expand = confident_weight.unsqueeze(1).expand(B, n_iter, N)  # (B, n_iter, N)

    # H_batch: (B, n_iter, 3, 3)
    # Need to reshape H_batch to (B*n_iter, 3, 3), src_homo_expand to (B*n_iter, N, 3)
    H_batch_flat = H_batch.reshape(-1, 3, 3)
    src_homo_expand_flat = src_homo_expand.reshape(-1, N, 3)
    proj = torch.bmm(src_homo_expand_flat, H_batch_flat.transpose(1, 2))  # (B*n_iter, N, 3)
    proj_xy = proj[:, :, :2] / proj[:, :, 2:3]  # (B*n_iter, N, 2)
    proj_xy = proj_xy.reshape(B, n_iter, N, 2)
    error = ((proj_xy - dst_pts_expand) ** 2).sum(dim=3).sqrt()  # (B, n_iter, N)
    inlier_mask = error < reproj_threshold  # (B, n_iter, N)
    total_score = (inlier_mask * confident_weight_expand).sum(dim=2)  # (B, n_iter)

    # 6. Select the sampling group with the highest score
    best_idx = torch.argmax(total_score, dim=1)  # (B,)
    best_inlier_mask = inlier_mask[torch.arange(B, device=device), best_idx]  # (B, N)

    # 7. Refit Homography using inliers
    H_inlier_list = []
    for b in range(B):
        mask = best_inlier_mask[b]
        inlier_src_pts = src_pts[b][mask]  # (?, 3)
        inlier_dst_pts = dst_pts[b][mask]  # (?, 2)
        inlier_confident_weight = confident_weight[b][mask]  # (?)

        sorted_idx = torch.argsort(inlier_confident_weight, descending=True)
        # # method 1: sort according to confident_weight, and only keep max_inlier_num pts
        # sorted_idx = sorted_idx[:max_inlier_num]
        # method 2: random choose max_inlier_num pts
        if len(sorted_idx) > max_inlier_num:
            # random choose from first 95% confident pts
            keep_len = max(int(len(sorted_idx) * 0.95), max_inlier_num)
            sorted_idx = sorted_idx[:keep_len]
            perm = torch.randperm(len(sorted_idx), device=device)[:max_inlier_num]
            sorted_idx = sorted_idx[perm]
        inlier_src_pts = inlier_src_pts[sorted_idx]
        inlier_dst_pts = inlier_dst_pts[sorted_idx]
        inlier_confident_weight = inlier_confident_weight[sorted_idx]

        H_inlier = find_homography_least_squares_weighted_torch(
            inlier_src_pts, inlier_dst_pts, inlier_confident_weight
        )  # (3, 3)
        H_inlier_list.append(H_inlier)
    H_inlier = torch.stack(H_inlier_list, dim=0)  # (B, 3, 3)
    return H_inlier

def get_params_for_ransac(N, device):
    n_iter=100
    sample_ratio=0.3
    num_sample_for_ransac=8
    n_sample = max(num_sample_for_ransac, int(N * sample_ratio))
    rand_sample_iters_idx = torch.stack(
            [torch.randperm(n_sample, device=device)[:num_sample_for_ransac] for _ in range(n_iter)],
            dim=0,
        )  # (n_iter, num_sample_for_ransac)
    return n_iter, num_sample_for_ransac, n_sample, rand_sample_iters_idx


def camray_to_caminfo(camray, confidence=None, reproj_threshold=0.2, training=False):
    """
    Args:
        camray: (B, S, num_patches_y, num_patches_x, 6)
        confidence: (B, S, num_patches_y, num_patches_x)
    Returns:
        R: (B, S, 3, 3)
        T: (B, S, 3)
        focal_lengths: (B, S, 2)
        principal_points: (B, S, 2)
    """
    if confidence is None:
        confidence = torch.ones_like(camray[:, :, :, :, 0])
    B, S, num_patches_y, num_patches_x, _ = camray.shape
    # identity K, assume imw=imh=2.0
    I_K = torch.eye(3, dtype=camray.dtype, device=camray.device)
    I_K[0, 2] = 1.0
    I_K[1, 2] = 1.0
    # repeat I_K to match camray
    I_K = I_K.unsqueeze(0).unsqueeze(0).expand(B, S, -1, -1)

    cam_plane_depth = torch.ones(
        B, S, num_patches_y, num_patches_x, 1, dtype=camray.dtype, device=camray.device
    )
    I_cam_plane_unproj = unproject_depth(
        cam_plane_depth,
        I_K,
        c2w=None,
        ixt_normalized=True,
        num_patches_x=num_patches_x,
        num_patches_y=num_patches_y,
    )  # (B, S, num_patches_y, num_patches_x, 3)

    camray = camray.flatten(0, 1).flatten(1, 2)  # (B*S, num_patches_y*num_patches_x, 6)
    I_cam_plane_unproj = I_cam_plane_unproj.flatten(0, 1).flatten(
        1, 2
    )  # (B*S, num_patches_y*num_patches_x, 3)
    confidence = confidence.flatten(0, 1).flatten(1, 2)  # (B*S, num_patches_y*num_patches_x)
    
    # Compute optimal rotation to align rays
    N = camray.shape[-2]
    device = camray.device
    n_iter, num_sample_for_ransac, n_sample, rand_sample_iters_idx = get_params_for_ransac(N, device)
    
    # Use batch processing (confidence is guaranteed to be not None at this point)
    if training:
        camray = camray.clone().detach()
        I_cam_plane_unproj = I_cam_plane_unproj.clone().detach()
        confidence = confidence.clone().detach()
    R, focal_lengths, principal_points = compute_optimal_rotation_intrinsics_batch(
        I_cam_plane_unproj,
        camray[:, :, :3],
        reproj_threshold=reproj_threshold,
        weights=confidence,
        n_sample = n_sample,
        n_iter=n_iter,
        num_sample_for_ransac=num_sample_for_ransac,
        rand_sample_iters_idx=rand_sample_iters_idx,
    )

    T = torch.sum(camray[:, :, 3:] * confidence.unsqueeze(-1), dim=1) / torch.sum(
        confidence, dim=-1, keepdim=True
    )

    R = R.reshape(B, S, 3, 3)
    T = T.reshape(B, S, 3)
    focal_lengths = focal_lengths.reshape(B, S, 2)
    principal_points = principal_points.reshape(B, S, 2)

    return R, T, 1.0 / focal_lengths, principal_points + 1.0

def get_extrinsic_from_camray(camray, conf, patch_size_y, patch_size_x, training=False):
    pred_R, pred_T, pred_focal_lengths, pred_principal_points = camray_to_caminfo(
        camray, confidence=conf.squeeze(-1), training=training
    )

    pred_extrinsic = torch.cat(
        [
            torch.cat([pred_R, pred_T.unsqueeze(-1)], dim=-1),
            repeat(
                torch.tensor([0, 0, 0, 1], dtype=pred_R.dtype, device=pred_R.device),
                "c -> b s 1 c",
                b=pred_R.shape[0],
                s=pred_R.shape[1],
            ),
        ],
        dim=-2,
    )  # B, S, 4, 4
    return pred_extrinsic, pred_focal_lengths, pred_principal_points


================================================
FILE: src/depth_anything_3/utils/read_write_model.py
================================================
# Copyright (c), ETH Zurich and UNC Chapel Hill.
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
# All rights reserved.
#
# This file has been modified by ByteDance Ltd. and/or its affiliates. on 11/05/2025
#
# Redistribution and use in source and binary forms, with or without
# modification, are permitted provided that the following conditions are met:
#
#     * Redistributions of source code must retain the above copyright
#       notice, this list of conditions and the following disclaimer.
#
#     * Redistributions in binary form must reproduce the above copyright
#       notice, this list of conditions and the following disclaimer in the
#       documentation and/or other materials provided with the distribution.
#
#     * Neither the name of ETH Zurich and UNC Chapel Hill nor the names of
#       its contributors may be used to endorse or promote products derived
#       from this software without specific prior written permission.
#
# THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
# AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
# IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE
# ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDERS OR CONTRIBUTORS BE
# LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR
# CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF
# SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS
# INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN
# CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE)
# ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE
# POSSIBILITY OF SUCH DAMAGE.


import argparse
import collections
import os
import struct
import numpy as np

CameraModel = collections.namedtuple("CameraModel", ["model_id", "model_name", "num_params"])
Camera = collections.namedtuple("Camera", ["id", "model", "width", "height", "params"])
BaseImage = collections.namedtuple(
    "Image", ["id", "qvec", "tvec", "camera_id", "name", "xys", "point3D_ids"]
)
Point3D = collections.namedtuple(
    "Point3D", ["id", "xyz", "rgb", "error", "image_ids", "point2D_idxs"]
)


class Image(BaseImage):
    def qvec2rotmat(self):
        return qvec2rotmat(self.qvec)


CAMERA_MODELS = {
    CameraModel(model_id=0, model_name="SIMPLE_PINHOLE", num_params=3),
    CameraModel(model_id=1, model_name="PINHOLE", num_params=4),
    CameraModel(model_id=2, model_name="SIMPLE_RADIAL", num_params=4),
    CameraModel(model_id=3, model_name="RADIAL", num_params=5),
    CameraModel(model_id=4, model_name="OPENCV", num_params=8),
    CameraModel(model_id=5, model_name="OPENCV_FISHEYE", num_params=8),
    CameraModel(model_id=6, model_name="FULL_OPENCV", num_params=12),
    CameraModel(model_id=7, model_name="FOV", num_params=5),
    CameraModel(model_id=8, model_name="SIMPLE_RADIAL_FISHEYE", num_params=4),
    CameraModel(model_id=9, model_name="RADIAL_FISHEYE", num_params=5),
    CameraModel(model_id=10, model_name="THIN_PRISM_FISHEYE", num_params=12),
}
CAMERA_MODEL_IDS = {camera_model.model_id: camera_model for camera_model in CAMERA_MODELS}
CAMERA_MODEL_NAMES = {camera_model.model_name: camera_model for camera_model in CAMERA_MODELS}


def read_next_bytes(fid, num_bytes, format_char_sequence, endian_character="<"):
    """Read and unpack the next bytes from a binary file.
    :param fid:
    :param num_bytes: Sum of combination of {2, 4, 8}, e.g. 2, 6, 16, 30, etc.
    :param format_char_sequence: List of {c, e, f, d, h, H, i, I, l, L, q, Q}.
    :param endian_character: Any of {@, =, <, >, !}
    :return: Tuple of read and unpacked values.
    """
    data = fid.read(num_bytes)
    return struct.unpack(endian_character + format_char_sequence, data)


def write_next_bytes(fid, data, format_char_sequence, endian_character="<"):
    """pack and write to a binary file.
    :param fid:
    :param data: data to send, if multiple elements are sent at the same time,
    they should be encapsuled either in a list or a tuple
    :param format_char_sequence: List of {c, e, f, d, h, H, i, I, l, L, q, Q}.
    should be the same length as the data list or tuple
    :param endian_character: Any of {@, =, <, >, !}
    """
    if isinstance(data, (list, tuple)):
        bytes = struct.pack(endian_character + format_char_sequence, *data)
    else:
        bytes = struct.pack(endian_character + format_char_sequence, data)
    fid.write(bytes)


def read_cameras_text(path):
    """
    see: src/colmap/scene/reconstruction.cc
        void Reconstruction::WriteCamerasText(const std::string& path)
        void Reconstruction::ReadCamerasText(const std::string& path)
    """
    cameras = {}
    with open(path) as fid:
        while True:
            line = fid.readline()
            if not line:
                break
            line = line.strip()
            if len(line) > 0 and line[0] != "#":
                elems = line.split()
                camera_id = int(elems[0])
                model = elems[1]
                width = int(elems[2])
                height = int(elems[3])
                params = np.array(tuple(map(float, elems[4:])))
                cameras[camera_id] = Camera(
                    id=camera_id,
                    model=model,
                    width=width,
                    height=height,
                    params=params,
                )
    return cameras


def read_cameras_binary(path_to_model_file):
    """
    see: src/colmap/scene/reconstruction.cc
        void Reconstruction::WriteCamerasBinary(const std::string& path)
        void Reconstruction::ReadCamerasBinary(const std::string& path)
    """
    cameras = {}
    with open(path_to_model_file, "rb") as fid:
        num_cameras = read_next_bytes(fid, 8, "Q")[0]
        for _ in range(num_cameras):
            camera_properties = read_next_bytes(fid, num_bytes=24, format_char_sequence="iiQQ")
            camera_id = camera_properties[0]
            model_id = camera_properties[1]
            model_name = CAMERA_MODEL_IDS[camera_properties[1]].model_name
            width = camera_properties[2]
            height = camera_properties[3]
            num_params = CAMERA_MODEL_IDS[model_id].num_params
            params = read_next_bytes(
                fid,
                num_bytes=8 * num_params,
                format_char_sequence="d" * num_params,
            )
            cameras[camera_id] = Camera(
                id=camera_id,
                model=model_name,
                width=width,
                height=height,
                params=np.array(params),
            )
        assert len(cameras) == num_cameras
    return cameras


def write_cameras_text(cameras, path):
    """
    see: src/colmap/scene/reconstruction.cc
        void Reconstruction::WriteCamerasText(const std::string& path)
        void Reconstruction::ReadCamerasText(const std::string& path)
    """
    HEADER = (
        "# Camera list with one line of data per camera:\n"
        + "#   CAMERA_ID, MODEL, WIDTH, HEIGHT, PARAMS[]\n"
        + f"# Number of cameras: {len(cameras)}\n"
    )
    with open(path, "w") as fid:
        fid.write(HEADER)
        for _, cam in cameras.items():
            to_write = [cam.id, cam.model, cam.width, cam.height, *cam.params]
            line = " ".join([str(elem) for elem in to_write])
            fid.write(line + "\n")


def write_cameras_binary(cameras, path_to_model_file):
    """
    see: src/colmap/scene/reconstruction.cc
        void Reconstruction::WriteCamerasBinary(const std::string& path)
        void Reconstruction::ReadCamerasBinary(const std::string& path)
    """
    with open(path_to_model_file, "wb") as fid:
        write_next_bytes(fid, len(cameras), "Q")
        for _, cam in cameras.items():
            model_id = CAMERA_MODEL_NAMES[cam.model].model_id
            camera_properties = [cam.id, model_id, cam.width, cam.height]
            write_next_bytes(fid, camera_properties, "iiQQ")
            for p in cam.params:
                write_next_bytes(fid, float(p), "d")
    return cameras


def read_images_text(path):
    """
    see: src/colmap/scene/reconstruction.cc
        void Reconstruction::ReadImagesText(const std::string& path)
        void Reconstruction::WriteImagesText(const std::string& path)
    """
    images = {}
    with open(path) as fid:
        while True:
            line = fid.readline()
            if not line:
                break
            line = line.strip()
            if len(line) > 0 and line[0] != "#":
                elems = line.split()
                image_id = int(elems[0])
                qvec = np.array(tuple(map(float, elems[1:5])))
                tvec = np.array(tuple(map(float, elems[5:8])))
                camera_id = int(elems[8])
                image_name = elems[9]
                elems = fid.readline().split()
                xys = np.column_stack(
                    [
                        tuple(map(float, elems[0::3])),
                        tuple(map(float, elems[1::3])),
                    ]
                )
                point3D_ids = np.array(tuple(map(int, elems[2::3])))
                images[image_id] = Image(
                    id=image_id,
                    qvec=qvec,
                    tvec=tvec,
                    camera_id=camera_id,
                    name=image_name,
                    xys=xys,
                    point3D_ids=point3D_ids,
                )
    return images


def read_images_binary(path_to_model_file):
    """
    see: src/colmap/scene/reconstruction.cc
        void Reconstruction::ReadImagesBinary(const std::string& path)
        void Reconstruction::WriteImagesBinary(const std::string& path)
    """
    images = {}
    with open(path_to_model_file, "rb") as fid:
        num_reg_images = read_next_bytes(fid, 8, "Q")[0]
        for _ in range(num_reg_images):
            binary_image_properties = read_next_bytes(
                fid, num_bytes=64, format_char_sequence="idddddddi"
            )
            image_id = binary_image_properties[0]
            qvec = np.array(binary_image_properties[1:5])
            tvec = np.array(binary_image_properties[5:8])
            camera_id = binary_image_properties[8]
            binary_image_name = b""
            current_char = read_next_bytes(fid, 1, "c")[0]
            while current_char != b"\x00":  # look for the ASCII 0 entry
                binary_image_name += current_char
                current_char = read_next_bytes(fid, 1, "c")[0]
            image_name = binary_image_name.decode("utf-8")
            num_points2D = read_next_bytes(fid, num_bytes=8, format_char_sequence="Q")[0]
            x_y_id_s = read_next_bytes(
                fid,
                num_bytes=24 * num_points2D,
                format_char_sequence="ddq" * num_points2D,
            )
            xys = np.column_stack(
                [
                    tuple(map(float, x_y_id_s[0::3])),
                    tuple(map(float, x_y_id_s[1::3])),
                ]
            )
            point3D_ids = np.array(tuple(map(int, x_y_id_s[2::3])))
            images[image_id] = Image(
                id=image_id,
                qvec=qvec,
                tvec=tvec,
                camera_id=camera_id,
                name=image_name,
                xys=xys,
                point3D_ids=point3D_ids,
            )
    return images


def write_images_text(images, path):
    """
    see: src/colmap/scene/reconstruction.cc
        void Reconstruction::ReadImagesText(const std::string& path)
        void Reconstruction::WriteImagesText(const std::string& path)
    """
    if len(images) == 0:
        mean_observations = 0
    else:
        mean_observations = sum((len(img.point3D_ids) for _, img in images.items())) / len(images)
    HEADER = (
        "# Image list with two lines of data per image:\n"
        + "#   IMAGE_ID, QW, QX, QY, QZ, TX, TY, TZ, CAMERA_ID, NAME\n"
        + "#   POINTS2D[] as (X, Y, POINT3D_ID)\n"
        + "# Number of images: {}, mean observations per image: {}\n".format(
            len(images), mean_observations
        )
    )

    with open(path, "w") as fid:
        fid.write(HEADER)
        for _, img in images.items():
            image_header = [
                img.id,
                *img.qvec,
                *img.tvec,
                img.camera_id,
                img.name,
            ]
            first_line = " ".join(map(str, image_header))
            fid.write(first_line + "\n")

            points_strings = []
            for xy, point3D_id in zip(img.xys, img.point3D_ids):
                points_strings.append(" ".join(map(str, [*xy, point3D_id])))
            fid.write(" ".join(points_strings) + "\n")


def write_images_binary(images, path_to_model_file):
    """
    see: src/colmap/scene/reconstruction.cc
        void Reconstruction::ReadImagesBinary(const std::string& path)
        void Reconstruction::WriteImagesBinary(const std::string& path)
    """
    with open(path_to_model_file, "wb") as fid:
        write_next_bytes(fid, len(images), "Q")
        for _, img in images.items():
            write_next_bytes(fid, img.id, "i")
            write_next_bytes(fid, img.qvec.tolist(), "dddd")
            write_next_bytes(fid, img.tvec.tolist(), "ddd")
            write_next_bytes(fid, img.camera_id, "i")
            for char in img.name:
                write_next_bytes(fid, char.encode("utf-8"), "c")
            write_next_bytes(fid, b"\x00", "c")
            write_next_bytes(fid, len(img.point3D_ids), "Q")
            for xy, p3d_id in zip(img.xys, img.point3D_ids):
                write_next_bytes(fid, [*xy, p3d_id], "ddq")


def read_points3D_text(path):
    """
    see: src/colmap/scene/reconstruction.cc
        void Reconstruction::ReadPoints3DText(const std::string& path)
        void Reconstruction::WritePoints3DText(const std::string& path)
    """
    points3D = {}
    with open(path) as fid:
        while True:
            line = fid.readline()
            if not line:
                break
            line = line.strip()
            if len(line) > 0 and line[0] != "#":
                elems = line.split()
                point3D_id = int(elems[0])
                xyz = np.array(tuple(map(float, elems[1:4])))
                rgb = np.array(tuple(map(int, elems[4:7])))
                error = float(elems[7])
                image_ids = np.array(tuple(map(int, elems[8::2])))
                point2D_idxs = np.array(tuple(map(int, elems[9::2])))
                points3D[point3D_id] = Point3D(
                    id=point3D_id,
                    xyz=xyz,
                    rgb=rgb,
                    error=error,
                    image_ids=image_ids,
                    point2D_idxs=point2D_idxs,
                )
    return points3D


def read_points3D_binary(path_to_model_file):
    """
    see: src/colmap/scene/reconstruction.cc
        void Reconstruction::ReadPoints3DBinary(const std::string& path)
        void Reconstruction::WritePoints3DBinary(const std::string& path)
    """
    points3D = {}
    with open(path_to_model_file, "rb") as fid:
        num_points = read_next_bytes(fid, 8, "Q")[0]
        for _ in range(num_points):
            binary_point_line_properties = read_next_bytes(
                fid, num_bytes=43, format_char_sequence="QdddBBBd"
            )
            point3D_id = binary_point_line_properties[0]
            xyz = np.array(binary_point_line_properties[1:4])
            rgb = np.array(binary_point_line_properties[4:7])
            error = np.array(binary_point_line_properties[7])
            track_length = read_next_bytes(fid, num_bytes=8, format_char_sequence="Q")[0]
            track_elems = read_next_bytes(
                fid,
                num_bytes=8 * track_length,
                format_char_sequence="ii" * track_length,
            )
            image_ids = np.array(tuple(map(int, track_elems[0::2])))
            point2D_idxs = np.array(tuple(map(int, track_elems[1::2])))
            points3D[point3D_id] = Point3D(
                id=point3D_id,
                xyz=xyz,
                rgb=rgb,
                error=error,
                image_ids=image_ids,
                point2D_idxs=point2D_idxs,
            )
    return points3D


def write_points3D_text(points3D, path):
    """
    see: src/colmap/scene/reconstruction.cc
        void Reconstruction::ReadPoints3DText(const std::string& path)
        void Reconstruction::WritePoints3DText(const std::string& path)
    """
    if len(points3D) == 0:
        mean_track_length = 0
    else:
        mean_track_length = sum((len(pt.image_ids) for _, pt in points3D.items())) / len(points3D)
    HEADER = (
        "# 3D point list with one line of data per point:\n"
        + "#   POINT3D_ID, X, Y, Z, R, G, B, ERROR, TRACK[] as (IMAGE_ID, POINT2D_IDX)\n"
        + "# Number of points: {}, mean track length: {}\n".format(
            len(points3D), mean_track_length
        )
    )

    with open(path, "w") as fid:
        fid.write(HEADER)
        for _, pt in points3D.items():
            point_header = [pt.id, *pt.xyz, *pt.rgb, pt.error]
            fid.write(" ".join(map(str, point_header)) + " ")
            track_strings = []
            for image_id, point2D in zip(pt.image_ids, pt.point2D_idxs):
                track_strings.append(" ".join(map(str, [image_id, point2D])))
            fid.write(" ".join(track_strings) + "\n")


def write_points3D_binary(points3D, path_to_model_file):
    """
    see: src/colmap/scene/reconstruction.cc
        void Reconstruction::ReadPoints3DBinary(const std::string& path)
        void Reconstruction::WritePoints3DBinary(const std::string& path)
    """
    with open(path_to_model_file, "wb") as fid:
        write_next_bytes(fid, len(points3D), "Q")
        for _, pt in points3D.items():
            write_next_bytes(fid, pt.id, "Q")
            write_next_bytes(fid, pt.xyz.tolist(), "ddd")
            write_next_bytes(fid, pt.rgb.tolist(), "BBB")
            write_next_bytes(fid, pt.error, "d")
            track_length = pt.image_ids.shape[0]
            write_next_bytes(fid, track_length, "Q")
            for image_id, point2D_id in zip(pt.image_ids, pt.point2D_idxs):
                write_next_bytes(fid, [image_id, point2D_id], "ii")


def detect_model_format(path, ext):
    if (
        os.path.isfile(os.path.join(path, "cameras" + ext))
        and os.path.isfile(os.path.join(path, "images" + ext))
        and os.path.isfile(os.path.join(path, "points3D" + ext))
    ):
        print("Detected model format: '" + ext + "'")
        return True

    return False


def read_model(path, ext=""):
    # try to detect the extension automatically
    if ext == "":
        if detect_model_format(path, ".bin"):
            ext = ".bin"
        elif detect_model_format(path, ".txt"):
            ext = ".txt"
        else:
            print("Provide model format: '.bin' or '.txt'")
            return

    if ext == ".txt":
        cameras = read_cameras_text(os.path.join(path, "cameras" + ext))
        images = read_images_text(os.path.join(path, "images" + ext))
        points3D = read_points3D_text(os.path.join(path, "points3D") + ext)
    else:
        cameras = read_cameras_binary(os.path.join(path, "cameras" + ext))
        images = read_images_binary(os.path.join(path, "images" + ext))
        points3D = read_points3D_binary(os.path.join(path, "points3D") + ext)
    return cameras, images, points3D


def write_model(cameras, images, points3D, path, ext=".bin"):
    if ext == ".txt":
        write_cameras_text(cameras, os.path.join(path, "cameras" + ext))
        write_images_text(images, os.path.join(path, "images" + ext))
        write_points3D_text(points3D, os.path.join(path, "points3D") + ext)
    else:
        write_cameras_binary(cameras, os.path.join(path, "cameras" + ext))
        write_images_binary(images, os.path.join(path, "images" + ext))
        write_points3D_binary(points3D, os.path.join(path, "points3D") + ext)
    return cameras, images, points3D


def qvec2rotmat(qvec):
    return np.array(
        [
            [
                1 - 2 * qvec[2] ** 2 - 2 * qvec[3] ** 2,
                2 * qvec[1] * qvec[2] - 2 * qvec[0] * qvec[3],
                2 * qvec[3] * qvec[1] + 2 * qvec[0] * qvec[2],
            ],
            [
                2 * qvec[1] * qvec[2] + 2 * qvec[0] * qvec[3],
                1 - 2 * qvec[1] ** 2 - 2 * qvec[3] ** 2,
                2 * qvec[2] * qvec[3] - 2 * qvec[0] * qvec[1],
            ],
            [
                2 * qvec[3] * qvec[1] - 2 * qvec[0] * qvec[2],
                2 * qvec[2] * qvec[3] + 2 * qvec[0] * qvec[1],
                1 - 2 * qvec[1] ** 2 - 2 * qvec[2] ** 2,
            ],
        ]
    )


def rotmat2qvec(R):
    Rxx, Ryx, Rzx, Rxy, Ryy, Rzy, Rxz, Ryz, Rzz = R.flat
    K = (
        np.array(
            [
                [Rxx - Ryy - Rzz, 0, 0, 0],
                [Ryx + Rxy, Ryy - Rxx - Rzz, 0, 0],
                [Rzx + Rxz, Rzy + Ryz, Rzz - Rxx - Ryy, 0],
                [Ryz - Rzy, Rzx - Rxz, Rxy - Ryx, Rxx + Ryy + Rzz],
            ]
        )
        / 3.0
    )
    eigvals, eigvecs = np.linalg.eigh(K)
    qvec = eigvecs[[3, 0, 1, 2], np.argmax(eigvals)]
    if qvec[0] < 0:
        qvec *= -1
    return qvec


def main():
    parser = argparse.ArgumentParser(description="Read and write COLMAP binary and text models")
    parser.add_argument("--input_model", help="path to input model folder")
    parser.add_argument(
        "--input_format",
        choices=[".bin", ".txt"],
        help="input model format",
        default="",
    )
    parser.add_argument("--output_model", help="path to output model folder")
    parser.add_argument(
        "--output_format",
        choices=[".bin", ".txt"],
        help="output model format",
        default=".txt",
    )
    args = parser.parse_args()

    cameras, images, points3D = read_model(path=args.input_model, ext=args.input_format)

    print("num_cameras:", len(cameras))
    print("num_images:", len(images))
    print("num_points3D:", len(points3D))

    if args.output_model is not None:
        write_model(
            cameras,
            images,
            points3D,
            path=args.output_model,
            ext=args.output_format,
        )


if __name__ == "__main__":
    main()



================================================
FILE: src/depth_anything_3/utils/registry.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

from typing import Any
from addict import Dict


class Registry(Dict[str, Any]):
    def __init__(self):
        super().__init__()
        self._map = Dict({})

    def register(self, name=None):
        def decorator(cls):
            key = name or cls.__name__
            self._map[key] = cls
            return cls

        return decorator

    def get(self, name):
        return self._map[name]

    def all(self):
        return self._map



================================================
FILE: src/depth_anything_3/utils/sh_helpers.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

from math import isqrt
import torch
from einops import einsum

try:
    from e3nn.o3 import matrix_to_angles, wigner_D
except ImportError:
    from depth_anything_3.utils.logger import logger

    logger.warn("Dependency 'e3nn' not found. Required for rotating the camera space SH coeff")


def project_to_so3_strict(M: torch.Tensor) -> torch.Tensor:
    if M.shape[-2:] != (3, 3):
        raise ValueError("Input must be a batch of 3x3 matrices (i.e., shape [..., 3, 3]).")

    # 1. Compute SVD
    U, S, Vh = torch.linalg.svd(M)
    V = Vh.mH

    # 2. Handle reflection case (det = -1)
    det_U = torch.det(U)
    det_V = torch.det(V)
    is_reflection = (det_U * det_V) < 0
    correction_sign = torch.where(
        is_reflection[..., None],
        torch.tensor([1, 1, -1.0], device=M.device, dtype=M.dtype),
        torch.tensor([1, 1, 1.0], device=M.device, dtype=M.dtype),
    )
    correction_matrix = torch.diag_embed(correction_sign)
    U_corrected = U @ correction_matrix
    R_so3_initial = U_corrected @ V.transpose(-2, -1)

    # 3. Explicitly ensure determinant is 1 (or extremely close)
    current_det = torch.det(R_so3_initial)
    det_correction_factor = torch.pow(current_det, -1 / 3)[..., None, None]
    R_so3_final = R_so3_initial * det_correction_factor

    return R_so3_final


def rotate_sh(
    sh_coefficients: torch.Tensor,  # "*#batch n"
    rotations: torch.Tensor,  # "*#batch 3 3"
) -> torch.Tensor:  # "*batch n"
    # https://github.com/graphdeco-inria/gaussian-splatting/issues/176#issuecomment-2452412653
    device = sh_coefficients.device
    dtype = sh_coefficients.dtype

    *_, n = sh_coefficients.shape

    with torch.autocast(device_type=rotations.device.type, enabled=False):
        rotations_float32 = rotations.to(torch.float32)

        # switch axes: yzx -> xyz
        P = torch.tensor([[0, 0, 1], [1, 0, 0], [0, 1, 0]]).unsqueeze(0).to(rotations_float32)
        permuted_rotations = torch.linalg.inv(P) @ rotations_float32 @ P

        # ensure rotation has det == 1 in float32 type
        permuted_rotations_so3 = project_to_so3_strict(permuted_rotations)

        alpha, beta, gamma = matrix_to_angles(permuted_rotations_so3)
        result = []
        for degree in range(isqrt(n)):
            with torch.device(device):
                sh_rotations = wigner_D(degree, alpha, -beta, gamma).type(dtype)
            sh_rotated = einsum(
                sh_rotations,
                sh_coefficients[..., degree**2 : (degree + 1) ** 2],
                "... i j, ... j -> ... i",
            )
            result.append(sh_rotated)

    return torch.cat(result, dim=-1)



================================================
FILE: src/depth_anything_3/utils/visualize.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

import matplotlib
import numpy as np
import torch
from einops import rearrange

from depth_anything_3.utils.logger import logger


def visualize_depth(
    depth: np.ndarray,
    depth_min=None,
    depth_max=None,
    percentile=2,
    ret_minmax=False,
    ret_type=np.uint8,
    cmap="Spectral",
):
    """
    Visualize a depth map using a colormap.

    Args:
        depth: Input depth map array
        depth_min: Minimum depth value for normalization. If None, uses percentile
        depth_max: Maximum depth value for normalization. If None, uses percentile
        percentile: Percentile for min/max computation if not provided
        ret_minmax: Whether to return min/max depth values
        ret_type: Return array type (uint8 or float)
        cmap: Matplotlib colormap name to use

    Returns:
        Colored depth visualization as numpy array
        If ret_minmax=True, also returns depth_min and depth_max
    """
    depth = depth.copy()
    depth.copy()
    valid_mask = depth > 0
    depth[valid_mask] = 1 / depth[valid_mask]
    if depth_min is None:
        if valid_mask.sum() <= 10:
            depth_min = 0
        else:
            depth_min = np.percentile(depth[valid_mask], percentile)
    if depth_max is None:
        if valid_mask.sum() <= 10:
            depth_max = 0
        else:
            depth_max = np.percentile(depth[valid_mask], 100 - percentile)
    if depth_min == depth_max:
        depth_min = depth_min - 1e-6
        depth_max = depth_max + 1e-6
    cm = matplotlib.colormaps[cmap]
    depth = ((depth - depth_min) / (depth_max - depth_min)).clip(0, 1)
    depth = 1 - depth
    img_colored_np = cm(depth[None], bytes=False)[:, :, :, 0:3]  # value from 0 to 1
    if ret_type == np.uint8:
        img_colored_np = (img_colored_np[0] * 255.0).astype(np.uint8)
    elif ret_type == np.float32 or ret_type == np.float64:
        img_colored_np = img_colored_np[0]
    else:
        raise ValueError(f"Invalid return type: {ret_type}")
    if ret_minmax:
        return img_colored_np, depth_min, depth_max
    else:
        return img_colored_np


# GS video rendering visulization function, since it operates in Tensor space...


def vis_depth_map_tensor(
    result: torch.Tensor,  # "*batch height width"
    color_map: str = "Spectral",
) -> torch.Tensor:  # "*batch 3 height with"
    """
    Color-map the depth map.
    """
    far = result.reshape(-1)[:16_000_000].float().quantile(0.99).log().to(result)
    try:
        near = result[result > 0][:16_000_000].float().quantile(0.01).log().to(result)
    except (RuntimeError, ValueError) as e:
        logger.error(f"No valid depth values found. Reason: {e}")
        near = torch.zeros_like(far)
    result = result.log()
    result = (result - near) / (far - near)
    return apply_color_map_to_image(result, color_map)


def apply_color_map(
    x: torch.Tensor,  # " *batch"
    color_map: str = "inferno",
) -> torch.Tensor:  # "*batch 3"
    cmap = matplotlib.cm.get_cmap(color_map)

    # Convert to NumPy so that Matplotlib color maps can be used.
    mapped = cmap(x.float().detach().clip(min=0, max=1).cpu().numpy())[..., :3]

    # Convert back to the original format.
    return torch.tensor(mapped, device=x.device, dtype=torch.float32)


def apply_color_map_to_image(
    image: torch.Tensor,  # "*batch height width"
    color_map: str = "inferno",
) -> torch.Tensor:  # "*batch 3 height with"
    image = apply_color_map(image, color_map)
    return rearrange(image, "... h w c -> ... c h w")



================================================
FILE: src/depth_anything_3/utils/export/__init__.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

from depth_anything_3.specs import Prediction
from depth_anything_3.utils.export.gs import export_to_gs_ply, export_to_gs_video

from .colmap import export_to_colmap
from .depth_vis import export_to_depth_vis
from .feat_vis import export_to_feat_vis
from .glb import export_to_glb
from .npz import export_to_mini_npz, export_to_npz


def export(
    prediction: Prediction,
    export_format: str,
    export_dir: str,
    **kwargs,
):
    if "-" in export_format:
        export_formats = export_format.split("-")
        for export_format in export_formats:
            export(prediction, export_format, export_dir, **kwargs)
        return  # Prevent falling through to single-format handling

    if export_format == "glb":
        export_to_glb(prediction, export_dir, **kwargs.get(export_format, {}))
    elif export_format == "mini_npz":
        export_to_mini_npz(prediction, export_dir)
    elif export_format == "npz":
        export_to_npz(prediction, export_dir)
    elif export_format == "feat_vis":
        export_to_feat_vis(prediction, export_dir, **kwargs.get(export_format, {}))
    elif export_format == "depth_vis":
        export_to_depth_vis(prediction, export_dir)
    elif export_format == "gs_ply":
        export_to_gs_ply(prediction, export_dir, **kwargs.get(export_format, {}))
    elif export_format == "gs_video":
        export_to_gs_video(prediction, export_dir, **kwargs.get(export_format, {}))
    elif export_format == "colmap":
        export_to_colmap(prediction, export_dir, **kwargs.get(export_format, {}))
    else:
        raise ValueError(f"Unsupported export format: {export_format}")


__all__ = [
    export,
]



================================================
FILE: src/depth_anything_3/utils/export/colmap.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

import os
import pycolmap
import cv2 as cv
import numpy as np

from PIL import Image

from depth_anything_3.specs import Prediction
from depth_anything_3.utils.logger import logger

from .glb import _depths_to_world_points_with_colors


def export_to_colmap(
    prediction: Prediction,
    export_dir: str,
    image_paths: list[str],
    conf_thresh_percentile: float = 40.0,
    process_res_method: str = "upper_bound_resize",
) -> None:
    # 1. Data preparation
    conf_thresh = np.percentile(prediction.conf, conf_thresh_percentile)
    points, colors = _depths_to_world_points_with_colors(
        prediction.depth,
        prediction.intrinsics,
        prediction.extrinsics,  # w2c
        prediction.processed_images,
        prediction.conf,
        conf_thresh,
    )
    num_points = len(points)
    logger.info(f"Exporting to COLMAP with {num_points} points")
    num_frames = len(prediction.processed_images)
    h, w = prediction.processed_images.shape[1:3]
    points_xyf = _create_xyf(num_frames, h, w)
    points_xyf = points_xyf[prediction.conf >= conf_thresh]

    # 2. Set Reconstruction
    reconstruction = pycolmap.Reconstruction()

    point3d_ids = []
    for vidx in range(num_points):
        point3d_id = reconstruction.add_point3D(points[vidx], pycolmap.Track(), colors[vidx])
        point3d_ids.append(point3d_id)

    for fidx in range(num_frames):
        orig_w, orig_h = Image.open(image_paths[fidx]).size

        intrinsic = prediction.intrinsics[fidx]
        if process_res_method.endswith("resize"):
            intrinsic[:1] *= orig_w / w
            intrinsic[1:2] *= orig_h / h
        elif process_res_method == "crop":
            raise NotImplementedError("COLMAP export for crop method is not implemented")
        else:
            raise ValueError(f"Unknown process_res_method: {process_res_method}")

        pycolmap_intri = np.array(
            [intrinsic[0, 0], intrinsic[1, 1], intrinsic[0, 2], intrinsic[1, 2]]
        )

        extrinsic = prediction.extrinsics[fidx]
        cam_from_world = pycolmap.Rigid3d(pycolmap.Rotation3d(extrinsic[:3, :3]), extrinsic[:3, 3])

        # set and add camera
        camera = pycolmap.Camera()
        camera.camera_id = fidx + 1
        camera.model = pycolmap.CameraModelId.PINHOLE
        camera.width = orig_w
        camera.height = orig_h
        camera.params = pycolmap_intri
        reconstruction.add_camera(camera)

        # set and add rig (from camera)
        rig = pycolmap.Rig()
        rig.rig_id = camera.camera_id
        rig.add_ref_sensor(camera.sensor_id)
        reconstruction.add_rig(rig)

        # set image
        image = pycolmap.Image()
        image.image_id = fidx + 1
        image.camera_id = camera.camera_id

        # set and add frame (from image)
        frame = pycolmap.Frame()
        frame.frame_id = image.image_id
        frame.rig_id = camera.camera_id
        frame.add_data_id(image.data_id)
        frame.rig_from_world = cam_from_world
        reconstruction.add_frame(frame)

        # set point2d and update track
        point2d_list = []
        points_in_frame = points_xyf[:, 2].astype(np.int32) == fidx
        for vidx in np.where(points_in_frame)[0]:
            point2d = points_xyf[vidx][:2]
            point2d[0] *= orig_w / w
            point2d[1] *= orig_h / h
            point3d_id = point3d_ids[vidx]
            point2d_list.append(pycolmap.Point2D(point2d, point3d_id))
            reconstruction.point3D(point3d_id).track.add_element(
                image.image_id, len(point2d_list) - 1
            )

        # set and add image
        image.frame_id = image.image_id
        image.name = os.path.basename(image_paths[fidx])
        image.points2D = pycolmap.Point2DList(point2d_list)
        reconstruction.add_image(image)

    # 3. Export
    reconstruction.write(export_dir)


def _create_xyf(num_frames, height, width):
    """
    Creates a grid of pixel coordinates and frame indices (fidx) for all frames.
    """
    # Create coordinate grids for a single frame
    y_grid, x_grid = np.indices((height, width), dtype=np.int32)
    x_grid = x_grid[np.newaxis, :, :]
    y_grid = y_grid[np.newaxis, :, :]

    # Broadcast to all frames
    x_coords = np.broadcast_to(x_grid, (num_frames, height, width))
    y_coords = np.broadcast_to(y_grid, (num_frames, height, width))

    # Create frame indices and broadcast
    f_idx = np.arange(num_frames, dtype=np.int32)[:, np.newaxis, np.newaxis]
    f_coords = np.broadcast_to(f_idx, (num_frames, height, width))

    # Stack coordinates and frame indices
    points_xyf = np.stack((x_coords, y_coords, f_coords), axis=-1)

    return points_xyf



================================================
FILE: src/depth_anything_3/utils/export/depth_vis.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

import os
import imageio
import numpy as np

from depth_anything_3.specs import Prediction
from depth_anything_3.utils.visualize import visualize_depth


def export_to_depth_vis(
    prediction: Prediction,
    export_dir: str,
):
    # Use prediction.processed_images, which is already processed image data
    if prediction.processed_images is None:
        raise ValueError("prediction.processed_images is required but not available")

    images_u8 = prediction.processed_images  # (N,H,W,3) uint8

    os.makedirs(os.path.join(export_dir, "depth_vis"), exist_ok=True)
    for idx in range(prediction.depth.shape[0]):
        depth_vis = visualize_depth(prediction.depth[idx])
        image_vis = images_u8[idx]
        depth_vis = depth_vis.astype(np.uint8)
        image_vis = image_vis.astype(np.uint8)
        vis_image = np.concatenate([image_vis, depth_vis], axis=1)
        save_path = os.path.join(export_dir, f"depth_vis/{idx:04d}.jpg")
        imageio.imwrite(save_path, vis_image, quality=95)



================================================
FILE: src/depth_anything_3/utils/export/feat_vis.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

import os
import cv2
import imageio
import numpy as np
from tqdm.auto import tqdm

from depth_anything_3.utils.parallel_utils import async_call
from depth_anything_3.utils.pca_utils import PCARGBVisualizer


@async_call
def export_to_feat_vis(
    prediction,
    export_dir,
    fps=15,
):
    """Export feature visualization with PCA.

    Args:
        prediction: Model prediction containing feature maps
        export_dir: Directory to export results
        fps: Frame rate for output video (default: 15)
    """
    out_dir = os.path.join(export_dir, "feat_vis")
    os.makedirs(out_dir, exist_ok=True)

    images = prediction.processed_images
    for k, v in prediction.aux.items():
        if not k.startswith("feat_layer_"):
            continue
        os.makedirs(os.path.join(out_dir, k), exist_ok=True)
        viz = PCARGBVisualizer(basis_mode="fixed", percentile_mode="global", clip_percent=10.0)
        viz.fit_reference(v)
        feats_vis = viz.transform_video(v)
        for idx in tqdm(range(len(feats_vis))):
            img = images[idx]
            feat_vis = (feats_vis[idx] * 255).astype(np.uint8)
            feat_vis = cv2.resize(
                feat_vis, (img.shape[1], img.shape[0]), interpolation=cv2.INTER_NEAREST
            )
            save_path = os.path.join(out_dir, f"{k}/{idx:06d}.jpg")
            save = np.concatenate([img, feat_vis], axis=1)
            imageio.imwrite(save_path, save, quality=95)
        cmd = (
            "ffmpeg -loglevel error -hide_banner -y "
            f"-framerate {fps} -start_number 0 "
            f"-i {out_dir}/{k}/%06d.jpg "
            f"-c:v libx264 -pix_fmt yuv420p "
            f"{out_dir}/{k}.mp4"
        )
        os.system(cmd)



================================================
FILE: src/depth_anything_3/utils/export/glb.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

from __future__ import annotations

import os
import numpy as np
import trimesh

from depth_anything_3.specs import Prediction
from depth_anything_3.utils.logger import logger

from .depth_vis import export_to_depth_vis


def set_sky_depth(prediction: Prediction, sky_mask: np.ndarray, sky_depth_def: float = 98.0):
    non_sky_mask = ~sky_mask
    valid_depth = prediction.depth[non_sky_mask]
    if valid_depth.size > 0:
        max_depth = np.percentile(valid_depth, sky_depth_def)
        prediction.depth[sky_mask] = max_depth


def get_conf_thresh(
    prediction: Prediction,
    sky_mask: np.ndarray,
    conf_thresh: float,
    conf_thresh_percentile: float = 10.0,
    ensure_thresh_percentile: float = 90.0,
):
    if sky_mask is not None and (~sky_mask).sum() > 10:
        conf_pixels = prediction.conf[~sky_mask]
    else:
        conf_pixels = prediction.conf
    lower = np.percentile(conf_pixels, conf_thresh_percentile)
    upper = np.percentile(conf_pixels, ensure_thresh_percentile)
    conf_thresh = min(max(conf_thresh, lower), upper)
    return conf_thresh


def export_to_glb(
    prediction: Prediction,
    export_dir: str,
    num_max_points: int = 1_000_000,
    conf_thresh: float = 1.05,
    filter_black_bg: bool = False,
    filter_white_bg: bool = False,
    conf_thresh_percentile: float = 40.0,
    ensure_thresh_percentile: float = 90.0,
    sky_depth_def: float = 98.0,
    show_cameras: bool = True,
    camera_size: float = 0.03,
    export_depth_vis: bool = True,
) -> str:
    """Generate a 3D point cloud and camera wireframes and export them as a ``.glb`` file.

    The function builds a point cloud from the predicted depth maps, aligns it to the
    first camera in glTF coordinates (X-right, Y-up, Z-backward), optionally draws
    camera wireframes, and writes the result to ``scene.glb``. Auxiliary assets such as
    depth visualizations can also be generated alongside the main export.

    Args:
        prediction: Model prediction containing depth, confidence, intrinsics, extrinsics,
            and pre-processed images.
        export_dir: Output directory where the glTF assets will be written.
        num_max_points: Maximum number of points retained after downsampling.
        conf_thresh: Base confidence threshold used before percentile adjustments.
        filter_black_bg: Mark near-black background pixels for removal during confidence filtering.
        filter_white_bg: Mark near-white background pixels for removal during confidence filtering.
        conf_thresh_percentile: Lower percentile used when adapting the confidence threshold.
        ensure_thresh_percentile: Upper percentile clamp for the adaptive threshold.
        sky_depth_def: Percentile used to fill sky pixels with plausible depth values.
        show_cameras: Whether to render camera wireframes in the exported scene.
        camera_size: Relative camera wireframe scale as a fraction of the scene diagonal.
        export_depth_vis: Whether to export raster depth visualisations alongside the glTF.

    Returns:
        Path to the exported ``scene.glb`` file.
    """
    # 1) Use prediction.processed_images, which is already processed image data
    assert (
        prediction.processed_images is not None
    ), "Export to GLB: prediction.processed_images is required but not available"
    assert (
        prediction.depth is not None
    ), "Export to GLB: prediction.depth is required but not available"
    assert (
        prediction.intrinsics is not None
    ), "Export to GLB: prediction.intrinsics is required but not available"
    assert (
        prediction.extrinsics is not None
    ), "Export to GLB: prediction.extrinsics is required but not available"
    assert (
        prediction.conf is not None
    ), "Export to GLB: prediction.conf is required but not available"
    logger.info(f"conf_thresh_percentile: {conf_thresh_percentile}")
    logger.info(f"num max points: {num_max_points}")
    logger.info(f"Exporting to GLB with num_max_points: {num_max_points}")
    if prediction.processed_images is None:
        raise ValueError("prediction.processed_images is required but not available")

    images_u8 = prediction.processed_images  # (N,H,W,3) uint8

    # 2) Sky processing (if sky_mask is provided)
    if getattr(prediction, "sky_mask", None) is not None:
        set_sky_depth(prediction, prediction.sky_mask, sky_depth_def)

    # 3) Confidence threshold (if no conf, then no filtering)
    if filter_black_bg:
        prediction.conf[(prediction.processed_images < 16).all(axis=-1)] = 1.0
    if filter_white_bg:
        prediction.conf[(prediction.processed_images >= 240).all(axis=-1)] = 1.0
    conf_thr = get_conf_thresh(
        prediction,
        getattr(prediction, "sky_mask", None),
        conf_thresh,
        conf_thresh_percentile,
        ensure_thresh_percentile,
    )

    # 4) Back-project to world coordinates and get colors (world frame)
    points, colors = _depths_to_world_points_with_colors(
        prediction.depth,
        prediction.intrinsics,
        prediction.extrinsics,  # w2c
        images_u8,
        prediction.conf,
        conf_thr,
    )

    # 5) Based on first camera orientation + glTF axis system, center by point cloud,
    # construct alignment transform, and apply to point cloud
    A = _compute_alignment_transform_first_cam_glTF_center_by_points(
        prediction.extrinsics[0], points
    )  # (4,4)

    if points.shape[0] > 0:
        points = trimesh.transform_points(points, A)

    # 6) Clean + downsample
    points, colors = _filter_and_downsample(points, colors, num_max_points)

    # 7) Assemble scene (add point cloud first)
    scene = trimesh.Scene()
    if scene.metadata is None:
        scene.metadata = {}
    scene.metadata["hf_alignment"] = A  # For camera wireframes and external reuse

    if points.shape[0] > 0:
        pc = trimesh.points.PointCloud(vertices=points, colors=colors)
        scene.add_geometry(pc)

    # 8) Draw cameras (wireframe pyramids), using the same transform A
    if show_cameras and prediction.intrinsics is not None and prediction.extrinsics is not None:
        scene_scale = _estimate_scene_scale(points, fallback=1.0)
        H, W = prediction.depth.shape[1:]
        _add_cameras_to_scene(
            scene=scene,
            K=prediction.intrinsics,
            ext_w2c=prediction.extrinsics,
            image_sizes=[(H, W)] * prediction.depth.shape[0],
            scale=scene_scale * camera_size,
        )

    # 9) Export
    os.makedirs(export_dir, exist_ok=True)
    out_path = os.path.join(export_dir, "scene.glb")
    scene.export(out_path)

    if export_depth_vis:
        export_to_depth_vis(prediction, export_dir)
        os.system(f"cp -r {export_dir}/depth_vis/0000.jpg {export_dir}/scene.jpg")
    return out_path


# =========================
# utilities
# =========================


def _as_homogeneous44(ext: np.ndarray) -> np.ndarray:
    """
    Accept (4,4) or (3,4) extrinsic parameters, return (4,4) homogeneous matrix.
    """
    if ext.shape == (4, 4):
        return ext
    if ext.shape == (3, 4):
        H = np.eye(4, dtype=ext.dtype)
        H[:3, :4] = ext
        return H
    raise ValueError(f"extrinsic must be (4,4) or (3,4), got {ext.shape}")


def _depths_to_world_points_with_colors(
    depth: np.ndarray,
    K: np.ndarray,
    ext_w2c: np.ndarray,
    images_u8: np.ndarray,
    conf: np.ndarray | None,
    conf_thr: float,
) -> tuple[np.ndarray, np.ndarray]:
    """
    For each frame, transform (u,v,1) through K^{-1} to get rays,
    multiply by depth to camera frame, then use (w2c)^{-1} to transform to world frame.
    Simultaneously extract colors.
    """
    N, H, W = depth.shape
    us, vs = np.meshgrid(np.arange(W), np.arange(H))
    ones = np.ones_like(us)
    pix = np.stack([us, vs, ones], axis=-1).reshape(-1, 3)  # (H*W,3)

    pts_all, col_all = [], []

    for i in range(N):
        d = depth[i]  # (H,W)
        valid = np.isfinite(d) & (d > 0)
        if conf is not None:
            valid &= conf[i] >= conf_thr
        if not np.any(valid):
            continue

        d_flat = d.reshape(-1)
        vidx = np.flatnonzero(valid.reshape(-1))

        K_inv = np.linalg.inv(K[i])  # (3,3)
        c2w = np.linalg.inv(_as_homogeneous44(ext_w2c[i]))  # (4,4)

        rays = K_inv @ pix[vidx].T  # (3,M)
        Xc = rays * d_flat[vidx][None, :]  # (3,M)
        Xc_h = np.vstack([Xc, np.ones((1, Xc.shape[1]))])
        Xw = (c2w @ Xc_h)[:3].T.astype(np.float32)  # (M,3)

        cols = images_u8[i].reshape(-1, 3)[vidx].astype(np.uint8)  # (M,3)

        pts_all.append(Xw)
        col_all.append(cols)

    if len(pts_all) == 0:
        return np.zeros((0, 3), dtype=np.float32), np.zeros((0, 3), dtype=np.uint8)

    return np.concatenate(pts_all, 0), np.concatenate(col_all, 0)


def _filter_and_downsample(points: np.ndarray, colors: np.ndarray, num_max: int):
    if points.shape[0] == 0:
        return points, colors
    finite = np.isfinite(points).all(axis=1)
    points, colors = points[finite], colors[finite]
    if points.shape[0] > num_max:
        idx = np.random.choice(points.shape[0], num_max, replace=False)
        points, colors = points[idx], colors[idx]
    return points, colors


def _estimate_scene_scale(points: np.ndarray, fallback: float = 1.0) -> float:
    if points.shape[0] < 2:
        return fallback
    lo = np.percentile(points, 5, axis=0)
    hi = np.percentile(points, 95, axis=0)
    diag = np.linalg.norm(hi - lo)
    return float(diag if np.isfinite(diag) and diag > 0 else fallback)


def _compute_alignment_transform_first_cam_glTF_center_by_points(
    ext_w2c0: np.ndarray,
    points_world: np.ndarray,
) -> np.ndarray:
    """Computes the transformation matrix to align the scene with glTF standards.

    This function calculates a 4x4 homogeneous matrix that centers the scene's
    point cloud and transforms its coordinate system from the computer vision (CV)
    standard to the glTF standard.

    The transformation process involves three main steps:
    1.  **Initial Alignment**: Orients the world coordinate system to match the
        first camera's view (x-right, y-down, z-forward).
    2.  **Coordinate System Conversion**: Converts the CV camera frame to the
        glTF frame (x-right, y-up, z-backward) by flipping the Y and Z axes.
    3.  **Centering**: Translates the entire scene so that the median of the
        point cloud becomes the new origin (0,0,0).

    Returns:
        A 4x4 homogeneous transformation matrix (torch.Tensor or np.ndarray)
        that applies these transformations.  A: X' = A @ [X;1]
    """

    w2c0 = _as_homogeneous44(ext_w2c0).astype(np.float64)

    # CV -> glTF axis transformation
    M = np.eye(4, dtype=np.float64)
    M[1, 1] = -1.0  # flip Y
    M[2, 2] = -1.0  # flip Z

    # Don't center first
    A_no_center = M @ w2c0

    # Calculate point cloud center in new coordinate system (use median to resist outliers)
    if points_world.shape[0] > 0:
        pts_tmp = trimesh.transform_points(points_world, A_no_center)
        center = np.median(pts_tmp, axis=0)
    else:
        center = np.zeros(3, dtype=np.float64)

    T_center = np.eye(4, dtype=np.float64)
    T_center[:3, 3] = -center

    A = T_center @ A_no_center
    return A


def _add_cameras_to_scene(
    scene: trimesh.Scene,
    K: np.ndarray,
    ext_w2c: np.ndarray,
    image_sizes: list[tuple[int, int]],
    scale: float,
) -> None:
    """Draws camera frustums to visualize their position and orientation.

    This function renders each camera as a wireframe pyramid, originating from
    the camera's center and extending to the corners of its imaging plane.

    It reads the 'hf_alignment' metadata from the scene to ensure the
    wireframes are correctly aligned with the 3D point cloud.
    """
    N = K.shape[0]
    if N == 0:
        return

    # Alignment matrix consistent with point cloud (use identity matrix if missing)
    A = None
    try:
        A = scene.metadata.get("hf_alignment", None) if scene.metadata else None
    except Exception:
        A = None
    if A is None:
        A = np.eye(4, dtype=np.float64)

    for i in range(N):
        H, W = image_sizes[i]
        segs = _camera_frustum_lines(K[i], ext_w2c[i], W, H, scale)  # (8,2,3) world frame
        # Apply unified transformation
        segs = trimesh.transform_points(segs.reshape(-1, 3), A).reshape(-1, 2, 3)
        path = trimesh.load_path(segs)
        color = _index_color_rgb(i, N)
        if hasattr(path, "colors"):
            path.colors = np.tile(color, (len(path.entities), 1))
        scene.add_geometry(path)


def _camera_frustum_lines(
    K: np.ndarray, ext_w2c: np.ndarray, W: int, H: int, scale: float
) -> np.ndarray:
    corners = np.array(
        [
            [0, 0, 1.0],
            [W - 1, 0, 1.0],
            [W - 1, H - 1, 1.0],
            [0, H - 1, 1.0],
        ],
        dtype=float,
    )  # (4,3)

    K_inv = np.linalg.inv(K)
    c2w = np.linalg.inv(_as_homogeneous44(ext_w2c))

    # camera center in world
    Cw = (c2w @ np.array([0, 0, 0, 1.0]))[:3]

    # rays -> z=1 plane points (camera frame)
    rays = (K_inv @ corners.T).T
    z = rays[:, 2:3]
    z[z == 0] = 1.0
    plane_cam = (rays / z) * scale  # (4,3)

    # to world
    plane_w = []
    for p in plane_cam:
        pw = (c2w @ np.array([p[0], p[1], p[2], 1.0]))[:3]
        plane_w.append(pw)
    plane_w = np.stack(plane_w, 0)  # (4,3)

    segs = []
    # center to corners
    for k in range(4):
        segs.append(np.stack([Cw, plane_w[k]], 0))
    # rectangle edges
    order = [0, 1, 2, 3, 0]
    for a, b in zip(order[:-1], order[1:]):
        segs.append(np.stack([plane_w[a], plane_w[b]], 0))

    return np.stack(segs, 0)  # (8,2,3)


def _index_color_rgb(i: int, n: int) -> np.ndarray:
    h = (i + 0.5) / max(n, 1)
    s, v = 0.85, 0.95
    r, g, b = _hsv_to_rgb(h, s, v)
    return (np.array([r, g, b]) * 255).astype(np.uint8)


def _hsv_to_rgb(h: float, s: float, v: float) -> tuple[float, float, float]:
    i = int(h * 6.0)
    f = h * 6.0 - i
    p = v * (1.0 - s)
    q = v * (1.0 - f * s)
    t = v * (1.0 - (1.0 - f) * s)
    i = i % 6
    if i == 0:
        r, g, b = v, t, p
    elif i == 1:
        r, g, b = q, v, p
    elif i == 2:
        r, g, b = p, v, t
    elif i == 3:
        r, g, b = p, q, v
    elif i == 4:
        r, g, b = t, p, v
    else:
        r, g, b = v, p, q
    return r, g, b



================================================
FILE: src/depth_anything_3/utils/export/gs.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

import os
from typing import Literal, Optional
import moviepy.editor as mpy
import torch

from depth_anything_3.model.utils.gs_renderer import run_renderer_in_chunk_w_trj_mode
from depth_anything_3.specs import Prediction
from depth_anything_3.utils.gsply_helpers import save_gaussian_ply
from depth_anything_3.utils.layout_helpers import hcat, vcat
from depth_anything_3.utils.visualize import vis_depth_map_tensor

VIDEO_QUALITY_MAP = {
    "low": {"crf": "28", "preset": "veryfast"},
    "medium": {"crf": "23", "preset": "medium"},
    "high": {"crf": "18", "preset": "slow"},
}


def export_to_gs_ply(
    prediction: Prediction,
    export_dir: str,
    gs_views_interval: Optional[
        int
    ] = 1,  # export GS every N views, useful for extremely dense inputs
):
    gs_world = prediction.gaussians
    pred_depth = torch.from_numpy(prediction.depth).unsqueeze(-1).to(gs_world.means)  # v h w 1
    idx = 0
    os.makedirs(os.path.join(export_dir, "gs_ply"), exist_ok=True)
    save_path = os.path.join(export_dir, f"gs_ply/{idx:04d}.ply")
    if gs_views_interval is None:  # select around 12 views in total
        gs_views_interval = max(pred_depth.shape[0] // 12, 1)
    save_gaussian_ply(
        gaussians=gs_world,
        save_path=save_path,
        ctx_depth=pred_depth,
        shift_and_scale=False,
        save_sh_dc_only=True,
        gs_views_interval=gs_views_interval,
        inv_opacity=True,
        prune_by_depth_percent=0.9,
        prune_border_gs=True,
        match_3dgs_mcmc_dev=False,
    )


def export_to_gs_video(
    prediction: Prediction,
    export_dir: str,
    extrinsics: Optional[torch.Tensor] = None,  # render views' world2cam, "b v 4 4"
    intrinsics: Optional[torch.Tensor] = None,  # render views' unnormed intrinsics, "b v 3 3"
    out_image_hw: Optional[tuple[int, int]] = None,  # render views' resolution, (h, w)
    chunk_size: Optional[int] = 4,
    trj_mode: Literal[
        "original",
        "smooth",
        "interpolate",
        "interpolate_smooth",
        "wander",
        "dolly_zoom",
        "extend",
        "wobble_inter",
    ] = "extend",
    color_mode: Literal["RGB+D", "RGB+ED"] = "RGB+ED",
    vis_depth: Optional[Literal["hcat", "vcat"]] = "hcat",
    enable_tqdm: Optional[bool] = True,
    output_name: Optional[str] = None,
    video_quality: Literal["low", "medium", "high"] = "high",
) -> None:
    gs_world = prediction.gaussians
    # if target poses are not provided, render the (smooth/interpolate) input poses
    if extrinsics is not None:
        tgt_extrs = extrinsics
    else:
        tgt_extrs = torch.from_numpy(prediction.extrinsics).unsqueeze(0).to(gs_world.means)
        if prediction.is_metric:
            scale_factor = prediction.scale_factor
            if scale_factor is not None:
                tgt_extrs[:, :, :3, 3] /= scale_factor
    tgt_intrs = (
        intrinsics
        if intrinsics is not None
        else torch.from_numpy(prediction.intrinsics).unsqueeze(0).to(gs_world.means)
    )
    # if render resolution is not provided, render the input ones
    if out_image_hw is not None:
        H, W = out_image_hw
    else:
        H, W = prediction.depth.shape[-2:]
    # if single views, render wander trj
    if tgt_extrs.shape[1] <= 1:
        trj_mode = "wander"
        # trj_mode = "dolly_zoom"

    color, depth = run_renderer_in_chunk_w_trj_mode(
        gaussians=gs_world,
        extrinsics=tgt_extrs,
        intrinsics=tgt_intrs,
        image_shape=(H, W),
        chunk_size=chunk_size,
        trj_mode=trj_mode,
        use_sh=True,
        color_mode=color_mode,
        enable_tqdm=enable_tqdm,
    )

    # save as video
    ffmpeg_params = [
        "-crf",
        VIDEO_QUALITY_MAP[video_quality]["crf"],
        "-preset",
        VIDEO_QUALITY_MAP[video_quality]["preset"],
        "-pix_fmt",
        "yuv420p",
    ]  # best compatibility

    os.makedirs(os.path.join(export_dir, "gs_video"), exist_ok=True)
    for idx in range(color.shape[0]):
        video_i = color[idx]
        if vis_depth is not None:
            depth_i = vis_depth_map_tensor(depth[0])
            cat_fn = hcat if vis_depth == "hcat" else vcat
            video_i = torch.stack([cat_fn(c, d) for c, d in zip(video_i, depth_i)])
        frames = list(
            (video_i.clamp(0, 1) * 255).byte().permute(0, 2, 3, 1).cpu().numpy()
        )  # T x H x W x C, uint8, numpy()

        fps = 24
        clip = mpy.ImageSequenceClip(frames, fps=fps)
        output_name = f"{idx:04d}_{trj_mode}" if output_name is None else output_name
        save_path = os.path.join(export_dir, f"gs_video/{output_name}.mp4")
        # clip.write_videofile(save_path, codec="libx264", audio=False, bitrate="4000k")
        clip.write_videofile(
            save_path,
            codec="libx264",
            audio=False,
            fps=fps,
            ffmpeg_params=ffmpeg_params,
        )
    return



================================================
FILE: src/depth_anything_3/utils/export/npz.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

import os
import numpy as np

from depth_anything_3.specs import Prediction
from depth_anything_3.utils.parallel_utils import async_call


@async_call
def export_to_npz(
    prediction: Prediction,
    export_dir: str,
):
    output_file = os.path.join(export_dir, "exports", "npz", "results.npz")
    os.makedirs(os.path.dirname(output_file), exist_ok=True)

    # Use prediction.processed_images, which is already processed image data
    if prediction.processed_images is None:
        raise ValueError("prediction.processed_images is required but not available")

    image = prediction.processed_images  # (N,H,W,3) uint8

    # Build save dict with only non-None values
    save_dict = {
        "image": image,
        "depth": np.round(prediction.depth, 6),
    }

    if prediction.conf is not None:
        save_dict["conf"] = np.round(prediction.conf, 2)
    if prediction.extrinsics is not None:
        save_dict["extrinsics"] = prediction.extrinsics
    if prediction.intrinsics is not None:
        save_dict["intrinsics"] = prediction.intrinsics

    # aux = {k: np.round(v, 4) for k, v in prediction.aux.items()}
    np.savez_compressed(output_file, **save_dict)


@async_call
def export_to_mini_npz(
    prediction: Prediction,
    export_dir: str,
):
    output_file = os.path.join(export_dir, "exports", "mini_npz", "results.npz")
    os.makedirs(os.path.dirname(output_file), exist_ok=True)

    # Build save dict with only non-None values
    save_dict = {
        "depth": np.round(prediction.depth, 8),
    }

    if prediction.conf is not None:
        save_dict["conf"] = np.round(prediction.conf, 2)
    if prediction.extrinsics is not None:
        save_dict["extrinsics"] = prediction.extrinsics
    if prediction.intrinsics is not None:
        save_dict["intrinsics"] = prediction.intrinsics

    np.savez_compressed(output_file, **save_dict)



================================================
FILE: src/depth_anything_3/utils/export/utils.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

import numpy as np
import torch


def _denorm_and_to_uint8(image_tensor: torch.Tensor) -> np.ndarray:
    """Denormalize to [0,255] and output (N, H, W, 3) uint8."""
    resnet_mean = torch.tensor(
        [0.485, 0.456, 0.406], dtype=image_tensor.dtype, device=image_tensor.device
    )
    resnet_std = torch.tensor(
        [0.229, 0.224, 0.225], dtype=image_tensor.dtype, device=image_tensor.device
    )
    img = image_tensor * resnet_std[None, :, None, None] + resnet_mean[None, :, None, None]
    img = torch.clamp(img, 0.0, 1.0)
    img = (img.permute(0, 2, 3, 1).cpu().numpy() * 255.0).round().astype(np.uint8)  # (N,H,W,3)
    return img



================================================
FILE: src/depth_anything_3/utils/io/input_processor.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

"""
Input processor for Depth Anything 3 (parallelized).

This version removes the square center-crop step for "*crop" methods (same as your note).
In addition, it parallelizes per-image preprocessing using the provided `parallel_execution`.
"""

from __future__ import annotations

from typing import Sequence
import cv2
import numpy as np
import torch
import torchvision.transforms as T
from PIL import Image

from depth_anything_3.utils.logger import logger
from depth_anything_3.utils.parallel_utils import parallel_execution


class InputProcessor:
    """Prepares a batch of images for model inference.
    This processor converts a list of image file paths into a single, model-ready
    tensor. The processing pipeline is executed in parallel across multiple workers
    for efficiency.

    Pipeline:
      1) Load image and convert to RGB
      2) Boundary resize (upper/lower bound, preserving aspect ratio)
      3) Enforce divisibility by PATCH_SIZE:
         - "*resize" methods: each dimension is rounded to nearest multiple
           (may up/downscale a few px)
         - "*crop"   methods: each dimension is floored to nearest multiple via center crop
      4) Convert to tensor and apply ImageNet normalization
      5) Stack into (1, N, 3, H, W)

    Parallelization:
      - Each image is processed independently in a worker.
      - Order of outputs matches the input order.
    """

    NORMALIZE = T.Normalize(mean=[0.485, 0.456, 0.406], std=[0.229, 0.224, 0.225])
    PATCH_SIZE = 14

    def __init__(self):
        pass

    # -----------------------------
    # Public API
    # -----------------------------
    def __call__(
        self,
        image: list[np.ndarray | Image.Image | str],
        extrinsics: np.ndarray | None = None,
        intrinsics: np.ndarray | None = None,
        process_res: int = 504,
        process_res_method: str = "upper_bound_resize",
        *,
        num_workers: int = 8,
        print_progress: bool = False,
        sequential: bool | None = None,
        desc: str | None = "Preprocess",
    ) -> tuple[torch.Tensor, torch.Tensor | None, torch.Tensor | None]:
        """
        Returns:
            (tensor, extrinsics_list, intrinsics_list)
            tensor shape: (1, N, 3, H, W)
        """
        sequential = self._resolve_sequential(sequential, num_workers)
        exts_list, ixts_list = self._validate_and_pack_meta(image, extrinsics, intrinsics)

        results = self._run_parallel(
            image=image,
            exts_list=exts_list,
            ixts_list=ixts_list,
            process_res=process_res,
            process_res_method=process_res_method,
            num_workers=num_workers,
            print_progress=print_progress,
            sequential=sequential,
            desc=desc,
        )

        proc_imgs, out_sizes, out_ixts, out_exts = self._unpack_results(results)
        proc_imgs, out_sizes, out_ixts = self._unify_batch_shapes(proc_imgs, out_sizes, out_ixts)

        batch_tensor = self._stack_batch(proc_imgs)
        out_exts = (
            torch.from_numpy(np.asarray(out_exts)).float()
            if out_exts is not None and out_exts[0] is not None
            else None
        )
        out_ixts = (
            torch.from_numpy(np.asarray(out_ixts)).float()
            if out_ixts is not None and out_ixts[0] is not None
            else None
        )
        return (batch_tensor, out_exts, out_ixts)

    # -----------------------------
    # __call__ helpers
    # -----------------------------
    def _resolve_sequential(self, sequential: bool | None, num_workers: int) -> bool:
        return (num_workers <= 1) if sequential is None else sequential

    def _validate_and_pack_meta(
        self,
        images: list[np.ndarray | Image.Image | str],
        extrinsics: np.ndarray | None,
        intrinsics: np.ndarray | None,
    ) -> tuple[list[np.ndarray | None] | None, list[np.ndarray | None] | None]:
        if extrinsics is not None and len(extrinsics) != len(images):
            raise ValueError("Length of extrinsics must match images when provided.")
        if intrinsics is not None and len(intrinsics) != len(images):
            raise ValueError("Length of intrinsics must match images when provided.")
        exts_list = [e for e in extrinsics] if extrinsics is not None else None
        ixts_list = [k for k in intrinsics] if intrinsics is not None else None
        return exts_list, ixts_list

    def _run_parallel(
        self,
        *,
        image: list[np.ndarray | Image.Image | str],
        exts_list: list[np.ndarray | None] | None,
        ixts_list: list[np.ndarray | None] | None,
        process_res: int,
        process_res_method: str,
        num_workers: int,
        print_progress: bool,
        sequential: bool,
        desc: str | None,
    ):
        results = parallel_execution(
            image,
            exts_list,
            ixts_list,
            action=self._process_one,  # (img, extrinsic, intrinsic, ...)
            num_processes=num_workers,
            print_progress=print_progress,
            sequential=sequential,
            desc=desc,
            process_res=process_res,
            process_res_method=process_res_method,
        )
        if not results:
            raise RuntimeError(
                "No preprocessing results returned. Check inputs and parallel_execution."
            )
        return results

    def _unpack_results(self, results):
        """
        results: List[Tuple[torch.Tensor, Tuple[H, W], Optional[np.ndarray], Optional[np.ndarray]]]
        -> processed_images, out_sizes, out_intrinsics, out_extrinsics
        """
        try:
            processed_images, out_sizes, out_intrinsics, out_extrinsics = zip(*results)
        except Exception as e:
            raise RuntimeError(
                "Unexpected results structure from parallel_execution: "
                f"{type(results)} / sample: {results[0]}"
            ) from e

        return list(processed_images), list(out_sizes), list(out_intrinsics), list(out_extrinsics)

    def _unify_batch_shapes(
        self,
        processed_images: list[torch.Tensor],
        out_sizes: list[tuple[int, int]],
        out_intrinsics: list[np.ndarray | None],
    ) -> tuple[list[torch.Tensor], list[tuple[int, int]], list[np.ndarray | None]]:
        """Center-crop all tensors to the smallest H, W; adjust intrinsics' cx, cy accordingly."""
        if len(set(out_sizes)) <= 1:
            return processed_images, out_sizes, out_intrinsics

        min_h = min(h for h, _ in out_sizes)
        min_w = min(w for _, w in out_sizes)
        logger.warn(
            f"Images in batch have different sizes {out_sizes}; "
            f"center-cropping all to smallest ({min_h},{min_w})"
        )

        center_crop = T.CenterCrop((min_h, min_w))
        new_imgs, new_sizes, new_ixts = [], [], []
        for img_t, (H, W), K in zip(processed_images, out_sizes, out_intrinsics):
            crop_top = max(0, (H - min_h) // 2)
            crop_left = max(0, (W - min_w) // 2)
            new_imgs.append(center_crop(img_t))
            new_sizes.append((min_h, min_w))
            if K is None:
                new_ixts.append(None)
            else:
                K_adj = K.copy()
                K_adj[0, 2] -= crop_left
                K_adj[1, 2] -= crop_top
                new_ixts.append(K_adj)
        return new_imgs, new_sizes, new_ixts

    def _stack_batch(self, processed_images: list[torch.Tensor]) -> torch.Tensor:
        return torch.stack(processed_images)

    # -----------------------------
    # Per-item worker
    # -----------------------------
    def _process_one(
        self,
        img: np.ndarray | Image.Image | str,
        extrinsic: np.ndarray | None = None,
        intrinsic: np.ndarray | None = None,
        *,
        process_res: int,
        process_res_method: str,
    ) -> tuple[torch.Tensor, tuple[int, int], np.ndarray | None, np.ndarray | None]:
        # Load & remember original size
        pil_img = self._load_image(img)
        orig_w, orig_h = pil_img.size

        # Boundary resize
        pil_img = self._resize_image(pil_img, process_res, process_res_method)
        w, h = pil_img.size
        intrinsic = self._resize_ixt(intrinsic, orig_w, orig_h, w, h)

        # Enforce divisibility by PATCH_SIZE
        if process_res_method.endswith("resize"):
            pil_img = self._make_divisible_by_resize(pil_img, self.PATCH_SIZE)
            new_w, new_h = pil_img.size
            intrinsic = self._resize_ixt(intrinsic, w, h, new_w, new_h)
            w, h = new_w, new_h
        elif process_res_method.endswith("crop"):
            pil_img = self._make_divisible_by_crop(pil_img, self.PATCH_SIZE)
            new_w, new_h = pil_img.size
            intrinsic = self._crop_ixt(intrinsic, w, h, new_w, new_h)
            w, h = new_w, new_h
        else:
            raise ValueError(f"Unsupported process_res_method: {process_res_method}")

        # Convert to tensor & normalize
        img_tensor = self._normalize_image(pil_img)
        _, H, W = img_tensor.shape
        assert (W, H) == (w, h), "Tensor size mismatch with PIL image size after processing."

        # Return: (img_tensor, (H, W), intrinsic, extrinsic)
        return img_tensor, (H, W), intrinsic, extrinsic

    # -----------------------------
    # Intrinsics transforms
    # -----------------------------
    def _resize_ixt(
        self,
        intrinsic: np.ndarray | None,
        orig_w: int,
        orig_h: int,
        w: int,
        h: int,
    ) -> np.ndarray | None:
        if intrinsic is None:
            return None
        K = intrinsic.copy()
        # scale fx, cx by w ratio; fy, cy by h ratio
        K[:1] *= w / float(orig_w)
        K[1:2] *= h / float(orig_h)
        return K

    def _crop_ixt(
        self,
        intrinsic: np.ndarray | None,
        orig_w: int,
        orig_h: int,
        w: int,
        h: int,
    ) -> np.ndarray | None:
        if intrinsic is None:
            return None
        K = intrinsic.copy()
        crop_h = (orig_h - h) // 2
        crop_w = (orig_w - w) // 2
        K[0, 2] -= crop_w
        K[1, 2] -= crop_h
        return K

    # -----------------------------
    # I/O & normalization
    # -----------------------------
    def _load_image(self, img: np.ndarray | Image.Image | str) -> Image.Image:
        if isinstance(img, str):
            return Image.open(img).convert("RGB")
        elif isinstance(img, np.ndarray):
            # Assume HxWxC uint8/RGB
            return Image.fromarray(img).convert("RGB")
        elif isinstance(img, Image.Image):
            return img.convert("RGB")
        else:
            raise ValueError(f"Unsupported image type: {type(img)}")

    def _normalize_image(self, img: Image.Image) -> torch.Tensor:
        img_tensor = T.ToTensor()(img)
        return self.NORMALIZE(img_tensor)

    # -----------------------------
    # Boundary resizing
    # -----------------------------
    def _resize_image(self, img: Image.Image, target_size: int, method: str) -> Image.Image:
        if method in ("upper_bound_resize", "upper_bound_crop"):
            return self._resize_longest_side(img, target_size)
        elif method in ("lower_bound_resize", "lower_bound_crop"):
            return self._resize_shortest_side(img, target_size)
        else:
            raise ValueError(f"Unsupported resize method: {method}")

    def _resize_longest_side(self, img: Image.Image, target_size: int) -> Image.Image:
        w, h = img.size
        longest = max(w, h)
        if longest == target_size:
            return img
        scale = target_size / float(longest)
        new_w = max(1, int(round(w * scale)))
        new_h = max(1, int(round(h * scale)))
        interpolation = cv2.INTER_CUBIC if scale > 1.0 else cv2.INTER_AREA
        arr = cv2.resize(np.asarray(img), (new_w, new_h), interpolation=interpolation)
        return Image.fromarray(arr)

    def _resize_shortest_side(self, img: Image.Image, target_size: int) -> Image.Image:
        w, h = img.size
        shortest = min(w, h)
        if shortest == target_size:
            return img
        scale = target_size / float(shortest)
        new_w = max(1, int(round(w * scale)))
        new_h = max(1, int(round(h * scale)))
        interpolation = cv2.INTER_CUBIC if scale > 1.0 else cv2.INTER_AREA
        arr = cv2.resize(np.asarray(img), (new_w, new_h), interpolation=interpolation)
        return Image.fromarray(arr)

    # -----------------------------
    # Make divisible by PATCH_SIZE
    # -----------------------------
    def _make_divisible_by_crop(self, img: Image.Image, patch: int) -> Image.Image:
        """
        Floor each dimension to the nearest multiple of PATCH_SIZE via center crop.
        Example: 504x377 -> 504x364
        """
        w, h = img.size
        new_w = (w // patch) * patch
        new_h = (h // patch) * patch
        if new_w == w and new_h == h:
            return img
        left = (w - new_w) // 2
        top = (h - new_h) // 2
        return img.crop((left, top, left + new_w, top + new_h))

    def _make_divisible_by_resize(self, img: Image.Image, patch: int) -> Image.Image:
        """
        Round each dimension to nearest multiple of PATCH_SIZE via small resize.
        """
        w, h = img.size

        def nearest_multiple(x: int, p: int) -> int:
            down = (x // p) * p
            up = down + p
            return up if abs(up - x) <= abs(x - down) else down

        new_w = max(1, nearest_multiple(w, patch))
        new_h = max(1, nearest_multiple(h, patch))
        if new_w == w and new_h == h:
            return img
        upscale = (new_w > w) or (new_h > h)
        interpolation = cv2.INTER_CUBIC if upscale else cv2.INTER_AREA
        arr = cv2.resize(np.asarray(img), (new_w, new_h), interpolation=interpolation)
        return Image.fromarray(arr)


# Backward compatibility alias
InputAdapter = InputProcessor


# ===========================
# Minimal test runner (parallel execution)
# ===========================
if __name__ == "__main__":
    """
    Minimal test suite:
      - Creates pairs of images so batch shapes match.
      - Tests all four process_res_methods.
      - Prints fx fy cx cy IN->OUT per image.
      - Includes cases with K/E provided and with None.
    """

    def fmt_k_line(K: np.ndarray | None) -> str:
        if K is None:
            return "None"
        fx, fy, cx, cy = float(K[0, 0]), float(K[1, 1]), float(K[0, 2]), float(K[1, 2])
        return f"fx={fx:.3f} fy={fy:.3f} cx={cx:.3f} cy={cy:.3f}"

    def show_result(
        tag: str,
        tensor: torch.Tensor,
        Ks_in: Sequence[np.ndarray | None] | None = None,
        Ks_out: Sequence[np.ndarray | None] | None = None,
    ):
        B, N, C, H, W = tensor.shape
        print(f"[{tag}] shape={tuple(tensor.shape)}  HxW=({H},{W})  div14=({H%14==0},{W%14==0})")
        assert H % 14 == 0 and W % 14 == 0, f"{tag}: output size not divisible by 14!"
        if Ks_in is not None or Ks_out is not None:
            Ks_in = Ks_in or [None] * N
            Ks_out = Ks_out or [None] * N
            for i in range(N):
                print(f"  K[{i}]: {fmt_k_line(Ks_in[i])}  ->  {fmt_k_line(Ks_out[i])}")

    proc = InputProcessor()
    process_res = 504
    methods = ["upper_bound_resize", "upper_bound_crop", "lower_bound_resize", "lower_bound_crop"]

    # Example sizes (two orientations)
    small_sizes = [(680, 1208), (1208, 680)]
    large_sizes = [(1208, 680), (680, 1208)]

    def make_K(w, h, fx=1200.0, fy=1100.0):
        cx, cy = w / 2.0, h / 2.0
        K = np.array([[fx, 0, cx], [0, fy, cy], [0, 0, 1]], dtype=np.float32)
        return K

    def run_suite(suite_name: str, sizes: list[tuple[int, int]]):
        print(f"\n===== {suite_name} =====")
        for w, h in sizes:
            img = Image.new("RGB", (w, h), color=(123, 222, 100))
            batch_imgs = [img, img]

            # intrinsics / extrinsics examples
            Ks_in = [make_K(w, h), make_K(w, h)]
            Es_in = [np.eye(4, dtype=np.float32), np.eye(4, dtype=np.float32)]

            for m in methods:
                tensor, Es_out, Ks_out = proc(
                    image=batch_imgs,
                    process_res=process_res,
                    process_res_method=m,
                    num_workers=8,
                    print_progress=False,
                    intrinsics=Ks_in,  # test with non-None
                    extrinsics=Es_in,
                )
                show_result(f"{suite_name} size=({w},{h}) | {m}", tensor, Ks_in, Ks_out)

            # Also test None path
            tensor2, Es_out2, Ks_out2 = proc(
                image=batch_imgs,
                process_res=process_res,
                process_res_method="upper_bound_resize",
                num_workers=8,
                intrinsics=None,
                extrinsics=None,
            )
            show_result(
                f"{suite_name} size=({w},{h}) | upper_bound_resize | no K/E",
                tensor2,
                None,
                Ks_out2,
            )

    run_suite("SMALL", small_sizes)
    run_suite("LARGE", large_sizes)

    # Extra sanity for 504x376
    print("\n===== EXTRA sanity for 504x376 =====")
    img_example = Image.new("RGB", (504, 376), color=(10, 20, 30))
    Ks_in_extra = [make_K(504, 376, fx=900.0, fy=900.0), make_K(504, 376, fx=900.0, fy=900.0)]

    out_r, _, Ks_out_r = proc(
        image=[img_example, img_example],
        process_res=504,
        process_res_method="upper_bound_resize",
        num_workers=8,
        intrinsics=Ks_in_extra,
    )
    out_c, _, Ks_out_c = proc(
        image=[img_example, img_example],
        process_res=504,
        process_res_method="upper_bound_crop",
        num_workers=8,
        intrinsics=Ks_in_extra,
    )
    _, _, _, Hr, Wr = out_r.shape
    _, _, _, Hc, Wc = out_c.shape
    print(f"upper_bound_resize -> ({Hr},{Wr})  (rounded to nearest multiple of 14)")
    show_result("Ks after upper_bound_resize", out_r, Ks_in_extra, Ks_out_r)
    print(f"upper_bound_crop   -> ({Hc},{Wc})  (floored to multiple of 14)")
    show_result("Ks after upper_bound_crop", out_c, Ks_in_extra, Ks_out_c)



================================================
FILE: src/depth_anything_3/utils/io/output_processor.py
================================================
# Copyright (c) 2025 ByteDance Ltd. and/or its affiliates
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

"""
Output processor for Depth Anything 3.

This module handles model output processing, including tensor-to-numpy conversion,
batch dimension removal, and Prediction object creation.
"""

from __future__ import annotations

import numpy as np
import torch
from addict import Dict as AddictDict

from depth_anything_3.specs import Prediction


class OutputProcessor:
    """
    Output processor for converting model outputs to Prediction objects.

    Handles tensor-to-numpy conversion, batch dimension removal,
    and creates structured Prediction objects with proper data types.
    """

    def __init__(self) -> None:
        """Initialize the output processor."""

    def __call__(self, model_output: dict[str, torch.Tensor]) -> Prediction:
        """
        Convert model output to Prediction object.

        Args:
            model_output: Model output dictionary containing depth, conf, extrinsics, intrinsics
                         Expected shapes: depth (B, N, 1, H, W), conf (B, N, 1, H, W),
                         extrinsics (B, N, 4, 4), intrinsics (B, N, 3, 3)

        Returns:
            Prediction: Object containing depth estimation results with shapes:
                       depth (N, H, W), conf (N, H, W), extrinsics (N, 4, 4), intrinsics (N, 3, 3)
        """
        # Extract data from batch dimension (B=1, N=number of images)
        depth = self._extract_depth(model_output)
        conf = self._extract_conf(model_output)
        extrinsics = self._extract_extrinsics(model_output)
        intrinsics = self._extract_intrinsics(model_output)
        sky = self._extract_sky(model_output)
        aux = self._extract_aux(model_output)
        gaussians = model_output.get("gaussians", None)
        scale_factor = model_output.get("scale_factor", None)

        return Prediction(
            depth=depth,
            sky=sky,
            conf=conf,
            extrinsics=extrinsics,
            intrinsics=intrinsics,
            is_metric=getattr(model_output, "is_metric", 0),
            gaussians=gaussians,
            aux=aux,
            scale_factor=scale_factor,
        )

    def _extract_depth(self, model_output: dict[str, torch.Tensor]) -> np.ndarray:
        """
        Extract depth tensor from model output and convert to numpy.

        Args:
            model_output: Model output dictionary

        Returns:
            Depth array with shape (N, H, W)
        """
        depth = model_output["depth"].squeeze(0).squeeze(-1).cpu().numpy()  # (N, H, W)
        return depth

    def _extract_conf(self, model_output: dict[str, torch.Tensor]) -> np.ndarray | None:
        """
        Extract confidence tensor from model output and convert to numpy.

        Args:
            model_output: Model output dictionary

        Returns:
            Confidence array with shape (N, H, W) or None
        """
        conf = model_output.get("depth_conf", None)
        if conf is not None:
            conf = conf.squeeze(0).cpu().numpy()  # (N, H, W)
        return conf

    def _extract_extrinsics(self, model_output: dict[str, torch.Tensor]) -> np.ndarray | None:
        """
        Extract extrinsics tensor from model output and convert to numpy.

        Args:
            model_output: Model output dictionary

        Returns:
            Extrinsics array with shape (N, 4, 4) or None
        """
        extrinsics = model_output.get("extrinsics", None)
        if extrinsics is not None:
            extrinsics = extrinsics.squeeze(0).cpu().numpy()  # (N, 4, 4)
        return extrinsics

    def _extract_intrinsics(self, model_output: dict[str, torch.Tensor]) -> np.ndarray | None:
        """
        Extract intrinsics tensor from model output and convert to numpy.

        Args:
            model_output: Model output dictionary

        Returns:
            Intrinsics array with shape (N, 3, 3) or None
        """
        intrinsics = model_output.get("intrinsics", None)
        if intrinsics is not None:
            intrinsics = intrinsics.squeeze(0).cpu().numpy()  # (N, 3, 3)
        return intrinsics

    def _extract_sky(self, model_output: dict[str, torch.Tensor]) -> np.ndarray | None:
        """
        Extract sky tensor from model output and convert to numpy.

        Args:
            model_output: Model output dictionary

        Returns:
            Sky mask array with shape (N, H, W) or None
        """
        sky = model_output.get("sky", None)
        if sky is not None:
            sky = sky.squeeze(0).cpu().numpy() >= 0.5  # (N, H, W)
        return sky

    def _extract_aux(self, model_output: dict[str, torch.Tensor]) -> AddictDict:
        """
        Extract auxiliary data from model output and convert to numpy.

        Args:
            model_output: Model output dictionary

        Returns:
            Dictionary containing auxiliary data
        """
        aux = model_output.get("aux", None)
        ret = AddictDict()
        if aux is not None:
            for k in aux.keys():
                if isinstance(aux[k], torch.Tensor):
                    ret[k] = aux[k].squeeze(0).cpu().numpy()
                else:
                    ret[k] = aux[k]
        return ret


# Backward compatibility alias
OutputAdapter = OutputProcessor
