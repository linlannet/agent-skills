# Removal and Iteration Plan Template

## Priority Levels

- [ ] **P0**: Immediate removal needed (security risk, significant cost, blocking other work)
- [ ] **P1**: Remove in current sprint
- [ ] **P2**: Backlog / next iteration

---

## Safe to Remove Now

### Item: [Name/Description]

| Field | Details |
|-------|---------|
| **Location** | `path/to/file.ts:line` |
| **Rationale** | Why this should be removed |
| **Evidence** | Unused (no references), dead feature flag, deprecated API |
| **Impact** | None / Low - no active consumers |
| **Deletion steps** | 1. Remove code 2. Remove tests 3. Remove config |
| **Verification** | Run tests, check no runtime errors, monitor logs |

---

## Defer Removal (Plan Required)

### Item: [Name/Description]

| Field | Details |
|-------|---------|
| **Location** | `path/to/file.ts:line` |
| **Why defer** | Active consumers, needs migration, stakeholder sign-off |
| **Preconditions** | Feature flag off for 2 weeks, telemetry shows 0 usage |
| **Breaking changes** | List any API/contract changes |
| **Migration plan** | Steps for consumers to migrate |
| **Timeline** | Target date or sprint |
| **Owner** | Person/team responsible |
| **Validation** | Metrics to confirm safe removal (error rates, usage counts) |
| **Rollback plan** | How to restore if issues found |

---

## Checklist Before Removal

- [ ] Searched codebase for all references (`rg`, `grep`)
- [ ] Checked for dynamic/reflection-based usage
- [ ] Verified no external consumers (APIs, SDKs, docs)
- [ ] Feature flag telemetry reviewed (if applicable)
- [ ] Tests updated/removed
- [ ] Documentation updated
- [ ] Team notified (if shared code)

---

# 移除和迭代计划模板

## 优先级等级

- [ ] **P0**：需要立即移除（安全风险、显著成本、阻塞其他工作）
- [ ] **P1**：在当前冲刺中移除
- [ ] **P2**：待办事项 / 下一次迭代

---

## 现在安全移除

### 项目：[名称/描述]

| 字段 | 详情 |
|------|------|
| **位置** | `path/to/file.ts:line` |
| **理由** | 为什么应该移除 |
| **证据** | 未使用（无引用）、已停用的功能标志、已弃用的API |
| **影响** | 无 / 低 - 无活跃消费者 |
| **删除步骤** | 1. 移除代码 2. 移除测试 3. 移除配置 |
| **验证** | 运行测试，检查无运行时错误，监控日志 |

---

## 延迟移除（需要计划）

### 项目：[名称/描述]

| 字段 | 详情 |
|------|------|
| **位置** | `path/to/file.ts:line` |
| **为什么延迟** | 活跃消费者、需要迁移、利益相关者签字 |
| **前置条件** | 功能标志关闭2周，遥测显示0使用 |
| **破坏性变更** | 列出任何API/合约变更 |
| **迁移计划** | 消费者迁移步骤 |
| **时间线** | 目标日期或冲刺 |
| **所有者** | 负责的人员/团队 |
| **验证** | 确认安全移除的指标（错误率、使用计数） |
| **回滚计划** | 如果发现问题如何恢复 |

---

## 移除前检查清单

- [ ] 搜索代码库中的所有引用（`rg`、`grep`）
- [ ] 检查动态/反射-based用法
- [ ] 验证无外部消费者（API、SDK、文档）
- [ ] 功能标志遥测已审查（如适用）
- [ ] 测试已更新/移除
- [ ] 文档已更新
- [ ] 团队已通知（如果是共享代码）
