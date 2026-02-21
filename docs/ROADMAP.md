# 🗺️ 路线图 | Roadmap

## 愿景 | Vision

构建最全面的AI研究技能开源库，使AI代理能够自主进行从假设到部署的实验。

Build the most comprehensive open-source library of AI research skills, enabling AI agents to autonomously conduct experiments from hypothesis to deployment.

**目标**：第6个月完成70个综合技能

## 进度概览 | Progress Overview

| 指标 | 当前 | 目标 |
|--------|---------|--------|
| **技能** | **70**（高质量，标准化YAML） | 70 ✅ |
| **平均行数/技能** | **420行**（专注+渐进式披露） | 200-500行 |
| **文档** | **约115,000行**总计（SKILL.md +参考资料） | 100,000+行 |
| **黄金标准技能** | **58**个带全面参考资料 | 50+ |
| **覆盖范围** | 架构、分词、微调、数据处理、后训练、安全、分布式、基础设施、优化、评估、推理、代理、RAG、多模态、MLOps、可观察性、提示工程、新兴技术 | 完整生命周期 ✅ |

## 开发阶段 | Development Phases

### ✅ 阶段1：模型架构（已完成 - 5个技能）
**状态**：核心模型架构已覆盖

**已完成技能**：
- ✅ **Megatron-Core** - NVIDIA用于训练2B-462B参数模型的框架
- ✅ **LitGPT** - Lightning AI的20+个干净的LLM实现
- ✅ **Mamba** - O(n)复杂度的状态空间模型
- ✅ **RWKV** - RNN+Transformer混合，无限上下文
- ✅ **NanoGPT** - Karpathy的约300行教育版GPT

### ✅ 阶段2：分词（已完成 - 2个技能）
**状态**：基本分词框架已覆盖

**已完成技能**：
- ✅ **HuggingFace Tokenizers** - 基于Rust，支持BPE/WordPiece/Unigram
- ✅ **SentencePiece** - 语言无关的分词

### ✅ 阶段3：微调（已完成 - 4个技能）
**状态**：核心微调框架已覆盖

**已完成技能**：
- ✅ **Axolotl** - 基于YAML的微调，支持100+模型
- ✅ **LLaMA-Factory** - WebUI无代码微调
- ✅ **Unsloth** - 2倍速的QLoRA微调
- ✅ **PEFT** - 参数高效微调，支持LoRA、QLoRA、DoRA，25+方法

### ✅ 阶段4：数据处理（已完成 - 2个技能）
**状态**：分布式数据处理已覆盖

**已完成技能**：
- ✅ **Ray Data** - 分布式ML数据处理
- ✅ **NeMo Curator** - GPU加速数据整理

### ✅ 阶段5：后训练（已完成 - 4个技能）
**状态**：RLHF和对齐技术已覆盖

**已完成技能**：
- ✅ **TRL Fine-Tuning** - Transformer强化学习
- ✅ **GRPO-RL-Training** - 群组相对策略优化（黄金标准）
- ✅ **OpenRLHF** - 完整RLHF管道，配合Ray + vLLM
- ✅ **SimPO** - 简单偏好优化

### ✅ 阶段6：安全与对齐（已完成 - 4个技能）
**状态**：核心安全框架已覆盖

**已完成技能**：
- ✅ **Constitutional AI** - 通过原则的AI驱动自我改进
- ✅ **LlamaGuard** - LLM输入/输出安全分类器
- ✅ **NeMo Guardrails** - 使用Colang的可编程护栏
- ✅ **Prompt Guard** - Meta的8600万提示注入和越狱检测器

### ✅ 阶段7：分布式训练（已完成 - 5个技能）
**状态**：主要分布式训练框架已覆盖

**已完成技能**：
- ✅ **DeepSpeed** - Microsoft的ZeRO优化
- ✅ **PyTorch FSDP** - 完全分片数据并行
- ✅ **Accelerate** - HuggingFace的分布式训练API
- ✅ **PyTorch Lightning** - 高层训练框架
- ✅ **Ray Train** - 多节点编排

### ✅ 阶段8：优化（已完成 - 6个技能）
**状态**：核心优化技术已覆盖

**已完成技能**：
- ✅ **Flash Attention** - 内存效率2-4倍速的注意力
- ✅ **bitsandbytes** - 8位/4位量化
- ✅ **GPTQ** - 4位训练后量化
- ✅ **AWQ** - 激活感知权重量化
- ✅ **HQQ** - 无需校准数据的半二次量化
- ✅ **GGUF** - llama.cpp量化格式，用于CPU/Metal推理

## Development Phases

### ✅ Phase 1: Model Architecture (COMPLETE - 5 skills)
**Status**: Core model architectures covered

**Completed Skills**:
- ✅ **Megatron-Core** - NVIDIA's framework for training 2B-462B param models
- ✅ **LitGPT** - Lightning AI's 20+ clean LLM implementations
- ✅ **Mamba** - State-space models with O(n) complexity
- ✅ **RWKV** - RNN+Transformer hybrid, infinite context
- ✅ **NanoGPT** - Educational GPT in ~300 lines by Karpathy

### ✅ Phase 2: Tokenization (COMPLETE - 2 skills)
**Status**: Essential tokenization frameworks covered

**Completed Skills**:
- ✅ **HuggingFace Tokenizers** - rust-based, BPE/WordPiece/Unigram
- ✅ **SentencePiece** - Language-independent tokenization

### ✅ Phase 3: Fine-Tuning (COMPLETE - 4 skills)
**Status**: Core fine-tuning frameworks covered

**Completed Skills**:
- ✅ **Axolotl** - YAML-based fine-tuning with 100+ models
- ✅ **LLaMA-Factory** - WebUI no-code fine-tuning
- ✅ **Unsloth** - 2x faster QLoRA fine-tuning
- ✅ **PEFT** - Parameter-efficient fine-tuning with LoRA, QLoRA, DoRA, 25+ methods

### ✅ Phase 4: Data Processing (COMPLETE - 2 skills)
**Status**: Distributed data processing covered

**Completed Skills**:
- ✅ **Ray Data** - Distributed ML data processing
- ✅ **NeMo Curator** - GPU-accelerated data curation

### ✅ Phase 5: Post-Training (COMPLETE - 4 skills)
**Status**: RLHF and alignment techniques covered

**Completed Skills**:
- ✅ **TRL Fine-Tuning** - Transformer Reinforcement Learning
- ✅ **GRPO-RL-Training** - Group Relative Policy Optimization (gold standard)
- ✅ **OpenRLHF** - Full RLHF pipeline with Ray + vLLM
- ✅ **SimPO** - Simple Preference Optimization

### ✅ Phase 6: Safety & Alignment (COMPLETE - 4 skills)
**Status**: Core safety frameworks covered

**Completed Skills**:
- ✅ **Constitutional AI** - AI-driven self-improvement via principles
- ✅ **LlamaGuard** - Safety classifier for LLM inputs/outputs
- ✅ **NeMo Guardrails** - Programmable guardrails with Colang
- ✅ **Prompt Guard** - Meta's 86M prompt injection & jailbreak detector

### ✅ Phase 7: Distributed Training (COMPLETE - 5 skills)
**Status**: Major distributed training frameworks covered

**Completed Skills**:
- ✅ **DeepSpeed** - Microsoft's ZeRO optimization
- ✅ **PyTorch FSDP** - Fully Sharded Data Parallel
- ✅ **Accelerate** - HuggingFace's distributed training API
- ✅ **PyTorch Lightning** - High-level training framework
- ✅ **Ray Train** - Multi-node orchestration

### ✅ Phase 8: Optimization (COMPLETE - 6 skills)
**Status**: Core optimization techniques covered

**Completed Skills**:
- ✅ **Flash Attention** - 2-4x faster attention with memory efficiency
- ✅ **bitsandbytes** - 8-bit/4-bit quantization
- ✅ **GPTQ** - 4-bit post-training quantization
- ✅ **AWQ** - Activation-aware weight quantization
- ✅ **HQQ** - Half-Quadratic Quantization without calibration data
- ✅ **GGUF** - llama.cpp quantization format for CPU/Metal inference

### ✅ 阶段9：评估（已完成 - 1个技能）
**状态**：标准基准框架可用

**已完成技能**：
- ✅ **lm-evaluation-harness** - EleutherAI的LLM基准测试标准

### ✅ 阶段10：推理与服务（已完成 - 4个技能）
**状态**：生产推理框架已覆盖

**已完成技能**：
- ✅ **vLLM** - 带PagedAttention的高吞吐量LLM服务
- ✅ **TensorRT-LLM** - NVIDIA最快的推理
- ✅ **llama.cpp** - CPU/Apple Silicon推理
- ✅ **SGLang** - 使用RadixAttention的结构化生成

### ✅ 阶段10.5：基础设施（已完成 - 3个技能）
**状态**：云基础设施和编排已覆盖

**已完成技能**：
- ✅ **Modal** - Python原生API的无服务器GPU云，T4-H200按需
- ✅ **SkyPilot** - 跨20+提供商的多云编排，支持spot恢复
- ✅ **Lambda Labs** - 预留/按需GPU云，支持H100/A100，持久文件系统

### ✅ 阶段11：代理（已完成 - 4个技能）
**状态**：主要代理框架已覆盖

**已完成技能**：
- ✅ **LangChain** - 最流行的代理框架，500+集成
- ✅ **LlamaIndex** - LLM应用的数据框架，300+连接器
- ✅ **CrewAI** - 基于角色协作的多代理编排
- ✅ **AutoGPT** - 带可视化工作流构建器的自主AI代理平台

### ✅ 阶段12：RAG（已完成 - 5个技能）
**状态**：核心RAG和向量数据库技能已覆盖

**已完成技能**：
- ✅ **Chroma** - 开源嵌入数据库
- ✅ **FAISS** - Facebook相似性搜索，十亿级规模
- ✅ **Sentence Transformers** - 5000+嵌入模型
- ✅ **Pinecone** - 托管向量数据库
- ✅ **Qdrant** - 高性能Rust向量搜索，支持混合过滤

### ✅ 阶段13：多模态（已完成 - 7个技能）
**状态**：全面的多模态框架已覆盖

**已完成技能**：
- ✅ **CLIP** - OpenAI的视觉语言模型
- ✅ **Whisper** - 鲁棒语音识别，99种语言
- ✅ **LLaVA** - 视觉语言助手，GPT-4V级别
- ✅ **Stable Diffusion** - 通过HuggingFace Diffusers的文本到图像生成
- ✅ **Segment Anything (SAM)** - Meta的零样本图像分割，支持点/框/掩码
- ✅ **BLIP-2** - 使用Q-Former的视觉语言预训练，图像描述，VQA
- ✅ **AudioCraft** - Meta的MusicGen/AudioGen，用于文本到音乐和文本到声音

### ✅ 阶段14：高级优化（已完成）
**状态**：高级优化技术已覆盖（已合并到阶段8）

**注意**：HQQ和GGUF技能已完成并合并到阶段8：优化。

### ✅ 阶段15：MLOps与可观察性（已完成 - 5个技能）
**状态**：核心MLOps和LLM可观察性已覆盖

**已完成技能**：
- ✅ **MLflow** - 开源MLOps平台，用于跟踪实验
- ✅ **TensorBoard** - 可视化和实验跟踪
- ✅ **Weights & Biases** - 实验跟踪和协作
- ✅ **LangSmith** - LLM可观察性，跟踪，评估
- ✅ **Phoenix** - 开源AI可观察性，使用OpenTelemetry跟踪

### ✅ 阶段16：提示工程与高级应用（已完成 - 6个技能）
**状态**：核心提示工程和多代理工具已覆盖

**已完成技能**：
- ✅ **DSPy** - 声明式提示优化和LM编程
- ✅ **Guidance** - 约束生成和结构化提示
- ✅ **Instructor** - 使用Pydantic模型的结构化输出
- ✅ **Outlines** - 使用regex和语法的结构化文本生成
- ✅ **CrewAI** - 多代理编排（已在阶段11完成）
- ✅ **AutoGPT** - 自主代理（已在阶段11完成）

### ✅ 阶段17：扩展多模态（已完成）
**状态**：所有扩展多模态技能已完成，合并到阶段13

**注意**：BLIP-2、SAM和AudioCraft已完成并合并到阶段13：多模态。

### ✅ 阶段18：新兴技术（已完成 - 6个技能）
**状态**：核心新兴技术已覆盖

**已完成技能**：
- ✅ **MoE Training** - 使用DeepSpeed/HuggingFace的混合专家
- ✅ **Model Merging** - mergekit，SLERP和模型组合
- ✅ **Long Context** - RoPE扩展，ALiBi和上下文缩放
- ✅ **Speculative Decoding** - Medusa，Lookahead和草稿模型以加快推理
- ✅ **Knowledge Distillation** - MiniLLM，反向KLD，教师-学生训练
- ✅ **Model Pruning** - Wanda，SparseGPT和结构化剪枝

## 为路线图做贡献 | Contributing to the Roadmap

想要帮助我们实现这些目标吗？

1. **从路线图中选择一个技能** - 在[GitHub讨论区](https://github.com/orchestra-research/AI-research-SKILLs/discussions)评论以认领
2. **遵循[贡献指南](CONTRIBUTING.md)** - 使用我们的模板和质量标准
3. **提交您的PR** - 我们在48小时内审核

## 🎉 路线图完成！

所有70个技能已完成！该库现在涵盖完整的AI研究生命周期：

1. ✅ **阶段1-10**：核心ML基础设施（架构、分词、微调、数据处理、后训练、安全、分布式训练、优化、评估、推理）
2. ✅ **阶段10.5**：基础设施（Modal、SkyPilot、Lambda Labs）
3. ✅ **阶段11-12**：应用（代理、RAG）
4. ✅ **阶段13**：多模态（CLIP、Whisper、LLaVA、Stable Diffusion、SAM、BLIP-2、AudioCraft）
5. ✅ **阶段14-16**：高级（优化、MLOps与可观察性、提示工程）
6. ✅ **阶段17-18**：扩展（扩展多模态、新兴技术）

## 未来方向 | Future Directions

虽然70个技能的路线图已完成，库将继续发展：
- **更新**：保持现有技能与最新版本同步
- **社区贡献**：来自贡献者的额外技能
- **新兴工具**：新框架和技术成熟后的添加

## 理念 | Philosophy

**质量重于数量**：每个技能必须提供真正的价值并提供全面指导，而不仅仅是文档链接。我们的目标是每个技能提供300+行专家级内容，包含真实代码示例、故障排除指南和生产就绪工作流。

### ✅ Phase 9: Evaluation (COMPLETE - 1 skill)
**Status**: Standard benchmarking framework available

**Completed Skills**:
- ✅ **lm-evaluation-harness** - EleutherAI's standard for benchmarking LLMs

### ✅ Phase 10: Inference & Serving (COMPLETE - 4 skills)
**Status**: Production inference frameworks covered

**Completed Skills**:
- ✅ **vLLM** - High-throughput LLM serving with PagedAttention
- ✅ **TensorRT-LLM** - NVIDIA's fastest inference
- ✅ **llama.cpp** - CPU/Apple Silicon inference
- ✅ **SGLang** - Structured generation with RadixAttention

### ✅ Phase 10.5: Infrastructure (COMPLETE - 3 skills)
**Status**: Cloud infrastructure and orchestration covered

**Completed Skills**:
- ✅ **Modal** - Serverless GPU cloud with Python-native API, T4-H200 on-demand
- ✅ **SkyPilot** - Multi-cloud orchestration across 20+ providers with spot recovery
- ✅ **Lambda Labs** - Reserved/on-demand GPU cloud with H100/A100, persistent filesystems

### ✅ Phase 11: Agents (COMPLETE - 4 skills)
**Status**: Major agent frameworks covered

**Completed Skills**:
- ✅ **LangChain** - Most popular agent framework, 500+ integrations
- ✅ **LlamaIndex** - Data framework for LLM apps, 300+ connectors
- ✅ **CrewAI** - Multi-agent orchestration with role-based collaboration
- ✅ **AutoGPT** - Autonomous AI agent platform with visual workflow builder

### ✅ Phase 12: RAG (COMPLETE - 5 skills)
**Status**: Core RAG and vector database skills covered

**Completed Skills**:
- ✅ **Chroma** - Open-source embedding database
- ✅ **FAISS** - Facebook's similarity search, billion-scale
- ✅ **Sentence Transformers** - 5000+ embedding models
- ✅ **Pinecone** - Managed vector database
- ✅ **Qdrant** - High-performance Rust vector search with hybrid filtering

### ✅ Phase 13: Multimodal (COMPLETE - 7 skills)
**Status**: Comprehensive multimodal frameworks covered

**Completed Skills**:
- ✅ **CLIP** - OpenAI's vision-language model
- ✅ **Whisper** - Robust speech recognition, 99 languages
- ✅ **LLaVA** - Vision-language assistant, GPT-4V level
- ✅ **Stable Diffusion** - Text-to-image generation via HuggingFace Diffusers
- ✅ **Segment Anything (SAM)** - Meta's zero-shot image segmentation with points/boxes/masks
- ✅ **BLIP-2** - Vision-language pretraining with Q-Former, image captioning, VQA
- ✅ **AudioCraft** - Meta's MusicGen/AudioGen for text-to-music and text-to-sound

### ✅ Phase 14: Advanced Optimization (COMPLETE)
**Status**: Advanced optimization techniques covered (merged into Phase 8)

### ✅ Phase 15: MLOps & Observability (COMPLETE - 5 skills)
**Status**: Core MLOps and LLM observability covered

### ✅ Phase 16: Prompt Engineering & Advanced Applications (COMPLETE - 6 skills)
**Status**: Core prompt engineering and multi-agent tools covered

### ✅ Phase 17: Extended Multimodal (COMPLETE)
**Status**: All extended multimodal skills complete, merged into Phase 13

### ✅ Phase 18: Emerging Techniques (COMPLETE - 6 skills)
**Status**: Core emerging techniques covered

## Contributing to the Roadmap

## 🎉 Roadmap Complete!

All 70 skills have been completed! The library now covers the full AI research lifecycle:

## Future Directions

## Philosophy

**Quality over Quantity**: Each skill must provide real value with comprehensive guidance, not just links to docs. We aim for 300+ lines of expert-level content per skill, with real code examples, troubleshooting guides, and production-ready workflows.
