---
name: java-jpa-hibernate
description: Master JPA/Hibernate - entity design, queries, transactions, performance optimization
sasmp_version: "1.3.0"
version: "3.0.0"
bonded_agent: 06-java-persistence
bond_type: PRIMARY_BOND
allowed-tools: Read, Write, Bash, Glob, Grep

# Parameter Validation
parameters:
  database:
    type: string
    enum: [postgresql, mysql, oracle, h2]
    description: Target database
  focus:
    type: string
    enum: [entities, queries, transactions, caching]
    description: Topic focus area
---

## Language / 语言

- **English** - Scroll down to the English section below
- **中文** - 向下滚动到下方的中文部分

---

# Java JPA Hibernate Skill

# Java JPA Hibernate 技能

Master data persistence with JPA and Hibernate for production applications.

## Overview

This skill covers JPA entity design, Hibernate optimization, Spring Data repositories, query strategies, and caching. Focuses on preventing N+1 queries and building high-performance persistence layers.

## When to Use This Skill

Use when you need to:
- Design JPA entities with relationships
- Optimize database queries
- Configure Hibernate for performance
- Implement caching strategies
- Debug persistence issues

## Topics Covered

### Entity Design
- Entity mapping annotations
- Relationship types (1:1, 1:N, N:M)
- Inheritance strategies
- Lifecycle callbacks
- Auditing

### Query Optimization
- N+1 problem prevention
- JOIN FETCH vs EntityGraph
- Batch fetching
- Projections and DTOs

### Transactions
- @Transactional configuration
- Propagation and isolation
- Optimistic vs pessimistic locking
- Deadlock prevention

### Caching
- First and second level cache
- Query cache
- Cache invalidation
- Redis integration

## Quick Reference

```java
// Entity with relationships
@Entity
@Table(name = "orders")
public class Order {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn(name = "customer_id", nullable = false)
    private Customer customer;

    @OneToMany(mappedBy = "order", cascade = CascadeType.ALL, orphanRemoval = true)
    @BatchSize(size = 20)
    private List<OrderItem> items = new ArrayList<>();

    @Version
    private Long version;

    // Bidirectional helper
    public void addItem(OrderItem item) {
        items.add(item);
        item.setOrder(this);
    }
}

// Auditing base class
@MappedSuperclass
@EntityListeners(AuditingEntityListener.class)
public abstract class Auditable {
    @CreatedDate
    @Column(updatable = false)
    private Instant createdAt;

    @LastModifiedDate
    private Instant updatedAt;
}

// Repository with query optimization
public interface OrderRepository extends JpaRepository<Order, Long> {

    // JOIN FETCH to prevent N+1
    @Query("SELECT DISTINCT o FROM Order o JOIN FETCH o.items WHERE o.status = :status")
    List<Order> findByStatusWithItems(@Param("status") Status status);

    // EntityGraph alternative
    @EntityGraph(attributePaths = {"items", "customer"})
    Optional<Order> findById(Long id);

    // DTO Projection
    @Query("SELECT new com.example.OrderSummary(o.id, o.status, c.name) " +
           "FROM Order o JOIN o.customer c WHERE o.id = :id")
    Optional<OrderSummary> findSummaryById(@Param("id") Long id);
}
```

## N+1 Prevention Strategies

| Strategy | Use When | Example |
|----------|----------|---------|
| JOIN FETCH | Always need relation | `JOIN FETCH o.items` |
| EntityGraph | Dynamic fetching | `@EntityGraph(attributePaths)` |
| @BatchSize | Collection access | `@BatchSize(size = 20)` |
| DTO Projection | Read-only queries | `new OrderSummary(...)` |

## Hibernate Configuration

```yaml
spring:
  jpa:
    open-in-view: false  # Critical!
    properties:
      hibernate:
        jdbc.batch_size: 50
        order_inserts: true
        order_updates: true
        default_batch_fetch_size: 20
        generate_statistics: ${HIBERNATE_STATS:false}

  datasource:
    hikari:
      maximum-pool-size: 20
      minimum-idle: 5
      leak-detection-threshold: 60000
```

## Troubleshooting

### Common Issues

| Problem | Cause | Solution |
|---------|-------|----------|
| N+1 queries | Lazy in loop | JOIN FETCH, EntityGraph |
| LazyInitException | Session closed | DTO projection |
| Slow queries | Missing index | EXPLAIN ANALYZE |
| Connection leak | No @Transactional | Add annotation |

### Debug Properties
```properties
spring.jpa.show-sql=true
logging.level.org.hibernate.SQL=DEBUG
logging.level.org.hibernate.orm.jdbc.bind=TRACE
hibernate.generate_statistics=true
```

### Debug Checklist
```
□ Enable SQL logging
□ Check query count per request
□ Verify fetch strategies
□ Review @Transactional
□ Check connection pool
```

## Usage

```
Skill("java-jpa-hibernate")
```

## Related Skills
- `java-performance` - Query optimization
- `java-spring-boot` - Spring Data

---

# Java JPA Hibernate 技能

掌握使用JPA和Hibernate进行生产应用程序的数据持久化。

## 概述

此技能涵盖JPA实体设计、Hibernate优化、Spring Data存储库、查询策略和缓存。专注于防止N+1查询和构建高性能持久化层。

## 何时使用此技能

当您需要：
- 设计带有关系的JPA实体
- 优化数据库查询
- 配置Hibernate以提高性能
- 实现缓存策略
- 调试持久化问题

## 涵盖的主题

### 实体设计
- 实体映射注解
- 关系类型（1:1, 1:N, N:M）
- 继承策略
- 生命周期回调
- 审计

### 查询优化
- N+1问题预防
- JOIN FETCH vs EntityGraph
- 批量获取
- 投影和DTO

### 事务
- @Transactional配置
- 传播和隔离
- 乐观锁vs悲观锁
- 死锁预防

### 缓存
- 一级和二级缓存
- 查询缓存
- 缓存失效
- Redis集成

## 快速参考

```java
// 带有关系的实体
@Entity
@Table(name = "orders")
public class Order {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn(name = "customer_id", nullable = false)
    private Customer customer;

    @OneToMany(mappedBy = "order", cascade = CascadeType.ALL, orphanRemoval = true)
    @BatchSize(size = 20)
    private List<OrderItem> items = new ArrayList<>();

    @Version
    private Long version;

    // 双向关系辅助方法
    public void addItem(OrderItem item) {
        items.add(item);
        item.setOrder(this);
    }
}

// 审计基类
@MappedSuperclass
@EntityListeners(AuditingEntityListener.class)
public abstract class Auditable {
    @CreatedDate
    @Column(updatable = false)
    private Instant createdAt;

    @LastModifiedDate
    private Instant updatedAt;
}

// 带有查询优化的存储库
public interface OrderRepository extends JpaRepository<Order, Long> {

    // JOIN FETCH 防止N+1
    @Query("SELECT DISTINCT o FROM Order o JOIN FETCH o.items WHERE o.status = :status")
    List<Order> findByStatusWithItems(@Param("status") Status status);

    // EntityGraph替代方案
    @EntityGraph(attributePaths = {"items", "customer"})
    Optional<Order> findById(Long id);

    // DTO投影
    @Query("SELECT new com.example.OrderSummary(o.id, o.status, c.name) " +
           "FROM Order o JOIN o.customer c WHERE o.id = :id")
    Optional<OrderSummary> findSummaryById(@Param("id") Long id);
}
```

## N+1预防策略

| 策略 | 使用场景 | 示例 |
|------|----------|------|
| JOIN FETCH | 始终需要关系 | `JOIN FETCH o.items` |
| EntityGraph | 动态获取 | `@EntityGraph(attributePaths)` |
| @BatchSize | 集合访问 | `@BatchSize(size = 20)` |
| DTO投影 | 只读查询 | `new OrderSummary(...)` |

## Hibernate配置

```yaml
spring:
  jpa:
    open-in-view: false  # 关键！
    properties:
      hibernate:
        jdbc.batch_size: 50
        order_inserts: true
        order_updates: true
        default_batch_fetch_size: 20
        generate_statistics: ${HIBERNATE_STATS:false}

  datasource:
    hikari:
      maximum-pool-size: 20
      minimum-idle: 5
      leak-detection-threshold: 60000
```

## 故障排除

### 常见问题

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| N+1查询 | 循环中的延迟加载 | JOIN FETCH, EntityGraph |
| LazyInitException | 会话关闭 | DTO投影 |
| 查询缓慢 | 缺少索引 | EXPLAIN ANALYZE |
| 连接泄漏 | 无@Transactional | 添加注解 |

### 调试属性
```properties
spring.jpa.show-sql=true
logging.level.org.hibernate.SQL=DEBUG
logging.level.org.hibernate.orm.jdbc.bind=TRACE
hibernate.generate_statistics=true
```

### 调试清单
```
□ 启用SQL日志
□ 检查每个请求的查询计数
□ 验证获取策略
□ 审查@Transactional
□ 检查连接池
```

## 使用

```
Skill("java-jpa-hibernate")
```

## 相关技能
- `java-performance` - 查询优化
- `java-spring-boot` - Spring Data
