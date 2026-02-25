---
name: java-gradle
description: Master Gradle - Kotlin DSL, task configuration, build optimization, caching
sasmp_version: "1.3.0"
version: "3.0.0"
bonded_agent: 05-java-build-tools
bond_type: SECONDARY_BOND
allowed-tools: Read, Write, Bash, Glob, Grep

# Parameter Validation
parameters:
  dsl:
    type: string
    enum: [kotlin, groovy]
    default: kotlin
    description: Gradle DSL preference
---

# Java Gradle 技能

掌握使用Kotlin DSL的Gradle构建工具，用于Java项目。

## 概述

此技能涵盖使用Kotlin DSL的Gradle配置，包括任务配置、使用目录管理依赖、构建缓存优化和CI/CD集成。

## 何时使用此技能

当您需要：
- 配置Gradle构建（Kotlin DSL）
- 使用目录管理依赖
- 优化构建性能
- 设置构建缓存
- 创建自定义任务

## 快速参考

```kotlin
// build.gradle.kts
plugins {
    java
    id("org.springframework.boot") version "3.2.1"
    id("io.spring.dependency-management") version "1.1.4"
}

java {
    toolchain {
        languageVersion = JavaLanguageVersion.of(21)
    }
}

repositories {
    mavenCentral()
}

dependencies {
    implementation("org.springframework.boot:spring-boot-starter-web")
    testImplementation("org.springframework.boot:spring-boot-starter-test")
}

tasks.withType<JavaCompile> {
    options.compilerArgs.addAll(listOf("-parameters", "-Xlint:all"))
    options.isFork = true
    options.isIncremental = true
}

tasks.test {
    useJUnitPlatform()
    maxParallelForks = Runtime.getRuntime().availableProcessors() / 2
}
```

## 版本目录

```toml
# gradle/libs.versions.toml
[versions]
spring-boot = "3.2.1"

[libraries]
spring-boot-web = { module = "org.springframework.boot:spring-boot-starter-web", version.ref = "spring-boot" }

[plugins]
spring-boot = { id = "org.springframework.boot", version.ref = "spring-boot" }
```

## 有用的命令

```bash
gradle dependencies              # 查看依赖
gradle dependencyInsight --dependency log4j  # 分析依赖
gradle build --scan              # 构建扫描
gradle build --build-cache       # 使用缓存
gradle wrapper --gradle-version 8.5  # 更新包装器
```

## 构建优化

```kotlin
// settings.gradle.kts
enableFeaturePreview("STABLE_CONFIGURATION_CACHE")

// 启用并行和缓存
org.gradle.parallel=true
org.gradle.caching=true
```

## 故障排除

| 问题 | 解决方案 |
|------|----------|
| 构建缓慢 | 启用 --build-cache |
| 版本冲突 | 使用 platform() 或 constraints |
| 缓存问题 | gradle --refresh-dependencies |

## 使用

```
Skill("java-gradle")
```