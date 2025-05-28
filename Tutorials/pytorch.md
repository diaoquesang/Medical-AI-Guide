# PyTorch 教程：深度学习框架快速上手指南

PyTorch 是由 Facebook 开发的开源深度学习框架，以动态计算图（Dynamic Computation Graph）和易用性著称。以下是针对初学者的核心功能教程。

---

## 目录

1. [安装与环境配置](#安装与环境配置)  
2. [张量（Tensor）基础](#张量tensor基础)  
3. [自动求导（Autograd）](#自动求导autograd)  
4. [数据处理（Dataset & DataLoader）](#数据处理dataset--dataloader)  
5. [模型构建与训练](#模型构建与训练)  
6. [高级功能](#高级功能)  
7. [注意事项](#注意事项)  

---

## 安装与环境配置

```bash
# 安装 CPU 版本
pip install torch

# 安装 CUDA 支持版本（根据显卡型号选择）
pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118

# 验证安装
python -c "import torch; print(torch.__version__, torch.cuda.is_available())"
```

---

## 张量（Tensor）基础

### 1. 创建张量

```python
import torch

# 从列表创建
x = torch.tensor([[1, 2], [3, 4]])

# 创建随机张量
rand_tensor = torch.rand(2, 3)  # 形状为 (2,3) 的随机数
zeros = torch.zeros(3, 4)       # 全零张量
ones = torch.ones(5,)          # 一维全一张量

# 与 NumPy 互操作
import numpy as np
np_array = np.random.rand(2, 2)
torch_tensor = torch.from_numpy(np_array)
```

### 2. 张量操作

```python
# 形状变换
x = torch.rand(2, 3)
print(x.view(3, 2))       # 形状改变
print(x.reshape(3, 2))    # 更安全的 reshape

# 运算
a = torch.tensor([1, 2])
b = torch.tensor([3, 4])
print(a + b)              # 加法
print(torch.matmul(a, b)) # 矩阵乘法

# GPU 加速
device = "cuda" if torch.cuda.is_available() else "cpu"
x = x.to(device)  # 将张量移动到 GPU
```

---

## 自动求导（Autograd）

### 1. 基本用法

```python
x = torch.tensor([2.0], requires_grad=True)
y = x ** 2 + 3 * x + 1

# 反向传播
y.backward()
print(x.grad)  # 输出: tensor([7.])
```

### 2. 禁用梯度计算

```python
with torch.no_grad():
    z = x * 2  # 此操作不会记录梯度
```

---

## 数据处理（Dataset & DataLoader）

### 1. 自定义数据集

```python
from torch.utils.data import Dataset

class CustomDataset(Dataset):
    def __init__(self, data, labels):
        self.data = data
        self.labels = labels

    def __len__(self):
        return len(self.data)

    def __getitem__(self, idx):
        return self.data[idx], self.labels[idx]
```

### 2. 数据加载器

```python
from torch.utils.data import DataLoader

dataset = CustomDataset(
    data=torch.randn(100, 3),
    labels=torch.randint(0, 2, (100,))
)

loader = DataLoader(dataset, batch_size=16, shuffle=True)
for batch in loader:
    inputs, targets = batch
    # 训练逻辑
```

---

## 模型构建与训练

### 1. 定义神经网络

```python
import torch.nn as nn

class SimpleNet(nn.Module):
    def __init__(self):
        super().__init__()
        self.layers = nn.Sequential(
            nn.Linear(10, 50),
            nn.ReLU(),
            nn.Linear(50, 1)
        )

    def forward(self, x):
        return self.layers(x)

model = SimpleNet().to(device)
```

### 2. 损失函数与优化器

```python
criterion = nn.MSELoss()
optimizer = torch.optim.Adam(model.parameters(), lr=0.001)
```

### 3. 训练循环

```python
for epoch in range(10):
    for inputs, targets in loader:
        inputs, targets = inputs.to(device), targets.to(device)
        
        # 前向传播
        outputs = model(inputs)
        loss = criterion(outputs, targets)

        # 反向传播
        optimizer.zero_grad()
        loss.backward()
        optimizer.step()

    print(f"Epoch {epoch+1}, Loss: {loss.item():.4f}")
```

---

## 高级功能

### 1. 保存与加载模型

```python
# 保存
torch.save(model.state_dict(), "model.pth")

# 加载
model = SimpleNet()
model.load_state_dict(torch.load("model.pth"))
model.eval()  # 设置为评估模式
```

### 2. 设备管理（CPU/GPU）

```python
device = torch.device("cuda" if torch.cuda.is_available() else "cpu")
model = model.to(device)  # 移动模型到 GPU
```

### 3. 自定义层

```python
class CustomLayer(nn.Module):
    def __init__(self):
        super().__init__()
        self.weight = nn.Parameter(torch.randn(1))

    def forward(self, x):
        return x * self.weight
```

---

## 注意事项

1. **张量形状匹配**：确保运算中的张量形状兼容，否则会抛出 `size mismatch` 错误。
2. **设备一致性**：张量和模型需在相同设备（CPU/GPU）上，否则抛出 `device not match` 错误。
3. **梯度清零**：每次反向传播前调用 `optimizer.zero_grad()`，否则梯度会累加。
4. **评估模式**：模型预测时使用 `model.eval()` 禁用 dropout 和 batch normalization。
5. **随机种子**：设置随机种子保证实验可复现：

   ```python
   torch.manual_seed(42)
   if torch.cuda.is_available():
       torch.cuda.manual_seed_all(42)
   ```

---

## 总结

PyTorch 的核心优势在于其动态计算图和 Pythonic 的编程风格，适合研究和快速迭代场景。关键点总结：

- **张量**：PyTorch 的基础数据结构，支持 GPU 加速。
- **自动求导**：通过 `requires_grad` 和 `backward()` 实现自动微分。
- **模块化设计**：`nn.Module` 提供封装神经网络的标准方式。
- **数据管道**：`Dataset` 和 `DataLoader` 简化数据加载与批处理。
- **灵活性**：支持自定义层、损失函数和训练逻辑。

**进一步学习**:
- [PyTorch 官方文档](https://pytorch.org/docs/stable/index.html)
- [PyTorch 教程合集](https://pytorch.org/tutorials/)
- [TorchVision](https://pytorch.org/vision/stable/index.html)（计算机视觉工具库）
