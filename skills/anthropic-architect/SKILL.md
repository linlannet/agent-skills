---
name: anthropic-architect
description: Determine the best Anthropic architecture for your project by analyzing requirements and recommending the optimal combination of Skills, Agents, Prompts, and SDK primitives.
---

## Language / 语言

- **English** - Scroll down to the English section below
- **中文** - 向下滚动到下方的中文部分

---

# Anthropic Architect

# Anthropic 架构师

Expert architectural guidance for Anthropic-based projects. Analyze your requirements and receive tailored recommendations on the optimal architecture using Skills, Agents, Subagents, Prompts, and SDK primitives.

## What This Skill Does

Helps you design the right Anthropic architecture for your project by:
- **Analyzing project requirements** - Understanding complexity, scope, and constraints
- **Recommending architectures** - Skills vs Agents vs Prompts vs SDK primitives
- **Applying decision rubrics** - Data-driven architectural choices
- **Following best practices** - 2025 Anthropic patterns and principles
- **Progressive disclosure design** - Efficient context management
- **Security considerations** - Safe, controllable AI systems

## Why Architecture Matters

**Without proper architecture:**
- Inefficient context usage and high costs
- Poor performance and slow responses
- Security vulnerabilities and risks
- Difficult to maintain and scale
- Agents reading entire skill contexts unnecessarily
- Mixed concerns and unclear boundaries

**With engineered architecture:**
- Optimal context utilization
- Fast, focused responses
- Secure, controlled operations
- Easy to maintain and extend
- Progressive disclosure of information
- Clear separation of concerns
- Scalable and reusable components

## Quick Start

### Analyze Your Project

```
Using the anthropic-architect skill, help me determine the best
architecture for: [describe your project]

Requirements:
- [List your key requirements]
- [Complexity level]
- [Reusability needs]
- [Security constraints]
```

### Get Architecture Recommendation

The skill will provide:
1. **Recommended architecture** - Specific primitives to use
2. **Decision reasoning** - Why this architecture fits
3. **Implementation guidance** - How to build it
4. **Best practices** - What to follow
5. **Example patterns** - Similar successful architectures

## The Four Anthropic Primitives

### 1. Skills (Prompt-Based Meta-Tools)

**What:** Organized folders of instructions, scripts, and resources that agents can discover and load dynamically.

**When to use:**
- ✅ Specialized domain knowledge needed
- ✅ Reusable across multiple projects
- ✅ Complex, multi-step workflows
- ✅ Reference materials required
- ✅ Progressive disclosure beneficial

**When NOT to use:**
- ❌ Simple, one-off tasks
- ❌ Project-specific logic only
- ❌ No need for reusability

**Example use cases:**
- Prompt engineering expertise
- Design system generation
- Code review guidelines
- Domain-specific knowledge (finance, medical, legal)

### 2. Agents/Subagents (Autonomous Task Handlers)

**What:** Specialized agents with independent system prompts, dedicated context windows, and specific tool permissions.

**When to use:**
- ✅ Complex, multi-step autonomous tasks
- ✅ Need for isolated context
- ✅ Different tool permissions required
- ✅ Parallel task execution
- ✅ Specialized expertise per task type

**When NOT to use:**
- ❌ Simple queries or lookups
- ❌ Shared context required
- ❌ Sequential dependencies
- ❌ Resource-constrained environments

**Example use cases:**
- Code exploration and analysis
- Test generation and execution
- Documentation generation
- Security audits
- Performance optimization

### 3. Direct Prompts (Simple Instructions)

**What:** Clear, explicit instructions passed directly to Claude without additional structure.

**When to use:**
- ✅ Simple, straightforward tasks
- ✅ One-time operations
- ✅ Quick questions or clarifications
- ✅ No need for specialization
- ✅ Minimal context required

**When NOT to use:**
- ❌ Complex, multi-step processes
- ❌ Need for reusability
- ❌ Requires domain expertise
- ❌ Multiple related operations

**Example use cases:**
- Code explanations
- Quick refactoring
- Simple bug fixes
- Documentation updates
- Direct questions

### 4. SDK Primitives (Custom Workflows)

**What:** Low-level building blocks from the Claude Agent SDK to create custom agent workflows.

**When to use:**
- ✅ Unique workflow requirements
- ✅ Custom tool integration needed
- ✅ Specific feedback loops required
- ✅ Integration with existing systems
- ✅ Fine-grained control needed

**When NOT to use:**
- ❌ Standard use cases covered by Skills/Agents
- ❌ Limited development resources
- ❌ Maintenance burden concern
- ❌ Faster time-to-market priority

**Example use cases:**
- Custom CI/CD integration
- Specialized code analysis pipelines
- Domain-specific automation
- Integration with proprietary systems

## Decision Rubric

Use this rubric to determine the right architecture:

### Task Complexity Analysis

**Low Complexity** → Direct Prompts
- Single operation
- Clear input/output
- No dependencies
- < 5 steps

**Medium Complexity** → Skills
- Multiple related operations
- Reusable patterns
- Reference materials helpful
- 5-20 steps

**High Complexity** → Agents/Subagents
- Multi-step autonomous workflow
- Needs isolated context
- Different tool permissions
- > 20 steps or parallel tasks

**Custom Complexity** → SDK Primitives
- Unique workflows
- System integration required
- Custom tools needed
- Specific feedback loops

### Reusability Assessment

**Single Use** → Direct Prompts
- One-time task
- Project-specific
- No future reuse

**Team Reuse** → Skills
- Multiple team members benefit
- Common workflows
- Shareable knowledge

**Organization Reuse** → Skills + Marketplace
- Cross-team benefit
- Standard patterns
- Company-wide knowledge

**Product Feature** → SDK Primitives
- End-user facing
- Production deployment
- Custom integration

### Context Management Needs

**Minimal Context** → Direct Prompts
- Self-contained task
- No external references
- Simple instructions

**Structured Context** → Skills
- Progressive disclosure needed
- Reference materials required
- Organized information

**Isolated Context** → Agents/Subagents
- Separate concerns
- Avoid context pollution
- Parallel execution

**Custom Context** → SDK Primitives
- Specific context handling
- Integration requirements
- Fine-grained control

### Security & Control Requirements

**Basic Safety** → Direct Prompts + Skills
- Standard guardrails
- No sensitive operations
- Read-only or low-risk

**Controlled Access** → Agents with Tool Restrictions
- Specific tool permissions
- Allowlist approach
- Confirmation required

**High Security** → SDK Primitives + Custom Controls
- Deny-all default
- Explicit confirmations
- Audit logging
- Custom security layers

## Architecture Patterns

### Pattern 1: Skills-First Architecture

**Use when:** Building reusable expertise and workflows

**Structure:**
```
Project
├── skills/
│   ├── domain-expert/
│   │   ├── SKILL.md
│   │   └── references/
│   │       ├── patterns.md
│   │       ├── best_practices.md
│   │       └── examples.md
│   └── workflow-automation/
│       ├── SKILL.md
│       └── scripts/
│           └── automate.sh
└── .claude/
    └── config
```

**Benefits:**
- Reusable across projects
- Progressive disclosure
- Easy to share and maintain
- Clear documentation

### Pattern 2: Agent-Based Architecture

**Use when:** Complex autonomous tasks with isolated concerns

**Structure:**
```
Main Agent (orchestrator)
├── Explore Agent (codebase analysis)
├── Plan Agent (task planning)
├── Code Agent (implementation)
└── Review Agent (validation)
```

**Benefits:**
- Parallel execution
- Isolated contexts
- Specialized expertise
- Clear responsibilities

### Pattern 3: Hybrid Architecture

**Use when:** Complex projects with varied requirements

**Structure:**
```
Main Conversation
├── Direct Prompts (simple tasks)
├── Skills (reusable expertise)
│   ├── code-review-skill
│   └── testing-skill
└── Subagents (complex workflows)
    ├── Explore Agent
    └── Plan Agent
```

**Benefits:**
- Right tool for each task
- Optimal resource usage
- Flexible and scalable
- Best of all approaches

### Pattern 4: SDK Custom Architecture

**Use when:** Unique requirements or product features

**Structure:**
```
Custom Agent SDK Implementation
├── Custom Tools
├── Specialized Feedback Loops
├── System Integrations
└── Domain-Specific Workflows
```

**Benefits:**
- Full control
- Custom integration
- Unique workflows
- Production-ready

## Key Principles (2025)

### 1. Progressive Disclosure
**What:** Show only what's needed, when it's needed.

**Why:** Avoids context limits, reduces costs, improves performance.

**How:** Organize skills with task-based navigation, provide query tools, structure information hierarchically.

### 2. Context as Resource
**What:** Treat context window as precious, limited resource.

**Why:** Every token counts toward limits and costs.

**How:** Use progressive disclosure, prefer retrieval over dumping, compress aggressively, reset periodically.

### 3. Clear Instructions
**What:** Explicit, unambiguous directions.

**Why:** Claude 4.x responds best to clarity.

**How:** Be specific, define output format, provide examples, avoid vagueness.

### 4. Security by Design
**What:** Deny-all default, allowlist approach.

**Why:** Safe, controlled AI systems.

**How:** Limit tool access, require confirmations, audit operations, block dangerous commands.

### 5. Thinking Capabilities
**What:** Leverage Claude's extended thinking mode.

**Why:** Better results for complex reasoning.

**How:** Request step-by-step thinking, allow reflection after tool use, guide initial thinking.

### 6. Two-Message Pattern
**What:** Use meta messages for context without UI clutter.

**Why:** Clean UX while providing necessary context.

**How:** Set isMeta: true for system messages, use for skill loading, keep UI focused.

## Reference Materials

All architectural patterns, decision frameworks, and examples are in the `references/` directory:

- **decision_rubric.md** - Comprehensive decision framework
- **architectural_patterns.md** - Detailed pattern catalog
- **best_practices.md** - 2025 Anthropic best practices
- **use_case_examples.md** - Real-world architecture examples

## Usage Examples

### Example 1: Determining Architecture for Content Generation

**Input:**
```
Using anthropic-architect, I need to build a system that:
- Generates blog posts from product features
- Ensures brand voice consistency
- Includes SEO optimization
- Reusable across marketing team
```

**Analysis:**
- Medium complexity (structured workflow)
- High reusability (team-wide)
- Domain expertise needed (content, SEO, brand)
- Progressive disclosure beneficial

**Recommendation:** **Skills-First Architecture**
- Create `content-generator` skill
- Include brand voice references
- SEO guidelines in references
- Example templates
- Progressive disclosure for different content types

### Example 2: Code Refactoring Tool

**Input:**
```
Using anthropic-architect, I want to:
- Analyze codebase for refactoring opportunities
- Generate refactoring plan
- Execute refactoring with tests
- Review and validate changes
```

**Analysis:**
- High complexity (multi-step, autonomous)
- Different contexts needed (explore, plan, code, review)
- Parallel execution beneficial
- Tool permissions vary by stage

**Recommendation:** **Agent-Based Architecture**
- Main orchestrator agent
- Explore subagent (read-only, codebase analysis)
- Plan subagent (planning, no execution)
- Code subagent (write permissions)
- Review subagent (validation, test execution)

### Example 3: Simple Code Review

**Input:**
```
Using anthropic-architect, I need to:
- Review this PR for bugs
- Check code style
- Suggest improvements
```

**Analysis:**
- Low complexity (single operation)
- One-time task
- No reusability needed
- Minimal context

**Recommendation:** **Direct Prompt**
- Simple, clear instructions
- No skill/agent overhead
- Fast execution
- Sufficient for task

### Example 4: Custom CI/CD Integration

**Input:**
```
Using anthropic-architect, I want to:
- Integrate Claude into CI pipeline
- Custom tool for deployment validation
- Specific workflow for our stack
- Production feature
```

**Analysis:**
- Custom complexity
- System integration required
- Production deployment
- Unique workflows

**Recommendation:** **SDK Primitives**
- Build custom agent with SDK
- Implement custom tools
- Create specialized feedback loops
- Integration with CI system

## Best Practices Checklist

When designing your architecture:

- [ ] Analyzed task complexity accurately
- [ ] Considered reusability requirements
- [ ] Evaluated context management needs
- [ ] Assessed security requirements
- [ ] Applied progressive disclosure where beneficial
- [ ] Chose simplest solution that works
- [ ] Documented architectural decisions
- [ ] Planned for maintenance and updates
- [ ] Considered cost implications
- [ ] Validated with prototype/POC

## Common Anti-Patterns

### Anti-Pattern 1: Over-Engineering
**Problem:** Using Agents/SDK for simple tasks

**Solution:** Start simple, scale complexity as needed

### Anti-Pattern 2: Context Dumping
**Problem:** Loading entire skills into context

**Solution:** Use progressive disclosure, query tools

### Anti-Pattern 3: Mixed Concerns
**Problem:** Single skill/agent doing too much

**Solution:** Separate concerns, use subagents or multiple skills

### Anti-Pattern 4: No Security Boundaries
**Problem:** Full tool access for all agents

**Solution:** Allowlist approach, minimal permissions

### Anti-Pattern 5: Ignoring Reusability
**Problem:** Recreating same prompts repeatedly

**Solution:** Extract to skills, share across projects

## Getting Started

### Step 1: Describe Your Project
Provide clear requirements, complexity level, and constraints.

### Step 2: Receive Recommendation
Get tailored architecture with reasoning.

### Step 3: Review Patterns
Explore similar successful architectures.

### Step 4: Implement
Follow implementation guidance.

### Step 5: Iterate
Refine based on results and feedback.

## Summary

The Anthropic Architect skill helps you:
- Choose the right primitives for your needs
- Design scalable, maintainable architectures
- Follow 2025 best practices
- Avoid common pitfalls
- Optimize for performance and cost

**Key Primitives:**
- **Skills** - Reusable domain expertise
- **Agents** - Autonomous complex workflows
- **Prompts** - Simple direct tasks
- **SDK** - Custom integrations

**Core Principles:**
- Progressive disclosure
- Context as resource
- Security by design
- Clear instructions
- Right tool for the job

---

**"The best architecture is the simplest one that meets your requirements."**

---

# Anthropic 架构师

为基于Anthropic的项目提供专业的架构指导。分析您的需求，并针对使用Skills、Agents、Subagents、Prompts和SDK原语的最佳架构提供定制建议。

## 此技能的功能

通过以下方式帮助您为项目设计合适的Anthropic架构：
- **分析项目需求** - 理解复杂性、范围和约束
- **推荐架构** - Skills vs Agents vs Prompts vs SDK原语
- **应用决策准则** - 数据驱动的架构选择
- **遵循最佳实践** - 2025年Anthropic模式和原则
- **渐进式信息披露设计** - 高效的上下文管理
- **安全考虑** - 安全、可控的AI系统

## 架构的重要性

**没有适当架构的后果：**
- 上下文使用效率低，成本高
- 性能差，响应慢
- 安全漏洞和风险
- 难以维护和扩展
- Agents不必要地读取整个skill上下文
- 混合关注点和模糊边界

**采用精心设计的架构的好处：**
- 最佳上下文利用率
- 快速、专注的响应
- 安全、可控的操作
- 易于维护和扩展
- 信息的渐进式披露
- 明确的关注点分离
- 可扩展和可重用的组件

## 快速开始

### 分析您的项目

```
使用anthropic-architect技能，帮助我确定最佳架构：[描述您的项目]

需求：
- [列出您的关键需求]
- [复杂性级别]
- [可重用性需求]
- [安全约束]
```

### 获取架构建议

该技能将提供：
1. **推荐架构** - 要使用的具体原语
2. **决策理由** - 为什么此架构适合
3. **实施指导** - 如何构建
4. **最佳实践** - 要遵循的内容
5. **示例模式** - 类似的成功架构

## 四种Anthropic原语

### 1. Skills（基于提示的元工具）

**定义：** 组织良好的指令、脚本和资源文件夹，agents可以动态发现和加载。

**何时使用：**
- ✅ 需要专业领域知识
- ✅ 可在多个项目中重用
- ✅ 复杂、多步骤工作流
- ✅ 需要参考材料
- ✅ 渐进式信息披露有益

**何时不使用：**
- ❌ 简单、一次性任务
- ❌ 仅项目特定逻辑
- ❌ 不需要可重用性

**示例用例：**
- 提示工程专业知识
- 设计系统生成
- 代码审查指南
- 特定领域知识（金融、医疗、法律）

### 2. Agents/Subagents（自主任务处理程序）

**定义：** 具有独立系统提示、专用上下文窗口和特定工具权限的专业agents。

**何时使用：**
- ✅ 复杂、多步骤自主任务
- ✅ 需要隔离的上下文
- ✅ 需要不同的工具权限
- ✅ 并行任务执行
- ✅ 每种任务类型需要专业知识

**何时不使用：**
- ❌ 简单查询或查找
- ❌ 需要共享上下文
- ❌ 顺序依赖
- ❌ 资源受限环境

**示例用例：**
- 代码探索和分析
- 测试生成和执行
- 文档生成
- 安全审计
- 性能优化

### 3. Direct Prompts（简单指令）

**定义：** 直接传递给Claude的清晰、明确的指令，无需额外结构。

**何时使用：**
- ✅ 简单、直接的任务
- ✅ 一次性操作
- ✅ 快速问题或澄清
- ✅ 不需要专业化
- ✅ 需要最小上下文

**何时不使用：**
- ❌ 复杂、多步骤流程
- ❌ 需要可重用性
- ❌ 需要领域专业知识
- ❌ 多个相关操作

**示例用例：**
- 代码解释
- 快速重构
- 简单错误修复
- 文档更新
- 直接问题

### 4. SDK Primitives（自定义工作流）

**定义：** 来自Claude Agent SDK的低级构建块，用于创建自定义agent工作流。

**何时使用：**
- ✅ 独特的工作流需求
- ✅ 需要自定义工具集成
- ✅ 需要特定的反馈循环
- ✅ 与现有系统集成
- ✅ 需要细粒度控制

**何时不使用：**
- ❌ Skills/Agents覆盖的标准用例
- ❌ 有限的开发资源
- ❌ 担心维护负担
- ❌ 优先考虑更快的上市时间

**示例用例：**
- 自定义CI/CD集成
- 专业代码分析管道
- 特定领域自动化
- 与专有系统集成

## 决策准则

使用此准则确定正确的架构：

### 任务复杂性分析

**低复杂性** → Direct Prompts
- 单一操作
- 明确的输入/输出
- 无依赖
- < 5步

**中等复杂性** → Skills
- 多个相关操作
- 可重用模式
- 参考材料有帮助
- 5-20步

**高复杂性** → Agents/Subagents
- 多步自主工作流
- 需要隔离的上下文
- 不同的工具权限
- > 20步或并行任务

**自定义复杂性** → SDK Primitives
- 独特的工作流
- 需要系统集成
- 需要自定义工具
- 特定的反馈循环

### 可重用性评估

**单次使用** → Direct Prompts
- 一次性任务
- 项目特定
- 无未来重用

**团队重用** → Skills
- 多个团队成员受益
- 常见工作流
- 可共享知识

**组织重用** → Skills + Marketplace
- 跨团队受益
- 标准模式
- 公司范围知识

**产品功能** → SDK Primitives
- 面向最终用户
- 生产部署
- 自定义集成

### 上下文管理需求

**最小上下文** → Direct Prompts
- 自包含任务
- 无外部引用
- 简单指令

**结构化上下文** → Skills
- 需要渐进式披露
- 需要参考材料
- 组织信息

**隔离上下文** → Agents/Subagents
- 分离关注点
- 避免上下文污染
- 并行执行

**自定义上下文** → SDK Primitives
- 特定的上下文处理
- 集成要求
- 细粒度控制

### 安全和控制要求

**基本安全** → Direct Prompts + Skills
- 标准护栏
- 无敏感操作
- 只读或低风险

**受控访问** → 带工具限制的Agents
- 特定工具权限
- 白名单方法
- 需要确认

**高安全性** → SDK Primitives + 自定义控制
- 默认拒绝所有
- 明确确认
- 审计日志
- 自定义安全层

## 架构模式

### 模式1：Skills优先架构

**何时使用：** 构建可重用的专业知识和工作流

**结构：**
```
项目
├── skills/
│   ├── domain-expert/
│   │   ├── SKILL.md
│   │   └── references/
│   │       ├── patterns.md
│   │       ├── best_practices.md
│   │       └── examples.md
│   └── workflow-automation/
│       ├── SKILL.md
│       └── scripts/
│           └── automate.sh
└── .claude/
    └── config
```

**好处：**
- 可在项目间重用
- 渐进式信息披露
- 易于共享和维护
- 清晰的文档

### 模式2：基于Agent的架构

**何时使用：** 具有隔离关注点的复杂自主任务

**结构：**
```
主Agent（编排器）
├── 探索Agent（代码库分析）
├── 计划Agent（任务规划）
├── 代码Agent（实现）
└── 审查Agent（验证）
```

**好处：**
- 并行执行
- 隔离的上下文
- 专业知识
- 明确的责任

### 模式3：混合架构

**何时使用：** 具有不同需求的复杂项目

**结构：**
```
主对话
├── Direct Prompts（简单任务）
├── Skills（可重用专业知识）
│   ├── code-review-skill
│   └── testing-skill
└── Subagents（复杂工作流）
    ├── 探索Agent
    └── 计划Agent
```

**好处：**
- 为每个任务选择正确的工具
- 最佳资源使用
- 灵活和可扩展
- 所有方法的优点

### 模式4：SDK自定义架构

**何时使用：** 独特需求或产品功能

**结构：**
```
自定义Agent SDK实现
├── 自定义工具
├── 专业反馈循环
├── 系统集成
└── 特定领域工作流
```

**好处：**
- 完全控制
- 自定义集成
- 独特的工作流
- 生产就绪

## 关键原则（2025）

### 1. 渐进式信息披露
**定义：** 只在需要时显示所需内容。

**原因：** 避免上下文限制，降低成本，提高性能。

**方法：** 组织具有基于任务导航的skills，提供查询工具，分层结构化信息。

### 2. 上下文作为资源
**定义：** 将上下文窗口视为宝贵、有限的资源。

**原因：** 每个token都计入限制和成本。

**方法：** 使用渐进式披露，优先检索而非倾倒，积极压缩，定期重置。

### 3. 清晰指令
**定义：** 明确、无歧义的指示。

**原因：** Claude 4.x对清晰度反应最佳。

**方法：** 具体说明，定义输出格式，提供示例，避免模糊。

### 4. 设计安全
**定义：** 默认拒绝所有，白名单方法。

**原因：** 安全、可控的AI系统。

**方法：** 限制工具访问，要求确认，审计操作，阻止危险命令。

### 5. 思考能力
**定义：** 利用Claude的扩展思考模式。

**原因：** 复杂推理的更好结果。

**方法：** 请求逐步思考，允许工具使用后反思，引导初始思考。

### 6. 两消息模式
**定义：** 使用元消息进行上下文而无UI混乱。

**原因：** 干净的UX同时提供必要的上下文。

**方法：** 为系统消息设置isMeta: true，用于skill加载，保持UI专注。

## 参考材料

所有架构模式、决策框架和示例都在`references/`目录中：

- **decision_rubric.md** - 综合决策框架
- **architectural_patterns.md** - 详细模式目录
- **best_practices.md** - 2025年Anthropic最佳实践
- **use_case_examples.md** - 真实世界架构示例

## 使用示例

### 示例1：内容生成架构确定

**输入：**
```
使用anthropic-architect，我需要构建一个系统，用于：
- 从产品功能生成博客文章
- 确保品牌声音一致性
- 包含SEO优化
- 可在营销团队中重用
```

**分析：**
- 中等复杂性（结构化工作流）
- 高可重用性（团队范围）
- 需要领域专业知识（内容、SEO、品牌）
- 渐进式信息披露有益

**推荐：** **Skills优先架构**
- 创建`content-generator` skill
- 包含品牌声音参考
- SEO指南在参考中
- 示例模板
- 不同内容类型的渐进式披露

### 示例2：代码重构工具

**输入：**
```
使用anthropic-architect，我想要：
- 分析代码库以寻找重构机会
- 生成重构计划
- 执行带测试的重构
- 审查和验证更改
```

**分析：**
- 高复杂性（多步、自主）
- 需要不同的上下文（探索、计划、代码、审查）
- 并行执行有益
- 工具权限因阶段而异

**推荐：** **基于Agent的架构**
- 主编排器agent
- 探索子agent（只读，代码库分析）
- 计划子agent（规划，无执行）
- 代码子agent（写入权限）
- 审查子agent（验证，测试执行）

### 示例3：简单代码审查

**输入：**
```
使用anthropic-architect，我需要：
- 审查此PR的错误
- 检查代码风格
- 建议改进
```

**分析：**
- 低复杂性（单一操作）
- 一次性任务
- 无需可重用性
- 最小上下文

**推荐：** **Direct Prompt**
- 简单、明确的指令
- 无skill/agent开销
- 快速执行
- 足以完成任务

### 示例4：自定义CI/CD集成

**输入：**
```
使用anthropic-architect，我想要：
- 将Claude集成到CI管道中
- 用于部署验证的自定义工具
- 针对我们栈的特定工作流
- 生产功能
```

**分析：**
- 自定义复杂性
- 需要系统集成
- 生产部署
- 独特的工作流

**推荐：** **SDK Primitives**
- 使用SDK构建自定义agent
- 实现自定义工具
- 创建专业反馈循环
- 与CI系统集成

## 最佳实践清单

设计架构时：

- [ ] 准确分析任务复杂性
- [ ] 考虑可重用性要求
- [ ] 评估上下文管理需求
- [ ] 评估安全要求
- [ ] 在有益处的地方应用渐进式披露
- [ ] 选择可行的最简单解决方案
- [ ] 记录架构决策
- [ ] 计划维护和更新
- [ ] 考虑成本影响
- [ ] 使用原型/POC验证

## 常见反模式

### 反模式1：过度工程
**问题：** 对简单任务使用Agents/SDK

**解决方案：** 从简单开始，根据需要扩展复杂性

### 反模式2：上下文倾倒
**问题：** 将整个skills加载到上下文

**解决方案：** 使用渐进式披露，查询工具

### 反模式3：混合关注点
**问题：** 单个skill/agent做太多事情

**解决方案：** 分离关注点，使用subagents或多个skills

### 反模式4：无安全边界
**问题：** 所有agents的完全工具访问

**解决方案：** 白名单方法，最小权限

### 反模式5：忽略可重用性
**问题：** 重复创建相同的提示

**解决方案：** 提取到skills，跨项目共享

## 入门指南

### 步骤1：描述您的项目
提供明确的需求、复杂性级别和约束。

### 步骤2：接收建议
获取带有理由的定制架构。

### 步骤3：审查模式
探索类似的成功架构。

### 步骤4：实施
遵循实施指导。

### 步骤5：迭代
基于结果和反馈进行完善。

## 总结

Anthropic Architect技能帮助您：
- 为您的需求选择正确的原语
- 设计可扩展、可维护的架构
- 遵循2025年最佳实践
- 避免常见陷阱
- 针对性能和成本进行优化

**关键原语：**
- **Skills** - 可重用领域专业知识
- **Agents** - 自主复杂工作流
- **Prompts** - 简单直接任务
- **SDK** - 自定义集成

**核心原则：**
- 渐进式信息披露
- 上下文作为资源
- 设计安全
- 清晰指令
- 为工作选择正确的工具

---

**"最佳架构是满足您需求的最简单架构。"**
