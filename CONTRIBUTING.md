# 贡献指南 | Contributing to Claude AI Research Skills

感谢您有兴趣做出贡献！本指南将帮助您向库中添加新技能。

Thank you for your interest in contributing! This guide will help you add new skills to the library.

---

## 🎯 我们的目标 | What We're Building

**愿景 | Vision**: 最全面的开源 AI 研究技能库，专为 Claude Code 设计。

**Target**: 70 comprehensive skills covering the entire AI research lifecycle—from model architecture to production deployment.

**当前进展 | Current Progress**: 7/70 skills (10%)

**理念 | Philosophy**: Quality > Quantity (质量优于数量). We deleted 9 low-quality skills to maintain high standards.

---

## 🤝 如何贡献 | How to Contribute

### 贡献方式 | Ways to Contribute

1. **Add a new skill** (添加新技能) - Most valuable contribution
2. **Improve existing skills** (改进现有技能) - Update docs, add examples, fix errors
3. **Report issues** (报告问题) - Outdated information, broken links, missing content
4. **Share feedback** (分享反馈) - What skills do you need? What's missing?

---

## 📝 添加新技能 | Adding a New Skill

### Step 1: Choose a Skill (选择一个技能)
### Step 2: Fork and Clone (分叉并克隆)

```bash
# Fork the repository on GitHub first
git clone https://github.com/YOUR_USERNAME/AI-research-SKILLs.git
cd claude-ai-research-skills

# Create a feature branch
git checkout -b add-vllm-skill
```

### Step 3: Use Skill Seeker MCP (使用 Skill Seeker MCP)

**Option A: Documentation Scraping** (选项 A：文档爬取)
```bash
# Create config file
python3 cli/doc_scraper.py --interactive
# Or copy and modify an existing config
# 或者复制并修改现有配置
cp configs/react.json configs/vllm.json

# Scrape and build
python3 cli/doc_scraper.py --config configs/vllm.json
```

**Option B: GitHub Scraping** (选项 B：GitHub 爬取)
```bash
# Scrape from GitHub repository
export GITHUB_TOKEN=$(gh auth token)
python3 cli/github_scraper.py --repo vllm-project/vllm --name vllm --description "High-performance LLM inference with PagedAttention"
```

**Option C: Unified Scraping** (recommended for comprehensive skills) (推荐用于综合技能)
```bash
# Combine documentation + GitHub + PDF
python3 cli/unified_scraper.py --config configs/vllm_unified.json
```

### Step 4: Move to Correct Directory (移动到正确的目录)

```bash
# Determine the category (see directory structure below)
git mv output/vllm/ 12-inference-serving/vllm/

# Move metadata
git mv output/vllm_data/ .metadata/vllm_data/
```

### Step 5: Validate Quality (验证质量)

**Based on [Anthropic Official Best Practices](anthropic_official_docs/best_practices.md)**

**Core Requirements** (or skill will be rejected) (核心要求，否则技能将被拒绝):
- ✅ YAML frontmatter with `name` (gerund form, e.g., "serving-llms") and `description` (third person, includes what AND when) (YAML 元数据，包含 name（动名词形式）和 description（第三人称，包含什么和何时使用）)
- ✅ SKILL.md body: **200-300 lines** (under 500 lines maximum) (SKILL.md 正文：200-300 行，最多不超过 500 行)
- ✅ Progressive disclosure: SKILL.md as overview, details in separate reference files (渐进式披露：SKILL.md 作为概述，详情在单独的参考文件中)
- ✅ Workflows with copy-paste checklists for complex tasks (针对复杂任务的工作流，包含可复制粘贴的清单)
- ✅ When to use vs alternatives guidance (何时使用与替代方案的指导)
- ✅ Common issues section with solutions (常见问题部分及解决方案)
- ✅ Concise content: assume Claude is smart, no over-explaining basics (简洁内容：假设 Claude 很聪明，不要过度解释基础知识)
- ✅ Code examples with language detection (```python, ```bash, etc.) (带语言检测的代码示例)

**Gold Standard** (aim for this):
- ✅ SKILL.md: 200-300 lines of focused, actionable guidance
- ✅ 2-3 complete workflows with step-by-step checklists
- ✅ Reference files for advanced topics (one level deep from SKILL.md)
- ✅ Feedback loops (validate → fix → repeat) for quality-critical operations
- ✅ Consistent terminology throughout
- ✅ Concrete examples (input/output pairs where helpful)
- ✅ Clear, concise troubleshooting guide

**NOT Acceptable**:
- ❌ SKILL.md over 500 lines (split into reference files instead)
- ❌ Over-explaining basics that Claude already knows
- ❌ First-person descriptions ("I can help you...")
- ❌ Vague skill names ("helper", "utils", "tools")
- ❌ Nested references (SKILL.md → ref1.md → ref2.md)
- ❌ Generic templates that just link to README/CHANGELOG
- ❌ Missing workflows with checklists for complex tasks
- ❌ Time-sensitive information (use "old patterns" section instead)

**Quick Quality Check**:
```bash
# Check SKILL.md has real code examples
cat 12-inference-serving/vllm/SKILL.md

# Check reference files exist
ls -lh 12-inference-serving/vllm/references/

# Verify total documentation size (should be 300KB+)
du -sh 12-inference-serving/vllm/references/
```

### YAML Frontmatter Format Standards

All SKILL.md files **must** include properly formatted YAML frontmatter with the following fields:

```yaml
---
name: skill-name-here
description: Clear description of when to use this skill
version: 1.0.0
author: Orchestra Research
license: MIT
tags: [Tag One, Tag Two, Tag Three]
dependencies: [package1>=1.0.0, package2>=2.0.0]
---
```

**Field Requirements:**

| Field | Required | Format | Notes |
|-------|----------|--------|-------|
| `name` | ✅ Yes | kebab-case | No quotes, lowercase with hyphens |
| `description` | ✅ Yes | Plain text | No quotes, concise explanation |
| `version` | ✅ Yes | Semantic version | Format: `MAJOR.MINOR.PATCH` |
| `author` | ✅ Yes | Plain text | Use "Orchestra Research" |
| `license` | ✅ Yes | License identifier | Typically `MIT` |
| `tags` | ✅ Yes | Array | Capitalized words, no quotes |
| `dependencies` | ⚠️ Optional | Array | Include version constraints |

**Tag Guidelines:**
- Use **Title Case** for all tags (capitalize first letter of each word)
- Keep acronyms **UPPERCASE** (e.g., `GRPO`, `TRL`, `RLHF`, `DPO`)
- Use descriptive, searchable terms
- Include 5-10 relevant tags
- No quotes around tags

**Example Tags:**
```yaml
tags: [Reinforcement Learning, GRPO, TRL, Post-Training, RLHF, Reward Modeling]
```

**Dependencies Guidelines:**
- Only include **direct dependencies** needed to use the skill
- Include **minimum version constraints** using `>=`
- No quotes around package names
- List core packages first, optional packages last

**Example Dependencies:**
```yaml
dependencies: [transformers>=4.47.0, trl>=0.14.0, datasets>=3.2.0, peft>=0.14.0, torch]
```

**Complete Example:**
```yaml
---
name: grpo-rl-training
description: Expert guidance for GRPO/RL fine-tuning with TRL for reasoning and task-specific model training
version: 1.0.0
author: Orchestra Research
license: MIT
tags: [Reinforcement Learning, GRPO, TRL, Post-Training, RLHF, Reward Modeling, Reasoning, DPO, PPO, Structured Output]
dependencies: [transformers>=4.47.0, trl>=0.14.0, datasets>=3.2.0, peft>=0.14.0, torch]
---
```

**Validation Checklist:**
- [ ] YAML frontmatter is present at the very beginning of SKILL.md
- [ ] All required fields are included
- [ ] No quotes around field values (except in arrays)
- [ ] Tags use Title Case (capitalized words)
- [ ] Dependencies include version constraints where appropriate
- [ ] YAML is valid (test with: `python -c "import yaml; yaml.safe_load(open('SKILL.md').read().split('---')[1])"`)

### Step 6: Update Marketplace

Add your skill to `.claude-plugin/marketplace.json` so it appears in the Claude Code plugin marketplace.

**Add a new entry to the `plugins` array:**
```json
{
  "name": "your-skill-name",
  "source": "./XX-category/skill-folder",
  "description": "Description from your SKILL.md frontmatter (what it does AND when to use it)"
}
```

**Example:**
```json
{
  "name": "serving-llms-vllm",
  "source": "./12-inference-serving/vllm",
  "description": "Serves LLMs with high throughput using vLLM's PagedAttention and continuous batching. Use when deploying production LLM APIs or optimizing inference latency/throughput."
}
```

**Validation:**
```bash
# Verify JSON is valid after editing
python3 -c "import json; json.load(open('.claude-plugin/marketplace.json'))"
```

**Important**: Place your entry in the correct position (skills are ordered by category number).

### Step 7: Submit Pull Request

```bash
# Add your changes
git add 12-inference-serving/vllm/
git add .metadata/vllm_data/
git add .claude-plugin/marketplace.json

# Commit with descriptive message
git commit -m "Add vLLM inference serving skill

- 215 pages of documentation
- 12 GitHub issues with solutions
- API reference and examples
- Performance benchmarks included"

# Push to your fork
git push origin add-vllm-skill
```

Then create a Pull Request on GitHub with:
- **Title**: "Add [Skill Name] skill"
- **Description**:
  - What the skill covers
  - Source (docs, GitHub, or both)
  - Documentation size
  - Key features/examples included

---

## 📂 Directory Structure

Place skills in the correct category:

```
claude-ai-research-skills/
├── 01-model-architecture/      # Model architectures (GPT, LLaMA, etc.)
├── 02-tokenization/            # Tokenizers (HuggingFace, SentencePiece)
├── 03-fine-tuning/             # Fine-tuning frameworks (Axolotl, TRL)
├── 04-peft/                    # Parameter-efficient methods (LoRA, QLoRA)
├── 05-data-processing/         # Data curation and processing
├── 06-post-training/           # RLHF, DPO, PPO
├── 07-safety-alignment/        # Guardrails, safety, content moderation
├── 08-distributed-training/    # DeepSpeed, FSDP, distributed systems
├── 09-infrastructure/          # PyTorch Lightning, Ray, Composer
├── 10-optimization/            # Flash Attention, bitsandbytes, kernels
├── 11-evaluation/              # Benchmarks, evaluation frameworks
├── 12-inference-serving/       # vLLM, TensorRT-LLM, llama.cpp
├── 13-mlops/                   # Weights & Biases, MLflow, TensorBoard
├── 14-agents/                  # LangChain, LlamaIndex, CrewAI
├── 15-rag/                     # RAG pipelines, vector databases
├── 16-prompt-engineering/      # DSPy, Instructor, structured output
├── 17-observability/           # LangSmith, Phoenix, monitoring
├── 18-multimodal/              # LLaVA, Whisper, Stable Diffusion
└── 19-emerging-techniques/     # MoE, model merging, long context
```

---

## 📋 Skill Structure Template

Use [SKILL_TEMPLATE.md](docs/SKILL_TEMPLATE.md) as a starting point. Each skill should contain:

```
skill-name/
├── SKILL.md                    # Quick reference (50-150 lines)
│   ├── Metadata (name, description, version)
│   ├── When to use this skill
│   ├── Quick start examples
│   ├── Common patterns
│   └── Links to references
│
├── references/                 # Deep documentation (300KB+)
│   ├── README.md              # From GitHub/official docs
│   ├── api.md                 # API reference
│   ├── tutorials.md           # Step-by-step guides
│   ├── issues.md              # Real GitHub issues (if applicable)
│   ├── releases.md            # Version history (if applicable)
│   └── file_structure.md      # Codebase navigation (if applicable)
│
├── scripts/                    # Helper scripts (optional)
└── assets/                     # Templates & examples (optional)
```

---

## 🔍 Quality Standards

### Code Examples

All code examples MUST have language detection:

✅ **Good**:
````markdown
```python
from transformers import AutoModel
model = AutoModel.from_pretrained("gpt2")
```
````

❌ **Bad**:
````markdown
```
from transformers import AutoModel
model = AutoModel.from_pretrained("gpt2")
```
````

### Documentation Size

- **Minimum**: 100KB total in references/
- **Target**: 300KB+ total
- **Gold Standard**: 500KB+ with issues, releases, examples

### Real-World Content

Prefer skills with:
- ✅ Real GitHub issues and solutions
- ✅ Release notes and breaking changes
- ✅ Community discussions
- ✅ Performance benchmarks
- ✅ Troubleshooting guides

### Links and Citations

Always include:
- ✅ Official documentation link
- ✅ GitHub repository link
- ✅ License information
- ✅ Version/release information

---

## 🧪 Testing

Before submitting, verify:

```bash
# 1. SKILL.md is well-formatted
cat your-skill/SKILL.md

# 2. All reference files exist
ls -R your-skill/references/

# 3. Documentation size is adequate (300KB+ target)
du -sh your-skill/references/

# 4. Code blocks have language tags
grep -A 1 '```' your-skill/SKILL.md | head -20

# 5. No broken links (manual check)
# Open SKILL.md and verify all [links](urls) work

# 6. Marketplace entry added and valid
python3 -c "import json; json.load(open('.claude-plugin/marketplace.json'))"
```

---

## 🎓 Examples of High-Quality Skills

**Gold Standard** (emulate this):
1. **06-post-training/grpo-rl-training/** (569 lines) ⭐⭐⭐⭐⭐
   - Complete implementation workflow
   - 10+ code examples with explanations
   - Troubleshooting guide
   - Common pitfalls and solutions
   - Performance tips
   - **This is the quality bar**

**Good Examples**:
2. **03-fine-tuning/axolotl/** (151 lines)
   - Real configuration examples
   - When to use guidance
   - Comprehensive but could add more workflows

3. **08-distributed-training/deepspeed/** (132 lines)
   - ZeRO optimization patterns
   - Configuration examples
   - Good foundation, needs more troubleshooting

---

## 🚫 What NOT to Contribute

- ❌ Proprietary/closed-source tools
- ❌ Deprecated libraries (unless historically important)
- ❌ Duplicate skills (check existing skills first)
- ❌ Incomplete skills (<50 lines SKILL.md, <100KB refs)
- ❌ Skills without code examples

---

## 🎖️ Recognition

All contributors will be:
- ✅ Listed in [CONTRIBUTORS.md](CONTRIBUTORS.md)
- ✅ Mentioned in release notes
- ✅ Featured on project homepage (when launched)
- ✅ Attributed in SKILL.md metadata

**Top contributors** (5+ skills) receive special recognition and maintainer status.

---

## 📞 Getting Help

- **Issues**: [GitHub Issues](https://github.com/YOUR_USERNAME/claude-ai-research-skills/issues)
- **Discussions**: [GitHub Discussions](https://github.com/YOUR_USERNAME/claude-ai-research-skills/discussions)
- **Questions**: Open a discussion with "Question:" prefix

---

## 📅 Review Process

1. **Automated Checks** (when implemented):
   - File structure validation
   - Code block language detection
   - Documentation size check
   - Marketplace.json validation

2. **Manual Review** (by maintainers):
   - Content quality and accuracy
   - Code example validity
   - Proper categorization
   - License compliance

3. **Feedback Loop**:
   - Reviews within 48-72 hours
   - Constructive feedback provided
   - Iterate until approved

4. **Merge**:
   - Merged to main branch
   - Added to release notes
   - Contributor recognized

---

## 🙏 Thank You!

Your contributions help the entire AI research community. Every skill added makes Claude Code more powerful for researchers, engineers, and students worldwide.

**Let's build something amazing together!** 🚀
