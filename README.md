<h1 align="center">🩺 医学人工智能科研指南 · Medical-AI-Guide</h1>

<p align="center">
  <strong>From Learning the Basics to Conducting Reproducible Medical AI Research</strong>
</p>

<p align="center">
  一个面向医学人工智能初学者与科研人员的系统化学习与科研指南
</p>

<p align="center">
  <a href="https://github.com/diaoquesang/Medical-AI-Guide">
    <img src="https://img.shields.io/github/stars/diaoquesang/Medical-AI-Guide?style=flat">
  </a>
  <a href="https://github.com/diaoquesang/Medical-AI-Guide/network/members">
    <img src="https://img.shields.io/github/forks/diaoquesang/Medical-AI-Guide?style=flat">
  </a>
  <a href="https://github.com/diaoquesang/Medical-AI-Guide/issues">
    <img src="https://img.shields.io/github/issues/diaoquesang/Medical-AI-Guide?style=flat">
  </a>
  <a href="https://github.com/diaoquesang/Medical-AI-Guide/blob/main/LICENSE">
    <img src="https://img.shields.io/github/license/diaoquesang/Medical-AI-Guide?style=flat">
  </a>
</p>

---

## 📖 About

**Medical-AI-Guide** 是一个面向医学人工智能学习者与科研人员的开源指南。

本项目最初希望帮助医学人工智能初学者快速建立完整的技术栈；随着医学 AI 从传统深度学习逐渐发展到 **Foundation Models、Multimodal Learning、Large Language Models、Vision-Language Models、Diffusion Models 与 Generative AI**，本项目也将内容逐步扩展为更加完整的医学 AI 科研工作流。

我们希望你在这里获得的不只是“如何运行代码”，更是：

> **如何发现问题 → 理解数据 → 设计方法 → 实现模型 → 正确评估 → 撰写论文 → 发布代码 → 做出可复现的医学 AI 研究。**

欢迎 ⭐ Star、💡 提交 Issue、🔀 Pull Request 与分享本项目。

---

# 🗺️ Learning Roadmap

如果你是第一次接触医学人工智能，推荐按照下面的路线逐步学习：

```text
Mathematics & Programming
          ↓
   Machine Learning
          ↓
     Deep Learning
          ↓
   Medical Imaging
          ↓
 Medical AI Research
          ↓
 ┌────────┼──────────┐
 ↓        ↓          ↓
CV      Generative   Multimodal
        AI / Diff.     AI
 ↓        ↓          ↓
Foundation Models / LLMs / VLMs
          ↓
     Medical AI Research
          ↓
 Evaluation & Reproducibility
          ↓
       Paper Writing
          ↓
    Open-source / Deployment
```

---

# 1. 🔍 Research & Paper Reading

医学 AI 科研的第一步不是写代码，而是**正确理解问题与建立研究视野**。

### 🔎 Academic Search

* [Google Scholar](https://scholar.google.com/) — 学术论文搜索与引用追踪
* [Semantic Scholar](https://www.semanticscholar.org/) — AI 驱动的论文搜索与推荐
* [arXiv](https://arxiv.org/) — 预印本论文平台
* [OpenReview](https://openreview.net/) — 会议论文、评审与讨论
* [PubMed](https://pubmed.ncbi.nlm.nih.gov/) — 生物医学论文检索
* [AMiner](https://www.aminer.cn/) — 学术资源搜索与学术网络分析
* [Connected Papers](https://www.connectedpapers.com/) — 论文关系图谱
* [DeepWiki](https://deepwiki.org/) — AI-assisted GitHub Repository 理解

### 📚 Recommended Reading Topics

* Medical Image Analysis
* Medical Image Segmentation
* Medical Image Classification
* Object Detection & Localization
* Image Registration
* Image Reconstruction
* Image Translation
* Generative AI
* Diffusion Models
* Foundation Models
* Large Language Models (LLMs)
* Vision-Language Models (VLMs)
* Multimodal Learning
* Medical Vision-Language Learning
* Medical Image Generation
* Virtual Staining
* Computational Pathology
* Radiology AI
* Clinical Decision Support

### 🧠 Paper Reading

推荐不要只关注“模型用了什么结构”，而是重点回答：

```text
What is the problem?
        ↓
Why does it matter?
        ↓
What are the limitations of previous methods?
        ↓
What is the key idea?
        ↓
Why should the proposed method work?
        ↓
How is it evaluated?
        ↓
Does the evidence really support the claim?
```

---

# 2. 🖥️ Research Environment

一个可靠的科研环境应该同时考虑：

**可用性 + 依赖管理 + 可复现性 + GPU + 远程开发**

### 🐧 Operating System

* [Linux](https://www.linux.org/) — 深度学习与服务器环境基础
* [Ubuntu](https://ubuntu.com/) — 常见科研服务器发行版
* [Windows](https://www.microsoft.com/windows/) — 本地开发与日常使用
* [WSL](https://learn.microsoft.com/windows/wsl/) — Windows 上使用 Linux 环境

### 🐍 Python Environment

* [Python](https://www.python.org/)
* [uv](https://docs.astral.sh/uv/) — 现代 Python 项目与环境管理工具
* [Conda](https://docs.conda.io/)
* [pip](https://pypi.org/project/pip/)
* [venv](https://docs.python.org/3/library/venv.html)

> 在现代 Python 项目中，可以优先考虑 `pyproject.toml` + lockfile 的项目管理方式，而不是依赖一份长期漂移的 `requirements.txt`。

### ⚡ GPU & CUDA

* [NVIDIA CUDA](https://developer.nvidia.com/cuda-toolkit)
* [cuDNN](https://developer.nvidia.com/cudnn)
* [NVIDIA Container Toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/)
* [Docker](https://www.docker.com/)

### ☁️ Remote Research

* SSH
* tmux
* VS Code Remote SSH
* Jupyter
* Docker
* GPU server / workstation
* Cloud GPU

---

# 3. 💻 Programming & Deep Learning

## 3.1 Python Fundamentals

* [Python Tutorial](https://docs.python.org/3/tutorial/)
* [NumPy](https://numpy.org/)
* [Pandas](https://pandas.pydata.org/)
* [Matplotlib](https://matplotlib.org/)
* [Pillow](https://python-pillow.org/)
* [OpenCV](https://opencv.org/)
* [tqdm](https://tqdm.github.io/)
* [dataclasses](https://docs.python.org/3/library/dataclasses.html)

## 3.2 Deep Learning

* [PyTorch](https://pytorch.org/)
* [torchvision](https://pytorch.org/vision/stable/)
* [PyTorch Lightning](https://lightning.ai/)
* [MONAI](https://monai.io/) — 医学影像 AI 开发框架
* [NiBabel](https://nipy.org/nibabel/) — NIfTI 等神经影像数据处理
* [SimpleITK](https://simpleitk.org/) — 医学图像读取、处理与转换

## 3.3 Computer Vision

重点掌握：

* CNN
* Vision Transformer
* Attention
* Object Detection
* Semantic Segmentation
* Instance Segmentation
* Image Registration
* Representation Learning
* Contrastive Learning
* Self-supervised Learning

---

# 4. 🤖 Modern Generative AI

如今的医学 AI 已经不应只围绕传统 CNN 分类与分割展开。

## 4.1 Generative Models

* GAN
* VAE
* Normalizing Flow
* Diffusion Models
* Score-based Models
* Flow Matching
* Rectified Flow
* Bridge / Schrödinger Bridge Models

## 4.2 Diffusion Models

推荐重点理解：

```text
Forward Process
      ↓
Noise / Corruption
      ↓
Denoising Network
      ↓
Reverse Process
      ↓
Generated / Translated Image
```

进一步学习：

* DDPM
* DDIM
* Latent Diffusion
* Conditional Diffusion
* Diffusion Transformer
* Image-to-Image Diffusion
* Video Diffusion
* Diffusion for Medical Imaging
* Diffusion-based Reconstruction
* Diffusion-based Translation
* Diffusion-based Image Enhancement

### 🧰 Tools

* [Hugging Face Diffusers](https://huggingface.co/docs/diffusers/)
* [Hugging Face](https://huggingface.co/)
* [PyTorch](https://pytorch.org/)

---

# 5. 🧠 Foundation Models

医学 AI 正逐渐从“为一个任务训练一个模型”转向：

> **Pretrain → Adapt → Evaluate → Deploy**

### 5.1 Foundation Models

重点关注：

* Vision Foundation Models
* Vision Transformers
* Self-supervised Pretraining
* Large-scale Pretrained Encoders
* Medical Foundation Models
* Domain Adaptation
* Parameter-efficient Fine-tuning

### 5.2 Large Language Models

重点掌握：

* Prompt Engineering
* Structured Output
* Function Calling
* Tool Use
* Retrieval-Augmented Generation
* Long-context Modeling
* LLM-based Information Extraction
* LLM-based Evaluation
* Agentic Workflows

### 5.3 Vision-Language Models

重点关注：

* Image-Text Alignment
* Contrastive Learning
* Visual Question Answering
* Image Captioning
* Medical VQA
* Radiology Report Understanding
* Multimodal Reasoning
* Vision-Language Agents

### 🧰 Recommended Ecosystem

* [Hugging Face Transformers](https://huggingface.co/docs/transformers/)
* [Hugging Face Hub](https://huggingface.co/models)
* [vLLM](https://docs.vllm.ai/)
* [llama.cpp](https://github.com/ggml-org/llama.cpp)
* [PEFT](https://huggingface.co/docs/peft/)

---

# 6. 🏥 Medical AI & Medical Imaging

## 6.1 Medical Imaging

### X-ray / Radiography

* Chest X-ray
* Bone Suppression
* Image Enhancement
* Reconstruction
* Disease Classification
* Abnormality Detection

### CT / MRI

* 2D / 3D Image Processing
* Segmentation
* Registration
* Reconstruction
* Volumetric Analysis

### Ultrasound

* Image Classification
* Segmentation
* Video Analysis
* Reconstruction

### Digital Pathology

* Whole Slide Imaging
* Computational Pathology
* Cell Detection
* Tissue Classification
* Virtual Staining
* Spatial Analysis

## 6.2 Medical AI Tasks

```text
Classification
Detection
Segmentation
Registration
Reconstruction
Generation
Translation
Report Generation
Visual Question Answering
Multimodal Reasoning
Clinical Prediction
```

---

# 7. 📊 Dataset & Data Processing

医学 AI 最大的挑战之一往往并不是模型，而是**数据**。

推荐系统学习：

* Dataset Construction
* Data Cleaning
* Data Annotation
* Data Quality Control
* Patient-level Splitting
* Train / Validation / Test
* Cross-validation
* Data Leakage
* Class Imbalance
* External Validation
* Domain Shift
* Multi-center Validation
* Public Dataset Reproducibility

### 📦 Common Resources

* [The Cancer Imaging Archive (TCIA)](https://www.cancerimagingarchive.net/)
* [PhysioNet](https://physionet.org/)
* [OpenNeuro](https://openneuro.org/)
* [Kaggle](https://www.kaggle.com/)
* [Hugging Face Datasets](https://huggingface.co/datasets)

---

# 8. 📐 Evaluation & Statistical Analysis

一个医学 AI 模型“效果更好”，并不等于实验结果可信。

除了常见指标之外，应该重点学习：

### Classification

* Accuracy
* Precision
* Recall
* F1-score
* AUROC
* AUPRC
* Sensitivity
* Specificity
* Calibration

### Segmentation

* Dice
* IoU
* HD95
* ASSD

### Image Generation / Translation

* PSNR
* SSIM
* LPIPS
* FID
* KID
* NIQE
* BRISQUE

同时注意：

* Statistical Significance
* Confidence Intervals
* Bootstrap
* Wilcoxon Signed-rank Test
* Paired / Unpaired Statistical Tests
* Multiple Comparisons
* Effect Size

### 🧑🏻‍⚕️ Clinical Evaluation

机器指标并不是终点。

进一步学习：

* Reader Study
* Human Evaluation
* Radiologist / Pathologist Assessment
* Inter-rater Agreement
* Cohen's Kappa
* Intraclass Correlation
* Clinical Utility
* External Validation

---

# 9. 🧪 Experimental Design

优秀的医学 AI 论文不只是“模型更复杂”。

应该形成完整的实验链：

```text
Research Question
       ↓
Hypothesis
       ↓
Method
       ↓
Baseline
       ↓
Ablation Study
       ↓
Quantitative Evaluation
       ↓
Qualitative Evaluation
       ↓
Statistical Analysis
       ↓
External / Clinical Validation
       ↓
Conclusion
```

重点关注：

* Strong Baselines
* Fair Comparison
* Ablation Study
* Sensitivity Analysis
* Robustness Analysis
* Generalization
* Computational Cost
* Inference Efficiency
* Failure Cases
* Reproducibility

---

# 10. 🔬 Reproducible Research

如今的医学 AI 科研越来越强调：

> **Can someone else reproduce your result?**

建议所有项目包含：

```text
project/
├── configs/
├── datasets/
├── models/
├── scripts/
├── src/
├── tests/
├── notebooks/
├── README.md
├── pyproject.toml
└── LICENSE
```

同时记录：

* Python version
* PyTorch version
* CUDA version
* GPU
* Random seed
* Dataset version
* Model checkpoint
* Training configuration
* Hyperparameters
* Evaluation protocol

### 🛠️ Recommended Tools

* Git
* GitHub
* Git LFS
* Docker
* uv
* DVC
* Weights & Biases
* MLflow

---

# 11. ✍🏻 Scientific Writing

科研最终需要通过论文、报告与公开代码完成交流。

## 11.1 LaTeX

* [LaTeX](https://www.latex-project.org/)
* [Overleaf](https://www.overleaf.com/)

## 11.2 Markdown

* [Markdown Guide](https://www.markdownguide.org/)
* [GitHub Markdown](https://docs.github.com/en/get-started/writing-on-github)

## 11.3 Scientific Figures

推荐掌握：

* Matplotlib
* Plotly
* Seaborn
* Illustrator
* Inkscape
* PowerPoint
* draw.io
* Mermaid

重点不是“把图做得漂亮”，而是：

> **让读者在最短时间内理解你的方法与实验。**

---

# 12. 🤝 AI-assisted Research

AI 已经逐渐成为科研工作流的一部分，但应该把它作为：

> **Research Assistant，而不是 Research Replacement。**

可以用于：

* Literature Search
* Paper Summarization
* Code Understanding
* Debugging
* Documentation
* Information Extraction
* Data Processing
* Figure Drafting
* Writing Assistance
* Translation
* Brainstorming

同时必须保持：

* Source Verification
* Experimental Verification
* Citation Verification
* Code Verification
* Data Privacy
* Clinical Safety Awareness

**AI 生成的内容永远不能替代研究者对实验结果与科学结论的最终判断。**

---

# 13. 🧰 Essential Tools

| Category               | Tools                                        |
| ---------------------- | -------------------------------------------- |
| 📝 Writing             | LaTeX · Overleaf · Markdown                  |
| 🔬 Research            | Google Scholar · PubMed · arXiv · OpenReview |
| 🐍 Python              | Python · uv · Conda · pip                    |
| 🧠 Deep Learning       | PyTorch · MONAI                              |
| 👁️ Vision             | OpenCV · torchvision · timm                  |
| 🤗 Foundation Models   | Hugging Face · Transformers · Diffusers      |
| 💬 LLM / VLM           | Transformers · vLLM · PEFT                   |
| 🐳 Deployment          | Docker · NVIDIA Container Toolkit            |
| 📈 Experiment Tracking | Weights & Biases · MLflow                    |
| 🔧 Version Control     | Git · GitHub · Git LFS                       |
| 📦 Data                | DVC · Hugging Face Datasets                  |
| 🧪 Statistics          | SciPy · statsmodels · R                      |

---

# 14. 🌐 Useful Resources

### Research Platforms

* [Google Scholar](https://scholar.google.com/)
* [PubMed](https://pubmed.ncbi.nlm.nih.gov/)
* [arXiv](https://arxiv.org/)
* [OpenReview](https://openreview.net/)
* [Semantic Scholar](https://www.semanticscholar.org/)

### Open-source AI

* [GitHub](https://github.com/)
* [Hugging Face](https://huggingface.co/)
* [Papers with Code](https://paperswithcode.com/)

### Medical AI

* [MONAI](https://monai.io/)
* [Project MONAI](https://project-monai.github.io/)
* [The Cancer Imaging Archive](https://www.cancerimagingarchive.net/)
* [PhysioNet](https://physionet.org/)
* [OpenNeuro](https://openneuro.org/)

---

# 👍 Citation

如果本项目对你的学习或研究有所帮助，欢迎引用：

```bibtex
@misc{medicalaiguide2026,
      title        = {Medical-AI-Guide},
      author       = {Sun, Yifei and Medical-AI-Guide Contributors},
      year         = {2026},
      howpublished = {\url{https://github.com/diaoquesang/Medical-AI-Guide/}},
}
```

---

# 🤝 Contributing

Medical-AI-Guide 是一个持续维护的开源项目。

欢迎：

* 补充优质学习资源
* 推荐值得阅读的论文
* 修复错误或过时内容
* 改进教程
* 分享医学 AI 实践经验

欢迎通过 Issue / Pull Request 参与项目。

📧 Contributor Application: [diaoquesang@gmail.com](mailto:diaoquesang@gmail.com)

---

<h2 align="center">🌱 Learn → Research → Reproduce → Share</h2>

<p align="center">
  <i>Build better models. Ask better questions. Do better science.</i>
</p>

---

## ⭐ Star History

[![Star History Chart](https://api.star-history.com/svg?repos=diaoquesang/Medical-AI-Guide\&type=Date)](https://star-history.com/#diaoquesang/Medical-AI-Guide&Date)

