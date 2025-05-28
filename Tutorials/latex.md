# LaTeX 教程：高质量文档排版终极指南

LaTeX 是基于 TeX 的排版系统，广泛用于学术论文、技术报告、书籍和复杂文档的排版。以下是快速掌握 LaTeX 的完整教程。

---

## 目录

1. [安装与环境配置](#安装与环境配置)  
2. [基础语法与文档结构](#基础语法与文档结构)  
3. [文本与段落格式](#文本与段落格式)  
4. [数学公式](#数学公式)  
5. [图表与浮动体](#图表与浮动体)  
6. [列表与表格](#列表与表格)  
7. [交叉引用与超链接](#交叉引用与超链接)  
8. [参考文献管理](#参考文献管理)  
9. [高级功能](#高级功能)  
10. [实战案例](#实战案例)  
11. [注意事项](#注意事项)  

---

## 安装与环境配置

### 1. 发行版安装

| 平台       | 推荐发行版                     | 下载地址                          |
|------------|--------------------------------|-----------------------------------|
| Windows    | TeX Live 或 MiKTeX            | https://www.tug.org/texlive/      |
| macOS      | MacTeX                         | https://www.tug.org/mactex/       |
| Linux      | TeX Live（包管理器安装）       | `sudo apt install texlive-full`   |

### 2. 编辑器推荐

- **Overleaf**：在线协作平台（推荐新手）[https://www.overleaf.com](https://www.overleaf.com)
- **TeXstudio**：跨平台开源编辑器
- **VS Code + LaTeX Workshop**：开发者友好

---

## 基础语法与文档结构

### 1. 最小工作示例（MWE）

```latex
\documentclass{article}     % 文档类
\usepackage{ctex}            % 中文支持
\title{我的第一篇 \LaTeX 文档}
\author{张三}
\date{\today}

\begin{document}
\maketitle                  % 生成标题
\section{引言}
这是一个简单的 \LaTeX 示例文档。
\end{document}
```

### 2. 常用文档类

| 文档类      | 适用场景               | 字号选项         |
|-------------|------------------------|------------------|
| `article`   | 短篇论文、博客         | 10pt/11pt/12pt   |
| `report`    | 长篇报告               |                  |
| `book`      | 书籍                   |                  |
| `beamer`    | 幻灯片                 |                  |

---

## 文本与段落格式

### 1. 特殊字符转义

```latex
\% \$ \& \# \_ \{ \} \~{} \textbackslash{}  % 特殊符号
```

### 2. 字体样式

```latex
\textbf{加粗} \textit{斜体} \underline{下划线}  
\texttt{等宽字体} \textsf{无衬线} \textrm{衬线体}
```

### 3. 段落控制

```latex
\section{章节标题}          % 一级标题
\subsection{子标题}         % 二级标题
\paragraph{段落标题}       % 不编号
\subparagraph{子段落标题}  % 不编号

\indent 首行缩进           % 默认已启用
\noindent 取消首行缩进

\linebreak\\ 或 \newline    % 换行
\clearpage                  % 强制分页
```

---

## 数学公式

### 1. 行内公式与显示公式

```latex
% 行内公式
欧拉公式：$e^{i\pi} + 1 = 0$

% 显示公式（自动编号）
$$\int_{-\infty}^{\infty} e^{-x^2} dx = \sqrt{\pi}$$

% 不编号公式
\begin{equation*}
\forall x \in \mathbb{R},\ \exists y \in \mathbb{R} \text{ s.t. } y > x
\end{equation*}
```

### 2. 常用数学符号

| 类别       | 示例命令                          | 输出效果       |
|------------|-----------------------------------|----------------|
| 希腊字母   | `\alpha \beta \gamma`             | αβγ            |
| 集合符号   | `\cup \cap \subset \in \mathbb{N}`| ∪∩⊂∈ℕ          |
| 箭头       | `\rightarrow \Leftarrow`          | →⇐             |
| 分数       | `\frac{a}{b}`                    | a/b            |
| 矩阵       | `\begin{bmatrix}...\end{bmatrix}` | 矩阵环境       |

---

## 图表与浮动体

### 1. 插入图片（需 `graphicx` 宏包）

```latex
\usepackage{graphicx}
\begin{figure}[htbp]
\centering
\includegraphics[width=0.5\textwidth]{example-image}  % 图片路径
\caption{示例图片}  % 标题
\label{fig:example}  % 标签
\end{figure}
```

### 2. 表格（`tabular` 环境）

```latex
\begin{table}[htbp]
\centering
\begin{tabular}{|l|c|r|}
\hline
左对齐 & 居中 & 右对齐 \\
\hline
A & 1 & X \\
B & 2 & Y \\
\hline
\end{tabular}
\caption{简单表格}
\label{tab:example}
\end{table}
```

---

## 列表与表格

### 1. 无序列表

```latex
\begin{itemize}
\item 第一项
\item 第二项
\end{itemize}
```

### 2. 有序列表

```latex
\begin{enumerate}
\item 第一步
\item 第二步
\end{enumerate}
```

### 3. 自定义列表间距

```latex
\usepackage{enumitem}
\begin{itemize}[noitemsep]
\item 紧凑列表
\end{itemize}
```

---

## 交叉引用与超链接

### 1. 标签与引用

```latex
\section{引言}\label{sec:intro}
参考章节 \ref{sec:intro} 和图表 \ref{fig:example}
```

### 2. 超链接（`hyperref` 宏包）

```latex
\usepackage{hyperref}
\href{https://example.com}{链接文本}
\url{https://example.com}
```

---

## 参考文献管理

### 1. 使用 BibTeX

```latex
% 在 .bib 文件中定义文献
@article{einstein,
  author = "Albert Einstein",
  title = "Relativity: The Special and General Theory",
  year = "1920"
}

% 在主文档中引用
\cite{einstein}

% 选择样式
\bibliographystyle{plain}
\bibliography{references}  % references.bib
```

### 2. 编译流程

1. `pdflatex main.tex`
2. `bibtex main`
3. `pdflatex main.tex`
4. `pdflatex main.tex`

---

## 高级功能

### 1. 自定义命令

```latex
\newcommand{\R}{\mathbb{R}}  % 快捷命令
\R^n  % 使用示例

\newenvironment{proof}{\textbf{证明：}}{\qed}  % 自定义环境
```

### 2. 代码高亮（`listings`）

```latex
\usepackage{listings}
\lstset{language=Python, basicstyle=\ttfamily}
\begin{lstlisting}
print("Hello, World!")
\end{lstlisting}
```

### 3. 多图并排

```latex
\usepackage{subcaption}
\begin{figure}
\begin{subfigure}{0.45\textwidth}
\includegraphics{img1}
\caption{子图1}
\end{subfigure}
\hfill
\begin{subfigure}{0.45\textwidth}
\includegraphics{img2}
\caption{子图2}
\end{subfigure}
\end{figure}
```

---

## 实战案例

### 1. 学术论文模板（IEEE）

```latex
\documentclass[10pt, conference]{IEEEtran}
\usepackage{amsmath}
\title{论文标题}
\author{\IEEEauthorblockN{作者姓名}\IEEEauthorblockA{单位}}
\begin{document}
\maketitle
\section{摘要}
这是摘要内容。
\bibliographystyle{ieeetr}
\bibliography{refs}
\end{document}
```

### 2. Beamer 幻灯片

```latex
\documentclass{beamer}
\title{演示文稿标题}
\author{张三}
\begin{document}
\frame{\titlepage}
\frame{\frametitle{目录}\tableofcontents}
\section{章节1}
\frame{\frametitle{标题} 内容}
\end{document}
```

---

## 注意事项

1. **编译错误处理**：
   - `Missing $ inserted`：数学模式缺失
   - `Undefined control sequence`：宏包未加载或拼写错误
   - `Overfull/Underfull \hbox`：排版警告（可忽略但建议优化）

2. **中文支持**：
   ```latex
   \usepackage[UTF8]{ctex}  % 支持中文
   \usepackage{fontspec}    % XeLaTeX 字体支持
   ```

3. **版本控制**：
   - 使用 Git 时忽略 `.aux`, `.log`, `.pdf` 等临时文件
   - `.gitignore` 示例：
     ```
     *.aux
     *.log
     *.pdf
     ```

4. **性能优化**：
   - 大文档使用 `\includeonly` 选择性编译
   - 图片格式优先使用 PDF/SVG（矢量图）

5. **调试技巧**：
   - 使用 `%` 注释逐段排除错误
   - 使用 `\listfiles` 查看宏包版本

---

## 总结

LaTeX 的核心优势在于：

- **高质量排版**：尤其适合数学公式和多语言文档
- **结构化写作**：分离内容与样式
- **学术生态支持**：几乎所有期刊提供 LaTeX 模板
- **可扩展性**：超过 4000 个宏包满足各种需求

**进一步学习**:
- [Overleaf 文档](https://www.overleaf.com/learn)
- [LaTeX Wikibook](https://en.wikibooks.org/wiki/LaTeX)
- 推荐书籍：《LaTeX 入门》（刘海洋）、《The LaTeX Companion》
