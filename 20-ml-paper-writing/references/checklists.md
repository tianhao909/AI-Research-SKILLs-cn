# 会议论文检查清单 | Conference Paper Checklists

本文档记录了主要ML/AI会议的强制检查清单要求。所有主要场所现在都要求论文检查清单——缺少检查清单将导致直接拒稿。

---

## 目录 | Contents

- [NeurIPS论文检查清单](#neurips论文检查清单)
- [ICML论文检查清单](#icml论文检查清单)
- [ICLR要求](#iclr要求)
- [ACL要求](#acl要求)
- [通用提交前检查清单](#通用提交前检查清单)

---

## NeurIPS论文检查清单 | NeurIPS Paper Checklist

### 强制组件

所有NeurIPS投稿必须包含完整的论文检查清单。缺少此元素的论文将面临**自动直接拒稿**。检查清单出现在参考文献之后和补充材料之前，不计入页数限制。

### 16项必需检查清单项目 | 16 Required Checklist Items

#### 1. 声明一致性 | Claims Alignment

作者必须验证摘要和引言中的声明与理论和实验结果相匹配，声明、假设和局限性必须清晰陈述。

**检查项 | What to check:**
- [ ] 摘要声明与实际结果一致
- [ ] 引言没有过度声明
- [ ] 贡献具体且可证伪

#### 2. 局限性讨论 | Limitations Discussion

论文应包含专门的"局限性"部分，讨论强假设、对违反的鲁棒性、范围约束和影响性能的因素。

**应包含内容 | What to include:**
- [ ] 专门的局限性部分
- [ ] 对范围的诚实评估
- [ ] 方法可能失败的条件

#### 3. 理论证明 | Theory & Proofs

理论贡献需要完整的假设陈述和完整证明（主论文或带证明概要的附录以提供直觉）。

**检查项 | What to check:**
- [ ] 所有假设正式陈述
- [ ] 完整证明已提供（正文或附录）
- [ ] 正文中有直觉证明概要

#### 4. 可复现性 | Reproducibility

作者必须描述确保结果可验证的步骤：通过代码发布、详细说明、模型访问或与其贡献类型适当的检查点。

**需提供内容 | What to provide:**
- [ ] 清晰的可复现性声明
- [ ] 代码可用性信息
- [ ] 模型检查点（如适用）

#### 5. 数据与代码访问 | Data & Code Access

应提供复现主要实验结果的说明（补充材料或URL），包括精确命令和环境规格。

**应包含内容 | What to include:**
- [ ] 运行实验的确切命令
- [ ] 环境规格（requirements.txt、conda环境）
- [ ] 数据访问说明

#### 6. 实验细节 | Experimental Details

论文必须指定训练细节：数据分割、超参数和选择方法（在主论文或补充材料中）。

**需记录内容 | What to document:**
- [ ] 训练/验证/测试分割详情
- [ ] 使用的所有超参数
- [ ] 超参数选择方法

#### 7. 统计显著性 | Statistical Significance

结果需要误差棒、置信区间或统计测试，并清晰说明计算方法和底层假设。

**应包含内容 | What to include:**
- [ ] 误差棒或置信区间
- [ ] 运行次数/种子数
- [ ] 计算方法（标准差vs标准误）

#### 8. 计算资源 | Compute Resources

需要规格：计算 worker 类型（CPU/GPU）、内存、存储、每次运行执行时间，以及项目总计算需求。

**需记录内容 | What to document:**
- [ ] GPU类型和数量
- [ ] 每次运行训练时间
- [ ] 使用的总计算量

#### 9. 伦理准则合规 | Ethics Code Compliance

作者确认遵守NeurIPS伦理准则，注明任何必要的偏差。

**验证项 | What to verify:**
- [ ] 阅读NeurIPS伦理准则
- [ ] 确认合规
- [ ] 注明任何偏差及理由

#### 10. 更广泛影响 | Broader Impacts

讨论潜在负面社会应用、公平性问题、隐私风险和可能的缓解策略（如适用）。

**需处理内容 | What to address:**
- [ ] 潜在负面应用
- [ ] 公平性考虑
- [ ] 隐私影响
- [ ] 缓解策略

#### 11. 保障措施 | Safeguards

高风险模型（语言模型、网络抓取的数据集）需要受控的发布机制和使用指南。

**需考虑内容 | What to consider:**
- [ ] 敏感模型的发布策略
- [ ] 如需要，提供使用指南
- [ ] 如适当，实施访问控制

#### 12. 许可证尊重 | License Respect

所有现有资产需要创作者引用、许可证名称、URL、版本号和服务条款确认。

**需记录内容 | What to document:**
- [ ] 数据集许可证已引用
- [ ] 代码许可证已遵守
- [ ] 版本号已包含

#### 13. 资产文档 | Asset Documentation

新发布需要结构化模板，记录训练细节、局限性、同意程序和许可信息。

**对于新数据集/模型 | For new datasets/models:**
- [ ] 数据表或模型卡
- [ ] 训练数据文档
- [ ] 已知局限性

#### 14. 人类受试者 | Human Subjects

众包研究必须包含参与者说明、截图、补偿详情，并符合最低工资要求。

**应包含内容 | What to include:**
- [ ] 任务说明
- [ ] 补偿详情
- [ ] 时间估计

#### 15. IRB批准 | IRB Approvals

人类受试者研究需要记录机构审查委员会批准或同等批准，并披露风险描述（在提交时保持匿名）。

**验证项 | What to verify:**
- [ ] 已获得IRB批准
- [ ] 已完成风险评估
- [ ] 提交时已匿名化

#### 16. LLM声明 | LLM Declaration

将大语言模型作为核心方法论组件使用需要披露；写作/编辑使用不需要声明。

**需披露内容 | What to disclose:**
- [ ] LLM作为核心方法论组件使用
- [ ] LLM如何使用
- [ ]（写作帮助不需要披露）

### 响应格式 | Response Format

作者对每个问题选择"是"、"否"或"不适用"，并可选择提供1-2句话的理由说明。

**重要 | Important:** 审稿人明确指示不要因为诚实地承认局限性而惩罚作者。

---

## ICML论文检查清单 | ICML Paper Checklist

### 更广泛影响声明 | Broader Impact Statement

ICML要求在论文末尾、参考文献之前放置更广泛影响声明。这**不计入**页数限制。

**必需元素 | Required elements:**
- 潜在正面影响
- 潜在负面影响
- 缓解策略
- 可能受影响的人

### ICML具体要求 | ICML Specific Requirements

#### 可复现性检查清单 | Reproducibility Checklist

- [ ] 数据分割清晰指定
- [ ] 超参数已列出
- [ ] 搜索范围已记录
- [ ] 选择方法已解释
- [ ] 计算资源已指定
- [ ] 代码可用性已声明

#### 统计报告 | Statistical Reporting

- [ ] 所有图表上有误差棒
- [ ] 指定标准差vs标准误
- [ ] 声明运行次数
- [ ] 比较方法时进行显著性测试

#### 匿名化 | Anonymization

- [ ] 论文中没有作者姓名
- [ ] 没有致谢
- [ ] 没有资助编号
- [ ] 以第三人称引用先前工作
- [ ] 没有可识别的仓库URL

---

## ICLR要求 | ICLR Requirements

### LLM披露政策（2026年新增）| LLM Disclosure Policy (New for 2026)

ICLR有特定的LLM披露要求：

> "如果LLM在研究构思和/或写作中发挥了重要作用，以至于可以被视为贡献者，作者必须在单独的附录部分描述其具体角色。"

**需要披露的情况 | When disclosure is required:**
- LLM用于重要的研究构思
- LLM用于大量写作
- LLM可被视为贡献者

**不需要披露的情况 | When disclosure is NOT required:**
- 语法检查
- 轻微编辑帮助
- 代码补全工具

**不披露的后果 | Consequences of non-disclosure:**
- 直接拒稿
- 潜在的发表后问题

### ICLR具体要求 | ICLR Specific Requirements

#### 可复现性声明（可选但推荐）| Reproducibility Statement (Optional but Recommended)

添加引用以下内容的声明：
- 支持材料
- 代码可用性
- 数据可用性
- 模型检查点

#### 伦理声明（可选）| Ethics Statement (Optional)

在≤1页内解决潜在问题。不计入页数限制。

#### 互惠审稿 | Reciprocal Reviewing

- 3篇以上论文的作者必须担任≥6篇论文的审稿人
- 每篇投稿需要≥1名作者注册审阅≥3篇论文

---

## ACL要求 | ACL Requirements

### 局限性部分（强制）| Limitations Section (Mandatory)

ACL明确要求局限性部分：

**应包含内容 | What to include:**
- 做出的强假设
- 范围局限性
- 方法可能失败的情况
- 泛化担忧

**重要 | Important:** 局限性部分**不计入**页数限制。

### ACL具体检查清单 | ACL Specific Checklist

#### 负责任的NLP | Responsible NLP

- [ ] 已处理偏见考虑
- [ ] 如适用已评估公平性
- [ ] 已讨论双重使用担忧

#### 多语言考虑 | Multilingual Considerations

如适用：
- [ ] 已处理语言多样性
- [ ] 包含非英语语言
- [ ] 已验证翻译质量

#### 人类评估 | Human Evaluation

如适用：
- [ ] 提供了标注员详情
- [ ] 报告了协议指标
- [ ] 已记录补偿

---

## 通用提交前检查清单 | Universal Pre-Submission Checklist

### 每次提交前 | Before Every Submission

#### 论文内容 | Paper Content

- [ ] 摘要 ≤ 字数限制（通常250-300词）
- [ ] 主内容在页数限制内
- [ ] 参考文献完整且已验证
- [ ] 包含局限性部分
- [ ] 所有图表/表格有标题
- [ ] 标题独立完整

#### 格式 | Formatting

- [ ] 使用正确的模板（场所+年份特定）
- [ ] 未修改边距
- [ ] 未修改字体大小
- [ ] 满足双盲要求
- [ ] 有页码（审稿用）或无页码（camera-ready）

#### 技术 | Technical
- [ ] 所有声明有证据支持
- [ ] 包含误差棒
- [ ] 基线适当
- [ ] 记录超参数
- [ ] 声明计算资源

#### 可复现性 | Reproducibility

- [ ] 代码将可用（或有正当理由）
- [ ] 数据将可用（或有正当理由）
- [ ] 环境已记录
- [ ] 提供复现命令

#### 伦理 | Ethics

- [ ] 已考虑更广泛影响
- [ ] 诚实陈述局限性
- [ ] 尊重许可证
- [ ] 如需要已获得IRB批准

#### 最终检查 | Final Checks

- [ ] PDF编译无错误
- [ ] 所有图表正确渲染
- [ ] 所有引用正确解析
- [ ] 补充材料已整理
- [ ] 会议检查清单已完成

---

## 快速参考：页数限制 | Quick Reference: Page Limits

| 会议 | 主内容 | 参考文献 | 附录 |
|------------|-------------|------------|----------|
| NeurIPS 2025 | 9页 | 无限 | 无限（检查清单单独）|
| ICML 2026 | 8页（+1 camera） | 无限 | 无限 |
| ICLR 2026 | 9页（+1 camera） | 无限 | 无限 |
| ACL 2025 | 8页（长论文） | 无限 | 无限 |
| AAAI 2026 | 7页（+1 camera） | 无限 | 无限 |
| COLM 2025 | 9页（+1 camera） | 无限 | 无限 |

---

## 模板位置 | Template Locations

所有会议模板在 `templates/` 目录中：

```
templates/
├── icml2026/       # ICML 2026 官方
├── iclr2026/       # ICLR 2026 官方
├── neurips2025/    # NeurIPS 2025
├── acl/            # ACL 样式文件
├── aaai2026/       # AAAI 2026
└── colm2025/       # COLM 2025
```
