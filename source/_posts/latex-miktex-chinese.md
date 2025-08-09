---
title: latex-miktex-chinese
date: 2025-01-19 23:14:19
tags:
---
在 MiKTeX 中使用中文需要配置 LaTeX 以支持中文排版。常用的中文支持方案包括 **CTeX 宏包**、**XeLaTeX/LuaLaTeX + fontspec** 等。以下是详细的配置和使用方法：

---

### 1. **使用 CTeX 宏包**
CTeX 宏包是一个专门为中文排版设计的宏包，支持多种中文环境和字体。

#### 安装 CTeX 宏包
1. 打开 MiKTeX Console。
2. 在 **“Packages”** 选项卡中搜索 `ctex`。
3. 找到 `ctex` 宏包后，点击右侧的 **“+”** 按钮进行安装。

#### 编写中文文档
在 LaTeX 文档中使用 `ctex` 宏包，并指定文档类为 `ctexart`、`ctexrep`、`ctexbook` 或 `ctexbeamer`。例如：
```latex
\documentclass[UTF8]{ctexart}

\begin{document}
\title{中文标题}
\author{作者}
\date{\today}
\maketitle

\section{中文章节}
这是一段中文内容。
\end{document}
```
- **注意**：确保文件保存为 UTF-8 编码。

#### 编译文档
使用 **pdfLaTeX** 编译文档：
1. 在编辑器（如 TeXworks 或 TeXstudio）中，选择编译引擎为 **pdfLaTeX**。
2. 点击编译按钮，生成 PDF 文件。

---

### 2. **使用 XeLaTeX + fontspec**
XeLaTeX 直接支持 Unicode 和系统字体，适合处理中文文档。

#### 安装所需宏包
1. 打开 MiKTeX Console。
2. 安装以下宏包：
   - `fontspec`：用于加载系统字体。
   - `xeCJK`：用于处理中日韩文字（可选，但推荐）。

#### 编写中文文档
使用 `article` 文档类，并加载 `fontspec` 和 `xeCJK` 宏包。例如：
```latex
\documentclass{article}
\usepackage{fontspec}
\usepackage{xeCJK}

\setCJKmainfont{SimSun} % 设置中文字体（例如宋体）

\begin{document}
\title{中文标题}
\author{作者}
\date{\today}
\maketitle

\section{中文章节}
这是一段中文内容。
\end{document}
```
- **注意**：确保文件保存为 UTF-8 编码。

#### 编译文档
使用 **XeLaTeX** 编译文档：
1. 在编辑器（如 TeXworks 或 TeXstudio）中，选择编译引擎为 **XeLaTeX**。
2. 点击编译按钮，生成 PDF 文件。

---

### 3. **使用 LuaLaTeX + fontspec**
LuaLaTeX 是另一种支持 Unicode 和系统字体的方式，功能与 XeLaTeX 类似。

#### 安装所需宏包
1. 打开 MiKTeX Console。
2. 安装以下宏包：
   - `fontspec`：用于加载系统字体。
   - `luatexja`：用于处理中日韩文字（可选，但推荐）。

#### 编写中文文档
使用 `article` 文档类，并加载 `fontspec` 和 `luatexja` 宏包。例如：
```latex
\documentclass{article}
\usepackage{fontspec}
\usepackage{luatexja}

\setmainjfont{SimSun} % 设置中文字体（例如宋体）

\begin{document}
\title{中文标题}
\author{作者}
\date{\today}
\maketitle

\section{中文章节}
这是一段中文内容。
\end{document}
```
- **注意**：确保文件保存为 UTF-8 编码。

#### 编译文档
使用 **LuaLaTeX** 编译文档：
1. 在编辑器（如 TeXworks 或 TeXstudio）中，选择编译引擎为 **LuaLaTeX**。
2. 点击编译按钮，生成 PDF 文件。

---

### 4. **常见问题**
#### （1）**字体无法加载**
- 确保系统中安装了所需的中文字体（如宋体、黑体等）。
- 在 Windows 中，可以通过 `fc-list` 命令查看已安装的字体：
  ```bash
  fc-list :lang=zh
  ```

#### （2）**编译报错**
- 确保文件保存为 UTF-8 编码。
- 如果使用 `ctex` 宏包，确保文档类为 `ctexart`、`ctexrep` 等。

#### （3）**MiKTeX 自动安装宏包失败**
- 手动安装所需宏包（如 `ctex`、`fontspec`、`xeCJK` 等）。

---

### 5. **总结**
- **CTeX 宏包**：适合初学者，简单易用，支持 pdfLaTeX 编译。
- **XeLaTeX + fontspec**：支持系统字体，适合需要自定义字体的文档。
- **LuaLaTeX + fontspec**：功能与 XeLaTeX 类似，但基于 LuaTeX 引擎。

根据您的需求选择合适的方案，配置完成后即可在 MiKTeX 中轻松编写和排版中文文档。