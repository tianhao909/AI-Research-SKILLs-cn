# 引用管理与幻觉预防 | Citation Management & Hallucination Prevention

本文档提供了完整的编程引用管理工作流，防止AI生成的引用幻觉，并维护干净的参考文献。

---

## 目录 | Contents

- [为什么引用验证很重要](#为什么引用验证很重要)
- [引用API概述](#引用api概述)
- [已验证引用工作流](#已验证引用工作流)
- [Python实现](#python实现)
- [BibTeX管理](#bibtex管理)
- [常见引用格式](#常见引用格式)
- [故障排除](#故障排除)

---

## 为什么引用验证很重要 | Why Citation Verification Matters

### 幻觉问题

研究记录了AI生成引用的重大问题：
- AI生成引用的**错误率约40%**（Enago Academy研究）
- NeurIPS 2025发现**100多个幻觉引用**通过了审稿
- 常见错误包括：
  - 使用真实作者姓名的伪造论文标题
  - 错误的发表场所或年份
  - 具有合理元数据的不存在论文
  - 错误的DOI或arXiv ID

### 后果

- 某些场所的直接拒稿
- 失去审稿人的信誉
- 如已发表可能撤回
- 浪费时间追查不存在的来源

### 解决方案

**永远不要凭记忆生成引用——始终通过编程验证。**

---

## 引用API概述 | Citation APIs Overview

### 主要API

| API | 覆盖范围 | 速率限制 | 最佳用途 |
|-----|----------|-------------|----------|
| **Semantic Scholar** | 2.14亿篇论文 | 1 RPS（免费密钥）| ML/AI论文，引用图 |
| **CrossRef** | 1.40亿+ DOI | 礼貌池带mailto | DOI查询，BibTeX检索 |
| **arXiv** | 预印本 | 3秒延迟 | ML预印本，PDF访问 |
| **OpenAlex** | 2.40亿+作品 | 100K/天，10 RPS | MAG的开源替代 |

### API选择指南

```
需要ML论文搜索？→ Semantic Scholar
有DOI，需要BibTeX？→ CrossRef内容协商
寻找预印本？→ arXiv API
需要开放数据，批量访问？→ OpenAlex
```

### 没有官方Google Scholar API

Google Scholar没有官方API。爬取违反服务条款。仅当Semantic Scholar覆盖不足时使用SerpApi（$75-275/月）。

---

## 已验证引用工作流 | Verified Citation Workflow

### 5步流程

```
1. 搜索 → 使用特定关键词查询Semantic Scholar
     ↓
2. 验证 → 确认论文在2个以上来源存在
     ↓
3. 检索 → 通过DOI内容协商获取BibTeX
     ↓
4. 验证 → 确认来源中包含该声明
     ↓
5. 添加 → 将验证条目添加到.bib文件
```

### 步骤1：搜索

使用Semantic Scholar搜索ML/AI论文：

```python
from semanticscholar import SemanticScholar

sch = SemanticScholar()
results = sch.search_paper("transformer attention mechanism", limit=10)

for paper in results:
    print(f"Title: {paper.title}")
    print(f"Year: {paper.year}")
    print(f"DOI: {paper.externalIds.get('DOI', 'N/A')}")
    print(f"arXiv: {paper.externalIds.get('ArXiv', 'N/A')}")
    print(f"Citation count: {paper.citationCount}")
    print("---")
```

### 步骤2：验证存在

确认论文在至少两个来源中存在：

```python
import requests

def verify_paper(doi=None, arxiv_id=None, title=None):
    """验证论文在多个来源中存在。"""
    sources_found = []

    # 检查Semantic Scholar
    sch = SemanticScholar()
    if doi:
        paper = sch.get_paper(f"DOI:{doi}")
        if paper:
            sources_found.append("Semantic Scholar")

    # 通过DOI检查CrossRef
    if doi:
        resp = requests.get(f"https://api.crossref.org/works/{doi}")
        if resp.status_code == 200:
            sources_found.append("CrossRef")

    # 检查arXiv
    if arxiv_id:
        resp = requests.get(
            f"http://export.arxiv.org/api/query?id_list={arxiv_id}"
        )
        if "<entry>" in resp.text:
            sources_found.append("arXiv")

    return len(sources_found) >= 2, sources_found
```

### 步骤3：检索BibTeX

使用DOI内容协商保证准确性：

```python
import requests

def doi_to_bibtex(doi: str) -> str:
    """通过CrossRef内容协商从DOI获取已验证的BibTeX。"""
    response = requests.get(
        f"https://doi.org/{doi}",
        headers={"Accept": "application/x-bibtex"},
        allow_redirects=True
    )
    response.raise_for_status()
    return response.text

# 示例："Attention Is All You Need"
bibtex = doi_to_bibtex("10.48550/arXiv.1706.03762")
print(bibtex)
```

### 步骤4：验证声明

在引用特定声明之前，验证该声明存在于论文中：

```python
def get_paper_abstract(doi):
    """获取摘要以验证声明。"""
    sch = SemanticScholar()
    paper = sch.get_paper(f"DOI:{doi}")
    return paper.abstract if paper else None

# 验证声明出现在摘要中
abstract = get_paper_abstract("10.48550/arXiv.1706.03762")
claim = "attention mechanism"
if claim.lower() in abstract.lower():
    print("Claim appears in paper")
```

### 步骤5：添加到参考文献

使用一致的键格式将验证条目添加到.bib文件：

```python
def generate_citation_key(bibtex: str) -> str:
    """生成一致的引用键：author_year_firstword。"""
    import re

    # 提取作者
    author_match = re.search(r'author\s*=\s*\{([^}]+)\}', bibtex, re.I)
    if author_match:
        first_author = author_match.group(1).split(',')[0].split()[-1]
    else:
        first_author = "unknown"

    # 提取年份
    year_match = re.search(r'year\s*=\s*\{?(\d{4})\}?', bibtex, re.I)
    year = year_match.group(1) if year_match else "0000"

    # 提取标题第一个词
    title_match = re.search(r'title\s*=\s*\{([^}]+)\}', bibtex, re.I)
    if title_match:
        first_word = title_match.group(1).split()[0].lower()
        first_word = re.sub(r'[^a-z]', '', first_word)
    else:
        first_word = "paper"

    return f"{first_author.lower()}_{year}_{first_word}"
```

---

## Python实现 | Python Implementation

### 完整的引用管理器类

```python
"""
引用管理器 - ML论文的已验证引用工作流。
"""

import requests
import time
from typing import Optional, List, Dict, Tuple
from dataclasses import dataclass

try:
    from semanticscholar import SemanticScholar
except ImportError:
    print("安装：pip install semanticscholar")
    SemanticScholar = None

@dataclass
class Paper:
    title: str
    authors: List[str]
    year: int
    doi: Optional[str]
    arxiv_id: Optional[str]
    venue: Optional[str]
    citation_count: int
    abstract: Optional[str]

class CitationManager:
    """管理已验证的引用。"""

    def __init__(self, api_key: Optional[str] = None):
        self.sch = SemanticScholar(api_key=api_key) if SemanticScholar else None
        self.verified_papers: Dict[str, Paper] = {}

    def search(self, query: str, limit: int = 10) -> List[Paper]:
        """使用Semantic Scholar搜索论文。"""
        if not self.sch:
            raise RuntimeError("Semantic Scholar不可用")

        results = self.sch.search_paper(query, limit=limit)
        papers = []

        for r in results:
            paper = Paper(
                title=r.title,
                authors=[a.name for a in (r.authors or [])],
                year=r.year or 0,
                doi=r.externalIds.get('DOI') if r.externalIds else None,
                arxiv_id=r.externalIds.get('ArXiv') if r.externalIds else None,
                venue=r.venue,
                citation_count=r.citationCount or 0,
                abstract=r.abstract
            )
            papers.append(paper)

        return papers

    def verify(self, paper: Paper) -> Tuple[bool, List[str]]:
        """验证论文在多个来源中存在。"""
        sources = []

        # 已通过搜索在Semantic Scholar中找到
        sources.append("Semantic Scholar")

        # 如果有DOI则检查CrossRef
        if paper.doi:
            try:
                resp = requests.get(
                    f"https://api.crossref.org/works/{paper.doi}",
                    timeout=10
                )
                if resp.status_code == 200:
                    sources.append("CrossRef")
            except:
                pass

        # 如果有ID则检查arXiv
        if paper.arxiv_id:
            try:
                resp = requests.get(
                    f"http://export.arxiv.org/api/query?id_list={paper.arxiv_id}",
                    timeout=10
                )
                if "<entry>" in resp.text and "<title>" in resp.text:
                    sources.append("arXiv")
            except:
                pass

        return len(sources) >= 2, sources

    def get_bibtex(self, paper: Paper) -> Optional[str]:
        """获取已验证论文的BibTeX。"""
        if paper.doi:
            try:
                resp = requests.get(
                    f"https://doi.org/{paper.doi}",
                    headers={"Accept": "application/x-bibtex"},
                    timeout=10,
                    allow_redirects=True
                )
                if resp.status_code == 200:
                    return resp.text
            except:
                pass

        # 回退：从论文数据生成
        return self._generate_bibtex(paper)

    def _generate_bibtex(self, paper: Paper) -> str:
        """从论文元数据生成BibTeX。"""
        # 生成引用键
        first_author = paper.authors[0].split()[-1] if paper.authors else "unknown"
        first_word = paper.title.split()[0].lower().replace(',', '').replace(':', '')
        key = f"{first_author.lower()}_{paper.year}_{first_word}"

        # 格式化作者
        authors = " and ".join(paper.authors) if paper.authors else "Unknown"

        bibtex = f"""@article{{{key},
  title = {{{paper.title}}},
  author = {{{authors}}},
  year = {{{paper.year}}},
  {'doi = {' + paper.doi + '},' if paper.doi else ''}
  {'eprint = {' + paper.arxiv_id + '},' if paper.arxiv_id else ''}
  {'journal = {' + paper.venue + '},' if paper.venue else ''}
}}"""
        return bibtex

    def cite(self, query: str) -> Optional[str]:
        """完整工作流：搜索，验证，返回BibTeX。"""
        # 搜索
        papers = self.search(query, limit=5)
        if not papers:
            return None

        # 取最优结果
        paper = papers[0]

        # 验证
        verified, sources = self.verify(paper)
        if not verified:
            print(f"警告：只能验证来源：{sources}")

        # 获取BibTeX
        bibtex = self.get_bibtex(paper)

        # 缓存
        if bibtex:
            self.verified_papers[paper.title] = paper

        return bibtex


# 使用示例
if __name__ == "__main__":
    cm = CitationManager()

    # 搜索并引用
    bibtex = cm.cite("attention is all you need transformer")
    if bibtex:
        print(bibtex)
```

### 快速函数

```python
def quick_cite(query: str) -> str:
    """一行引用。"""
    cm = CitationManager()
    return cm.cite(query)

def batch_cite(queries: List[str], output_file: str = "references.bib"):
    """引用多篇论文并保存到文件。"""
    cm = CitationManager()
    bibtex_entries = []

    for query in queries:
        print(f"处理中：{query}")
        bibtex = cm.cite(query)
        if bibtex:
            bibtex_entries.append(bibtex)
        time.sleep(1)  # 速率限制

    with open(output_file, 'w') as f:
        f.write("\n\n".join(bibtex_entries))

    print(f"已保存{len(bibtex_entries)}个引用到{output_file}")
```

---

## BibTeX管理 | BibTeX Management

### BibTeX vs BibLaTeX

| 特性 | BibTeX | BibLaTeX |
|---------|--------|----------|
| Unicode支持 | 有限 | 完整 |
| 条目类型 | 标准 | 扩展（@online, @dataset）|
| 自定义 | 有限 | 高度灵活 |
| 后端 | bibtex | Biber（推荐）|

**建议**：新论文使用BibLaTeX和Biber。

### LaTeX设置

```latex
% 在导言区
\usepackage[
    backend=biber,
    style=numeric,
    sorting=none
]{biblatex}
\addbibresource{references.bib}

% 在文档中
\cite{vaswani_2017_attention}

% 在末尾
\printbibliography
```

### 引用命令

```latex
\cite{key}      % 数字：[1]
\citep{key}     % 圆括号：(Author, 2020)
\citet{key}     % 文字：Author (2020)
\citeauthor{key} % 仅作者名
\citeyear{key}  % 仅年份
```

### 一致的引用键

使用格式：`author_year_firstword`

```
vaswani_2017_attention
devlin_2019_bert
brown_2020_language
```

---

## 常见引用格式 | Common Citation Formats

### 会议论文

```bibtex
@inproceedings{vaswani_2017_attention,
  title = {Attention Is All You Need},
  author = {Vaswani, Ashish and Shazeer, Noam and Parmar, Niki and
            Uszkoreit, Jakob and Jones, Llion and Gomez, Aidan N and
            Kaiser, Lukasz and Polosukhin, Illia},
  booktitle = {Advances in Neural Information Processing Systems},
  volume = {30},
  year = {2017},
  publisher = {Curran Associates, Inc.}
}
```

### 期刊文章

```bibtex
@article{hochreiter_1997_long,
  title = {Long Short-Term Memory},
  author = {Hochreiter, Sepp and Schmidhuber, J{\"u}rgen},
  journal = {Neural Computation},
  volume = {9},
  number = {8},
  pages = {1735--1780},
  year = {1997},
  publisher = {MIT Press}
}
```

### arXiv预印本

```bibtex
@misc{brown_2020_language,
  title = {Language Models are Few-Shot Learners},
  author = {Brown, Tom and Mann, Benjamin and Ryder, Nick and others},
  year = {2020},
  eprint = {2005.14165},
  archiveprefix = {arXiv},
  primaryclass = {cs.CL}
}
```

---

## 故障排除 | Troubleshooting

### 常见问题

**问题：Semantic Scholar返回无结果**
- 尝试更具体的关键词
- 检查作者姓名拼写
- 对精确短语使用引号

**问题：DOI无法解析为BibTeX**
- DOI可能已注册但未链接到CrossRef
- 如有arXiv ID可尝试
- 手动从元数据生成BibTeX

**问题：速率限制错误**
- 在请求之间添加延迟（1-3秒）
- 如有API密钥则使用
- 缓存结果以避免重复查询

**问题：BibTeX编码问题**
- 使用正确的LaTeX转义：`{\"u}` 表示 ü
- 确保文件是UTF-8编码
- 使用BibLaTeX和Biber获得更好的Unicode支持

### 验证清单

添加引用前：

- [ ] 论文在至少2个来源中找到
- [ ] DOI或arXiv ID已验证
- [ ] BibTeX已检索（不是凭记忆生成）
- [ ] 条目类型正确（@inproceedings vs @article）
- [ ] 作者姓名完整且格式正确
- [ ] 年份和场所已验证
- [ ] 引用键遵循一致格式

---

## 其他资源 | Additional Resources

**API：**
- Semantic Scholar: https://api.semanticscholar.org/api-docs/
- CrossRef: https://www.crossref.org/documentation/retrieve-metadata/rest-api/
- arXiv: https://info.arxiv.org/help/api/basics.html
- OpenAlex: https://docs.openalex.org/

**Python库：**
- `semanticscholar`: https://pypi.org/project/semanticscholar/
- `arxiv`: https://pypi.org/project/arxiv/
- `habanero` (CrossRef): https://github.com/sckott/habanero

**验证工具：**
- Citely: https://citely.ai/citation-checker
- ReciteWorks: https://reciteworks.com/
