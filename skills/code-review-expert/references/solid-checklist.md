# SOLID Smell Prompts

## SRP (Single Responsibility)

- File owns unrelated concerns (e.g., HTTP + DB + domain rules in one file)
- Large class/module with low cohesion or multiple reasons to change
- Functions that orchestrate many unrelated steps
- God objects that know too much about the system
- **Ask**: "What is the single reason this module would change?"

## OCP (Open/Closed)

- Adding a new behavior requires editing many switch/if blocks
- Feature growth requires modifying core logic rather than extending
- No plugin/strategy/hook points for variation
- **Ask**: "Can I add a new variant without touching existing code?"

## LSP (Liskov Substitution)

- Subclass checks for concrete type or throws for base method
- Overridden methods weaken preconditions or strengthen postconditions
- Subclass ignores or no-ops parent behavior
- **Ask**: "Can I substitute any subclass without the caller knowing?"

## ISP (Interface Segregation)

- Interfaces with many methods, most unused by implementers
- Callers depend on broad interfaces for narrow needs
- Empty/stub implementations of interface methods
- **Ask**: "Do all implementers use all methods?"

## DIP (Dependency Inversion)

- High-level logic depends on concrete IO, storage, or network types
- Hard-coded implementations instead of abstractions or injection
- Import chains that couple business logic to infrastructure
- **Ask**: "Can I swap the implementation without changing business logic?"

---

## Common Code Smells (Beyond SOLID)

| Smell | Signs |
|-------|-------|
| **Long method** | Function > 30 lines, multiple levels of nesting |
| **Feature envy** | Method uses more data from another class than its own |
| **Data clumps** | Same group of parameters passed together repeatedly |
| **Primitive obsession** | Using strings/numbers instead of domain types |
| **Shotgun surgery** | One change requires edits across many files |
| **Divergent change** | One file changes for many unrelated reasons |
| **Dead code** | Unreachable or never-called code |
| **Speculative generality** | Abstractions for hypothetical future needs |
| **Magic numbers/strings** | Hardcoded values without named constants |

---

## Refactor Heuristics

1. **Split by responsibility, not by size** - A small file can still violate SRP
2. **Introduce abstraction only when needed** - Wait for the second use case
3. **Keep refactors incremental** - Isolate behavior before moving
4. **Preserve behavior first** - Add tests before restructuring
5. **Name things by intent** - If naming is hard, the abstraction might be wrong
6. **Prefer composition over inheritance** - Inheritance creates tight coupling
7. **Make illegal states unrepresentable** - Use types to enforce invariants

---

# SOLID 异味提示

## SRP (单一职责原则)

- 文件包含不相关的关注点（例如，一个文件中包含 HTTP + 数据库 + 领域规则）
- 大型类/模块，内聚性低或有多个变更原因
- 编排许多不相关步骤的函数
- 了解系统过多的上帝对象
- **询问**："这个模块变更的唯一原因是什么？"

## OCP (开放/封闭原则)

- 添加新行为需要编辑多个 switch/if 块
- 功能增长需要修改核心逻辑而不是扩展
- 没有用于变体的插件/策略/钩子点
- **询问**："我可以在不触及现有代码的情况下添加新变体吗？"

## LSP (里氏替换原则)

- 子类检查具体类型或对基类方法抛出异常
- 重写的方法弱化前置条件或强化后置条件
- 子类忽略或不执行父类行为
- **询问**："我可以替换任何子类而调用者不知道吗？"

## ISP (接口隔离原则)

- 接口有许多方法，大多数实现者都未使用
- 调用者为了狭窄的需求而依赖广泛的接口
- 接口方法的空/存根实现
- **询问**："所有实现者都使用所有方法吗？"

## DIP (依赖倒置原则)

- 高层逻辑依赖于具体的 IO、存储或网络类型
- 硬编码实现而不是抽象或注入
- 将业务逻辑与基础设施耦合的导入链
- **询问**："我可以在不更改业务逻辑的情况下交换实现吗？"

---

## 常见代码异味（超越 SOLID）

| 异味 | 迹象 |
|------|------|
| **长方法** | 函数 > 30 行，多层嵌套 |
| **特性嫉妒** | 方法使用其他类的数据多于自己类的数据 |
| **数据块** | 同一组参数重复传递 |
| **原始类型痴迷** | 使用字符串/数字而不是领域类型 |
| **霰弹式修改** | 一个变更需要编辑多个文件 |
| **发散变更** | 一个文件因许多不相关原因而变更 |
| **死代码** | 不可达或从未调用的代码 |
| **过度抽象** | 为假设的未来需求而抽象 |
| **魔术数字/字符串** | 没有命名常量的硬编码值 |

---

## 重构启发式方法

1. **按职责拆分，而不是按大小** - 小文件仍然可能违反 SRP
2. **仅在需要时引入抽象** - 等待第二个用例
3. **保持重构增量** - 在移动前隔离行为
4. **首先保持行为** - 在重构前添加测试
5. **按意图命名** - 如果命名困难，抽象可能有问题
6. **优先组合而非继承** - 继承会创建紧密耦合
7. **使非法状态不可表示** - 使用类型强制执行不变量