# ML/AI会议LaTeX模板 | LaTeX Templates for ML/AI Conferences

此目录包含主要机器学习和AI会议的官方LaTeX模板。

---

## 编译LaTeX到PDF | Compiling LaTeX to PDF

### 选项1：VS Code + LaTeX Workshop（推荐）

**设置：**
1. 安装 [TeX Live](https://www.tug.org/texlive/)（推荐完整发行版）
   - macOS：`brew install --cask mactex`
   - Ubuntu：`sudo apt install texlive-full`
   - Windows：从 [tug.org/texlive](https://www.tug.org/texlive/) 下载

2. 安装VS Code扩展：**LaTeX Workshop**（James Yu开发）
   - 打开VS Code → 扩展（Cmd/Ctrl+Shift+X）→ 搜索"LaTeX Workshop" → 安装

**使用：**
- 在VS Code中打开任何`.tex`文件
- 保存文件（Cmd/Ctrl+S）→ 自动编译为PDF
- 点击绿色播放按钮或使用`Cmd/Ctrl+Alt+B`构建
- 查看PDF：点击"View LaTeX PDF"图标或`Cmd/Ctrl+Alt+V`
- 并排视图：`Cmd/Ctrl+Alt+V`然后拖动标签页

**设置**（添加到VS Code `settings.json`）：
```json
{
  "latex-workshop.latex.autoBuild.run": "onSave",
  "latex-workshop.view.pdf.viewer": "tab",
  "latex-workshop.latex.recipes": [
    {
      "name": "pdflatex → bibtex → pdflatex × 2",
      "tools": ["pdflatex", "bibtex", "pdflatex", "pdflatex"]
    }
  ]
}
```

### 选项2：命令行

```bash
# 基本编译
pdflatex main.tex

# 带参考文献（完整工作流）
pdflatex main.tex
bibtex main
pdflatex main.tex
pdflatex main.tex

# 使用latexmk（自动处理依赖）
latexmk -pdf main.tex

# 持续编译（监视更改）
latexmk -pdf -pvc main.tex
```

### 选项3：Overleaf（在线）

1. 访问 [overleaf.com](https://www.overleaf.com)
2. 新建项目 → 上传项目 → 将模板文件夹作为ZIP上传
3. 在线编辑，实时预览PDF
4. 无需本地安装

### 选项4：其他IDE

| IDE | 扩展/插件 | 备注 |
|-----|------------------|-------|
| **Cursor** | LaTeX Workshop | 与VS Code相同 |
| **Sublime Text** | LaTeXTools | 流行，维护良好 |
| **Vim/Neovim** | VimTeX | 强大，键盘驱动 |
| **Emacs** | AUCTeX | 全面的LaTeX环境 |
| **TeXstudio** | 内置 | 专用LaTeX IDE |
| **Texmaker** | 内置 | 跨平台LaTeX编辑器 |

### 故障排除编译

**"文件未找到"错误：**
```bash
# 确保在模板目录中
cd templates/icml2026
pdflatex example_paper.tex
```

**参考文献不显示：**
```bash
# 第一次pdflatex后运行bibtex
pdflatex main.tex
bibtex main        # 使用main.aux查找引用
pdflatex main.tex  # 合并参考文献
pdflatex main.tex  # 解析引用
```

**缺少包：**
```bash
# TeX Live包管理器
tlmgr install <package-name>

# 或安装完整发行版以避免此问题
```

---

## 可用模板 | Available Templates

| 会议 | 目录 | 年份 | 来源 |
|------------|-----------|------|--------|
| ICML | `icml2026/` | 2026 | [官方ICML](https://icml.cc/Conferences/2026/AuthorInstructions) |
| ICLR | `iclr2026/` | 2026 | [官方GitHub](https://github.com/ICLR/Master-Template) |
| NeurIPS | `neurips2025/` | 2025 | 社区模板 |
| ACL | `acl/` | 2025+ | [官方ACL](https://github.com/acl-org/acl-style-files) |
| AAAI | `aaai2026/` | 2026 | [AAAI Author Kit](https://aaai.org/authorkit26/) |
| COLM | `colm2025/` | 2025 | [官方COLM](https://github.com/COLM-org/Template) |

## 使用方法

### ICML 2026

```latex
\documentclass{article}
\usepackage{icml2026}  % 投稿用
% \usepackage[accepted]{icml2026}  % camera-ready用

\begin{document}
% 你的论文内容
\end{document}
```

关键文件：
- `icml2026.sty` - 样式文件
- `icml2026.bst` - 参考文献样式
- `example_paper.tex` - 示例文档

### ICLR 2026

```latex
\documentclass{article}
\usepackage[submission]{iclr2026_conference}  % 投稿用
% \usepackage[final]{iclr2026_conference}  % camera-ready用

\begin{document}
% 你的论文内容
\end{document}
```

关键文件：
- `iclr2026_conference.sty` - 样式文件
- `iclr2026_conference.bst` - 参考文献样式
- `iclr2026_conference.tex` - 示例文档

### ACL会议（ACL、EMNLP、NAACL）

```latex
\documentclass[11pt]{article}
\usepackage[review]{acl}  % 审稿用
% \usepackage{acl}  % camera-ready用

\begin{document}
% 你的论文内容
\end{document}
```

关键文件：
- `acl.sty` - 样式文件
- `acl_natbib.bst` - 参考文献样式
- `acl_latex.tex` - 示例文档

### AAAI 2026

```latex
\documentclass[letterpaper]{article}
\usepackage[submission]{aaai2026}  % 投稿用
% \usepackage{aaai2026}  % camera-ready用

\begin{document}
% 你的论文内容
\end{document}
```

关键文件：
- `aaai2026.sty` - 样式文件
- `aaai2026.bst` - 参考文献样式

### COLM 2025

```latex
\documentclass{article}
\usepackage[submission]{colm2025_conference}  % 投稿用
% \usepackage[final]{colm2025_conference}  % camera-ready用

\begin{document}
% 你的论文内容
\end{document}
```

关键文件：
- `colm2025_conference.sty` - 样式文件
- `colm2025_conference.bst` - 参考文献样式

## 页数限制摘要 | Page Limits Summary

| 会议 | 投稿 | Camera-Ready | 备注 |
|------------|-----------|--------------|-------|
| ICML 2026 | 8页 | 9页 | +无限参考文献/附录 |
| ICLR 2026 | 9页 | 10页 | +无限参考文献/附录 |
| NeurIPS 2025 | 9页 | 9页 | +检查清单在限制外 |
| ACL 2025 | 8页（长论文） | 变化 | +无限参考文献/附录 |
| AAAI 2026 | 7页 | 8页 | +无限参考文献/附录 |
| COLM 2025 | 9页 | 10页 | +无限参考文献/附录 |

## 常见问题 | Common Issues

### 编译错误

1. **缺少包**：安装完整TeX发行版（TeX Live Full或MikTeX）
2. **参考文献错误**：使用提供的`.bst`文件和`\bibliographystyle{}`
3. **字体警告**：安装`cm-super`或使用`\usepackage{lmodern}`

### 匿名化

确保投稿时：
- `\author{}`中没有作者姓名
- 没有致谢部分
- 没有资助编号
- 使用匿名仓库
- 以第三人称引用自己的作品

### 常用LaTeX包

```latex
% 推荐包（检查与场所样式兼容性）
\usepackage{amsmath,amsthm,amssymb}  % 数学
\usepackage{graphicx}                 % 图表
\usepackage{booktabs}                 % 表格
\usepackage{hyperref}                 % 链接
\usepackage{algorithm,algorithmic}    % 算法
\usepackage{natbib}                   % 引用
```

## 更新模板

模板每年更新。每次投稿前检查官方来源：

- ICML: https://icml.cc/
- ICLR: https://iclr.cc/
- NeurIPS: https://neurips.cc/
- ACL: https://github.com/acl-org/acl-style-files
- AAAI: https://aaai.org/
- COLM: https://colmweb.org/
