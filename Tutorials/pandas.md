# Pandas 教程：Python 数据分析终极指南

Pandas 是 Python 中用于数据清洗、处理和分析的核心库，基于 NumPy 构建，提供了高效的 DataFrame 和 Series 数据结构。以下是快速掌握 Pandas 的完整教程。

---

## 目录

1. [安装与导入](#安装与导入)  
2. [核心数据结构](#核心数据结构)  
3. [数据读写](#数据读写)  
4. [数据清洗](#数据清洗)  
5. [数据操作](#数据操作)  
6. [分组与聚合](#分组与聚合)  
7. [时间序列](#时间序列)  
8. [可视化](#可视化)  
9. [实战案例](#实战案例)  
10. [注意事项](#注意事项)  

---

## 安装与导入

```bash
# 使用 pip 安装
pip install pandas

# 使用 conda 安装
conda install -c conda-forge pandas
```

```python
import pandas as pd
```

---

## 核心数据结构

### 1. Series（一维）

```python
s = pd.Series([10, 20, 30], index=['a', 'b', 'c'])
print(s)
# 输出:
# a    10
# b    20
# c    30
```

### 2. DataFrame（二维）

```python
data = {
    'Name': ['Alice', 'Bob'],
    'Age': [25, 30],
    'City': ['New York', 'London']
}
df = pd.DataFrame(data)
print(df)
# 输出:
#     Name  Age      City
# 0  Alice   25  New York
# 1    Bob   30    London
```

---

## 数据读写

### 1. 读取数据

```python
# 从 CSV 读取
df = pd.read_csv('data.csv')

# 从 Excel 读取
df = pd.read_excel('data.xlsx', sheet_name='Sheet1')

# 从字典创建
df = pd.DataFrame.from_dict(data)

# 从列表创建
df = pd.DataFrame.from_records([(1, 2), (3, 4)], columns=['A', 'B'])
```

### 2. 写入数据

```python
df.to_csv('output.csv', index=False)
df.to_excel('output.xlsx', sheet_name='Data')
```

---

## 数据清洗

### 1. 处理缺失值

```python
# 检查缺失值
print(df.isnull().sum())

# 删除缺失值
df_clean = df.dropna()

# 填充缺失值
df_filled = df.fillna(0)  # 填充 0
df_filled = df.fillna(df.mean())  # 按列均值填充
```

### 2. 类型转换

```python
df['Age'] = df['Age'].astype(int)  # 转换为整数
df['Date'] = pd.to_datetime(df['Date'])  # 转换为日期
```

### 3. 去重

```python
df_unique = df.drop_duplicates()
```

---

## 数据操作

### 1. 筛选与排序

```python
# 按条件筛选
df_filtered = df[df['Age'] > 25]

# 多条件筛选
df_filtered = df[(df['Age'] > 25) & (df['City'] == 'New York')]

# 排序
df_sorted = df.sort_values(by='Age', ascending=False)
```

### 2. 新增列

```python
# 直接赋值
df['Salary'] = [50000, 60000]

# 通过计算生成
df['Bonus'] = df['Salary'] * 0.1
```

### 3. 合并数据

```python
# 横向合并（join）
df_merged = pd.merge(df1, df2, on='ID', how='inner')

# 纵向合并（concat）
df_concat = pd.concat([df1, df2], axis=0)
```

---

## 分组与聚合

### 1. GroupBy 基础

```python
# 按城市分组
grouped = df.groupby('City')

# 聚合操作
print(grouped['Age'].mean())
print(grouped.agg({'Salary': 'mean', 'Age': 'max'}))
```

### 2. 透视表（Pivot Table）

```python
pivot = df.pivot_table(values='Salary', index='City', columns='Year', aggfunc=np.mean)
```

---

## 时间序列

### 1. 日期范围生成

```python
dates = pd.date_range(start='2023-01-01', periods=30, freq='D')
```

### 2. 时间序列操作

```python
df['Date'] = pd.to_datetime(df['Date'])
df.set_index('Date', inplace=True)  # 设置为索引
df.resample('M').mean()  # 按月重采样
```

---

## 可视化

### 1. 内置绘图

```python
df.plot(kind='line', x='Year', y='Sales', title='Sales Trend')
df.hist(column='Age', bins=10)
```

### 2. 集成 Matplotlib/Seaborn

```python
import matplotlib.pyplot as plt
import seaborn as sns

sns.barplot(x='City', y='Salary', data=df)
plt.show()
```

---

## 实战案例

### 分析销售数据

```python
# 读取数据
sales = pd.read_csv('sales_data.csv')

# 数据清洗
sales['Date'] = pd.to_datetime(sales['Date'])
sales['Revenue'] = sales['Units'] * sales['Unit_Price']

# 按月份分析销售额
monthly_sales = sales.resample('M', on='Date').sum()
monthly_sales.plot(kind='bar', y='Revenue')
```

---

## 注意事项

1. **索引问题**：
   - 操作后保留索引：`reset_index(drop=True)`
   - 避免重复索引：`df = df.reset_index(drop=True)`

2. **链式赋值警告**：
   ```python
   # 错误写法
   df[df['Age'] > 25]['City'] = 'New York'  # 可能无效

   # 正确写法
   df.loc[df['Age'] > 25, 'City'] = 'New York'
   ```

3. **内存优化**：
   ```python
   # 降低内存占用
   df['Category'] = df['Category'].astype('category')
   ```

4. **性能建议**：
   - 避免逐行循环，优先使用向量化操作
   - 大数据量使用 `df.iterrows()` 或 `df.itertuples()` 替代循环

5. **版本兼容性**：
   - 使用 `pd.__version__` 检查版本
   - 过渡到 `pyarrow` 引擎（Pandas 2.0+）：
     ```python
     pd.options.mode.dtype_backend = "pyarrow"
     ```

---

## 总结

Pandas 是 Python 数据分析的基石，核心优势在于：

- **高效数据结构**：DataFrame 提供类 SQL 操作体验
- **灵活清洗能力**：缺失值处理、类型转换等
- **丰富分析工具**：分组聚合、时间序列、可视化集成
- **生态系统兼容**：与 NumPy、Matplotlib、Scikit-learn 无缝衔接

**进一步学习**:
- [Pandas 官方文档](https://pandas.pydata.org/docs/)
- [Pandas 教程合集](https://pandas.pydata.org/docs/getting_started/tutorials.html)
- 推荐书籍：《利用 Python 进行数据分析》（作者：Wes McKinney）
