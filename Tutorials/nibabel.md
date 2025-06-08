# NiBabel 教程：神经影像数据处理入门

> **NiBabel** 是 Python 中用于处理神经影像格式（如 NIfTI、Analyze、MINC 等）的核心库。它广泛应用于脑成像数据的读取、写入、转换和分析。本教程将带你快速掌握其核心功能。

---

## 📦 1. 安装 NiBabel

### 1.1 使用 pip 安装
```bash
pip install nibabel
```

### 1.2 使用 conda 安装
```bash
conda install -c conda-forge nibabel
```

---

## 🧩 2. 核心概念

### 2.1 NIfTI 文件结构
- **Header**：包含元数据（如维度、数据类型、仿射变换矩阵等）。
- **Data**：多维数组（如 3D 脑部图像或 4D 时间序列）。
- **Affine**：4x4 矩阵，定义体素坐标到世界坐标的映射。

### 2.2 数据维度
- 3D 图像：`(x, y, z)`，如 T1 加权解剖图。
- 4D 图像：`(x, y, z, t)`，如 fMRI 时间序列。

---

## 📖 3. 基础操作

### 3.1 读取 NIfTI 文件
```python
import nibabel as nib

# 加载图像
img = nib.load('data/example.nii.gz')

# 获取数据（返回 numpy 数组）
data = img.get_fdata()

# 查看形状和数据类型
print(data.shape)  # 例如 (128, 128, 64)
print(data.dtype)  # 例如 float32
```

### 3.2 写入 NIfTI 文件
```python
# 创建新的 NIfTI 图像
new_img = nib.Nifti1Image(data, affine=img.affine)

# 保存到文件
nib.save(new_img, 'output/new_image.nii.gz')
```

### 3.3 访问元数据
```python
# 获取仿射矩阵
affine = img.affine

# 获取 Header 信息
header = img.header

# 打印所有元数据
print(header)
```

---

## 🛠️ 4. 数据处理

### 4.1 提取单个体素时间序列（4D 数据）
```python
# 假设 data 是 4D 数组 (x, y, z, t)
x, y, z, t = 60, 60, 30, 100  # 指定体素坐标
time_series = data[x, y, z, :]
print(time_series.shape)  # 输出 (t,)
```

### 4.2 切片可视化（使用 matplotlib）
```python
import matplotlib.pyplot as plt

# 取一个中间切片（如 Z=30）
slice_data = data[:, :, 30]

plt.imshow(slice_data, cmap='gray')
plt.title("Axial Slice (Z=30)")
plt.axis('off')
plt.show()
```

### 4.3 数据归一化
```python
import numpy as np

# 对每个体素进行 Z-score 归一化
mean = np.mean(data, axis=-1, keepdims=True)
std = np.std(data, axis=-1, keepdims=True)
normalized_data = (data - mean) / (std + 1e-6)  # 防止除零
```

---

## 📈 5. 进阶功能

### 5.1 格式转换（NIfTI → Numpy）
```python
# 保存为 .npy 文件
np.save('data.npy', data)

# 从 .npy 加载
loaded_data = np.load('data.npy')
```

### 5.2 仿射变换（坐标映射）
```python
# 将体素坐标 (i, j, k) 转换为世界坐标
voxel_coords = [60, 60, 30, 1]  # 注意末尾的 1
world_coords = img.affine @ voxel_coords  # 矩阵乘法
print(world_coords[:3])  # 输出世界坐标 (x, y, z)
```

### 5.3 合并多个 NIfTI 文件
```python
from nilearn.image import concat_imgs

# 合并多个 3D 图像为 4D 图像
img1 = nib.load('img1.nii.gz')
img2 = nib.load('img2.nii.gz')
combined_img = concat_imgs([img1, img2])
nib.save(combined_img, 'combined.nii.gz')
```

---

## 📌 6. 常见问题

### Q1: 为什么 `img.get_data()` 报错？
- **原因**：NiBabel 3.0+ 已弃用 `.get_data()`，改用 `.get_fdata()`。
- **解决方案**：升级代码使用 `img.get_fdata()`。

### Q2: 如何修复仿射矩阵不一致？
- **问题**：多个图像的 `affine` 矩阵不匹配导致配准失败。
- **解决**：使用 `nilearn.image.resample_img` 统一分辨率：
  ```python
  from nilearn.image import resample_img

  # 将 img2 重采样到 img1 的空间
  resampled_img = resample_img(img2, target_affine=img1.affine, target_shape=img1.shape)
  ```

---

## 📚 7. 学习资源

- [NiBabel 官方文档](https://nipy.org/nibabel/)
- [Neuroimaging in Python 教程](https://github.com/nipy/nibabel/tree/master/doc)
- [BIDS 标准规范](https://bids.neuroimaging.io/)（推荐结合使用）
