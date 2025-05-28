# NumPy 教程：Python 科学计算核心库

NumPy 是 Python 中用于科学计算和数据分析的基础库，提供了高效的多维数组（`ndarray`）和丰富的数学函数。以下是快速上手 NumPy 的详细教程。

---

## 目录

1. [安装与导入](#安装与导入)  
2. [数组创建与属性](#数组创建与属性)  
3. [数组操作](#数组操作)  
4. [广播机制（Broadcasting）](#广播机制broadcasting)  
5. [索引与切片](#索引与切片)  
6. [常用函数与统计计算](#常用函数与统计计算)  
7. [线性代数运算](#线性代数运算)  
8. [随机模块（Random）](#随机模块random)  
9. [注意事项](#注意事项)  

---

## 安装与导入

```bash
# 使用 pip 安装
pip install numpy

# 使用 conda 安装
conda install -c conda-forge numpy
```

```python
import numpy as np
```

---

## 数组创建与属性

### 1. 创建数组

```python
# 从列表创建
a = np.array([1, 2, 3])                # 一维数组
b = np.array([[1, 2], [3, 4]])         # 二维数组

# 预设函数创建
zeros = np.zeros((3, 4))               # 全零数组
ones = np.ones((2, 3), dtype=np.int8)  # 指定数据类型
random_arr = np.random.rand(2, 3)      # 随机数组（0~1）
range_arr = np.arange(0, 10, 2)        # 类似 range，输出: [0 2 4 6 8]
linspace_arr = np.linspace(0, 1, 5)    # 等差数列（包含端点）
```

### 2. 数组属性

```python
arr = np.array([[1, 2, 3], [4, 5, 6]])

print(arr.ndim)        # 维度数量: 2
print(arr.shape)       # 形状: (2, 3)
print(arr.dtype)       # 数据类型: int64
print(arr.size)        # 总元素数: 6
print(arr.itemsize)    # 单个元素字节大小: 8（int64）
```

---

## 数组操作

### 1. 类型转换与重塑

```python
arr = np.array([1, 2, 3], dtype=np.float32)
arr.astype(np.int32)  # 转换为整数类型

# 重塑数组
arr.reshape(3, 1)     # 变为 3 行 1 列
arr.resize((3, 1))    # 原地修改形状（注意与 reshape 区别）
```

### 2. 数组拼接与分割

```python
a = np.array([[1, 2], [3, 4]])
b = np.array([[5, 6], [7, 8]])

# 拼接
np.concatenate((a, b), axis=0)  # 按行拼接
np.vstack((a, b))              # 垂直拼接
np.hstack((a, b))              # 水平拼接

# 分割
np.split(a, 2, axis=0)         # 按行分割为两部分
```

---

## 广播机制（Broadcasting）

### 1. 基本规则

当操作两个形状不同的数组时，NumPy 会自动广播较小的数组以匹配较大数组的形状：

```python
a = np.array([[1, 2, 3], [4, 5, 6]])
b = np.array([10, 20, 30])

result = a + b  # b 被广播为 [[10,20,30], [10,20,30]]
```

### 2. 无效广播示例

```python
a = np.array([[1, 2], [3, 4]])
b = np.array([10, 20, 30])
a + b  # 报错: "operands could not be broadcast together"
```

---

## 索引与切片

### 1. 基本索引

```python
arr = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])

# 一维索引
arr[0]      # 第一行: [1 2 3]

# 二维索引
arr[1, 2]   # 第二行第三列: 6

# 布尔索引
arr[arr > 5]  # 所有大于 5 的元素: [6 7 8 9]
```

### 2. 切片操作

```python
# 一维切片
arr[0, 1:3]    # 第一行第 2~3 列: [2 3]

# 多维切片
arr[1:, :2]    # 第二行开始，前两列:
               # [[4 5]
               #  [7 8]]
```

---

## 常用函数与统计计算

### 1. 数学运算

```python
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

np.add(a, b)        # 加法: [5 7 9]
np.subtract(a, b)   # 减法: [-3 -3 -3]
np.multiply(a, b)   # 乘法: [4 10 18]
np.divide(b, a)     # 除法: [4.  2.5 2. ]
np.power(a, 2)      # 平方: [1 4 9]
```

### 2. 统计函数

```python
arr = np.array([[1, 2], [3, 4]])

np.sum(arr)         # 所有元素和: 10
np.mean(arr)        # 平均值: 2.5
np.std(arr)         # 标准差: 1.118...
np.min(arr, axis=0) # 每列最小值: [1 2]
np.max(arr, axis=1) # 每行最大值: [2 4]
```

---

## 线性代数运算

### 1. 矩阵乘法

```python
a = np.array([[1, 2], [3, 4]])
b = np.array([[5, 6], [7, 8]])

np.dot(a, b)        # 矩阵乘法
a @ b               # Python 3.5+ 的简写
```

### 2. 逆矩阵与行列式

```python
a = np.array([[1, 2], [3, 4]])

np.linalg.inv(a)    # 逆矩阵（要求矩阵可逆）
np.linalg.det(a)    # 行列式: -2.0
```

### 3. 特征值与特征向量

```python
w, v = np.linalg.eig(a)
print("特征值:", w)
print("特征向量:", v)
```

---

## 随机模块（Random）

### 1. 常用分布生成

```python
np.random.rand(2, 3)       # 均匀分布（0~1）
np.random.randn(2, 3)      # 正态分布（均值 0，方差 1）
np.random.randint(1, 10, size=(3, 4))  # 整数随机数
np.random.choice([1,2,3,4], size=5, p=[0.1,0.2,0.3,0.4])  # 按概率抽样
```

### 2. 随机种子设置

```python
np.random.seed(42)  # 设置随机种子以保证结果可复现
```

---

## 注意事项

1. **数据类型一致性**：NumPy 数组所有元素必须是同一类型，混合类型会自动转换：
   ```python
   arr = np.array([1, 2.0, 3])  # 所有元素转为 float64
   ```

2. **内存共享问题**：切片操作返回视图（view），修改会影响原数组：
   ```python
   a = np.array([1, 2, 3])
   b = a[1:]
   b[0] = 10
   print(a)  # 输出: [ 1 10  3]
   ```

3. **浮点数精度问题**：避免直接比较浮点数：
   ```python
   np.allclose(0.1 + 0.2, 0.3)  # True
   ```

4. **性能优化**：
   - 避免使用 Python 循环，优先使用向量化操作。
   - 大数组操作时注意内存占用。

5. **与 PyTorch/TensorFlow 互操作**：
   ```python
   import torch
   torch_tensor = torch.from_numpy(np_array)  # 共享内存
   np_array = torch_tensor.numpy()
   ```

---

## 总结

NumPy 是 Python 科学计算的基石，核心优势在于：

- **高效的多维数组**：`ndarray` 支持大规模数据存储和快速计算。
- **广播机制**：简化不同形状数组的运算。
- **丰富的数学函数**：涵盖线性代数、统计、随机等。
- **兼容性**：与 Pandas、Matplotlib、PyTorch 等库无缝集成。

**进一步学习**:
- [NumPy 官方文档](https://numpy.org/doc/)
- [NumPy 教程合集](https://numpy.org/learn/)
- 推荐书籍：《利用 Python 进行数据分析》（作者：Wes McKinney）
