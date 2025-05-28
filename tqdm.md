# tqdm 教程：Python 进度条库

`tqdm` 是一个快速、可扩展的 Python 进度条库，用于在长时间运行的循环中显示实时进度条。以下是详细的使用教程。

---

## 安装

```bash
# 使用 pip 安装
pip install tqdm

# 或使用 conda 安装
conda install -c conda-forge tqdm
```

---

## 基本用法

### 1. 简单进度条

```python
from tqdm import tqdm
import time

for i in tqdm(range(100)):
    time.sleep(0.01)  # 模拟耗时操作
```

### 2. 添加描述信息

```python
for i in tqdm(range(100), desc="Processing"):
    time.sleep(0.01)
```

### 3. 自定义进度条单位

```python
for i in tqdm(range(100), unit="item"):
    time.sleep(0.01)
```

---

## 高级用法

### 1. 作为装饰器使用

```python
from tqdm import tqdm

@tqdm(desc="Function Progress")
def long_function(n):
    for _ in range(n):
        time.sleep(0.01)

long_function(100)
```

### 2. 手动控制进度条

```python
from tqdm import tqdm

pbar = tqdm(total=100)
for i in range(10):
    time.sleep(0.1)
    pbar.update(10)  # 手动更新进度
pbar.close()
```

### 3. 嵌套进度条

```python
from tqdm import tqdm, trange

for i in trange(3, desc="Outer Loop"):
    for j in tqdm(range(5), desc="Inner Loop", leave=False):
        time.sleep(0.1)
```

### 4. 多进程支持

```python
from tqdm.contrib.concurrent import process_map
import time

def task(x):
    time.sleep(0.1)
    return x

results = process_map(task, range(100), max_workers=4)
```

---

## 在 Jupyter Notebook 中使用

```python
from tqdm.notebook import tqdm
import time

for i in tqdm(range(100)):
    time.sleep(0.01)
```

---

## 自定义样式

### 1. 修改进度条描述和单位

```python
for i in tqdm(range(100), desc="Loading", unit="step"):
    time.sleep(0.01)
```

### 2. 设置进度条颜色（需 `colorama`）

```python
from tqdm import tqdm
import colorama

colorama.init()
for i in tqdm(range(100), bar_format="{l_bar}%s{bar}%s{r_bar}" % (colorama.Fore.RED, colorama.Fore.RESET)):
    time.sleep(0.01)
```

---

## 注意事项

1. **性能开销**：`tqdm` 的性能开销极低，但在高频循环中建议测试性能影响。
2. **多线程/多进程**：默认进度条可能不兼容多线程/多进程，可使用 `tqdm.contrib.concurrent` 模块。
3. **异常处理**：在 `try-except` 块中使用时，需手动关闭进度条：

   ```python
   pbar = tqdm(total=100)
   try:
       for i in range(100):
           time.sleep(0.01)
           pbar.update(1)
   except Exception as e:
       pbar.close()
       raise e
   ```

---

## 总结

`tqdm` 是一个轻量级且功能强大的进度条工具，适用于各种需要可视化进度的场景。通过简单的 API 可以快速集成到现有代码中，同时支持丰富的自定义选项。

更多详情请参考 [官方文档](https://github.com/tqdm/tqdm)
```
