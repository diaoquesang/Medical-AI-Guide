# Python `dataclass` 教程：简化类定义的利器

`dataclass` 是 Python 3.7 引入的标准库特性（`from dataclasses import dataclass`），用于自动生成类的特殊方法（如 `__init__`、`__repr__` 等），大幅减少样板代码。以下是详细教程。

---

## 目录

1. [基本用法](#基本用法)  
2. [字段定义与默认值](#字段定义与默认值)  
3. [比较与排序](#比较与排序)  
4. [不可变实例](#不可变实例)  
5. [继承与组合](#继承与组合)  
6. [常见用例](#常见用例)  
7. [注意事项](#注意事项)  

---

## 基本用法

### 1. 最简类定义

```python
from dataclasses import dataclass

@dataclass
class Point:
    x: int
    y: int

# 自动生成 __init__, __repr__, __eq__ 等方法
p = Point(1, 2)
print(p)  # 输出: Point(x=1, y=2)
```

### 2. 自动生成的方法

- `__init__`: 初始化所有字段
- `__repr__`: 自动生成可读字符串表示
- `__eq__`: 基于字段值的比较
- `__hash__`: 若 `frozen=True` 则自动生成

---

## 字段定义与默认值

### 1. 指定默认值

```python
@dataclass
class Product:
    name: str
    price: float = 0.0
    in_stock: bool = True

p = Product("Laptop")
print(p)  # 输出: Product(name='Laptop', price=0.0, in_stock=True)
```

### 2. 使用 `field()` 定制字段

```python
from dataclasses import field, dataclass

@dataclass
class User:
    name: str
    hobbies: list = field(default_factory=list)  # 避免可变默认值共享问题
    id: str = field(default="", compare=False)   # 不参与比较

u = User(name="Alice")
print(u)  # 输出: User(name='Alice', hobbies=[], id='')
```

**常用 `field()` 参数**:
- `default`: 固定默认值
- `default_factory`: 可调用对象生成默认值（如 `list`, `dict`）
- `init`: 是否包含在 `__init__`
- `repr`: 是否包含在 `__repr__`
- `compare`: 是否参与比较

---

## 比较与排序

### 1. 启用排序功能

```python
@dataclass(order=True)
class Student:
    name: str
    grade: int

s1 = Student("Alice", 85)
s2 = Student("Bob", 90)
print(s1 < s2)  # 输出: True
```

### 2. 自定义比较逻辑

```python
@dataclass(order=True)
class Student:
    name: str
    grade: int

    def __post_init__(self):
        # 可在此添加验证逻辑
        if self.grade < 0:
            raise ValueError("Grade cannot be negative")
```

---

## 不可变实例

```python
@dataclass(frozen=True)
class ImmutablePoint:
    x: int
    y: int

p = ImmutablePoint(1, 2)
p.x = 3  # 抛出 FrozenInstanceError
```

---

## 继承与组合

### 1. 父类字段继承

```python
@dataclass
class Base:
    x: int = 1

@dataclass
class Sub(Base):
    y: int

s = Sub(y=2)
print(s)  # 输出: Sub(x=1, y=2)
```

### 2. 多继承注意

```python
@dataclass
class A:
    x: int

@dataclass
class B:
    y: int

class C(A, B):  # 需确保父类也是 dataclass
    pass
```

---

## 常见用例

### 1. 数据模型类

```python
@dataclass
class User:
    id: int
    name: str
    email: str
```

### 2. 配置类

```python
@dataclass
class Config:
    host: str = "localhost"
    port: int = 8080
    debug: bool = False
```

### 3. DTO（数据传输对象）

```python
@dataclass
class ProductDTO:
    name: str
    price: float
    category: str = field(compare=False)
```

---

## 注意事项

### 1. 可变默认值陷阱

```python
# 错误写法！所有实例共享同一列表
@dataclass
class BadClass:
    data: list = []  # ❌

# 正确写法
@dataclass
class GoodClass:
    data: list = field(default_factory=list)  # ✅
```

### 2. `__post_init__` 方法

用于初始化后验证或计算字段：

```python
@dataclass
class Rectangle:
    width: int
    height: int

    def __post_init__(self):
        if self.width <= 0:
            raise ValueError("Width must be positive")
```

### 3. 性能优化

- 避免在高频循环中使用 `dataclass` 的 `__repr__` 和 `__eq__`
- 对性能敏感场景可手动实现关键方法

### 4. 类型提示要求

必须显式声明字段类型（Python 3.7+）：

```python
@dataclass
class Example:
    x = 10  # ❌ 缺少类型注解，不会被识别为字段
    y: int = 20  # ✅ 正确
```

---

## 总结

`dataclass` 通过减少样板代码显著提升开发效率，适用于数据模型、配置管理等场景。核心优势：
- 自动生成常用方法
- 支持默认值和自定义逻辑
- 兼容不可变对象和继承

**进一步学习**:
- [PEP 557 - Data Classes](https://peps.python.org/pep-0557/)
- `dataclasses` 官方文档: https://docs.python.org/3/library/dataclasses.html
