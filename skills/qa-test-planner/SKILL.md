---
name: qa-test-planner
description: Generate comprehensive test plans, manual test cases, regression test suites, and bug reports for QA engineers. Includes Figma MCP integration for design validation.
---

## Language / 语言

- **English** - Scroll down to the English section below
- **中文** - 向下滚动到下方的中文部分

---

# QA Test Planner

A comprehensive skill for QA engineers to create test plans, generate manual test cases, build regression test suites, validate designs against Figma, and document bugs effectively.

## What This Skill Does

Helps QA engineers with:
- **Test Plan Creation** - Comprehensive test strategy and planning
- **Manual Test Case Generation** - Detailed step-by-step test cases
- **Regression Test Suites** - Critical path and smoke test suites
- **Figma Design Validation** - Compare implementation against designs (requires Figma MCP)
- **Bug Report Templates** - Clear, reproducible bug documentation
- **Test Coverage Analysis** - Identify gaps in testing
- **Test Execution Tracking** - Monitor testing progress

## Why You Need This Skill

**Without structured testing:**
- Inconsistent test coverage
- Missed edge cases
- Poor bug documentation
- No regression safety net
- Design implementation gaps
- Unclear test strategy

**With this skill:**
- Comprehensive test coverage
- Repeatable test cases
- Systematic regression testing
- Design-implementation validation
- Professional bug reports
- Clear testing roadmap

## Core Components

### 1. Test Plan Generator
- Test scope and objectives
- Testing approach and strategy
- Test environment requirements
- Entry/exit criteria
- Risk assessment
- Resource allocation
- Timeline and milestones

### 2. Manual Test Case Generator
- Step-by-step instructions
- Expected vs actual results
- Preconditions and setup
- Test data requirements
- Priority and severity
- Edge case identification

### 3. Regression Test Suite Builder
- Smoke test cases
- Critical path testing
- Integration test scenarios
- Backward compatibility checks
- Performance regression tests

### 4. Figma Design Validation (with MCP)
- Compare UI implementation to designs
- Identify visual discrepancies
- Validate spacing, colors, typography
- Check component consistency
- Flag design-dev mismatches

### 5. Bug Report Generator
- Clear reproduction steps
- Environment details
- Expected vs actual behavior
- Screenshots and evidence
- Severity and priority
- Related test cases

## Test Case Structure

### Standard Test Case Format

```markdown
## TC-001: [Test Case Title]

**Priority:** High | Medium | Low
**Type:** Functional | UI | Integration | Regression
**Status:** Not Run | Pass | Fail | Blocked

### Objective
[What are we testing and why]

### Preconditions
- [Setup requirement 1]
- [Setup requirement 2]
- [Test data needed]

### Test Steps
1. [Action to perform]
   **Expected:** [What should happen]

2. [Action to perform]
   **Expected:** [What should happen]

3. [Action to perform]
   **Expected:** [What should happen]

### Test Data
- Input: [Test data values]
- User: [Test account details]
- Configuration: [Environment settings]

### Post-conditions
- [System state after test]
- [Cleanup required]

### Notes
- [Edge cases to consider]
- [Related test cases]
- [Known issues]
```

## Test Plan Template

### Executive Summary
- Feature/product being tested
- Testing objectives
- Key risks
- Timeline overview

### Test Scope

**In Scope:**
- Features to be tested
- Test types (functional, UI, performance, etc.)
- Platforms and environments
- User flows and scenarios

**Out of Scope:**
- Features not being tested (deferred)
- Known limitations
- Third-party integrations (if applicable)

### Test Strategy

**Test Types:**
- Manual testing
- Exploratory testing
- Regression testing
- Integration testing
- User acceptance testing
- Performance testing (if applicable)

**Test Approach:**
- Black box testing
- Positive and negative testing
- Boundary value analysis
- Equivalence partitioning

### Test Environment
- Operating systems
- Browsers and versions
- Devices (mobile, tablet, desktop)
- Test data requirements
- Backend/API environments

### Entry Criteria
- [ ] Requirements documented
- [ ] Designs finalized
- [ ] Test environment ready
- [ ] Test data prepared
- [ ] Build deployed to test environment

### Exit Criteria
- [ ] All high-priority test cases executed
- [ ] 90%+ test case pass rate
- [ ] All critical bugs fixed
- [ ] No open high-severity bugs
- [ ] Regression suite passed
- [ ] Stakeholder sign-off

### Risk Assessment

| Risk | Probability | Impact | Mitigation |
|------|-------------|--------|------------|
| [Risk 1] | High/Med/Low | High/Med/Low | [How to mitigate] |
| [Risk 2] | High/Med/Low | High/Med/Low | [How to mitigate] |

### Test Deliverables
- Test plan document
- Test cases
- Test execution reports
- Bug reports
- Test summary report

## Test Types and Approaches

### 1. Functional Testing

**What:** Verify features work as specified

**Test Cases:**
- Happy path scenarios
- Error handling
- Input validation
- Business logic
- Data integrity

**Example:**
```
TC: User Login with Valid Credentials
1. Navigate to login page
2. Enter valid email and password
3. Click "Login" button
Expected: User redirected to dashboard, welcome message shown
```

### 2. UI/Visual Testing

**What:** Verify visual appearance and layout

**Test Cases:**
- Layout and alignment
- Responsive design
- Color and typography
- Component states (hover, active, disabled)
- Cross-browser compatibility

**With Figma MCP:**
- Compare implementation to Figma designs
- Verify spacing (padding, margins)
- Check font sizes and weights
- Validate color values
- Ensure icon accuracy

**Example:**
```
TC: Homepage Hero Section Visual Validation
1. Open homepage in browser
2. Compare against Figma design [link]
3. Verify:
   - Heading font: 48px, bold, #1A1A1A
   - CTA button: 16px padding, #0066FF background
   - Image aspect ratio: 16:9
   - Spacing: 64px margin-bottom
Expected: All visual elements match Figma exactly
```

### 3. Regression Testing

**What:** Ensure existing functionality still works

**When to Run:**
- Before each release
- After bug fixes
- After new features
- Weekly smoke tests

**Suite Components:**
- Smoke tests (critical paths)
- Full regression (comprehensive)
- Targeted regression (affected areas)

**Example:**
```
Regression Suite: User Authentication
- Login with valid credentials
- Login with invalid credentials
- Password reset flow
- Session timeout handling
- Multi-device login
- Social login (Google, GitHub)
```

### 4. Integration Testing

**What:** Verify different components work together

**Test Cases:**
- API integration
- Database operations
- Third-party services
- Cross-module interactions
- Data flow between components

**Example:**
```
TC: Checkout Payment Integration
1. Add item to cart
2. Proceed to checkout
3. Enter payment details (Stripe)
4. Submit payment
Expected:
- Payment processed via Stripe API
- Order created in database
- Confirmation email sent
- Inventory updated
```

### 5. Exploratory Testing

**What:** Unscripted, creative testing

**Approach:**
- Charter-based exploration
- User persona simulation
- Edge case discovery
- Usability evaluation

**Session Template:**
```
Exploratory Testing Session
Charter: Explore [feature] as [user type]
Time: 60 minutes
Focus: [Area to explore]

Findings:
- [Bug/issue discovered]
- [UX concern]
- [Improvement suggestion]

Follow-up:
- [Test cases to create]
- [Bugs to file]
```

## Figma MCP Integration

### Design Validation Workflow

**Prerequisites:**
- Figma MCP server configured
- Design file access
- Figma URLs available

**Validation Process:**

1. **Get Design Specs from Figma**
```
"Get the button specifications from Figma file [URL]"
- Component: Primary Button
- Width: 120px
- Height: 40px
- Border-radius: 8px
- Background: #0066FF
- Font: 16px, Medium, #FFFFFF
```

2. **Compare Implementation**
```
TC: Primary Button Visual Validation
1. Inspect primary button in browser dev tools
2. Compare against Figma specs:
   - Dimensions: 120x40px ✓ / ✗
   - Border-radius: 8px ✓ / ✗
   - Background color: #0066FF ✓ / ✗
   - Font: 16px Medium #FFFFFF ✓ / ✗
3. Document discrepancies
```

3. **Create Bug if Mismatch**
```
BUG: Primary button color doesn't match design
Severity: Medium
Expected (Figma): #0066FF
Actual (Implementation): #0052CC
Screenshot: [attached]
Figma link: [specific component]
```

### Design-Dev Handoff Checklist

**Using Figma MCP:**
- [ ] Retrieve spacing values from design
- [ ] Verify color palette matches
- [ ] Check typography specifications
- [ ] Validate component states (hover, active, disabled)
- [ ] Confirm breakpoint behavior
- [ ] Review iconography and assets
- [ ] Check accessibility annotations

## Bug Reporting Best Practices

### Effective Bug Report Template

```markdown
# BUG-[ID]: [Clear, specific title]

**Severity:** Critical | High | Medium | Low
**Priority:** P0 | P1 | P2 | P3
**Type:** Functional | UI | Performance | Security
**Status:** Open | In Progress | Fixed | Closed

## Environment
- **OS:** [Windows 11, macOS 14, etc.]
- **Browser:** [Chrome 120, Firefox 121, etc.]
- **Device:** [Desktop, iPhone 15, etc.]
- **Build:** [Version/commit]
- **URL:** [Page where bug occurs]

## Description
[Clear, concise description of the issue]

## Steps to Reproduce
1. [Specific step]
2. [Specific step]
3. [Specific step]

## Expected Behavior
[What should happen]

## Actual Behavior
[What actually happens]

## Visual Evidence
- Screenshot: [attached]
- Video: [link if applicable]
- Console errors: [paste errors]
- Network logs: [if relevant]

## Impact
- **User Impact:** [How many users affected]
- **Frequency:** [Always, Sometimes, Rarely]
- **Workaround:** [If one exists]

## Additional Context
- Related to: [Feature/ticket]
- First noticed: [When]
- Regression: [Yes/No - if yes, since when]
- Figma design: [Link if UI bug]

## Test Cases Affected
- TC-001: [Test case that failed]
- TC-045: [Related test case]
```

### Bug Severity Definitions

**Critical (P0):**
- System crash or data loss
- Security vulnerability
- Complete feature breakdown
- Blocks release

**High (P1):**
- Major feature not working
- Significant user impact
- No workaround available
- Should fix before release

**Medium (P2):**
- Feature partially working
- Workaround available
- Minor user inconvenience
- Can ship with fix in next release

**Low (P3):**
- Cosmetic issues
- Rare edge cases
- Minimal impact
- Nice to have fixed

## Test Coverage Analysis

### Coverage Metrics

**Feature Coverage:**
```
Total Features: 25
Tested: 23
Not Tested: 2
Coverage: 92%
```

**Requirement Coverage:**
```
Total Requirements: 150
With Test Cases: 142
Without Test Cases: 8
Coverage: 95%
```

**Risk Coverage:**
```
High-Risk Areas: 12
Tested: 12
Medium-Risk: 35
Tested: 30
```

### Coverage Matrix

| Feature | Requirements | Test Cases | Status | Gaps |
|---------|--------------|------------|--------|------|
| Login | 8 | 12 | ✓ Complete | None |
| Checkout | 15 | 10 | ⚠ Partial | Payment errors |
| Dashboard | 12 | 15 | ✓ Complete | None |

## Regression Test Suite Structure

### Smoke Test Suite (15-30 min)
**Run:** Before every test cycle, daily builds

**Critical Paths:**
- User login/logout
- Core user flow (e.g., create order)
- Navigation and routing
- API health checks
- Database connectivity

**Example:**
```
SMOKE-001: Critical User Flow
1. Login as standard user
2. Navigate to main feature
3. Perform primary action
4. Verify success message
5. Logout
Expected: All steps complete without errors
```

### Full Regression Suite (2-4 hours)
**Run:** Weekly, before releases

**Coverage:**
- All functional test cases
- Integration scenarios
- UI validation
- Cross-browser checks
- Data integrity tests

### Targeted Regression (30-60 min)
**Run:** After bug fixes, feature updates

**Coverage:**
- Affected feature area
- Related components
- Integration points
- Previously failed tests

## Test Execution Tracking

### Test Run Template

```markdown
# Test Run: [Release Version]

**Date:** 2024-01-15
**Build:** v2.5.0-rc1
**Tester:** [Name]
**Environment:** Staging

## Summary
- Total Test Cases: 150
- Executed: 145
- Passed: 130
- Failed: 10
- Blocked: 5
- Not Run: 5
- Pass Rate: 90%

## Test Cases by Priority

| Priority | Total | Pass | Fail | Blocked |
|----------|-------|------|------|---------|
| P0 (Critical) | 25 | 23 | 2 | 0 |
| P1 (High) | 50 | 45 | 3 | 2 |
| P2 (Medium) | 50 | 45 | 3 | 2 |
| P3 (Low) | 25 | 17 | 2 | 1 |

## Failures

### Critical Failures
- TC-045: Payment processing fails
  - Bug: BUG-234
  - Status: Open

### High Priority Failures
- TC-089: Email notification not sent
  - Bug: BUG-235
  - Status: In Progress

## Blocked Tests
- TC-112: Dashboard widget (API endpoint down)
- TC-113: Export feature (dependency not deployed)

## Risks
- 2 critical bugs blocking release
- Payment integration needs attention
- Email service intermittent

## Next Steps
- Retest after BUG-234 fix
- Complete remaining 5 test cases
- Run full regression before sign-off
```

## Using This Skill

### Generate Test Plan

```bash
./scripts/generate_test_plan.sh
```

Interactive workflow for creating comprehensive test plans.

### Generate Manual Test Cases

```bash
./scripts/generate_test_cases.sh
```

Create manual test cases for features with step-by-step instructions.

### Build Regression Suite

```bash
./scripts/build_regression_suite.sh
```

Create smoke and regression test suites.

### Validate Design with Figma

**With Figma MCP configured:**
```
"Compare the login page implementation against the Figma design at [URL] and generate test cases for visual validation"
```

### Create Bug Report

```bash
./scripts/create_bug_report.sh
```

Generate structured bug reports with all required details.

### Access Templates

```
references/test_case_templates.md - Various test case formats
references/bug_report_templates.md - Bug documentation templates
references/regression_testing.md - Regression testing guide
references/figma_validation.md - Design validation with Figma MCP
```

## QA Process Workflow

### 1. Planning Phase
- [ ] Review requirements and designs
- [ ] Create test plan
- [ ] Identify test scenarios
- [ ] Estimate effort and timeline
- [ ] Set up test environment

### 2. Test Design Phase
- [ ] Write test cases
- [ ] Review test cases with team
- [ ] Prepare test data
- [ ] Build regression suite
- [ ] Get Figma design access

### 3. Test Execution Phase
- [ ] Execute test cases
- [ ] Log bugs with clear reproduction steps
- [ ] Validate against Figma designs (UI tests)
- [ ] Track test progress
- [ ] Communicate blockers

### 4. Reporting Phase
- [ ] Compile test results
- [ ] Analyze coverage
- [ ] Document risks
- [ ] Provide go/no-go recommendation
- [ ] Archive test artifacts

## Best Practices

### Test Case Writing

**DO:**
- ✅ Be specific and unambiguous
- ✅ Include expected results for each step
- ✅ Test one thing per test case
- ✅ Use consistent naming conventions
- ✅ Keep test cases maintainable

**DON'T:**
- ❌ Assume knowledge
- ❌ Make test cases too long
- ❌ Skip preconditions
- ❌ Forget edge cases
- ❌ Leave expected results vague

### Bug Reporting

**DO:**
- ✅ Provide clear reproduction steps
- ✅ Include screenshots/videos
- ✅ Specify exact environment details
- ✅ Describe impact on users
- ✅ Link to Figma for UI bugs

**DON'T:**
- ❌ Report without reproduction steps
- ❌ Use vague descriptions
- ❌ Skip environment details
- ❌ Forget to assign priority
- ❌ Duplicate existing bugs

### Regression Testing

**DO:**
- ✅ Automate repetitive tests when possible
- ✅ Maintain regression suite regularly
- ✅ Prioritize critical paths
- ✅ Run smoke tests frequently
- ✅ Update suite after each release

**DON'T:**
- ❌ Skip regression before releases
- ❌ Let suite become outdated
- ❌ Test everything every time
- ❌ Ignore failed regression tests

## Figma MCP Setup

### Configuration

**Install Figma MCP server:**
```bash
# Follow Figma MCP installation instructions
# Configure with your Figma API token
# Set file access permissions
```

**Usage in test planning:**
```
"Analyze the Figma design file at [URL] and generate visual validation test cases for:
- Color scheme compliance
- Typography specifications
- Component spacing
- Responsive breakpoints
- Interactive states"
```

**Example queries:**
```
"Get button specifications from Figma design [URL]"
"Compare navigation menu implementation against Figma design"
"Extract spacing values for dashboard layout from Figma"
"List all color tokens used in Figma design system"
```

## Test Case Examples

### Example 1: Login Flow

```markdown
## TC-LOGIN-001: Valid User Login

**Priority:** P0 (Critical)
**Type:** Functional
**Estimated Time:** 2 minutes

### Objective
Verify users can successfully login with valid credentials

### Preconditions
- User account exists (test@example.com / Test123!)
- User is not already logged in
- Browser cookies cleared

### Test Steps
1. Navigate to https://app.example.com/login
   **Expected:** Login page displays with email and password fields

2. Enter email: test@example.com
   **Expected:** Email field accepts input

3. Enter password: Test123!
   **Expected:** Password field shows masked characters

4. Click "Login" button
   **Expected:**
   - Loading indicator appears
   - User redirected to /dashboard
   - Welcome message shown: "Welcome back, Test User"
   - Avatar/profile image displayed in header

### Post-conditions
- User session created
- Auth token stored
- Analytics event logged

### Visual Validation (with Figma)
- Compare dashboard layout against Figma design [link]
- Verify welcome message typography: 24px, Medium, #1A1A1A
- Check avatar size: 40x40px, border-radius 50%

### Edge Cases to Consider
- TC-LOGIN-002: Invalid password
- TC-LOGIN-003: Non-existent email
- TC-LOGIN-004: SQL injection attempt
- TC-LOGIN-005: Very long password
```

### Example 2: Responsive Design Validation

```markdown
## TC-UI-045: Mobile Navigation Menu

**Priority:** P1 (High)
**Type:** UI/Responsive
**Devices:** Mobile (iPhone, Android)

### Objective
Verify navigation menu works correctly on mobile devices

### Preconditions
- Access from mobile device or responsive mode
- Viewport width: 375px (iPhone SE) to 428px (iPhone Pro Max)

### Test Steps
1. Open homepage on mobile device
   **Expected:** Hamburger menu icon visible (top-right)

2. Tap hamburger icon
   **Expected:**
   - Menu slides in from right
   - Overlay appears over content
   - Close (X) button visible

3. Tap menu item
   **Expected:** Navigate to section, menu closes

4. Compare against Figma mobile design [link]
   **Expected:**
   - Menu width: 280px
   - Slide animation: 300ms ease-out
   - Overlay opacity: 0.5, color #000000
   - Font size: 16px, line-height 24px

### Breakpoints to Test
- 375px (iPhone SE)
- 390px (iPhone 14)
- 428px (iPhone 14 Pro Max)
- 360px (Galaxy S21)
```

## Summary

This QA Test Planner skill provides:
- **Structured test planning** - Comprehensive test strategies
- **Manual test case generation** - Detailed, repeatable tests
- **Regression testing** - Protect against breaking changes
- **Figma validation** - Design-implementation verification
- **Bug documentation** - Clear, actionable reports
- **Coverage analysis** - Identify testing gaps

**Remember:** Quality is everyone's responsibility, but QA ensures it's systematically verified.

---

**"Testing shows the presence, not the absence of bugs." - Edsger Dijkstra**

**"Quality is not an act, it is a habit." - Aristotle**

---

# QA 测试规划器

专为 QA 工程师设计的综合技能，用于创建测试计划、生成手动测试用例、构建回归测试套件、根据 Figma 验证设计以及有效记录缺陷。

## 本技能功能

帮助 QA 工程师：
- **测试计划创建** - 全面的测试策略和规划
- **手动测试用例生成** - 详细的分步测试用例
- **回归测试套件** - 关键路径和冒烟测试套件
- **Figma 设计验证** - 比较实现与设计（需要 Figma MCP）
- **缺陷报告模板** - 清晰、可重现的缺陷文档
- **测试覆盖分析** - 识别测试中的漏洞
- **测试执行跟踪** - 监控测试进度

## 为什么需要此技能

**没有结构化测试：**
- 测试覆盖不一致
- 遗漏边缘情况
- 缺陷文档质量差
- 无回归安全网
- 设计实现差距
- 测试策略不明确

**使用此技能：**
- 全面的测试覆盖
- 可重复的测试用例
- 系统的回归测试
- 设计-实现验证
- 专业的缺陷报告
- 清晰的测试路线图

## 核心组件

### 1. 测试计划生成器
- 测试范围和目标
- 测试方法和策略
- 测试环境要求
- 进入/退出标准
- 风险评估
- 资源分配
- 时间线和里程碑

### 2. 手动测试用例生成器
- 分步说明
- 预期与实际结果
- 前置条件和设置
- 测试数据要求
- 优先级和严重性
- 边缘情况识别

### 3. 回归测试套件构建器
- 冒烟测试用例
- 关键路径测试
- 集成测试场景
- 向后兼容性检查
- 性能回归测试

### 4. Figma 设计验证（带 MCP）
- 将 UI 实现与设计进行比较
- 识别视觉差异
- 验证间距、颜色、排版
- 检查组件一致性
- 标记设计-开发不匹配

### 5. 缺陷报告生成器
- 清晰的重现步骤
- 环境详细信息
- 预期与实际行为
- 截图和证据
- 严重性和优先级
- 相关测试用例

## 测试用例结构

### 标准测试用例格式

```markdown
## TC-001: [Test Case Title]

**Priority:** High | Medium | Low
**Type:** Functional | UI | Integration | Regression
**Status:** Not Run | Pass | Fail | Blocked

### Objective
[What are we testing and why]

### Preconditions
- [Setup requirement 1]
- [Setup requirement 2]
- [Test data needed]

### Test Steps
1. [Action to perform]
   **Expected:** [What should happen]

2. [Action to perform]
   **Expected:** [What should happen]

3. [Action to perform]
   **Expected:** [What should happen]

### Test Data
- Input: [Test data values]
- User: [Test account details]
- Configuration: [Environment settings]

### Post-conditions
- [System state after test]
- [Cleanup required]

### Notes
- [Edge cases to consider]
- [Related test cases]
- [Known issues]
```

## 测试计划模板

### 执行摘要
- 正在测试的功能/产品
- 测试目标
- 关键风险
- 时间线概览

### 测试范围

**范围内：**
- 要测试的功能
- 测试类型（功能、UI、性能等）
- 平台和环境
- 用户流程和场景

**范围外：**
- 未测试的功能（延迟）
- 已知限制
- 第三方集成（如适用）

### 测试策略

**测试类型：**
- 手动测试
- 探索性测试
- 回归测试
- 集成测试
- 用户验收测试
- 性能测试（如适用）

**测试方法：**
- 黑盒测试
- 正向和负向测试
- 边界值分析
- 等价类划分

### 测试环境
- 操作系统
- 浏览器和版本
- 设备（移动、平板、桌面）
- 测试数据要求
- 后端/API 环境

### 进入标准
- [ ] 需求已文档化
- [ ] 设计已完成
- [ ] 测试环境就绪
- [ ] 测试数据已准备
- [ ] 构建已部署到测试环境

### 退出标准
- [ ] 所有高优先级测试用例已执行
- [ ] 90%+ 测试用例通过率
- [ ] 所有关键缺陷已修复
- [ ] 无开放的高严重性缺陷
- [ ] 回归套件通过
- [ ] 利益相关者签字

### 风险评估

| 风险 | 概率 | 影响 | 缓解措施 |
|------|------|------|----------|
| [风险 1] | 高/中/低 | 高/中/低 | [如何缓解] |
| [风险 2] | 高/中/低 | 高/中/低 | [如何缓解] |

### 测试交付物
- 测试计划文档
- 测试用例
- 测试执行报告
- 缺陷报告
- 测试摘要报告

## 测试类型和方法

### 1. 功能测试

**内容：** 验证功能按规定工作

**测试用例：**
- 正常路径场景
- 错误处理
- 输入验证
- 业务逻辑
- 数据完整性

**示例：**
```
TC: User Login with Valid Credentials
1. Navigate to login page
2. Enter valid email and password
3. Click "Login" button
Expected: User redirected to dashboard, welcome message shown
```

### 2. UI/视觉测试

**内容：** 验证视觉外观和布局

**测试用例：**
- 布局和对齐
- 响应式设计
- 颜色和排版
- 组件状态（悬停、激活、禁用）
- 跨浏览器兼容性

**使用 Figma MCP：**
- 将实现与 Figma 设计进行比较
- 验证间距（内边距、外边距）
- 检查字体大小和粗细
- 验证颜色值
- 确保图标准确性

**示例：**
```
TC: Homepage Hero Section Visual Validation
1. Open homepage in browser
2. Compare against Figma design [link]
3. Verify:
   - Heading font: 48px, bold, #1A1A1A
   - CTA button: 16px padding, #0066FF background
   - Image aspect ratio: 16:9
   - Spacing: 64px margin-bottom
Expected: All visual elements match Figma exactly
```

### 3. 回归测试

**内容：** 确保现有功能仍然有效

**何时运行：**
- 每次发布前
- 缺陷修复后
- 新功能后
- 每周冒烟测试

**套件组件：**
- 冒烟测试（关键路径）
- 完整回归（全面）
- 目标回归（受影响区域）

**示例：**
```
Regression Suite: User Authentication
- Login with valid credentials
- Login with invalid credentials
- Password reset flow
- Session timeout handling
- Multi-device login
- Social login (Google, GitHub)
```

### 4. 集成测试

**内容：** 验证不同组件一起工作

**测试用例：**
- API 集成
- 数据库操作
- 第三方服务
- 跨模块交互
- 组件间数据流

**示例：**
```
TC: Checkout Payment Integration
1. Add item to cart
2. Proceed to checkout
3. Enter payment details (Stripe)
4. Submit payment
Expected:
- Payment processed via Stripe API
- Order created in database
- Confirmation email sent
- Inventory updated
```

### 5. 探索性测试

**内容：** 无脚本、创造性测试

**方法：**
- 基于章程的探索
- 用户角色模拟
- 边缘情况发现
- 可用性评估

**会话模板：**
```
Exploratory Testing Session
Charter: Explore [feature] as [user type]
Time: 60 minutes
Focus: [Area to explore]

Findings:
- [Bug/issue discovered]
- [UX concern]
- [Improvement suggestion]

Follow-up:
- [Test cases to create]
- [Bugs to file]
```

## Figma MCP 集成

### 设计验证工作流程

**先决条件：**
- Figma MCP 服务器已配置
- 设计文件访问权限
- Figma URL 可用

**验证过程：**

1. **从 Figma 获取设计规格**
```
"Get the button specifications from Figma file [URL]"
- Component: Primary Button
- Width: 120px
- Height: 40px
- Border-radius: 8px
- Background: #0066FF
- Font: 16px, Medium, #FFFFFF
```

2. **比较实现**
```
TC: Primary Button Visual Validation
1. Inspect primary button in browser dev tools
2. Compare against Figma specs:
   - Dimensions: 120x40px ✓ / ✗
   - Border-radius: 8px ✓ / ✗
   - Background color: #0066FF ✓ / ✗
   - Font: 16px Medium #FFFFFF ✓ / ✗
3. Document discrepancies
```

3. **如不匹配则创建缺陷**
```
BUG: Primary button color doesn't match design
Severity: Medium
Expected (Figma): #0066FF
Actual (Implementation): #0052CC
Screenshot: [attached]
Figma link: [specific component]
```

### 设计-开发交接清单

**使用 Figma MCP：**
- [ ] 从设计中获取间距值
- [ ] 验证调色板匹配
- [ ] 检查排版规格
- [ ] 验证组件状态（悬停、激活、禁用）
- [ ] 确认断点行为
- [ ] 审查图标和资产
- [ ] 检查可访问性注释

## 缺陷报告最佳实践

### 有效的缺陷报告模板

```markdown
# BUG-[ID]: [Clear, specific title]

**Severity:** Critical | High | Medium | Low
**Priority:** P0 | P1 | P2 | P3
**Type:** Functional | UI | Performance | Security
**Status:** Open | In Progress | Fixed | Closed

## Environment
- **OS:** [Windows 11, macOS 14, etc.]
- **Browser:** [Chrome 120, Firefox 121, etc.]
- **Device:** [Desktop, iPhone 15, etc.]
- **Build:** [Version/commit]
- **URL:** [Page where bug occurs]

## Description
[Clear, concise description of the issue]

## Steps to Reproduce
1. [Specific step]
2. [Specific step]
3. [Specific step]

## Expected Behavior
[What should happen]

## Actual Behavior
[What actually happens]

## Visual Evidence
- Screenshot: [attached]
- Video: [link if applicable]
- Console errors: [paste errors]
- Network logs: [if relevant]

## Impact
- **User Impact:** [How many users affected]
- **Frequency:** [Always, Sometimes, Rarely]
- **Workaround:** [If one exists]

## Additional Context
- Related to: [Feature/ticket]
- First noticed: [When]
- Regression: [Yes/No - if yes, since when]
- Figma design: [Link if UI bug]

## Test Cases Affected
- TC-001: [Test case that failed]
- TC-045: [Related test case]
```

### 缺陷严重性定义

**关键 (P0)：**
- 系统崩溃或数据丢失
- 安全漏洞
- 功能完全失效
- 阻止发布

**高 (P1)：**
- 主要功能不工作
- 重大用户影响
- 无可用解决方法
- 应在发布前修复

**中 (P2)：**
- 功能部分工作
- 有可用解决方法
- 轻微用户不便
- 可随下一版本修复一起发布

**低 (P3)：**
- 外观问题
- 罕见边缘情况
- 最小影响
- 修复更好

## 测试覆盖分析

### 覆盖指标

**功能覆盖：**
```
Total Features: 25
Tested: 23
Not Tested: 2
Coverage: 92%
```

**需求覆盖：**
```
Total Requirements: 150
With Test Cases: 142
Without Test Cases: 8
Coverage: 95%
```

**风险覆盖：**
```
High-Risk Areas: 12
Tested: 12
Medium-Risk: 35
Tested: 30
```

### 覆盖矩阵

| 功能 | 需求 | 测试用例 | 状态 | 漏洞 |
|------|------|----------|------|------|
| 登录 | 8 | 12 | ✓ 完整 | 无 |
| 结账 | 15 | 10 | ⚠ 部分 | 支付错误 |
| 仪表板 | 12 | 15 | ✓ 完整 | 无 |

## 回归测试套件结构

### 冒烟测试套件（15-30 分钟）
**运行：** 每个测试周期前，每日构建

**关键路径：**
- 用户登录/注销
- 核心用户流程（例如，创建订单）
- 导航和路由
- API 健康检查
- 数据库连接

**示例：**
```
SMOKE-001: Critical User Flow
1. Login as standard user
2. Navigate to main feature
3. Perform primary action
4. Verify success message
5. Logout
Expected: All steps complete without errors
```

### 完整回归套件（2-4 小时）
**运行：** 每周，发布前

**覆盖：**
- 所有功能测试用例
- 集成场景
- UI 验证
- 跨浏览器检查
- 数据完整性测试

### 目标回归（30-60 分钟）
**运行：** 缺陷修复后，功能更新后

**覆盖：**
- 受影响的功能区域
- 相关组件
- 集成点
- 以前失败的测试

## 测试执行跟踪

### 测试运行模板

```markdown
# Test Run: [Release Version]

**Date:** 2024-01-15
**Build:** v2.5.0-rc1
**Tester:** [Name]
**Environment:** Staging

## Summary
- Total Test Cases: 150
- Executed: 145
- Passed: 130
- Failed: 10
- Blocked: 5
- Not Run: 5
- Pass Rate: 90%

## Test Cases by Priority

| Priority | Total | Pass | Fail | Blocked |
|----------|-------|------|------|---------|
| P0 (Critical) | 25 | 23 | 2 | 0 |
| P1 (High) | 50 | 45 | 3 | 2 |
| P2 (Medium) | 50 | 45 | 3 | 2 |
| P3 (Low) | 25 | 17 | 2 | 1 |

## Failures

### Critical Failures
- TC-045: Payment processing fails
  - Bug: BUG-234
  - Status: Open

### High Priority Failures
- TC-089: Email notification not sent
  - Bug: BUG-235
  - Status: In Progress

## Blocked Tests
- TC-112: Dashboard widget (API endpoint down)
- TC-113: Export feature (dependency not deployed)

## Risks
- 2 critical bugs blocking release
- Payment integration needs attention
- Email service intermittent

## Next Steps
- Retest after BUG-234 fix
- Complete remaining 5 test cases
- Run full regression before sign-off
```

## 使用此技能

### 生成测试计划

```bash
./scripts/generate_test_plan.sh
```

创建综合测试计划的交互式工作流。

### 生成手动测试用例

```bash
./scripts/generate_test_cases.sh
```

为功能创建带有分步说明的手动测试用例。

### 构建回归套件

```bash
./scripts/build_regression_suite.sh
```

创建冒烟和回归测试套件。

### 使用 Figma 验证设计

**配置 Figma MCP 后：**
```
"Compare the login page implementation against the Figma design at [URL] and generate test cases for visual validation"
```

### 创建缺陷报告

```bash
./scripts/create_bug_report.sh
```

生成包含所有必要详细信息的结构化缺陷报告。

### 访问模板

```
references/test_case_templates.md - 各种测试用例格式
references/bug_report_templates.md - 缺陷文档模板
references/regression_testing.md - 回归测试指南
references/figma_validation.md - 使用 Figma MCP 进行设计验证
```

## QA 流程工作流

### 1. 规划阶段
- [ ] 审查需求和设计
- [ ] 创建测试计划
- [ ] 识别测试场景
- [ ] 估计工作量和时间线
- [ ] 设置测试环境

### 2. 测试设计阶段
- [ ] 编写测试用例
- [ ] 与团队审查测试用例
- [ ] 准备测试数据
- [ ] 构建回归套件
- [ ] 获取 Figma 设计访问权限

### 3. 测试执行阶段
- [ ] 执行测试用例
- [ ] 记录带有清晰重现步骤的缺陷
- [ ] 根据 Figma 设计验证（UI 测试）
- [ ] 跟踪测试进度
- [ ] 沟通阻塞项

### 4. 报告阶段
- [ ] 编译测试结果
- [ ] 分析覆盖
- [ ] 记录风险
- [ ] 提供通过/不通过建议
- [ ] 存档测试工件

## 最佳实践

### 测试用例编写

**建议：**
- ✅ 具体明确
- ✅ 为每个步骤包含预期结果
- ✅ 每个测试用例测试一件事
- ✅ 使用一致的命名约定
- ✅ 保持测试用例可维护

**避免：**
- ❌ 假设知识
- ❌ 使测试用例过长
- ❌ 跳过前置条件
- ❌ 忘记边缘情况
- ❌ 留下模糊的预期结果

### 缺陷报告

**建议：**
- ✅ 提供清晰的重现步骤
- ✅ 包含截图/视频
- ✅ 指定确切的环境详细信息
- ✅ 描述对用户的影响
- ✅ 为 UI 缺陷链接到 Figma

**避免：**
- ❌ 无重现步骤报告
- ❌ 使用模糊描述
- ❌ 跳过环境详细信息
- ❌ 忘记分配优先级
- ❌ 重复现有缺陷

### 回归测试

**建议：**
- ✅ 尽可能自动化重复测试
- ✅ 定期维护回归套件
- ✅ 优先考虑关键路径
- ✅ 频繁运行冒烟测试
- ✅ 每次发布后更新套件

**避免：**
- ❌ 发布前跳过回归
- ❌ 让套件过时
- ❌ 每次测试所有内容
- ❌ 忽略失败的回归测试

## Figma MCP 设置

### 配置

**安装 Figma MCP 服务器：**
```bash
# 按照 Figma MCP 安装说明
# 使用您的 Figma API 令牌配置
# 设置文件访问权限
```

**在测试规划中使用：**
```
"Analyze the Figma design file at [URL] and generate visual validation test cases for:
- Color scheme compliance
- Typography specifications
- Component spacing
- Responsive breakpoints
- Interactive states"
```

**示例查询：**
```
"Get button specifications from Figma design [URL]"
"Compare navigation menu implementation against Figma design"
"Extract spacing values for dashboard layout from Figma"
"List all color tokens used in Figma design system"
```

## 测试用例示例

### 示例 1：登录流程

```markdown
## TC-LOGIN-001: Valid User Login

**Priority:** P0 (Critical)
**Type:** Functional
**Estimated Time:** 2 minutes

### Objective
Verify users can successfully login with valid credentials

### Preconditions
- User account exists (test@example.com / Test123!)
- User is not already logged in
- Browser cookies cleared

### Test Steps
1. Navigate to https://app.example.com/login
   **Expected:** Login page displays with email and password fields

2. Enter email: test@example.com
   **Expected:** Email field accepts input

3. Enter password: Test123!
   **Expected:** Password field shows masked characters

4. Click "Login" button
   **Expected:**
   - Loading indicator appears
   - User redirected to /dashboard
   - Welcome message shown: "Welcome back, Test User"
   - Avatar/profile image displayed in header

### Post-conditions
- User session created
- Auth token stored
- Analytics event logged

### Visual Validation (with Figma)
- Compare dashboard layout against Figma design [link]
- Verify welcome message typography: 24px, Medium, #1A1A1A
- Check avatar size: 40x40px, border-radius 50%

### Edge Cases to Consider
- TC-LOGIN-002: Invalid password
- TC-LOGIN-003: Non-existent email
- TC-LOGIN-004: SQL injection attempt
- TC-LOGIN-005: Very long password
```

### 示例 2：响应式设计验证

```markdown
## TC-UI-045: Mobile Navigation Menu

**Priority:** P1 (High)
**Type:** UI/Responsive
**Devices:** Mobile (iPhone, Android)

### Objective
Verify navigation menu works correctly on mobile devices

### Preconditions
- Access from mobile device or responsive mode
- Viewport width: 375px (iPhone SE) to 428px (iPhone Pro Max)

### Test Steps
1. Open homepage on mobile device
   **Expected:** Hamburger menu icon visible (top-right)

2. Tap hamburger icon
   **Expected:**
   - Menu slides in from right
   - Overlay appears over content
   - Close (X) button visible

3. Tap menu item
   **Expected:** Navigate to section, menu closes

4. Compare against Figma mobile design [link]
   **Expected:**
   - Menu width: 280px
   - Slide animation: 300ms ease-out
   - Overlay opacity: 0.5, color #000000
   - Font size: 16px, line-height 24px

### Breakpoints to Test
- 375px (iPhone SE)
- 390px (iPhone 14)
- 428px (iPhone 14 Pro Max)
- 360px (Galaxy S21)
```

## 摘要

此 QA 测试规划器技能提供：
- **结构化测试规划** - 全面的测试策略
- **手动测试用例生成** - 详细、可重复的测试
- **回归测试** - 防止破坏性变更
- **Figma 验证** - 设计-实现验证
- **缺陷文档** - 清晰、可操作的报告
- **覆盖分析** - 识别测试漏洞

**记住：** 质量是每个人的责任，但 QA 确保它得到系统验证。

---

**"测试显示缺陷的存在，而非不存在。" - Edsger Dijkstra**

**"质量不是行为，而是习惯。" - Aristotle**
