# 代理技能 | Agent Skills

> 代理技能是扩展Claude功能的模块化能力。每个技能打包指令、元数据和可选资源（脚本、模板），Claude会在相关时自动使用它们。

> Agent Skills are modular capabilities that extend Claude's functionality. Each Skill packages instructions, metadata, and optional resources (scripts, templates) that Claude uses automatically when relevant.

## 为什么使用技能 | Why use Skills

技能是可在文件系统中复用的资源，为Claude提供领域专业知识：工作流、上下文和最佳实践，将通用代理转变为专家。不同于提示（针对一次性任务的会话级指令），技能按需加载，消除了在多个对话中重复提供相同指导的需要。

Skills are reusable, filesystem-based resources that provide Claude with domain-specific expertise: workflows, context, and best practices that transform general-purpose agents into specialists. Unlike prompts (conversation-level instructions for one-off tasks), Skills load on-demand and eliminate the need to repeatedly provide the same guidance across multiple conversations.

**关键优势**：

* **专业化Claude**：为领域特定任务定制能力
* **减少重复**：创建一次，自动使用
* **组合能力**：组合技能构建复杂工作流

**Key benefits**:

* **Specialize Claude**: Tailor capabilities for domain-specific tasks
* **Reduce repetition**: Create once, use automatically
* **Compose capabilities**: Combine Skills to build complex workflows

<Note>
  For a deep dive into the architecture and real-world applications of Agent Skills, read our engineering blog: [Equipping agents for the real world with Agent Skills](https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills).
</Note>

## 使用技能 | Using Skills

Anthropic为常见的文档任务（PowerPoint、Excel、Word、PDF）提供预构建代理技能，您也可以创建自己的自定义技能。两者的工作方式相同。Claude会在与您的请求相关时自动使用它们。

Anthropic provides pre-built Agent Skills for common document tasks (PowerPoint, Excel, Word, PDF), and you can create your own custom Skills. Both work the same way. Claude automatically uses them when relevant to your request.

**预构建代理技能**可供claude.ai上的所有用户和Claude API使用。请参阅下面的[可用技能](#available-skills)部分获取完整列表。

**Pre-built Agent Skills** are available to all users on claude.ai and via the Claude API. See the [Available Skills](#available-skills) section below for the complete list.

**自定义技能**让您打包领域专业知识和组织知识。它们在Claude的所有产品中都可用：在Claude Code中创建，通过API上传，或在claude.ai设置中添加。

**Custom Skills** let you package domain expertise and organizational knowledge. They're available across Claude's products: create them in Claude Code, upload them via the API, or add them in claude.ai settings.

<Note>
  **Get started:**

  * For pre-built Agent Skills: See the [quickstart tutorial](/en/docs/agents-and-tools/agent-skills/quickstart) to start using PowerPoint, Excel, Word, and PDF skills in the API
  * For custom Skills: See the [Agent Skills Cookbook](https://github.com/anthropics/claude-cookbooks/tree/main/skills) to learn how to create your own Skills
</Note>

## 技能如何工作 | How Skills work

技能利用Claude的虚拟机环境提供仅靠提示无法实现的能力。Claude在具有文件系统访问权限的虚拟机中运行，允许技能作为包含指令、可执行代码和参考材料的目录存在，就像您为新团队成员创建的入职指南一样组织。

Skills leverage Claude's VM environment to provide capabilities beyond what's possible with prompts alone. Claude operates in a virtual machine with filesystem access, allowing Skills to exist as directories containing instructions, executable code, and reference materials, organized like an onboarding guide you'd create for a new team member.

这种基于文件系统的架构实现了**渐进式披露**：Claude按需分阶段加载信息，而不是预先消耗上下文。

This filesystem-based architecture enables **progressive disclosure**: Claude loads information in stages as needed, rather than consuming context upfront.

### 三种技能内容类型，三个加载级别 | Three types of Skill content, three levels of loading

技能可以包含三种类型的内容，每种在不同时间加载：

Skills can contain three types of content, each loaded at different times:

### 级别1：元数据（始终加载）| Level 1: Metadata (always loaded)

**内容类型：指令**。技能的YAML frontmatter提供发现信息：

**Content type: Instructions**. The Skill's YAML frontmatter provides discovery information:

```yaml  theme={null}
---
name: pdf-processing
description: Extract text and tables from PDF files, fill forms, merge documents. Use when working with PDF files or when the user mentions PDFs, forms, or document extraction.
---
```

Claude loads this metadata at startup and includes it in the system prompt. This lightweight approach means you can install many Skills without context penalty; Claude only knows each Skill exists and when to use it.

### Level 2: Instructions (loaded when triggered)

**内容类型：指令**。SKILL.md的主体包含程序性知识：工作流、最佳实践和指导：

**Content type: Instructions**. The main body of SKILL.md contains procedural knowledge: workflows, best practices, and guidance:

当您请求的内容与技能的描述匹配时，Claude通过bash从文件系统读取SKILL.md。只有到那时，此内容才会进入上下文窗口。

When you request something that matches a Skill's description, Claude reads SKILL.md from the filesystem via bash. Only then does this content enter the context window.

### Level 3: Resources and code (loaded as needed)

**内容类型：指令、代码和资源**。技能可以打包额外材料：

**Content types: Instructions, code, and resources**. Skills can bundle additional materials:

```
pdf-skill/
├── SKILL.md (main instructions)
├── FORMS.md (form-filling guide)
├── REFERENCE.md (detailed API reference)
└── scripts/
    └── fill_form.py (utility script)
```

**Instructions**: 其他markdown文件（FORMS.md, REFERENCE.md），包含专业指导和工作流

**Code**: 可执行脚本（fill_form.py, validate.py），Claude通过bash运行；脚本提供确定性操作，不消耗上下文

**Resources**: 参考材料，如数据库模式、API文档、模板或示例

Claude仅在引用时访问这些文件。文件系统模型意味着每种内容类型有不同的优势：指令用于灵活指导，代码用于可靠性，资源用于事实查找。

**Instructions**: Additional markdown files (FORMS.md, REFERENCE.md) containing specialized guidance and workflows

**Code**: Executable scripts (fill_form.py, validate.py) that Claude runs via bash; scripts provide deterministic operations without consuming context

**Resources**: Reference materials like database schemas, API documentation, templates, or examples

Claude accesses these files only when referenced. The filesystem model means each content type has different strengths: instructions for flexible guidance, code for reliability, resources for factual lookup.

| 级别 | 加载时间 | Token消耗 | 内容 |
| ------------------------- | ----------------------- | ---------------------- | --------------------------------------------------------------------- |
| **级别1：元数据** | 始终（启动时） | 每个技能约100 tokens | YAML frontmatter中的`name`和`description` |
| **级别2：指令** | 技能触发时 | 5k tokens以下 | 包含指令和指导的SKILL.md正文 |
| **级别3+：资源** | 按需 | 实际上无限 | 通过bash执行的捆绑文件，不将内容加载到上下文 |

Progressive disclosure ensures only relevant content occupies the context window at any given time.

| Level                     | When Loaded             | Token Cost             | Content                                                               |
| ------------------------- | ----------------------- | ---------------------- | --------------------------------------------------------------------- |
| **Level 1: Metadata**     | Always (at startup)     | ~100 tokens per Skill | `name` and `description` from YAML frontmatter                        |
| **Level 2: Instructions** | When Skill is triggered | Under 5k tokens        | SKILL.md body with instructions and guidance                          |
| **Level 3+: Resources**   | As needed               | Effectively unlimited  | Bundled files executed via bash without loading contents into context |

渐进式披露确保只有相关内容在任何给定时间占据上下文窗口。

Progressive disclosure ensures only relevant content occupies the context window at any given time.

### 技能架构 | The Skills architecture

技能在代码执行环境中运行，Claude可以访问文件系统，执行bash命令和执行代码。可以这样理解：技能作为目录存在于虚拟机中，Claude使用与您导航计算机文件相同的bash命令与它们交互。

Skills run in a code execution environment where Claude has filesystem access, bash commands, and code execution capabilities. Think of it like this: Skills exist as directories on a virtual machine, and Claude interacts with them using the same bash commands you'd use to navigate files on your computer.

**Claude如何访问技能内容：**

当技能被触发时，Claude使用bash从文件系统读取SKILL.md，将其指令带入上下文窗口。如果这些指令引用其他文件（如FORMS.md或数据库模式），Claude也会使用额外的bash命令读取这些文件。当指令提到可执行脚本时，Claude通过bash运行它们，只接收输出（脚本代码本身从不进入上下文）。

When a Skill is triggered, Claude uses bash to read SKILL.md from the filesystem, bringing its instructions into the context window. If those instructions reference other files (like FORMS.md or a database schema), Claude reads those files too using additional bash commands. When instructions mention executable scripts, Claude runs them via bash and receives only the output (the script code itself never enters context).

**此架构实现的功能：**

**按需文件访问**：Claude只读取每个特定任务所需的文件。一个技能可以包含数十个参考文件，但如果您的任务只需要销售模式，Claude只加载那一个文件。其余保留在文件系统中，消耗零token。

**高效脚本执行**：当Claude运行`validate_form.py`时，脚本代码永远不会加载到上下文窗口中。只有脚本的输出（如「验证通过」或特定错误消息）消耗token。这使得脚本比让Claude即时生成等效代码更高效。

**捆绑内容实际上无限制**：因为文件在被访问之前不消耗上下文，技能可以包含全面的API文档、大型数据集、广泛的示例或您需要的任何参考材料。对于未使用的捆绑内容没有上下文惩罚。

This filesystem-based model is what makes progressive disclosure work. Claude navigates your Skill like you'd reference specific sections of an onboarding guide, accessing exactly what each task requires.

**What this architecture enables:**

**On-demand file access**: Claude reads only the files needed for each specific task. A Skill can include dozens of reference files, but if your task only needs the sales schema, Claude loads just that one file. The rest remain on the filesystem consuming zero tokens.

**Efficient script execution**: When Claude runs `validate_form.py`, the script's code never loads into the context window. Only the script's output (like "Validation passed" or specific error messages) consumes tokens. This makes scripts far more efficient than having Claude generate equivalent code on the fly.

**No practical limit on bundled content**: Because files don't consume context until accessed, Skills can include comprehensive API documentation, large datasets, extensive examples, or any reference materials you need. There's no context penalty for bundled content that isn't used.

这种基于文件系统的模型是渐进式披露工作的原因。Claude像您参考入职指南的特定部分一样导航您的技能，访问每个任务所需的内容。

This filesystem-based model is what makes progressive disclosure work. Claude navigates your Skill like you'd reference specific sections of an onboarding guide, accessing exactly what each task requires.

### Example: Loading a PDF processing skill

Here's how Claude loads and uses a PDF processing skill:

1. **Startup**: System prompt includes: `PDF Processing - Extract text and tables from PDF files, fill forms, merge documents`
2. **User request**: "Extract the text from this PDF and summarize it"
3. **Claude invokes**: `bash: read pdf-skill/SKILL.md` → Instructions loaded into context
4. **Claude determines**: Form filling is not needed, so FORMS.md is not read
5. **Claude executes**: Uses instructions from SKILL.md to complete the task

<img src="https://mintcdn.com/anthropic-claude-docs/4Bny2bjzuGBK7o00/images/agent-skills-context-window.png?fit=max&auto=format&n=4Bny2bjzuGBK7o00&q=85&s=0127e014bfc3dd3c86567aad8609111b" alt="Skills loading into context window - showing the progressive loading of skill metadata and content" data-og-width="2048" width="2048" data-og-height="1154" height="1154" data-path="images/agent-skills-context-window.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/anthropic-claude-docs/4Bny2bjzuGBK7o00/images/agent-skills-context-window.png?w=280&fit=max&auto=format&n=4Bny2bjzuGBK7o00&q=85&s=a17315d47b7c5a85b389026b70676e98 280w, https://mintcdn.com/anthropic-claude-docs/4Bny2bjzuGBK7o00/images/agent-skills-context-window.png?w=560&fit=max&auto=format&n=4Bny2bjzuGBK7o00&q=85&s=267349b063954588d4fae2650cb90cd8 560w, https://mintcdn.com/anthropic-claude-docs/4Bny2bjzuGBK7o00/images/agent-skills-context-window.png?w=840&fit=max&auto=format&n=4Bny2bjzuGBK7o00&q=85&s=0864972aba7bcb10bad86caf82cb415f 840w, https://mintcdn.com/anthropic-claude-docs/4Bny2bjzuGBK7o00/images/agent-skills-context-window.png?w=1100&fit=max&auto=format&n=4Bny2bjzuGBK7o00&q=85&s=631d661cbadcbdb62fd0935b91bd09f8 1100w, https://mintcdn.com/anthropic-claude-docs/4Bny2bjzuGBK7o00/images/agent-skills-context-window.png?w=1650&fit=max&auto=format&n=4Bny2bjzuGBK7o00&q=85&s=c1f80d0e37c517eb335db83615483ae0 1650w, https://mintcdn.com/anthropic-claude-docs/4Bny2bjzuGBK7o00/images/agent-skills-context-window.png?w=2500&fit=max&auto=format&n=4Bny2bjzuGBK7o00&q=85&s=4b6d0f1baf011ff9b49de501d8d83cc7 2500w" />

The diagram shows:

1. Default state with system prompt and skill metadata pre-loaded
2. Claude triggers the skill by reading SKILL.md via bash
3. Claude optionally reads additional bundled files like FORMS.md as needed
4. Claude proceeds with the task

This dynamic loading ensures only relevant skill content occupies the context window.

## 技能在哪里工作 | Where Skills work

技能在Claude的代理产品中均可用：

Skills are available across Claude's agent products:

### Claude API

Claude API同时支持预构建代理技能和自定义技能。两者工作方式相同：在`container`参数中指定相关的`skill_id`，以及代码执行工具。

The Claude API supports both pre-built Agent Skills and custom Skills. Both work identically: specify the relevant `skill_id` in the `container` parameter along with the code execution tool.

**先决条件**：通过API使用技能需要三个beta头：

* `code-execution-2025-08-25` - 技能在代码执行容器中运行
* `skills-2025-10-02` - 启用技能功能
* `files-api-2025-04-14` - 需要用于向容器上传/下载文件

通过引用其`skill_id`（如`pptx`、`xlsx`）使用预构建代理技能，或通过技能API（`/v1/skills`端点）创建和上传您自己的。自定义技能在工作空间范围内共享。

To learn more, see [Use Skills with the Claude API](/en/api/skills-guide).

### Claude Code

Claude Code仅支持自定义技能。

**自定义技能**：创建带有SKILL.md文件的目录作为技能。Claude自动发现并使用它们。

Claude Code中的自定义技能是基于文件系统的，不需要API上传。

To learn more, see [Use Skills in Claude Code](https://code.claude.com/docs/skills).

### Claude Agent SDK

Claude Agent SDK通过基于文件系统的配置支持自定义技能。

**自定义技能**：在`.claude/skills/`中创建带有SKILL.md文件的目录作为技能。在`allowed_tools`配置中包含`"Skill"`以启用技能。

然后，当SDK运行时，技能会自动被发现。

To learn more, see [Agent Skills in the SDK](/en/api/agent-sdk/skills).

### Claude.ai

Claude.ai同时支持预构建代理技能和自定义技能。

**预构建代理技能**：当您创建文档时，这些技能已在后台工作。Claude使用它们不需要任何设置。

**自定义技能**：通过设置>功能上传您自己的技能为zip文件。在Pro、Max、Team和Enterprise计划中可用，并启用代码执行。自定义技能对每个用户个人；它们不在工作空间范围内共享，不能由管理员集中管理。

To learn more about using Skills in Claude.ai, see the following resources in the Claude Help Center:

* [什么是技能？](https://support.claude.com/en/articles/12512176-what-are-skills)
* [在Claude中使用技能](https://support.claude.com/en/articles/12512180-using-skills-in-claude)
* [如何创建自定义技能](https://support.claude.com/en/articles/12512198-creating-custom-skills)
* [使用技能教Claude您的工作方式](https://support.claude.com/en/articles/12580051-teach-claude-your-way-of-working-using-skills)

## 技能结构 | Skill structure

每个技能都需要一个带有YAML frontmatter的`SKILL.md`文件：

Every Skill requires a `SKILL.md` file with YAML frontmatter:

```yaml  theme={null}
---
name: your-skill-name
description: Brief description of what this Skill does and when to use it
---

# Your Skill Name

## Instructions
[Clear, step-by-step guidance for Claude to follow]

## Examples
[Concrete examples of using this Skill]
```

**Required fields**: `name` and `description`

**Field requirements**:

`name`:

* Maximum 64 characters
* Must contain only lowercase letters, numbers, and hyphens
* Cannot contain XML tags
* Cannot contain reserved words: "anthropic", "claude"

`description`:

* Must be non-empty
* Maximum 1024 characters
* Cannot contain XML tags

The `description` should include both what the Skill does and when Claude should use it. For complete authoring guidance, see the [best practices guide](/en/docs/agents-and-tools/agent-skills/best-practices).

## 安全考虑 | Security considerations

我们强烈建议仅使用来自可信来源的技能：您自己创建的或从Anthropic获得的。技能通过指令和代码为Claude提供新能力，虽然这使它们强大，但也意味着恶意技能可以指示Claude以不符合技能声明目的的方式调用工具或执行代码。

We strongly recommend using Skills only from trusted sources: those you created yourself or obtained from Anthropic. Skills provide Claude with new capabilities through instructions and code, and while this makes them powerful, it also means a malicious Skill can direct Claude to invoke tools or execute code in ways that don't match the Skill's stated purpose.

**关键安全考虑**：

* **彻底审计**：审查技能中打包的所有文件：SKILL.md、脚本、图像和其他资源。寻找异常模式，如意外的网络调用、文件访问模式或与技能声明目的不匹配的操作
* **外部来源有风险**：从外部URL获取数据的技能尤其有风险，因为获取的内容可能包含恶意指令。即使可信的技能，如果其外部依赖随时间变化，也可能被篡改
* **工具滥用**：恶意技能可以以有害方式调用工具（文件操作、bash命令、代码执行）
* **数据暴露**：可以访问敏感数据的技能可能被设计为将信息泄露到外部系统
* **像安装软件一样对待**：仅使用来自可信来源的技能。在将技能集成到可访问敏感数据或关键操作的生产系统中时要特别小心

**Key security considerations**:

* **Audit thoroughly**: Review all files bundled in the Skill: SKILL.md, scripts, images, and other resources. Look for unusual patterns like unexpected network calls, file access patterns, or operations that don't match the Skill's stated purpose
* **External sources are risky**: Skills that fetch data from external URLs pose particular risk, as fetched content may contain malicious instructions. Even trustworthy Skills can be compromised if their external dependencies change over time
* **Tool misuse**: Malicious Skills can invoke tools (file operations, bash commands, code execution) in harmful ways
* **Data exposure**: Skills with access to sensitive data could be designed to leak information to external systems
* **Treat like installing software**: Only use Skills from trusted sources. Be especially careful when integrating Skills into production systems with access to sensitive data or critical operations

## 可用技能 | Available Skills

### 预构建代理技能

以下预构建代理技能可供立即使用：

* **PowerPoint (pptx)**：创建演示文稿，编辑幻灯片，分析演示内容
* **Excel (xlsx)**：创建电子表格，分析数据，生成带图表的报告
* **Word (docx)**：创建文档，编辑内容，格式化文本
* **PDF (pdf)**：生成格式化的PDF文档和报告

这些技能在Claude API和claude.ai上都可用。请参阅[快速入门教程](/en/docs/agents-and-tools/agent-skills/quickstart)开始在API中使用它们。

### 自定义技能示例

有关自定义技能的完整示例，请参阅[技能食谱](https://github.com/anthropics/claude-cookbooks/tree/main/skills)。

## 限制和约束 | Limitations and constraints

了解这些限制有助于您有效地规划技能部署。

### 跨表面可用性

**自定义技能不会跨表面同步**。上传到一个表面的技能不会自动在其他表面可用：

* 上传到Claude.ai的技能必须单独上传到API
* 通过API上传的技能在Claude.ai上不可用
* Claude Code技能是基于文件系统的，与Claude.ai和API分开

您需要为您想使用技能的每个表面单独管理和上传技能。

### 共享范围

技能根据使用位置有不同的共享模式：

* **Claude.ai**：仅限个人用户；每个团队成员必须单独上传
* **Claude API**：工作空间范围；所有工作空间成员都可以访问上传的技能
* **Claude Code**：个人（`~/.claude/skills/`）或项目级别（`.claude/skills/`）；也可以通过Claude Code插件共享

Claude.ai目前不支持自定义技能的集中管理员管理或组织范围分发。

### 运行时环境约束

技能可用的确切运行时环境取决于您使用它的产品表面。

* **Claude.ai**：
  * **网络访问可变**：根据用户/管理员设置，技能可能具有完全、部分或无网络访问权限
* **Claude API**：
  * **无网络访问**：技能无法进行外部API调用或访问互联网
  * **无运行时包安装**：仅预安装的包可用。您不能在执行期间安装新包
  * **仅预配置依赖**：请参阅[代码执行工具文档](/en/docs/agents-and-tools/tool-use/code-execution-tool)获取可用包列表
* **Claude Code**：
  * **完全网络访问**：技能具有与用户计算机上任何其他程序相同的网络访问
  * **不鼓励全局包安装**：技能应仅在本地安装包，以免干扰用户的计算机

请在这些约束范围内规划您的技能。

## 下一步 | Next steps

请参阅技能文档获取更多信息。

Pre-built Agent Skills

The following pre-built Agent Skills are available for immediate use:

* **PowerPoint (pptx)**: Create presentations, edit slides, analyze presentation content
* **Excel (xlsx)**: Create spreadsheets, analyze data, generate reports with charts
* **Word (docx)**: Create documents, edit content, format text
* **PDF (pdf)**: Generate formatted PDF documents and reports

These Skills are available on the Claude API and claude.ai. See the [quickstart tutorial](/en/docs/agents-and-tools/agent-skills/quickstart) to start using them in the API.

### Custom Skills examples

For complete examples of custom Skills, see the [Skills cookbook](https://github.com/anthropics/claude-cookbooks/tree/main/skills).

## Limitations and constraints

Understanding these limitations helps you plan your Skills deployment effectively.

### Cross-surface availability

**Custom Skills do not sync across surfaces**. Skills uploaded to one surface are not automatically available on others:

* Skills uploaded to Claude.ai must be separately uploaded to the API
* Skills uploaded via the API are not available on Claude.ai
* Claude Code Skills are filesystem-based and separate from both Claude.ai and API

You'll need to manage and upload Skills separately for each surface where you want to use them.

### Sharing scope

Skills have different sharing models depending on where you use them:

* **Claude.ai**: Individual user only; each team member must upload separately
* **Claude API**: Workspace-wide; all workspace members can access uploaded Skills
* **Claude Code**: Personal (`~/.claude/skills/`) or project-based (`.claude/skills/`); can also be shared via Claude Code Plugins

Claude.ai does not currently support centralized admin management or org-wide distribution of custom Skills.

### Runtime environment constraints

The exact runtime environment available to your skill depends on the product surface where you use it.

* **Claude.ai**:
  * **Varying network access**: Depending on user/admin settings, Skills may have full, partial, or no network access
* **Claude API**:
  * **No network access**: Skills cannot make external API calls or access the internet
  * **No runtime package installation**: Only pre-installed packages are available
  * **Pre-configured dependencies only**: Check the [code execution tool documentation](/en/docs/agents-and-tools/tool-use/code-execution-tool) for the list of available packages
* **Claude Code**:
  * **Full network access**: Skills have the same network access as any other program on the user's computer
  * **Global package installation discouraged**: Skills should only install packages locally in order to avoid interfering with the user's computer

Plan your Skills to work within these constraints.

## Next steps

Refer to the Skills documentation for more information.