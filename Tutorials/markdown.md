# Markdown 教程：从零打造专业级技术文档

Markdown 是一种轻量级标记语言，允许用户使用易读易写的纯文本格式编写文档，并转换为结构化的 HTML/XHTML 等格式。以下是完整的 Markdown 语法指南。

---

## 目录
1. [基础语法](#基础语法)
2. [高级功能](#高级功能)
3. [实用技巧](#实用技巧)

---

## 基础语法

### 标题
使用 `#` 定义标题（支持六级标题）：
```markdown
# 一级标题
## 二级标题
### 三级标题
```

### 段落与换行
段落之间用空行分隔，强制换行在行尾加两个空格：
```markdown
这是第一段  
这是第二段（通过两个空格换行）
```

### 强调文本
- **加粗**：`**加粗**` 或 `__加粗__`
- *斜体*：`*斜体*` 或 `_斜体_`
- ~~删除线~~：`~~删除线~~`

### 列表
#### 无序列表
```markdown
- 项目1
- 项目2
  - 子项目
```

#### 有序列表
```markdown
1. 第一步
2. 第二步
```

### 链接与图片
- 超链接：`[显示文本](URL "可选标题")`
- 图片：`![替代文本](图片路径 "可选标题")`

### 代码块
- 行内代码：用反引号包裹 `` `code` ``
- 多行代码块：


```python
def hello():
    print("Hello World")
```



### 引用
```markdown
> 这是引用内容
>> 嵌套引用
```

### 分隔线
```markdown
---
```

---

## 高级功能

### 表格
```markdown
| 姓名     | 年龄 |
|----------|------|
| 张三     | 25   |
| 李四     | 30   |
```

### 任务列表
```markdown
- [x] 完成任务1
- [ ] 待办任务2
```

### 脚注
```markdown
这是带脚注的文本[^1]

[^1]: 这是脚注内容
```

### 数学公式（LaTeX 语法）
```markdown
行内公式：$ E = mc^2 $
独立公式：
$$
\int_{a}^{b} f(x)dx
$$
```

### HTML 标签
Markdown 支持直接嵌入 HTML：
```html
<details>
  <summary>点击展开</summary>
  <p>隐藏的内容</p>
</details>
```

---

## 实用技巧

### 兼容性注意事项
- 不同解析器对扩展语法支持不同（如 GitHub Flavored Markdown）
- 使用 [CommonMark](https://commonmark.org/) 保证基本兼容性

### 推荐工具
- **编辑器**：Typora / VS Code（安装 Markdown 插件）
- **在线编辑**：[StackEdit](https://stackedit.io/) / [Dillinger](https://dillinger.io/)
- **实时预览**：使用 VS Code 的 `Ctrl+Shift+V` 预览功能

### 快捷键示例（Typora）
- `Ctrl+H`：创建标题
- `Ctrl+B`：加粗
- `Ctrl+K`：插入链接

---

## 总结
Markdown 通过简洁的语法实现了内容与格式的分离，特别适合：
- 技术文档编写
- 博客写作
- 跨平台笔记记录

建议通过实践掌握，尝试将本文示例复制到编辑器中实时预览效果。更多高级用法可参考 [GitHub Flavored Markdown](https://github.github.com/gfm/) 官方文档。
