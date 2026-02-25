---
name: java-spring-boot
description: Build production Spring Boot applications - REST APIs, Security, Data, Actuator
sasmp_version: "1.3.0"
version: "3.0.0"
bonded_agent: 03-java-spring
bond_type: PRIMARY_BOND
allowed-tools: Read, Write, Bash, Glob, Grep

# Parameter Validation
parameters:
  spring_version:
    type: string
    default: "3.2"
    description: Spring Boot version
  module:
    type: string
    enum: [web, security, data, actuator, cloud]
    description: Spring module focus
---

# Java Spring Boot 技能

使用现代最佳实践构建生产级 Spring Boot 应用程序。

## 概述

本技能涵盖 Spring Boot 开发，包括 REST API、安全配置、数据访问、Actuator 监控和云集成。遵循 Spring Boot 3.x 模式，强调生产就绪性。

## 何时使用此技能

当您需要以下操作时使用：
- 使用 Spring MVC/WebFlux 创建 REST API
- 配置 Spring Security（OAuth2、JWT）
- 使用 Spring Data 设置数据库访问
- 使用 Actuator 启用监控
- 与 Spring Cloud 集成

## 涵盖主题

### Spring Boot 核心
- 自动配置和启动器
- 应用程序属性和配置文件
- Bean 生命周期和配置
- DevTools 和热重载

### REST API 开发
- @RestController 和 @RequestMapping
- 请求/响应处理
- 使用 Bean Validation 进行验证
- 使用 @ControllerAdvice 进行异常处理

### Spring Security
- SecurityFilterChain 配置
- OAuth2 和 JWT 认证
- 方法安全（@PreAuthorize）
- CORS 和 CSRF 配置

### Spring Data JPA
- 仓库模式
- 查询方法和 @Query
- 分页和排序
- 审计和事务

### Actuator & 监控
- 健康检查和探针
- 使用 Micrometer 的指标
- 自定义端点
- Prometheus 集成

## 快速参考

```java
// REST Controller
@RestController
@RequestMapping("/api/users")
@Validated
public class UserController {

    @GetMapping("/{id}")
    public ResponseEntity<User> getUser(@PathVariable Long id) {
        return userService.findById(id)
            .map(ResponseEntity::ok)
            .orElse(ResponseEntity.notFound().build());
    }

    @PostMapping
    public ResponseEntity<User> createUser(@Valid @RequestBody UserRequest request) {
        User user = userService.create(request);
        URI location = URI.create("/api/users/" + user.getId());
        return ResponseEntity.created(location).body(user);
    }
}

// Security Configuration
@Configuration
@EnableWebSecurity
public class SecurityConfig {

    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        return http
            .csrf(csrf -> csrf.disable())
            .sessionManagement(s -> s.sessionCreationPolicy(STATELESS))
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/actuator/health/**").permitAll()
                .requestMatchers("/api/public/**").permitAll()
                .anyRequest().authenticated())
            .oauth2ResourceServer(oauth2 -> oauth2.jwt(Customizer.withDefaults()))
            .build();
    }
}

// Exception Handler
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(EntityNotFoundException.class)
    public ProblemDetail handleNotFound(EntityNotFoundException ex) {
        return ProblemDetail.forStatusAndDetail(NOT_FOUND, ex.getMessage());
    }
}
```

## 配置模板

```yaml
# application.yml
spring:
  application:
    name: ${APP_NAME:my-service}
  profiles:
    active: ${SPRING_PROFILES_ACTIVE:local}
  jpa:
    open-in-view: false
    properties:
      hibernate:
        jdbc.batch_size: 50

management:
  endpoints:
    web:
      exposure:
        include: health,info,metrics,prometheus
  endpoint:
    health:
      probes:
        enabled: true

server:
  error:
    include-stacktrace: never
```

## 常见模式

### 分层架构
```
Controller → Service → Repository → Database
     ↓           ↓          ↓
   DTOs      Entities    Entities
```

### 验证模式
```java
public record CreateUserRequest(
    @NotBlank @Size(max = 100) String name,
    @Email @NotBlank String email,
    @NotNull @Min(18) Integer age
) {}
```

## 故障排除

### 常见问题

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| Bean not found | 缺少 @Component | 添加注解或 @Bean |
| Circular dependency | 构造函数注入 | 使用 @Lazy 或重构 |
| 401 Unauthorized | 安全配置 | 检查 permitAll 路径 |
| Slow startup | 繁重的自动配置 | 排除未使用的启动器 |

### 调试属性
```properties
debug=true
logging.level.org.springframework.security=DEBUG
spring.jpa.show-sql=true
```

### 调试清单
```
□ 检查 /actuator/conditions
□ 验证活动配置文件
□ 审查安全过滤器链
□ 检查 Bean 定义
□ 测试健康端点
```

## 使用方法

```
Skill("java-spring-boot")
```

## 相关技能
- `java-testing` - Spring 测试模式
- `java-jpa-hibernate` - 数据访问