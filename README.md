
# step by step 一步一步创建
## skills 初始化过程
```
npx skills init
npx skills update
```
## Installation

```bash
npx skills add linlannet/agent-skills.git

```

Or via Agent Skills:

```bash
npx agent-skills-cli install linlannet/agent-skills
```

## Structure 目录结构

该插件遵循标准的Claude Code插件架构：
```
agent-skills/
├── 📁 .claude-plugin/
│   ├── plugin.json
│   └── marketplace.json
├── 📁 agents/              # 8 agents 智能体
│   ├── 01-java-fundamentals/
│   ├── 02-java-advanced/
│   ├── 03-java-spring/
│   ├── 04-java-testing/
│   ├── 05-java-build-tools/
│   ├── 06-java-persistence/
│   ├── 07-java-microservices/
│   ├── 08-java-devops/
├── 📁 skills/              # 20+ skills 能力体
│   ├── anthropic-architect/
│   ├── anthropic-prompt-engineer/
│   ├── java-docker/
│   ├── java-fundamentals/
│   ├── java-gradle/
│   ├── java-jpa-hibernate/
│   ├── java-maven/
│   ├── java-microservices/
│   ├── java-persistence/
│   ├── java-spring-boot/
│   ├── java-testing/
│   ├── java-testing-advance/
│   ├── prd-generator/
│   ├── technical-launch-planner/
│   ├── design-brief-generator/
│   ├── frontend-designer/
│   ├── code-review-expert/
│   ├── query-expert/
│   ├── qa-test-planner/
├── 📁 commands/            # 4 commands 命令
│   ├── java-build/
│   ├── java-new/
│   ├── java-check/
│   ├── java-debug/
├── 📁 packages/            # 包目录
├── 📄 README.md
├── 📄 CHANGELOG.md
└── 📄 LICENSE
```

## 🤖 Agents 智能体

### 8 Production-Grade Agents 8个生产级智能体

| # | Agent | Purpose | Primary Skill |
|---|-------|---------|---------------|
| 1 | **01-java-fundamentals** | Java语法、面向对象编程、集合、流 | `java-fundamentals` |
| 2 | **02-java-advanced** | 并发、JVM内部、性能 | `java-concurrency` |
| 3 | **03-java-spring** | Spring Boot、MVC、安全、云 | `java-spring-boot` |
| 4 | **04-java-testing** | JUnit 5、Mockito、集成测试 | `java-testing` |
| 5 | **05-java-build-tools** | Maven、Gradle、CI/CD管道 | `java-maven-gradle` |
| 6 | **06-java-persistence** | JPA、Hibernate、查询优化 | `java-jpa-hibernate` |
| 7 | **07-java-microservices** | Spring Cloud、分布式系统 | `java-microservices` |
| 8 | **08-java-devops** | Docker、Kubernetes、监控 | `java-docker` |

---

## 🛠️ Skills 技能

### 12 SASMP-Compliant Skills 12个符合SASMP标准的技能

| Skill | Description | Bond Type |
|-------|-------------|-----------|
| `java-fundamentals` | 核心Java语法、面向对象编程、集合、流 | PRIMARY |
| `java-spring-boot` | Spring Boot REST API、安全、数据、执行器 | PRIMARY |
| `java-testing` | JUnit 5、Mockito、集成测试、TDD | PRIMARY |
| `java-jpa-hibernate` | 实体设计、查询、事务、缓存 | PRIMARY |
| `java-microservices` | Spring Cloud、服务网格、事件驱动模式 | PRIMARY |
| `java-docker` | Dockerfile优化、JVM设置、安全 | PRIMARY |
| `java-maven` | Maven POM、生命周期、插件 | SECONDARY |
| `java-gradle` | Gradle Kotlin DSL、构建优化 | SECONDARY |
| `java-performance` | JVM调优、GC、分析、基准测试 | SECONDARY |
| `java-testing-advanced` | Testcontainers、契约测试、突变测试 | SECONDARY |
| `anthropic-architect` | 为您的项目确定最佳的Anthropic架构 | PRIMARY |
| `anthropic-prompt-engineer` | 掌握Anthropic的提示工程技术 | PRIMARY |
| `prd-generator` | 生成产品需求文档 | PRIMARY |
| `technical-launch-planner` | 规划技术产品发布 | PRIMARY |
| `design-brief-generator` | 生成全面的设计简报 | PRIMARY |
| `frontend-designer` | 构建可访问、响应式的用户界面 | PRIMARY |
| `code-review-expert` | 代码审查专家 | PRIMARY |
| `query-expert` | 掌握SQL和数据库查询 | PRIMARY |
| `qa-test-planner` | 生成测试计划和错误报告 | PRIMARY |

---

## ⌨️ Commands 命令

| Command | Description |
|---------|-------------|
| `/java-build` | 使用Maven或Gradle构建Java项目 |
| `/java-new` | 使用Maven或Gradle创建新的Java项目 |
| `/java-check` | 检查Java和构建工具的安装和配置 |
| `/java-debug` | 调试Java应用程序并排查常见问题 |

---

