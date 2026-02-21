# AI 研究技能 - 演示库 | Demo Gallery

> **精选的演示仓库集合，展示技能的实际应用**

每个演示都是一个独立的仓库，展示如何使用此库中的特定技能来完成真实的 AI 研究任务。演示包含完整的代码、结果、分析和文档。

---

## 可用演示 | Available Demos

### 1. NeMo Evaluator: GPQA Diamond Benchmark

**仓库地址：** [zechenzhangAGI/Nemo-Eval-Skill-Demo](https://github.com/zechenzhangAGI/Nemo-Eval-Skill-Demo)

**使用的技能：** [NeMo Evaluator](../11-evaluation/nemo-evaluator/)

**功能描述：**
使用 NVIDIA NeMo Evaluator 在 GPQA Diamond 基准（198道研究生级别科学问题）上对比 Llama 模型（8B、70B、405B）。展示端到端的评估工作流程。

**主要结果：**
| 模型 | 准确率 | 备注 |
|-------|----------|-------|
| Llama-3.1-8B-Instruct | 27.3% | 20.7% 提取失败 |
| Llama-3.3-70B-Instruct | 48.0% | 清洁提取 |
| Llama-3.1-405B-Instruct | 53.0% | 最佳性能 |

**你将学到：**
- 使用 NVIDIA Build API 配置 NeMo Evaluator
- 为不同模型编写评估配置
- 跨模型规模分析基准测试结果
- 创建可视化图表（准确率图、韦恩图、失败分类图）

**仓库内容：**
```
├── configs/           # 每个模型的 YAML 配置
├── results/           # 原始评估输出
├── analysis/          # 分析脚本和可视化图表
│   ├── model_accuracy.png
│   ├── failure_taxonomy_plot.png
│   └── venn_diagrams.png
└── README.md          # 完整文档
```

---

### 2. 使用 AI Agent 复现 "LoRA Without Regret"

**仓库地址：** featured on [Orchestra Research Blog](https://www.orchestra-research.com/perspectives/LLM-with-Orchestra)

**使用的技能：** [GRPO RL Training](../06-post-training/grpo-rl-training/), [TRL Fine-Tuning](../06-post-training/trl-fine-tuning/)

**功能描述：**
通过**完全使用提示 AI Agent** 的方式复现 Thinking Machines Lab 的 "LoRA Without Regret" 论文成果。Agent 自立完成：
- 编写 SFT 和 GRPO 强化学习的训练代码
- 配置 H100 GPU 并通宵运行实验
- 执行 LoRA 秩消融研究（rank 1 到 256）
- 生成可直接发表的分析和可视化结果

**令人印象深刻的地方：**
研究人员只需描述他们想要复现的论文，AI Agent 就能处理一切——从理解方法论到执行多天 GPU 实验再到分析结果。无需手动编码。

**你将学到：**
- 如何提示 AI Agent 进行自主研究复现
- 端到端 SFT 和 GRPO 训练流程
- LoRA 与全参数微调的实验设计
- 自动化分析和报告

**资源：**
- [博客文章](https://www.orchestra-research.com/perspectives/LLM-with-Orchestra) - 完整教程
- [视频演示](https://www.youtube.com/watch?v=X0DoLYfXl5I) - 观看 Agent 实际操作

---

### 3. 逐层量化实验

**仓库地址：** [AmberLJC/llama-quantization-experiment](https://github.com/AmberLJC/llama-quantization-experiment)

**使用的技能：** [llama.cpp](../12-inference-serving/llama-cpp/), [GGUF](../10-optimization/gguf/)

**功能描述：**
研究量化 LLMs 的最优层精度分配。研究表明，早期层使用 Q8 可以实现 1.9 倍压缩，而困惑度损失仅为 1.3%——说明并非所有层在量化方面都同等重要。

**你将学到：**
- LLMs 的逐层量化策略
- 测量不同精度级别对各层困惑度的影响
- 使用 llama.cpp 和 GGUF 进行量化实验
- 识别哪些层对降低精度最敏感

---

### 4. 跨语言对齐分析

**仓库地址：** [AmberLJC/faiss-demo](https://github.com/AmberLJC/faiss-demo)

**使用的技能：** [FAISS](../15-rag/faiss/)

**功能描述：**
使用 FAISS 相似性搜索量化 8 种语言中多语言嵌入对齐语义概念的程度。揭示跨语言表示的结构以及对齐在哪里失效。

**你将学到：**
- 为多语言嵌入构建和查询 FAISS 索引
- 测量跨语言语义对齐质量
- 分析跨语言的嵌入空间结构
- 使用相似性搜索评估多语言模型

---

## 即将推出 | Coming Soon

### 5. ML 论文写作：从代码库到发表

**使用的技能：** [ML Paper Writing](../20-ml-paper-writing/)

**功能描述：**
将包含实验结果的研究代码库转换为可发表在顶级 ML 会议（NeurIPS、ICML、ICLR）的论文。

**计划内容：**
- 包含代码和结果的研究源代码库
- 生成的论文草稿（LaTeX）
- 引用验证工作流程
- 修改前后对比

*状态：开发中*

---

## 演示组织方式 | How Demos Are Organized

每个演示仓库遵循一致的结构：

```
demo-name/
├── README.md              # 概述、结果摘要、运行说明
├── configs/               # 配置文件
├── results/               # 原始输出和数据
├── analysis/              # 脚本和可视化图表
├── .env.example           # 所需环境变量
└── requirements.txt       # Python 依赖（如有）
```

**设计原则：**
- **自包含**：克隆即可运行，无需外部依赖（除 API 密钥外）
- **可复现**：清晰说明以复制结果
- **教育性**：解释"为什么"而不仅仅是"怎么做"
- **真实结果**：实际输出，非模拟数据

---

## 贡献演示 | Contributing a Demo

想要展示某个技能吗？我们欢迎演示贡献！

**要求：**
1. 使用此库中的一个或多个技能
2. 产生有意义的、可复现的结果
3. 包含清晰的文档
4. 有可视化输出（图表、表格、报告）

**贡献方式：**
1. 创建你的演示仓库
2. 遵循上述结构
3. 提交 issue 或 PR 将其添加到此索引

---

## 快速链接 | Quick Links

- [主技能库](../README.md)
- [全部 83 项技能](../README.md#available-ai-research-engineering-skills)
- [贡献指南](../CONTRIBUTING.md)
