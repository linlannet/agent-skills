---
name: java-testing
description: Test Java applications - JUnit 5, Mockito, integration testing, TDD patterns
sasmp_version: "1.3.0"
version: "3.0.0"
bonded_agent: 04-java-testing
bond_type: PRIMARY_BOND
allowed-tools: Read, Write, Bash, Glob, Grep

# Parameter Validation
parameters:
  test_type:
    type: string
    enum: [unit, integration, e2e, contract]
    description: Type of test to create
  framework:
    type: string
    default: junit5
    enum: [junit5, testng]
    description: Testing framework
---

## Language / 语言

- **English** - Scroll down to the English section below
- **中文** - 向下滚动到下方的中文部分

---

# Java Testing Skill

Write comprehensive tests for Java applications with modern testing practices.

## Overview

This skill covers Java testing with JUnit 5, Mockito, AssertJ, and integration testing with Spring Boot Test and Testcontainers. Includes TDD patterns and test coverage strategies.

## When to Use This Skill

Use when you need to:
- Write unit tests with JUnit 5
- Create mocks with Mockito
- Build integration tests with Testcontainers
- Implement TDD/BDD practices
- Improve test coverage

## Topics Covered

### JUnit 5
- @Test, @Nested, @DisplayName
- @ParameterizedTest with sources
- Lifecycle annotations
- Extensions and custom annotations

### Mockito
- @Mock, @InjectMocks, @Spy
- Stubbing (when/thenReturn)
- Verification (verify, times)
- BDD style (given/willReturn)

### AssertJ
- Fluent assertions 
- Collection assertions
- Exception assertions
- Custom assertions

### Integration Testing
- @SpringBootTest slices
- Testcontainers setup
- MockMvc for APIs
- Database testing

## Quick Reference

```java
// Unit Test with Mockito
@ExtendWith(MockitoExtension.class)
class UserServiceTest {

    @Mock
    private UserRepository userRepository;

    @InjectMocks
    private UserService userService;

    @Test
    @DisplayName("Should find user by ID")
    void shouldFindUserById() {
        // Given
        User user = new User(1L, "John");
        given(userRepository.findById(1L)).willReturn(Optional.of(user));

        // When
        Optional<User> result = userService.findById(1L);

        // Then
        assertThat(result)
            .isPresent()
            .hasValueSatisfying(u ->
                assertThat(u.getName()).isEqualTo("John"));
        then(userRepository).should().findById(1L);
    }
}

// Parameterized Test
@ParameterizedTest
@CsvSource({
    "valid@email.com, true",
    "invalid-email, false",
    "'', false"
})
void shouldValidateEmail(String email, boolean expected) {
    assertThat(validator.isValid(email)).isEqualTo(expected);
}

// Integration Test with Testcontainers
@Testcontainers
@SpringBootTest
class OrderRepositoryIT {

    @Container
    static PostgreSQLContainer<?> postgres =
        new PostgreSQLContainer<>("postgres:15");

    @DynamicPropertySource
    static void configure(DynamicPropertyRegistry registry) {
        registry.add("spring.datasource.url", postgres::getJdbcUrl);
        registry.add("spring.datasource.username", postgres::getUsername);
        registry.add("spring.datasource.password", postgres::getPassword);
    }

    @Autowired
    private OrderRepository repository;

    @Test
    void shouldPersistOrder() {
        Order saved = repository.save(new Order("item", 100.0));
        assertThat(saved.getId()).isNotNull();
    }
}

// API Test with MockMvc
@WebMvcTest(UserController.class)
class UserControllerTest {

    @Autowired
    private MockMvc mockMvc;

    @MockBean
    private UserService userService;

    @Test
    void shouldReturnUser() throws Exception {
        given(userService.findById(1L))
            .willReturn(Optional.of(new User(1L, "John")));

        mockMvc.perform(get("/api/users/1"))
            .andExpect(status().isOk())
            .andExpect(jsonPath("$.name").value("John"));
    }
}
```

## Test Data Builders

```java
public class UserTestBuilder {
    private Long id = 1L;
    private String name = "John Doe";
    private String email = "john@example.com";
    private boolean active = true;

    public static UserTestBuilder aUser() {
        return new UserTestBuilder();
    }

    public UserTestBuilder withName(String name) {
        this.name = name;
        return this;
    }

    public UserTestBuilder inactive() {
        this.active = false;
        return this;
    }

    public User build() {
        return new User(id, name, email, active);
    }
}

// Usage
User user = aUser().withName("Jane").inactive().build();
```

## Coverage Goals

```xml
<!-- JaCoCo configuration -->
<configuration>
    <rules>
        <rule>
            <element>BUNDLE</element>
            <limits>
                <limit>
                    <counter>LINE</counter>
                    <value>COVEREDRATIO</value>
                    <minimum>0.80</minimum>
                </limit>
            </limits>
        </rule>
    </rules>
</configuration>
```

## Troubleshooting

### Common Issues

| Problem | Cause | Solution |
|---------|-------|----------|
| Mock not working | Missing @ExtendWith | Add MockitoExtension |
| NPE in test | Mock not initialized | Check @InjectMocks |
| Flaky test | Shared state | Isolate test data |
| Context fails | Missing bean | Use @MockBean |

### Debug Checklist
```
□ Run single test in isolation
□ Check mock setup matches invocation
□ Verify @BeforeEach setup
□ Review @Transactional boundaries
□ Check for shared mutable state
```

## Usage

```
Skill("java-testing")
```

## Related Skills
- `java-testing-advanced` - Advanced patterns
- `java-spring-boot` - Spring test slices

---

# Java 测试技能

使用现代测试实践为 Java 应用程序编写全面的测试。

## 概述

本技能涵盖使用 JUnit 5、Mockito、AssertJ 的 Java 测试，以及使用 Spring Boot Test 和 Testcontainers 的集成测试。包括 TDD 模式和测试覆盖率策略。

## 何时使用此技能

当您需要以下操作时使用：
- 使用 JUnit 5 编写单元测试
- 使用 Mockito 创建模拟对象
- 使用 Testcontainers 构建集成测试
- 实现 TDD/BDD 实践
- 提高测试覆盖率

## 涵盖主题

### JUnit 5
- @Test、@Nested、@DisplayName
- 带数据源的 @ParameterizedTest
- 生命周期注解
- 扩展和自定义注解

### Mockito
- @Mock、@InjectMocks、@Spy
- 存根（when/thenReturn）
- 验证（verify、times）
- BDD 风格（given/willReturn）

### AssertJ
- 流畅的断言
- 集合断言
- 异常断言
- 自定义断言

### 集成测试
- @SpringBootTest 切片
- Testcontainers 设置
- 用于 API 的 MockMvc
- 数据库测试

## 快速参考

```java
// Unit Test with Mockito
@ExtendWith(MockitoExtension.class)
class UserServiceTest {

    @Mock
    private UserRepository userRepository;

    @InjectMocks
    private UserService userService;

    @Test
    @DisplayName("Should find user by ID")
    void shouldFindUserById() {
        // Given
        User user = new User(1L, "John");
        given(userRepository.findById(1L)).willReturn(Optional.of(user));

        // When
        Optional<User> result = userService.findById(1L);

        // Then
        assertThat(result)
            .isPresent()
            .hasValueSatisfying(u ->
                assertThat(u.getName()).isEqualTo("John"));
        then(userRepository).should().findById(1L);
    }
}

// Parameterized Test
@ParameterizedTest
@CsvSource({
    "valid@email.com, true",
    "invalid-email, false",
    "'', false"
})
void shouldValidateEmail(String email, boolean expected) {
    assertThat(validator.isValid(email)).isEqualTo(expected);
}

// Integration Test with Testcontainers
@Testcontainers
@SpringBootTest
class OrderRepositoryIT {

    @Container
    static PostgreSQLContainer<?> postgres =
        new PostgreSQLContainer<>("postgres:15");

    @DynamicPropertySource
    static void configure(DynamicPropertyRegistry registry) {
        registry.add("spring.datasource.url", postgres::getJdbcUrl);
        registry.add("spring.datasource.username", postgres::getUsername);
        registry.add("spring.datasource.password", postgres::getPassword);
    }

    @Autowired
    private OrderRepository repository;

    @Test
    void shouldPersistOrder() {
        Order saved = repository.save(new Order("item", 100.0));
        assertThat(saved.getId()).isNotNull();
    }
}

// API Test with MockMvc
@WebMvcTest(UserController.class)
class UserControllerTest {

    @Autowired
    private MockMvc mockMvc;

    @MockBean
    private UserService userService;

    @Test
    void shouldReturnUser() throws Exception {
        given(userService.findById(1L))
            .willReturn(Optional.of(new User(1L, "John")));

        mockMvc.perform(get("/api/users/1"))
            .andExpect(status().isOk())
            .andExpect(jsonPath("$.name").value("John"));
    }
}
```

## 测试数据构建器

```java
public class UserTestBuilder {
    private Long id = 1L;
    private String name = "John Doe";
    private String email = "john@example.com";
    private boolean active = true;

    public static UserTestBuilder aUser() {
        return new UserTestBuilder();
    }

    public UserTestBuilder withName(String name) {
        this.name = name;
        return this;
    }

    public UserTestBuilder inactive() {
        this.active = false;
        return this;
    }

    public User build() {
        return new User(id, name, email, active);
    }
}

// Usage
User user = aUser().withName("Jane").inactive().build();
```

## 覆盖率目标

```xml
<!-- JaCoCo configuration -->
<configuration>
    <rules>
        <rule>
            <element>BUNDLE</element>
            <limits>
                <limit>
                    <counter>LINE</counter>
                    <value>COVEREDRATIO</value>
                    <minimum>0.80</minimum>
                </limit>
            </limits>
        </rule>
    </rules>
</configuration>
```

## 故障排除

### 常见问题

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| Mock 不工作 | 缺少 @ExtendWith | 添加 MockitoExtension |
| 测试中的 NPE | Mock 未初始化 | 检查 @InjectMocks |
| 不稳定的测试 | 共享状态 | 隔离测试数据 |
| 上下文失败 | 缺少 bean | 使用 @MockBean |

### 调试清单
```
□ 单独运行单个测试
□ 检查 mock 设置是否匹配调用
□ 验证 @BeforeEach 设置
□ 审查 @Transactional 边界
□ 检查共享的可变状态
```

## 使用方法

```
Skill("java-testing")
```

## 相关技能
- `java-testing-advanced` - 高级模式
- `java-spring-boot` - Spring 测试切片
