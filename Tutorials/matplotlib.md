# Matplotlib 教程：Python 数据可视化终极指南

Matplotlib 是 Python 最流行的 2D 绘图库，广泛用于科学计算、数据分析和可视化。以下是快速掌握 Matplotlib 的完整教程。

---

## 目录

1. [安装与基础配置](#安装与基础配置)  
2. [绘图基础](#绘图基础)  
3. [常用图表类型](#常用图表类型)  
4. [样式与美化](#样式与美化)  
5. [子图与布局](#子图与布局)  
6. [高级功能](#高级功能)  
7. [保存图像](#保存图像)  
8. [注意事项](#注意事项)  

---

## 安装与基础配置

```bash
# 使用 pip 安装
pip install matplotlib

# 使用 conda 安装
conda install -c conda-forge matplotlib
```

```python
import matplotlib.pyplot as plt
import numpy as np

# 设置默认风格（可选）
plt.style.use('ggplot')  # 或 'seaborn', 'classic' 等
```

---

## 绘图基础

### 1. 折线图（Line Plot）

```python
x = np.linspace(0, 10, 100)
y = np.sin(x)

plt.figure(figsize=(10, 6))  # 设置画布大小
plt.plot(x, y, label='sin(x)', color='blue', linestyle='--', linewidth=2)
plt.title('Sine Wave')
plt.xlabel('X-axis')
plt.ylabel('Y-axis')
plt.grid(True)
plt.legend()
plt.show()
```

### 2. 基本元素说明

| 元素       | 说明                     |
|------------|--------------------------|
| figure     | 整个图像（画布）         |
| axes       | 子图（包含坐标轴、标签） |
| axis       | 单个坐标轴（X/Y/Z轴）    |
| spines     | 坐标轴脊柱               |

---

## 常用图表类型

### 1. 柱状图（Bar Chart）

```python
categories = ['A', 'B', 'C']
values = [3, 7, 5]

plt.bar(categories, values, color=['red', 'green', 'blue'], width=0.6)
plt.title('Bar Chart')
plt.ylabel('Values')
plt.show()
```

### 2. 散点图（Scatter Plot）

```python
x = np.random.rand(50)
y = np.random.rand(50)
sizes = np.random.randint(10, 200, 50)

plt.scatter(x, y, s=sizes, c=y, cmap='viridis', alpha=0.6)
plt.colorbar(label='Y Value')
plt.title('Scatter Plot')
plt.show()
```

### 3. 直方图（Histogram）

```python
data = np.random.randn(1000)
plt.hist(data, bins=30, color='skyblue', edgecolor='black', alpha=0.7)
plt.title('Histogram')
plt.xlabel('Value')
plt.ylabel('Frequency')
plt.show()
```

### 4. 饼图（Pie Chart）

```python
labels = ['A', 'B', 'C']
sizes = [25, 35, 40]
plt.pie(sizes, labels=labels, autopct='%1.1f%%', startangle=90)
plt.axis('equal')  # 保持圆形
plt.title('Pie Chart')
plt.show()
```

---

## 样式与美化

### 1. 线条样式

```python
plt.plot(x, y, 
         color='red',       # 颜色
         linestyle='--',    # 虚线
         marker='o',        # 标记点
         markersize=8,      # 标记大小
         markerfacecolor='yellow')
```

### 2. 颜色映射（Colormap）

```python
plt.imshow(np.random.rand(10,10), cmap='hot')
plt.colorbar()
plt.title('Colormap: hot')
plt.show()
```

### 3. 数学公式支持（LaTeX）

```python
plt.title(r'$\alpha > \beta$')  # 使用 LaTeX 语法
plt.xlabel('Time ($t$)')
plt.ylabel('Amplitude ($A$)')
```

---

## 子图与布局

### 1. 使用 `subplots`

```python
fig, axes = plt.subplots(nrows=2, ncols=2, figsize=(10, 8))

axes[0, 0].plot(x, np.sin(x))
axes[0, 1].plot(x, np.cos(x))
axes[1, 0].plot(x, np.tan(x))
axes[1, 1].plot(x, x**2)

plt.tight_layout()  # 自动调整布局
plt.show()
```

### 2. GridSpec 布局

```python
from matplotlib.gridspec import GridSpec

fig = plt.figure(figsize=(8, 6))
gs = GridSpec(2, 2)

ax1 = fig.add_subplot(gs[0, :])  # 第一行跨两列
ax2 = fig.add_subplot(gs[1, 0])
ax3 = fig.add_subplot(gs[1, 1])

ax1.plot(x, np.sin(x))
ax2.plot(x, np.cos(x))
ax3.plot(x, x**2)
plt.tight_layout()
plt.show()
```

---

## 高级功能

### 1. 注释与文本

```python
plt.plot(x, y)
plt.annotate('Max Point', 
             xy=(np.pi/2, 1), 
             xytext=(np.pi/2+1, 0.5),
             arrowprops=dict(facecolor='black'))
plt.text(5, 0, 'Important Note', fontsize=12, color='red')
```

### 2. 双坐标轴

```python
fig, ax1 = plt.subplots()
ax2 = ax1.twinx()

ax1.plot(x, y, 'g-')
ax2.plot(x, y*2, 'b-')

ax1.set_xlabel('X')
ax1.set_ylabel('Y (green)')
ax2.set_ylabel('2Y (blue)')
plt.show()
```

### 3. 动态更新（实时绘图）

```python
plt.ion()  # 开启交互模式
fig, ax = plt.subplots()
x, y = [], []

for i in range(100):
    x.append(i)
    y.append(np.sin(i/10))
    ax.clear()
    ax.plot(x, y)
    plt.pause(0.1)
```

---

## 保存图像

```python
plt.savefig('output.png', dpi=300, bbox_inches='tight', transparent=True)
# 支持格式：png, pdf, svg, jpg 等
```

---

## 注意事项

1. **中文显示问题**：
   ```python
   plt.rcParams['font.sans-serif'] = ['SimHei']  # 设置中文
   plt.rcParams['axes.unicode_minus'] = False    # 正常显示负号
   ```

2. **坐标轴截断**：
   ```python
   plt.xlim(0, 10)    # 限制 X 轴范围
   plt.ylim(-1, 1)    # 限制 Y 轴范围
   ```

3. **图例位置调整**：
   ```python
   plt.legend(loc='upper left', bbox_to_anchor=(1,1))  # 右上角
   ```

4. **后端选择**：
   - Jupyter Notebook 使用 `%matplotlib inline`
   - GUI 应用推荐使用 TkAgg/WxAgg 后端
   - 服务器环境建议使用 Agg（无头模式）

5. **性能优化**：
   - 大数据量绘图时使用 `set_data()` 而非重复调用 `plot()`
   - 关闭交互模式：`plt.ioff()`
   - 简化图表元素（如减少标记点）

---

## 总结

Matplotlib 提供了完整的 2D 可视化解决方案，核心优势在于：

- **灵活性**：支持从基础图表到复杂定制的可视化需求
- **兼容性**：与 NumPy、Pandas、Seaborn 等库无缝集成
- **扩展性**：可通过 `mpl_toolkits` 实现 3D 绘图、动画等功能

**进一步学习**:
- [Matplotlib 官方文档](https://matplotlib.org/stable/index.html)
- [Matplotlib 教程合集](https://matplotlib.org/stable/tutorials/index.html)
- 推荐书籍：《Python for Data Analysis》（作者：Wes McKinney）
