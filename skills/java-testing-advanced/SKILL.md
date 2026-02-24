---
name: java-testing-advanced
description: Advanced testing - Testcontainers, contract testing, mutation testing, property-based
sasmp_version: "1.3.0"
version: "3.0.0"
bonded_agent: 04-java-testing
bond_type: SECONDARY_BOND
allowed-tools: Read, Write, Bash, Glob, Grep

# Parameter Validation
parameters:
  technique:
    type: string
    enum: [testcontainers, contract, mutation, property_based]
    description: Advanced testing technique
---

## Language / 语言

- **English** - Scroll down to the English section below
- **中文** - 向下滚动到下方的中文部分

---

# Java Testing Advanced Skill

Advanced testing techniques for comprehensive test coverage.

## Overview

This skill covers advanced testing patterns including Testcontainers for integration testing, contract testing with Pact, mutation testing with PIT, and property-based testing.

## When to Use This Skill

Use when you need to:
- Test with real databases (Testcontainers)
- Verify API contracts
- Find gaps with mutation testing
- Generate test cases automatically

## Quick Reference

### Testcontainers

```java
@Testcontainers
@SpringBootTest
class OrderRepositoryIT {

    @Container
    static PostgreSQLContainer<?> postgres =
        new PostgreSQLContainer<>("postgres:15")
            .withDatabaseName("test")
            .withUsername("test")
            .withPassword("test");

    @Container
    static KafkaContainer kafka =
        new KafkaContainer(DockerImageName.parse("confluentinc/cp-kafka:7.4.0"));

    @DynamicPropertySource
    static void configure(DynamicPropertyRegistry registry) {
        registry.add("spring.datasource.url", postgres::getJdbcUrl);
        registry.add("spring.kafka.bootstrap-servers", kafka::getBootstrapServers);
    }

    @Test
    void shouldPersistOrder() {
        Order saved = repository.save(new Order("item", 100.0));
        assertThat(saved.getId()).isNotNull();
    }
}
```

### Contract Testing (Pact)

```java
@ExtendWith(PactConsumerTestExt.class)
class UserServiceContractTest {

    @Pact(consumer = "order-service", provider = "user-service")
    public RequestResponsePact createPact(PactDslWithProvider builder) {
        return builder
            .given("user exists")
            .uponReceiving("get user request")
                .path("/users/1")
                .method("GET")
            .willRespondWith()
                .status(200)
                .body(new PactDslJsonBody()
                    .integerType("id", 1)
                    .stringType("name", "John"))
            .toPact();
    }

    @Test
    @PactTestFor(pactMethod = "createPact")
    void testGetUser(MockServer mockServer) {
        User user = client.getUser(mockServer.getUrl(), 1L);
        assertThat(user.getName()).isEqualTo("John");
    }
}
```

### Mutation Testing (PIT)

```xml
<plugin>
    <groupId>org.pitest</groupId>
    <artifactId>pitest-maven</artifactId>
    <version>1.15.0</version>
    <configuration>
        <targetClasses>
            <param>com.example.service.*</param>
        </targetClasses>
        <mutationThreshold>80</mutationThreshold>
    </configuration>
</plugin>
```

### Property-Based Testing

```java
@Property
void shouldReverseListTwiceReturnsOriginal(@ForAll List<Integer> list) {
    Collections.reverse(list);
    Collections.reverse(list);
    // Original order restored
}
```

## Testing Pyramid

```
     /\        E2E Tests (few)
    /  \       Contract Tests
   /----\      Integration Tests
  /------\     Unit Tests (many)
```

## Troubleshooting

| Problem | Solution |
|---------|----------|
| Container slow | Reuse containers |
| Port conflicts | Random ports |
| Flaky tests | Wait strategies |

## Usage

```
Skill("java-testing-advanced")
```

---

# Java 高级测试技能

用于全面测试覆盖的高级测试技术。

## 概述

本技能涵盖高级测试模式，包括用于集成测试的 Testcontainers、使用 Pact 的契约测试、使用 PIT 的突变测试和基于属性的测试。

## 何时使用此技能

当您需要以下操作时使用：
- 使用真实数据库进行测试（Testcontainers）
- 验证 API 契约
- 使用突变测试发现测试漏洞
- 自动生成测试用例

## 快速参考

### Testcontainers

```java
@Testcontainers
@SpringBootTest
class OrderRepositoryIT {

    @Container
    static PostgreSQLContainer<?> postgres =
        new PostgreSQLContainer<>("postgres:15")
            .withDatabaseName("test")
            .withUsername("test")
            .withPassword("test");

    @Container
    static KafkaContainer kafka =
        new KafkaContainer(DockerImageName.parse("confluentinc/cp-kafka:7.4.0"));

    @DynamicPropertySource
    static void configure(DynamicPropertyRegistry registry) {
        registry.add("spring.datasource.url", postgres::getJdbcUrl);
        registry.add("spring.kafka.bootstrap-servers", kafka::getBootstrapServers);
    }

    @Test
    void shouldPersistOrder() {
        Order saved = repository.save(new Order("item", 100.0));
        assertThat(saved.getId()).isNotNull();
    }
}
```

### 契约测试（Pact）

```java
@ExtendWith(PactConsumerTestExt.class)
class UserServiceContractTest {

    @Pact(consumer = "order-service", provider = "user-service")
    public RequestResponsePact createPact(PactDslWithProvider builder) {
        return builder
            .given("user exists")
            .uponReceiving("get user request")
                .path("/users/1")
                .method("GET")
            .willRespondWith()
                .status(200)
                .body(new PactDslJsonBody()
                    .integerType("id", 1)
                    .stringType("name", "John"))
            .toPact();
    }

    @Test
    @PactTestFor(pactMethod = "createPact")
    void testGetUser(MockServer mockServer) {
        User user = client.getUser(mockServer.getUrl(), 1L);
        assertThat(user.getName()).isEqualTo("John");
    }
}
```

### 突变测试（PIT）

```xml
<plugin>
    <groupId>org.pitest</groupId>
    <artifactId>pitest-maven</artifactId>
    <version>1.15.0</version>
    <configuration>
        <targetClasses>
            <param>com.example.service.*</param>
        </targetClasses>
        <mutationThreshold>80</mutationThreshold>
    </configuration>
</plugin>
```

### 基于属性的测试

```java
@Property
void shouldReverseListTwiceReturnsOriginal(@ForAll List<Integer> list) {
    Collections.reverse(list);
    Collections.reverse(list);
    // Original order restored
}
```

## 测试金字塔

```
     /\        E2E 测试（少量）
    /  \       契约测试
   /----\      集成测试
  /------\     单元测试（大量）
```

## 故障排除

| 问题 | 解决方案 |
|------|----------|
| 容器缓慢 | 重用容器 |
| 端口冲突 | 随机端口 |
| 不稳定的测试 | 等待策略 |

## 使用方法

```
Skill("java-testing-advanced")
```
