```
Directory structure:
└── kgmufassa-qwen-image-layered/
    ├── README.md
    ├── LICENSE
    └── src/
        ├── app.py
        └── tool/
            ├── combine_layers.py
            └── edit_rgba_image.py
```
================================================
FILE: README.md
================================================
<p align="center">
    <img src="https://qianwen-res.oss-cn-beijing.aliyuncs.com/Qwen-Image/layered/qwen-image-layered-logo.png" width="800"/>
<p> 
<p align="center">&nbsp&nbsp🤗 <a href="https://huggingface.co/Qwen/Qwen-Image-Layered">HuggingFace</a>&nbsp&nbsp | &nbsp&nbsp🤖 <a href="https://modelscope.cn/models/Qwen/Qwen-Image-Layered">ModelScope</a>&nbsp&nbsp | &nbsp&nbsp 📑 <a href="https://arxiv.org/abs/2512.15603">Research Paper</a> &nbsp&nbsp | &nbsp&nbsp 📑 <a href="https://qwen.ai/blog?id=qwen-image-layered">Blog</a> &nbsp&nbsp | &nbsp&nbsp 🤗 <a href="https://huggingface.co/spaces/Qwen/Qwen-Image-Layered">Demo</a> &nbsp&nbsp 
</p>

<p align="center">
    <img src="https://qianwen-res.oss-cn-beijing.aliyuncs.com/Qwen-Image/layered/layered.JPG" width="1024"/>
<p>

## Introduction
We are excited to introduce **Qwen-Image-Layered**, a model capable of decomposing an image into multiple RGBA layers. This layered representation unlocks **inherent editability**: each layer can be independently manipulated without affecting other content. Meanwhile, such a layered representation naturally supports **high-fidelity elementary operations**-such as resizing, reposition, and recoloring. By physically isolating semantic or structural components into distinct layers, our approach enables high-fidelity and consistent editing.


[![Qwen Image Layered](https://img.youtube.com/vi/OVhmiBrsziQ/0.jpg)](https://www.youtube.com/watch?v=OVhmiBrsziQ)


## News
- 2025.12.22: You can try Qwen-Image-Layered on [Huggingface Spaces](https://huggingface.co/spaces/Qwen/Qwen-Image-Layered) and [Modelscope Studio](https://modelscope.cn/studios/Qwen/Qwen-Image-Layered).
- 2025.12.19: We released Qwen-Image-Layered weights! Check at [Huggingface](https://huggingface.co/Qwen/Qwen-Image-Layered) and [ModelScope](https://modelscope.cn/models/Qwen/Qwen-Image-Layered)!
- 2025.12.19: We released Qwen-Image-Layered! Check our [Blog](https://qwen.ai/blog?id=qwen-image-layered) for more details!
- 2025.12.18: We released our [Research Paper](https://arxiv.org/abs/2512.15603) on Arxiv!

> [!NOTE]
> - The text prompt is intended to describe the overall content of the input image—including elements that may be partially occluded (e.g., you may specify the text hidden behind a foreground object). It is not designed to control the semantic content of individual layers explicitly.
> - The released weights are specifically fine-tuned for the image-to-multi-RGBA decomposition task. As a result, while the model supports text-conditioned inference, its performance on text-to-multi-RGBA generation is limited.

## Quick Start

1. Make sure your transformers>=4.51.3 (Supporting Qwen2.5-VL)

2. Install the latest version of diffusers
```
pip install git+https://github.com/huggingface/diffusers
pip install python-pptx
pip install psd-tools
```


```python
from diffusers import QwenImageLayeredPipeline
import torch
from PIL import Image

pipeline = QwenImageLayeredPipeline.from_pretrained("Qwen/Qwen-Image-Layered")
pipeline = pipeline.to("cuda", torch.bfloat16)
pipeline.set_progress_bar_config(disable=None)

image = Image.open("asserts/test_images/1.png").convert("RGBA")
inputs = {
    "image": image,
    "generator": torch.Generator(device='cuda').manual_seed(777),
    "true_cfg_scale": 4.0,
    "negative_prompt": " ",
    "num_inference_steps": 50,
    "num_images_per_prompt": 1,
    "layers": 4,
    "resolution": 640,      # Using different bucket (640, 1024) to determine the resolution. For this version, 640 is recommended
    "cfg_normalize": True,  # Whether enable cfg normalization.
    "use_en_prompt": True,  # Automatic caption language if user does not provide caption
}

with torch.inference_mode():
    output = pipeline(**inputs)
    output_image = output.images[0]

for i, image in enumerate(output_image):
    image.save(f"{i}.png")
```

## Deploy Qwen-Image-Layered
The following scripts will start a Gradio-based web interface where you can decompose an image and export the layers into pptx, zip, and psd files, where you can edit and move these layers flexibly.
```bash
python src/app.py
```

After decomposition, you may want to edit specific layers. The following scripts will launch a Gradio-based web interface where you can edit images with transparency using Qwen-Image-Edit.
```bash
python src/tool/edit_rgba_image.py
```

After editing the individual decomposed layers, you can use the following script to combine them into a new image. Remember to upload the layers in order—from the bottom layer to the top.
```bash
python src/tool/combine_layers.py
```

### vLLM-Omni
[vLLM-Omni](https://github.com/vllm-project/vllm-omni) now supports Qwen-Image-Layered. See the [recipes](https://docs.vllm.ai/projects/recipes/en/latest/Qwen/Qwen-Image.html) for up-to-date details.

## Showcase
### Layered Decomposition in Application
Given an image, Qwen-Image-Layered can decompose it into several RGBA layers:
![Example Image](https://qianwen-res.oss-cn-beijing.aliyuncs.com/Qwen-Image/layered/幻灯片1.JPG)

After decomposition, edits are applied exclusively to the target layer, physically isolating it from the rest of the content, and thereby fundamentally ensuring consistency across edits. 

For example, we can recolor the first layer and keep all other content untouched:
![Example Image](https://qianwen-res.oss-cn-beijing.aliyuncs.com/Qwen-Image/layered/幻灯片2.JPG)

We can also replace the second layer from a girl to a boy (The target layer is edited using Qwen-Image-Edit):
![Example Image](https://qianwen-res.oss-cn-beijing.aliyuncs.com/Qwen-Image/layered/幻灯片3.JPG)

Here, we revise the text to "Qwen-Image" (The target layer is edited using Qwen-Image-Edit):
![Example Image](https://qianwen-res.oss-cn-beijing.aliyuncs.com/Qwen-Image/layered/幻灯片4.JPG)

Furthermore, the layered structure naturally supports elemetary operations. For example, we can delete unwanted objects cleanly:
![Example Image](https://qianwen-res.oss-cn-beijing.aliyuncs.com/Qwen-Image/layered/幻灯片5.JPG)

We can also resize an object without distortion:
![Example Image](https://qianwen-res.oss-cn-beijing.aliyuncs.com/Qwen-Image/layered/幻灯片6.JPG)

After layer decomposition, we can move objects freely within the canvas:
![Example Image](https://qianwen-res.oss-cn-beijing.aliyuncs.com/Qwen-Image/layered/幻灯片7.JPG)

### Flexible and Iterative Decomposition
Qwen-Image-Layered is not limited to a fixed number of layers. The model supports variable-layer decomposition. For example, we can decompose an image into either 3 or 8 layers as needed:

![Example Image](https://qianwen-res.oss-cn-beijing.aliyuncs.com/Qwen-Image/layered/幻灯片8.JPG)

Moreover, decomposition can be applied recursively: any layer can itself be further decomposed, enabling infinite decomposition. 

![Example Image](https://qianwen-res.oss-cn-beijing.aliyuncs.com/Qwen-Image/layered/幻灯片9.JPG)


## License Agreement

Qwen-Image-Layered is licensed under Apache 2.0. 

## Citation

We kindly encourage citation of our work if you find it useful.

```bibtex
@misc{yin2025qwenimagelayered,
      title={Qwen-Image-Layered: Towards Inherent Editability via Layer Decomposition}, 
      author={Shengming Yin, Zekai Zhang, Zecheng Tang, Kaiyuan Gao, Xiao Xu, Kun Yan, Jiahao Li, Yilei Chen, Yuxiang Chen, Heung-Yeung Shum, Lionel M. Ni, Jingren Zhou, Junyang Lin, Chenfei Wu},
      year={2025},
      eprint={2512.15603},
      archivePrefix={arXiv},
      primaryClass={cs.CV},
      url={https://arxiv.org/abs/2512.15603}, 
}
```



================================================
FILE: LICENSE
================================================
                                 Apache License
                           Version 2.0, January 2004
                        http://www.apache.org/licenses/

   TERMS AND CONDITIONS FOR USE, REPRODUCTION, AND DISTRIBUTION

   1. Definitions.

      "License" shall mean the terms and conditions for use, reproduction,
      and distribution as defined by Sections 1 through 9 of this document.

      "Licensor" shall mean the copyright owner or entity authorized by
      the copyright owner that is granting the License.

      "Legal Entity" shall mean the union of the acting entity and all
      other entities that control, are controlled by, or are under common
      control with that entity. For the purposes of this definition,
      "control" means (i) the power, direct or indirect, to cause the
      direction or management of such entity, whether by contract or
      otherwise, or (ii) ownership of fifty percent (50%) or more of the
      outstanding shares, or (iii) beneficial ownership of such entity.

      "You" (or "Your") shall mean an individual or Legal Entity
      exercising permissions granted by this License.

      "Source" form shall mean the preferred form for making modifications,
      including but not limited to software source code, documentation
      source, and configuration files.

      "Object" form shall mean any form resulting from mechanical
      transformation or translation of a Source form, including but
      not limited to compiled object code, generated documentation,
      and conversions to other media types.

      "Work" shall mean the work of authorship, whether in Source or
      Object form, made available under the License, as indicated by a
      copyright notice that is included in or attached to the work
      (an example is provided in the Appendix below).

      "Derivative Works" shall mean any work, whether in Source or Object
      form, that is based on (or derived from) the Work and for which the
      editorial revisions, annotations, elaborations, or other modifications
      represent, as a whole, an original work of authorship. For the purposes
      of this License, Derivative Works shall not include works that remain
      separable from, or merely link (or bind by name) to the interfaces of,
      the Work and Derivative Works thereof.

      "Contribution" shall mean any work of authorship, including
      the original version of the Work and any modifications or additions
      to that Work or Derivative Works thereof, that is intentionally
      submitted to Licensor for inclusion in the Work by the copyright owner
      or by an individual or Legal Entity authorized to submit on behalf of
      the copyright owner. For the purposes of this definition, "submitted"
      means any form of electronic, verbal, or written communication sent
      to the Licensor or its representatives, including but not limited to
      communication on electronic mailing lists, source code control systems,
      and issue tracking systems that are managed by, or on behalf of, the
      Licensor for the purpose of discussing and improving the Work, but
      excluding communication that is conspicuously marked or otherwise
      designated in writing by the copyright owner as "Not a Contribution."

      "Contributor" shall mean Licensor and any individual or Legal Entity
      on behalf of whom a Contribution has been received by Licensor and
      subsequently incorporated within the Work.

   2. Grant of Copyright License. Subject to the terms and conditions of
      this License, each Contributor hereby grants to You a perpetual,
      worldwide, non-exclusive, no-charge, royalty-free, irrevocable
      copyright license to reproduce, prepare Derivative Works of,
      publicly display, publicly perform, sublicense, and distribute the
      Work and such Derivative Works in Source or Object form.

   3. Grant of Patent License. Subject to the terms and conditions of
      this License, each Contributor hereby grants to You a perpetual,
      worldwide, non-exclusive, no-charge, royalty-free, irrevocable
      (except as stated in this section) patent license to make, have made,
      use, offer to sell, sell, import, and otherwise transfer the Work,
      where such license applies only to those patent claims licensable
      by such Contributor that are necessarily infringed by their
      Contribution(s) alone or by combination of their Contribution(s)
      with the Work to which such Contribution(s) was submitted. If You
      institute patent litigation against any entity (including a
      cross-claim or counterclaim in a lawsuit) alleging that the Work
      or a Contribution incorporated within the Work constitutes direct
      or contributory patent infringement, then any patent licenses
      granted to You under this License for that Work shall terminate
      as of the date such litigation is filed.

   4. Redistribution. You may reproduce and distribute copies of the
      Work or Derivative Works thereof in any medium, with or without
      modifications, and in Source or Object form, provided that You
      meet the following conditions:

      (a) You must give any other recipients of the Work or
          Derivative Works a copy of this License; and

      (b) You must cause any modified files to carry prominent notices
          stating that You changed the files; and

      (c) You must retain, in the Source form of any Derivative Works
          that You distribute, all copyright, patent, trademark, and
          attribution notices from the Source form of the Work,
          excluding those notices that do not pertain to any part of
          the Derivative Works; and

      (d) If the Work includes a "NOTICE" text file as part of its
          distribution, then any Derivative Works that You distribute must
          include a readable copy of the attribution notices contained
          within such NOTICE file, excluding those notices that do not
          pertain to any part of the Derivative Works, in at least one
          of the following places: within a NOTICE text file distributed
          as part of the Derivative Works; within the Source form or
          documentation, if provided along with the Derivative Works; or,
          within a display generated by the Derivative Works, if and
          wherever such third-party notices normally appear. The contents
          of the NOTICE file are for informational purposes only and
          do not modify the License. You may add Your own attribution
          notices within Derivative Works that You distribute, alongside
          or as an addendum to the NOTICE text from the Work, provided
          that such additional attribution notices cannot be construed
          as modifying the License.

      You may add Your own copyright statement to Your modifications and
      may provide additional or different license terms and conditions
      for use, reproduction, or distribution of Your modifications, or
      for any such Derivative Works as a whole, provided Your use,
      reproduction, and distribution of the Work otherwise complies with
      the conditions stated in this License.

   5. Submission of Contributions. Unless You explicitly state otherwise,
      any Contribution intentionally submitted for inclusion in the Work
      by You to the Licensor shall be under the terms and conditions of
      this License, without any additional terms or conditions.
      Notwithstanding the above, nothing herein shall supersede or modify
      the terms of any separate license agreement you may have executed
      with Licensor regarding such Contributions.

   6. Trademarks. This License does not grant permission to use the trade
      names, trademarks, service marks, or product names of the Licensor,
      except as required for reasonable and customary use in describing the
      origin of the Work and reproducing the content of the NOTICE file.

   7. Disclaimer of Warranty. Unless required by applicable law or
      agreed to in writing, Licensor provides the Work (and each
      Contributor provides its Contributions) on an "AS IS" BASIS,
      WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or
      implied, including, without limitation, any warranties or conditions
      of TITLE, NON-INFRINGEMENT, MERCHANTABILITY, or FITNESS FOR A
      PARTICULAR PURPOSE. You are solely responsible for determining the
      appropriateness of using or redistributing the Work and assume any
      risks associated with Your exercise of permissions under this License.

   8. Limitation of Liability. In no event and under no legal theory,
      whether in tort (including negligence), contract, or otherwise,
      unless required by applicable law (such as deliberate and grossly
      negligent acts) or agreed to in writing, shall any Contributor be
      liable to You for damages, including any direct, indirect, special,
      incidental, or consequential damages of any character arising as a
      result of this License or out of the use or inability to use the
      Work (including but not limited to damages for loss of goodwill,
      work stoppage, computer failure or malfunction, or any and all
      other commercial damages or losses), even if such Contributor
      has been advised of the possibility of such damages.

   9. Accepting Warranty or Additional Liability. While redistributing
      the Work or Derivative Works thereof, You may choose to offer,
      and charge a fee for, acceptance of support, warranty, indemnity,
      or other liability obligations and/or rights consistent with this
      License. However, in accepting such obligations, You may act only
      on Your own behalf and on Your sole responsibility, not on behalf
      of any other Contributor, and only if You agree to indemnify,
      defend, and hold each Contributor harmless for any liability
      incurred by, or claims asserted against, such Contributor by reason
      of your accepting any such warranty or additional liability.

   END OF TERMS AND CONDITIONS

   APPENDIX: How to apply the Apache License to your work.

      To apply the Apache License to your work, attach the following
      boilerplate notice, with the fields enclosed by brackets "[]"
      replaced with your own identifying information. (Don't include
      the brackets!)  The text should be enclosed in the appropriate
      comment syntax for the file format. We also recommend that a
      file or class name and description of purpose be included on the
      same "printed page" as the copyright notice for easier
      identification within third-party archives.

   Copyright [yyyy] [name of copyright owner]

   Licensed under the Apache License, Version 2.0 (the "License");
   you may not use this file except in compliance with the License.
   You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

   Unless required by applicable law or agreed to in writing, software
   distributed under the License is distributed on an "AS IS" BASIS,
   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
   See the License for the specific language governing permissions and
   limitations under the License.



================================================
FILE: src/app.py
================================================
from diffusers import QwenImageLayeredPipeline
import torch
from PIL import Image
from pptx import Presentation
import os
import gradio as gr
import uuid
import numpy as np
import random
import tempfile
import zipfile 
from psd_tools import PSDImage
MAX_SEED = np.iinfo(np.int32).max

pipeline = QwenImageLayeredPipeline.from_pretrained("Qwen/Qwen-Image-Layered")
pipeline = pipeline.to("cuda", torch.bfloat16)
pipeline.set_progress_bar_config(disable=None)

def imagelist_to_pptx(img_files):
    with Image.open(img_files[0]) as img:
        img_width_px, img_height_px = img.size

    def px_to_emu(px, dpi=96):
        inch = px / dpi
        emu = inch * 914400
        return int(emu)

    prs = Presentation()
    prs.slide_width = px_to_emu(img_width_px)
    prs.slide_height = px_to_emu(img_height_px)

    slide = prs.slides.add_slide(prs.slide_layouts[6])

    left = top = 0
    for img_path in img_files:
        slide.shapes.add_picture(img_path, left, top, width=px_to_emu(img_width_px), height=px_to_emu(img_height_px))

    with tempfile.NamedTemporaryFile(suffix=".pptx", delete=False) as tmp:
        prs.save(tmp.name)
        return tmp.name

def imagelist_to_psd(img_files):
    layers = []
    for path in img_files:
        layers.append(Image.open(path).convert('RGBA'))

    width, height = layers[0].size
    psd = PSDImage.new(mode='RGBA', size=(width, height))

    for i, img in enumerate(layers):
        name = f"Layer {i + 1}"
        layer = psd.create_pixel_layer(image=img, name=name)
        psd.append(layer)
    
    with tempfile.NamedTemporaryFile(suffix=".psd", delete=False) as tmp:
        psd.save(tmp.name)
        return tmp.name

def export_gallery(images):
    # images: list of image file paths
    images = [e[0] for e in images]
    pptx_path = imagelist_to_pptx(images)
    return pptx_path

def infer(input_image,
          seed=777,
          randomize_seed=False,
          prompt=None,
          neg_prompt=" ",
          true_guidance_scale=4.0,
          num_inference_steps=50,
          layer=4,
          cfg_norm=True,
          use_en_prompt=True):
    
    if randomize_seed:
        seed = random.randint(0, MAX_SEED)
        
    if isinstance(input_image, list):
        input_image = input_image[0]
        
    if isinstance(input_image, str):
        pil_image = Image.open(input_image).convert("RGB").convert("RGBA")
    elif isinstance(input_image, Image.Image):
        pil_image = input_image.convert("RGB").convert("RGBA")
    elif isinstance(input_image, np.ndarray):
        pil_image = Image.fromarray(input_image).convert("RGB").convert("RGBA")
    else:
        raise ValueError("Unsupported input_image type: %s" % type(input_image))
    
    inputs = {
        "image": pil_image,
        "generator": torch.Generator(device='cuda').manual_seed(seed),
        "true_cfg_scale": true_guidance_scale,
        "prompt": prompt,
        "negative_prompt": neg_prompt,
        "num_inference_steps": num_inference_steps,
        "num_images_per_prompt": 1,
        "layers": layer,
        "resolution": 640,      # Using different bucket (640, 1024) to determine the resolution. For this version, 640 is recommended
        "cfg_normalize": cfg_norm,  # Whether enable cfg normalization.
        "use_en_prompt": use_en_prompt, 
    }
    print(inputs)
    with torch.inference_mode():
        output = pipeline(**inputs)
        output_images = output.images[0]
    
    output = []
    temp_files = []
    for i, image in enumerate(output_images):
        output.append(image)
        # Save to temp file for export
        tmp = tempfile.NamedTemporaryFile(suffix=".png", delete=False)
        image.save(tmp.name)
        temp_files.append(tmp.name)
    
    # Generate PPTX
    pptx_path = imagelist_to_pptx(temp_files)
    
    # Generate ZIP
    with tempfile.NamedTemporaryFile(suffix=".zip", delete=False) as tmp:
        with zipfile.ZipFile(tmp.name, 'w', zipfile.ZIP_DEFLATED) as zipf:
            for i, img_path in enumerate(temp_files):
                zipf.write(img_path, f"layer_{i+1}.png")
        zip_path = tmp.name
    
    # Generate PSD
    psd_path = imagelist_to_psd(temp_files)
    return output, pptx_path, zip_path, psd_path

examples = [
            "assets/test_images/1.png",
            "assets/test_images/2.png",
            "assets/test_images/3.png",
            "assets/test_images/4.png",
            "assets/test_images/5.png",
            "assets/test_images/6.png",
            "assets/test_images/7.png",
            "assets/test_images/8.png",
            "assets/test_images/9.png",
            "assets/test_images/10.png",
            "assets/test_images/11.png",
            "assets/test_images/12.png",
            "assets/test_images/13.png",
            ]


with gr.Blocks() as demo:
    with gr.Column(elem_id="col-container"):
        gr.HTML('''<p align="center"><img src="https://qianwen-res.oss-cn-beijing.aliyuncs.com/Qwen-Image/layered/qwen-image-layered-logo.png" width="400"/><p>''')
        gr.Markdown("""
                    The text prompt is intended to describe the overall content of the input image—including elements that may be partially occluded (e.g., you may specify the text hidden behind a foreground object). It is not designed to control the semantic content of individual layers explicitly.
                    """)
        with gr.Row():
            with gr.Column(scale=1):
                input_image = gr.Image(label="Input Image", image_mode="RGBA")
                
                
                with gr.Accordion("Advanced Settings", open=False):
                    prompt = gr.Textbox(
                        label="Prompt (Optional)",
                        placeholder="Please enter the prompt to describe the image. It is not designed to control the semantic content of individual layers explicitly. (Optional)",
                        value="",
                        lines=3,
                    )
                    neg_prompt = gr.Textbox(
                        label="Negative Prompt (Optional)",
                        placeholder="Please enter the negative prompt",
                        value=" ",
                        lines=3,
                    )
                    
                    seed = gr.Slider(
                        label="Seed",
                        minimum=0,
                        maximum=MAX_SEED,
                        step=1,
                        value=0,
                    )
                    randomize_seed = gr.Checkbox(label="Randomize seed", value=True)
                    
                    true_guidance_scale = gr.Slider(
                        label="True guidance scale",
                        minimum=1.0,
                        maximum=10.0,
                        step=0.1,
                        value=4.0
                    )

                    num_inference_steps = gr.Slider(
                        label="Number of inference steps",
                        minimum=1,
                        maximum=50,
                        step=1,
                        value=50,
                    )

                    layer = gr.Slider(
                        label="Layers",
                        minimum=2,
                        maximum=10,
                        step=1,
                        value=4,
                    )

                    cfg_norm = gr.Checkbox(label="Whether enable CFG normalization", value=True)
                    use_en_prompt = gr.Checkbox(label="Automatic caption language if no prompt provided, True for EN, False for ZH", value=True)
                
                run_button = gr.Button("Decompose!", variant="primary")

            with gr.Column(scale=2):
                gallery = gr.Gallery(label="Layers", columns=4, rows=1, format="png")
                with gr.Row():
                    export_file = gr.File(label="Download PPTX")
                    export_zip_file = gr.File(label="Download ZIP")
                    export_psd_file = gr.File(label="Download PSD")

    gr.Examples(examples=examples,
                inputs=[input_image], 
                outputs=[gallery, export_file, export_zip_file, export_psd_file],
                fn=infer, 
                examples_per_page=14,
                cache_examples=False,
                run_on_click=True
    )

    run_button.click(
        fn=infer,
        inputs=[
            input_image,
            seed,
            randomize_seed,
            prompt,
            neg_prompt,
            true_guidance_scale,
            num_inference_steps,
            layer,
            cfg_norm,
            use_en_prompt,
        ], 
        outputs=[gallery, export_file, export_zip_file, export_psd_file],
    )

demo.launch(
    server_name="0.0.0.0",
    server_port=7869,
)



================================================
FILE: src/tool/combine_layers.py
================================================
import gradio as gr
from PIL import Image

def combine_images(uploaded_files):
    if not uploaded_files:
        return None

    images = []
    for f in uploaded_files:
        img = Image.open(f.name).convert("RGBA")
        images.append(img)

    min_height = min(img.height for img in images)
    resized_images = [img.resize((int(img.width * min_height / img.height), min_height), Image.LANCZOS) for img in images]

    combined = resized_images[0]
    for img in resized_images[1:]:
        combined = Image.alpha_composite(combined, img)

    return combined

demo = gr.Interface(
    fn=combine_images,
    inputs=gr.File(file_count="multiple", label="Upload images with transparency (PNG) in order."),
    outputs=gr.Image(type="pil", label="Combined Result"),
    title="Layer Blender",
    description="Upload multiple PNG images, and the system will blend them into a single image.",
)

if __name__ == "__main__":
    demo.launch()



================================================
FILE: src/tool/edit_rgba_image.py
================================================
import gradio as gr
import numpy as np
import random
import torch

from PIL import Image, ImageDraw
from torchvision import transforms
from transformers import AutoModelForImageSegmentation
from diffusers import QwenImageEditPlusPipeline

# --- Model Loading ---
dtype = torch.bfloat16
device = "cuda" if torch.cuda.is_available() else "cpu"

# Load the model pipeline
pipe = QwenImageEditPlusPipeline.from_pretrained("Qwen/Qwen-Image-Edit-2509", torch_dtype=dtype).to(device)
rmbg_model = AutoModelForImageSegmentation.from_pretrained('briaai/RMBG-2.0', trust_remote_code=True).eval().to(device)
rmbg_transforms = transforms.Compose([
        transforms.Resize((1024, 1024)),
        transforms.ToTensor(),
        transforms.Normalize([0.485, 0.456, 0.406], [0.229, 0.224, 0.225])
    ])

# --- UI Constants and Helpers ---
MAX_SEED = np.iinfo(np.int32).max

def blend_with_green_bg(input_img):
    bg = Image.new("RGB", input_img.size, (30, 215, 96)).convert("RGBA")
    input_rgba = input_img.convert("RGBA")
    blended = Image.alpha_composite(bg, input_rgba).convert("RGB")
    return blended

# --- Main Inference Function (with hardcoded negative prompt) ---
def infer(
    image,
    prompt,
    seed=42,
    randomize_seed=False,
    true_guidance_scale=1.0,
    num_inference_steps=50,
    progress=gr.Progress(track_tqdm=True),
):
    """
    Generates an image using the local Qwen-Image diffusers pipeline.
    """
    # Hardcode the negative prompt as requested
    negative_prompt = " "
    
    if randomize_seed:
        seed = random.randint(0, MAX_SEED)

    # Set up the generator for reproducibility
    generator = torch.Generator(device=device).manual_seed(seed)
    
    print(f"Calling pipeline with prompt: '{prompt}'")
    print(f"Negative Prompt: '{negative_prompt}'")
    print(f"Seed: {seed}, Steps: {num_inference_steps}, Guidance: {true_guidance_scale}")

    image = blend_with_green_bg(image)

    # Generate the image
    edited_image = pipe(
        image,
        prompt=prompt,
        negative_prompt=negative_prompt,
        num_inference_steps=num_inference_steps,
        generator=generator,
        true_cfg_scale=true_guidance_scale,
        num_images_per_prompt=1
    ).images[0]

    # Remove background
    input_images = rmbg_transforms(edited_image).unsqueeze(0).to(device)
    with torch.no_grad():
        preds = rmbg_model(input_images)[-1].sigmoid().cpu()
    pred = preds[0].squeeze()
    pred_pil = transforms.ToPILImage()(pred)
    mask = pred_pil.resize(edited_image.size)
    edited_image.putalpha(mask)
    
    return edited_image, seed

# --- Examples and UI Layout ---
examples = []

css = """
#col-container {
    margin: 0 auto;
    max-width: 1024px;
}
#edit_text{margin-top: -62px !important}
"""

with gr.Blocks(css=css) as demo:
    with gr.Column(elem_id="col-container"):
        gr.HTML('<img src="https://qianwen-res.oss-cn-beijing.aliyuncs.com/Qwen-Image/qwen_image_edit_logo.png" alt="Qwen-Image-Edit Logo" width="400" style="display: block; margin: 0 auto;">')
        gr.Markdown("This Gradio-based web interface use [Qwen-Image-Edit](https://github.com/QwenLM/Qwen-Image) to edit layers with transparent background. Upload an image with alpha channel (RGBA) and provide an edit instruction to get started!")
        with gr.Row():
            with gr.Column():
                input_image = gr.Image(label="Input Image", show_label=False, type="pil", image_mode="RGBA")

            result = gr.Image(label="Result", show_label=False, type="pil")
        with gr.Row():
            prompt = gr.Text(
                    label="Prompt",
                    show_label=False,
                    placeholder="describe the edit instruction",
                    container=False,
            )
            run_button = gr.Button("Edit!", variant="primary")

        with gr.Accordion("Advanced Settings", open=False):
            seed = gr.Slider(
                label="Seed",
                minimum=0,
                maximum=MAX_SEED,
                step=1,
                value=0,
            )

            randomize_seed = gr.Checkbox(label="Randomize seed", value=True)

            with gr.Row():

                true_guidance_scale = gr.Slider(
                    label="True guidance scale",
                    minimum=1.0,
                    maximum=10.0,
                    step=0.1,
                    value=4.0
                )

                num_inference_steps = gr.Slider(
                    label="Number of inference steps",
                    minimum=1,
                    maximum=50,
                    step=1,
                    value=50,
                )
                

        # gr.Examples(examples=examples, inputs=[prompt], outputs=[result, seed], fn=infer, cache_examples=False)

    gr.on(
        triggers=[run_button.click, prompt.submit],
        fn=infer,
        inputs=[
            input_image,
            prompt,
            seed,
            randomize_seed,
            true_guidance_scale,
            num_inference_steps,
        ],
        outputs=[result, seed],
    )

if __name__ == "__main__":
    demo.launch()
