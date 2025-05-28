# OpenCV 教程：计算机视觉基础与实战

OpenCV（Open Source Computer Vision Library）是一个开源的计算机视觉库，广泛用于图像处理、视频分析、物体检测等领域。以下是快速上手 OpenCV 的教程。

---

## 目录

1. [安装与环境配置](#安装与环境配置)  
2. [图像基础操作](#图像基础操作)  
3. [颜色空间与阈值处理](#颜色空间与阈值处理)  
4. [边缘检测与轮廓分析](#边缘检测与轮廓分析)  
5. [滤波与形态学操作](#滤波与形态学操作)  
6. [视频处理](#视频处理)  
7. [注意事项](#注意事项)  

---

## 安装与环境配置

```bash
# 使用 pip 安装
pip install opencv-python  # 基础包
pip install opencv-contrib-python  # 包含额外模块（如 SIFT）

# 使用 conda 安装
conda install -c conda-forge opencv

# 验证安装
python -c "import cv2; print(cv2.__version__)"
```

---

## 图像基础操作

### 1. 读取与显示图像

```python
import cv2

# 读取图像
img = cv2.imread('image.jpg')  # 默认 BGR 格式
if img is None:
    print("图像加载失败！")

# 显示图像
cv2.imshow('Image', img)
cv2.waitKey(0)  # 等待按键
cv2.destroyAllWindows()
```

### 2. 图像属性与保存

```python
# 获取图像尺寸和通道数
print(img.shape)  # 输出: (height, width, channels)

# 保存图像
cv2.imwrite('output.jpg', img)
```

### 3. 调整图像尺寸

```python
resized = cv2.resize(img, (new_width, new_height))
```

---

## 颜色空间与阈值处理

### 1. 颜色空间转换

```python
# BGR 转 RGB
rgb_img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)

# BGR 转灰度图
gray_img = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
```

### 2. 阈值处理（二值化）

```python
# 全局阈值
_, binary = cv2.threshold(gray_img, thresh=127, maxval=255, type=cv2.THRESH_BINARY)

# 自适应阈值
adaptive_binary = cv2.adaptiveThreshold(
    gray_img, 255, 
    cv2.ADAPTIVE_THRESH_GAUSSIAN_C, 
    cv2.THRESH_BINARY, 
    blockSize=11, 
    C=2
)
```

---

## 边缘检测与轮廓分析

### 1. Canny 边缘检测

```python
edges = cv2.Canny(gray_img, threshold1=100, threshold2=200)
```

### 2. 轮廓检测

```python
# 查找轮廓
contours, _ = cv2.findContours(binary, mode=cv2.RETR_EXTERNAL, method=cv2.CHAIN_APPROX_SIMPLE)

# 绘制轮廓
contour_img = cv2.drawContours(img.copy(), contours, -1, (0, 255, 0), 2)
```

---

## 滤波与形态学操作

### 1. 均值滤波（去噪）

```python
blurred = cv2.blur(img, ksize=(5, 5))
```

### 2. 高斯滤波（保留边缘）

```python
gaussian_blur = cv2.GaussianBlur(img, (5, 5), sigmaX=0)
```

### 3. 形态学操作（膨胀与腐蚀）

```python
kernel = cv2.getStructuringElement(cv2.MORPH_RECT, (5, 5))

# 膨胀（扩大前景）
dilated = cv2.dilate(binary, kernel, iterations=1)

# 腐蚀（缩小前景）
eroded = cv2.erode(dilated, kernel, iterations=1)
```

---

## 视频处理

### 1. 实时视频捕获

```python
cap = cv2.VideoCapture(0)  # 0 表示默认摄像头

while True:
    ret, frame = cap.read()
    if not ret:
        break
    
    # 处理帧（例如灰度化）
    gray_frame = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
    
    # 显示帧
    cv2.imshow('Video', gray_frame)
    
    if cv2.waitKey(1) == 27:  # 按 ESC 键退出
        break

cap.release()
cv2.destroyAllWindows()
```

### 2. 保存视频

```python
fourcc = cv2.VideoWriter_fourcc(*'XVID')  # 编码格式
out = cv2.VideoWriter('output.avi', fourcc, 20.0, (width, height))

while cap.isOpened():
    ret, frame = cap.read()
    if not ret:
        break
    out.write(frame)  # 写入帧

out.release()
```

---

## 注意事项

1. **路径问题**：确保图像/视频路径正确，OpenCV 不会抛出异常而是返回 `None`。
2. **颜色空间**：OpenCV 默认使用 BGR 而非 RGB，显示或保存时需转换。
3. **坐标顺序**：OpenCV 的图像坐标是 (width, height)，而 NumPy 是 (height, width)。
4. **性能优化**：
   - 避免在循环中频繁调用 `cv2.imshow()` 或 `print()`。
   - 使用 NumPy 数组操作替代 Python 循环。
5. **SIFT/SURF 算法**：
   - 需安装 `opencv-contrib-python` 包。
   - 可能受专利保护，生产环境需谨慎使用。

---

## 总结

OpenCV 提供了丰富的图像和视频处理工具，适用于从基础图像操作到复杂计算机视觉任务。关键点总结：

- **图像处理**：读取、显示、保存、调整尺寸。
- **颜色与阈值**：颜色空间转换、二值化处理。
- **边缘与轮廓**：Canny 边缘检测、轮廓分析。
- **滤波与形态学**：去噪、膨胀/腐蚀。
- **视频处理**：实时捕获、保存视频。

**进一步学习**:
- [OpenCV 官方文档](https://docs.opencv.org/4.x/)
- [OpenCV-Python 教程](https://opencv-python-tutroals.readthedocs.io/en/latest/)
- 推荐书籍：《学习 OpenCV 4》（作者：Gary Bradski & Adrian Kaehler）
