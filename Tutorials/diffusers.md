# Diffusers 教程：扩散模型开发终极指南

Diffusers 是 Hugging Face 推出的开源扩散模型（Diffusion Models）库，提供 SOTA 文本到图像生成、音频合成、视频生成等模型的实现与预训练权重。以下是快速掌握 Diffusers 的完整教程。

---

## 目录

1. [安装与环境配置](#安装与环境配置)  
2. [核心概念解析](#核心概念解析)  
3. [文本到图像生成](#文本到图像生成)  
4. [图像到图像转换](#图像到图像转换)  
5. [模型推理与训练](#模型推理与训练)  
6. [高级功能](#高级功能)  
7. [实战案例](#实战案例)  
8. [注意事项](#注意事项)  

---

## 安装与环境配置

```bash
# 安装稳定版
pip install diffusers

# 安装最新开发版
pip install git+https://github.com/huggingface/diffusers

# 安装 CUDA 支持（推荐）
pip install torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/cu118
```

### 推荐环境
```bash
Python >= 3.8
PyTorch >= 1.13 或 TensorFlow >= 2.11
CUDA 11.8 (用于GPU加速)
NVIDIA驱动 >= 520.xx
```

---

## 核心概念解析

### 1. 扩散模型类型

| 模型类型              | 典型应用场景               | 示例模型                          |
|-----------------------|----------------------------|-----------------------------------|
| DDPM                  | 图像生成                   | `ddpm-celebahq-128`              |
| DDIM                  | 加速采样                   | `stabilityai/stable-diffusion-2` |
| LDM                   | 文本到图像                 | `CompVis/ldm-text2im-large-4365098` |
| Stable Diffusion      | 多模态生成                 | `runwayml/stable-diffusion-v1-5`  |
| Latent Diffusion Video| 视频生成                   | `damo-vilab/modelscope-diffusion` |

### 2. 核心组件

```python
from diffusers import (
    DDPMPipeline, 
    DDIMPipeline, 
    StableDiffusionPipeline,
    AutoencoderKL,
    UNet2DModel,
    SchedulerMixin
)
```

---

## 文本到图像生成

### 1. 基础用法

```python
from diffusers import StableDiffusionPipeline
import torch

pipe = StableDiffusionPipeline.from_pretrained(
    "runwayml/stable-diffusion-v1-5", 
    torch_dtype=torch.float16
).to("cuda")

prompt = "A cyberpunk cityscape at night with neon lights"
image = pipe(prompt).images[0]
image.save("cyberpunk_city.png")
```

### 2. 自定义参数

```python
image = pipe(
    prompt,
    height=768,               # 图像高度
    width=1024,              # 图像宽度
    num_inference_steps=50,  # 采样步数
    guidance_scale=7.5,      # 无分类指导系数
    negative_prompt="blurry, low quality"  # 负向提示
).images[0]
```

---

## 图像到图像转换

### 1. 图像编辑（img2img）

```python
from diffusers import StableDiffusionImg2ImgPipeline

pipe = StableDiffusionImg2ImgPipeline.from_pretrained(
    "runwayml/stable-diffusion-v1-5", 
    torch_dtype=torch.float16
).to("cuda")

init_image = Image.open("input.jpg").convert("RGB")
prompt = "A photo of a cat in the style of Van Gogh"

image = pipe(
    prompt=prompt, 
    image=init_image, 
    strength=0.75,  # 修改强度 (0-1)
    guidance_scale=7.5
).images[0]
```

### 2. 图像超分辨率

```python
from diffusers import DiffusionPipeline

pipeline = DiffusionPipeline.from_pretrained(
    "stabilityai/stable-unclip-2-1-high-res"
)
image = pipeline(prompt).images[0]
```

---

## 模型推理与训练

### 1. 自定义模型加载

```python
from diffusers import UNet2DModel, DDPMScheduler

noise_scheduler = DDPMScheduler(num_train_timesteps=1000)
model = UNet2DModel.from_pretrained("google/ddpm-cat-256", subfolder="unet")
```

### 2. 训练循环示例

```python
from torch.optim import AdamW
from accelerate import Accelerator

accelerator = Accelerator(mixed_precision="fp16")
model, optimizer, train_dataloader = accelerator.prepare(
    model, optimizer, train_dataloader
)

for epoch in range(10):
    for step, batch in enumerate(train_dataloader):
        clean_images = batch["images"]
        noise = torch.randn_like(clean_images)
        timesteps = torch.randint(0, noise_scheduler.num_train_timesteps, (clean_images.shape[0],), device=model.device)
        noisy_images = noise_scheduler.add_noise(clean_images, noise, timesteps)

        with accelerator.accumulate(model):
            noise_pred = model(noisy_images, timesteps).sample
            loss = F.mse_loss(noise_pred, noise)
            accelerator.backward(loss)
            optimizer.step()
            optimizer.zero_grad()
```

---

## 高级功能

### 1. 控制生成（ControlNet）

```python
from diffusers import StableDiffusionControlNetPipeline, ControlNetModel

controlnet = ControlNetModel.from_pretrained("lllyasviel/sd-controlnet-canny")
pipe = StableDiffusionControlNetPipeline.from_pretrained(
    "runwayml/stable-diffusion-v1-5", 
    controlnet=controlnet,
    torch_dtype=torch.float16
).to("cuda")

canny_image = Image.open("canny_edge.jpg")
image = pipe(prompt, image=canny_image).images[0]
```

### 2. 低秩适配（LoRA）

```python
from diffusers import StableDiffusionPipeline
from peft import PeftModel

base_model = StableDiffusionPipeline.from_pretrained("runwayml/stable-diffusion-v1-5")
lora_model = PeftModel.from_pretrained(base_model, "path/to/lora_weights")
```

---

## 实战案例

### 1. 视频生成（Latent Diffusion Video）

```python
from diffusers import VideoLCM Pipeline

pipe = VideoLCMPipeline.from_pretrained("damo-vilab/modelscope-diffusion", subfolder="video lcm")
video_frames = pipe(prompt="A rotating 3D cube").frames
```

### 2. 音频生成（Audio Diffusion）

```python
from diffusers import AudioDiffusionPipeline

pipe = AudioDiffusionPipeline.from_pretrained("teticio/audio-diffusion-256")
audio = pipe("music").audios[0]
```

---

## 注意事项

1. **硬件要求**：
   - 推荐使用 NVIDIA A100/H100 或消费级 RTX 4090
   - 16GB 显存可支持 512x512 生成，1024x1024 需 24GB+

2. **内存优化**：
   ```python
   pipe.enable_attention_slicing()  # 降低显存占用
   pipe.enable_sequential_cpu_offload()  # CPU/GPU 内存交换
   ```

3. **版本兼容性**：
   - 确保 PyTorch 版本与 CUDA 驱动匹配
   - 使用 `pip install diffusers --pre` 安装 nightly 版本

4. **安全过滤**：
   ```python
   pipe.safety_checker = None  # 禁用 NSFW 过滤器
   ```

5. **调试技巧**：
   - 使用 `accelerate` 库进行分布式训练
   - 使用 `diffusers.utils.logging.set_verbosity_error()` 降低日志级别

---

## 总结

Diffusers 的核心优势在于：

- **模块化设计**：可灵活组合调度器、UNet、VAE 等组件
- **SOTA 模型**：集成最新扩散模型论文实现（如 SDXL、LCM、PixArt）
- **生产就绪**：支持 ONNX 导出、TensorRT 加速、LoRA 微调
- **生态整合**：与 Hugging Face Datasets、Transformers 无缝衔接

**进一步学习**:
- [Diffusers 官方文档](https://huggingface.co/docs/diffusers)
- [扩散模型论文合集](https://github.com/huggingface/diffusers/tree/main/papers)
- 推荐书籍：《扩散模型：原理与实践》（Hugging Face 出版）
