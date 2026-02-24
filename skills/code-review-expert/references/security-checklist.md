# Security and Reliability Checklist

## Input/Output Safety

- **XSS**: Unsafe HTML injection, `dangerouslySetInnerHTML`, unescaped templates, innerHTML assignments
- **Injection**: SQL/NoSQL/command/GraphQL injection via string concatenation or template literals
- **SSRF**: User-controlled URLs reaching internal services without allowlist validation
- **Path traversal**: User input in file paths without sanitization (`../` attacks)
- **Prototype pollution**: Unsafe object merging in JavaScript (`Object.assign`, spread with user input)

## AuthN/AuthZ

- Missing tenant or ownership checks for read/write operations
- New endpoints without auth guards or RBAC enforcement
- Trusting client-provided roles/flags/IDs
- Broken access control (IDOR - Insecure Direct Object Reference)
- Session fixation or weak session management

## JWT & Token Security

- Algorithm confusion attacks (accepting `none` or `HS256` when expecting `RS256`)
- Weak or hardcoded secrets
- Missing expiration (`exp`) or not validating it
- Sensitive data in JWT payload (tokens are base64, not encrypted)
- Not validating `iss` (issuer) or `aud` (audience)

## Secrets and PII

- API keys, tokens, or credentials in code/config/logs
- Secrets in git history or environment variables exposed to client
- Excessive logging of PII or sensitive payloads
- Missing data masking in error messages

## Supply Chain & Dependencies

- Unpinned dependencies allowing malicious updates
- Dependency confusion (private package name collision)
- Importing from untrusted sources or CDNs without integrity checks
- Outdated dependencies with known CVEs

## CORS & Headers

- Overly permissive CORS (`Access-Control-Allow-Origin: *` with credentials)
- Missing security headers (CSP, X-Frame-Options, X-Content-Type-Options)
- Exposed internal headers or stack traces

## Runtime Risks

- Unbounded loops, recursive calls, or large in-memory buffers
- Missing timeouts, retries, or rate limiting on external calls
- Blocking operations on request path (sync I/O in async context)
- Resource exhaustion (file handles, connections, memory)
- ReDoS (Regular Expression Denial of Service)

## Cryptography

- Weak algorithms (MD5, SHA1 for security purposes)
- Hardcoded IVs or salts
- Using encryption without authentication (ECB mode, no HMAC)
- Insufficient key length

## Race Conditions

Race conditions are subtle bugs that cause intermittent failures and security vulnerabilities. Pay special attention to:

### Shared State Access
- Multiple threads/goroutines/async tasks accessing shared variables without synchronization
- Global state or singletons modified concurrently
- Lazy initialization without proper locking (double-checked locking issues)
- Non-thread-safe collections used in concurrent context

### Check-Then-Act (TOCTOU)
- `if (exists) then use` patterns without atomic operations
- `if (authorized) then perform` where authorization can change
- File existence check followed by file operation
- Balance check followed by deduction (financial operations)
- Inventory check followed by order placement

### Database Concurrency
- Missing optimistic locking (`version` column, `updated_at` checks)
- Missing pessimistic locking (`SELECT FOR UPDATE`)
- Read-modify-write without transaction isolation
- Counter increments without atomic operations (`UPDATE SET count = count + 1`)
- Unique constraint violations in concurrent inserts

### Distributed Systems
- Missing distributed locks for shared resources
- Leader election race conditions
- Cache invalidation races (stale reads after writes)
- Event ordering dependencies without proper sequencing
- Split-brain scenarios in cluster operations

### Common Patterns to Flag
```
# Dangerous patterns:
if not exists(key):       # TOCTOU
    create(key)

value = get(key)          # Read-modify-write
value += 1
set(key, value)

if user.balance >= amount:  # Check-then-act
    user.balance -= amount
```

### Questions to Ask
- "What happens if two requests hit this code simultaneously?"
- "Is this operation atomic or can it be interrupted?"
- "What shared state does this code access?"
- "How does this behave under high concurrency?"

## Data Integrity

- Missing transactions, partial writes, or inconsistent state updates
- Weak validation before persistence (type coercion issues)
- Missing idempotency for retryable operations
- Lost updates due to concurrent modifications

---

# 安全与可靠性检查清单

## 输入/输出安全

- **XSS**：不安全的HTML注入，`dangerouslySetInnerHTML`，未转义的模板，innerHTML赋值
- **注入**：通过字符串拼接或模板字面量进行SQL/NoSQL/命令/GraphQL注入
- **SSRF**：用户控制的URL在没有白名单验证的情况下访问内部服务
- **路径遍历**：文件路径中的用户输入未经过 sanitization（`../` 攻击）
- **原型污染**：JavaScript中不安全的对象合并（`Object.assign`，使用用户输入的展开操作）

## 认证/授权

- 读取/写入操作缺少租户或所有权检查
- 新端点没有认证守卫或RBAC强制执行
- 信任客户端提供的角色/标志/ID
- 损坏的访问控制（IDOR - 不安全的直接对象引用）
- 会话固定或弱会话管理

## JWT 和令牌安全

- 算法混淆攻击（期望 `RS256` 时接受 `none` 或 `HS256`）
- 弱或硬编码的密钥
- 缺少过期时间（`exp`）或未验证
- JWT 载荷中的敏感数据（令牌是 base64，未加密）
- 未验证 `iss`（发行者）或 `aud`（受众）

## 密钥和个人身份信息

- 代码/配置/日志中的API密钥、令牌或凭证
- Git历史或环境变量中的密钥暴露给客户端
- 过度记录个人身份信息或敏感载荷
- 错误消息中缺少数据掩码

## 供应链和依赖

- 未固定版本的依赖允许恶意更新
- 依赖混淆（私有包名冲突）
- 从未受信任的源或CDN导入，没有完整性检查
- 具有已知CVE的过时依赖

## CORS 和头部

- 过于宽松的CORS（带凭证的 `Access-Control-Allow-Origin: *`）
- 缺少安全头部（CSP，X-Frame-Options，X-Content-Type-Options）
- 暴露的内部头部或堆栈跟踪

## 运行时风险

- 无界循环、递归调用或大型内存缓冲区
- 外部调用缺少超时、重试或速率限制
- 请求路径上的阻塞操作（异步上下文中的同步I/O）
- 资源耗尽（文件句柄、连接、内存）
- ReDoS（正则表达式拒绝服务）

## 密码学

- 弱算法（用于安全目的的MD5，SHA1）
- 硬编码的IV或盐
- 使用没有认证的加密（ECB模式，无HMAC）
- 密钥长度不足

## 竞态条件

竞态条件是导致间歇性故障和安全漏洞的微妙错误。特别注意：

### 共享状态访问
- 多个线程/协程/异步任务在没有同步的情况下访问共享变量
- 并发修改的全局状态或单例
- 没有适当锁定的延迟初始化（双重检查锁定问题）
- 在并发上下文中使用非线程安全的集合

### 检查后行动（TOCTOU）
- 没有原子操作的 `if (exists) then use` 模式
- 授权可能更改的 `if (authorized) then perform`
- 文件存在检查后进行文件操作
- 余额检查后进行扣除（财务操作）
- 库存检查后进行订单放置

### 数据库并发
- 缺少乐观锁定（`version` 列，`updated_at` 检查）
- 缺少悲观锁定（`SELECT FOR UPDATE`）
- 没有事务隔离的读取-修改-写入
- 没有原子操作的计数器递增（`UPDATE SET count = count + 1`）
- 并发插入中的唯一约束冲突

### 分布式系统
- 共享资源缺少分布式锁
- 领导者选举竞态条件
- 缓存失效竞态（写入后的陈旧读取）
- 没有适当排序的事件顺序依赖
- 集群操作中的脑裂场景

### 常见危险模式
```
# 危险模式：
if not exists(key):       # TOCTOU
    create(key)

value = get(key)          # 读取-修改-写入
value += 1
set(key, value)

if user.balance >= amount:  # 检查后行动
    user.balance -= amount
```

### 要问的问题
- "如果两个请求同时访问这段代码会发生什么？"
- "这个操作是原子的还是可以被中断？"
- "这段代码访问什么共享状态？"
- "在高并发下这会如何表现？"

## 数据完整性

- 缺少事务、部分写入或不一致的状态更新
- 持久化前验证薄弱（类型强制问题）
- 可重试操作缺少幂等性
- 由于并发修改导致的更新丢失