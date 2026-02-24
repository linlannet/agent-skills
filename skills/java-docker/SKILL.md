---
name: java-docker
description: Containerize Java applications - Dockerfile optimization, JVM settings, security
sasmp_version: "1.3.0"
version: "3.0.0"
bonded_agent: 08-java-devops
bond_type: PRIMARY_BOND
allowed-tools: Read, Write, Bash, Glob, Grep

# Parameter Validation
parameters:
  base_image:
    type: string
    enum: [temurin, distroless, alpine]
    description: Base image type
  java_version:
    type: string
    default: "21"
    description: Java version
---

## Language / 语言

- **English** - Scroll down to the English section below
- **中文** - 向下滚动到下方的中文部分

---

# Java Docker Skill

# Java Docker 技能

Containerize Java applications with optimized Dockerfiles and JVM settings.

## Overview

This skill covers Docker best practices for Java including multi-stage builds, JVM container settings, security hardening, and layer optimization.

## When to Use This Skill

Use when you need to:
- Create optimized Java Dockerfiles
- Configure JVM for containers
- Implement security best practices
- Reduce image size
- Set up health checks

## Topics Covered

### Dockerfile Optimization
- Multi-stage builds
- Layer caching strategy
- Spring Boot layered JARs
- Dependency caching

### JVM Container Settings
- UseContainerSupport
- MaxRAMPercentage
- GC selection
- Exit on OOM

### Security
- Non-root users
- Read-only filesystem
- Vulnerability scanning
- Secrets handling

## Quick Reference

```dockerfile
# Multi-stage optimized Dockerfile
FROM eclipse-temurin:21-jdk-alpine AS builder

WORKDIR /app

# Cache dependencies
COPY pom.xml .
COPY .mvn .mvn
RUN mvn dependency:go-offline -B

# Build and extract layers
COPY src ./src
RUN mvn package -DskipTests && \
    java -Djarmode=layertools -jar target/*.jar extract

# Runtime stage
FROM eclipse-temurin:21-jre-alpine

# Security: non-root user
RUN addgroup -S app && adduser -S app -G app
USER app

WORKDIR /app

# Copy layers in order of change frequency
COPY --from=builder /app/dependencies/ ./
COPY --from=builder /app/spring-boot-loader/ ./
COPY --from=builder /app/snapshot-dependencies/ ./
COPY --from=builder /app/application/ ./

# JVM container settings
ENV JAVA_OPTS="-XX:+UseContainerSupport \
    -XX:MaxRAMPercentage=75.0 \
    -XX:+ExitOnOutOfMemoryError \
    -XX:+UseG1GC"

EXPOSE 8080

HEALTHCHECK --interval=30s --timeout=3s --start-period=30s \
    CMD wget -qO- http://localhost:8080/actuator/health/liveness || exit 1

ENTRYPOINT ["sh", "-c", "java $JAVA_OPTS org.springframework.boot.loader.launch.JarLauncher"]
```

## JVM Container Flags

```bash
# Recommended production settings
JAVA_OPTS="
  -XX:+UseContainerSupport
  -XX:MaxRAMPercentage=75.0
  -XX:InitialRAMPercentage=50.0
  -XX:+ExitOnOutOfMemoryError
  -XX:+HeapDumpOnOutOfMemoryError
  -XX:HeapDumpPath=/tmp/heapdump.hprof
  -XX:+UseG1GC
  -Djava.security.egd=file:/dev/./urandom
"
```

## Base Image Comparison

| Image | Size | Security | Use Case |
|-------|------|----------|----------|
| temurin:21-jre | ~200MB | Good | General use |
| temurin:21-jre-alpine | ~100MB | Good | Size-optimized |
| distroless/java21 | ~80MB | Best | Production |

## Security Best Practices

```dockerfile
# Non-root user
RUN addgroup -S app && adduser -S app -G app
USER app

# Read-only filesystem
# (Configure at runtime with --read-only)

# No shell access with distroless
FROM gcr.io/distroless/java21-debian12

# Health check
HEALTHCHECK --interval=30s --timeout=3s \
    CMD wget -qO- localhost:8080/actuator/health || exit 1
```

## Troubleshooting

### Common Issues

| Problem | Cause | Solution |
|---------|-------|----------|
| OOMKilled | Heap > limit | Set MaxRAMPercentage |
| Slow startup | Large image | Multi-stage build |
| Permission denied | Root required | Fix file permissions |
| No memory info | Old JVM | Update to Java 11+ |

### Debug Checklist
```
□ Check container memory limits
□ Verify JVM sees container limits
□ Review health check configuration
□ Scan image for vulnerabilities
□ Test with resource constraints
```

## Usage

```
Skill("java-docker")
```

## Related Skills
- `java-maven-gradle` - Build integration
- `java-microservices` - K8s deployment

---

# Java Docker 技能

使用优化的Dockerfile和JVM设置容器化Java应用程序。

## 概述

此技能涵盖Java的Docker最佳实践，包括多阶段构建、JVM容器设置、安全加固和层优化。

## 何时使用此技能

当您需要：
- 创建优化的Java Dockerfile
- 为容器配置JVM
- 实施安全最佳实践
- 减小镜像大小
- 设置健康检查

## 涵盖的主题

### Dockerfile优化
- 多阶段构建
- 层缓存策略
- Spring Boot分层JAR
- 依赖缓存

### JVM容器设置
- UseContainerSupport
- MaxRAMPercentage
- GC选择
- OOM时退出

### 安全
- 非root用户
- 只读文件系统
- 漏洞扫描
- 密钥处理

## 快速参考

```dockerfile
# 多阶段优化Dockerfile
FROM eclipse-temurin:21-jdk-alpine AS builder

WORKDIR /app

# 缓存依赖
COPY pom.xml .
COPY .mvn .mvn
RUN mvn dependency:go-offline -B

# 构建并提取层
COPY src ./src
RUN mvn package -DskipTests && \
    java -Djarmode=layertools -jar target/*.jar extract

# 运行时阶段
FROM eclipse-temurin:21-jre-alpine

# 安全：非root用户
RUN addgroup -S app && adduser -S app -G app
USER app

WORKDIR /app

# 按更改频率顺序复制层
COPY --from=builder /app/dependencies/ ./
COPY --from=builder /app/spring-boot-loader/ ./
COPY --from=builder /app/snapshot-dependencies/ ./
COPY --from=builder /app/application/ ./

# JVM容器设置
ENV JAVA_OPTS="-XX:+UseContainerSupport \
    -XX:MaxRAMPercentage=75.0 \
    -XX:+ExitOnOutOfMemoryError \
    -XX:+UseG1GC"

EXPOSE 8080

HEALTHCHECK --interval=30s --timeout=3s --start-period=30s \
    CMD wget -qO- http://localhost:8080/actuator/health/liveness || exit 1

ENTRYPOINT ["sh", "-c", "java $JAVA_OPTS org.springframework.boot.loader.launch.JarLauncher"]
```

## JVM容器标志

```bash
# 推荐的生产设置
JAVA_OPTS="
  -XX:+UseContainerSupport
  -XX:MaxRAMPercentage=75.0
  -XX:InitialRAMPercentage=50.0
  -XX:+ExitOnOutOfMemoryError
  -XX:+HeapDumpOnOutOfMemoryError
  -XX:HeapDumpPath=/tmp/heapdump.hprof
  -XX:+UseG1GC
  -Djava.security.egd=file:/dev/./urandom
"
```

## 基础镜像比较

| 镜像 | 大小 | 安全性 | 用例 |
|------|------|--------|------|
| temurin:21-jre | ~200MB | 良好 | 一般使用 |
| temurin:21-jre-alpine | ~100MB | 良好 | 大小优化 |
| distroless/java21 | ~80MB | 最佳 | 生产环境 |

## 安全最佳实践

```dockerfile
# 非root用户
RUN addgroup -S app && adduser -S app -G app
USER app

# 只读文件系统
# (在运行时使用 --read-only 配置)

# 使用distroless无shell访问
FROM gcr.io/distroless/java21-debian12

# 健康检查
HEALTHCHECK --interval=30s --timeout=3s \
    CMD wget -qO- localhost:8080/actuator/health || exit 1
```

## 故障排除

### 常见问题

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| OOMKilled | 堆内存 > 限制 | 设置 MaxRAMPercentage |
| 启动缓慢 | 镜像过大 | 多阶段构建 |
| 权限被拒绝 | 需要root | 修复文件权限 |
| 无内存信息 | 旧JVM | 更新到Java 11+ |

### 调试清单
```
□ 检查容器内存限制
□ 验证JVM是否看到容器限制
□ 审查健康检查配置
□ 扫描镜像漏洞
□ 测试资源约束
```

## 使用

```
Skill("java-docker")
```

## 相关技能
- `java-maven-gradle` - 构建集成
- `java-microservices` - K8s部署
