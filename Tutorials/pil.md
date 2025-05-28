# PIL 教程：Python 图像处理终极指南

PIL（Python Imaging Library）是 Python 中用于图像处理的核心库，但已停止维护。**当前推荐使用其分支 Pillow**，完全兼容 PIL 并持续更新。以下是针对图像处理的完整教程。

---

## 目录

1. [安装与历史背景](#安装与历史背景)  
2. [核心模块与功能](#核心模块与功能)  
3. [图像基础操作](#图像基础操作)  
4. [图像处理技巧](#图像处理技巧)  
5. [高级功能](#高级功能)  
6. [实战案例](#实战案例)  
7. [注意事项](#注意事项)  

---

## 安装与历史背景

### 1. 安装 Pillow（现代替代品）

```bash
# 安装 Pillow（兼容 PIL 的所有功能）
pip install pillow
```

### 2. 历史背景

- **PIL**：原作者 Fredrik Lundh 于 1995 年开发，2011 年停止维护。
- **Pillow**：社区维护的分支，自 2010 年起成为事实标准，支持 Python 3.x 和现代图像格式。

---

## 核心模块与功能

### 1. 主要模块

| 模块名            | 功能说明                     |
|-------------------|------------------------------|
| `Image`           | 核心图像加载/保存/创建       |
| `ImageFilter`     | 图像滤波器（模糊、锐化等）   |
| `ImageEnhance`    | 图像增强（亮度、对比度等）   |
| `ImageDraw`       | 图像绘图（绘制线条、文本等） |
| `ImageOps`        | 高级图像操作（自动对比度等） |

### 2. 支持的图像格式

- **输入格式**：JPEG、PNG、GIF、BMP、WebP、TIFF、ICO 等 50+ 种
- **输出格式**：JPEG、PNG、BMP、WebP、PPM、PGM、PBM 等

---

## 图像基础操作

### 1. 打开与保存图像

```python
from PIL import Image

# 打开图像
img = Image.open('input.jpg')

# 显示图像
img.show()

# 保存为其他格式
img.save('output.png')
```

### 2. 获取图像信息

```python
print(img.format)      # 格式: JPEG
print(img.size)        # 尺寸: (width, height)
print(img.mode)        # 模式: RGB/L/P 等
print(img.info)        # 元数据字典
```

### 3. 调整尺寸与旋转

```python
# 调整尺寸
resized = img.resize((128, 128))

# 保持宽高比缩放
resized = img.resize((new_width, new_height), Image.ANTIALIAS)

# 旋转图像
rotated = img.rotate(45)  # 45 度
```

---

## 图像处理技巧

### 1. 颜色空间转换

```python
# RGB -> 灰度图
gray = img.convert('L')

# RGB -> HSV
hsv = img.convert('HSV')

# 单通道提取
r, g, b = img.split()
```

### 2. 图像滤镜

```python
from PIL import ImageFilter

# 模糊
blurred = img.filter(ImageFilter.BLUR)

# 锐化
sharpened = img.filter(ImageFilter.SHARPEN)

# 边缘检测
edges = img.filter(ImageFilter.FIND_EDGES)
```

### 3. 图像增强

```python
from PIL import ImageEnhance

# 亮度增强
enhancer = ImageEnhance.Brightness(img)
bright = enhancer.enhance(2.0)  # 2.0 表示两倍亮度

# 对比度增强
enhancer = ImageEnhance.Contrast(img)
contrast = enhancer.enhance(1.5)

# 饱和度增强
enhancer = ImageEnhance.Color(img)
color = enhancer.enhance(1.5)
```

---

## 高级功能

### 1. 图像合成与叠加

```python
# 创建新图像
new_img = Image.new('RGB', (256, 256), color=(255, 0, 0))  # 红色背景

# 图像叠加
mask = Image.new('L', (256, 256), 128)  # 半透明遮罩
Image.composite(img1, img2, mask)  # 使用遮罩合成
```

### 2. 绘图功能

```python
from PIL import ImageDraw, ImageFont

draw = ImageDraw.Draw(img)
# 绘制矩形
draw.rectangle([10, 10, 100, 100], outline='red', width=3)
# 绘制文本
try:
    font = ImageFont.truetype("arial.ttf", 24)  # 指定字体
except:
    font = ImageFont.load_default()
draw.text((10, 10), "Hello World", fill=(255, 255, 255), font=font)
```

### 3. 动画处理（如 GIF）

```python
# 读取动画帧
img = Image.open('animation.gif')
for frame in range(img.n_frames):
    img.seek(frame)
    # 处理每一帧...

# 保存为动画
frames = [frame.convert('RGB') for frame in frames]
frames[0].save('output.gif', save_all=True, append_images=frames[1:], duration=100, loop=0)
```

---

## 实战案例

### 1. 批量处理图像

```python
import os

def batch_resize(folder, size=(128, 128)):
    for filename in os.listdir(folder):
        if filename.lower().endswith(('.png', '.jpg')):
            img = Image.open(os.path.join(folder, filename))
            img = img.resize(size, Image.ANTIALIAS)
            img.save(os.path.join(folder, 'resized_' + filename))

batch_resize('./images')
```

### 2. 添加水印

```python
def add_watermark(input_path, output_path, watermark_path):
    base = Image.open(input_path).convert('RGBA')
    watermark = Image.open(watermark_path).convert('RGBA')
    watermark = watermark.resize((100, 100))
    position = (base.width - watermark.width, base.height - watermark.height)
    transparent = Image.new('RGBA', base.size, (0,0,0,0))
    transparent.paste(base, (0,0))
    transparent.paste(watermark, position, mask=watermark)
    transparent.convert('RGB').save(output_path)

add_watermark('input.jpg', 'output.jpg', 'logo.png')
```

---

## 注意事项

1. **版本兼容性**：
   - **Pillow 9+** 已移除 `Image.OPEN` 等旧式 API，使用 `Image.open()` 替代
   - 使用 `pip install pillow==8.4.0` 回退旧版本（不推荐）

2. **文件格式限制**：
   - 读取 RAW 格式需安装额外依赖（如 `libraw`）
   - 保存 WebP 需安装 `libwebp`

3. **性能优化**：
   - 大图像处理时使用 `Image.thumbnail()` 而非 `resize()`
   - 启用 `ImageFile.LOAD_TRUNCATED_IMAGES = True` 处理损坏图片

4. **内存管理**：
   ```python
   from PIL import ImageFile
   ImageFile.LOAD_TRUNCATED_IMAGES = True  # 允许加载部分损坏图像
   ```

5. **多线程安全**：
   - Pillow 的 `Image.open()` 不是线程安全的，建议使用进程池替代线程池

---

## 总结

Pillow 的核心优势在于：

- **易用性**：简洁的 API，适合快速实现图像处理需求
- **跨平台**：兼容 Windows/macOS/Linux
- **生态系统**：与 NumPy、OpenCV、Matplotlib 无缝集成
- **活跃维护**：每月发布新版本，持续支持现代图像格式

**进一步学习**:
- [Pillow 官方文档](https://pillow.readthedocs.io/en/stable/)
- [Python 图像处理教程合集](https://realpython.com/tutorials/images/)
- 推荐书籍：《Python 图像处理实战》（作者：Michael Crump）
