```
Directory structure:
└── facebookresearch-sam3/
    ├── README.md
    ├── MANIFEST.in
    ├── pyproject.toml
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
    │   └── sam/
    │       ├── __init__.py
    │       ├── common.py
    │       ├── mask_decoder.py
    │       ├── prompt_encoder.py
    │       ├── rope.py
    │       └── transformer.py
    └── scripts/
        ├── measure_speed.py
        ├── qualitative_test.py
        └── eval/
            ├── standalone_cgf1.py
            ├── gold/
            │   └── eval_sam3.py
            └── veval/
                ├── README.md
                ├── __init__.py
                ├── saco_yt1b_annot_update.py
                ├── saco_yt1b_downloader.py
                └── saco_yt1b_frame_prep_util.py
```
================================================
FILE: README.md
================================================
# SAM 3: Segment Anything with Concepts

Meta Superintelligence Labs

[Nicolas Carion](https://www.nicolascarion.com/)\*,
[Laura Gustafson](https://scholar.google.com/citations?user=c8IpF9gAAAAJ&hl=en)\*,
[Yuan-Ting Hu](https://scholar.google.com/citations?user=E8DVVYQAAAAJ&hl=en)\*,
[Shoubhik Debnath](https://scholar.google.com/citations?user=fb6FOfsAAAAJ&hl=en)\*,
[Ronghang Hu](https://ronghanghu.com/)\*,
[Didac Suris](https://www.didacsuris.com/)\*,
[Chaitanya Ryali](https://scholar.google.com/citations?user=4LWx24UAAAAJ&hl=en)\*,
[Kalyan Vasudev Alwala](https://scholar.google.co.in/citations?user=m34oaWEAAAAJ&hl=en)\*,
[Haitham Khedr](https://hkhedr.com/)\*, Andrew Huang,
[Jie Lei](https://jayleicn.github.io/),
[Tengyu Ma](https://scholar.google.com/citations?user=VeTSl0wAAAAJ&hl=en),
[Baishan Guo](https://scholar.google.com/citations?user=BC5wDu8AAAAJ&hl=en),
Arpit Kalla, [Markus Marks](https://damaggu.github.io/),
[Joseph Greer](https://scholar.google.com/citations?user=guL96CkAAAAJ&hl=en),
Meng Wang, [Peize Sun](https://peizesun.github.io/),
[Roman Rädle](https://scholar.google.com/citations?user=Tpt57v0AAAAJ&hl=en),
[Triantafyllos Afouras](https://www.robots.ox.ac.uk/~afourast/),
[Effrosyni Mavroudi](https://scholar.google.com/citations?user=vYRzGGEAAAAJ&hl=en),
[Katherine Xu](https://k8xu.github.io/)°,
[Tsung-Han Wu](https://patrickthwu.com/)°,
[Yu Zhou](https://yu-bryan-zhou.github.io/)°,
[Liliane Momeni](https://scholar.google.com/citations?user=Lb-KgVYAAAAJ&hl=en)°,
[Rishi Hazra](https://rishihazra.github.io/)°,
[Shuangrui Ding](https://mark12ding.github.io/)°,
[Sagar Vaze](https://sgvaze.github.io/)°,
[Francois Porcher](https://scholar.google.com/citations?user=LgHZ8hUAAAAJ&hl=en)°,
[Feng Li](https://fengli-ust.github.io/)°,
[Siyuan Li](https://siyuanliii.github.io/)°,
[Aishwarya Kamath](https://ashkamath.github.io/)°,
[Ho Kei Cheng](https://hkchengrex.com/)°,
[Piotr Dollar](https://pdollar.github.io/)†,
[Nikhila Ravi](https://nikhilaravi.com/)†,
[Kate Saenko](https://ai.bu.edu/ksaenko.html)†,
[Pengchuan Zhang](https://pzzhang.github.io/pzzhang/)†,
[Christoph Feichtenhofer](https://feichtenhofer.github.io/)†

\* core contributor, ° intern, † project lead, order is random within groups

[[`Paper`](https://ai.meta.com/research/publications/sam-3-segment-anything-with-concepts/)]
[[`Project`](https://ai.meta.com/sam3)]
[[`Demo`](https://segment-anything.com/)]
[[`Blog`](https://ai.meta.com/blog/segment-anything-model-3/)]
[[`BibTeX`](#citing-sam-3)]

![SAM 3 architecture](assets/model_diagram.png?raw=true) SAM 3 is a unified foundation model for promptable segmentation in images and videos. It can detect, segment, and track objects using text or visual prompts such as points, boxes, and masks. Compared to its predecessor [SAM 2](https://github.com/facebookresearch/sam2), SAM 3 introduces the ability to exhaustively segment all instances of an open-vocabulary concept specified by a short text phrase or exemplars. Unlike prior work, SAM 3 can handle a vastly larger set of open-vocabulary prompts. It achieves 75-80% of human performance on our new [SA-CO benchmark](https://github.com/facebookresearch/sam3?tab=readme-ov-file#sa-co-dataset) which contains 270K unique concepts, over 50 times more than existing benchmarks.

This breakthrough is driven by an innovative data engine that has automatically annotated over 4 million unique concepts, creating the largest high-quality open-vocabulary segmentation dataset to date. In addition, SAM 3 introduces a new model architecture featuring a presence token that improves discrimination between closely related text prompts (e.g., “a player in white” vs. “a player in red”), as well as a decoupled detector–tracker design that minimizes task interference and scales efficiently with data.

<p align="center">
  <img src="assets/dog.gif" width=380 />
  <img src="assets/player.gif" width=380 />
</p>

## Latest updates

**03/27/2026 -- SAM 3.1 Object Multiplex is released. It introduces a shared-memory approach for joint multi-object tracking that is significantly faster without sacrificing accuracy.**

- A new suite of improved model checkpoints (denoted as **SAM 3.1**) are released on [Hugging Face](https://huggingface.co/facebook/sam3.1). See [`RELEASE_SAM3p1.md`](RELEASE_SAM3p1.md) for full details.
  * To use the new SAM 3.1 checkpoints, you need the latest model code from this repo. If you have installed an earlier version of this repo, pull the latest code from this repo (with `git pull`), and then reinstall the repo following [Installation](#installation) below.

## Installation

### Prerequisites

- Python 3.12 or higher
- PyTorch 2.7 or higher
- CUDA-compatible GPU with CUDA 12.6 or higher

1. **Create a new Conda environment:**

```bash
conda create -n sam3 python=3.12
conda deactivate
conda activate sam3
```

2. **Install PyTorch with CUDA support:**

```bash
pip install torch==2.10.0 torchvision --index-url https://download.pytorch.org/whl/cu128
```

3. **Clone the repository and install the package:**

```bash
git clone https://github.com/facebookresearch/sam3.git
cd sam3
pip install -e .
```

4. **Install additional dependencies for example notebooks or development:**

```bash
# For running example notebooks
pip install -e ".[notebooks]"

# For development
pip install -e ".[train,dev]"
```

5. **Optional dependencies for faster inference**
```bash
pip install einops ninja && pip install flash-attn-3 --no-deps --index-url https://download.pytorch.org/whl/cu128
pip install git+https://github.com/ronghanghu/cc_torch.git
```

## Getting Started

⚠️ Before using SAM 3, please request access to the checkpoints on the SAM 3
Hugging Face [repo](https://huggingface.co/facebook/sam3). Once accepted, you
need to be authenticated to download the checkpoints. You can do this by running
the following [steps](https://huggingface.co/docs/huggingface_hub/en/quick-start#authentication)
(e.g. `hf auth login` after generating an access token.)

### Basic Usage

```python
import torch
#################################### For Image ####################################
from PIL import Image
from sam3.model_builder import build_sam3_image_model
from sam3.model.sam3_image_processor import Sam3Processor
# Load the model
model = build_sam3_image_model()
processor = Sam3Processor(model)
# Load an image
image = Image.open("<YOUR_IMAGE_PATH.jpg>")
inference_state = processor.set_image(image)
# Prompt the model with text
output = processor.set_text_prompt(state=inference_state, prompt="<YOUR_TEXT_PROMPT>")

# Get the masks, bounding boxes, and scores
masks, boxes, scores = output["masks"], output["boxes"], output["scores"]

#################################### For Video ####################################

from sam3.model_builder import build_sam3_video_predictor

video_predictor = build_sam3_video_predictor()
video_path = "<YOUR_VIDEO_PATH>" # a JPEG folder or an MP4 video file
# Start a session
response = video_predictor.handle_request(
    request=dict(
        type="start_session",
        resource_path=video_path,
    )
)
response = video_predictor.handle_request(
    request=dict(
        type="add_prompt",
        session_id=response["session_id"],
        frame_index=0, # Arbitrary frame index
        text="<YOUR_TEXT_PROMPT>",
    )
)
output = response["outputs"]
```

## Examples

The `examples` directory contains notebooks demonstrating how to use SAM3 with
various types of prompts:

- [`sam3_image_predictor_example.ipynb`](examples/sam3_image_predictor_example.ipynb)
  : Demonstrates how to prompt SAM 3 with text and visual box prompts on images.
- [`sam3_video_predictor_example.ipynb`](examples/sam3_video_predictor_example.ipynb)
  : Demonstrates how to prompt SAM 3 with text prompts on videos, and doing
  further interactive refinements with points.
- [`sam3_image_batched_inference.ipynb`](examples/sam3_image_batched_inference.ipynb)
  : Demonstrates how to run batched inference with SAM 3 on images.
- [`sam3_agent.ipynb`](examples/sam3_agent.ipynb): Demonsterates the use of SAM
  3 Agent to segment complex text prompt on images.
- [`saco_gold_silver_vis_example.ipynb`](examples/saco_gold_silver_vis_example.ipynb)
  : Shows a few examples from SA-Co image evaluation set.
- [`saco_veval_vis_example.ipynb`](examples/saco_veval_vis_example.ipynb) :
  Shows a few examples from SA-Co video evaluation set.

There are additional notebooks in the examples directory that demonstrate how to
use SAM 3 for interactive instance segmentation in images and videos (SAM 1/2
tasks), or as a tool for an MLLM, and how to run evaluations on the SA-Co
dataset.

To run the Jupyter notebook examples:

```bash
# Make sure you have the notebooks dependencies installed
pip install -e ".[notebooks]"

# Start Jupyter notebook
jupyter notebook examples/sam3_image_predictor_example.ipynb
```

## Model

SAM 3 consists of a detector and a tracker that share a vision encoder. It has 848M parameters. The
detector is a DETR-based model conditioned on text, geometry, and image
exemplars. The tracker inherits the SAM 2 transformer encoder-decoder
architecture, supporting video segmentation and interactive refinement.

## Image Results

<div align="center">
<table style="min-width: 80%; border: 2px solid #ddd; border-collapse: collapse">
  <thead>
    <tr>
      <th rowspan="3" style="border-right: 2px solid #ddd; padding: 12px 20px">Model</th>
      <th colspan="3" style="text-align: center; border-right: 2px solid #ddd; padding: 12px 20px">Instance Segmentation</th>
      <th colspan="5" style="text-align: center; padding: 12px 20px">Box Detection</th>
    </tr>
    <tr>
      <th colspan="2" style="text-align: center; border-right: 1px solid #eee; padding: 12px 20px">LVIS</th>
      <th style="text-align: center; border-right: 2px solid #ddd; padding: 12px 20px">SA-Co/Gold</th>
      <th colspan="2" style="text-align: center; border-right: 1px solid #eee; padding: 12px 20px">LVIS</th>
      <th colspan="2" style="text-align: center; border-right: 1px solid #eee; padding: 12px 20px">COCO</th>
      <th style="text-align: center; padding: 12px 20px">SA-Co/Gold</th>
    </tr>
    <tr>
      <th style="text-align: center; padding: 12px 20px">cgF1</th>
      <th style="text-align: center; border-right: 1px solid #eee; padding: 12px 20px">AP</th>
      <th style="text-align: center; border-right: 2px solid #ddd; padding: 12px 20px">cgF1</th>
      <th style="text-align: center; padding: 12px 20px">cgF1</th>
      <th style="text-align: center; border-right: 1px solid #eee; padding: 12px 20px">AP</th>
      <th style="text-align: center; padding: 12px 20px">AP</th>
      <th style="text-align: center; border-right: 1px solid #eee; padding: 12px 20px">AP<sub>o</sub>
</th>
      <th style="text-align: center; padding: 12px 20px">cgF1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="border-right: 2px solid #ddd; padding: 10px 20px">Human</td>
      <td style="text-align: center; padding: 10px 20px">-</td>
      <td style="text-align: center; border-right: 1px solid #eee; padding: 10px 20px">-</td>
      <td style="text-align: center; border-right: 2px solid #ddd; padding: 10px 20px">72.8</td>
      <td style="text-align: center; padding: 10px 20px">-</td>
      <td style="text-align: center; border-right: 1px solid #eee; padding: 10px 20px">-</td>
      <td style="text-align: center; padding: 10px 20px">-</td>
      <td style="text-align: center; border-right: 1px solid #eee; padding: 10px 20px">-</td>
      <td style="text-align: center; padding: 10px 20px">74.0</td>
    </tr>
    <tr>
      <td style="border-right: 2px solid #ddd; padding: 10px 20px">OWLv2*</td>
      <td style="text-align: center; padding: 10px 20px; color: #999">29.3</td>
      <td style="text-align: center; border-right: 1px solid #eee; padding: 10px 20px; color: #999">43.4</td>
      <td style="text-align: center; border-right: 2px solid #ddd; padding: 10px 20px">24.6</td>
      <td style="text-align: center; padding: 10px 20px; color: #999">30.2</td>
      <td style="text-align: center; border-right: 1px solid #eee; padding: 10px 20px; color: #999">45.5</td>
      <td style="text-align: center; padding: 10px 20px">46.1</td>
      <td style="text-align: center; border-right: 1px solid #eee; padding: 10px 20px">23.9</td>
      <td style="text-align: center; padding: 10px 20px">24.5</td>
    </tr>
    <tr>
      <td style="border-right: 2px solid #ddd; padding: 10px 20px">DINO-X</td>
      <td style="text-align: center; padding: 10px 20px">-</td>
      <td style="text-align: center; border-right: 1px solid #eee; padding: 10px 20px">38.5</td>
      <td style="text-align: center; border-right: 2px solid #ddd; padding: 10px 20px">21.3</td>
      <td style="text-align: center; padding: 10px 20px">-</td>
      <td style="text-align: center; border-right: 1px solid #eee; padding: 10px 20px">52.4</td>
      <td style="text-align: center; padding: 10px 20px">56.0</td>
      <td style="text-align: center; border-right: 1px solid #eee; padding: 10px 20px">-</td>
      <td style="text-align: center; padding: 10px 20px">22.5</td>
    </tr>
    <tr>
      <td style="border-right: 2px solid #ddd; padding: 10px 20px">Gemini 2.5</td>
      <td style="text-align: center; padding: 10px 20px">13.4</td>
      <td style="text-align: center; border-right: 1px solid #eee; padding: 10px 20px">-</td>
      <td style="text-align: center; border-right: 2px solid #ddd; padding: 10px 20px">13.0</td>
      <td style="text-align: center; padding: 10px 20px">16.1</td>
      <td style="text-align: center; border-right: 1px solid #eee; padding: 10px 20px">-</td>
      <td style="text-align: center; padding: 10px 20px">-</td>
      <td style="text-align: center; border-right: 1px solid #eee; padding: 10px 20px">-</td>
      <td style="text-align: center; padding: 10px 20px">14.4</td>
    </tr>
    <tr style="border-top: 2px solid #b19c9cff">
      <td style="border-right: 2px solid #ddd; padding: 10px 20px">SAM 3</td>
      <td style="text-align: center; padding: 10px 20px">37.2</td>
      <td style="text-align: center; border-right: 1px solid #eee; padding: 10px 20px">48.5</td>
      <td style="text-align: center; border-right: 2px solid #ddd; padding: 10px 20px">54.1</td>
      <td style="text-align: center; padding: 10px 20px">40.6</td>
      <td style="text-align: center; border-right: 1px solid #eee; padding: 10px 20px">53.6</td>
      <td style="text-align: center; padding: 10px 20px">56.4</td>
      <td style="text-align: center; border-right: 1px solid #eee; padding: 10px 20px">55.7</td>
      <td style="text-align: center; padding: 10px 20px">55.7</td>
    </tr>
  </tbody>
</table>

<p style="text-align: center; margin-top: 10px; font-size: 0.9em; color: #ddd;">* Partially trained on LVIS, AP<sub>o</sub> refers to COCO-O accuracy</p>

</div>

## Video Results

<div align="center">
<table style="min-width: 80%; border: 2px solid #ddd; border-collapse: collapse">
  <thead>
    <tr>
      <th rowspan="2" style="border-right: 2px solid #ddd; padding: 12px 20px">Model</th>
      <th colspan="2" style="text-align: center; border-right: 1px solid #eee; padding: 12px 20px">SA-V test</th>
      <th colspan="2" style="text-align: center; border-right: 1px solid #eee; padding: 12px 20px">YT-Temporal-1B test</th>
      <th colspan="2" style="text-align: center; border-right: 1px solid #eee; padding: 12px 20px">SmartGlasses test</th>
      <th style="text-align: center; border-right: 1px solid #eee; padding: 12px 20px">LVVIS test</th>
      <th style="text-align: center; padding: 12px 20px">BURST test</th>
    </tr>
    <tr>
      <th style="text-align: center; padding: 12px 20px">cgF1</th>
      <th style="text-align: center; border-right: 1px solid #eee; padding: 12px 20px">pHOTA</th>
      <th style="text-align: center; padding: 12px 20px">cgF1</th>
      <th style="text-align: center; border-right: 1px solid #eee; padding: 12px 20px">pHOTA</th>
      <th style="text-align: center; padding: 12px 20px">cgF1</th>
      <th style="text-align: center; border-right: 1px solid #eee; padding: 12px 20px">pHOTA</th>
      <th style="text-align: center; border-right: 1px solid #eee; padding: 12px 20px">mAP</th>
      <th style="text-align: center; padding: 12px 20px">HOTA</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="border-right: 2px solid #ddd; padding: 10px 20px">Human</td>
      <td style="text-align: center; padding: 10px 20px">53.1</td>
      <td style="text-align: center; border-right: 1px solid #eee; padding: 10px 20px">70.5</td>
      <td style="text-align: center; padding: 10px 20px">71.2</td>
      <td style="text-align: center; border-right: 1px solid #eee; padding: 10px 20px">78.4</td>
      <td style="text-align: center; padding: 10px 20px">58.5</td>
      <td style="text-align: center; border-right: 1px solid #eee; padding: 10px 20px">72.3</td>
      <td style="text-align: center; border-right: 1px solid #eee; padding: 10px 20px">-</td>
      <td style="text-align: center; padding: 10px 20px">-</td>
    </tr>
    <tr style="border-top: 2px solid #b19c9cff">
      <td style="border-right: 2px solid #ddd; padding: 10px 20px">SAM 3</td>
      <td style="text-align: center; padding: 10px 20px">30.3</td>
      <td style="text-align: center; border-right: 1px solid #eee; padding: 10px 20px">58.0</td>
      <td style="text-align: center; padding: 10px 20px">50.8</td>
      <td style="text-align: center; border-right: 1px solid #eee; padding: 10px 20px">69.9</td>
      <td style="text-align: center; padding: 10px 20px">36.4</td>
      <td style="text-align: center; border-right: 1px solid #eee; padding: 10px 20px">63.6</td>
      <td style="text-align: center; border-right: 1px solid #eee; padding: 10px 20px">36.3</td>
      <td style="text-align: center; padding: 10px 20px">44.5</td>
    </tr>
  </tbody>
</table>
</div>

## SA-Co Dataset

We release 2 image benchmarks, [SA-Co/Gold](scripts/eval/gold/README.md) and
[SA-Co/Silver](scripts/eval/silver/README.md), and a video benchmark
[SA-Co/VEval](scripts/eval/veval/README.md). The datasets contain images (or videos) with annotated noun phrases. Each image/video and noun phrase pair is annotated with instance masks and unique IDs of each object matching the phrase. Phrases that have no matching objects (negative prompts) have no masks, shown in red font in the figure. See the linked READMEs for more details on how to download and run evaluations on the datasets.

* HuggingFace host: [SA-Co/Gold](https://huggingface.co/datasets/facebook/SACo-Gold), [SA-Co/Silver](https://huggingface.co/datasets/facebook/SACo-Silver) and [SA-Co/VEval](https://huggingface.co/datasets/facebook/SACo-VEval)
* Roboflow host: [SA-Co/Gold](https://universe.roboflow.com/sa-co-gold), [SA-Co/Silver](https://universe.roboflow.com/sa-co-silver) and [SA-Co/VEval](https://universe.roboflow.com/sa-co-veval)

![SA-Co dataset](assets/sa_co_dataset.jpg?raw=true)

## Development

To set up the development environment:

```bash
pip install -e ".[dev,train]"
```

To format the code:

```bash
ufmt format .
```

## Contributing

See [contributing](CONTRIBUTING.md) and the
[code of conduct](CODE_OF_CONDUCT.md).

## License

This project is licensed under the SAM License - see the [LICENSE](LICENSE) file
for details.

## Acknowledgements

We would like to thank the following people for their contributions to the SAM 3 project: Alex He, Alexander Kirillov,
Alyssa Newcomb, Ana Paula Kirschner Mofarrej, Andrea Madotto, Andrew Westbury, Ashley Gabriel, Azita Shokpour,
Ben Samples, Bernie Huang, Carleigh Wood, Ching-Feng Yeh, Christian Puhrsch, Claudette Ward, Daniel Bolya,
Daniel Li, Facundo Figueroa, Fazila Vhora, George Orlin, Hanzi Mao, Helen Klein, Hu Xu, Ida Cheng, Jake Kinney,
Jiale Zhi, Jo Sampaio, Joel Schlosser, Justin Johnson, Kai Brown, Karen Bergan, Karla Martucci, Kenny Lehmann,
Maddie Mintz, Mallika Malhotra, Matt Ward, Michelle Chan, Michelle Restrepo, Miranda Hartley, Muhammad Maaz,
Nisha Deo, Peter Park, Phillip Thomas, Raghu Nayani, Rene Martinez Doehner, Robbie Adkins, Ross Girshik, Sasha
Mitts, Shashank Jain, Spencer Whitehead, Ty Toledano, Valentin Gabeur, Vincent Cho, Vivian Lee, William Ngan,
Xuehai He, Yael Yungster, Ziqi Pang, Ziyi Dou, Zoe Quake.

## Citing SAM 3

If you use SAM 3 or the SA-Co dataset in your research, please use the following BibTeX entry.

```bibtex
@misc{carion2025sam3segmentconcepts,
      title={SAM 3: Segment Anything with Concepts},
      author={Nicolas Carion and Laura Gustafson and Yuan-Ting Hu and Shoubhik Debnath and Ronghang Hu and Didac Suris and Chaitanya Ryali and Kalyan Vasudev Alwala and Haitham Khedr and Andrew Huang and Jie Lei and Tengyu Ma and Baishan Guo and Arpit Kalla and Markus Marks and Joseph Greer and Meng Wang and Peize Sun and Roman Rädle and Triantafyllos Afouras and Effrosyni Mavroudi and Katherine Xu and Tsung-Han Wu and Yu Zhou and Liliane Momeni and Rishi Hazra and Shuangrui Ding and Sagar Vaze and Francois Porcher and Feng Li and Siyuan Li and Aishwarya Kamath and Ho Kei Cheng and Piotr Dollár and Nikhila Ravi and Kate Saenko and Pengchuan Zhang and Christoph Feichtenhofer},
      year={2025},
      eprint={2511.16719},
      archivePrefix={arXiv},
      primaryClass={cs.CV},
      url={https://arxiv.org/abs/2511.16719},
}
```



================================================
FILE: MANIFEST.in
================================================
include LICENSE
include README.md
recursive-include examples *.py
recursive-include examples *.ipynb
recursive-include examples *.md
recursive-include tests *.py



================================================
FILE: pyproject.toml
================================================
[build-system]
requires = ["setuptools>=61", "wheel"]
build-backend = "setuptools.build_meta"

[project]
name = "sam3"
dynamic = ["version"]
description = "SAM3 (Segment Anything Model 3) implementation"
readme = "README.md"
requires-python = ">=3.8"
license = {file = "LICENSE"}
authors = [
    {name = "Meta AI Research"}
]
classifiers = [
    "Development Status :: 4 - Beta",
    "Intended Audience :: Science/Research",
    "License :: OSI Approved :: MIT License",
    "Programming Language :: Python :: 3",
    "Programming Language :: Python :: 3.8",
    "Programming Language :: Python :: 3.9",
    "Programming Language :: Python :: 3.10",
    "Programming Language :: Python :: 3.11",
    "Programming Language :: Python :: 3.12",
    "Topic :: Scientific/Engineering :: Artificial Intelligence",
]
dependencies = [
    "timm>=1.0.17",
    "numpy>=1.26,<2",
    "tqdm",
    "ftfy==6.1.1",
    "regex",
    "iopath>=0.1.10",
    "typing_extensions",
    "huggingface_hub",
]

[project.optional-dependencies]
dev = [
    "pytest",
    "pytest-cov",
    "black==24.2.0",
    "ufmt==2.8.0",
    "ruff-api==0.1.0",
    "usort==1.0.2",
    "gitpython==3.1.31",
    "yt-dlp",
    "pandas",
    "opencv-python",
    "pycocotools",
    "numba",
    "python-rapidjson",
]
notebooks = [
    "matplotlib",
    "jupyter",
    "notebook",
    "ipywidgets",
    "ipycanvas",
    "ipympl",
    "pycocotools",
    "decord",
    "opencv-python",
    "einops",
    "scikit-image",
    "scikit-learn",
]
train = [
    "hydra-core",
    "submitit",
    "tensorboard",
    "zstandard",
    "scipy",
    "torchmetrics",
    "fvcore",
    "fairscale",
    "scikit-image",
    "scikit-learn",
]

[project.urls]
"Homepage" = "https://github.com/facebookresearch/sam3"
"Bug Tracker" = "https://github.com/facebookresearch/sam3/issues"

[tool.setuptools.packages.find]
include = ["sam3*"]
exclude = ["build*", "scripts*", "examples*"]

[tool.setuptools.package-data]
sam3 = ["assets/*.txt.gz"]

[tool.setuptools.dynamic]
version = {attr = "sam3.__version__"}

[tool.black]
line-length = 88
target-version = ['py38', 'py39', 'py310', 'py311', 'py312']
include = '\.pyi?$'

[tool.isort]
profile = "black"
multi_line_output = 3

[tool.usort]
first_party_detection = false

[tool.ufmt]
formatter = "ruff-api"

[tool.mypy]
python_version = "3.12"
warn_return_any = true
warn_unused_configs = true
disallow_untyped_defs = true
disallow_incomplete_defs = true

[[tool.mypy.overrides]]
module = [
    "torch.*",
    "torchvision.*",
    "timm.*",
    "numpy.*",
    "PIL.*",
    "tqdm.*",
    "ftfy.*",
    "regex.*",
    "iopath.*",
]
ignore_missing_imports = true

[tool.pytest.ini_options]
testpaths = ["tests"]
python_files = "test_*.py"
python_classes = "Test*"
python_functions = "test_*"



================================================
FILE: examples/saco_gold_silver_vis_example.ipynb
================================================
# Jupyter notebook converted to Python script.

# Copyright (c) Meta Platforms, Inc. and affiliates.

using_colab = False

if using_colab:
    import torch
    import torchvision
    print("PyTorch version:", torch.__version__)
    print("Torchvision version:", torchvision.__version__)
    print("CUDA is available:", torch.cuda.is_available())
    import sys
    !{sys.executable} -m pip install opencv-python matplotlib scikit-learn
    !{sys.executable} -m pip install 'git+https://github.com/facebookresearch/sam3.git'

import os
from glob import glob

import numpy as np
import sam3.visualization_utils as utils

from matplotlib import pyplot as plt

COLORS = utils.pascal_color_map()[1:]

"""
1. Load the data
"""

# Preapre the data path
ANNOT_DIR = None # PUT YOUR ANNOTATION PATH HERE
IMG_DIR = None # PUT YOUR IMAGE PATH HERE

# Load the SA-CO/Gold annotation files
annot_file_list = glob(os.path.join(ANNOT_DIR, "*gold*.json"))
annot_dfs = utils.get_annot_dfs(file_list=annot_file_list)

"""
Show the annotation files being loaded
"""

annot_dfs.keys()

"""
2. Examples of the data format
"""

annot_dfs["gold_fg_sports_equipment_merged_a_release_test"].keys()

annot_dfs["gold_fg_sports_equipment_merged_a_release_test"]["info"]

annot_dfs["gold_fg_sports_equipment_merged_a_release_test"]["images"].head(3)

annot_dfs["gold_fg_sports_equipment_merged_a_release_test"]["annotations"].head(3)

"""
3. Visualize the data
"""

# Select a target dataset
target_dataset_name = "gold_fg_food_merged_a_release_test"

import cv2
from pycocotools import mask as mask_util
from collections import defaultdict

# Group GT annotations by image_id
gt_image_np_pairs = annot_dfs[target_dataset_name]["images"]
gt_annotations = annot_dfs[target_dataset_name]["annotations"]

gt_image_np_map = {img["id"]: img for _, img in gt_image_np_pairs.iterrows()}
gt_image_np_ann_map = defaultdict(list)
for _, ann in gt_annotations.iterrows():
    image_id = ann["image_id"]
    if image_id not in gt_image_np_ann_map:
        gt_image_np_ann_map[image_id] = []
    gt_image_np_ann_map[image_id].append(ann)

positiveNPs = common_image_ids = [img_id for img_id in gt_image_np_map.keys() if img_id in gt_image_np_ann_map and gt_image_np_ann_map[img_id]]
negativeNPs = [img_id for img_id in gt_image_np_map.keys() if img_id not in gt_image_np_ann_map or not gt_image_np_ann_map[img_id]]

num_image_nps_to_show = 10
fig, axes = plt.subplots(num_image_nps_to_show, 3, figsize=(15, 5 * num_image_nps_to_show))
for idx in range(num_image_nps_to_show):
    rand_idx = np.random.randint(len(positiveNPs))
    image_id = positiveNPs[rand_idx]
    noun_phrase = gt_image_np_map[image_id]["text_input"]
    img_rel_path = gt_image_np_map[image_id]["file_name"]
    full_path = os.path.join(IMG_DIR, f"{img_rel_path}")
    img = cv2.imread(full_path)
    img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
    gt_annotation = gt_image_np_ann_map[image_id]

    def display_image_in_subplot(img, axes, row, col, title=""):
        axes[row, col].imshow(img)
        axes[row, col].set_title(title)
        axes[row, col].axis('off')


    noun_phrases = [noun_phrase]
    annot_masks = [mask_util.decode(ann["segmentation"]) for ann in gt_annotation]

    # Show the image
    display_image_in_subplot(img, axes, idx, 0, f"{noun_phrase}")

    # Show all masks over a white background
    all_masks = utils.draw_masks_to_frame(
        frame=np.ones_like(img)*255, masks=annot_masks, colors=COLORS[: len(annot_masks)]
    )
    display_image_in_subplot(all_masks, axes, idx, 1, f"{noun_phrase} - Masks only")

    # Show masks overlaid on the image
    masked_frame = utils.draw_masks_to_frame(
        frame=img, masks=annot_masks, colors=COLORS[: len(annot_masks)]
    )
    display_image_in_subplot(masked_frame, axes, idx, 2, f"{noun_phrase} - Masks overlaid")




================================================
FILE: examples/saco_veval_eval_example.ipynb
================================================
# Jupyter notebook converted to Python script.

import json
import os

from sam3.eval.saco_veval_eval import VEvalEvaluator

DATASETS_TO_EVAL = [
    "saco_veval_sav_test",
    "saco_veval_yt1b_test",
    "saco_veval_smartglasses_test",
]
# Update to the directory where the GT annotation and PRED files exist
GT_DIR = None # PUT YOUR ANNOTATION PATH HERE
PRED_DIR = None # PUT YOUR IMAGE PATH HERE

all_eval_res = {}
for dataset_name in DATASETS_TO_EVAL:
    gt_annot_file = os.path.join(GT_DIR, dataset_name + ".json")
    pred_file = os.path.join(PRED_DIR, dataset_name + "_preds.json")
    eval_res_file = os.path.join(PRED_DIR, dataset_name + "_eval_res.json")

    if os.path.exists(eval_res_file):
        with open(eval_res_file, "r") as f:
            eval_res = json.load(f)
    else:
        # Alternatively, we can run the evaluator offline first
        # by leveraging sam3/eval/saco_veval_eval.py
        print(f"=== Running evaluation for Pred {pred_file} vs GT {gt_annot_file} ===")
        veval_evaluator = VEvalEvaluator(
            gt_annot_file=gt_annot_file, eval_res_file=eval_res_file
        )
        eval_res = veval_evaluator.run_eval(pred_file=pred_file)
        print(f"=== Results saved to {eval_res_file} ===")

    all_eval_res[dataset_name] = eval_res

REPORT_METRICS = {
    "video_mask_demo_cgf1_micro_50_95": "cgf1",
    "video_mask_all_phrase_HOTA": "pHOTA",
}

res_to_print = []
for dataset_name in DATASETS_TO_EVAL:
    eval_res = all_eval_res[dataset_name]
    row = [dataset_name]
    for metric_k, metric_v in REPORT_METRICS.items():
        row.append(eval_res["dataset_results"][metric_k])
    res_to_print.append(row)

# Print dataset header (each dataset spans 2 metrics: 13 + 3 + 13 = 29 chars)
print("| " + " | ".join(f"{ds:^29}" for ds in DATASETS_TO_EVAL) + " |")

# Print metric header
metrics = list(REPORT_METRICS.values())
print("| " + " | ".join(f"{m:^13}" for _ in DATASETS_TO_EVAL for m in metrics) + " |")

# Print eval results
values = []
for row in res_to_print:
    values.extend([f"{v * 100:^13.1f}" for v in row[1:]])
print("| " + " | ".join(values) + " |")



================================================
FILE: examples/saco_veval_vis_example.ipynb
================================================
# Jupyter notebook converted to Python script.

# Copyright (c) Meta Platforms, Inc. and affiliates.

using_colab = False

if using_colab:
    import torch
    import torchvision
    print("PyTorch version:", torch.__version__)
    print("Torchvision version:", torchvision.__version__)
    print("CUDA is available:", torch.cuda.is_available())
    import sys
    !{sys.executable} -m pip install opencv-python matplotlib scikit-learn
    !{sys.executable} -m pip install 'git+https://github.com/facebookresearch/sam3.git'

import os
from glob import glob

import numpy as np
import utils

from matplotlib import pyplot as plt

COLORS = utils.pascal_color_map()[1:]

"""
1. Load the data
"""

# Preapre the data path
DATA_DIR = "./sam3_saco_veval_data" # PUT YOUR DATA PATH HERE
ANNOT_DIR = os.path.join(DATA_DIR, "annotation")

# Load the SACO/Veval annotation files
annot_file_list = glob(os.path.join(ANNOT_DIR, "*veval*.json"))
annot_dfs = utils.get_annot_dfs(file_list=annot_file_list)

"""
Show the annotation files being loaded
"""

annot_dfs.keys()

"""
2. Examples of the data format
"""

annot_dfs["saco_veval_yt1b_val"].keys()

annot_dfs["saco_veval_yt1b_val"]["info"]

annot_dfs["saco_veval_yt1b_val"]["videos"].head(3)

annot_dfs["saco_veval_yt1b_val"]["annotations"].head(3)

annot_dfs["saco_veval_yt1b_val"]["categories"].head(3)

annot_dfs["saco_veval_yt1b_val"]["video_np_pairs"].head(3)

"""
3. Visualize the data
"""

# Select a target dataset
target_dataset_name = "saco_veval_yt1b_val"

# visualize a random positive video-np pair
df_pairs = annot_dfs[target_dataset_name]["video_np_pairs"]
df_positive_pairs = df_pairs[df_pairs.num_masklets > 0]
rand_idx = np.random.randint(len(df_positive_pairs))
pair_row = df_positive_pairs.iloc[rand_idx]
video_id = pair_row.video_id
noun_phrase = pair_row.noun_phrase
print(f"Randomly selected video-np pair: video_id={video_id}, noun_phrase={noun_phrase}")

def display_image_in_subplot(img, axes, row, col, title=""):
    axes[row, col].imshow(img)
    axes[row, col].set_title(title)
    axes[row, col].axis('off')

num_frames_to_show = 5  # Number of frames to show per dataset
every_n_frames = 4  # Interval between frames to show

fig, axes = plt.subplots(num_frames_to_show, 3, figsize=(15, 5 * num_frames_to_show))

for idx in range(0, num_frames_to_show):
    sampled_frame_idx = idx * every_n_frames
    print(f"Reading annotations for frame {sampled_frame_idx}")
    # Get the frame and the corresponding masks and noun phrases
    frame, annot_masks, annot_noun_phrases = utils.get_all_annotations_for_frame(
        annot_dfs[target_dataset_name], video_id=video_id, frame_idx=sampled_frame_idx, data_dir=DATA_DIR, dataset=target_dataset_name
    )
    # Filter masks and noun phrases by the selected noun phrase
    annot_masks = [m for m, np in zip(annot_masks, annot_noun_phrases) if np == noun_phrase]

    # Show the frame
    display_image_in_subplot(frame, axes, idx, 0, f"{target_dataset_name} - {noun_phrase} - Frame {sampled_frame_idx}")

    # Show the annotated masks
    if annot_masks is None:
        print(f"No masks found for video_id {video_id} at frame {sampled_frame_idx}")
    else:
        # Show all masks over a white background
        all_masks = utils.draw_masks_to_frame(
            frame=np.ones_like(frame)*255, masks=annot_masks, colors=COLORS[: len(annot_masks)]
        )
        display_image_in_subplot(all_masks, axes, idx, 1, f"{target_dataset_name} - {noun_phrase} - Frame {sampled_frame_idx} - Masks")
        
        # Show masks overlaid on the frame
        masked_frame = utils.draw_masks_to_frame(
            frame=frame, masks=annot_masks, colors=COLORS[: len(annot_masks)]
        )
        display_image_in_subplot(masked_frame, axes, idx, 2, f"Dataset: {target_dataset_name} - {noun_phrase} - Frame {sampled_frame_idx} - Masks overlaid")

plt.tight_layout()
plt.show()



================================================
FILE: examples/sam3.1_video_predictor_example.ipynb
================================================
# Jupyter notebook converted to Python script.

# Copyright (c) Meta Platforms, Inc. and affiliates.

"""
## Video segmentation and tracking with SAM 3.1 (Object Multiplex)

This notebook demonstrates how to use SAM 3.1 with Object Multiplex for interactive video segmentation and dense tracking. Object Multiplex groups objects into fixed-capacity buckets and processes them jointly, drastically reducing redundant computation compared to SAM 3's per-object inference. It covers the following capabilities:

- **Text prompts**: Using natural language descriptions to segment objects (e.g., "person", "shoe")
- **Point prompts**: Adding positive/negative clicks to segment and refine objects

We use the terms _segment_ or _mask_ to refer to the model prediction for an object on a single frame, and _masklet_ to refer to the spatio-temporal masks across the entire video. 
"""

"""
<a target="_blank" href="https://colab.research.google.com/github/facebookresearch/sam3/blob/main/notebooks/sam3.1_video_predictor_example.ipynb">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/>
</a>
"""

using_colab = False

if using_colab:
    import torch
    import torchvision
    print("PyTorch version:", torch.__version__)
    print("Torchvision version:", torchvision.__version__)
    print("CUDA is available:", torch.cuda.is_available())
    import sys
    !{sys.executable} -m pip install opencv-python matplotlib scikit-learn
    !{sys.executable} -m pip install 'git+https://github.com/facebookresearch/sam3.git'

!nvidia-smi

"""
## Set-up
"""

import os
import sam3
import torch

sam3_root = os.path.join(os.path.dirname(sam3.__file__), "..")

"""
#### Inference and visualization utils
"""

from sam3.model_builder import build_sam3_multiplex_video_predictor

predictor = build_sam3_multiplex_video_predictor()

import glob
import os

import cv2
import matplotlib.pyplot as plt
import numpy as np
from PIL import Image
from sam3.visualization_utils import (
    load_frame,
    prepare_masks_for_visualization,
    visualize_formatted_frame_output,
)

plt.rcParams["axes.titlesize"] = 12
plt.rcParams["figure.titlesize"] = 12


def propagate_in_video(predictor, session_id):
    outputs_per_frame = {}
    for response in predictor.handle_stream_request(
        request=dict(
            type="propagate_in_video",
            session_id=session_id,
        )
    ):
        outputs_per_frame[response["frame_index"]] = response["outputs"]

    return outputs_per_frame


def abs_to_rel_coords(coords, IMG_WIDTH, IMG_HEIGHT, coord_type="point"):
    """Convert absolute coordinates to relative coordinates (0-1 range)

    Args:
        coords: List of coordinates
        coord_type: 'point' for [x, y] or 'box' for [x, y, w, h]
    """
    if coord_type == "point":
        return [[x / IMG_WIDTH, y / IMG_HEIGHT] for x, y in coords]
    elif coord_type == "box":
        return [
            [x / IMG_WIDTH, y / IMG_HEIGHT, w / IMG_WIDTH, h / IMG_HEIGHT]
            for x, y, w, h in coords
        ]
    else:
        raise ValueError(f"Unknown coord_type: {coord_type}")

"""
### Loading an example video

We assume that the video is stored as either **a list of JPEG frames with filenames like `<frame_index>.jpg`** or **an MP4 video**.

Note that you can extract their JPEG frames using ffmpeg (https://ffmpeg.org/) as follows:
```
ffmpeg -i <your_video>.mp4 -q:v 2 -start_number 0 <output_dir>/'%05d.jpg'
```
where `-q:v` generates high-quality JPEG frames and `-start_number 0` asks ffmpeg to start the JPEG file from `00000.jpg`.
"""

# "video_path" needs to be either a JPEG folder or a MP4 video file
video_path = f"{sam3_root}/assets/videos/0001"

# load "video_frames_for_vis" for visualization purposes (they are not used by the model)
if isinstance(video_path, str) and video_path.endswith(".mp4"):
    cap = cv2.VideoCapture(video_path)
    video_frames_for_vis = []
    while True:
        ret, frame = cap.read()
        if not ret:
            break
        video_frames_for_vis.append(cv2.cvtColor(frame, cv2.COLOR_BGR2RGB))
    cap.release()
else:
    video_frames_for_vis = glob.glob(os.path.join(video_path, "*.jpg"))
    try:
        video_frames_for_vis.sort(
            key=lambda p: int(os.path.splitext(os.path.basename(p))[0])
        )
    except ValueError:
        print(
            f'frame names are not in "<frame_index>.jpg" format: {video_frames_for_vis[:5]=}, '
            f"falling back to lexicographic sort."
        )
        video_frames_for_vis.sort()

"""
### Opening an inference session on this video

SAM 3.1 requires stateful inference for interactive video segmentation, so we need to initialize an **inference session** on this video.

During initialization, it loads all the video frames and stores their pixels in the session state.
"""

response = predictor.handle_request(
    request=dict(
        type="start_session",
        resource_path=video_path,
    )
)
session_id = response["session_id"]

"""
### Video promptable concept segmentation with text

Using SAM 3.1 you can describe objects using natural language, and the model will automatically detect and track all instances of that object throughout the video.

In the example below, we add a text prompt on frame 0 and propagation throughout the video. Here we use the text prompt "person" to detect all people in the video. SAM 3.1 will automatically identify multiple person instances and assign each a unique object ID.

Note that the first call might be slower due to setting up buffers. **You can rerun all the cells below when measuring speed.**
"""

# note: in case you already ran one text prompt and now want to switch to another text prompt
# it's required to reset the session first (otherwise the results would be wrong)
_ = predictor.handle_request(
    request=dict(
        type="reset_session",
        session_id=session_id,
    )
)

prompt_text_str = "person"
frame_idx = 0  # add a text prompt on frame 0
response = predictor.handle_request(
    request=dict(
        type="add_prompt",
        session_id=session_id,
        frame_index=frame_idx,
        text=prompt_text_str,
    )
)
out = response["outputs"]

plt.close("all")
visualize_formatted_frame_output(
    frame_idx,
    video_frames_for_vis,
    outputs_list=[prepare_masks_for_visualization({frame_idx: out})],
    titles=["SAM 3.1 Dense Tracking outputs"],
    figsize=(6, 4),
)

# now we propagate the outputs from frame 0 to the end of the video and collect all outputs
outputs_per_frame = propagate_in_video(predictor, session_id)

# finally, we reformat the outputs for visualization and plot the outputs every 60 frames
outputs_per_frame = prepare_masks_for_visualization(outputs_per_frame)

vis_frame_stride = 60
plt.close("all")
for frame_idx in range(0, len(outputs_per_frame), vis_frame_stride):
    visualize_formatted_frame_output(
        frame_idx,
        video_frames_for_vis,
        outputs_list=[outputs_per_frame],
        titles=["SAM 3.1 Dense Tracking outputs"],
        figsize=(6, 4),
    )

"""
###  Removing objects

We can remove individual objects using their id.

As an example, let's remove object 2 (which is the dancer in the front).
"""

# we pick id 2, which is the dancer in the front
obj_id = 2
response = predictor.handle_request(
    request=dict(
        type="remove_object",
        session_id=session_id,
        obj_id=obj_id,
    )
)

# now we propagate the outputs from frame 0 to the end of the video and collect all outputs
outputs_per_frame = propagate_in_video(predictor, session_id)

# finally, we reformat the outputs for visualization and plot the outputs every 60 frames
outputs_per_frame = prepare_masks_for_visualization(outputs_per_frame)

vis_frame_stride = 60
plt.close("all")
for frame_idx in range(0, len(outputs_per_frame), vis_frame_stride):
    visualize_formatted_frame_output(
        frame_idx,
        video_frames_for_vis,
        outputs_list=[outputs_per_frame],
        titles=["SAM 3.1 Dense Tracking outputs"],
        figsize=(6, 4),
    )

"""
### Adding new objects with point prompts

We can add new objects through point prompts.

Assuming that we've changed our mind, and now that we want to add back the dancer in the front (whom we just removed in the step above). We can use interactive clicks to add her back.
"""

sample_img = Image.fromarray(load_frame(video_frames_for_vis[0]))

IMG_WIDTH, IMG_HEIGHT = sample_img.size

# let's add back the dancer via point prompts.
# we will use a single positive click to add the dancer back.

frame_idx = 0
obj_id = 2
points_abs = np.array(
    [
        [760, 550],  # positive click
    ]
)
# positive clicks have label 1, while negative clicks have label 0
labels = np.array([1])

# convert points and labels to tensors; also convert to relative coordinates
points_tensor = torch.tensor(
    abs_to_rel_coords(points_abs, IMG_WIDTH, IMG_HEIGHT, coord_type="point"),
    dtype=torch.float32,
)
points_labels_tensor = torch.tensor(labels, dtype=torch.int32)

response = predictor.handle_request(
    request=dict(
        type="add_prompt",
        session_id=session_id,
        frame_index=frame_idx,
        points=points_tensor,
        point_labels=points_labels_tensor,
        obj_id=obj_id,
    )
)
out = response["outputs"]

plt.close("all")
visualize_formatted_frame_output(
    frame_idx,
    video_frames_for_vis,
    outputs_list=[prepare_masks_for_visualization({frame_idx: out})],
    titles=["SAM 3.1 Dense Tracking outputs"],
    figsize=(6, 4),
    points_list=[points_abs],
    points_labels_list=[labels],
)

# now we propagate the outputs from frame 0 to the end of the video and collect all outputs
outputs_per_frame = propagate_in_video(predictor, session_id)

# finally, we reformat the outputs for visualization and plot the outputs every 60 frames
outputs_per_frame = prepare_masks_for_visualization(outputs_per_frame)

vis_frame_stride = 60
plt.close("all")
for frame_idx in range(0, len(outputs_per_frame), vis_frame_stride):
    visualize_formatted_frame_output(
        frame_idx,
        video_frames_for_vis,
        outputs_list=[outputs_per_frame],
        titles=["SAM 3.1 Dense Tracking outputs"],
        figsize=(6, 4),
    )

"""
### Refining an existing object with point prompts

We can also refine the segmentation mask of an existing object through point prompts.

Assuming that we've changed our mind (again) -- for Object ID 2 (the dancer in the front whom we just added back in the step above), now we only want to segment her T-shirt instead of her whole body. We can adjust the segmentation mask with a few more positive and negative clicks.
"""

# For the dancer in the front, suppose now we only want to segment her T-shirt instead of her whole body
# we will use 2 positive clicks and 2 negative clicks to select her shirt.

refine_object_3 = True

if refine_object_3:
    frame_idx = 0
    obj_id = 3
    points_abs = np.array(
        [
            [800, 135],  # positive click
            [800, 180],  # negative click
        ]
    )
    # positive clicks have label 1, while negative clicks have label 0
    labels = np.array([1, 0])
        
else:
    frame_idx = 0
    obj_id = 2
    points_abs = np.array(
        [
            [740, 450],  # positive click
            [760, 630],  # negative click
            [840, 640],  # negative click
            [760, 550],  # positive click
        ]
    )
    # positive clicks have label 1, while negative clicks have label 0
    labels = np.array([1, 0, 0, 1])

# convert points and labels to tensors; also convert to relative coordinates
points_tensor = torch.tensor(
    abs_to_rel_coords(points_abs, IMG_WIDTH, IMG_HEIGHT, coord_type="point"),
    dtype=torch.float32,
)
points_labels_tensor = torch.tensor(labels, dtype=torch.int32)

response = predictor.handle_request(
    request=dict(
        type="add_prompt",
        session_id=session_id,
        frame_index=frame_idx,
        points=points_tensor,
        point_labels=points_labels_tensor,
        obj_id=obj_id,
    )
)
out = response["outputs"]

plt.close("all")
visualize_formatted_frame_output(
    frame_idx,
    video_frames_for_vis,
    outputs_list=[prepare_masks_for_visualization({frame_idx: out})],
    titles=["SAM 3.1 Dense Tracking outputs"],
    figsize=(6, 4),
    points_list=[points_abs],
    points_labels_list=[labels],
)

# now we propagate the outputs from frame 0 to the end of the video and collect all outputs
outputs_per_frame = propagate_in_video(predictor, session_id)

# finally, we reformat the outputs for visualization and plot the outputs every 60 frames
outputs_per_frame = prepare_masks_for_visualization(outputs_per_frame)

vis_frame_stride = 60
plt.close("all")
for frame_idx in range(0, len(outputs_per_frame), vis_frame_stride):
    visualize_formatted_frame_output(
        frame_idx,
        video_frames_for_vis,
        outputs_list=[outputs_per_frame],
        titles=["SAM 3.1 Dense Tracking outputs"],
        figsize=(6, 4),
    )

"""
### Close session

Each session is tied to a single video. We can close the session after inference to free up its resources.

(Then, you may start a new session on another video.)
"""

_ = predictor.handle_request(
    request=dict(
        type="close_session",
        session_id=session_id,
    )
)



================================================
FILE: examples/sam3_agent.ipynb
================================================
# Jupyter notebook converted to Python script.

# Copyright (c) Meta Platforms, Inc. and affiliates.

"""
# SAM 3 Agent
"""

"""
This notebook shows an example of how an MLLM can use SAM 3 as a tool, i.e., "SAM 3 Agent", to segment more complex text queries such as "the leftmost child wearing blue vest".
"""

"""
## Env Setup
"""

"""
First install `sam3` in your environment using the [installation instructions](https://github.com/facebookresearch/sam3?tab=readme-ov-file#installation) in the repository.
"""

import torch
# turn on tfloat32 for Ampere GPUs
# https://pytorch.org/docs/stable/notes/cuda.html#tensorfloat-32-tf32-on-ampere-devices
torch.backends.cuda.matmul.allow_tf32 = True
torch.backends.cudnn.allow_tf32 = True

# use bfloat16 for the entire notebook. If your card doesn't support it, try float16 instead
torch.autocast("cuda", dtype=torch.bfloat16).__enter__()

# inference mode for the whole notebook. Disable if you need gradients
torch.inference_mode().__enter__()

import os

SAM3_ROOT = os.path.dirname(os.getcwd())
os.chdir(SAM3_ROOT)

# setup GPU to use -  A single GPU is good with the purpose of this demo
os.environ["CUDA_VISIBLE_DEVICES"] = "0"
_ = os.system("nvidia-smi")

"""
## Build SAM3 Model
"""

import sam3
from sam3 import build_sam3_image_model
from sam3.model.sam3_image_processor import Sam3Processor

sam3_root = os.path.dirname(sam3.__file__)
bpe_path = f"{sam3_root}/assets/bpe_simple_vocab_16e6.txt.gz"
model = build_sam3_image_model(bpe_path=bpe_path)
processor = Sam3Processor(model, confidence_threshold=0.5)

"""
## LLM Setup

Config which MLLM to use, it can either be a model served by vLLM that you launch from your own machine or a model is served via external API. If you want to using a vLLM model, we also provided insturctions below.
"""

LLM_CONFIGS = {
    # vLLM-served models
    "qwen3_vl_8b_thinking": {
        "provider": "vllm",
        "model": "Qwen/Qwen3-VL-8B-Thinking",
    },
    # models served via external APIs
    # add your own
}

model = "qwen3_vl_8b_thinking"
LLM_API_KEY = "DUMMY_API_KEY"

llm_config = LLM_CONFIGS[model]
llm_config["api_key"] = LLM_API_KEY
llm_config["name"] = model

# setup API endpoint
if llm_config["provider"] == "vllm":
    LLM_SERVER_URL = "http://0.0.0.0:8001/v1"  # replace this with your vLLM server address as needed
else:
    LLM_SERVER_URL = llm_config["base_url"]

"""
### Setup vLLM server 
This step is only required if you are using a model served by vLLM, skip this step if you are calling LLM using an API like Gemini and GPT.

* Install vLLM (in a separate conda env from SAM 3 to avoid dependency conflicts).
  ```bash
    conda create -n vllm python=3.12
    pip install vllm --extra-index-url https://download.pytorch.org/whl/cu128
  ```
* Start vLLM server on the same machine of this notebook
  ```bash
    # qwen 3 VL 8B thinking
    vllm serve Qwen/Qwen3-VL-8B-Thinking --tensor-parallel-size 4 --allowed-local-media-path / --enforce-eager --port 8001
  ```
"""

"""
## Run SAM3 Agent Inference
"""

from functools import partial
from IPython.display import display, Image
from sam3.agent.client_llm import send_generate_request as send_generate_request_orig
from sam3.agent.client_sam3 import call_sam_service as call_sam_service_orig
from sam3.agent.inference import run_single_image_inference

# prepare input args and run single image inference
image = "assets/images/test_image.jpg"
prompt = "the leftmost child wearing blue vest"
image = os.path.abspath(image)
send_generate_request = partial(send_generate_request_orig, server_url=LLM_SERVER_URL, model=llm_config["model"], api_key=llm_config["api_key"])
call_sam_service = partial(call_sam_service_orig, sam3_processor=processor)
output_image_path = run_single_image_inference(
    image, prompt, llm_config, send_generate_request, call_sam_service,
    debug=True, output_dir="agent_output"
)

# display output
if output_image_path is not None:
    display(Image(filename=output_image_path))



================================================
FILE: examples/sam3_for_sam1_task_example.ipynb
================================================
# Jupyter notebook converted to Python script.

# Copyright (c) Meta Platforms, Inc. and affiliates.

"""
# Interactive Instance Segmentation using SAM 3
"""

"""
Segment Anything Model 3 (SAM 3) predicts instance masks that indicate the desired object given geometric prompts (SAM 1 task).
The `SAM3Image` and `Sam3Processor` classes provide an easy interface to prompt the model. The user first sets an image using the `Sam3Processor.set_image` method, which computes the necessary image embeddings. Then, prompts can be provided via the `predict` method to efficiently predict masks from those prompts. The model can take as input both point and box prompts, as well as masks from the previous iteration of prediction.

This notebook follows the SAM 2 API for interactive image segmentation.

# <a target="_blank" href="https://colab.research.google.com/github/facebookresearch/sam3/blob/main/notebooks/sam3_for_sam1_task_example.ipynb">
#   <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/>
# </a>

"""

"""
## Environment Set-up
"""

"""
First install `sam3` in your environment using the [installation instructions](https://github.com/facebookresearch/sam3?tab=readme-ov-file#installation) in the repository.
"""

"""
## Set-up
"""

"""
Necessary imports and helper functions for displaying points, boxes, and masks.
"""

using_colab = False

if using_colab:
    import torch
    import torchvision
    print("PyTorch version:", torch.__version__)
    print("Torchvision version:", torchvision.__version__)
    print("CUDA is available:", torch.cuda.is_available())
    import sys
    !{sys.executable} -m pip install opencv-python matplotlib scikit-learn
    !{sys.executable} -m pip install 'git+https://github.com/facebookresearch/sam3.git'

import os
# if using Apple MPS, fall back to CPU for unsupported ops
os.environ["PYTORCH_ENABLE_MPS_FALLBACK"] = "1"
import numpy as np
import torch
import matplotlib.pyplot as plt
from PIL import Image
import sam3
sam3_root = os.path.join(os.path.dirname(sam3.__file__), "..")


# select the device for computation
if torch.cuda.is_available():
    device = torch.device("cuda")
elif torch.backends.mps.is_available():
    device = torch.device("mps")
else:
    device = torch.device("cpu")
print(f"using device: {device}")

if device.type == "cuda":
    # use bfloat16 for the entire notebook
    torch.autocast("cuda", dtype=torch.bfloat16).__enter__()
    # turn on tfloat32 for Ampere GPUs (https://pytorch.org/docs/stable/notes/cuda.html#tensorfloat-32-tf32-on-ampere-devices)
    if torch.cuda.get_device_properties(0).major >= 8:
        torch.backends.cuda.matmul.allow_tf32 = True
        torch.backends.cudnn.allow_tf32 = True
elif device.type == "mps":
    print(
        "\nSupport for MPS devices is preliminary. SAM 3 is trained with CUDA and might "
        "give numerically different outputs and sometimes degraded performance on MPS. "
        "See e.g. https://github.com/pytorch/pytorch/issues/84936 for a discussion."
    )

np.random.seed(3)

def show_mask(mask, ax, random_color=False, borders = True):
    if random_color:
        color = np.concatenate([np.random.random(3), np.array([0.6])], axis=0)
    else:
        color = np.array([30/255, 144/255, 255/255, 0.6])
    h, w = mask.shape[-2:]
    mask = mask.astype(np.uint8)
    mask_image =  mask.reshape(h, w, 1) * color.reshape(1, 1, -1)
    if borders:
        import cv2
        contours, _ = cv2.findContours(mask,cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_NONE) 
        # Try to smooth contours
        contours = [cv2.approxPolyDP(contour, epsilon=0.01, closed=True) for contour in contours]
        mask_image = cv2.drawContours(mask_image, contours, -1, (1, 1, 1, 0.5), thickness=2) 
    ax.imshow(mask_image)

def show_points(coords, labels, ax, marker_size=375):
    pos_points = coords[labels==1]
    neg_points = coords[labels==0]
    ax.scatter(pos_points[:, 0], pos_points[:, 1], color='green', marker='*', s=marker_size, edgecolor='white', linewidth=1.25)
    ax.scatter(neg_points[:, 0], neg_points[:, 1], color='red', marker='*', s=marker_size, edgecolor='white', linewidth=1.25)   

def show_box(box, ax):
    x0, y0 = box[0], box[1]
    w, h = box[2] - box[0], box[3] - box[1]
    ax.add_patch(plt.Rectangle((x0, y0), w, h, edgecolor='green', facecolor=(0, 0, 0, 0), lw=2))    

def show_masks(image, masks, scores, point_coords=None, box_coords=None, input_labels=None, borders=True):
    for i, (mask, score) in enumerate(zip(masks, scores)):
        plt.figure(figsize=(10, 10))
        plt.imshow(image)
        show_mask(mask, plt.gca(), borders=borders)
        if point_coords is not None:
            assert input_labels is not None
            show_points(point_coords, input_labels, plt.gca())
        if box_coords is not None:
            # boxes
            show_box(box_coords, plt.gca())
        if len(scores) > 1:
            plt.title(f"Mask {i+1}, Score: {score:.3f}", fontsize=18)
        plt.axis('off')
        plt.show()

"""
## Example image
"""

image = Image.open(f"{sam3_root}/assets/images/truck.jpg")

plt.figure(figsize=(10, 10))
plt.imshow(image)
plt.axis('on')
plt.show()

"""
## Selecting objects with SAM 3
"""

"""
First, load the SAM 3 model. Running on CUDA and using the default model are recommended for best results.
"""

from sam3 import build_sam3_image_model
from sam3.model.sam3_image_processor import Sam3Processor

bpe_path = f"{sam3_root}/assets/bpe_simple_vocab_16e6.txt.gz"
model = build_sam3_image_model(bpe_path=bpe_path, enable_inst_interactivity=True)


"""
Process the image to produce an image embedding by calling `Sam3Processor.set_image`.
"""

processor = Sam3Processor(model)
inference_state = processor.set_image(image)

"""
To select the truck, choose a point on it. Points are input to the model in (x,y) format and come with labels 1 (foreground point) or 0 (background point). Multiple points can be input; here we use only one. The chosen point will be shown as a star on the image.
"""

input_point = np.array([[520, 375]])
input_label = np.array([1])

plt.figure(figsize=(10, 10))
plt.imshow(image)
show_points(input_point, input_label, plt.gca())
plt.axis('on')
plt.show()  

"""
Predict with `SAM3Image.predict_inst`. The model returns masks, quality predictions for those masks, and low resolution mask logits that can be passed to the next iteration of prediction.
"""

masks, scores, logits = model.predict_inst(
    inference_state,
    point_coords=input_point,
    point_labels=input_label,
    multimask_output=True,
)
sorted_ind = np.argsort(scores)[::-1]
masks = masks[sorted_ind]
scores = scores[sorted_ind]
logits = logits[sorted_ind]

"""
With `multimask_output=True` (the default setting), SAM 3 outputs 3 masks, where `scores` gives the model's own estimation of the quality of these masks. This setting is intended for ambiguous input prompts, and helps the model disambiguate different objects consistent with the prompt. When `False`, it will return a single mask. For ambiguous prompts such as a single point, it is recommended to use `multimask_output=True` even if only a single mask is desired; the best single mask can be chosen by picking the one with the highest score returned in `scores`. This will often result in a better mask.
"""

masks.shape  # (number_of_masks) x H x W

show_masks(image, masks, scores, point_coords=input_point, input_labels=input_label, borders=True)

"""
## Specifying a specific object with additional points
"""

"""
The single input point is ambiguous, and the model has returned multiple objects consistent with it. To obtain a single object, multiple points can be provided. If available, a mask from a previous iteration can also be supplied to the model to aid in prediction. When specifying a single object with multiple prompts, a single mask can be requested by setting `multimask_output=False`.
"""

input_point = np.array([[500, 375], [1125, 625]])
input_label = np.array([1, 1])

mask_input = logits[np.argmax(scores), :, :]  # Choose the model's best mask

masks, scores, _ = model.predict_inst(
    inference_state,
    point_coords=input_point,
    point_labels=input_label,
    mask_input=mask_input[None, :, :],
    multimask_output=False,
)

masks.shape

show_masks(image, masks, scores, point_coords=input_point, input_labels=input_label)

"""
To exclude the car and specify just the window, a background point (with label 0, here shown in red) can be supplied.
"""

input_point = np.array([[500, 375], [1125, 625]])
input_label = np.array([1, 0])

mask_input = logits[np.argmax(scores), :, :]  # Choose the model's best mask

masks, scores, _ = model.predict_inst(
    inference_state,
    point_coords=input_point,
    point_labels=input_label,
    mask_input=mask_input[None, :, :],
    multimask_output=False,
)

show_masks(image, masks, scores, point_coords=input_point, input_labels=input_label)

"""
## Specifying a specific object with a box
"""

"""
The model can also take a box as input, provided in xyxy format.
"""

input_box = np.array([425, 600, 700, 875])

masks, scores, _ = model.predict_inst(
    inference_state,
    point_coords=None,
    point_labels=None,
    box=input_box[None, :],
    multimask_output=False,
)

show_masks(image, masks, scores, box_coords=input_box)

"""
## Combining points and boxes
"""

"""
Points and boxes may be combined, just by including both types of prompts to the predictor. Here this can be used to select just the trucks's tire, instead of the entire wheel.
"""

input_box = np.array([425, 600, 700, 875])
input_point = np.array([[575, 750]])
input_label = np.array([0])

masks, scores, logits = model.predict_inst(
    inference_state,
    point_coords=input_point,
    point_labels=input_label,
    box=input_box,
    multimask_output=False,
)

show_masks(image, masks, scores, box_coords=input_box, point_coords=input_point, input_labels=input_label)

"""
## Batched prompt inputs
"""

"""
`SAM3Image` can take multiple input prompts for the same image, using `predict_inst` method. For example, imagine we have several box outputs from an object detector.
"""

input_boxes = np.array([
    [75, 275, 1725, 850],
    [425, 600, 700, 875],
    [1375, 550, 1650, 800],
    [1240, 675, 1400, 750],
])

masks, scores, _ = model.predict_inst(
    inference_state,
    point_coords=None,
    point_labels=None,
    box=input_boxes,
    multimask_output=False,
)

masks.shape  # (batch_size) x (num_predicted_masks_per_input) x H x W

plt.figure(figsize=(10, 10))
plt.imshow(image)
for mask in masks:
    show_mask(mask.squeeze(0), plt.gca(), random_color=True)
for box in input_boxes:
    show_box(box, plt.gca())
plt.axis('off')
plt.show()

"""
## End-to-end batched inference
If all prompts are available in advance, it is possible to run SAM 3 directly in an end-to-end fashion. This also allows batching over images.
"""

image1 = image  # truck.jpg from above
image1_boxes = np.array([
    [75, 275, 1725, 850],
    [425, 600, 700, 875],
    [1375, 550, 1650, 800],
    [1240, 675, 1400, 750],
])

image2 = Image.open(f"{sam3_root}/assets/images/groceries.jpg")
image2_boxes = np.array([
    [450, 170, 520, 350],
    [350, 190, 450, 350],
    [500, 170, 580, 350],
    [580, 170, 640, 350],
])

img_batch = [image1, image2]
boxes_batch = [image1_boxes, image2_boxes]

inference_state = processor.set_image_batch(img_batch)

masks_batch, scores_batch, _ = model.predict_inst_batch(
    inference_state,
    None,
    None, 
    box_batch=boxes_batch, 
    multimask_output=False
)

for image, boxes, masks in zip(img_batch, boxes_batch, masks_batch):
    plt.figure(figsize=(10, 10))
    plt.imshow(image)   
    for mask in masks:
        show_mask(mask.squeeze(0), plt.gca(), random_color=True)
    for box in boxes:
        show_box(box, plt.gca())

"""
Similarly, we can have a batch of point prompts defined over a batch of images
"""

image1 = image  # truck.jpg from above
image1_pts = np.array([
    [[500, 375]],
    [[650, 750]]
    ]) # Bx1x2 where B corresponds to number of objects 
image1_labels = np.array([[1], [1]])

image2_pts = np.array([
    [[400, 300]],
    [[630, 300]],
])
image2_labels = np.array([[1], [1]])

pts_batch = [image1_pts, image2_pts]
labels_batch = [image1_labels, image2_labels]

masks_batch, scores_batch, _ = model.predict_inst_batch(inference_state, pts_batch, labels_batch, box_batch=None, multimask_output=True)

# Select the best single mask per object
best_masks = []
for masks, scores in zip(masks_batch,scores_batch):
    best_masks.append(masks[range(len(masks)), np.argmax(scores, axis=-1)])

for image, points, labels, masks in zip(img_batch, pts_batch, labels_batch, best_masks):
    plt.figure(figsize=(10, 10))
    plt.imshow(image)   
    for mask in masks:
        show_mask(mask, plt.gca(), random_color=True)
    show_points(points, labels, plt.gca())



================================================
FILE: examples/sam3_for_sam2_video_task_example.ipynb
================================================
# Jupyter notebook converted to Python script.

# Copyright (c) Meta Platforms, Inc. and affiliates.

"""
# Video object segmentation with SAM 3
"""

"""
This notebook shows how to use SAM 3 for video object segmentation in videos, illustrating the use of the  `Sam3TrackerPredictor` class.


This notebook follows the SAM 2 API for interactive video segmentation.

<a target="_blank" href="https://colab.research.google.com/github/facebookresearch/sam3/blob/main/notebooks/sam3_for_sam2_video_task_example.ipynb">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/>
</a>
"""

"""
## Environment Set-up
"""

"""
First install `sam3` in your environment using the [installation instructions](https://github.com/facebookresearch/sam3?tab=readme-ov-file#installation) in the repository.
"""

using_colab = False

if using_colab:
    import torch
    import torchvision
    print("PyTorch version:", torch.__version__)
    print("Torchvision version:", torchvision.__version__)
    print("CUDA is available:", torch.cuda.is_available())
    import sys
    !{sys.executable} -m pip install opencv-python matplotlib scikit-learn
    !{sys.executable} -m pip install 'git+https://github.com/facebookresearch/sam3.git'

"""
## Set-up
"""

import torch

# select the device for computation
if torch.cuda.is_available():
    device = torch.device("cuda")
elif torch.backends.mps.is_available():
    device = torch.device("mps")
else:
    device = torch.device("cpu")
print(f"using device: {device}")

if device.type == "cuda":
    # use bfloat16 for the entire notebook
    torch.autocast("cuda", dtype=torch.bfloat16).__enter__()
    # turn on tfloat32 for Ampere GPUs (https://pytorch.org/docs/stable/notes/cuda.html#tensorfloat-32-tf32-on-ampere-devices)
    if torch.cuda.get_device_properties(0).major >= 8:
        torch.backends.cuda.matmul.allow_tf32 = True
        torch.backends.cudnn.allow_tf32 = True

elif device.type == "mps":
    print(
        "\nSupport for MPS devices is preliminary. SAM 3 is trained with CUDA and might "
        "give numerically different outputs and sometimes degraded performance on MPS. "
        "See e.g. https://github.com/pytorch/pytorch/issues/84936 for a discussion."
    )

import glob
import os

import cv2
import matplotlib.pyplot as plt
import numpy as np

import sam3
import torch
from PIL import Image
from sam3.visualization_utils import show_box, show_mask, show_points

# font size for axes titles
plt.rcParams["axes.titlesize"] = 12
plt.rcParams["figure.titlesize"] = 12

sam3_root = os.path.join(os.path.dirname(sam3.__file__), "..")

"""
### Loading the SAM 3 tracking predictor
"""

from sam3.model_builder import build_sam3_video_model

sam3_model = build_sam3_video_model()
predictor = sam3_model.tracker
predictor.backbone = sam3_model.detector.backbone

"""
#### Initialize the inference state
"""

"""
Just like SAM 2, SAM 3 requires stateful inference for interactive video segmentation, so we need to initialize an **inference state** on this video.

During initialization, it loads all the JPEG frames in `video_path` and stores their pixels in `inference_state` (as shown in the progress bar below).
"""

video_path = f"{sam3_root}/assets/videos/bedroom.mp4"
inference_state = predictor.init_state(video_path=video_path)

"""
### Example 1: Segment & track one object
"""

"""
Note: if you have run any previous tracking using this `inference_state`, please reset it first via `clear_all_points_in_video`.

(The cell below is just for illustration; it's not needed to call `clear_all_points_in_video` here as this `inference_state` is just freshly initialized above.)
"""

predictor.clear_all_points_in_video(inference_state)

"""
#### Step 1: Add a first click on a frame
"""

"""
To get started, let's try to segment the child on the left.

Here we make a **positive click** at (x, y) = (210, 350) with label `1`, by sending their coordinates and labels into the `add_new_points` API.

Note: label `1` indicates a *positive click (to add a region)* while label `0` indicates a *negative click (to remove a region)*.
"""

# load the frames for visualization
cap = cv2.VideoCapture(video_path)
video_frames_for_vis = []
while True:
    ret, frame = cap.read()
    if not ret:
        break
    video_frames_for_vis.append(cv2.cvtColor(frame, cv2.COLOR_BGR2RGB))
cap.release()
frame0 = video_frames_for_vis[0]

width, height = frame0.shape[1], frame0.shape[0]

ann_frame_idx = 0  # the frame index we interact with
ann_obj_id = 1  # give a unique id to each object we interact with (it can be any integers)

# Let's add a positive click at (x, y) = (210, 350) to get started
points = np.array([[210, 350]], dtype=np.float32)
# for labels, `1` means positive click and `0` means negative click
labels = np.array([1], np.int32)

rel_points = [[x / width, y / height] for x, y in points]

points_tensor = torch.tensor(rel_points, dtype=torch.float32)
points_labels_tensor = torch.tensor(labels, dtype=torch.int32)

_, out_obj_ids, low_res_masks, video_res_masks = predictor.add_new_points(
    inference_state=inference_state,
    frame_idx=ann_frame_idx,
    obj_id=ann_obj_id,
    points=points_tensor,
    labels=points_labels_tensor,
    clear_old_points=False,
)

# show the results on the current (interacted) frame
plt.figure(figsize=(9, 6))
plt.title(f"frame {ann_frame_idx}")
plt.imshow(frame0)
show_points(points, labels, plt.gca())
show_mask((video_res_masks[0] > 0.0).cpu().numpy(), plt.gca(), obj_id=out_obj_ids[0])

"""
#### Step 2: Add a second click to refine the prediction
"""

"""
Hmm, it seems that although we wanted to segment the child on the left, the model predicts the mask for only the shorts -- this can happen since there is ambiguity from a single click about what the target object should be. We can refine the mask on this frame via another positive click on the child's shirt.

Here we make a **second positive click** at (x, y) = (250, 220) with label `1` to expand the mask.

Note: we need to send **all the clicks and their labels** (i.e. not just the last click) when calling `add_new_points`.
"""

ann_frame_idx = 0  # the frame index we interact with
ann_obj_id = 1  # give a unique id to each object we interact with (it can be any integers)

# Let's add a 2nd positive click at (x, y) = (250, 220) to refine the mask
# sending all clicks (and their labels) to `add_new_points_or_box`
points = np.array([[210, 350], [250, 220]], dtype=np.float32)
# for labels, `1` means positive click and `0` means negative click
labels = np.array([1, 1], np.int32)

rel_points = [[x / width, y / height] for x, y in points]

points_tensor = torch.tensor(rel_points, dtype=torch.float32)
points_labels_tensor = torch.tensor(labels, dtype=torch.int32)

_, out_obj_ids, low_res_masks, video_res_masks  = predictor.add_new_points(
    inference_state=inference_state,
    frame_idx=ann_frame_idx,
    obj_id=ann_obj_id,
    points=points_tensor,
    labels=points_labels_tensor,
    clear_old_points=False,
)

# show the results on the current (interacted) frame
plt.figure(figsize=(9, 6))
plt.title(f"frame {ann_frame_idx}")
plt.imshow(frame0)
show_points(points, labels, plt.gca())
show_mask((video_res_masks[0] > 0.0).cpu().numpy(), plt.gca(), obj_id=out_obj_ids[0])

"""
With this 2nd refinement click, now we get a segmentation mask of the entire child on frame 0.
"""

"""
#### Step 3: Propagate the prompts to get the masklet across the video
"""

"""
To get the masklet throughout the entire video, we propagate the prompts using the `propagate_in_video` API.
"""

# run propagation throughout the video and collect the results in a dict
video_segments = {}  # video_segments contains the per-frame segmentation results
for frame_idx, obj_ids, low_res_masks, video_res_masks, obj_scores in predictor.propagate_in_video(inference_state, start_frame_idx=0, max_frame_num_to_track=240, reverse=False, propagate_preflight=True):
    video_segments[frame_idx] = {
        out_obj_id: (video_res_masks[i] > 0.0).cpu().numpy()
        for i, out_obj_id in enumerate(out_obj_ids)
    }

# render the segmentation results every few frames
vis_frame_stride = 30
plt.close("all")
for out_frame_idx in range(0, len(video_frames_for_vis), vis_frame_stride):
    plt.figure(figsize=(6, 4))
    plt.title(f"frame {out_frame_idx}")
    plt.imshow(video_frames_for_vis[out_frame_idx])
    for out_obj_id, out_mask in video_segments[out_frame_idx].items():
        show_mask(out_mask, plt.gca(), obj_id=out_obj_id)

"""
#### Step 4: Add new prompts to further refine the masklet
"""

"""
It appears that in the output masklet above, there are some small imperfections in boundary details on frame 150.

With SAM 3 we can fix the model predictions interactively. We can add a **negative click** at (x, y) = (82, 415) on this frame with label `0` to refine the masklet. Here we call the `add_new_points_or_box` API with a different `frame_idx` argument to indicate the frame index we want to refine.
"""

ann_frame_idx = 150  # further refine some details on this frame
ann_obj_id = 1  # give a unique id to the object we interact with (it can be any integers)

# show the segment before further refinement
plt.figure(figsize=(9, 6))
plt.title(f"frame {ann_frame_idx} -- before refinement")
plt.imshow(video_frames_for_vis[ann_frame_idx])
show_mask(video_segments[ann_frame_idx][ann_obj_id], plt.gca(), obj_id=ann_obj_id)

# Let's add a negative click on this frame at (x, y) = (82, 415) to refine the segment
points = np.array([[82, 410]], dtype=np.float32)
# for labels, `1` means positive click and `0` means negative click
labels = np.array([0], np.int32)

rel_points = [[x / width, y / height] for x, y in points]

points_tensor = torch.tensor(rel_points, dtype=torch.float32)
points_labels_tensor = torch.tensor(labels, dtype=torch.int32)

_, out_obj_ids, low_res_masks, video_res_masks  = predictor.add_new_points(
    inference_state=inference_state,
    frame_idx=ann_frame_idx,
    obj_id=ann_obj_id,
    points=points_tensor,
    labels=points_labels_tensor,
    clear_old_points=False,
)


# show the segment after the further refinement
plt.figure(figsize=(9, 6))
plt.title(f"frame {ann_frame_idx} -- after refinement")
plt.imshow(video_frames_for_vis[ann_frame_idx])
show_points(points, labels, plt.gca())
show_mask((video_res_masks > 0.0).cpu().numpy(), plt.gca(), obj_id=ann_obj_id)

"""
#### Step 5: Propagate the prompts (again) to get the masklet across the video
"""

"""
Let's get an updated masklet for the entire video. Here we call `propagate_in_video` again to propagate all the prompts after adding the new refinement click above.
"""

# run propagation throughout the video and collect the results in a dict
video_segments = {}  # video_segments contains the per-frame segmentation results
for frame_idx, obj_ids, low_res_masks, video_res_masks, obj_scores in predictor.propagate_in_video(inference_state, start_frame_idx=0, max_frame_num_to_track=300, reverse=False, propagate_preflight=True):
    video_segments[frame_idx] = {
        out_obj_id: (video_res_masks[i] > 0.0).cpu().numpy()
        for i, out_obj_id in enumerate(out_obj_ids)
    }

# render the segmentation results every few frames
vis_frame_stride = 30
plt.close("all")
for out_frame_idx in range(0, len(video_frames_for_vis), vis_frame_stride):
    plt.figure(figsize=(6, 4))
    plt.title(f"frame {out_frame_idx}")
    plt.imshow(video_frames_for_vis[out_frame_idx])
    for out_obj_id, out_mask in video_segments[out_frame_idx].items():
        show_mask(out_mask, plt.gca(), obj_id=out_obj_id)

"""
The segments now look good on all frames.
"""

"""
### Example 2: Segment an object using box prompt
"""

"""
Note: if you have run any previous tracking using this `inference_state`, please reset it first via `clear_all_points_in_video`.
"""

predictor.clear_all_points_in_video(inference_state)

"""
In addition to using clicks as inputs, SAM 3 also supports segmenting and tracking objects in a video via **bounding boxes**.

In the example below, we segment the child on the right using a **box prompt** of (x_min, y_min, x_max, y_max) = (300, 0, 500, 400) on frame 0 as input into the `add_new_points_or_box` API.
"""

ann_frame_idx = 0  # the frame index we interact with
ann_obj_id = 4  # give a unique id to each object we interact with (it can be any integers)

# Let's add a box at (x_min, y_min, x_max, y_max) = (300, 0, 500, 400) to get started
box = np.array([[300, 0, 500, 400]], dtype=np.float32)

rel_box = [[xmin / width, ymin / height, xmax / width, ymax / height] for xmin, ymin, xmax, ymax in box]
rel_box = np.array(rel_box, dtype=np.float32)

_, out_obj_ids, low_res_masks, video_res_masks  = predictor.add_new_points_or_box(
    inference_state=inference_state,
    frame_idx=ann_frame_idx,
    obj_id=ann_obj_id,
    box=rel_box,
)

# show the results on the current (interacted) frame
plt.figure(figsize=(9, 6))
plt.title(f"frame {ann_frame_idx}")
plt.imshow(video_frames_for_vis[ann_frame_idx])
show_box(box[0], plt.gca())
show_mask((video_res_masks[0] > 0.0).cpu().numpy(), plt.gca(), obj_id=ann_obj_id)

"""
Here, SAM 3 gets a pretty good segmentation mask of the entire child, even though the input bounding box is not perfectly tight around the object.

Similar to the previous example, if the returned mask from is not perfect when using a box prompt, we can also further **refine** the output using positive or negative clicks. To illustrate this, here we make a **positive click** at (x, y) = (460, 60) with label `1` to expand the segment around the child's hair.

Note: to refine the segmentation mask from a box prompt, we need to send **both the original box input and all subsequent refinement clicks and their labels** when calling `add_new_points_or_box`.
"""

ann_frame_idx = 0  # the frame index we interact with
ann_obj_id = 4  # give a unique id to each object we interact with (it can be any integers)

# Let's add a positive click at (x, y) = (460, 60) to refine the mask
points = np.array([[460, 60]], dtype=np.float32)
# for labels, `1` means positive click and `0` means negative click
labels = np.array([1], np.int32)
# note that we also need to send the original box input along with
# the new refinement click together into `add_new_points_or_box`
box = np.array([[300, 0, 500, 400]], dtype=np.float32)

rel_box = [[xmin / width, ymin / height, xmax / width, ymax / height] for xmin, ymin, xmax, ymax in box]
rel_box = np.array(rel_box, dtype=np.float32)

rel_points = [[x / width, y / height] for x, y in points]

points_tensor = torch.tensor(rel_points, dtype=torch.float32)
points_labels_tensor = torch.tensor(labels, dtype=torch.int32)

_, out_obj_ids, low_res_masks, video_res_masks  = predictor.add_new_points_or_box(
    inference_state=inference_state,
    frame_idx=ann_frame_idx,
    obj_id=ann_obj_id,
    points=points_tensor,
    labels=points_labels_tensor,
    box=rel_box,
)

# show the results on the current (interacted) frame
plt.figure(figsize=(9, 6))
plt.title(f"frame {ann_frame_idx}")
plt.imshow(video_frames_for_vis[ann_frame_idx])
show_box(box[0], plt.gca())
show_points(points, labels, plt.gca())
show_mask((video_res_masks[0][0] > 0.0).cpu().numpy(), plt.gca(), obj_id=out_obj_ids[0])

"""
Then, to get the masklet throughout the entire video, we propagate the prompts using the `propagate_in_video` API.
"""

# run propagation throughout the video and collect the results in a dict
video_segments = {}  # video_segments contains the per-frame segmentation results
for frame_idx, obj_ids, low_res_masks, video_res_masks, obj_scores in predictor.propagate_in_video(inference_state, start_frame_idx=0, max_frame_num_to_track=300, reverse=False, propagate_preflight=True):
    video_segments[frame_idx] = {
        out_obj_id: (video_res_masks[i] > 0.0).cpu().numpy()
        for i, out_obj_id in enumerate(out_obj_ids)
    }

# render the segmentation results every few frames
vis_frame_stride = 30
plt.close("all")
for out_frame_idx in range(0, len(video_frames_for_vis), vis_frame_stride):
    plt.figure(figsize=(6, 4))
    plt.title(f"frame {out_frame_idx}")
    plt.imshow(video_frames_for_vis[out_frame_idx])
    for out_obj_id, out_mask in video_segments[out_frame_idx].items():
        show_mask(out_mask, plt.gca(), obj_id=out_obj_id)

"""
Note that in addition to clicks or boxes, SAM 3 also supports directly using a **mask prompt** as input via the `add_new_mask` method in the `Sam3TrackerPredictor` class. This can be helpful in e.g. semi-supervised VOS evaluations (see [tools/vos_inference.py](https://github.com/facebookresearch/sam2/blob/main/tools/vos_inference.py) for an example).
"""

"""
### Example 3: Segment multiple objects simultaneously
"""

"""
Note: if you have run any previous tracking using this `inference_state`, please reset it first via `clear_all_points_in_video`.
"""

predictor.clear_all_points_in_video(inference_state)

"""
#### Step 1: Add two objects on a frame
"""

"""
SAM 3 can also segment and track two or more objects at the same time. One way, of course, is to do them one by one. However, it would be more efficient to batch them together (e.g. so that we can share the image features between objects to reduce computation costs).

This time, let's focus on object parts and segment **the shirts of both childen** in this video. Here we add prompts for these two objects and assign each of them a unique object id.
"""

prompts = {}  # hold all the clicks we add for visualization

"""
Add the first object (the left child's shirt) with a **positive click** at (x, y) = (200, 300) on frame 0.

We assign it to object id `2` (it can be arbitrary integers, and only needs to be unique for each object to track), which is passed to the `add_new_points_or_box` API to distinguish the object we are clicking upon.
"""

ann_frame_idx = 0  # the frame index we interact with
ann_obj_id = 2  # give a unique id to each object we interact with (it can be any integers)

# Let's add a positive click at (x, y) = (200, 300) to get started on the first object
points = np.array([[200, 300]], dtype=np.float32)
# for labels, `1` means positive click and `0` means negative click
labels = np.array([1], np.int32)
prompts[ann_obj_id] = points, labels

rel_points = [[x / width, y / height] for x, y in points]
points_tensor = torch.tensor(rel_points, dtype=torch.float32)
points_labels_tensor = torch.tensor(labels, dtype=torch.int32)

_, out_obj_ids, low_res_masks, video_res_masks = predictor.add_new_points_or_box(
    inference_state=inference_state,
    frame_idx=ann_frame_idx,
    obj_id=ann_obj_id,
    points=points_tensor,
    labels=points_labels_tensor,
)


# show the results on the current (interacted) frame
plt.figure(figsize=(9, 6))
plt.title(f"frame {ann_frame_idx}")
plt.imshow(video_frames_for_vis[ann_frame_idx])
for i, out_obj_id in enumerate(out_obj_ids):
    show_points(points, labels, plt.gca())
    show_points(*prompts[out_obj_id], plt.gca())
    show_mask((video_res_masks[i][0] > 0.0).cpu().numpy(), plt.gca(), obj_id=out_obj_id)

"""
Hmm, this time we just want to select the child's shirt, but the model predicts the mask for the entire child. Let's refine the prediction with a **negative click** at (x, y) = (275, 175).
"""

# add the first object
ann_frame_idx = 0  # the frame index we interact with
ann_obj_id = 2  # give a unique id to each object we interact with (it can be any integers)

# Let's add a 2nd negative click at (x, y) = (275, 175) to refine the first object
# sending all clicks (and their labels) to `add_new_points_or_box`
points = np.array([[200, 300], [275, 175]], dtype=np.float32)
# for labels, `1` means positive click and `0` means negative click
labels = np.array([1, 0], np.int32)
prompts[ann_obj_id] = points, labels

rel_points = [[x / width, y / height] for x, y in points]
points_tensor = torch.tensor(rel_points, dtype=torch.float32)
points_labels_tensor = torch.tensor(labels, dtype=torch.int32)


_, out_obj_ids, low_res_masks, video_res_masks  = predictor.add_new_points_or_box(
    inference_state=inference_state,
    frame_idx=ann_frame_idx,
    obj_id=ann_obj_id,
    points=rel_points,
    labels=points_labels_tensor,
)

# show the results on the current (interacted) frame
plt.figure(figsize=(9, 6))
plt.title(f"frame {ann_frame_idx}")
plt.imshow(video_frames_for_vis[ann_frame_idx])
for i, out_obj_id in enumerate(out_obj_ids):
    show_points(points, labels, plt.gca())
    show_points(*prompts[out_obj_id], plt.gca())
    show_mask((video_res_masks[i][0] > 0.0).cpu().numpy(), plt.gca(), obj_id=out_obj_id)

"""
After the 2nd negative click, now we get the left child's shirt as our first object.

Let's move on to the second object (the right child's shirt) with a positive click at (x, y) = (400, 150) on frame 0. Here we assign object id `3` to this second object (it can be arbitrary integers, and only needs to be unique for each object to track).

Note: when there are multiple objects, the `add_new_points_or_box` API will return a list of masks for each object.
"""

ann_frame_idx = 0  # the frame index we interact with
ann_obj_id = 3  # give a unique id to each object we interact with (it can be any integers)

# Let's now move on to the second object we want to track (giving it object id `3`)
# with a positive click at (x, y) = (400, 150)
points = np.array([[400, 150]], dtype=np.float32)
# for labels, `1` means positive click and `0` means negative click
labels = np.array([1], np.int32)
prompts[ann_obj_id] = points, labels

rel_points = [[x / width, y / height] for x, y in points]
points_tensor = torch.tensor(rel_points, dtype=torch.float32)
points_labels_tensor = torch.tensor(labels, dtype=torch.int32)


# `add_new_points_or_box` returns masks for all objects added so far on this interacted frame
_, out_obj_ids, low_res_masks, video_res_masks = predictor.add_new_points_or_box(
    inference_state=inference_state,
    frame_idx=ann_frame_idx,
    obj_id=ann_obj_id,
    points=points_tensor,
    labels=points_labels_tensor,
)

# show the results on the current (interacted) frame on all objects
plt.figure(figsize=(9, 6))
plt.title(f"frame {ann_frame_idx}")
plt.imshow(video_frames_for_vis[ann_frame_idx])
for i, out_obj_id in enumerate(out_obj_ids):
    show_points(points, labels, plt.gca())
    show_points(*prompts[out_obj_id], plt.gca())
    show_mask((video_res_masks[i][0] > 0.0).cpu().numpy(), plt.gca(), obj_id=out_obj_id)

"""
This time the model predicts the mask of the shirt we want to track in just one click. Nice!
"""

"""
#### Step 2: Propagate the prompts to get masklets across the video
"""

"""
Now, we propagate the prompts for both objects to get their masklets throughout the video.

Note: when there are multiple objects, the `propagate_in_video` API will return a list of masks for each object.
"""

# run propagation throughout the video and collect the results in a dict
video_segments = {}  # video_segments contains the per-frame segmentation results
for frame_idx, obj_ids, low_res_masks, video_res_masks, obj_scores in predictor.propagate_in_video(inference_state, start_frame_idx=0, max_frame_num_to_track=300, reverse=False, propagate_preflight=True):
    video_segments[frame_idx] = {
        out_obj_id: (video_res_masks[i] > 0.0).cpu().numpy()
        for i, out_obj_id in enumerate(out_obj_ids)
    }

# render the segmentation results every few frames
vis_frame_stride = 30
plt.close("all")
for out_frame_idx in range(0, len(video_frames_for_vis), vis_frame_stride):
    plt.figure(figsize=(6, 4))
    plt.title(f"frame {out_frame_idx}")
    plt.imshow(video_frames_for_vis[out_frame_idx])
    for out_obj_id, out_mask in video_segments[out_frame_idx].items():
        show_mask(out_mask, plt.gca(), obj_id=out_obj_id)

"""
Looks like both children's shirts are well segmented in this video.

Now you can try SAM 3 on your own videos and use cases! 
"""



================================================
FILE: examples/sam3_image_interactive.ipynb
================================================
# Jupyter notebook converted to Python script.

# Copyright (c) Meta Platforms, Inc. and affiliates.

"""
# <a target="_blank" href="https://colab.research.google.com/github/facebookresearch/sam3/blob/main/notebooks/sam3_image_interactive.ipynb">
#   <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/>
# </a>
"""

using_colab = False

if using_colab:
    import torch
    import torchvision
    print("PyTorch version:", torch.__version__)
    print("Torchvision version:", torchvision.__version__)
    print("CUDA is available:", torch.cuda.is_available())
    import sys
    !{sys.executable} -m pip install opencv-python matplotlib scikit-learn
    !{sys.executable} -m pip install 'git+https://github.com/facebookresearch/sam3.git'

%matplotlib widget

import torch
# turn on tfloat32 for Ampere GPUs
# https://pytorch.org/docs/stable/notes/cuda.html#tensorfloat-32-tf32-on-ampere-devices
torch.backends.cuda.matmul.allow_tf32 = True
torch.backends.cudnn.allow_tf32 = True

# use bfloat16 for the entire notebook. If your card doesn't support it, try float16 instead
torch.autocast("cuda", dtype=torch.bfloat16).__enter__()

# inference mode for the whole notebook. Disable if you need gradients
torch.inference_mode().__enter__()

"""
# Load the model
"""

import sam3
from sam3 import build_sam3_image_model
import os
sam3_root = os.path.join(os.path.dirname(sam3.__file__), "..")
bpe_path = f"{sam3_root}/assets/bpe_simple_vocab_16e6.txt.gz"

model = build_sam3_image_model(bpe_path=bpe_path)

from sam3.model.sam3_image_processor import Sam3Processor
processor = Sam3Processor(model)

"""
# Jupyter widget
"""

import io

import ipywidgets as widgets
import matplotlib.pyplot as plt
import numpy as np
import PIL.Image
import requests
from IPython.display import clear_output, display, HTML
from matplotlib.patches import Rectangle


class Sam3SegmentationWidget:
    """Interactive Jupyter widget for SAM3 segmentation with text and box prompts."""

    def __init__(self, processor):
        """
        Initialize the segmentation widget.

        Args:
            processor: Sam3Processor instance
        """
        self.processor = processor
        self.state = None
        self.current_image = None
        self.current_image_array = None
        self.box_mode = "positive"
        self.drawing_box = False
        self.box_start = None
        self.current_rect = None

        self._setup_ui()
        self._setup_plot()

    def _setup_ui(self):
        """Set up the UI components."""
        self.upload_widget = widgets.FileUpload(
            accept="image/*", multiple=False, description="Upload Image"
        )
        self.upload_widget.observe(self._on_image_upload, names="value")

        self.url_input = widgets.Text(
            placeholder="Or enter image URL",
        )
        self.url_button = widgets.Button(description="Load URL", button_style="info")
        self.url_button.on_click(self._on_load_url)
        url_box = widgets.HBox(
            [self.url_input, self.url_button],
            layout=widgets.Layout(width="100%", justify_content="space-between"),
        )

        self.text_input = widgets.Text(
            placeholder='Enter segmentation prompt (e.g., "person", "dog")',
            continuous_update=False,
        )
        self.text_input.observe(self._on_text_submit, names="value")
        self.text_button = widgets.Button(description="Segment", button_style="success")
        self.text_button.on_click(self._on_text_prompt)
        text_box = widgets.HBox(
            [self.text_input, self.text_button],
            layout=widgets.Layout(width="100%", justify_content="space-between"),
        )

        self.box_mode_buttons = widgets.ToggleButtons(
            options=["Positive Boxes", "Negative Boxes"],
            description="Box Mode:",
            button_style="",
            tooltips=[
                "Draw boxes around objects to include",
                "Draw boxes around objects to exclude",
            ],
        )
        self.box_mode_buttons.observe(self._on_box_mode_change, names="value")

        self.clear_button = widgets.Button(
            description="Clear All Prompts", button_style="warning"
        )
        self.clear_button.on_click(self._on_clear_prompts)

        self.confidence_slider = widgets.FloatSlider(
            value=0.5,
            min=0.0,
            max=1.0,
            step=0.01,
            description="Confidence:",
            continuous_update=False,
            style={"description_width": "initial"},
        )
        self.confidence_slider.observe(self._on_confidence_change, names="value")

        self.size_slider = widgets.IntSlider(
            value=960,
            min=300,
            max=2000,
            step=10,
            description="Image Size:",
            continuous_update=False,
            style={"description_width": "initial"},
        )
        self.size_slider.observe(self._on_size_change, names="value")

        slider_box = widgets.HBox(
            [self.confidence_slider, self.size_slider],
            layout=widgets.Layout(justify_content="space-between"),
        )

        self.output = widgets.Output()
        self.status_label = widgets.Label(value="Upload an image to begin")

        # This box will hold our matplotlib output and we can target it with CSS.
        self.plot_container = widgets.Box([self.output])
        self.plot_container.add_class("no-drag")

        # CSS to make the cursor a crosshair over the matplotlib canvas
        css_style = widgets.HTML(
            """
        <style>
            .jupyter-matplotlib-canvas, canvas {
                cursor: crosshair !important;
            }
        </style>
        """
        )
        # Create VBoxes for each accordion pane
        source_pane = widgets.VBox([self.upload_widget, url_box])
        prompt_pane = widgets.VBox(
            [
                widgets.Label("Text Prompt:"),
                text_box,
                self.box_mode_buttons,
                self.confidence_slider,
                self.clear_button,
            ]
        )
        display_pane = widgets.VBox([self.size_slider])

        # Create the Accordion to hold the control panes
        self.accordion = widgets.Accordion(
            children=[source_pane, prompt_pane, display_pane]
        )
        self.accordion.set_title(0, "Image Source")
        self.accordion.set_title(1, "Segmentation Prompts")
        self.accordion.set_title(2, "Display Settings")
        self.accordion.selected_index = 0  # Start with the first pane open

        # Create the left sidebar for controls
        sidebar = widgets.VBox(
            [self.status_label, widgets.HTML("<h4>Controls</h4>"), self.accordion]
        )
        sidebar.layout = widgets.Layout(
            width="380px",
            min_width="380px",
            max_width="380px",
            border="1px solid #e0e0e0",
            padding="10px",
            margin="0 15px 0 0",
            flex="0 0 auto",
        )

        # Create the main area for the image display
        main_area = widgets.VBox([self.plot_container])
        main_area.layout = widgets.Layout(flex="1", min_width="500px", overflow="auto")

        # Combine sidebar and main area into the final app layout
        app_layout = widgets.HBox([sidebar, main_area])
        app_layout.layout = widgets.Layout(
            width="100%",
            display="flex",
            flex_flow="row",
            align_items="stretch",
        )

        # Set the main container
        self.container = widgets.VBox(
            [
                css_style,
                widgets.HTML("<h3>🖼️ SAM3 Interactive Segmentation</h3>"),
                app_layout,
            ]
        )

    def _setup_plot(self):
        """Set up the matplotlib figure."""
        # plt.ioff()
        self.fig, self.ax = plt.subplots(figsize=(12, 8))
        # plt.ion()
        self.ax.axis("off")
        self.fig.subplots_adjust(left=0, right=1, top=1, bottom=0)
        self.fig.canvas.toolbar_visible = False
        self.fig.canvas.header_visible = False
        self.fig.canvas.footer_visible = False
        self.fig.canvas.resizable = False

        # plt.close(self.fig)

    def _set_loading(self, is_loading, message="Processing..."):
        """Show/hide loading state and disable/enable controls."""
        if is_loading:
            self.status_label.value = f"⏳ {message}"
            self.upload_widget.disabled = True
            self.url_button.disabled = True
            self.text_button.disabled = True
            self.clear_button.disabled = True
            self.box_mode_buttons.disabled = True
            self.confidence_slider.disabled = True
        else:
            self.upload_widget.disabled = False
            self.url_button.disabled = False
            self.text_button.disabled = False
            self.clear_button.disabled = False
            self.box_mode_buttons.disabled = False
            self.confidence_slider.disabled = False

    def _on_image_upload(self, change):
        """Handle image upload."""
        if change["new"]:
            uploaded_file = change["new"][0]
            image = PIL.Image.open(io.BytesIO(uploaded_file["content"])).convert("RGB")
            self._set_image(image)

    def _on_load_url(self, button):
        """Handle loading image from URL."""
        url = self.url_input.value.strip()
        if not url:
            self.status_label.value = "Please enter a URL"
            return

        self._set_loading(True, "Downloading image from URL...")

        try:
            response = requests.get(url, timeout=10)
            response.raise_for_status()
            image = PIL.Image.open(io.BytesIO(response.content)).convert("RGB")
            self._set_image(image)
        except Exception as e:
            self._set_loading(False)
            self.status_label.value = f"Error loading image: {str(e)}"

    def _set_image(self, image):
        """Set the current image, adjust figure size, and initialize state."""
        self._set_loading(True, "Processing image through model...")

        try:

            self.current_image = image
            self.current_image_array = np.array(image)
            self.state = self.processor.set_image(image)
            self._set_loading(False)
            self.status_label.value = (
                f"Image loaded: {image.size[0]}x{image.size[1]} pixels"
            )
            self._resize_figure()
            self._update_display()
            self._connect_plot_events()
            self.accordion.selected_index = 1
        except Exception as e:
            self._set_loading(False)
            self.status_label.value = f"Error processing image: {str(e)}"

    def _on_text_submit(self, change):
        """Handle text prompt submission via Enter key."""
        # Call the same handler as the button click
        self._on_text_prompt(None)

    def _on_text_prompt(self, button):
        """Handle text prompt submission."""
        if self.state is None:
            self.status_label.value = "Please load an image first"
            return

        prompt = self.text_input.value.strip()
        if not prompt:
            self.status_label.value = "Please enter a prompt"
            return

        self._set_loading(True, f'Segmenting with prompt: "{prompt}"...')

        try:
            self.state = self.processor.set_text_prompt(prompt, self.state)
            self._set_loading(False)
            self.status_label.value = f'Segmented with prompt: "{prompt}"'
            self._update_display()
        except Exception as e:
            self._set_loading(False)
            self.status_label.value = f"Error: {str(e)}"

    def _on_box_mode_change(self, change):
        """Handle box mode toggle."""
        self.box_mode = "positive" if change["new"] == "Positive Boxes" else "negative"

    def _on_clear_prompts(self, button):
        """Clear all prompts and reset to image only."""
        if self.current_image is not None:
            try:
                self._set_loading(True, "Clearing prompts and resetting...")
                self.state = self.processor.reset_all_prompts(self.state)
                if "prompted_boxes" in self.state:
                    del self.state["prompted_boxes"]
                self.text_input.value = ""
                self._set_loading(False)
                self.status_label.value = "Cleared all prompts"
                self._update_display()
            except Exception as e:
                self._set_loading(False)
                import traceback

                self.status_label.value = f"Error: {str(e)} {traceback.format_exc()}"

    def _on_confidence_change(self, change):
        """Handle confidence threshold change."""
        if self.state is not None:
            self.state = self.processor.set_confidence_threshold(
                change["new"], self.state
            )
            self._update_display()

    def _connect_plot_events(self):
        """Connect matplotlib event handlers for box drawing."""
        # Disable matplotlib's toolbar navigation to allow custom box drawing
        if hasattr(self.fig.canvas, "toolbar") and self.fig.canvas.toolbar is not None:
            self.fig.canvas.toolbar.pan()
            self.fig.canvas.toolbar.pan()

        self.fig.canvas.mpl_connect("button_press_event", self._on_press)
        self.fig.canvas.mpl_connect("button_release_event", self._on_release)
        self.fig.canvas.mpl_connect("motion_notify_event", self._on_motion)

    def _on_press(self, event):
        """Handle mouse press for box drawing."""
        if event.inaxes != self.ax:
            return
        self.drawing_box = True
        self.box_start = (event.xdata, event.ydata)

    def _on_motion(self, event):
        """Handle mouse motion for box preview."""
        if not self.drawing_box or event.inaxes != self.ax or self.box_start is None:
            return

        if self.current_rect is not None:
            self.current_rect.remove()

        x0, y0 = self.box_start
        x1, y1 = event.xdata, event.ydata
        width = x1 - x0
        height = y1 - y0

        color = "green" if self.box_mode == "positive" else "red"
        self.current_rect = Rectangle(
            (x0, y0),
            width,
            height,
            fill=False,
            edgecolor=color,
            linewidth=2,
            linestyle="--",
        )
        self.ax.add_patch(self.current_rect)
        self.fig.canvas.draw_idle()

    def _on_release(self, event):
        """Handle mouse release to finalize box."""
        if not self.drawing_box or event.inaxes != self.ax or self.box_start is None:
            self.drawing_box = False
            return

        self.drawing_box = False

        if self.current_rect is not None:
            self.current_rect.remove()
            self.current_rect = None

        if self.state is None:
            return

        x0, y0 = self.box_start
        x1, y1 = event.xdata, event.ydata

        x_min = min(x0, x1)
        x_max = max(x0, x1)
        y_min = min(y0, y1)
        y_max = max(y0, y1)

        if abs(x_max - x_min) < 5 or abs(y_max - y_min) < 5:
            return

        # Get image dimensions
        img_h = self.state["original_height"]
        img_w = self.state["original_width"]

        # Convert from xyxy pixel coordinates to cxcywh normalized format
        center_x = (x_min + x_max) / 2.0 / img_w
        center_y = (y_min + y_max) / 2.0 / img_h
        width = (x_max - x_min) / img_w
        height = (y_max - y_min) / img_h

        box = [center_x, center_y, width, height]
        label = self.box_mode == "positive"
        mode_str = "positive" if label else "negative"

        # Store the prompted box in pixel coordinates for display
        if "prompted_boxes" not in self.state:
            self.state["prompted_boxes"] = []
        self.state["prompted_boxes"].append(
            {"box": [x_min, y_min, x_max, y_max], "label": label}
        )

        self._set_loading(True, f"Adding {mode_str} box and re-segmenting...")

        try:
            self.state = self.processor.add_geometric_prompt(box, label, self.state)
            self._set_loading(False)
            self.status_label.value = f"Added {mode_str} box"
            self._update_display()
        except Exception as e:
            self._set_loading(False)
            self.status_label.value = f"Error adding box: {str(e)}"

    def _resize_figure(self):
        """Calculate and apply new figure size based on image and slider value."""
        if self.current_image is None:
            return

        # 1. Get original image dimensions
        img_w, img_h = self.current_image.size

        # 2. The slider's value is now the direct target width for the display
        display_w = float(self.size_slider.value)

        # 3. Calculate the corresponding height to maintain the original aspect ratio
        aspect_ratio = img_h / img_w
        display_h = int(display_w * aspect_ratio)

        # 4. Convert pixel dimensions to inches for Matplotlib and apply
        dpi = self.fig.dpi
        new_figsize = (display_w / dpi, display_h / dpi)
        self.fig.set_size_inches(new_figsize, forward=True)

    def _on_size_change(self, change):
        """Handle a change from the image size slider."""
        if self.current_image is not None:
            self._resize_figure()
            # After resizing the canvas, we must redraw the content
            self._update_display()

    def _update_display(self):
        """Update the display with current results."""
        if self.current_image_array is None:
            return

        with self.output:
            clear_output(wait=True)

            self.ax.clear()
            self.ax.axis("off")
            self.ax.imshow(self.current_image_array)

            if self.state is not None and "masks" in self.state:
                masks = self.state.get("masks", [])
                boxes = self.state.get("boxes", [])
                scores = self.state.get("scores", [])

                if len(masks) > 0:
                    mask_overlay = np.zeros((*self.current_image_array.shape[:2], 4))

                    for i, (mask, box, score) in enumerate(zip(masks, boxes, scores)):
                        mask_np = mask[0].cpu().numpy()

                        color = plt.cm.tab10(i % 10)[:3]
                        mask_overlay[mask_np > 0.5] = (*color, 0.5)

                        x0, y0, x1, y1 = box.cpu().numpy()
                        rect = Rectangle(
                            (x0, y0),
                            x1 - x0,
                            y1 - y0,
                            fill=False,
                            edgecolor=color,
                            linewidth=2,
                        )
                        self.ax.add_patch(rect)

                        self.ax.text(
                            x0,
                            y0 - 5,
                            f"{score:.2f}",
                            color="white",
                            fontsize=10,
                            bbox=dict(
                                facecolor=color, alpha=0.7, edgecolor="none", pad=2
                            ),
                        )

                    self.ax.imshow(mask_overlay)
                    self.status_label.value = f"Found {len(masks)} object(s)"
                else:
                    self.status_label.value = (
                        "No objects found above confidence threshold"
                    )

            # Display prompted boxes with dashed lines
            if self.state is not None and "prompted_boxes" in self.state:
                for prompted_box in self.state["prompted_boxes"]:
                    box_coords = prompted_box["box"]
                    is_positive = prompted_box["label"]

                    x0, y0, x1, y1 = box_coords
                    color = "green" if is_positive else "red"

                    rect = Rectangle(
                        (x0, y0),
                        x1 - x0,
                        y1 - y0,
                        fill=False,
                        edgecolor=color,
                        linewidth=2,
                        linestyle="--",
                    )
                    self.ax.add_patch(rect)

            # display(self.fig.canvas)

    def display(self):
        display(self.container)

    # Add this for more convenient display in notebooks
    def _ipython_display_(self):
        self.display()


"""
# Run!
"""

widget = Sam3SegmentationWidget(processor)
widget.display()
# Output:
#   VBox(children=(HTML(value='\n        <style>\n            .jupyter-matplotlib-canvas, canvas {\n              …
#   Canvas(footer_visible=False, header_visible=False, resizable=False, toolbar=Toolbar(toolitems=[('Home', 'Reset…



================================================
FILE: sam3/__init__.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

from .model_builder import build_sam3_image_model, build_sam3_predictor

__version__ = "0.1.0"

__all__ = ["build_sam3_image_model", "build_sam3_predictor"]



================================================
FILE: sam3/logger.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe
import logging
import os

LOG_LEVELS = {
    "DEBUG": logging.DEBUG,
    "INFO": logging.INFO,
    "WARNING": logging.WARNING,
    "ERROR": logging.ERROR,
    "CRITICAL": logging.CRITICAL,
}


class ColoredFormatter(logging.Formatter):
    """A command line formatter with different colors for each level."""

    def __init__(self):
        super().__init__()
        reset = "\033[0m"
        colors = {
            logging.DEBUG: f"{reset}\033[36m",  # cyan,
            logging.INFO: f"{reset}\033[32m",  # green
            logging.WARNING: f"{reset}\033[33m",  # yellow
            logging.ERROR: f"{reset}\033[31m",  # red
            logging.CRITICAL: f"{reset}\033[35m",  # magenta
        }
        fmt_str = "{color}%(levelname)s %(asctime)s %(process)d %(filename)s:%(lineno)4d:{reset} %(message)s"
        self.formatters = {
            level: logging.Formatter(fmt_str.format(color=color, reset=reset))
            for level, color in colors.items()
        }
        self.default_formatter = self.formatters[logging.INFO]

    def format(self, record):
        formatter = self.formatters.get(record.levelno, self.default_formatter)
        return formatter.format(record)


def get_logger(name, level=logging.INFO):
    """A command line logger."""
    if "LOG_LEVEL" in os.environ:
        level = os.environ["LOG_LEVEL"].upper()
        assert level in LOG_LEVELS, (
            f"Invalid LOG_LEVEL: {level}, must be one of {list(LOG_LEVELS.keys())}"
        )
        level = LOG_LEVELS[level]
    logger = logging.getLogger(name)
    logger.setLevel(level)
    logger.propagate = False
    ch = logging.StreamHandler()
    ch.setLevel(level)
    ch.setFormatter(ColoredFormatter())
    logger.addHandler(ch)
    return logger



================================================
FILE: sam3/model_builder.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

import os
from typing import Optional

import pkg_resources
import torch
import torch.nn as nn
from huggingface_hub import hf_hub_download
from iopath.common.file_io import g_pathmgr
from sam3.model.decoder import (
    DecoupledTransformerDecoderLayerv2,
    SimpleRoPEAttention,
    TransformerDecoder,
    TransformerDecoderLayer,
    TransformerDecoderLayerv2,
    TransformerEncoderCrossAttention,
    TransformerEncoderDecoupledCrossAttention,
)
from sam3.model.encoder import TransformerEncoderFusion, TransformerEncoderLayer
from sam3.model.geometry_encoders import SequenceGeometryEncoder
from sam3.model.maskformer_segmentation import PixelDecoder, UniversalSegmentationHead
from sam3.model.memory import (
    CXBlock,
    SimpleFuser,
    SimpleMaskDownSampler,
    SimpleMaskEncoder,
)
from sam3.model.model_misc import (
    DotProductScoring,
    MLP,
    MultiheadAttentionWrapper as MultiheadAttention,
    TransformerWrapper,
)
from sam3.model.multiplex_utils import MultiplexController
from sam3.model.necks import Sam3DualViTDetNeck, Sam3TriViTDetNeck
from sam3.model.position_encoding import PositionEmbeddingSine
from sam3.model.sam1_task_predictor import SAM3InteractiveImagePredictor
from sam3.model.sam3_image import Sam3Image, Sam3ImageOnVideoMultiGPU
from sam3.model.sam3_tracking_predictor import Sam3TrackerPredictor
from sam3.model.sam3_video_inference import Sam3VideoInferenceWithInstanceInteractivity
from sam3.model.sam3_video_predictor import Sam3VideoPredictorMultiGPU
from sam3.model.text_encoder_ve import VETextEncoder
from sam3.model.tokenizer_ve import SimpleTokenizer
from sam3.model.video_tracking_multiplex import VideoTrackingDynamicMultiplex
from sam3.model.vitdet import ViT
from sam3.model.vl_combiner import SAM3VLBackbone, SAM3VLBackboneTri, TriHeadVisionOnly
from sam3.sam.transformer import RoPEAttention


# Setup TensorFloat-32 for Ampere GPUs if available
def _setup_tf32() -> None:
    """Enable TensorFloat-32 for Ampere GPUs if available."""
    if torch.cuda.is_available():
        device_props = torch.cuda.get_device_properties(0)
        if device_props.major >= 8:
            torch.backends.cuda.matmul.allow_tf32 = True
            torch.backends.cudnn.allow_tf32 = True


_setup_tf32()


def _create_position_encoding(precompute_resolution=None):
    """Create position encoding for visual backbone."""
    return PositionEmbeddingSine(
        num_pos_feats=256,
        normalize=True,
        scale=None,
        temperature=10000,
        precompute_resolution=precompute_resolution,
    )


def _create_vit_backbone(compile_mode=None, use_fa3=False, use_rope_real=False):
    """Create ViT backbone for visual feature extraction."""
    return ViT(
        img_size=1008,
        pretrain_img_size=336,
        patch_size=14,
        embed_dim=1024,
        depth=32,
        num_heads=16,
        mlp_ratio=4.625,
        norm_layer="LayerNorm",
        drop_path_rate=0.1,
        qkv_bias=True,
        use_abs_pos=True,
        tile_abs_pos=True,
        global_att_blocks=(7, 15, 23, 31),
        rel_pos_blocks=(),
        use_rope=True,
        use_interp_rope=True,
        window_size=24,
        pretrain_use_cls_token=True,
        retain_cls_token=False,
        ln_pre=True,
        ln_post=False,
        return_interm_layers=False,
        bias_patch_embed=False,
        compile_mode=compile_mode,
        use_fa3=use_fa3,
        use_rope_real=use_rope_real,
    )


def _create_vit_neck(position_encoding, vit_backbone, enable_inst_interactivity=False):
    """Create ViT neck for feature pyramid."""
    return Sam3DualViTDetNeck(
        position_encoding=position_encoding,
        d_model=256,
        scale_factors=[4.0, 2.0, 1.0, 0.5],
        trunk=vit_backbone,
        add_sam2_neck=enable_inst_interactivity,
    )


def _create_vl_backbone(vit_neck, text_encoder):
    """Create visual-language backbone."""
    return SAM3VLBackbone(visual=vit_neck, text=text_encoder, scalp=1)


def _create_transformer_encoder(use_fa3=False) -> TransformerEncoderFusion:
    """Create transformer encoder with its layer."""
    encoder_layer = TransformerEncoderLayer(
        activation="relu",
        d_model=256,
        dim_feedforward=2048,
        dropout=0.1,
        pos_enc_at_attn=True,
        pos_enc_at_cross_attn_keys=False,
        pos_enc_at_cross_attn_queries=False,
        pre_norm=True,
        self_attention=MultiheadAttention(
            num_heads=8,
            dropout=0.1,
            embed_dim=256,
            batch_first=True,
            use_fa3=use_fa3,
        ),
        cross_attention=MultiheadAttention(
            num_heads=8,
            dropout=0.1,
            embed_dim=256,
            batch_first=True,
            use_fa3=use_fa3,
        ),
    )

    encoder = TransformerEncoderFusion(
        layer=encoder_layer,
        num_layers=6,
        d_model=256,
        num_feature_levels=1,
        frozen=False,
        use_act_checkpoint=True,
        add_pooled_text_to_img_feat=False,
        pool_text_with_mask=True,
    )
    return encoder


def _create_transformer_decoder(use_fa3=False) -> TransformerDecoder:
    """Create transformer decoder with its layer."""
    decoder_layer = TransformerDecoderLayer(
        activation="relu",
        d_model=256,
        dim_feedforward=2048,
        dropout=0.1,
        cross_attention=MultiheadAttention(
            num_heads=8,
            dropout=0.1,
            embed_dim=256,
            use_fa3=use_fa3,
        ),
        n_heads=8,
        use_text_cross_attention=True,
    )

    decoder = TransformerDecoder(
        layer=decoder_layer,
        num_layers=6,
        num_queries=200,
        return_intermediate=True,
        box_refine=True,
        num_o2m_queries=0,
        dac=True,
        boxRPB="log",
        d_model=256,
        frozen=False,
        interaction_layer=None,
        dac_use_selfatt_ln=True,
        resolution=1008,
        stride=14,
        use_act_checkpoint=True,
        presence_token=True,
    )
    return decoder


def _create_dot_product_scoring():
    """Create dot product scoring module."""
    prompt_mlp = MLP(
        input_dim=256,
        hidden_dim=2048,
        output_dim=256,
        num_layers=2,
        dropout=0.1,
        residual=True,
        out_norm=nn.LayerNorm(256),
    )
    return DotProductScoring(d_model=256, d_proj=256, prompt_mlp=prompt_mlp)


def _create_segmentation_head(compile_mode=None, use_fa3=False):
    """Create segmentation head with pixel decoder."""
    pixel_decoder = PixelDecoder(
        num_upsampling_stages=3,
        interpolation_mode="nearest",
        hidden_dim=256,
        compile_mode=compile_mode,
    )

    cross_attend_prompt = MultiheadAttention(
        num_heads=8,
        dropout=0,
        embed_dim=256,
        use_fa3=use_fa3,
    )

    segmentation_head = UniversalSegmentationHead(
        hidden_dim=256,
        upsampling_stages=3,
        aux_masks=False,
        presence_head=False,
        dot_product_scorer=None,
        act_ckpt=True,
        cross_attend_prompt=cross_attend_prompt,
        pixel_decoder=pixel_decoder,
    )
    return segmentation_head


def _create_geometry_encoder():
    """Create geometry encoder with all its components."""
    # Create position encoding for geometry encoder
    geo_pos_enc = _create_position_encoding()
    # Create CX block for fuser
    cx_block = CXBlock(
        dim=256,
        kernel_size=7,
        padding=3,
        layer_scale_init_value=1.0e-06,
        use_dwconv=True,
    )
    # Create geometry encoder layer
    geo_layer = TransformerEncoderLayer(
        activation="relu",
        d_model=256,
        dim_feedforward=2048,
        dropout=0.1,
        pos_enc_at_attn=False,
        pre_norm=True,
        self_attention=MultiheadAttention(
            num_heads=8,
            dropout=0.1,
            embed_dim=256,
            batch_first=False,
        ),
        pos_enc_at_cross_attn_queries=False,
        pos_enc_at_cross_attn_keys=True,
        cross_attention=MultiheadAttention(
            num_heads=8,
            dropout=0.1,
            embed_dim=256,
            batch_first=False,
        ),
    )

    # Create geometry encoder
    input_geometry_encoder = SequenceGeometryEncoder(
        pos_enc=geo_pos_enc,
        encode_boxes_as_points=False,
        points_direct_project=True,
        points_pool=True,
        points_pos_enc=True,
        boxes_direct_project=True,
        boxes_pool=True,
        boxes_pos_enc=True,
        d_model=256,
        num_layers=3,
        layer=geo_layer,
        use_act_ckpt=True,
        add_cls=True,
        add_post_encode_proj=True,
    )
    return input_geometry_encoder


def _create_sam3_model(
    backbone,
    transformer,
    input_geometry_encoder,
    segmentation_head,
    dot_prod_scoring,
    inst_interactive_predictor,
    eval_mode,
):
    """Create the SAM3 image model."""
    common_params = {
        "backbone": backbone,
        "transformer": transformer,
        "input_geometry_encoder": input_geometry_encoder,
        "segmentation_head": segmentation_head,
        "num_feature_levels": 1,
        "o2m_mask_predict": True,
        "dot_prod_scoring": dot_prod_scoring,
        "use_instance_query": False,
        "multimask_output": True,
        "inst_interactive_predictor": inst_interactive_predictor,
    }

    matcher = None
    if not eval_mode:
        from sam3.train.matcher import BinaryHungarianMatcherV2

        matcher = BinaryHungarianMatcherV2(
            focal=True,
            cost_class=2.0,
            cost_bbox=5.0,
            cost_giou=2.0,
            alpha=0.25,
            gamma=2,
            stable=False,
        )
    common_params["matcher"] = matcher
    model = Sam3Image(**common_params)

    return model


def _create_tracker_maskmem_backbone():
    """Create the SAM3 Tracker memory encoder."""
    # Position encoding for mask memory backbone
    position_encoding = PositionEmbeddingSine(
        num_pos_feats=64,
        normalize=True,
        scale=None,
        temperature=10000,
        precompute_resolution=1008,
    )

    # Mask processing components
    mask_downsampler = SimpleMaskDownSampler(
        kernel_size=3, stride=2, padding=1, interpol_size=[1152, 1152]
    )

    cx_block_layer = CXBlock(
        dim=256,
        kernel_size=7,
        padding=3,
        layer_scale_init_value=1.0e-06,
        use_dwconv=True,
    )

    fuser = SimpleFuser(layer=cx_block_layer, num_layers=2)

    maskmem_backbone = SimpleMaskEncoder(
        out_dim=64,
        position_encoding=position_encoding,
        mask_downsampler=mask_downsampler,
        fuser=fuser,
    )

    return maskmem_backbone


def _create_tracker_transformer():
    """Create the SAM3 Tracker transformer components."""
    # Self attention
    self_attention = RoPEAttention(
        embedding_dim=256,
        num_heads=1,
        downsample_rate=1,
        dropout=0.1,
        rope_theta=10000.0,
        feat_sizes=[72, 72],
        use_fa3=False,
        use_rope_real=False,
    )

    # Cross attention
    cross_attention = RoPEAttention(
        embedding_dim=256,
        num_heads=1,
        downsample_rate=1,
        dropout=0.1,
        kv_in_dim=64,
        rope_theta=10000.0,
        feat_sizes=[72, 72],
        rope_k_repeat=True,
        use_fa3=False,
        use_rope_real=False,
    )

    # Encoder layer
    encoder_layer = TransformerDecoderLayerv2(
        cross_attention_first=False,
        activation="relu",
        dim_feedforward=2048,
        dropout=0.1,
        pos_enc_at_attn=False,
        pre_norm=True,
        self_attention=self_attention,
        d_model=256,
        pos_enc_at_cross_attn_keys=True,
        pos_enc_at_cross_attn_queries=False,
        cross_attention=cross_attention,
    )

    # Encoder
    encoder = TransformerEncoderCrossAttention(
        remove_cross_attention_layers=[],
        batch_first=True,
        d_model=256,
        frozen=False,
        pos_enc_at_input=True,
        layer=encoder_layer,
        num_layers=4,
        use_act_checkpoint=False,
    )

    # Transformer wrapper
    transformer = TransformerWrapper(
        encoder=encoder,
        decoder=None,
        d_model=256,
    )

    return transformer


def build_tracker(
    apply_temporal_disambiguation: bool, with_backbone: bool = False, compile_mode=None
) -> Sam3TrackerPredictor:
    """
    Build the SAM3 Tracker module for video tracking.

    Returns:
        Sam3TrackerPredictor: Wrapped SAM3 Tracker module
    """

    # Create model components
    maskmem_backbone = _create_tracker_maskmem_backbone()
    transformer = _create_tracker_transformer()
    backbone = None
    if with_backbone:
        vision_backbone = _create_vision_backbone(compile_mode=compile_mode)
        backbone = SAM3VLBackbone(scalp=1, visual=vision_backbone, text=None)
    # Create the Tracker module
    model = Sam3TrackerPredictor(
        image_size=1008,
        num_maskmem=7,
        backbone=backbone,
        backbone_stride=14,
        transformer=transformer,
        maskmem_backbone=maskmem_backbone,
        # SAM parameters
        multimask_output_in_sam=True,
        # Evaluation
        forward_backbone_per_frame_for_eval=True,
        trim_past_non_cond_mem_for_eval=False,
        # Multimask
        multimask_output_for_tracking=True,
        multimask_min_pt_num=0,
        multimask_max_pt_num=1,
        # Additional settings
        always_start_from_first_ann_frame=False,
        # Mask overlap
        non_overlap_masks_for_mem_enc=False,
        non_overlap_masks_for_output=False,
        max_cond_frames_in_attn=4,
        offload_output_to_cpu_for_eval=False,
        # SAM decoder settings
        sam_mask_decoder_extra_args={
            "dynamic_multimask_via_stability": True,
            "dynamic_multimask_stability_delta": 0.05,
            "dynamic_multimask_stability_thresh": 0.98,
        },
        clear_non_cond_mem_around_input=True,
        fill_hole_area=0,
        use_memory_selection=apply_temporal_disambiguation,
    )

    return model


def _create_text_encoder(bpe_path: str) -> VETextEncoder:
    """Create SAM3 text encoder."""
    tokenizer = SimpleTokenizer(bpe_path=bpe_path)
    return VETextEncoder(
        tokenizer=tokenizer,
        d_model=256,
        width=1024,
        heads=16,
        layers=24,
    )


def _create_vision_backbone(
    compile_mode=None, enable_inst_interactivity=True
) -> Sam3DualViTDetNeck:
    """Create SAM3 visual backbone with ViT and neck."""
    # Position encoding
    position_encoding = _create_position_encoding(precompute_resolution=1008)
    # ViT backbone
    vit_backbone: ViT = _create_vit_backbone(compile_mode=compile_mode)
    vit_neck: Sam3DualViTDetNeck = _create_vit_neck(
        position_encoding,
        vit_backbone,
        enable_inst_interactivity=enable_inst_interactivity,
    )
    # Visual neck
    return vit_neck


def _create_sam3_transformer(
    has_presence_token: bool = True, use_fa3: bool = False
) -> TransformerWrapper:
    """Create SAM3 transformer encoder and decoder."""
    encoder: TransformerEncoderFusion = _create_transformer_encoder(use_fa3=use_fa3)
    decoder: TransformerDecoder = _create_transformer_decoder(use_fa3=use_fa3)

    return TransformerWrapper(encoder=encoder, decoder=decoder, d_model=256)


def _load_checkpoint(model, checkpoint_path):
    """Load model checkpoint from file."""
    with g_pathmgr.open(checkpoint_path, "rb") as f:
        ckpt = torch.load(f, map_location="cpu", weights_only=True)
    if "model" in ckpt and isinstance(ckpt["model"], dict):
        ckpt = ckpt["model"]
    sam3_image_ckpt = {
        k.replace("detector.", ""): v for k, v in ckpt.items() if "detector" in k
    }
    if model.inst_interactive_predictor is not None:
        sam3_image_ckpt.update(
            {
                k.replace("tracker.", "inst_interactive_predictor.model."): v
                for k, v in ckpt.items()
                if "tracker" in k
            }
        )
    missing_keys, _ = model.load_state_dict(sam3_image_ckpt, strict=False)
    if len(missing_keys) > 0:
        print(
            f"loaded {checkpoint_path} and found "
            f"missing and/or unexpected keys:\n{missing_keys=}"
        )


def _setup_device_and_mode(model, device, eval_mode):
    """Setup model device and evaluation mode."""
    if device == "cuda":
        model = model.cuda()
    if eval_mode:
        model.eval()
    return model


def build_sam3_image_model(
    bpe_path=None,
    device="cuda" if torch.cuda.is_available() else "cpu",
    eval_mode=True,
    checkpoint_path=None,
    load_from_HF=True,
    enable_segmentation=True,
    enable_inst_interactivity=False,
    compile=False,
):
    """
    Build SAM3 image model

    Args:
        bpe_path: Path to the BPE tokenizer vocabulary
        device: Device to load the model on ('cuda' or 'cpu')
        eval_mode: Whether to set the model to evaluation mode
        checkpoint_path: Optional path to model checkpoint
        enable_segmentation: Whether to enable segmentation head
        enable_inst_interactivity: Whether to enable instance interactivity (SAM 1 task)
        compile_mode: To enable compilation, set to "default"

    Returns:
        A SAM3 image model
    """
    if bpe_path is None:
        bpe_path = pkg_resources.resource_filename(
            "sam3", "assets/bpe_simple_vocab_16e6.txt.gz"
        )

    # Create visual components
    compile_mode = "default" if compile else None
    vision_encoder = _create_vision_backbone(
        compile_mode=compile_mode, enable_inst_interactivity=enable_inst_interactivity
    )

    # Create text components
    text_encoder = _create_text_encoder(bpe_path)

    # Create visual-language backbone
    backbone = _create_vl_backbone(vision_encoder, text_encoder)

    # Create transformer components
    transformer = _create_sam3_transformer()

    # Create dot product scoring
    dot_prod_scoring = _create_dot_product_scoring()

    # Create segmentation head if enabled
    segmentation_head = (
        _create_segmentation_head(compile_mode=compile_mode)
        if enable_segmentation
        else None
    )

    # Create geometry encoder
    input_geometry_encoder = _create_geometry_encoder()
    if enable_inst_interactivity:
        sam3_pvs_base = build_tracker(apply_temporal_disambiguation=False)
        inst_predictor = SAM3InteractiveImagePredictor(sam3_pvs_base)
    else:
        inst_predictor = None
    # Create the SAM3 model
    model = _create_sam3_model(
        backbone,
        transformer,
        input_geometry_encoder,
        segmentation_head,
        dot_prod_scoring,
        inst_predictor,
        eval_mode,
    )
    if load_from_HF and checkpoint_path is None:
        checkpoint_path = download_ckpt_from_hf(version="sam3")
    # Load checkpoint if provided
    if checkpoint_path is not None:
        _load_checkpoint(model, checkpoint_path)

    # Setup device and mode
    model = _setup_device_and_mode(model, device, eval_mode)

    return model


def download_ckpt_from_hf(version="sam3"):
    """Download model checkpoint from HuggingFace Hub.

    Args:
        version: "sam3" or "sam3.1"
    """
    if version == "sam3.1":
        repo_id = "facebook/sam3.1"
        ckpt_name = "sam3.1_multiplex.pt"
        cfg_name = "config.json"
    else:
        repo_id = "facebook/sam3"
        ckpt_name = "sam3.pt"
        cfg_name = "config.json"
    _ = hf_hub_download(repo_id=repo_id, filename=cfg_name)
    checkpoint_path = hf_hub_download(repo_id=repo_id, filename=ckpt_name)
    return checkpoint_path


def build_sam3_video_model(
    checkpoint_path: Optional[str] = None,
    load_from_HF=True,
    bpe_path: Optional[str] = None,
    has_presence_token: bool = True,
    geo_encoder_use_img_cross_attn: bool = True,
    strict_state_dict_loading: bool = True,
    apply_temporal_disambiguation: bool = True,
    device="cuda" if torch.cuda.is_available() else "cpu",
    compile=False,
) -> Sam3VideoInferenceWithInstanceInteractivity:
    """
    Build SAM3 dense tracking model.

    Args:
        checkpoint_path: Optional path to checkpoint file
        bpe_path: Path to the BPE tokenizer file

    Returns:
        Sam3VideoInferenceWithInstanceInteractivity: The instantiated dense tracking model
    """
    if bpe_path is None:
        bpe_path = pkg_resources.resource_filename(
            "sam3", "assets/bpe_simple_vocab_16e6.txt.gz"
        )

    # Build Tracker module
    tracker = build_tracker(apply_temporal_disambiguation=apply_temporal_disambiguation)

    # Build Detector components
    visual_neck = _create_vision_backbone()
    text_encoder = _create_text_encoder(bpe_path)
    backbone = SAM3VLBackbone(scalp=1, visual=visual_neck, text=text_encoder)
    transformer = _create_sam3_transformer(has_presence_token=has_presence_token)
    segmentation_head: UniversalSegmentationHead = _create_segmentation_head()
    input_geometry_encoder = _create_geometry_encoder()

    # Create main dot product scoring
    main_dot_prod_mlp = MLP(
        input_dim=256,
        hidden_dim=2048,
        output_dim=256,
        num_layers=2,
        dropout=0.1,
        residual=True,
        out_norm=nn.LayerNorm(256),
    )
    main_dot_prod_scoring = DotProductScoring(
        d_model=256, d_proj=256, prompt_mlp=main_dot_prod_mlp
    )

    # Build Detector module
    detector = Sam3ImageOnVideoMultiGPU(
        num_feature_levels=1,
        backbone=backbone,
        transformer=transformer,
        segmentation_head=segmentation_head,
        semantic_segmentation_head=None,
        input_geometry_encoder=input_geometry_encoder,
        use_early_fusion=True,
        use_dot_prod_scoring=True,
        dot_prod_scoring=main_dot_prod_scoring,
        supervise_joint_box_scores=has_presence_token,
    )

    # Build the main SAM3 video model
    if apply_temporal_disambiguation:
        model = Sam3VideoInferenceWithInstanceInteractivity(
            detector=detector,
            tracker=tracker,
            score_threshold_detection=0.5,
            assoc_iou_thresh=0.1,
            det_nms_thresh=0.1,
            new_det_thresh=0.7,
            hotstart_delay=15,
            hotstart_unmatch_thresh=8,
            hotstart_dup_thresh=8,
            suppress_unmatched_only_within_hotstart=True,
            min_trk_keep_alive=-1,
            max_trk_keep_alive=30,
            init_trk_keep_alive=30,
            suppress_overlapping_based_on_recent_occlusion_threshold=0.7,
            suppress_det_close_to_boundary=False,
            fill_hole_area=16,
            recondition_every_nth_frame=16,
            masklet_confirmation_enable=False,
            decrease_trk_keep_alive_for_empty_masklets=False,
            image_size=1008,
            image_mean=(0.5, 0.5, 0.5),
            image_std=(0.5, 0.5, 0.5),
            compile_model=compile,
        )
    else:
        # a version without any heuristics for ablation studies
        model = Sam3VideoInferenceWithInstanceInteractivity(
            detector=detector,
            tracker=tracker,
            score_threshold_detection=0.5,
            assoc_iou_thresh=0.1,
            det_nms_thresh=0.1,
            new_det_thresh=0.7,
            hotstart_delay=0,
            hotstart_unmatch_thresh=0,
            hotstart_dup_thresh=0,
            suppress_unmatched_only_within_hotstart=True,
            min_trk_keep_alive=-1,
            max_trk_keep_alive=30,
            init_trk_keep_alive=30,
            suppress_overlapping_based_on_recent_occlusion_threshold=0.7,
            suppress_det_close_to_boundary=False,
            fill_hole_area=16,
            recondition_every_nth_frame=0,
            masklet_confirmation_enable=False,
            decrease_trk_keep_alive_for_empty_masklets=False,
            image_size=1008,
            image_mean=(0.5, 0.5, 0.5),
            image_std=(0.5, 0.5, 0.5),
            compile_model=compile,
        )

    # Load checkpoint if provided
    if load_from_HF and checkpoint_path is None:
        checkpoint_path = download_ckpt_from_hf(version="sam3")
    if checkpoint_path is not None:
        with g_pathmgr.open(checkpoint_path, "rb") as f:
            ckpt = torch.load(f, map_location="cpu", weights_only=True)
        if "model" in ckpt and isinstance(ckpt["model"], dict):
            ckpt = ckpt["model"]

        missing_keys, unexpected_keys = model.load_state_dict(
            ckpt, strict=strict_state_dict_loading
        )
        if missing_keys:
            print(f"Missing keys: {missing_keys}")
        if unexpected_keys:
            print(f"Unexpected keys: {unexpected_keys}")

    model.to(device=device)
    return model


def build_sam3_video_predictor(*model_args, gpus_to_use=None, **model_kwargs):
    return Sam3VideoPredictorMultiGPU(
        *model_args, gpus_to_use=gpus_to_use, **model_kwargs
    )


def _create_multiplex_maskmem_backbone(multiplex_count=16):
    """Create the multiplex memory encoder with per-object mask channels."""
    position_encoding = PositionEmbeddingSine(
        num_pos_feats=256,
        normalize=True,
        scale=None,
        temperature=10000,
        precompute_resolution=1008,
    )

    mask_downsampler = SimpleMaskDownSampler(
        kernel_size=3,
        stride=2,
        padding=1,
        interpol_size=[1152, 1152],
        multiplex_count=multiplex_count,
        starting_out_chan=4,
        input_channel_multiplier=2,
    )

    cx_block_layer = CXBlock(
        dim=256,
        kernel_size=7,
        padding=3,
        layer_scale_init_value=1.0e-06,
        use_dwconv=True,
    )

    fuser = SimpleFuser(layer=cx_block_layer, num_layers=2)

    maskmem_backbone = SimpleMaskEncoder(
        out_dim=256,
        position_encoding=position_encoding,
        mask_downsampler=mask_downsampler,
        fuser=fuser,
    )

    return maskmem_backbone


def _create_multiplex_transformer(use_fa3=False, use_rope_real=False):
    """Create the decoupled transformer for multiplex memory attention."""
    self_attention_rope = SimpleRoPEAttention(
        d_model=256,
        num_heads=8,
        dropout_p=0.1,
        rope_theta=10000.0,
        feat_sizes=[72, 72],
        use_fa3=use_fa3,
        use_rope_real=use_rope_real,
    )

    cross_attention_rope = SimpleRoPEAttention(
        d_model=256,
        num_heads=8,
        dropout_p=0.1,
        rope_theta=10000.0,
        feat_sizes=[72, 72],
        rope_k_repeat=True,
        use_fa3=use_fa3,
        use_rope_real=use_rope_real,
    )

    encoder_layer = DecoupledTransformerDecoderLayerv2(
        activation="gelu",
        d_model=256,
        num_heads=8,
        dropout=0.1,
        dim_feedforward=2048,
        pos_enc_at_attn=False,
        pre_norm=True,
        pos_enc_at_cross_attn_keys=True,
        pos_enc_at_cross_attn_queries=False,
        self_attention_rope=self_attention_rope,
        cross_attention_rope=cross_attention_rope,
    )

    encoder = TransformerEncoderDecoupledCrossAttention(
        d_model=256,
        frozen=False,
        pos_enc_at_input=True,
        use_image_in_output=False,
        layer=encoder_layer,
        num_layers=4,
        use_act_checkpoint=False,
        batch_first=True,
    )

    transformer = TransformerWrapper(
        encoder=encoder,
        decoder=None,
        d_model=256,
    )

    return transformer


def _create_multiplex_tri_backbone(
    compile_mode=None, use_fa3=False, use_rope_real=False
):
    """Create the TriHead vision backbone for multiplex model."""
    position_encoding = _create_position_encoding(precompute_resolution=1008)
    vit_backbone = _create_vit_backbone(
        compile_mode=compile_mode, use_fa3=use_fa3, use_rope_real=use_rope_real
    )
    tri_neck = Sam3TriViTDetNeck(
        trunk=vit_backbone,
        position_encoding=position_encoding,
        d_model=256,
        scale_factors=[4.0, 2.0, 1.0],
    )
    return tri_neck


def build_sam3_multiplex_video_model(
    checkpoint_path: Optional[str] = None,
    load_from_HF=True,
    multiplex_count: int = 16,
    use_fa3: bool = False,
    use_rope_real: bool = False,
    strict_state_dict_loading: bool = True,
    device="cuda" if torch.cuda.is_available() else "cpu",
    compile=False,
):
    """
    Build SAM3 multiplex video tracking model.

    Args:
        checkpoint_path: Optional path to checkpoint file
        multiplex_count: Number of objects per multiplex bucket
        use_fa3: Whether to use FlashAttention 3
        use_rope_real: Whether to use real-valued RoPE (for compile compat)
        strict_state_dict_loading: Whether to use strict state dict loading
        device: Device to place model on
        compile: Whether to compile model components

    Returns:
        VideoTrackingDynamicMultiplex: The instantiated multiplex tracking model
    """
    # Build multiplex-specific components
    maskmem_backbone = _create_multiplex_maskmem_backbone(
        multiplex_count=multiplex_count
    )
    transformer = _create_multiplex_transformer(
        use_fa3=use_fa3, use_rope_real=use_rope_real
    )
    tri_neck = _create_multiplex_tri_backbone(
        compile_mode="max-autotune" if compile else None
    )
    backbone = TriHeadVisionOnly(
        visual=tri_neck,
        n_features=256,
        scalp=0,
    )
    multiplex_controller = MultiplexController(
        multiplex_count=multiplex_count,
        eval_multiplex_count=multiplex_count,
    )

    # Build the multiplex model (use demo class for init_state and other demo methods)
    from sam3.model.video_tracking_multiplex_demo import Sam3VideoTrackingMultiplexDemo

    model = Sam3VideoTrackingMultiplexDemo(
        backbone=backbone,
        transformer=transformer,
        maskmem_backbone=maskmem_backbone,
        multiplex_controller=multiplex_controller,
        image_size=1008,
        backbone_stride=14,
        num_maskmem=7,
        # Multiplex-specific settings
        use_high_res_features_in_sam=True,
        use_obj_ptrs_in_encoder=True,
        max_obj_ptrs_in_encoder=16,
        add_tpos_enc_to_obj_ptrs=True,
        proj_tpos_enc_in_obj_ptrs=True,
        use_mlp_for_obj_ptr_proj=True,
        pred_obj_scores=True,
        pred_obj_scores_mlp=True,
        fixed_no_obj_ptr=True,
        use_no_obj_ptr=True,
        use_linear_no_obj_ptr=True,
        no_obj_embed_spatial=True,
        sincos_tpos_enc=True,
        # Multimask settings
        multimask_output_in_sam=True,
        multimask_output_for_tracking=True,
        multimask_min_pt_num=0,
        multimask_max_pt_num=1,
        use_multimask_token_for_obj_ptr=True,
        num_multimask_outputs=3,
        # Memory encoder settings
        apply_sigmoid_to_mask_logits_for_mem_enc=True,
        sigmoid_scale_for_mem_enc=2.0,
        sigmoid_bias_for_mem_enc=-1.0,
        non_overlap_masks_for_mem_enc=False,
        # Suppression/conditional embeddings
        add_output_suppression_embeddings=True,
        add_object_conditional_embeddings=False,
        condition_as_mask_input=True,
        condition_as_mask_input_fg=1.0,
        condition_as_mask_input_bg=0.0,
        # Memory settings
        use_maskmem_tpos_v2=True,
        save_image_features=True,
        randomness_fix=True,
        # Interaction settings
        use_mask_input_as_output_without_sam=True,
        directly_add_no_mem_embed=True,
        iou_prediction_use_sigmoid=False,
        forward_backbone_per_frame_for_eval=True,
        offload_output_to_cpu_for_eval=False,
        trim_past_non_cond_mem_for_eval=False,
        max_cond_frames_in_attn=4,
        # Dynamic multiplex settings
        is_dynamic_model=True,
        # SAM mask decoder extra args
        sam_mask_decoder_extra_args={
            "dynamic_multimask_via_stability": True,
            "dynamic_multimask_stability_delta": 0.05,
            "dynamic_multimask_stability_thresh": 0.98,
        },
        compile_all_components=compile,
        use_memory_selection=False,
    )

    # Load checkpoint if provided
    if load_from_HF and checkpoint_path is None:
        checkpoint_path = download_ckpt_from_hf(version="sam3.1")
    if checkpoint_path is not None:
        with g_pathmgr.open(checkpoint_path, "rb") as f:
            ckpt = torch.load(f, map_location="cpu", weights_only=True)
        if "model" in ckpt and isinstance(ckpt["model"], dict):
            ckpt = ckpt["model"]

        missing_keys, unexpected_keys = model.load_state_dict(
            ckpt, strict=strict_state_dict_loading
        )
        if missing_keys:
            print(f"Missing keys: {missing_keys}")
        if unexpected_keys:
            print(f"Unexpected keys: {unexpected_keys}")

    model.to(device=device)
    return model


def build_sam3_multiplex_video_predictor(
    checkpoint_path: Optional[str] = None,
    bpe_path: Optional[str] = None,
    max_num_objects: int = 16,
    multiplex_count: int = 16,
    use_fa3: bool = True,
    use_rope_real: bool = True,
    compile: bool = False,
    warm_up: bool = False,
    session_expiration_sec: int = 1200,
    default_output_prob_thresh: float = 0.5,
    async_loading_frames: bool = True,
):
    """
    Build a fully-initialized Sam3MultiplexVideoPredictor.

    This is the recommended entry point for SAM 3.1 multiplex video tracking.
    It builds the full model stack (tracker + detector + demo model), loads
    the checkpoint, and wraps everything in Sam3MultiplexVideoPredictor with
    handle_request / handle_stream_request API.

    Args:
        checkpoint_path: Path to the merged multiplex checkpoint
        bpe_path: Path to the BPE tokenizer vocabulary
        max_num_objects: Maximum number of tracked objects
        multiplex_count: Number of objects per multiplex bucket
        use_fa3: Whether to use FlashAttention 3
        use_rope_real: Whether to use real-valued RoPE (for compile compat)
        compile: Whether to enable torch.compile on model components
        warm_up: Whether to run warm-up compilation (requires compile=True)
        session_expiration_sec: Session expiration timeout in seconds
        default_output_prob_thresh: Default probability threshold for output masks
        async_loading_frames: Whether to load frames asynchronously

    Returns:
        Sam3MultiplexVideoPredictor: The fully-initialized predictor
    """
    if bpe_path is None:
        bpe_path = pkg_resources.resource_filename(
            "sam3", "assets/bpe_simple_vocab_16e6.txt.gz"
        )

    from sam3.model.sam3_multiplex_base import Sam3MultiplexPredictorWrapper
    from sam3.model.sam3_multiplex_detector import Sam3MultiplexDetector
    from sam3.model.sam3_multiplex_tracking import (
        Sam3MultiplexTrackingWithInteractivity,
    )
    from sam3.model.sam3_multiplex_video_predictor import Sam3MultiplexVideoPredictor

    # Build tracker
    tracker_model = build_sam3_multiplex_video_model(
        checkpoint_path=checkpoint_path,
        load_from_HF=False,
        multiplex_count=multiplex_count,
        use_fa3=use_fa3,
        use_rope_real=use_rope_real,
        compile=False,
        strict_state_dict_loading=False,
    )
    del tracker_model.backbone
    tracker_model.backbone = None

    sam2_predictor = Sam3MultiplexPredictorWrapper(
        model=tracker_model,
        per_obj_inference=False,
        fill_hole_area=0,
        is_multiplex=True,
        is_multiplex_dynamic=True,
    )

    # Build detector
    tri_neck = _create_multiplex_tri_backbone(
        compile_mode=None, use_fa3=use_fa3, use_rope_real=use_rope_real
    )
    text_encoder = _create_text_encoder(bpe_path)
    backbone = SAM3VLBackboneTri(scalp=0, visual=tri_neck, text=text_encoder)
    transformer = _create_sam3_transformer(use_fa3=use_fa3)
    segmentation_head = _create_segmentation_head(use_fa3=use_fa3)
    geometry_encoder = _create_geometry_encoder()
    dot_prod_scoring = _create_dot_product_scoring()

    detector = Sam3MultiplexDetector(
        num_feature_levels=1,
        backbone=backbone,
        transformer=transformer,
        segmentation_head=segmentation_head,
        semantic_segmentation_head=None,
        input_geometry_encoder=geometry_encoder,
        use_early_fusion=True,
        use_dot_prod_scoring=True,
        dot_prod_scoring=dot_prod_scoring,
        supervise_joint_box_scores=True,
        is_multiplex=True,
    )

    # Assemble demo model
    demo_model = Sam3MultiplexTrackingWithInteractivity(
        tracker=sam2_predictor,
        detector=detector,
        score_threshold_detection=0.4,
        det_nms_thresh=0.1,
        det_nms_use_iom=True,
        assoc_iou_thresh=0.1,
        new_det_thresh=0.65,
        hotstart_delay=15,
        hotstart_unmatch_thresh=8,
        hotstart_dup_thresh=8,
        suppress_unmatched_only_within_hotstart=False,
        suppress_overlapping_based_on_recent_occlusion_threshold=0.7,
        suppress_det_close_to_boundary=True,
        fill_hole_area=0,  # OV effectively 0 (Sam3MultiplexTrackerPredictor Hydra override clobbers yaml's 16)
        recondition_every_nth_frame=16,
        use_iom_recondition=True,
        iom_thresh_recondition=0.5,
        masklet_confirmation_enable=True,
        reconstruction_bbox_iou_thresh=-1,
        reconstruction_bbox_det_score=0.8,
        max_num_objects=max_num_objects,
        postprocess_batch_size=16,
        use_batched_grounding=True,
        batched_grounding_batch_size=16,
        max_num_kboxes=0,
        sprinkle_removal_area=0,
        is_multiplex=True,
        image_size=1008,
        image_mean=(0.5, 0.5, 0.5),
        image_std=(0.5, 0.5, 0.5),
        compile_model=compile,
    )

    # Load checkpoint (auto-download from HuggingFace if not provided)
    if checkpoint_path is None:
        checkpoint_path = download_ckpt_from_hf(version="sam3.1")
    if checkpoint_path is not None:
        ckpt = torch.load(checkpoint_path, map_location="cpu", weights_only=True)
        if "model" in ckpt and isinstance(ckpt["model"], dict):
            ckpt = ckpt["model"]
        # Remap checkpoint keys if needed (internal naming -> OSS naming)
        # HF checkpoints are already remapped; local checkpoints may use old naming
        needs_remap = any(
            k.startswith("sam3_model.") or k.startswith("sam2_predictor.") for k in ckpt
        )
        if needs_remap:
            remapped_ckpt = {}
            for k, v in ckpt.items():
                new_k = k
                if k.startswith("sam3_model."):
                    new_k = "detector." + k[len("sam3_model.") :]
                elif k.startswith("sam2_predictor."):
                    new_k = "tracker." + k[len("sam2_predictor.") :]
                remapped_ckpt[new_k] = v
            ckpt = remapped_ckpt
        missing_keys, unexpected_keys = demo_model.load_state_dict(ckpt, strict=False)
        if missing_keys:
            print(f"Missing keys ({len(missing_keys)}): {missing_keys[:10]}...")
        if unexpected_keys:
            print(
                f"Unexpected keys ({len(unexpected_keys)}): {unexpected_keys[:10]}..."
            )

    demo_model.cuda().eval()

    # Wrap in predictor
    predictor = Sam3MultiplexVideoPredictor(
        model=demo_model,
        session_expiration_sec=session_expiration_sec,
        default_output_prob_thresh=default_output_prob_thresh,
        async_loading_frames=async_loading_frames,
        warm_up=warm_up,
    )
    return predictor


def build_sam3_predictor(
    checkpoint_path: Optional[str] = None,
    bpe_path: Optional[str] = None,
    version: str = "sam3.1",  # "sam3" or "sam3.1"
    compile: bool = False,
    warm_up: bool = False,
    # SAM 3.1 specific
    max_num_objects: int = 16,
    multiplex_count: int = 16,
    # Common
    use_fa3: bool = True,
    use_rope_real: bool = True,
    async_loading_frames: bool = True,
    **kwargs,
):
    """
    Build a SAM3 video predictor.

    Args:
        checkpoint_path: Path to model checkpoint
        bpe_path: Path to BPE tokenizer vocabulary
        version: Model version - "sam3" for base or "sam3.1" for multiplex
        compile: Enable torch.compile for ~2x speedup (SAM 3.1 only currently)
        warm_up: Run warm-up compilation passes
        max_num_objects: Maximum tracked objects (SAM 3.1 only)
        multiplex_count: Objects per multiplex bucket (SAM 3.1 only)
        use_fa3: Use Flash Attention 3
        use_rope_real: Use real-valued RoPE
        async_loading_frames: Load video frames asynchronously
        **kwargs: Additional arguments passed to the underlying builder

    Returns:
        A predictor with handle_request() and handle_stream_request() API.
        Both versions support: start_session, add_prompt, propagate_in_video,
        remove_object, reset_session, close_session.

    Example:
        # SAM 3.1 (auto-downloads from HuggingFace):
        predictor = build_sam3_predictor(version="sam3.1", compile=True)

        # SAM 3 (auto-downloads from HuggingFace):
        predictor = build_sam3_predictor(version="sam3")

        # Or with a local checkpoint:
        predictor = build_sam3_predictor(checkpoint_path="path/to/ckpt.pt", version="sam3.1")

        # Both use the same API:
        response = predictor.handle_request({"type": "start_session", "resource_path": video_dir})
        session_id = response["session_id"]
        predictor.handle_request({"type": "add_prompt", "session_id": session_id, "frame_index": 0, "text": "person"})
        for out in predictor.handle_stream_request({"type": "propagate_in_video", "session_id": session_id}):
            masks = out["out_binary_masks"]
    """
    if version == "sam3.1":
        return build_sam3_multiplex_video_predictor(
            checkpoint_path=checkpoint_path,
            bpe_path=bpe_path,
            max_num_objects=max_num_objects,
            multiplex_count=multiplex_count,
            use_fa3=use_fa3,
            use_rope_real=use_rope_real,
            compile=compile,
            warm_up=warm_up,
            async_loading_frames=async_loading_frames,
            **kwargs,
        )
    elif version == "sam3":
        return build_sam3_video_predictor(
            checkpoint_path=checkpoint_path,
            bpe_path=bpe_path,
            compile=compile,
            async_loading_frames=async_loading_frames,
            **kwargs,
        )
    else:
        raise ValueError(f"Unknown version: {version!r}. Use 'sam3' or 'sam3.1'.")



================================================
FILE: sam3/visualization_utils.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe
import json
import os
import subprocess
from pathlib import Path

import cv2
import matplotlib.patches as patches
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import pycocotools.mask as mask_utils
import torch
from matplotlib.colors import to_rgb
from PIL import Image
from skimage.color import lab2rgb, rgb2lab
from sklearn.cluster import KMeans
from torchvision.ops import masks_to_boxes
from tqdm import tqdm


def generate_colors(n_colors=256, n_samples=5000):
    # Step 1: Random RGB samples
    np.random.seed(42)
    rgb = np.random.rand(n_samples, 3)
    # Step 2: Convert to LAB for perceptual uniformity
    # print(f"Converting {n_samples} RGB samples to LAB color space...")
    lab = rgb2lab(rgb.reshape(1, -1, 3)).reshape(-1, 3)
    # print("Conversion to LAB complete.")
    # Step 3: k-means clustering in LAB
    kmeans = KMeans(n_clusters=n_colors, n_init=10)
    # print(f"Fitting KMeans with {n_colors} clusters on {n_samples} samples...")
    kmeans.fit(lab)
    # print("KMeans fitting complete.")
    centers_lab = kmeans.cluster_centers_
    # Step 4: Convert LAB back to RGB
    colors_rgb = lab2rgb(centers_lab.reshape(1, -1, 3)).reshape(-1, 3)
    colors_rgb = np.clip(colors_rgb, 0, 1)
    return colors_rgb


COLORS = generate_colors(n_colors=128, n_samples=5000)


def show_img_tensor(img_batch, vis_img_idx=0):
    MEAN_IMG = np.array([0.5, 0.5, 0.5])
    STD_IMG = np.array([0.5, 0.5, 0.5])
    im_tensor = img_batch[vis_img_idx].detach().cpu()
    assert im_tensor.dim() == 3
    im_tensor = im_tensor.numpy().transpose((1, 2, 0))
    im_tensor = (im_tensor * STD_IMG) + MEAN_IMG
    im_tensor = np.clip(im_tensor, 0, 1)
    plt.imshow(im_tensor)


def draw_box_on_image(image, box, color=(0, 255, 0)):
    """
    Draws a rectangle on a given PIL image using the provided box coordinates in xywh format.
    :param image: PIL.Image - The image on which to draw the rectangle.
    :param box: tuple - A tuple (x, y, w, h) representing the top-left corner, width, and height of the rectangle.
    :param color: tuple - A tuple (R, G, B) representing the color of the rectangle. Default is red.
    :return: PIL.Image - The image with the rectangle drawn on it.
    """
    # Ensure the image is in RGB mode
    image = image.convert("RGB")
    # Unpack the box coordinates
    x, y, w, h = box
    x, y, w, h = int(x), int(y), int(w), int(h)
    # Get the pixel data
    pixels = image.load()
    # Draw the top and bottom edges
    for i in range(x, x + w):
        pixels[i, y] = color
        pixels[i, y + h - 1] = color
        pixels[i, y + 1] = color
        pixels[i, y + h] = color
        pixels[i, y - 1] = color
        pixels[i, y + h - 2] = color
    # Draw the left and right edges
    for j in range(y, y + h):
        pixels[x, j] = color
        pixels[x + 1, j] = color
        pixels[x - 1, j] = color
        pixels[x + w - 1, j] = color
        pixels[x + w, j] = color
        pixels[x + w - 2, j] = color
    return image


def plot_bbox(
    img_height,
    img_width,
    box,
    box_format="XYXY",
    relative_coords=True,
    color="r",
    linestyle="solid",
    text=None,
    ax=None,
):
    if box_format == "XYXY":
        x, y, x2, y2 = box
        w = x2 - x
        h = y2 - y
    elif box_format == "XYWH":
        x, y, w, h = box
    elif box_format == "CxCyWH":
        cx, cy, w, h = box
        x = cx - w / 2
        y = cy - h / 2
    else:
        raise RuntimeError(f"Invalid box_format {box_format}")

    if relative_coords:
        x *= img_width
        w *= img_width
        y *= img_height
        h *= img_height

    if ax is None:
        ax = plt.gca()
    rect = patches.Rectangle(
        (x, y),
        w,
        h,
        linewidth=1.5,
        edgecolor=color,
        facecolor="none",
        linestyle=linestyle,
    )
    ax.add_patch(rect)
    if text is not None:
        facecolor = "w"
        ax.text(
            x,
            y - 5,
            text,
            color=color,
            weight="bold",
            fontsize=8,
            bbox={"facecolor": facecolor, "alpha": 0.75, "pad": 2},
        )


def plot_mask(mask, color="r", ax=None):
    im_h, im_w = mask.shape
    mask_img = np.zeros((im_h, im_w, 4), dtype=np.float32)
    mask_img[..., :3] = to_rgb(color)
    mask_img[..., 3] = mask * 0.5
    # Use the provided ax or the current axis
    if ax is None:
        ax = plt.gca()
    ax.imshow(mask_img)


def normalize_bbox(bbox_xywh, img_w, img_h):
    # Assumes bbox_xywh is in XYWH format
    if isinstance(bbox_xywh, list):
        assert len(bbox_xywh) == 4, (
            "bbox_xywh list must have 4 elements. Batching not support except for torch tensors."
        )
        normalized_bbox = bbox_xywh.copy()
        normalized_bbox[0] /= img_w
        normalized_bbox[1] /= img_h
        normalized_bbox[2] /= img_w
        normalized_bbox[3] /= img_h
    else:
        assert isinstance(bbox_xywh, torch.Tensor), (
            "Only torch tensors are supported for batching."
        )
        normalized_bbox = bbox_xywh.clone()
        assert normalized_bbox.size(-1) == 4, (
            "bbox_xywh tensor must have last dimension of size 4."
        )
        normalized_bbox[..., 0] /= img_w
        normalized_bbox[..., 1] /= img_h
        normalized_bbox[..., 2] /= img_w
        normalized_bbox[..., 3] /= img_h
    return normalized_bbox


def visualize_frame_output(frame_idx, video_frames, outputs, figsize=(12, 8)):
    plt.figure(figsize=figsize)
    plt.title(f"frame {frame_idx}")
    img = load_frame(video_frames[frame_idx])
    img_H, img_W, _ = img.shape
    plt.imshow(img)
    for i in range(len(outputs["out_probs"])):
        box_xywh = outputs["out_boxes_xywh"][i]
        prob = outputs["out_probs"][i]
        obj_id = outputs["out_obj_ids"][i]
        binary_mask = outputs["out_binary_masks"][i]
        color = COLORS[obj_id % len(COLORS)]
        plot_bbox(
            img_H,
            img_W,
            box_xywh,
            text=f"(id={obj_id}, {prob=:.2f})",
            box_format="XYWH",
            color=color,
        )
        plot_mask(binary_mask, color=color)


def visualize_formatted_frame_output(
    frame_idx,
    video_frames,
    outputs_list,
    titles=None,
    points_list=None,
    points_labels_list=None,
    figsize=(12, 8),
    title_suffix="",
    prompt_info=None,
):
    """Visualize up to three sets of segmentation masks on a video frame.

    Args:
        frame_idx: Frame index to visualize
        image_files: List of image file paths
        outputs_list: List of {frame_idx: {obj_id: mask_tensor}} or single dict {obj_id: mask_tensor}
        titles: List of titles for each set of outputs_list
        points_list: Optional list of point coordinates
        points_labels_list: Optional list of point labels
        figsize: Figure size tuple
        save: Whether to save the visualization to file
        output_dir: Base output directory when saving
        scenario_name: Scenario name for organizing saved files
        title_suffix: Additional title suffix
        prompt_info: Dictionary with prompt information (boxes, points, etc.)
    """
    # Handle single output dict case
    if isinstance(outputs_list, dict) and frame_idx in outputs_list:
        # This is a single outputs dict with frame indices as keys
        outputs_list = [outputs_list]
    elif isinstance(outputs_list, dict) and not any(
        isinstance(k, int) for k in outputs_list.keys()
    ):
        # This is a single frame's outputs {obj_id: mask}
        single_frame_outputs = {frame_idx: outputs_list}
        outputs_list = [single_frame_outputs]

    num_outputs = len(outputs_list)
    if titles is None:
        titles = [f"Set {i + 1}" for i in range(num_outputs)]
    assert len(titles) == num_outputs, (
        "length of `titles` should match that of `outputs_list` if not None."
    )

    _, axes = plt.subplots(1, num_outputs, figsize=figsize)
    if num_outputs == 1:
        axes = [axes]  # Make it iterable

    img = load_frame(video_frames[frame_idx])
    img_H, img_W, _ = img.shape

    for idx in range(num_outputs):
        ax, outputs_set, ax_title = axes[idx], outputs_list[idx], titles[idx]
        ax.set_title(f"Frame {frame_idx} - {ax_title}{title_suffix}")
        ax.imshow(img)

        if frame_idx in outputs_set:
            _outputs = outputs_set[frame_idx]
        else:
            print(f"Warning: Frame {frame_idx} not found in outputs_set")
            continue

        if prompt_info and frame_idx == 0:  # Show prompts on first frame
            if "boxes" in prompt_info:
                for box in prompt_info["boxes"]:
                    # box is in [x, y, w, h] normalized format
                    x, y, w, h = box
                    plot_bbox(
                        img_H,
                        img_W,
                        [x, y, x + w, y + h],  # Convert to XYXY
                        box_format="XYXY",
                        relative_coords=True,
                        color="yellow",
                        linestyle="dashed",
                        text="PROMPT BOX",
                        ax=ax,
                    )

            if "points" in prompt_info and "point_labels" in prompt_info:
                points = np.array(prompt_info["points"])
                labels = np.array(prompt_info["point_labels"])
                # Convert normalized to pixel coordinates
                points_pixel = points * np.array([img_W, img_H])

                # Draw positive points (green stars)
                pos_points = points_pixel[labels == 1]
                if len(pos_points) > 0:
                    ax.scatter(
                        pos_points[:, 0],
                        pos_points[:, 1],
                        color="lime",
                        marker="*",
                        s=200,
                        edgecolor="white",
                        linewidth=2,
                        label="Positive Points",
                        zorder=10,
                    )

                # Draw negative points (red stars)
                neg_points = points_pixel[labels == 0]
                if len(neg_points) > 0:
                    ax.scatter(
                        neg_points[:, 0],
                        neg_points[:, 1],
                        color="red",
                        marker="*",
                        s=200,
                        edgecolor="white",
                        linewidth=2,
                        label="Negative Points",
                        zorder=10,
                    )

        objects_drawn = 0
        for obj_id, binary_mask in _outputs.items():
            mask_sum = (
                binary_mask.sum()
                if hasattr(binary_mask, "sum")
                else np.sum(binary_mask)
            )

            if mask_sum > 0:  # Only draw if mask has content
                # Convert to torch tensor if it's not already
                if not isinstance(binary_mask, torch.Tensor):
                    binary_mask = torch.tensor(binary_mask)

                # Find bounding box from mask
                if binary_mask.any():
                    box_xyxy = masks_to_boxes(binary_mask.unsqueeze(0)).squeeze()
                    box_xyxy = normalize_bbox(box_xyxy, img_W, img_H)
                else:
                    # Fallback: create a small box at center
                    box_xyxy = [0.45, 0.45, 0.55, 0.55]

                color = COLORS[obj_id % len(COLORS)]

                plot_bbox(
                    img_H,
                    img_W,
                    box_xyxy,
                    text=f"(id={obj_id})",
                    box_format="XYXY",
                    color=color,
                    ax=ax,
                )

                # Convert back to numpy for plotting
                mask_np = (
                    binary_mask.numpy()
                    if isinstance(binary_mask, torch.Tensor)
                    else binary_mask
                )
                plot_mask(mask_np, color=color, ax=ax)
                objects_drawn += 1

        if objects_drawn == 0:
            ax.text(
                0.5,
                0.5,
                "No objects detected",
                transform=ax.transAxes,
                fontsize=16,
                ha="center",
                va="center",
                color="red",
                weight="bold",
            )

        # Draw additional points if provided
        if points_list is not None and points_list[idx] is not None:
            show_points(
                points_list[idx], points_labels_list[idx], ax=ax, marker_size=200
            )

        ax.axis("off")

    plt.tight_layout()
    plt.show()


def render_masklet_frame(img, outputs, frame_idx=None, alpha=0.5):
    """
    Overlays masklets and bounding boxes on a single image frame.
    Args:
        img: np.ndarray, shape (H, W, 3), uint8 or float32 in [0,255] or [0,1]
        outputs: dict with keys: out_boxes_xywh, out_probs, out_obj_ids, out_binary_masks
        frame_idx: int or None, for overlaying frame index text
        alpha: float, mask overlay alpha
    Returns:
        overlay: np.ndarray, shape (H, W, 3), uint8
    """
    if img.dtype == np.float32 or img.max() <= 1.0:
        img = (img * 255).astype(np.uint8)
    img = img[..., :3]  # drop alpha if present
    height, width = img.shape[:2]
    overlay = img.copy()

    for i in range(len(outputs["out_probs"])):
        obj_id = outputs["out_obj_ids"][i]
        color = COLORS[obj_id % len(COLORS)]
        color255 = (color * 255).astype(np.uint8)
        mask = outputs["out_binary_masks"][i]
        if mask.shape != img.shape[:2]:
            mask = cv2.resize(
                mask.astype(np.float32),
                (img.shape[1], img.shape[0]),
                interpolation=cv2.INTER_NEAREST,
            )
        mask_bool = mask > 0.5
        for c in range(3):
            overlay[..., c][mask_bool] = (
                alpha * color255[c] + (1 - alpha) * overlay[..., c][mask_bool]
            ).astype(np.uint8)

    # Draw bounding boxes and text
    for i in range(len(outputs["out_probs"])):
        box_xywh = outputs["out_boxes_xywh"][i]
        obj_id = outputs["out_obj_ids"][i]
        prob = outputs["out_probs"][i]
        color = COLORS[obj_id % len(COLORS)]
        color255 = tuple(int(x * 255) for x in color)
        x, y, w, h = box_xywh
        x1 = int(x * width)
        y1 = int(y * height)
        x2 = int((x + w) * width)
        y2 = int((y + h) * height)
        cv2.rectangle(overlay, (x1, y1), (x2, y2), color255, 2)
        if prob is not None:
            label = f"id={obj_id}, p={prob:.2f}"
        else:
            label = f"id={obj_id}"
        cv2.putText(
            overlay,
            label,
            (x1, max(y1 - 10, 0)),
            cv2.FONT_HERSHEY_SIMPLEX,
            0.5,
            color255,
            1,
            cv2.LINE_AA,
        )

    # Overlay frame index at the top-left corner
    if frame_idx is not None:
        cv2.putText(
            overlay,
            f"Frame {frame_idx}",
            (10, 30),
            cv2.FONT_HERSHEY_SIMPLEX,
            1.0,
            (255, 255, 255),
            2,
            cv2.LINE_AA,
        )

    return overlay


def save_masklet_video(video_frames, outputs, out_path, alpha=0.5, fps=10):
    # Each outputs dict has keys: "out_boxes_xywh", "out_probs", "out_obj_ids", "out_binary_masks"
    # video_frames: list of video frame data, same length as outputs_list

    # Read first frame to get size
    first_img = load_frame(video_frames[0])
    height, width = first_img.shape[:2]
    if first_img.dtype == np.float32 or first_img.max() <= 1.0:
        first_img = (first_img * 255).astype(np.uint8)
    # Use 'mp4v' for best compatibility with VSCode playback (.mp4 files)
    fourcc = cv2.VideoWriter_fourcc(*"mp4v")
    writer = cv2.VideoWriter("temp.mp4", fourcc, fps, (width, height))

    outputs_list = [
        (video_frames[frame_idx], frame_idx, outputs[frame_idx])
        for frame_idx in sorted(outputs.keys())
    ]

    for frame, frame_idx, frame_outputs in tqdm(outputs_list):
        img = load_frame(frame)
        overlay = render_masklet_frame(
            img, frame_outputs, frame_idx=frame_idx, alpha=alpha
        )
        writer.write(cv2.cvtColor(overlay, cv2.COLOR_RGB2BGR))

    writer.release()

    # Re-encode the video for VSCode compatibility using ffmpeg
    subprocess.run(["ffmpeg", "-y", "-i", "temp.mp4", out_path])
    print(f"Re-encoded video saved to {out_path}")

    os.remove("temp.mp4")  # Clean up temporary file


def save_masklet_image(frame, outputs, out_path, alpha=0.5, frame_idx=None):
    """
    Save a single image with masklet overlays.
    """
    img = load_frame(frame)
    overlay = render_masklet_frame(img, outputs, frame_idx=frame_idx, alpha=alpha)
    Image.fromarray(overlay).save(out_path)
    print(f"Overlay image saved to {out_path}")


def prepare_masks_for_visualization(frame_to_output):
    # frame_to_obj_masks --> {frame_idx: {'output_probs': np.array, `out_obj_ids`: np.array, `out_binary_masks`: np.array}}
    for frame_idx, out in frame_to_output.items():
        _processed_out = {}
        for idx, obj_id in enumerate(out["out_obj_ids"].tolist()):
            if out["out_binary_masks"][idx].any():
                _processed_out[obj_id] = out["out_binary_masks"][idx]
        frame_to_output[frame_idx] = _processed_out
    return frame_to_output


def convert_coco_to_masklet_format(
    annotations, img_info, is_prediction=False, score_threshold=0.5
):
    """
    Convert COCO format annotations to format expected by render_masklet_frame
    """
    outputs = {
        "out_boxes_xywh": [],
        "out_probs": [],
        "out_obj_ids": [],
        "out_binary_masks": [],
    }

    img_h, img_w = img_info["height"], img_info["width"]

    for idx, ann in enumerate(annotations):
        # Get bounding box in relative XYWH format
        if "bbox" in ann:
            bbox = ann["bbox"]
            if max(bbox) > 1.0:  # Convert absolute to relative coordinates
                bbox = [
                    bbox[0] / img_w,
                    bbox[1] / img_h,
                    bbox[2] / img_w,
                    bbox[3] / img_h,
                ]
        else:
            mask = mask_utils.decode(ann["segmentation"])
            rows = np.any(mask, axis=1)
            cols = np.any(mask, axis=0)
            if np.any(rows) and np.any(cols):
                rmin, rmax = np.where(rows)[0][[0, -1]]
                cmin, cmax = np.where(cols)[0][[0, -1]]
                # Convert to relative XYWH
                bbox = [
                    cmin / img_w,
                    rmin / img_h,
                    (cmax - cmin + 1) / img_w,
                    (rmax - rmin + 1) / img_h,
                ]
            else:
                bbox = [0, 0, 0, 0]

        outputs["out_boxes_xywh"].append(bbox)

        # Get probability/score
        if is_prediction:
            prob = ann["score"]
        else:
            prob = 1.0  # GT has no probability
        outputs["out_probs"].append(prob)

        outputs["out_obj_ids"].append(idx)
        mask = mask_utils.decode(ann["segmentation"])
        mask = (mask > score_threshold).astype(np.uint8)

        outputs["out_binary_masks"].append(mask)

    return outputs


def save_side_by_side_visualization(img, gt_anns, pred_anns, noun_phrase):
    """
    Create side-by-side visualization of GT and predictions
    """

    # Create side-by-side visualization
    fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(14, 7))

    main_title = f"Noun phrase: '{noun_phrase}'"
    fig.suptitle(main_title, fontsize=16, fontweight="bold")

    gt_overlay = render_masklet_frame(img, gt_anns, alpha=0.5)
    ax1.imshow(gt_overlay)
    ax1.set_title("Ground Truth", fontsize=14, fontweight="bold")
    ax1.axis("off")

    pred_overlay = render_masklet_frame(img, pred_anns, alpha=0.5)
    ax2.imshow(pred_overlay)
    ax2.set_title("Predictions", fontsize=14, fontweight="bold")
    ax2.axis("off")

    plt.subplots_adjust(top=0.88)
    plt.tight_layout()


def bitget(val, idx):
    return (val >> idx) & 1


def pascal_color_map():
    colormap = np.zeros((512, 3), dtype=int)
    ind = np.arange(512, dtype=int)
    for shift in reversed(list(range(8))):
        for channel in range(3):
            colormap[:, channel] |= bitget(ind, channel) << shift
        ind >>= 3

    return colormap.astype(np.uint8)


def draw_masks_to_frame(
    frame: np.ndarray, masks: np.ndarray, colors: np.ndarray
) -> np.ndarray:
    masked_frame = frame
    for mask, color in zip(masks, colors):
        curr_masked_frame = np.where(mask[..., None], color, masked_frame)
        masked_frame = cv2.addWeighted(masked_frame, 0.75, curr_masked_frame, 0.25, 0)

        if int(cv2.__version__[0]) > 3:
            contours, _ = cv2.findContours(
                np.array(mask, dtype=np.uint8).copy(),
                cv2.RETR_TREE,
                cv2.CHAIN_APPROX_NONE,
            )
        else:
            _, contours, _ = cv2.findContours(
                np.array(mask, dtype=np.uint8).copy(),
                cv2.RETR_TREE,
                cv2.CHAIN_APPROX_NONE,
            )

        cv2.drawContours(
            masked_frame, contours, -1, (255, 255, 255), 7
        )  # White outer contour
        cv2.drawContours(
            masked_frame, contours, -1, (0, 0, 0), 5
        )  # Black middle contour
        cv2.drawContours(
            masked_frame, contours, -1, color.tolist(), 3
        )  # Original color inner contour
    return masked_frame


def get_annot_df(file_path: str):
    with open(file_path, "r") as f:
        data = json.load(f)

    dfs = {}

    for k, v in data.items():
        if k in ("info", "licenses"):
            dfs[k] = v
            continue
        df = pd.DataFrame(v)
        dfs[k] = df

    return dfs


def get_annot_dfs(file_list: list[str]):
    dfs = {}
    for annot_file in tqdm(file_list):
        dataset_name = Path(annot_file).stem
        dfs[dataset_name] = get_annot_df(annot_file)

    return dfs


def get_media_dir(media_dir: str, dataset: str):
    if dataset in ["saco_veval_sav_test", "saco_veval_sav_val"]:
        return os.path.join(media_dir, "saco_sav", "JPEGImages_24fps")
    elif dataset in ["saco_veval_yt1b_test", "saco_veval_yt1b_val"]:
        return os.path.join(media_dir, "saco_yt1b", "JPEGImages_6fps")
    elif dataset in ["saco_veval_smartglasses_test", "saco_veval_smartglasses_val"]:
        return os.path.join(media_dir, "saco_sg", "JPEGImages_6fps")
    elif dataset == "sa_fari_test":
        return os.path.join(media_dir, "sa_fari", "JPEGImages_6fps")
    else:
        raise ValueError(f"Dataset {dataset} not found")


def get_all_annotations_for_frame(
    dataset_df: pd.DataFrame, video_id: int, frame_idx: int, data_dir: str, dataset: str
):
    media_dir = os.path.join(data_dir, "media")

    # Load the annotation and video data
    annot_df = dataset_df["annotations"]
    video_df = dataset_df["videos"]

    # Get the frame
    video_df_current = video_df[video_df.id == video_id]
    assert len(video_df_current) == 1, (
        f"Expected 1 video row, got {len(video_df_current)}"
    )
    video_row = video_df_current.iloc[0]
    file_name = video_row.file_names[frame_idx]
    file_path = os.path.join(
        get_media_dir(media_dir=media_dir, dataset=dataset), file_name
    )
    frame = cv2.imread(file_path)
    frame = cv2.cvtColor(frame, cv2.COLOR_BGR2RGB)

    # Get the masks and noun phrases annotated in this video in this frame
    annot_df_current_video = annot_df[annot_df.video_id == video_id]
    if len(annot_df_current_video) == 0:
        print(f"No annotations found for video_id {video_id}")
        return frame, None, None
    else:
        empty_mask = np.zeros(frame.shape[:2], dtype=np.uint8)
        mask_np_pairs = annot_df_current_video.apply(
            lambda row: (
                (
                    mask_utils.decode(row.segmentations[frame_idx])
                    if row.segmentations[frame_idx]
                    else empty_mask
                ),
                row.noun_phrase,
            ),
            axis=1,
        )
        # sort based on noun_phrases
        mask_np_pairs = sorted(mask_np_pairs, key=lambda x: x[1])
        masks, noun_phrases = zip(*mask_np_pairs)

    return frame, masks, noun_phrases


def visualize_prompt_overlay(
    frame_idx,
    video_frames,
    title="Prompt Visualization",
    text_prompt=None,
    point_prompts=None,
    point_labels=None,
    bounding_boxes=None,
    box_labels=None,
    obj_id=None,
):
    """Simple prompt visualization function"""
    img = Image.fromarray(load_frame(video_frames[frame_idx]))
    fig, ax = plt.subplots(1, figsize=(6, 4))
    ax.imshow(img)

    img_w, img_h = img.size

    if text_prompt:
        ax.text(
            0.02,
            0.98,
            f'Text: "{text_prompt}"',
            transform=ax.transAxes,
            fontsize=12,
            color="white",
            weight="bold",
            bbox=dict(boxstyle="round,pad=0.3", facecolor="red", alpha=0.7),
            verticalalignment="top",
        )

    if point_prompts:
        for i, point in enumerate(point_prompts):
            x, y = point
            # Convert relative to absolute coordinates
            x_img, y_img = x * img_w, y * img_h

            # Use different colors for positive/negative points
            if point_labels and len(point_labels) > i:
                color = "green" if point_labels[i] == 1 else "red"
                marker = "o" if point_labels[i] == 1 else "x"
            else:
                color = "green"
                marker = "o"

            ax.plot(
                x_img,
                y_img,
                marker=marker,
                color=color,
                markersize=10,
                markeredgewidth=2,
                markeredgecolor="white",
            )
            ax.text(
                x_img + 5,
                y_img - 5,
                f"P{i + 1}",
                color=color,
                fontsize=10,
                weight="bold",
                bbox=dict(boxstyle="round,pad=0.2", facecolor="white", alpha=0.8),
            )

    if bounding_boxes:
        for i, box in enumerate(bounding_boxes):
            x, y, w, h = box
            # Convert relative to absolute coordinates
            x_img, y_img = x * img_w, y * img_h
            w_img, h_img = w * img_w, h * img_h

            # Use different colors for positive/negative boxes
            if box_labels and len(box_labels) > i:
                color = "green" if box_labels[i] == 1 else "red"
            else:
                color = "green"

            rect = patches.Rectangle(
                (x_img, y_img),
                w_img,
                h_img,
                linewidth=2,
                edgecolor=color,
                facecolor="none",
            )
            ax.add_patch(rect)
            ax.text(
                x_img,
                y_img - 5,
                f"B{i + 1}",
                color=color,
                fontsize=10,
                weight="bold",
                bbox=dict(boxstyle="round,pad=0.2", facecolor="white", alpha=0.8),
            )

    # Add object ID info if provided
    if obj_id is not None:
        ax.text(
            0.02,
            0.02,
            f"Object ID: {obj_id}",
            transform=ax.transAxes,
            fontsize=10,
            color="white",
            weight="bold",
            bbox=dict(boxstyle="round,pad=0.3", facecolor="blue", alpha=0.7),
            verticalalignment="bottom",
        )

    ax.set_title(title)
    ax.axis("off")
    plt.tight_layout()
    plt.show()


def plot_results(img, results):
    plt.figure(figsize=(12, 8))
    plt.imshow(img)
    nb_objects = len(results["scores"])
    print(f"found {nb_objects} object(s)")
    for i in range(nb_objects):
        color = COLORS[i % len(COLORS)]
        plot_mask(results["masks"][i].squeeze(0).cpu(), color=color)
        w, h = img.size
        prob = results["scores"][i].item()
        plot_bbox(
            h,
            w,
            results["boxes"][i].cpu(),
            text=f"(id={i}, {prob=:.2f})",
            box_format="XYXY",
            color=color,
            relative_coords=False,
        )


def single_visualization(img, anns, title):
    """
    Create a single image visualization with overlays.
    """
    fig, ax = plt.subplots(figsize=(7, 7))
    fig.suptitle(title, fontsize=16, fontweight="bold")
    overlay = render_masklet_frame(img, anns, alpha=0.5)
    ax.imshow(overlay)
    ax.axis("off")
    plt.tight_layout()


def show_mask(mask, ax, obj_id=None, random_color=False):
    if random_color:
        color = np.concatenate([np.random.random(3), np.array([0.6])], axis=0)
    else:
        cmap = plt.get_cmap("tab10")
        cmap_idx = 0 if obj_id is None else obj_id
        color = np.array([*cmap(cmap_idx)[:3], 0.6])
    h, w = mask.shape[-2:]
    mask_image = mask.reshape(h, w, 1) * color.reshape(1, 1, -1)
    ax.imshow(mask_image)


def show_box(box, ax):
    x0, y0 = box[0], box[1]
    w, h = box[2] - box[0], box[3] - box[1]
    ax.add_patch(
        plt.Rectangle((x0, y0), w, h, edgecolor="green", facecolor=(0, 0, 0, 0), lw=2)
    )


def show_points(coords, labels, ax, marker_size=375):
    pos_points = coords[labels == 1]
    neg_points = coords[labels == 0]
    ax.scatter(
        pos_points[:, 0],
        pos_points[:, 1],
        color="green",
        marker="*",
        s=marker_size,
        edgecolor="white",
        linewidth=1.25,
    )
    ax.scatter(
        neg_points[:, 0],
        neg_points[:, 1],
        color="red",
        marker="*",
        s=marker_size,
        edgecolor="white",
        linewidth=1.25,
    )


def load_frame(frame):
    if isinstance(frame, np.ndarray):
        img = frame
    elif isinstance(frame, Image.Image):
        img = np.array(frame)
    elif isinstance(frame, str) and os.path.isfile(frame):
        img = plt.imread(frame)
    else:
        raise ValueError(f"Invalid video frame type: {type(frame)=}")
    return img



================================================
FILE: sam3/agent/__init__.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe



================================================
FILE: sam3/agent/agent_core.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

import copy
import json
import os

import cv2
from PIL import Image

from .client_llm import send_generate_request
from .client_sam3 import call_sam_service
from .viz import visualize


def save_debug_messages(messages_list, debug, debug_folder_path, debug_jsonl_path):
    """Save messages to debug jsonl file if debug is enabled"""
    if debug and debug_jsonl_path:
        # Ensure the debug directory exists before writing
        os.makedirs(debug_folder_path, exist_ok=True)
        with open(debug_jsonl_path, "w") as f:
            for msg in messages_list:
                f.write(json.dumps(msg, indent=4) + "\n")


def cleanup_debug_files(debug, debug_folder_path, debug_jsonl_path):
    """Clean up debug files when function successfully returns"""
    if debug and debug_folder_path:
        try:
            if os.path.exists(debug_jsonl_path):
                os.remove(debug_jsonl_path)
            if os.path.exists(debug_folder_path):
                os.rmdir(debug_folder_path)
        except Exception as e:
            print(f"Warning: Could not clean up debug files: {e}")


def count_images(messages):
    """Count the total number of images present in the messages history."""
    total = 0
    for message in messages:
        # Check if message has content (should be a list)
        if "content" in message and isinstance(message["content"], list):
            # Iterate through each content item
            for content_item in message["content"]:
                # Check if content item is a dict with type "image"
                if (
                    isinstance(content_item, dict)
                    and content_item.get("type") == "image"
                ):
                    total += 1
    return total


def _prune_messages_for_next_round(
    messages_list,
    used_text_prompts,
    latest_sam3_text_prompt,
    img_path,
    initial_text_prompt,
):
    """Return a new messages list that contains only:
    1) messages[:2] (with optional warning text added to the second message's content)
    2) the latest assistant message (and everything after it) that contains a segment_phrase tool call
    """
    # There should not be more than 10 messages in the conversation history
    assert len(messages_list) < 10

    # Part 1: always keep the first two message JSONs
    part1 = copy.deepcopy(messages_list[:2])

    # Part 2: search backwards for the latest assistant message containing a segment_phrase tool call
    part2_start_idx = None
    for idx in range(len(messages_list) - 1, 1, -1):
        msg = messages_list[idx]
        # We only consider assistant messages with a "content" list
        if msg.get("role") != "assistant" or "content" not in msg:
            continue
        # Look for any content element that is a text containing the segment_phrase tool call
        for content in msg["content"]:
            if (
                isinstance(content, dict)
                and content.get("type") == "text"
                and "<tool>" in content.get("text", "")
                and "segment_phrase" in content.get("text", "")
            ):
                part2_start_idx = idx
                break
        if part2_start_idx is not None:
            break

    part2 = messages_list[part2_start_idx:] if part2_start_idx is not None else []

    # Part 3: decide whether to add warning text to the second message in part1
    previously_used = (
        [p for p in used_text_prompts if p != latest_sam3_text_prompt]
        if latest_sam3_text_prompt
        else list(used_text_prompts)
    )
    if part2 and len(previously_used) > 0:
        warning_text = f'Note that we have previously called the segment_phrase tool with each "text_prompt" in this list: {list(previously_used)}, but none of the generated results were satisfactory. So make sure that you do not use any of these phrases as the "text_prompt" to call the segment_phrase tool again.'
        # Replace the second message entirely to keep exactly 2 content items
        part1[1] = {
            "role": "user",
            "content": [
                {"type": "image", "image": img_path},
                {
                    "type": "text",
                    "text": f"The above image is the raw input image. The initial user input query is: '{initial_text_prompt}'."
                    + " "
                    + warning_text,
                },
            ],
        }
        assert len(part1[1]["content"]) == 2

    # Build the new messages list: part1 (with optional warning), then part2
    new_messages = list(part1)
    new_messages.extend(part2)
    return new_messages


def agent_inference(
    img_path: str,
    initial_text_prompt: str,
    debug: bool = False,
    send_generate_request=send_generate_request,
    call_sam_service=call_sam_service,
    max_generations: int = 100,
    output_dir="../../sam3_agent_out",
):
    """
    Given a text prompt and an image, this tool will perform all aspects of agentic problem solving,
    while saving sam3 and MLLM outputs to their respective directories.

    Args:
        img_path: Path to the input image
        initial_text_prompt: Initial text prompt from the user
        debug: Whether to enable debug mode
        max_generations: Maximum number of send_generate_request calls allowed (default: 100)
    """
    # setup dir
    sam_output_dir = os.path.join(output_dir, "sam_out")
    error_save_dir = os.path.join(output_dir, "none_out")
    debug_save_dir = os.path.join(output_dir, "agent_debug_out")
    os.makedirs(sam_output_dir, exist_ok=True)
    os.makedirs(error_save_dir, exist_ok=True)
    os.makedirs(debug_save_dir, exist_ok=True)
    current_dir = os.path.dirname(os.path.abspath(__file__))
    MLLM_SYSTEM_PROMPT_PATH = os.path.join(
        current_dir, "system_prompts/system_prompt.txt"
    )
    ITERATIVE_CHECKING_SYSTEM_PROMPT_PATH = os.path.join(
        current_dir, "system_prompts/system_prompt_iterative_checking.txt"
    )
    # init variables
    PATH_TO_LATEST_OUTPUT_JSON = ""
    LATEST_SAM3_TEXT_PROMPT = ""
    USED_TEXT_PROMPTS = (
        set()
    )  # Track all previously used text prompts for segment_phrase
    generation_count = 0  # Counter for number of send_generate_request calls

    # debug setup
    debug_folder_path = None
    debug_jsonl_path = None
    if debug:
        debug_folder_path = os.path.join(
            debug_save_dir, f"{img_path.rsplit('/', 1)[-1].rsplit('.', 1)[0]}"
        )
        debug_jsonl_path = os.path.join(debug_folder_path, "debug_history.json")
        os.makedirs(debug_folder_path, exist_ok=True)

    # The helper functions are now defined outside the agent_inference function
    with open(MLLM_SYSTEM_PROMPT_PATH, "r") as f:
        system_prompt = f.read().strip()
    with open(ITERATIVE_CHECKING_SYSTEM_PROMPT_PATH, "r") as f:
        iterative_checking_system_prompt = f.read().strip()

    # Construct the initial message list
    messages = [
        {"role": "system", "content": system_prompt},
        {
            "role": "user",
            "content": [
                {"type": "image", "image": img_path},
                {
                    "type": "text",
                    "text": f"The above image is the raw input image. The initial user input query is: '{initial_text_prompt}'.",
                },
            ],
        },
    ]
    print(f"> Text prompt: {initial_text_prompt}")
    print(f"> Image path: {img_path}")

    print("\n\n")
    print("-" * 30 + f" Round {str(generation_count + 1)}" + "-" * 30)
    print("\n\n")
    generated_text = send_generate_request(messages)
    print(f"\n>>> MLLM Response [start]\n{generated_text}\n<<< MLLM Response [end]\n")
    while generated_text is not None:
        save_debug_messages(messages, debug, debug_folder_path, debug_jsonl_path)
        assert (
            "<tool>" in generated_text,
            f"Generated text does not contain <tool> tag: {generated_text}",
        )
        generated_text = generated_text.split("</tool>", 1)[0] + "</tool>"
        tool_call_json_str = (
            generated_text.split("<tool>")[-1]
            .split("</tool>")[0]
            .strip()
            .replace(r"}}}", r"}}")  # remove extra } if any
        )
        try:
            tool_call = json.loads(tool_call_json_str)
        except json.JSONDecodeError:
            raise ValueError(f"Invalid JSON in tool call: {tool_call_json_str}")

        if PATH_TO_LATEST_OUTPUT_JSON == "":
            # The first tool call must be segment_phrase or report_no_mask
            assert (
                tool_call["name"] == "segment_phrase"
                or tool_call["name"] == "report_no_mask"
            )

        if tool_call["name"] == "segment_phrase":
            print("🔍 Calling segment_phrase tool...")
            assert list(tool_call["parameters"].keys()) == ["text_prompt"]

            # Check if this text_prompt has been used before
            current_text_prompt = tool_call["parameters"]["text_prompt"]
            if current_text_prompt in USED_TEXT_PROMPTS:
                print(
                    f"❌ Text prompt '{current_text_prompt}' has been used before. Requesting a different prompt."
                )
                duplicate_prompt_message = f"You have previously used '{current_text_prompt}' as your text_prompt to call the segment_phrase tool. You may not use it again. Please call the segment_phrase tool again with a different, perhaps more general, or more creative simple noun phrase prompt, while adhering to all the rules stated in the system prompt. You must also never use any of the following text_prompt(s): {str(list(USED_TEXT_PROMPTS))}."
                messages.append(
                    {
                        "role": "assistant",
                        "content": [{"type": "text", "text": generated_text}],
                    }
                )
                messages.append(
                    {
                        "role": "user",
                        "content": [{"type": "text", "text": duplicate_prompt_message}],
                    }
                )
            else:
                # Add the text_prompt to the set of used prompts
                USED_TEXT_PROMPTS.add(current_text_prompt)
                LATEST_SAM3_TEXT_PROMPT = current_text_prompt
                PATH_TO_LATEST_OUTPUT_JSON = call_sam_service(
                    image_path=img_path,
                    text_prompt=current_text_prompt,
                    output_folder_path=sam_output_dir,
                )
                sam3_outputs = json.load(open(PATH_TO_LATEST_OUTPUT_JSON, "r"))
                sam3_output_image_path = sam3_outputs["output_image_path"]
                num_masks = len(sam3_outputs["pred_boxes"])

                messages.append(
                    {
                        "role": "assistant",
                        "content": [{"type": "text", "text": generated_text}],
                    }
                )
                if num_masks == 0:
                    print("❌ No masks generated by SAM3, reporting no mask to Qwen.")
                    sam3_output_text_message = f"The segment_phrase tool did not generate any masks for the text_prompt '{current_text_prompt}'. Now, please call the segment_phrase tool again with a different, perhaps more general, or more creative simple noun phrase text_prompt, while adhering to all the rules stated in the system prompt. Please be reminded that the original user query was '{initial_text_prompt}'."
                    messages.append(
                        {
                            "role": "user",
                            "content": [
                                {"type": "text", "text": sam3_output_text_message}
                            ],
                        }
                    )
                else:
                    sam3_output_text_message = rf"The segment_phrase tool generated {num_masks} available masks. All {num_masks} available masks are rendered in this image below, now you must analyze the {num_masks} available mask(s) carefully, compare them against the raw input image and the original user query, and determine your next action. Please be reminded that the original user query was '{initial_text_prompt}'."
                    messages.append(
                        {
                            "role": "user",
                            "content": [
                                {"type": "text", "text": sam3_output_text_message},
                                {"type": "image", "image": sam3_output_image_path},
                            ],
                        }
                    )
                print("\n\n>>> sam3_output_text_message:\n", sam3_output_text_message)

        elif tool_call["name"] == "examine_each_mask":
            print("🔍 Calling examine_each_mask tool...")
            assert LATEST_SAM3_TEXT_PROMPT != ""

            # Make sure that the last message is a image
            assert messages[-1]["content"][1]["type"] == "image", (
                "Second content element should be an image"
            )
            messages.pop()  # Remove the last user message
            # Add simplified replacement message
            simplified_message = {
                "role": "user",
                "content": [
                    {
                        "type": "text",
                        "text": "The segment_phrase tool generated several masks. Now you must analyze the mask(s) carefully, compare them against the raw input image and the original user query, and determine your next action.",
                    }
                ],
            }
            messages.append(simplified_message)

            current_outputs = json.load(open(PATH_TO_LATEST_OUTPUT_JSON, "r"))
            num_masks = len(current_outputs["pred_masks"])
            masks_to_keep = []

            # MLLM check the mask one by one
            for i in range(num_masks):
                print(f"🔍 Checking mask {i + 1}/{num_masks}...")
                image_w_mask_i, image_w_zoomed_in_mask_i = visualize(current_outputs, i)

                image_w_zoomed_in_mask_i_path = os.path.join(
                    sam_output_dir, rf"{LATEST_SAM3_TEXT_PROMPT}.png".replace("/", "_")
                ).replace(".png", f"_zoom_in_mask_{i + 1}.png")
                image_w_mask_i_path = os.path.join(
                    sam_output_dir, rf"{LATEST_SAM3_TEXT_PROMPT}.png".replace("/", "_")
                ).replace(".png", f"_selected_mask_{i + 1}.png")
                image_w_zoomed_in_mask_i.save(image_w_zoomed_in_mask_i_path)
                image_w_mask_i.save(image_w_mask_i_path)

                iterative_checking_messages = [
                    {"role": "system", "content": iterative_checking_system_prompt},
                    {
                        "role": "user",
                        "content": [
                            {"type": "text", "text": f"The raw input image: "},
                            {"type": "image", "image": img_path},
                            {
                                "type": "text",
                                "text": f"The initial user input query is: '{initial_text_prompt}'",
                            },
                            {
                                "type": "text",
                                "text": f"Image with the predicted segmentation mask rendered on it: ",
                            },
                            {"type": "image", "image": image_w_mask_i_path},
                            {
                                "type": "text",
                                "text": f"Image with the zoomed-in mask: ",
                            },
                            {"type": "image", "image": image_w_zoomed_in_mask_i_path},
                        ],
                    },
                ]
                checking_generated_text = send_generate_request(
                    iterative_checking_messages
                )

                # Process the generated text to determine if the mask should be kept or rejected
                if checking_generated_text is None:
                    raise ValueError(
                        "Generated text is None, which is unexpected. Please check the Qwen server and the input parameters."
                    )
                print(f"Generated text for mask {i + 1}: {checking_generated_text}")
                verdict = (
                    checking_generated_text.split("<verdict>")[-1]
                    .split("</verdict>")[0]
                    .strip()
                )
                if "Accept" in verdict:
                    assert not "Reject" in verdict
                    print(f"Mask {i + 1} accepted, keeping it in the outputs.")
                    masks_to_keep.append(i)
                elif "Reject" in verdict:
                    assert not "Accept" in verdict
                    print(f"Mask {i + 1} rejected, removing it from the outputs.")
                else:
                    raise ValueError(
                        f"Unexpected verdict in generated text: {checking_generated_text}. Expected 'Accept' or 'Reject'."
                    )

            updated_outputs = {
                "original_image_path": current_outputs["original_image_path"],
                "orig_img_h": current_outputs["orig_img_h"],
                "orig_img_w": current_outputs["orig_img_w"],
                "pred_boxes": [current_outputs["pred_boxes"][i] for i in masks_to_keep],
                "pred_scores": [
                    current_outputs["pred_scores"][i] for i in masks_to_keep
                ],
                "pred_masks": [current_outputs["pred_masks"][i] for i in masks_to_keep],
            }

            image_w_check_masks = visualize(updated_outputs)
            image_w_check_masks_path = os.path.join(
                sam_output_dir, rf"{LATEST_SAM3_TEXT_PROMPT}.png"
            ).replace(
                ".png",
                f"_selected_masks_{'-'.join(map(str, [i + 1 for i in masks_to_keep]))}.png".replace(
                    "/", "_"
                ),
            )
            image_w_check_masks.save(image_w_check_masks_path)
            # save the updated json outputs and append to message history
            messages.append(
                {
                    "role": "assistant",
                    "content": [{"type": "text", "text": generated_text}],
                }
            )
            if len(masks_to_keep) == 0:
                messages.append(
                    {
                        "role": "user",
                        "content": [
                            {
                                "type": "text",
                                "text": f"The original user query was: '{initial_text_prompt}'. The examine_each_mask tool examined and rejected all of the masks generated by the segment_phrase tool. Now, please call the segment_phrase tool again with a different, perhaps more general, or more creative simple noun phrase text_prompt, while adhering to all the rules stated in the system prompt.",
                            }
                        ],
                    }
                )
            else:
                messages.append(
                    {
                        "role": "user",
                        "content": [
                            {
                                "type": "text",
                                "text": f"The original user query was: '{initial_text_prompt}'. After calling the examine_each_mask tool on the available masks, the number of available masks is now {len(masks_to_keep)}. All {len(masks_to_keep)} available masks are rendered in this image below, now you must analyze the {len(masks_to_keep)} available mask(s) carefully, compare them against the raw input image and the original user query, and determine your next action.",
                            },
                            {"type": "image", "image": image_w_check_masks_path},
                        ],
                    }
                )

            # Create a new filename based on the original path to avoid filename length issues
            base_path = PATH_TO_LATEST_OUTPUT_JSON
            # Remove any existing "masks_" suffix to avoid duplication
            if "masks_" in base_path:
                base_path = base_path.split("masks_")[0] + ".json"
            # Create new filename with current masks; use a clearer suffix when empty
            if len(masks_to_keep) == 0:
                PATH_TO_LATEST_OUTPUT_JSON = base_path.replace(
                    ".json", "masks_none.json"
                )
            else:
                PATH_TO_LATEST_OUTPUT_JSON = base_path.replace(
                    ".json", f"masks_{'_'.join(map(str, masks_to_keep))}.json"
                )
            json.dump(updated_outputs, open(PATH_TO_LATEST_OUTPUT_JSON, "w"), indent=4)

        elif tool_call["name"] == "select_masks_and_return":
            print("🔍 Calling select_masks_and_return tool...")
            current_outputs = json.load(open(PATH_TO_LATEST_OUTPUT_JSON, "r"))

            assert list(tool_call["parameters"].keys()) == ["final_answer_masks"]
            masks_to_keep = tool_call["parameters"]["final_answer_masks"]

            # Keep only valid mask indices, remove duplicates, and preserve deterministic ascending order
            available_masks = set(range(1, len(current_outputs["pred_masks"]) + 1))
            masks_to_keep = sorted({i for i in masks_to_keep if i in available_masks})
            # Change this to a update message telling the model to try again along with information about errors made.

            final_outputs = {
                "original_image_path": current_outputs["original_image_path"],
                "orig_img_h": current_outputs["orig_img_h"],
                "orig_img_w": current_outputs["orig_img_w"],
                "pred_boxes": [
                    current_outputs["pred_boxes"][i - 1] for i in masks_to_keep
                ],
                "pred_scores": [
                    current_outputs["pred_scores"][i - 1] for i in masks_to_keep
                ],
                "pred_masks": [
                    current_outputs["pred_masks"][i - 1] for i in masks_to_keep
                ],
            }

            rendered_final_output = visualize(final_outputs)
            messages.append(
                {
                    "role": "assistant",
                    "content": [{"type": "text", "text": generated_text}],
                }
            )

            # Clean up debug files before successful return
            cleanup_debug_files(debug, debug_folder_path, debug_jsonl_path)
            return messages, final_outputs, rendered_final_output

        elif tool_call["name"] == "report_no_mask":
            print("🔍 Calling report_no_mask tool...")
            height, width = cv2.imread(img_path).shape[:2]
            final_outputs = {
                "original_image_path": img_path,
                "orig_img_h": height,
                "orig_img_w": width,
                "pred_boxes": [],
                "pred_scores": [],
                "pred_masks": [],
            }
            rendered_final_output = Image.open(img_path)
            messages.append(
                {
                    "role": "assistant",
                    "content": [{"type": "text", "text": generated_text}],
                }
            )
            return messages, final_outputs, rendered_final_output

        else:
            raise ValueError(f"Unknown tool call: {tool_call['name']}")

        # sometimes the MLLM don't know when to stop, and generates multiple tool calls in one round, so we need to split the generated text by </tool> and only keep the first one

        for message in messages:
            if message["role"] == "assistant" and "content" in message:
                for content in message["content"]:
                    if (
                        isinstance(content, dict)
                        and content.get("type") == "text"
                        and "text" in content
                    ):
                        content["text"] = (
                            content["text"].split("</tool>", 1)[0] + "</tool>\n\n"
                        )
        # Prune the messages history before the next MLLM generation round according to the 3-part rules.
        # This keeps history compact and ensures the model sees only the allowed parts.
        messages = _prune_messages_for_next_round(
            messages,
            USED_TEXT_PROMPTS,
            LATEST_SAM3_TEXT_PROMPT,
            img_path,
            initial_text_prompt,
        )
        # make sure there can never be more than 2 images in the context
        assert count_images(messages) <= 2
        generation_count += 1
        if generation_count > max_generations:
            raise ValueError(
                f"Exceeded maximum number of allowed generation requests ({max_generations})"
            )

        print("\n\n")
        print("-" * 30 + f" Round {str(generation_count + 1)}" + "-" * 30)
        print("\n\n")
        generated_text = send_generate_request(messages)
        print(
            f"\n>>> MLLM Response [start]\n{generated_text}\n<<< MLLM Response [end]\n"
        )

    print("\n\n>>> SAM 3 Agent execution ended.\n\n")

    error_save_path = os.path.join(
        error_save_dir,
        f"{img_path.rsplit('/', 1)[-1].rsplit('.', 1)[0]}_error_history.json",
    )
    with open(error_save_path, "w") as f:
        json.dump(messages, f, indent=4)
    print("Saved messages history that caused error to:", error_save_path)
    raise ValueError(
        rf"Generated text is None, which is unexpected. Please check the Qwen server and the input parameters for image path: {img_path} and initial text prompt: {initial_text_prompt}."
    )



================================================
FILE: sam3/agent/client_llm.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

import base64
import os
from typing import Any, Optional

from openai import OpenAI


def get_image_base64_and_mime(image_path):
    """Convert image file to base64 string and get MIME type"""
    try:
        # Get MIME type based on file extension
        ext = os.path.splitext(image_path)[1].lower()
        mime_types = {
            ".jpg": "image/jpeg",
            ".jpeg": "image/jpeg",
            ".png": "image/png",
            ".gif": "image/gif",
            ".webp": "image/webp",
            ".bmp": "image/bmp",
        }
        mime_type = mime_types.get(ext, "image/jpeg")  # Default to JPEG

        # Convert image to base64
        with open(image_path, "rb") as image_file:
            base64_data = base64.b64encode(image_file.read()).decode("utf-8")
            return base64_data, mime_type
    except Exception as e:
        print(f"Error converting image to base64: {e}")
        return None, None


def send_generate_request(
    messages,
    server_url=None,
    model="meta-llama/Llama-4-Maverick-17B-128E-Instruct-FP8",
    api_key=None,
    max_tokens=4096,
):
    """
    Sends a request to the OpenAI-compatible API endpoint using the OpenAI client library.

    Args:
        server_url (str): The base URL of the server, e.g. "http://127.0.0.1:8000"
        messages (list): A list of message dicts, each containing role and content.
        model (str): The model to use for generation (default: "llama-4")
        max_tokens (int): Maximum number of tokens to generate (default: 4096)

    Returns:
        str: The generated response text from the server.
    """
    # Process messages to convert image paths to base64
    processed_messages = []
    for message in messages:
        processed_message = message.copy()
        if message["role"] == "user" and "content" in message:
            processed_content = []
            for c in message["content"]:
                if isinstance(c, dict) and c.get("type") == "image":
                    # Convert image path to base64 format
                    image_path = c["image"]

                    print("image_path", image_path)
                    new_image_path = image_path.replace(
                        "?", "%3F"
                    )  # Escape ? in the path

                    # Read the image file and convert to base64
                    try:
                        base64_image, mime_type = get_image_base64_and_mime(
                            new_image_path
                        )
                        if base64_image is None:
                            print(
                                f"Warning: Could not convert image to base64: {new_image_path}"
                            )
                            continue

                        # Create the proper image_url structure with base64 data
                        processed_content.append(
                            {
                                "type": "image_url",
                                "image_url": {
                                    "url": f"data:{mime_type};base64,{base64_image}",
                                    "detail": "high",
                                },
                            }
                        )

                    except FileNotFoundError:
                        print(f"Warning: Image file not found: {new_image_path}")
                        continue
                    except Exception as e:
                        print(f"Warning: Error processing image {new_image_path}: {e}")
                        continue
                else:
                    processed_content.append(c)

            processed_message["content"] = processed_content
        processed_messages.append(processed_message)

    # Create OpenAI client with custom base URL
    client = OpenAI(api_key=api_key, base_url=server_url)

    try:
        print(f"🔍 Calling model {model}...")
        response = client.chat.completions.create(
            model=model,
            messages=processed_messages,
            max_completion_tokens=max_tokens,
            n=1,
        )
        # print(f"Received response: {response.choices[0].message}")

        # Extract the response content
        if response.choices and len(response.choices) > 0:
            return response.choices[0].message.content
        else:
            print(f"Unexpected response format: {response}")
            return None

    except Exception as e:
        print(f"Request failed: {e}")
        return None


def send_direct_request(
    llm: Any,
    messages: list[dict[str, Any]],
    sampling_params: Any,
) -> Optional[str]:
    """
    Run inference on a vLLM model instance directly without using a server.

    Args:
        llm: Initialized vLLM LLM instance (passed from external initialization)
        messages: List of message dicts with role and content (OpenAI format)
        sampling_params: vLLM SamplingParams instance (initialized externally)

    Returns:
        str: Generated response text, or None if inference fails
    """
    try:
        # Process messages to handle images (convert to base64 if needed)
        processed_messages = []
        for message in messages:
            processed_message = message.copy()
            if message["role"] == "user" and "content" in message:
                processed_content = []
                for c in message["content"]:
                    if isinstance(c, dict) and c.get("type") == "image":
                        # Convert image path to base64 format
                        image_path = c["image"]
                        new_image_path = image_path.replace("?", "%3F")

                        try:
                            base64_image, mime_type = get_image_base64_and_mime(
                                new_image_path
                            )
                            if base64_image is None:
                                print(
                                    f"Warning: Could not convert image: {new_image_path}"
                                )
                                continue

                            # vLLM expects image_url format
                            processed_content.append(
                                {
                                    "type": "image_url",
                                    "image_url": {
                                        "url": f"data:{mime_type};base64,{base64_image}"
                                    },
                                }
                            )
                        except Exception as e:
                            print(
                                f"Warning: Error processing image {new_image_path}: {e}"
                            )
                            continue
                    else:
                        processed_content.append(c)

                processed_message["content"] = processed_content
            processed_messages.append(processed_message)

        print("🔍 Running direct inference with vLLM...")

        # Run inference using vLLM's chat interface
        outputs = llm.chat(
            messages=processed_messages,
            sampling_params=sampling_params,
        )

        # Extract the generated text from the first output
        if outputs and len(outputs) > 0:
            generated_text = outputs[0].outputs[0].text
            return generated_text
        else:
            print(f"Unexpected output format: {outputs}")
            return None

    except Exception as e:
        print(f"Direct inference failed: {e}")
        return None



================================================
FILE: sam3/agent/client_sam3.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

import json
import os

import torch
from PIL import Image
from sam3.model.box_ops import box_xyxy_to_xywh
from sam3.train.masks_ops import rle_encode

from .helpers.mask_overlap_removal import remove_overlapping_masks
from .viz import visualize


def sam3_inference(processor, image_path, text_prompt):
    """Run SAM 3 image inference with text prompts and format the outputs"""
    image = Image.open(image_path)
    orig_img_w, orig_img_h = image.size

    # model inference
    inference_state = processor.set_image(image)
    inference_state = processor.set_text_prompt(
        state=inference_state, prompt=text_prompt
    )

    # format and assemble outputs
    pred_boxes_xyxy = torch.stack(
        [
            inference_state["boxes"][:, 0] / orig_img_w,
            inference_state["boxes"][:, 1] / orig_img_h,
            inference_state["boxes"][:, 2] / orig_img_w,
            inference_state["boxes"][:, 3] / orig_img_h,
        ],
        dim=-1,
    )  # normalized in range [0, 1]
    pred_boxes_xywh = box_xyxy_to_xywh(pred_boxes_xyxy).tolist()
    pred_masks = rle_encode(inference_state["masks"].squeeze(1))
    pred_masks = [m["counts"] for m in pred_masks]
    outputs = {
        "orig_img_h": orig_img_h,
        "orig_img_w": orig_img_w,
        "pred_boxes": pred_boxes_xywh,
        "pred_masks": pred_masks,
        "pred_scores": inference_state["scores"].tolist(),
    }
    return outputs


def call_sam_service(
    sam3_processor,
    image_path: str,
    text_prompt: str,
    output_folder_path: str = "sam3_output",
):
    """
    Loads an image, sends it with a text prompt to the service,
    saves the results, and renders the visualization.
    """
    print(f"📞 Loading image '{image_path}' and sending with prompt '{text_prompt}'...")

    text_prompt_for_save_path = (
        text_prompt.replace("/", "_") if "/" in text_prompt else text_prompt
    )

    os.makedirs(
        os.path.join(output_folder_path, image_path.replace("/", "-")), exist_ok=True
    )
    output_json_path = os.path.join(
        output_folder_path,
        image_path.replace("/", "-"),
        rf"{text_prompt_for_save_path}.json",
    )
    output_image_path = os.path.join(
        output_folder_path,
        image_path.replace("/", "-"),
        rf"{text_prompt_for_save_path}.png",
    )

    try:
        # Send the image and text prompt as a multipart/form-data request
        serialized_response = sam3_inference(sam3_processor, image_path, text_prompt)

        # 1. Prepare the response dictionary
        serialized_response = remove_overlapping_masks(serialized_response)
        serialized_response = {
            "original_image_path": image_path,
            "output_image_path": output_image_path,
            **serialized_response,
        }

        # 2. Reorder predictions by scores (highest to lowest) if scores are available
        if "pred_scores" in serialized_response and serialized_response["pred_scores"]:
            # Create indices sorted by scores in descending order
            score_indices = sorted(
                range(len(serialized_response["pred_scores"])),
                key=lambda i: serialized_response["pred_scores"][i],
                reverse=True,
            )

            # Reorder all three lists based on the sorted indices
            serialized_response["pred_scores"] = [
                serialized_response["pred_scores"][i] for i in score_indices
            ]
            serialized_response["pred_boxes"] = [
                serialized_response["pred_boxes"][i] for i in score_indices
            ]
            serialized_response["pred_masks"] = [
                serialized_response["pred_masks"][i] for i in score_indices
            ]

        # 3. Remove any invalid RLE masks that is too short (shorter than 5 characters)
        valid_masks = []
        valid_boxes = []
        valid_scores = []
        for i, rle in enumerate(serialized_response["pred_masks"]):
            if len(rle) > 4:
                valid_masks.append(rle)
                valid_boxes.append(serialized_response["pred_boxes"][i])
                valid_scores.append(serialized_response["pred_scores"][i])
        serialized_response["pred_masks"] = valid_masks
        serialized_response["pred_boxes"] = valid_boxes
        serialized_response["pred_scores"] = valid_scores

        with open(output_json_path, "w") as f:
            json.dump(serialized_response, f, indent=4)
        print(f"✅ Raw JSON response saved to '{output_json_path}'")

        # 4. Render and save visualizations on the image and save it in the SAM3 output folder
        print("🔍 Rendering visualizations on the image ...")
        viz_image = visualize(serialized_response)
        os.makedirs(os.path.dirname(output_image_path), exist_ok=True)
        viz_image.save(output_image_path)
        print("✅ Saved visualization at:", output_image_path)
    except Exception as e:
        print(f"❌ Error calling service: {e}")

    return output_json_path



================================================
FILE: sam3/agent/inference.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

import json
import os

from sam3.agent.agent_core import agent_inference


def run_single_image_inference(
    image_path,
    text_prompt,
    llm_config,
    send_generate_request,
    call_sam_service,
    output_dir="agent_output",
    debug=False,
):
    """Run inference on a single image with provided prompt"""

    llm_name = llm_config["name"]

    if not os.path.exists(image_path):
        raise FileNotFoundError(f"Image file not found: {image_path}")

    # Create output directory
    os.makedirs(output_dir, exist_ok=True)

    # Generate output file names
    image_basename = os.path.splitext(os.path.basename(image_path))[0]
    prompt_for_filename = text_prompt.replace("/", "_").replace(" ", "_")

    base_filename = f"{image_basename}_{prompt_for_filename}_agent_{llm_name}"
    output_json_path = os.path.join(output_dir, f"{base_filename}_pred.json")
    output_image_path = os.path.join(output_dir, f"{base_filename}_pred.png")
    agent_history_path = os.path.join(output_dir, f"{base_filename}_history.json")

    # Check if output already exists and skip
    if os.path.exists(output_json_path):
        print(f"Output JSON {output_json_path} already exists. Skipping.")
        return

    print(f"{'-' * 30} Starting SAM 3 Agent Session... {'-' * 30} ")
    agent_history, final_output_dict, rendered_final_output = agent_inference(
        image_path,
        text_prompt,
        send_generate_request=send_generate_request,
        call_sam_service=call_sam_service,
        output_dir=output_dir,
        debug=debug,
    )
    print(f"{'-' * 30} End of SAM 3 Agent Session... {'-' * 30} ")

    final_output_dict["text_prompt"] = text_prompt
    final_output_dict["image_path"] = image_path

    # Save outputs
    json.dump(final_output_dict, open(output_json_path, "w"), indent=4)
    json.dump(agent_history, open(agent_history_path, "w"), indent=4)
    rendered_final_output.save(output_image_path)

    print(f"\n✅ Successfully processed single image!")
    print(f"Output JSON: {output_json_path}")
    print(f"Output Image: {output_image_path}")
    print(f"Agent History: {agent_history_path}")
    return output_image_path



================================================
FILE: sam3/agent/viz.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

import cv2
import numpy as np
import pycocotools.mask as mask_utils
from PIL import Image

from .helpers.visualizer import Visualizer
from .helpers.zoom_in import render_zoom_in


def visualize(
    input_json: dict,
    zoom_in_index: int | None = None,
    mask_alpha: float = 0.15,
    label_mode: str = "1",
    font_size_multiplier: float = 1.2,
    boarder_width_multiplier: float = 0,
):
    """
    Unified visualization function.

    If zoom_in_index is None:
        - Render all masks in input_json (equivalent to visualize_masks_from_result_json).
        - Returns: PIL.Image

    If zoom_in_index is provided:
        - Returns two PIL.Images:
            1) Output identical to zoom_in_and_visualize(input_json, index).
            2) The same instance rendered via the general overlay using the color
               returned by (1), equivalent to calling visualize_masks_from_result_json
               on a single-mask json_i with color=color_hex.
    """
    # Common fields
    orig_h = int(input_json["orig_img_h"])
    orig_w = int(input_json["orig_img_w"])
    img_path = input_json["original_image_path"]

    # ---------- Mode A: Full-scene render ----------
    if zoom_in_index is None:
        boxes = np.array(input_json["pred_boxes"])
        rle_masks = [
            {"size": (orig_h, orig_w), "counts": rle}
            for rle in input_json["pred_masks"]
        ]
        binary_masks = [mask_utils.decode(rle) for rle in rle_masks]

        img_bgr = cv2.imread(img_path)
        if img_bgr is None:
            raise FileNotFoundError(f"Could not read image: {img_path}")
        img_rgb = cv2.cvtColor(img_bgr, cv2.COLOR_BGR2RGB)

        viz = Visualizer(
            img_rgb,
            font_size_multiplier=font_size_multiplier,
            boarder_width_multiplier=boarder_width_multiplier,
        )
        viz.overlay_instances(
            boxes=boxes,
            masks=rle_masks,
            binary_masks=binary_masks,
            assigned_colors=None,
            alpha=mask_alpha,
            label_mode=label_mode,
        )
        pil_all_masks = Image.fromarray(viz.output.get_image())
        return pil_all_masks

    # ---------- Mode B: Zoom-in pair ----------
    else:
        idx = int(zoom_in_index)
        num_masks = len(input_json.get("pred_masks", []))
        if idx < 0 or idx >= num_masks:
            raise ValueError(
                f"zoom_in_index {idx} is out of range (0..{num_masks - 1})."
            )

        # (1) Replicate zoom_in_and_visualize
        object_data = {
            "labels": [{"noun_phrase": f"mask_{idx}"}],
            "segmentation": {
                "counts": input_json["pred_masks"][idx],
                "size": [orig_h, orig_w],
            },
        }
        pil_img = Image.open(img_path)
        pil_mask_i_zoomed, color_hex = render_zoom_in(
            object_data, pil_img, mask_alpha=mask_alpha
        )

        # (2) Single-instance render with the same color
        boxes_i = np.array([input_json["pred_boxes"][idx]])
        rle_i = {"size": (orig_h, orig_w), "counts": input_json["pred_masks"][idx]}
        bin_i = mask_utils.decode(rle_i)

        img_bgr_i = cv2.imread(img_path)
        if img_bgr_i is None:
            raise FileNotFoundError(f"Could not read image: {img_path}")
        img_rgb_i = cv2.cvtColor(img_bgr_i, cv2.COLOR_BGR2RGB)

        viz_i = Visualizer(
            img_rgb_i,
            font_size_multiplier=font_size_multiplier,
            boarder_width_multiplier=boarder_width_multiplier,
        )
        viz_i.overlay_instances(
            boxes=boxes_i,
            masks=[rle_i],
            binary_masks=[bin_i],
            assigned_colors=[color_hex],
            alpha=mask_alpha,
            label_mode=label_mode,
        )
        pil_mask_i = Image.fromarray(viz_i.output.get_image())

        return pil_mask_i, pil_mask_i_zoomed



================================================
FILE: sam3/agent/helpers/__init__.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe



================================================
FILE: sam3/agent/helpers/boxes.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

import math
from enum import IntEnum, unique
from typing import List, Tuple, Union

import numpy as np
import torch
from torch import device

_RawBoxType = Union[List[float], Tuple[float, ...], torch.Tensor, np.ndarray]


@unique
class BoxMode(IntEnum):
    """
    Enum of different ways to represent a box.
    """

    XYXY_ABS = 0
    """
    (x0, y0, x1, y1) in absolute floating points coordinates.
    The coordinates in range [0, width or height].
    """
    XYWH_ABS = 1
    """
    (x0, y0, w, h) in absolute floating points coordinates.
    """
    XYXY_REL = 2
    """
    Not yet supported!
    (x0, y0, x1, y1) in range [0, 1]. They are relative to the size of the image.
    """
    XYWH_REL = 3
    """
    Not yet supported!
    (x0, y0, w, h) in range [0, 1]. They are relative to the size of the image.
    """
    XYWHA_ABS = 4
    """
    (xc, yc, w, h, a) in absolute floating points coordinates.
    (xc, yc) is the center of the rotated box, and the angle a is in degrees ccw.
    """

    @staticmethod
    def convert(
        box: _RawBoxType, from_mode: "BoxMode", to_mode: "BoxMode"
    ) -> _RawBoxType:
        """
        Args:
            box: can be a k-tuple, k-list or an Nxk array/tensor, where k = 4 or 5
            from_mode, to_mode (BoxMode)

        Returns:
            The converted box of the same type.
        """
        if from_mode == to_mode:
            return box

        original_type = type(box)
        is_numpy = isinstance(box, np.ndarray)
        single_box = isinstance(box, (list, tuple))
        if single_box:
            assert len(box) == 4 or len(box) == 5, (
                "BoxMode.convert takes either a k-tuple/list or an Nxk array/tensor,"
                " where k == 4 or 5"
            )
            arr = torch.tensor(box)[None, :]
        else:
            # avoid modifying the input box
            if is_numpy:
                arr = torch.from_numpy(np.asarray(box)).clone()
            else:
                arr = box.clone()

        assert to_mode not in [
            BoxMode.XYXY_REL,
            BoxMode.XYWH_REL,
        ] and from_mode not in [
            BoxMode.XYXY_REL,
            BoxMode.XYWH_REL,
        ], "Relative mode not yet supported!"

        if from_mode == BoxMode.XYWHA_ABS and to_mode == BoxMode.XYXY_ABS:
            assert arr.shape[-1] == 5, (
                "The last dimension of input shape must be 5 for XYWHA format"
            )
            original_dtype = arr.dtype
            arr = arr.double()

            w = arr[:, 2]
            h = arr[:, 3]
            a = arr[:, 4]
            c = torch.abs(torch.cos(a * math.pi / 180.0))
            s = torch.abs(torch.sin(a * math.pi / 180.0))
            # This basically computes the horizontal bounding rectangle of the rotated box
            new_w = c * w + s * h
            new_h = c * h + s * w

            # convert center to top-left corner
            arr[:, 0] -= new_w / 2.0
            arr[:, 1] -= new_h / 2.0
            # bottom-right corner
            arr[:, 2] = arr[:, 0] + new_w
            arr[:, 3] = arr[:, 1] + new_h

            arr = arr[:, :4].to(dtype=original_dtype)
        elif from_mode == BoxMode.XYWH_ABS and to_mode == BoxMode.XYWHA_ABS:
            original_dtype = arr.dtype
            arr = arr.double()
            arr[:, 0] += arr[:, 2] / 2.0
            arr[:, 1] += arr[:, 3] / 2.0
            angles = torch.zeros((arr.shape[0], 1), dtype=arr.dtype)
            arr = torch.cat((arr, angles), axis=1).to(dtype=original_dtype)
        else:
            if to_mode == BoxMode.XYXY_ABS and from_mode == BoxMode.XYWH_ABS:
                arr[:, 2] += arr[:, 0]
                arr[:, 3] += arr[:, 1]
            elif from_mode == BoxMode.XYXY_ABS and to_mode == BoxMode.XYWH_ABS:
                arr[:, 2] -= arr[:, 0]
                arr[:, 3] -= arr[:, 1]
            else:
                raise NotImplementedError(
                    "Conversion from BoxMode {} to {} is not supported yet".format(
                        from_mode, to_mode
                    )
                )

        if single_box:
            return original_type(arr.flatten().tolist())
        if is_numpy:
            return arr.numpy()
        else:
            return arr


class Boxes:
    """
    This structure stores a list of boxes as a Nx4 torch.Tensor.
    It supports some common methods about boxes
    (`area`, `clip`, `nonempty`, etc),
    and also behaves like a Tensor
    (support indexing, `to(device)`, `.device`, and iteration over all boxes)

    Attributes:
        tensor (torch.Tensor): float matrix of Nx4. Each row is (x1, y1, x2, y2).
    """

    def __init__(self, tensor: torch.Tensor):
        """
        Args:
            tensor (Tensor[float]): a Nx4 matrix.  Each row is (x1, y1, x2, y2).
        """
        if not isinstance(tensor, torch.Tensor):
            tensor = torch.as_tensor(
                tensor, dtype=torch.float32, device=torch.device("cpu")
            )
        else:
            tensor = tensor.to(torch.float32)
        if tensor.numel() == 0:
            # Use reshape, so we don't end up creating a new tensor that does not depend on
            # the inputs (and consequently confuses jit)
            tensor = tensor.reshape((-1, 4)).to(dtype=torch.float32)
        assert tensor.dim() == 2 and tensor.size(-1) == 4, tensor.size()

        self.tensor = tensor

    def clone(self) -> "Boxes":
        """
        Clone the Boxes.

        Returns:
            Boxes
        """
        return Boxes(self.tensor.clone())

    def to(self, device: torch.device):
        # Boxes are assumed float32 and does not support to(dtype)
        return Boxes(self.tensor.to(device=device))

    def area(self) -> torch.Tensor:
        """
        Computes the area of all the boxes.

        Returns:
            torch.Tensor: a vector with areas of each box.
        """
        box = self.tensor
        area = (box[:, 2] - box[:, 0]) * (box[:, 3] - box[:, 1])
        return area

    def clip(self, box_size: Tuple[int, int]) -> None:
        """
        Clip (in place) the boxes by limiting x coordinates to the range [0, width]
        and y coordinates to the range [0, height].

        Args:
            box_size (height, width): The clipping box's size.
        """
        assert torch.isfinite(self.tensor).all(), "Box tensor contains infinite or NaN!"
        h, w = box_size
        x1 = self.tensor[:, 0].clamp(min=0, max=w)
        y1 = self.tensor[:, 1].clamp(min=0, max=h)
        x2 = self.tensor[:, 2].clamp(min=0, max=w)
        y2 = self.tensor[:, 3].clamp(min=0, max=h)
        self.tensor = torch.stack((x1, y1, x2, y2), dim=-1)

    def nonempty(self, threshold: float = 0.0) -> torch.Tensor:
        """
        Find boxes that are non-empty.
        A box is considered empty, if either of its side is no larger than threshold.

        Returns:
            Tensor:
                a binary vector which represents whether each box is empty
                (False) or non-empty (True).
        """
        box = self.tensor
        widths = box[:, 2] - box[:, 0]
        heights = box[:, 3] - box[:, 1]
        keep = (widths > threshold) & (heights > threshold)
        return keep

    def __getitem__(self, item) -> "Boxes":
        """
        Args:
            item: int, slice, or a BoolTensor

        Returns:
            Boxes: Create a new :class:`Boxes` by indexing.

        The following usage are allowed:

        1. `new_boxes = boxes[3]`: return a `Boxes` which contains only one box.
        2. `new_boxes = boxes[2:10]`: return a slice of boxes.
        3. `new_boxes = boxes[vector]`, where vector is a torch.BoolTensor
           with `length = len(boxes)`. Nonzero elements in the vector will be selected.

        Note that the returned Boxes might share storage with this Boxes,
        subject to Pytorch's indexing semantics.
        """
        if isinstance(item, int):
            return Boxes(self.tensor[item].view(1, -1))
        b = self.tensor[item]
        assert b.dim() == 2, (
            "Indexing on Boxes with {} failed to return a matrix!".format(item)
        )
        return Boxes(b)

    def __len__(self) -> int:
        return self.tensor.shape[0]

    def __repr__(self) -> str:
        return "Boxes(" + str(self.tensor) + ")"

    def inside_box(
        self, box_size: Tuple[int, int], boundary_threshold: int = 0
    ) -> torch.Tensor:
        """
        Args:
            box_size (height, width): Size of the reference box.
            boundary_threshold (int): Boxes that extend beyond the reference box
                boundary by more than boundary_threshold are considered "outside".

        Returns:
            a binary vector, indicating whether each box is inside the reference box.
        """
        height, width = box_size
        inds_inside = (
            (self.tensor[..., 0] >= -boundary_threshold)
            & (self.tensor[..., 1] >= -boundary_threshold)
            & (self.tensor[..., 2] < width + boundary_threshold)
            & (self.tensor[..., 3] < height + boundary_threshold)
        )
        return inds_inside

    def get_centers(self) -> torch.Tensor:
        """
        Returns:
            The box centers in a Nx2 array of (x, y).
        """
        return (self.tensor[:, :2] + self.tensor[:, 2:]) / 2

    def scale(self, scale_x: float, scale_y: float) -> None:
        """
        Scale the box with horizontal and vertical scaling factors
        """
        self.tensor[:, 0::2] *= scale_x
        self.tensor[:, 1::2] *= scale_y

    @classmethod
    def cat(cls, boxes_list: List["Boxes"]) -> "Boxes":
        """
        Concatenates a list of Boxes into a single Boxes

        Arguments:
            boxes_list (list[Boxes])

        Returns:
            Boxes: the concatenated Boxes
        """
        assert isinstance(boxes_list, (list, tuple))
        if len(boxes_list) == 0:
            return cls(torch.empty(0))
        assert all([isinstance(box, Boxes) for box in boxes_list])

        # use torch.cat (v.s. layers.cat) so the returned boxes never share storage with input
        cat_boxes = cls(torch.cat([b.tensor for b in boxes_list], dim=0))
        return cat_boxes

    @property
    def device(self) -> device:
        return self.tensor.device

    # type "Iterator[torch.Tensor]", yield, and iter() not supported by torchscript
    # https://github.com/pytorch/pytorch/issues/18627
    @torch.jit.unused
    def __iter__(self):
        """
        Yield a box as a Tensor of shape (4,) at a time.
        """
        yield from self.tensor


def pairwise_intersection(boxes1: Boxes, boxes2: Boxes) -> torch.Tensor:
    """
    Given two lists of boxes of size N and M,
    compute the intersection area between __all__ N x M pairs of boxes.
    The box order must be (xmin, ymin, xmax, ymax)

    Args:
        boxes1,boxes2 (Boxes): two `Boxes`. Contains N & M boxes, respectively.

    Returns:
        Tensor: intersection, sized [N,M].
    """
    boxes1, boxes2 = boxes1.tensor, boxes2.tensor
    width_height = torch.min(boxes1[:, None, 2:], boxes2[:, 2:]) - torch.max(
        boxes1[:, None, :2], boxes2[:, :2]
    )  # [N,M,2]

    width_height.clamp_(min=0)  # [N,M,2]
    intersection = width_height.prod(dim=2)  # [N,M]
    return intersection


# implementation from https://github.com/kuangliu/torchcv/blob/master/torchcv/utils/box.py
# with slight modifications
def pairwise_iou(boxes1: Boxes, boxes2: Boxes) -> torch.Tensor:
    """
    Given two lists of boxes of size N and M, compute the IoU
    (intersection over union) between **all** N x M pairs of boxes.
    The box order must be (xmin, ymin, xmax, ymax).

    Args:
        boxes1,boxes2 (Boxes): two `Boxes`. Contains N & M boxes, respectively.

    Returns:
        Tensor: IoU, sized [N,M].
    """
    area1 = boxes1.area()  # [N]
    area2 = boxes2.area()  # [M]
    inter = pairwise_intersection(boxes1, boxes2)

    # handle empty boxes
    iou = torch.where(
        inter > 0,
        inter / (area1[:, None] + area2 - inter),
        torch.zeros(1, dtype=inter.dtype, device=inter.device),
    )
    return iou


def pairwise_ioa(boxes1: Boxes, boxes2: Boxes) -> torch.Tensor:
    """
    Similar to :func:`pariwise_iou` but compute the IoA (intersection over boxes2 area).

    Args:
        boxes1,boxes2 (Boxes): two `Boxes`. Contains N & M boxes, respectively.

    Returns:
        Tensor: IoA, sized [N,M].
    """
    area2 = boxes2.area()  # [M]
    inter = pairwise_intersection(boxes1, boxes2)

    # handle empty boxes
    ioa = torch.where(
        inter > 0, inter / area2, torch.zeros(1, dtype=inter.dtype, device=inter.device)
    )
    return ioa


def pairwise_point_box_distance(points: torch.Tensor, boxes: Boxes):
    """
    Pairwise distance between N points and M boxes. The distance between a
    point and a box is represented by the distance from the point to 4 edges
    of the box. Distances are all positive when the point is inside the box.

    Args:
        points: Nx2 coordinates. Each row is (x, y)
        boxes: M boxes

    Returns:
        Tensor: distances of size (N, M, 4). The 4 values are distances from
            the point to the left, top, right, bottom of the box.
    """
    x, y = points.unsqueeze(dim=2).unbind(dim=1)  # (N, 1)
    x0, y0, x1, y1 = boxes.tensor.unsqueeze(dim=0).unbind(dim=2)  # (1, M)
    return torch.stack([x - x0, y - y0, x1 - x, y1 - y], dim=2)


def matched_pairwise_iou(boxes1: Boxes, boxes2: Boxes) -> torch.Tensor:
    """
    Compute pairwise intersection over union (IOU) of two sets of matched
    boxes that have the same number of boxes.
    Similar to :func:`pairwise_iou`, but computes only diagonal elements of the matrix.

    Args:
        boxes1 (Boxes): bounding boxes, sized [N,4].
        boxes2 (Boxes): same length as boxes1
    Returns:
        Tensor: iou, sized [N].
    """
    assert len(boxes1) == len(boxes2), (
        "boxlists should have the samenumber of entries, got {}, {}".format(
            len(boxes1), len(boxes2)
        )
    )
    area1 = boxes1.area()  # [N]
    area2 = boxes2.area()  # [N]
    box1, box2 = boxes1.tensor, boxes2.tensor
    lt = torch.max(box1[:, :2], box2[:, :2])  # [N,2]
    rb = torch.min(box1[:, 2:], box2[:, 2:])  # [N,2]
    wh = (rb - lt).clamp(min=0)  # [N,2]
    inter = wh[:, 0] * wh[:, 1]  # [N]
    iou = inter / (area1 + area2 - inter)  # [N]
    return iou



================================================
FILE: sam3/agent/helpers/color_map.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

"""
An awesome colormap for really neat visualizations.
Copied from Detectron, and removed gray colors.
"""

import random

import numpy as np

__all__ = ["colormap", "random_color", "random_colors"]


# A list of 25 bright and sharp colors for segmentation masks,
# generated from the edges of the sRGB color space for maximum intensity.
_COLORS = (
    np.array(
        [
            # The original 8 sharp colors
            1.000,
            1.000,
            0.000,  # 1. Yellow
            0.000,
            1.000,
            0.000,  # 2. Lime
            0.000,
            1.000,
            1.000,  # 3. Cyan
            1.000,
            0.000,
            1.000,  # 4. Magenta
            1.000,
            0.000,
            0.000,  # 5. Red
            1.000,
            0.498,
            0.000,  # 6. Orange
            0.498,
            1.000,
            0.000,  # 7. Chartreuse
            0.000,
            1.000,
            0.498,  # 8. Spring Green
            1.000,
            0.000,
            0.498,  # 9. Rose
            0.498,
            0.000,
            1.000,  # 10. Violet
            0.753,
            1.000,
            0.000,  # 11. Electric Lime
            1.000,
            0.753,
            0.000,  # 12. Vivid Orange
            0.000,
            1.000,
            0.753,  # 13. Turquoise
            0.753,
            0.000,
            1.000,  # 14. Bright Violet
            1.000,
            0.000,
            0.753,  # 15. Bright Pink
            1.000,
            0.251,
            0.000,  # 16. Fiery Orange
            0.251,
            1.000,
            0.000,  # 17. Bright Chartreuse
            0.000,
            1.000,
            0.251,  # 18. Malachite Green
            0.251,
            0.000,
            1.000,  # 19. Deep Violet
            1.000,
            0.000,
            0.251,  # 20. Hot Pink
        ]
    )
    .astype(np.float32)
    .reshape(-1, 3)
)


def colormap(rgb=False, maximum=255):
    """
    Args:
        rgb (bool): whether to return RGB colors or BGR colors.
        maximum (int): either 255 or 1

    Returns:
        ndarray: a float32 array of Nx3 colors, in range [0, 255] or [0, 1]
    """
    assert maximum in [255, 1], maximum
    c = _COLORS * maximum
    if not rgb:
        c = c[:, ::-1]
    return c


def random_color(rgb=False, maximum=255):
    """
    Args:
        rgb (bool): whether to return RGB colors or BGR colors.
        maximum (int): either 255 or 1

    Returns:
        ndarray: a vector of 3 numbers
    """
    idx = np.random.randint(0, len(_COLORS))
    ret = _COLORS[idx] * maximum
    if not rgb:
        ret = ret[::-1]
    return ret


def random_colors(N, rgb=False, maximum=255):
    """
    Args:
        N (int): number of unique colors needed
        rgb (bool): whether to return RGB colors or BGR colors.
        maximum (int): either 255 or 1

    Returns:
        ndarray: a list of random_color
    """
    indices = random.sample(range(len(_COLORS)), N)
    ret = [_COLORS[i] * maximum for i in indices]
    if not rgb:
        ret = [x[::-1] for x in ret]
    return ret


if __name__ == "__main__":
    import cv2

    size = 100
    H, W = 10, 10
    canvas = np.random.rand(H * size, W * size, 3).astype("float32")
    for h in range(H):
        for w in range(W):
            idx = h * W + w
            if idx >= len(_COLORS):
                break
            canvas[h * size : (h + 1) * size, w * size : (w + 1) * size] = _COLORS[idx]
    cv2.imshow("a", canvas)
    cv2.waitKey(0)



================================================
FILE: sam3/agent/helpers/keypoints.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

from typing import Any, List, Tuple, Union

import numpy as np
import torch
from torch.nn import functional as F


class Keypoints:
    """
    Stores keypoint **annotation** data. GT Instances have a `gt_keypoints` property
    containing the x,y location and visibility flag of each keypoint. This tensor has shape
    (N, K, 3) where N is the number of instances and K is the number of keypoints per instance.

    The visibility flag follows the COCO format and must be one of three integers:

    * v=0: not labeled (in which case x=y=0)
    * v=1: labeled but not visible
    * v=2: labeled and visible
    """

    def __init__(self, keypoints: Union[torch.Tensor, np.ndarray, List[List[float]]]):
        """
        Arguments:
            keypoints: A Tensor, numpy array, or list of the x, y, and visibility of each keypoint.
                The shape should be (N, K, 3) where N is the number of
                instances, and K is the number of keypoints per instance.
        """
        device = (
            keypoints.device
            if isinstance(keypoints, torch.Tensor)
            else torch.device("cpu")
        )
        keypoints = torch.as_tensor(keypoints, dtype=torch.float32, device=device)
        assert keypoints.dim() == 3 and keypoints.shape[2] == 3, keypoints.shape
        self.tensor = keypoints

    def __len__(self) -> int:
        return self.tensor.size(0)

    def to(self, *args: Any, **kwargs: Any) -> "Keypoints":
        return type(self)(self.tensor.to(*args, **kwargs))

    @property
    def device(self) -> torch.device:
        return self.tensor.device

    def to_heatmap(self, boxes: torch.Tensor, heatmap_size: int) -> torch.Tensor:
        """
        Convert keypoint annotations to a heatmap of one-hot labels for training,
        as described in :paper:`Mask R-CNN`.

        Arguments:
            boxes: Nx4 tensor, the boxes to draw the keypoints to

        Returns:
            heatmaps:
                A tensor of shape (N, K), each element is integer spatial label
                in the range [0, heatmap_size**2 - 1] for each keypoint in the input.
            valid:
                A tensor of shape (N, K) containing whether each keypoint is in the roi or not.
        """
        return _keypoints_to_heatmap(self.tensor, boxes, heatmap_size)

    def __getitem__(self, item: Union[int, slice, torch.BoolTensor]) -> "Keypoints":
        """
        Create a new `Keypoints` by indexing on this `Keypoints`.

        The following usage are allowed:

        1. `new_kpts = kpts[3]`: return a `Keypoints` which contains only one instance.
        2. `new_kpts = kpts[2:10]`: return a slice of key points.
        3. `new_kpts = kpts[vector]`, where vector is a torch.ByteTensor
           with `length = len(kpts)`. Nonzero elements in the vector will be selected.

        Note that the returned Keypoints might share storage with this Keypoints,
        subject to Pytorch's indexing semantics.
        """
        if isinstance(item, int):
            return Keypoints([self.tensor[item]])
        return Keypoints(self.tensor[item])

    def __repr__(self) -> str:
        s = self.__class__.__name__ + "("
        s += "num_instances={})".format(len(self.tensor))
        return s

    @staticmethod
    def cat(keypoints_list: List["Keypoints"]) -> "Keypoints":
        """
        Concatenates a list of Keypoints into a single Keypoints

        Arguments:
            keypoints_list (list[Keypoints])

        Returns:
            Keypoints: the concatenated Keypoints
        """
        assert isinstance(keypoints_list, (list, tuple))
        assert len(keypoints_list) > 0
        assert all(isinstance(keypoints, Keypoints) for keypoints in keypoints_list)

        cat_kpts = type(keypoints_list[0])(
            torch.cat([kpts.tensor for kpts in keypoints_list], dim=0)
        )
        return cat_kpts


def _keypoints_to_heatmap(
    keypoints: torch.Tensor, rois: torch.Tensor, heatmap_size: int
) -> Tuple[torch.Tensor, torch.Tensor]:
    """
    Encode keypoint locations into a target heatmap for use in SoftmaxWithLoss across space.

    Maps keypoints from the half-open interval [x1, x2) on continuous image coordinates to the
    closed interval [0, heatmap_size - 1] on discrete image coordinates. We use the
    continuous-discrete conversion from Heckbert 1990 ("What is the coordinate of a pixel?"):
    d = floor(c) and c = d + 0.5, where d is a discrete coordinate and c is a continuous coordinate.

    Arguments:
        keypoints: tensor of keypoint locations in of shape (N, K, 3).
        rois: Nx4 tensor of rois in xyxy format
        heatmap_size: integer side length of square heatmap.

    Returns:
        heatmaps: A tensor of shape (N, K) containing an integer spatial label
            in the range [0, heatmap_size**2 - 1] for each keypoint in the input.
        valid: A tensor of shape (N, K) containing whether each keypoint is in
            the roi or not.
    """

    if rois.numel() == 0:
        return rois.new().long(), rois.new().long()
    offset_x = rois[:, 0]
    offset_y = rois[:, 1]
    scale_x = heatmap_size / (rois[:, 2] - rois[:, 0])
    scale_y = heatmap_size / (rois[:, 3] - rois[:, 1])

    offset_x = offset_x[:, None]
    offset_y = offset_y[:, None]
    scale_x = scale_x[:, None]
    scale_y = scale_y[:, None]

    x = keypoints[..., 0]
    y = keypoints[..., 1]

    x_boundary_inds = x == rois[:, 2][:, None]
    y_boundary_inds = y == rois[:, 3][:, None]

    x = (x - offset_x) * scale_x
    x = x.floor().long()
    y = (y - offset_y) * scale_y
    y = y.floor().long()

    x[x_boundary_inds] = heatmap_size - 1
    y[y_boundary_inds] = heatmap_size - 1

    valid_loc = (x >= 0) & (y >= 0) & (x < heatmap_size) & (y < heatmap_size)
    vis = keypoints[..., 2] > 0
    valid = (valid_loc & vis).long()

    lin_ind = y * heatmap_size + x
    heatmaps = lin_ind * valid

    return heatmaps, valid


@torch.jit.script_if_tracing
def heatmaps_to_keypoints(maps: torch.Tensor, rois: torch.Tensor) -> torch.Tensor:
    """
    Extract predicted keypoint locations from heatmaps.

    Args:
        maps (Tensor): (#ROIs, #keypoints, POOL_H, POOL_W). The predicted heatmap of logits for
            each ROI and each keypoint.
        rois (Tensor): (#ROIs, 4). The box of each ROI.

    Returns:
        Tensor of shape (#ROIs, #keypoints, 4) with the last dimension corresponding to
        (x, y, logit, score) for each keypoint.

    When converting discrete pixel indices in an NxN image to a continuous keypoint coordinate,
    we maintain consistency with :meth:`Keypoints.to_heatmap` by using the conversion from
    Heckbert 1990: c = d + 0.5, where d is a discrete coordinate and c is a continuous coordinate.
    """

    offset_x = rois[:, 0]
    offset_y = rois[:, 1]

    widths = (rois[:, 2] - rois[:, 0]).clamp(min=1)
    heights = (rois[:, 3] - rois[:, 1]).clamp(min=1)
    widths_ceil = widths.ceil()
    heights_ceil = heights.ceil()

    num_rois, num_keypoints = maps.shape[:2]
    xy_preds = maps.new_zeros(rois.shape[0], num_keypoints, 4)

    width_corrections = widths / widths_ceil
    height_corrections = heights / heights_ceil

    keypoints_idx = torch.arange(num_keypoints, device=maps.device)

    for i in range(num_rois):
        outsize = (int(heights_ceil[i]), int(widths_ceil[i]))
        roi_map = F.interpolate(
            maps[[i]], size=outsize, mode="bicubic", align_corners=False
        )

        # Although semantically equivalent, `reshape` is used instead of `squeeze` due
        # to limitation during ONNX export of `squeeze` in scripting mode
        roi_map = roi_map.reshape(roi_map.shape[1:])  # keypoints x H x W

        # softmax over the spatial region
        max_score, _ = roi_map.view(num_keypoints, -1).max(1)
        max_score = max_score.view(num_keypoints, 1, 1)
        tmp_full_resolution = (roi_map - max_score).exp_()
        tmp_pool_resolution = (maps[i] - max_score).exp_()
        # Produce scores over the region H x W, but normalize with POOL_H x POOL_W,
        # so that the scores of objects of different absolute sizes will be more comparable
        roi_map_scores = tmp_full_resolution / tmp_pool_resolution.sum(
            (1, 2), keepdim=True
        )

        w = roi_map.shape[2]
        pos = roi_map.view(num_keypoints, -1).argmax(1)

        x_int = pos % w
        y_int = (pos - x_int) // w

        assert (
            roi_map_scores[keypoints_idx, y_int, x_int]
            == roi_map_scores.view(num_keypoints, -1).max(1)[0]
        ).all()

        x = (x_int.float() + 0.5) * width_corrections[i]
        y = (y_int.float() + 0.5) * height_corrections[i]

        xy_preds[i, :, 0] = x + offset_x[i]
        xy_preds[i, :, 1] = y + offset_y[i]
        xy_preds[i, :, 2] = roi_map[keypoints_idx, y_int, x_int]
        xy_preds[i, :, 3] = roi_map_scores[keypoints_idx, y_int, x_int]

    return xy_preds



================================================
FILE: sam3/agent/helpers/mask_overlap_removal.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

from typing import Dict, List

import numpy as np
import torch

try:
    from pycocotools import mask as mask_utils
except Exception:
    mask_utils = None


def mask_intersection(
    masks1: torch.Tensor, masks2: torch.Tensor, block_size: int = 16
) -> torch.Tensor:
    assert masks1.shape[1:] == masks2.shape[1:]
    assert masks1.dtype == torch.bool and masks2.dtype == torch.bool
    N, M = masks1.shape[0], masks2.shape[0]
    out = torch.zeros(N, M, device=masks1.device, dtype=torch.long)
    for i in range(0, N, block_size):
        for j in range(0, M, block_size):
            a = masks1[i : i + block_size]
            b = masks2[j : j + block_size]
            inter = (a[:, None] & b[None, :]).flatten(-2).sum(-1)
            out[i : i + block_size, j : j + block_size] = inter
    return out


def mask_iom(masks1: torch.Tensor, masks2: torch.Tensor) -> torch.Tensor:
    assert masks1.shape[1:] == masks2.shape[1:]
    assert masks1.dtype == torch.bool and masks2.dtype == torch.bool
    inter = mask_intersection(masks1, masks2)
    area1 = masks1.flatten(-2).sum(-1)  # (N,)
    area2 = masks2.flatten(-2).sum(-1)  # (M,)
    min_area = torch.min(area1[:, None], area2[None, :]).clamp_min(1)
    return inter.float() / (min_area.float() + 1e-8)


def _decode_single_mask(mask_repr, h: int, w: int) -> np.ndarray:
    if isinstance(mask_repr, (list, tuple, np.ndarray)):
        arr = np.array(mask_repr)
        if arr.ndim != 2:
            raise ValueError("Mask array must be 2D (H, W).")
        return (arr > 0).astype(np.uint8)

    if mask_utils is None:
        raise ImportError(
            "pycocotools is required to decode RLE mask strings. pip install pycocotools"
        )

    if not isinstance(mask_repr, (str, bytes)):
        raise ValueError("Unsupported mask representation type for RLE decode.")

    rle = {
        "counts": mask_repr if isinstance(mask_repr, (str, bytes)) else str(mask_repr),
        "size": [h, w],
    }
    decoded = mask_utils.decode(rle)
    if decoded.ndim == 3:
        decoded = decoded[:, :, 0]
    return (decoded > 0).astype(np.uint8)


def _decode_masks_to_torch_bool(pred_masks: List, h: int, w: int) -> torch.Tensor:
    bin_masks = [_decode_single_mask(m, h, w) for m in pred_masks]
    masks_np = np.stack(bin_masks, axis=0).astype(np.uint8)  # (N, H, W)
    return torch.from_numpy(masks_np > 0)


def remove_overlapping_masks(sample: Dict, iom_thresh: float = 0.3) -> Dict:
    """
    Greedy keep: sort by score desc; keep a mask if IoM to all kept masks <= threshold.
    If pred_masks has length 0 or 1, returns sample unchanged (no extra keys).
    """
    # Basic presence checks
    if "pred_masks" not in sample or not isinstance(sample["pred_masks"], list):
        return sample  # nothing to do / preserve as-is

    pred_masks = sample["pred_masks"]
    N = len(pred_masks)

    # --- Early exit: 0 or 1 mask -> do NOT modify the JSON at all ---
    if N <= 1:
        return sample

    # From here on we have at least 2 masks
    h = int(sample["orig_img_h"])
    w = int(sample["orig_img_w"])
    pred_scores = sample.get("pred_scores", [1.0] * N)  # fallback if scores missing
    pred_boxes = sample.get("pred_boxes", None)

    assert N == len(pred_scores), "pred_masks and pred_scores must have same length"
    if pred_boxes is not None:
        assert N == len(pred_boxes), "pred_masks and pred_boxes must have same length"

    masks_bool = _decode_masks_to_torch_bool(pred_masks, h, w)  # (N, H, W)

    order = sorted(range(N), key=lambda i: float(pred_scores[i]), reverse=True)
    kept_idx: List[int] = []
    kept_masks: List[torch.Tensor] = []

    for i in order:
        cand = masks_bool[i].unsqueeze(0)  # (1, H, W)
        if len(kept_masks) == 0:
            kept_idx.append(i)
            kept_masks.append(masks_bool[i])
            continue

        kept_stack = torch.stack(kept_masks, dim=0)  # (K, H, W)
        iom_vals = mask_iom(cand, kept_stack).squeeze(0)  # (K,)
        if torch.any(iom_vals > iom_thresh):
            continue  # overlaps too much with a higher-scored kept mask
        kept_idx.append(i)
        kept_masks.append(masks_bool[i])

    kept_idx_sorted = sorted(kept_idx)

    # Build filtered JSON (this *does* modify fields; only for N>=2 case)
    out = dict(sample)
    out["pred_masks"] = [pred_masks[i] for i in kept_idx_sorted]
    out["pred_scores"] = [pred_scores[i] for i in kept_idx_sorted]
    if pred_boxes is not None:
        out["pred_boxes"] = [pred_boxes[i] for i in kept_idx_sorted]
    out["kept_indices"] = kept_idx_sorted
    out["removed_indices"] = [i for i in range(N) if i not in set(kept_idx_sorted)]
    out["iom_threshold"] = float(iom_thresh)
    return out



================================================
FILE: sam3/agent/helpers/masks.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

import copy
import itertools
from typing import Any, Iterator, List, Union

import numpy as np
import pycocotools.mask as mask_util
import torch
from torch import device

from .boxes import Boxes
from .memory import retry_if_cuda_oom
from .roi_align import ROIAlign


def polygon_area(x, y):
    # Using the shoelace formula
    # https://stackoverflow.com/questions/24467972/calculate-area-of-polygon-given-x-y-coordinates
    return 0.5 * np.abs(np.dot(x, np.roll(y, 1)) - np.dot(y, np.roll(x, 1)))


def polygons_to_bitmask(
    polygons: List[np.ndarray], height: int, width: int
) -> np.ndarray:
    """
    Args:
        polygons (list[ndarray]): each array has shape (Nx2,)
        height, width (int)

    Returns:
        ndarray: a bool mask of shape (height, width)
    """
    if len(polygons) == 0:
        # COCOAPI does not support empty polygons
        return np.zeros((height, width)).astype(bool)
    rles = mask_util.frPyObjects(polygons, height, width)
    rle = mask_util.merge(rles)
    return mask_util.decode(rle).astype(bool)


def rasterize_polygons_within_box(
    polygons: List[np.ndarray], box: np.ndarray, mask_size: int
) -> torch.Tensor:
    """
    Rasterize the polygons into a mask image and
    crop the mask content in the given box.
    The cropped mask is resized to (mask_size, mask_size).

    This function is used when generating training targets for mask head in Mask R-CNN.
    Given original ground-truth masks for an image, new ground-truth mask
    training targets in the size of `mask_size x mask_size`
    must be provided for each predicted box. This function will be called to
    produce such targets.

    Args:
        polygons (list[ndarray[float]]): a list of polygons, which represents an instance.
        box: 4-element numpy array
        mask_size (int):

    Returns:
        Tensor: BoolTensor of shape (mask_size, mask_size)
    """
    # 1. Shift the polygons w.r.t the boxes
    w, h = box[2] - box[0], box[3] - box[1]

    polygons = copy.deepcopy(polygons)
    for p in polygons:
        p[0::2] = p[0::2] - box[0]
        p[1::2] = p[1::2] - box[1]

    # 2. Rescale the polygons to the new box size
    # max() to avoid division by small number
    ratio_h = mask_size / max(h, 0.1)
    ratio_w = mask_size / max(w, 0.1)

    if ratio_h == ratio_w:
        for p in polygons:
            p *= ratio_h
    else:
        for p in polygons:
            p[0::2] *= ratio_w
            p[1::2] *= ratio_h

    # 3. Rasterize the polygons with coco api
    mask = polygons_to_bitmask(polygons, mask_size, mask_size)
    mask = torch.from_numpy(mask)
    return mask


class BitMasks:
    """
    This class stores the segmentation masks for all objects in one image, in
    the form of bitmaps.

    Attributes:
        tensor: bool Tensor of N,H,W, representing N instances in the image.
    """

    def __init__(self, tensor: Union[torch.Tensor, np.ndarray]):
        """
        Args:
            tensor: bool Tensor of N,H,W, representing N instances in the image.
        """
        if isinstance(tensor, torch.Tensor):
            tensor = tensor.to(torch.bool)
        else:
            tensor = torch.as_tensor(
                tensor, dtype=torch.bool, device=torch.device("cpu")
            )
        assert tensor.dim() == 3, tensor.size()
        self.image_size = tensor.shape[1:]
        self.tensor = tensor

    @torch.jit.unused
    def to(self, *args: Any, **kwargs: Any) -> "BitMasks":
        return BitMasks(self.tensor.to(*args, **kwargs))

    @property
    def device(self) -> torch.device:
        return self.tensor.device

    @torch.jit.unused
    def __getitem__(self, item: Union[int, slice, torch.BoolTensor]) -> "BitMasks":
        """
        Returns:
            BitMasks: Create a new :class:`BitMasks` by indexing.

        The following usage are allowed:

        1. `new_masks = masks[3]`: return a `BitMasks` which contains only one mask.
        2. `new_masks = masks[2:10]`: return a slice of masks.
        3. `new_masks = masks[vector]`, where vector is a torch.BoolTensor
           with `length = len(masks)`. Nonzero elements in the vector will be selected.

        Note that the returned object might share storage with this object,
        subject to Pytorch's indexing semantics.
        """
        if isinstance(item, int):
            return BitMasks(self.tensor[item].unsqueeze(0))
        m = self.tensor[item]
        assert m.dim() == 3, (
            "Indexing on BitMasks with {} returns a tensor with shape {}!".format(
                item, m.shape
            )
        )
        return BitMasks(m)

    @torch.jit.unused
    def __iter__(self) -> torch.Tensor:
        yield from self.tensor

    @torch.jit.unused
    def __repr__(self) -> str:
        s = self.__class__.__name__ + "("
        s += "num_instances={})".format(len(self.tensor))
        return s

    def __len__(self) -> int:
        return self.tensor.shape[0]

    def nonempty(self) -> torch.Tensor:
        """
        Find masks that are non-empty.

        Returns:
            Tensor: a BoolTensor which represents
                whether each mask is empty (False) or non-empty (True).
        """
        return self.tensor.flatten(1).any(dim=1)

    @staticmethod
    def from_polygon_masks(
        polygon_masks: Union["PolygonMasks", List[List[np.ndarray]]],
        height: int,
        width: int,
    ) -> "BitMasks":
        """
        Args:
            polygon_masks (list[list[ndarray]] or PolygonMasks)
            height, width (int)
        """
        if isinstance(polygon_masks, PolygonMasks):
            polygon_masks = polygon_masks.polygons
        masks = [polygons_to_bitmask(p, height, width) for p in polygon_masks]
        if len(masks):
            return BitMasks(torch.stack([torch.from_numpy(x) for x in masks]))
        else:
            return BitMasks(torch.empty(0, height, width, dtype=torch.bool))

    @staticmethod
    def from_roi_masks(roi_masks: "ROIMasks", height: int, width: int) -> "BitMasks":
        """
        Args:
            roi_masks:
            height, width (int):
        """
        return roi_masks.to_bitmasks(height, width)

    def crop_and_resize(self, boxes: torch.Tensor, mask_size: int) -> torch.Tensor:
        """
        Crop each bitmask by the given box, and resize results to (mask_size, mask_size).
        This can be used to prepare training targets for Mask R-CNN.
        It has less reconstruction error compared to rasterization with polygons.
        However we observe no difference in accuracy,
        but BitMasks requires more memory to store all the masks.

        Args:
            boxes (Tensor): Nx4 tensor storing the boxes for each mask
            mask_size (int): the size of the rasterized mask.

        Returns:
            Tensor:
                A bool tensor of shape (N, mask_size, mask_size), where
                N is the number of predicted boxes for this image.
        """
        assert len(boxes) == len(self), "{} != {}".format(len(boxes), len(self))
        device = self.tensor.device

        batch_inds = torch.arange(len(boxes), device=device).to(dtype=boxes.dtype)[
            :, None
        ]
        rois = torch.cat([batch_inds, boxes], dim=1)  # Nx5

        bit_masks = self.tensor.to(dtype=torch.float32)
        rois = rois.to(device=device)
        output = (
            ROIAlign((mask_size, mask_size), 1.0, 0, aligned=True)
            .forward(bit_masks[:, None, :, :], rois)
            .squeeze(1)
        )
        output = output >= 0.5
        return output

    def get_bounding_boxes(self) -> Boxes:
        """
        Returns:
            Boxes: tight bounding boxes around bitmasks.
            If a mask is empty, it's bounding box will be all zero.
        """
        boxes = torch.zeros(self.tensor.shape[0], 4, dtype=torch.float32)
        x_any = torch.any(self.tensor, dim=1)
        y_any = torch.any(self.tensor, dim=2)
        for idx in range(self.tensor.shape[0]):
            x = torch.where(x_any[idx, :])[0]
            y = torch.where(y_any[idx, :])[0]
            if len(x) > 0 and len(y) > 0:
                boxes[idx, :] = torch.as_tensor(
                    [x[0], y[0], x[-1] + 1, y[-1] + 1], dtype=torch.float32
                )
        return Boxes(boxes)

    @staticmethod
    def cat(bitmasks_list: List["BitMasks"]) -> "BitMasks":
        """
        Concatenates a list of BitMasks into a single BitMasks

        Arguments:
            bitmasks_list (list[BitMasks])

        Returns:
            BitMasks: the concatenated BitMasks
        """
        assert isinstance(bitmasks_list, (list, tuple))
        assert len(bitmasks_list) > 0
        assert all(isinstance(bitmask, BitMasks) for bitmask in bitmasks_list)

        cat_bitmasks = type(bitmasks_list[0])(
            torch.cat([bm.tensor for bm in bitmasks_list], dim=0)
        )
        return cat_bitmasks


class PolygonMasks:
    """
    This class stores the segmentation masks for all objects in one image, in the form of polygons.

    Attributes:
        polygons: list[list[ndarray]]. Each ndarray is a float64 vector representing a polygon.
    """

    def __init__(self, polygons: List[List[Union[torch.Tensor, np.ndarray]]]):
        """
        Arguments:
            polygons (list[list[np.ndarray]]): The first
                level of the list correspond to individual instances,
                the second level to all the polygons that compose the
                instance, and the third level to the polygon coordinates.
                The third level array should have the format of
                [x0, y0, x1, y1, ..., xn, yn] (n >= 3).
        """
        if not isinstance(polygons, list):
            raise ValueError(
                "Cannot create PolygonMasks: Expect a list of list of polygons per image. "
                "Got '{}' instead.".format(type(polygons))
            )

        def _make_array(t: Union[torch.Tensor, np.ndarray]) -> np.ndarray:
            # Use float64 for higher precision, because why not?
            # Always put polygons on CPU (self.to is a no-op) since they
            # are supposed to be small tensors.
            # May need to change this assumption if GPU placement becomes useful
            if isinstance(t, torch.Tensor):
                t = t.cpu().numpy()
            return np.asarray(t).astype("float64")

        def process_polygons(
            polygons_per_instance: List[Union[torch.Tensor, np.ndarray]],
        ) -> List[np.ndarray]:
            if not isinstance(polygons_per_instance, list):
                raise ValueError(
                    "Cannot create polygons: Expect a list of polygons per instance. "
                    "Got '{}' instead.".format(type(polygons_per_instance))
                )
            # transform each polygon to a numpy array
            polygons_per_instance = [_make_array(p) for p in polygons_per_instance]
            for polygon in polygons_per_instance:
                if len(polygon) % 2 != 0 or len(polygon) < 6:
                    raise ValueError(
                        f"Cannot create a polygon from {len(polygon)} coordinates."
                    )
            return polygons_per_instance

        self.polygons: List[List[np.ndarray]] = [
            process_polygons(polygons_per_instance)
            for polygons_per_instance in polygons
        ]

    def to(self, *args: Any, **kwargs: Any) -> "PolygonMasks":
        return self

    @property
    def device(self) -> torch.device:
        return torch.device("cpu")

    def get_bounding_boxes(self) -> Boxes:
        """
        Returns:
            Boxes: tight bounding boxes around polygon masks.
        """
        boxes = torch.zeros(len(self.polygons), 4, dtype=torch.float32)
        for idx, polygons_per_instance in enumerate(self.polygons):
            minxy = torch.as_tensor([float("inf"), float("inf")], dtype=torch.float32)
            maxxy = torch.zeros(2, dtype=torch.float32)
            for polygon in polygons_per_instance:
                coords = torch.from_numpy(polygon).view(-1, 2).to(dtype=torch.float32)
                minxy = torch.min(minxy, torch.min(coords, dim=0).values)
                maxxy = torch.max(maxxy, torch.max(coords, dim=0).values)
            boxes[idx, :2] = minxy
            boxes[idx, 2:] = maxxy
        return Boxes(boxes)

    def nonempty(self) -> torch.Tensor:
        """
        Find masks that are non-empty.

        Returns:
            Tensor:
                a BoolTensor which represents whether each mask is empty (False) or not (True).
        """
        keep = [1 if len(polygon) > 0 else 0 for polygon in self.polygons]
        return torch.from_numpy(np.asarray(keep, dtype=bool))

    def __getitem__(
        self, item: Union[int, slice, List[int], torch.BoolTensor]
    ) -> "PolygonMasks":
        """
        Support indexing over the instances and return a `PolygonMasks` object.
        `item` can be:

        1. An integer. It will return an object with only one instance.
        2. A slice. It will return an object with the selected instances.
        3. A list[int]. It will return an object with the selected instances,
           correpsonding to the indices in the list.
        4. A vector mask of type BoolTensor, whose length is num_instances.
           It will return an object with the instances whose mask is nonzero.
        """
        if isinstance(item, int):
            selected_polygons = [self.polygons[item]]
        elif isinstance(item, slice):
            selected_polygons = self.polygons[item]
        elif isinstance(item, list):
            selected_polygons = [self.polygons[i] for i in item]
        elif isinstance(item, torch.Tensor):
            # Polygons is a list, so we have to move the indices back to CPU.
            if item.dtype == torch.bool:
                assert item.dim() == 1, item.shape
                item = item.nonzero().squeeze(1).cpu().numpy().tolist()
            elif item.dtype in [torch.int32, torch.int64]:
                item = item.cpu().numpy().tolist()
            else:
                raise ValueError(
                    "Unsupported tensor dtype={} for indexing!".format(item.dtype)
                )
            selected_polygons = [self.polygons[i] for i in item]
        return PolygonMasks(selected_polygons)

    def __iter__(self) -> Iterator[List[np.ndarray]]:
        """
        Yields:
            list[ndarray]: the polygons for one instance.
            Each Tensor is a float64 vector representing a polygon.
        """
        return iter(self.polygons)

    def __repr__(self) -> str:
        s = self.__class__.__name__ + "("
        s += "num_instances={})".format(len(self.polygons))
        return s

    def __len__(self) -> int:
        return len(self.polygons)

    def crop_and_resize(self, boxes: torch.Tensor, mask_size: int) -> torch.Tensor:
        """
        Crop each mask by the given box, and resize results to (mask_size, mask_size).
        This can be used to prepare training targets for Mask R-CNN.

        Args:
            boxes (Tensor): Nx4 tensor storing the boxes for each mask
            mask_size (int): the size of the rasterized mask.

        Returns:
            Tensor: A bool tensor of shape (N, mask_size, mask_size), where
            N is the number of predicted boxes for this image.
        """
        assert len(boxes) == len(self), "{} != {}".format(len(boxes), len(self))

        device = boxes.device
        # Put boxes on the CPU, as the polygon representation is not efficient GPU-wise
        # (several small tensors for representing a single instance mask)
        boxes = boxes.to(torch.device("cpu"))

        results = [
            rasterize_polygons_within_box(poly, box.numpy(), mask_size)
            for poly, box in zip(self.polygons, boxes)
        ]
        """
        poly: list[list[float]], the polygons for one instance
        box: a tensor of shape (4,)
        """
        if len(results) == 0:
            return torch.empty(0, mask_size, mask_size, dtype=torch.bool, device=device)
        return torch.stack(results, dim=0).to(device=device)

    def area(self):
        """
        Computes area of the mask.
        Only works with Polygons, using the shoelace formula:
        https://stackoverflow.com/questions/24467972/calculate-area-of-polygon-given-x-y-coordinates

        Returns:
            Tensor: a vector, area for each instance
        """

        area = []
        for polygons_per_instance in self.polygons:
            area_per_instance = 0
            for p in polygons_per_instance:
                area_per_instance += polygon_area(p[0::2], p[1::2])
            area.append(area_per_instance)

        return torch.tensor(area)

    @staticmethod
    def cat(polymasks_list: List["PolygonMasks"]) -> "PolygonMasks":
        """
        Concatenates a list of PolygonMasks into a single PolygonMasks

        Arguments:
            polymasks_list (list[PolygonMasks])

        Returns:
            PolygonMasks: the concatenated PolygonMasks
        """
        assert isinstance(polymasks_list, (list, tuple))
        assert len(polymasks_list) > 0
        assert all(isinstance(polymask, PolygonMasks) for polymask in polymasks_list)

        cat_polymasks = type(polymasks_list[0])(
            list(itertools.chain.from_iterable(pm.polygons for pm in polymasks_list))
        )
        return cat_polymasks


class ROIMasks:
    """
    Represent masks by N smaller masks defined in some ROIs. Once ROI boxes are given,
    full-image bitmask can be obtained by "pasting" the mask on the region defined
    by the corresponding ROI box.
    """

    def __init__(self, tensor: torch.Tensor):
        """
        Args:
            tensor: (N, M, M) mask tensor that defines the mask within each ROI.
        """
        if tensor.dim() != 3:
            raise ValueError("ROIMasks must take a masks of 3 dimension.")
        self.tensor = tensor

    def to(self, device: torch.device) -> "ROIMasks":
        return ROIMasks(self.tensor.to(device))

    @property
    def device(self) -> device:
        return self.tensor.device

    def __len__(self):
        return self.tensor.shape[0]

    def __getitem__(self, item) -> "ROIMasks":
        """
        Returns:
            ROIMasks: Create a new :class:`ROIMasks` by indexing.

        The following usage are allowed:

        1. `new_masks = masks[2:10]`: return a slice of masks.
        2. `new_masks = masks[vector]`, where vector is a torch.BoolTensor
           with `length = len(masks)`. Nonzero elements in the vector will be selected.

        Note that the returned object might share storage with this object,
        subject to Pytorch's indexing semantics.
        """
        t = self.tensor[item]
        if t.dim() != 3:
            raise ValueError(
                f"Indexing on ROIMasks with {item} returns a tensor with shape {t.shape}!"
            )
        return ROIMasks(t)

    @torch.jit.unused
    def __repr__(self) -> str:
        s = self.__class__.__name__ + "("
        s += "num_instances={})".format(len(self.tensor))
        return s

    @torch.jit.unused
    def to_bitmasks(self, boxes: torch.Tensor, height, width, threshold=0.5):
        """
        Args: see documentation of :func:`paste_masks_in_image`.
        """
        from detectron2.layers.mask_ops import (
            _paste_masks_tensor_shape,
            paste_masks_in_image,
        )

        if torch.jit.is_tracing():
            if isinstance(height, torch.Tensor):
                paste_func = _paste_masks_tensor_shape
            else:
                paste_func = paste_masks_in_image
        else:
            paste_func = retry_if_cuda_oom(paste_masks_in_image)
        bitmasks = paste_func(
            self.tensor, boxes.tensor, (height, width), threshold=threshold
        )
        return BitMasks(bitmasks)



================================================
FILE: sam3/agent/helpers/memory.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

import logging
from contextlib import contextmanager
from functools import wraps

import torch

__all__ = ["retry_if_cuda_oom"]


@contextmanager
def _ignore_torch_cuda_oom():
    """
    A context which ignores CUDA OOM exception from pytorch.
    """
    try:
        yield
    except RuntimeError as e:
        # NOTE: the string may change?
        if "CUDA out of memory. " in str(e):
            pass
        else:
            raise


def retry_if_cuda_oom(func):
    """
    Makes a function retry itself after encountering
    pytorch's CUDA OOM error.
    It will first retry after calling `torch.cuda.empty_cache()`.

    If that still fails, it will then retry by trying to convert inputs to CPUs.
    In this case, it expects the function to dispatch to CPU implementation.
    The return values may become CPU tensors as well and it's user's
    responsibility to convert it back to CUDA tensor if needed.

    Args:
        func: a stateless callable that takes tensor-like objects as arguments

    Returns:
        a callable which retries `func` if OOM is encountered.

    Examples:
    ::
        output = retry_if_cuda_oom(some_torch_function)(input1, input2)
        # output may be on CPU even if inputs are on GPU

    Note:
        1. When converting inputs to CPU, it will only look at each argument and check
           if it has `.device` and `.to` for conversion. Nested structures of tensors
           are not supported.

        2. Since the function might be called more than once, it has to be
           stateless.
    """

    def maybe_to_cpu(x):
        try:
            like_gpu_tensor = x.device.type == "cuda" and hasattr(x, "to")
        except AttributeError:
            like_gpu_tensor = False
        if like_gpu_tensor:
            return x.to(device="cpu")
        else:
            return x

    @wraps(func)
    def wrapped(*args, **kwargs):
        with _ignore_torch_cuda_oom():
            return func(*args, **kwargs)

        # Clear cache and retry
        torch.cuda.empty_cache()
        with _ignore_torch_cuda_oom():
            return func(*args, **kwargs)

        # Try on CPU. This slows down the code significantly, therefore print a notice.
        logger = logging.getLogger(__name__)
        logger.info(
            "Attempting to copy inputs of {} to CPU due to CUDA OOM".format(str(func))
        )
        new_args = (maybe_to_cpu(x) for x in args)
        new_kwargs = {k: maybe_to_cpu(v) for k, v in kwargs.items()}
        return func(*new_args, **new_kwargs)

    return wrapped



================================================
FILE: sam3/agent/helpers/rle.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

"""Some utilities for RLE encoding that doesn't require downloading the masks to the cpu"""

import numpy as np
import torch
from pycocotools import mask as mask_util


@torch.no_grad()
def rle_encode(orig_mask, return_areas=False):
    """Encodes a collection of masks in RLE format

    This function emulates the behavior of the COCO API's encode function, but
    is executed partially on the GPU for faster execution.

    Args:
        mask (torch.Tensor): A mask of shape (N, H, W) with dtype=torch.bool
        return_areas (bool): If True, add the areas of the masks as a part of
            the RLE output dict under the "area" key. Default is False.

    Returns:
        str: The RLE encoded masks
    """
    assert orig_mask.ndim == 3, "Mask must be of shape (N, H, W)"
    assert orig_mask.dtype == torch.bool, "Mask must have dtype=torch.bool"

    if orig_mask.numel() == 0:
        return []

    # First, transpose the spatial dimensions.
    # This is necessary because the COCO API uses Fortran order
    mask = orig_mask.transpose(1, 2)

    # Flatten the mask
    flat_mask = mask.reshape(mask.shape[0], -1)
    if return_areas:
        mask_areas = flat_mask.sum(-1).tolist()
    # Find the indices where the mask changes
    differences = torch.ones(
        mask.shape[0], flat_mask.shape[1] + 1, device=mask.device, dtype=torch.bool
    )
    differences[:, 1:-1] = flat_mask[:, :-1] != flat_mask[:, 1:]
    differences[:, 0] = flat_mask[:, 0]
    _, change_indices = torch.where(differences)

    try:
        boundaries = torch.cumsum(differences.sum(-1), 0).cpu()
    except RuntimeError as _:
        boundaries = torch.cumsum(differences.cpu().sum(-1), 0)

    change_indices_clone = change_indices.clone()
    # First pass computes the RLEs on GPU, in a flatten format
    for i in range(mask.shape[0]):
        # Get the change indices for this batch item
        beg = 0 if i == 0 else boundaries[i - 1].item()
        end = boundaries[i].item()
        change_indices[beg + 1 : end] -= change_indices_clone[beg : end - 1]

    # Now we can split the RLES of each batch item, and convert them to strings
    # No more gpu at this point
    change_indices = change_indices.tolist()

    batch_rles = []
    # Process each mask in the batch separately
    for i in range(mask.shape[0]):
        beg = 0 if i == 0 else boundaries[i - 1].item()
        end = boundaries[i].item()
        run_lengths = change_indices[beg:end]

        uncompressed_rle = {"counts": run_lengths, "size": list(orig_mask.shape[1:])}
        h, w = uncompressed_rle["size"]
        rle = mask_util.frPyObjects(uncompressed_rle, h, w)
        rle["counts"] = rle["counts"].decode("utf-8")
        if return_areas:
            rle["area"] = mask_areas[i]
        batch_rles.append(rle)

    return batch_rles


def robust_rle_encode(masks):
    """Encodes a collection of masks in RLE format. Uses the gpu version fist, falls back to the cpu version if it fails"""

    assert masks.ndim == 3, "Mask must be of shape (N, H, W)"
    assert masks.dtype == torch.bool, "Mask must have dtype=torch.bool"

    try:
        return rle_encode(masks)
    except RuntimeError as _:
        masks = masks.cpu().numpy()
        rles = [
            mask_util.encode(
                np.array(mask[:, :, np.newaxis], dtype=np.uint8, order="F")
            )[0]
            for mask in masks
        ]
        for rle in rles:
            rle["counts"] = rle["counts"].decode("utf-8")
        return rles


def ann_to_rle(segm, im_info):
    """Convert annotation which can be polygons, uncompressed RLE to RLE.
    Args:
        ann (dict) : annotation object
    Returns:
        ann (rle)
    """
    h, w = im_info["height"], im_info["width"]
    if isinstance(segm, list):
        # polygon -- a single object might consist of multiple parts
        # we merge all parts into one mask rle code
        rles = mask_util.frPyObjects(segm, h, w)
        rle = mask_util.merge(rles)
    elif isinstance(segm["counts"], list):
        # uncompressed RLE
        rle = mask_util.frPyObjects(segm, h, w)
    else:
        # rle
        rle = segm
    return rle



================================================
FILE: sam3/agent/helpers/roi_align.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

from torch import nn
from torchvision.ops import roi_align


# NOTE: torchvision's RoIAlign has a different default aligned=False
class ROIAlign(nn.Module):
    def __init__(self, output_size, spatial_scale, sampling_ratio, aligned=True):
        """
        Args:
            output_size (tuple): h, w
            spatial_scale (float): scale the input boxes by this number
            sampling_ratio (int): number of inputs samples to take for each output
                sample. 0 to take samples densely.
            aligned (bool): if False, use the legacy implementation in
                Detectron. If True, align the results more perfectly.

        Note:
            The meaning of aligned=True:

            Given a continuous coordinate c, its two neighboring pixel indices (in our
            pixel model) are computed by floor(c - 0.5) and ceil(c - 0.5). For example,
            c=1.3 has pixel neighbors with discrete indices [0] and [1] (which are sampled
            from the underlying signal at continuous coordinates 0.5 and 1.5). But the original
            roi_align (aligned=False) does not subtract the 0.5 when computing neighboring
            pixel indices and therefore it uses pixels with a slightly incorrect alignment
            (relative to our pixel model) when performing bilinear interpolation.

            With `aligned=True`,
            we first appropriately scale the ROI and then shift it by -0.5
            prior to calling roi_align. This produces the correct neighbors; see
            detectron2/tests/test_roi_align.py for verification.

            The difference does not make a difference to the model's performance if
            ROIAlign is used together with conv layers.
        """
        super().__init__()
        self.output_size = output_size
        self.spatial_scale = spatial_scale
        self.sampling_ratio = sampling_ratio
        self.aligned = aligned

        from torchvision import __version__

        version = tuple(int(x) for x in __version__.split(".")[:2])
        # https://github.com/pytorch/vision/pull/2438
        assert version >= (0, 7), "Require torchvision >= 0.7"

    def forward(self, input, rois):
        """
        Args:
            input: NCHW images
            rois: Bx5 boxes. First column is the index into N. The other 4 columns are xyxy.
        """
        assert rois.dim() == 2 and rois.size(1) == 5
        if input.is_quantized:
            input = input.dequantize()
        return roi_align(
            input,
            rois.to(dtype=input.dtype),
            self.output_size,
            self.spatial_scale,
            self.sampling_ratio,
            self.aligned,
        )

    def __repr__(self):
        tmpstr = self.__class__.__name__ + "("
        tmpstr += "output_size=" + str(self.output_size)
        tmpstr += ", spatial_scale=" + str(self.spatial_scale)
        tmpstr += ", sampling_ratio=" + str(self.sampling_ratio)
        tmpstr += ", aligned=" + str(self.aligned)
        tmpstr += ")"
        return tmpstr



================================================
FILE: sam3/agent/helpers/rotated_boxes.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

from __future__ import absolute_import, division, print_function, unicode_literals

import math
from typing import List, Tuple

import torch

# from detectron2.layers.rotated_boxes import pairwise_iou_rotated

from .boxes import Boxes


def pairwise_iou_rotated(boxes1, boxes2):
    """
    Return intersection-over-union (Jaccard index) of boxes.

    Both sets of boxes are expected to be in
    (x_center, y_center, width, height, angle) format.

    Arguments:
        boxes1 (Tensor[N, 5])
        boxes2 (Tensor[M, 5])

    Returns:
        iou (Tensor[N, M]): the NxM matrix containing the pairwise
            IoU values for every element in boxes1 and boxes2
    """
    return torch.ops.detectron2.box_iou_rotated(boxes1, boxes2)


class RotatedBoxes(Boxes):
    """
    This structure stores a list of rotated boxes as a Nx5 torch.Tensor.
    It supports some common methods about boxes
    (`area`, `clip`, `nonempty`, etc),
    and also behaves like a Tensor
    (support indexing, `to(device)`, `.device`, and iteration over all boxes)
    """

    def __init__(self, tensor: torch.Tensor):
        """
        Args:
            tensor (Tensor[float]): a Nx5 matrix.  Each row is
                (x_center, y_center, width, height, angle),
                in which angle is represented in degrees.
                While there's no strict range restriction for it,
                the recommended principal range is between [-180, 180) degrees.

        Assume we have a horizontal box B = (x_center, y_center, width, height),
        where width is along the x-axis and height is along the y-axis.
        The rotated box B_rot (x_center, y_center, width, height, angle)
        can be seen as:

        1. When angle == 0:
           B_rot == B
        2. When angle > 0:
           B_rot is obtained by rotating B w.r.t its center by :math:`|angle|` degrees CCW;
        3. When angle < 0:
           B_rot is obtained by rotating B w.r.t its center by :math:`|angle|` degrees CW.

        Mathematically, since the right-handed coordinate system for image space
        is (y, x), where y is top->down and x is left->right, the 4 vertices of the
        rotated rectangle :math:`(yr_i, xr_i)` (i = 1, 2, 3, 4) can be obtained from
        the vertices of the horizontal rectangle :math:`(y_i, x_i)` (i = 1, 2, 3, 4)
        in the following way (:math:`\\theta = angle*\\pi/180` is the angle in radians,
        :math:`(y_c, x_c)` is the center of the rectangle):

        .. math::

            yr_i = \\cos(\\theta) (y_i - y_c) - \\sin(\\theta) (x_i - x_c) + y_c,

            xr_i = \\sin(\\theta) (y_i - y_c) + \\cos(\\theta) (x_i - x_c) + x_c,

        which is the standard rigid-body rotation transformation.

        Intuitively, the angle is
        (1) the rotation angle from y-axis in image space
        to the height vector (top->down in the box's local coordinate system)
        of the box in CCW, and
        (2) the rotation angle from x-axis in image space
        to the width vector (left->right in the box's local coordinate system)
        of the box in CCW.

        More intuitively, consider the following horizontal box ABCD represented
        in (x1, y1, x2, y2): (3, 2, 7, 4),
        covering the [3, 7] x [2, 4] region of the continuous coordinate system
        which looks like this:

        .. code:: none

            O--------> x
            |
            |  A---B
            |  |   |
            |  D---C
            |
            v y

        Note that each capital letter represents one 0-dimensional geometric point
        instead of a 'square pixel' here.

        In the example above, using (x, y) to represent a point we have:

        .. math::

            O = (0, 0), A = (3, 2), B = (7, 2), C = (7, 4), D = (3, 4)

        We name vector AB = vector DC as the width vector in box's local coordinate system, and
        vector AD = vector BC as the height vector in box's local coordinate system. Initially,
        when angle = 0 degree, they're aligned with the positive directions of x-axis and y-axis
        in the image space, respectively.

        For better illustration, we denote the center of the box as E,

        .. code:: none

            O--------> x
            |
            |  A---B
            |  | E |
            |  D---C
            |
            v y

        where the center E = ((3+7)/2, (2+4)/2) = (5, 3).

        Also,

        .. math::

            width = |AB| = |CD| = 7 - 3 = 4,
            height = |AD| = |BC| = 4 - 2 = 2.

        Therefore, the corresponding representation for the same shape in rotated box in
        (x_center, y_center, width, height, angle) format is:

        (5, 3, 4, 2, 0),

        Now, let's consider (5, 3, 4, 2, 90), which is rotated by 90 degrees
        CCW (counter-clockwise) by definition. It looks like this:

        .. code:: none

            O--------> x
            |   B-C
            |   | |
            |   |E|
            |   | |
            |   A-D
            v y

        The center E is still located at the same point (5, 3), while the vertices
        ABCD are rotated by 90 degrees CCW with regard to E:
        A = (4, 5), B = (4, 1), C = (6, 1), D = (6, 5)

        Here, 90 degrees can be seen as the CCW angle to rotate from y-axis to
        vector AD or vector BC (the top->down height vector in box's local coordinate system),
        or the CCW angle to rotate from x-axis to vector AB or vector DC (the left->right
        width vector in box's local coordinate system).

        .. math::

            width = |AB| = |CD| = 5 - 1 = 4,
            height = |AD| = |BC| = 6 - 4 = 2.

        Next, how about (5, 3, 4, 2, -90), which is rotated by 90 degrees CW (clockwise)
        by definition? It looks like this:

        .. code:: none

            O--------> x
            |   D-A
            |   | |
            |   |E|
            |   | |
            |   C-B
            v y

        The center E is still located at the same point (5, 3), while the vertices
        ABCD are rotated by 90 degrees CW with regard to E:
        A = (6, 1), B = (6, 5), C = (4, 5), D = (4, 1)

        .. math::

            width = |AB| = |CD| = 5 - 1 = 4,
            height = |AD| = |BC| = 6 - 4 = 2.

        This covers exactly the same region as (5, 3, 4, 2, 90) does, and their IoU
        will be 1. However, these two will generate different RoI Pooling results and
        should not be treated as an identical box.

        On the other hand, it's easy to see that (X, Y, W, H, A) is identical to
        (X, Y, W, H, A+360N), for any integer N. For example (5, 3, 4, 2, 270) would be
        identical to (5, 3, 4, 2, -90), because rotating the shape 270 degrees CCW is
        equivalent to rotating the same shape 90 degrees CW.

        We could rotate further to get (5, 3, 4, 2, 180), or (5, 3, 4, 2, -180):

        .. code:: none

            O--------> x
            |
            |  C---D
            |  | E |
            |  B---A
            |
            v y

        .. math::

            A = (7, 4), B = (3, 4), C = (3, 2), D = (7, 2),

            width = |AB| = |CD| = 7 - 3 = 4,
            height = |AD| = |BC| = 4 - 2 = 2.

        Finally, this is a very inaccurate (heavily quantized) illustration of
        how (5, 3, 4, 2, 60) looks like in case anyone wonders:

        .. code:: none

            O--------> x
            |     B\
            |    /  C
            |   /E /
            |  A  /
            |   `D
            v y

        It's still a rectangle with center of (5, 3), width of 4 and height of 2,
        but its angle (and thus orientation) is somewhere between
        (5, 3, 4, 2, 0) and (5, 3, 4, 2, 90).
        """
        device = (
            tensor.device if isinstance(tensor, torch.Tensor) else torch.device("cpu")
        )
        tensor = torch.as_tensor(tensor, dtype=torch.float32, device=device)
        if tensor.numel() == 0:
            # Use reshape, so we don't end up creating a new tensor that does not depend on
            # the inputs (and consequently confuses jit)
            tensor = tensor.reshape((0, 5)).to(dtype=torch.float32, device=device)
        assert tensor.dim() == 2 and tensor.size(-1) == 5, tensor.size()

        self.tensor = tensor

    def clone(self) -> "RotatedBoxes":
        """
        Clone the RotatedBoxes.

        Returns:
            RotatedBoxes
        """
        return RotatedBoxes(self.tensor.clone())

    def to(self, device: torch.device, non_blocking: bool = False):
        # Boxes are assumed float32 and does not support to(dtype)
        return RotatedBoxes(self.tensor.to(device=device, non_blocking=non_blocking))

    def area(self) -> torch.Tensor:
        """
        Computes the area of all the boxes.

        Returns:
            torch.Tensor: a vector with areas of each box.
        """
        box = self.tensor
        area = box[:, 2] * box[:, 3]
        return area

    # Avoid in-place operations so that we can torchscript; NOTE: this creates a new tensor
    def normalize_angles(self) -> None:
        """
        Restrict angles to the range of [-180, 180) degrees
        """
        angle_tensor = (self.tensor[:, 4] + 180.0) % 360.0 - 180.0
        self.tensor = torch.cat((self.tensor[:, :4], angle_tensor[:, None]), dim=1)

    def clip(
        self, box_size: Tuple[int, int], clip_angle_threshold: float = 1.0
    ) -> None:
        """
        Clip (in place) the boxes by limiting x coordinates to the range [0, width]
        and y coordinates to the range [0, height].

        For RRPN:
        Only clip boxes that are almost horizontal with a tolerance of
        clip_angle_threshold to maintain backward compatibility.

        Rotated boxes beyond this threshold are not clipped for two reasons:

        1. There are potentially multiple ways to clip a rotated box to make it
           fit within the image.
        2. It's tricky to make the entire rectangular box fit within the image
           and still be able to not leave out pixels of interest.

        Therefore we rely on ops like RoIAlignRotated to safely handle this.

        Args:
            box_size (height, width): The clipping box's size.
            clip_angle_threshold:
                Iff. abs(normalized(angle)) <= clip_angle_threshold (in degrees),
                we do the clipping as horizontal boxes.
        """
        h, w = box_size

        # normalize angles to be within (-180, 180] degrees
        self.normalize_angles()

        idx = torch.where(torch.abs(self.tensor[:, 4]) <= clip_angle_threshold)[0]

        # convert to (x1, y1, x2, y2)
        x1 = self.tensor[idx, 0] - self.tensor[idx, 2] / 2.0
        y1 = self.tensor[idx, 1] - self.tensor[idx, 3] / 2.0
        x2 = self.tensor[idx, 0] + self.tensor[idx, 2] / 2.0
        y2 = self.tensor[idx, 1] + self.tensor[idx, 3] / 2.0

        # clip
        x1.clamp_(min=0, max=w)
        y1.clamp_(min=0, max=h)
        x2.clamp_(min=0, max=w)
        y2.clamp_(min=0, max=h)

        # convert back to (xc, yc, w, h)
        self.tensor[idx, 0] = (x1 + x2) / 2.0
        self.tensor[idx, 1] = (y1 + y2) / 2.0
        # make sure widths and heights do not increase due to numerical errors
        self.tensor[idx, 2] = torch.min(self.tensor[idx, 2], x2 - x1)
        self.tensor[idx, 3] = torch.min(self.tensor[idx, 3], y2 - y1)

    def nonempty(self, threshold: float = 0.0) -> torch.Tensor:
        """
        Find boxes that are non-empty.
        A box is considered empty, if either of its side is no larger than threshold.

        Returns:
            Tensor: a binary vector which represents
            whether each box is empty (False) or non-empty (True).
        """
        box = self.tensor
        widths = box[:, 2]
        heights = box[:, 3]
        keep = (widths > threshold) & (heights > threshold)
        return keep

    def __getitem__(self, item) -> "RotatedBoxes":
        """
        Returns:
            RotatedBoxes: Create a new :class:`RotatedBoxes` by indexing.

        The following usage are allowed:

        1. `new_boxes = boxes[3]`: return a `RotatedBoxes` which contains only one box.
        2. `new_boxes = boxes[2:10]`: return a slice of boxes.
        3. `new_boxes = boxes[vector]`, where vector is a torch.ByteTensor
           with `length = len(boxes)`. Nonzero elements in the vector will be selected.

        Note that the returned RotatedBoxes might share storage with this RotatedBoxes,
        subject to Pytorch's indexing semantics.
        """
        if isinstance(item, int):
            return RotatedBoxes(self.tensor[item].view(1, -1))
        b = self.tensor[item]
        assert b.dim() == 2, (
            "Indexing on RotatedBoxes with {} failed to return a matrix!".format(item)
        )
        return RotatedBoxes(b)

    def __len__(self) -> int:
        return self.tensor.shape[0]

    def __repr__(self) -> str:
        return "RotatedBoxes(" + str(self.tensor) + ")"

    def inside_box(
        self, box_size: Tuple[int, int], boundary_threshold: int = 0
    ) -> torch.Tensor:
        """
        Args:
            box_size (height, width): Size of the reference box covering
                [0, width] x [0, height]
            boundary_threshold (int): Boxes that extend beyond the reference box
                boundary by more than boundary_threshold are considered "outside".

        For RRPN, it might not be necessary to call this function since it's common
        for rotated box to extend to outside of the image boundaries
        (the clip function only clips the near-horizontal boxes)

        Returns:
            a binary vector, indicating whether each box is inside the reference box.
        """
        height, width = box_size

        cnt_x = self.tensor[..., 0]
        cnt_y = self.tensor[..., 1]
        half_w = self.tensor[..., 2] / 2.0
        half_h = self.tensor[..., 3] / 2.0
        a = self.tensor[..., 4]
        c = torch.abs(torch.cos(a * math.pi / 180.0))
        s = torch.abs(torch.sin(a * math.pi / 180.0))
        # This basically computes the horizontal bounding rectangle of the rotated box
        max_rect_dx = c * half_w + s * half_h
        max_rect_dy = c * half_h + s * half_w

        inds_inside = (
            (cnt_x - max_rect_dx >= -boundary_threshold)
            & (cnt_y - max_rect_dy >= -boundary_threshold)
            & (cnt_x + max_rect_dx < width + boundary_threshold)
            & (cnt_y + max_rect_dy < height + boundary_threshold)
        )

        return inds_inside

    def get_centers(self) -> torch.Tensor:
        """
        Returns:
            The box centers in a Nx2 array of (x, y).
        """
        return self.tensor[:, :2]

    def scale(self, scale_x: float, scale_y: float) -> None:
        """
        Scale the rotated box with horizontal and vertical scaling factors
        Note: when scale_factor_x != scale_factor_y,
        the rotated box does not preserve the rectangular shape when the angle
        is not a multiple of 90 degrees under resize transformation.
        Instead, the shape is a parallelogram (that has skew)
        Here we make an approximation by fitting a rotated rectangle to the parallelogram.
        """
        self.tensor[:, 0] *= scale_x
        self.tensor[:, 1] *= scale_y
        theta = self.tensor[:, 4] * math.pi / 180.0
        c = torch.cos(theta)
        s = torch.sin(theta)

        # In image space, y is top->down and x is left->right
        # Consider the local coordintate system for the rotated box,
        # where the box center is located at (0, 0), and the four vertices ABCD are
        # A(-w / 2, -h / 2), B(w / 2, -h / 2), C(w / 2, h / 2), D(-w / 2, h / 2)
        # the midpoint of the left edge AD of the rotated box E is:
        # E = (A+D)/2 = (-w / 2, 0)
        # the midpoint of the top edge AB of the rotated box F is:
        # F(0, -h / 2)
        # To get the old coordinates in the global system, apply the rotation transformation
        # (Note: the right-handed coordinate system for image space is yOx):
        # (old_x, old_y) = (s * y + c * x, c * y - s * x)
        # E(old) = (s * 0 + c * (-w/2), c * 0 - s * (-w/2)) = (-c * w / 2, s * w / 2)
        # F(old) = (s * (-h / 2) + c * 0, c * (-h / 2) - s * 0) = (-s * h / 2, -c * h / 2)
        # After applying the scaling factor (sfx, sfy):
        # E(new) = (-sfx * c * w / 2, sfy * s * w / 2)
        # F(new) = (-sfx * s * h / 2, -sfy * c * h / 2)
        # The new width after scaling tranformation becomes:

        # w(new) = |E(new) - O| * 2
        #        = sqrt[(sfx * c * w / 2)^2 + (sfy * s * w / 2)^2] * 2
        #        = sqrt[(sfx * c)^2 + (sfy * s)^2] * w
        # i.e., scale_factor_w = sqrt[(sfx * c)^2 + (sfy * s)^2]
        #
        # For example,
        # when angle = 0 or 180, |c| = 1, s = 0, scale_factor_w == scale_factor_x;
        # when |angle| = 90, c = 0, |s| = 1, scale_factor_w == scale_factor_y
        self.tensor[:, 2] *= torch.sqrt((scale_x * c) ** 2 + (scale_y * s) ** 2)

        # h(new) = |F(new) - O| * 2
        #        = sqrt[(sfx * s * h / 2)^2 + (sfy * c * h / 2)^2] * 2
        #        = sqrt[(sfx * s)^2 + (sfy * c)^2] * h
        # i.e., scale_factor_h = sqrt[(sfx * s)^2 + (sfy * c)^2]
        #
        # For example,
        # when angle = 0 or 180, |c| = 1, s = 0, scale_factor_h == scale_factor_y;
        # when |angle| = 90, c = 0, |s| = 1, scale_factor_h == scale_factor_x
        self.tensor[:, 3] *= torch.sqrt((scale_x * s) ** 2 + (scale_y * c) ** 2)

        # The angle is the rotation angle from y-axis in image space to the height
        # vector (top->down in the box's local coordinate system) of the box in CCW.
        #
        # angle(new) = angle_yOx(O - F(new))
        #            = angle_yOx( (sfx * s * h / 2, sfy * c * h / 2) )
        #            = atan2(sfx * s * h / 2, sfy * c * h / 2)
        #            = atan2(sfx * s, sfy * c)
        #
        # For example,
        # when sfx == sfy, angle(new) == atan2(s, c) == angle(old)
        self.tensor[:, 4] = torch.atan2(scale_x * s, scale_y * c) * 180 / math.pi

    @classmethod
    def cat(cls, boxes_list: List["RotatedBoxes"]) -> "RotatedBoxes":
        """
        Concatenates a list of RotatedBoxes into a single RotatedBoxes

        Arguments:
            boxes_list (list[RotatedBoxes])

        Returns:
            RotatedBoxes: the concatenated RotatedBoxes
        """
        assert isinstance(boxes_list, (list, tuple))
        if len(boxes_list) == 0:
            return cls(torch.empty(0))
        assert all([isinstance(box, RotatedBoxes) for box in boxes_list])

        # use torch.cat (v.s. layers.cat) so the returned boxes never share storage with input
        cat_boxes = cls(torch.cat([b.tensor for b in boxes_list], dim=0))
        return cat_boxes

    @property
    def device(self) -> torch.device:
        return self.tensor.device

    @torch.jit.unused
    def __iter__(self):
        """
        Yield a box as a Tensor of shape (5,) at a time.
        """
        yield from self.tensor


def pairwise_iou(boxes1: RotatedBoxes, boxes2: RotatedBoxes) -> None:
    """
    Given two lists of rotated boxes of size N and M,
    compute the IoU (intersection over union)
    between **all** N x M pairs of boxes.
    The box order must be (x_center, y_center, width, height, angle).

    Args:
        boxes1, boxes2 (RotatedBoxes):
            two `RotatedBoxes`. Contains N & M rotated boxes, respectively.

    Returns:
        Tensor: IoU, sized [N,M].
    """

    return pairwise_iou_rotated(boxes1.tensor, boxes2.tensor)



================================================
FILE: sam3/agent/helpers/som_utils.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

import colorsys
from dataclasses import dataclass
from typing import List, Tuple

import cv2
import matplotlib as mpl
import matplotlib.colors as mplc
import numpy as np
import pycocotools.mask as mask_utils


def rgb_to_hex(rgb_color):
    """
    Convert a rgb color to hex color.

    Args:
        rgb_color (tuple/list of ints): RGB color in tuple or list format.

    Returns:
        str: Hex color.

    Example:
        ```
        >>> rgb_to_hex((255, 0, 244))
        '#ff00ff'
        ```
    """
    return "#" + "".join([hex(c)[2:].zfill(2) for c in rgb_color])


# DEFAULT_COLOR_HEX_TO_NAME = {
#     rgb_to_hex((255, 0, 0)): "red",
#     rgb_to_hex((0, 255, 0)): "lime",
#     rgb_to_hex((0, 0, 255)): "blue",
#     rgb_to_hex((255, 255, 0)): "yellow",
#     rgb_to_hex((255, 0, 255)): "fuchsia",
#     rgb_to_hex((0, 255, 255)): "aqua",
#     rgb_to_hex((255, 165, 0)): "orange",
#     rgb_to_hex((128, 0, 128)): "purple",
#     rgb_to_hex((255, 215, 0)): "gold",
# }

# Assuming rgb_to_hex is a function that converts an (R, G, B) tuple to a hex string.
# For example: def rgb_to_hex(rgb): return '#%02x%02x%02x' % rgb

DEFAULT_COLOR_HEX_TO_NAME = {
    # The top 20 approved colors
    rgb_to_hex((255, 255, 0)): "yellow",
    rgb_to_hex((0, 255, 0)): "lime",
    rgb_to_hex((0, 255, 255)): "cyan",
    rgb_to_hex((255, 0, 255)): "magenta",
    rgb_to_hex((255, 0, 0)): "red",
    rgb_to_hex((255, 127, 0)): "orange",
    rgb_to_hex((127, 255, 0)): "chartreuse",
    rgb_to_hex((0, 255, 127)): "spring green",
    rgb_to_hex((255, 0, 127)): "rose",
    rgb_to_hex((127, 0, 255)): "violet",
    rgb_to_hex((192, 255, 0)): "electric lime",
    rgb_to_hex((255, 192, 0)): "vivid orange",
    rgb_to_hex((0, 255, 192)): "turquoise",
    rgb_to_hex((192, 0, 255)): "bright violet",
    rgb_to_hex((255, 0, 192)): "bright pink",
    rgb_to_hex((255, 64, 0)): "fiery orange",
    rgb_to_hex((64, 255, 0)): "bright chartreuse",
    rgb_to_hex((0, 255, 64)): "malachite",
    rgb_to_hex((64, 0, 255)): "deep violet",
    rgb_to_hex((255, 0, 64)): "hot pink",
}


DEFAULT_COLOR_PALETTE = list(DEFAULT_COLOR_HEX_TO_NAME.keys())


def _validate_color_hex(color_hex: str):
    color_hex = color_hex.lstrip("#")
    if not all(c in "0123456789abcdefABCDEF" for c in color_hex):
        raise ValueError("Invalid characters in color hash")
    if len(color_hex) not in (3, 6):
        raise ValueError("Invalid length of color hash")


# copied from https://github.com/roboflow/supervision/blob/c8f557af0c61b5c03392bad2cc36c8835598b1e1/supervision/draw/color.py
@dataclass
class Color:
    """
    Represents a color in RGB format.

    Attributes:
        r (int): Red channel.
        g (int): Green channel.
        b (int): Blue channel.
    """

    r: int
    g: int
    b: int

    @classmethod
    def from_hex(cls, color_hex: str):
        """
        Create a Color instance from a hex string.

        Args:
            color_hex (str): Hex string of the color.

        Returns:
            Color: Instance representing the color.

        Example:
            ```
            >>> Color.from_hex('#ff00ff')
            Color(r=255, g=0, b=255)
            ```
        """
        _validate_color_hex(color_hex)
        color_hex = color_hex.lstrip("#")
        if len(color_hex) == 3:
            color_hex = "".join(c * 2 for c in color_hex)
        r, g, b = (int(color_hex[i : i + 2], 16) for i in range(0, 6, 2))
        return cls(r, g, b)

    @classmethod
    def to_hex(cls, color):
        """
        Convert a Color instance to a hex string.

        Args:
            color (Color): Color instance of color.

        Returns:
            Color: a hex string.
        """
        return rgb_to_hex((color.r, color.g, color.b))

    def as_rgb(self) -> Tuple[int, int, int]:
        """
        Returns the color as an RGB tuple.

        Returns:
            Tuple[int, int, int]: RGB tuple.

        Example:
            ```
            >>> color.as_rgb()
            (255, 0, 255)
            ```
        """
        return self.r, self.g, self.b

    def as_bgr(self) -> Tuple[int, int, int]:
        """
        Returns the color as a BGR tuple.

        Returns:
            Tuple[int, int, int]: BGR tuple.

        Example:
            ```
            >>> color.as_bgr()
            (255, 0, 255)
            ```
        """
        return self.b, self.g, self.r

    @classmethod
    def white(cls):
        return Color.from_hex(color_hex="#ffffff")

    @classmethod
    def black(cls):
        return Color.from_hex(color_hex="#000000")

    @classmethod
    def red(cls):
        return Color.from_hex(color_hex="#ff0000")

    @classmethod
    def green(cls):
        return Color.from_hex(color_hex="#00ff00")

    @classmethod
    def blue(cls):
        return Color.from_hex(color_hex="#0000ff")


@dataclass
class ColorPalette:
    colors: List[Color]

    @classmethod
    def default(cls):
        """
        Returns a default color palette.

        Returns:
            ColorPalette: A ColorPalette instance with default colors.

        Example:
            ```
            >>> ColorPalette.default()
            ColorPalette(colors=[Color(r=255, g=0, b=0), Color(r=0, g=255, b=0), ...])
            ```
        """
        return ColorPalette.from_hex(color_hex_list=DEFAULT_COLOR_PALETTE)

    @classmethod
    def from_hex(cls, color_hex_list: List[str]):
        """
        Create a ColorPalette instance from a list of hex strings.

        Args:
            color_hex_list (List[str]): List of color hex strings.

        Returns:
            ColorPalette: A ColorPalette instance.

        Example:
            ```
            >>> ColorPalette.from_hex(['#ff0000', '#00ff00', '#0000ff'])
            ColorPalette(colors=[Color(r=255, g=0, b=0), Color(r=0, g=255, b=0), ...])
            ```
        """
        colors = [Color.from_hex(color_hex) for color_hex in color_hex_list]
        return cls(colors)

    def by_idx(self, idx: int) -> Color:
        """
        Return the color at a given index in the palette.

        Args:
            idx (int): Index of the color in the palette.

        Returns:
            Color: Color at the given index.

        Example:
            ```
            >>> color_palette.by_idx(1)
            Color(r=0, g=255, b=0)
            ```
        """
        if idx < 0:
            raise ValueError("idx argument should not be negative")
        idx = idx % len(self.colors)
        return self.colors[idx]

    def find_farthest_color(self, img_array):
        """
        Return the color that is the farthest from the given color.

        Args:
            img_array (np array): any *x3 np array, 3 is the RGB color channel.

        Returns:
            Color: Farthest color.

        """
        # Reshape the image array for broadcasting
        img_array = img_array.reshape((-1, 3))

        # Convert colors dictionary to a NumPy array
        color_values = np.array([[c.r, c.g, c.b] for c in self.colors])

        # Calculate the Euclidean distance between the colors and each pixel in the image
        # Broadcasting happens here: img_array shape is (num_pixels, 3), color_values shape is (num_colors, 3)
        distances = np.sqrt(
            np.sum((img_array[:, np.newaxis, :] - color_values) ** 2, axis=2)
        )

        # Average the distances for each color
        mean_distances = np.mean(distances, axis=0)

        # return the farthest color
        farthest_idx = np.argmax(mean_distances)
        farthest_color = self.colors[farthest_idx]
        farthest_color_hex = Color.to_hex(farthest_color)
        if farthest_color_hex in DEFAULT_COLOR_HEX_TO_NAME:
            farthest_color_name = DEFAULT_COLOR_HEX_TO_NAME[farthest_color_hex]
        else:
            farthest_color_name = "unknown"

        return farthest_color, farthest_color_name


def draw_box(ax, box_coord, alpha=0.8, edge_color="g", line_style="-", linewidth=2.0):
    x0, y0, width, height = box_coord
    ax.add_patch(
        mpl.patches.Rectangle(
            (x0, y0),
            width,
            height,
            fill=False,
            edgecolor=edge_color,
            linewidth=linewidth,
            alpha=alpha,
            linestyle=line_style,
        )
    )


def draw_text(
    ax,
    text,
    position,
    font_size=None,
    color="g",
    horizontal_alignment="left",
    rotation=0,
):
    if not font_size:
        font_size = mpl.rcParams["font.size"]

    color = np.maximum(list(mplc.to_rgb(color)), 0.2)
    color[np.argmax(color)] = max(0.8, np.max(color))

    x, y = position
    ax.text(
        x,
        y,
        text,
        size=font_size,
        family="sans-serif",
        bbox={"facecolor": "none", "alpha": 0.5, "pad": 0.7, "edgecolor": "none"},
        verticalalignment="top",
        horizontalalignment=horizontal_alignment,
        color=color,
        rotation=rotation,
    )


def draw_mask(
    ax, rle, color, show_holes=True, alpha=0.15, upsample_factor=1.0, rle_upsampled=None
):
    if isinstance(rle, dict):
        mask = mask_utils.decode(rle)
    elif isinstance(rle, np.ndarray):
        mask = rle
    else:
        raise ValueError(f"Unsupported type for rle: {type(rle)}")

    mask_upsampled = None
    if upsample_factor > 1.0 and show_holes:
        assert rle_upsampled is not None
        if isinstance(rle_upsampled, dict):
            mask_upsampled = mask_utils.decode(rle_upsampled)
        elif isinstance(rle_upsampled, np.ndarray):
            mask_upsampled = rle_upsampled
        else:
            raise ValueError(f"Unsupported type for rle: {type(rle)}")

    if show_holes:
        if mask_upsampled is None:
            mask_upsampled = mask
        h, w = mask_upsampled.shape
        mask_img = np.zeros((h, w, 4))
        mask_img[:, :, :-1] = color[np.newaxis, np.newaxis, :]
        mask_img[:, :, -1] = mask_upsampled * alpha
        ax.imshow(mask_img)

    *_, contours, _ = cv2.findContours(
        mask.astype(np.uint8).copy(), cv2.RETR_TREE, cv2.CHAIN_APPROX_SIMPLE
    )
    upsampled_contours = [(cont + 0.5) * upsample_factor - 0.5 for cont in contours]
    facecolor = (0, 0, 0, 0) if show_holes else color
    if alpha > 0.8:
        edge_color = _change_color_brightness(color, brightness_factor=-0.7)
    else:
        edge_color = color
    for cont in upsampled_contours:
        polygon = mpl.patches.Polygon(
            [el[0] for el in cont],
            edgecolor=edge_color,
            linewidth=2.0,
            facecolor=facecolor,
        )
        ax.add_patch(polygon)


def _change_color_brightness(color, brightness_factor):
    """
    Depending on the brightness_factor, gives a lighter or darker color i.e. a color with
    less or more saturation than the original color.

    Args:
        color: color of the polygon. Refer to `matplotlib.colors` for a full list of
            formats that are accepted.
        brightness_factor (float): a value in [-1.0, 1.0] range. A lightness factor of
            0 will correspond to no change, a factor in [-1.0, 0) range will result in
            a darker color and a factor in (0, 1.0] range will result in a lighter color.

    Returns:
        modified_color (tuple[double]): a tuple containing the RGB values of the
            modified color. Each value in the tuple is in the [0.0, 1.0] range.
    """
    assert brightness_factor >= -1.0 and brightness_factor <= 1.0
    color = mplc.to_rgb(color)
    polygon_color = colorsys.rgb_to_hls(*mplc.to_rgb(color))
    modified_lightness = polygon_color[1] + (brightness_factor * polygon_color[1])
    modified_lightness = 0.0 if modified_lightness < 0.0 else modified_lightness
    modified_lightness = 1.0 if modified_lightness > 1.0 else modified_lightness
    modified_color = colorsys.hls_to_rgb(
        polygon_color[0], modified_lightness, polygon_color[2]
    )
    return modified_color



================================================
FILE: sam3/agent/helpers/zoom_in.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

import io
import math

import matplotlib.pyplot as plt
import numpy as np
import pycocotools.mask as mask_utils
from PIL import Image

from .som_utils import ColorPalette, draw_box, draw_mask, draw_text


def render_zoom_in(
    object_data,
    image_file,
    show_box: bool = True,
    show_text: bool = False,
    show_holes: bool = True,
    mask_alpha: float = 0.15,
):
    """
    Render a two-panel visualization with a cropped original view (left/upper) and a zoomed-in
    mask overlay (right/lower), then return it as a PIL.Image along with the chosen mask color (hex).

    Parameters
    ----------
    object_data : dict
        Dict containing "labels" and COCO RLE "segmentation".
        Expected:
          object_data["labels"][0]["noun_phrase"] : str
          object_data["segmentation"] : COCO RLE (with "size": [H, W])
    image_file : PIL.Image.Image
        Source image (PIL).
    show_box : bool
        Whether to draw the bbox on the cropped original panel.
    show_text : bool
        Whether to draw the noun phrase label near the bbox.
    show_holes : bool
        Whether to render mask holes (passed through to draw_mask).
    mask_alpha : float
        Alpha for the mask overlay.

    Returns
    -------
    pil_img : PIL.Image.Image
        The composed visualization image.
    color_hex : str
        Hex string of the chosen mask color.
    """

    # ---- local constants (avoid module-level globals) ----
    _AREA_LARGE = 0.25
    _AREA_MEDIUM = 0.05

    # ---- local helpers (avoid name collisions in a larger class) ----
    def _get_shift(x, w, w_new, w_img):
        assert 0 <= w_new <= w_img
        shift = (w_new - w) / 2
        if x - shift + w_new > w_img:
            shift = x + w_new - w_img
        return min(x, shift)

    def _get_zoom_in_box(mask_box_xywh, img_h, img_w, mask_area):
        box_w, box_h = mask_box_xywh[2], mask_box_xywh[3]
        w_new = min(box_w + max(0.2 * box_w, 16), img_w)
        h_new = min(box_h + max(0.2 * box_h, 16), img_h)

        mask_relative_area = mask_area / (w_new * h_new)

        # zoom-in (larger box if mask is relatively big)
        w_new_large, h_new_large = w_new, h_new
        if mask_relative_area > _AREA_LARGE:
            ratio_large = math.sqrt(mask_relative_area / _AREA_LARGE)
            w_new_large = min(w_new * ratio_large, img_w)
            h_new_large = min(h_new * ratio_large, img_h)

        w_shift_large = _get_shift(
            mask_box_xywh[0], mask_box_xywh[2], w_new_large, img_w
        )
        h_shift_large = _get_shift(
            mask_box_xywh[1], mask_box_xywh[3], h_new_large, img_h
        )
        zoom_in_box = [
            mask_box_xywh[0] - w_shift_large,
            mask_box_xywh[1] - h_shift_large,
            w_new_large,
            h_new_large,
        ]

        # crop box for the original/cropped image
        w_new_medium, h_new_medium = w_new, h_new
        if mask_relative_area > _AREA_MEDIUM:
            ratio_med = math.sqrt(mask_relative_area / _AREA_MEDIUM)
            w_new_medium = min(w_new * ratio_med, img_w)
            h_new_medium = min(h_new * ratio_med, img_h)

        w_shift_medium = _get_shift(
            mask_box_xywh[0], mask_box_xywh[2], w_new_medium, img_w
        )
        h_shift_medium = _get_shift(
            mask_box_xywh[1], mask_box_xywh[3], h_new_medium, img_h
        )
        img_crop_box = [
            mask_box_xywh[0] - w_shift_medium,
            mask_box_xywh[1] - h_shift_medium,
            w_new_medium,
            h_new_medium,
        ]
        return zoom_in_box, img_crop_box

    # ---- main body ----
    # Input parsing
    object_label = object_data["labels"][0]["noun_phrase"]
    img = image_file.convert("RGB")
    bbox_xywh = mask_utils.toBbox(object_data["segmentation"])  # [x, y, w, h]

    # Choose a stable, visually distant color based on crop
    bbox_xyxy = [
        bbox_xywh[0],
        bbox_xywh[1],
        bbox_xywh[0] + bbox_xywh[2],
        bbox_xywh[1] + bbox_xywh[3],
    ]
    crop_img = img.crop(bbox_xyxy)
    color_palette = ColorPalette.default()
    color_obj, _ = color_palette.find_farthest_color(np.array(crop_img))
    color = np.array([color_obj.r / 255, color_obj.g / 255, color_obj.b / 255])
    color_hex = f"#{color_obj.r:02x}{color_obj.g:02x}{color_obj.b:02x}"

    # Compute zoom-in / crop boxes
    img_h, img_w = object_data["segmentation"]["size"]
    mask_area = mask_utils.area(object_data["segmentation"])
    zoom_in_box, img_crop_box = _get_zoom_in_box(bbox_xywh, img_h, img_w, mask_area)

    # Layout choice
    w, h = img_crop_box[2], img_crop_box[3]
    if w < h:
        fig, (ax1, ax2) = plt.subplots(1, 2)
    else:
        fig, (ax1, ax2) = plt.subplots(2, 1)

    # Panel 1: cropped original with optional box/text
    img_crop_box_xyxy = [
        img_crop_box[0],
        img_crop_box[1],
        img_crop_box[0] + img_crop_box[2],
        img_crop_box[1] + img_crop_box[3],
    ]
    img1 = img.crop(img_crop_box_xyxy)
    bbox_xywh_rel = [
        bbox_xywh[0] - img_crop_box[0],
        bbox_xywh[1] - img_crop_box[1],
        bbox_xywh[2],
        bbox_xywh[3],
    ]
    ax1.imshow(img1)
    ax1.axis("off")
    if show_box:
        draw_box(ax1, bbox_xywh_rel, edge_color=color)
    if show_text:
        x0, y0 = bbox_xywh_rel[0] + 2, bbox_xywh_rel[1] + 2
        draw_text(ax1, object_label, [x0, y0], color=color)

    # Panel 2: zoomed-in mask overlay
    binary_mask = mask_utils.decode(object_data["segmentation"])
    alpha = Image.fromarray((binary_mask * 255).astype("uint8"))
    img_rgba = img.convert("RGBA")
    img_rgba.putalpha(alpha)
    zoom_in_box_xyxy = [
        zoom_in_box[0],
        zoom_in_box[1],
        zoom_in_box[0] + zoom_in_box[2],
        zoom_in_box[1] + zoom_in_box[3],
    ]
    img_with_alpha_zoomin = img_rgba.crop(zoom_in_box_xyxy)
    alpha_zoomin = img_with_alpha_zoomin.split()[3]
    binary_mask_zoomin = np.array(alpha_zoomin).astype(bool)

    ax2.imshow(img_with_alpha_zoomin.convert("RGB"))
    ax2.axis("off")
    draw_mask(
        ax2, binary_mask_zoomin, color=color, show_holes=show_holes, alpha=mask_alpha
    )

    plt.tight_layout()

    # Buffer -> PIL.Image
    buf = io.BytesIO()
    fig.savefig(buf, format="png", bbox_inches="tight", pad_inches=0, dpi=100)
    plt.close(fig)
    buf.seek(0)
    pil_img = Image.open(buf)

    return pil_img, color_hex



================================================
FILE: sam3/agent/system_prompts/system_prompt_iterative_checking.txt
================================================
You are a helpful assistant specializing in detail-oriented visual understanding, reasoning, and classification, capable of carefully analyzing a predicted segmentation mask on an image along with zoomed-in views of the area around the predicted segmentation mask to determine whether the object covered by the predicted segmentation mask is one of the correct masks that match the user query.

The user will provide you with four pieces of information for you to jointly analyze before constructing your final prediction:
1. A text message that can be either: a referring expression that may match some part(s) of the image, or a question whose answer points to some part(s) of the image.
2. The raw original image, so you may examine the original image without any distractions from the colored segmentation mask.
3. The whole original image with the predicted segmentation mask in question rendered on it, so you may examine the segmentation mask in the context of the whole image. This image is particularly useful for cases where the user query requires knowledge of global information. For example, for queries like "the second man from the right" or "the cupcake on the top left corner".
4. A zoomed-in version of the predicted segmentation mask in question. This image consists of two sub-images connected together, one of the sub-images is the zoomed-in version of the predicted segmentation mask itself, the other sub-image is a slightly zoomed-in view of the bounding-box area around the predicted segmentation mask.


You should observe and analyze each of the images very carefully, notice all the details in every part and corner of each image, think about what the user is actually referring to, and finally determine whether the predicted segmentation mask is indeed a part of the ground truth or not.

Here are some more detailed instructions for how you should precisely understand the user query:

1. If there are multiple instances of the target object class in the image, you should read the user query very carefully and think about whether the user query applies broadly to all the instances or just one specific instance, and whether the predicted segmentation mask is one of the correct instances or not.
2. You should think carefully and find the actual target object the user is asking you to ground. Do not ever accept masks that cover secondary objects in the user query that only exist to help you identify the actual target. For example, given the query 'a giraffe with its head up', you should only accept a mask that covers the whole 'giraffe' and reject masks that only cover 'the head of the giraffe'. Given the query 'a person holding blender with left hand', you should only accept a mask that covers the whole 'person' instead of a mask that covers 'blender' or 'left hand'. Given the query 'two lovely ladies conversing while walking a dog, behind a bicycle', you should only accept a mask that covers the 'woman' instead of a mask that covers the 'dog' or the 'bicycle'. Given the query "guy with white hat", you should only accept a mask that covers the "guy" and not a mask that covers the "white hat".
3. Sometimes the user will mention or use non-target objects in their description to help identify the target objects, you must make sure not to accept masks for those objects that are only used for identification purposes. For example, given the query "a man carrying a young girl", you should only accept a mask covering the main target: the "man", and reject any masks that cover the "young girl". Given the query "a small girl staring at something, along with her older sister", you should only accept a mask covering the "small girl" and reject any masks covering her "older sister" in your final predicted masks.
4. Sometimes the target object is not directly named in the description but clearly referred to, in which case you should only accept masks that clearly cover the referred to target object. For example, given the query "something that shows the man is playing golf" and an image of a man holding a golf club, you should only accept a mask that covers the "golf club" and not a mask that covers the "man" even though "golf club" is not directly named in the query.
5. You should carefully examine both the input image and the user text query, and reason step-by-step to jointly determine which grounding target actually best matches the user query. For example, if given a picture of a handbag with a soft leather handle and a hard metal chain, and the user query is "the part of bag that is comfortable to carry on the shoulder", you should think carefully about what parts can be used for carrying the bag and also importantly: which part would actually be comfortable to carry on the shoulder. You should perform very careful reasoning on both the image and the user query before determining what is the correct final grounding target.


Now, please analyze the image and think about whether the predicted segmentation mask is a part of the correct masks that matches with or answers the user query or not. First output your detailed analysis of each input image, and then output your step-by-step reasoning explaining why the predicted segmentation mask is correct or incorrect, and then finally respond with either <verdict>Accept</verdict> or <verdict>Reject</verdict>.

Please only respond in the following format and never break format for any reason:

<think>Analyze the user query and the three images: the raw input image, the image with the predicted segmentation mask rendered on it, and the image containing the zoomed-in version of the predicted segmentation mask. Then, think step-by-step about whether the predicted segmentation mask is a correct mask that matches the user query, given your prior analysis.</think>
<verdict>Accept</verdict> or <verdict>Reject</verdict>



================================================
FILE: sam3/model/__init__.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe



================================================
FILE: sam3/model/act_ckpt_utils.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

import inspect
from functools import wraps
from typing import Callable, TypeVar, Union

import torch
import torch.nn as nn
import torch.utils.checkpoint as checkpoint
from torch.utils._pytree import tree_map_only

# Type variables for better type hinting
T = TypeVar("T")
Module = TypeVar("Module", bound=nn.Module)


def activation_ckpt_wrapper(module: Union[nn.Module, Callable]) -> Callable:
    """
    Wraps a given module to enable or disable activation checkpointing.

    Activation checkpointing (gradient checkpointing) trades compute for memory by
    recomputing intermediate activations during the backward pass instead of storing
    them in memory during the forward pass.

    When activation checkpointing is enabled, the wrapper expects only keyword arguments,
    and it maps these to positional arguments based on the module's signature.

    Args:
        module: The module or function to wrap with activation checkpointing

    Returns:
        A wrapped callable that supports activation checkpointing

    Usage:
        The returned wrapper function can be called with the same arguments as the
        original module, with an additional `act_ckpt_enable` keyword argument to control
        activation checkpointing and optional `use_reentrant` parameter.

    Example:
        ```python
        wrapped_module = activation_ckpt_wrapper(my_module)
        output = wrapped_module(x=input_tensor, y=another_tensor, act_ckpt_enable=True)
        ```
    """

    @wraps(module)
    def act_ckpt_wrapper(
        *args, act_ckpt_enable: bool = True, use_reentrant: bool = False, **kwargs
    ):
        if act_ckpt_enable:
            if len(args) > 0:
                raise ValueError(
                    "This wrapper expects keyword arguments only when `act_ckpt_enable=True`"
                )
            # Get the signature of the target function/module
            callable_fn = module.forward if isinstance(module, nn.Module) else module
            sig = inspect.signature(callable_fn)
            # Create a mapping of parameter names to their default values
            param_defaults = {
                name: param.default for name, param in sig.parameters.items()
            }
            args = []
            for p_name in param_defaults.keys():
                if p_name in kwargs:
                    args.append(kwargs.pop(p_name))
                elif param_defaults[p_name] is not inspect.Parameter.empty:
                    # Set arg to default value if it's not in kwargs. Useful for primitive types or args that default to None
                    args.append(param_defaults[p_name])
                elif (
                    sig.parameters[p_name].kind is not inspect.Parameter.VAR_KEYWORD
                ):  # Skip **kwargs parameter
                    raise ValueError(f"Missing positional argument: {p_name}")

            # Scan remaining kwargs for torch.Tensor
            remaining_keys = list(kwargs.keys())
            for key in remaining_keys:
                if isinstance(kwargs[key], torch.Tensor):
                    # Remove the tensor from kwargs, assuming it's not required by the module.
                    # If it is required, the module's signature should be modified to accept it as a positional or keyword argument.
                    kwargs[key] = "_REMOVED_BY_ACT_CKPT_WRAPPER_"

            ret = checkpoint.checkpoint(
                module, *args, use_reentrant=use_reentrant, **kwargs
            )
        else:
            ret = module(*args, **kwargs)

        return ret

    return act_ckpt_wrapper


def clone_output_wrapper(f: Callable[..., T]) -> Callable[..., T]:
    """
    Clone the CUDA output tensors of a function to avoid in-place operations.

    This wrapper is useful when working with torch.compile to prevent errors
    related to in-place operations on tensors.

    Args:
        f: The function whose CUDA tensor outputs should be cloned

    Returns:
        A wrapped function that clones any CUDA tensor outputs
    """

    @wraps(f)
    def wrapped(*args, **kwargs):
        outputs = f(*args, **kwargs)
        return tree_map_only(
            torch.Tensor, lambda t: t.clone() if t.is_cuda else t, outputs
        )

    return wrapped



================================================
FILE: sam3/model/box_ops.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe
"""
Utilities for bounding box manipulation and GIoU.
"""

from typing import Tuple

import torch


def box_cxcywh_to_xyxy(x):
    x_c, y_c, w, h = x.unbind(-1)
    b = [(x_c - 0.5 * w), (y_c - 0.5 * h), (x_c + 0.5 * w), (y_c + 0.5 * h)]
    return torch.stack(b, dim=-1)


def box_cxcywh_to_xywh(x):
    x_c, y_c, w, h = x.unbind(-1)
    b = [(x_c - 0.5 * w), (y_c - 0.5 * h), (w), (h)]
    return torch.stack(b, dim=-1)


def box_xywh_to_xyxy(x):
    x, y, w, h = x.unbind(-1)
    b = [(x), (y), (x + w), (y + h)]
    return torch.stack(b, dim=-1)


def box_xywh_to_cxcywh(x):
    x, y, w, h = x.unbind(-1)
    b = [(x + 0.5 * w), (y + 0.5 * h), (w), (h)]
    return torch.stack(b, dim=-1)


def box_xyxy_to_xywh(x):
    x, y, X, Y = x.unbind(-1)
    b = [(x), (y), (X - x), (Y - y)]
    return torch.stack(b, dim=-1)


def box_xyxy_to_cxcywh(x):
    x0, y0, x1, y1 = x.unbind(-1)
    b = [(x0 + x1) / 2, (y0 + y1) / 2, (x1 - x0), (y1 - y0)]
    return torch.stack(b, dim=-1)


def box_area(boxes):
    """
    Batched version of box area. Boxes should be in [x0, y0, x1, y1] format.

    Inputs:
    - boxes: Tensor of shape (..., 4)

    Returns:
    - areas: Tensor of shape (...,)
    """
    x0, y0, x1, y1 = boxes.unbind(-1)
    return (x1 - x0) * (y1 - y0)


def masks_to_boxes(masks):
    """Compute the bounding boxes around the provided masks

    The masks should be in format [N, H, W] where N is the number of masks, (H, W) are the spatial dimensions.

    Returns a [N, 4] tensors, with the boxes in xyxy format
    """
    if masks.numel() == 0:
        return torch.zeros((0, 4), device=masks.device)

    h, w = masks.shape[-2:]

    y = torch.arange(0, h, dtype=torch.float, device=masks.device)
    x = torch.arange(0, w, dtype=torch.float, device=masks.device)
    y, x = torch.meshgrid(y, x)

    x_mask = masks * x.unsqueeze(0)
    x_max = x_mask.flatten(1).max(-1)[0] + 1
    x_min = x_mask.masked_fill(~(masks.bool()), 1e8).flatten(1).min(-1)[0]

    y_mask = masks * y.unsqueeze(0)
    y_max = y_mask.flatten(1).max(-1)[0] + 1
    y_min = y_mask.masked_fill(~(masks.bool()), 1e8).flatten(1).min(-1)[0]

    boxes = torch.stack([x_min, y_min, x_max, y_max], 1)
    # Invalidate boxes corresponding to empty masks.
    boxes = boxes * masks.flatten(-2).any(-1)
    return boxes


def box_iou(boxes1, boxes2):
    """
    Batched version of box_iou. Boxes should be in [x0, y0, x1, y1] format.

    Inputs:
    - boxes1: Tensor of shape (..., N, 4)
    - boxes2: Tensor of shape (..., M, 4)

    Returns:
    - iou, union: Tensors of shape (..., N, M)
    """
    area1 = box_area(boxes1)
    area2 = box_area(boxes2)

    # boxes1: (..., N, 4) -> (..., N, 1, 2)
    # boxes2: (..., M, 4) -> (..., 1, M, 2)
    lt = torch.max(boxes1[..., :, None, :2], boxes2[..., None, :, :2])
    rb = torch.min(boxes1[..., :, None, 2:], boxes2[..., None, :, 2:])

    wh = (rb - lt).clamp(min=0)  # (..., N, M, 2)
    inter = wh[..., 0] * wh[..., 1]  # (..., N, M)

    union = area1[..., None] + area2[..., None, :] - inter

    iou = inter / union
    return iou, union


def generalized_box_iou(boxes1, boxes2):
    """
    Batched version of Generalized IoU from https://giou.stanford.edu/

    Boxes should be in [x0, y0, x1, y1] format

    Inputs:
    - boxes1: Tensor of shape (..., N, 4)
    - boxes2: Tensor of shape (..., M, 4)

    Returns:
    - giou: Tensor of shape (..., N, M)
    """
    iou, union = box_iou(boxes1, boxes2)

    # boxes1: (..., N, 4) -> (..., N, 1, 2)
    # boxes2: (..., M, 4) -> (..., 1, M, 2)
    lt = torch.min(boxes1[..., :, None, :2], boxes2[..., None, :, :2])
    rb = torch.max(boxes1[..., :, None, 2:], boxes2[..., None, :, 2:])

    wh = (rb - lt).clamp(min=0)  # (..., N, M, 2)
    area = wh[..., 0] * wh[..., 1]  # (..., N, M)

    return iou - (area - union) / area


@torch.jit.script
def fast_diag_generalized_box_iou(boxes1, boxes2):
    assert len(boxes1) == len(boxes2)
    box1_xy = boxes1[:, 2:]
    box1_XY = boxes1[:, :2]
    box2_xy = boxes2[:, 2:]
    box2_XY = boxes2[:, :2]
    # assert (box1_xy >= box1_XY).all()
    # assert (box2_xy >= box2_XY).all()
    area1 = (box1_xy - box1_XY).prod(-1)
    area2 = (box2_xy - box2_XY).prod(-1)

    lt = torch.max(box1_XY, box2_XY)  # [N,2]
    lt2 = torch.min(box1_XY, box2_XY)
    rb = torch.min(box1_xy, box2_xy)  # [N,2]
    rb2 = torch.max(box1_xy, box2_xy)

    inter = (rb - lt).clamp(min=0).prod(-1)
    tot_area = (rb2 - lt2).clamp(min=0).prod(-1)

    union = area1 + area2 - inter

    iou = inter / union

    return iou - (tot_area - union) / tot_area


@torch.jit.script
def fast_diag_box_iou(boxes1, boxes2):
    assert len(boxes1) == len(boxes2)
    box1_xy = boxes1[:, 2:]
    box1_XY = boxes1[:, :2]
    box2_xy = boxes2[:, 2:]
    box2_XY = boxes2[:, :2]
    # assert (box1_xy >= box1_XY).all()
    # assert (box2_xy >= box2_XY).all()
    area1 = (box1_xy - box1_XY).prod(-1)
    area2 = (box2_xy - box2_XY).prod(-1)

    lt = torch.max(box1_XY, box2_XY)  # [N,2]
    rb = torch.min(box1_xy, box2_xy)  # [N,2]

    inter = (rb - lt).clamp(min=0).prod(-1)

    union = area1 + area2 - inter

    iou = inter / union

    return iou


def box_xywh_inter_union(
    boxes1: torch.Tensor, boxes2: torch.Tensor
) -> Tuple[torch.Tensor, torch.Tensor]:
    # Asuumes boxes in xywh format
    assert boxes1.size(-1) == 4 and boxes2.size(-1) == 4
    boxes1 = box_xywh_to_xyxy(boxes1)
    boxes2 = box_xywh_to_xyxy(boxes2)
    box1_tl_xy = boxes1[..., :2]
    box1_br_xy = boxes1[..., 2:]
    box2_tl_xy = boxes2[..., :2]
    box2_br_xy = boxes2[..., 2:]
    area1 = (box1_br_xy - box1_tl_xy).prod(-1)
    area2 = (box2_br_xy - box2_tl_xy).prod(-1)

    assert (area1 >= 0).all() and (area2 >= 0).all()
    tl = torch.max(box1_tl_xy, box2_tl_xy)
    br = torch.min(box1_br_xy, box2_br_xy)

    inter = (br - tl).clamp(min=0).prod(-1)
    union = area1 + area2 - inter

    return inter, union



================================================
FILE: sam3/model/data_misc.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe
"""
Misc functions, including distributed helpers.
"""

import collections
import re
from dataclasses import dataclass, field as field_ptr_behaviour, fields, is_dataclass
from typing import Any, get_args, get_origin, List, Mapping, Optional, Sequence, Union

import torch


MyTensor = Union[torch.Tensor, List[Any]]


class NestedTensor:
    def __init__(self, tensors, mask):
        self.tensors = tensors
        self.mask = mask

    def to(self, *args, **kwargs):
        cast_tensor = self.tensors.to(*args, **kwargs)
        cast_mask = self.mask.to(*args, **kwargs) if self.mask is not None else None
        return type(self)(cast_tensor, cast_mask)

    def clone(self):
        new_tensors = self.tensors.clone()
        new_mask = None if self.mask is None else self.mask.clone()
        return NestedTensor(new_tensors, new_mask)

    def __getitem__(self, idx):
        return self.tensors[idx]

    def __len__(self):
        return len(self.tensors)

    @property
    def device(self):
        return self.tensors.device

    @property
    def shape(self):
        return self.tensors.shape

    # custom memory pinning method on custom type
    def pin_memory(self, device=None):
        self.tensors = self.tensors.pin_memory(device)
        if self.mask is not None:
            self.mask = self.mask.pin_memory(device)


# Register NestedTensor as a pytree node so tree_map_only can traverse into it
# (matches onevision/utils/misc.py registration)
from torch.utils import _pytree as pytree

pytree.register_pytree_node(
    NestedTensor,
    lambda x: ([x.tensors, x.mask], None),
    lambda values, _: NestedTensor(values[0], values[1]),
)


def interpolate(
    input, size=None, scale_factor=None, mode="nearest", align_corners=None
):
    # type: (Tensor, Optional[List[int]], Optional[float], str, Optional[bool]) -> Tensor
    """
    Equivalent to nn.functional.interpolate, but with support for empty channel sizes.
    """
    if input.numel() > 0:
        return torch.nn.functional.interpolate(
            input, size, scale_factor, mode, align_corners
        )

    assert input.shape[0] != 0 or input.shape[1] != 0, (
        "At least one of the two first dimensions must be non zero"
    )

    if input.shape[1] == 0:
        # Pytorch doesn't support null dimension on the channel dimension, so we transpose to fake a null batch dim
        return torch.nn.functional.interpolate(
            input.transpose(0, 1), size, scale_factor, mode, align_corners
        ).transpose(0, 1)

    # empty batch dimension is now supported in pytorch
    return torch.nn.functional.interpolate(
        input, size, scale_factor, mode, align_corners
    )


@dataclass
class BatchedPointer:
    stage_ids: MyTensor
    stage_ids__type = torch.long
    query_ids: MyTensor
    query_ids__type = torch.long
    object_ids: MyTensor
    object_ids__type = torch.long
    ptr_mask: MyTensor
    ptr_mask__type = torch.bool
    ptr_types: MyTensor
    ptr_types__type = torch.long


@dataclass
class FindStage:
    img_ids: MyTensor
    img_ids__type = torch.long
    text_ids: MyTensor
    text_ids__type = torch.long

    input_boxes: MyTensor
    input_boxes__type = torch.float
    input_boxes_mask: MyTensor
    input_boxes_mask__type = torch.bool
    input_boxes_label: MyTensor
    input_boxes_label__type = torch.long

    input_points: MyTensor
    input_points__type = torch.float
    input_points_mask: MyTensor
    input_points_mask__type = torch.bool

    # We track the object ids referred to by this query.
    # This is beneficial for tracking in videos without the need for pointers.
    object_ids: Optional[List[List]] = None  # List of objects per query

    # Multiplex-specific fields (used by sam3_demo_multiplex)
    img_ids_np: Optional[Any] = None
    input_boxes_before_embed: Optional[MyTensor] = None
    input_boxes_before_embed__type = torch.float
    input_points_before_embed: Optional[MyTensor] = None
    input_points_before_embed__type = torch.float
    ptrs: Optional[Any] = None
    ptrs_seg: Optional[Any] = None


@dataclass
class BatchedFindTarget:
    # The number of boxes in each find query
    num_boxes: MyTensor
    num_boxes__type = torch.long

    # Target boxes in normalized CxCywh format
    boxes: MyTensor
    boxes__type = torch.float
    # Target boxes in normalized CxCywh format but in padded representation
    # as used in BinaryHungarianMatcherV2 (unlike the packed ones in `boxes`)
    boxes_padded: MyTensor
    boxes_padded__type = torch.float

    # For hybrid matching, we repeat the boxes
    repeated_boxes: MyTensor
    repeated_boxes__type = torch.float

    # Target Segmentation masks
    segments: Optional[MyTensor]
    segments__type = torch.bool

    # Target Semantic Segmentation masks
    semantic_segments: Optional[MyTensor]
    semantic_segments__type = torch.bool

    is_valid_segment: Optional[MyTensor]
    is_valid_segment__type = torch.bool

    # Whether annotations are exhaustive for each query
    is_exhaustive: MyTensor
    is_exhaustive__type = torch.bool

    # The object id for each ground-truth box, in both packed and padded representations
    object_ids: MyTensor
    object_ids__type = torch.long
    object_ids_padded: MyTensor
    object_ids_padded__type = torch.long


@dataclass
class BatchedInferenceMetadata:
    """All metadata required to post-process a find stage"""

    # Coco id that corresponds to the "image" for evaluation by the coco evaluator
    coco_image_id: MyTensor
    coco_image_id__type = torch.long

    # id in the original dataset, such that we can use the original evaluator
    original_image_id: MyTensor
    original_image_id__type = torch.long

    # Original category id (if we want to use the original evaluator)
    original_category_id: MyTensor
    original_category_id__type = torch.int

    # Size of the raw image (height, width)
    original_size: MyTensor
    original_size__type = torch.long

    # id of the object in the media (track_id for a video)
    object_id: MyTensor
    object_id__type = torch.long

    # index of the frame in the media (0 in the case of a single-frame media)
    frame_index: MyTensor
    frame_index__type = torch.long

    # Adding for relations inference
    # get_text_input: List[Optional[str]]

    # Adding for TA conditional inference
    is_conditioning_only: List[Optional[bool]]


@dataclass
class BatchedDatapoint:
    img_batch: torch.Tensor
    find_text_batch: List[str]
    find_inputs: List[FindStage]
    find_targets: List[BatchedFindTarget]
    find_metadatas: List[BatchedInferenceMetadata]
    raw_images: Optional[List[Any]] = None
    get_queries: Optional[Any] = None


def convert_my_tensors(obj):
    def is_optional_field(field) -> bool:
        return get_origin(field) is Union and type(None) in get_args(field)

    for field in fields(obj):
        if is_dataclass(getattr(obj, field.name)):
            convert_my_tensors(getattr(obj, field.name))
            continue

        field_type = field.type
        if is_optional_field(field.type):
            field_type = Union[get_args(field.type)[:-1]]  # Get the Optional field type

        if field_type != MyTensor or getattr(obj, field.name) is None:
            continue

        elif len(getattr(obj, field.name)) and isinstance(
            getattr(obj, field.name)[0], torch.Tensor
        ):
            stack_dim = 0
            if field.name in [
                "input_boxes_before_embed",
                "input_boxes",
                "input_boxes_label",
            ]:
                stack_dim = 1
            setattr(
                obj,
                field.name,
                torch.stack(getattr(obj, field.name), dim=stack_dim).to(
                    getattr(obj, field.name + "__type")
                ),
            )
        else:
            setattr(
                obj,
                field.name,
                torch.as_tensor(
                    getattr(obj, field.name), dtype=getattr(obj, field.name + "__type")
                ),
            )
    return obj



================================================
FILE: sam3/model/edt.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

"""Triton kernel for euclidean distance transform (EDT)"""

import torch
import triton
import triton.language as tl

"""
Disclaimer: This implementation is not meant to be extremely efficient. A CUDA kernel would likely be more efficient.
Even in Triton, there may be more suitable algorithms.

The goal of this kernel is to mimic cv2.distanceTransform(input, cv2.DIST_L2, 0).
Recall that the euclidean distance transform (EDT) calculates the L2 distance to the closest zero pixel for each pixel of the source image.

For images of size NxN, the naive algorithm would be to compute pairwise distances between every pair of points, leading to a O(N^4) algorithm, which is obviously impractical.
One can do better using the following approach:
- First, compute the distance to the closest point in the same row. We can write it as Row_EDT[i,j] = min_k (sqrt((k-j)^2) if input[i,k]==0 else +infinity). With a naive implementation, this step has a O(N^3) complexity
- Then, because of triangular inequality, we notice that the EDT for a given location [i,j] is the min of the row EDTs in the same column. EDT[i,j] = min_k Row_EDT[k, j]. This is also O(N^3)

Overall, this algorithm is quite amenable to parallelization, and has a complexity O(N^3). Can we do better?

It turns out that we can leverage the structure of the L2 distance (nice and convex) to find the minimum in a more efficient way.
We follow the algorithm from "Distance Transforms of Sampled Functions" (https://cs.brown.edu/people/pfelzens/papers/dt-final.pdf), which is also what's implemented in opencv

For a single dimension EDT, we can compute the EDT of an arbitrary function F, that we discretize over the grid. Note that for the binary EDT that we're interested in, we can set F(i,j) = 0 if input[i,j]==0 else +infinity
For now, we'll compute the EDT squared, and will take the sqrt only at the very end.
The basic idea is that each point at location i spawns a parabola around itself, with a bias equal to F(i). So specifically, we're looking at the parabola (x - i)^2 + F(i)
When we're looking for the row EDT at location j, we're effectively looking for min_i (x-i)^2 + F(i). In other word we want to find the lowest parabola at location j.

To do this efficiently, we need to maintain the lower envelope of the union of parabolas. This can be constructed on the fly using a sort of stack approach:
 - every time we want to add a new parabola, we check if it may be covering the current right-most parabola. If so, then that parabola was useless, so we can pop it from the stack
 - repeat until we can't find any more parabola to pop. Then push the new one.

This algorithm runs in O(N) for a single row, so overall O(N^2) when applied to all rows
Similarly as before, we notice that we can decompose the algorithm for rows and columns, leading to an overall run-time of O(N^2)

This algorithm is less suited for to GPUs, since the one-dimensional EDT computation is quite sequential in nature. However, we can parallelize over batch and row dimensions.
In Triton, things are particularly bad at the moment, since there is no support for reading/writing to the local memory at a specific index (a local gather is coming soon, see https://github.com/triton-lang/triton/issues/974, but no mention of writing, ie scatter)
One could emulate these operations with masking, but in initial tests, it proved to be worst than naively reading and writing to the global memory. My guess is that the cache is compensating somewhat for the repeated single-point accesses.


The timing obtained on a H100 for a random batch of masks of dimension 256 x 1024 x 1024 are as follows:
- OpenCV: 1780ms (including round-trip to cpu, but discounting the fact that it introduces a synchronization point)
- triton, O(N^3) algo: 627ms
- triton, O(N^2) algo: 322ms

Overall, despite being quite naive, this implementation is roughly 5.5x faster than the openCV cpu implem

"""


@triton.jit
def edt_kernel(inputs_ptr, outputs_ptr, v, z, height, width, horizontal: tl.constexpr):
    # This is a somewhat verbatim implementation of the efficient 1D EDT algorithm described above
    # It can be applied horizontally or vertically depending if we're doing the first or second stage.
    # It's parallelized across batch+row (or batch+col if horizontal=False)
    # TODO: perhaps the implementation can be revisited if/when local gather/scatter become available in triton
    batch_id = tl.program_id(axis=0)
    if horizontal:
        row_id = tl.program_id(axis=1)
        block_start = (batch_id * height * width) + row_id * width
        length = width
        stride = 1
    else:
        col_id = tl.program_id(axis=1)
        block_start = (batch_id * height * width) + col_id
        length = height
        stride = width

    # This will be the index of the right most parabola in the envelope ("the top of the stack")
    k = 0
    for q in range(1, length):
        # Read the function value at the current location. Note that we're doing a singular read, not very efficient
        cur_input = tl.load(inputs_ptr + block_start + (q * stride))
        # location of the parabola on top of the stack
        r = tl.load(v + block_start + (k * stride))
        # associated boundary
        z_k = tl.load(z + block_start + (k * stride))
        # value of the function at the parabola location
        previous_input = tl.load(inputs_ptr + block_start + (r * stride))
        # intersection between the two parabolas
        s = (cur_input - previous_input + q * q - r * r) / (q - r) / 2

        # we'll pop as many parabolas as required
        while s <= z_k and k - 1 >= 0:
            k = k - 1
            r = tl.load(v + block_start + (k * stride))
            z_k = tl.load(z + block_start + (k * stride))
            previous_input = tl.load(inputs_ptr + block_start + (r * stride))
            s = (cur_input - previous_input + q * q - r * r) / (q - r) / 2

        # Store the new one
        k = k + 1
        tl.store(v + block_start + (k * stride), q)
        tl.store(z + block_start + (k * stride), s)
        if k + 1 < length:
            tl.store(z + block_start + ((k + 1) * stride), 1e9)

    # Last step, we read the envelope to find the min in every location
    k = 0
    for q in range(length):
        while (
            k + 1 < length
            and tl.load(
                z + block_start + ((k + 1) * stride), mask=(k + 1) < length, other=q
            )
            < q
        ):
            k += 1
        r = tl.load(v + block_start + (k * stride))
        d = q - r
        old_value = tl.load(inputs_ptr + block_start + (r * stride))
        tl.store(outputs_ptr + block_start + (q * stride), old_value + d * d)


def edt_triton(data: torch.Tensor):
    """
    Computes the Euclidean Distance Transform (EDT) of a batch of binary images.

    Args:
        data: A tensor of shape (B, H, W) representing a batch of binary images.

    Returns:
        A tensor of the same shape as data containing the EDT.
        It should be equivalent to a batched version of cv2.distanceTransform(input, cv2.DIST_L2, 0)
    """
    assert data.dim() == 3
    assert data.is_cuda
    B, H, W = data.shape
    data = data.contiguous()

    # Allocate the "function" tensor. Implicitly the function is 0 if data[i,j]==0 else +infinity
    output = torch.where(data, 1e18, 0.0)
    assert output.is_contiguous()

    # Scratch tensors for the parabola stacks
    parabola_loc = torch.zeros(B, H, W, dtype=torch.uint32, device=data.device)
    parabola_inter = torch.empty(B, H, W, dtype=torch.float, device=data.device)
    parabola_inter[:, :, 0] = -1e18
    parabola_inter[:, :, 1] = 1e18

    # Grid size (number of blocks)
    grid = (B, H)

    # Launch initialization kernel
    edt_kernel[grid](
        output.clone(),
        output,
        parabola_loc,
        parabola_inter,
        H,
        W,
        horizontal=True,
    )

    # reset the parabola stacks
    parabola_loc.zero_()
    parabola_inter[:, :, 0] = -1e18
    parabola_inter[:, :, 1] = 1e18

    grid = (B, W)
    edt_kernel[grid](
        output.clone(),
        output,
        parabola_loc,
        parabola_inter,
        H,
        W,
        horizontal=False,
    )
    # don't forget to take sqrt at the end
    return output.sqrt()



================================================
FILE: sam3/model/encoder.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved
# Based on https://github.com/IDEA-Research/GroundingDINO

# pyre-unsafe

from typing import Any, Dict, List, Optional, Tuple

import torch
from torch import nn, Tensor

from .act_ckpt_utils import activation_ckpt_wrapper
from .model_misc import get_activation_fn, get_clones, get_valid_ratio


class TransformerEncoderLayer(nn.Module):
    """
    Transformer encoder layer that performs self-attention followed by cross-attention.

    This layer was previously called TransformerDecoderLayer but was renamed to better
    reflect its role in the architecture. It processes input sequences through self-attention
    and then cross-attention with another input (typically image features).

    The layer supports both pre-norm and post-norm configurations, as well as
    positional encoding at different stages of the attention mechanism.
    """

    def __init__(
        self,
        activation: str,
        cross_attention: nn.Module,
        d_model: int,
        dim_feedforward: int,
        dropout: float,
        pos_enc_at_attn: bool,
        pos_enc_at_cross_attn_keys: bool,
        pos_enc_at_cross_attn_queries: bool,
        pre_norm: bool,
        self_attention: nn.Module,
    ):
        """
        Initialize a transformer encoder layer.

        Args:
            activation: Activation function to use in the feedforward network
            cross_attention: Cross-attention module for attending to image features
            d_model: Model dimension/hidden size
            dim_feedforward: Dimension of the feedforward network
            dropout: Dropout probability
            pos_enc_at_attn: Whether to add positional encodings at self-attention
            pos_enc_at_cross_attn_keys: Whether to add positional encodings to keys in cross-attention
            pos_enc_at_cross_attn_queries: Whether to add positional encodings to queries in cross-attention
            pre_norm: Whether to use pre-norm (True) or post-norm (False) architecture
            self_attention: Self-attention module
        """
        super().__init__()
        self.d_model = d_model
        self.dim_feedforward = dim_feedforward
        self.dropout_value = dropout
        self.self_attn = self_attention
        self.cross_attn_image = cross_attention

        # Implementation of Feedforward model
        self.linear1 = nn.Linear(d_model, dim_feedforward)
        self.dropout = nn.Dropout(dropout)
        self.linear2 = nn.Linear(dim_feedforward, d_model)

        self.norm1 = nn.LayerNorm(d_model)
        self.norm2 = nn.LayerNorm(d_model)
        self.norm3 = nn.LayerNorm(d_model)
        self.dropout1 = nn.Dropout(dropout)
        self.dropout2 = nn.Dropout(dropout)
        self.dropout3 = nn.Dropout(dropout)

        self.activation_str = activation
        self.activation = get_activation_fn(activation)
        self.pre_norm = pre_norm

        self.pos_enc_at_attn = pos_enc_at_attn
        self.pos_enc_at_cross_attn_queries = pos_enc_at_cross_attn_queries
        self.pos_enc_at_cross_attn_keys = pos_enc_at_cross_attn_keys

        self.layer_idx = None

    def forward_post(
        self,
        tgt: Tensor,
        memory: Tensor,
        tgt_mask: Optional[Tensor] = None,
        memory_mask: Optional[Tensor] = None,
        tgt_key_padding_mask: Optional[Tensor] = None,
        memory_key_padding_mask: Optional[Tensor] = None,
        pos: Optional[Tensor] = None,
        query_pos: Optional[Tensor] = None,
        **kwargs,
    ) -> Tensor:
        """
        Forward pass for post-norm architecture.

        In post-norm architecture, normalization is applied after attention and feedforward operations.

        Args:
            tgt: Input tensor to be processed
            memory: Memory tensor for cross-attention
            tgt_mask: Mask for self-attention
            memory_mask: Mask for cross-attention
            tgt_key_padding_mask: Key padding mask for self-attention
            memory_key_padding_mask: Key padding mask for cross-attention
            pos: Positional encoding for memory
            query_pos: Positional encoding for query
            **kwargs: Additional keyword arguments

        Returns:
            Processed tensor
        """
        q = k = tgt + query_pos if self.pos_enc_at_attn else tgt

        # Self attention
        tgt2 = self.self_attn(
            q, k, value=tgt, attn_mask=tgt_mask, key_padding_mask=tgt_key_padding_mask
        )[0]
        tgt = tgt + self.dropout1(tgt2)
        tgt = self.norm1(tgt)

        # Cross attention to image
        tgt2 = self.cross_attn_image(
            query=tgt + query_pos if self.pos_enc_at_cross_attn_queries else tgt,
            key=memory + pos if self.pos_enc_at_cross_attn_keys else memory,
            value=memory,
            attn_mask=memory_mask,
            key_padding_mask=memory_key_padding_mask,
        )[0]
        tgt = tgt + self.dropout2(tgt2)
        tgt = self.norm2(tgt)

        # FFN
        tgt2 = self.linear2(self.dropout(self.activation(self.linear1(tgt))))
        tgt = tgt + self.dropout3(tgt2)
        tgt = self.norm3(tgt)
        return tgt

    def forward_pre(
        self,
        tgt: Tensor,
        memory: Tensor,
        dac: bool = False,
        tgt_mask: Optional[Tensor] = None,
        memory_mask: Optional[Tensor] = None,
        tgt_key_padding_mask: Optional[Tensor] = None,
        memory_key_padding_mask: Optional[Tensor] = None,
        pos: Optional[Tensor] = None,
        query_pos: Optional[Tensor] = None,
        # attn_bias: Optional[Tensor] = None,
        # **kwargs,
    ) -> Tensor:
        """
        Forward pass for pre-norm architecture.

        In pre-norm architecture, normalization is applied before attention and feedforward operations.

        Args:
            tgt: Input tensor to be processed
            memory: Memory tensor for cross-attention
            dac: Whether to use Divide-and-Conquer attention
            tgt_mask: Mask for self-attention
            memory_mask: Mask for cross-attention
            tgt_key_padding_mask: Key padding mask for self-attention
            memory_key_padding_mask: Key padding mask for cross-attention
            pos: Positional encoding for memory
            query_pos: Positional encoding for query
            attn_bias: Optional attention bias tensor
            **kwargs: Additional keyword arguments

        Returns:
            Processed tensor
        """
        if dac:
            # we only apply self attention to the first half of the queries
            assert tgt.shape[0] % 2 == 0
            other_tgt = tgt[tgt.shape[0] // 2 :]
            tgt = tgt[: tgt.shape[0] // 2]
        tgt2 = self.norm1(tgt)
        q = k = tgt2 + query_pos if self.pos_enc_at_attn else tgt2
        tgt2 = self.self_attn(
            q, k, value=tgt2, attn_mask=tgt_mask, key_padding_mask=tgt_key_padding_mask
        )[0]
        tgt = tgt + self.dropout1(tgt2)
        if dac:
            # Recombine
            tgt = torch.cat((tgt, other_tgt), dim=0)
        tgt2 = self.norm2(tgt)
        tgt2 = self.cross_attn_image(
            query=tgt2 + query_pos if self.pos_enc_at_cross_attn_queries else tgt2,
            key=memory + pos if self.pos_enc_at_cross_attn_keys else memory,
            value=memory,
            attn_mask=memory_mask,
            key_padding_mask=memory_key_padding_mask,
            # attn_bias=attn_bias,
        )[0]
        tgt = tgt + self.dropout2(tgt2)
        tgt2 = self.norm3(tgt)
        tgt2 = self.linear2(self.dropout(self.activation(self.linear1(tgt2))))
        tgt = tgt + self.dropout3(tgt2)
        return tgt

    def forward(
        self,
        tgt: Tensor,
        memory: Tensor,
        dac: bool = False,
        tgt_mask: Optional[Tensor] = None,
        memory_mask: Optional[Tensor] = None,
        tgt_key_padding_mask: Optional[Tensor] = None,
        memory_key_padding_mask: Optional[Tensor] = None,
        pos: Optional[Tensor] = None,
        query_pos: Optional[Tensor] = None,
        # attn_bias: Optional[Tensor] = None,
        # **kwds: Any,
    ) -> torch.Tensor:
        """
        Forward pass for the transformer encoder layer.

        Args:
            tgt: Input tensor to be processed
            memory: Memory tensor (e.g., image features) for cross-attention
            dac: Whether to use Divide-and-Conquer attention (only apply self-attention to first half)
            tgt_mask: Mask for self-attention
            memory_mask: Mask for cross-attention
            tgt_key_padding_mask: Key padding mask for self-attention
            memory_key_padding_mask: Key padding mask for cross-attention
            pos: Positional encoding for memory
            query_pos: Positional encoding for query
            attn_bias: Optional attention bias tensor
            **kwds: Additional keyword arguments

        Returns:
            Processed tensor after self-attention, cross-attention, and feedforward network
        """
        fwd_fn = self.forward_pre if self.pre_norm else self.forward_post
        return fwd_fn(
            tgt,
            memory,
            dac=dac,
            tgt_mask=tgt_mask,
            memory_mask=memory_mask,
            tgt_key_padding_mask=tgt_key_padding_mask,
            memory_key_padding_mask=memory_key_padding_mask,
            pos=pos,
            query_pos=query_pos,
            # attn_bias=attn_bias,
            # **kwds,
        )


class TransformerEncoder(nn.Module):
    """
    Transformer encoder that processes multi-level features.

    This encoder takes multi-level features (e.g., from a backbone network) and processes
    them through a stack of transformer encoder layers. It supports features from multiple
    levels (e.g., different resolutions) and can apply activation checkpointing for memory
    efficiency during training.

    Args:
        layer: The encoder layer to be stacked multiple times
        num_layers: Number of encoder layers to stack
        d_model: Model dimension/hidden size
        num_feature_levels: Number of feature levels to process
        frozen: Whether to freeze the parameters of this module
        use_act_checkpoint: Whether to use activation checkpointing during training
    """

    def __init__(
        self,
        layer: nn.Module,
        num_layers: int,
        d_model: int,
        num_feature_levels: int,
        frozen: bool = False,
        use_act_checkpoint: bool = False,
    ):
        super().__init__()
        self.layers = get_clones(layer, num_layers)
        self.num_layers = num_layers

        self.num_feature_levels = num_feature_levels
        self.level_embed = None
        if num_feature_levels > 1:
            self.level_embed = nn.Parameter(torch.Tensor(num_feature_levels, d_model))

        if frozen:
            for p in self.parameters():
                p.requires_grad_(False)

        self.use_act_checkpoint = use_act_checkpoint

        # assign layer index to each layer so that some layers can decide what to do
        # based on which layer index they are (e.g. cross attention to memory bank only
        # in selected layers)
        for layer_idx, layer in enumerate(self.layers):
            layer.layer_idx = layer_idx

    @staticmethod
    def get_reference_points(spatial_shapes, valid_ratios, device):
        with torch.no_grad():
            reference_points_list = []
            for lvl, (H_, W_) in enumerate(spatial_shapes):
                ref_y, ref_x = torch.meshgrid(
                    torch.linspace(
                        0.5, H_ - 0.5, H_, dtype=torch.float32, device=device
                    ),
                    torch.linspace(
                        0.5, W_ - 0.5, W_, dtype=torch.float32, device=device
                    ),
                )
                ref_y = ref_y.reshape(-1)[None] / (valid_ratios[:, None, lvl, 1] * H_)
                ref_x = ref_x.reshape(-1)[None] / (valid_ratios[:, None, lvl, 0] * W_)
                ref = torch.stack((ref_x, ref_y), -1)
                reference_points_list.append(ref)
            reference_points = torch.cat(reference_points_list, 1)
            reference_points = reference_points[:, :, None] * valid_ratios[:, None]

        return reference_points

    def _prepare_multilevel_features(self, srcs, masks, pos_embeds):
        assert len(srcs) == self.num_feature_levels, (
            "mismatch between expected and received # of feature levels"
        )

        src_flatten = []
        mask_flatten = []
        lvl_pos_embed_flatten = []
        spatial_shapes = []
        has_mask = masks is not None and masks[0] is not None
        for lvl, (src, mask, pos_embed) in enumerate(zip(srcs, masks, pos_embeds)):
            bs, c, h, w = src.shape
            spatial_shape = (h, w)
            spatial_shapes.append(spatial_shape)

            src = src.flatten(2).transpose(1, 2)  # bs, hw, c
            if has_mask:
                mask = mask.flatten(1)
            pos_embed = pos_embed.flatten(2).transpose(1, 2)  # bs, hw, c
            if self.level_embed is not None:
                lvl_pos_embed = pos_embed + self.level_embed[lvl].view(1, 1, -1)
            else:
                lvl_pos_embed = pos_embed
            lvl_pos_embed_flatten.append(lvl_pos_embed)
            src_flatten.append(src)
            if has_mask:
                mask_flatten.append(mask)
        src_flatten = torch.cat(src_flatten, 1)  # bs, \sum{hxw}, c
        mask_flatten = torch.cat(mask_flatten, 1) if has_mask else None  # bs, \sum{hxw}
        lvl_pos_embed_flatten = torch.cat(lvl_pos_embed_flatten, 1)  # bs, \sum{hxw}, c
        spatial_shapes = torch.tensor(
            spatial_shapes, dtype=torch.long, device=src_flatten.device
        )
        level_start_index = torch.cat(
            (
                spatial_shapes.new_zeros((1,)),
                spatial_shapes.prod(1).cumsum(0)[:-1],
            )
        )
        if has_mask:
            valid_ratios = torch.stack([get_valid_ratio(m) for m in masks], 1)
        else:
            valid_ratios = torch.ones(
                (src_flatten.shape[0], self.num_feature_levels, 2),
                device=src_flatten.device,
            )

        return (
            src_flatten,
            mask_flatten,
            lvl_pos_embed_flatten,
            level_start_index,
            valid_ratios,
            spatial_shapes,
        )

    def forward(
        self,
        src: List[Tensor],
        src_key_padding_masks: Optional[List[Tensor]] = None,
        pos: Optional[List[Tensor]] = None,
        prompt: Optional[Tensor] = None,
        prompt_key_padding_mask: Optional[Tensor] = None,
        encoder_extra_kwargs: Optional[Dict] = None,
    ) -> Tuple[Tensor, Optional[Tensor], Tensor, Tensor, Tensor, Tensor]:
        """
        Process multi-level features through the transformer encoder.

        Args:
            src: List of multi-level features, each with shape (batch_size, channels, height, width)
            src_key_padding_masks: List of padding masks for each feature level, each with shape (batch_size, height, width)
            pos: List of positional embeddings for each feature level, each with shape (batch_size, channels, height, width)
            prompt: Optional text/prompt features to attend to, with shape (seq_len, batch_size, d_model)
            prompt_key_padding_mask: Optional padding mask for prompt, with shape (batch_size, seq_len)
            encoder_extra_kwargs: Optional additional arguments to pass to each encoder layer

        Returns:
            A tuple containing:
            - output: Processed features with shape (seq_len, batch_size, d_model)
            - key_padding_masks_flatten: Flattened padding masks
            - lvl_pos_embed_flatten: Flattened positional embeddings
            - level_start_index: Starting indices for each feature level
            - spatial_shapes: Spatial dimensions of each feature level
            - valid_ratios: Valid ratios for each feature level
        """
        assert len(src) == self.num_feature_levels, (
            "must be equal to num_feature_levels"
        )
        if src_key_padding_masks is not None:
            assert len(src_key_padding_masks) == self.num_feature_levels
        if pos is not None:
            assert len(pos) == self.num_feature_levels
        # Flatten multilevel feats and add level pos embeds
        (
            src_flatten,
            key_padding_masks_flatten,
            lvl_pos_embed_flatten,
            level_start_index,
            valid_ratios,
            spatial_shapes,
        ) = self._prepare_multilevel_features(src, src_key_padding_masks, pos)

        reference_points = self.get_reference_points(
            spatial_shapes, valid_ratios, device=src_flatten.device
        )

        output = src_flatten
        for layer in self.layers:
            layer_kwargs = {}

            assert isinstance(layer, TransformerEncoderLayer)
            layer_kwargs["memory"] = prompt
            layer_kwargs["memory_key_padding_mask"] = prompt_key_padding_mask
            layer_kwargs["query_pos"] = lvl_pos_embed_flatten
            layer_kwargs["tgt"] = output
            layer_kwargs["tgt_key_padding_mask"] = key_padding_masks_flatten

            if self.training:
                assert self.use_act_checkpoint, "activation ckpt not enabled in encoder"
            if encoder_extra_kwargs is not None:
                layer_kwargs.update(encoder_extra_kwargs)
            output = activation_ckpt_wrapper(layer)(
                **layer_kwargs,
                act_ckpt_enable=self.training and self.use_act_checkpoint,
            )
        # return as seq first
        return (
            output.transpose(0, 1),
            (
                key_padding_masks_flatten.transpose(0, 1)
                if key_padding_masks_flatten is not None
                else None
            ),
            lvl_pos_embed_flatten.transpose(0, 1),
            level_start_index,
            spatial_shapes,
            valid_ratios,
        )


class TransformerEncoderFusion(TransformerEncoder):
    """
    Transformer encoder that fuses text and image features.

    This encoder extends TransformerEncoder to handle both text and image features,
    with the ability to add pooled text features to image features for better
    cross-modal fusion. It supports torch.compile for performance optimization.

    Args:
        layer: The encoder layer to be stacked multiple times
        num_layers: Number of encoder layers to stack
        d_model: Model dimension/hidden size
        num_feature_levels: Number of feature levels to process
        add_pooled_text_to_img_feat: Whether to add pooled text features to image features
        pool_text_with_mask: Whether to use the mask when pooling text features
        compile_mode: Mode for torch.compile, or None to disable compilation
        **kwargs: Additional arguments to pass to the parent class
    """

    def __init__(
        self,
        layer: nn.Module,
        num_layers: int,
        d_model: int,
        num_feature_levels: int,
        add_pooled_text_to_img_feat: bool = True,
        pool_text_with_mask: bool = False,
        compile_mode: Optional[str] = None,
        **kwargs,
    ):
        super().__init__(
            layer,
            num_layers,
            d_model,
            num_feature_levels,
            **kwargs,
        )
        self.add_pooled_text_to_img_feat = add_pooled_text_to_img_feat
        if self.add_pooled_text_to_img_feat:
            self.text_pooling_proj = nn.Linear(d_model, d_model)
        self.pool_text_with_mask = pool_text_with_mask
        if compile_mode is not None:
            self.forward = torch.compile(
                self.forward, mode=compile_mode, fullgraph=True
            )

    @staticmethod
    def get_reference_points(spatial_shapes, valid_ratios, device):
        # Not needed here
        return None

    def forward(
        self,
        src: List[Tensor],
        prompt: Tensor,
        src_key_padding_mask: Optional[List[Tensor]] = None,
        src_pos: Optional[List[Tensor]] = None,
        prompt_key_padding_mask: Optional[Tensor] = None,
        prompt_pos: Optional[Tensor] = None,
        feat_sizes: Optional[List[int]] = None,
        encoder_extra_kwargs: Optional[Dict] = None,
    ):
        # Restore spatial shapes of vision
        bs = src[0].shape[1]  # seq first
        if feat_sizes is not None:
            assert len(feat_sizes) == len(src)
            if src_key_padding_mask is None:
                src_key_padding_mask = [None] * len(src)
            for i, (h, w) in enumerate(feat_sizes):
                src[i] = src[i].reshape(h, w, bs, -1).permute(2, 3, 0, 1)
                src_pos[i] = src_pos[i].reshape(h, w, bs, -1).permute(2, 3, 0, 1)
                src_key_padding_mask[i] = (
                    src_key_padding_mask[i].reshape(h, w, bs).permute(2, 0, 1)
                    if src_key_padding_mask[i] is not None
                    else None
                )
        else:
            assert all(x.dim == 4 for x in src), (
                "expected list of (bs, c, h, w) tensors"
            )

        if self.add_pooled_text_to_img_feat:
            # Fusion: Add mean pooled text to image features
            pooled_text = pool_text_feat(
                prompt, prompt_key_padding_mask, self.pool_text_with_mask
            )
            pooled_text = self.text_pooling_proj(pooled_text)[
                ..., None, None
            ]  # prompt is seq first
            src = [x.add_(pooled_text) for x in src]

        (
            out,
            key_padding_masks_flatten,
            lvl_pos_embed_flatten,
            level_start_index,
            spatial_shapes,
            valid_ratios,
        ) = super().forward(
            src,
            src_key_padding_masks=src_key_padding_mask,
            pos=src_pos,
            prompt=prompt.transpose(0, 1),
            prompt_key_padding_mask=prompt_key_padding_mask,
            encoder_extra_kwargs=encoder_extra_kwargs,
        )

        return {
            "memory": out,
            "padding_mask": key_padding_masks_flatten,
            "pos_embed": lvl_pos_embed_flatten,
            "memory_text": prompt,
            "level_start_index": level_start_index,
            "spatial_shapes": spatial_shapes,
            "valid_ratios": valid_ratios,
        }


def pool_text_feat(prompt, prompt_mask, pool_with_mask):
    # prompt has shape (seq, bs, dim)
    if not pool_with_mask:
        return prompt.mean(dim=0)

    # prompt_mask has shape (bs, seq), where False is valid and True is padding
    assert prompt_mask.dim() == 2
    # is_valid has shape (seq, bs, 1), where 1 is valid and 0 is padding
    is_valid = (~prompt_mask).float().permute(1, 0)[..., None]
    # num_valid has shape (bs, 1)
    num_valid = torch.clamp(torch.sum(is_valid, dim=0), min=1.0)

    # mean pool over all the valid tokens
    pooled_text = (prompt * is_valid).sum(dim=0) / num_valid
    return pooled_text



================================================
FILE: sam3/model/geometry_encoders.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

from typing import Tuple

import torch
import torch.nn as nn
import torchvision
from typing_extensions import override

from .act_ckpt_utils import activation_ckpt_wrapper
from .box_ops import box_cxcywh_to_xyxy
from .model_misc import get_clones


def is_right_padded(mask):
    """Given a padding mask (following pytorch convention, 1s for padded values),
    returns whether the padding is on the right or not."""
    return (mask.long() == torch.sort(mask.long(), dim=-1)[0]).all()


def concat_padded_sequences(seq1, mask1, seq2, mask2, return_index: bool = False):
    """
    Concatenates two right-padded sequences, such that the resulting sequence
    is contiguous and also right-padded.

    Following pytorch's convention, tensors are sequence first, and the mask are
    batch first, with 1s for padded values.

    :param seq1: A tensor of shape (seq1_length, batch_size, hidden_size).
    :param mask1: A tensor of shape (batch_size, seq1_length).
    :param seq2: A tensor of shape (seq2_length, batch_size,  hidden_size).
    :param mask2: A tensor of shape (batch_size, seq2_length).
    :param return_index: If True, also returns the index of the ids of the element of seq2
        in the concatenated sequence. This can be used to retrieve the elements of seq2
    :return: A tuple (concatenated_sequence, concatenated_mask) if return_index is False,
        otherwise (concatenated_sequence, concatenated_mask, index).
    """
    seq1_length, batch_size, hidden_size = seq1.shape
    seq2_length, batch_size, hidden_size = seq2.shape

    assert batch_size == seq1.size(1) == seq2.size(1) == mask1.size(0) == mask2.size(0)
    assert hidden_size == seq1.size(2) == seq2.size(2)
    assert seq1_length == mask1.size(1)
    assert seq2_length == mask2.size(1)

    torch._assert_async(is_right_padded(mask1))
    torch._assert_async(is_right_padded(mask2))

    actual_seq1_lengths = (~mask1).sum(dim=-1)
    actual_seq2_lengths = (~mask2).sum(dim=-1)

    final_lengths = actual_seq1_lengths + actual_seq2_lengths
    max_length = seq1_length + seq2_length
    concatenated_mask = (
        torch.arange(max_length, device=seq2.device)[None].repeat(batch_size, 1)
        >= final_lengths[:, None]
    )

    # (max_len, batch_size, hidden_size)
    concatenated_sequence = torch.zeros(
        (max_length, batch_size, hidden_size), device=seq2.device, dtype=seq2.dtype
    )
    concatenated_sequence[:seq1_length, :, :] = seq1

    # At this point, the element of seq1 are in the right place
    # We just need to shift the elements of seq2

    index = torch.arange(seq2_length, device=seq2.device)[:, None].repeat(1, batch_size)
    index = index + actual_seq1_lengths[None]

    concatenated_sequence = concatenated_sequence.scatter(
        0, index[:, :, None].expand(-1, -1, hidden_size), seq2
    )

    if return_index:
        return concatenated_sequence, concatenated_mask, index

    return concatenated_sequence, concatenated_mask


class Prompt:
    """Utility class to manipulate geometric prompts.

    We expect the sequences in pytorch convention, that is sequence first, batch second
    The dimensions are expected as follows:
    box_embeddings shape: N_boxes x B x C_box
    box_mask shape: B x N_boxes. Can be None if nothing is masked out
    point_embeddings shape: N_points x B x C_point
    point_mask shape: B x N_points. Can be None if nothing is masked out
    mask_embeddings shape: N_masks x B x 1 x H_mask x W_mask
    mask_mask shape: B x N_masks. Can be None if nothing is masked out

    We also store positive/negative labels. These tensors are also stored batch-first
    If they are None, we'll assume positive labels everywhere
    box_labels: long tensor of shape N_boxes x B
    point_labels: long tensor of shape N_points x B
    mask_labels: long tensor of shape N_masks x B
    """

    def __init__(
        self,
        box_embeddings=None,
        box_mask=None,
        point_embeddings=None,
        point_mask=None,
        box_labels=None,
        point_labels=None,
        mask_embeddings=None,
        mask_mask=None,  # Attention mask for mask prompt
        mask_labels=None,
    ):
        # Check for null prompt
        if (
            box_embeddings is None
            and point_embeddings is None
            and mask_embeddings is None
        ):
            self.box_embeddings = None
            self.box_labels = None
            self.box_mask = None
            self.point_embeddings = None
            self.point_labels = None
            self.point_mask = None
            self.mask_embeddings = None
            self.mask_mask = None
            # Masks are assumed positive only for now.
            self.mask_labels = None
            return
        # Get sequence lengths and device
        box_seq_len, point_seq_len, mask_seq_len, bs, device = (
            self._init_seq_len_and_device(
                box_embeddings, point_embeddings, mask_embeddings
            )
        )

        # Initialize embeds, labels, attention masks.
        box_embeddings, box_labels, box_mask = self._init_box(
            box_embeddings, box_labels, box_mask, box_seq_len, bs, device
        )
        point_embeddings, point_labels, point_mask = self._init_point(
            point_embeddings, point_labels, point_mask, point_seq_len, bs, device
        )
        mask_embeddings, mask_labels, mask_mask = self._init_mask(
            mask_embeddings, mask_labels, mask_mask, mask_seq_len, bs, device
        )

        # Dimension checks
        assert box_embeddings is not None and list(box_embeddings.shape[:2]) == [
            box_seq_len,
            bs,
        ], (
            f"Wrong dimension for box embeddings. Expected [{box_seq_len}, {bs}, *] got {box_embeddings.shape}"
        )
        assert box_mask is not None and list(box_mask.shape) == [
            bs,
            box_seq_len,
        ], (
            f"Wrong dimension for box mask. Expected [{bs}, {box_seq_len}] got {box_mask.shape}"
        )
        assert point_embeddings is not None and list(point_embeddings.shape[:2]) == [
            point_seq_len,
            bs,
        ], (
            f"Wrong dimension for point embeddings. Expected [{point_seq_len}, {bs}, *] got {point_embeddings.shape}"
        )
        assert point_mask is not None and list(point_mask.shape) == [
            bs,
            point_seq_len,
        ], (
            f"Wrong dimension for point mask. Expected [{bs}, {point_seq_len}] got {point_mask.shape}"
        )
        assert box_labels is not None and list(box_labels.shape) == [
            box_seq_len,
            bs,
        ], (
            f"Wrong dimension for box labels. Expected [{box_seq_len}, {bs}] got {box_labels.shape}"
        )
        assert point_labels is not None and list(point_labels.shape) == [
            point_seq_len,
            bs,
        ], (
            f"Wrong dimension for point labels. Expected [{point_seq_len}, {bs}] got {point_labels.shape}"
        )
        assert (
            # Allowed to be None, we leave it to the encoder to check for validity before encoding.
            mask_embeddings is None
            or list(mask_embeddings.shape[:2])
            == [
                mask_seq_len,
                bs,
            ]
        ), (
            f"Wrong dimension for mask embeddings. Expected [{mask_seq_len}, {bs}, *] got {mask_embeddings.shape}"
        )
        assert mask_mask is None or list(mask_mask.shape) == [
            bs,
            mask_seq_len,
        ], (
            f"Wrong dimension for mask attn. mask. Expected [{bs}, {mask_seq_len}] got {mask_mask.shape}"
        )

        # Device checks
        assert box_embeddings is not None and box_embeddings.device == device, (
            f"Expected box embeddings to be on device {device}, got {box_embeddings.device}"
        )
        assert box_mask is not None and box_mask.device == device, (
            f"Expected box mask to be on device {device}, got {box_mask.device}"
        )
        assert box_labels is not None and box_labels.device == device, (
            f"Expected box labels to be on device {device}, got {box_labels.device}"
        )
        assert point_embeddings is not None and point_embeddings.device == device, (
            f"Expected point embeddings to be on device {device}, got {point_embeddings.device}"
        )
        assert point_mask is not None and point_mask.device == device, (
            f"Expected point mask to be on device {device}, got {point_mask.device}"
        )
        assert point_labels is not None and point_labels.device == device, (
            f"Expected point labels to be on device {device}, got {point_labels.device}"
        )
        assert mask_embeddings is None or mask_embeddings.device == device, (
            f"Expected mask embeddings to be on device {device}, got {mask_embeddings.device}"
        )
        assert mask_mask is None or mask_mask.device == device, (
            f"Expected mask attn. mask to be on device {device}, got {mask_mask.device}"
        )

        self.box_embeddings = box_embeddings
        self.point_embeddings = point_embeddings
        self.box_mask = box_mask
        self.point_mask = point_mask
        self.box_labels = box_labels
        self.point_labels = point_labels
        self.mask_embeddings = mask_embeddings
        self.mask_labels = mask_labels
        self.mask_mask = mask_mask

    def _init_seq_len_and_device(
        self, box_embeddings, point_embeddings, mask_embeddings
    ):
        box_seq_len = point_seq_len = mask_seq_len = 0
        bs = None
        device = None
        if box_embeddings is not None:
            bs = box_embeddings.shape[1]
            box_seq_len = box_embeddings.shape[0]
            device = box_embeddings.device

        if point_embeddings is not None:
            point_seq_len = point_embeddings.shape[0]
            if bs is not None:
                assert bs == point_embeddings.shape[1], (
                    f"Batch size mismatch between box and point embeddings. Got {bs} and {point_embeddings.shape[1]}."
                )
            else:
                bs = point_embeddings.shape[1]
            if device is not None:
                assert device == point_embeddings.device, (
                    "Device mismatch between box and point embeddings"
                )
            else:
                device = point_embeddings.device

        if mask_embeddings is not None:
            mask_seq_len = mask_embeddings.shape[0]
            if bs is not None:
                assert bs == mask_embeddings.shape[1], (
                    f"Batch size mismatch between box/point and mask embedding. Got {bs} and {mask_embeddings.shape[1]}"
                )
            else:
                bs = mask_embeddings.shape[1]
            if device is not None:
                assert device == mask_embeddings.device, (
                    "Device mismatch between box/point and mask embeddings."
                )
            else:
                device = mask_embeddings.device

        return box_seq_len, point_seq_len, mask_seq_len, bs, device

    def _init_box(self, box_embeddings, box_labels, box_mask, box_seq_len, bs, device):
        if box_embeddings is None:
            box_embeddings = torch.zeros(box_seq_len, bs, 4, device=device)
        if box_labels is None:
            box_labels = torch.ones(box_seq_len, bs, device=device, dtype=torch.long)
        if box_mask is None:
            box_mask = torch.zeros(bs, box_seq_len, device=device, dtype=torch.bool)
        return box_embeddings, box_labels, box_mask

    def _init_point(
        self, point_embeddings, point_labels, point_mask, point_seq_len, bs, device
    ):
        """
        Identical to _init_box. Except that C=2 for points (vs. 4 for boxes).
        """
        if point_embeddings is None:
            point_embeddings = torch.zeros(point_seq_len, bs, 2, device=device)
        if point_labels is None:
            point_labels = torch.ones(
                point_seq_len, bs, device=device, dtype=torch.long
            )
        if point_mask is None:
            point_mask = torch.zeros(bs, point_seq_len, device=device, dtype=torch.bool)
        return point_embeddings, point_labels, point_mask

    def _init_mask(
        self, mask_embeddings, mask_labels, mask_mask, mask_seq_len, bs, device
    ):
        # NOTE: Mask embeddings can be of arbitrary resolution, so we don't initialize it here.
        # In case we append new mask, we check that its resolution matches exisiting ones (if any).
        # In case mask_embeddings is None, we should never encode it.
        if mask_labels is None:
            mask_labels = torch.ones(mask_seq_len, bs, device=device, dtype=torch.long)
        if mask_mask is None:
            mask_mask = torch.zeros(bs, mask_seq_len, device=device, dtype=torch.bool)
        return mask_embeddings, mask_labels, mask_mask

    def append_boxes(self, boxes, labels, mask=None):
        if self.box_embeddings is None:
            self.box_embeddings = boxes
            self.box_labels = labels
            self.box_mask = mask
            return

        bs = self.box_embeddings.shape[1]
        assert boxes.shape[1] == labels.shape[1] == bs
        assert list(boxes.shape[:2]) == list(labels.shape[:2])
        if mask is None:
            mask = torch.zeros(
                bs, boxes.shape[0], dtype=torch.bool, device=boxes.device
            )

        self.box_labels, _ = concat_padded_sequences(
            self.box_labels.unsqueeze(-1), self.box_mask, labels.unsqueeze(-1), mask
        )
        self.box_labels = self.box_labels.squeeze(-1)
        self.box_embeddings, self.box_mask = concat_padded_sequences(
            self.box_embeddings, self.box_mask, boxes, mask
        )

    def append_points(self, points, labels, mask=None):
        if self.point_embeddings is None:
            self.point_embeddings = points
            self.point_labels = labels
            self.point_mask = mask
            return

        bs = self.point_embeddings.shape[1]
        assert points.shape[1] == labels.shape[1] == bs
        assert list(points.shape[:2]) == list(labels.shape[:2])
        if mask is None:
            mask = torch.zeros(
                bs, points.shape[0], dtype=torch.bool, device=points.device
            )

        self.point_labels, _ = concat_padded_sequences(
            self.point_labels.unsqueeze(-1), self.point_mask, labels.unsqueeze(-1), mask
        )
        self.point_labels = self.point_labels.squeeze(-1)
        self.point_embeddings, self.point_mask = concat_padded_sequences(
            self.point_embeddings, self.point_mask, points, mask
        )

    def append_masks(self, masks, labels=None, attn_mask=None):
        if labels is not None:
            assert list(masks.shape[:2]) == list(labels.shape[:2])
        if self.mask_embeddings is None:
            self.mask_embeddings = masks
            mask_seq_len, bs = masks.shape[:2]
            if labels is None:
                self.mask_labels = torch.ones(
                    mask_seq_len, bs, device=masks.device, dtype=torch.long
                )
            else:
                self.mask_labels = labels
            if attn_mask is None:
                self.mask_mask = torch.zeros(
                    bs, mask_seq_len, device=masks.device, dtype=torch.bool
                )
            else:
                self.mask_mask = attn_mask
        else:
            raise NotImplementedError("Only one mask per prompt is supported.")

    def clone(self):
        return Prompt(
            box_embeddings=(
                None if self.box_embeddings is None else self.box_embeddings.clone()
            ),
            box_mask=None if self.box_mask is None else self.box_mask.clone(),
            point_embeddings=(
                None if self.point_embeddings is None else self.point_embeddings.clone()
            ),
            point_mask=None if self.point_mask is None else self.point_mask.clone(),
            box_labels=None if self.box_labels is None else self.box_labels.clone(),
            point_labels=(
                None if self.point_labels is None else self.point_labels.clone()
            ),
        )


class MaskEncoder(nn.Module):
    """
    Base class for mask encoders.
    """

    def __init__(
        self,
        mask_downsampler: nn.Module,
        position_encoding: nn.Module,
    ):
        super().__init__()
        self.mask_downsampler = mask_downsampler
        self.position_encoding = position_encoding

    def forward(self, masks, *args, **kwargs) -> Tuple[torch.Tensor, torch.Tensor]:
        masks = self.mask_downsampler(masks)
        masks_pos = self.position_encoding(masks).to(masks.dtype)

        return masks, masks_pos


class FusedMaskEncoder(MaskEncoder):
    """
    Identical to memory.SimpleMaskEncoder but follows the interface of geometry_encoders.MaskEncoder.
    We also remove the `skip_mask_sigmoid` option (to be handled outside the MaskEncoder).
    Fuses backbone image features with mask features.
    """

    def __init__(
        self,
        mask_downsampler: nn.Module,
        position_encoding: nn.Module,
        fuser: nn.Module,
        in_dim: int = 256,
        out_dim: int = 256,
    ):
        super().__init__(mask_downsampler, position_encoding)
        self.fuser = fuser
        self.out_proj = nn.Identity()
        if out_dim != in_dim:
            self.out_proj = nn.Conv2d(in_dim, out_dim, kernel_size=1)
        self.pix_feat_proj = nn.Conv2d(in_dim, in_dim, kernel_size=1)

    @override
    def forward(
        self,
        masks: torch.Tensor,
        pix_feat: torch.Tensor,
        **kwargs,
    ) -> Tuple[torch.Tensor, torch.Tensor]:
        masks = self.mask_downsampler(masks)

        ## Fuse pix_feats and downsampled masks
        # in case the visual features are on CPU, cast them to CUDA
        pix_feat = pix_feat.to(masks.device)

        x = self.pix_feat_proj(pix_feat)
        x = x + masks
        x = self.fuser(x)
        x = self.out_proj(x)

        pos = self.position_encoding(x).to(x.dtype)

        return x, pos


class SequenceGeometryEncoder(nn.Module):
    """
    This a fully fledged encoder for geometric prompts.
    It assumes boxes are passed in the "normalized CxCyWH" format, and points in normalized xy
    This allows flexibility in how to encode the features (eg do pooling)

    Points and boxes can be encoded with any of the three possibilities:
     - direct projection: we just compute a linear from coordinate space to d_model
     - pooling: pool features from the backbone in the requested location.
                For boxes, it's a roi align
                For points it's a grid sample
     - pos encoder: Take the position encoding of the point or box center

    These three options are mutually compatible. If several are selected, we'll take a simple addition

    As an alternative, we offer the possibility to encode points only.
    In that case, the boxes are converted to two points for the top left and bottom right corners (with appropriate labels)

    On top of these encodings, we offer the possibility to further encode the prompt sequence with a transformer.
    """

    def __init__(
        self,
        encode_boxes_as_points: bool,
        points_direct_project: bool,
        points_pool: bool,
        points_pos_enc: bool,
        boxes_direct_project: bool,
        boxes_pool: bool,
        boxes_pos_enc: bool,
        d_model: int,
        pos_enc,
        num_layers: int,
        layer: nn.Module,
        roi_size: int = 7,  # for boxes pool
        add_cls: bool = True,
        add_post_encode_proj: bool = True,
        mask_encoder: MaskEncoder = None,
        add_mask_label: bool = False,
        use_act_ckpt: bool = False,
    ):
        super().__init__()

        self.d_model = d_model
        self.pos_enc = pos_enc
        self.encode_boxes_as_points = encode_boxes_as_points
        self.roi_size = roi_size
        # There usually are two labels: positive and negatives.
        # If we encode boxes as points, we have 3 types of points: regular, top left, bottom right
        # These 3 types can be positives or negatives, hence 2*3 = 6 labels
        num_labels = 6 if self.encode_boxes_as_points else 2
        self.label_embed = torch.nn.Embedding(num_labels, self.d_model)

        # This is a cls token, can be used for pooling if need be.
        # It also ensures that the encoded sequences are always non-empty
        self.cls_embed = None
        if add_cls:
            self.cls_embed = torch.nn.Embedding(1, self.d_model)

        assert points_direct_project or points_pos_enc or points_pool, (
            "Error: need at least one way to encode points"
        )
        assert (
            encode_boxes_as_points
            or boxes_direct_project
            or boxes_pos_enc
            or boxes_pool
        ), "Error: need at least one way to encode boxes"

        self.points_direct_project = None
        if points_direct_project:
            self.points_direct_project = nn.Linear(2, self.d_model)
        self.points_pool_project = None
        if points_pool:
            self.points_pool_project = nn.Linear(self.d_model, self.d_model)
        self.points_pos_enc_project = None
        if points_pos_enc:
            self.points_pos_enc_project = nn.Linear(self.d_model, self.d_model)

        self.boxes_direct_project = None
        self.boxes_pool_project = None
        self.boxes_pos_enc_project = None
        if not encode_boxes_as_points:
            if boxes_direct_project:
                self.boxes_direct_project = nn.Linear(4, self.d_model)
            if boxes_pool:
                self.boxes_pool_project = nn.Conv2d(
                    self.d_model, self.d_model, self.roi_size
                )
            if boxes_pos_enc:
                self.boxes_pos_enc_project = nn.Linear(self.d_model + 2, self.d_model)

        self.final_proj = None
        if add_post_encode_proj:
            self.final_proj = nn.Linear(self.d_model, self.d_model)
            self.norm = nn.LayerNorm(self.d_model)

        self.img_pre_norm = nn.Identity()
        if self.points_pool_project is not None or self.boxes_pool_project is not None:
            self.img_pre_norm = nn.LayerNorm(self.d_model)

        self.encode = None
        if num_layers > 0:
            assert add_cls, (
                "It's currently highly recommended to add a CLS when using a transformer"
            )
            self.encode = get_clones(layer, num_layers)
            self.encode_norm = nn.LayerNorm(self.d_model)

        if mask_encoder is not None:
            assert isinstance(mask_encoder, MaskEncoder), (
                f"Expected mask_encoder of type MaskEncoder. Got {type(mask_encoder)}."
            )
            if add_mask_label:
                self.mask_label_embed = torch.nn.Embedding(2, self.d_model)
        self.add_mask_label = add_mask_label
        self.mask_encoder = mask_encoder
        self.use_act_ckpt = use_act_ckpt

    def _encode_points(self, points, points_mask, points_labels, img_feats):
        points_embed = None
        n_points, bs = points.shape[:2]

        if self.points_direct_project is not None:
            proj = self.points_direct_project(points)
            assert points_embed is None
            points_embed = proj

        if self.points_pool_project is not None:
            # points are [Num_points, bs, 2], normalized in [0, 1]
            # the grid needs to be [Bs, H_out, W_out, 2] normalized in [-1,1]
            # Will take H_out = num_points, w_out = 1
            grid = points.transpose(0, 1).unsqueeze(2)
            # re normalize to [-1, 1]
            grid = (grid * 2) - 1
            sampled = torch.nn.functional.grid_sample(
                img_feats, grid, align_corners=False
            )
            assert list(sampled.shape) == [bs, self.d_model, n_points, 1]
            sampled = sampled.squeeze(-1).permute(2, 0, 1)
            proj = self.points_pool_project(sampled)
            if points_embed is None:
                points_embed = proj
            else:
                points_embed = points_embed + proj

        if self.points_pos_enc_project is not None:
            x, y = points.unbind(-1)
            enc_x, enc_y = self.pos_enc._encode_xy(x.flatten(), y.flatten())
            enc_x = enc_x.view(n_points, bs, enc_x.shape[-1])
            enc_y = enc_y.view(n_points, bs, enc_y.shape[-1])
            enc = torch.cat([enc_x, enc_y], -1)

            proj = self.points_pos_enc_project(enc)
            if points_embed is None:
                points_embed = proj
            else:
                points_embed = points_embed + proj

        type_embed = self.label_embed(points_labels.long())
        return type_embed + points_embed, points_mask

    def _encode_boxes(self, boxes, boxes_mask, boxes_labels, img_feats):
        boxes_embed = None
        n_boxes, bs = boxes.shape[:2]

        if self.boxes_direct_project is not None:
            proj = self.boxes_direct_project(boxes)
            assert boxes_embed is None
            boxes_embed = proj

        if self.boxes_pool_project is not None:
            H, W = img_feats.shape[-2:]

            # boxes are [Num_boxes, bs, 4], normalized in [0, 1]
            # We need to denormalize, and convert to [x, y, x, y]
            boxes_xyxy = box_cxcywh_to_xyxy(boxes)
            scale = torch.tensor([W, H, W, H], dtype=boxes_xyxy.dtype)
            scale = scale.pin_memory().to(device=boxes_xyxy.device, non_blocking=True)
            scale = scale.view(1, 1, 4)
            boxes_xyxy = boxes_xyxy * scale
            sampled = torchvision.ops.roi_align(
                img_feats, boxes_xyxy.float().transpose(0, 1).unbind(0), self.roi_size
            )
            assert list(sampled.shape) == [
                bs * n_boxes,
                self.d_model,
                self.roi_size,
                self.roi_size,
            ]
            proj = self.boxes_pool_project(sampled)
            proj = proj.view(bs, n_boxes, self.d_model).transpose(0, 1)
            if boxes_embed is None:
                boxes_embed = proj
            else:
                boxes_embed = boxes_embed + proj

        if self.boxes_pos_enc_project is not None:
            cx, cy, w, h = boxes.unbind(-1)
            enc = self.pos_enc.encode_boxes(
                cx.flatten(), cy.flatten(), w.flatten(), h.flatten()
            )
            enc = enc.view(boxes.shape[0], boxes.shape[1], enc.shape[-1])

            proj = self.boxes_pos_enc_project(enc)
            if boxes_embed is None:
                boxes_embed = proj
            else:
                boxes_embed = boxes_embed + proj

        type_embed = self.label_embed(boxes_labels.long())
        return type_embed + boxes_embed, boxes_mask

    def _encode_masks(
        self,
        masks: torch.Tensor,
        attn_mask: torch.Tensor,
        mask_labels: torch.Tensor,
        img_feats: torch.Tensor = None,
    ):
        n_masks, bs = masks.shape[:2]
        assert n_masks == 1, (
            "We assume one mask per prompt for now. Code should still be functional if this assertion is removed."
        )
        assert list(attn_mask.shape) == [
            bs,
            n_masks,
        ], (
            f"Expected attn_mask to be of shape {bs}x{n_masks}. Got {list(attn_mask.shape)}."
        )
        masks, pos = self.mask_encoder(
            masks=masks.flatten(0, 1).float(),
            pix_feat=img_feats,
        )
        H, W = masks.shape[-2:]
        n_tokens_per_mask = H * W
        # NOTE: We directly add pos enc here as we usually don't keep track of pos encoding for the concatenated prompt (text, other geometric prompts). Might need to do some refactoring for more flexibility.
        masks = masks + pos
        masks = masks.view(n_masks, bs, *masks.shape[1:]).flatten(
            -2
        )  # n_masks x bs x C x H*W
        masks = masks.permute(0, 3, 1, 2).flatten(0, 1)  # n_masks * H*W x bs x C
        attn_mask = attn_mask.repeat_interleave(n_tokens_per_mask, dim=1)
        if self.add_mask_label:
            masks = masks + self.mask_label_embed(mask_labels.long())
        return masks, attn_mask

    def forward(self, geo_prompt: Prompt, img_feats, img_sizes, img_pos_embeds=None):
        points = geo_prompt.point_embeddings
        points_mask = geo_prompt.point_mask
        points_labels = geo_prompt.point_labels
        boxes = geo_prompt.box_embeddings
        boxes_mask = geo_prompt.box_mask
        boxes_labels = geo_prompt.box_labels
        masks = geo_prompt.mask_embeddings
        masks_mask = geo_prompt.mask_mask
        masks_labels = geo_prompt.mask_labels
        seq_first_img_feats = img_feats[-1]  # [H*W, B, C]
        seq_first_img_pos_embeds = (
            img_pos_embeds[-1]
            if img_pos_embeds is not None
            else torch.zeros_like(seq_first_img_feats)
        )

        if self.points_pool_project or self.boxes_pool_project:
            assert len(img_feats) == len(img_sizes)
            cur_img_feat = img_feats[-1]
            cur_img_feat = self.img_pre_norm(cur_img_feat)
            H, W = img_sizes[-1]
            assert cur_img_feat.shape[0] == H * W
            N, C = cur_img_feat.shape[-2:]
            # Put back in NxCxHxW
            cur_img_feat = cur_img_feat.permute(1, 2, 0)
            cur_img_feat = cur_img_feat.view(N, C, H, W)
            img_feats = cur_img_feat

        if self.encode_boxes_as_points:
            assert boxes is not None
            assert geo_prompt.box_mask is not None
            assert geo_prompt.box_labels is not None
            assert boxes.shape[-1] == 4

            boxes_xyxy = box_cxcywh_to_xyxy(boxes)
            top_left, bottom_right = boxes_xyxy.split(split_size=2, dim=-1)

            labels_tl = geo_prompt.box_labels + 2
            labels_br = geo_prompt.box_labels + 4

            # Append to the existing points
            points, _ = concat_padded_sequences(
                points, points_mask, top_left, boxes_mask
            )
            points_labels, points_mask = concat_padded_sequences(
                points_labels.unsqueeze(-1),
                points_mask,
                labels_tl.unsqueeze(-1),
                boxes_mask,
            )
            points_labels = points_labels.squeeze(-1)

            points, _ = concat_padded_sequences(
                points, points_mask, bottom_right, boxes_mask
            )
            points_labels, points_mask = concat_padded_sequences(
                points_labels.unsqueeze(-1),
                points_mask,
                labels_br.unsqueeze(-1),
                boxes_mask,
            )
            points_labels = points_labels.squeeze(-1)

        final_embeds, final_mask = self._encode_points(
            points=points,
            points_mask=points_mask,
            points_labels=points_labels,
            img_feats=img_feats,
        )

        if not self.encode_boxes_as_points:
            boxes_embeds, boxes_mask = self._encode_boxes(
                boxes=boxes,
                boxes_mask=boxes_mask,
                boxes_labels=boxes_labels,
                img_feats=img_feats,
            )

            final_embeds, final_mask = concat_padded_sequences(
                final_embeds, final_mask, boxes_embeds, boxes_mask
            )

        if masks is not None and self.mask_encoder is not None:
            masks_embed, masks_mask = self._encode_masks(
                masks=masks,
                attn_mask=masks_mask,
                mask_labels=masks_labels,
                img_feats=img_feats,
            )
            if points.size(0) == boxes.size(0) == 0:
                return masks_embed, masks_mask
        bs = final_embeds.shape[1]
        assert final_mask.shape[0] == bs
        if self.cls_embed is not None:
            cls = self.cls_embed.weight.view(1, 1, self.d_model).repeat(1, bs, 1)
            cls_mask = torch.zeros(
                bs, 1, dtype=final_mask.dtype, device=final_mask.device
            )
            final_embeds, final_mask = concat_padded_sequences(
                final_embeds, final_mask, cls, cls_mask
            )

        if self.final_proj is not None:
            final_embeds = self.norm(self.final_proj(final_embeds))

        if self.encode is not None:
            for lay in self.encode:
                final_embeds = activation_ckpt_wrapper(lay)(
                    tgt=final_embeds,
                    memory=seq_first_img_feats,
                    tgt_key_padding_mask=final_mask,
                    pos=seq_first_img_pos_embeds,
                    act_ckpt_enable=self.training and self.use_act_ckpt,
                )
            final_embeds = self.encode_norm(final_embeds)
        # Finally, concat mask embeddings if any
        if masks is not None and self.mask_encoder is not None:
            final_embeds, final_mask = concat_padded_sequences(
                final_embeds, final_mask, masks_embed, masks_mask
            )
        return final_embeds, final_mask



================================================
FILE: sam3/model/io_utils.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

import contextlib
import os
import queue
import re
import time
from threading import Condition, get_ident, Lock, Thread

import numpy as np
import torch
import torch.nn.functional as F
import torchvision.transforms.functional as TF
from PIL import Image
from sam3.logger import get_logger
from tqdm import tqdm

logger = get_logger(__name__)

IS_MAIN_PROCESS = os.getenv("IS_MAIN_PROCESS", "1") == "1"
RANK = int(os.getenv("RANK", "0"))

IMAGE_EXTS = [".jpg", ".jpeg", ".png", ".bmp", ".tiff", ".webp"]
VIDEO_EXTS = [".mp4", ".mov", ".avi", ".mkv", ".webm"]


def load_resource_as_video_frames(
    resource_path,
    image_size,
    offload_video_to_cpu,
    img_mean=(0.5, 0.5, 0.5),
    img_std=(0.5, 0.5, 0.5),
    async_loading_frames=False,
    video_loader_type="cv2",
):
    """
    Load video frames from either a video or an image (as a single-frame video).
    Alternatively, if input is a list of PIL images, convert its format
    """
    if isinstance(resource_path, list):
        img_mean = torch.tensor(img_mean, dtype=torch.float16)[:, None, None]
        img_std = torch.tensor(img_std, dtype=torch.float16)[:, None, None]
        assert all(isinstance(img_pil, Image.Image) for img_pil in resource_path)
        assert len(resource_path) is not None
        orig_height, orig_width = resource_path[0].size
        orig_height, orig_width = (
            orig_width,
            orig_height,
        )  # For some reason, this method returns these swapped
        images = []
        for img_pil in resource_path:
            img_np = np.array(img_pil.convert("RGB").resize((image_size, image_size)))
            assert img_np.dtype == np.uint8, "np.uint8 is expected for JPEG images"
            img_np = img_np / 255.0
            img = torch.from_numpy(img_np).permute(2, 0, 1)
            # float16 precision should be sufficient for image tensor storage
            img = img.to(dtype=torch.float16)
            # normalize by mean and std
            img -= img_mean
            img /= img_std
            images.append(img)
        images = torch.stack(images)
        if not offload_video_to_cpu:
            images = images.cuda()
        return images, orig_height, orig_width

    is_image = (
        isinstance(resource_path, str)
        and os.path.splitext(resource_path)[-1].lower() in IMAGE_EXTS
    )
    if is_image:
        return load_image_as_single_frame_video(
            image_path=resource_path,
            image_size=image_size,
            offload_video_to_cpu=offload_video_to_cpu,
            img_mean=img_mean,
            img_std=img_std,
        )
    else:
        return load_video_frames(
            video_path=resource_path,
            image_size=image_size,
            offload_video_to_cpu=offload_video_to_cpu,
            img_mean=img_mean,
            img_std=img_std,
            async_loading_frames=async_loading_frames,
            video_loader_type=video_loader_type,
        )


def load_image_as_single_frame_video(
    image_path,
    image_size,
    offload_video_to_cpu,
    img_mean=(0.5, 0.5, 0.5),
    img_std=(0.5, 0.5, 0.5),
):
    """Load an image as a single-frame video."""
    images, image_height, image_width = _load_img_as_tensor(image_path, image_size)
    images = images.unsqueeze(0).half()

    img_mean = torch.tensor(img_mean, dtype=torch.float16)[:, None, None]
    img_std = torch.tensor(img_std, dtype=torch.float16)[:, None, None]
    if not offload_video_to_cpu:
        images = images.cuda()
        img_mean = img_mean.cuda()
        img_std = img_std.cuda()
    # normalize by mean and std
    images -= img_mean
    images /= img_std
    return images, image_height, image_width


def load_video_frames(
    video_path,
    image_size,
    offload_video_to_cpu,
    img_mean=(0.5, 0.5, 0.5),
    img_std=(0.5, 0.5, 0.5),
    async_loading_frames=False,
    video_loader_type="cv2",
):
    """
    Load the video frames from video_path. The frames are resized to image_size as in
    the model and are loaded to GPU if offload_video_to_cpu=False. This is used by the demo.
    """
    assert isinstance(video_path, str)
    if video_path.startswith("<load-dummy-video"):
        # Check for pattern <load-dummy-video-N> where N is an integer
        match = re.match(r"<load-dummy-video-(\d+)>", video_path)
        num_frames = int(match.group(1)) if match else 60
        return load_dummy_video(image_size, offload_video_to_cpu, num_frames=num_frames)
    elif video_path.startswith("<load-zero-video"):
        # Check for pattern <load-zero-video-N> where N is an integer
        match = re.match(r"<load-zero-video-(\d+)>", video_path)
        num_frames = int(match.group(1)) if match else 60
        return load_dummy_video(
            image_size, offload_video_to_cpu, num_frames=num_frames, do_zeros=True
        )
    elif os.path.isdir(video_path):
        return load_video_frames_from_image_folder(
            image_folder=video_path,
            image_size=image_size,
            offload_video_to_cpu=offload_video_to_cpu,
            img_mean=img_mean,
            img_std=img_std,
            async_loading_frames=async_loading_frames,
        )
    elif os.path.splitext(video_path)[-1].lower() in VIDEO_EXTS:
        return load_video_frames_from_video_file(
            video_path=video_path,
            image_size=image_size,
            offload_video_to_cpu=offload_video_to_cpu,
            img_mean=img_mean,
            img_std=img_std,
            async_loading_frames=async_loading_frames,
            video_loader_type=video_loader_type,
        )
    else:
        raise NotImplementedError("Only video files and image folders are supported")


def load_video_frames_from_image_folder(
    image_folder,
    image_size,
    offload_video_to_cpu,
    img_mean,
    img_std,
    async_loading_frames,
):
    """
    Load the video frames from a directory of image files ("<frame_index>.<img_ext>" format)
    """
    frame_names = [
        p
        for p in os.listdir(image_folder)
        if os.path.splitext(p)[-1].lower() in IMAGE_EXTS
    ]
    try:
        frame_names.sort(key=lambda p: int(os.path.splitext(p)[0]))
    except ValueError:
        # fallback to lexicographic sort if the format is not "<frame_index>.<img_ext>"
        logger.warning(
            f'frame names are not in "<frame_index>.<img_ext>" format: {frame_names[:5]=}, '
            f"falling back to lexicographic sort."
        )
        frame_names.sort()
    num_frames = len(frame_names)
    if num_frames == 0:
        raise RuntimeError(f"no images found in {image_folder}")
    img_paths = [os.path.join(image_folder, frame_name) for frame_name in frame_names]
    img_mean = torch.tensor(img_mean, dtype=torch.float16)[:, None, None]
    img_std = torch.tensor(img_std, dtype=torch.float16)[:, None, None]

    if async_loading_frames:
        lazy_images = AsyncImageFrameLoader(
            img_paths, image_size, offload_video_to_cpu, img_mean, img_std
        )
        return lazy_images, lazy_images.video_height, lazy_images.video_width

    # float16 precision should be sufficient for image tensor storage
    images = torch.zeros(num_frames, 3, image_size, image_size, dtype=torch.float16)
    video_height, video_width = None, None
    for n, img_path in enumerate(
        tqdm(img_paths, desc=f"frame loading (image folder) [rank={RANK}]")
    ):
        images[n], video_height, video_width = _load_img_as_tensor(img_path, image_size)
    if not offload_video_to_cpu:
        images = images.cuda()
        img_mean = img_mean.cuda()
        img_std = img_std.cuda()
    # normalize by mean and std
    images -= img_mean
    images /= img_std
    return images, video_height, video_width


def load_video_frames_from_video_file(
    video_path,
    image_size,
    offload_video_to_cpu,
    img_mean,
    img_std,
    async_loading_frames,
    gpu_acceleration=False,
    gpu_device=None,
    video_loader_type="cv2",
):
    """Load the video frames from a video file."""
    if video_loader_type == "cv2":
        return load_video_frames_from_video_file_using_cv2(
            video_path=video_path,
            image_size=image_size,
            img_mean=img_mean,
            img_std=img_std,
            offload_video_to_cpu=offload_video_to_cpu,
        )
    elif video_loader_type == "torchcodec":
        logger.info("Using torchcodec to load video file")
        lazy_images = AsyncVideoFileLoaderWithTorchCodec(
            video_path=video_path,
            image_size=image_size,
            offload_video_to_cpu=offload_video_to_cpu,
            img_mean=img_mean,
            img_std=img_std,
            gpu_acceleration=gpu_acceleration,
            gpu_device=gpu_device,
        )
        # The `AsyncVideoFileLoaderWithTorchCodec` class always loads the videos asynchronously,
        # so we just wait for its loading thread to finish if async_loading_frames=False.
        if not async_loading_frames:
            async_thread = lazy_images.thread
            if async_thread is not None:
                async_thread.join()
        return lazy_images, lazy_images.video_height, lazy_images.video_width
    else:
        raise RuntimeError("video_loader_type must be either 'cv2' or 'torchcodec'")


def load_video_frames_from_video_file_using_cv2(
    video_path: str,
    image_size: int,
    img_mean: tuple = (0.5, 0.5, 0.5),
    img_std: tuple = (0.5, 0.5, 0.5),
    offload_video_to_cpu: bool = False,
) -> torch.Tensor:
    """
    Load video from path, convert to normalized tensor with specified preprocessing

    Args:
        video_path: Path to video file
        image_size: Target size for square frames (height and width)
        img_mean: Normalization mean (RGB)
        img_std: Normalization standard deviation (RGB)

    Returns:
        torch.Tensor: Preprocessed video tensor in shape (T, C, H, W) with float16 dtype
    """
    import cv2  # delay OpenCV import to avoid unnecessary dependency

    # Initialize video capture
    cap = cv2.VideoCapture(video_path)
    if not cap.isOpened():
        raise ValueError(f"Could not open video: {video_path}")

    original_height = int(cap.get(cv2.CAP_PROP_FRAME_HEIGHT))
    original_width = int(cap.get(cv2.CAP_PROP_FRAME_WIDTH))
    num_frames = int(cap.get(cv2.CAP_PROP_FRAME_COUNT))
    num_frames = num_frames if num_frames > 0 else None

    frames = []
    pbar = tqdm(desc=f"frame loading (OpenCV) [rank={RANK}]", total=num_frames)
    while True:
        ret, frame = cap.read()
        if not ret:
            break

        # Convert BGR to RGB and resize
        frame_rgb = cv2.cvtColor(frame, cv2.COLOR_BGR2RGB)
        frame_resized = cv2.resize(
            frame_rgb, (image_size, image_size), interpolation=cv2.INTER_CUBIC
        )
        frames.append(frame_resized)
        pbar.update(1)
    cap.release()
    pbar.close()

    if len(frames) == 0:
        raise RuntimeError(
            f"No frames could be decoded from video: {video_path}. "
            f"The file may be corrupted, empty, or encoded with an unsupported codec."
        )

    # Convert to tensor
    frames_np = np.stack(frames, axis=0).astype(np.float32)  # (T, H, W, C)
    video_tensor = torch.from_numpy(frames_np).permute(0, 3, 1, 2)  # (T, C, H, W)

    img_mean = torch.tensor(img_mean, dtype=torch.float16).view(1, 3, 1, 1)
    img_std = torch.tensor(img_std, dtype=torch.float16).view(1, 3, 1, 1)
    if not offload_video_to_cpu:
        video_tensor = video_tensor.cuda()
        img_mean = img_mean.cuda()
        img_std = img_std.cuda()
    # normalize by mean and std
    video_tensor -= img_mean
    video_tensor /= img_std
    return video_tensor, original_height, original_width


def load_dummy_video(image_size, offload_video_to_cpu, num_frames=60, do_zeros=False):
    """
    Load a dummy video with random frames for testing and compilation warmup purposes.
    """
    video_height, video_width = 480, 640  # dummy original video sizes
    if not do_zeros:
        images = torch.randn(num_frames, 3, image_size, image_size, dtype=torch.float16)
    else:
        images = torch.zeros(num_frames, 3, image_size, image_size, dtype=torch.float16)
    if not offload_video_to_cpu:
        images = images.cuda()
    return images, video_height, video_width


def _load_img_as_tensor(img_path, image_size):
    """Load and resize an image and convert it into a PyTorch tensor."""
    img = Image.open(img_path).convert("RGB")
    orig_width, orig_height = img.width, img.height
    img = TF.resize(img, size=(image_size, image_size))
    img = TF.to_tensor(img)
    return img, orig_height, orig_width


class AsyncImageFrameLoader:
    """
    A list of video frames to be load asynchronously without blocking session start.
    """

    def __init__(self, img_paths, image_size, offload_video_to_cpu, img_mean, img_std):
        self.img_paths = img_paths
        self.image_size = image_size
        self.offload_video_to_cpu = offload_video_to_cpu
        self.img_mean = img_mean
        self.img_std = img_std
        # items in `self._images` will be loaded asynchronously
        self.images = [None] * len(img_paths)
        # catch and raise any exceptions in the async loading thread
        self.exception = None
        # video_height and video_width be filled when loading the first image
        self.video_height = None
        self.video_width = None

        # load the first frame to fill video_height and video_width and also
        # to cache it (since it's most likely where the user will click)
        self.__getitem__(0)

        # load the rest of frames asynchronously without blocking the session start
        def _load_frames():
            try:
                for n in tqdm(
                    range(len(self.images)),
                    desc=f"frame loading (image folder) [rank={RANK}]",
                ):
                    self.__getitem__(n)
            except Exception as e:
                self.exception = e

        self.thread = Thread(target=_load_frames, daemon=True)
        self.thread.start()

    def __getitem__(self, index):
        if self.exception is not None:
            raise RuntimeError("Failure in frame loading thread") from self.exception

        img = self.images[index]
        if img is not None:
            return img

        img, video_height, video_width = _load_img_as_tensor(
            self.img_paths[index], self.image_size
        )
        self.video_height = video_height
        self.video_width = video_width
        # float16 precision should be sufficient for image tensor storage
        img = img.to(dtype=torch.float16)
        # normalize by mean and std
        img -= self.img_mean
        img /= self.img_std
        if not self.offload_video_to_cpu:
            img = img.cuda()
        self.images[index] = img
        return img

    def __len__(self):
        return len(self.images)


class TorchCodecDecoder:
    """
    A wrapper to support GPU device and num_threads in TorchCodec decoder,
    which are not supported by `torchcodec.decoders.SimpleVideoDecoder` yet.
    """

    def __init__(self, source, dimension_order="NCHW", device="cpu", num_threads=1):
        from torchcodec import _core as core

        self._source = source  # hold a reference to the source to prevent it from GC
        if isinstance(source, str):
            self._decoder = core.create_from_file(source, "exact")
        elif isinstance(source, bytes):
            self._decoder = core.create_from_bytes(source, "exact")
        else:
            raise TypeError(f"Unknown source type: {type(source)}.")
        assert dimension_order in ("NCHW", "NHWC")

        device_string = str(device)
        core.scan_all_streams_to_update_metadata(self._decoder)
        core.add_video_stream(
            self._decoder,
            dimension_order=dimension_order,
            device=device_string,
            num_threads=(1 if "cuda" in device_string else num_threads),
        )
        video_metadata = core.get_container_metadata(self._decoder)
        best_stream_index = video_metadata.best_video_stream_index
        assert best_stream_index is not None
        self.metadata = video_metadata.streams[best_stream_index]
        assert self.metadata.num_frames_from_content is not None
        self._num_frames = self.metadata.num_frames_from_content

    def __len__(self) -> int:
        return self._num_frames

    def __getitem__(self, key: int):
        from torchcodec import _core as core

        if key < 0:
            key += self._num_frames
        if key >= self._num_frames or key < 0:
            raise IndexError(
                f"Index {key} is out of bounds; length is {self._num_frames}"
            )
        frame_data, *_ = core.get_frame_at_index(
            self._decoder,
            frame_index=key,
        )
        return frame_data


class FIFOLock:
    """A lock that ensures FIFO ordering of lock acquisitions."""

    def __init__(self):
        self._lock = Lock()
        self._waiters = queue.Queue()
        self._condition = Condition()

    def acquire(self):
        ident = get_ident()
        with self._condition:
            self._waiters.put(ident)
            while self._waiters.queue[0] != ident or not self._lock.acquire(
                blocking=False
            ):
                self._condition.wait()
                # got the lock and it's our turn

    def release(self):
        with self._condition:
            self._lock.release()
            self._waiters.get()
            self._condition.notify_all()

    def __enter__(self):
        self.acquire()

    def __exit__(self, t, v, tb):
        self.release()


class AsyncVideoFileLoaderWithTorchCodec:
    """
    Loading frames from video files asynchronously without blocking session start.

    Unlike `AsyncVideoFileLoader`, this class uses PyTorch's offical TorchCodec library
    for video decoding, which is more efficient and supports more video formats.
    """

    def __init__(
        self,
        video_path,
        image_size,
        offload_video_to_cpu,
        img_mean,
        img_std,
        gpu_acceleration=True,
        gpu_device=None,
        use_rand_seek_in_loading=False,
    ):
        # Check and possibly infer the output device (and also get its GPU id when applicable)
        assert gpu_device is None or gpu_device.type == "cuda"
        gpu_id = (
            gpu_device.index
            if gpu_device is not None and gpu_device.index is not None
            else torch.cuda.current_device()
        )
        if offload_video_to_cpu:
            out_device = torch.device("cpu")
        else:
            out_device = torch.device("cuda") if gpu_device is None else gpu_device
        self.out_device = out_device
        self.gpu_acceleration = gpu_acceleration
        self.gpu_id = gpu_id
        self.image_size = image_size
        self.offload_video_to_cpu = offload_video_to_cpu
        if not isinstance(img_mean, torch.Tensor):
            img_mean = torch.tensor(img_mean, dtype=torch.float16)[:, None, None]
        self.img_mean = img_mean
        if not isinstance(img_std, torch.Tensor):
            img_std = torch.tensor(img_std, dtype=torch.float16)[:, None, None]
        self.img_std = img_std

        if gpu_acceleration:
            self.img_mean = self.img_mean.to(f"cuda:{self.gpu_id}")
            self.img_std = self.img_std.to(f"cuda:{self.gpu_id}")
            decoder_option = {"device": f"cuda:{self.gpu_id}"}
        else:
            self.img_mean = self.img_mean.cpu()
            self.img_std = self.img_std.cpu()
            decoder_option = {"num_threads": 1}  # use a single thread to save memory

        self.rank = int(os.environ.get("RANK", "0"))
        self.world_size = int(os.environ.get("WORLD_SIZE", "1"))
        self.async_reader = TorchCodecDecoder(video_path, **decoder_option)

        # `num_frames_from_content` is the true number of frames in the video content
        # from the scan operation (rather than from the metadata, which could be wrong)
        self.num_frames = self.async_reader.metadata.num_frames_from_content
        self.video_height = self.async_reader.metadata.height
        self.video_width = self.async_reader.metadata.width

        # items in `self._images` will be loaded asynchronously
        self.images_loaded = [False] * self.num_frames
        self.images = torch.zeros(
            self.num_frames,
            3,
            self.image_size,
            self.image_size,
            dtype=torch.float16,
            device=self.out_device,
        )
        # catch and raise any exceptions in the async loading thread
        self.exception = None
        self.use_rand_seek_in_loading = use_rand_seek_in_loading
        self.rand_seek_idx_queue = queue.Queue()
        # use a lock to avoid race condition between concurrent access to torchcodec
        # libs (which are not thread-safe); the lock is replaced with a nullcontext
        # when the video is fully loaded
        self.torchcodec_access_lock = FIFOLock()
        self._start_video_loading()

    def _load_one_frame(self, idx):
        frame_resized = self._transform_frame(self.async_reader[idx])
        return frame_resized

    @torch.inference_mode()
    def _start_video_loading(self):
        desc = f"frame loading (TorchCodec w/ {'GPU' if self.gpu_acceleration else 'CPU'}) [rank={RANK}]"
        pbar = tqdm(desc=desc, total=self.num_frames)
        self.num_loaded_frames = 0
        # load the first frame synchronously to cache it before the session is opened
        idx = self.num_loaded_frames
        self.images[idx] = self._load_one_frame(idx)
        self.images_loaded[idx] = True
        self.num_loaded_frames += 1
        pbar.update(n=1)
        self.all_frames_loaded = self.num_loaded_frames == self.num_frames

        # load the frames asynchronously without blocking the session start
        def _load_frames():
            finished = self.all_frames_loaded
            chunk_size = 16
            while not finished:
                # asynchronously load `chunk_size` frames each time we acquire the lock
                with self.torchcodec_access_lock, torch.inference_mode():
                    for _ in range(chunk_size):
                        try:
                            idx = self.num_loaded_frames
                            self.images[idx] = self._load_one_frame(idx)
                            self.images_loaded[idx] = True
                            self.num_loaded_frames += 1
                            pbar.update(n=1)
                            if self.num_loaded_frames >= self.num_frames:
                                finished = True
                                break
                        except Exception as e:
                            self.exception = e
                            raise

                    # also read the frame that is being randomly seeked to
                    while True:
                        try:
                            idx = self.rand_seek_idx_queue.get_nowait()
                            if not self.images_loaded[idx]:
                                self.images[idx] = self._load_one_frame(idx)
                                self.images_loaded[idx] = True
                        except queue.Empty:
                            break
                        except Exception as e:
                            self.exception = e
                            raise

            # finished -- check whether we have loaded the total number of frames
            if self.num_loaded_frames != self.num_frames:
                raise RuntimeError(
                    f"There are {self.num_frames} frames in the video, but only "
                    f"{self.num_loaded_frames} frames can be loaded successfully."
                )
            else:
                self.all_frames_loaded = True
                pbar.close()
                with self.torchcodec_access_lock:
                    import gc

                    # all frames have been loaded, so we can release the readers and free their memory
                    # also remove pbar and thread (which shouldn't be a part of session saving)
                    reader = self.async_reader
                    if reader is not None:
                        reader._source = None
                    self.async_reader = None
                    self.pbar = None
                    self.thread = None
                    self.rand_seek_idx_queue = None
                    gc.collect()
                # remove the lock (replace it with nullcontext) when the video is fully loaded
                self.torchcodec_access_lock = contextlib.nullcontext()

        self.thread = Thread(target=_load_frames, daemon=True)
        self.thread.start()

    def _transform_frame(self, frame):
        frame = frame.clone()  # make a copy to avoid modifying the original frame bytes
        frame = frame.float()  # convert to float32 before interpolation
        frame_resized = F.interpolate(
            frame[None, :],
            size=(self.image_size, self.image_size),
            mode="bicubic",
            align_corners=False,
        )[0]
        # float16 precision should be sufficient for image tensor storage
        frame_resized = frame_resized.half()  # uint8 -> float16
        frame_resized /= 255
        frame_resized -= self.img_mean
        frame_resized /= self.img_std
        if self.offload_video_to_cpu:
            frame_resized = frame_resized.cpu()
        elif frame_resized.device != self.out_device:
            frame_resized = frame_resized.to(device=self.out_device, non_blocking=True)
        return frame_resized

    def __getitem__(self, index):
        if self.exception is not None:
            raise RuntimeError("Failure in frame loading thread") from self.exception

        max_tries = 1200
        for _ in range(max_tries):
            # use a lock to avoid race condition between concurrent access to torchcodec
            # libs (which are not thread-safe); the lock is replaced with a nullcontext
            # when the video is fully loaded
            with self.torchcodec_access_lock:
                if self.images_loaded[index]:
                    return self.images[index]

                if self.use_rand_seek_in_loading:
                    # async loading hasn't reached this frame yet, so we load this frame individually
                    # (it will be loaded by in _load_frames thread and added to self.images[index])
                    self.rand_seek_idx_queue.put(index)

            time.sleep(0.1)

        raise RuntimeError(f"Failed to load frame {index} after {max_tries} tries")

    def __len__(self):
        return len(self.images)

    def __getstate__(self):
        """
        Remove a few attributes during pickling, so that this async video loader can be
        saved and loaded as a part of the model session.
        """
        # wait for async video loading to finish before pickling
        async_thread = self.thread
        if async_thread is not None:
            async_thread.join()
        # release a few objects that cannot be pickled
        reader = self.async_reader
        if reader is not None:
            reader._source = None
        self.async_reader = None
        self.pbar = None
        self.thread = None
        self.rand_seek_idx_queue = None
        self.torchcodec_access_lock = contextlib.nullcontext()
        return self.__dict__.copy()



================================================
FILE: sam3/model/maskformer_segmentation.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

import math
from typing import Dict, List, Optional

import torch
import torch.nn as nn
import torch.nn.functional as F
import torch.utils.checkpoint as checkpoint

from .model_misc import MLP


class LinearPresenceHead(nn.Sequential):
    def __init__(self, d_model):
        # a hack to make `LinearPresenceHead` compatible with old checkpoints
        super().__init__(nn.Identity(), nn.Identity(), nn.Linear(d_model, 1))

    def forward(self, hs, prompt, prompt_mask):
        return super().forward(hs)


class MaskPredictor(nn.Module):
    def __init__(self, hidden_dim, mask_dim):
        super().__init__()
        self.mask_embed = MLP(hidden_dim, hidden_dim, mask_dim, 3)

    def forward(self, obj_queries, pixel_embed):
        if len(obj_queries.shape) == 3:
            if pixel_embed.ndim == 3:
                # batch size was omitted
                mask_preds = torch.einsum(
                    "bqc,chw->bqhw", self.mask_embed(obj_queries), pixel_embed
                )
            else:
                mask_preds = torch.einsum(
                    "bqc,bchw->bqhw", self.mask_embed(obj_queries), pixel_embed
                )
        else:
            # Assumed to have aux masks
            if pixel_embed.ndim == 3:
                # batch size was omitted
                mask_preds = torch.einsum(
                    "lbqc,chw->lbqhw", self.mask_embed(obj_queries), pixel_embed
                )
            else:
                mask_preds = torch.einsum(
                    "lbqc,bchw->lbqhw", self.mask_embed(obj_queries), pixel_embed
                )

        return mask_preds


class SegmentationHead(nn.Module):
    def __init__(
        self,
        hidden_dim,
        upsampling_stages,
        use_encoder_inputs=False,
        aux_masks=False,
        no_dec=False,
        pixel_decoder=None,
        act_ckpt=False,
        shared_conv=False,
        compile_mode_pixel_decoder=None,
    ):
        super().__init__()
        self.use_encoder_inputs = use_encoder_inputs
        self.aux_masks = aux_masks
        if pixel_decoder is not None:
            self.pixel_decoder = pixel_decoder
        else:
            self.pixel_decoder = PixelDecoder(
                hidden_dim,
                upsampling_stages,
                shared_conv=shared_conv,
                compile_mode=compile_mode_pixel_decoder,
            )
        self.no_dec = no_dec
        if no_dec:
            self.mask_predictor = nn.Conv2d(
                hidden_dim, 1, kernel_size=3, stride=1, padding=1
            )
        else:
            self.mask_predictor = MaskPredictor(hidden_dim, mask_dim=hidden_dim)

        self.act_ckpt = act_ckpt

        # used to update the output dictionary
        self.instance_keys = ["pred_masks"]

    @property
    def device(self):
        self._device = getattr(self, "_device", None) or next(self.parameters()).device
        return self._device

    def to(self, *args, **kwargs):
        # clear cached _device in case the model is moved to a different device
        self._device = None
        return super().to(*args, **kwargs)

    def _embed_pixels(
        self,
        backbone_feats: List[torch.Tensor],
        image_ids,
        encoder_hidden_states,
    ) -> torch.Tensor:
        # Unwrap NestedTensors to plain tensors if needed (multiplex path)
        from sam3.model.data_misc import NestedTensor

        def _unwrap(x):
            return x.tensors if isinstance(x, NestedTensor) else x

        feature_device = backbone_feats[0].device  # features could be on CPU
        model_device = self.device
        image_ids_ = image_ids.to(feature_device)
        if self.use_encoder_inputs:
            if backbone_feats[0].shape[0] > 1:
                # For bs > 1, we construct the per query backbone features
                backbone_visual_feats = []
                for feat in backbone_feats:
                    # Copy the img features per query (pixel decoder won't share img feats)
                    backbone_visual_feats.append(
                        _unwrap(feat)[image_ids_, ...].to(model_device)
                    )
            else:
                # Bs=1, we rely on broadcasting for query-based processing
                backbone_visual_feats = [
                    _unwrap(bb_feat).clone() for bb_feat in backbone_feats
                ]
            # Extract visual embeddings
            encoder_hidden_states = encoder_hidden_states.permute(1, 2, 0)
            spatial_dim = math.prod(backbone_feats[-1].shape[-2:])
            encoder_visual_embed = encoder_hidden_states[..., :spatial_dim].reshape(
                -1, *backbone_feats[-1].shape[1:]
            )

            backbone_visual_feats[-1] = encoder_visual_embed
            if self.act_ckpt:
                pixel_embed = checkpoint.checkpoint(
                    self.pixel_decoder, backbone_visual_feats, use_reentrant=False
                )
            else:
                pixel_embed = self.pixel_decoder(backbone_visual_feats)
        else:
            backbone_feats = [_unwrap(x).to(model_device) for x in backbone_feats]
            pixel_embed = self.pixel_decoder(backbone_feats)
            if pixel_embed.shape[0] == 1:
                # For batch_size=1 training, we can avoid the indexing to save memory
                pixel_embed = pixel_embed.squeeze(0)
            else:
                pixel_embed = pixel_embed[image_ids, ...]
        return pixel_embed

    def forward(
        self,
        backbone_feats: List[torch.Tensor],
        obj_queries: torch.Tensor,
        image_ids,
        encoder_hidden_states: Optional[torch.Tensor] = None,
        **kwargs,
    ) -> Dict[str, torch.Tensor]:
        if self.use_encoder_inputs:
            assert encoder_hidden_states is not None

        pixel_embed = self._embed_pixels(
            backbone_feats=backbone_feats,
            image_ids=image_ids,
            encoder_hidden_states=encoder_hidden_states,
        )

        if self.no_dec:
            mask_pred = self.mask_predictor(pixel_embed)
        elif self.aux_masks:
            mask_pred = self.mask_predictor(obj_queries, pixel_embed)
        else:
            mask_pred = self.mask_predictor(obj_queries[-1], pixel_embed)

        return {"pred_masks": mask_pred}


class PixelDecoder(nn.Module):
    def __init__(
        self,
        hidden_dim,
        num_upsampling_stages,
        interpolation_mode="nearest",
        shared_conv=False,
        compile_mode=None,
    ):
        super().__init__()
        self.hidden_dim = hidden_dim
        self.num_upsampling_stages = num_upsampling_stages
        self.interpolation_mode = interpolation_mode
        conv_layers = []
        norms = []
        num_convs = 1 if shared_conv else num_upsampling_stages
        for _ in range(num_convs):
            conv_layers.append(nn.Conv2d(self.hidden_dim, self.hidden_dim, 3, 1, 1))
            norms.append(nn.GroupNorm(8, self.hidden_dim))

        self.conv_layers = nn.ModuleList(conv_layers)
        self.norms = nn.ModuleList(norms)
        self.shared_conv = shared_conv
        self.out_dim = self.conv_layers[-1].out_channels
        if compile_mode is not None:
            self.forward = torch.compile(
                self.forward, mode=compile_mode, dynamic=True, fullgraph=True
            )
            # Needed to make checkpointing happy. But we don't know if the module is checkpointed, so we disable it by default.
            torch._dynamo.config.optimize_ddp = False

    def forward(self, backbone_feats: List[torch.Tensor]):
        # Assumes backbone features are already projected (C == hidden dim)

        prev_fpn = backbone_feats[-1]
        fpn_feats = backbone_feats[:-1]
        for layer_idx, bb_feat in enumerate(fpn_feats[::-1]):
            curr_fpn = bb_feat
            prev_fpn = curr_fpn + F.interpolate(
                prev_fpn, size=curr_fpn.shape[-2:], mode=self.interpolation_mode
            )
            if self.shared_conv:
                # only one conv layer
                layer_idx = 0
            prev_fpn = self.conv_layers[layer_idx](prev_fpn)
            prev_fpn = F.relu(self.norms[layer_idx](prev_fpn))

        return prev_fpn


class UniversalSegmentationHead(SegmentationHead):
    """This module handles semantic+instance segmentation"""

    def __init__(
        self,
        hidden_dim,
        upsampling_stages,
        pixel_decoder,
        aux_masks=False,
        no_dec=False,
        act_ckpt=False,
        presence_head: bool = False,
        dot_product_scorer=None,
        cross_attend_prompt=None,
    ):
        super().__init__(
            hidden_dim=hidden_dim,
            upsampling_stages=upsampling_stages,
            use_encoder_inputs=True,
            aux_masks=aux_masks,
            no_dec=no_dec,
            pixel_decoder=pixel_decoder,
            act_ckpt=act_ckpt,
        )
        self.d_model = hidden_dim

        if dot_product_scorer is not None:
            assert presence_head, (
                "Specifying a dot product scorer without a presence head is likely a mistake"
            )

        self.presence_head = None
        if presence_head:
            self.presence_head = (
                dot_product_scorer
                if dot_product_scorer is not None
                else LinearPresenceHead(self.d_model)
            )

        self.cross_attend_prompt = cross_attend_prompt
        if self.cross_attend_prompt is not None:
            self.cross_attn_norm = nn.LayerNorm(self.d_model)

        self.semantic_seg_head = nn.Conv2d(self.pixel_decoder.out_dim, 1, kernel_size=1)
        self.instance_seg_head = nn.Conv2d(
            self.pixel_decoder.out_dim, self.d_model, kernel_size=1
        )

    def forward(
        self,
        backbone_feats: List[torch.Tensor],
        obj_queries: torch.Tensor,
        image_ids,
        encoder_hidden_states: Optional[torch.Tensor] = None,
        prompt: Optional[torch.Tensor] = None,
        prompt_mask: Optional[torch.Tensor] = None,
        **kwargs,
    ) -> Dict[str, Optional[torch.Tensor]]:
        assert encoder_hidden_states is not None
        bs = encoder_hidden_states.shape[1]

        if self.cross_attend_prompt is not None:
            tgt2 = self.cross_attn_norm(encoder_hidden_states)
            tgt2 = self.cross_attend_prompt(
                query=tgt2,
                key=prompt,
                value=prompt,
                key_padding_mask=prompt_mask,
            )[0]
            encoder_hidden_states = tgt2 + encoder_hidden_states

        presence_logit = None
        if self.presence_head is not None:
            pooled_enc = encoder_hidden_states.mean(0)
            presence_logit = (
                self.presence_head(
                    pooled_enc.view(1, bs, 1, self.d_model),
                    prompt=prompt,
                    prompt_mask=prompt_mask,
                )
                .squeeze(0)
                .squeeze(1)
            )

        pixel_embed = self._embed_pixels(
            backbone_feats=backbone_feats,
            image_ids=image_ids,
            encoder_hidden_states=encoder_hidden_states,
        )

        instance_embeds = self.instance_seg_head(pixel_embed)

        if self.no_dec:
            mask_pred = self.mask_predictor(instance_embeds)
        elif self.aux_masks:
            mask_pred = self.mask_predictor(obj_queries, instance_embeds)
        else:
            mask_pred = self.mask_predictor(obj_queries[-1], instance_embeds)

        return {
            "pred_masks": mask_pred,
            "semantic_seg": self.semantic_seg_head(pixel_embed),
            "presence_logit": presence_logit,
        }



================================================
FILE: sam3/model/memory.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

import math
from typing import Tuple

import torch
import torch.nn as nn
import torch.nn.functional as F

try:
    from timm.layers import DropPath
except ModuleNotFoundError:
    # compatibility for older timm versions
    from timm.models.layers import DropPath

from .model_misc import get_clones, LayerNorm2d


class SimpleMaskDownSampler(nn.Module):
    """
    Progressively downsample a mask by total_stride, each time by stride.
    Note that LayerNorm is applied per *token*, like in ViT.

    With each downsample (by a factor stride**2), channel capacity increases by the same factor.
    In the end, we linearly project to embed_dim channels.
    """

    def __init__(
        self,
        embed_dim=256,
        kernel_size=4,
        stride=4,
        padding=0,
        total_stride=16,
        activation=nn.GELU,
        # Option to interpolate the input mask first before downsampling using convs. In that case, the total_stride is assumed to be after interpolation.
        # If set to input resolution or None, we don't interpolate. We default to None to be safe (for older configs or if not explicitly set)
        interpol_size=None,
        # options for incorporating multiplex memory encoding
        multiplex_count: int = 1,
        starting_out_chan: int = 1,
        input_channel_multiplier: int = 1,
    ):
        super().__init__()
        num_layers = int(math.log2(total_stride) // math.log2(stride))
        multiplex_count = multiplex_count * input_channel_multiplier
        assert stride**num_layers == total_stride
        self.encoder = nn.Sequential()
        mask_in_chans, mask_out_chans = multiplex_count, starting_out_chan
        for _ in range(num_layers):
            mask_out_chans = mask_out_chans * (stride**2)
            self.encoder.append(
                nn.Conv2d(
                    mask_in_chans,
                    mask_out_chans,
                    kernel_size=kernel_size,
                    stride=stride,
                    padding=padding,
                )
            )
            self.encoder.append(LayerNorm2d(mask_out_chans))
            self.encoder.append(activation())
            mask_in_chans = mask_out_chans

        self.encoder.append(nn.Conv2d(mask_out_chans, embed_dim, kernel_size=1))
        self.multiplex_count = multiplex_count
        self.interpol_size = interpol_size
        if self.interpol_size is not None:
            assert isinstance(self.interpol_size, (list, tuple)), (
                f"Unsupported type {type(self.interpol_size)}. Should be a list or tuple."
            )
            self.interpol_size = list(interpol_size)
            assert len(self.interpol_size) == 2

    def forward(self, x: torch.Tensor):
        if self.interpol_size is not None and self.interpol_size != list(x.shape[-2:]):
            x = F.interpolate(
                x.float(),
                size=self.interpol_size,
                align_corners=False,
                mode="bilinear",
                antialias=True,
            )
        return self.encoder(x)


# Lightly adapted from ConvNext (https://github.com/facebookresearch/ConvNeXt)
class CXBlock(nn.Module):
    r"""ConvNeXt Block. There are two equivalent implementations:
    (1) DwConv -> LayerNorm (channels_first) -> 1x1 Conv -> GELU -> 1x1 Conv; all in (N, C, H, W)
    (2) DwConv -> Permute to (N, H, W, C); LayerNorm (channels_last) -> Linear -> GELU -> Linear; Permute back
    We use (2) as we find it slightly faster in PyTorch

    Args:
        dim (int): Number of input channels.
        drop_path (float): Stochastic depth rate. Default: 0.0
        layer_scale_init_value (float): Init value for Layer Scale. Default: 1e-6.
    """

    def __init__(
        self,
        dim,
        kernel_size=7,
        padding=3,
        drop_path=0.0,
        layer_scale_init_value=1e-6,
        use_dwconv=True,
    ):
        super().__init__()
        self.dwconv = nn.Conv2d(
            dim,
            dim,
            kernel_size=kernel_size,
            padding=padding,
            groups=dim if use_dwconv else 1,
        )  # depthwise conv
        self.norm = LayerNorm2d(dim, eps=1e-6)
        self.pwconv1 = nn.Linear(
            dim, 4 * dim
        )  # pointwise/1x1 convs, implemented with linear layers
        self.act = nn.GELU()
        self.pwconv2 = nn.Linear(4 * dim, dim)
        self.gamma = (
            nn.Parameter(layer_scale_init_value * torch.ones((dim)), requires_grad=True)
            if layer_scale_init_value > 0
            else None
        )
        self.drop_path = DropPath(drop_path) if drop_path > 0.0 else nn.Identity()

    def forward(self, x):
        input = x
        x = self.dwconv(x)
        x = self.norm(x)
        x = x.permute(0, 2, 3, 1)  # (N, C, H, W) -> (N, H, W, C)
        x = self.pwconv1(x)
        x = self.act(x)
        x = self.pwconv2(x)
        if self.gamma is not None:
            x = self.gamma * x
        x = x.permute(0, 3, 1, 2)  # (N, H, W, C) -> (N, C, H, W)

        x = input + self.drop_path(x)
        return x


class SimpleFuser(nn.Module):
    def __init__(self, layer, num_layers, dim=None, input_projection=False):
        super().__init__()
        self.proj = nn.Identity()
        self.layers = get_clones(layer, num_layers)

        if input_projection:
            assert dim is not None
            self.proj = nn.Conv2d(dim, dim, kernel_size=1)

    def forward(self, x):
        # normally x: (N, C, H, W)
        x = self.proj(x)
        for layer in self.layers:
            x = layer(x)
        return x


class SimpleMaskEncoder(nn.Module):
    def __init__(
        self,
        out_dim,
        mask_downsampler,
        fuser,
        position_encoding,
        in_dim=256,  # in_dim of pix_feats
    ):
        super().__init__()

        self.mask_downsampler = mask_downsampler

        self.pix_feat_proj = nn.Conv2d(in_dim, in_dim, kernel_size=1)
        self.fuser = fuser
        self.position_encoding = position_encoding
        self.out_proj = nn.Identity()
        if out_dim != in_dim:
            self.out_proj = nn.Conv2d(in_dim, out_dim, kernel_size=1)

    def forward(
        self,
        pix_feat: torch.Tensor,
        masks: torch.Tensor,
        skip_mask_sigmoid: bool = False,
    ) -> Tuple[torch.Tensor, torch.Tensor]:
        ## Process masks
        # sigmoid, so that less domain shift from gt masks which are bool
        if not skip_mask_sigmoid:
            masks = F.sigmoid(masks)
        masks = self.mask_downsampler(masks)

        ## Fuse pix_feats and downsampled masks
        # in case the visual features are on CPU, cast them to CUDA
        pix_feat = pix_feat.to(masks.device)

        x = self.pix_feat_proj(pix_feat)
        x = x + masks
        x = self.fuser(x)
        x = self.out_proj(x)

        pos = self.position_encoding(x).to(x.dtype)

        return {"vision_features": x, "vision_pos_enc": [pos]}



================================================
FILE: sam3/model/model_misc.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

"""Various utility models"""

import copy
import math
import warnings
import weakref
from collections.abc import Iterator
from contextlib import AbstractContextManager
from enum import auto, Enum
from typing import Dict, List, Optional, Tuple, Union

import numpy as np
import torch
import torch.nn.functional as F
from torch import nn, Tensor
from torch.overrides import handle_torch_function, has_torch_function
from typing_extensions import override

try:
    import xformers
except ImportError:
    xformers = None


def inverse_sigmoid(x, eps=1e-3):
    """
    The inverse function for sigmoid activation function.
    Note: It might face numberical issues with fp16 small eps.
    """
    x = x.clamp(min=0, max=1)
    x1 = x.clamp(min=eps)
    x2 = (1 - x).clamp(min=eps)
    return torch.log(x1 / x2)


def get_sdpa_settings():
    if torch.cuda.is_available():
        old_gpu = torch.cuda.get_device_properties(0).major < 7
        # only use Flash Attention on Ampere (8.0) or newer GPUs
        use_flash_attn = torch.cuda.get_device_properties(0).major >= 8
        if not use_flash_attn:
            warnings.warn(
                "Flash Attention is disabled as it requires a GPU with Ampere (8.0) CUDA capability.",
                category=UserWarning,
                stacklevel=2,
            )
        # keep math kernel for PyTorch versions before 2.2 (Flash Attention v2 is only
        # available on PyTorch 2.2+, while Flash Attention v1 cannot handle all cases)
        pytorch_version = tuple(int(v) for v in torch.__version__.split(".")[:2])
        if pytorch_version < (2, 2):
            warnings.warn(
                f"You are using PyTorch {torch.__version__} without Flash Attention v2 support. "
                "Consider upgrading to PyTorch 2.2+ for Flash Attention v2 (which could be faster).",
                category=UserWarning,
                stacklevel=2,
            )
        math_kernel_on = pytorch_version < (2, 2) or not use_flash_attn
    else:
        old_gpu = True
        use_flash_attn = False
        math_kernel_on = True

    return old_gpu, use_flash_attn, math_kernel_on


OLD_GPU, USE_FLASH_ATTN, MATH_KERNEL_ON = get_sdpa_settings()


class AttentionType:
    """Type of attention"""

    # Simple dot product attention
    Vanilla = "Vanilla"

    # Efficient attention from xformers
    Xformer = "Xformer"

    # Sparse attention
    Sparse = "Sparse"

    # Deformable attention (not compatible with text)
    Deformable = "Deformable"


def multi_head_attention_forward(
    query: Tensor,
    key: Tensor,
    value: Tensor,
    embed_dim_to_check: int,
    num_heads: int,
    in_proj_weight: Optional[Tensor],
    in_proj_bias: Optional[Tensor],
    bias_k: Optional[Tensor],
    bias_v: Optional[Tensor],
    add_zero_attn: bool,
    dropout_p: float,
    out_proj_weight: Tensor,
    out_proj_bias: Optional[Tensor],
    training: bool = True,
    key_padding_mask: Optional[Tensor] = None,
    need_weights: bool = True,
    attn_mask: Optional[Tensor] = None,
    use_separate_proj_weight: bool = False,
    q_proj_weight: Optional[Tensor] = None,
    k_proj_weight: Optional[Tensor] = None,
    v_proj_weight: Optional[Tensor] = None,
    static_k: Optional[Tensor] = None,
    static_v: Optional[Tensor] = None,
    average_attn_weights: bool = True,
    is_causal: bool = False,
    attn_type: AttentionType = AttentionType.Vanilla,
    attn_sparsity: float = 0.0,
    attn_bias: Optional[Tensor] = None,
    use_fa3: bool = False,
) -> Tuple[Tensor, Optional[Tensor]]:
    tens_ops = (
        query,
        key,
        value,
        in_proj_weight,
        in_proj_bias,
        bias_k,
        bias_v,
        out_proj_weight,
        out_proj_bias,
    )
    if has_torch_function(tens_ops):
        return handle_torch_function(
            multi_head_attention_forward,
            tens_ops,
            query,
            key,
            value,
            embed_dim_to_check,
            num_heads,
            in_proj_weight,
            in_proj_bias,
            bias_k,
            bias_v,
            add_zero_attn,
            dropout_p,
            out_proj_weight,
            out_proj_bias,
            training=training,
            key_padding_mask=key_padding_mask,
            need_weights=need_weights,
            attn_mask=attn_mask,
            is_causal=is_causal,
            use_separate_proj_weight=use_separate_proj_weight,
            q_proj_weight=q_proj_weight,
            k_proj_weight=k_proj_weight,
            v_proj_weight=v_proj_weight,
            static_k=static_k,
            static_v=static_v,
            average_attn_weights=average_attn_weights,
            use_fa3=use_fa3,
        )

    is_batched = True

    if is_causal:
        raise NotImplementedError("is_causal is not supported in this implem")
        attn_mask = None

    if not is_batched:
        query = query.unsqueeze(1)
        key = key.unsqueeze(1)
        value = value.unsqueeze(1)
        if key_padding_mask is not None:
            key_padding_mask = key_padding_mask.unsqueeze(0)

    # set up shape vars
    tgt_len, bsz, embed_dim = query.shape
    src_len, _, _ = key.shape
    if key_padding_mask is not None:
        _kpm_dtype = key_padding_mask.dtype
        if _kpm_dtype != torch.bool and not torch.is_floating_point(key_padding_mask):
            raise AssertionError(
                "only bool and floating types of key_padding_mask are supported"
            )
    assert embed_dim == embed_dim_to_check, (
        f"was expecting embedding dimension of {embed_dim_to_check}, but got {embed_dim}"
    )
    if isinstance(embed_dim, torch.Tensor):
        head_dim = embed_dim.div(num_heads, rounding_mode="trunc")
    else:
        head_dim = embed_dim // num_heads
    assert head_dim * num_heads == embed_dim, (
        f"embed_dim {embed_dim} not divisible by num_heads {num_heads}"
    )
    if use_separate_proj_weight:
        assert key.shape[:2] == value.shape[:2], (
            f"key's sequence and batch dims {key.shape[:2]} do not match value's {value.shape[:2]}"
        )
    else:
        assert key.shape == value.shape, (
            f"key shape {key.shape} does not match value shape {value.shape}"
        )

    #
    # compute in-projection
    #
    if not use_separate_proj_weight:
        assert in_proj_weight is not None, (
            "use_separate_proj_weight is False but in_proj_weight is None"
        )
        q, k, v = F._in_projection_packed(
            query, key, value, in_proj_weight, in_proj_bias
        )
    else:
        assert q_proj_weight is not None, (
            "use_separate_proj_weight is True but q_proj_weight is None"
        )
        assert k_proj_weight is not None, (
            "use_separate_proj_weight is True but k_proj_weight is None"
        )
        assert v_proj_weight is not None, (
            "use_separate_proj_weight is True but v_proj_weight is None"
        )
        if in_proj_bias is None:
            b_q = b_k = b_v = None
        else:
            b_q, b_k, b_v = in_proj_bias.chunk(3)
        q, k, v = F._in_projection(
            query,
            key,
            value,
            q_proj_weight,
            k_proj_weight,
            v_proj_weight,
            b_q,
            b_k,
            b_v,
        )

    # prep attention mask
    if attn_mask is not None:
        if attn_mask.dtype == torch.uint8:
            warnings.warn(
                "Byte tensor for attn_mask in nn.MultiheadAttention is deprecated. Use bool tensor instead."
            )
            attn_mask = attn_mask.to(torch.bool)
        else:
            assert attn_mask.is_floating_point() or attn_mask.dtype == torch.bool, (
                f"Only float, byte, and bool types are supported for attn_mask, not {attn_mask.dtype}"
            )
        # ensure attn_mask's dim is 3
        if attn_mask.dim() == 2:
            correct_2d_size = (tgt_len, src_len)
            if attn_mask.shape != correct_2d_size:
                raise RuntimeError(
                    f"The shape of the 2D attn_mask is {attn_mask.shape}, but should be {correct_2d_size}."
                )
            attn_mask = attn_mask.unsqueeze(0)
        elif attn_mask.dim() == 3:
            correct_3d_size = (bsz * num_heads, tgt_len, src_len)
            if attn_mask.shape != correct_3d_size:
                raise RuntimeError(
                    f"The shape of the 3D attn_mask is {attn_mask.shape}, but should be {correct_3d_size}."
                )
        else:
            raise RuntimeError(
                f"attn_mask's dimension {attn_mask.dim()} is not supported"
            )

    # add bias along batch dimension (currently second)
    if bias_k is not None and bias_v is not None:
        assert static_k is None, "bias cannot be added to static key."
        assert static_v is None, "bias cannot be added to static value."
        k = torch.cat([k, bias_k.repeat(1, bsz, 1)])
        v = torch.cat([v, bias_v.repeat(1, bsz, 1)])
        if attn_mask is not None:
            attn_mask = F.pad(attn_mask, (0, 1))
        if key_padding_mask is not None:
            key_padding_mask = F.pad(key_padding_mask, (0, 1))
    else:
        assert bias_k is None
        assert bias_v is None

    #
    # reshape q, k, v for multihead attention and make em batch first
    #
    q = q.contiguous().view(tgt_len, bsz * num_heads, head_dim).transpose(0, 1)
    if static_k is None:
        k = k.contiguous().view(k.shape[0], bsz * num_heads, head_dim).transpose(0, 1)
    else:
        assert static_k.size(0) == bsz * num_heads, (
            f"expecting static_k.size(0) of {bsz * num_heads}, but got {static_k.size(0)}"
        )
        assert static_k.size(2) == head_dim, (
            f"expecting static_k.size(2) of {head_dim}, but got {static_k.size(2)}"
        )
        k = static_k
    if static_v is None:
        v = v.contiguous().view(v.shape[0], bsz * num_heads, head_dim).transpose(0, 1)
    else:
        assert static_v.size(0) == bsz * num_heads, (
            f"expecting static_v.size(0) of {bsz * num_heads}, but got {static_v.size(0)}"
        )
        assert static_v.size(2) == head_dim, (
            f"expecting static_v.size(2) of {head_dim}, but got {static_v.size(2)}"
        )
        v = static_v

    # add zero attention along batch dimension (now first)
    if add_zero_attn:
        zero_attn_shape = (bsz * num_heads, 1, head_dim)
        k = torch.cat(
            [k, torch.zeros(zero_attn_shape, dtype=k.dtype, device=k.device)], dim=1
        )
        v = torch.cat(
            [v, torch.zeros(zero_attn_shape, dtype=v.dtype, device=v.device)], dim=1
        )
        if attn_mask is not None:
            attn_mask = F.pad(attn_mask, (0, 1))
        if key_padding_mask is not None:
            key_padding_mask = F.pad(key_padding_mask, (0, 1))

    # update source sequence length after adjustments
    src_len = k.size(1)

    # merge key padding and attention masks
    if key_padding_mask is not None:
        assert key_padding_mask.shape == (
            bsz,
            src_len,
        ), (
            f"expecting key_padding_mask shape of {(bsz, src_len)}, but got {key_padding_mask.shape}"
        )
        key_padding_mask = (
            key_padding_mask.view(bsz, 1, 1, src_len)
            .expand(-1, num_heads, -1, -1)
            .reshape(bsz * num_heads, 1, src_len)
        )
        if attn_mask is None:
            attn_mask = key_padding_mask
        elif attn_mask.dtype == torch.bool:
            attn_mask = attn_mask.logical_or(key_padding_mask)
        else:
            attn_mask = attn_mask.masked_fill(key_padding_mask, float("-inf"))

    # convert mask to float
    if attn_mask is not None and attn_mask.dtype == torch.bool:
        new_attn_mask = torch.zeros_like(attn_mask, dtype=q.dtype)
        new_attn_mask.masked_fill_(attn_mask, float("-inf"))
        attn_mask = new_attn_mask

    # adjust dropout probability
    if not training:
        dropout_p = 0.0

    #
    # (deep breath) calculate attention and out projection
    #

    if attn_mask is not None:
        if attn_mask.size(0) == 1:
            attn_mask = attn_mask.unsqueeze(0)
        else:
            attn_mask = attn_mask.view(bsz, num_heads, -1, src_len)

    if attn_bias is not None:
        assert attn_bias.shape == (
            bsz,
            num_heads,
            tgt_len,
            src_len,
        ), (
            f"expecting attn_bias shape of {(bsz, num_heads, tgt_len, src_len)}, but got {attn_bias.shape}"
        )
        if attn_mask is None:
            attn_mask = attn_bias
        else:
            attn_mask = attn_mask + attn_bias

    q = q.view(bsz, num_heads, tgt_len, head_dim)
    k = k.view(bsz, num_heads, src_len, head_dim)
    v = v.view(bsz, num_heads, src_len, head_dim)

    if attn_type == AttentionType.Vanilla:
        if attn_mask is None and not is_causal and use_fa3:
            from sam3.perflib.fa3 import flash_attn_func

            assert dropout_p == 0.0
            attn_output = flash_attn_func(
                q.transpose(1, 2), k.transpose(1, 2), v.transpose(1, 2)
            ).transpose(1, 2)
        else:
            torch.backends.cuda.enable_flash_sdp(True)
            torch.backends.cuda.enable_math_sdp(True)
            torch.backends.cuda.enable_mem_efficient_sdp(True)

            attn_output = F.scaled_dot_product_attention(
                q, k, v, attn_mask, dropout_p, is_causal
            )

        attn_output = (
            attn_output.permute(2, 0, 1, 3).contiguous().view(bsz * tgt_len, embed_dim)
        )
    elif attn_type == AttentionType.Xformer:
        attn_output_weights = None
        assert not need_weights, "need_weights is not supported in efficient mode"
        attn_output = xformers.ops.memory_efficient_attention(
            q.transpose(1, 2),
            k.transpose(1, 2),
            v.transpose(1, 2),
            attn_bias=attn_mask,
            p=dropout_p,
        )
        attn_output = attn_output.permute(1, 0, 2, 3).reshape(bsz * tgt_len, embed_dim)
    elif attn_type == AttentionType.Sparse:
        attn_output_weights = None
        assert not need_weights, "need_weights is not supported in efficient mode"
        # Need to collapse heads and batch dimensions
        q = q.reshape(bsz * num_heads, tgt_len, head_dim).contiguous()
        k = k.reshape(bsz * num_heads, src_len, head_dim).contiguous()
        v = v.reshape(bsz * num_heads, src_len, head_dim).contiguous()
        row_offsets, column_indices = xformers.ops.find_locations_new(
            q, k, attn_sparsity, True
        )
        attn_output = xformers.ops.sparse_memory_efficient_attention(
            q, k, v, row_offsets, column_indices, attn_bias=attn_mask
        ).reshape(bsz, num_heads, tgt_len, head_dim)
        attn_output = attn_output.permute(2, 0, 1, 3).reshape(bsz * tgt_len, embed_dim)
    else:
        raise ValueError(f"Unsupported attention type {attn_type}")

    attn_output = F.linear(attn_output, out_proj_weight, out_proj_bias)
    attn_output = attn_output.view(tgt_len, bsz, attn_output.size(1))

    if need_weights:
        attn_output_weights = (q * head_dim**-0.5) @ k.transpose(-2, -1)
        attn_output_weights = attn_output_weights.softmax(dim=-1)
        attn_output_weights = attn_output_weights.view(bsz, num_heads, tgt_len, src_len)
        if average_attn_weights:
            attn_output_weights = attn_output_weights.sum(dim=1) / num_heads

        if not is_batched:
            attn_output = attn_output.squeeze(1)
            attn_output_weights = attn_output_weights.squeeze(0)
        return attn_output, attn_output_weights
    else:
        attn_output_weights = None
        if not is_batched:
            attn_output = attn_output.squeeze(1)
        return attn_output, None


class MultiheadAttention(nn.Module):
    __constants__ = ["batch_first"]
    bias_k: Optional[torch.Tensor]
    bias_v: Optional[torch.Tensor]

    def __init__(
        self,
        embed_dim,
        num_heads,
        dropout=0.0,
        bias=True,
        add_bias_kv=False,
        add_zero_attn=False,
        kdim=None,
        vdim=None,
        batch_first=False,
        device=None,
        dtype=None,
        attn_type: AttentionType = AttentionType.Vanilla,
        sparsity: float = 0.0,
        use_act_checkpoint: bool = False,
        use_fa3: bool = False,
    ) -> None:
        factory_kwargs = {"device": device, "dtype": dtype}
        super(MultiheadAttention, self).__init__()
        self.embed_dim = embed_dim
        self.kdim = kdim if kdim is not None else embed_dim
        self.vdim = vdim if vdim is not None else embed_dim
        self._qkv_same_embed_dim = self.kdim == embed_dim and self.vdim == embed_dim

        self.num_heads = num_heads
        self.dropout = dropout
        self.batch_first = batch_first
        self.head_dim = embed_dim // num_heads
        self.use_act_checkpoint = use_act_checkpoint
        assert self.head_dim * num_heads == self.embed_dim, (
            "embed_dim must be divisible by num_heads"
        )

        assert attn_type == AttentionType.Sparse or sparsity == 0.0, (
            "sparsity is only supported for sparse attention"
        )

        if not self._qkv_same_embed_dim:
            self.q_proj_weight = nn.Parameter(
                torch.empty((embed_dim, embed_dim), **factory_kwargs)
            )
            self.k_proj_weight = nn.Parameter(
                torch.empty((embed_dim, self.kdim), **factory_kwargs)
            )
            self.v_proj_weight = nn.Parameter(
                torch.empty((embed_dim, self.vdim), **factory_kwargs)
            )
            self.register_parameter("in_proj_weight", None)
        else:
            self.in_proj_weight = nn.Parameter(
                torch.empty((3 * embed_dim, embed_dim), **factory_kwargs)
            )
            self.register_parameter("q_proj_weight", None)
            self.register_parameter("k_proj_weight", None)
            self.register_parameter("v_proj_weight", None)

        if bias:
            self.in_proj_bias = nn.Parameter(
                torch.empty(3 * embed_dim, **factory_kwargs)
            )
        else:
            self.register_parameter("in_proj_bias", None)
        self.out_proj = nn.modules.linear.NonDynamicallyQuantizableLinear(
            embed_dim, embed_dim, bias=bias, **factory_kwargs
        )

        if add_bias_kv:
            self.bias_k = nn.Parameter(torch.empty((1, 1, embed_dim), **factory_kwargs))
            self.bias_v = nn.Parameter(torch.empty((1, 1, embed_dim), **factory_kwargs))
        else:
            self.bias_k = self.bias_v = None

        self.add_zero_attn = add_zero_attn

        self.attn_type = attn_type
        self.sparsity = sparsity
        self.use_fa3 = use_fa3

        self._reset_parameters()

    def _reset_parameters(self):
        if self._qkv_same_embed_dim:
            nn.init.xavier_uniform_(self.in_proj_weight)
        else:
            nn.init.xavier_uniform_(self.q_proj_weight)
            nn.init.xavier_uniform_(self.k_proj_weight)
            nn.init.xavier_uniform_(self.v_proj_weight)

        if self.in_proj_bias is not None:
            nn.init.constant_(self.in_proj_bias, 0.0)
            nn.init.constant_(self.out_proj.bias, 0.0)
        if self.bias_k is not None:
            nn.init.xavier_normal_(self.bias_k)
        if self.bias_v is not None:
            nn.init.xavier_normal_(self.bias_v)

    def __setstate__(self, state):
        if "_qkv_same_embed_dim" not in state:
            state["_qkv_same_embed_dim"] = True

        super(MultiheadAttention, self).__setstate__(state)

    def forward(
        self,
        query: Tensor,
        key: Tensor,
        value: Tensor,
        key_padding_mask: Optional[Tensor] = None,
        need_weights: bool = False,
        attn_mask: Optional[Tensor] = None,
        average_attn_weights: bool = True,
        attn_bias: Optional[Tensor] = None,
    ) -> Tuple[Tensor, Optional[Tensor]]:
        is_batched = query.dim() == 3
        if key_padding_mask is not None:
            _kpm_dtype = key_padding_mask.dtype
            if _kpm_dtype != torch.bool and not torch.is_floating_point(
                key_padding_mask
            ):
                raise AssertionError(
                    "only bool and floating types of key_padding_mask are supported"
                )

        if self.batch_first and is_batched:
            if key is value:
                if query is key:
                    query = key = value = query.transpose(1, 0)
                else:
                    query, key = [x.transpose(1, 0) for x in (query, key)]
                    value = key
            else:
                query, key, value = [x.transpose(1, 0) for x in (query, key, value)]

        if not self._qkv_same_embed_dim:
            if self.use_act_checkpoint:
                attn_output, attn_output_weights = torch.utils.checkpoint.checkpoint(
                    multi_head_attention_forward,
                    query,
                    key,
                    value,
                    self.embed_dim,
                    self.num_heads,
                    self.in_proj_weight,
                    self.in_proj_bias,
                    self.bias_k,
                    self.bias_v,
                    self.add_zero_attn,
                    self.dropout,
                    self.out_proj.weight,
                    self.out_proj.bias,
                    use_reentrant=False,
                    training=self.training,
                    key_padding_mask=key_padding_mask,
                    need_weights=need_weights,
                    attn_mask=attn_mask,
                    use_separate_proj_weight=True,
                    q_proj_weight=self.q_proj_weight,
                    k_proj_weight=self.k_proj_weight,
                    v_proj_weight=self.v_proj_weight,
                    average_attn_weights=average_attn_weights,
                    attn_type=self.attn_type,
                    attn_sparsity=self.sparsity,
                    attn_bias=attn_bias,
                    use_fa3=self.use_fa3,
                )
            else:
                attn_output, attn_output_weights = multi_head_attention_forward(
                    query,
                    key,
                    value,
                    self.embed_dim,
                    self.num_heads,
                    self.in_proj_weight,
                    self.in_proj_bias,
                    self.bias_k,
                    self.bias_v,
                    self.add_zero_attn,
                    self.dropout,
                    self.out_proj.weight,
                    self.out_proj.bias,
                    training=self.training,
                    key_padding_mask=key_padding_mask,
                    need_weights=need_weights,
                    attn_mask=attn_mask,
                    use_separate_proj_weight=True,
                    q_proj_weight=self.q_proj_weight,
                    k_proj_weight=self.k_proj_weight,
                    v_proj_weight=self.v_proj_weight,
                    average_attn_weights=average_attn_weights,
                    attn_type=self.attn_type,
                    attn_sparsity=self.sparsity,
                    attn_bias=attn_bias,
                    use_fa3=self.use_fa3,
                )
        else:
            if self.use_act_checkpoint:
                attn_output, attn_output_weights = torch.utils.checkpoint.checkpoint(
                    multi_head_attention_forward,
                    query,
                    key,
                    value,
                    self.embed_dim,
                    self.num_heads,
                    self.in_proj_weight,
                    self.in_proj_bias,
                    self.bias_k,
                    self.bias_v,
                    self.add_zero_attn,
                    self.dropout,
                    self.out_proj.weight,
                    self.out_proj.bias,
                    use_reentrant=False,
                    training=self.training,
                    key_padding_mask=key_padding_mask,
                    need_weights=need_weights,
                    attn_mask=attn_mask,
                    average_attn_weights=average_attn_weights,
                    attn_type=self.attn_type,
                    attn_sparsity=self.sparsity,
                    attn_bias=attn_bias,
                )
            else:
                attn_output, attn_output_weights = multi_head_attention_forward(
                    query,
                    key,
                    value,
                    self.embed_dim,
                    self.num_heads,
                    self.in_proj_weight,
                    self.in_proj_bias,
                    self.bias_k,
                    self.bias_v,
                    self.add_zero_attn,
                    self.dropout,
                    self.out_proj.weight,
                    self.out_proj.bias,
                    training=self.training,
                    key_padding_mask=key_padding_mask,
                    need_weights=need_weights,
                    attn_mask=attn_mask,
                    average_attn_weights=average_attn_weights,
                    attn_type=self.attn_type,
                    attn_sparsity=self.sparsity,
                    attn_bias=attn_bias,
                )
        if self.batch_first and is_batched:
            return attn_output.transpose(1, 0), attn_output_weights
        else:
            return attn_output, attn_output_weights


# Keep backward compatibility alias
MultiheadAttentionWrapper = MultiheadAttention


class DotProductScoring(torch.nn.Module):
    def __init__(
        self,
        d_model,
        d_proj,
        prompt_mlp=None,
        clamp_logits=True,
        clamp_max_val=12.0,
    ):
        super().__init__()
        self.d_proj = d_proj
        assert isinstance(prompt_mlp, torch.nn.Module) or prompt_mlp is None
        self.prompt_mlp = prompt_mlp  # an optional MLP projection for prompt
        self.prompt_proj = torch.nn.Linear(d_model, d_proj)
        self.hs_proj = torch.nn.Linear(d_model, d_proj)
        self.scale = float(1.0 / np.sqrt(d_proj))
        self.clamp_logits = clamp_logits
        if self.clamp_logits:
            self.clamp_max_val = clamp_max_val

    def mean_pool_text(self, prompt, prompt_mask):
        # is_valid has shape (seq, bs, 1), where 1 is valid and 0 is padding
        is_valid = (~prompt_mask).float().permute(1, 0)[..., None]
        # num_valid has shape (bs, 1)
        num_valid = torch.clamp(torch.sum(is_valid, dim=0), min=1.0)
        # mean pool over all the valid tokens -- pooled_prompt has shape (bs, proj_dim)
        pooled_prompt = (prompt * is_valid).sum(dim=0) / num_valid
        return pooled_prompt

    def forward(self, hs, prompt, prompt_mask):
        # hs has shape (num_layer, bs, num_query, d_model)
        # prompt has shape (seq, bs, d_model)
        # prompt_mask has shape (bs, seq), where 1 is valid and 0 is padding
        assert hs.dim() == 4 and prompt.dim() == 3 and prompt_mask.dim() == 2

        # apply MLP on prompt if specified
        if self.prompt_mlp is not None:
            prompt = self.prompt_mlp(prompt)

        # first, get the mean-pooled version of the prompt
        pooled_prompt = self.mean_pool_text(prompt, prompt_mask)

        # then, project pooled_prompt and hs to d_proj dimensions
        proj_pooled_prompt = self.prompt_proj(pooled_prompt)  # (bs, d_proj)
        proj_hs = self.hs_proj(hs)  # (num_layer, bs, num_query, d_proj)

        # finally, get dot-product scores of shape (num_layer, bs, num_query, 1)
        scores = torch.matmul(proj_hs, proj_pooled_prompt.unsqueeze(-1))
        scores *= self.scale

        # clamp scores to a max value to avoid numerical issues in loss or matcher
        if self.clamp_logits:
            scores.clamp_(min=-self.clamp_max_val, max=self.clamp_max_val)

        return scores


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


class LayerNorm2d(nn.Module):
    def __init__(self, num_channels: int, eps: float = 1e-6) -> None:
        super().__init__()
        self.weight = nn.Parameter(torch.ones(num_channels))
        self.bias = nn.Parameter(torch.zeros(num_channels))
        self.eps = eps

    def forward(self, x: torch.Tensor) -> torch.Tensor:
        u = x.mean(1, keepdim=True)
        s = (x - u).pow(2).mean(1, keepdim=True)
        x = (x - u) / torch.sqrt(s + self.eps)
        x = self.weight[:, None, None] * x + self.bias[:, None, None]
        return x


class TransformerWrapper(nn.Module):
    def __init__(
        self,
        encoder,
        decoder,
        d_model: int,
        two_stage_type="none",  # ["none"] only for now
        pos_enc_at_input_dec=True,
    ):
        super().__init__()

        self.encoder = encoder
        self.decoder = decoder
        self.num_queries = decoder.num_queries if decoder is not None else None
        self.pos_enc_at_input_dec = pos_enc_at_input_dec

        # for two stage
        assert two_stage_type in ["none"], "unknown param {} of two_stage_type".format(
            two_stage_type
        )
        self.two_stage_type = two_stage_type

        self._reset_parameters()
        self.d_model = d_model

    def _reset_parameters(self):
        for n, p in self.named_parameters():
            if p.dim() > 1:
                if (
                    "box_embed" not in n
                    and "query_embed" not in n
                    and "reference_points" not in n
                ):
                    nn.init.xavier_uniform_(p)


class MLP(nn.Module):
    """Very simple multi-layer perceptron (also called FFN)"""

    def __init__(
        self,
        input_dim: int,
        hidden_dim: int,
        output_dim: int,
        num_layers: int,
        dropout: float = 0.0,
        residual: bool = False,
        out_norm: Optional[nn.Module] = None,
    ):
        super().__init__()
        self.num_layers = num_layers
        h = [hidden_dim] * (num_layers - 1)
        self.layers = nn.ModuleList(
            nn.Linear(n, k) for n, k in zip([input_dim] + h, h + [output_dim])
        )
        self.drop = nn.Dropout(dropout) if dropout > 0 else nn.Identity()
        # whether to add the output as a residual connection to the input
        if residual and input_dim != output_dim:
            raise ValueError("residual is only supported if input_dim == output_dim")
        self.residual = residual
        # whether to apply a normalization layer to the output
        assert isinstance(out_norm, nn.Module) or out_norm is None
        self.out_norm = out_norm or nn.Identity()

    def forward(self, x):
        orig_x = x
        for i, layer in enumerate(self.layers):
            x = self.drop(F.relu(layer(x))) if i < self.num_layers - 1 else layer(x)
        if self.residual:
            x = x + orig_x
        x = self.out_norm(x)
        return x


def get_clones(module, N):
    return nn.ModuleList([copy.deepcopy(module) for i in range(N)])


def get_clones_seq(module, N):
    return nn.Sequential(*[copy.deepcopy(module) for i in range(N)])


def get_activation_fn(activation):
    """Return an activation function given a string"""
    if activation == "relu":
        return F.relu
    if activation == "gelu":
        return F.gelu
    if activation == "glu":
        return F.glu
    raise RuntimeError(f"activation should be relu/gelu, not {activation}.")


def get_activation_module(activation):
    """Return an activation function given a string"""
    if activation == "relu":
        return nn.ReLU
    if activation == "gelu":
        return nn.GELU
    if activation == "glu":
        return nn.GLU
    raise RuntimeError(f"activation should be relu/gelu, not {activation}.")


def get_valid_ratio(mask):
    _, H, W = mask.shape
    valid_H = torch.sum(~mask[:, :, 0], 1)
    valid_W = torch.sum(~mask[:, 0, :], 1)
    valid_ratio_h = valid_H.float() / H
    valid_ratio_w = valid_W.float() / W
    valid_ratio = torch.stack([valid_ratio_w, valid_ratio_h], -1)
    return valid_ratio


def gen_sineembed_for_position(pos_tensor, num_feats=256):
    assert num_feats % 2 == 0
    num_feats = num_feats // 2
    # n_query, bs, _ = pos_tensor.size()
    # sineembed_tensor = torch.zeros(n_query, bs, 256)
    scale = 2 * math.pi
    dim_t = torch.arange(num_feats, dtype=torch.float32, device=pos_tensor.device)
    dim_t = 10000 ** (2 * (torch.div(dim_t, 2, rounding_mode="floor")) / num_feats)
    x_embed = pos_tensor[:, :, 0] * scale
    y_embed = pos_tensor[:, :, 1] * scale
    pos_x = x_embed[:, :, None] / dim_t
    pos_y = y_embed[:, :, None] / dim_t
    pos_x = torch.stack(
        (pos_x[:, :, 0::2].sin(), pos_x[:, :, 1::2].cos()), dim=3
    ).flatten(2)
    pos_y = torch.stack(
        (pos_y[:, :, 0::2].sin(), pos_y[:, :, 1::2].cos()), dim=3
    ).flatten(2)
    if pos_tensor.size(-1) == 2:
        pos = torch.cat((pos_y, pos_x), dim=2)
    elif pos_tensor.size(-1) == 4:
        w_embed = pos_tensor[:, :, 2] * scale
        pos_w = w_embed[:, :, None] / dim_t
        pos_w = torch.stack(
            (pos_w[:, :, 0::2].sin(), pos_w[:, :, 1::2].cos()), dim=3
        ).flatten(2)

        h_embed = pos_tensor[:, :, 3] * scale
        pos_h = h_embed[:, :, None] / dim_t
        pos_h = torch.stack(
            (pos_h[:, :, 0::2].sin(), pos_h[:, :, 1::2].cos()), dim=3
        ).flatten(2)

        pos = torch.cat((pos_y, pos_x, pos_w, pos_h), dim=2)
    else:
        raise ValueError("Unknown pos_tensor shape(-1):{}".format(pos_tensor.size(-1)))
    return pos


class SAM3Output(list):
    """
    A class representing the output of a SAM3 model.
    It provides an iterable interface that supports different iteration modes, including iterating over all steps per stage,
    last step per stage, and flattened output.
    Attributes:
        output: The output of the SAM3 model, represented as a list of lists.
        iter_mode: The current iteration mode.
    Example:
        >>> output = [[1, 2], [3, 4], [5, 6]]
        >>> sam3_output = SAM3Output(output)
        >>> for step in sam3_output:
        ...     print(step)
        [1, 2]
        [3, 4]
        [5, 6]
        >>> with SAM3Output.iteration_mode(SAM3Output.IterMode.LAST_STEP_PER_STAGE) as sam3_last_step_out:
        ...     for step in sam3_last_step_out:
        ...         print(step)
        [2]
        [4]
        [6]
        >>> with SAM3Output.iteration_mode(SAM3Output.IterMode.FLATTENED) as sam3_flattened_out:
        ...     for step in sam3_flattened_out:
        ...         print(step)
        1
        2
        3
        4
        5
        6
    """

    class IterMode(Enum):
        # Defines the type of iterator over ouptuts.
        ALL_STEPS_PER_STAGE = auto()
        LAST_STEP_PER_STAGE = auto()
        FLATTENED = auto()  # Returns each interactivity step as if it is a separate stage (this is used in SAM3Image model)

    def __init__(
        self,
        output: List[List[Dict]] = None,
        iter_mode: IterMode = IterMode.ALL_STEPS_PER_STAGE,
        loss_stages: Optional[List[int]] = None,
    ):
        if output is not None:
            assert (
                isinstance(output, list)
                and len(output) > 0
                and isinstance(output[0], list)
            ), "Expected output to be a list of lists"
            self.output = output
        else:
            self.output = []
        assert isinstance(iter_mode, SAM3Output.IterMode), (
            f"iter_mode shoulf be of enum type 'SAM3Output.IterMode'. Got {type(iter_mode)}"
        )

        self.iter_mode = iter_mode
        # We create a weak reference to self to be used in the lambda functions.
        # This is to avoid cyclic references and let SAM3Output be garabge collected.
        self_ref = weakref.ref(self)
        self._mode2iter = {
            SAM3Output.IterMode.ALL_STEPS_PER_STAGE: lambda: iter(self_ref().output),
            SAM3Output.IterMode.LAST_STEP_PER_STAGE: lambda: (
                inner_list[-1] for inner_list in self_ref().output
            ),
            SAM3Output.IterMode.FLATTENED: lambda: (
                element for inner_list in self_ref().output for element in inner_list
            ),
        }
        self.loss_stages = loss_stages

    @override
    def __iter__(self) -> Iterator:
        return self._mode2iter[self.iter_mode]()

    def __getitem__(self, index):
        """
        Returns the item at the specified index.
        Args:
            index (int): The index of the item to return.
        Returns:
            list or element: The item at the specified index.
        """
        assert isinstance(index, int), f"index should be an integer. Got {type(index)}"
        if self.iter_mode == SAM3Output.IterMode.ALL_STEPS_PER_STAGE:
            return self.output[index]
        elif self.iter_mode == SAM3Output.IterMode.LAST_STEP_PER_STAGE:
            return self.output[index][-1]
        elif self.iter_mode == SAM3Output.IterMode.FLATTENED:
            if index == -1:
                return self.self.output[-1][-1]
            else:
                flattened_output = sum(self.output, [])
                return flattened_output[index]

    class _IterationMode(AbstractContextManager):
        """
        A context manager that temporarily changes the iteration mode of a SAM3Output object.
        This class is used internally by the SAM3Output.iteration_mode method.
        """

        def __init__(
            self, model_output: "SAM3Output", iter_mode: "SAM3Output.IterMode"
        ):
            self._model_output = model_output
            self._orig_iter_mode = model_output.iter_mode
            self._new_iter_mode = iter_mode

        @override
        def __enter__(self) -> "SAM3Output":
            self._model_output.iter_mode = self._new_iter_mode
            return self._model_output

        @override
        def __exit__(self, exc_type, exc_value, traceback):
            self._model_output.iter_mode = self._orig_iter_mode
            return super().__exit__(exc_type, exc_value, traceback)

    @staticmethod
    def iteration_mode(
        model_output: "SAM3Output", iter_mode: IterMode
    ) -> _IterationMode:
        """
        Returns a context manager that allows you to temporarily change the iteration mode of the SAM3Output object.
        Args:
            model_output: The SAM3Output object.
            iter_mode: The new iteration mode.
        Returns:
            SAM3Output._IterationMode: A context manager that changes the iteration mode of the SAM3Output object.
        """
        return SAM3Output._IterationMode(model_output=model_output, iter_mode=iter_mode)

    def append(self, item: list):
        assert isinstance(item, list), (
            f"Only list items are supported. Got {type(item)}"
        )
        self.output.append(item)

    def __repr__(self):
        return self.output.__repr__()

    def __len__(self):
        if self.iter_mode in [
            SAM3Output.IterMode.ALL_STEPS_PER_STAGE,
            SAM3Output.IterMode.LAST_STEP_PER_STAGE,
        ]:
            return len(self.output)
        elif self.iter_mode == SAM3Output.IterMode.FLATTENED:
            flattened_output = sum(self.output, [])
            return len(flattened_output)



================================================
FILE: sam3/model/multiplex_mask_decoder.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates.
# All rights reserved.

# This source code is licensed under the license found in the
# LICENSE file in the root directory of this source tree.


from typing import List, Optional, Type

import torch
from sam3.sam.common import LayerNorm2d
from torch import nn
from torch.nn import functional as F


class MultiplexMaskDecoder(nn.Module):
    def __init__(
        self,
        *,
        transformer_dim: int,
        transformer: nn.Module,
        multiplex_count: int,
        num_multimask_outputs: int = 3,
        activation: Type[nn.Module] = nn.GELU,
        iou_head_depth: int = 3,
        iou_head_hidden_dim: int = 256,
        use_high_res_features: bool = False,
        iou_prediction_use_sigmoid: bool = False,
        dynamic_multimask_via_stability=False,
        dynamic_multimask_stability_delta=0.05,
        dynamic_multimask_stability_thresh=0.98,
        pred_obj_scores: bool = False,
        pred_obj_scores_mlp: bool = False,
        use_multimask_token_for_obj_ptr: bool = False,
        decode_mask_with_shared_tokens: bool = False,
        decode_mask_attribute_with_shared_tokens: bool = False,
        multimask_outputs_only: bool = False,
    ) -> None:
        """
        Predicts masks given an image and prompt embeddings, using a
        transformer architecture with multiplex capabilities.

        Arguments:
          multiplex_count: the number of masks multiplexed into a single feature map
          num_multimask_outputs: the number of masks to predict per multiplex output
            (the total number of masks is (num_multimask_outputs+1) * multiplex_count)
          use_multimask_token_for_obj_ptr: whether to use multimask tokens for object pointers
          decode_mask_with_shared_tokens: use the same mask token for multimasks with different projection layers
          decode_mask_attribute_with_shared_tokens: use the mask tokens (instead of separate tokens)
            to predict iou and object scores
          multimask_outputs_only: predict num_multimask_outputs masks without the single
            mask output token (i.e., without the +1)
        """
        super().__init__()
        self.transformer_dim = transformer_dim
        self.transformer = transformer

        self.multiplex_count = multiplex_count
        self.num_multimask_outputs = num_multimask_outputs
        self.multimask_outputs_only = multimask_outputs_only
        self.decode_mask_with_shared_tokens = decode_mask_with_shared_tokens
        self.decode_mask_attribute_with_shared_tokens = (
            decode_mask_attribute_with_shared_tokens
        )

        if self.decode_mask_with_shared_tokens:
            assert multimask_outputs_only, (
                "multimask_outputs_only must be True if decode_mask_with_shared_tokens"
            )

        if self.multimask_outputs_only:
            self.num_mask_output_per_object = num_multimask_outputs
        else:
            self.num_mask_output_per_object = num_multimask_outputs + 1

        if self.decode_mask_with_shared_tokens:
            self.num_mask_tokens = multiplex_count
        else:
            self.num_mask_tokens = multiplex_count * self.num_mask_output_per_object

        self.pred_obj_scores = pred_obj_scores
        self.use_multimask_token_for_obj_ptr = use_multimask_token_for_obj_ptr

        if not self.decode_mask_attribute_with_shared_tokens:
            self.iou_token = nn.Embedding(multiplex_count, transformer_dim)
            if self.pred_obj_scores:
                self.obj_score_token = nn.Embedding(multiplex_count, transformer_dim)

        self.mask_tokens = nn.Embedding(self.num_mask_tokens, transformer_dim)

        self.output_upscaling = nn.Sequential(
            nn.ConvTranspose2d(
                transformer_dim, transformer_dim // 4, kernel_size=2, stride=2
            ),
            LayerNorm2d(transformer_dim // 4),
            activation(),
            nn.ConvTranspose2d(
                transformer_dim // 4, transformer_dim // 8, kernel_size=2, stride=2
            ),
            activation(),
        )
        self.use_high_res_features = use_high_res_features
        if use_high_res_features:
            self.conv_s0 = nn.Conv2d(
                transformer_dim, transformer_dim // 8, kernel_size=1, stride=1
            )
            self.conv_s1 = nn.Conv2d(
                transformer_dim, transformer_dim // 4, kernel_size=1, stride=1
            )

        if self.num_multimask_outputs == 0:
            self.output_hypernetworks_mlp = MLP(
                transformer_dim, transformer_dim, transformer_dim // 8, 3
            )
        else:
            self.output_hypernetworks_mlps = nn.ModuleList(
                [
                    MLP(transformer_dim, transformer_dim, transformer_dim // 8, 3)
                    for _ in range(self.num_mask_output_per_object)
                ]
            )

        self.iou_prediction_head = MLP(
            transformer_dim,
            iou_head_hidden_dim,
            (
                1
                if (
                    self.decode_mask_attribute_with_shared_tokens
                    and not self.decode_mask_with_shared_tokens
                )
                else self.num_mask_output_per_object
            ),
            iou_head_depth,
            sigmoid_output=iou_prediction_use_sigmoid,
        )

        if self.pred_obj_scores:
            self.pred_obj_score_head = nn.Linear(transformer_dim, 1)
            if pred_obj_scores_mlp:
                self.pred_obj_score_head = MLP(transformer_dim, transformer_dim, 1, 3)

        # When outputting a single mask, optionally we can dynamically fall back to the best
        # multimask output token if the single mask output token gives low stability scores.
        self.dynamic_multimask_via_stability = dynamic_multimask_via_stability
        self.dynamic_multimask_stability_delta = dynamic_multimask_stability_delta
        self.dynamic_multimask_stability_thresh = dynamic_multimask_stability_thresh

    def forward(
        self,
        image_embeddings: torch.Tensor,
        image_pe: torch.Tensor,
        multimask_output: bool,
        high_res_features: Optional[List[torch.Tensor]] = None,
        extra_per_object_embeddings: Optional[torch.Tensor] = None,
    ) -> dict[str, torch.Tensor]:
        """
        Predict masks given image and prompt embeddings.

        Arguments:
          image_embeddings (torch.Tensor): the embeddings from the image encoder
          image_pe (torch.Tensor): positional encoding with the shape of image_embeddings
          extra_per_object_embeddings (torch.Tensor): a tensor with shape b * multiplex_count * C to be added to the mask tokens

        Returns: a dict of Tensors indexed by strings
          masks: batched predicted masks
          iou_pred: batched predictions of mask quality
          object_score_logits: batched predictions of object existence
        """

        if self.num_multimask_outputs <= 0:
            assert not multimask_output, (
                f"multimask_output must be False with {self.num_multimask_outputs=}"
            )

        if self.multimask_outputs_only:
            assert multimask_output, (
                f"multimask_output must be True with {self.multimask_outputs_only=}"
            )

        out = self.predict_masks(
            image_embeddings=image_embeddings,
            image_pe=image_pe,
            high_res_features=high_res_features,
            extra_per_object_embeddings=extra_per_object_embeddings,
        )

        masks = out["masks"]  # [B, M, (self.num_mask_token_per_object), H, W]
        iou_pred = out["iou_pred"]  # [B, M, (self.num_mask_token_per_object)]
        mask_tokens_out = out[
            "mask_tokens_out"
        ]  # [B, M, (self.num_mask_token_per_object), C]

        # Select the correct mask or masks for output
        if multimask_output:
            if not self.multimask_outputs_only:
                masks = masks[:, :, 1:, :, :]
                iou_pred = iou_pred[:, :, 1:]
        elif self.dynamic_multimask_via_stability and not self.training:
            masks, iou_pred = self._dynamic_multimask_via_stability(masks, iou_pred)
        else:
            masks = masks[:, :, 0:1, :, :]
            iou_pred = iou_pred[:, :, 0:1]

        if multimask_output and self.use_multimask_token_for_obj_ptr:
            if self.multimask_outputs_only:
                sam_tokens_out = mask_tokens_out
            else:
                sam_tokens_out = mask_tokens_out[
                    :, :, 1:
                ]  # [B, M, num_multimask_outputs, C] shape
        else:
            # Take the mask output token. Here we *always* use the token for single mask output.
            # At test time, even if we track after 1-click (and using multimask_output=True),
            # we still take the single mask token here. The rationale is that we always track
            # after multiple clicks during training, so the past tokens seen during training
            # are always the single mask token (and we'll let it be the object-memory token).
            sam_tokens_out = mask_tokens_out[:, :, 0:1]  # [B, M, 1, C] shape

        del out["mask_tokens_out"]
        out["masks"] = masks
        out["iou_pred"] = iou_pred
        out["sam_tokens_out"] = sam_tokens_out

        if multimask_output:
            assert masks.shape[2] == self.num_mask_output_per_object, (
                f"{masks.shape=}, {self.num_mask_output_per_object=}"
            )
            assert iou_pred.shape[2] == self.num_mask_output_per_object, (
                f"{iou_pred.shape=}, {self.num_mask_output_per_object=}"
            )
            if self.use_multimask_token_for_obj_ptr:
                if self.decode_mask_with_shared_tokens:
                    assert sam_tokens_out.shape[2] == 1, f"{sam_tokens_out.shape=}"
                else:
                    assert sam_tokens_out.shape[2] == self.num_mask_output_per_object, (
                        f"{sam_tokens_out.shape=}, {self.num_mask_output_per_object=}"
                    )
        else:
            assert masks.shape[2] == 1, f"{masks.shape=}"
            assert iou_pred.shape[2] == 1, f"{iou_pred.shape=}"
            assert sam_tokens_out.shape[2] == 1, f"{sam_tokens_out.shape=}"

        return out

    def predict_masks(
        self,
        image_embeddings: torch.Tensor,
        image_pe: torch.Tensor,
        high_res_features: Optional[List[torch.Tensor]] = None,
        extra_per_object_embeddings: Optional[
            torch.Tensor
        ] = None,  # num_buckets, multiplex_count, C
    ) -> dict[str, torch.Tensor]:
        """Predicts masks. See 'forward' for more details."""
        # Concatenate output tokens
        B = image_embeddings.shape[0]
        token_list = []
        if self.pred_obj_scores and not self.decode_mask_attribute_with_shared_tokens:
            token_list.append(self.obj_score_token.weight)
        if not self.decode_mask_attribute_with_shared_tokens:
            token_list.append(self.iou_token.weight)

        tokens = torch.cat(token_list, dim=0)
        tokens = tokens.unsqueeze(0).expand(B, -1, -1)

        if extra_per_object_embeddings is not None:
            mask_tokens = self.mask_tokens.weight.view(
                1, self.multiplex_count, self.num_mask_output_per_object, -1
            ).expand(B, -1, -1, -1)

            mask_tokens = mask_tokens + extra_per_object_embeddings.unsqueeze(2)
            mask_tokens = mask_tokens.flatten(1, 2)
        else:
            mask_tokens = self.mask_tokens.weight.unsqueeze(0).expand(B, -1, -1)

        tokens = torch.cat([tokens, mask_tokens], dim=1)

        src = image_embeddings

        assert image_pe.size(0) == 1, (
            "image_pe should have size 1 in batch dim (from `get_dense_pe()`)"
        )
        pos_src = torch.repeat_interleave(image_pe, tokens.shape[0], dim=0)
        b, c, h, w = src.shape

        # Run the transformer
        hs, src = self.transformer(src, pos_src, tokens)

        # Parse transformer outputs based on token sharing configuration
        if self.decode_mask_attribute_with_shared_tokens:
            assert hs.shape[1] == self.num_mask_tokens, (
                f"{hs.shape=}, {self.num_mask_tokens=}"
            )
            iou_token_out = mask_tokens_out = hs[:, 0 : self.num_mask_tokens]
            if self.pred_obj_scores:
                obj_score_token_out = mask_tokens_out
        else:
            # Separate tokens for each prediction type
            s = 0
            if self.pred_obj_scores:
                obj_score_token_out = hs[:, s : s + self.multiplex_count, :]
                s += self.multiplex_count

            iou_token_out = hs[:, s : s + self.multiplex_count, :]
            s += self.multiplex_count
            mask_tokens_out = hs[:, s : s + self.num_mask_tokens, :]
            assert hs.shape[1] == s + self.num_mask_tokens, (
                f"{hs.shape=}, {s=}, {self.num_mask_tokens=}"
            )

        # Upscale mask embeddings and predict masks using the mask tokens
        src = src.transpose(1, 2).view(b, c, h, w)
        if not self.use_high_res_features:
            upscaled_embedding = self.output_upscaling(src)
        else:
            dc1, ln1, act1, dc2, act2 = self.output_upscaling
            feat_s0, feat_s1 = high_res_features
            upscaled_embedding = act1(ln1(dc1(src) + feat_s1))
            upscaled_embedding = act2(dc2(upscaled_embedding) + feat_s0)

        if self.decode_mask_with_shared_tokens:
            mask_tokens_out = mask_tokens_out.view(B, self.multiplex_count, 1, -1)
        else:
            mask_tokens_out = mask_tokens_out.view(
                B, self.multiplex_count, self.num_mask_output_per_object, -1
            )
        if self.num_multimask_outputs == 0:
            hyper_in = self.output_hypernetworks_mlp(
                mask_tokens_out[:, :, 0, :]
            ).unsqueeze(2)  # [B, M, 1, C]
        else:
            hyper_in_list: List[torch.Tensor] = []
            for i in range(self.num_mask_output_per_object):
                if self.decode_mask_with_shared_tokens:
                    hyper_in_list.append(
                        self.output_hypernetworks_mlps[i](mask_tokens_out[:, :, 0, :])
                    )
                else:
                    hyper_in_list.append(
                        self.output_hypernetworks_mlps[i](mask_tokens_out[:, :, i, :])
                    )
            # hyper_in: [B, M, num_multimask_outputs+1, C]
            hyper_in = torch.stack(hyper_in_list, dim=2)

        # generate the masks
        b, c, h, w = upscaled_embedding.shape
        masks = torch.bmm(
            hyper_in.flatten(1, 2), upscaled_embedding.view(b, c, h * w)
        ).view(b, self.multiplex_count, self.num_mask_output_per_object, h, w)

        # Generate mask quality predictions, with shape b * multiplex_count * (num_multimask_outputs+1)
        iou_pred = self.iou_prediction_head(iou_token_out).view(
            b, self.multiplex_count, self.num_mask_output_per_object
        )

        if self.pred_obj_scores:
            # Generate mask quality predictions, with shape b * (num_multimask_outputs+1)
            if (
                self.decode_mask_attribute_with_shared_tokens
                and not self.decode_mask_with_shared_tokens
            ):
                object_score_logits = (
                    self.pred_obj_score_head(obj_score_token_out)
                    .view(b, self.multiplex_count, self.num_mask_output_per_object)
                    .sum(-1, keepdim=True)
                )
            else:
                object_score_logits = self.pred_obj_score_head(obj_score_token_out)
        else:
            # Obj scores logits - default to 10.0, i.e. assuming the object is present, sigmoid(10)=1
            object_score_logits = 10.0 * iou_pred.new_ones(
                iou_pred.shape[0], iou_pred.shape[1]
            )

        outputs = {
            "masks": masks,
            "iou_pred": iou_pred,
            "mask_tokens_out": mask_tokens_out,
            "object_score_logits": object_score_logits,
        }

        return outputs

    def _get_stability_scores(self, mask_logits):
        """
        Compute stability scores of the mask logits based on the IoU between upper and
        lower thresholds.
        """
        mask_logits = mask_logits.flatten(-2)
        stability_delta = self.dynamic_multimask_stability_delta
        area_i = torch.sum(mask_logits > stability_delta, dim=-1).float()
        area_u = torch.sum(mask_logits > -stability_delta, dim=-1).float()
        stability_scores = torch.where(area_u > 0, area_i / area_u, 1.0)
        return stability_scores

    def _dynamic_multimask_via_stability(self, all_mask_logits, all_iou_scores):
        """
        When outputting a single mask, if the stability score from the current single-mask
        output (based on output token 0) falls below a threshold, we instead select from
        multi-mask outputs (based on output token 1~3) the mask with the highest predicted
        IoU score. This is intended to ensure a valid mask for both clicking and tracking.
        """
        # first, flatten the batch and the multiplex dimensions
        B, M = all_mask_logits.shape[:2]
        all_mask_logits = all_mask_logits.flatten(0, 1)
        all_iou_scores = all_iou_scores.flatten(0, 1)

        # The best mask from multimask output tokens (1~3)
        multimask_logits = all_mask_logits[:, 1:, :, :]
        multimask_iou_scores = all_iou_scores[:, 1:]
        best_scores_inds = torch.argmax(multimask_iou_scores, dim=-1)
        batch_inds = torch.arange(
            multimask_iou_scores.size(0), device=all_iou_scores.device
        )
        best_multimask_logits = multimask_logits[batch_inds, best_scores_inds]
        best_multimask_logits = best_multimask_logits.unsqueeze(1)
        best_multimask_iou_scores = multimask_iou_scores[batch_inds, best_scores_inds]
        best_multimask_iou_scores = best_multimask_iou_scores.unsqueeze(1)

        # The mask from singlemask output token 0 and its stability score
        singlemask_logits = all_mask_logits[:, 0:1, :, :]
        singlemask_iou_scores = all_iou_scores[:, 0:1]
        stability_scores = self._get_stability_scores(singlemask_logits)
        is_stable = stability_scores >= self.dynamic_multimask_stability_thresh

        # Dynamically fall back to best multimask output upon low stability scores.
        mask_logits_out = torch.where(
            is_stable[..., None, None].expand_as(singlemask_logits),
            singlemask_logits,
            best_multimask_logits,
        )
        iou_scores_out = torch.where(
            is_stable.expand_as(singlemask_iou_scores),
            singlemask_iou_scores,
            best_multimask_iou_scores,
        )

        # restore the batch and multiplex dimensions
        mask_logits_out = mask_logits_out.unflatten(0, (B, M))
        iou_scores_out = iou_scores_out.unflatten(0, (B, M))

        return mask_logits_out, iou_scores_out


# Lightly adapted from
# https://github.com/facebookresearch/MaskFormer/blob/main/mask_former/modeling/transformer/transformer_predictor.py # noqa
class MLP(nn.Module):
    def __init__(
        self,
        input_dim: int,
        hidden_dim: int,
        output_dim: int,
        num_layers: int,
        sigmoid_output: bool = False,
    ) -> None:
        super().__init__()
        self.num_layers = num_layers
        h = [hidden_dim] * (num_layers - 1)
        self.layers = nn.ModuleList(
            nn.Linear(n, k) for n, k in zip([input_dim] + h, h + [output_dim])
        )
        self.sigmoid_output = sigmoid_output

    def forward(self, x):
        for i, layer in enumerate(self.layers):
            x = F.relu(layer(x)) if i < self.num_layers - 1 else layer(x)
        if self.sigmoid_output:
            x = F.sigmoid(x)
        return x



================================================
FILE: sam3/model/multiplex_utils.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

import logging
import math
from typing import Optional

import torch
from torch import nn

# Special values for object tracking
_PADDING_NUM = -1  # Marks empty slots in buckets
_REMOVED_NUM = -1116  # Marks objects that have been removed


logger = logging.getLogger(__name__)


class MultiplexState:
    """
    MultiplexState records the state of multiplexing, for one or more buckets.

    At a high level, we deal with the conversion of tensors between the data space (batch_size, num_channels, ...)
    and the multiplex space (num_buckets, multiplex_count, num_channels, ...).

    The multiplex state stores the assignments of each batch element to a slot in a bucket.
    Each bucket has a fixed number of slots (multiplex_count), and not all slots need to be filled.
    The batch size should equate to total_valid_entries, which is the sum of the number of valid entries in each bucket.

    There are two main operations that this class supports:
        mux: convert tensors in the data space to the multiplex space.
        The mental model is that we start from a tensor of zeros that has the shape of the output,
        then we go through the valid entries and place them into the corresponding slots, indicated by the assignments.

        demux: convert tensors in the multiplex space to the data space.
        This is the reverse operation of mux. Note that zeros were used in mux for the padding slots,
        and that those slots are ignored in demux.

    There are also two utility functions for object mangement:
        add_objects: add new objects to the state by filling in empty slots
        remove_objects: remove objects from the state by marking them as removed (not the same as empty!)
    """

    def __init__(
        self,
        assignments: list[list[int]],
        device: torch.device,
        dtype: torch.dtype,
        allowed_bucket_capacity: int,
        *,
        object_ids: Optional[list[int]] = None,
    ):
        """
        assignments: a list of lists of object indices
            Each top-level list represents a bucket
            Each inner list represents the object indices that are in the bucket
            The object indices must ranges from 0 to num_valid_entries - 1, except for the following special values (all negatives):
                _PADDING_NUM, which denotes padding entries
                _REMOVED_NUM, which denotes an pre-existing object that got removed (currently not used during init)
            If you wish to save the "true" object IDs, i.e., during inference, you can bookkeep them here
        """
        self.device = device
        self.dtype = dtype

        # Initialize bucket assignments and precompute matrices
        self.allowed_bucket_capacity = allowed_bucket_capacity
        self._initialize_assignments(assignments, object_ids=object_ids)

    def _initialize_assignments(
        self, assignments: list[list[int]], *, object_ids: Optional[list[int]] = None
    ):
        self.assignments = assignments
        self.num_buckets = len(self.assignments)
        if self.num_buckets == 0:
            logger.error("No buckets found in the state")
            raise ValueError("No buckets found in the state")

        self.multiplex_count = len(self.assignments[0])
        assert all(
            len(self.assignments[i]) == self.multiplex_count
            for i in range(self.num_buckets)
        )

        # number of non-negative elements in the state
        self.total_valid_entries = sum(
            sum(1 for x in bucket if x >= 0) for bucket in self.assignments
        )
        self.total_non_padding_entries = sum(
            sum(1 for x in bucket if x != _PADDING_NUM) for bucket in self.assignments
        )

        # check the validity of the object IDs
        self.object_ids = object_ids
        if self.object_ids is not None:
            assert len(self.object_ids) == self.total_valid_entries, (
                "object_ids should map 1:1 to the valid entries"
            )

        # check the validity of the assignments
        all_object_idxs = set()
        for bucket in self.assignments:
            valid_entries_in_bucket = sum(1 for x in bucket if x != _PADDING_NUM)
            assert valid_entries_in_bucket <= self.allowed_bucket_capacity, (
                f"{valid_entries_in_bucket=} > {self.allowed_bucket_capacity=}"
            )
            for obj_idx in bucket:
                if obj_idx >= 0:
                    assert obj_idx < self.total_non_padding_entries, (
                        f"object ID {obj_idx} >= {self.total_non_padding_entries}"
                    )
                    assert obj_idx not in all_object_idxs, "object IDs must be unique"
                    all_object_idxs.add(obj_idx)

        # Precompute and cache the actual selection matrices
        self._precompute_transition_matrices(self.device, self.dtype)

    @property
    def available_slots(self) -> int:
        # returns the number of available slots in the state
        return (
            self.num_buckets * self.allowed_bucket_capacity
            - self.total_non_padding_entries
        )

    def find_next_batch_of_available_indices(
        self,
        num_objects: int,
        *,
        allow_new_buckets: bool = False,
        prefer_new_buckets: bool = False,
    ) -> list[int]:
        # produce a list of consecutive indices that are available in the state
        # Note: prefer_new_buckets parameter is accepted for API compatibility but not used here
        # as the actual bucket allocation logic is in add_objects()
        assert num_objects > 0, f"{num_objects=} must be positive"
        if not allow_new_buckets:
            assert self.available_slots >= num_objects, (
                f"not enough available slots {self.available_slots} < {num_objects}"
            )

        return list(
            range(
                self.total_valid_entries,
                self.total_valid_entries + num_objects,
            )
        )

    def add_objects(
        self,
        object_indices: list[int],
        *,
        object_ids: Optional[list[int]] = None,
        allow_new_buckets: bool = False,
        prefer_new_buckets: bool = False,
    ):
        """
        Add new objects to the state by filling in empty slots and
        creating new buckets if necessary.

        object_indices must be sorted and follow existing object indices.
        If prefer_new_buckets is True, we skip filling existing slots and place
        the objects into freshly created buckets (requires allow_new_buckets=True).
        """
        if len(object_indices) == 0:
            return

        # we will modify this in-place
        object_indices = object_indices.copy()
        assert (object_ids is None) == (self.object_ids is None), (
            "object_ids must either be always given or always omitted"
        )

        if object_ids is not None:
            assert len(object_ids) == len(object_indices), (
                "object_ids must have the same length as object_indices"
            )
            object_ids = object_ids.copy()

        num_new_objects = len(object_indices)
        assert object_indices == sorted(object_indices), "object_indices must be sorted"
        object_indices.reverse()  # reverse so we can pop from the end
        if object_ids is not None:
            object_ids.reverse()

        if prefer_new_buckets:
            assert allow_new_buckets, "prefer_new_buckets requires allow_new_buckets"

        slots_filled = 0
        buckets_created = 0

        def _pop_next():
            idx = object_indices.pop()
            if object_ids is not None and self.object_ids is not None:
                self.object_ids.append(object_ids.pop())
            return idx

        if not prefer_new_buckets:
            # Fill empty slots in existing buckets first
            for bucket in self.assignments:
                for i in range(self.allowed_bucket_capacity):
                    if bucket[i] == _PADDING_NUM:
                        bucket[i] = _pop_next()
                        slots_filled += 1
                        if len(object_indices) == 0:
                            break
                if len(object_indices) == 0:
                    break

        if len(object_indices) > 0 and not allow_new_buckets:
            raise ValueError(
                f"Cannot place objects {list(reversed(object_indices))} without creating new buckets"
            )

        # Create new buckets for remaining objects (or all objects if prefer_new_buckets)
        while len(object_indices) > 0:
            new_bucket = [_PADDING_NUM] * self.multiplex_count
            for i in range(self.allowed_bucket_capacity):
                if len(object_indices) == 0:
                    break
                new_bucket[i] = _pop_next()
            self.assignments.append(new_bucket)
            buckets_created += 1

        # reinitialize all the settings
        original_num_entries = self.total_valid_entries
        self._initialize_assignments(self.assignments, object_ids=self.object_ids)
        assert self.total_valid_entries == original_num_entries + num_new_objects, (
            f"{self.total_valid_entries=} != {original_num_entries=} + {num_new_objects=}"
        )

        logger.info(
            f"Filled {slots_filled} slots and created {buckets_created} new buckets"
        )
        logger.info(
            f"{self.num_buckets=}, {self.total_valid_entries=}, {self.total_non_padding_entries=}"
        )

    def remove_objects(self, object_indices: list[int], strict: bool = True):
        """
        Remove objects from the state by marking them as removed.
        Remove a bucket if all objects in the bucket are removed.

        Args:
            object_indices: List of object indices to remove
            strict: If True, will raise an error if any object indices are not found in the state

        Returns:
            List of bucket indices that we are going to keep
        """
        object_indices = object_indices.copy()

        # Mark objects as removed in assignments
        for bucket_idx, bucket in enumerate(self.assignments):
            for slot_idx, obj_id in enumerate(bucket):
                if obj_id in object_indices:
                    self.assignments[bucket_idx][slot_idx] = _REMOVED_NUM
                    object_indices.remove(obj_id)

        if strict:
            assert len(object_indices) == 0, (
                f"Failed to remove objects: {object_indices}"
            )

        # Check which buckets should be completely removed (all objects removed/paddings)
        # and which buckets we will keep
        buckets_to_remove = []
        buckets_to_keep = []
        for bucket_idx, bucket in enumerate(self.assignments):
            # Check if all objects in this bucket are removed or are paddings
            all_removed = all(
                obj_id in [_PADDING_NUM, _REMOVED_NUM] for obj_id in bucket
            )
            if all_removed:
                buckets_to_remove.append(bucket_idx)
                logger.info(
                    f"Bucket {bucket_idx} marked for removal - all objects removed/paddings"
                )
            else:
                buckets_to_keep.append(bucket_idx)

        # Remove buckets in reverse order to maintain correct indices
        for bucket_idx in reversed(buckets_to_remove):
            del self.assignments[bucket_idx]

        if len(buckets_to_keep) == 0:
            logger.info(f"Removing all buckets: {buckets_to_remove}; state invalidated")
            self.assignments = None
            if self.object_ids is not None:
                self.object_ids = []
            return buckets_to_keep

        # After removal, remap object IDs to be sequential
        # Collect all unique positive object IDs and create a mapping to sequential IDs
        all_positive_ids = set()
        for bucket in self.assignments:
            for obj_id in bucket:
                if obj_id >= 0:
                    all_positive_ids.add(obj_id)

        # Create mapping from old IDs to new sequential IDs
        sorted_ids = sorted(all_positive_ids)
        id_mapping = {old_id: new_id for new_id, old_id in enumerate(sorted_ids)}

        # Apply the mapping to assignments to make IDs sequential
        for bucket in self.assignments:
            for i, obj_id in enumerate(bucket):
                if obj_id >= 0:
                    bucket[i] = id_mapping[obj_id]

        # Update object_ids if they exist
        if self.object_ids is not None:
            # Create new object_ids array based on the remapped indices
            # We need to preserve the original object_ids for the objects that weren't removed
            new_object_ids = [None] * len(sorted_ids)

            # Map the original object_ids to their new positions
            for old_idx, new_idx in id_mapping.items():
                new_object_ids[new_idx] = self.object_ids[old_idx]

            assert not any(obj_id is None for obj_id in new_object_ids)
            self.object_ids = new_object_ids

        # Reinitialize the state to update all internal structures
        self._initialize_assignments(self.assignments, object_ids=self.object_ids)

        logger.info(f"Removed these buckets: {buckets_to_remove}")
        logger.info(f"Kept these buckets: {buckets_to_keep}")
        logger.info(
            f"Remaining buckets: {self.num_buckets}, total valid entries: {self.total_valid_entries}"
        )

        return buckets_to_keep

    def _precompute_transition_matrices(self, device: torch.device, dtype: torch.dtype):
        """
        Precompute the transition matrices for maximum efficiency.
        Note that these should be partial permutation matrices.
        """
        # Create a transition matrix for muxing
        self.mux_matrix = torch.zeros(
            self.num_buckets * self.multiplex_count,
            self.total_valid_entries,
            device=device,
            dtype=dtype,
        )

        # Create a transition matrix for demuxing
        self.demux_matrix = torch.zeros(
            self.total_valid_entries,
            self.num_buckets * self.multiplex_count,
            device=device,
            dtype=dtype,
        )

        # Fill both matrices based on assignments
        for i in range(self.num_buckets):
            for j in range(self.multiplex_count):
                bucket_idx = i * self.multiplex_count + j
                object_idx = self.assignments[i][j]
                if object_idx >= 0:
                    self.mux_matrix[bucket_idx, object_idx] = 1.0
                    self.demux_matrix[object_idx, bucket_idx] = 1.0

    def mux(self, x: torch.Tensor) -> torch.Tensor:
        """
        Multiplexing operation
            x: self.total_valid_entries * ...

            return num_buckets * multiplex_count * ...
            with padding entries filled with 0
        """
        num_valid_entries = x.shape[0]
        assert num_valid_entries == self.total_valid_entries, (
            f"{num_valid_entries=} != {self.total_valid_entries=}"
        )
        output_shape = (
            self.num_buckets,
            self.multiplex_count,
        ) + x.shape[1:]

        x_flat = x.reshape(num_valid_entries, -1)

        # Apply mux matrix: (num_buckets * multiplex_count, batch_size) @ (batch_size, features)
        # Result: (num_buckets * multiplex_count, features)
        result_flat = self.mux_matrix @ x_flat

        result = result_flat.view(output_shape)
        return result

    def demux(self, x: torch.Tensor) -> torch.Tensor:
        """
        Inverse operation of mux
            x: num_buckets, multiplex_count * ...
            Returns: total_valid_entries * ...
        """
        num_buckets, multiplex_count = x.shape[:2]
        assert num_buckets == self.num_buckets, f"{num_buckets=} != {self.num_buckets=}"
        assert multiplex_count == self.multiplex_count, (
            f"{multiplex_count=} != {self.multiplex_count=}"
        )
        output_shape = (self.total_valid_entries,) + x.shape[2:]

        x_flat = x.reshape(num_buckets * multiplex_count, -1)

        # Apply demux matrix: (total_valid_entries, num_buckets*multiplex_count) @ (num_buckets*multiplex_count, features)
        # Result: (total_valid_entries, features)
        result_flat = self.demux_matrix @ x_flat

        result = result_flat.view(output_shape)
        return result

    def get_valid_object_mask(self) -> torch.Tensor:
        """
        Returns a (num_buckets, multiplex_count) tensor with 1 for valid entries and 0 for padding entries
        """
        valid_mask = self.mux_matrix.sum(dim=1) > 0
        valid_mask = valid_mask.reshape(self.num_buckets, self.multiplex_count)

        return valid_mask

    def get_all_valid_object_idx(self) -> set[int]:
        """
        Returns a set of all valid object idx in the state
        Note that this returns the internal object idx representations,
        not the arbitrary object IDs that are passed in during initialization
        """
        all_valid_objects = {
            obj_idx for bucket in self.assignments for obj_idx in bucket if obj_idx >= 0
        }
        return all_valid_objects


class MultiplexController(nn.Module):
    def __init__(
        self,
        multiplex_count: int,
        full_shuffle: bool = False,
        eval_multiplex_count: int = -1,
    ):
        super().__init__()

        self.multiplex_count = multiplex_count
        self.full_shuffle = full_shuffle
        if eval_multiplex_count < 0:
            self.eval_multiplex_count = multiplex_count
        else:
            self.eval_multiplex_count = eval_multiplex_count
        assert self.multiplex_count >= 1

    @property
    def allowed_bucket_capacity(self) -> int:
        if self.training:
            return self.multiplex_count
        else:
            return self.eval_multiplex_count

    def get_state(
        self,
        num_valid_entries: int,
        device: torch.device,
        dtype: torch.dtype,
        random: bool = True,
        *,
        object_ids: Optional[
            list[int]
        ] = None,  # object_ids is an auxiliary field that we pass to the state unmodified
    ) -> MultiplexState:
        # returns a state that maps elements in the batch to buckets of size self.multiplex_count

        allowed_bucket_capacity = self.allowed_bucket_capacity

        # the size of the bucket during training
        true_bucket_capacity = self.multiplex_count

        num_buckets = math.ceil(num_valid_entries / allowed_bucket_capacity)
        # each bucket contains at most self.multiplex_count elements
        # padding elements are marked with _PADDING_NUM (only the last bucket should contain _PADDING_NUM)

        if self.full_shuffle:
            # Shuffle all IDs, including the paddings
            ids = torch.cat(
                [
                    torch.arange(num_valid_entries, dtype=torch.long),
                    torch.tensor(
                        [_PADDING_NUM]
                        * (num_buckets * true_bucket_capacity - num_valid_entries),
                        dtype=torch.long,
                    ),
                ],
                dim=0,
            )
            if random:
                indices = torch.randperm(ids.shape[0], dtype=torch.long)
                ids = ids[indices]

            # convert to a list of list
            assignments = []
            for i in range(num_buckets):
                assignments.append(
                    ids[
                        i * true_bucket_capacity : (i + 1) * true_bucket_capacity
                    ].tolist()
                )
        else:
            # Only shuffle the the IDs within the first #batch_size slots, leave all paddings at the end
            if random:
                # randomly assign ids to buckets
                ids = torch.randperm(num_valid_entries, dtype=torch.int64)
            else:
                ids = torch.arange(num_valid_entries)
            # append with _PADDING_NUM to make a multiple of bucket_capacity
            total_elements = num_buckets * allowed_bucket_capacity
            if ids.shape[0] < total_elements:
                ids = torch.cat(
                    [
                        ids,
                        torch.tensor([_PADDING_NUM] * (total_elements - ids.shape[0])),
                    ]
                )

            # convert to a list of list
            assignments = []
            for i in range(num_buckets):
                assignments.append(
                    ids[
                        i * allowed_bucket_capacity : (i + 1) * allowed_bucket_capacity
                    ].tolist()
                    + [_PADDING_NUM] * (true_bucket_capacity - allowed_bucket_capacity)
                )

        return MultiplexState(
            assignments,
            device,
            dtype,
            allowed_bucket_capacity=allowed_bucket_capacity,
            object_ids=object_ids,
        )



================================================
FILE: sam3/model/necks.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

"""Necks are the interface between a vision backbone and the rest of the detection model"""

from copy import deepcopy
from typing import List, Optional, Tuple

import torch
import torch.nn as nn
from sam3.model.data_misc import NestedTensor


class Sam3DualViTDetNeck(nn.Module):
    def __init__(
        self,
        trunk: nn.Module,
        position_encoding: nn.Module,
        d_model: int,
        scale_factors=(4.0, 2.0, 1.0, 0.5),
        add_sam2_neck: bool = False,
    ):
        """
        SimpleFPN neck a la ViTDet
        (From detectron2, very lightly adapted)
        It supports a "dual neck" setting, where we have two identical necks (for SAM3 and SAM2), with different weights

        :param trunk: the backbone
        :param position_encoding: the positional encoding to use
        :param d_model: the dimension of the model
        """
        super().__init__()
        self.trunk = trunk
        self.position_encoding = position_encoding
        self.convs = nn.ModuleList()

        self.scale_factors = scale_factors
        use_bias = True
        dim: int = self.trunk.channel_list[-1]

        for _, scale in enumerate(scale_factors):
            current = nn.Sequential()

            if scale == 4.0:
                current.add_module(
                    "dconv_2x2_0",
                    nn.ConvTranspose2d(dim, dim // 2, kernel_size=2, stride=2),
                )
                current.add_module(
                    "gelu",
                    nn.GELU(),
                )
                current.add_module(
                    "dconv_2x2_1",
                    nn.ConvTranspose2d(dim // 2, dim // 4, kernel_size=2, stride=2),
                )
                out_dim = dim // 4
            elif scale == 2.0:
                current.add_module(
                    "dconv_2x2",
                    nn.ConvTranspose2d(dim, dim // 2, kernel_size=2, stride=2),
                )
                out_dim = dim // 2
            elif scale == 1.0:
                out_dim = dim
            elif scale == 0.5:
                current.add_module(
                    "maxpool_2x2",
                    nn.MaxPool2d(kernel_size=2, stride=2),
                )
                out_dim = dim
            else:
                raise NotImplementedError(f"scale_factor={scale} is not supported yet.")

            current.add_module(
                "conv_1x1",
                nn.Conv2d(
                    in_channels=out_dim,
                    out_channels=d_model,
                    kernel_size=1,
                    bias=use_bias,
                ),
            )
            current.add_module(
                "conv_3x3",
                nn.Conv2d(
                    in_channels=d_model,
                    out_channels=d_model,
                    kernel_size=3,
                    padding=1,
                    bias=use_bias,
                ),
            )
            self.convs.append(current)

        self.sam2_convs = None
        if add_sam2_neck:
            # Assumes sam2 neck is just a clone of the original neck
            self.sam2_convs = deepcopy(self.convs)

    def forward(
        self, tensor_list: List[torch.Tensor]
    ) -> Tuple[
        List[torch.Tensor],
        List[torch.Tensor],
        Optional[List[torch.Tensor]],
        Optional[List[torch.Tensor]],
    ]:
        xs = self.trunk(tensor_list)
        sam3_out, sam3_pos = [], []
        sam2_out, sam2_pos = None, None
        if self.sam2_convs is not None:
            sam2_out, sam2_pos = [], []
        x = xs[-1]  # simpleFPN
        for i in range(len(self.convs)):
            sam3_x_out = self.convs[i](x)
            sam3_pos_out = self.position_encoding(sam3_x_out).to(sam3_x_out.dtype)
            sam3_out.append(sam3_x_out)
            sam3_pos.append(sam3_pos_out)

            if self.sam2_convs is not None:
                sam2_x_out = self.sam2_convs[i](x)
                sam2_pos_out = self.position_encoding(sam2_x_out).to(sam2_x_out.dtype)
                sam2_out.append(sam2_x_out)
                sam2_pos.append(sam2_pos_out)
        return sam3_out, sam3_pos, sam2_out, sam2_pos


class Sam3TriViTDetNeck(nn.Module):
    def __init__(
        self,
        trunk: nn.Module,
        position_encoding: nn.Module,
        d_model: int,
        neck_norm=None,
        scale_factors=(4.0, 2.0, 1.0),
    ):
        """
        SimpleFPN neck with three heads (sam3, interactive, propagation).
        """
        super().__init__()
        self.trunk = trunk
        self.position_encoding = position_encoding
        self.convs = nn.ModuleList()

        self.scale_factors = scale_factors
        use_bias = neck_norm is None
        dim = self.trunk.channel_list[-1]

        for _, scale in enumerate(scale_factors):
            current = nn.Sequential()

            if scale == 4.0:
                current.add_module(
                    "dconv_2x2_0",
                    nn.ConvTranspose2d(dim, dim // 2, kernel_size=2, stride=2),
                )
                current.add_module(
                    "gelu",
                    nn.GELU(),
                )
                current.add_module(
                    "dconv_2x2_1",
                    nn.ConvTranspose2d(dim // 2, dim // 4, kernel_size=2, stride=2),
                )
                out_dim = dim // 4
            elif scale == 2.0:
                current.add_module(
                    "dconv_2x2",
                    nn.ConvTranspose2d(dim, dim // 2, kernel_size=2, stride=2),
                )
                out_dim = dim // 2
            elif scale == 1.0:
                out_dim = dim
            elif scale == 0.5:
                current.add_module(
                    "maxpool_2x2",
                    nn.MaxPool2d(kernel_size=2, stride=2),
                )
                out_dim = dim
            else:
                raise NotImplementedError(f"scale_factor={scale} is not supported yet.")

            current.add_module(
                "conv_1x1",
                nn.Conv2d(
                    in_channels=out_dim,
                    out_channels=d_model,
                    kernel_size=1,
                    bias=use_bias,
                ),
            )
            current.add_module(
                "conv_3x3",
                nn.Conv2d(
                    in_channels=d_model,
                    out_channels=d_model,
                    kernel_size=3,
                    padding=1,
                    bias=use_bias,
                ),
            )
            self.convs.append(current)

        # Assumes the new necks are just clones of the original neck
        self.interactive_convs = deepcopy(self.convs)
        self.propagation_convs = deepcopy(self.convs)

    def forward(
        self,
        tensor_list,
        *,
        need_sam3_out: bool = True,
        need_interactive_out: bool = True,
        need_propagation_out: bool = True,
    ):
        xs = self.trunk(tensor_list)
        sam3_out = []
        interactive_out = []
        propagation_out = []

        sam3_pos = []
        interactive_pos = []
        propagation_pos = []
        x = xs[-1]  # simpleFPN
        # OSS trunk returns plain tensors; onevision trunk returns NestedTensors.
        # Use getattr to handle both in a torch.compile-friendly way.
        x_data = getattr(x, "tensors", x)
        x_mask = getattr(x, "mask", None)
        for _, (conv, interactive_conv, propagation_conv) in enumerate(
            zip(self.convs, self.interactive_convs, self.propagation_convs)
        ):
            if need_sam3_out:
                sam3_conv_out = conv(x_data)
                sam3_x_out = NestedTensor(sam3_conv_out, x_mask)
                sam3_out.append(sam3_x_out)
                sam3_pos.append(
                    self.position_encoding(sam3_conv_out).to(sam3_conv_out.dtype)
                )

            if need_interactive_out:
                interactive_conv_out_t = interactive_conv(x_data)
                interactive_conv_out = NestedTensor(interactive_conv_out_t, x_mask)
                interactive_out.append(interactive_conv_out)
                interactive_pos.append(
                    self.position_encoding(interactive_conv_out_t).to(
                        interactive_conv_out_t.dtype
                    )
                )

            if need_propagation_out:
                propagation_conv_out = propagation_conv(x_data)
                propagation_x_out = NestedTensor(propagation_conv_out, x_mask)
                propagation_out.append(propagation_x_out)
                propagation_pos.append(
                    self.position_encoding(propagation_conv_out).to(
                        propagation_conv_out.dtype
                    )
                )

        return (
            sam3_out,
            sam3_pos,
            interactive_out,
            interactive_pos,
            propagation_out,
            propagation_pos,
        )



================================================
FILE: sam3/model/position_encoding.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

import math
from typing import Optional

import torch
from torch import nn


class PositionEmbeddingSine(nn.Module):
    """
    This is a more standard version of the position embedding, very similar to the one
    used by the Attention is all you need paper, generalized to work on images.
    """

    def __init__(
        self,
        num_pos_feats,
        temperature: int = 10000,
        normalize: bool = True,
        scale: Optional[float] = None,
        precompute_resolution: Optional[int] = None,
    ):
        super().__init__()
        assert num_pos_feats % 2 == 0, "Expecting even model width"
        self.num_pos_feats = num_pos_feats // 2
        self.temperature = temperature
        self.normalize = normalize
        if scale is not None and normalize is False:
            raise ValueError("normalize should be True if scale is passed")
        if scale is None:
            scale = 2 * math.pi
        self.scale = scale

        self.cache = {}
        # Precompute positional encodings under `precompute_resolution` to fill the cache
        # and avoid symbolic shape tracing errors in torch.compile in PyTorch 2.4 nightly.
        if precompute_resolution is not None:
            # We precompute pos enc for all strides used by both DualViTDetNeck and
            # TriViTDetNeck (scale_factors 4.0, 2.0, 1.0, 0.5 applied to backbone
            # output at stride 14 from 1008px input → 72x72).
            precompute_sizes = [
                (int(precompute_resolution // 3.5), int(precompute_resolution // 3.5)),
                (precompute_resolution // 4, precompute_resolution // 4),
                (int(precompute_resolution // 7), int(precompute_resolution // 7)),
                (precompute_resolution // 8, precompute_resolution // 8),
                (int(precompute_resolution // 14), int(precompute_resolution // 14)),
                (precompute_resolution // 16, precompute_resolution // 16),
                (int(precompute_resolution // 28), int(precompute_resolution // 28)),
                (precompute_resolution // 32, precompute_resolution // 32),
            ]
            for size in precompute_sizes:
                tensors = torch.zeros((1, 1) + size, device="cuda")
                self.forward(tensors)
                # further clone and detach it in the cache (just to be safe)
                self.cache[size] = self.cache[size].clone().detach()

    def _encode_xy(self, x, y):
        # The positions are expected to be normalized
        assert len(x) == len(y) and x.ndim == y.ndim == 1
        x_embed = x * self.scale
        y_embed = y * self.scale

        dim_t = torch.arange(self.num_pos_feats, dtype=torch.float32, device=x.device)
        dim_t = self.temperature ** (2 * (dim_t // 2) / self.num_pos_feats)

        pos_x = x_embed[:, None] / dim_t
        pos_y = y_embed[:, None] / dim_t
        pos_x = torch.stack(
            (pos_x[:, 0::2].sin(), pos_x[:, 1::2].cos()), dim=2
        ).flatten(1)
        pos_y = torch.stack(
            (pos_y[:, 0::2].sin(), pos_y[:, 1::2].cos()), dim=2
        ).flatten(1)
        return pos_x, pos_y

    @torch.no_grad()
    def encode_boxes(self, x, y, w, h):
        pos_x, pos_y = self._encode_xy(x, y)
        pos = torch.cat((pos_y, pos_x, h[:, None], w[:, None]), dim=1)
        return pos

    encode = encode_boxes  # Backwards compatibility

    @torch.no_grad()
    def encode_points(self, x, y, labels):
        (bx, nx), (by, ny), (bl, nl) = x.shape, y.shape, labels.shape
        assert bx == by and nx == ny and bx == bl and nx == nl
        pos_x, pos_y = self._encode_xy(x.flatten(), y.flatten())
        pos_x, pos_y = pos_x.reshape(bx, nx, -1), pos_y.reshape(by, ny, -1)
        pos = torch.cat((pos_y, pos_x, labels[:, :, None]), dim=2)
        return pos

    @torch.no_grad()
    def forward(self, x):
        cache_key = None
        cache_key = (x.shape[-2], x.shape[-1])
        if cache_key in self.cache:
            return self.cache[cache_key][None].repeat(x.shape[0], 1, 1, 1)
        y_embed = (
            torch.arange(1, x.shape[-2] + 1, dtype=torch.float32, device=x.device)
            .view(1, -1, 1)
            .repeat(x.shape[0], 1, x.shape[-1])
        )
        x_embed = (
            torch.arange(1, x.shape[-1] + 1, dtype=torch.float32, device=x.device)
            .view(1, 1, -1)
            .repeat(x.shape[0], x.shape[-2], 1)
        )

        if self.normalize:
            eps = 1e-6
            y_embed = y_embed / (y_embed[:, -1:, :] + eps) * self.scale
            x_embed = x_embed / (x_embed[:, :, -1:] + eps) * self.scale

        dim_t = torch.arange(self.num_pos_feats, dtype=torch.float32, device=x.device)
        dim_t = self.temperature ** (2 * (dim_t // 2) / self.num_pos_feats)

        pos_x = x_embed[:, :, :, None] / dim_t
        pos_y = y_embed[:, :, :, None] / dim_t
        pos_x = torch.stack(
            (pos_x[:, :, :, 0::2].sin(), pos_x[:, :, :, 1::2].cos()), dim=4
        ).flatten(3)
        pos_y = torch.stack(
            (pos_y[:, :, :, 0::2].sin(), pos_y[:, :, :, 1::2].cos()), dim=4
        ).flatten(3)
        pos = torch.cat((pos_y, pos_x), dim=3).permute(0, 3, 1, 2)
        if cache_key is not None:
            self.cache[cache_key] = pos[0]
        return pos



================================================
FILE: sam3/model/sam1_task_predictor.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved
# All rights reserved.

# pyre-unsafe

# This source code is licensed under the license found in the
# LICENSE file in the root directory of this source tree.

import logging
from typing import List, Optional, Tuple, Union

import numpy as np
import torch
import torch.nn as nn
from PIL.Image import Image
from sam3.model.sam3_tracker_base import Sam3TrackerBase
from sam3.model.utils.sam1_utils import SAM2Transforms


# Adapted from https://github.com/facebookresearch/sam2/blob/main/sam2/sam2_image_predictor.py
class SAM3InteractiveImagePredictor(nn.Module):
    def __init__(
        self,
        sam_model: Sam3TrackerBase,
        mask_threshold=0.0,
        max_hole_area=256.0,
        max_sprinkle_area=0.0,
        **kwargs,
    ) -> None:
        """
        Uses SAM-3 to calculate the image embedding for an image, and then
        allow repeated, efficient mask prediction given prompts.

        Arguments:
          sam_model : The model to use for mask prediction.
          mask_threshold (float): The threshold to use when converting mask logits
            to binary masks. Masks are thresholded at 0 by default.
          max_hole_area (int): If max_hole_area > 0, we fill small holes in up to
            the maximum area of max_hole_area in low_res_masks.
          max_sprinkle_area (int): If max_sprinkle_area > 0, we remove small sprinkles up to
            the maximum area of max_sprinkle_area in low_res_masks.
        """
        super().__init__()
        self.model = sam_model
        self._transforms = SAM2Transforms(
            resolution=self.model.image_size,
            mask_threshold=mask_threshold,
            max_hole_area=max_hole_area,
            max_sprinkle_area=max_sprinkle_area,
        )

        # Predictor state
        self._is_image_set = False
        self._features = None
        self._orig_hw = None
        # Whether the predictor is set for single image or a batch of images
        self._is_batch = False

        # Predictor config
        self.mask_threshold = mask_threshold

        # Spatial dim for backbone feature maps
        self._bb_feat_sizes = [
            (288, 288),
            (144, 144),
            (72, 72),
        ]

    @torch.no_grad()
    def set_image(
        self,
        image: Union[np.ndarray, Image],
    ) -> None:
        """
        Calculates the image embeddings for the provided image, allowing
        masks to be predicted with the 'predict' method.

        Arguments:
          image (np.ndarray or PIL Image): The input image to embed in RGB format. The image should be in HWC format if np.ndarray, or WHC format if PIL Image
          with pixel values in [0, 255].
          image_format (str): The color format of the image, in ['RGB', 'BGR'].
        """
        self.reset_predictor()
        # Transform the image to the form expected by the model
        if isinstance(image, np.ndarray):
            logging.info("For numpy array image, we assume (HxWxC) format")
            self._orig_hw = [image.shape[:2]]
        elif isinstance(image, Image):
            w, h = image.size
            self._orig_hw = [(h, w)]
        else:
            raise NotImplementedError("Image format not supported")

        input_image = self._transforms(image)
        input_image = input_image[None, ...].to(self.device)

        assert len(input_image.shape) == 4 and input_image.shape[1] == 3, (
            f"input_image must be of size 1x3xHxW, got {input_image.shape}"
        )
        logging.info("Computing image embeddings for the provided image...")
        backbone_out = self.model.forward_image(input_image)
        (
            _,
            vision_feats,
            _,
            _,
        ) = self.model._prepare_backbone_features(backbone_out)
        # Add no_mem_embed, which is added to the lowest rest feat. map during training on videos
        vision_feats[-1] = vision_feats[-1] + self.model.no_mem_embed

        feats = [
            feat.permute(1, 2, 0).view(1, -1, *feat_size)
            for feat, feat_size in zip(vision_feats[::-1], self._bb_feat_sizes[::-1])
        ][::-1]
        self._features = {"image_embed": feats[-1], "high_res_feats": feats[:-1]}
        self._is_image_set = True
        logging.info("Image embeddings computed.")

    @torch.no_grad()
    def set_image_batch(
        self,
        image_list: List[Union[np.ndarray]],
    ) -> None:
        """
        Calculates the image embeddings for the provided image batch, allowing
        masks to be predicted with the 'predict_batch' method.

        Arguments:
          image_list (List[np.ndarray]): The input images to embed in RGB format. The image should be in HWC format if np.ndarray
          with pixel values in [0, 255].
        """
        self.reset_predictor()
        assert isinstance(image_list, list)
        self._orig_hw = []
        for image in image_list:
            assert isinstance(image, np.ndarray), (
                "Images are expected to be an np.ndarray in RGB format, and of shape  HWC"
            )
            self._orig_hw.append(image.shape[:2])
        # Transform the image to the form expected by the model
        img_batch = self._transforms.forward_batch(image_list)
        img_batch = img_batch.to(self.device)
        batch_size = img_batch.shape[0]
        assert len(img_batch.shape) == 4 and img_batch.shape[1] == 3, (
            f"img_batch must be of size Bx3xHxW, got {img_batch.shape}"
        )
        logging.info("Computing image embeddings for the provided images...")
        backbone_out = self.model.forward_image(img_batch)
        (
            _,
            vision_feats,
            _,
            _,
        ) = self.model._prepare_backbone_features(backbone_out)
        # Add no_mem_embed, which is added to the lowest rest feat. map during training on videos
        vision_feats[-1] = vision_feats[-1] + self.model.no_mem_embed

        feats = [
            feat.permute(1, 2, 0).view(batch_size, -1, *feat_size)
            for feat, feat_size in zip(vision_feats[::-1], self._bb_feat_sizes[::-1])
        ][::-1]
        self._features = {"image_embed": feats[-1], "high_res_feats": feats[:-1]}
        self._is_image_set = True
        self._is_batch = True
        logging.info("Image embeddings computed.")

    def predict_batch(
        self,
        point_coords_batch: List[np.ndarray] = None,
        point_labels_batch: List[np.ndarray] = None,
        box_batch: List[np.ndarray] = None,
        mask_input_batch: List[np.ndarray] = None,
        multimask_output: bool = True,
        return_logits: bool = False,
        normalize_coords=True,
    ) -> Tuple[List[np.ndarray], List[np.ndarray], List[np.ndarray]]:
        """This function is very similar to predict(...), however it is used for batched mode, when the model is expected to generate predictions on multiple images.
        It returns a tuple of lists of masks, ious, and low_res_masks_logits.
        """
        assert self._is_batch, "This function should only be used when in batched mode"
        if not self._is_image_set:
            raise RuntimeError(
                "An image must be set with .set_image_batch(...) before mask prediction."
            )
        num_images = len(self._features["image_embed"])
        all_masks = []
        all_ious = []
        all_low_res_masks = []
        for img_idx in range(num_images):
            # Transform input prompts
            point_coords = (
                point_coords_batch[img_idx] if point_coords_batch is not None else None
            )
            point_labels = (
                point_labels_batch[img_idx] if point_labels_batch is not None else None
            )
            box = box_batch[img_idx] if box_batch is not None else None
            mask_input = (
                mask_input_batch[img_idx] if mask_input_batch is not None else None
            )
            mask_input, unnorm_coords, labels, unnorm_box = self._prep_prompts(
                point_coords,
                point_labels,
                box,
                mask_input,
                normalize_coords,
                img_idx=img_idx,
            )
            masks, iou_predictions, low_res_masks = self._predict(
                unnorm_coords,
                labels,
                unnorm_box,
                mask_input,
                multimask_output,
                return_logits=return_logits,
                img_idx=img_idx,
            )
            masks_np = masks.squeeze(0).float().detach().cpu().numpy()
            iou_predictions_np = (
                iou_predictions.squeeze(0).float().detach().cpu().numpy()
            )
            low_res_masks_np = low_res_masks.squeeze(0).float().detach().cpu().numpy()
            all_masks.append(masks_np)
            all_ious.append(iou_predictions_np)
            all_low_res_masks.append(low_res_masks_np)

        return all_masks, all_ious, all_low_res_masks

    def predict(
        self,
        point_coords: Optional[np.ndarray] = None,
        point_labels: Optional[np.ndarray] = None,
        box: Optional[np.ndarray] = None,
        mask_input: Optional[np.ndarray] = None,
        multimask_output: bool = True,
        return_logits: bool = False,
        normalize_coords=True,
    ) -> Tuple[np.ndarray, np.ndarray, np.ndarray]:
        """
        Predict masks for the given input prompts, using the currently set image.

        Arguments:
          point_coords (np.ndarray or None): A Nx2 array of point prompts to the
            model. Each point is in (X,Y) in pixels.
          point_labels (np.ndarray or None): A length N array of labels for the
            point prompts. 1 indicates a foreground point and 0 indicates a
            background point.
          box (np.ndarray or None): A length 4 array given a box prompt to the
            model, in XYXY format.
          mask_input (np.ndarray): A low resolution mask input to the model, typically
            coming from a previous prediction iteration. Has form 1xHxW, where
            for SAM, H=W=256.
          multimask_output (bool): If true, the model will return three masks.
            For ambiguous input prompts (such as a single click), this will often
            produce better masks than a single prediction. If only a single
            mask is needed, the model's predicted quality score can be used
            to select the best mask. For non-ambiguous prompts, such as multiple
            input prompts, multimask_output=False can give better results.
          return_logits (bool): If true, returns un-thresholded masks logits
            instead of a binary mask.
          normalize_coords (bool): If true, the point coordinates will be normalized to the range [0,1] and point_coords is expected to be wrt. image dimensions.

        Returns:
          (np.ndarray): The output masks in CxHxW format, where C is the
            number of masks, and (H, W) is the original image size.
          (np.ndarray): An array of length C containing the model's
            predictions for the quality of each mask.
          (np.ndarray): An array of shape CxHxW, where C is the number
            of masks and H=W=256. These low resolution logits can be passed to
            a subsequent iteration as mask input.
        """
        if not self._is_image_set:
            raise RuntimeError(
                "An image must be set with .set_image(...) before mask prediction."
            )

        # Transform input prompts

        mask_input, unnorm_coords, labels, unnorm_box = self._prep_prompts(
            point_coords, point_labels, box, mask_input, normalize_coords
        )

        masks, iou_predictions, low_res_masks = self._predict(
            unnorm_coords,
            labels,
            unnorm_box,
            mask_input,
            multimask_output,
            return_logits=return_logits,
        )

        masks_np = masks.squeeze(0).float().detach().cpu().numpy()
        iou_predictions_np = iou_predictions.squeeze(0).float().detach().cpu().numpy()
        low_res_masks_np = low_res_masks.squeeze(0).float().detach().cpu().numpy()
        return masks_np, iou_predictions_np, low_res_masks_np

    def _prep_prompts(
        self, point_coords, point_labels, box, mask_logits, normalize_coords, img_idx=-1
    ):
        unnorm_coords, labels, unnorm_box, mask_input = None, None, None, None
        if point_coords is not None:
            assert point_labels is not None, (
                "point_labels must be supplied if point_coords is supplied."
            )
            point_coords = torch.as_tensor(
                point_coords, dtype=torch.float, device=self.device
            )
            unnorm_coords = self._transforms.transform_coords(
                point_coords, normalize=normalize_coords, orig_hw=self._orig_hw[img_idx]
            )
            labels = torch.as_tensor(point_labels, dtype=torch.int, device=self.device)
            if len(unnorm_coords.shape) == 2:
                unnorm_coords, labels = unnorm_coords[None, ...], labels[None, ...]
        if box is not None:
            box = torch.as_tensor(box, dtype=torch.float, device=self.device)
            unnorm_box = self._transforms.transform_boxes(
                box, normalize=normalize_coords, orig_hw=self._orig_hw[img_idx]
            )  # Bx2x2
        if mask_logits is not None:
            mask_input = torch.as_tensor(
                mask_logits, dtype=torch.float, device=self.device
            )
            if len(mask_input.shape) == 3:
                mask_input = mask_input[None, :, :, :]
        return mask_input, unnorm_coords, labels, unnorm_box

    @torch.no_grad()
    def _predict(
        self,
        point_coords: Optional[torch.Tensor],
        point_labels: Optional[torch.Tensor],
        boxes: Optional[torch.Tensor] = None,
        mask_input: Optional[torch.Tensor] = None,
        multimask_output: bool = True,
        return_logits: bool = False,
        img_idx: int = -1,
    ) -> Tuple[torch.Tensor, torch.Tensor, torch.Tensor]:
        """
        Predict masks for the given input prompts, using the currently set image.
        Input prompts are batched torch tensors and are expected to already be
        transformed to the input frame using SAM2Transforms.

        Arguments:
          point_coords (torch.Tensor or None): A BxNx2 array of point prompts to the
            model. Each point is in (X,Y) in pixels.
          point_labels (torch.Tensor or None): A BxN array of labels for the
            point prompts. 1 indicates a foreground point and 0 indicates a
            background point.
          boxes (np.ndarray or None): A Bx4 array given a box prompt to the
            model, in XYXY format.
          mask_input (np.ndarray): A low resolution mask input to the model, typically
            coming from a previous prediction iteration. Has form Bx1xHxW, where
            for SAM, H=W=256. Masks returned by a previous iteration of the
            predict method do not need further transformation.
          multimask_output (bool): If true, the model will return three masks.
            For ambiguous input prompts (such as a single click), this will often
            produce better masks than a single prediction. If only a single
            mask is needed, the model's predicted quality score can be used
            to select the best mask. For non-ambiguous prompts, such as multiple
            input prompts, multimask_output=False can give better results.
          return_logits (bool): If true, returns un-thresholded masks logits
            instead of a binary mask.

        Returns:
          (torch.Tensor): The output masks in BxCxHxW format, where C is the
            number of masks, and (H, W) is the original image size.
          (torch.Tensor): An array of shape BxC containing the model's
            predictions for the quality of each mask.
          (torch.Tensor): An array of shape BxCxHxW, where C is the number
            of masks and H=W=256. These low res logits can be passed to
            a subsequent iteration as mask input.
        """
        if not self._is_image_set:
            raise RuntimeError(
                "An image must be set with .set_image(...) before mask prediction."
            )

        if point_coords is not None:
            concat_points = (point_coords, point_labels)
        else:
            concat_points = None

        # Embed prompts
        if boxes is not None:
            box_coords = boxes.reshape(-1, 2, 2)
            box_labels = torch.tensor([[2, 3]], dtype=torch.int, device=boxes.device)
            box_labels = box_labels.repeat(boxes.size(0), 1)
            # we merge "boxes" and "points" into a single "concat_points" input (where
            # boxes are added at the beginning) to sam_prompt_encoder
            if concat_points is not None:
                concat_coords = torch.cat([box_coords, concat_points[0]], dim=1)
                concat_labels = torch.cat([box_labels, concat_points[1]], dim=1)
                concat_points = (concat_coords, concat_labels)
            else:
                concat_points = (box_coords, box_labels)

        sparse_embeddings, dense_embeddings = self.model.sam_prompt_encoder(
            points=concat_points,
            boxes=None,
            masks=mask_input,
        )

        # Predict masks
        batched_mode = (
            concat_points is not None and concat_points[0].shape[0] > 1
        )  # multi object prediction
        high_res_features = [
            feat_level[img_idx].unsqueeze(0)
            for feat_level in self._features["high_res_feats"]
        ]
        low_res_masks, iou_predictions, _, _ = self.model.sam_mask_decoder(
            image_embeddings=self._features["image_embed"][img_idx].unsqueeze(0),
            image_pe=self.model.sam_prompt_encoder.get_dense_pe(),
            sparse_prompt_embeddings=sparse_embeddings,
            dense_prompt_embeddings=dense_embeddings,
            multimask_output=multimask_output,
            repeat_image=batched_mode,
            high_res_features=high_res_features,
        )

        # Upscale the masks to the original image resolution
        masks = self._transforms.postprocess_masks(
            low_res_masks, self._orig_hw[img_idx]
        )
        low_res_masks = torch.clamp(low_res_masks, -32.0, 32.0)
        if not return_logits:
            masks = masks > self.mask_threshold

        return masks, iou_predictions, low_res_masks

    def get_image_embedding(self) -> torch.Tensor:
        """
        Returns the image embeddings for the currently set image, with
        shape 1xCxHxW, where C is the embedding dimension and (H,W) are
        the embedding spatial dimension of SAM (typically C=256, H=W=64).
        """
        if not self._is_image_set:
            raise RuntimeError(
                "An image must be set with .set_image(...) to generate an embedding."
            )
        assert self._features is not None, (
            "Features must exist if an image has been set."
        )
        return self._features["image_embed"]

    @property
    def device(self) -> torch.device:
        return self.model.device

    def reset_predictor(self) -> None:
        """
        Resets the image embeddings and other state variables.
        """
        self._is_image_set = False
        self._features = None
        self._orig_hw = None
        self._is_batch = False



================================================
FILE: sam3/model/sam3_base_predictor.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

"""
Base predictor class shared by SAM3 and SAM3.1 (multiplex) video predictors.

Provides the common handle_request/handle_stream_request API and session management.
Subclasses only need to override methods where their behavior differs.
"""

import gc
import time
import uuid
from typing import Dict, List, Optional

import torch
from sam3.logger import get_logger

logger = get_logger(__name__)


class Sam3BasePredictor:
    """
    Base class for SAM3 video predictors. Provides:
    - Session management (start, reset, close)
    - Request dispatch (handle_request / handle_stream_request)
    - Common add_prompt / propagate_in_video / remove_object / reset_session / close_session

    Subclasses must set `self.model` and `self._all_inference_states` before use.
    """

    def __init__(self):
        # Subclasses must populate these
        self.model = None
        self._all_inference_states: Dict[str, dict] = {}

    # ── Request dispatch ──────────────────────────────────────────────

    @torch.inference_mode()
    def handle_request(self, request):
        """Dispatch a request based on its type."""
        request_type = request["type"]
        if request_type == "start_session":
            return self.start_session(
                resource_path=request["resource_path"],
                session_id=request.get("session_id", None),
                offload_video_to_cpu=request.get("offload_video_to_cpu", False),
            )
        elif request_type == "add_prompt":
            return self.add_prompt(
                session_id=request["session_id"],
                frame_idx=request["frame_index"],
                text=request.get("text", None),
                points=request.get("points", None),
                point_labels=request.get("point_labels", None),
                clear_old_points=request.get("clear_old_points", True),
                bounding_boxes=request.get("bounding_boxes", None),
                bounding_box_labels=request.get("bounding_box_labels", None),
                clear_old_boxes=request.get("clear_old_boxes", True),
                output_prob_thresh=request.get(
                    "output_prob_thresh",
                    getattr(self, "default_output_prob_thresh", 0.5),
                ),
                obj_id=request.get("obj_id", None),
            )
        elif request_type == "remove_object":
            return self.remove_object(
                session_id=request["session_id"],
                frame_idx=request.get("frame_index", 0),
                obj_id=request["obj_id"],
            )
        elif request_type == "reset_session":
            return self.reset_session(session_id=request["session_id"])
        elif request_type == "cancel_propagation":
            return self.cancel_propagation(session_id=request["session_id"])
        elif request_type == "close_session":
            return self.close_session(
                session_id=request["session_id"],
                run_gc_collect=request.get("run_gc_collect", True),
            )
        else:
            raise RuntimeError(f"invalid request type: {request_type}")

    @torch.inference_mode()
    def handle_stream_request(self, request):
        """Dispatch a stream request based on its type."""
        request_type = request["type"]
        if request_type == "propagate_in_video":
            yield from self.propagate_in_video(
                session_id=request["session_id"],
                propagation_direction=request.get("propagation_direction", "both"),
                start_frame_idx=request.get("start_frame_index", None),
                max_frame_num_to_track=request.get("max_frame_num_to_track", None),
                output_prob_thresh=request.get(
                    "output_prob_thresh",
                    getattr(self, "default_output_prob_thresh", 0.5),
                ),
            )
        else:
            raise RuntimeError(f"invalid request type: {request_type}")

    # ── Session management ────────────────────────────────────────────

    def start_session(
        self,
        resource_path,
        session_id=None,
        offload_video_to_cpu=False,
    ):
        """Start a new inference session on a video directory or path."""
        init_kwargs = dict(
            resource_path=resource_path,
            offload_video_to_cpu=offload_video_to_cpu,
        )
        if hasattr(self, "async_loading_frames"):
            init_kwargs["async_loading_frames"] = self.async_loading_frames
        if hasattr(self, "video_loader_type"):
            init_kwargs["video_loader_type"] = self.video_loader_type
        inference_state = self.model.init_state(**init_kwargs)

        if not session_id:
            session_id = str(uuid.uuid4())
        self._all_inference_states[session_id] = {
            "state": inference_state,
            "session_id": session_id,
            "start_time": time.time(),
            "last_use_time": time.time(),
        }
        logger.info(f"started new session {session_id}")
        return {"session_id": session_id}

    def add_prompt(
        self,
        session_id: str,
        frame_idx: int,
        text: Optional[str] = None,
        points=None,
        point_labels=None,
        clear_old_points: bool = True,
        bounding_boxes=None,
        bounding_box_labels=None,
        clear_old_boxes: bool = True,
        output_prob_thresh: float = 0.5,
        obj_id: Optional[int] = None,
    ):
        """Add text, box and/or point prompt on a specific video frame."""
        session = self._get_session(session_id)
        inference_state = session["state"]
        self._extend_expiration_time(session)

        # Convert lists to tensors if needed
        if points is not None and not isinstance(points, torch.Tensor):
            points = torch.tensor(points, dtype=torch.float32)
        if point_labels is not None and not isinstance(point_labels, torch.Tensor):
            point_labels = torch.tensor(point_labels, dtype=torch.int32)
        if bounding_boxes is not None and not isinstance(bounding_boxes, torch.Tensor):
            bounding_boxes = torch.tensor(bounding_boxes, dtype=torch.float32)
        if bounding_box_labels is not None and not isinstance(
            bounding_box_labels, torch.Tensor
        ):
            bounding_box_labels = torch.tensor(bounding_box_labels, dtype=torch.int32)

        kwargs = dict(
            inference_state=inference_state,
            frame_idx=frame_idx,
            text_str=text,
            points=points,
            point_labels=point_labels,
            clear_old_points=clear_old_points,
            boxes_xywh=bounding_boxes,
            box_labels=bounding_box_labels,
            clear_old_boxes=clear_old_boxes,
            output_prob_thresh=output_prob_thresh,
        )
        if obj_id is not None:
            kwargs["obj_id"] = obj_id

        # Filter kwargs to only pass what the model accepts
        # (SAM3 has a simpler add_prompt than SAM3.1)
        import inspect

        sig = inspect.signature(self.model.add_prompt)
        valid_params = set(sig.parameters.keys())
        filtered_kwargs = {k: v for k, v in kwargs.items() if k in valid_params}

        frame_idx, outputs = self.model.add_prompt(**filtered_kwargs)
        return {"frame_index": frame_idx, "outputs": outputs}

    def remove_object(
        self,
        session_id: str,
        frame_idx: int = 0,
        obj_id: int = 0,
        is_user_action: bool = True,
    ):
        """Remove an object from tracking."""
        session = self._get_session(session_id)
        inference_state = session["state"]
        self._extend_expiration_time(session)

        result = self.model.remove_object(
            inference_state, obj_id, frame_idx=frame_idx, is_user_action=is_user_action
        )
        # Handle both return conventions
        if result is None or (isinstance(result, tuple) and result[1] is None):
            import numpy as np

            out_obj_ids = torch.zeros(0, dtype=torch.int64)
            out_binary_masks = torch.zeros(
                0,
                inference_state["orig_height"],
                inference_state["orig_width"],
                dtype=torch.bool,
            )
            out_boxes_xywh = torch.zeros(0, 4, dtype=torch.float32)
            outputs = {
                "out_obj_ids": out_obj_ids.cpu().numpy(),
                "out_boxes_xywh": out_boxes_xywh.cpu().numpy(),
                "out_binary_masks": out_binary_masks.cpu().numpy(),
            }
        elif isinstance(result, tuple):
            _, outputs = result
        else:
            outputs = result
        return {"frame_index": frame_idx, "outputs": outputs}

    def cancel_propagation(self, session_id):
        """Cancel any ongoing propagation. No-op if not supported by the model."""
        session = self._get_session(session_id)
        inference_state = session["state"]
        self._extend_expiration_time(session)
        if hasattr(self.model, "cancel_propagation"):
            self.model.cancel_propagation(inference_state)
        return {"is_success": True}

    def propagate_in_video(
        self,
        session_id,
        propagation_direction="both",
        start_frame_idx=None,
        max_frame_num_to_track=None,
        output_prob_thresh=0.5,
        **kwargs,
    ):
        """Propagate the added prompts to get results on all video frames."""
        try:
            session = self._get_session(session_id)
            inference_state = session["state"]
            self._extend_expiration_time(session)
            if propagation_direction not in ["both", "forward", "backward"]:
                raise ValueError(
                    f"invalid propagation direction: {propagation_direction}"
                )

            propagate_kwargs = dict(
                inference_state=inference_state,
                start_frame_idx=start_frame_idx,
                max_frame_num_to_track=max_frame_num_to_track,
            )
            # Only pass output_prob_thresh / extra kwargs if the model supports them
            import inspect

            sig = inspect.signature(self.model.propagate_in_video)
            if "output_prob_thresh" in sig.parameters:
                propagate_kwargs["output_prob_thresh"] = output_prob_thresh
            for k, v in kwargs.items():
                if k in sig.parameters:
                    propagate_kwargs[k] = v

            # Forward propagation
            if propagation_direction in ["both", "forward"]:
                for frame_idx, outputs in self.model.propagate_in_video(
                    **propagate_kwargs,
                    reverse=False,
                ):
                    yield {"frame_index": frame_idx, "outputs": outputs}
            # Backward propagation
            if propagation_direction in ["both", "backward"]:
                for frame_idx, outputs in self.model.propagate_in_video(
                    **propagate_kwargs,
                    reverse=True,
                ):
                    yield {"frame_index": frame_idx, "outputs": outputs}
        finally:
            logger.info(f"propagation ended in session {session_id}")

    def reset_session(self, session_id):
        """Reset the session to its initial state."""
        session = self._get_session(session_id)
        inference_state = session["state"]
        self._extend_expiration_time(session)
        self.model.reset_state(inference_state)
        return {"is_success": True}

    def close_session(self, session_id, run_gc_collect=True):
        """Close a session. Idempotent."""
        session = self._all_inference_states.pop(session_id, None)
        if session is None:
            logger.warning(f"cannot close session {session_id} as it does not exist")
        else:
            del session
            if run_gc_collect:
                gc.collect()
            logger.info(f"removed session {session_id}")
        return {"is_success": True}

    def _get_session(self, session_id):
        session = self._all_inference_states.get(session_id, None)
        if session is None:
            raise RuntimeError(
                f"Cannot find session {session_id}; it might have expired"
            )
        return session

    def _extend_expiration_time(self, session):
        """Update last-use time for session expiration tracking."""
        session["last_use_time"] = time.time()

    def shutdown(self):
        """Shutdown the predictor and clear all sessions."""
        self._all_inference_states.clear()



================================================
FILE: sam3/model/sam3_image.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

import os
from copy import deepcopy
from typing import Dict, List, Optional, Tuple

import numpy as np
import torch
from sam3.model.model_misc import SAM3Output
from sam3.model.sam1_task_predictor import SAM3InteractiveImagePredictor
from sam3.model.vl_combiner import SAM3VLBackbone
from sam3.perflib.nms import nms_masks
from sam3.train.data.collator import BatchedDatapoint

from .act_ckpt_utils import activation_ckpt_wrapper
from .box_ops import box_cxcywh_to_xyxy
from .data_misc import FindStage
from .geometry_encoders import Prompt
from .model_misc import inverse_sigmoid


def _update_out(out, out_name, out_value, auxiliary=True, update_aux=True):
    out[out_name] = out_value[-1] if auxiliary else out_value
    if auxiliary and update_aux:
        if "aux_outputs" not in out:
            out["aux_outputs"] = [{} for _ in range(len(out_value) - 1)]
        assert len(out["aux_outputs"]) == len(out_value) - 1
        for aux_output, aux_value in zip(out["aux_outputs"], out_value[:-1]):
            aux_output[out_name] = aux_value


class Sam3Image(torch.nn.Module):
    TEXT_ID_FOR_TEXT = 0
    TEXT_ID_FOR_VISUAL = 1
    TEXT_ID_FOR_GEOMETRIC = 2

    def __init__(
        self,
        backbone: SAM3VLBackbone,
        transformer,
        input_geometry_encoder,
        segmentation_head=None,
        num_feature_levels=1,
        o2m_mask_predict=True,
        dot_prod_scoring=None,
        use_instance_query: bool = True,
        multimask_output: bool = True,
        use_act_checkpoint_seg_head: bool = True,
        interactivity_in_encoder: bool = True,
        matcher=None,
        use_dot_prod_scoring=True,
        supervise_joint_box_scores: bool = False,  # only relevant if using presence token/score
        detach_presence_in_joint_score: bool = False,  # only relevant if using presence token/score
        separate_scorer_for_instance: bool = False,
        num_interactive_steps_val: int = 0,
        inst_interactive_predictor: SAM3InteractiveImagePredictor = None,
        **kwargs,
    ):
        super().__init__()
        self.backbone = backbone
        self.geometry_encoder = input_geometry_encoder
        self.transformer = transformer
        self.hidden_dim = transformer.d_model
        self.num_feature_levels = num_feature_levels
        self.segmentation_head = segmentation_head

        self.o2m_mask_predict = o2m_mask_predict

        self.dot_prod_scoring = dot_prod_scoring
        self.use_act_checkpoint_seg_head = use_act_checkpoint_seg_head
        self.interactivity_in_encoder = interactivity_in_encoder
        self.matcher = matcher

        self.num_interactive_steps_val = num_interactive_steps_val
        self.use_dot_prod_scoring = use_dot_prod_scoring

        if self.use_dot_prod_scoring:
            assert dot_prod_scoring is not None
            self.dot_prod_scoring = dot_prod_scoring
            self.instance_dot_prod_scoring = None
            if separate_scorer_for_instance:
                self.instance_dot_prod_scoring = deepcopy(dot_prod_scoring)
        else:
            self.class_embed = torch.nn.Linear(self.hidden_dim, 1)
            self.instance_class_embed = None
            if separate_scorer_for_instance:
                self.instance_class_embed = deepcopy(self.class_embed)

        self.supervise_joint_box_scores = supervise_joint_box_scores
        self.detach_presence_in_joint_score = detach_presence_in_joint_score

        # verify the number of queries for O2O and O2M
        num_o2o_static = self.transformer.decoder.num_queries
        num_o2m_static = self.transformer.decoder.num_o2m_queries
        assert num_o2m_static == (num_o2o_static if self.transformer.decoder.dac else 0)
        self.dac = self.transformer.decoder.dac

        self.use_instance_query = use_instance_query
        self.multimask_output = multimask_output

        self.inst_interactive_predictor = inst_interactive_predictor

    @property
    def device(self):
        self._device = getattr(self, "_device", None) or next(self.parameters()).device
        return self._device

    def to(self, *args, **kwargs):
        # clear cached _device in case the model is moved to a different device
        self._device = None
        return super().to(*args, **kwargs)

    def _get_img_feats(self, backbone_out, img_ids):
        """Retrieve correct image features from backbone output."""
        if "backbone_fpn" in backbone_out:
            if "id_mapping" in backbone_out and backbone_out["id_mapping"] is not None:
                img_ids = backbone_out["id_mapping"][img_ids]
                # If this assert fails, it likely means we're requesting different img_ids (perhaps a different frame?)
                # We currently don't expect this to happen. We could technically trigger a recompute here,
                # but likely at the cost of a cpu<->gpu sync point, which would deteriorate perf
                torch._assert_async((img_ids >= 0).all())

            vis_feats = backbone_out["backbone_fpn"][-self.num_feature_levels :]
            vis_pos_enc = backbone_out["vision_pos_enc"][-self.num_feature_levels :]
            vis_feat_sizes = [x.shape[-2:] for x in vis_pos_enc]  # (H, W) shapes
            # index and flatten visual features NxCxHxW => HWxNxC (batch-first => seq-first)
            img_feats = [x[img_ids].flatten(2).permute(2, 0, 1) for x in vis_feats]
            img_pos_embeds = [
                x[img_ids].flatten(2).permute(2, 0, 1) for x in vis_pos_enc
            ]
            return backbone_out, img_feats, img_pos_embeds, vis_feat_sizes

        # Image features not available in backbone output, so we compute them on the fly
        # This case likely occurs for video. In that case, we want to forward only the current frame
        img_batch = backbone_out["img_batch_all_stages"]
        if img_ids.numel() > 1:
            # Only forward backbone on unique image ids to avoid repetitive computation
            unique_ids, _ = torch.unique(img_ids, return_inverse=True)
        else:
            unique_ids, _ = img_ids, slice(None)
        # Compute the image features on those unique image ids
        # note: we allow using a list (or other indexable types) of tensors as img_batch
        # (e.g. for async frame loading in demo). In this case we index img_batch.tensors directly
        if isinstance(img_batch, torch.Tensor):
            image = img_batch[unique_ids]
        elif unique_ids.numel() == 1:
            image = img_batch[unique_ids.item()].unsqueeze(0)
        else:
            image = torch.stack([img_batch[i] for i in unique_ids.tolist()])
        # `img_batch` might be fp16 and offloaded to CPU
        image = image.to(dtype=torch.float32, device=self.device)
        # Next time we call this function, we want to remember which indices we computed
        id_mapping = torch.full(
            (len(img_batch),), -1, dtype=torch.long, device=self.device
        )
        id_mapping[unique_ids] = torch.arange(len(unique_ids), device=self.device)
        backbone_out = {
            **backbone_out,
            **self.backbone.forward_image(image),
            "id_mapping": id_mapping,
        }
        assert "backbone_fpn" in backbone_out
        return self._get_img_feats(backbone_out, img_ids=img_ids)

    def _encode_prompt(
        self,
        backbone_out,
        find_input,
        geometric_prompt,
        visual_prompt_embed=None,
        visual_prompt_mask=None,
        encode_text=True,
        prev_mask_pred=None,
    ):
        # index text features (note that regardless of early or late fusion, the batch size of
        # `txt_feats` is always the number of *prompts* in the encoder)
        txt_ids = find_input.text_ids
        txt_feats = backbone_out["language_features"][:, txt_ids]
        txt_masks = backbone_out["language_mask"][txt_ids]

        feat_tuple = self._get_img_feats(backbone_out, find_input.img_ids)
        backbone_out, img_feats, img_pos_embeds, vis_feat_sizes = feat_tuple

        if prev_mask_pred is not None:
            img_feats = [img_feats[-1] + prev_mask_pred]
        # Encode geometry
        geo_feats, geo_masks = self.geometry_encoder(
            geo_prompt=geometric_prompt,
            img_feats=img_feats,
            img_sizes=vis_feat_sizes,
            img_pos_embeds=img_pos_embeds,
        )
        if visual_prompt_embed is None:
            visual_prompt_embed = torch.zeros(
                (0, *geo_feats.shape[1:]), device=geo_feats.device
            )
            visual_prompt_mask = torch.zeros(
                (*geo_masks.shape[:-1], 0),
                device=geo_masks.device,
                dtype=geo_masks.dtype,
            )
        if encode_text:
            prompt = torch.cat([txt_feats, geo_feats, visual_prompt_embed], dim=0)
            prompt_mask = torch.cat([txt_masks, geo_masks, visual_prompt_mask], dim=1)
        else:
            prompt = torch.cat([geo_feats, visual_prompt_embed], dim=0)
            prompt_mask = torch.cat([geo_masks, visual_prompt_mask], dim=1)
        return prompt, prompt_mask, backbone_out

    def _run_encoder(
        self,
        backbone_out,
        find_input,
        prompt,
        prompt_mask,
        encoder_extra_kwargs: Optional[Dict] = None,
    ):
        feat_tuple = self._get_img_feats(backbone_out, find_input.img_ids)
        backbone_out, img_feats, img_pos_embeds, vis_feat_sizes = feat_tuple

        # Run the encoder
        prompt_pos_embed = torch.zeros_like(prompt)
        # make a copy of the image feature lists since the encoder may modify these lists in-place
        memory = self.transformer.encoder(
            src=img_feats.copy(),
            src_key_padding_mask=None,
            src_pos=img_pos_embeds.copy(),
            prompt=prompt,
            prompt_pos=prompt_pos_embed,
            prompt_key_padding_mask=prompt_mask,
            feat_sizes=vis_feat_sizes,
            encoder_extra_kwargs=encoder_extra_kwargs,
        )
        encoder_out = {
            # encoded image features
            "encoder_hidden_states": memory["memory"],
            "pos_embed": memory["pos_embed"],
            "padding_mask": memory["padding_mask"],
            "level_start_index": memory["level_start_index"],
            "spatial_shapes": memory["spatial_shapes"],
            "valid_ratios": memory["valid_ratios"],
            "vis_feat_sizes": vis_feat_sizes,
            # encoded text features (or other prompts)
            "prompt_before_enc": prompt,
            "prompt_after_enc": memory.get("memory_text", prompt),
            "prompt_mask": prompt_mask,
        }
        return backbone_out, encoder_out, feat_tuple

    def _run_decoder(
        self,
        pos_embed,
        memory,
        src_mask,
        out,
        prompt,
        prompt_mask,
        encoder_out,
    ):
        bs = memory.shape[1]
        query_embed = self.transformer.decoder.query_embed.weight
        tgt = query_embed.unsqueeze(1).repeat(1, bs, 1)

        apply_dac = self.transformer.decoder.dac and self.training
        hs, reference_boxes, dec_presence_out, dec_presence_feats = (
            self.transformer.decoder(
                tgt=tgt,
                memory=memory,
                memory_key_padding_mask=src_mask,
                pos=pos_embed,
                reference_boxes=None,
                level_start_index=encoder_out["level_start_index"],
                spatial_shapes=encoder_out["spatial_shapes"],
                valid_ratios=encoder_out["valid_ratios"],
                tgt_mask=None,
                memory_text=prompt,
                text_attention_mask=prompt_mask,
                apply_dac=apply_dac,
            )
        )
        hs = hs.transpose(1, 2)  # seq-first to batch-first
        reference_boxes = reference_boxes.transpose(1, 2)  # seq-first to batch-first
        if dec_presence_out is not None:
            # seq-first to batch-first
            dec_presence_out = dec_presence_out.transpose(1, 2)

        out["presence_feats"] = dec_presence_feats
        self._update_scores_and_boxes(
            out,
            hs,
            reference_boxes,
            prompt,
            prompt_mask,
            dec_presence_out=dec_presence_out,
        )
        return out, hs

    def _update_scores_and_boxes(
        self,
        out,
        hs,
        reference_boxes,
        prompt,
        prompt_mask,
        dec_presence_out=None,
        is_instance_prompt=False,
    ):
        apply_dac = self.transformer.decoder.dac and self.training
        num_o2o = (hs.size(2) // 2) if apply_dac else hs.size(2)
        num_o2m = hs.size(2) - num_o2o
        assert num_o2m == (num_o2o if apply_dac else 0)
        out["queries"] = hs[-1][:, :num_o2o]  # remove o2m queries if there are any
        # score prediction
        if self.use_dot_prod_scoring:
            dot_prod_scoring_head = self.dot_prod_scoring
            if is_instance_prompt and self.instance_dot_prod_scoring is not None:
                dot_prod_scoring_head = self.instance_dot_prod_scoring
            outputs_class = dot_prod_scoring_head(hs, prompt, prompt_mask)
        else:
            class_embed_head = self.class_embed
            if is_instance_prompt and self.instance_class_embed is not None:
                class_embed_head = self.instance_class_embed
            outputs_class = class_embed_head(hs)

        # box prediction
        box_head = self.transformer.decoder.bbox_embed
        if (
            is_instance_prompt
            and self.transformer.decoder.instance_bbox_embed is not None
        ):
            box_head = self.transformer.decoder.instance_bbox_embed
        anchor_box_offsets = box_head(hs)
        reference_boxes_inv_sig = inverse_sigmoid(reference_boxes)
        outputs_coord = (reference_boxes_inv_sig + anchor_box_offsets).sigmoid()
        outputs_boxes_xyxy = box_cxcywh_to_xyxy(outputs_coord)

        if dec_presence_out is not None:
            _update_out(
                out, "presence_logit_dec", dec_presence_out, update_aux=self.training
            )

        if self.supervise_joint_box_scores:
            assert dec_presence_out is not None
            prob_dec_presence_out = dec_presence_out.clone().sigmoid()
            if self.detach_presence_in_joint_score:
                prob_dec_presence_out = prob_dec_presence_out.detach()

            outputs_class = inverse_sigmoid(
                outputs_class.sigmoid() * prob_dec_presence_out.unsqueeze(2)
            ).clamp(min=-10.0, max=10.0)

        _update_out(
            out, "pred_logits", outputs_class[:, :, :num_o2o], update_aux=self.training
        )
        _update_out(
            out, "pred_boxes", outputs_coord[:, :, :num_o2o], update_aux=self.training
        )
        _update_out(
            out,
            "pred_boxes_xyxy",
            outputs_boxes_xyxy[:, :, :num_o2o],
            update_aux=self.training,
        )
        if num_o2m > 0 and self.training:
            _update_out(
                out,
                "pred_logits_o2m",
                outputs_class[:, :, num_o2o:],
                update_aux=self.training,
            )
            _update_out(
                out,
                "pred_boxes_o2m",
                outputs_coord[:, :, num_o2o:],
                update_aux=self.training,
            )
            _update_out(
                out,
                "pred_boxes_xyxy_o2m",
                outputs_boxes_xyxy[:, :, num_o2o:],
                update_aux=self.training,
            )

    def _run_segmentation_heads(
        self,
        out,
        backbone_out,
        img_ids,
        vis_feat_sizes,
        encoder_hidden_states,
        prompt,
        prompt_mask,
        hs,
    ):
        apply_dac = self.transformer.decoder.dac and self.training
        if self.segmentation_head is not None:
            num_o2o = (hs.size(2) // 2) if apply_dac else hs.size(2)
            num_o2m = hs.size(2) - num_o2o
            obj_queries = hs if self.o2m_mask_predict else hs[:, :, :num_o2o]
            seg_head_outputs = activation_ckpt_wrapper(self.segmentation_head)(
                backbone_feats=backbone_out["backbone_fpn"],
                obj_queries=obj_queries,
                image_ids=img_ids,
                encoder_hidden_states=encoder_hidden_states,
                act_ckpt_enable=self.training and self.use_act_checkpoint_seg_head,
                prompt=prompt,
                prompt_mask=prompt_mask,
            )
            aux_masks = False  # self.aux_loss and self.segmentation_head.aux_masks
            for k, v in seg_head_outputs.items():
                if k in self.segmentation_head.instance_keys:
                    _update_out(out, k, v[:, :num_o2o], auxiliary=aux_masks)
                    if (
                        self.o2m_mask_predict and num_o2m > 0
                    ):  # handle o2m mask prediction
                        _update_out(
                            out, f"{k}_o2m", v[:, num_o2o:], auxiliary=aux_masks
                        )
                else:
                    out[k] = v
        else:
            backbone_out.pop("backbone_fpn", None)

    def _get_best_mask(self, out):
        prev_mask_idx = out["pred_logits"].argmax(dim=1).squeeze(1)
        batch_idx = torch.arange(
            out["pred_logits"].shape[0], device=prev_mask_idx.device
        )
        prev_mask_pred = out["pred_masks"][batch_idx, prev_mask_idx][:, None]
        # Downsample mask to match image resolution.
        prev_mask_pred = self.geometry_encoder.mask_encoder.mask_downsampler(
            prev_mask_pred
        )
        prev_mask_pred = prev_mask_pred.flatten(-2).permute(2, 0, 1)

        return prev_mask_pred

    def forward_grounding(
        self,
        backbone_out,
        find_input,
        find_target,
        geometric_prompt: Prompt,
        **kwargs,
    ):
        with torch.profiler.record_function("SAM3Image._encode_prompt"):
            prompt, prompt_mask, backbone_out = self._encode_prompt(
                backbone_out, find_input, geometric_prompt
            )
        # Run the encoder
        with torch.profiler.record_function("SAM3Image._run_encoder"):
            backbone_out, encoder_out, _ = self._run_encoder(
                backbone_out, find_input, prompt, prompt_mask
            )
        out = {
            "encoder_hidden_states": encoder_out["encoder_hidden_states"],
            "prev_encoder_out": {
                "encoder_out": encoder_out,
                "backbone_out": backbone_out,
            },
        }

        # Run the decoder
        with torch.profiler.record_function("SAM3Image._run_decoder"):
            out, hs = self._run_decoder(
                memory=out["encoder_hidden_states"],
                pos_embed=encoder_out["pos_embed"],
                src_mask=encoder_out["padding_mask"],
                out=out,
                prompt=prompt,
                prompt_mask=prompt_mask,
                encoder_out=encoder_out,
            )

        # Run segmentation heads
        with torch.profiler.record_function("SAM3Image._run_segmentation_heads"):
            # Apply id_mapping to img_ids if backbone features were recomputed
            seg_img_ids = find_input.img_ids
            if "id_mapping" in backbone_out and backbone_out["id_mapping"] is not None:
                seg_img_ids = backbone_out["id_mapping"][seg_img_ids]
            self._run_segmentation_heads(
                out=out,
                backbone_out=backbone_out,
                img_ids=seg_img_ids,
                vis_feat_sizes=encoder_out["vis_feat_sizes"],
                encoder_hidden_states=out["encoder_hidden_states"],
                prompt=prompt,
                prompt_mask=prompt_mask,
                hs=hs,
            )

        if self.training or self.num_interactive_steps_val > 0:
            self._compute_matching(out, self.back_convert(find_target))
        return out

    def _postprocess_out(self, out: Dict, multimask_output: bool = False):
        # For multimask output, during eval we return the single best mask with the dict keys expected by the evaluators, but also return the multimasks output with new keys.
        num_mask_boxes = out["pred_boxes"].size(1)
        if not self.training and multimask_output and num_mask_boxes > 1:
            out["multi_pred_logits"] = out["pred_logits"]
            if "pred_masks" in out:
                out["multi_pred_masks"] = out["pred_masks"]
            out["multi_pred_boxes"] = out["pred_boxes"]
            out["multi_pred_boxes_xyxy"] = out["pred_boxes_xyxy"]

            best_mask_idx = out["pred_logits"].argmax(1).squeeze(1)
            batch_idx = torch.arange(len(best_mask_idx), device=best_mask_idx.device)

            out["pred_logits"] = out["pred_logits"][batch_idx, best_mask_idx].unsqueeze(
                1
            )
            if "pred_masks" in out:
                out["pred_masks"] = out["pred_masks"][
                    batch_idx, best_mask_idx
                ].unsqueeze(1)
            out["pred_boxes"] = out["pred_boxes"][batch_idx, best_mask_idx].unsqueeze(1)
            out["pred_boxes_xyxy"] = out["pred_boxes_xyxy"][
                batch_idx, best_mask_idx
            ].unsqueeze(1)

        return out

    def _get_geo_prompt_from_find_input(self, find_input: FindStage):
        """Construct an initial geometric prompt from the find input."""
        point_embeddings, point_mask, point_labels = None, None, None
        if find_input.input_points_before_embed is not None:
            # Point embeddings are batch first, switch to seq first
            point_embeddings = find_input.input_points_before_embed.transpose(0, 1)

            # they are stored as (x,y,label), so we unpack
            point_labels = point_embeddings[..., -1]
            point_embeddings = point_embeddings[..., :-1]
            point_mask = find_input.input_points_mask

        geometric_prompt = Prompt(
            box_embeddings=find_input.input_boxes_before_embed,
            box_mask=find_input.input_boxes_mask,
            box_labels=find_input.input_boxes_label,
            point_embeddings=point_embeddings,
            point_mask=point_mask,
            point_labels=point_labels,
        )
        return geometric_prompt

    def _get_dummy_prompt(self, num_prompts=1):
        device = self.device
        geometric_prompt = Prompt(
            box_embeddings=torch.zeros(0, num_prompts, 4, device=device),
            box_mask=torch.zeros(num_prompts, 0, device=device, dtype=torch.bool),
        )
        return geometric_prompt

    def forward(self, input: BatchedDatapoint):
        device = self.device
        backbone_out = {"img_batch_all_stages": input.img_batch}
        backbone_out.update(self.backbone.forward_image(input.img_batch))
        num_frames = len(input.find_inputs)
        assert num_frames == 1

        text_outputs = self.backbone.forward_text(input.find_text_batch, device=device)
        backbone_out.update(text_outputs)

        previous_stages_out = SAM3Output(
            iter_mode=SAM3Output.IterMode.LAST_STEP_PER_STAGE
        )

        find_input = input.find_inputs[0]
        find_target = input.find_targets[0]

        if find_input.input_points is not None and find_input.input_points.numel() > 0:
            print("Warning: Point prompts are ignored in PCS.")

        num_interactive_steps = 0 if self.training else self.num_interactive_steps_val
        geometric_prompt = Prompt(
            box_embeddings=find_input.input_boxes,
            box_mask=find_input.input_boxes_mask,
            box_labels=find_input.input_boxes_label,
        )

        # Init vars that are shared across the loop.
        stage_outs = []
        for cur_step in range(num_interactive_steps + 1):
            if cur_step > 0:
                # We sample interactive geometric prompts (boxes, points)
                geometric_prompt, _ = self.interactive_prompt_sampler.sample(
                    geo_prompt=geometric_prompt,
                    find_target=find_target,
                    previous_out=stage_outs[-1],
                )
            out = self.forward_grounding(
                backbone_out=backbone_out,
                find_input=find_input,
                find_target=find_target,
                geometric_prompt=geometric_prompt.clone(),
            )
            stage_outs.append(out)

        previous_stages_out.append(stage_outs)
        return previous_stages_out

    def _compute_matching(self, out, targets):
        out["indices"] = self.matcher(out, targets)
        for aux_out in out.get("aux_outputs", []):
            aux_out["indices"] = self.matcher(aux_out, targets)

    def back_convert(self, targets):
        batched_targets = {
            "boxes": targets.boxes.view(-1, 4),
            "boxes_xyxy": box_cxcywh_to_xyxy(targets.boxes.view(-1, 4)),
            "boxes_padded": targets.boxes_padded,
            "positive_map": targets.boxes.new_ones(len(targets.boxes), 1),
            "num_boxes": targets.num_boxes,
            "masks": targets.segments,
            "semantic_masks": targets.semantic_segments,
            "is_valid_mask": targets.is_valid_segment,
            "is_exhaustive": targets.is_exhaustive,
            "object_ids_packed": targets.object_ids,
            "object_ids_padded": targets.object_ids_padded,
        }
        return batched_targets

    def predict_inst(
        self,
        inference_state,
        **kwargs,
    ) -> Tuple[np.ndarray, np.ndarray, np.ndarray]:
        orig_h, orig_w = (
            inference_state["original_height"],
            inference_state["original_width"],
        )
        backbone_out = inference_state["backbone_out"]["sam2_backbone_out"]
        (
            _,
            vision_feats,
            _,
            _,
        ) = self.inst_interactive_predictor.model._prepare_backbone_features(
            backbone_out
        )
        # Add no_mem_embed, which is added to the lowest rest feat. map during training on videos
        vision_feats[-1] = (
            vision_feats[-1] + self.inst_interactive_predictor.model.no_mem_embed
        )
        feats = [
            feat.permute(1, 2, 0).view(1, -1, *feat_size)
            for feat, feat_size in zip(
                vision_feats[::-1], self.inst_interactive_predictor._bb_feat_sizes[::-1]
            )
        ][::-1]
        self.inst_interactive_predictor._features = {
            "image_embed": feats[-1],
            "high_res_feats": feats[:-1],
        }
        self.inst_interactive_predictor._is_image_set = True
        self.inst_interactive_predictor._orig_hw = [(orig_h, orig_w)]
        res = self.inst_interactive_predictor.predict(**kwargs)
        self.inst_interactive_predictor._features = None
        self.inst_interactive_predictor._is_image_set = False
        return res

    def predict_inst_batch(
        self,
        inference_state,
        *args,
        **kwargs,
    ) -> Tuple[List[np.ndarray], List[np.ndarray], List[np.ndarray]]:
        backbone_out = inference_state["backbone_out"]["sam2_backbone_out"]
        (
            _,
            vision_feats,
            _,
            _,
        ) = self.inst_interactive_predictor.model._prepare_backbone_features(
            backbone_out
        )
        # Add no_mem_embed, which is added to the lowest res feat. map during training on videos
        vision_feats[-1] = (
            vision_feats[-1] + self.inst_interactive_predictor.model.no_mem_embed
        )
        batch_size = vision_feats[-1].shape[1]
        orig_heights, orig_widths = (
            inference_state["original_heights"],
            inference_state["original_widths"],
        )
        assert batch_size == len(orig_heights) == len(orig_widths), (
            f"Batch size mismatch in predict_inst_batch. Got {batch_size}, {len(orig_heights)}, {len(orig_widths)}"
        )
        feats = [
            feat.permute(1, 2, 0).view(batch_size, -1, *feat_size)
            for feat, feat_size in zip(
                vision_feats[::-1], self.inst_interactive_predictor._bb_feat_sizes[::-1]
            )
        ][::-1]
        self.inst_interactive_predictor._features = {
            "image_embed": feats[-1],
            "high_res_feats": feats[:-1],
        }
        self.inst_interactive_predictor._is_image_set = True
        self.inst_interactive_predictor._is_batch = True
        self.inst_interactive_predictor._orig_hw = [
            (orig_h, orig_w) for orig_h, orig_w in zip(orig_heights, orig_widths)
        ]
        res = self.inst_interactive_predictor.predict_batch(*args, **kwargs)
        self.inst_interactive_predictor._features = None
        self.inst_interactive_predictor._is_image_set = False
        self.inst_interactive_predictor._is_batch = False
        return res


class Sam3ImageOnVideoMultiGPU(Sam3Image):
    def __init__(
        self, *args, async_all_gather=True, gather_backbone_out=None, **kwargs
    ):
        super().__init__(*args, **kwargs)
        self.rank = int(os.getenv("RANK", "0"))
        self.world_size = int(os.getenv("WORLD_SIZE", "1"))
        self.async_all_gather = async_all_gather

        # if gather_backbone is not set, default to gathering only for `SAM3VLBackbone`
        if gather_backbone_out is None:
            gather_backbone_out = isinstance(self.backbone, SAM3VLBackbone)
        self.gather_backbone_out = gather_backbone_out

    def forward_video_grounding_multigpu(
        self,
        backbone_out,
        find_inputs,
        geometric_prompt: Prompt,
        frame_idx,
        num_frames,
        # `multigpu_buffer` is a dict to cache detector's outputs in a chunk between different calls
        multigpu_buffer,
        track_in_reverse=False,
        # whether to also return the SAM2 backbone features
        return_sam2_backbone_feats=False,
        # whether to perform NMS and suppress the scores of those detections removed by NMS
        run_nms=False,
        nms_prob_thresh=None,
        nms_iou_thresh=None,
        **kwargs,
    ):
        """
        Compute the detector's detection outputs in a distributed manner, where all GPUs process
        a chunk of frames (equal to the number of GPUs) at once and store them in cache.
        """
        # Step 1: fetch the detector outputs in the current chunk from buffer
        frame_idx_curr_b = frame_idx - frame_idx % self.world_size
        frame_idx_curr_e = min(frame_idx_curr_b + self.world_size, num_frames)
        # in case the current frame's detection results are not in the buffer yet, build the current chunk
        # (this should only happen on the first chunk, since we are also building the next chunk below)
        if frame_idx not in multigpu_buffer:
            with torch.profiler.record_function("build_multigpu_buffer_next_chunk1"):
                self._build_multigpu_buffer_next_chunk(
                    backbone_out=backbone_out,
                    find_inputs=find_inputs,
                    geometric_prompt=geometric_prompt,
                    frame_idx_begin=frame_idx_curr_b,
                    frame_idx_end=frame_idx_curr_e,
                    num_frames=num_frames,
                    multigpu_buffer=multigpu_buffer,
                    run_nms=run_nms,
                    nms_prob_thresh=nms_prob_thresh,
                    nms_iou_thresh=nms_iou_thresh,
                )

        # read out the current frame's results from `multigpu_buffer`
        out = {}
        for k, (v, handle) in multigpu_buffer[frame_idx].items():
            if k.startswith("sam2_backbone_") and not return_sam2_backbone_feats:
                continue
            if handle is not None:
                handle.wait()  # wait for async all-gather to finish
            out[k] = v

        # Step 2: remove detection outputs of the previous chunk from cache to save GPU memory
        if not track_in_reverse and frame_idx_curr_b - self.world_size >= 0:
            frame_idx_prev_e = frame_idx_curr_b
            frame_idx_prev_b = frame_idx_curr_b - self.world_size
        elif track_in_reverse and frame_idx_curr_e < num_frames:
            frame_idx_prev_b = frame_idx_curr_e
            frame_idx_prev_e = min(frame_idx_prev_b + self.world_size, num_frames)
        else:
            frame_idx_prev_b = frame_idx_prev_e = None
        if frame_idx_prev_b is not None:
            for frame_idx_rm in range(frame_idx_prev_b, frame_idx_prev_e):
                multigpu_buffer.pop(frame_idx_rm, None)

        # Step 3: compute and cache detection outputs of the next chunk ahead of time
        # (so that we can overlap computation with all-gather transfer)
        if not track_in_reverse and frame_idx_curr_e < num_frames:
            frame_idx_next_b = frame_idx_curr_e
            frame_idx_next_e = min(frame_idx_next_b + self.world_size, num_frames)
        elif track_in_reverse and frame_idx_curr_b - self.world_size >= 0:
            frame_idx_next_e = frame_idx_curr_b
            frame_idx_next_b = frame_idx_curr_b - self.world_size
        else:
            frame_idx_next_b = frame_idx_next_e = None
        if frame_idx_next_b is not None and frame_idx_next_b not in multigpu_buffer:
            with torch.profiler.record_function("build_multigpu_buffer_next_chunk2"):
                self._build_multigpu_buffer_next_chunk(
                    backbone_out=backbone_out,
                    find_inputs=find_inputs,
                    geometric_prompt=geometric_prompt,
                    frame_idx_begin=frame_idx_next_b,
                    frame_idx_end=frame_idx_next_e,
                    num_frames=num_frames,
                    multigpu_buffer=multigpu_buffer,
                    run_nms=run_nms,
                    nms_prob_thresh=nms_prob_thresh,
                    nms_iou_thresh=nms_iou_thresh,
                )

        return out, backbone_out

    def _build_multigpu_buffer_next_chunk(
        self,
        backbone_out,
        find_inputs,
        geometric_prompt: Prompt,
        frame_idx_begin,
        frame_idx_end,
        num_frames,
        multigpu_buffer,
        run_nms=False,
        nms_prob_thresh=None,
        nms_iou_thresh=None,
    ):
        """Compute detection outputs on a chunk of frames and store their results in multigpu_buffer."""
        # each GPU computes detections on one frame in the chunk (in a round-robin manner)
        frame_idx_local_gpu = min(frame_idx_begin + self.rank, frame_idx_end - 1)
        # `forward_grounding` (from base class `Sam3ImageOnVideo`) runs the detector on a single frame
        with torch.profiler.record_function("forward_grounding"):
            out_local = self.forward_grounding(
                backbone_out=backbone_out,
                find_input=find_inputs[frame_idx_local_gpu],
                find_target=None,
                geometric_prompt=geometric_prompt,
            )
        if run_nms:
            with torch.profiler.record_function("nms_masks"):
                # run NMS as a post-processing step on top of the detection outputs
                assert nms_prob_thresh is not None and nms_iou_thresh is not None
                pred_probs = out_local["pred_logits"].squeeze(-1).sigmoid()
                pred_masks = out_local["pred_masks"]
                # loop over text prompts (not an overhead for demo where there's only 1 prompt)
                for prompt_idx in range(pred_probs.size(0)):
                    keep = nms_masks(
                        pred_probs=pred_probs[prompt_idx],
                        pred_masks=pred_masks[prompt_idx],
                        prob_threshold=nms_prob_thresh,
                        iou_threshold=nms_iou_thresh,
                    )
                    # set a very low threshold for those detections removed by NMS
                    out_local["pred_logits"][prompt_idx, :, 0] -= 1e4 * (~keep).float()

        if self.gather_backbone_out:
            # gather the SAM 2 backbone features across GPUs
            feats = out_local["prev_encoder_out"]["backbone_out"]["sam2_backbone_out"]
            assert len(feats["backbone_fpn"]) == 3  # SAM2 backbone always have 3 levels
            # cast the SAM2 backbone features to bfloat16 for all-gather (this is usually
            # a no-op, SAM2 backbone features are likely already in bfloat16 due to AMP)
            backbone_fpn_bf16 = [x.to(torch.bfloat16) for x in feats["backbone_fpn"]]
            fpn0, fpn_handle0 = self._gather_tensor(backbone_fpn_bf16[0])
            fpn1, fpn_handle1 = self._gather_tensor(backbone_fpn_bf16[1])
            fpn2, fpn_handle2 = self._gather_tensor(backbone_fpn_bf16[2])
            # vision_pos_enc is the same on all frames, so no need to all-gather them
            vision_pos_enc = feats["vision_pos_enc"]

        # trim the detector output to only include the necessary keys
        out_local = {
            "pred_logits": out_local["pred_logits"],
            "pred_boxes": out_local["pred_boxes"],
            "pred_boxes_xyxy": out_local["pred_boxes_xyxy"],
            "pred_masks": out_local["pred_masks"],
        }

        # gather the results: after this step, each GPU will receive detector outputs on
        # all frames in the chunk and store them in `multigpu_buffer`
        out_gathered = {k: self._gather_tensor(v) for k, v in out_local.items()}
        for rank in range(self.world_size):
            frame_idx_to_save = frame_idx_begin + rank
            if frame_idx_to_save >= num_frames:
                continue
            frame_buffer = {
                k: (v[rank], handle) for k, (v, handle) in out_gathered.items()
            }
            if self.gather_backbone_out:
                # also add gathered SAM 2 backbone features to frame_buffer
                frame_buffer["tracker_backbone_fpn_0"] = (fpn0[rank], fpn_handle0)
                frame_buffer["tracker_backbone_fpn_1"] = (fpn1[rank], fpn_handle1)
                frame_buffer["tracker_backbone_fpn_2"] = (fpn2[rank], fpn_handle2)
                frame_buffer["tracker_backbone_pos_enc"] = (vision_pos_enc, None)

            multigpu_buffer[frame_idx_to_save] = frame_buffer

    def _gather_tensor(self, x):
        if self.world_size == 1:
            return [x], None

        async_op = self.async_all_gather
        # here `.contiguous()` is required -- otherwise NCCL all_gather
        # sometimes gives wrong results
        x = x.contiguous()  # ensure contiguous memory for NCCL
        output_list = [torch.empty_like(x) for _ in range(self.world_size)]
        handle = torch.distributed.all_gather(output_list, x, async_op=async_op)
        return output_list, handle



================================================
FILE: sam3/model/sam3_image_processor.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe
from typing import Dict, List

import numpy as np
import PIL
import torch
from sam3.model import box_ops
from sam3.model.data_misc import FindStage, interpolate
from torchvision.transforms import v2


class Sam3Processor:
    """ """

    def __init__(self, model, resolution=1008, device="cuda", confidence_threshold=0.5):
        self.model = model
        self.resolution = resolution
        self.device = device
        self.transform = v2.Compose(
            [
                v2.ToDtype(torch.uint8, scale=True),
                v2.Resize(size=(resolution, resolution)),
                v2.ToDtype(torch.float32, scale=True),
                v2.Normalize(mean=[0.5, 0.5, 0.5], std=[0.5, 0.5, 0.5]),
            ]
        )
        self.confidence_threshold = confidence_threshold

        self.find_stage = FindStage(
            img_ids=torch.tensor([0], device=device, dtype=torch.long),
            text_ids=torch.tensor([0], device=device, dtype=torch.long),
            input_boxes=None,
            input_boxes_mask=None,
            input_boxes_label=None,
            input_points=None,
            input_points_mask=None,
        )

    @torch.inference_mode()
    def set_image(self, image, state=None):
        """Sets the image on which we want to do predictions."""
        if state is None:
            state = {}

        if isinstance(image, PIL.Image.Image):
            width, height = image.size
        elif isinstance(image, (torch.Tensor, np.ndarray)):
            height, width = image.shape[-2:]
        else:
            raise ValueError("Image must be a PIL image or a tensor")

        image = v2.functional.to_image(image).to(self.device)
        image = self.transform(image).unsqueeze(0)

        state["original_height"] = height
        state["original_width"] = width
        state["backbone_out"] = self.model.backbone.forward_image(image)
        inst_interactivity_en = self.model.inst_interactive_predictor is not None
        if inst_interactivity_en and "sam2_backbone_out" in state["backbone_out"]:
            sam2_backbone_out = state["backbone_out"]["sam2_backbone_out"]
            sam2_backbone_out["backbone_fpn"][0] = (
                self.model.inst_interactive_predictor.model.sam_mask_decoder.conv_s0(
                    sam2_backbone_out["backbone_fpn"][0]
                )
            )
            sam2_backbone_out["backbone_fpn"][1] = (
                self.model.inst_interactive_predictor.model.sam_mask_decoder.conv_s1(
                    sam2_backbone_out["backbone_fpn"][1]
                )
            )
        return state

    @torch.inference_mode()
    def set_image_batch(self, images: List[np.ndarray], state=None):
        """Sets the image batch on which we want to do predictions."""
        if state is None:
            state = {}

        if not isinstance(images, list):
            raise ValueError("Images must be a list of PIL images or tensors")
        assert len(images) > 0, "Images list must not be empty"
        assert isinstance(images[0], PIL.Image.Image), (
            "Images must be a list of PIL images"
        )

        state["original_heights"] = [image.height for image in images]
        state["original_widths"] = [image.width for image in images]

        images = [
            self.transform(v2.functional.to_image(image).to(self.device))
            for image in images
        ]
        images = torch.stack(images, dim=0)
        state["backbone_out"] = self.model.backbone.forward_image(images)
        inst_interactivity_en = self.model.inst_interactive_predictor is not None
        if inst_interactivity_en and "sam2_backbone_out" in state["backbone_out"]:
            sam2_backbone_out = state["backbone_out"]["sam2_backbone_out"]
            sam2_backbone_out["backbone_fpn"][0] = (
                self.model.inst_interactive_predictor.model.sam_mask_decoder.conv_s0(
                    sam2_backbone_out["backbone_fpn"][0]
                )
            )
            sam2_backbone_out["backbone_fpn"][1] = (
                self.model.inst_interactive_predictor.model.sam_mask_decoder.conv_s1(
                    sam2_backbone_out["backbone_fpn"][1]
                )
            )
        return state

    @torch.inference_mode()
    def set_text_prompt(self, prompt: str, state: Dict):
        """Sets the text prompt and run the inference"""

        if "backbone_out" not in state:
            raise ValueError("You must call set_image before set_text_prompt")

        text_outputs = self.model.backbone.forward_text([prompt], device=self.device)
        # will erase the previous text prompt if any
        state["backbone_out"].update(text_outputs)
        if "geometric_prompt" not in state:
            state["geometric_prompt"] = self.model._get_dummy_prompt()

        return self._forward_grounding(state)

    @torch.inference_mode()
    def add_geometric_prompt(self, box: List, label: bool, state: Dict):
        """Adds a box prompt and run the inference.
        The image needs to be set, but not necessarily the text prompt.
        The box is assumed to be in [center_x, center_y, width, height] format and normalized in [0, 1] range.
        The label is True for a positive box, False for a negative box.
        """
        if "backbone_out" not in state:
            raise ValueError("You must call set_image before set_text_prompt")

        if "language_features" not in state["backbone_out"]:
            # Looks like we don't have a text prompt yet. This is allowed, but we need to set the text prompt to "visual" for the model to rely only on the geometric prompt
            dummy_text_outputs = self.model.backbone.forward_text(
                ["visual"], device=self.device
            )
            state["backbone_out"].update(dummy_text_outputs)

        if "geometric_prompt" not in state:
            state["geometric_prompt"] = self.model._get_dummy_prompt()

        # adding a batch and sequence dimension
        boxes = torch.tensor(box, device=self.device, dtype=torch.float32).view(1, 1, 4)
        labels = torch.tensor([label], device=self.device, dtype=torch.bool).view(1, 1)
        state["geometric_prompt"].append_boxes(boxes, labels)

        return self._forward_grounding(state)

    def reset_all_prompts(self, state: Dict):
        """Removes all the prompts and results"""
        if "backbone_out" in state:
            backbone_keys_to_del = [
                "language_features",
                "language_mask",
                "language_embeds",
            ]
            for key in backbone_keys_to_del:
                if key in state["backbone_out"]:
                    del state["backbone_out"][key]

        keys_to_del = ["geometric_prompt", "boxes", "masks", "masks_logits", "scores"]
        for key in keys_to_del:
            if key in state:
                del state[key]

    @torch.inference_mode()
    def set_confidence_threshold(self, threshold: float, state=None):
        """Sets the confidence threshold for the masks"""
        self.confidence_threshold = threshold
        if state is not None and "boxes" in state:
            # we need to filter the boxes again
            # In principle we could do this more efficiently since we would only need
            # to rerun the heads. But this is simpler and not too inefficient
            return self._forward_grounding(state)
        return state

    @torch.inference_mode()
    def _forward_grounding(self, state: Dict):
        outputs = self.model.forward_grounding(
            backbone_out=state["backbone_out"],
            find_input=self.find_stage,
            geometric_prompt=state["geometric_prompt"],
            find_target=None,
        )

        out_bbox = outputs["pred_boxes"]
        out_logits = outputs["pred_logits"]
        out_masks = outputs["pred_masks"]
        out_probs = out_logits.sigmoid()
        presence_score = outputs["presence_logit_dec"].sigmoid().unsqueeze(1)
        out_probs = (out_probs * presence_score).squeeze(-1)

        keep = out_probs > self.confidence_threshold
        out_probs = out_probs[keep]
        out_masks = out_masks[keep]
        out_bbox = out_bbox[keep]

        # convert to [x0, y0, x1, y1] format
        boxes = box_ops.box_cxcywh_to_xyxy(out_bbox)

        img_h = state["original_height"]
        img_w = state["original_width"]
        scale_fct = torch.tensor([img_w, img_h, img_w, img_h]).to(self.device)
        boxes = boxes * scale_fct[None, :]

        out_masks = interpolate(
            out_masks.unsqueeze(1),
            (img_h, img_w),
            mode="bilinear",
            align_corners=False,
        ).sigmoid()

        state["masks_logits"] = out_masks
        state["masks"] = out_masks > 0.5
        state["boxes"] = boxes
        state["scores"] = out_probs
        return state



================================================
FILE: sam3/model/sam3_multiplex_detector.py
================================================
import os

import torch
from sam3.model.vl_combiner import SAM3VLBackbone

try:
    from sam3.model.vl_combiner import SAM3VLBackboneTri
except ImportError:
    SAM3VLBackboneTri = None
from typing import Dict, List, Optional

import numpy as np
from sam3.model.data_misc import BatchedDatapoint, FindStage
from sam3.model.geometry_encoders import Prompt
from sam3.model.model_misc import SAM3Output
from sam3.model.sam3_image import Sam3Image
from sam3.model.sam3_multiplex_detector_utils import nms_masks


class Sam3MultiplexImageBase(Sam3Image):
    """A wrapper class to run Sam3Image on videos for per-frame detection (no tracking)."""

    def __init__(
        self,
        *args,
        tracking_score_thresh: float = 0.0,
        offload_outputs_to_cpu_for_eval: bool = False,
        **kwargs,
    ):
        super().__init__(*args, **kwargs)
        self.tracking_score_thresh = tracking_score_thresh
        self.offload_outputs_to_cpu_for_eval = offload_outputs_to_cpu_for_eval
        self.trim_outputs_for_eval = True  # dummy option -- it doesn't do anything

    def forward(
        self,
        input: BatchedDatapoint,
        is_inference=False,  # (a dummy parameter not used anymore)
    ):
        assert not self.training, (
            "Sam3MultiplexImageBase should only be used in eval mode."
        )

        device = self.device
        backbone_out = {"img_batch_all_stages": input.img_batch}
        text_outputs = self.backbone.forward_text(input.find_text_batch, device=device)
        backbone_out.update(text_outputs)
        num_frames = len(input.find_inputs)

        previous_stages_out = SAM3Output(
            iter_mode=SAM3Output.IterMode.LAST_STEP_PER_STAGE
        )
        for frame_idx in range(num_frames):
            find_input = input.find_inputs[frame_idx]
            find_target = input.find_targets[frame_idx]
            geometric_prompt = self._get_geo_prompt_from_find_input(find_input)
            cur_out, _ = self.forward_video_grounding(
                backbone_out=backbone_out,
                find_input=find_input,
                find_target=find_target,
                geometric_prompt=geometric_prompt,
            )
            # offload model outputs to CPU (to save GPU memory) for evaluation
            if self.offload_outputs_to_cpu_for_eval:
                cur_out = {k: v.cpu() for k, v in cur_out.items()}

            previous_stages_out.append([cur_out])

        get_queries = None
        return previous_stages_out, get_queries

    def forward_video_grounding(
        self,
        backbone_out,
        find_input,
        find_target,
        geometric_prompt: Prompt,
        **kwargs,
    ):
        # route this to the image grounding forward method
        out = self.forward_grounding(
            backbone_out=backbone_out,
            find_input=find_input,
            find_target=find_target,
            geometric_prompt=geometric_prompt,
        )
        # trim the output to only include the necessary keys
        out = {
            "pred_logits": out["pred_logits"],
            "pred_boxes": out["pred_boxes"],
            "pred_boxes_xyxy": out["pred_boxes_xyxy"],
            "pred_masks": out["pred_masks"],
            "pred_object_ids": self._get_dummy_object_ids(out["pred_logits"]),
        }
        return out, backbone_out

    def _get_dummy_object_ids(self, pred_logits):
        """Generate dummy object IDs for the detected objects, based on their detection query indices."""
        # Assuming pred_logits has shape [batch_size, num_queries, num_classes]
        B, Q, _ = pred_logits.shape
        is_above_thresh = pred_logits.squeeze(2) > self.tracking_score_thresh
        dummy_obj_ids = torch.arange(Q, device=self.device).expand(B, -1)
        dummy_obj_ids = torch.where(is_above_thresh, dummy_obj_ids, -1)
        return dummy_obj_ids

    def _trim_outputs(self, *args, **kwargs):
        pass  # not needed for image-on-video

    def _batch_find_inputs(
        self,
        find_inputs: List[FindStage],
        chunk_start: int,
        chunk_end: int,
    ) -> FindStage:
        """
        Batch multiple FindStage objects into a single batched FindStage.

        For each frame in the chunk, creates img_ids that point to the correct
        frame index. When processing streaming video, the img_ids are the actual
        frame indices (e.g., [0, 1, 2, ..., 15] for chunk 0-16), and the modulo
        for circular buffer access is applied later in _get_img_feats.

        Args:
            find_inputs: List of FindStage objects for all frames.
            chunk_start: Start index of the chunk.
            chunk_end: End index of the chunk (exclusive).

        Returns:
            A single FindStage with batched tensors.
        """
        chunk_find_inputs = [
            find_inputs[i % len(find_inputs)] for i in range(chunk_start, chunk_end)
        ]

        # Generate img_ids based on chunk frame indices
        # Each frame in the chunk gets its corresponding frame index
        # The modulo for circular buffer access is handled in _get_img_feats
        device = chunk_find_inputs[0].img_ids.device
        dtype = chunk_find_inputs[0].img_ids.dtype
        img_ids_list = [
            torch.tensor([i], device=device, dtype=dtype)
            for i in range(chunk_start, chunk_end)
        ]
        batched_img_ids = torch.cat(img_ids_list, dim=0)

        # Generate img_ids_np to match
        img_ids_np_list = [np.array([i]) for i in range(chunk_start, chunk_end)]
        batched_img_ids_np = np.concatenate(img_ids_np_list, axis=0)

        # Concatenate text_ids
        text_ids_list = [fi.text_ids for fi in chunk_find_inputs]
        batched_text_ids = torch.cat(text_ids_list, dim=0)

        # Concatenate input_boxes
        input_boxes_list = [fi.input_boxes for fi in chunk_find_inputs]
        batched_input_boxes = (
            torch.cat(input_boxes_list, dim=0)
            if input_boxes_list[0] is not None
            else None
        )

        # Concatenate input_boxes_mask
        input_boxes_mask_list = [fi.input_boxes_mask for fi in chunk_find_inputs]
        batched_input_boxes_mask = (
            torch.cat(input_boxes_mask_list, dim=0)
            if input_boxes_mask_list[0] is not None
            else None
        )

        # Concatenate input_boxes_label
        input_boxes_label_list = [fi.input_boxes_label for fi in chunk_find_inputs]
        batched_input_boxes_label = (
            torch.cat(input_boxes_label_list, dim=0)
            if input_boxes_label_list[0] is not None
            else None
        )

        # Concatenate input_points
        input_points_list = [fi.input_points for fi in chunk_find_inputs]
        batched_input_points = (
            torch.cat(input_points_list, dim=0)
            if input_points_list[0] is not None
            else None
        )

        # Concatenate input_points_mask
        input_points_mask_list = [fi.input_points_mask for fi in chunk_find_inputs]
        batched_input_points_mask = (
            torch.cat(input_points_mask_list, dim=0)
            if input_points_mask_list[0] is not None
            else None
        )

        # Handle optional fields
        input_boxes_before_embed_list = [
            fi.input_boxes_before_embed for fi in chunk_find_inputs
        ]
        batched_input_boxes_before_embed = (
            torch.cat(input_boxes_before_embed_list, dim=0)
            if input_boxes_before_embed_list[0] is not None
            else None
        )

        input_points_before_embed_list = [
            fi.input_points_before_embed for fi in chunk_find_inputs
        ]
        batched_input_points_before_embed = (
            torch.cat(input_points_before_embed_list, dim=0)
            if input_points_before_embed_list[0] is not None
            else None
        )

        # Create batched FindStage
        batched_find_input = FindStage(
            img_ids=batched_img_ids,
            img_ids_np=batched_img_ids_np,
            text_ids=batched_text_ids,
            input_boxes=batched_input_boxes,
            input_boxes_mask=batched_input_boxes_mask,
            input_boxes_label=batched_input_boxes_label,
            input_points=batched_input_points,
            input_points_mask=batched_input_points_mask,
            ptrs=None,  # Not batching pointers for now
            ptrs_seg=None,
            object_ids=None,
            input_boxes_before_embed=batched_input_boxes_before_embed,
            input_points_before_embed=batched_input_points_before_embed,
        )

        return batched_find_input

    def _batch_geometric_prompts(
        self,
        geometric_prompts: List[Prompt],
        chunk_start: int,
        chunk_end: int,
    ) -> Prompt:
        """
        Batch multiple Prompt objects into a single batched Prompt.

        Args:
            geometric_prompts: List of Prompt objects for all frames.
            chunk_start: Start index of the chunk.
            chunk_end: End index of the chunk (exclusive).

        Returns:
            A single Prompt with batched tensors.
        """
        chunk_prompts = [geometric_prompts[i] for i in range(chunk_start, chunk_end)]
        return self._batch_geometric_prompts_from_list(chunk_prompts)

    def _batch_geometric_prompts_from_list(
        self,
        chunk_prompts: List[Prompt],
    ) -> Prompt:
        """
        Batch a list of Prompt objects into a single batched Prompt.

        Prompt uses seq-first, batch-second convention:
        - box_embeddings: N_boxes x B x C_box - batch along dim 1
        - box_mask: B x N_boxes - batch along dim 0
        - box_labels: N_boxes x B - batch along dim 1
        - point_embeddings: N_points x B x C_point - batch along dim 1
        - point_mask: B x N_points - batch along dim 0
        - point_labels: N_points x B - batch along dim 1

        Args:
            chunk_prompts: List of Prompt objects to batch.

        Returns:
            A single Prompt with batched tensors.
        """

        # Helper function to batch tensors along specified dimension
        def batch_tensors(tensors, dim):
            if tensors[0] is None:
                return None
            return torch.cat(tensors, dim=dim)

        # Batch box embeddings (N_boxes x B x C_box - batch along dim 1)
        box_embeddings_list = [p.box_embeddings for p in chunk_prompts]
        batched_box_embeddings = batch_tensors(box_embeddings_list, dim=1)

        # Batch box mask (B x N_boxes - batch along dim 0)
        box_mask_list = [p.box_mask for p in chunk_prompts]
        batched_box_mask = batch_tensors(box_mask_list, dim=0)

        # Batch box labels (N_boxes x B - batch along dim 1)
        box_labels_list = [p.box_labels for p in chunk_prompts]
        batched_box_labels = batch_tensors(box_labels_list, dim=1)

        # Batch point embeddings (N_points x B x C_point - batch along dim 1)
        point_embeddings_list = [p.point_embeddings for p in chunk_prompts]
        batched_point_embeddings = batch_tensors(point_embeddings_list, dim=1)

        # Batch point mask (B x N_points - batch along dim 0)
        point_mask_list = [p.point_mask for p in chunk_prompts]
        batched_point_mask = batch_tensors(point_mask_list, dim=0)

        # Batch point labels (N_points x B - batch along dim 1)
        point_labels_list = [p.point_labels for p in chunk_prompts]
        batched_point_labels = batch_tensors(point_labels_list, dim=1)

        # Create batched Prompt
        batched_prompt = Prompt(
            box_embeddings=batched_box_embeddings,
            box_mask=batched_box_mask,
            box_labels=batched_box_labels,
            point_embeddings=batched_point_embeddings,
            point_mask=batched_point_mask,
            point_labels=batched_point_labels,
        )

        return batched_prompt


class Sam3MultiplexDetector(Sam3MultiplexImageBase):
    def __init__(
        self,
        *args,
        async_all_gather=True,
        gather_backbone_out=None,
        is_multiplex=False,
        **kwargs,
    ):
        super().__init__(*args, **kwargs)
        self.rank = int(os.getenv("RANK", "0"))
        self.world_size = int(os.getenv("WORLD_SIZE", "1"))
        self.async_all_gather = async_all_gather

        # if gather_backbone is not set, default to gathering only for `SAM3VLBackbone`
        if gather_backbone_out is None:
            gather_backbone_out = isinstance(self.backbone, SAM3VLBackbone) or (
                SAM3VLBackboneTri is not None
                and isinstance(self.backbone, SAM3VLBackboneTri)
            )
        self.gather_backbone_out = gather_backbone_out
        self.is_multiplex = is_multiplex

    def forward_video_grounding_multigpu(
        self,
        backbone_out,
        find_inputs,
        geometric_prompt: Prompt,
        frame_idx,
        num_frames,
        # `multigpu_buffer` is a dict to cache FA outputs in a chunk between different calls
        multigpu_buffer,
        track_in_reverse=False,
        # whether to also return the SAM2 backbone features (in addition to FA results)
        return_sam2_backbone_feats=False,
        # whether to perform NMS and suppress the scores of those detections removed by NMS
        run_nms=False,
        nms_prob_thresh=None,
        nms_iou_thresh=None,
        nms_use_iom=False,
        # tracking bounds to respect max_frame_num_to_track
        max_frame_num_to_track=None,
        propagate_in_video_start_frame_idx=None,
        # feature_cache for buffered backbone computation
        feature_cache=None,
        **kwargs,
    ):
        """
        Compute the FA detection outputs in a distributed manner, where all GPUs process
        a chunk of frames (equal to the number of GPUs) at once and store them in cache.
        """
        # Calculate valid frame range based on max_frame_num_to_track
        # We prevent pre-fetching beyond the tracking window relative to current frame
        if max_frame_num_to_track is not None:
            if propagate_in_video_start_frame_idx is None:
                propagate_in_video_start_frame_idx = 0
            if track_in_reverse:
                # When going backwards, limit how far back we can go from current frame
                valid_frame_start = max(
                    0,
                    propagate_in_video_start_frame_idx - max_frame_num_to_track + 1,
                )
                valid_frame_end = num_frames
            else:
                # When going forwards, limit how far ahead we can go from current frame
                valid_frame_start = 0
                valid_frame_end = min(
                    num_frames,
                    propagate_in_video_start_frame_idx + max_frame_num_to_track,
                )
        else:
            # No tracking limit specified, use full video range
            valid_frame_start = 0
            valid_frame_end = num_frames

        # Step 1: fetch the FA outputs in the current chunk from buffer
        frame_idx_curr_b = frame_idx - frame_idx % self.world_size
        frame_idx_curr_e = min(frame_idx_curr_b + self.world_size, num_frames)

        # Clamp the current chunk to the valid tracking range
        frame_idx_curr_b = max(frame_idx_curr_b, valid_frame_start)
        frame_idx_curr_e = min(frame_idx_curr_e, valid_frame_end)
        # in case the current frame's FA results are not in the buffer yet, build the current chunk
        # (this should only happen on the first chunk, since we are also building the next chunk below)
        if frame_idx not in multigpu_buffer:
            with torch.profiler.record_function("build_multigpu_buffer_next_chunk1"):
                self._build_multigpu_buffer_next_chunk(
                    backbone_out=backbone_out,
                    find_inputs=find_inputs,
                    geometric_prompt=geometric_prompt,
                    frame_idx_begin=frame_idx_curr_b,
                    frame_idx_end=frame_idx_curr_e,
                    num_frames=num_frames,
                    multigpu_buffer=multigpu_buffer,
                    run_nms=run_nms,
                    nms_prob_thresh=nms_prob_thresh,
                    nms_iou_thresh=nms_iou_thresh,
                    nms_use_iom=nms_use_iom,
                    feature_cache=feature_cache,
                )

        # read out the current frame's results from `multigpu_buffer`
        out = {}
        for k, (v, handle) in multigpu_buffer[frame_idx].items():
            if self.is_multiplex:
                if (
                    k.startswith("interactive_backbone_")
                    or k.startswith("propagation_backbone_")
                ) and not return_sam2_backbone_feats:
                    continue
            else:
                if k.startswith("sam2_backbone_") and not return_sam2_backbone_feats:
                    continue
            if handle is not None:
                handle.wait()  # wait for async all-gather to finish
            out[k] = v

        # Step 2: remove FA outputs of the previous chunk from cache to save GPU memory
        if not track_in_reverse and frame_idx_curr_b - self.world_size >= 0:
            frame_idx_prev_e = frame_idx_curr_b
            frame_idx_prev_b = frame_idx_curr_b - self.world_size
        elif track_in_reverse and frame_idx_curr_e < num_frames:
            frame_idx_prev_b = frame_idx_curr_e
            frame_idx_prev_e = min(frame_idx_prev_b + self.world_size, num_frames)
        else:
            frame_idx_prev_b = frame_idx_prev_e = None
        if frame_idx_prev_b is not None:
            for frame_idx_rm in range(frame_idx_prev_b, frame_idx_prev_e):
                multigpu_buffer.pop(frame_idx_rm, None)

        # Step 3: compute and cache FA outputs of the next chunk ahead of time
        # (so that we can overlap computation with all-gather transfer)
        # Respect tracking bounds when calculating next chunk

        if not track_in_reverse and frame_idx_curr_e < valid_frame_end:
            frame_idx_next_b = frame_idx_curr_e
            frame_idx_next_e = min(frame_idx_next_b + self.world_size, valid_frame_end)
        elif (
            track_in_reverse and frame_idx_curr_b - self.world_size >= valid_frame_start
        ):
            frame_idx_next_e = frame_idx_curr_b
            frame_idx_next_b = max(
                frame_idx_curr_b - self.world_size, valid_frame_start
            )
        else:
            frame_idx_next_b = frame_idx_next_e = None
        if frame_idx_next_b is not None and frame_idx_next_b not in multigpu_buffer:
            with torch.profiler.record_function("build_multigpu_buffer_next_chunk2"):
                self._build_multigpu_buffer_next_chunk(
                    backbone_out=backbone_out,
                    find_inputs=find_inputs,
                    geometric_prompt=geometric_prompt,
                    frame_idx_begin=frame_idx_next_b,
                    frame_idx_end=frame_idx_next_e,
                    num_frames=num_frames,
                    multigpu_buffer=multigpu_buffer,
                    run_nms=run_nms,
                    nms_prob_thresh=nms_prob_thresh,
                    nms_iou_thresh=nms_iou_thresh,
                    feature_cache=feature_cache,
                )

        return out, backbone_out

    def _build_multigpu_buffer_next_chunk(
        self,
        backbone_out,
        find_inputs,
        geometric_prompt: Prompt,
        frame_idx_begin,
        frame_idx_end,
        num_frames,
        multigpu_buffer,
        run_nms=False,
        nms_prob_thresh=None,
        nms_iou_thresh=None,
        nms_use_iom=False,
        feature_cache=None,
    ):
        """Compute FA outputs on a chunk of frames and store their results in multigpu_buffer."""
        # each GPU computes FA on one frame in the chunk (in a round-robin manner)
        frame_idx_local_gpu = min(frame_idx_begin + self.rank, frame_idx_end - 1)
        # `forward_grounding` (from base class `Sam3MultiplexImageBase`) runs FA on a single frame
        with torch.profiler.record_function("forward_grounding"):
            out_local = self.forward_grounding(
                backbone_out=backbone_out,
                # HACK: Since find_inputs is on GPU having to realloc is expensive so changing the values in place for the prod usecase
                # i.e. when using the streaming frame loader resource instead of local file. For non-prod is always
                # frame_idx_local_gpu < len(find_inputs) so should be a no-op
                find_input=find_inputs[frame_idx_local_gpu % len(find_inputs)],
                find_target=None,
                geometric_prompt=geometric_prompt,
                feature_cache=feature_cache,
            )
        if run_nms:
            with torch.profiler.record_function("nms_masks"):
                # run NMS as a post-processing step on top of the detection outputs
                assert nms_prob_thresh is not None and nms_iou_thresh is not None
                pred_probs = out_local["pred_logits"].squeeze(-1).sigmoid()
                pred_masks = out_local["pred_masks"]
                # loop over text prompts (not an overhead for demo where there's only 1 prompt)
                for prompt_idx in range(pred_probs.size(0)):
                    keep = nms_masks(
                        pred_probs=pred_probs[prompt_idx],
                        pred_masks=pred_masks[prompt_idx],
                        prob_threshold=nms_prob_thresh,
                        iou_threshold=nms_iou_thresh,
                        nms_use_iom=nms_use_iom,
                        do_compile=getattr(self, "compile_model", False),
                        running_in_prod=getattr(self, "running_in_prod", False),
                    )
                    # set a very low threshold for those detections removed by NMS
                    out_local["pred_logits"][prompt_idx, :, 0] -= 1e4 * (~keep).float()

        if self.gather_backbone_out:
            # gather the SAM 2 backbone features across GPUs
            if self.is_multiplex:
                # Note that we should not need to compute the interaction features every frame
                # TODO: rooms for optimization

                # Interaction features
                inte_feats = out_local["prev_encoder_out"]["backbone_out"][
                    "interactive"
                ]
                assert inte_feats["vision_mask"] is None
                assert (
                    len(inte_feats["backbone_fpn"]) == 3
                )  # SAM2 backbone always have 3 levels
                assert all(x.mask is None for x in inte_feats["backbone_fpn"])
                # cast the SAM2 backbone features to bfloat16 for all-gather (this is usually
                # a no-op, SAM2 backbone features are likely already in bfloat16 due to AMP)
                inte_backbone_fpn_bf16 = [
                    x.to(torch.bfloat16) for x in inte_feats["backbone_fpn"]
                ]
                inte_fpn0, inte_fpn_handle0 = self._gather_tensor(
                    inte_backbone_fpn_bf16[0].tensors
                )
                inte_fpn1, inte_fpn_handle1 = self._gather_tensor(
                    inte_backbone_fpn_bf16[1].tensors
                )
                inte_fpn2, inte_fpn_handle2 = self._gather_tensor(
                    inte_backbone_fpn_bf16[2].tensors
                )
                # vision_pos_enc is the same on all frames, so no need to all-gather them
                inte_vision_pos_enc = inte_feats["vision_pos_enc"]

            feats = out_local["prev_encoder_out"]["backbone_out"]["sam2_backbone_out"]
            assert feats["vision_mask"] is None
            assert len(feats["backbone_fpn"]) == 3  # SAM2 backbone always have 3 levels
            assert all(x.mask is None for x in feats["backbone_fpn"])
            # cast the SAM2 backbone features to bfloat16 for all-gather (this is usually
            # a no-op, SAM2 backbone features are likely already in bfloat16 due to AMP)
            backbone_fpn_bf16 = [x.to(torch.bfloat16) for x in feats["backbone_fpn"]]
            fpn0, fpn_handle0 = self._gather_tensor(backbone_fpn_bf16[0].tensors)
            fpn1, fpn_handle1 = self._gather_tensor(backbone_fpn_bf16[1].tensors)
            fpn2, fpn_handle2 = self._gather_tensor(backbone_fpn_bf16[2].tensors)
            # vision_pos_enc is the same on all frames, so no need to all-gather them
            vision_pos_enc = feats["vision_pos_enc"]

        # trim the FA output to only include the necessary keys
        out_local = {
            "pred_logits": out_local["pred_logits"],
            "pred_boxes": out_local["pred_boxes"],
            "pred_boxes_xyxy": out_local["pred_boxes_xyxy"],
            "pred_masks": out_local["pred_masks"],
            "pred_object_ids": self._get_dummy_object_ids(out_local["pred_logits"]),
        }

        # gather the results: after this step, each GPU will receive FA outputs on
        # all frames in the chunk and store them in `multigpu_buffer`
        out_gathered = {k: self._gather_tensor(v) for k, v in out_local.items()}
        for rank in range(self.world_size):
            frame_idx_to_save = frame_idx_begin + rank
            if frame_idx_to_save >= num_frames:
                continue
            frame_buffer = {
                k: (v[rank], handle) for k, (v, handle) in out_gathered.items()
            }
            if self.gather_backbone_out:
                # also add gathered SAM 2 backbone features to frame_buffer
                if self.is_multiplex:
                    frame_buffer["interactive_backbone_fpn_0"] = (
                        inte_fpn0[rank],
                        inte_fpn_handle0,
                    )
                    frame_buffer["interactive_backbone_fpn_1"] = (
                        inte_fpn1[rank],
                        inte_fpn_handle1,
                    )
                    frame_buffer["interactive_backbone_fpn_2"] = (
                        inte_fpn2[rank],
                        inte_fpn_handle2,
                    )
                    frame_buffer["interactive_backbone_pos_enc"] = (
                        inte_vision_pos_enc,
                        None,
                    )
                frame_buffer["sam2_backbone_fpn_0"] = (fpn0[rank], fpn_handle0)
                frame_buffer["sam2_backbone_fpn_1"] = (fpn1[rank], fpn_handle1)
                frame_buffer["sam2_backbone_fpn_2"] = (fpn2[rank], fpn_handle2)
                frame_buffer["sam2_backbone_pos_enc"] = (vision_pos_enc, None)

            multigpu_buffer[frame_idx_to_save] = frame_buffer

    def _gather_tensor(self, x):
        if self.world_size == 1:
            return [x], None

        async_op = self.async_all_gather
        # here `.contiguous()` is required -- otherwise NCCL all_gather
        # sometimes gives wrong results (based on Ronghang's observations)
        x = x.contiguous()  # ensure contiguous memory for NCCL
        output_list = [torch.empty_like(x) for _ in range(self.world_size)]
        handle = torch.distributed.all_gather(output_list, x, async_op=async_op)
        return output_list, handle

    def forward_video_grounding_batched_multigpu(
        self,
        backbone_out,
        find_inputs,
        geometric_prompt: Prompt,
        frame_idx,
        num_frames,
        # `grounding_cache` is a dict to cache FA outputs in a chunk between different calls
        grounding_cache,
        track_in_reverse=False,
        # whether to also return the SAM2 backbone features (in addition to FA results)
        return_sam2_backbone_feats=False,
        # whether to perform NMS and suppress the scores of those detections removed by NMS
        run_nms=False,
        nms_prob_thresh=None,
        nms_iou_thresh=None,
        nms_use_iom=False,
        # tracking bounds to respect max_frame_num_to_track
        max_frame_num_to_track=None,
        propagate_in_video_start_frame_idx=None,
        # feature_cache for buffered backbone computation
        feature_cache=None,
        # batch_size for batched forward_grounding (default: 16)
        batch_size=16,
    ):
        """
        Fully batched forward_grounding that processes chunks of frames together on each GPU.

        Unlike forward_video_grounding_multigpu which processes 1 frame per GPU per chunk,
        this method processes `batch_size` frames at once using the batched forward_grounding
        approach from Sam3MultiplexImageBase.

        For single-GPU (world_size=1), this is equivalent to forward_grounding_batched.
        For multi-GPU, each GPU processes batch_size frames in parallel.

        Args:
            backbone_out: Dictionary containing backbone outputs and image batch.
            find_inputs: List of FindStage objects for all frames.
            geometric_prompt: Prompt object (used as template, individual prompts are
                constructed from find_inputs for batching).
            frame_idx: Current frame index to process.
            num_frames: Total number of frames in the video.
            grounding_cache: Dictionary to cache grounding outputs.
            track_in_reverse: If True, processing in reverse frame order.
            return_sam2_backbone_feats: Whether to also return SAM2 backbone features.
            run_nms: Whether to perform NMS on detection outputs.
            nms_prob_thresh: Probability threshold for NMS.
            nms_iou_thresh: IoU threshold for NMS.
            nms_use_iom: Whether to use IoM for NMS.
            max_frame_num_to_track: Maximum number of frames to track.
            propagate_in_video_start_frame_idx: Start frame index for propagation.
            feature_cache: Optional dictionary for backbone feature caching.
            batch_size: Number of frames to batch together per GPU (default: 16).

        Returns:
            Tuple of (out, backbone_out) where out contains detection results for frame_idx.
        """
        # Calculate valid frame range based on max_frame_num_to_track
        if max_frame_num_to_track is not None:
            if propagate_in_video_start_frame_idx is None:
                propagate_in_video_start_frame_idx = 0
            if track_in_reverse:
                valid_frame_start = (
                    propagate_in_video_start_frame_idx - max_frame_num_to_track + 1
                )
                valid_frame_end = propagate_in_video_start_frame_idx
            else:
                valid_frame_start = propagate_in_video_start_frame_idx
                valid_frame_end = (
                    propagate_in_video_start_frame_idx + max_frame_num_to_track
                )
        else:
            valid_frame_start = 0
            valid_frame_end = num_frames

        # Initialize grounding_buffer if not present
        if "grounding_buffer" not in grounding_cache:
            grounding_cache["grounding_buffer"] = {}

        # Calculate chunk boundaries - use batch_size instead of world_size
        chunk_start = (frame_idx // batch_size) * batch_size
        chunk_end = min(chunk_start + batch_size, valid_frame_end)
        chunk_key = (chunk_start, chunk_end)

        # Process chunk if not already cached
        if chunk_key not in grounding_cache["grounding_buffer"]:
            with torch.profiler.record_function(
                "forward_grounding_batched.process_chunk"
            ):
                chunk_outputs = self._process_grounding_chunk_batched(
                    backbone_out=backbone_out,
                    find_inputs=find_inputs,
                    chunk_start=chunk_start,
                    chunk_end=chunk_end,
                    run_nms=run_nms,
                    nms_prob_thresh=nms_prob_thresh,
                    nms_iou_thresh=nms_iou_thresh,
                    nms_use_iom=nms_use_iom,
                    feature_cache=feature_cache,
                    return_sam2_backbone_feats=return_sam2_backbone_feats,
                )
                grounding_cache["grounding_buffer"][chunk_key] = chunk_outputs

            # Auto-cleanup previous chunks
            self._cleanup_previous_chunks_multigpu(
                grounding_cache=grounding_cache,
                current_chunk_key=chunk_key,
                batch_size=batch_size,
                num_frames=num_frames,
                track_in_reverse=track_in_reverse,
            )

        # Retrieve the cached output for this frame
        chunk_outputs = grounding_cache["grounding_buffer"][chunk_key]
        local_idx = frame_idx - chunk_start

        # Slice out the output for this specific frame
        out = self._slice_batched_output(
            chunk_outputs, local_idx, return_sam2_backbone_feats
        )

        return out, backbone_out

    def _process_grounding_chunk_batched(
        self,
        backbone_out,
        find_inputs,
        chunk_start: int,
        chunk_end: int,
        run_nms: bool,
        nms_prob_thresh,
        nms_iou_thresh,
        nms_use_iom: bool,
        feature_cache,
        return_sam2_backbone_feats: bool,
    ):
        """
        Process a chunk of frames through the full forward_grounding pipeline in batch.
        """
        chunk_size = chunk_end - chunk_start

        # Build geometric prompts for the chunk
        chunk_geo_prompts = [
            self._get_geo_prompt_from_find_input(find_inputs[i % len(find_inputs)])
            for i in range(chunk_start, chunk_end)
        ]

        # Batch the find_inputs for this chunk
        batched_find_input = self._batch_find_inputs(
            find_inputs, chunk_start, chunk_end
        )

        # Batch the geometric prompts
        batched_geometric_prompt = self._batch_geometric_prompts_from_list(
            chunk_geo_prompts
        )

        # Run forward_grounding on the batched input
        with torch.profiler.record_function("forward_grounding_batched.forward"):
            out = self.forward_grounding(
                backbone_out=backbone_out,
                find_input=batched_find_input,
                find_target=None,
                geometric_prompt=batched_geometric_prompt,
                feature_cache=feature_cache,
            )

        # Apply NMS per frame in the batch
        if run_nms:
            with torch.profiler.record_function("forward_grounding_batched.nms"):
                assert nms_prob_thresh is not None and nms_iou_thresh is not None
                pred_probs = out["pred_logits"].squeeze(-1).sigmoid()
                pred_masks = out["pred_masks"]
                # pred_probs shape: [batch_size, num_queries]
                # pred_masks shape: [batch_size, num_queries, H, W]
                # Use batched NMS to process all frames at once
                keep = nms_masks(
                    pred_probs=pred_probs,
                    pred_masks=pred_masks,
                    prob_threshold=nms_prob_thresh,
                    iou_threshold=nms_iou_thresh,
                    nms_use_iom=nms_use_iom,
                    do_compile=getattr(self, "compile_model", False),
                    running_in_prod=getattr(self, "running_in_prod", False),
                )
                # Set a very low threshold for detections removed by NMS
                # keep shape: [batch_size, num_queries]
                out["pred_logits"][:, :, 0] -= 1e4 * (~keep).float()

        # Extract SAM2 backbone features if requested
        if return_sam2_backbone_feats and "prev_encoder_out" in out:
            backbone_data = out["prev_encoder_out"]["backbone_out"]
            if self.is_multiplex and "interactive" in backbone_data:
                out["_interactive_backbone"] = backbone_data["interactive"]
            if "sam2_backbone_out" in backbone_data:
                out["_sam2_backbone"] = backbone_data["sam2_backbone_out"]

        out["_chunk_size"] = chunk_size
        return out

    def _slice_batched_output(
        self,
        chunk_outputs,
        local_idx: int,
        return_sam2_backbone_feats: bool,
    ):
        """
        Slice a single frame's output from the batched chunk outputs.
        """
        out = {}

        # Keys to slice at batch dimension
        batch_dim_keys = {
            "pred_logits",
            "pred_boxes",
            "pred_boxes_xyxy",
            "pred_masks",
            "pred_logits_o2m",
            "pred_boxes_o2m",
            "pred_boxes_xyxy_o2m",
            "pred_masks_o2m",
            "queries",
            "presence_logit_dec",
        }

        # Keys to skip
        skip_keys = {
            "_chunk_size",
            "_interactive_backbone",
            "_sam2_backbone",
            "prev_encoder_out",
            "encoder_hidden_states",
            "aux_outputs",
        }

        for key, value in chunk_outputs.items():
            if key in skip_keys:
                continue
            if key in batch_dim_keys and isinstance(value, torch.Tensor):
                out[key] = value[local_idx : local_idx + 1]
            elif isinstance(value, torch.Tensor):
                try:
                    out[key] = value[local_idx : local_idx + 1]
                except (IndexError, RuntimeError):
                    out[key] = value

        # Add object IDs
        if "pred_logits" in out:
            out["pred_object_ids"] = self._get_dummy_object_ids(out["pred_logits"])

        # Add SAM2 backbone features if requested
        if return_sam2_backbone_feats:
            if "_sam2_backbone" in chunk_outputs:
                sam2_bb = chunk_outputs["_sam2_backbone"]
                out["sam2_backbone_fpn_0"] = sam2_bb["backbone_fpn"][0].tensors[
                    local_idx : local_idx + 1
                ]
                out["sam2_backbone_fpn_1"] = sam2_bb["backbone_fpn"][1].tensors[
                    local_idx : local_idx + 1
                ]
                out["sam2_backbone_fpn_2"] = sam2_bb["backbone_fpn"][2].tensors[
                    local_idx : local_idx + 1
                ]
                out["sam2_backbone_pos_enc"] = [
                    x[local_idx : local_idx + 1] for x in sam2_bb["vision_pos_enc"]
                ]

            if self.is_multiplex and "_interactive_backbone" in chunk_outputs:
                inte_bb = chunk_outputs["_interactive_backbone"]
                out["interactive_backbone_fpn_0"] = inte_bb["backbone_fpn"][0].tensors[
                    local_idx : local_idx + 1
                ]
                out["interactive_backbone_fpn_1"] = inte_bb["backbone_fpn"][1].tensors[
                    local_idx : local_idx + 1
                ]
                out["interactive_backbone_fpn_2"] = inte_bb["backbone_fpn"][2].tensors[
                    local_idx : local_idx + 1
                ]
                out["interactive_backbone_pos_enc"] = [
                    x[local_idx : local_idx + 1] for x in inte_bb["vision_pos_enc"]
                ]

        return out

    def _cleanup_previous_chunks_multigpu(
        self,
        grounding_cache,
        current_chunk_key,
        batch_size: int,
        num_frames: int,
        track_in_reverse: bool,
    ):
        """Remove previous chunks from cache to save GPU memory."""
        chunk_start, chunk_end = current_chunk_key

        if not track_in_reverse:
            prev_chunk_start = chunk_start - batch_size
            if prev_chunk_start >= 0:
                prev_chunk_end = chunk_start
                prev_chunk_key = (prev_chunk_start, prev_chunk_end)

                # Cleanup grounding_buffer entry
                chunk = grounding_cache["grounding_buffer"].pop(prev_chunk_key, None)
                if chunk is not None:
                    del chunk
        else:
            next_chunk_start = chunk_end
            if next_chunk_start < num_frames:
                next_chunk_end = min(next_chunk_start + batch_size, num_frames)
                next_chunk_key = (next_chunk_start, next_chunk_end)
                grounding_cache["grounding_buffer"].pop(next_chunk_key, None)



================================================
FILE: sam3/model/sam3_multiplex_detector_utils.py
================================================
import logging

import numpy as np
import torch
from sam3 import perflib

try:
    # Ronghang's generic GPU NMS implementation; install via
    # pip uninstall -y torch_generic_nms; TORCH_CUDA_ARCH_LIST="8.0 9.0" pip install git+https://github.com/ronghanghu/torch_generic_nms
    from torch_generic_nms import generic_nms

    GENERIC_NMS_AVAILABLE = True
except ImportError:
    GENERIC_NMS_AVAILABLE = False

from sam3.perflib.masks_ops import mask_iou
from sam3.train.masks_ops import mask_iom


def nms_masks(
    pred_probs: torch.Tensor,
    pred_masks: torch.Tensor,
    prob_threshold: float,
    iou_threshold: float,
    nms_use_iom: bool = False,
    do_compile: bool = False,
    running_in_prod: bool = False,
) -> torch.Tensor:
    """
    Args:
      - pred_probs: (num_det,) or (B, num_det) float Tensor, containing the score (probability) of each detection
      - pred_masks: (num_det, H_mask, W_mask) or (B, num_det, H_mask, W_mask) float Tensor, containing the binary segmentation mask of each detection
      - prob_threshold: float, score threshold to prefilter detections (NMS is performed on detections above threshold)
      - iou_threshold: float, mask IoU threshold for NMS (it would also be used as IoM threshold if `nms_use_iom` is True)
      - nms_use_iom: bool, if True, use IoM instead of IoU for NMS
      - do_compile: bool, whether to compile the function for optimization
      - running_in_prod: bool, whether the function is running in production (ie, in Instagram)

    Returns:
     - keep: (num_det,) or (B, num_det) bool Tensor, indicating whether each detection is kept after score thresholding + NMS
    """
    if do_compile and perflib.is_enabled:
        # Apply torch.compile with the same settings as before
        compiled_fn = torch.compile(
            _nms_masks_core,
            mode="max-autotune",
            fullgraph=True,
            # dynamic=False,
        )
        return compiled_fn(
            pred_probs, pred_masks, prob_threshold, iou_threshold, nms_use_iom
        )
    else:
        return _nms_masks_core(
            pred_probs, pred_masks, prob_threshold, iou_threshold, nms_use_iom
        )


def _nms_masks_core(
    pred_probs: torch.Tensor,
    pred_masks: torch.Tensor,
    prob_threshold: float,
    iou_threshold: float,
    nms_use_iom: bool = False,
) -> torch.Tensor:
    """Core NMS implementation without compilation.

    Supports both single-frame and batched inputs:
      - Single-frame: pred_probs (num_det,), pred_masks (num_det, H, W)
      - Batched: pred_probs (B, num_det), pred_masks (B, num_det, H, W)

    Returns:
      - keep: bool Tensor with same leading dimensions as input, indicating kept detections
    """
    # Check if input is batched (has batch dimension)
    is_batched = pred_probs.dim() == 2

    if is_batched:
        return _nms_masks_core_batched(
            pred_probs, pred_masks, prob_threshold, iou_threshold, nms_use_iom
        )
    else:
        # Single-frame input: use original logic
        return _nms_masks_core_single(
            pred_probs, pred_masks, prob_threshold, iou_threshold, nms_use_iom
        )


def _nms_masks_core_batched(
    pred_probs: torch.Tensor,
    pred_masks: torch.Tensor,
    prob_threshold: float,
    iou_threshold: float,
    nms_use_iom: bool = False,
) -> torch.Tensor:
    """Core NMS implementation for batched inputs using vectorized operations.

    Args:
      - pred_probs: (B, num_det) float Tensor
      - pred_masks: (B, num_det, H_mask, W_mask) float Tensor
      - prob_threshold: float, score threshold to prefilter detections
      - iou_threshold: float, mask IoU/IoM threshold for NMS
      - nms_use_iom: bool, if True, use IoM instead of IoU for NMS

    Returns:
      - keep: (B, num_det) bool Tensor
    """
    B, num_det, H, W = pred_masks.shape
    device = pred_masks.device

    is_valid = pred_probs > prob_threshold  # (B, num_det)
    masks_binary = pred_masks > 0  # (B, num_det, H, W)

    if perflib.is_enabled:
        # Compute batched pairwise IoU/IoM
        if nms_use_iom:
            overlaps = _batched_mask_iom(masks_binary)  # (B, num_det, num_det)
        else:
            overlaps = _batched_mask_iou(masks_binary)  # (B, num_det, num_det)
        keep = _batched_generic_nms_mask(overlaps, pred_probs, is_valid, iou_threshold)
        return keep

    # Non-perflib path: compute batched IoU/IoM
    if nms_use_iom:
        overlaps = _batched_mask_iom(masks_binary)  # (B, num_det, num_det)
    else:
        overlaps = _batched_mask_iou(masks_binary)  # (B, num_det, num_det)

    # Apply batched NMS
    keep = _batched_generic_nms_mask(overlaps, pred_probs, is_valid, iou_threshold)
    return keep


def _batched_mask_iou(masks: torch.Tensor) -> torch.Tensor:
    """Compute batched pairwise IoU for masks.

    Args:
      - masks: (B, N, H, W) bool Tensor

    Returns:
      - ious: (B, N, N) float Tensor
    """
    B, N, H, W = masks.shape
    # Flatten spatial dims: (B, N, H*W)
    masks_flat = masks.reshape(B, N, -1).float()

    # Compute intersection via batched matrix multiplication: (B, N, N)
    intersection = torch.bmm(masks_flat, masks_flat.transpose(1, 2))

    # Compute areas: (B, N)
    areas = masks_flat.sum(dim=-1)

    # Compute union: (B, N, N)
    union = areas.unsqueeze(2) + areas.unsqueeze(1) - intersection

    return intersection / (union + 1e-8)


def _batched_mask_iom(masks: torch.Tensor) -> torch.Tensor:
    """Compute batched pairwise IoM (Intersection over Minimum) for masks.

    Args:
      - masks: (B, N, H, W) bool Tensor

    Returns:
      - ioms: (B, N, N) float Tensor
    """
    B, N, H, W = masks.shape
    # Flatten spatial dims: (B, N, H*W)
    masks_flat = masks.reshape(B, N, -1).float()

    # Compute intersection via batched matrix multiplication: (B, N, N)
    intersection = torch.bmm(masks_flat, masks_flat.transpose(1, 2))

    # Compute areas: (B, N)
    areas = masks_flat.sum(dim=-1)

    # Compute min area: (B, N, N)
    min_area = torch.minimum(areas.unsqueeze(2), areas.unsqueeze(1))

    return intersection / (min_area + 1e-8)


def _batched_generic_nms_mask(
    ious: torch.Tensor,
    scores: torch.Tensor,
    is_valid: torch.Tensor,
    iou_threshold: float,
) -> torch.Tensor:
    """Batched NMS using vectorized operations.

    Args:
      - ious: (B, N, N) float Tensor, pairwise IoU/IoM matrix
      - scores: (B, N) float Tensor, detection scores
      - is_valid: (B, N) bool Tensor, valid detections mask
      - iou_threshold: float, threshold for suppression

    Returns:
      - keep: (B, N) bool Tensor
    """
    B, N = scores.shape
    device = scores.device

    # Sort by score descending for each batch: (B, N)
    order = scores.argsort(dim=-1, descending=True)

    # Create batch indices for advanced indexing
    batch_idx = torch.arange(B, device=device).unsqueeze(1).expand(B, N)

    # Reorder IoU matrix according to sorted scores: (B, N, N)
    # ious_sorted[b, i, j] = ious[b, order[b, i], order[b, j]]
    ious_sorted = ious[batch_idx.unsqueeze(2), order.unsqueeze(2), order.unsqueeze(1)]

    # Create threshold mask: (B, N, N)
    threshold_mask = ious_sorted > iou_threshold

    # Initialize keep mask with valid detections in sorted order: (B, N)
    keep = is_valid[batch_idx, order]

    # Upper triangular mask to avoid double processing: (N, N)
    triu = torch.triu(torch.ones(N, N, device=device, dtype=torch.bool), diagonal=1)

    # Vectorized NMS - iterate through detections
    for i in range(N):
        # For each position i, suppress later detections with high overlap
        # Only suppress if current detection is kept
        suppress = (
            threshold_mask[:, i, :] & triu[i].unsqueeze(0) & keep[:, i].unsqueeze(1)
        )
        keep = keep & ~suppress

    # Return keep mask in original order: (B, N)
    original_keep = torch.zeros_like(keep)
    original_keep[batch_idx, order] = keep
    return original_keep


def _nms_masks_core_single(
    pred_probs: torch.Tensor,
    pred_masks: torch.Tensor,
    prob_threshold: float,
    iou_threshold: float,
    nms_use_iom: bool = False,
) -> torch.Tensor:
    """Core NMS implementation for a single frame (no batch dimension).

    Args:
      - pred_probs: (num_det,) float Tensor
      - pred_masks: (num_det, H_mask, W_mask) float Tensor
      - prob_threshold: float, score threshold to prefilter detections
      - iou_threshold: float, mask IoU/IoM threshold for NMS
      - nms_use_iom: bool, if True, use IoM instead of IoU for NMS

    Returns:
      - keep: (num_det,) bool Tensor
    """
    is_valid = pred_probs > prob_threshold  # (num_det,)

    if perflib.is_enabled:
        masks_binary = pred_masks > 0  # (num_det, H_mask, W_mask)
        if nms_use_iom:
            ious = perf_mask_iom(masks_binary, masks_binary)  # (num_det, num_det)
        else:
            ious = perf_mask_iou(masks_binary, masks_binary)  # (num_det, num_det)
        kept_mask = generic_nms_mask(ious, pred_probs, is_valid, iou_threshold)
        return kept_mask
    # prefilter the detections with prob_threshold ("valid" are those above prob_threshold)
    probs = pred_probs[is_valid]  # (num_valid,)
    masks_binary = pred_masks[is_valid] > 0  # (num_valid, H_mask, W_mask)
    if probs.numel() == 0:
        return is_valid  # no valid detection, return empty keep mask

    if nms_use_iom:
        overlaps = mask_iom(masks_binary, masks_binary)  # (num_valid, num_valid)
    else:
        overlaps = mask_iou(masks_binary, masks_binary)  # (num_valid, num_valid)
    # kept_inds are the indices among `probs` of those kept detections after NMS
    if GENERIC_NMS_AVAILABLE:
        kept_inds = generic_nms(overlaps, probs, iou_threshold, use_iou_matrix=True)
    else:
        logging.warning(
            "Falling back to CPU mask NMS implementation -- please install `torch_generic_nms` via\n\t"
            'pip uninstall -y torch_generic_nms; TORCH_CUDA_ARCH_LIST="8.0 9.0" pip install git+https://github.com/ronghanghu/torch_generic_nms'
        )
        kept_inds = generic_nms_cpu(overlaps, probs, iou_threshold)

    # valid_inds are the indices among `probs` of valid detections before NMS (or -1 for invalid)
    valid_inds = torch.where(is_valid, is_valid.cumsum(dim=0) - 1, -1)  # (num_det,)
    keep = torch.isin(valid_inds, kept_inds)  # (num_det,)
    return keep


def generic_nms_cpu(
    ious: torch.Tensor, scores: torch.Tensor, iou_threshold=0.5
) -> torch.Tensor:
    """
    A generic version of `torchvision.ops.nms` that takes a pairwise IoU matrix. (CPU implementation
    based on https://github.com/jwyang/faster-rcnn.pytorch/blob/master/lib/model/nms/nms_cpu.py)
    """
    ious_np = ious.float().detach().cpu().numpy()
    scores_np = scores.float().detach().cpu().numpy()
    order = scores_np.argsort()[::-1]
    kept_inds = []
    while order.size > 0:
        i = order.item(0)
        kept_inds.append(i)
        inds = np.where(ious_np[i, order[1:]] <= iou_threshold)[0]
        order = order[inds + 1]

    return torch.tensor(kept_inds, dtype=torch.int64, device=scores.device)


def generic_nms_mask(
    ious: torch.Tensor, scores: torch.Tensor, is_valid: torch.Tensor, iou_threshold=0.5
) -> torch.Tensor:
    """
    A generic version of `torchvision.ops.nms` that takes a pairwise IoU matrix. (CPU implementation
    using vectorized operations similar to nms_masks_kernel)
    """
    # Sort by score descending
    order = scores.argsort(descending=True)

    # Reorder IoU matrix according to sorted scores
    ious_sorted = ious[order][:, order]

    # Create threshold mask
    threshold_mask = ious_sorted > iou_threshold

    # Initialize keep mask
    # keep = torch.ones(len(scores), device=ious.device, dtype=torch.bool)
    keep = is_valid[order]

    # Upper triangular mask to avoid double processing
    tr = torch.triu(torch.ones_like(threshold_mask), diagonal=1)

    # Vectorized NMS
    for i in range(len(scores)):
        # Suppress all boxes that have high IoU with current box
        m = threshold_mask[i]
        keep = torch.where(m & tr[i], torch.zeros_like(keep), keep)

    # Return keep mask in original order
    original_keep = torch.zeros_like(keep)
    original_keep[order] = keep
    return original_keep


def perf_mask_iou(pred_masks: torch.Tensor, gt_masks: torch.Tensor) -> torch.Tensor:
    """
    Compute the IoU (Intersection over Union) between predicted masks and ground truth masks.

    Args:
      - pred_masks: (N, H, W) bool Tensor, containing binary predicted segmentation masks
      - gt_masks: (M, H, W) bool Tensor, containing binary ground truth segmentation masks

    Returns:
      - ious: (N, M) float Tensor, containing IoUs for each pair of predicted and ground truth masks
    """
    assert pred_masks.dtype == gt_masks.dtype == torch.bool
    from sam3.perflib.iou import pairwise_iou

    return pairwise_iou(pred_masks, gt_masks, eps=None)


def perf_mask_iom(pred_masks: torch.Tensor, gt_masks: torch.Tensor) -> torch.Tensor:
    assert pred_masks.dtype == gt_masks.dtype == torch.bool
    from sam3.perflib.iou import pairwise_iom

    return pairwise_iom(pred_masks, gt_masks)



================================================
FILE: sam3/model/sam3_multiplex_video_predictor.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

"""
Sam3MultiplexVideoPredictor — user-facing entry point for SAM 3.1 multiplex.

Ported from onevision Sam3Model (webdemo/ta/models/sam3_model.py).
Handles warm-up compilation, bf16 autocast, and session management
via the shared Sam3BasePredictor handle_request/handle_stream_request API.
"""

from typing import Dict, Optional

import torch
from sam3.logger import get_logger
from sam3.model.sam3_base_predictor import Sam3BasePredictor

logger = get_logger(__name__)


class Sam3MultiplexVideoPredictor(Sam3BasePredictor):
    """
    User-facing predictor for SAM 3.1 multiplex video tracking.

    Wraps Sam3MultiplexTrackingWithInteractivity with:
    - bf16 autocast
    - Warm-up compilation (when compile=True)
    - Session expiration management
    - handle_request / handle_stream_request dispatch API (from Sam3BasePredictor)
    """

    def __init__(
        self,
        model,
        session_expiration_sec=1200,
        default_output_prob_thresh=0.5,
        async_loading_frames=True,
        warm_up=False,
    ):
        super().__init__()
        self.model = model
        self.session_expiration_sec = session_expiration_sec
        self.default_output_prob_thresh = default_output_prob_thresh
        self.async_loading_frames = async_loading_frames

        # turn on tfloat32 for Ampere GPUs
        torch.backends.cuda.matmul.allow_tf32 = True
        torch.backends.cudnn.allow_tf32 = True
        # use bfloat16 inference for Flash Attention kernel
        self.bf16_context = torch.autocast(device_type="cuda", dtype=torch.bfloat16)
        self.bf16_context.__enter__()

        if warm_up:
            self.model._warm_up_complete = False
            self.model.warm_up_compilation()
            self.model._warm_up_complete = True

    def _extend_expiration_time(self, session):
        """Update last-use time and store session expiration timeout."""
        super()._extend_expiration_time(session)
        if self.session_expiration_sec:
            session["expiration_sec"] = self.session_expiration_sec



================================================
FILE: sam3/model/sam3_tracker_utils.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

import numpy as np
import torch
import torch.nn.functional as F
from numpy.typing import NDArray
from sam3.model.edt import edt_triton


def sample_box_points(
    masks: torch.Tensor,
    noise: float = 0.1,  # SAM default
    noise_bound: int = 20,  # SAM default
    top_left_label: int = 2,
    bottom_right_label: int = 3,
) -> tuple[NDArray, NDArray]:
    """
    Sample a noised version of the top left and bottom right corners of a given `bbox`

    Inputs:
    - masks: [B, 1, H, W] tensor
    - noise: noise as a fraction of box width and height, dtype=float
    - noise_bound: maximum amount of noise (in pure pixels), dtype=int

    Returns:
    - box_coords: [B, num_pt, 2], contains (x, y) coordinates of top left and bottom right box corners, dtype=torch.float
    - box_labels: [B, num_pt], label 2 is reserverd for top left and 3 for bottom right corners, dtype=torch.int32
    """
    device = masks.device
    box_coords = mask_to_box(masks)
    B, _, H, W = masks.shape
    box_labels = torch.tensor(
        [top_left_label, bottom_right_label], dtype=torch.int, device=device
    ).repeat(B)
    if noise > 0.0:
        if not isinstance(noise_bound, torch.Tensor):
            noise_bound = torch.tensor(noise_bound, device=device)
        bbox_w = box_coords[..., 2] - box_coords[..., 0]
        bbox_h = box_coords[..., 3] - box_coords[..., 1]
        max_dx = torch.min(bbox_w * noise, noise_bound)
        max_dy = torch.min(bbox_h * noise, noise_bound)
        box_noise = 2 * torch.rand(B, 1, 4, device=device) - 1
        box_noise = box_noise * torch.stack((max_dx, max_dy, max_dx, max_dy), dim=-1)

        box_coords = box_coords + box_noise
        img_bounds = (
            torch.tensor([W, H, W, H], device=device) - 1
        )  # uncentered pixel coords
        box_coords.clamp_(torch.zeros_like(img_bounds), img_bounds)  # In place clamping

    box_coords = box_coords.reshape(-1, 2, 2)  # always 2 points
    box_labels = box_labels.reshape(-1, 2)
    return box_coords, box_labels


def mask_to_box(masks: torch.Tensor):
    """
    compute bounding box given an input mask

    Inputs:
    - masks: [B, 1, H, W] tensor

    Returns:
    - box_coords: [B, 1, 4], contains (x, y) coordinates of top left and bottom right box corners, dtype=torch.Tensor
    """
    B, _, h, w = masks.shape
    device = masks.device
    mask_area = masks.sum(dim=(-1, -2))
    xs = torch.arange(w, device=device, dtype=torch.int32)
    ys = torch.arange(h, device=device, dtype=torch.int32)
    grid_xs, grid_ys = torch.meshgrid(xs, ys, indexing="xy")
    grid_xs = grid_xs[None, None, ...].expand(B, 1, h, w)
    grid_ys = grid_ys[None, None, ...].expand(B, 1, h, w)
    min_xs, _ = torch.min(torch.where(masks, grid_xs, w).flatten(-2), dim=-1)
    max_xs, _ = torch.max(torch.where(masks, grid_xs, -1).flatten(-2), dim=-1)
    min_ys, _ = torch.min(torch.where(masks, grid_ys, h).flatten(-2), dim=-1)
    max_ys, _ = torch.max(torch.where(masks, grid_ys, -1).flatten(-2), dim=-1)
    bbox_coords = torch.stack((min_xs, min_ys, max_xs, max_ys), dim=-1)
    bbox_coords = torch.where(
        mask_area[..., None] > 0, bbox_coords, torch.zeros_like(bbox_coords)
    )
    return bbox_coords


def sample_random_points_from_errors(gt_masks, pred_masks, num_pt=1):
    """
    Sample `num_pt` random points (along with their labels) independently from the error regions.

    Inputs:
    - gt_masks: [B, 1, H_im, W_im] masks, dtype=torch.bool
    - pred_masks: [B, 1, H_im, W_im] masks, dtype=torch.bool or None
    - num_pt: int, number of points to sample independently for each of the B error maps

    Outputs:
    - points: [B, num_pt, 2], dtype=torch.float, contains (x, y) coordinates of each sampled point
    - labels: [B, num_pt], dtype=torch.int32, where 1 means positive clicks and 0 means
      negative clicks
    """
    if pred_masks is None:  # if pred_masks is not provided, treat it as empty
        pred_masks = torch.zeros_like(gt_masks)
    assert gt_masks.dtype == torch.bool and gt_masks.size(1) == 1
    assert pred_masks.dtype == torch.bool and pred_masks.shape == gt_masks.shape
    assert num_pt >= 0

    B, _, H_im, W_im = gt_masks.shape
    device = gt_masks.device

    # false positive region, a new point sampled in this region should have
    # negative label to correct the FP error
    fp_masks = ~gt_masks & pred_masks
    # false negative region, a new point sampled in this region should have
    # positive label to correct the FN error
    fn_masks = gt_masks & ~pred_masks
    # whether the prediction completely match the ground-truth on each mask
    all_correct = torch.all((gt_masks == pred_masks).flatten(2), dim=2)
    all_correct = all_correct[..., None, None]

    # channel 0 is FP map, while channel 1 is FN map
    pts_noise = torch.rand(B, num_pt, H_im, W_im, 2, device=device)
    # sample a negative new click from FP region or a positive new click
    # from FN region, depend on where the maximum falls,
    # and in case the predictions are all correct (no FP or FN), we just
    # sample a negative click from the background region
    pts_noise[..., 0] *= fp_masks | (all_correct & ~gt_masks)
    pts_noise[..., 1] *= fn_masks
    pts_idx = pts_noise.flatten(2).argmax(dim=2)
    labels = (pts_idx % 2).to(torch.int32)
    pts_idx = pts_idx // 2
    pts_x = pts_idx % W_im
    pts_y = pts_idx // W_im
    points = torch.stack([pts_x, pts_y], dim=2).to(torch.float)
    return points, labels


def sample_one_point_from_error_center(gt_masks, pred_masks, padding=True):
    """
    Sample 1 random point (along with its label) from the center of each error region,
    that is, the point with the largest distance to the boundary of each error region.
    This is the RITM sampling method from https://github.com/saic-vul/ritm_interactive_segmentation/blob/master/isegm/inference/clicker.py

    Inputs:
    - gt_masks: [B, 1, H_im, W_im] masks, dtype=torch.bool
    - pred_masks: [B, 1, H_im, W_im] masks, dtype=torch.bool or None
    - padding: if True, pad with boundary of 1 px for distance transform

    Outputs:
    - points: [B, 1, 2], dtype=torch.float, contains (x, y) coordinates of each sampled point
    - labels: [B, 1], dtype=torch.int32, where 1 means positive clicks and 0 means negative clicks
    """
    if pred_masks is None:
        pred_masks = torch.zeros_like(gt_masks)
    assert gt_masks.dtype == torch.bool and gt_masks.size(1) == 1
    assert pred_masks.dtype == torch.bool and pred_masks.shape == gt_masks.shape

    B, _, H, W = gt_masks.shape

    # false positive region, a new point sampled in this region should have
    # negative label to correct the FP error
    fp_masks = (~gt_masks & pred_masks).squeeze(1)
    # false negative region, a new point sampled in this region should have
    # positive label to correct the FN error
    fn_masks = (gt_masks & ~pred_masks).squeeze(1)

    if padding:
        padded_fp_masks = torch.zeros(
            B, H + 2, W + 2, dtype=fp_masks.dtype, device=fp_masks.device
        )
        padded_fp_masks[:, 1 : H + 1, 1 : W + 1] = fp_masks
        padded_fn_masks = torch.zeros(
            B, H + 2, W + 2, dtype=fp_masks.dtype, device=fp_masks.device
        )
        padded_fn_masks[:, 1 : H + 1, 1 : W + 1] = fn_masks
    else:
        padded_fp_masks = fp_masks
        padded_fn_masks = fn_masks

    fn_mask_dt = edt_triton(padded_fn_masks)
    fp_mask_dt = edt_triton(padded_fp_masks)
    if padding:
        fn_mask_dt = fn_mask_dt[:, 1:-1, 1:-1]
        fp_mask_dt = fp_mask_dt[:, 1:-1, 1:-1]

    fn_max, fn_argmax = fn_mask_dt.reshape(B, -1).max(dim=-1)
    fp_max, fp_argmax = fp_mask_dt.reshape(B, -1).max(dim=-1)
    is_positive = fn_max > fp_max
    chosen = torch.where(is_positive, fn_argmax, fp_argmax)
    points_x = chosen % W
    points_y = chosen // W

    labels = is_positive.long()
    points = torch.stack([points_x, points_y], -1)
    return points.unsqueeze(1), labels.unsqueeze(1)


def sample_one_point_from_error_center_slow(gt_masks, pred_masks, padding=True):
    """
    Sample 1 random point (along with its label) from the center of each error region,
    that is, the point with the largest distance to the boundary of each error region.
    This is the RITM sampling method from https://github.com/saic-vul/ritm_interactive_segmentation/blob/master/isegm/inference/clicker.py

    Inputs:
    - gt_masks: [B, 1, H_im, W_im] masks, dtype=torch.bool
    - pred_masks: [B, 1, H_im, W_im] masks, dtype=torch.bool or None
    - padding: if True, pad with boundary of 1 px for distance transform

    Outputs:
    - points: [B, 1, 2], dtype=torch.float, contains (x, y) coordinates of each sampled point
    - labels: [B, 1], dtype=torch.int32, where 1 means positive clicks and 0 means negative clicks
    """
    import cv2  # delay OpenCV import to avoid unnecessary dependency

    if pred_masks is None:
        pred_masks = torch.zeros_like(gt_masks)
    assert gt_masks.dtype == torch.bool and gt_masks.size(1) == 1
    assert pred_masks.dtype == torch.bool and pred_masks.shape == gt_masks.shape

    B, _, _, W_im = gt_masks.shape
    device = gt_masks.device

    # false positive region, a new point sampled in this region should have
    # negative label to correct the FP error
    fp_masks = ~gt_masks & pred_masks
    # false negative region, a new point sampled in this region should have
    # positive label to correct the FN error
    fn_masks = gt_masks & ~pred_masks

    fp_masks = fp_masks.cpu().numpy()
    fn_masks = fn_masks.cpu().numpy()
    points = torch.zeros(B, 1, 2, dtype=torch.float)
    labels = torch.ones(B, 1, dtype=torch.int32)
    for b in range(B):
        fn_mask = fn_masks[b, 0]
        fp_mask = fp_masks[b, 0]
        if padding:
            fn_mask = np.pad(fn_mask, ((1, 1), (1, 1)), "constant")
            fp_mask = np.pad(fp_mask, ((1, 1), (1, 1)), "constant")
        # compute the distance of each point in FN/FP region to its boundary
        fn_mask_dt = cv2.distanceTransform(fn_mask.astype(np.uint8), cv2.DIST_L2, 0)
        fp_mask_dt = cv2.distanceTransform(fp_mask.astype(np.uint8), cv2.DIST_L2, 0)
        if padding:
            fn_mask_dt = fn_mask_dt[1:-1, 1:-1]
            fp_mask_dt = fp_mask_dt[1:-1, 1:-1]

        # take the point in FN/FP region with the largest distance to its boundary
        fn_mask_dt_flat = fn_mask_dt.reshape(-1)
        fp_mask_dt_flat = fp_mask_dt.reshape(-1)
        fn_argmax = np.argmax(fn_mask_dt_flat)
        fp_argmax = np.argmax(fp_mask_dt_flat)
        is_positive = fn_mask_dt_flat[fn_argmax] > fp_mask_dt_flat[fp_argmax]
        pt_idx = fn_argmax if is_positive else fp_argmax
        points[b, 0, 0] = pt_idx % W_im  # x
        points[b, 0, 1] = pt_idx // W_im  # y
        labels[b, 0] = int(is_positive)

    points = points.to(device)
    labels = labels.to(device)
    return points, labels


def get_next_point(gt_masks, pred_masks, method):
    if method == "uniform":
        return sample_random_points_from_errors(gt_masks, pred_masks)
    elif method == "center":
        return sample_one_point_from_error_center(gt_masks, pred_masks)
    else:
        raise ValueError(f"unknown sampling method {method}")


def select_closest_cond_frames(
    frame_idx, cond_frame_outputs, max_cond_frame_num, keep_first_cond_frame=False
):
    """
    Select up to `max_cond_frame_num` conditioning frames from `cond_frame_outputs`
    that are temporally closest to the current frame at `frame_idx`. Here, we take
    - a) the closest conditioning frame before `frame_idx` (if any);
    - b) the closest conditioning frame after `frame_idx` (if any);
    - c) any other temporally closest conditioning frames until reaching a total
         of `max_cond_frame_num` conditioning frames.

    Outputs:
    - selected_outputs: selected items (keys & values) from `cond_frame_outputs`.
    - unselected_outputs: items (keys & values) not selected in `cond_frame_outputs`.
    """
    if max_cond_frame_num == -1 or len(cond_frame_outputs) <= max_cond_frame_num:
        selected_outputs = cond_frame_outputs
        unselected_outputs = {}
    else:
        assert max_cond_frame_num >= 2, "we should allow using 2+ conditioning frames"
        selected_outputs = {}
        if keep_first_cond_frame:
            idx_first = min(
                (t for t in cond_frame_outputs if t < frame_idx), default=None
            )
            if idx_first is None:
                # Maybe we are tracking in reverse
                idx_first = max(
                    (t for t in cond_frame_outputs if t > frame_idx), default=None
                )
            if idx_first is not None:
                selected_outputs[idx_first] = cond_frame_outputs[idx_first]
        # the closest conditioning frame before `frame_idx` (if any)
        idx_before = max((t for t in cond_frame_outputs if t < frame_idx), default=None)
        if idx_before is not None:
            selected_outputs[idx_before] = cond_frame_outputs[idx_before]

        # the closest conditioning frame after `frame_idx` (if any)
        idx_after = min((t for t in cond_frame_outputs if t >= frame_idx), default=None)
        if idx_after is not None:
            selected_outputs[idx_after] = cond_frame_outputs[idx_after]

        # add other temporally closest conditioning frames until reaching a total
        # of `max_cond_frame_num` conditioning frames.
        num_remain = max_cond_frame_num - len(selected_outputs)
        inds_remain = sorted(
            (t for t in cond_frame_outputs if t not in selected_outputs),
            key=lambda x: abs(x - frame_idx),
        )[:num_remain]
        selected_outputs.update((t, cond_frame_outputs[t]) for t in inds_remain)
        unselected_outputs = {
            t: v for t, v in cond_frame_outputs.items() if t not in selected_outputs
        }

    return selected_outputs, unselected_outputs


def get_1d_sine_pe(pos_inds, dim, temperature=10000):
    """
    Get 1D sine positional embedding as in the original Transformer paper.
    """
    pe_dim = dim // 2
    dim_t = torch.arange(pe_dim, dtype=torch.float32, device=pos_inds.device)
    dim_t = temperature ** (2 * (dim_t // 2) / pe_dim)

    pos_embed = pos_inds.unsqueeze(-1) / dim_t
    pos_embed = torch.cat([pos_embed.sin(), pos_embed.cos()], dim=-1)
    return pos_embed


def get_best_gt_match_from_multimasks(pred_multimasks, gt_masks, pred_scores=None):
    """
    Get the mask with the best match to GT masks (based on IoU) from pred_multimasks.
    Optionally, use `pred_scores` to break ties in case all IoUs are zeros.
    """
    assert pred_multimasks.ndim == 4 and gt_masks.ndim == 4
    if pred_multimasks.size(1) == 1:
        return pred_multimasks  # only a single mask channel, nothing to select

    pred_multimasks_binary = pred_multimasks > 0
    area_i = torch.sum(pred_multimasks_binary & gt_masks, dim=(2, 3)).float()
    area_u = torch.sum(pred_multimasks_binary | gt_masks, dim=(2, 3)).float()
    ious = area_i / torch.clamp(area_u, min=1.0)

    # In case all IoUs are zeros (e.g. because the GT mask is empty), use pred_scores
    # to break ties and select the best mask
    if pred_scores is not None:
        has_nonzero_ious = torch.any(ious > 0).expand_as(ious)
        scores = torch.where(has_nonzero_ious, ious, pred_scores)
    else:
        scores = ious

    # Finally, take the best mask prediction (with the highest score)
    best_scores_inds = torch.argmax(scores, dim=-1)
    batch_inds = torch.arange(scores.size(0), device=scores.device)
    best_pred_mask = pred_multimasks[batch_inds, best_scores_inds].unsqueeze(1)
    return best_pred_mask


def fill_holes_in_mask_scores(
    mask,
    max_area=None,
    fill_holes=True,
    remove_sprinkles=True,
    fill_hole_area=None,
    sprinkle_removal_area=None,
):
    # Support onevision-style keyword args
    if fill_hole_area is not None and max_area is None:
        max_area = fill_hole_area
    """
    A post processor to fill small holes in mask scores with area under `max_area`.
    Holes are those small connected components in either background or foreground.

    Note that it relies on the "cc_torch" package to find connected components fast. You can
    install it via the following command (`TORCH_CUDA_ARCH_LIST=8.0` is for A100 GPUs):
    ```
    pip uninstall -y cc_torch; TORCH_CUDA_ARCH_LIST=8.0 9.0 pip install git+https://github.com/ronghanghu/cc_torch
    ```
    Otherwise, it will fallback to a slightly slower triton implementation, or skimage if the tensor is on cpu
    """

    if max_area <= 0:
        return mask  # nothing to fill in this case

    if fill_holes:
        # We remove small connected components in background by changing them to foreground
        # with a small positive mask score (0.1).
        mask_bg = mask <= 0
        bg_area_thresh = max_area
        _, areas_bg = _get_connected_components_with_padding(mask_bg)
        small_components_bg = mask_bg & (areas_bg <= bg_area_thresh)
        mask = torch.where(small_components_bg, 0.1, mask)

    if remove_sprinkles:
        # We remove small connected components in foreground by changing them to background
        # with a small negative mask score (-0.1). Here we only remove connected components
        # whose areas are under both `max_area` and half of the entire mask's area. This
        # removes sprinkles while avoids filtering out tiny objects that we want to track.
        mask_fg = mask > 0
        fg_area_thresh = torch.sum(mask_fg, dim=(2, 3), keepdim=True, dtype=torch.int32)
        fg_area_thresh.floor_divide_(2).clamp_(max=max_area)
        _, areas_fg = _get_connected_components_with_padding(mask_fg)
        small_components_fg = mask_fg & (areas_fg <= fg_area_thresh)
        mask = torch.where(small_components_fg, -0.1, mask)
    return mask


def _get_connected_components_with_padding(mask):
    """Get connected components from masks (possibly padding them to an even size)."""
    from sam3.perflib.connected_components import connected_components

    mask = mask.to(torch.uint8)
    _, _, H, W = mask.shape
    # make sure both height and width are even (to be compatible with cc_torch)
    pad_h = H % 2
    pad_w = W % 2
    if pad_h == 0 and pad_w == 0:
        labels, counts = connected_components(mask)
    else:
        # pad the mask to make its height and width even
        # padding format is (padding_left,padding_right,padding_top,padding_bottom)
        mask_pad = F.pad(mask, (0, pad_w, 0, pad_h), mode="constant", value=0)
        labels, counts = connected_components(mask_pad)
        labels = labels[:, :, :H, :W]
        counts = counts[:, :, :H, :W]

    return labels, counts



================================================
FILE: sam3/model/sam3_video_predictor.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

import datetime
import gc
import multiprocessing as mp
import os
import queue
import socket
import sys
import time
import uuid
from contextlib import closing
from typing import List, Optional

import psutil
import torch
from sam3.logger import get_logger
from sam3.model.sam3_base_predictor import Sam3BasePredictor

logger = get_logger(__name__)


class Sam3VideoPredictor(Sam3BasePredictor):
    def __init__(
        self,
        checkpoint_path=None,
        bpe_path=None,
        has_presence_token=True,
        geo_encoder_use_img_cross_attn=True,
        strict_state_dict_loading=True,
        async_loading_frames=False,
        video_loader_type="cv2",
        apply_temporal_disambiguation: bool = True,
        compile: bool = False,
    ):
        super().__init__()
        self.async_loading_frames = async_loading_frames
        self.video_loader_type = video_loader_type
        from sam3.model_builder import build_sam3_video_model

        self.model = (
            build_sam3_video_model(
                checkpoint_path=checkpoint_path,
                bpe_path=bpe_path,
                has_presence_token=has_presence_token,
                geo_encoder_use_img_cross_attn=geo_encoder_use_img_cross_attn,
                strict_state_dict_loading=strict_state_dict_loading,
                apply_temporal_disambiguation=apply_temporal_disambiguation,
                compile=compile,
            )
            .cuda()
            .eval()
        )

    def remove_object(
        self,
        session_id: str,
        frame_idx: int = 0,
        obj_id: int = 0,
        is_user_action: bool = True,
    ):
        """Remove an object from tracking (SAM3 uses a simpler remove_object API)."""
        session = self._get_session(session_id)
        inference_state = session["state"]

        self.model.remove_object(
            inference_state=inference_state,
            obj_id=obj_id,
            is_user_action=is_user_action,
        )
        return {"is_success": True}

    def _get_session_stats(self):
        """Get a statistics string for live sessions and their GPU usage."""
        live_session_strs = []
        for sid, s in self._all_inference_states.items():
            nf = s["state"]["num_frames"]
            live_session_strs.append(f"'{sid}' ({nf} frames)")
        joined = ", ".join(live_session_strs)
        mem_alloc = torch.cuda.memory_allocated() // 1024**2
        mem_res = torch.cuda.memory_reserved() // 1024**2
        max_alloc = torch.cuda.max_memory_allocated() // 1024**2
        max_res = torch.cuda.max_memory_reserved() // 1024**2
        return (
            f"live sessions: [{joined}], GPU memory: "
            f"{mem_alloc} MiB used and {mem_res} MiB reserved"
            f" (max over time: {max_alloc} MiB used and {max_res} MiB reserved)"
        )

    def _get_torch_and_gpu_properties(self):
        """Get a string for PyTorch and GPU properties."""
        return (
            f"torch: {torch.__version__} with CUDA arch {torch.cuda.get_arch_list()}, "
            f"GPU device: {torch.cuda.get_device_properties(torch.cuda.current_device())}"
        )


class Sam3VideoPredictorMultiGPU(Sam3VideoPredictor):
    def __init__(self, *model_args, gpus_to_use=None, **model_kwargs):
        if gpus_to_use is None:
            # if not specified, use only the current GPU by default
            gpus_to_use = [torch.cuda.current_device()]

        IS_MAIN_PROCESS = os.getenv("IS_MAIN_PROCESS", "1") == "1"
        if IS_MAIN_PROCESS:
            gpus_to_use = sorted(set(gpus_to_use))
            logger.info(f"using the following GPU IDs: {gpus_to_use}")
            assert len(gpus_to_use) > 0 and all(isinstance(i, int) for i in gpus_to_use)
            assert all(0 <= i < torch.cuda.device_count() for i in gpus_to_use)
            os.environ["MASTER_ADDR"] = "localhost"
            os.environ["MASTER_PORT"] = f"{self._find_free_port()}"
            os.environ["RANK"] = "0"
            os.environ["WORLD_SIZE"] = f"{len(gpus_to_use)}"

        self.gpus_to_use = gpus_to_use
        self.rank = int(os.environ["RANK"])
        self.world_size = int(os.environ["WORLD_SIZE"])
        self.rank_str = f"rank={self.rank} with world_size={self.world_size}"
        self.device = torch.device(f"cuda:{self.gpus_to_use[self.rank]}")
        torch.cuda.set_device(self.device)
        self.has_shutdown = False
        if self.rank == 0:
            logger.info("\n\n\n\t*** START loading model on all ranks ***\n\n")

        logger.info(f"loading model on {self.rank_str} -- this could take a while ...")
        super().__init__(*model_args, **model_kwargs)
        logger.info(f"loading model on {self.rank_str} -- DONE locally")

        if self.world_size > 1 and self.rank == 0:
            # start the worker processes *after* the model is loaded in the main process
            # so that the main process can run torch.compile and fill the cache first
            self._start_worker_processes(*model_args, **model_kwargs)
            for rank in range(1, self.world_size):
                self.command_queues[rank].put(("start_nccl_process_group", None))
            self._start_nccl_process_group()

        if self.rank == 0:
            logger.info("\n\n\n\t*** DONE loading model on all ranks ***\n\n")

    @torch.inference_mode()
    def handle_request(self, request):
        """Dispatch a request based on its type."""
        if self.has_shutdown:
            raise RuntimeError(
                "cannot handle request after the predictor has shutdown; please create a new predictor"
            )

        # when starting a session, we need to create a session id before dispatching
        # the request to the workers
        if request["type"] == "start_session" and request.get("session_id") is None:
            request["session_id"] = str(uuid.uuid4())
        # dispatch the request to all worker processes
        if self.world_size > 1 and self.rank == 0:
            for rank in range(1, self.world_size):
                self.command_queues[rank].put((request, False))

        response = super().handle_request(request)

        if self.world_size > 1:
            torch.distributed.barrier()  # wait for all ranks to finish
        return response

    @torch.inference_mode()
    def handle_stream_request(self, request):
        """Dispatch a stream request based on its type."""
        if self.has_shutdown:
            raise RuntimeError(
                "cannot handle request after the predictor has shutdown; please create a new predictor"
            )

        # dispatch the request to all worker processes
        if self.world_size > 1 and self.rank == 0:
            for rank in range(1, self.world_size):
                self.command_queues[rank].put((request, True))

        yield from super().handle_stream_request(request)

        if self.world_size > 1:
            torch.distributed.barrier()  # wait for all ranks to finish

    def _start_worker_processes(self, *model_args, **model_kwargs):
        """Start worker processes for handling model inference."""
        world_size = self.world_size
        logger.info(f"spawning {world_size - 1} worker processes")
        # Use "spawn" (instead of "fork") for different PyTorch or CUDA context
        mp_ctx = mp.get_context("spawn")
        self.command_queues = {rank: mp_ctx.Queue() for rank in range(1, world_size)}
        self.result_queues = {rank: mp_ctx.Queue() for rank in range(1, world_size)}
        parent_pid = os.getpid()
        for rank in range(1, world_size):
            # set the environment variables for each worker process
            os.environ["IS_MAIN_PROCESS"] = "0"  # mark this as a worker process
            os.environ["RANK"] = f"{rank}"
            worker_process = mp_ctx.Process(
                target=Sam3VideoPredictorMultiGPU._worker_process_command_loop,
                args=(
                    rank,
                    world_size,
                    self.command_queues[rank],
                    self.result_queues[rank],
                    model_args,
                    model_kwargs,
                    self.gpus_to_use,
                    parent_pid,
                ),
                daemon=True,
            )
            worker_process.start()
        # revert the environment variables for the main process
        os.environ["IS_MAIN_PROCESS"] = "1"
        os.environ["RANK"] = "0"
        # wait for all the worker processes to load the model and collect their PIDs
        self.worker_pids = {}
        for rank in range(1, self.world_size):
            # a large timeout to cover potentially long model loading time due to compilation
            _, worker_pid = self.result_queues[rank].get(timeout=7200)
            self.worker_pids[rank] = worker_pid
        logger.info(f"spawned {world_size - 1} worker processes")

    def _start_nccl_process_group(self):
        rank = int(os.environ["RANK"])
        world_size = int(os.environ["WORLD_SIZE"])
        if world_size == 1:
            return

        logger.debug(f"starting NCCL process group on {rank=} with {world_size=}")
        assert not torch.distributed.is_initialized()
        # use the "env://" init method with environment variables set in start_worker_processes
        # a short 3-min timeout to quickly detect any synchronization failures
        timeout_sec = int(os.getenv("SAM3_COLLECTIVE_OP_TIMEOUT_SEC", "180"))
        timeout = datetime.timedelta(seconds=timeout_sec)
        torch.distributed.init_process_group(
            backend="nccl",
            init_method="env://",
            timeout=timeout,
            device_id=self.device,
        )
        # warm-up the NCCL process group by running a dummy all-reduce
        tensor = torch.ones(1024, 1024).cuda()
        torch.distributed.all_reduce(tensor)
        logger.debug(f"started NCCL process group on {rank=} with {world_size=}")

    def _find_free_port(self) -> int:
        """
        Find a free port (a random free port from 1024 to 65535 will be selected)
        https://stackoverflow.com/questions/1365265/on-localhost-how-do-i-pick-a-free-port-number)
        """
        with closing(socket.socket(socket.AF_INET, socket.SOCK_STREAM)) as s:
            s.bind(("", 0))
            s.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
            return s.getsockname()[1]

    @staticmethod
    def _worker_process_command_loop(
        rank,
        world_size,
        command_queue,
        result_queue,
        model_args,
        model_kwargs,
        gpus_to_use,
        parent_pid,
    ):
        """
        The command loop for each worker process. It listens to commands from the main process
        and executes them using the model.
        """
        logger.info(f"starting worker process {rank=} with {world_size=}")
        # verify that the environment variables are set correctly
        assert int(os.environ["IS_MAIN_PROCESS"]) == 0
        assert int(os.environ["RANK"]) == rank
        assert int(os.environ["WORLD_SIZE"]) == world_size
        # load the model in this worker process
        predictor = Sam3VideoPredictorMultiGPU(
            *model_args, gpus_to_use=gpus_to_use, **model_kwargs
        )
        logger.info(f"started worker {rank=} with {world_size=}")
        # return the worker process id to the main process for bookkeeping
        worker_pid = os.getpid()
        result_queue.put(("load_model", worker_pid))

        # wait for the command to start the NCCL process group
        request_type, _ = command_queue.get(timeout=7200)
        assert request_type == "start_nccl_process_group"
        predictor._start_nccl_process_group()

        # keep listening to commands from the main process
        while True:
            try:
                request, is_stream_request = command_queue.get(timeout=5.0)
                if request == "shutdown":
                    logger.info(f"worker {rank=} shutting down")
                    torch.distributed.destroy_process_group()
                    result_queue.put(("shutdown", True))  # acknowledge the shutdown
                    sys.exit(0)

                logger.debug(f"worker {rank=} received request {request['type']=}")
                if is_stream_request:
                    for _ in predictor.handle_stream_request(request):
                        pass  # handle stream requests in a generator fashion
                else:
                    predictor.handle_request(request)
            except queue.Empty:
                # Usually Python's multiprocessing module will shutdown all the daemon worker
                # processes when the main process exits gracefully. However, the user may kill
                # the main process using SIGKILL and thereby leaving no chance for the main process
                # to clean up its daemon child processes. So here we manually check whether the
                # parent process still exists (every 5 sec as in `command_queue.get` timeout).
                if not psutil.pid_exists(parent_pid):
                    logger.info(
                        f"stopping worker {rank=} as its parent process has exited"
                    )
                    sys.exit(1)
            except Exception as e:
                logger.error(f"worker {rank=} exception: {e}", exc_info=True)

    def shutdown(self):
        """Shutdown all worker processes."""
        if self.rank == 0 and self.world_size > 1:
            logger.info(f"shutting down {self.world_size - 1} worker processes")
            for rank in range(1, self.world_size):
                self.command_queues[rank].put(("shutdown", False))
            torch.distributed.destroy_process_group()
            for rank in range(1, self.world_size):
                self.result_queues[rank].get()  # wait for the worker to acknowledge
            logger.info(f"shut down {self.world_size - 1} worker processes")
        self.has_shutdown = True

        super().shutdown()



================================================
FILE: sam3/model/text_encoder_ve.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

from collections import OrderedDict
from typing import Callable, List, Optional, Tuple, Union

import torch
import torch.nn as nn
from torch.utils.checkpoint import checkpoint

from .model_misc import LayerScale


class ResidualAttentionBlock(nn.Module):
    def __init__(
        self,
        d_model: int,
        n_head: int,
        mlp_ratio: float = 4.0,
        ls_init_value: Optional[float] = None,
        act_layer: Callable[[], nn.Module] = nn.GELU,
        norm_layer: Callable[[int], nn.Module] = nn.LayerNorm,
    ):
        super().__init__()
        # Attention
        self.attn = nn.MultiheadAttention(d_model, n_head, batch_first=True)

        # LayerNorm, LayerScale
        self.ln_1 = norm_layer(d_model)
        self.ln_2 = norm_layer(d_model)

        self.ls_1 = (
            LayerScale(d_model, ls_init_value)
            if ls_init_value is not None
            else nn.Identity()
        )
        self.ls_2 = (
            LayerScale(d_model, ls_init_value)
            if ls_init_value is not None
            else nn.Identity()
        )

        # MLP
        mlp_width = int(d_model * mlp_ratio)
        self.mlp = nn.Sequential(
            OrderedDict(
                [
                    ("c_fc", nn.Linear(d_model, mlp_width)),
                    ("gelu", act_layer()),
                    ("c_proj", nn.Linear(mlp_width, d_model)),
                ]
            )
        )

    def attention(
        self,
        q_x: torch.Tensor,
        k_x: Optional[torch.Tensor] = None,
        v_x: Optional[torch.Tensor] = None,
        attn_mask: Optional[torch.Tensor] = None,
    ) -> torch.Tensor:
        k_x = k_x if k_x is not None else q_x
        v_x = v_x if v_x is not None else q_x
        if attn_mask is not None:
            # Leave boolean masks as is
            if not attn_mask.dtype == torch.bool:
                attn_mask = attn_mask.to(q_x.dtype)

        return self.attn(q_x, k_x, v_x, need_weights=False, attn_mask=attn_mask)[0]

    def forward(
        self,
        q_x: torch.Tensor,
        k_x: Optional[torch.Tensor] = None,
        v_x: Optional[torch.Tensor] = None,
        attn_mask: Optional[torch.Tensor] = None,
    ) -> torch.Tensor:
        k_x = (
            self.ln_1_kv(k_x) if hasattr(self, "ln_1_kv") and k_x is not None else None
        )
        v_x = (
            self.ln_1_kv(v_x) if hasattr(self, "ln_1_kv") and v_x is not None else None
        )
        x = q_x + self.ls_1(
            self.attention(q_x=self.ln_1(q_x), k_x=k_x, v_x=v_x, attn_mask=attn_mask)
        )
        x = x + self.ls_2(self.mlp(self.ln_2(x)))
        return x


class Transformer(nn.Module):
    def __init__(
        self,
        width: int,
        layers: int,
        heads: int,
        mlp_ratio: float = 4.0,
        ls_init_value: Optional[float] = None,
        act_layer: Callable[[], nn.Module] = nn.GELU,
        norm_layer: Callable[[int], nn.Module] = nn.LayerNorm,
        compile_mode: Optional[str] = None,
        use_act_checkpoint: bool = False,
    ):
        super().__init__()
        self.width = width
        self.layers = layers
        self.grad_checkpointing = use_act_checkpoint
        self.resblocks = nn.ModuleList(
            [
                ResidualAttentionBlock(
                    width,
                    heads,
                    mlp_ratio,
                    ls_init_value=ls_init_value,
                    act_layer=act_layer,
                    norm_layer=norm_layer,
                )
                for _ in range(layers)
            ]
        )

        if compile_mode is not None:
            self.forward = torch.compile(
                self.forward, mode=compile_mode, fullgraph=True
            )
            if self.grad_checkpointing:
                torch._dynamo.config.optimize_ddp = False

    def forward(
        self,
        x: torch.Tensor,
        attn_mask: Optional[torch.Tensor] = None,
    ) -> torch.Tensor:
        for _, r in enumerate(self.resblocks):
            if (
                self.grad_checkpointing
                and not torch.jit.is_scripting()
                and self.training
            ):
                x = checkpoint(r, x, None, None, attn_mask, use_reentrant=False)
            else:
                x = r(
                    x,
                    attn_mask=attn_mask,
                )
        return x


def text_global_pool(
    x: torch.Tensor, text: Optional[torch.Tensor] = None, pool_type: str = "argmax"
) -> Tuple[torch.Tensor, torch.Tensor]:
    if pool_type == "first":
        pooled, tokens = x[:, 0], x[:, 1:]
    elif pool_type == "last":
        pooled, tokens = x[:, -1], x[:, :-1]
    elif pool_type == "argmax":
        # take features from the eot embedding (eot_token is the highest number in each sequence)
        assert text is not None
        pooled, tokens = x[torch.arange(x.shape[0]), text.argmax(dim=-1)], x
    else:
        pooled = tokens = x
    return pooled, tokens


class TextTransformer(nn.Module):
    def __init__(
        self,
        context_length: int = 77,
        vocab_size: int = 49408,
        width: int = 512,
        heads: int = 8,
        layers: int = 12,
        mlp_ratio: float = 4.0,
        ls_init_value: Optional[float] = None,
        output_dim: int = 512,
        no_causal_mask: bool = False,
        pool_type: str = "none",  # no pooling
        proj_bias: bool = False,
        act_layer: Callable = nn.GELU,
        norm_layer: Callable = nn.LayerNorm,
        output_tokens: bool = False,
        use_ln_post: bool = True,
        compile_mode: Optional[str] = None,
        use_act_checkpoint: bool = False,
    ):
        super().__init__()
        assert pool_type in ("first", "last", "argmax", "none")
        self.output_tokens = output_tokens
        self.num_pos = self.context_length = context_length
        self.vocab_size = vocab_size
        self.width = width
        self.output_dim = output_dim
        self.heads = heads
        self.pool_type = pool_type

        self.token_embedding = nn.Embedding(self.vocab_size, width)
        self.positional_embedding = nn.Parameter(torch.empty(self.num_pos, width))
        self.transformer = Transformer(
            width=width,
            layers=layers,
            heads=heads,
            mlp_ratio=mlp_ratio,
            ls_init_value=ls_init_value,
            act_layer=act_layer,
            norm_layer=norm_layer,
            compile_mode=compile_mode,
            use_act_checkpoint=use_act_checkpoint,
        )
        self.ln_final = norm_layer(width) if use_ln_post else nn.Identity()
        if no_causal_mask:
            self.attn_mask = None
        else:
            self.register_buffer(
                "attn_mask", self.build_causal_mask(), persistent=False
            )
        if proj_bias:
            self.text_projection = nn.Linear(width, output_dim)
        else:
            self.text_projection = nn.Parameter(torch.empty(width, output_dim))

    def build_causal_mask(self) -> torch.Tensor:
        # lazily create causal attention mask, with full attention between the tokens
        # pytorch uses additive attention mask; fill with -inf
        mask = torch.empty(self.num_pos, self.num_pos)
        mask.fill_(float("-inf"))
        mask.triu_(1)  # zero out the lower diagonal
        return mask

    def forward(
        self, text: torch.Tensor
    ) -> Union[torch.Tensor, Tuple[torch.Tensor, torch.Tensor]]:
        seq_len = text.shape[1]
        x = self.token_embedding(text)  # [batch_size, n_ctx, d_model]

        attn_mask = self.attn_mask
        if attn_mask is not None:
            attn_mask = attn_mask[:seq_len, :seq_len]

        x = x + self.positional_embedding[:seq_len]
        x = self.transformer(x, attn_mask=attn_mask)

        x = self.ln_final(x)
        pooled, tokens = text_global_pool(x, text, pool_type=self.pool_type)
        if self.text_projection is not None:
            if isinstance(self.text_projection, nn.Linear):
                pooled = self.text_projection(pooled)
            else:
                pooled = pooled @ self.text_projection
        if self.output_tokens:
            return pooled, tokens
        return pooled


class VETextEncoder(nn.Module):
    def __init__(
        self,
        d_model: int,
        tokenizer: Callable,
        width: int = 1024,
        heads: int = 16,
        layers: int = 24,
        context_length: int = 32,
        vocab_size: int = 49408,
        use_ln_post: bool = True,
        compile_mode: Optional[str] = None,
        use_act_checkpoint: bool = True,
    ):
        super().__init__()
        self.context_length = context_length
        self.use_ln_post = use_ln_post
        self.tokenizer = tokenizer

        self.encoder = TextTransformer(
            context_length=self.context_length,
            vocab_size=vocab_size,
            width=width,
            heads=heads,
            layers=layers,
            # we want the tokens, not just the pooled output
            output_tokens=True,
            use_ln_post=use_ln_post,
            compile_mode=compile_mode,
            use_act_checkpoint=use_act_checkpoint,
        )
        self.resizer = nn.Linear(self.encoder.width, d_model)

    def forward(
        self,
        text: Union[List[str], Tuple[torch.Tensor, torch.Tensor, dict]],
        input_boxes: Optional[List] = None,
        device: torch.device = None,
    ) -> Tuple[torch.Tensor, torch.Tensor, torch.Tensor]:
        if isinstance(text[0], str):
            # no use case for this
            assert input_boxes is None or len(input_boxes) == 0, "not supported"

            # Encode the text
            tokenized = self.tokenizer(text, context_length=self.context_length).to(
                device
            )  # [b, seq_len]
            text_attention_mask = (tokenized != 0).bool()

            # manually embed the tokens
            inputs_embeds = self.encoder.token_embedding(
                tokenized
            )  # [b, seq_len, d=1024]
            _, text_memory = self.encoder(tokenized)  # [b, seq_len, d=1024]

            assert text_memory.shape[1] == inputs_embeds.shape[1]
            # Invert attention mask because its the opposite in pytorch transformer
            text_attention_mask = text_attention_mask.ne(1)
            # Transpose memory because pytorch's attention expects sequence first
            text_memory = text_memory.transpose(0, 1)
            # Resize the encoder hidden states to be of the same d_model as the decoder
            text_memory_resized = self.resizer(text_memory)
        else:
            # The text is already encoded, use as is.
            text_attention_mask, text_memory_resized, tokenized = text
            inputs_embeds = tokenized["inputs_embeds"]
            assert input_boxes is None or len(input_boxes) == 0, (
                "Can't replace boxes in text if it's already encoded"
            )

        # Note that the input_embeds are returned in pytorch's convention (sequence first)
        return (
            text_attention_mask,
            text_memory_resized,
            inputs_embeds.transpose(0, 1),
        )



================================================
FILE: sam3/model/tokenizer_ve.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

"""
Text Tokenizer.

Copied and lightly adapted from VE repo, which in turn copied
from open_clip and openAI CLIP.
"""

import gzip
import html
import io
import os
import string
from functools import lru_cache
from typing import List, Optional, Union

import ftfy
import regex as re
import torch
from iopath.common.file_io import g_pathmgr


# https://stackoverflow.com/q/62691279
os.environ["TOKENIZERS_PARALLELISM"] = "false"
DEFAULT_CONTEXT_LENGTH = 77


@lru_cache()
def bytes_to_unicode():
    """
    Returns list of utf-8 byte and a corresponding list of unicode strings.
    The reversible bpe codes work on unicode strings.
    This means you need a large # of unicode characters in your vocab if you want to avoid UNKs.
    When you're at something like a 10B token dataset you end up needing around 5K for decent coverage.
    This is a significant percentage of your normal, say, 32K bpe vocab.
    To avoid that, we want lookup tables between utf-8 bytes and unicode strings.
    And avoids mapping to whitespace/control characters the bpe code barfs on.
    """
    bs = (
        list(range(ord("!"), ord("~") + 1))
        + list(range(ord("¡"), ord("¬") + 1))
        + list(range(ord("®"), ord("ÿ") + 1))
    )
    cs = bs[:]
    n = 0
    for b in range(2**8):
        if b not in bs:
            bs.append(b)
            cs.append(2**8 + n)
            n += 1
    cs = [chr(n) for n in cs]
    return dict(zip(bs, cs))


def get_pairs(word):
    """Return set of symbol pairs in a word.
    Word is represented as tuple of symbols (symbols being variable-length strings).
    """
    pairs = set()
    prev_char = word[0]
    for char in word[1:]:
        pairs.add((prev_char, char))
        prev_char = char
    return pairs


def basic_clean(text):
    text = ftfy.fix_text(text)
    text = html.unescape(html.unescape(text))
    return text.strip()


def whitespace_clean(text):
    text = re.sub(r"\s+", " ", text)
    text = text.strip()
    return text


def _clean_canonicalize(x):
    # basic, remove whitespace, remove punctuation, lower case
    return canonicalize_text(basic_clean(x))


def _clean_lower(x):
    # basic, remove whitespace, lower case
    return whitespace_clean(basic_clean(x)).lower()


def _clean_whitespace(x):
    # basic, remove whitespace
    return whitespace_clean(basic_clean(x))


def get_clean_fn(type: str):
    if type == "canonicalize":
        return _clean_canonicalize
    elif type == "lower":
        return _clean_lower
    elif type == "whitespace":
        return _clean_whitespace
    else:
        assert False, f"Invalid clean function ({type})."


def canonicalize_text(text, *, keep_punctuation_exact_string=None):
    """Returns canonicalized `text` (lowercase and punctuation removed).
    From: https://github.com/google-research/big_vision/blob/53f18caf27a9419231bbf08d3388b07671616d3d/big_vision/evaluators/proj/image_text/prompt_engineering.py#L94
    Args:
      text: string to be canonicalized.
      keep_punctuation_exact_string: If provided, then this exact string kept.
        For example providing '{}' will keep any occurrences of '{}' (but will
        still remove '{' and '}' that appear separately).
    """
    text = text.replace("_", " ")
    if keep_punctuation_exact_string:
        text = keep_punctuation_exact_string.join(
            part.translate(str.maketrans("", "", string.punctuation))
            for part in text.split(keep_punctuation_exact_string)
        )
    else:
        text = text.translate(str.maketrans("", "", string.punctuation))
    text = text.lower()
    text = re.sub(r"\s+", " ", text)
    return text.strip()


class SimpleTokenizer(object):
    def __init__(
        self,
        bpe_path: Union[str, os.PathLike],
        additional_special_tokens: Optional[List[str]] = None,
        context_length: Optional[int] = DEFAULT_CONTEXT_LENGTH,
        clean: str = "lower",
    ):
        self.byte_encoder = bytes_to_unicode()
        self.byte_decoder = {v: k for k, v in self.byte_encoder.items()}
        with g_pathmgr.open(bpe_path, "rb") as fh:
            bpe_bytes = io.BytesIO(fh.read())
            merges = gzip.open(bpe_bytes).read().decode("utf-8").split("\n")
        # merges = gzip.open(bpe_path).read().decode("utf-8").split("\n")
        merges = merges[1 : 49152 - 256 - 2 + 1]
        merges = [tuple(merge.split()) for merge in merges]
        vocab = list(bytes_to_unicode().values())
        vocab = vocab + [v + "</w>" for v in vocab]
        for merge in merges:
            vocab.append("".join(merge))
        special_tokens = ["<start_of_text>", "<end_of_text>"]
        if additional_special_tokens:
            special_tokens += additional_special_tokens
        vocab.extend(special_tokens)
        self.encoder = dict(zip(vocab, range(len(vocab))))
        self.decoder = {v: k for k, v in self.encoder.items()}
        self.bpe_ranks = dict(zip(merges, range(len(merges))))
        self.cache = {t: t for t in special_tokens}
        special = "|".join(special_tokens)
        self.pat = re.compile(
            special + r"""|'s|'t|'re|'ve|'m|'ll|'d|[\p{L}]+|[\p{N}]|[^\s\p{L}\p{N}]+""",
            re.IGNORECASE,
        )
        self.vocab_size = len(self.encoder)
        self.all_special_ids = [self.encoder[t] for t in special_tokens]
        self.sot_token_id = self.all_special_ids[0]
        self.eot_token_id = self.all_special_ids[1]
        self.context_length = context_length
        self.clean_fn = get_clean_fn(clean)

    def bpe(self, token):
        if token in self.cache:
            return self.cache[token]
        word = tuple(token[:-1]) + (token[-1] + "</w>",)
        pairs = get_pairs(word)
        if not pairs:
            return token + "</w>"
        while True:
            bigram = min(pairs, key=lambda pair: self.bpe_ranks.get(pair, float("inf")))
            if bigram not in self.bpe_ranks:
                break
            first, second = bigram
            new_word = []
            i = 0
            while i < len(word):
                try:
                    j = word.index(first, i)
                    new_word.extend(word[i:j])
                    i = j
                except:
                    new_word.extend(word[i:])
                    break
                if word[i] == first and i < len(word) - 1 and word[i + 1] == second:
                    new_word.append(first + second)
                    i += 2
                else:
                    new_word.append(word[i])
                    i += 1
            new_word = tuple(new_word)
            word = new_word
            if len(word) == 1:
                break
            else:
                pairs = get_pairs(word)
        word = " ".join(word)
        self.cache[token] = word
        return word

    def encode(self, text):
        bpe_tokens = []
        text = self.clean_fn(text)
        for token in re.findall(self.pat, text):
            token = "".join(self.byte_encoder[b] for b in token.encode("utf-8"))
            bpe_tokens.extend(
                self.encoder[bpe_token] for bpe_token in self.bpe(token).split(" ")
            )
        return bpe_tokens

    def decode(self, tokens):
        text = "".join([self.decoder[token] for token in tokens])
        text = (
            bytearray([self.byte_decoder[c] for c in text])
            .decode("utf-8", errors="replace")
            .replace("</w>", " ")
        )
        return text

    def __call__(
        self, texts: Union[str, List[str]], context_length: Optional[int] = None
    ) -> torch.LongTensor:
        """Returns the tokenized representation of given input string(s)
        Parameters
        ----------
        texts : Union[str, List[str]]
            An input string or a list of input strings to tokenize
        context_length : int
            The context length to use; all CLIP models use 77 as the context length
        Returns
        -------
        A two-dimensional tensor containing the resulting tokens, shape = [number of input strings, context_length]
        """
        if isinstance(texts, str):
            texts = [texts]
        context_length = context_length or self.context_length
        assert context_length, "Please set a valid context length"
        all_tokens = [
            [self.sot_token_id] + self.encode(text) + [self.eot_token_id]
            for text in texts
        ]
        result = torch.zeros(len(all_tokens), context_length, dtype=torch.long)
        for i, tokens in enumerate(all_tokens):
            if len(tokens) > context_length:
                tokens = tokens[:context_length]  # Truncate
                tokens[-1] = self.eot_token_id
            result[i, : len(tokens)] = torch.tensor(tokens)
        return result



================================================
FILE: sam3/model/vitdet.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

"""
ViTDet backbone adapted from Detectron2.
This module implements Vision Transformer (ViT) backbone for object detection.

Rope embedding code adopted from:
1. https://github.com/meta-llama/codellama/blob/main/llama/model.py
2. https://github.com/naver-ai/rope-vit
3. https://github.com/lucidrains/rotary-embedding-torch
"""

import math
from functools import partial
from typing import Callable, List, Optional, Tuple, Union

import torch
import torch.nn as nn
import torch.nn.functional as F
import torch.utils.checkpoint as checkpoint

try:
    from timm.layers import DropPath, trunc_normal_
except ModuleNotFoundError:
    # compatibility for older timm versions
    from timm.models.layers import DropPath, trunc_normal_
from sam3.model.data_misc import NestedTensor
from sam3.model.model_misc import AttentionType, LayerScale
from sam3.perflib.fused import addmm_act
from sam3.sam.rope import apply_rotary_enc_real, VisionRotaryEmbeddingVE
from torch import Tensor


class Mlp(nn.Module):
    """MLP as used in Vision Transformer, MLP-Mixer and related networks"""

    def __init__(
        self,
        in_features,
        hidden_features=None,
        out_features=None,
        act_layer=nn.GELU,
        norm_layer=None,
        bias=True,
        drop=0.0,
        use_conv=False,
    ):
        super().__init__()
        out_features = out_features or in_features
        hidden_features = hidden_features or in_features
        if isinstance(bias, bool):
            bias = (bias, bias)
        if isinstance(drop, (int, float)):
            drop_probs = (drop, drop)
        else:
            drop_probs = drop
        linear_layer = partial(nn.Conv2d, kernel_size=1) if use_conv else nn.Linear

        self.fc1 = linear_layer(in_features, hidden_features, bias=bias[0])
        self.act = act_layer()
        self.drop1 = nn.Dropout(drop_probs[0])
        self.norm = (
            norm_layer(hidden_features) if norm_layer is not None else nn.Identity()
        )
        self.fc2 = linear_layer(hidden_features, out_features, bias=bias[1])
        self.drop2 = nn.Dropout(drop_probs[1])

    def forward(self, x):
        x = addmm_act(type(self.act), self.fc1, x)
        x = self.drop1(x)
        x = self.norm(x)
        x = self.fc2(x)
        x = self.drop2(x)
        return x


def init_t_xy(
    end_x: int, end_y: int, scale: float = 1.0, offset: int = 0
) -> Tuple[torch.Tensor, torch.Tensor]:
    t = torch.arange(end_x * end_y, dtype=torch.float32)
    t_x = (t % end_x).float()
    t_y = torch.div(t, end_x, rounding_mode="floor").float()
    return t_x * scale + offset, t_y * scale + offset


def compute_axial_cis(
    dim: int,
    end_x: int,
    end_y: int,
    theta: float = 10000.0,
    scale_pos: float = 1.0,
    offset: int = 0,
) -> torch.Tensor:
    freqs_x = 1.0 / (theta ** (torch.arange(0, dim, 4)[: (dim // 4)].float() / dim))
    freqs_y = 1.0 / (theta ** (torch.arange(0, dim, 4)[: (dim // 4)].float() / dim))

    t_x, t_y = init_t_xy(end_x, end_y, scale_pos, offset)
    freqs_x = torch.outer(t_x, freqs_x)
    freqs_y = torch.outer(t_y, freqs_y)
    freqs_cis_x = torch.polar(torch.ones_like(freqs_x), freqs_x)
    freqs_cis_y = torch.polar(torch.ones_like(freqs_y), freqs_y)
    return torch.cat([freqs_cis_x, freqs_cis_y], dim=-1)


def reshape_for_broadcast(freqs_cis: torch.Tensor, x: torch.Tensor) -> torch.Tensor:
    ndim = x.ndim
    assert 0 <= 1 < ndim
    assert freqs_cis.shape == (x.shape[-2], x.shape[-1])
    shape = [d if i >= ndim - 2 else 1 for i, d in enumerate(x.shape)]
    return freqs_cis.view(*shape)


def apply_rotary_enc(
    xq: torch.Tensor,
    xk: torch.Tensor,
    freqs_cis: torch.Tensor,
    repeat_freqs_k: bool = False,
) -> Tuple[torch.Tensor, torch.Tensor]:
    xq_ = torch.view_as_complex(xq.float().reshape(*xq.shape[:-1], -1, 2))
    xk_ = (
        torch.view_as_complex(xk.float().reshape(*xk.shape[:-1], -1, 2))
        if xk.shape[-2] != 0
        else None
    )
    freqs_cis = reshape_for_broadcast(freqs_cis, xq_)
    xq_out = torch.view_as_real(xq_ * freqs_cis).flatten(3)
    if xk_ is None:
        # no keys to rotate, due to dropout
        return xq_out.type_as(xq).to(xq.device), xk
    # repeat freqs along seq_len dim to match k seq_len
    if repeat_freqs_k:
        r = xk_.shape[-2] // xq_.shape[-2]
        freqs_cis = freqs_cis.repeat(*([1] * (freqs_cis.ndim - 2)), r, 1)
    xk_out = torch.view_as_real(xk_ * freqs_cis).flatten(3)
    return xq_out.type_as(xq).to(xq.device), xk_out.type_as(xk).to(xk.device)


def window_partition(x: Tensor, window_size: int) -> Tuple[Tensor, Tuple[int, int]]:
    """
    Partition into non-overlapping windows with padding if needed.
    Args:
        x (tensor): input tokens with [B, H, W, C].
        window_size (int): window size.
    Returns:
        windows: windows after partition with [B * num_windows, window_size, window_size, C].
        (Hp, Wp): padded height and width before partition
    """
    B, H, W, C = x.shape

    pad_h = (window_size - H % window_size) % window_size
    pad_w = (window_size - W % window_size) % window_size
    if pad_h > 0 or pad_w > 0:
        x = F.pad(x, (0, 0, 0, pad_w, 0, pad_h))
    Hp, Wp = H + pad_h, W + pad_w

    x = x.view(B, Hp // window_size, window_size, Wp // window_size, window_size, C)
    windows = x.permute(0, 1, 3, 2, 4, 5).reshape(-1, window_size, window_size, C)
    return windows, (Hp, Wp)


def window_unpartition(
    windows: Tensor, window_size: int, pad_hw: Tuple[int, int], hw: Tuple[int, int]
) -> Tensor:
    """
    Window unpartition into original sequences and removing padding.
    Args:
        x (tensor): input tokens with [B * num_windows, window_size, window_size, C].
        window_size (int): window size.
        pad_hw (Tuple): padded height and width (Hp, Wp).
        hw (Tuple): original height and width (H, W) before padding.
    Returns:
        x: unpartitioned sequences with [B, H, W, C].
    """
    Hp, Wp = pad_hw
    H, W = hw
    B = windows.shape[0] // (Hp * Wp // window_size // window_size)
    x = windows.reshape(
        B, Hp // window_size, Wp // window_size, window_size, window_size, -1
    )
    x = x.permute(0, 1, 3, 2, 4, 5).reshape(B, Hp, Wp, -1)

    if Hp > H or Wp > W:
        x = x[:, :H, :W, :]
    return x


def get_rel_pos(q_size: int, k_size: int, rel_pos: Tensor) -> Tensor:
    """
    Get relative positional embeddings according to the relative positions of
        query and key sizes.
    Args:
        q_size (int): size of query q.
        k_size (int): size of key k.
        rel_pos (Tensor): relative position embeddings (L, C).
    Returns:
        Extracted positional embeddings according to relative positions.
    """
    max_rel_dist = int(2 * max(q_size, k_size) - 1)
    # Interpolate rel pos if needed.
    if rel_pos.shape[0] != max_rel_dist:
        # Interpolate rel pos.
        rel_pos_resized = F.interpolate(
            rel_pos.reshape(1, rel_pos.shape[0], -1).permute(0, 2, 1),
            size=max_rel_dist,
            mode="linear",
            align_corners=False,
        )
        rel_pos_resized = rel_pos_resized.reshape(-1, max_rel_dist).permute(1, 0)
    else:
        rel_pos_resized = rel_pos

    # Scale the coords with short length if shapes for q and k are different.
    q_coords = torch.arange(q_size)[:, None] * max(k_size / q_size, 1.0)
    k_coords = torch.arange(k_size)[None, :] * max(q_size / k_size, 1.0)
    relative_coords = (q_coords - k_coords) + (k_size - 1) * max(q_size / k_size, 1.0)

    return rel_pos_resized[relative_coords.long()]


def get_abs_pos(
    abs_pos: Tensor,
    has_cls_token: bool,
    hw: Tuple[int, int],
    retain_cls_token: bool = False,
    tiling: bool = False,
) -> Tensor:
    """
    Calculate absolute positional embeddings. If needed, resize embeddings and remove cls_token
        dimension for the original embeddings.
    Args:
        abs_pos (Tensor): absolute positional embeddings with (1, num_position, C).
        has_cls_token (bool): If true, has 1 embedding in abs_pos for cls token.
        hw (Tuple): size of input image tokens.
        retain_cls_token: whether to retain the cls_token
        tiling: whether to tile the embeddings, *instead* of interpolation (a la abs_win)
    Returns:
        Absolute positional embeddings after processing with shape (1, H, W, C),
        if retain_cls_token is False, otherwise (1, 1+H*W, C)
    """
    if retain_cls_token:
        assert has_cls_token

    h, w = hw
    if has_cls_token:
        cls_pos = abs_pos[:, :1]
        abs_pos = abs_pos[:, 1:]

    xy_num = abs_pos.shape[1]
    size = int(math.sqrt(xy_num))
    assert size * size == xy_num

    if size != h or size != w:
        new_abs_pos = abs_pos.reshape(1, size, size, -1).permute(0, 3, 1, 2)
        if tiling:
            new_abs_pos = new_abs_pos.tile(
                [1, 1] + [x // y + 1 for x, y in zip((h, w), new_abs_pos.shape[2:])]
            )[:, :, :h, :w]
        else:
            new_abs_pos = F.interpolate(
                new_abs_pos,
                size=(h, w),
                mode="bicubic",
                align_corners=False,
            )

        if not retain_cls_token:
            return new_abs_pos.permute(0, 2, 3, 1)
        else:
            # add cls_token back, flatten spatial dims
            assert has_cls_token
            return torch.cat(
                [cls_pos, new_abs_pos.permute(0, 2, 3, 1).reshape(1, h * w, -1)],
                dim=1,
            )

    else:
        if not retain_cls_token:
            return abs_pos.reshape(1, h, w, -1)
        else:
            assert has_cls_token
            return torch.cat([cls_pos, abs_pos], dim=1)


def concat_rel_pos(
    q: Tensor,
    k: Tensor,
    q_hw: Tuple[int, int],
    k_hw: Tuple[int, int],
    rel_pos_h: Tensor,
    rel_pos_w: Tensor,
    rescale: bool = False,
    relative_coords: Optional[Tensor] = None,
) -> Tuple[Tensor, Tensor]:
    """
    Concatenate rel pos coeffs to the q & k tensors, so that qk^T is now
    effectively including rel pos biases.
    Args:
        q (Tensor): q tensor with shape (B, L_q, C).
        k (Tensor): k tensor with shape (B, L_k, C).
        q_hw, k_hw: These are spatial size of q & k tensors.
        rel_pos_h, rel_pos_w: These are relative pos embeddings/params of height, width.
        rescale (bool): whether to rescale. e.g. for use when using sdpa, pytorch will
            scale by the wrong factor due to the concat.
    Returns:
        q, k: But, padded so that qk^T accounts for rel pos biases
    """
    q_h, q_w = q_hw
    k_h, k_w = k_hw

    assert (q_h == q_w) and (k_h == k_w), "only square inputs supported"

    if relative_coords is not None:
        Rh = rel_pos_h[relative_coords]
        Rw = rel_pos_w[relative_coords]
    else:
        Rh = get_rel_pos(q_h, k_h, rel_pos_h)
        Rw = get_rel_pos(q_w, k_w, rel_pos_w)

    B, _, dim = q.shape
    r_q = q.reshape(B, q_h, q_w, dim)

    old_scale = dim**0.5
    new_scale = (dim + k_h + k_w) ** 0.5 if rescale else old_scale  # for sdpa
    # attn will be divided by new_scale, but we want to divide q by old_scale
    scale_ratio = new_scale / old_scale

    rel_h = torch.einsum("bhwc,hkc->bhwk", r_q, Rh) * new_scale  # (B, q_h, q_w, k_h)
    rel_w = torch.einsum("bhwc,wkc->bhwk", r_q, Rw) * new_scale  # (B, q_h, q_w, k_w)

    eye_h = torch.eye(k_h, dtype=q.dtype, device=q.device)
    eye_w = torch.eye(k_w, dtype=q.dtype, device=q.device)

    eye_h = eye_h.view(1, k_h, 1, k_h).expand([B, k_h, k_w, k_h])
    eye_w = eye_w.view(1, 1, k_w, k_w).expand([B, k_h, k_w, k_w])

    q = torch.cat([r_q * scale_ratio, rel_h, rel_w], dim=-1).view(B, q_h * q_w, -1)
    k = torch.cat([k.view(B, k_h, k_w, -1), eye_h, eye_w], dim=-1).view(
        B, k_h * k_w, -1
    )

    return q, k


class PatchEmbed(nn.Module):
    """
    Image to Patch Embedding.
    """

    def __init__(
        self,
        kernel_size: Tuple[int, int] = (16, 16),
        stride: Tuple[int, int] = (16, 16),
        padding: Tuple[int, int] = (0, 0),
        in_chans: int = 3,
        embed_dim: int = 768,
        bias: bool = True,
    ):
        """
        Args:
            kernel_size (Tuple): kernel size of the projection layer.
            stride (Tuple): stride of the projection layer.
            padding (Tuple): padding size of the projection layer.
            in_chans (int): Number of input image channels.
            embed_dim (int):  embed_dim (int): Patch embedding dimension.
        """
        super().__init__()

        self.proj = nn.Conv2d(
            in_chans,
            embed_dim,
            kernel_size=kernel_size,
            stride=stride,
            padding=padding,
            bias=bias,
        )

    def forward(self, x: Tensor) -> Tensor:
        x = self.proj(x)
        # B C H W -> B H W C
        x = x.permute(0, 2, 3, 1)
        return x


class Attention(nn.Module):
    """Multi-head Attention block with relative position embeddings and 2d-rope."""

    def __init__(
        self,
        dim: int,
        num_heads: int = 8,
        qkv_bias: bool = True,
        use_rel_pos: bool = False,
        rel_pos_zero_init: bool = True,
        input_size: Optional[Tuple[int, int]] = None,
        attn_type: AttentionType = AttentionType.Vanilla,
        cls_token: bool = False,
        use_rope: bool = False,
        rope_theta: float = 10000.0,
        rope_pt_size: Optional[Tuple[int, int]] = None,
        rope_interp: bool = False,
        rope_tiled: bool = False,
        use_ve_rope: bool = False,
        use_fa3: bool = False,
        use_rope_real: bool = False,
    ):
        """
        Args:
            dim (int): Number of input channels.
            num_heads (int): Number of attention heads.
            qkv_bias (bool:  If True, add a learnable bias to query, key, value.
            rel_pos (bool): If True, add relative positional embeddings to the attention map.
            rel_pos_zero_init (bool): If True, zero initialize relative positional parameters.
            input_size (int or None): Input resolution for calculating the relative positional
                parameter size or rope size.
            attn_type: Type of attention operation, e.g. "vanilla", "vanilla-xformer".
            cls_token: whether a cls_token is present.
            use_rope: whether to use rope 2d (indep of use_rel_pos, as it can be used together)
            rope_theta: control frequencies of rope
            rope_pt_size: size of rope in previous stage of training, needed for interpolation or tiling
            rope_tiled: whether to tile rope or not; tile expected to be of size rope_pt_size x rope_pt_size
            rope_interp: whether to interpolate (or extrapolate) rope to match input size
            use_ve_rope: use ve orig rope implementation, if small numerical differences are important (normally not)
        """
        super().__init__()
        self.num_heads = num_heads
        self.head_dim = dim // num_heads
        self.scale = self.head_dim**-0.5
        self.cls_token = cls_token

        self.attn_type = attn_type
        self.qkv = nn.Linear(dim, dim * 3, bias=qkv_bias)
        self.proj = nn.Linear(dim, dim)

        # rel_pos embeddings and rope
        self.use_rel_pos = use_rel_pos
        self.input_size = input_size

        self.use_rope = use_rope
        self.rope_theta = rope_theta
        self.rope_pt_size = rope_pt_size
        self.rope_interp = rope_interp
        self.rope_tiled = rope_tiled
        self.use_ve_rope = use_ve_rope
        self.use_fa3 = use_fa3
        self.use_rope_real = use_rope_real

        # init rel_pos embeddings and rope
        self._setup_rel_pos(rel_pos_zero_init)
        self._setup_rope_freqs()

    def _setup_rel_pos(self, rel_pos_zero_init: bool = True) -> None:
        if not self.use_rel_pos:
            self.rel_pos_h = None
            self.rel_pos_w = None
            return

        assert self.input_size is not None
        assert self.cls_token is False, "not supported"
        # initialize relative positional embeddings
        self.rel_pos_h = nn.Parameter(
            torch.zeros(2 * self.input_size[0] - 1, self.head_dim)
        )
        self.rel_pos_w = nn.Parameter(
            torch.zeros(2 * self.input_size[1] - 1, self.head_dim)
        )

        if not rel_pos_zero_init:
            trunc_normal_(self.rel_pos_h, std=0.02)
            trunc_normal_(self.rel_pos_w, std=0.02)

        # Precompute the relative coords
        H, W = self.input_size
        q_coords = torch.arange(H)[:, None]
        k_coords = torch.arange(W)[None, :]
        relative_coords = (q_coords - k_coords) + (H - 1)
        self.register_buffer("relative_coords", relative_coords.long())

    def _setup_rope_freqs(self) -> None:
        if not self.use_rope:
            self.freqs_cis = None
            return

        assert self.input_size is not None
        # determine rope input size
        if self.rope_pt_size is None:
            self.rope_pt_size = self.input_size

        if self.use_ve_rope:
            assert not self.rope_tiled, "not supported"
            self.rope = VisionRotaryEmbeddingVE(
                dim=self.head_dim // 2,
                seq_len=self.input_size[0],
                pt_seq_len=self.rope_pt_size[0],
            )
            return

        # initialize 2d rope freqs
        self.compute_cis = partial(
            compute_axial_cis,
            dim=self.head_dim,
            theta=self.rope_theta,
        )

        if self.rope_pt_size != self.input_size and self.rope_tiled:
            assert not self.rope_interp
            # window/tiled rope
            freqs_cis = self.compute_cis(
                end_x=self.rope_pt_size[0], end_y=self.rope_pt_size[1]
            )
            # check dims are tileable
            rh, rw = (
                self.input_size[0] // self.rope_pt_size[0],
                self.input_size[1] // self.rope_pt_size[1],
            )
            assert rh >= 1, rw >= 1
            assert (
                self.input_size[0] % self.rope_pt_size[0] == 0
                and self.input_size[1] % self.rope_pt_size[1] == 0
            )

            # restore spatial shape, tile and then flatten spatial dims
            freqs_cis = (
                freqs_cis.reshape(self.rope_pt_size[0], self.rope_pt_size[1], -1)
                .tile(rh, rw, 1)
                .reshape(-1, freqs_cis.shape[-1])
            )
        else:
            # interpolate rope
            scale_pos = 1.0
            if self.rope_interp:
                scale_pos = self.rope_pt_size[0] / self.input_size[0]
            # get scaled freqs_cis
            freqs_cis = self.compute_cis(
                end_x=self.input_size[0],
                end_y=self.input_size[1],
                scale_pos=scale_pos,
            )
        if self.cls_token:
            t = torch.zeros(
                self.head_dim // 2,
                dtype=torch.float32,
                device=freqs_cis.device,
            )
            cls_freqs_cis = torch.polar(torch.ones_like(t), t)[None, :]
            freqs_cis = torch.cat([cls_freqs_cis, freqs_cis], dim=0)

        self.register_buffer("freqs_cis", freqs_cis)
        if self.use_rope_real:
            self.register_buffer("freqs_cis_real", freqs_cis.real)
            self.register_buffer("freqs_cis_imag", freqs_cis.imag)

    def _apply_rope(self, q, k) -> Tuple[Tensor, Tensor]:
        if not self.use_rope:
            return q, k

        if self.use_ve_rope:
            dtype = q.dtype
            return self.rope(q).to(dtype), self.rope(k).to(dtype)

        assert self.freqs_cis is not None

        if self.use_rope_real:
            return apply_rotary_enc_real(
                q,
                k,
                freqs_cis_imag=self.freqs_cis_imag,
                freqs_cis_real=self.freqs_cis_real,
            )
        return apply_rotary_enc(q, k, freqs_cis=self.freqs_cis)

    def forward(self, x: Tensor) -> Tensor:
        s = 1 if self.cls_token else 0  # used to exclude cls_token
        if x.ndim == 4:
            B, H, W, _ = x.shape
            assert s == 0  # no cls_token
            L = H * W
            ndim = 4
        else:
            assert x.ndim == 3
            B, L, _ = x.shape
            ndim = 3
            H = W = math.sqrt(L - s)

        # qkv with shape (3, B, nHead, L, C)
        qkv = self.qkv(x).reshape(B, L, 3, self.num_heads, -1)
        # q, k, v with shape (B, nHead, L, C)
        q, k, v = qkv.permute(2, 0, 3, 1, 4).unbind(0)

        # handle rope and rel pos embeddings
        q, k = self._apply_rope(q, k)
        if self.use_rel_pos:
            q, k = concat_rel_pos(
                q.flatten(0, 1),
                k.flatten(0, 1),
                (H, W),
                x.shape[1:3],
                self.rel_pos_h,
                self.rel_pos_w,
                rescale=True,
                relative_coords=self.relative_coords,
            )

            # sdpa expects [B, nheads, H*W, C] so we transpose back
            q = q.reshape(B, self.num_heads, H * W, -1)
            k = k.reshape(B, self.num_heads, H * W, -1)

        if self.attn_type == AttentionType.Vanilla:
            if self.use_fa3:
                from sam3.perflib.fa3 import flash_attn_func

                x = flash_attn_func(
                    q.transpose(1, 2), k.transpose(1, 2), v.transpose(1, 2)
                ).transpose(1, 2)
            else:
                x = F.scaled_dot_product_attention(q, k, v)
        else:
            raise NotImplementedError

        if ndim == 4:
            x = (
                x.view(B, self.num_heads, H, W, -1)
                .permute(0, 2, 3, 1, 4)
                .reshape(B, H, W, -1)
            )
        else:
            x = x.view(B, self.num_heads, L, -1).permute(0, 2, 1, 3).reshape(B, L, -1)

        x = self.proj(x)

        return x


class Block(nn.Module):
    """Transformer blocks with support of window attention"""

    def __init__(
        self,
        dim: int,
        num_heads: int,
        mlp_ratio: float = 4.0,
        qkv_bias: bool = True,
        drop_path: float = 0.0,
        norm_layer: Callable[..., nn.Module] = nn.LayerNorm,
        act_layer: Callable[..., nn.Module] = nn.GELU,
        use_rel_pos: bool = False,
        rel_pos_zero_init: bool = True,
        window_size: int = 0,
        input_size: Optional[Tuple[int, int]] = None,
        use_rope: bool = False,
        rope_pt_size: Optional[Tuple[int, int]] = None,
        rope_tiled: bool = False,
        rope_interp: bool = False,
        use_ve_rope: bool = False,
        cls_token: bool = False,
        dropout: float = 0.0,
        init_values: Optional[float] = None,
        attn_type: AttentionType = AttentionType.Vanilla,
        use_fa3: bool = False,
        use_rope_real: bool = False,
    ):
        """
        Args:
            dim (int): Number of input channels.
            num_heads (int): Number of attention heads in each ViT block.
            mlp_ratio (float): Ratio of mlp hidden dim to embedding dim.
            qkv_bias (bool): If True, add a learnable bias to query, key, value.
            drop_path (float): Stochastic depth rate.
            norm_layer (nn.Module): Normalization layer.
            act_layer (nn.Module): Activation layer.
            use_rel_pos (bool): If True, add relative positional embeddings to the attention map.
            rel_pos_zero_init (bool): If True, zero initialize relative positional parameters.
            window_size (int): Window size for window attention blocks. If it equals 0, then not
                use window attention.
            input_size (int or None): Input resolution for calculating the relative positional
                parameter size.
            dropout (float): Dropout rate.
            cls_token: whether a cls_token is present.
            use_rope: whether to use rope 2d (indep of use_rel_pos, as it can be used together)
            rope_pt_size: size of rope in previous stage of training, needed for interpolation or tiling
            rope_tiled: whether to tile rope or not; tile expected to be of size rope_pt_size x rope_pt_size
            rope_interp: whether to interpolate (or extrapolate) rope to match target input size,
                expected to specify source size as rope_pt_size.
            use_ve_rope: use ve orig rope implementation, if small numerical differences are important (normally not)
        """
        super().__init__()
        self.norm1 = norm_layer(dim)
        self.attn = Attention(
            dim,
            num_heads=num_heads,
            qkv_bias=qkv_bias,
            use_rel_pos=use_rel_pos,
            rel_pos_zero_init=rel_pos_zero_init,
            input_size=input_size if window_size == 0 else (window_size, window_size),
            attn_type=attn_type,
            use_rope=use_rope,
            rope_pt_size=rope_pt_size,
            rope_tiled=rope_tiled,
            rope_interp=rope_interp,
            use_ve_rope=use_ve_rope,
            cls_token=cls_token,
            use_fa3=use_fa3,
            use_rope_real=use_rope_real,
        )
        self.ls1 = (
            LayerScale(dim, init_values=init_values) if init_values else nn.Identity()
        )
        self.drop_path = DropPath(drop_path) if drop_path > 0.0 else nn.Identity()

        self.norm2 = norm_layer(dim)
        self.mlp = Mlp(
            in_features=dim,
            hidden_features=int(dim * mlp_ratio),
            act_layer=act_layer,
            drop=(dropout, 0.0),
        )
        self.ls2 = (
            LayerScale(dim, init_values=init_values) if init_values else nn.Identity()
        )
        self.dropout = nn.Dropout(dropout)
        self.window_size = window_size

    def forward(self, x: Tensor) -> Tensor:
        shortcut = x
        x = self.norm1(x)
        # Window partition
        if self.window_size > 0:
            H, W = x.shape[1], x.shape[2]
            x, pad_hw = window_partition(x, self.window_size)

        x = self.ls1(self.attn(x))
        # Reverse window partition
        if self.window_size > 0:
            x = window_unpartition(x, self.window_size, pad_hw, (H, W))

        x = shortcut + self.dropout(self.drop_path(x))
        x = x + self.dropout(self.drop_path(self.ls2(self.mlp(self.norm2(x)))))

        return x


class ViT(nn.Module):
    """
    This module implements Vision Transformer (ViT) backbone in :paper:`vitdet`.
    "Exploring Plain Vision Transformer Backbones for Object Detection",
    https://arxiv.org/abs/2203.16527
    """

    def __init__(
        self,
        img_size: int = 1024,
        patch_size: int = 16,
        in_chans: int = 3,
        embed_dim: int = 768,
        depth: int = 12,
        num_heads: int = 12,
        mlp_ratio: float = 4.0,
        qkv_bias: bool = True,
        drop_path_rate: float = 0.0,
        norm_layer: Union[Callable[..., nn.Module], str] = "LayerNorm",
        act_layer: Callable[..., nn.Module] = nn.GELU,
        use_abs_pos: bool = True,
        tile_abs_pos: bool = True,
        rel_pos_blocks: Union[Tuple[int, ...], bool] = (2, 5, 8, 11),
        rel_pos_zero_init: bool = True,
        window_size: int = 14,
        global_att_blocks: Tuple[int, ...] = (2, 5, 8, 11),
        use_rope: bool = False,
        use_tiled_rope: bool = False,
        rope_pt_size: Optional[int] = None,
        use_interp_rope: bool = False,
        use_ve_rope: bool = False,
        use_act_checkpoint: bool = True,
        pretrain_img_size: int = 224,
        pretrain_use_cls_token: bool = True,
        retain_cls_token: bool = True,
        dropout: float = 0.0,
        return_interm_layers: bool = False,
        init_values: Optional[float] = None,  # for layerscale
        attn_type: AttentionType = AttentionType.Vanilla,
        ln_pre: bool = False,
        ln_post: bool = False,
        bias_patch_embed: bool = True,
        compile_mode: Optional[str] = None,
        use_fa3: bool = False,
        use_rope_real: bool = False,
    ):
        """
        Args:
            img_size (int): Input image size. Only relevant for rel pos or rope.
            patch_size (int): Patch size.
            in_chans (int): Number of input image channels.
            embed_dim (int): Patch embedding dimension.
            depth (int): Depth of ViT.
            num_heads (int): Number of attention heads in each ViT block.
            mlp_ratio (float): Ratio of mlp hidden dim to embedding dim.
            qkv_bias (bool): If True, add a learnable bias to query, key, value.
            drop_path_rate (float): Stochastic depth rate.
            norm_layer (nn.Module): Normalization layer.
            act_layer (nn.Module): Activation layer.
            use_abs_pos (bool): If True, use absolute positional embeddings.
            tile_abs_pos (bool): If True, tile absolute positional embeddings instead of interpolation.
            rel_pos_blocks (list): Blocks which have rel pos embeddings.
            rel_pos_zero_init (bool): If True, zero initialize relative positional parameters.
            window_size (int): Window size for window attention blocks.
            global_att_blocks (list): Indexes for blocks using global attention (other blocks use window attention).
            use_rope (bool): whether to use rope 2d (indep of rel_pos_blocks, as it can be used together).
            rope_pt_size (int): size of rope in previous stage of training, needed for interpolation or tiling.
            use_interp_rope: whether to interpolate (or extrapolate) rope to match target input size,
                expected to specify source size as rope_pt_size.
            use_act_checkpoint (bool): If True, use activation checkpointing.
            pretrain_img_size (int): input image size for pretraining models.
            pretrain_use_cls_token (bool): If True, pretraining models use class token.
            retain_cls_token: whether cls_token should be retained.
            dropout (float): Dropout rate. Applied in residual blocks of attn, mlp and inside the mlp.

            return_interm_layers (bool): Whether to return intermediate layers (all global attention blocks).
            init_values: layer scale init, None for no layer scale.

            ln_pre (bool): If True, apply layer norm before transformer blocks.
            ln_post (bool): If True, apply layer norm after transformer blocks.
            bias_patch_embed (bool): bias in conv for patch embed?
            compile_mode (str): mode to compile the forward
        """
        super().__init__()
        self.pretrain_use_cls_token = pretrain_use_cls_token

        window_block_indexes = [i for i in range(depth) if i not in global_att_blocks]
        self.full_attn_ids = list(global_att_blocks)
        self.rel_pos_blocks = [False] * depth
        if isinstance(rel_pos_blocks, bool) and rel_pos_blocks:
            self.rel_pos_blocks = [True] * depth
        else:
            for i in rel_pos_blocks:
                self.rel_pos_blocks[i] = True

        self.retain_cls_token = retain_cls_token
        if self.retain_cls_token:
            assert pretrain_use_cls_token
            assert len(window_block_indexes) == 0, (
                "windowing not supported with cls token"
            )

            assert sum(self.rel_pos_blocks) == 0, "rel pos not supported with cls token"

            scale = embed_dim**-0.5
            self.class_embedding = nn.Parameter(scale * torch.randn(1, 1, embed_dim))

        if isinstance(norm_layer, str):
            norm_layer = partial(getattr(nn, norm_layer), eps=1e-5)

        self.patch_embed = PatchEmbed(
            kernel_size=(patch_size, patch_size),
            stride=(patch_size, patch_size),
            in_chans=in_chans,
            embed_dim=embed_dim,
            bias=bias_patch_embed,
        )

        # Handle absolute positional embedding
        self.tile_abs_pos = tile_abs_pos
        self.use_abs_pos = use_abs_pos
        if self.tile_abs_pos:
            assert self.use_abs_pos

        if self.use_abs_pos:
            # Initialize absolute positional embedding with pretrain image size.
            num_patches = (pretrain_img_size // patch_size) * (
                pretrain_img_size // patch_size
            )
            num_positions = (num_patches + 1) if pretrain_use_cls_token else num_patches
            self.pos_embed = nn.Parameter(torch.zeros(1, num_positions, embed_dim))
        else:
            self.pos_embed = None

        # stochastic depth decay rule
        dpr = [x.item() for x in torch.linspace(0, drop_path_rate, depth)]

        self.blocks = nn.ModuleList()
        cur_stage = 1
        for i in range(depth):
            block = Block(
                dim=embed_dim,
                num_heads=num_heads,
                mlp_ratio=mlp_ratio,
                qkv_bias=qkv_bias,
                drop_path=dpr[i],
                norm_layer=norm_layer,
                act_layer=act_layer,
                use_rel_pos=self.rel_pos_blocks[i],
                rel_pos_zero_init=rel_pos_zero_init,
                window_size=window_size if i in window_block_indexes else 0,
                input_size=(img_size // patch_size, img_size // patch_size),
                use_rope=use_rope,
                rope_pt_size=(
                    (window_size, window_size)
                    if rope_pt_size is None
                    else (rope_pt_size, rope_pt_size)
                ),
                rope_tiled=use_tiled_rope,
                use_ve_rope=use_ve_rope,
                rope_interp=use_interp_rope,
                cls_token=self.retain_cls_token,
                dropout=dropout,
                init_values=init_values,
                attn_type=attn_type,
                use_fa3=use_fa3,
                use_rope_real=use_rope_real,
            )

            if i not in window_block_indexes:
                cur_stage += 1

            self.use_act_checkpoint = use_act_checkpoint

            self.blocks.append(block)

        self.return_interm_layers = return_interm_layers
        self.channel_list = (
            [embed_dim] * len(self.full_attn_ids)
            if return_interm_layers
            else [embed_dim]
        )

        if self.pos_embed is not None:
            trunc_normal_(self.pos_embed, std=0.02)

        self.ln_pre = norm_layer(embed_dim) if ln_pre else nn.Identity()
        self.ln_post = norm_layer(embed_dim) if ln_post else nn.Identity()

        self.apply(self._init_weights)

        if compile_mode is not None:
            self.forward = torch.compile(
                self.forward, mode=compile_mode, fullgraph=True
            )
            if self.use_act_checkpoint and self.training:
                torch._dynamo.config.optimize_ddp = False

    def _init_weights(self, m: nn.Module) -> None:
        if isinstance(m, nn.Linear):
            trunc_normal_(m.weight, std=0.02)
            if isinstance(m, nn.Linear) and m.bias is not None:
                nn.init.constant_(m.bias, 0)
        elif isinstance(m, nn.LayerNorm):
            nn.init.constant_(m.bias, 0)
            nn.init.constant_(m.weight, 1.0)

    def forward(self, tensor_list):
        if isinstance(tensor_list, NestedTensor):
            x = tensor_list.tensors
            mask = tensor_list.mask
        else:
            x = tensor_list
            mask = None

        x = self.patch_embed(x)
        h, w = x.shape[1], x.shape[2]

        s = 0
        if self.retain_cls_token:
            # If cls_token is retained, we don't
            # maintain spatial shape
            x = torch.cat([self.class_embedding, x.flatten(1, 2)], dim=1)
            s = 1

        if self.pos_embed is not None:
            x = x + get_abs_pos(
                self.pos_embed,
                self.pretrain_use_cls_token,
                (h, w),
                self.retain_cls_token,
                tiling=self.tile_abs_pos,
            )

        x = self.ln_pre(x)

        outputs = []
        masks = None
        for i, blk in enumerate(self.blocks):
            if self.use_act_checkpoint and self.training:
                x = checkpoint.checkpoint(blk, x, use_reentrant=False)
            else:
                x = blk(x)
            if (i == self.full_attn_ids[-1]) or (
                self.return_interm_layers and i in self.full_attn_ids
            ):
                if i == self.full_attn_ids[-1]:
                    x = self.ln_post(x)

                feats = x[:, s:]
                if feats.ndim == 4:
                    feats = feats.permute(0, 3, 1, 2)
                else:
                    assert feats.ndim == 3
                    h = w = math.sqrt(feats.shape[1])
                    feats = feats.reshape(
                        feats.shape[0], h, w, feats.shape[-1]
                    ).permute(0, 3, 1, 2)

                if isinstance(tensor_list, NestedTensor):
                    # Optimization, if the mask is all False, just ignore it
                    if mask is not None and mask.any() and masks is None:
                        masks = F.interpolate(
                            mask[None].float(), size=feats.shape[-2:]
                        ).bool()[0]
                    outputs.append(NestedTensor(feats, masks))
                else:
                    outputs.append(feats)

        return outputs

    def get_layer_id(self, layer_name: str) -> int:
        # https://github.com/microsoft/unilm/blob/master/beit/optim_factory.py#L33
        num_layers = self.get_num_layers()

        if layer_name.find("rel_pos") != -1:
            return num_layers + 1
        elif layer_name.find("ln_pre") != -1:
            return 0
        elif layer_name.find("pos_embed") != -1 or layer_name.find("cls_token") != -1:
            return 0
        elif layer_name.find("patch_embed") != -1:
            return 0
        elif layer_name.find("blocks") != -1:
            return int(layer_name.split("blocks")[1].split(".")[1]) + 1
        else:
            return num_layers + 1

    def get_num_layers(self) -> int:
        return len(self.blocks)



================================================
FILE: sam3/model/vl_combiner.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

"""Provides utility to combine a vision backbone with a language backbone."""

from copy import copy
from typing import List, Optional

import torch
import torch.nn as nn
from torch.nn.attention import sdpa_kernel, SDPBackend

from .act_ckpt_utils import activation_ckpt_wrapper
from .data_misc import NestedTensor
from .necks import Sam3DualViTDetNeck, Sam3TriViTDetNeck


class SAM3VLBackbone(nn.Module):
    """This backbone combines a vision backbone and a language backbone without fusion.
    As such it is more of a convenience wrapper to handle the two backbones together.

    It adds support for activation checkpointing and compilation.
    """

    def __init__(
        self,
        visual: Sam3DualViTDetNeck,
        text,
        compile_visual: bool = False,
        act_ckpt_whole_vision_backbone: bool = False,
        act_ckpt_whole_language_backbone: bool = False,
        scalp=0,
    ):
        """Initialize the backbone combiner.

        :param visual: The vision backbone to use
        :param text: The text encoder to use
        """
        super().__init__()
        self.vision_backbone: Sam3DualViTDetNeck = (
            torch.compile(visual) if compile_visual else visual
        )
        self.language_backbone = text
        self.scalp = scalp
        # allow running activation checkpointing on the entire vision and language backbones
        self.act_ckpt_whole_vision_backbone = act_ckpt_whole_vision_backbone
        self.act_ckpt_whole_language_backbone = act_ckpt_whole_language_backbone

    def forward(
        self,
        samples: torch.Tensor,
        captions: List[str],
        input_boxes: Optional[torch.Tensor] = None,
        additional_text: Optional[List[str]] = None,
    ):
        """Forward pass of the backbone combiner.

        :param samples: The input images
        :param captions: The input captions
        :param input_boxes: If the text contains place-holders for boxes, this
            parameter contains the tensor containing their spatial features
        :param additional_text: This can be used to encode some additional text
            (different from the captions) in the same forward of the backbone
        :return: Output dictionary with the following keys:
            - vision_features: The output of the vision backbone
            - language_features: The output of the language backbone
            - language_mask: The attention mask of the language backbone
            - vision_pos_enc: The positional encoding of the vision backbone
            - (optional) additional_text_features: The output of the language
                backbone for the additional text
            - (optional) additional_text_mask: The attention mask of the
                language backbone for the additional text
        """
        output = self.forward_image(samples)
        device = output["vision_features"].device
        output.update(self.forward_text(captions, input_boxes, additional_text, device))
        return output

    def forward_image(self, samples: torch.Tensor):
        return activation_ckpt_wrapper(self._forward_image_no_act_ckpt)(
            samples=samples,
            act_ckpt_enable=self.act_ckpt_whole_vision_backbone and self.training,
        )

    def _forward_image_no_act_ckpt(self, samples):
        # Forward through backbone
        sam3_features, sam3_pos, sam2_features, sam2_pos = self.vision_backbone.forward(
            samples
        )
        if self.scalp > 0:
            # Discard the lowest resolution features
            sam3_features, sam3_pos = (
                sam3_features[: -self.scalp],
                sam3_pos[: -self.scalp],
            )
            if sam2_features is not None and sam2_pos is not None:
                sam2_features, sam2_pos = (
                    sam2_features[: -self.scalp],
                    sam2_pos[: -self.scalp],
                )

        sam2_output = None

        if sam2_features is not None and sam2_pos is not None:
            sam2_src = sam2_features[-1]
            sam2_output = {
                "vision_features": sam2_src,
                "vision_pos_enc": sam2_pos,
                "backbone_fpn": sam2_features,
            }

        sam3_src = sam3_features[-1]
        output = {
            "vision_features": sam3_src,
            "vision_pos_enc": sam3_pos,
            "backbone_fpn": sam3_features,
            "sam2_backbone_out": sam2_output,
        }

        return output

    def forward_text(
        self, captions, input_boxes=None, additional_text=None, device="cuda"
    ):
        return activation_ckpt_wrapper(self._forward_text_no_ack_ckpt)(
            captions=captions,
            input_boxes=input_boxes,
            additional_text=additional_text,
            device=device,
            act_ckpt_enable=self.act_ckpt_whole_language_backbone and self.training,
        )

    def _forward_text_no_ack_ckpt(
        self,
        captions,
        input_boxes=None,
        additional_text=None,
        device="cuda",
    ):
        output = {}

        # Forward through text_encoder
        text_to_encode = copy(captions)
        if additional_text is not None:
            # if there are additional_text, we piggy-back them into this forward.
            # They'll be used later for output alignment
            text_to_encode += additional_text

        sdpa_context = sdpa_kernel(
            [
                SDPBackend.MATH,
                SDPBackend.EFFICIENT_ATTENTION,
                SDPBackend.FLASH_ATTENTION,
            ]
        )

        with sdpa_context:
            text_attention_mask, text_memory, text_embeds = self.language_backbone(
                text_to_encode, input_boxes, device=device
            )

        if additional_text is not None:
            output["additional_text_features"] = text_memory[:, -len(additional_text) :]
            output["additional_text_mask"] = text_attention_mask[
                -len(additional_text) :
            ]

        text_memory = text_memory[:, : len(captions)]
        text_attention_mask = text_attention_mask[: len(captions)]
        text_embeds = text_embeds[:, : len(captions)]
        output["language_features"] = text_memory
        output["language_mask"] = text_attention_mask
        output["language_embeds"] = (
            text_embeds  # Text embeddings before forward to the encoder
        )

        return output


class SAM3VLBackboneTri(SAM3VLBackbone):
    """VL backbone with triple-head vision (sam3, interactive, propagation) + text encoder."""

    def __init__(self, visual, text, compile_visual=False, scalp=0):
        super().__init__(
            visual=visual, text=text, compile_visual=compile_visual, scalp=scalp
        )
        assert isinstance(self.vision_backbone, Sam3TriViTDetNeck), (
            f"Expected vision backbone to be of type Sam3TriViTDetNeck, got {type(self.vision_backbone)}"
        )

    def forward_image(
        self,
        samples,
        *,
        need_sam3_out: bool = True,
        need_interactive_out: bool = True,
        need_propagation_out: bool = True,
    ):
        return activation_ckpt_wrapper(self._forward_image_tri_no_act_ckpt)(
            samples=samples,
            need_sam3_out=need_sam3_out,
            need_interactive_out=need_interactive_out,
            need_propagation_out=need_propagation_out,
            act_ckpt_enable=self.act_ckpt_whole_vision_backbone and self.training,
        )

    def _forward_image_tri_no_act_ckpt(
        self,
        samples,
        need_sam3_out=True,
        need_interactive_out=True,
        need_propagation_out=True,
    ):
        (
            sam3_features,
            sam3_pos,
            interactive_features,
            interactive_pos,
            propagation_features,
            propagation_pos,
        ) = self.vision_backbone.forward(
            samples,
            need_sam3_out=need_sam3_out,
            need_interactive_out=need_interactive_out,
            need_propagation_out=need_propagation_out,
        )
        if self.scalp > 0:
            sam3_features, sam3_pos = (
                sam3_features[: -self.scalp],
                sam3_pos[: -self.scalp],
            )
            interactive_features, interactive_pos = (
                interactive_features[: -self.scalp],
                interactive_pos[: -self.scalp],
            )
            propagation_features, propagation_pos = (
                propagation_features[: -self.scalp],
                propagation_pos[: -self.scalp],
            )

        output = {}
        if need_sam3_out:
            sam3_last = sam3_features[-1]
            output.update(
                {
                    "vision_features": sam3_last.tensors,
                    "vision_mask": sam3_last.mask,
                    "vision_pos_enc": sam3_pos,
                    "backbone_fpn": sam3_features,
                }
            )
        if need_interactive_out:
            inte_last = interactive_features[-1]
            output["interactive"] = {
                "vision_features": inte_last.tensors,
                "vision_mask": inte_last.mask,
                "vision_pos_enc": interactive_pos,
                "backbone_fpn": interactive_features,
            }
        if need_propagation_out:
            prop_last = propagation_features[-1]
            output["sam2_backbone_out"] = {
                "vision_features": prop_last.tensors,
                "vision_mask": prop_last.mask,
                "vision_pos_enc": propagation_pos,
                "backbone_fpn": propagation_features,
            }
        return output


class VisionOnly(nn.Module):
    def __init__(
        self,
        visual,
        n_features,
        forward_in_chunk_for_eval=False,
        eval_chunk_size=4,
        eval_cast_to_cpu=False,
        scalp=0,
        compile_mode: str = None,
        compile_extra_args: Optional[dict] = None,
    ):
        super().__init__()
        self.vision_backbone = visual
        self.should_compile = compile_mode is not None or compile_extra_args is not None
        self.compile_mode = compile_mode
        self.compile_extra_args = compile_extra_args or {}
        self.compiled = False
        self.n_features = n_features
        self.forward_in_chunk_for_eval = forward_in_chunk_for_eval
        self.eval_chunk_size = eval_chunk_size
        self.eval_cast_to_cpu = eval_cast_to_cpu
        self.scalp = scalp

    def _compile(self):
        if self.should_compile and not self.compiled:
            self.vision_backbone = torch.compile(
                self.vision_backbone, mode=self.compile_mode, **self.compile_extra_args
            )
            self.compiled = True

    def forward_image(self, samples):
        self._compile()
        # Forward through backbone
        features, pos = self.vision_backbone(samples)
        if self.scalp > 0:
            features, pos = features[: -self.scalp], pos[: -self.scalp]
        elif self.scalp < 0:
            features.pop(self.scalp)
            pos.pop(self.scalp)

        src, mask = features[-1].decompose()
        output = {
            "vision_features": src,
            "vision_mask": mask,
            "vision_pos_enc": pos,
            "backbone_fpn": features,
        }
        return output

    def forward_text(
        self,
        captions,
        input_boxes=None,
        additional_text=None,
        device="cuda",
    ):
        bs = len(captions)
        output = {
            "language_features": torch.zeros((0, bs, self.n_features), device=device),
            "language_mask": torch.zeros((bs, 0), device=device),
        }
        return output


class TriHeadVisionOnly(VisionOnly):
    def __init__(
        self,
        visual,
        n_features,
        forward_in_chunk_for_eval=False,
        eval_chunk_size=4,
        eval_cast_to_cpu=False,
        scalp=0,
        compile_mode: str = None,
        compile_extra_args: Optional[dict] = None,
    ):
        super().__init__(
            visual=visual,
            n_features=n_features,
            forward_in_chunk_for_eval=forward_in_chunk_for_eval,
            eval_chunk_size=eval_chunk_size,
            eval_cast_to_cpu=eval_cast_to_cpu,
            scalp=scalp,
            compile_mode=compile_mode,
            compile_extra_args=compile_extra_args,
        )
        assert isinstance(self.vision_backbone, Sam3TriViTDetNeck), (
            f"Expected vision backbone to be of type Sam3TriViTDetNeck, got {type(self.vision_backbone)}"
        )

    def forward_image(
        self,
        samples,
        *,
        need_sam3_out: bool = True,
        need_interactive_out: bool = True,
        need_propagation_out: bool = True,
    ):
        self._compile()
        # Forward through backbone
        (
            sam3_features,
            sam3_pos,
            interactive_features,
            interactive_pos,
            propagation_features,
            propagation_pos,
        ) = self.vision_backbone(
            samples,
            need_sam3_out=need_sam3_out,
            need_interactive_out=need_interactive_out,
            need_propagation_out=need_propagation_out,
        )

        if self.scalp > 0:
            sam3_features, sam3_pos = (
                sam3_features[: -self.scalp],
                sam3_pos[: -self.scalp],
            )
            interactive_features, interactive_pos = (
                interactive_features[: -self.scalp],
                interactive_pos[: -self.scalp],
            )
            propagation_features, propagation_pos = (
                propagation_features[: -self.scalp],
                propagation_pos[: -self.scalp],
            )

        output = {}

        if need_sam3_out:
            sam3_last = sam3_features[-1]
            output.update(
                {
                    "vision_features": sam3_last.tensors,
                    "vision_mask": sam3_last.mask,
                    "vision_pos_enc": sam3_pos,
                    "backbone_fpn": sam3_features,
                }
            )
        if need_interactive_out:
            inte_last = interactive_features[-1]
            output["interactive"] = {
                "vision_features": inte_last.tensors,
                "vision_mask": inte_last.mask,
                "vision_pos_enc": interactive_pos,
                "backbone_fpn": interactive_features,
            }
        if need_propagation_out:
            prop_last = propagation_features[-1]
            output["sam2_backbone_out"] = {
                "vision_features": prop_last.tensors,
                "vision_mask": prop_last.mask,
                "vision_pos_enc": propagation_pos,
                "backbone_fpn": propagation_features,
            }

        return output



================================================
FILE: sam3/model/utils/__init__.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved
# All rights reserved.

# pyre-unsafe

# This source code is licensed under the license found in the
# LICENSE file in the root directory of this source tree.



================================================
FILE: sam3/model/utils/misc.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

from collections import defaultdict
from dataclasses import fields, is_dataclass
from typing import Any, Mapping, Protocol, runtime_checkable

import torch


def _is_named_tuple(x) -> bool:
    return isinstance(x, tuple) and hasattr(x, "_asdict") and hasattr(x, "_fields")


@runtime_checkable
class _CopyableData(Protocol):
    def to(self, device: torch.device, *args: Any, **kwargs: Any):
        """Copy data to the specified device"""
        ...


def copy_data_to_device(data, device: torch.device, *args: Any, **kwargs: Any):
    """Function that recursively copies data to a torch.device.

    Args:
        data: The data to copy to device
        device: The device to which the data should be copied
        args: positional arguments that will be passed to the `to` call
        kwargs: keyword arguments that will be passed to the `to` call

    Returns:
        The data on the correct device
    """

    if _is_named_tuple(data):
        return type(data)(
            **copy_data_to_device(data._asdict(), device, *args, **kwargs)
        )
    elif isinstance(data, (list, tuple)):
        return type(data)(copy_data_to_device(e, device, *args, **kwargs) for e in data)
    elif isinstance(data, defaultdict):
        return type(data)(
            data.default_factory,
            {
                k: copy_data_to_device(v, device, *args, **kwargs)
                for k, v in data.items()
            },
        )
    elif isinstance(data, Mapping):
        return type(data)(
            {
                k: copy_data_to_device(v, device, *args, **kwargs)
                for k, v in data.items()
            }
        )
    elif is_dataclass(data) and not isinstance(data, type):
        new_data_class = type(data)(
            **{
                field.name: copy_data_to_device(
                    getattr(data, field.name), device, *args, **kwargs
                )
                for field in fields(data)
                if field.init
            }
        )
        for field in fields(data):
            if not field.init:
                setattr(
                    new_data_class,
                    field.name,
                    copy_data_to_device(
                        getattr(data, field.name), device, *args, **kwargs
                    ),
                )
        return new_data_class
    elif isinstance(data, _CopyableData):
        return data.to(device, *args, **kwargs)
    return data



================================================
FILE: sam3/model/utils/sam1_utils.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved
# All rights reserved.

# pyre-unsafe

# This source code is licensed under the license found in the
# LICENSE file in the root directory of this source tree.

import warnings

import torch
import torch.nn as nn
import torch.nn.functional as F
from torchvision.transforms import Normalize, Resize, ToTensor


# Adapted from https://github.com/facebookresearch/sam2/blob/main/sam2/utils/transforms.py
class SAM2Transforms(nn.Module):
    def __init__(
        self, resolution, mask_threshold, max_hole_area=0.0, max_sprinkle_area=0.0
    ):
        """
        Transforms for SAM2.
        """
        super().__init__()
        self.resolution = resolution
        self.mask_threshold = mask_threshold
        self.max_hole_area = max_hole_area
        self.max_sprinkle_area = max_sprinkle_area
        self.mean = [0.5, 0.5, 0.5]
        self.std = [0.5, 0.5, 0.5]
        self.to_tensor = ToTensor()
        self.transforms = torch.jit.script(
            nn.Sequential(
                Resize((self.resolution, self.resolution)),
                Normalize(self.mean, self.std),
            )
        )

    def __call__(self, x):
        x = self.to_tensor(x)
        return self.transforms(x)

    def forward_batch(self, img_list):
        img_batch = [self.transforms(self.to_tensor(img)) for img in img_list]
        img_batch = torch.stack(img_batch, dim=0)
        return img_batch

    def transform_coords(
        self, coords: torch.Tensor, normalize=False, orig_hw=None
    ) -> torch.Tensor:
        """
        Expects a torch tensor with length 2 in the last dimension. The coordinates can be in absolute image or normalized coordinates,
        If the coords are in absolute image coordinates, normalize should be set to True and original image size is required.

        Returns
            Un-normalized coordinates in the range of [0, 1] which is expected by the SAM2 model.
        """
        if normalize:
            assert orig_hw is not None
            h, w = orig_hw
            coords = coords.clone()
            coords[..., 0] = coords[..., 0] / w
            coords[..., 1] = coords[..., 1] / h

        coords = coords * self.resolution  # unnormalize coords
        return coords

    def transform_boxes(
        self, boxes: torch.Tensor, normalize=False, orig_hw=None
    ) -> torch.Tensor:
        """
        Expects a tensor of shape Bx4. The coordinates can be in absolute image or normalized coordinates,
        if the coords are in absolute image coordinates, normalize should be set to True and original image size is required.
        """
        boxes = self.transform_coords(boxes.reshape(-1, 2, 2), normalize, orig_hw)
        return boxes

    def postprocess_masks(self, masks: torch.Tensor, orig_hw) -> torch.Tensor:
        """
        Perform PostProcessing on output masks.
        """
        masks = masks.float()
        input_masks = masks
        mask_flat = masks.flatten(0, 1).unsqueeze(1)  # flatten as 1-channel image
        try:
            from sam3.perflib.connected_components import connected_components

            if self.max_hole_area > 0:
                # Holes are those connected components in background with area <= self.fill_hole_area
                # (background regions are those with mask scores <= self.mask_threshold)
                labels, areas = connected_components(
                    (mask_flat <= self.mask_threshold).to(torch.uint8)
                )
                is_hole = (labels > 0) & (areas <= self.max_hole_area)
                is_hole = is_hole.reshape_as(masks)
                # We fill holes with a small positive mask score (10.0) to change them to foreground.
                masks = torch.where(is_hole, self.mask_threshold + 10.0, masks)

            if self.max_sprinkle_area > 0:
                labels, areas = connected_components(
                    (mask_flat > self.mask_threshold).to(torch.uint8)
                )
                is_hole = (labels > 0) & (areas <= self.max_sprinkle_area)
                is_hole = is_hole.reshape_as(masks)
                # We fill holes with negative mask score (-10.0) to change them to background.
                masks = torch.where(is_hole, self.mask_threshold - 10.0, masks)
        except Exception as e:
            # Skip the post-processing step if the CUDA kernel fails
            warnings.warn(
                f"{e}\n\nSkipping the post-processing step due to the error above. You can "
                "still use SAM 3 and it's OK to ignore the error above, although some post-processing "
                "functionality may be limited (which doesn't affect the results in most cases; see "
                "https://github.com/facebookresearch/sam3/blob/main/INSTALL.md).",
                category=UserWarning,
                stacklevel=2,
            )
            masks = input_masks

        masks = F.interpolate(masks, orig_hw, mode="bilinear", align_corners=False)
        return masks



================================================
FILE: sam3/model/utils/sam2_utils.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved
# All rights reserved.

# pyre-unsafe

# This source code is licensed under the license found in the
# LICENSE file in the root directory of this source tree.

import os
from threading import Thread

import numpy as np
import torch
from PIL import Image
from tqdm import tqdm


def _load_img_as_tensor(img_path, image_size):
    img_pil = Image.open(img_path)
    img_np = np.array(img_pil.convert("RGB").resize((image_size, image_size)))
    if img_np.dtype == np.uint8:  # np.uint8 is expected for JPEG images
        img_np = img_np / 255.0
    else:
        raise RuntimeError(f"Unknown image dtype: {img_np.dtype} on {img_path}")
    img = torch.from_numpy(img_np).permute(2, 0, 1)
    video_width, video_height = img_pil.size  # the original video size
    return img, video_height, video_width


class AsyncVideoFrameLoader:
    """
    A list of video frames to be load asynchronously without blocking session start.
    """

    def __init__(
        self,
        img_paths,
        image_size,
        offload_video_to_cpu,
        img_mean,
        img_std,
        compute_device,
    ):
        self.img_paths = img_paths
        self.image_size = image_size
        self.offload_video_to_cpu = offload_video_to_cpu
        self.img_mean = img_mean
        self.img_std = img_std
        # items in `self.images` will be loaded asynchronously
        self.images = [None] * len(img_paths)
        # catch and raise any exceptions in the async loading thread
        self.exception = None
        # video_height and video_width be filled when loading the first image
        self.video_height = None
        self.video_width = None
        self.compute_device = compute_device

        # load the first frame to fill video_height and video_width and also
        # to cache it (since it's most likely where the user will click)
        self.__getitem__(0)

        # load the rest of frames asynchronously without blocking the session start
        def _load_frames():
            try:
                for n in tqdm(range(len(self.images)), desc="frame loading (JPEG)"):
                    self.__getitem__(n)
            except Exception as e:
                self.exception = e

        self.thread = Thread(target=_load_frames, daemon=True)
        self.thread.start()

    def __getitem__(self, index):
        if self.exception is not None:
            raise RuntimeError("Failure in frame loading thread") from self.exception

        img = self.images[index]
        if img is not None:
            return img

        img, video_height, video_width = _load_img_as_tensor(
            self.img_paths[index], self.image_size
        )
        self.video_height = video_height
        self.video_width = video_width
        # normalize by mean and std
        img -= self.img_mean
        img /= self.img_std
        if not self.offload_video_to_cpu:
            img = img.to(self.compute_device, non_blocking=True)
        self.images[index] = img
        return img

    def __len__(self):
        return len(self.images)


def load_video_frames(
    video_path,
    image_size,
    offload_video_to_cpu,
    img_mean=(0.5, 0.5, 0.5),
    img_std=(0.5, 0.5, 0.5),
    async_loading_frames=False,
    compute_device=torch.device("cuda"),
):
    """
    Load the video frames from video_path. The frames are resized to image_size as in
    the model and are loaded to GPU if offload_video_to_cpu=False. This is used by the demo.
    """
    is_bytes = isinstance(video_path, bytes)
    is_str = isinstance(video_path, str)
    is_mp4_path = is_str and os.path.splitext(video_path)[-1] in [".mp4", ".MP4"]
    if is_bytes or is_mp4_path:
        return load_video_frames_from_video_file(
            video_path=video_path,
            image_size=image_size,
            offload_video_to_cpu=offload_video_to_cpu,
            img_mean=img_mean,
            img_std=img_std,
            compute_device=compute_device,
        )
    elif is_str and os.path.isdir(video_path):
        return load_video_frames_from_jpg_images(
            video_path=video_path,
            image_size=image_size,
            offload_video_to_cpu=offload_video_to_cpu,
            img_mean=img_mean,
            img_std=img_std,
            async_loading_frames=async_loading_frames,
            compute_device=compute_device,
        )
    else:
        raise NotImplementedError(
            "Only MP4 video and JPEG folder are supported at this moment"
        )


def load_video_frames_from_jpg_images(
    video_path,
    image_size,
    offload_video_to_cpu,
    img_mean=(0.5, 0.5, 0.5),
    img_std=(0.5, 0.5, 0.5),
    async_loading_frames=False,
    compute_device=torch.device("cuda"),
):
    """
    Load the video frames from a directory of JPEG files ("<frame_index>.jpg" format).

    The frames are resized to image_size x image_size and are loaded to GPU if
    `offload_video_to_cpu` is `False` and to CPU if `offload_video_to_cpu` is `True`.

    You can load a frame asynchronously by setting `async_loading_frames` to `True`.
    """
    if isinstance(video_path, str) and os.path.isdir(video_path):
        jpg_folder = video_path
    else:
        raise NotImplementedError(
            "Only JPEG frames are supported at this moment. For video files, you may use "
            "ffmpeg (https://ffmpeg.org/) to extract frames into a folder of JPEG files, such as \n"
            "```\n"
            "ffmpeg -i <your_video>.mp4 -q:v 2 -start_number 0 <output_dir>/'%05d.jpg'\n"
            "```\n"
            "where `-q:v` generates high-quality JPEG frames and `-start_number 0` asks "
            "ffmpeg to start the JPEG file from 00000.jpg."
        )

    frame_names = [
        p
        for p in os.listdir(jpg_folder)
        if os.path.splitext(p)[-1] in [".jpg", ".jpeg", ".JPG", ".JPEG"]
    ]
    frame_names.sort(key=lambda p: int(os.path.splitext(p)[0]))
    num_frames = len(frame_names)
    if num_frames == 0:
        raise RuntimeError(f"no images found in {jpg_folder}")
    img_paths = [os.path.join(jpg_folder, frame_name) for frame_name in frame_names]
    img_mean = torch.tensor(img_mean, dtype=torch.float32)[:, None, None]
    img_std = torch.tensor(img_std, dtype=torch.float32)[:, None, None]

    if async_loading_frames:
        lazy_images = AsyncVideoFrameLoader(
            img_paths,
            image_size,
            offload_video_to_cpu,
            img_mean,
            img_std,
            compute_device,
        )
        return lazy_images, lazy_images.video_height, lazy_images.video_width

    images = torch.zeros(num_frames, 3, image_size, image_size, dtype=torch.float32)
    for n, img_path in enumerate(tqdm(img_paths, desc="frame loading (JPEG)")):
        images[n], video_height, video_width = _load_img_as_tensor(img_path, image_size)
    if not offload_video_to_cpu:
        images = images.to(compute_device)
        img_mean = img_mean.to(compute_device)
        img_std = img_std.to(compute_device)
    # normalize by mean and std
    images -= img_mean
    images /= img_std
    return images, video_height, video_width


def load_video_frames_from_video_file(
    video_path,
    image_size,
    offload_video_to_cpu,
    img_mean=(0.5, 0.5, 0.5),
    img_std=(0.5, 0.5, 0.5),
    compute_device=torch.device("cuda"),
):
    """Load the video frames from a video file."""
    import decord

    img_mean = torch.tensor(img_mean, dtype=torch.float32)[:, None, None]
    img_std = torch.tensor(img_std, dtype=torch.float32)[:, None, None]
    # Get the original video height and width
    decord.bridge.set_bridge("torch")
    video_height, video_width, _ = decord.VideoReader(video_path).next().shape
    # Iterate over all frames in the video
    images = []
    for frame in decord.VideoReader(video_path, width=image_size, height=image_size):
        images.append(frame.permute(2, 0, 1))

    images = torch.stack(images, dim=0).float() / 255.0
    if not offload_video_to_cpu:
        images = images.to(compute_device)
        img_mean = img_mean.to(compute_device)
        img_std = img_std.to(compute_device)
    # normalize by mean and std
    images -= img_mean
    images /= img_std
    return images, video_height, video_width



================================================
FILE: sam3/sam/__init__.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe
from .mask_decoder import MaskDecoder
from .prompt_encoder import PromptEncoder
from .transformer import TwoWayTransformer



================================================
FILE: sam3/sam/common.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

from typing import Type

import torch
import torch.nn as nn


class MLPBlock(nn.Module):
    def __init__(
        self,
        embedding_dim: int,
        mlp_dim: int,
        act: Type[nn.Module] = nn.GELU,
    ) -> None:
        super().__init__()
        self.lin1 = nn.Linear(embedding_dim, mlp_dim)
        self.lin2 = nn.Linear(mlp_dim, embedding_dim)
        self.act = act()

    def forward(self, x: torch.Tensor) -> torch.Tensor:
        return self.lin2(self.act(self.lin1(x)))


# From https://github.com/facebookresearch/detectron2/blob/main/detectron2/layers/batch_norm.py # noqa
# Itself from https://github.com/facebookresearch/ConvNeXt/blob/d1fa8f6fef0a165b27399986cc2bdacc92777e40/models/convnext.py#L119  # noqa
class LayerNorm2d(nn.Module):
    def __init__(self, num_channels: int, eps: float = 1e-6) -> None:
        super().__init__()
        self.weight = nn.Parameter(torch.ones(num_channels))
        self.bias = nn.Parameter(torch.zeros(num_channels))
        self.eps = eps

    def forward(self, x: torch.Tensor) -> torch.Tensor:
        u = x.mean(1, keepdim=True)
        s = (x - u).pow(2).mean(1, keepdim=True)
        x = (x - u) / torch.sqrt(s + self.eps)
        x = self.weight[:, None, None] * x + self.bias[:, None, None]
        return x



================================================
FILE: sam3/sam/mask_decoder.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

from typing import List, Optional, Tuple, Type

import torch
from torch import nn
from torch.nn import functional as F

from .common import LayerNorm2d


class MaskDecoder(nn.Module):
    def __init__(
        self,
        *,
        transformer_dim: int,
        transformer: nn.Module,
        num_multimask_outputs: int = 3,
        activation: Type[nn.Module] = nn.GELU,
        iou_head_depth: int = 3,
        iou_head_hidden_dim: int = 256,
        use_high_res_features: bool = False,
        iou_prediction_use_sigmoid=False,
        dynamic_multimask_via_stability=False,
        dynamic_multimask_stability_delta=0.05,
        dynamic_multimask_stability_thresh=0.98,
        pred_obj_scores: bool = False,
        pred_obj_scores_mlp: bool = False,
        use_multimask_token_for_obj_ptr: bool = False,
    ) -> None:
        """
        Predicts masks given an image and prompt embeddings, using a
        transformer architecture.

        Arguments:
          transformer_dim (int): the channel dimension of the transformer
          transformer (nn.Module): the transformer used to predict masks
          num_multimask_outputs (int): the number of masks to predict
            when disambiguating masks
          activation (nn.Module): the type of activation to use when
            upscaling masks
          iou_head_depth (int): the depth of the MLP used to predict
            mask quality
          iou_head_hidden_dim (int): the hidden dimension of the MLP
            used to predict mask quality
        """
        super().__init__()
        self.transformer_dim = transformer_dim
        self.transformer = transformer

        self.num_multimask_outputs = num_multimask_outputs

        self.iou_token = nn.Embedding(1, transformer_dim)
        self.num_mask_tokens = num_multimask_outputs + 1
        self.mask_tokens = nn.Embedding(self.num_mask_tokens, transformer_dim)

        self.pred_obj_scores = pred_obj_scores
        if self.pred_obj_scores:
            self.obj_score_token = nn.Embedding(1, transformer_dim)
        self.use_multimask_token_for_obj_ptr = use_multimask_token_for_obj_ptr

        self.output_upscaling = nn.Sequential(
            nn.ConvTranspose2d(
                transformer_dim, transformer_dim // 4, kernel_size=2, stride=2
            ),
            LayerNorm2d(transformer_dim // 4),
            activation(),
            nn.ConvTranspose2d(
                transformer_dim // 4, transformer_dim // 8, kernel_size=2, stride=2
            ),
            activation(),
        )
        self.use_high_res_features = use_high_res_features
        if use_high_res_features:
            self.conv_s0 = nn.Conv2d(
                transformer_dim, transformer_dim // 8, kernel_size=1, stride=1
            )
            self.conv_s1 = nn.Conv2d(
                transformer_dim, transformer_dim // 4, kernel_size=1, stride=1
            )

        self.output_hypernetworks_mlps = nn.ModuleList(
            [
                MLP(transformer_dim, transformer_dim, transformer_dim // 8, 3)
                for i in range(self.num_mask_tokens)
            ]
        )

        self.iou_prediction_head = MLP(
            transformer_dim,
            iou_head_hidden_dim,
            self.num_mask_tokens,
            iou_head_depth,
            sigmoid_output=iou_prediction_use_sigmoid,
        )
        if self.pred_obj_scores:
            self.pred_obj_score_head = nn.Linear(transformer_dim, 1)
            if pred_obj_scores_mlp:
                self.pred_obj_score_head = MLP(transformer_dim, transformer_dim, 1, 3)

        # When outputting a single mask, optionally we can dynamically fall back to the best
        # multimask output token if the single mask output token gives low stability scores.
        self.dynamic_multimask_via_stability = dynamic_multimask_via_stability
        self.dynamic_multimask_stability_delta = dynamic_multimask_stability_delta
        self.dynamic_multimask_stability_thresh = dynamic_multimask_stability_thresh

    def forward(
        self,
        image_embeddings: torch.Tensor,
        image_pe: torch.Tensor,
        sparse_prompt_embeddings: torch.Tensor,
        dense_prompt_embeddings: torch.Tensor,
        multimask_output: bool,
        repeat_image: bool,
        high_res_features: Optional[List[torch.Tensor]] = None,
    ) -> Tuple[torch.Tensor, torch.Tensor]:
        """
        Predict masks given image and prompt embeddings.

        Arguments:
          image_embeddings (torch.Tensor): the embeddings from the image encoder
          image_pe (torch.Tensor): positional encoding with the shape of image_embeddings
          sparse_prompt_embeddings (torch.Tensor): the embeddings of the points and boxes
          dense_prompt_embeddings (torch.Tensor): the embeddings of the mask inputs
          multimask_output (bool): Whether to return multiple masks or a single
            mask.

        Returns:
          torch.Tensor: batched predicted masks
          torch.Tensor: batched predictions of mask quality
          torch.Tensor: batched SAM token for mask output
        """
        masks, iou_pred, mask_tokens_out, object_score_logits = self.predict_masks(
            image_embeddings=image_embeddings,
            image_pe=image_pe,
            sparse_prompt_embeddings=sparse_prompt_embeddings,
            dense_prompt_embeddings=dense_prompt_embeddings,
            repeat_image=repeat_image,
            high_res_features=high_res_features,
        )

        # Select the correct mask or masks for output
        if multimask_output:
            masks = masks[:, 1:, :, :]
            iou_pred = iou_pred[:, 1:]
        elif self.dynamic_multimask_via_stability and not self.training:
            masks, iou_pred = self._dynamic_multimask_via_stability(masks, iou_pred)
        else:
            masks = masks[:, 0:1, :, :]
            iou_pred = iou_pred[:, 0:1]

        if multimask_output and self.use_multimask_token_for_obj_ptr:
            sam_tokens_out = mask_tokens_out[:, 1:]  # [b, 3, c] shape
        else:
            # Take the mask output token. Here we *always* use the token for single mask output.
            # At test time, even if we track after 1-click (and using multimask_output=True),
            # we still take the single mask token here. The rationale is that we always track
            # after multiple clicks during training, so the past tokens seen during training
            # are always the single mask token (and we'll let it be the object-memory token).
            sam_tokens_out = mask_tokens_out[:, 0:1]  # [b, 1, c] shape

        # Prepare output
        return masks, iou_pred, sam_tokens_out, object_score_logits

    def predict_masks(
        self,
        image_embeddings: torch.Tensor,
        image_pe: torch.Tensor,
        sparse_prompt_embeddings: torch.Tensor,
        dense_prompt_embeddings: torch.Tensor,
        repeat_image: bool,
        high_res_features: Optional[List[torch.Tensor]] = None,
    ) -> Tuple[torch.Tensor, torch.Tensor]:
        """Predicts masks. See 'forward' for more details."""
        # Concatenate output tokens
        s = 0
        if self.pred_obj_scores:
            output_tokens = torch.cat(
                [
                    self.obj_score_token.weight,
                    self.iou_token.weight,
                    self.mask_tokens.weight,
                ],
                dim=0,
            )
            s = 1
        else:
            output_tokens = torch.cat(
                [self.iou_token.weight, self.mask_tokens.weight], dim=0
            )
        output_tokens = output_tokens.unsqueeze(0).expand(
            sparse_prompt_embeddings.size(0), -1, -1
        )
        tokens = torch.cat((output_tokens, sparse_prompt_embeddings), dim=1)

        # Expand per-image data in batch direction to be per-mask
        if repeat_image:
            src = torch.repeat_interleave(image_embeddings, tokens.shape[0], dim=0)
        else:
            assert image_embeddings.shape[0] == tokens.shape[0]
            src = image_embeddings
        src = src + dense_prompt_embeddings
        assert image_pe.size(0) == 1, (
            "image_pe should have size 1 in batch dim (from `get_dense_pe()`)"
        )
        pos_src = torch.repeat_interleave(image_pe, tokens.shape[0], dim=0)
        b, c, h, w = src.shape

        # Run the transformer
        hs, src = self.transformer(src, pos_src, tokens)
        iou_token_out = hs[:, s, :]
        mask_tokens_out = hs[:, s + 1 : (s + 1 + self.num_mask_tokens), :]

        # Upscale mask embeddings and predict masks using the mask tokens
        src = src.transpose(1, 2).view(b, c, h, w)
        if not self.use_high_res_features:
            upscaled_embedding = self.output_upscaling(src)
        else:
            dc1, ln1, act1, dc2, act2 = self.output_upscaling
            feat_s0, feat_s1 = high_res_features
            upscaled_embedding = act1(ln1(dc1(src) + feat_s1))
            upscaled_embedding = act2(dc2(upscaled_embedding) + feat_s0)

        hyper_in_list: List[torch.Tensor] = []
        for i in range(self.num_mask_tokens):
            hyper_in_list.append(
                self.output_hypernetworks_mlps[i](mask_tokens_out[:, i, :])
            )
        hyper_in = torch.stack(hyper_in_list, dim=1)
        b, c, h, w = upscaled_embedding.shape
        masks = (hyper_in @ upscaled_embedding.view(b, c, h * w)).view(b, -1, h, w)

        # Generate mask quality predictions
        iou_pred = self.iou_prediction_head(iou_token_out)
        if self.pred_obj_scores:
            assert s == 1
            object_score_logits = self.pred_obj_score_head(hs[:, 0, :])
        else:
            # Obj scores logits - default to 10.0, i.e. assuming the object is present, sigmoid(10)=1
            object_score_logits = 10.0 * iou_pred.new_ones(iou_pred.shape[0], 1)

        return masks, iou_pred, mask_tokens_out, object_score_logits

    def _get_stability_scores(self, mask_logits):
        """
        Compute stability scores of the mask logits based on the IoU between upper and
        lower thresholds.
        """
        mask_logits = mask_logits.flatten(-2)
        stability_delta = self.dynamic_multimask_stability_delta
        area_i = torch.sum(mask_logits > stability_delta, dim=-1).float()
        area_u = torch.sum(mask_logits > -stability_delta, dim=-1).float()
        stability_scores = torch.where(area_u > 0, area_i / area_u, 1.0)
        return stability_scores

    def _dynamic_multimask_via_stability(self, all_mask_logits, all_iou_scores):
        """
        When outputting a single mask, if the stability score from the current single-mask
        output (based on output token 0) falls below a threshold, we instead select from
        multi-mask outputs (based on output token 1~3) the mask with the highest predicted
        IoU score. This is intended to ensure a valid mask for both clicking and tracking.
        """
        # The best mask from multimask output tokens (1~3)
        multimask_logits = all_mask_logits[:, 1:, :, :]
        multimask_iou_scores = all_iou_scores[:, 1:]
        best_scores_inds = torch.argmax(multimask_iou_scores, dim=-1)
        batch_inds = torch.arange(
            multimask_iou_scores.size(0), device=all_iou_scores.device
        )
        best_multimask_logits = multimask_logits[batch_inds, best_scores_inds]
        best_multimask_logits = best_multimask_logits.unsqueeze(1)
        best_multimask_iou_scores = multimask_iou_scores[batch_inds, best_scores_inds]
        best_multimask_iou_scores = best_multimask_iou_scores.unsqueeze(1)

        # The mask from singlemask output token 0 and its stability score
        singlemask_logits = all_mask_logits[:, 0:1, :, :]
        singlemask_iou_scores = all_iou_scores[:, 0:1]
        stability_scores = self._get_stability_scores(singlemask_logits)
        is_stable = stability_scores >= self.dynamic_multimask_stability_thresh

        # Dynamically fall back to best multimask output upon low stability scores.
        mask_logits_out = torch.where(
            is_stable[..., None, None].expand_as(singlemask_logits),
            singlemask_logits,
            best_multimask_logits,
        )
        iou_scores_out = torch.where(
            is_stable.expand_as(singlemask_iou_scores),
            singlemask_iou_scores,
            best_multimask_iou_scores,
        )
        return mask_logits_out, iou_scores_out


# Lightly adapted from
# https://github.com/facebookresearch/MaskFormer/blob/main/mask_former/modeling/transformer/transformer_predictor.py # noqa
class MLP(nn.Module):
    def __init__(
        self,
        input_dim: int,
        hidden_dim: int,
        output_dim: int,
        num_layers: int,
        sigmoid_output: bool = False,
    ) -> None:
        super().__init__()
        self.num_layers = num_layers
        h = [hidden_dim] * (num_layers - 1)
        self.layers = nn.ModuleList(
            nn.Linear(n, k) for n, k in zip([input_dim] + h, h + [output_dim])
        )
        self.sigmoid_output = sigmoid_output

    def forward(self, x):
        for i, layer in enumerate(self.layers):
            x = F.relu(layer(x)) if i < self.num_layers - 1 else layer(x)
        if self.sigmoid_output:
            x = F.sigmoid(x)
        return x



================================================
FILE: sam3/sam/prompt_encoder.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

from typing import Any, Optional, Tuple, Type

import numpy as np
import torch
from torch import nn

from .common import LayerNorm2d


class PromptEncoder(nn.Module):
    def __init__(
        self,
        embed_dim: int,
        image_embedding_size: Tuple[int, int],
        input_image_size: Tuple[int, int],
        mask_in_chans: int,
        activation: Type[nn.Module] = nn.GELU,
    ) -> None:
        """
        Encodes prompts for input to SAM's mask decoder.

        Arguments:
          embed_dim (int): The prompts' embedding dimension
          image_embedding_size (tuple(int, int)): The spatial size of the
            image embedding, as (H, W).
          input_image_size (int): The padded size of the image as input
            to the image encoder, as (H, W).
          mask_in_chans (int): The number of hidden channels used for
            encoding input masks.
          activation (nn.Module): The activation to use when encoding
            input masks.
        """
        super().__init__()
        self.embed_dim = embed_dim
        self.input_image_size = input_image_size
        self.image_embedding_size = image_embedding_size
        self.pe_layer = PositionEmbeddingRandom(embed_dim // 2)

        self.num_point_embeddings: int = 4  # pos/neg point + 2 box corners
        point_embeddings = [
            nn.Embedding(1, embed_dim) for i in range(self.num_point_embeddings)
        ]
        self.point_embeddings = nn.ModuleList(point_embeddings)
        self.not_a_point_embed = nn.Embedding(1, embed_dim)

        self.mask_input_size = (
            4 * image_embedding_size[0],
            4 * image_embedding_size[1],
        )
        self.mask_downscaling = nn.Sequential(
            nn.Conv2d(1, mask_in_chans // 4, kernel_size=2, stride=2),
            LayerNorm2d(mask_in_chans // 4),
            activation(),
            nn.Conv2d(mask_in_chans // 4, mask_in_chans, kernel_size=2, stride=2),
            LayerNorm2d(mask_in_chans),
            activation(),
            nn.Conv2d(mask_in_chans, embed_dim, kernel_size=1),
        )
        self.no_mask_embed = nn.Embedding(1, embed_dim)

    def get_dense_pe(self) -> torch.Tensor:
        """
        Returns the positional encoding used to encode point prompts,
        applied to a dense set of points the shape of the image encoding.

        Returns:
          torch.Tensor: Positional encoding with shape
            1x(embed_dim)x(embedding_h)x(embedding_w)
        """
        return self.pe_layer(self.image_embedding_size).unsqueeze(0)

    def _embed_points(
        self,
        points: torch.Tensor,
        labels: torch.Tensor,
        pad: bool,
    ) -> torch.Tensor:
        """Embeds point prompts."""
        points = points + 0.5  # Shift to center of pixel
        if pad:
            padding_point = torch.zeros((points.shape[0], 1, 2), device=points.device)
            padding_label = -torch.ones((labels.shape[0], 1), device=labels.device)
            points = torch.cat([points, padding_point], dim=1)
            labels = torch.cat([labels, padding_label], dim=1)
        point_embedding = self.pe_layer.forward_with_coords(
            points, self.input_image_size
        )

        point_embedding = torch.where(
            (labels == -1).unsqueeze(-1),
            torch.zeros_like(point_embedding) + self.not_a_point_embed.weight,
            point_embedding,
        )
        point_embedding = torch.where(
            (labels == 0).unsqueeze(-1),
            point_embedding + self.point_embeddings[0].weight,
            point_embedding,
        )
        point_embedding = torch.where(
            (labels == 1).unsqueeze(-1),
            point_embedding + self.point_embeddings[1].weight,
            point_embedding,
        )
        point_embedding = torch.where(
            (labels == 2).unsqueeze(-1),
            point_embedding + self.point_embeddings[2].weight,
            point_embedding,
        )
        point_embedding = torch.where(
            (labels == 3).unsqueeze(-1),
            point_embedding + self.point_embeddings[3].weight,
            point_embedding,
        )
        return point_embedding

    def _embed_boxes(self, boxes: torch.Tensor) -> torch.Tensor:
        """Embeds box prompts."""
        boxes = boxes + 0.5  # Shift to center of pixel
        coords = boxes.reshape(-1, 2, 2)
        corner_embedding = self.pe_layer.forward_with_coords(
            coords, self.input_image_size
        )
        corner_embedding[:, 0, :] += self.point_embeddings[2].weight
        corner_embedding[:, 1, :] += self.point_embeddings[3].weight
        return corner_embedding

    def _embed_masks(self, masks: torch.Tensor) -> torch.Tensor:
        """Embeds mask inputs."""
        mask_embedding = self.mask_downscaling(masks)
        return mask_embedding

    def _get_batch_size(
        self,
        points: Optional[Tuple[torch.Tensor, torch.Tensor]],
        boxes: Optional[torch.Tensor],
        masks: Optional[torch.Tensor],
    ) -> int:
        """
        Gets the batch size of the output given the batch size of the input prompts.
        """
        if points is not None:
            return points[0].shape[0]
        elif boxes is not None:
            return boxes.shape[0]
        elif masks is not None:
            return masks.shape[0]
        else:
            return 1

    def _get_device(self) -> torch.device:
        return self.point_embeddings[0].weight.device

    def forward(
        self,
        points: Optional[Tuple[torch.Tensor, torch.Tensor]],
        boxes: Optional[torch.Tensor],
        masks: Optional[torch.Tensor],
    ) -> Tuple[torch.Tensor, torch.Tensor]:
        """
        Embeds different types of prompts, returning both sparse and dense
        embeddings.

        Arguments:
          points (tuple(torch.Tensor, torch.Tensor) or none): point coordinates
            and labels to embed.
          boxes (torch.Tensor or none): boxes to embed
          masks (torch.Tensor or none): masks to embed

        Returns:
          torch.Tensor: sparse embeddings for the points and boxes, with shape
            BxNx(embed_dim), where N is determined by the number of input points
            and boxes.
          torch.Tensor: dense embeddings for the masks, in the shape
            Bx(embed_dim)x(embed_H)x(embed_W)
        """
        bs = self._get_batch_size(points, boxes, masks)
        sparse_embeddings = torch.empty(
            (bs, 0, self.embed_dim), device=self._get_device()
        )
        if points is not None:
            coords, labels = points
            point_embeddings = self._embed_points(coords, labels, pad=(boxes is None))
            sparse_embeddings = torch.cat([sparse_embeddings, point_embeddings], dim=1)
        if boxes is not None:
            box_embeddings = self._embed_boxes(boxes)
            sparse_embeddings = torch.cat([sparse_embeddings, box_embeddings], dim=1)

        if masks is not None:
            dense_embeddings = self._embed_masks(masks)
        else:
            dense_embeddings = self.no_mask_embed.weight.reshape(1, -1, 1, 1).expand(
                bs, -1, self.image_embedding_size[0], self.image_embedding_size[1]
            )

        return sparse_embeddings, dense_embeddings


class PositionEmbeddingRandom(nn.Module):
    """
    Positional encoding using random spatial frequencies.
    """

    def __init__(self, num_pos_feats: int = 64, scale: Optional[float] = None) -> None:
        super().__init__()
        if scale is None or scale <= 0.0:
            scale = 1.0
        self.register_buffer(
            "positional_encoding_gaussian_matrix",
            scale * torch.randn((2, num_pos_feats)),
        )

    def _pe_encoding(self, coords: torch.Tensor) -> torch.Tensor:
        """Positionally encode points that are normalized to [0,1]."""
        # assuming coords are in [0, 1]^2 square and have d_1 x ... x d_n x 2 shape
        coords = 2 * coords - 1
        coords = coords @ self.positional_encoding_gaussian_matrix
        coords = 2 * np.pi * coords
        # outputs d_1 x ... x d_n x C shape
        return torch.cat([torch.sin(coords), torch.cos(coords)], dim=-1)

    def forward(self, size: Tuple[int, int]) -> torch.Tensor:
        """Generate positional encoding for a grid of the specified size."""
        h, w = size
        device: Any = self.positional_encoding_gaussian_matrix.device
        grid = torch.ones((h, w), device=device, dtype=torch.float32)
        y_embed = grid.cumsum(dim=0) - 0.5
        x_embed = grid.cumsum(dim=1) - 0.5
        y_embed = y_embed / h
        x_embed = x_embed / w

        pe = self._pe_encoding(torch.stack([x_embed, y_embed], dim=-1))
        return pe.permute(2, 0, 1)  # C x H x W

    def forward_with_coords(
        self, coords_input: torch.Tensor, image_size: Tuple[int, int]
    ) -> torch.Tensor:
        """Positionally encode points that are not normalized to [0,1]."""
        coords = coords_input.clone()
        coords[:, :, 0] = coords[:, :, 0] / image_size[1]
        coords[:, :, 1] = coords[:, :, 1] / image_size[0]
        return self._pe_encoding(coords.to(torch.float))  # B x N x C



================================================
FILE: sam3/sam/rope.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

"""
Adapted from:
1. https://github.com/meta-llama/codellama/blob/main/llama/model.py
2. https://github.com/naver-ai/rope-vit
3. https://github.com/lucidrains/rotary-embedding-torch
"""

from typing import Optional

import torch
from einops import rearrange, repeat
from torch import broadcast_tensors, nn


def init_t_xy(end_x: int, end_y: int, scale: float = 1.0, offset: int = 0, device=None):
    t = torch.arange(end_x * end_y, dtype=torch.float32, device=device)
    t_x = (t % end_x).float()
    t_y = torch.div(t, end_x, rounding_mode="floor").float()
    return t_x * scale + offset, t_y * scale + offset


def compute_axial_cis(
    dim: int,
    end_x: int,
    end_y: int,
    theta: float = 10000.0,
    scale_pos: float = 1.0,
    offset: int = 0,
    device=None,
):
    freqs_x = 1.0 / (
        theta ** (torch.arange(0, dim, 4, device=device)[: (dim // 4)].float() / dim)
    )
    freqs_y = 1.0 / (
        theta ** (torch.arange(0, dim, 4, device=device)[: (dim // 4)].float() / dim)
    )

    t_x, t_y = init_t_xy(end_x, end_y, scale_pos, offset, device=device)
    freqs_x = torch.outer(t_x, freqs_x)
    freqs_y = torch.outer(t_y, freqs_y)
    freqs_cis_x = torch.polar(torch.ones_like(freqs_x), freqs_x)
    freqs_cis_y = torch.polar(torch.ones_like(freqs_y), freqs_y)
    return torch.cat([freqs_cis_x, freqs_cis_y], dim=-1)


def reshape_for_broadcast(freqs_cis: torch.Tensor, x: torch.Tensor):
    ndim = x.ndim
    assert 0 <= 1 < ndim
    assert freqs_cis.shape == (x.shape[-2], x.shape[-1])
    shape = [d if i >= ndim - 2 else 1 for i, d in enumerate(x.shape)]
    return freqs_cis.view(*shape)


def apply_rotary_enc(
    xq: torch.Tensor,
    xk: torch.Tensor,
    freqs_cis: torch.Tensor,
    repeat_freqs_k: bool = False,
):
    xq_ = torch.view_as_complex(xq.float().reshape(*xq.shape[:-1], -1, 2))
    xk_ = (
        torch.view_as_complex(xk.float().reshape(*xk.shape[:-1], -1, 2))
        if xk.shape[-2] != 0
        else None
    )
    freqs_cis = reshape_for_broadcast(freqs_cis, xq_)
    xq_out = torch.view_as_real(xq_ * freqs_cis).flatten(3)
    if xk_ is None:
        # no keys to rotate, due to dropout
        return xq_out.type_as(xq).to(xq.device), xk
    # repeat freqs along seq_len dim to match k seq_len
    if repeat_freqs_k:
        r = xk_.shape[-2] // xq_.shape[-2]
        freqs_cis = freqs_cis.repeat(*([1] * (freqs_cis.ndim - 2)), r, 1)
    xk_out = torch.view_as_real(xk_ * freqs_cis).flatten(3)
    return xq_out.type_as(xq).to(xq.device), xk_out.type_as(xk).to(xk.device)


def complex_mult(xq_real, xq_imag, freqs_cis_real, freqs_cis_imag):
    # Compute the real part of the product
    real_part = xq_real * freqs_cis_real - xq_imag * freqs_cis_imag
    # Compute the imaginary part of the product
    imag_part = xq_real * freqs_cis_imag + xq_imag * freqs_cis_real
    # Stack the real and imaginary parts along the last dimension
    return torch.stack([real_part, imag_part], dim=-1)


def apply_rotary_enc_real(
    xq: torch.Tensor,
    xk: torch.Tensor,
    freqs_cis_real: torch.Tensor,
    freqs_cis_imag: torch.Tensor,
    repeat_freqs_k: bool = False,
):
    assert xk is not None
    assert xk.shape[-2] != 0

    xq_real = xq.float().reshape(*xq.shape[:-1], -1, 2)[..., 0]
    xq_imag = xq.float().reshape(*xq.shape[:-1], -1, 2)[..., 1]
    xk_real = xk.float().reshape(*xk.shape[:-1], -1, 2)[..., 0]
    xk_imag = xk.float().reshape(*xk.shape[:-1], -1, 2)[..., 1]
    freqs_cis_real = reshape_for_broadcast(freqs_cis_real, xq_real)
    freqs_cis_imag = reshape_for_broadcast(freqs_cis_imag, xq_imag)
    xq_out = complex_mult(xq_real, xq_imag, freqs_cis_real, freqs_cis_imag).flatten(3)
    if repeat_freqs_k:
        r = xk_real.shape[-2] // xq_real.shape[-2]
        freqs_cis_real = freqs_cis_real.repeat(*([1] * (freqs_cis_real.ndim - 2)), r, 1)
        freqs_cis_imag = freqs_cis_imag.repeat(*([1] * (freqs_cis_imag.ndim - 2)), r, 1)
    xk_out = complex_mult(xk_real, xk_imag, freqs_cis_real, freqs_cis_imag).flatten(3)
    # xq_out = torch.view_as_real(torch.complex(xq_real, xq_imag) * torch.complex(freqs_cis_real, freqs_cis_imag)).flatten(3)
    # xk_out = torch.view_as_real(torch.compelx(xk_real, xk_imag) * torch.complex(freqs_cis_real, freqs_cis_imag)).flatten(3)
    return xq_out.type_as(xq).to(xq.device), xk_out.type_as(xk).to(xk.device)


# rotary embedding helper functions
def broadcat(tensors, dim=-1):
    broadcasted_tensors = broadcast_tensors(*tensors)
    return torch.cat(broadcasted_tensors, dim=dim)


def rotate_half(x: torch.Tensor):
    x = rearrange(x, "... (d r) -> ... d r", r=2)
    x1, x2 = x.unbind(dim=-1)
    x = torch.stack((-x2, x1), dim=-1)
    return rearrange(x, "... d r -> ... (d r)")


class VisionRotaryEmbeddingVE(nn.Module):
    def __init__(
        self,
        dim: int,
        seq_len: int,
        pt_seq_len: Optional[int] = None,
        theta: float = 10000.0,
        offset: int = 1,  # specific to VE
    ):
        super().__init__()

        freqs = 1.0 / (theta ** (torch.arange(0, dim, 2)[: (dim // 2)].float() / dim))
        scale = 1.0
        if pt_seq_len is not None:
            scale = pt_seq_len / seq_len

        # offset of +1 following VE - even though for the
        # attention op only differences matter
        t = torch.arange(seq_len) * scale + offset

        freqs = torch.einsum("..., f -> ... f", t, freqs)
        freqs = repeat(freqs, "... n -> ... (n r)", r=2)

        freqs = broadcat((freqs[None, :, :], freqs[:, None, :]), dim=-1)
        freqs_cos = freqs.cos().view(-1, freqs.shape[-1])
        freqs_sin = freqs.sin().view(-1, freqs.shape[-1])

        self.register_buffer("freqs_cos", freqs_cos)
        self.register_buffer("freqs_sin", freqs_sin)

    def forward(self, t: torch.Tensor):
        return t * self.freqs_cos + rotate_half(t) * self.freqs_sin



================================================
FILE: sam3/sam/transformer.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

import math
from functools import partial
from typing import Tuple, Type

import torch
import torch.nn.functional as F
from sam3.sam.rope import apply_rotary_enc, apply_rotary_enc_real, compute_axial_cis
from torch import nn, Tensor

from .common import MLPBlock


class TwoWayTransformer(nn.Module):
    def __init__(
        self,
        depth: int,
        embedding_dim: int,
        num_heads: int,
        mlp_dim: int,
        activation: Type[nn.Module] = nn.ReLU,
        attention_downsample_rate: int = 2,
    ) -> None:
        """
        A transformer decoder that attends to an input image using
        queries whose positional embedding is supplied.

        Args:
          depth (int): number of layers in the transformer
          embedding_dim (int): the channel dimension for the input embeddings
          num_heads (int): the number of heads for multihead attention. Must
            divide embedding_dim
          mlp_dim (int): the channel dimension internal to the MLP block
          activation (nn.Module): the activation to use in the MLP block
        """
        super().__init__()
        self.depth = depth
        self.embedding_dim = embedding_dim
        self.num_heads = num_heads
        self.mlp_dim = mlp_dim
        self.layers = nn.ModuleList()

        for i in range(depth):
            self.layers.append(
                TwoWayAttentionBlock(
                    embedding_dim=embedding_dim,
                    num_heads=num_heads,
                    mlp_dim=mlp_dim,
                    activation=activation,
                    attention_downsample_rate=attention_downsample_rate,
                    skip_first_layer_pe=(i == 0),
                )
            )

        self.final_attn_token_to_image = Attention(
            embedding_dim, num_heads, downsample_rate=attention_downsample_rate
        )
        self.norm_final_attn = nn.LayerNorm(embedding_dim)

    def forward(
        self,
        image_embedding: Tensor,
        image_pe: Tensor,
        point_embedding: Tensor,
    ) -> Tuple[Tensor, Tensor]:
        """
        Args:
          image_embedding (torch.Tensor): image to attend to. Should be shape
            B x embedding_dim x h x w for any h and w.
          image_pe (torch.Tensor): the positional encoding to add to the image. Must
            have the same shape as image_embedding.
          point_embedding (torch.Tensor): the embedding to add to the query points.
            Must have shape B x N_points x embedding_dim for any N_points.

        Returns:
          torch.Tensor: the processed point_embedding
          torch.Tensor: the processed image_embedding
        """
        # BxCxHxW -> BxHWxC == B x N_image_tokens x C
        bs, c, h, w = image_embedding.shape
        image_embedding = image_embedding.flatten(2).permute(0, 2, 1)
        image_pe = image_pe.flatten(2).permute(0, 2, 1)

        # Prepare queries
        queries = point_embedding
        keys = image_embedding

        # Apply transformer blocks and final layernorm
        for layer in self.layers:
            queries, keys = layer(
                queries=queries,
                keys=keys,
                query_pe=point_embedding,
                key_pe=image_pe,
            )

        # Apply the final attention layer from the points to the image
        q = queries + point_embedding
        k = keys + image_pe
        attn_out = self.final_attn_token_to_image(q=q, k=k, v=keys)
        queries = queries + attn_out
        queries = self.norm_final_attn(queries)

        return queries, keys


class TwoWayAttentionBlock(nn.Module):
    def __init__(
        self,
        embedding_dim: int,
        num_heads: int,
        mlp_dim: int = 2048,
        activation: Type[nn.Module] = nn.ReLU,
        attention_downsample_rate: int = 2,
        skip_first_layer_pe: bool = False,
    ) -> None:
        """
        A transformer block with four layers: (1) self-attention of sparse
        inputs, (2) cross attention of sparse inputs to dense inputs, (3) mlp
        block on sparse inputs, and (4) cross attention of dense inputs to sparse
        inputs.

        Arguments:
          embedding_dim (int): the channel dimension of the embeddings
          num_heads (int): the number of heads in the attention layers
          mlp_dim (int): the hidden dimension of the mlp block
          activation (nn.Module): the activation of the mlp block
          skip_first_layer_pe (bool): skip the PE on the first layer
        """
        super().__init__()
        self.self_attn = Attention(embedding_dim, num_heads)
        self.norm1 = nn.LayerNorm(embedding_dim)

        self.cross_attn_token_to_image = Attention(
            embedding_dim, num_heads, downsample_rate=attention_downsample_rate
        )
        self.norm2 = nn.LayerNorm(embedding_dim)

        self.mlp = MLPBlock(embedding_dim, mlp_dim, activation)
        self.norm3 = nn.LayerNorm(embedding_dim)

        self.norm4 = nn.LayerNorm(embedding_dim)
        self.cross_attn_image_to_token = Attention(
            embedding_dim, num_heads, downsample_rate=attention_downsample_rate
        )

        self.skip_first_layer_pe = skip_first_layer_pe

    def forward(
        self, queries: Tensor, keys: Tensor, query_pe: Tensor, key_pe: Tensor
    ) -> Tuple[Tensor, Tensor]:
        # Self attention block
        if self.skip_first_layer_pe:
            queries = self.self_attn(q=queries, k=queries, v=queries)
        else:
            q = queries + query_pe
            attn_out = self.self_attn(q=q, k=q, v=queries)
            queries = queries + attn_out
        queries = self.norm1(queries)

        # Cross attention block, tokens attending to image embedding
        q = queries + query_pe
        k = keys + key_pe
        attn_out = self.cross_attn_token_to_image(q=q, k=k, v=keys)
        queries = queries + attn_out
        queries = self.norm2(queries)

        # MLP block
        mlp_out = self.mlp(queries)
        queries = queries + mlp_out
        queries = self.norm3(queries)

        # Cross attention block, image embedding attending to tokens
        q = queries + query_pe
        k = keys + key_pe
        attn_out = self.cross_attn_image_to_token(q=k, k=q, v=queries)
        keys = keys + attn_out
        keys = self.norm4(keys)

        return queries, keys


class Attention(nn.Module):
    """
    An attention layer that allows for downscaling the size of the embedding
    after projection to queries, keys, and values.
    """

    def __init__(
        self,
        embedding_dim: int,
        num_heads: int,
        downsample_rate: int = 1,
        dropout: float = 0.0,
        kv_in_dim: int = None,
        use_fa3: bool = False,
    ) -> None:
        super().__init__()
        self.embedding_dim = embedding_dim
        self.kv_in_dim = kv_in_dim if kv_in_dim is not None else embedding_dim
        self.internal_dim = embedding_dim // downsample_rate
        self.num_heads = num_heads
        self.use_fa3 = use_fa3
        assert self.internal_dim % num_heads == 0, (
            "num_heads must divide embedding_dim."
        )

        self.q_proj = nn.Linear(embedding_dim, self.internal_dim)
        self.k_proj = nn.Linear(self.kv_in_dim, self.internal_dim)
        self.v_proj = nn.Linear(self.kv_in_dim, self.internal_dim)
        self.out_proj = nn.Linear(self.internal_dim, embedding_dim)

        self.dropout_p = dropout

    def _separate_heads(self, x: Tensor, num_heads: int) -> Tensor:
        b, n, c = x.shape
        x = x.reshape(b, n, num_heads, c // num_heads)
        return x.transpose(1, 2)  # B x N_heads x N_tokens x C_per_head

    def _recombine_heads(self, x: Tensor) -> Tensor:
        b, n_heads, n_tokens, c_per_head = x.shape
        x = x.transpose(1, 2)
        return x.reshape(b, n_tokens, n_heads * c_per_head)  # B x N_tokens x C

    def forward(self, q: Tensor, k: Tensor, v: Tensor) -> Tensor:
        # Input projections
        q = self.q_proj(q)
        k = self.k_proj(k)
        v = self.v_proj(v)

        # Separate into heads
        q = self._separate_heads(q, self.num_heads)
        k = self._separate_heads(k, self.num_heads)
        v = self._separate_heads(v, self.num_heads)

        dropout_p = self.dropout_p if self.training else 0.0
        # Attention
        # with torch.backends.cuda.sdp_kernel(
        #     enable_flash=USE_FLASH_ATTN,
        #     # if Flash attention kernel is off, then math kernel needs to be enabled
        #     enable_math=(OLD_GPU and dropout_p > 0.0) or MATH_KERNEL_ON,
        #     enable_mem_efficient=OLD_GPU,
        # ):
        # Let's trust the dispatcher....
        if self.use_fa3:
            from sam3.perflib.fa3 import flash_attn_func

            assert dropout_p == 0.0
            out = flash_attn_func(
                q.transpose(1, 2), k.transpose(1, 2), v.transpose(1, 2)
            ).transpose(1, 2)
        else:
            torch.backends.cuda.enable_flash_sdp(True)
            torch.backends.cuda.enable_math_sdp(True)
            torch.backends.cuda.enable_mem_efficient_sdp(True)
            out = F.scaled_dot_product_attention(q, k, v, dropout_p=dropout_p)

        out = self._recombine_heads(out)
        out = self.out_proj(out)

        return out


class RoPEAttention(Attention):
    """Attention with rotary position encoding."""

    def __init__(
        self,
        *args,
        rope_theta=10000.0,
        # whether to repeat q rope to match k length
        # this is needed for cross-attention to memories
        rope_k_repeat=False,
        feat_sizes=(64, 64),  # [w, h] for stride 16 feats at 1024 resolution
        use_rope_real=False,
        **kwargs,
    ):
        super().__init__(*args, **kwargs)
        self.use_rope_real = use_rope_real
        self.compute_cis = partial(
            compute_axial_cis, dim=self.internal_dim // self.num_heads, theta=rope_theta
        )
        device = torch.device("cuda") if torch.cuda.is_available() else None
        self.freqs_cis = self.compute_cis(
            end_x=feat_sizes[0], end_y=feat_sizes[1], device=device
        )
        if self.use_rope_real:
            self.freqs_cis_real = self.freqs_cis.real
            self.freqs_cis_imag = self.freqs_cis.imag
        self.rope_k_repeat = rope_k_repeat

    def forward(
        self, q: Tensor, k: Tensor, v: Tensor, num_k_exclude_rope: int = 0
    ) -> Tensor:
        # Input projections
        q = self.q_proj(q)
        k = self.k_proj(k)
        v = self.v_proj(v)

        # Separate into heads
        q = self._separate_heads(q, self.num_heads)
        k = self._separate_heads(k, self.num_heads)
        v = self._separate_heads(v, self.num_heads)

        # Apply rotary position encoding
        w = h = math.sqrt(q.shape[-2])
        if self.freqs_cis.shape[0] != q.shape[-2]:
            self.freqs_cis = self.compute_cis(end_x=w, end_y=h, device=q.device)
            self.freqs_cis_real = self.freqs_cis.real
            self.freqs_cis_imag = self.freqs_cis.imag
        if q.shape[-2] != k.shape[-2]:
            assert self.rope_k_repeat

        num_k_rope = k.size(-2) - num_k_exclude_rope
        if self.use_rope_real:
            q, k[:, :, :num_k_rope] = apply_rotary_enc_real(
                q,
                k[:, :, :num_k_rope],
                freqs_cis_real=self.freqs_cis_real,
                freqs_cis_imag=self.freqs_cis_imag,
                repeat_freqs_k=self.rope_k_repeat,
            )
        else:
            q, k[:, :, :num_k_rope] = apply_rotary_enc(
                q,
                k[:, :, :num_k_rope],
                self.freqs_cis,
                repeat_freqs_k=self.rope_k_repeat,
            )

        dropout_p = self.dropout_p if self.training else 0.0
        # Attention
        # with torch.backends.cuda.sdp_kernel(
        #     enable_flash=USE_FLASH_ATTN,
        #     # if Flash attention kernel is off, then math kernel needs to be enabled
        #     enable_math=(OLD_GPU and dropout_p > 0.0) or MATH_KERNEL_ON,
        #     enable_mem_efficient=OLD_GPU,
        # ):
        # Let's trust the dispatcher....
        if self.use_fa3:
            from sam3.perflib.fa3 import flash_attn_func

            assert dropout_p == 0.0
            out = flash_attn_func(
                q.transpose(1, 2), k.transpose(1, 2), v.transpose(1, 2)
            ).transpose(1, 2)
        else:
            torch.backends.cuda.enable_flash_sdp(True)
            torch.backends.cuda.enable_math_sdp(True)
            torch.backends.cuda.enable_mem_efficient_sdp(True)
            out = F.scaled_dot_product_attention(q, k, v, dropout_p=dropout_p)

        out = self._recombine_heads(out)
        out = self.out_proj(out)

        return out



================================================
FILE: scripts/measure_speed.py
================================================
"""
SAM3 Speed Test — supports both SAM3 and SAM3.1 (multiplex).

Generates synthetic video with moving circles, runs text-prompt detection
+ propagation, and measures FPS. Checkpoints are auto-downloaded from
HuggingFace if not provided.

Usage:
  # SAM 3.1 (default, auto-downloads from HuggingFace):
  python scripts/measure_speed.py

  # SAM 3 (non-multiplex):
  python scripts/measure_speed.py --version sam3

  # Custom settings:
  python scripts/measure_speed.py --num_objects 32 --n_frames 100 --no-compile
  python scripts/measure_speed.py --version sam3.1 --compile --num_objects 5
"""

import argparse
import getpass
import os
import shutil
import time

import numpy as np
import torch
from PIL import Image, ImageDraw


def max_memory_allocated():
    max_memory_allocated_bytes = torch.cuda.max_memory_allocated()
    _, total_memory = torch.cuda.mem_get_info()
    max_memory_allocated_percentage = int(
        100 * (max_memory_allocated_bytes / total_memory)
    )
    max_memory_allocated_bytes = max_memory_allocated_bytes >> 20
    print(
        f"max_memory_allocated_bytes: {max_memory_allocated_bytes}MiB or {max_memory_allocated_percentage}%"
    )


def synthesize_video_data(
    num_objects: int,
    out_dir: str,
    radius: int,
    speed: int,
    width: int,
    height: int,
    n_frames: int,
):
    circle_colors = [
        tuple(np.random.randint(0, 256, size=3).tolist()) for _ in range(num_objects)
    ]

    if os.path.exists(out_dir):
        shutil.rmtree(out_dir)
    os.makedirs(out_dir, exist_ok=True)

    positions = []
    velocities = []
    for _ in range(num_objects):
        px = float(np.random.randint(radius, width - radius))
        py = float(np.random.randint(radius, height - radius))
        vx = np.random.choice([-1, 1]) * speed
        vy = np.random.choice([-1, 1]) * speed
        positions.append([px, py])
        velocities.append([vx, vy])

    print(f"Generate {n_frames} frames with {num_objects} objects")
    for i in range(n_frames):
        img = Image.new("RGB", (width, height), (0, 0, 0))
        draw = ImageDraw.Draw(img)
        for obj_idx in range(num_objects):
            x, y = positions[obj_idx]
            rx, ry = round(x), round(y)
            draw.ellipse(
                [(rx - radius, ry - radius), (rx + radius, ry + radius)],
                fill=circle_colors[obj_idx],
            )
            vx, vy = velocities[obj_idx]
            x += vx
            y += vy
            positions[obj_idx] = [
                np.clip(x, radius, width - radius),
                np.clip(y, radius, height - radius),
            ]
            if x - radius < 0 or x + radius > width:
                vx *= -1
            if y - radius < 0 or y + radius > height:
                vy *= -1
            velocities[obj_idx] = [vx, vy]

        img.save(os.path.join(out_dir, f"{i:03d}.jpg"))


def profiler_runner(fn, profile_save_dir=None, profile_end_frame=-1, *args, **kwargs):
    if profile_save_dir is None:
        profile_save_dir = os.path.expanduser("~/traces")

    os.environ["ENABLE_PROFILING"] = "1"
    os.environ["PROFILE_SAVE_DIR"] = profile_save_dir
    if profile_end_frame >= 0:
        os.environ["PROFILE_END_FRAME"] = str(profile_end_frame)

    print(f"Profiling enabled. Traces will be saved to: {profile_save_dir}")
    if profile_end_frame >= 0:
        print(f"Profiling will stop at frame: {profile_end_frame}")

    try:
        result = fn(*args, **kwargs)
    finally:
        os.environ.pop("ENABLE_PROFILING", None)
        os.environ.pop("PROFILE_SAVE_DIR", None)
        os.environ.pop("PROFILE_END_FRAME", None)

    return result


def main_loop(model_wrapper, session_id, text_prompt):
    model_wrapper.handle_request({"type": "reset_session", "session_id": session_id})
    model_wrapper.handle_request(
        {
            "type": "add_prompt",
            "session_id": session_id,
            "frame_index": 0,
            "text": text_prompt,
        }
    )

    t0 = time.perf_counter()
    frame_count = 0
    for _response in model_wrapper.handle_stream_request(
        {"type": "propagate_in_video", "session_id": session_id}
    ):
        frame_count += 1
    torch.cuda.synchronize()
    t1 = time.perf_counter()

    if frame_count > 0:
        return frame_count / (t1 - t0)
    return -1


def run_test(
    version: str,
    profile: bool,
    video_dir: str,
    num_objects: int,
    radius: int,
    speed: int,
    width: int,
    height: int,
    n_frames: int,
    synthesize_data: bool = True,
    profile_save_dir: str = None,
    profile_end_frame: int = -1,
    do_compile: bool = True,
    checkpoint_path: str = None,
) -> float:
    torch.autocast(device_type="cuda", dtype=torch.bfloat16).__enter__()

    if synthesize_data:
        synthesize_video_data(
            num_objects=num_objects,
            out_dir=video_dir,
            radius=radius,
            speed=speed,
            width=width,
            height=height,
            n_frames=n_frames,
        )

    from sam3 import build_sam3_predictor

    print(f"Building {version} model...")
    build_kwargs = dict(
        version=version,
        compile=do_compile,
        async_loading_frames=False,
    )
    if checkpoint_path:
        build_kwargs["checkpoint_path"] = checkpoint_path
    if version == "sam3.1":
        build_kwargs["warm_up"] = do_compile
        build_kwargs["max_num_objects"] = num_objects

    model_wrapper = build_sam3_predictor(**build_kwargs)

    # Initialize session
    response = model_wrapper.handle_request(
        {"type": "start_session", "resource_path": video_dir}
    )
    session_id = response["session_id"]

    print("\nWarm-up round.")
    NUM_WARMUP_TRIES = 3
    fps = 0
    for _ in range(NUM_WARMUP_TRIES):
        fps = max(
            main_loop(
                model_wrapper=model_wrapper, session_id=session_id, text_prompt="circle"
            ),
            fps,
        )

    print("\nProfile round.")
    if profile:
        profiler_runner(
            main_loop,
            profile_save_dir=profile_save_dir or os.path.expanduser("~/traces"),
            profile_end_frame=profile_end_frame,
            model_wrapper=model_wrapper,
            session_id=session_id,
            text_prompt="circle",
        )
    else:
        fps = max(
            main_loop(
                model_wrapper=model_wrapper, session_id=session_id, text_prompt="circle"
            ),
            fps,
        )

    NUM_TRIES = 10
    for i in range(NUM_TRIES):
        torch.cuda.empty_cache()
        torch.cuda.reset_peak_memory_stats()
        print(f"\nTiming round {i + 1} ")
        fps = max(
            main_loop(
                model_wrapper=model_wrapper, session_id=session_id, text_prompt="circle"
            ),
            fps,
        )
        print(f"Frames per second (FPS): {fps:.2f}")
        max_memory_allocated()

    if synthesize_data:
        print("\nDeleting temporary video directory.")
        shutil.rmtree(video_dir)

    return fps


if __name__ == "__main__":
    username = getpass.getuser()
    os.environ["TORCHINDUCTOR_CACHE_DIR"] = f"/tmp/torchinductor_cache_{username}"
    os.environ["USE_PERFLIB"] = "1"

    parser = argparse.ArgumentParser(description="SAM3 Speed Test")
    parser.add_argument(
        "--version",
        type=str,
        default="sam3.1",
        choices=["sam3", "sam3.1"],
        help="Model version (default: sam3.1)",
    )
    parser.add_argument(
        "--checkpoint",
        type=str,
        default=None,
        help="Path to checkpoint (auto-downloads from HuggingFace if not provided)",
    )
    parser.add_argument(
        "--video_dir", type=str, default="/tmp/segment-anything-3/synth_video"
    )
    parser.add_argument("--num_objects", type=int, default=5)
    parser.add_argument("--n_frames", type=int, default=50)
    parser.add_argument("--radius", type=int, default=50)
    parser.add_argument("--speed", type=int, default=20)
    parser.add_argument("--width", type=int, default=1024)
    parser.add_argument("--height", type=int, default=1024)
    parser.add_argument(
        "--no-compile",
        action="store_false",
        dest="compile",
        help="Disable torch.compile",
    )
    parser.add_argument("--no-torch-profiling", action="store_false", dest="profile")
    parser.add_argument(
        "--no-data-synthesis", action="store_false", dest="synthesize_data"
    )
    parser.add_argument("--profile-save-dir", type=str, default=None)
    parser.add_argument("--profile-end-frame", type=int, default=-1)

    args = parser.parse_args()

    run_test(
        version=args.version,
        profile=args.profile,
        num_objects=args.num_objects,
        video_dir=args.video_dir,
        radius=args.radius,
        speed=args.speed,
        width=args.width,
        height=args.height,
        n_frames=args.n_frames,
        synthesize_data=args.synthesize_data,
        profile_save_dir=args.profile_save_dir,
        profile_end_frame=args.profile_end_frame,
        do_compile=args.compile,
        checkpoint_path=args.checkpoint,
    )



================================================
FILE: scripts/qualitative_test.py
================================================
"""
SAM3 Qualitative Test — supports both SAM3 and SAM3.1.

Tests text prompt detection + propagation on a synthetic video.
Checkpoints are auto-downloaded from HuggingFace.

Usage:
  python scripts/qualitative_test.py                    # SAM 3.1 default
  python scripts/qualitative_test.py --version sam3     # SAM 3
  python scripts/qualitative_test.py --video /path/to/video.mp4
"""

import argparse
import getpass
import os
import shutil

import cv2
import matplotlib
import numpy as np
import torch
from PIL import Image as PIL_Image, ImageDraw

matplotlib.use("Agg")
import matplotlib.pyplot as plt
from PIL import Image as PIL_Image, ImageDraw


OUTPUT_DIR = "/tmp/sam3_qualitative_test"

MASK_COLORS = [
    (255, 0, 0),
    (0, 255, 0),
    (0, 0, 255),
    (255, 255, 0),
    (255, 0, 255),
    (0, 255, 255),
    (255, 128, 0),
    (128, 0, 255),
    (0, 128, 255),
    (255, 64, 128),
    (128, 255, 0),
    (64, 128, 255),
    (255, 200, 0),
    (0, 200, 128),
    (200, 0, 128),
    (128, 128, 255),
    (255, 128, 128),
    (128, 255, 128),
    (128, 128, 0),
    (0, 128, 128),
]


def extract_frames(video_path, output_dir):
    if os.path.exists(output_dir) and len(os.listdir(output_dir)) > 0:
        n = len([f for f in os.listdir(output_dir) if f.endswith(".jpg")])
        print(f"Using existing {n} frames in {output_dir}")
        return n
    if os.path.exists(output_dir):
        shutil.rmtree(output_dir)
    os.makedirs(output_dir)
    cap = cv2.VideoCapture(video_path)
    idx = 0
    while True:
        ret, frame = cap.read()
        if not ret:
            break
        cv2.imwrite(os.path.join(output_dir, f"{idx:05d}.jpg"), frame)
        idx += 1
    cap.release()
    print(f"Extracted {idx} frames to {output_dir}")
    return idx


def synthesize_video(out_dir, num_objects=5, n_frames=30, width=1024, height=1024):
    if os.path.exists(out_dir):
        shutil.rmtree(out_dir)
    os.makedirs(out_dir)
    colors = [
        tuple(np.random.randint(0, 256, size=3).tolist()) for _ in range(num_objects)
    ]
    positions = [
        [
            float(np.random.randint(80, width - 80)),
            float(np.random.randint(80, height - 80)),
        ]
        for _ in range(num_objects)
    ]
    velocities = [
        [np.random.choice([-1, 1]) * 15, np.random.choice([-1, 1]) * 15]
        for _ in range(num_objects)
    ]
    for i in range(n_frames):
        img = PIL_Image.new("RGB", (width, height), (0, 0, 0))
        draw = ImageDraw.Draw(img)
        for j in range(num_objects):
            x, y = positions[j]
            draw.ellipse([(x - 50, y - 50), (x + 50, y + 50)], fill=colors[j])
            vx, vy = velocities[j]
            positions[j] = [
                np.clip(x + vx, 50, width - 50),
                np.clip(y + vy, 50, height - 50),
            ]
            if x < 50 or x > width - 50:
                velocities[j][0] *= -1
            if y < 50 or y > height - 50:
                velocities[j][1] *= -1
        img.save(os.path.join(out_dir, f"{i:05d}.jpg"))
    print(f"Generated {n_frames} synthetic frames with {num_objects} circles")
    return n_frames


def load_frame(frame_dir, frame_idx):
    return cv2.cvtColor(
        cv2.imread(os.path.join(frame_dir, f"{frame_idx:05d}.jpg")),
        cv2.COLOR_BGR2RGB,
    )


def render_overlay(frame_rgb, masks_by_obj, alpha=0.4):
    overlay = frame_rgb.copy().astype(np.float32)
    for obj_id, mask in sorted(masks_by_obj.items()):
        color = MASK_COLORS[obj_id % len(MASK_COLORS)]
        mask_bool = mask.astype(bool)
        for c in range(3):
            overlay[:, :, c] = np.where(
                mask_bool,
                overlay[:, :, c] * (1 - alpha) + color[c] * alpha,
                overlay[:, :, c],
            )
    return overlay.astype(np.uint8)


def save_overlay(frame_rgb, masks_by_obj, output_path, title=None):
    overlay = render_overlay(frame_rgb, masks_by_obj)
    fig, ax = plt.subplots(1, 1, figsize=(12, 7), dpi=100)
    ax.imshow(overlay)
    for obj_id, mask in sorted(masks_by_obj.items()):
        mask_bool = mask.astype(bool)
        if mask_bool.any():
            ys, xs = np.where(mask_bool)
            cx, cy = int(xs.mean()), int(ys.mean())
            color_rgb = MASK_COLORS[obj_id % len(MASK_COLORS)]
            facecolor = (color_rgb[0] / 255, color_rgb[1] / 255, color_rgb[2] / 255)
            ax.text(
                cx,
                cy,
                str(obj_id),
                color="white",
                fontsize=10,
                ha="center",
                va="center",
                fontweight="bold",
                bbox=dict(boxstyle="round,pad=0.2", facecolor=facecolor, alpha=0.8),
            )
    if title:
        ax.set_title(title, fontsize=12, fontweight="bold", pad=8)
    ax.axis("off")
    fig.tight_layout(pad=0)
    fig.savefig(output_path, bbox_inches="tight", pad_inches=0)
    plt.close(fig)


def collect_propagation(model, session_id):
    mask_dict = {}
    for response in model.handle_stream_request(
        {"type": "propagate_in_video", "session_id": session_id}
    ):
        frame_idx = response.get("frame_index")
        if frame_idx is None:
            continue
        outputs = response.get("outputs", {})
        obj_ids = outputs.get("out_obj_ids", [])
        binary_masks = outputs.get("out_binary_masks")
        if binary_masks is None:
            mask_dict[frame_idx] = {}
            continue
        if isinstance(obj_ids, torch.Tensor):
            obj_ids = obj_ids.cpu().numpy()
        if isinstance(binary_masks, torch.Tensor):
            binary_masks = binary_masks.cpu().numpy()
        masks = {}
        for i, oid in enumerate(obj_ids):
            m = binary_masks[i]
            if m.ndim == 3:
                m = m[0]
            masks[int(oid)] = m
        mask_dict[frame_idx] = masks
    torch.cuda.synchronize()
    return mask_dict


def main():
    parser = argparse.ArgumentParser(description="SAM3 Qualitative Test")
    parser.add_argument(
        "--version", type=str, default="sam3.1", choices=["sam3", "sam3.1"]
    )
    parser.add_argument(
        "--video",
        type=str,
        default=None,
        help="Path to video file. If not provided, generates synthetic video.",
    )
    parser.add_argument(
        "--checkpoint",
        type=str,
        default=None,
        help="Path to checkpoint (auto-downloads from HuggingFace if not provided)",
    )
    parser.add_argument(
        "--text_prompt", type=str, default="circle", help="Text prompt for detection"
    )
    parser.add_argument(
        "--n_frames", type=int, default=30, help="Number of frames for synthetic video"
    )
    args = parser.parse_args()

    username = getpass.getuser()
    os.environ["TORCHINDUCTOR_CACHE_DIR"] = f"/tmp/torchinductor_cache_{username}"
    os.environ["USE_PERFLIB"] = "1"
    torch.autocast(device_type="cuda", dtype=torch.bfloat16).__enter__()

    # Prepare video frames
    frame_dir = "/tmp/sam3_qualitative_frames"
    if args.video:
        n_frames = extract_frames(args.video, frame_dir)
    else:
        n_frames = synthesize_video(frame_dir, n_frames=args.n_frames)

    img = load_frame(frame_dir, 0)
    img_h, img_w = img.shape[:2]
    print(f"Video: {img_w}x{img_h}, {n_frames} frames")

    # Build model
    from sam3 import build_sam3_predictor

    print(f"\nBuilding {args.version} model...")
    build_kwargs = dict(version=args.version, compile=False, async_loading_frames=False)
    if args.checkpoint:
        build_kwargs["checkpoint_path"] = args.checkpoint
    model = build_sam3_predictor(**build_kwargs)

    # Start session
    response = model.handle_request(
        {"type": "start_session", "resource_path": frame_dir}
    )
    session_id = response["session_id"]
    print(f"Session: {session_id}")

    # Test: text prompt -> propagate
    out_dir = os.path.join(OUTPUT_DIR, f"{args.version}_text_{args.text_prompt}")
    if os.path.exists(out_dir):
        shutil.rmtree(out_dir)
    os.makedirs(out_dir)

    print(f"\nTest: text prompt '{args.text_prompt}' -> propagate")
    model.handle_request(
        {
            "type": "add_prompt",
            "session_id": session_id,
            "frame_index": 0,
            "text": args.text_prompt,
        }
    )

    mask_dict = collect_propagation(model, session_id)
    print(f"Propagated through {len(mask_dict)} frames")

    # Save overlays
    saved = 0
    for frame_idx in sorted(mask_dict.keys()):
        if frame_idx % 5 != 0:
            continue
        masks = mask_dict[frame_idx]
        if not masks:
            continue
        frame_rgb = load_frame(frame_dir, frame_idx)
        save_overlay(
            frame_rgb,
            masks,
            os.path.join(out_dir, f"frame_{frame_idx:05d}.png"),
            title=f"{args.version} | frame {frame_idx} | {len(masks)} objects",
        )
        saved += 1

    # Print results
    frame0 = mask_dict.get(0, {})
    print(f"\nDetected {len(frame0)} objects on frame 0:")
    for obj_id, mask in sorted(frame0.items()):
        mask_bool = mask.astype(bool)
        n_pixels = int(mask_bool.sum())
        if mask_bool.any():
            ys, xs = np.where(mask_bool)
            print(
                f"  obj {obj_id}: centroid ({int(xs.mean())}, {int(ys.mean())}), {n_pixels} pixels"
            )

    print(f"\nSaved {saved} overlay images to {out_dir}")
    print(
        "QUALITATIVE TEST PASSED"
        if len(frame0) > 0
        else "WARNING: No objects detected!"
    )

    # Cleanup
    if not args.video:
        shutil.rmtree(frame_dir)


if __name__ == "__main__":
    main()



================================================
FILE: scripts/eval/standalone_cgf1.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

"""Simple script to run the CGF1 evaluator given a prediction file and GT file(s).

Usage: python standalone_cgf1.py --pred_file <path_to_prediction_file> --gt_files <path_to_gt_file1> <path_to_gt_file2> ...
"""

import argparse

from sam3.eval.cgf1_eval import CGF1Evaluator


def main():
    parser = argparse.ArgumentParser()
    parser.add_argument(
        "--pred_file",
        type=str,
        required=True,
        help="Path to the prediction file in COCO format.",
    )
    parser.add_argument(
        "--gt_files",
        type=str,
        nargs="+",
        required=True,
        help="Paths to the ground truth files in COCO format.",
    )
    args = parser.parse_args()
    if len(args.gt_files) == 0:
        raise ValueError("At least one GT file must be provided.")

    is_gold = args.gt_files[0].split("_")[-1].startswith("gold_")
    if is_gold and len(args.gt_files) < 3:
        print(
            "WARNING: based on the name, it seems you are using gold GT files. Typically, there should be 3 GT files for gold subsets (a, b, c)."
        )

    evaluator = CGF1Evaluator(
        gt_path=args.gt_files, verbose=True, iou_type="segm"
    )  # change to bbox if you want detection performance

    results = evaluator.evaluate(args.pred_file)

    print(results)


if __name__ == "__main__":
    main()



================================================
FILE: scripts/eval/gold/eval_sam3.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe

"""Script to run the evaluator offline given the GTs for SAC-Gold test set and SAM3 model prediction files.
It reports CGF1, IL_MCC, PM_F1 metrics for each subset of SAC-Gold test set.

Usage: python eval_sam3.py --gt-folder <folder_with_gts> --pred-folder <folder_with_predictions>
"""

import argparse
import os

from sam3.eval.cgf1_eval import CGF1Evaluator

# Relative file names for GT files for 7 SA-Co/Gold subsets

saco_gold_gts = {
    # MetaCLIP Captioner
    "metaclip_nps": [
        "gold_metaclip_merged_a_release_test.json",
        "gold_metaclip_merged_b_release_test.json",
        "gold_metaclip_merged_c_release_test.json",
    ],
    # SA-1B captioner
    "sa1b_nps": [
        "gold_sa1b_merged_a_release_test.json",
        "gold_sa1b_merged_b_release_test.json",
        "gold_sa1b_merged_c_release_test.json",
    ],
    # Crowded
    "crowded": [
        "gold_crowded_merged_a_release_test.json",
        "gold_crowded_merged_b_release_test.json",
        "gold_crowded_merged_c_release_test.json",
    ],
    # FG Food
    "fg_food": [
        "gold_fg_food_merged_a_release_test.json",
        "gold_fg_food_merged_b_release_test.json",
        "gold_fg_food_merged_c_release_test.json",
    ],
    # FG Sports
    "fg_sports_equipment": [
        "gold_fg_sports_equipment_merged_a_release_test.json",
        "gold_fg_sports_equipment_merged_b_release_test.json",
        "gold_fg_sports_equipment_merged_c_release_test.json",
    ],
    # Attributes
    "attributes": [
        "gold_attributes_merged_a_release_test.json",
        "gold_attributes_merged_b_release_test.json",
        "gold_attributes_merged_c_release_test.json",
    ],
    # Wiki common
    "wiki_common": [
        "gold_wiki_common_merged_a_release_test.json",
        "gold_wiki_common_merged_b_release_test.json",
        "gold_wiki_common_merged_c_release_test.json",
    ],
}


def main():
    parser = argparse.ArgumentParser()
    parser.add_argument(
        "-g",
        "--gt-folder",
        type=str,
        help="Path to the folder containing the ground truth json files.",
    )
    parser.add_argument(
        "-p",
        "--pred-folder",
        type=str,
        help="Path to the folder containing the predictions json files.",
    )
    args = parser.parse_args()

    results = ""

    for subset_name, gts in saco_gold_gts.items():
        print("Processing subset: ", subset_name)
        gt_paths = [os.path.join(args.gt_folder, gt) for gt in gts]
        evaluator = CGF1Evaluator(
            gt_path=gt_paths, verbose=True, iou_type="segm"
        )  # change to bbox if you want detection performance

        pred_path = os.path.join(
            args.pred_folder,
            f"gold_{subset_name}/dumps/gold_{subset_name}/coco_predictions_segm.json",
        )
        summary = evaluator.evaluate(pred_path)

        cgf1 = str(round(summary["cgF1_eval_segm_cgF1"] * 100, 2))
        il_mcc = str(round(summary["cgF1_eval_segm_IL_MCC"], 2))
        pmf1 = str(round(summary["cgF1_eval_segm_positive_micro_F1"] * 100, 2))
        final_str = f"{cgf1},{il_mcc},{pmf1}"
        results += subset_name + ": " + final_str + "\n"

    print("Subset name, CG_F1, IL_MCC, pmF1")
    print(results)


if __name__ == "__main__":
    main()



================================================
FILE: scripts/eval/veval/README.md
================================================
# SA-Co/VEval Dataset
**License** each domain has its own License
* SA-Co/VEval - SA-V: CC-BY-NC 4.0
* SA-Co/VEval - YT-Temporal-1B: CC-BY-NC 4.0
* SA-Co/VEval - SmartGlasses: CC-by-4.0

**SA-Co/VEval** is an evaluation dataset comprising of 3 domains, each domain has a val and test split.
* SA-Co/VEval - SA-V: videos are from the [SA-V dataset](https://ai.meta.com/datasets/segment-anything-video/)
* SA-Co/VEval - YT-Temporal-1B: videos are from the [YT-Temporal-1B](https://cove.thecvf.com/datasets/704)
* SA-Co/VEval - SmartGlasses: egocentric videos from [Smart Glasses](https://huggingface.co/datasets/facebook/SACo-VEval/blob/main/media/saco_sg.tar.gz)

## Environment
Install the SA-Co/VEVal required environment
```
pip install -e ".[veval]"
```
This will allow us to run:
* `scripts/eval/veval/saco_yt1b_downloader.py` preparing frames for SA-Co/VEval - YT-Temporal-1B
* `examples/saco_veval_eval_example.ipynb` example of running an offline evaluator
* `examples/saco_veval_vis_example.ipynb` example of loading and visualizing the data

## Download
### The expected folder structure
The following folder structure is expected after finishing all the download and pre-processing steps in this section
```
data/
├── annotation/
│   ├── saco_veval_sav_test.json
│   ├── saco_veval_sav_val.json
│   ├── saco_veval_smartglasses_test.json
│   ├── saco_veval_smartglasses_val.json
│   ├── saco_veval_yt1b_test.json
│   ├── saco_veval_yt1b_val.json
└── media/
    ├── saco_sav
    │   └── JPEGImages_24fps
    ├── saco_sg
    │   └── JPEGImages_6fps
    └── saco_yt1b
        └── JPEGImages_6fps
```
### Download ready-to-use data
The following links provide ready-to-use data, hosted on Roboflow, after completing the pre-processing steps outlined in the next section.

For each domain:
- [SA-Co/VEval - SA-V](https://universe.roboflow.com/sa-co-veval/sa-v-test/)
- [SA-Co/VEval - YT-Temporal-1B](https://universe.roboflow.com/sa-co-veval/yt-temporal-1b-test/)
- [SA-Co/VEval - SmartGlasses](https://universe.roboflow.com/sa-co-veval/smartglasses-test/)

For all three domains:
- [SA-Co/VEval](https://universe.roboflow.com/sa-co-veval)

Special note on **SA-Co/VEval - YT-Temporal-1B**:
* **Frame Shifting Alert!**
* The ready-to-use data hosted on Roboflow was produced by following the preprocessing steps below. Therefore, the frame-shifting issue for YT-Temporal-1B still exists: due to the nature of Youtube videos, the re-downloaded videos may not be exactly the same as those used during annotation, which can affect eval number reproducibility.

### Download via preprocessing steps
#### Download annotations
The GT annotations are available at Hugging Face:
* [SA-Co/VEval](https://huggingface.co/datasets/facebook/SACo-VEval/tree/main)
    * SA-Co/VEval SA-V
        * Test: `annotation/saco_veval_sav_test.json`
        * Val: `annotation/saco_veval_sav_val.json`
    * SA-Co/VEval YT-Temporal-1B
        * Test: `annotation/saco_veval_yt1b_test.json`
        * Val: `annotation/saco_veval_yt1b_val.json`
    * SA-Co/VEval SmartGlasses
        * Test: `annotation/saco_veval_smartglasses_test.json`
        * Val: `annotation/saco_veval_smartglasses_val.json`

#### Download videos or frames
##### SA-Co/VEval - SAV
Follow instructions in [SA-V dataset](https://ai.meta.com/datasets/segment-anything-video/). Only the following two datasets are needed:
* sav_test.tar
* sav_val.tar

After untar:
```
sav_test/
├── Annotations_6fps [ignore this is the SAM 2 annotation]
├── JPEGImages_24fps
sav_val/
├── Annotations_6fps [ignore this is the SAM 2 annotation]
└── JPEGImages_24fps
```
Then merge the two JPEGImages_24fps together to better match our annotation json file path e.g.
```
media/
    └── saco_sav
        └── JPEGImages_24fps [merged from the two JPEGImages_24fps above]
```
Example commands to download and merge folders
```
cd ../data/media/saco_sav
wget -O sav_test.tar <sav_test.tar download link from the SA-V dataset page>
wget -O sav_val.tar <sav_val.tar download link from the SA-V dataset page>
tar -xf sav_test.tar
tar -xf sav_val.tar
mkdir JPEGImages_24fps
chmod -R u+w sav_test/
chmod -R u+w sav_val/
mv sav_test/JPEGImages_24fps/* JPEGImages_24fps/
mv sav_val/JPEGImages_24fps/* JPEGImages_24fps/
```

##### SA-Co/VEval - YT-Temporal-1B
Two files are needed to download the SA-Co/VEval - YT-Temporal-1B Youtube videos.
* Download `media/yt1b_start_end_time.json` from [SA-Co/VEval](https://huggingface.co/datasets/facebook/SACo-VEval/tree/main), which contains the Youtube video ids and the start and end time used in SA-Co/VEval - YT-Temporal-1B.
* Prepare the `cookies.txt` file. Follow instruction in yt-dlp [exporting-youtube-cookies](https://github.com/yt-dlp/yt-dlp/wiki/Extractors#exporting-youtube-cookies) and [pass-cookies-to-yt-dlp](https://github.com/yt-dlp/yt-dlp/wiki/FAQ#how-do-i-pass-cookies-to-yt-dlp) to prepare the cookies_file.
    * Please see the full **WARNINGS** in yt-dlp regarding the risk of Youtube account ban!!

Then run `scripts/eval/veval/saco_yt1b_downloader.py` to download the videos and prepare the frames e.g.
```
python saco_yt1b_downloader.py \
--data_dir ../data/media/saco_yt1b \
--cookies_file ../data/media/saco_yt1b/cookies.txt \
--yt1b_start_end_time_file ../data/media/saco_yt1b/yt1b_start_end_time.json \
--yt1b_frame_prep_log_file ../data/media/saco_yt1b/yt1b_frame_prep.log
```
* data_dir: The directoy to download the Youtube videos and store the extraced frames
* cookies_file: the `cookies.txt` downloaded above
* yt1b_start_end_time_file: the `yt1b_start_end_time.json` downloaded above
* yt1b_frame_prep_log_file: a log file to track the video downloading and frame extracting status

Then run `scripts/eval/veval/saco_yt1b_annot_update.py` to update the annotation based on the video availability e.g.
```
python saco_yt1b_annot_update.py \
--yt1b_media_dir ../data/media/saco_yt1b/JPEGImages_6fps \
--yt1b_input_annot_path ../data/annotation/saco_veval_yt1b_val.json \
--yt1b_output_annot_path ../data/annotation/saco_veval_yt1b_val_updated.json \
--yt1b_annot_update_log_path ../data/annotation/saco_veval_yt1b_val_updated.log
```

**NOTE**:
* Not all Youtube videos might be available as Youtube videos can be deleted or become private. The script `saco_yt1b_annot_update.py` is used to remove the annotations of the unavailable videos.
* **Frame Shifting Alert!!** Even when the videos are still available, their specifications, such as fps and duration, may differ from those used during annotation when re-downloaded from YouTube. Additionally, sometimes `ffmpeg` seems to find it hard to guarantee consistent frame extraction from the same video across different environments. This may cause the re-downloaded and re-extracted frames to have alignment issues with our annotations due to frame shifting. Please be aware of this caveat when evaluating on SA-Co/VEval - YT-Temporal-1B.

##### SA-Co/VEval - SmartGlasses
Go to [SACo-VEval](https://huggingface.co/datasets/facebook/SACo-VEval/tree/main) download `media/saco_sg.tar.gz`
```
cd ../data
hf download facebook/SACo-VEval media/saco_sg.tar.gz --repo-type dataset --local-dir .
cd ../data/media
tar -xzf saco_sg.tar.gz
```

## Annotation Format
The format is similar to the [YTVIS](https://youtube-vos.org/dataset/vis/) format.

In the annotation json, e.g. `saco_veval_sav_test.json` there are 5 fields:
* info:
    * A dict containing the dataset info
    * E.g. {'version': 'v1', 'date': '2025-09-24', 'description': 'SA-Co/VEval SA-V Test'}
* videos
    * A list of videos that are used in the current annotation json
    * It contains {id, video_name, file_names, height, width, length}
* annotations
    * A list of **positive** masklets and their related info
    * It contains {id, segmentations, bboxes, areas, iscrowd, video_id, height, width, category_id, noun_phrase}
        * video_id should match to the `videos - id` field above
        * category_id should match to the `categories - id` field below
        * segmentations is a list of [RLE](https://github.com/cocodataset/cocoapi/blob/master/PythonAPI/pycocotools/mask.py)
* categories
    * A **globally** used noun phrase id map, which is true across all 3 domains.
    * It contains {id, name}
        * name is the noun phrase
* video_np_pairs
    * A list of video-np pairs, including both **positive** and **negative** used in the current annotation json
    * It contains {id, video_id, category_id, noun_phrase, num_masklets}
        * video_id should match the `videos - id` above
        * category_id should match the `categories - id` above
        * when `num_masklets > 0` it is a positive video-np pair, and the presenting masklets can be found in the annotations field
        * when `num_masklets = 0` it is a negative video-np pair, meaning no masklet presenting at all
```
data {
    "info": info
    "videos": [video]
    "annotations": [annotation]
    "categories": [category]
    "video_np_pairs": [video_np_pair]
}
video {
    "id": int
    "video_name": str  # e.g. sav_000000
    "file_names": List[str]
    "height": int
    "width": width
    "length": length
}
annotation {
    "id": int
    "segmentations": List[RLE]
    "bboxes": List[List[int, int, int, int]]
    "areas": List[int]
    "iscrowd": int
    "video_id": str
    "height": int
    "width": int
    "category_id": int
    "noun_phrase": str
}
category {
    "id": int
    "name": str
}
video_np_pair {
    "id": int
    "video_id": str
    "category_id": int
    "noun_phrase": str
    "num_masklets" int
}
```
[sam3/examples/saco_veval_vis_example.ipynb](https://github.com/facebookresearch/sam3/blob/main/examples/saco_veval_vis_example.ipynb) shows some examples of the data format and data visualization.

## Run Offline Eval
An example notebook and an eval script have been provided for offline evaluation.
```
sam3/
├── examples/
│   └── saco_veval_eval_example.ipynb  # this notebook will load eval res or run the eval on the fly, and print the results
└── sam3/eval/
    └── saco_veval_eval.py  # this script will run the offline evaluator
```
`saco_veval_eval.py` supports two modes, `one` and `all`.
* `one`: will take only one pair of gt and pred files to eval
* `all`: will eval on all 6 SACo/VEval datasets

Example usage
```
python saco_veval_eval.py one \
--gt_annot_file ../sam3/assets/veval/toy_gt_and_pred/toy_saco_veval_sav_test_gt.json \
--pred_file ../sam3/assets/veval/toy_gt_and_pred/toy_saco_veval_sav_test_pred.json \
--eval_res_file ../sam3/assets/veval/toy_gt_and_pred/toy_saco_veval_sav_test_eval_res.json
```
* `gt_annot_file`: the location of the GT file
* `pred_file`: the location of the Pred file
* `eval_res_file`: the location where the eval result will be written to

```
python saco_veval_eval.py all \
--gt_annot_dir ../data/annotation \
--pred_dir ../data/pred \
--eval_res_dir ../data/pred
```
* `gt_annot_dir`: the location of the GT files
* `pred_dir`: the location of the Pred files
* `eval_res_dir`: the location where the eval results will be written to



================================================
FILE: scripts/eval/veval/__init__.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe



================================================
FILE: scripts/eval/veval/saco_yt1b_annot_update.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe
import argparse
import json
import logging
import os

import pandas as pd


logger = logging.getLogger(__name__)


def get_available_saco_yt1b_ids(yt1b_meida_dir, data):
    vdf = pd.DataFrame(data["videos"])
    expected_saco_yt1b_ids = vdf.video_name.tolist()

    yt1b_media_folders = os.listdir(yt1b_meida_dir)

    available_saco_yt1b_ids = []
    for yt1b_media_folder in yt1b_media_folders:
        if yt1b_media_folder not in expected_saco_yt1b_ids:
            continue
        jpeg_folder_dir = os.path.join(yt1b_meida_dir, yt1b_media_folder)
        jpeg_count = len(os.listdir(jpeg_folder_dir))
        if jpeg_count > 0:
            available_saco_yt1b_ids.append(yt1b_media_folder)
        else:
            logger.info(
                f"No JPEG images found for {yt1b_media_folder}. The annotation related to this video will be removed."
            )

    logger.info(
        f"Expected {len(expected_saco_yt1b_ids)} videos for {data['info']}. Found {len(available_saco_yt1b_ids)} videos available in {yt1b_meida_dir}."
    )
    return available_saco_yt1b_ids


def update_yt1b_annot_per_field(data, field, id_col, available_ids):
    field_data = data[field]
    new_field_data = []
    for data_entry in field_data:
        if data_entry[id_col] not in available_ids:
            logger.info(
                f"{field}: Removing {data_entry} due to the video being unavailable."
            )
            continue
        new_field_data.append(data_entry)

    data[field] = new_field_data
    logger.info(
        f"Updated {field} by {id_col} - Before: {len(field_data)}, After: {len(new_field_data)}, Removed: {len(field_data) - len(new_field_data)}"
    )
    return data


def update_yt1b_annot(yt1b_input_annot_path, yt1b_media_dir, yt1b_output_annot_path):
    with open(yt1b_input_annot_path, "r") as f:
        data = json.load(f)

    available_saco_yt1b_ids = get_available_saco_yt1b_ids(yt1b_media_dir, data)

    data = update_yt1b_annot_per_field(
        data=data,
        field="videos",
        id_col="video_name",
        available_ids=available_saco_yt1b_ids,
    )

    videos_data = data["videos"]
    available_video_incremental_ids = [data_entry["id"] for data_entry in videos_data]

    data = update_yt1b_annot_per_field(
        data=data,
        field="annotations",
        id_col="video_id",
        available_ids=available_video_incremental_ids,
    )
    data = update_yt1b_annot_per_field(
        data=data,
        field="video_np_pairs",
        id_col="video_id",
        available_ids=available_video_incremental_ids,
    )

    with open(yt1b_output_annot_path, "w") as f:
        json.dump(data, f)

    return data


def main():
    parser = argparse.ArgumentParser(description="Run video grounding evaluators")
    parser.add_argument(
        "--yt1b_media_dir",
        type=str,
        help="Path to the directory where the yt1b media is stored e.g media/saco_yt1b/JPEGImages_6fps",
    )
    parser.add_argument(
        "--yt1b_input_annot_path",
        type=str,
        help="Path to the saco_veval_yt1b input annotation file e.g annotation/saco_veval_yt1b_test.json or annotation/saco_veval_yt1b_val.json",
    )
    parser.add_argument(
        "--yt1b_output_annot_path",
        type=str,
        help="Path to the output annotation file e.g annotation/saco_veval_yt1b_test_updated.json or annotation/saco_veval_yt1b_val_updated.json",
    )
    parser.add_argument(
        "--yt1b_annot_update_log_path",
        type=str,
        help="Path to the yt1b annot update log file e.g annotation/yt1b_annot_update_log.log",
    )

    args = parser.parse_args()

    os.makedirs(os.path.dirname(args.yt1b_annot_update_log_path), exist_ok=True)
    os.makedirs(os.path.dirname(args.yt1b_output_annot_path), exist_ok=True)

    logging.basicConfig(
        filename=args.yt1b_annot_update_log_path,
        format="%(asctime)s [%(threadName)s] %(levelname)s: %(message)s",
        level=logging.INFO,
        filemode="w",
    )

    _ = update_yt1b_annot(
        yt1b_input_annot_path=args.yt1b_input_annot_path,
        yt1b_media_dir=args.yt1b_media_dir,
        yt1b_output_annot_path=args.yt1b_output_annot_path,
    )

    print("Done!! Check the log at", args.yt1b_annot_update_log_path)


if __name__ == "__main__":
    main()



================================================
FILE: scripts/eval/veval/saco_yt1b_downloader.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe
import argparse
import logging
import multiprocessing as mp
import os
from functools import partial

import pandas as pd
from saco_yt1b_frame_prep_util import YtVideoPrep
from tqdm import tqdm

logger = logging.getLogger(__name__)


def download_and_extract_frames(saco_yt1b_id, args):
    video_prep = YtVideoPrep(
        saco_yt1b_id=saco_yt1b_id,
        data_dir=args.data_dir,
        cookies_file=args.cookies_file,
        yt1b_start_end_time_file=args.yt1b_start_end_time_file,
        ffmpeg_timeout=args.ffmpeg_timeout,
        sleep_interval=args.sleep_interval,
        max_sleep_interval=args.max_sleep_interval,
    )

    status = video_prep.download_youtube_video()
    logger.info(f"[video download][{saco_yt1b_id}] download status {status}")

    if status not in ["already exists", "success"]:
        logger.warning(
            f"Video download failed for {saco_yt1b_id}, skipping frame generation"
        )
        return False

    status = video_prep.extract_frames_in_6fps_and_width_1080()
    logger.info(f"[frame extracting][{saco_yt1b_id}] frame extracting status {status}")
    return True


def main():
    parser = argparse.ArgumentParser()
    parser.add_argument(
        "--data_dir",
        type=str,
        required=True,
    )
    parser.add_argument(
        "--cookies_file",
        type=str,
        required=True,
    )
    parser.add_argument(
        "--yt1b_start_end_time_file",
        type=str,
        required=True,
    )
    parser.add_argument(
        "--yt1b_frame_prep_log_file",
        type=str,
        required=True,
    )
    parser.add_argument(
        "--ffmpeg_timeout",
        type=str,
        default=7200,  # Use longer timeout in case of large videos processing timeout
    )
    parser.add_argument(
        "--sleep_interval",
        type=int,
        default=10,
    )
    parser.add_argument(
        "--max_sleep_interval",
        type=int,
        default=30,
    )
    parser.add_argument(
        "--num_workers",
        type=int,
        default=4,
    )
    args = parser.parse_args()

    log_dir = os.path.dirname(args.yt1b_frame_prep_log_file)
    if log_dir:
        os.makedirs(log_dir, exist_ok=True)

    # Set up logging to both file and console
    # Configure the ROOT logger so all child loggers inherit the configuration
    logging.basicConfig(
        level=logging.INFO,
        format="%(asctime)s [%(processName)s/%(threadName)s] %(name)s - %(levelname)s: %(message)s",
        handlers=[
            logging.FileHandler(args.yt1b_frame_prep_log_file, mode="w"),
            logging.StreamHandler(),
        ],
        force=True,  # Override any existing configuration
    )

    YT_DLP_WARNING_STR = """ ==========
        NOTICE!!
        This script uses yt-dlp to download youtube videos.
        See the youtube account banning risk in https://github.com/yt-dlp/yt-dlp/wiki/Extractors#exporting-youtube-cookies
        ==========
        """

    logger.info(YT_DLP_WARNING_STR)

    args = parser.parse_args()

    with open(args.yt1b_start_end_time_file, "r") as f:
        yt1b_start_end_time_df = pd.read_json(f)

    saco_yt1b_ids = yt1b_start_end_time_df.saco_yt1b_id.unique()
    num_workers = args.num_workers
    logger.info(
        f"Starting with {num_workers} parallel worker(s) (sleep_interval={args.sleep_interval}-{args.max_sleep_interval}s)"
    )

    with mp.Pool(num_workers) as p:
        download_func = partial(download_and_extract_frames, args=args)
        list(tqdm(p.imap(download_func, saco_yt1b_ids), total=len(saco_yt1b_ids)))

    done_str = f""" ==========
        All DONE!!
        Download, frame extraction, and frame matching is all done! YT1B frames are not ready to use in {args.data_dir}/JPEGImages_6fps
        Check video frame preparing log at {args.yt1b_frame_prep_log_file}
        Some videos might not be available any more which will affect the eval reproducibility
        ==========
    """
    logger.info(done_str)


if __name__ == "__main__":
    main()



================================================
FILE: scripts/eval/veval/saco_yt1b_frame_prep_util.py
================================================
# Copyright (c) Meta Platforms, Inc. and affiliates. All Rights Reserved

# pyre-unsafe
import argparse
import logging
import os
import subprocess

import pandas as pd
import yt_dlp

logger = logging.getLogger(__name__)


class YtVideoPrep:
    def __init__(
        self,
        saco_yt1b_id: str,
        data_dir: str,
        cookies_file: str,
        yt1b_start_end_time_file: str,
        ffmpeg_timeout: int,
        sleep_interval: int = 10,
        max_sleep_interval: int = 30,
    ):
        self.saco_yt1b_id = saco_yt1b_id  # saco_yt1b_id is like saco_yt1b_000000
        self.data_dir = data_dir
        self.cookies_file = cookies_file
        self.ffmpeg_timeout = ffmpeg_timeout
        self.sleep_interval = sleep_interval
        self.max_sleep_interval = max_sleep_interval

        self.yt1b_start_end_time_df = pd.read_json(yt1b_start_end_time_file)
        (
            self.yt_video_id,
            self.yt_video_id_w_timestamps,
            self.start_time,
            self.end_time,
            self.expected_num_frames,
        ) = self._get_yt_video_id_map_info()

        self.raw_video_dir = os.path.join(self.data_dir, "raw_videos")
        self.raw_video_path = os.path.join(
            self.raw_video_dir, f"{self.yt_video_id}.mp4"
        )

        self.JPEGImages_6fps_dir = os.path.join(
            self.data_dir, "JPEGImages_6fps", self.saco_yt1b_id
        )
        self.JPEGImages_6fps_pattern = os.path.join(
            self.JPEGImages_6fps_dir, "%05d.jpg"
        )

        os.makedirs(self.raw_video_dir, exist_ok=True)
        os.makedirs(self.JPEGImages_6fps_dir, exist_ok=True)

    def _get_yt_video_id_map_info(self):
        df = self.yt1b_start_end_time_df[
            self.yt1b_start_end_time_df.saco_yt1b_id == self.saco_yt1b_id
        ]
        assert len(df) == 1, (
            f"Expected exactly 1 row for saco_yt1b_id: {self.saco_yt1b_id}, found {len(df)}"
        )
        id_and_frame_map_row = df.iloc[0]

        yt_video_id = (
            id_and_frame_map_row.yt_video_id
        )  # yt_video_id is like -06NgWyZxC0
        yt_video_id_w_timestamps = id_and_frame_map_row.yt_video_id_w_timestamps
        start_time = id_and_frame_map_row.start_time
        end_time = id_and_frame_map_row.end_time
        expected_num_frames = id_and_frame_map_row.length

        return (
            yt_video_id,
            yt_video_id_w_timestamps,
            start_time,
            end_time,
            expected_num_frames,
        )

    def download_youtube_video(self):
        video_url = f"https://youtube.com/watch?v={self.yt_video_id}"

        assert os.path.exists(self.cookies_file), (
            f"Cookies file '{self.cookies_file}' not found. Must have it to download videos."
        )

        outtmpl = self.raw_video_path

        # Check if the output file already exists
        if os.path.exists(outtmpl) and os.path.isfile(outtmpl):
            return "already exists"

        ydl_opts = {
            "format": "best[height<=720]/best",  # 720p or lower
            "outtmpl": outtmpl,
            "merge_output_format": "mp4",
            "noplaylist": True,
            "quiet": True,
            "cookiefile": self.cookies_file,
            "sleep_interval": self.sleep_interval,  # Sleep before each download to avoid rate limiting
            "max_sleep_interval": self.max_sleep_interval,  # Random sleep for more human-like behavior
        }

        if self.yt_video_id in ["euohdDLEMRg", "nzfAn7n4d-0"]:
            # For "euohdDLEMRg", we have to specify the https protocol or the video sometimes can't be downloaded completely
            # For "nzfAn7n4d-0", without the https protocol, the video will be downloaded as 654×480, however we need 490×360 to match the frame matching after the 1080 width resizing
            ydl_opts["format"] = (
                "best[height<=720][ext=mp4][protocol^=https]/best[ext=mp4][protocol^=https]/best[height<=720]/best"
            )

        try:
            with yt_dlp.YoutubeDL(ydl_opts) as ydl:
                ydl.download([video_url])
                return "success"
        except Exception as e:
            logger.warning(
                f"[video download][{self.saco_yt1b_id}] Error downloading video {self.yt_video_id}: {e}"
            )
            return f"error {e}"

    def extract_frames_in_6fps_and_width_1080(self):
        """
        Extract target frames in 6fps and width 1080.
        """
        if not os.path.exists(self.raw_video_path):
            logger.warning(
                f"[frame extracting][{self.saco_yt1b_id}] Raw video file not found at {self.raw_video_path}"
            )
            os.rmdir(self.JPEGImages_6fps_dir)
            return False

        if (
            os.path.exists(self.JPEGImages_6fps_dir)
            and len(os.listdir(self.JPEGImages_6fps_dir)) == self.expected_num_frames
        ):
            logger.info(
                f"[frame extracting][{self.saco_yt1b_id}] JPEGImages_6fps directory already exists at {self.JPEGImages_6fps_dir} and expected number of frames {self.expected_num_frames} matches"
            )
            return True

        # Clear the directory before extracting new frames
        for file in os.listdir(self.JPEGImages_6fps_dir):
            os.remove(os.path.join(self.JPEGImages_6fps_dir, file))

        args = [
            "-nostdin",
            "-y",
            # select video segment
            "-ss",
            str(self.start_time),
            "-to",
            str(self.end_time),
            "-i",
            self.raw_video_path,
            # set output video resolution to be 6fps and at most 1080p
            "-vf",
            "fps=6,scale=1080:-2",
            "-vsync",
            "0",  # passthrough mode - no frame duplication/dropping
            "-q:v",
            "2",  # high quality JPEG output
            "-start_number",
            "0",  # start frame numbering from 0
            self.JPEGImages_6fps_pattern,
        ]

        result = subprocess.run(
            ["ffmpeg"] + args,
            timeout=self.ffmpeg_timeout,
            capture_output=True,
            text=True,
        )

        if result.returncode != 0:
            logger.warning(
                f"[frame extracting][{self.saco_yt1b_id}] Failed to extract raw frames: {result.stderr}"
            )
            os.rmdir(self.JPEGImages_6fps_dir)
            return False

        if len(os.listdir(self.JPEGImages_6fps_dir)) != self.expected_num_frames:
            logger.warning(
                f"[frame extracting][{self.saco_yt1b_id}] Expected {self.expected_num_frames} frames but extracted {len(os.listdir(self.JPEGImages_6fps_dir))}"
            )
            # Clear the directory after failed extraction
            for file in os.listdir(self.JPEGImages_6fps_dir):
                os.remove(os.path.join(self.JPEGImages_6fps_dir, file))

            os.rmdir(self.JPEGImages_6fps_dir)
            return False

        logger.info(
            f"[frame extracting][{self.saco_yt1b_id}] Successfully extracted {self.expected_num_frames} frames to {self.JPEGImages_6fps_dir}"
        )
        return True


def main():
    parser = argparse.ArgumentParser()
    parser.add_argument("--saco_yt1b_id", type=str, required=True)
    parser.add_argument(
        "--data_dir",
        type=str,
        required=True,
    )
    parser.add_argument(
        "--cookies_file",
        type=str,
        required=True,
    )
    parser.add_argument(
        "--yt1b_start_end_time_file",
        type=str,
        required=True,
    )
    parser.add_argument(
        "--yt1b_frame_prep_log_file",
        type=str,
        required=True,
    )
    parser.add_argument(
        "--ffmpeg_timeout",
        type=str,
        default=7200,  # Use longer timeout in case of large videos processing timeout
    )
    parser.add_argument(
        "--sleep_interval",
        type=int,
        default=10,
    )
    parser.add_argument(
        "--max_sleep_interval",
        type=int,
        default=30,
    )
    args = parser.parse_args()

    logging.basicConfig(
        filename=args.yt1b_frame_prep_log_file,
        format="%(asctime)s [%(threadName)s] %(levelname)s: %(message)s",
        level=logging.INFO,
        filemode="w",
    )

    video_prep = YtVideoPrep(
        saco_yt1b_id=args.saco_yt1b_id,
        data_dir=args.data_dir,
        cookies_file=args.cookies_file,
        yt1b_start_end_time_file=args.yt1b_start_end_time_file,
        ffmpeg_timeout=args.ffmpeg_timeout,
        sleep_interval=args.sleep_interval,
        max_sleep_interval=args.max_sleep_interval,
    )

    status = video_prep.download_youtube_video()
    logger.info(f"[video download][{args.saco_yt1b_id}] download status {status}")

    status = video_prep.extract_frames_in_6fps_and_width_1080()
    logger.info(
        f"[frame extracting][{args.saco_yt1b_id}] frame extracting status {status}"
    )


if __name__ == "__main__":
    main()
