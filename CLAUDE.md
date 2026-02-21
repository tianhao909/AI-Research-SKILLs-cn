# CLAUDE.md

本文件为 Claude Code (claude.ai/code) 在此仓库中工作时提供指导。

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 项目概览 | Project Overview

**AI 研究工程技能库 | AI Research Engineering Skills Library** - 一个全面的开源库，包含 54 个 AI 研究技能，旨在使 AI 代理能够自主进行 AI 研究实验。每个技能提供专家级指导（200-600 行），包含真实代码示例、故障排除指南和生产就绪的工作流程。

Each skill provides expert-level guidance (200-600 lines) with real code examples, troubleshooting guides, and production-ready workflows.

**使命 | Mission**: 使 AI 代理能够自主进行从假设到实验验证的 AI 研究，涵盖数据集准备、训练管道、模型部署和科学假设验证。

Enable AI agents to autonomously conduct AI research from hypothesis to experimental verification, covering dataset preparation, training pipelines, model deployment, and scientific hypothesis validation.

## 仓库架构 | Repository Architecture

### 目录结构 | Directory Structure（76 个技能跨越 19 个类别）

技能按编号分类组织，代表 AI 研究生命周期：

Skills are organized into numbered categories representing the AI research lifecycle:

- `01-model-architecture/` - 模型架构（5 个技能：Megatron-Core, LitGPT, Mamba, RWKV, NanoGPT）
- `02-tokenization/` - 分词器（2 个技能：HuggingFace Tokenizers, SentencePiece）
- `03-fine-tuning/` - 微调框架（4 个技能：Axolotl, LLaMA-Factory, Unsloth, Torchtune）
- `04-mechanistic-interpretability/` - 可解释性工具（4 个技能：TransformerLens, SAELens, NNsight, Pyvene）
- `05-data-processing/` - 数据整理（2 个技能：Ray Data, NeMo Curator）
- `06-post-training/` - RLHF/DPO/GRPO（4 个技能：TRL, GRPO, OpenRLHF, SimPO）
- `07-safety-alignment/` - 安全和护栏（4 个技能：Constitutional AI, LlamaGuard, NeMo Guardrails, Prompt Guard）
- `08-distributed-training/` - 分布式系统（5 个技能：DeepSpeed, FSDP, Accelerate, PyTorch Lightning, Ray Train）
- `09-infrastructure/` - 云计算（3 个技能：Modal, SkyPilot, Lambda Labs）
- `10-optimization/` - 优化技术（6 个技能：Flash Attention, bitsandbytes, GPTQ, AWQ, GGUF, Quanto）
- `11-evaluation/` - 基准测试（3 个技能：lm-evaluation-harness, NeMo Evaluator, Inspect AI）
- `12-inference-serving/` - 推理引擎（4 个技能：vLLM, TensorRT-LLM, llama.cpp, SGLang）
- `13-mlops/` - 实验跟踪（3 个技能：Weights & Wandb, MLflow, TensorBoard）
- `14-agents/` - 代理框架（4 个技能：LangChain, LlamaIndex, Smolagents, Claude Agent SDK）
- `15-rag/` - 检索增强生成（5 个技能：Chroma, FAISS, Sentence Transformers, Pinecone, Milvus）
- `16-prompt-engineering/` - 结构化输出（4 个技能：DSPy, Instructor, Guidance, Outlines）
- `17-observability/` - LLM 可观测性（2 个技能：LangSmith, Phoenix）
- `18-multimodal/` - 视觉和语音（7 个技能：CLIP, Whisper, LLaVA, Qwen2-VL, Pixtral, Florence-2, ColPali）
- `19-emerging-techniques/` - 高级方法（6 个技能：MoE Training, Model Merging, Long Context, Speculative Decoding, Knowledge Distillation, Model Pruning）

### 技能文件结构 | Skill File Structure

每个技能遵循标准化格式：

Each skill follows a standardized format:

```
skill-name/
├── SKILL.md                    # 主要指导（200-600 行，包含 YAML frontmatter）
│                               # Main guidance (200-600 lines with YAML frontmatter)
├── references/                 # 深度文档（300KB+ 目标）
│   ├── README.md              # 来自官方文档 | From official docs
│   ├── api.md                 # API 参考 | API reference
│   ├── tutorials.md           # 分步指南 | Step-by-step guides
│   ├── issues.md              # 真实 GitHub issues 和解决方案 | Real GitHub issues & solutions
│   └── releases.md            # 版本历史 | Version history
├── scripts/                    # 辅助脚本（可选） | Helper scripts (optional)
├── templates/                  # 代码模板（可选） | Code templates (optional)
└── examples/                   # 示例实现（可选） | Example implementations (optional)
```

## 技能质量标准 | Skill Quality Standards

### YAML Frontmatter 要求 | YAML Frontmatter Requirements (CRITICAL)

所有 `SKILL.md` 文件**必须**包含 YAML frontmatter，并使用以下精确字段：

All `SKILL.md` files MUST include YAML frontmatter with these exact fields:

```yaml
---
name: skill-name-here              # kebab-case，无引号，建议使用动名词形式 | gerund form preferred
description: 第三人称描述，说明什么 AND 何时使用此技能 | Third-person description of what AND when to use this skill  # 无引号，最多 1024 字符 | max 1024 chars
version: 1.0.0                     # 语义化版本 | Semantic versioning
author: Orchestra Research         # 标准作者 | Standard author
license: MIT                       # 标准许可证 | Standard license
tags: [Tag One, Tag Two]          # 标题大小写（Title Case），除了大写缩写词（如 GRPO, TRL, RLHF） | Title Case (except UPPERCASE acronyms like GRPO, TRL, RLHF)
dependencies: [pkg>=1.0.0]         # 可选，带版本约束 | Optional, with version constraints
---
```

**关键规则 | Critical Rules**:
- `name`: 使用动名词形式（例如 `serving-llms`, `processing-data`, `grpo-rl-training`）
- `description`: 第三人称（"Provides guidance for..."），包含**做什么**和**何时使用** | include WHAT it does AND WHEN to use it
- `tags`: 常规单词用标题大小写（Title Case），缩写词用大写（GRPO, TRL, RLHF, DPO, PPO）
- 任何字段值都不需要引号（数组除外） | No quotes around any field values (except in arrays)
- 依赖项应包含版本约束：`transformers>=4.47.0`

### 内容质量标准 | Content Quality Standards

**核心要求 | Core Requirements**（基于 Anthropic official best practices）:
- ✅ SKILL.md 正文：**200-500 行**（少于 500 行对性能至关重要）
- ✅ 渐进式披露：SKILL.md 作为概览，详细信息在单独的参考文件中
- ✅ 带有复制粘贴清单的工作流程，适用于复杂任务
- ✅ "何时使用与替代方案" 指导部分 | "When to use vs alternatives" guidance section
- ✅ 常见问题部分及解决方案 | Common issues section with solutions
- ✅ 简洁内容：假设 Claude 很聪明，不要过度解释基础知识
- ✅ 带语言检测的代码示例（```python, ```bash 等）
- ✅ 从 SKILL.md 引用**一层**深度（无嵌套引用） | References ONE level deep from SKILL.md (no nested references)

**黄金标准 | Gold Standard**（以此为目标 - 参见 `06-post-training/grpo-rl-training/`）:
- ✅ 2-3 个完整的工作流程，包含分步清单
- ✅ 参考文件用于高级主题（一层深度）
- ✅ 质量关键操作的反馈循环（验证 → 修复 → 重复）
- ✅ 整个文档中一致的术语 | Consistent terminology throughout
- ✅ 具体的输入/输出示例 | Concrete input/output examples
- ✅ 真实的 GitHub issues 及解决方案（如有）

**不可接受 | NOT Acceptable**:
- ❌ SKILL.md 超过 500 行（应拆分到参考文件中）
- ❌ 过度解释 Claude 已经知道的基础知识
- ❌ 第一人称描述（"I can help you..."）
- ❌ 模糊的技能名称（"helper", "utils", "tools"）
- ❌ 嵌套引用（SKILL.md → ref1.md → ref2.md）
- ❌ 复杂任务缺少带清单的工作流程

## 开发工作流 | Development Workflow

### 添加新技能 | Adding a New Skill

1. **从路线图中选择技能**（参见 CONTRIBUTING.md 或 README.md）
2. **在相应类别中创建目录结构**（01-19）
3. **编写 SKILL.md**，包含 YAML frontmatter，遵循上述标准
4. **添加参考文档**（目标 300KB+，来自官方来源）
5. **验证质量**：
   - 检查 SKILL.md 是否有 YAML frontmatter
   - 验证 SKILL.md 是否为 200-500 行
   - 确保代码块有语言标签
   - 确认引用从 SKILL.md 只有一层深度
   - 检查文档大小：`du -sh skill-name/references/`
6. **在提交前用真实用例测试技能**

### 改进现有技能 | Improving Existing Skills

更新技能时：
1. **维护 YAML frontmatter** 格式和字段
2. **保持 SKILL.md 少于 500 行** - 如需要拆分到参考文件中
3. **添加工作流程**，为复杂操作提供清单
4. **更新版本号**（在 YAML frontmatter 中）
5. **用代表性任务测试更改**

### 质量验证命令 | Quality Validation Commands

```bash
# 检查 YAML frontmatter 是否存在 | Check YAML frontmatter exists
head -20 skill-name/SKILL.md

# 验证 SKILL.md 行数（目标 200-500 行） | Verify SKILL.md line count (target 200-500 lines)
wc -l skill-name/SKILL.md

# 检查文档大小（目标 300KB+） | Check documentation size (target 300KB+)
du -sh skill-name/references/

# 验证代码块是否有语言标签 | Verify code blocks have language tags
grep -A 1 '```' skill-name/SKILL.md | head -20

# 验证 YAML frontmatter 语法 | Validate YAML frontmatter syntax
python -c "import yaml; yaml.safe_load(open('skill-name/SKILL.md').read().split('---')[1])"
```

## 关键文件 | Key Files

- **README.md** - 项目概览，列出所有 54 个技能及其描述和统计信息
- **CONTRIBUTING.md** - 完整的贡献指南和质量标准
- **SKILL_TEMPLATE.md** - 新技能的复制粘贴模板
- **ROADMAP.md** - 发展到 70 个技能的开发路线图
- **anthropic_official_docs/** - Anthropic 官方的技能最佳实践

## Git 工作流 | Git Workflow

标准 Git 工作流：

Standard Git workflow:
```bash
# 创建功能分支 | Create feature branch
git checkout -b add-skill-name

# 添加并提交更改 | Add and commit changes
git add category/skill-name/
git commit -m "Add [Skill Name] skill

- X lines of documentation
- Y GitHub issues with solutions
- API reference and examples included"

# 推送到 fork 并创建 PR | Push to fork and create PR
git push origin add-skill-name
```

## 自动化：Orchestra Skill Marketplace 同步 | Automation: Orchestra Skill Marketplace Sync

### 自动同步工作原理 | How Auto-Sync Works

当技能提交到 `main` 分支时，GitHub Actions 会自动将它们同步到 Orchestra skill marketplace：

When skills are committed to the `main` branch, GitHub Actions automatically syncs them to the Orchestra skill marketplace:

1. **GitHub Actions 检测** 推送到 `main` 时更改的技能文件夹
2. **对于每个更改的技能**：
   - 从 SKILL.md frontmatter 提取元数据（`name`, `author` 等）
   - 创建包含整个技能目录的 ZIP 文件（SKILL.md, references/, scripts/ 等）
   - 上传到 Orchestra API 端点
3. **Orchestra 存储** ZIP 到 Supabase Storage 并创建数据库记录
4. **技能显示在** marketplace: `https://orchestra.com/research-skills`

### 工作流文件位置 | Workflow File Location

- **文件**：`.github/workflows/sync-skills.yml`
- **触发器**：推送到 `main` 分支，手动工作流调度
- **同步内容**：仅在提交中更改的技能目录

### 作者检测（Orchestra vs Community） | Author Detection (Orchestra vs Community)

工作流从 SKILL.md frontmatter 读取 `author:` 字段以确定徽章：

The workflow reads the `author:` field from SKILL.md frontmatter to determine badge:

**官方 Orchestra Skill**:
```yaml
---
author: Orchestra Research  # 包含 "Orchestra" | Contains "Orchestra"
---
```
- 结果：Source = `orchestra`（官方徽章 | Official badge）
- 存储：`research-skills/orchestra/skill-name.zip`

**社区 Skill**:
```yaml
---
author: Jane Doe  # 不包含 "Orchestra" | Does NOT contain "Orchestra"
---
```
- 结果：Source = `community`（社区徽章 | Community badge）
- 存储：`research-skills/community/skill-name.zip`

### 同步内容 | What Gets Synced

工作流会压缩技能目录的**所有内容**：

The workflow zips **ALL contents** of skill directory:
- ✅ SKILL.md
- ✅ references/（所有子目录 | all subdirectories）
- ✅ scripts/（如存在 | if exists）
- ✅ assets/（如存在 | if exists）
- ✅ examples/（如存在 | if exists）
- ✅ templates/（如存在 | if exists）
- ❌ 隐藏文件（`.gitkeep`, `.DS_Store`）

### 测试同步 | Testing the Sync

**手动触发 | Manual trigger**:
1. 前往 GitHub Actions 标签页
2. 选择 "Sync Skills to Orchestra" 工作流
3. 点击 "Run workflow"

**用提交测试 | Test with commit**:
```bash
# 对任何技能做小改动
echo "\n<!-- Updated $(date) -->" >> 01-model-architecture/litgpt/SKILL.md

# 提交并推送到 main
git add .
git commit -m "test: trigger auto-sync"
git push origin main
```

**验证同步是否成功 | Verify sync worked**:
1. 在 GitHub Actions 标签页检查工作流运行状态
2. 在 Orchestra marketplace 检查更新的技能
3. 在 Supabase Storage 检查 ZIP 文件

### 重要说明 | Important Notes

- **需要 GitHub Secrets**：`ORCHESTRA_API_URL`, `ORCHESTRA_SYNC_API_KEY`（已配置）
- **仅同步更改的技能**：工作流检测提交中哪些技能目录发生了更改
- **SKILL.md 是必需的**：没有 SKILL.md 的技能会被跳过并发出警告
- **查看详细设置**：`dev_data/GITHUB_SKILLS_SYNC_SETUP.md`

## npm 包发布 | npm Package Publishing

### 工作原理 | How It Works

`publish-npm.yml` 工作流会在 `packages/ai-research-skills/package.json` 中的版本号在 `main` 分支上更改时自动发布到 npm。

The `publish-npm.yml` workflow auto-publishes to npm when the version in `packages/ai-research-skills/package.json` changes on `main`.

- **认证**：使用 OIDC 可信发布（无需 npm tokens）。在 npmjs.com 下该包的 Trusted Publishers 设置中配置。
- **可验证性**：`--provenance` 标志使用 Sigstore 签名包，用于供应链安全。
- **工作流**：`.github/workflows/publish-npm.yml`

### 升级版本 | Bumping Versions

**始终使用 `npm version`**（而非手动编辑），以保持 `package-lock.json` 同步：

**Always use `npm version`** (not manual edits) to keep `package-lock.json` in sync:

```bash
cd packages/ai-research-skills
npm version patch   # 1.3.6 → 1.3.7
npm version minor   # 1.3.7 → 1.4.0
npm version major   # 1.4.0 → 2.0.0
```

如果希望手动提交，使用 `--no-git-tag-version`。

### 常见问题 | Common Issues

- **`npm ci` fails in CI**: `package-lock.json` is out of sync. Run `npm install` locally and commit the lockfile.
  - **解决**：在本地运行 `npm install` 并提交 lockfile
  
- **OIDC auth fails**: The trusted publisher config on npmjs.com must match the repo exactly (case-sensitive: `Orchestra-Research/AI-Research-SKILLs`, workflow: `publish-npm.yml`).
  - **解决**：确保 npmjs.com 上的可信发布者配置与仓库完全匹配（区分大小写）
  
- **`NODE_AUTH_TOKEN` blocks OIDC**: `actions/setup-node` with `registry-url` auto-sets this token. The workflow unsets it before publish so OIDC takes over.
  - **解决**：工作流在发布前会取消设置此 token，以便 OIDC 接管
  
- **Version unchanged skip**: The workflow compares `HEAD` vs `HEAD~1`. If only the lockfile changed (not `package.json` version), publish is skipped. Bump the version to trigger.
  - **解决**：如果只有 lockfile 更改而 `package.json` 版本未变，发布会被跳过。需要升级版本来触发

## 重要约定 | Important Conventions

### 命名约定 | Naming Conventions

- **技能名**：使用动名词形式（动词 + -ing），kebab-case 格式：`processing-pdfs`, `serving-llms`, `grpo-rl-training`
- **标签**：单词用标题大小写（Title Case），缩写词用大写（GRPO, TRL, RLHF, DPO, PPO, FSDP, MoE）
- **描述**：第三人称，包含**做什么**和**何时使用**

### 代码示例 | Code Examples

始终在代码块中使用语言检测：

Always use language detection in code blocks:
```python
# Good - has language tag
from transformers import AutoModel
```

NOT:
```
# Bad - no language tag
from transformers import AutoModel
```

### 渐进式披露模式 | Progressive Disclosure Pattern

SKILL.md 应该直接链接到参考文件（一层深度）：

SKILL.md should link directly to reference files (one level deep):

```markdown
## Advanced Features

**API Reference**: See [references/api.md](references/api.md)
**Troubleshooting**: See [references/issues.md](references/issues.md)
```

## 理念 | Philosophy

**质量优于数量 | Quality over Quantity**: 本库通过以下方式保持高标准：

This library maintains high standards by:
- 要求 200-500 行的 SKILL.md 文件（专注、可操作的指导）
- 包含来自官方的 300KB+ 文档
- 提供真实的 GitHub issues 及解决方案
- 遵循 Anthropic 官方的技能最佳实践
- 在纳入之前用真实用例测试技能

每个技能都代表了专家级知识，经过提炼成适合 AI 代理消费的格式。

Each skill represents expert-level knowledge distilled into a format optimized for AI agent consumption.
