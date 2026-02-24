# Code Quality Checklist

## Error Handling

### Anti-patterns to Flag

- **Swallowed exceptions**: Empty catch blocks or catch with only logging
  ```javascript
  try { ... } catch (e) { }  // Silent failure
  try { ... } catch (e) { console.log(e) }  // Log and forget
  ```
- **Overly broad catch**: Catching `Exception`/`Error` base class instead of specific types
- **Error information leakage**: Stack traces or internal details exposed to users
- **Missing error handling**: No try-catch around fallible operations (I/O, network, parsing)
- **Async error handling**: Unhandled promise rejections, missing `.catch()`, no error boundary

### Best Practices to Check

- [ ] Errors are caught at appropriate boundaries
- [ ] Error messages are user-friendly (no internal details exposed)
- [ ] Errors are logged with sufficient context for debugging
- [ ] Async errors are properly propagated or handled
- [ ] Fallback behavior is defined for recoverable errors
- [ ] Critical errors trigger alerts/monitoring

### Questions to Ask
- "What happens when this operation fails?"
- "Will the caller know something went wrong?"
- "Is there enough context to debug this error?"

---

## Performance & Caching

### CPU-Intensive Operations

- **Expensive operations in hot paths**: Regex compilation, JSON parsing, crypto in loops
- **Blocking main thread**: Sync I/O, heavy computation without worker/async
- **Unnecessary recomputation**: Same calculation done multiple times
- **Missing memoization**: Pure functions called repeatedly with same inputs

### Database & I/O

- **N+1 queries**: Loop that makes a query per item instead of batch
  ```javascript
  // Bad: N+1
  for (const id of ids) {
    const user = await db.query(`SELECT * FROM users WHERE id = ?`, id)
  }
  // Good: Batch
  const users = await db.query(`SELECT * FROM users WHERE id IN (?)`, ids)
  ```
- **Missing indexes**: Queries on unindexed columns
- **Over-fetching**: SELECT * when only few columns needed
- **No pagination**: Loading entire dataset into memory

### Caching Issues

- **Missing cache for expensive operations**: Repeated API calls, DB queries, computations
- **Cache without TTL**: Stale data served indefinitely
- **Cache without invalidation strategy**: Data updated but cache not cleared
- **Cache key collisions**: Insufficient key uniqueness
- **Caching user-specific data globally**: Security/privacy issue

### Memory

- **Unbounded collections**: Arrays/maps that grow without limit
- **Large object retention**: Holding references preventing GC
- **String concatenation in loops**: Use StringBuilder/join instead
- **Loading large files entirely**: Use streaming instead

### Questions to Ask
- "What's the time complexity of this operation?"
- "How does this behave with 10x/100x data?"
- "Is this result cacheable? Should it be?"
- "Can this be batched instead of one-by-one?"

---

## Boundary Conditions

### Null/Undefined Handling

- **Missing null checks**: Accessing properties on potentially null objects
- **Truthy/falsy confusion**: `if (value)` when `0` or `""` are valid
- **Optional chaining overuse**: `a?.b?.c?.d` hiding structural issues
- **Null vs undefined inconsistency**: Mixed usage without clear convention

### Empty Collections

- **Empty array not handled**: Code assumes array has items
- **Empty object edge case**: `for...in` or `Object.keys` on empty object
- **First/last element access**: `arr[0]` or `arr[arr.length-1]` without length check

### Numeric Boundaries

- **Division by zero**: Missing check before division
- **Integer overflow**: Large numbers exceeding safe integer range
- **Floating point comparison**: Using `===` instead of epsilon comparison
- **Negative values**: Index or count that shouldn't be negative
- **Off-by-one errors**: Loop bounds, array slicing, pagination

### String Boundaries

- **Empty string**: Not handled as edge case
- **Whitespace-only string**: Passes truthy check but is effectively empty
- **Very long strings**: No length limits causing memory/display issues
- **Unicode edge cases**: Emoji, RTL text, combining characters

### Common Patterns to Flag

```javascript
// Dangerous: no null check
const name = user.profile.name

// Dangerous: array access without check
const first = items[0]

// Dangerous: division without check
const avg = total / count

// Dangerous: truthy check excludes valid values
if (value) { ... }  // fails for 0, "", false
```

### Questions to Ask
- "What if this is null/undefined?"
- "What if this collection is empty?"
- "What's the valid range for this number?"
- "What happens at the boundaries (0, -1, MAX_INT)?"

---

# 代码质量检查清单

## 错误处理

### 要标记的反模式

- **吞掉的异常**：空的catch块或只记录日志的catch
  ```javascript
  try { ... } catch (e) { }  // 静默失败
  try { ... } catch (e) { console.log(e) }  // 记录并忘记
  ```
- **过于宽泛的捕获**：捕获 `Exception`/`Error` 基类而不是特定类型
- **错误信息泄露**：堆栈跟踪或内部细节暴露给用户
- **缺少错误处理**：易失败操作（I/O、网络、解析）周围没有try-catch
- **异步错误处理**：未处理的promise拒绝、缺少 `.catch()`、没有错误边界

### 要检查的最佳实践

- [ ] 错误在适当的边界被捕获
- [ ] 错误消息对用户友好（不暴露内部细节）
- [ ] 错误记录有足够的调试上下文
- [ ] 异步错误被正确传播或处理
- [ ] 为可恢复错误定义了回退行为
- [ ] 严重错误触发警报/监控

### 要问的问题
- "当这个操作失败时会发生什么？"
- "调用者会知道出了问题吗？"
- "有足够的上下文来调试这个错误吗？"

---

## 性能与缓存

### CPU密集型操作

- **热路径中的昂贵操作**：正则表达式编译、JSON解析、循环中的加密
- **阻塞主线程**：同步I/O、没有worker/异步的 heavy计算
- **不必要的重复计算**：相同计算多次执行
- **缺少记忆化**：纯函数使用相同输入重复调用

### 数据库与I/O

- **N+1查询**：循环中每次迭代都查询而不是批量查询
  ```javascript
  // 不好：N+1
  for (const id of ids) {
    const user = await db.query(`SELECT * FROM users WHERE id = ?`, id)
  }
  // 好：批量
  const users = await db.query(`SELECT * FROM users WHERE id IN (?)`, ids)
  ```
- **缺少索引**：在未索引列上查询
- **过度获取**：只需要几列时使用SELECT *
- **没有分页**：将整个数据集加载到内存中

### 缓存问题

- **昂贵操作缺少缓存**：重复的API调用、数据库查询、计算
- **缓存没有TTL**：无限期提供陈旧数据
- **缓存没有失效策略**：数据更新但缓存未清除
- **缓存键冲突**：键唯一性不足
- **全局缓存用户特定数据**：安全/隐私问题

### 内存

- **无界集合**：无限增长的数组/映射
- **大对象保留**：持有引用防止GC
- **循环中的字符串拼接**：使用StringBuilder/join代替
- **完全加载大文件**：使用流代替

### 要问的问题
- "这个操作的时间复杂度是多少？"
- "使用10倍/100倍数据时表现如何？"
- "这个结果可缓存吗？应该缓存吗？"
- "这个可以批量处理而不是逐个处理吗？"

---

## 边界条件

### Null/Undefined处理

- **缺少null检查**：访问可能为null的对象的属性
- **真值/假值混淆**：当 `0` 或 `""` 有效时使用 `if (value)`
- **可选链过度使用**：`a?.b?.c?.d` 隐藏结构问题
- **Null vs undefined不一致**：混合使用没有明确约定

### 空集合

- **空数组未处理**：代码假设数组有项目
- **空对象边缘情况**：对空对象使用 `for...in` 或 `Object.keys`
- **首/尾元素访问**：没有长度检查的 `arr[0]` 或 `arr[arr.length-1]`

### 数值边界

- **除以零**：除法前缺少检查
- **整数溢出**：超出安全整数范围的大数字
- **浮点数比较**：使用 `===` 而不是epsilon比较
- **负值**：不应该为负的索引或计数
- **差一错误**：循环边界、数组切片、分页

### 字符串边界

- **空字符串**：未作为边缘情况处理
- **仅空白字符串**：通过真值检查但实际上为空
- **非常长的字符串**：无长度限制导致内存/显示问题
- **Unicode边缘情况**：表情符号、RTL文本、组合字符

### 常见危险模式

```javascript
// 危险：无null检查
const name = user.profile.name

// 危险：无检查的数组访问
const first = items[0]

// 危险：无检查的除法
const avg = total / count

// 危险：真值检查排除有效值
if (value) { ... }  // 对 0, "", false 失败
```

### 要问的问题
- "如果这是null/undefined会怎样？"
- "如果这个集合为空会怎样？"
- "这个数字的有效范围是什么？"
- "在边界（0, -1, MAX_INT）会发生什么？"
