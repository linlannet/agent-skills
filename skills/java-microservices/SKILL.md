---
name: java-microservices
description: Build microservices - Spring Cloud, service mesh, event-driven, resilience patterns
sasmp_version: "1.3.0"
version: "3.0.0"
bonded_agent: 07-java-microservices
bond_type: PRIMARY_BOND
allowed-tools: Read, Write, Bash, Glob, Grep

# Parameter Validation
parameters:
  pattern:
    type: string
    enum: [saga, cqrs, event_sourcing, api_gateway]
    description: Architecture pattern
  messaging:
    type: string
    enum: [kafka, rabbitmq, redis]
    description: Messaging platform
---

# Java 微服务技能

使用 Spring Cloud 和分布式系统模式构建生产级微服务。

## 概述

本技能涵盖使用 Spring Cloud 的微服务架构，包括服务发现、API 网关、断路器、事件驱动通信和分布式追踪。

## 何时使用此技能

当您需要以下操作时使用：
- 设计微服务架构
- 实现服务间通信
- 配置弹性模式
- 设置事件驱动消息传递
- 添加分布式追踪

## 涵盖主题

### Spring Cloud 组件
- Config Server（集中配置）
- Service Discovery（服务发现，Eureka、Consul）
- API Gateway（API 网关，Spring Cloud Gateway）
- Load Balancing（负载均衡，Spring Cloud LoadBalancer）

### 弹性模式
- Circuit Breaker（断路器，Resilience4j）
- 带退避的重试
- 舱壁隔离
- 速率限制

### 事件驱动架构
- Apache Kafka 集成
- Spring Cloud Stream
- Saga 模式
- 事件溯源基础

### 可观测性
- 分布式追踪（Micrometer）
- 指标（Prometheus）
- 日志关联

## 快速参考

```java
// Saga with Choreography
@Component
public class OrderSagaListener {

    @KafkaListener(topics = "order.created")
    public void handleOrderCreated(OrderCreatedEvent event) {
        inventoryService.reserve(event.getItems());
    }

    @KafkaListener(topics = "payment.failed")
    public void handlePaymentFailed(PaymentFailedEvent event) {
        // Compensating transaction
        inventoryService.release(event.getOrderId());
        orderService.cancel(event.getOrderId());
    }
}

// Circuit Breaker Configuration
@Configuration
public class ResilienceConfig {

    @Bean
    public Customizer<Resilience4JCircuitBreakerFactory> cbCustomizer() {
        return factory -> factory.configureDefault(id ->
            new Resilience4JConfigBuilder(id)
                .circuitBreakerConfig(CircuitBreakerConfig.custom()
                    .failureRateThreshold(50)
                    .waitDurationInOpenState(Duration.ofSeconds(30))
                    .slidingWindowSize(10)
                    .build())
                .build());
    }
}

// API Gateway Routes
@Configuration
public class GatewayConfig {

    @Bean
    public RouteLocator routes(RouteLocatorBuilder builder) {
        return builder.routes()
            .route("orders", r -> r
                .path("/api/orders/**")
                .filters(f -> f
                    .stripPrefix(1)
                    .circuitBreaker(c -> c.setName("order-cb"))
                    .retry(retry -> retry.setRetries(3)))
                .uri("lb://order-service"))
            .build();
    }
}
```

## 可观测性配置

```yaml
management:
  tracing:
    sampling:
      probability: 1.0
  endpoints:
    web:
      exposure:
        include: health,info,metrics,prometheus

logging:
  pattern:
    level: "%5p [${spring.application.name:},%X{traceId:-},%X{spanId:-}]"
```

## 常见模式

### Saga 模式
```
Order → Inventory → Payment → (Success | Compensate)
```

### 断路器状态
```
CLOSED → (failures exceed threshold) → OPEN
OPEN → (wait duration) → HALF_OPEN
HALF_OPEN → (success) → CLOSED
HALF_OPEN → (failure) → OPEN
```

## 故障排除

### 常见问题

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| 级联失败 | 无断路器 | 添加 Resilience4j |
| 消息丢失 | 无确认 | 启用手动确认 |
| 数据不一致 | 无补偿 | 实现 saga |
| 服务未找到 | 发现延迟 | 调整心跳 |

### 调试清单
```
□ 追踪请求 (traceId)
□ 检查断路器状态
□ 验证 Kafka 消费者滞后
□ 审查网关路由
□ 监控重试次数
```

## 使用方法

```
Skill("java-microservices")
```

## 相关技能
- `java-spring-boot` - Spring Cloud
- `java-docker` - 容器化