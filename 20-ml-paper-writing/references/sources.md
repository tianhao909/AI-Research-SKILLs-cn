# 资源参考书目 | Source Bibliography

本文档列出了构建此技能所使用的所有权威来源，按主题组织。

---

## 写作理念与指南 | Writing Philosophy & Guides

### 主要来源（必读）

| 来源 | 作者 | 链接 | 关键贡献 |
|--------|--------|-----|------------------|
| **Highly Opinionated Advice on How to Write ML Papers** | Neel Nanda | [Alignment Forum](https://www.alignmentforum.org/posts/eJGptPbbFPZGLpjsp/highly-opinionated-advice-on-how-to-write-ml-papers) | 叙事框架，"What/Why/So What"，时间分配 |
| **How to Write ML Papers** | Sebastian Farquhar (DeepMind) | [Blog](https://sebastianfarquhar.com/on-research/2024/11/04/how_to_write_ml_papers/) | 5句话摘要公式，结构模板 |
| **A Survival Guide to a PhD** | Andrej Karpathy | [Blog](http://karpathy.github.io/2016/09/07/phd/) | 论文结构配方，贡献框架 |
| **Heuristics for Scientific Writing** | Zachary Lipton (CMU) | [Blog](https://www.approximatelycorrect.com/2018/01/29/heuristics-technical-scientific-writing-machine-learning-perspective/) | 措辞选择，章节平衡，强化词警告 |
| **Advice for Authors** | Jacob Steinhardt (UC Berkeley) | [Blog](https://jsteinhardt.stat.berkeley.edu/blog/advice-for-authors) | 精确胜于简洁，一致术语 |
| **Easy Paper Writing Tips** | Ethan Perez (Anthropic) | [Blog](https://ethanperez.net/easy-paper-writing-tips/) | 微观层面技巧，省略号展开，清晰技巧 |

### 基础科学写作

| 来源 | 作者 | 链接 | 关键贡献 |
|--------|--------|-----|------------------|
| **The Science of Scientific Writing** | Gopen & Swan | [PDF](https://cseweb.ucsd.edu/~swanson/papers/science-of-writing.pdf) | 主题/强调位置，旧前新后，7项原则 |
| **Summary of Science of Scientific Writing** | Lawrence Crowl | [Summary](https://www.crowl.org/Lawrence/writing/GopenSwan90.html) | Gopen & Swan精简版 |

### 其他资源

| 来源 | 链接 | 关键贡献 |
|--------|-----|------------------|
| How To Write A Research Paper In ML | [Blog](https://grigorisg9gr.github.io/machine%20learning/research%20paper/how-to-write-a-research-paper-in-machine-learning/) | 实践指南，LaTeX技巧 |
| A Recipe for Training Neural Networks | [Karpathy Blog](http://karpathy.github.io/2019/04/25/recipe/) | 调试方法转化为论文结构 |
| ICML Paper Writing Best Practices | [ICML](https://icml.cc/Conferences/2022/BestPractices) | 官方场所指南 |
| Bill Freeman's Writing Slides | [MIT](https://billf.mit.edu/sites/default/files/documents/cvprPapers.pdf) | 论文结构视觉指南 |

---

## 官方会议指南 | Official Conference Guidelines

### NeurIPS

| 文档 | 链接 | 用途 |
|----------|-----|---------|
| 论文检查清单指南 | [NeurIPS](https://neurips.cc/public/guides/PaperChecklist) | 16项强制检查清单 |
| 2025审稿人指南 | [NeurIPS](https://neurips.cc/Conferences/2025/ReviewerGuidelines) | 评估标准，评分 |
| 样式文件 | [NeurIPS](https://neurips.cc/Conferences/2025/PaperInformation/StyleFiles) | LaTeX模板 |

### ICML

| 文档 | 链接 | 用途 |
|----------|-----|---------|
| 论文指南 | [ICML](https://icml.cc/Conferences/2024/PaperGuidelines) | 投稿要求 |
| 2025审稿人说明 | [ICML](https://icml.cc/Conferences/2025/ReviewerInstructions) | 审稿表格，评估 |
| 样式与作者说明 | [ICML](https://icml.cc/Conferences/2022/StyleAuthorInstructions) | 格式规格 |

### ICLR

| 文档 | 链接 | 用途 |
|----------|-----|---------|
| 2026作者指南 | [ICLR](https://iclr.cc/Conferences/2026/AuthorGuide) | 投稿要求，LLM披露 |
| 2025审稿人指南 | [ICLR](https://iclr.cc/Conferences/2025/ReviewerGuide) | 审稿流程，评估 |

### ACL/EMNLP

| 文档 | 链接 | 用途 |
|----------|-----|---------|
| ACL样式文件 | [GitHub](https://github.com/acl-org/acl-style-files) | LaTeX模板 |
| ACL滚动审稿 | [ARR](https://aclrollingreview.org/) | 投稿流程 |

### AAAI

| 文档 | 链接 | 用途 |
|----------|-----|---------|
| 2026作者套件 | [AAAI](https://aaai.org/authorkit26/) | 模板和指南 |

### COLM

| 文档 | 链接 | 用途 |
|----------|-----|---------|
| 模板 | [GitHub](https://github.com/COLM-org/Template) | LaTeX模板 |

---

## 引用 API 与工具 | Citation APIs & Tools

### API 接口

| API | 文档 | 最佳用途 |
|-----|---------------|----------|
| **Semantic Scholar** | [文档](https://api.semanticscholar.org/api-docs/) | ML/AI 论文，引用图谱 |
| **CrossRef** | [文档](https://www.crossref.org/documentation/retrieve-metadata/rest-api/) | DOI 查询，BibTeX 获取 |
| **arXiv** | [文档](https://info.arxiv.org/help/api/basics.html) | 预印本，PDF 访问 |
| **OpenAlex** | [文档](https://docs.openalex.org/) | 开源替代，批量访问 |

### Python 库

| 库 | 安装命令 | 用途 |
|---------|---------|---------|
| `semanticscholar` | `pip install semanticscholar` | Semantic Scholar 封装器 |
| `arxiv` | `pip install arxiv` | arXiv 搜索与下载 |
| `habanero` | `pip install habanero` | CrossRef 客户端 |

### 引用验证

| 工具 | 网址 | 用途 |
|------|-----|---------|
| Citely | [citely.ai](https://citely.ai/citation-checker) | 批量验证 |
| ReciteWorks | [reciteworks.com](https://reciteworks.com/) | 文中引用检查 |

---

## 可视化与格式 | Visualization & Formatting

### 图表创建

| 工具 | 网址 | 用途 |
|------|-----|---------|
| PlotNeuralNet | [GitHub](https://github.com/HarisIqbal88/PlotNeuralNet) | TikZ 神经网络图 |
| SciencePlots | [GitHub](https://github.com/garrettj403/SciencePlots) | 出版级 matplotlib 样式 |
| Okabe-Ito Palette | [参考](https://jfly.uni-koeln.de/color/) | 色盲友好配色 |

### LaTeX 资源

| 资源 | 网址 | 用途 |
|----------|-----|---------|
| Overleaf 模板 | [Overleaf](https://www.overleaf.com/latex/templates) | 在线 LaTeX 编辑器 |
| BibLaTeX 指南 | [CTAN](https://ctan.org/pkg/biblatex) | 现代引用管理 |

---

## AI 写作与幻觉研究 | Research on AI Writing & Hallucination

| 来源 | 网址 | 关键发现 |
|--------|-----|-------------|
| AI 引用中的幻觉 | [Enago](https://www.enago.com/academy/ai-hallucinations-research-citations/) | 约 40% 错误率 |
| AI 写作中的幻觉 | [PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC10726751/) | 引用错误类型 |
| NeurIPS 2025 AI 报告 | [ByteIota](https://byteiota.com/neurips-2025-100-ai-hallucinations-slip-through-review/) | 100+ 幻觉引用 |

---

## 按主题快速参考 | Quick Reference by Topic

### 叙事与结构
→ 入门参考：Neel Nanda、Sebastian Farquhar、Andrej Karpathy

### 句子级别清晰度
→ 入门参考：Gopen & Swan、Ethan Perez、Zachary Lipton

### 措辞与风格
→ 入门参考：Zachary Lipton、Jacob Steinhardt

### 会议特定要求
→ 入门参考：官方会议指南（NeurIPS、ICML、ICLR、ACL）

### 引用管理
→ 入门参考：Semantic Scholar API、CrossRef、citation-workflow.md

### 审稿人期望
→ 入门参考：会议审稿人指南、reviewer-guidelines.md
