---
name: code-review-expert
description: "Expert code review of current git changes with a senior engineer lens. Detects SOLID violations, security risks, and proposes actionable improvements."
---

## Language / 语言

- **English** - Scroll down to the English section below
- **中文** - 向下滚动到下方的中文部分

---

# Code Review Expert

## Overview

Perform a structured review of the current git changes with focus on SOLID, architecture, removal candidates, and security risks. Default to review-only output unless the user asks to implement changes.

## Severity Levels

| Level | Name | Description | Action |
|-------|------|-------------|--------|
| **P0** | Critical | Security vulnerability, data loss risk, correctness bug | Must block merge |
| **P1** | High | Logic error, significant SOLID violation, performance regression | Should fix before merge |
| **P2** | Medium | Code smell, maintainability concern, minor SOLID violation | Fix in this PR or create follow-up |
| **P3** | Low | Style, naming, minor suggestion | Optional improvement |

## Workflow

### 1) Preflight context

- Use `git status -sb`, `git diff --stat`, and `git diff` to scope changes.
- If needed, use `rg` or `grep` to find related modules, usages, and contracts.
- Identify entry points, ownership boundaries, and critical paths (auth, payments, data writes, network).

**Edge cases:**
- **No changes**: If `git diff` is empty, inform user and ask if they want to review staged changes or a specific commit range.
- **Large diff (>500 lines)**: Summarize by file first, then review in batches by module/feature area.
- **Mixed concerns**: Group findings by logical feature, not just file order.

### 2) SOLID + architecture smells

- Load `references/solid-checklist.md` for specific prompts.
- Look for:
  - **SRP**: Overloaded modules with unrelated responsibilities.
  - **OCP**: Frequent edits to add behavior instead of extension points.
  - **LSP**: Subclasses that break expectations or require type checks.
  - **ISP**: Wide interfaces with unused methods.
  - **DIP**: High-level logic tied to low-level implementations.
- When you propose a refactor, explain *why* it improves cohesion/coupling and outline a minimal, safe split.
- If refactor is non-trivial, propose an incremental plan instead of a large rewrite.

### 3) Removal candidates + iteration plan

- Load `references/removal-plan.md` for template.
- Identify code that is unused, redundant, or feature-flagged off.
- Distinguish **safe delete now** vs **defer with plan**.
- Provide a follow-up plan with concrete steps and checkpoints (tests/metrics).

### 4) Security and reliability scan

- Load `references/security-checklist.md` for coverage.
- Check for:
  - XSS, injection (SQL/NoSQL/command), SSRF, path traversal
  - AuthZ/AuthN gaps, missing tenancy checks
  - Secret leakage or API keys in logs/env/files
  - Rate limits, unbounded loops, CPU/memory hotspots
  - Unsafe deserialization, weak crypto, insecure defaults
  - **Race conditions**: concurrent access, check-then-act, TOCTOU, missing locks
- Call out both **exploitability** and **impact**.

### 5) Code quality scan

- Load `references/code-quality-checklist.md` for coverage.
- Check for:
  - **Error handling**: swallowed exceptions, overly broad catch, missing error handling, async errors
  - **Performance**: N+1 queries, CPU-intensive ops in hot paths, missing cache, unbounded memory
  - **Boundary conditions**: null/undefined handling, empty collections, numeric boundaries, off-by-one
- Flag issues that may cause silent failures or production incidents.

### 6) Output format

Structure your review as follows:

```markdown
## Code Review Summary

**Files reviewed**: X files, Y lines changed
**Overall assessment**: [APPROVE / REQUEST_CHANGES / COMMENT]

---

## Findings

### P0 - Critical
(none or list)

### P1 - High
1. **[file:line]** Brief title
  - Description of issue
  - Suggested fix

### P2 - Medium
2. (continue numbering across sections)
  - ...

### P3 - Low
...

---

## Removal/Iteration Plan
(if applicable)

## Additional Suggestions
(optional improvements, not blocking)
```

**Inline comments**: Use this format for file-specific findings:
```
::code-comment{file="path/to/file.ts" line="42" severity="P1"}
Description of the issue and suggested fix.
::
```

**Clean review**: If no issues found, explicitly state:
- What was checked
- Any areas not covered (e.g., "Did not verify database migrations")
- Residual risks or recommended follow-up tests

### 7) Next steps confirmation

After presenting findings, ask user how to proceed:

```markdown
---

## Next Steps

I found X issues (P0: _, P1: _, P2: _, P3: _).

**How would you like to proceed?**

1. **Fix all** - I'll implement all suggested fixes
2. **Fix P0/P1 only** - Address critical and high priority issues
3. **Fix specific items** - Tell me which issues to fix
4. **No changes** - Review complete, no implementation needed

Please choose an option or provide specific instructions.
```

**Important**: Do NOT implement any changes until user explicitly confirms. This is a review-first workflow.

## Resources

### references/

| File | Purpose |
|------|---------|
| `solid-checklist.md` | SOLID smell prompts and refactor heuristics |
| `security-checklist.md` | Web/app security and runtime risk checklist |
| `code-quality-checklist.md` | Error handling, performance, boundary conditions |
| `removal-plan.md` | Template for deletion candidates and follow-up plan |

---

# 代码审查专家

## 概述

对当前git变更进行结构化审查，重点关注SOLID原则、架构设计、可移除代码和安全风险。默认仅输出审查结果，除非用户要求实施更改。

## 严重程度等级

| 等级 | 名称 | 描述 | 操作 |
|------|------|------|------|
| **P0** | 严重 | 安全漏洞、数据丢失风险、正确性错误 | 必须阻止合并 |
| **P1** | 高 | 逻辑错误、严重SOLID违规、性能回退 | 应在合并前修复 |
| **P2** | 中 | 代码异味、可维护性问题、轻微SOLID违规 | 在此PR中修复或创建后续任务 |
| **P3** | 低 | 风格、命名、小建议 | 可选改进 |

## 工作流程

### 1) 预检上下文

- 使用 `git status -sb`、`git diff --stat` 和 `git diff` 确定变更范围。
- 如有需要，使用 `rg` 或 `grep` 查找相关模块、用法和合约。
- 识别入口点、所有权边界和关键路径（认证、支付、数据写入、网络）。

**边缘情况：**
- **无变更**：如果 `git diff` 为空，告知用户并询问是否要审查已暂存的变更或特定的提交范围。
- **大型差异 (>500 行)**：先按文件汇总，然后按模块/功能区域分批审查。
- **混合关注点**：按逻辑功能分组发现，而不仅仅是文件顺序。

### 2) SOLID + 架构异味

- 加载 `references/solid-checklist.md` 获取具体提示。
- 查找：
  - **SRP**：具有不相关职责的过载模块。
  - **OCP**：频繁编辑以添加行为而不是扩展点。
  - **LSP**：打破期望或需要类型检查的子类。
  - **ISP**：具有未使用方法的广泛接口。
  - **DIP**：高层逻辑依赖于低层实现。
- 当您提出重构时，解释*为什么*它提高了内聚/耦合度，并概述一个最小、安全的拆分方案。
- 如果重构非微不足道，提出增量计划而不是大规模重写。

### 3) 可移除代码 + 迭代计划

- 加载 `references/removal-plan.md` 获取模板。
- 识别未使用、冗余或功能标记关闭的代码。
- 区分**现在安全删除**与**计划延迟删除**。
- 提供具有具体步骤和检查点（测试/指标）的后续计划。

### 4) 安全和可靠性扫描

- 加载 `references/security-checklist.md` 获取覆盖范围。
- 检查：
  - XSS、注入（SQL/NoSQL/命令）、SSRF、路径遍历
  - 授权/认证缺口、缺少租户检查
  - 秘密泄露或API密钥在日志/环境/文件中
  - 速率限制、无界循环、CPU/内存热点
  - 不安全的反序列化、弱加密、不安全的默认值
  - **竞态条件**：并发访问、检查后行动、TOCTOU、缺少锁
- 同时指出**可利用性**和**影响**。

### 5) 代码质量扫描

- 加载 `references/code-quality-checklist.md` 获取覆盖范围。
- 检查：
  - **错误处理**：吞掉的异常、过于宽泛的捕获、缺少错误处理、异步错误
  - **性能**：N+1查询、热路径中的CPU密集型操作、缺少缓存、无界内存
  - **边界条件**：null/undefined处理、空集合、数值边界、差一错误
- 标记可能导致静默失败或生产事故的问题。

### 6) 输出格式

按以下结构组织您的审查：

```markdown
## 代码审查摘要

**审查文件**：X 文件，Y 行变更
**总体评估**：[批准 / 请求变更 / 评论]

---

## 发现

### P0 - 严重
(无或列表)

### P1 - 高
1. **[文件:行号]** 简短标题
  - 问题描述
  - 建议的修复方案

### P2 - 中
2. (跨部分继续编号)
  - ...

### P3 - 低
...

---

## 移除/迭代计划
(如适用)

## 其他建议
(可选改进，不阻塞)
```

**内联评论**：对特定文件的发现使用以下格式：
```
::code-comment{file="path/to/file.ts" line="42" severity="P1"}
问题描述和建议的修复方案。
::
```

**干净审查**：如果未发现问题，明确说明：
- 检查了什么
- 未覆盖的区域（例如，"未验证数据库迁移"）
- 剩余风险或建议的后续测试

### 7) 后续步骤确认

提出发现后，询问用户如何继续：

```markdown
---

## 后续步骤

我发现了 X 个问题（P0: _，P1: _，P2: _，P3: _）。

**您希望如何继续？**

1. **修复全部** - 我将实施所有建议的修复
2. **仅修复 P0/P1** - 解决严重和高优先级问题
3. **修复特定项目** - 告诉我要修复哪些问题
4. **无变更** - 审查完成，无需实施

请选择一个选项或提供具体说明。
```

**重要**：在用户明确确认之前，不要实施任何更改。这是一个审查优先的工作流程。

## 资源

### references/

| 文件 | 用途 |
|------|------|
| `solid-checklist.md` | SOLID 异味提示和重构启发式方法 |
| `security-checklist.md` | Web/应用安全和运行时风险检查清单 |
| `code-quality-checklist.md` | 错误处理、性能、边界条件 |
| `removal-plan.md` | 删除候选和后续计划模板 |