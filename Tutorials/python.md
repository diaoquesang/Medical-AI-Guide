# Python 教程：从基础语法到实战

Python 是一门以简洁、易读和高效著称的通用编程语言，广泛应用于数据分析、人工智能、Web 开发、自动化脚本等领域。以下是快速掌握 Python 的完整教程。

---

## 目录

1. [安装与环境配置](#安装与环境配置)  
2. [基础语法](#基础语法)  
3. [数据类型](#数据类型)  
4. [控制流](#控制流)  
5. [函数](#函数)  
6. [模块与包](#模块与包)  
7. [文件操作](#文件操作)  
8. [异常处理](#异常处理)  
9. [面向对象编程](#面向对象编程)  
10. [实战案例](#实战案例)  
11. [注意事项](#注意事项)  

---

## 安装与环境配置

```bash
# 安装 Python（Windows/macOS/Linux）
# 官方下载地址: https://www.python.org/downloads/

# 验证安装
python --version  # 或 python3 --version
```

### 虚拟环境（推荐）

```bash
# 创建虚拟环境
python -m venv env

# 激活虚拟环境
# Windows: env\Scripts\activate
# macOS/Linux: source env/bin/activate

# 安装第三方包
pip install requests
```

---

## 基础语法

### 1. 变量与注释

```python
# 单行注释
name = "Alice"  # 动态类型，无需声明类型
age = 25
PI = 3.14159  # 常量命名惯例（非强制）
```

### 2. 输入输出

```python
# 输入
user_input = input("Enter your name: ")

# 输出
print("Hello, " + user_input)
print(f"Your age is {age}")  # f-string（Python 3.6+）
```

### 3. 缩进规则

```python
# Python 使用缩进定义代码块（强制！）
if age > 18:
    print("Adult")
else:
    print("Minor")
```

---

## 数据类型

### 1. 基础类型

```python
# 整数
x = 10

# 浮点数
y = 3.14

# 布尔值
is_valid = True

# None（空值）
result = None
```

### 2. 序列类型

```python
# 字符串
s = "Python"
print(s[0])  # 索引访问: 'P'

# 列表（可变）
fruits = ["apple", "banana", "cherry"]
fruits.append("orange")

# 元组（不可变）
coordinates = (1, 2)

# 字典（键值对）
person = {"name": "Alice", "age": 25}

# 集合（无序、唯一元素）
unique_numbers = {1, 2, 3, 3}  # 输出: {1, 2, 3}
```

---

## 控制流

### 1. 条件语句

```python
if age >= 18:
    print("Adult")
elif age >= 13:
    print("Teenager")
else:
    print("Child")
```

### 2. 循环

```python
# for 循环
for fruit in fruits:
    print(fruit)

# range() 用法
for i in range(3):
    print(i)  # 输出 0, 1, 2

# while 循环
count = 0
while count < 3:
    print(count)
    count += 1
```

### 3. 推导式（Comprehensions）

```python
# 列表推导式
squares = [x**2 for x in range(5)]  # [0, 1, 4, 9, 16]

# 字典推导式
square_dict = {x: x**2 for x in range(3)}  # {0:0, 1:1, 2:4}
```

---

## 函数

### 1. 定义与调用

```python
def greet(name="Guest"):
    return f"Hello, {name}"

print(greet("Alice"))  # 输出: Hello, Alice
```

### 2. 参数传递

```python
def add(a, b=0, *args, **kwargs):
    total = a + b
    for num in args:
        total += num
    for key, value in kwargs.items():
        print(f"{key}: {value}")
    return total

add(1, 2, 3, 4, name="Test")  # args=(3,4), kwargs={'name': 'Test'}
```

### 3. 匿名函数（Lambda）

```python
square = lambda x: x**2
print(square(5))  # 输出: 25
```

---

## 模块与包

### 1. 导入模块

```python
import math
print(math.sqrt(16))  # 输出: 4.0

from datetime import datetime
print(datetime.now())  # 当前时间
```

### 2. 标准库示例

```python
import os
print(os.getcwd())  # 获取当前工作目录

import json
data = {"name": "Alice"}
json_str = json.dumps(data)  # 字典转 JSON
```

---

## 文件操作

### 1. 读写文本文件

```python
# 写文件
with open("example.txt", "w") as f:
    f.write("Hello, World!")

# 读文件
with open("example.txt", "r") as f:
    content = f.read()
    print(content)
```

### 2. 读写 JSON 文件

```python
# 写 JSON
with open("data.json", "w") as f:
    json.dump(data, f)

# 读 JSON
with open("data.json", "r") as f:
    loaded_data = json.load(f)
```

---

## 异常处理

```python
try:
    result = 10 / 0
except ZeroDivisionError as e:
    print(f"Error: {e}")
finally:
    print("Cleanup code here")
```

---

## 面向对象编程

### 1. 类定义

```python
class Dog:
    def __init__(self, name):
        self.name = name  # 实例变量

    def bark(self):
        print(f"{self.name} says Woof!")

my_dog = Dog("Buddy")
my_dog.bark()  # 输出: Buddy says Woof!
```

### 2. 继承

```python
class Animal:
    def speak(self):
        pass

class Cat(Animal):
    def speak(self):
        return "Meow"
```

---

## 实战案例

### 1. 计算斐波那契数列

```python
def fibonacci(n):
    a, b = 0, 1
    result = []
    while a < n:
        result.append(a)
        a, b = b, a+b
    return result

print(fibonacci(100))  # 输出: [0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89]
```

### 2. 爬取网页内容（需安装 requests）

```python
import requests

response = requests.get("https://example.com")
print(response.status_code)
print(response.text[:100])  # 打印前 100 字符
```

---

## 注意事项

1. **缩进错误**：Python 依赖缩进定义代码块，混用空格和 Tab 会导致 `IndentationError`。
2. **可变默认参数陷阱**：

   ```python
   # 错误写法！所有调用共享同一列表
   def add_item(item, lst=[]):
       lst.append(item)
       return lst

   # 正确写法
   def add_item(item, lst=None):
       if lst is None:
           lst = []
       lst.append(item)
       return lst
   ```

3. **浅拷贝 vs 深拷贝**：

   ```python
   import copy
   a = [[1, 2], [3, 4]]
   b = a.copy()      # 浅拷贝
   c = copy.deepcopy(a)  # 深拷贝
   ```

4. **全局变量**：函数内修改全局变量需使用 `global` 关键字：

   ```python
   x = 10
   def func():
       global x
       x = 20
   ```

5. **迭代器与生成器**：

   ```python
   # 生成器函数
   def my_range(n):
       i = 0
       while i < n:
           yield i
           i += 1
   ```

---

## 总结

Python 的核心优势在于：

- **简洁语法**：接近自然语言，降低学习门槛。
- **丰富标准库**：涵盖文件操作、网络请求、数据处理等。
- **强大生态系统**：支持数据分析（Pandas）、机器学习（PyTorch）、Web 开发（Django）等。
- **跨平台兼容性**：支持 Windows、macOS、Linux 等系统。

**进一步学习**:
- [Python 官方文档](https://docs.python.org/3/)
- [Python 教程合集](https://docs.python.org/3/tutorial/index.html)
- 推荐书籍：《流畅的 Python》（作者：Luciano Ramalho）
