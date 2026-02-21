# 综合来源列表：构建ML论文写作技能 | Comprehensive Source List: Building an ML Paper Writing Skill

本文档汇编了为ICLR、NeurIPS和ICML等场所编写高质量ML/AI论文的Claude技能的权威来源。

---

## 第1部分：ML研究员的写作哲学与指南 | Part 1: Writing Philosophy & Guides from ML Researchers

### 主要来源（必读）| Primary Sources (Must-Read)

| 来源 | 作者 | 网址 | 核心价值 |
|--------|--------|-----|-----------|
| **Highly Opinionated Advice on How to Write ML Papers** | Neel Nanda | https://www.alignmentforum.org/posts/eJGptPbbFPZGLpjsp/highly-opinionated-advice-on-how-to-write-ml-papers | 核心叙事哲学，"什么/为什么/那又怎样"框架，图表优先方法 |
| **How to Write ML Papers** | Sebastian Farquhar (DeepMind) | https://sebastianfarquhar.com/on-research/2024/11/04/how_to_write_ml_papers/ | 五句摘要公式，结构模板，读者期望 |
| **A Survival Guide to a PhD** | Andrej Karpathy | http://karpathy.github.io/2016/09/07/phd/ | 论文结构配方，审阅糟糕论文的重要性，贡献框架 |
| **Heuristics for Scientific Writing (ML Perspective)** | Zachary Lipton (CMU) | https://www.approximatelycorrect.com/2018/01/29/heuristics-technical-scientific-writing-machine-learning-perspective/ | 清晰散文的有力格言，空洞强化词警告，章节平衡 |
| **Advice for Authors** | Jacob Steinhardt (UC Berkeley) | https://jsteinhardt.stat.berkeley.edu/blog/advice-for-authors | 精确胜于简洁，一致术语，以读者为中心的写作 |
| **Easy Paper Writing Tips** | Ethan Perez (Anthropic) | https://ethanperez.net/easy-paper-writing-tips/ | 实用的微观层面技巧，撇号展开，清晰度技巧 |

### 基础科学写作 | Foundational Scientific Writing

| 来源 | 作者 | 网址 | 核心价值 |
|--------|--------|-----|-----------|
| **The Science of Scientific Writing** | Gopen & Swan | https://cseweb.ucsd.edu/~swanson/papers/science-of-writing.pdf | 主题/应力位置，旧前新后原则，句子层面清晰度 |
| **Summary of Science of Scientific Writing** | Lawrence Crowl | https://www.crowl.org/Lawrence/writing/GopenSwan90.html | Gopen & Swan原则的精简版本 |

### 其他研究员视角 | Additional Researcher Perspectives

| 来源 | 网址 | 核心价值 |
|--------|-----|-----------|
| How To Write A Research Paper In Machine Learning | https://grigorisg9gr.github.io/machine%20learning/research%20paper/how-to-write-a-research-paper-in-machine-learning/ | 实践演练 |
| A Recipe for Training Neural Networks (Karpathy) | http://karpathy.github.io/2019/04/25/recipe/ | 调试方法论转化为论文结构 |

---

## 第2部分：官方会议指南 | Part 2: Official Conference Guidelines

### NeurIPS

| 文档 | 网址 | 目的 |
|----------|-----|---------|
| **Paper Checklist Guidelines** | https://neurips.cc/public/guides/PaperChecklist | 强制清单项目，可复现性要求 |
| **2025 Reviewer Guidelines** | https://neurips.cc/Conferences/2025/ReviewerGuidelines | 审稿人寻找什么，评分标准 |
| **Formatting Instructions** | https://arxiv.org/html/2505.10292v1 | LaTeX模板，页数限制，样式要求 |

### ICML

| 文档 | 网址 | 目的 |
|----------|-----|---------|
| **Paper Guidelines** | https://icml.cc/Conferences/2024/PaperGuidelines | 提交要求，伦理政策 |
| **Style & Author Instructions** | https://icml.cc/Conferences/2022/StyleAuthorInstructions | 格式规范 |
| **Reviewer Tutorial** | https://icml.cc/Conferences/2022/ReviewerTutorial | 审稿人视角的评估标准 |
| **Reviewer Guidelines (2020)** | https://icml.cc/Conferences/2020/ReviewerGuidelines | 详细评审标准 |
| **ICML 2025 LaTeX Template** | https://www.overleaf.com/latex/templates/icml2025-template/dhxrkcgkvnkt | 官方Overleaf模板 |

### ICLR

| 文档 | 网址 | 目的 |
|----------|-----|---------|
| **Author Guide 2026** | https://iclr.cc/Conferences/2026/AuthorGuide | 提交要求，LLM披露政策 |
| **LLM Disclosure Policy** | https://eu.36kr.com/en/p/3443306502428032 | 新规：强制AI使用披露（缺失则直接拒绝）|

---

## 第3部分：引文API和工具（防止幻觉）| Part 3: Citation APIs & Tools (Hallucination Prevention)

### 论文搜索和元数据的主要API | Primary APIs for Paper Search & Metadata

| API | 文档网址 | 关键功能 | 速率限制 |
|-----|-------------------|--------------|-------------|
| **Semantic Scholar API** | https://api.semanticscholar.org/api-docs/ | 2.14亿论文，引文图，AI训练的搜索 | 使用API密钥每秒1次请求 |
| **Semantic Scholar Tutorial** | https://www.semanticscholar.org/product/api/tutorial | 分步使用指南 | - |
| **CrossRef REST API** | https://www.crossref.org/documentation/retrieve-metadata/rest-api/ | DOI元数据，通过内容协商直接获取BibTeX | 带有邮箱的礼貌池 |
| **arXiv API** | https://info.arxiv.org/help/api/basics.html | 预印本元数据，全文访问 | 3秒延迟 |
| **OpenAlex API** | https://docs.openalex.org/api-entities/works | 2.4亿+作品，CC0许可，MAG的开放继承者 | 每天10万次，每秒10次 |

### Python库 | Python Libraries

| 库 | 安装 | 文档 | 目的 |
|---------|---------|---------------|---------|
| `semanticscholar` | `pip install semanticscholar` | https://semanticscholar.readthedocs.io/ | 官方Python包装器 |
| `arxiv` | `pip install arxiv` | https://pypi.org/project/arxiv/ | arXiv搜索和下载 |
| `habanero` | `pip install habanero` | https://github.com/sckott/habanero | CrossRef Python客户端 |

### BibTeX获取代码模式 | BibTeX Retrieval Code Pattern

```python
import requests

def doi_to_bibtex(doi: str) -> str:
    """直接从DOI通过CrossRef内容协商获取BibTeX。"""
    response = requests.get(
        f"https://doi.org/{doi}",
        headers={"Accept": "application/x-bibtex"}
    )
    response.raise_for_status()
    return response.text

# 示例：获取"Attention Is All You Need"的经验证BibTeX
bibtex = doi_to_bibtex("10.48550/arXiv.1706.03762")
```

### 引文验证工具 | Citation Verification Tools

| 工具 | 网址 | 目的 |
|------|-----|---------|
| **Citely** | https://citely.ai/citation-checker | AI生成引文的批量验证 |
| **ReciteWorks** | https://reciteworks.com/ | 检查文本引文是否与参考文献列表匹配 |

### LaTeX引文管理 | LaTeX Citation Management

| 资源 | 网址 | 关键信息 |
|----------|-----|----------|
| BibTeX vs BibLaTeX指南 | https://electreexpert.com/latex-vs-bibtex-vs-biblatex/ | 何时使用哪个系统 |
| BibLaTeX全面指南 | https://latextutorial.net/latex-vs-bibtex-vs-biblatex/ | 现代引文管理 |

---

## 第4部分：经验证的引文工作流 | Part 4: The Verified Citation Workflow

### AI辅助写作的推荐流程 | Recommended Pipeline for AI-Assisted Writing

```
1. 搜索：用户指定主题 → 查询Semantic Scholar API
   └— 使用paper/search端点与特定关键词
   
2. 验证存在：对于每个候选论文：
   └— 确认论文出现在2+个来源（Semantic Scholar + CrossRef/arXiv）
   └— 验证DOI正确解析
   
3. 获取BIBTEX：使用DOI内容协商
   └— requests.get(f"https://doi.org/{doi}", headers={"Accept": "application/x-bibtex"})
   └— 切勿从记忆生成BibTeX - 始终获取
   
4. 验证声明：在为特定声明引用论文之前：
   └— 通过Semantic Scholar获取论文摘要/全文
   └— 确认归属的声明实际出现在来源中
   
5. 构建参考文献：
   └— 维护仅包含经验证条目的.bib文件
   └— 使用一致的引文键（例如author_year_firstword）
```

### 为什么这很重要 | Why This Matters

来自AI引文幻觉的研究：
- AI生成的引文约40%包含错误（Enago Academy研究）
- NeurIPS 2025发现100+个幻觉引文通过了审查
- 常见错误：伪造标题，错误作者，具有可信元数据的不存在论文

---

## 第5部分：可视化和格式化资源 | Part 5: Visualization & Formatting Resources

### 图表创建 | Figure Creation

| 工具 | 网址 | 目的 |
|------|-----|---------|
| **PlotNeuralNet** | https://github.com/HarisIqbal88/PlotNeuralNet | TikZ神经网络图 |
| **SciencePlots** | https://github.com/garrettj403/SciencePlots | 出版就绪的matplotlib样式 |
| **Okabe-Ito调色板** | https://jfly.uni-koeln.de/color/ | 色盲安全的配色方案 |

### LaTeX模板 | LaTeX Templates

| 会议 | 模板网址 |
|-------|--------------|
| NeurIPS | https://neurips.cc/Conferences/2025/PaperInformation/StyleFiles |
| ICML | https://www.overleaf.com/latex/templates/icml2025-template/dhxrkcgkvnkt |
| ICLR | https://iclr.cc/Conferences/2026/AuthorGuide (链接到模板) |

---

## 第6部分：关键原则总结（技能编码用）| Part 6: Key Principles Summary (For Skill Encoding)

### 来自Neel Nanda
1. 论文 = 简短、严谨、基于证据的技术故事，带有读者关心的要点
2. 花费相等时间在：摘要、引言、图表、其他所有内容
3. 每个实验必须支持与贡献相关的具体声明
4. "如果你不能用一句话陈述你的贡献，你还没有一篇论文"

### 来自Karpathy
1. "论文推销的是以前不存在或不明显的一个东西"
2. 默认结构：引言 → 相关工作 → 模型 → 实验 → 结论
3. 审阅糟糕的论文以学习不该做什么（二元分类器训练）

### 来自Zachary Lipton
1. "如果第一句话可以加在任何ML论文前面，删除它"
2. 图表应该讲述连贯的故事，即使读者跳过文本
3. 章节应该像幻灯片上的点一样平衡
4. "提供*非常*紧密的近似"充满不安全感 → "提供紧密的近似"

### 来自Sebastian Farquhar
1. 方法部分应最多从第2-3页开始
2. 摘要公式：(1) 完成了什么，(2) 为什么难/重要，(3) 如何用关键词，(4-5) 证据+最佳数字
3. 引言必须有2-4项要点贡献列表（每项最多1-2行）

### 来自Gopen & Swan
1. 将强调放在句子结尾（应力位置）
2. 先放上下文（旧信息）再放新信息
3. 保持主语和动词靠近
4. 一个单元 = 一个功能（每个段落 = 一个要点）

---

## 第7部分：额外资源 | Part 7: Additional Resources

### 幻觉和AI写作问题 | Hallucination & AI Writing Concerns

| 来源 | 网址 |
|--------|-----|
| AI Hallucinations in Research Citations | https://www.enago.com/academy/ai-hallucinations-research-citations/ |
| Hallucination in AI-Generated Writing (PMC) | https://pmc.ncbi.nlm.nih.gov/articles/PMC10726751/ |
| NeurIPS 2025 AI Hallucination Report | https://byteiota.com/neurips-2025-100-ai-hallucinations-slip-through-review/ |

### ML会议审稿系统分析 | ML Conference Review System Analysis

| 来源 | 网址 |
|--------|-----|
| Position: ML Conferences Should Have Refutations Track | https://arxiv.org/html/2506.19882v1 |

---

## 技能开发使用说明 | Usage Notes for Skill Development

1. **对于论文结构**：从Nanda + Farquhar开始获取高层哲学，使用会议指南获取具体细节

2. **对于写作风格**：结合Lipton的启发式方法 + Gopen & Swan的原则 + Ethan Perez的微观技巧

3. **对于引文工作流**：实现Semantic Scholar → DOI验证 → CrossRef BibTeX管道；切勿从模型记忆生成引文

4. **对于图表/表格**：参考booktabs做表格，SciencePlots做图表，始终使用色盲安全的调色板

5. **对于审稿人模拟**：研究所有三个会议的审稿人指南以预测批评
