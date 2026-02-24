---
name: java-maven
description: Master Apache Maven - POM configuration, plugins, lifecycle, dependency management
sasmp_version: "1.3.0"
version: "3.0.0"
bonded_agent: 05-java-build-tools
bond_type: SECONDARY_BOND
allowed-tools: Read, Write, Bash, Glob, Grep

# Parameter Validation
parameters:
  project_type:
    type: string
    enum: [single, multi_module, library]
    description: Project structure
---

## Language / 语言

- **English** - Scroll down to the English section below
- **中文** - 向下滚动到下方的中文部分

---

# Java Maven Skill

# Java Maven 技能

Master Apache Maven for Java project builds and dependency management.

## Overview

This skill covers Maven configuration including POM structure, lifecycle phases, plugin configuration, dependency management with BOMs, and multi-module projects.

## When to Use This Skill

Use when you need to:
- Configure Maven POM files
- Manage dependencies with BOMs
- Set up build plugins
- Create multi-module projects
- Troubleshoot build issues

## Quick Reference

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>my-app</artifactId>
    <version>1.0.0-SNAPSHOT</version>

    <properties>
        <java.version>21</java.version>
        <maven.compiler.source>${java.version}</maven.compiler.source>
        <maven.compiler.target>${java.version}</maven.compiler.target>
    </properties>

    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-dependencies</artifactId>
                <version>3.2.1</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-enforcer-plugin</artifactId>
                <version>3.4.1</version>
            </plugin>
        </plugins>
    </build>
</project>
```

## Lifecycle Phases

```
validate → compile → test → package → verify → install → deploy
```

## Useful Commands

```bash
mvn dependency:tree                    # View dependencies
mvn dependency:analyze                 # Find unused/undeclared
mvn versions:display-dependency-updates  # Check updates
mvn help:effective-pom                 # View effective POM
mvn -B verify                          # Batch mode build
```

## Troubleshooting

| Problem | Solution |
|---------|----------|
| Dependency not found | Check repository, version |
| Version conflict | Use BOM or enforcer |
| Build OOM | Set MAVEN_OPTS=-Xmx1g |

## Usage

```
Skill("java-maven")
```

---

# Java Maven 技能

掌握Apache Maven用于Java项目构建和依赖管理。

## 概述

此技能涵盖Maven配置，包括POM结构、生命周期阶段、插件配置、使用BOM管理依赖和多模块项目。

## 何时使用此技能

当您需要：
- 配置Maven POM文件
- 使用BOM管理依赖
- 设置构建插件
- 创建多模块项目
- 排查构建问题

## 快速参考

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>my-app</artifactId>
    <version>1.0.0-SNAPSHOT</version>

    <properties>
        <java.version>21</java.version>
        <maven.compiler.source>${java.version}</maven.compiler.source>
        <maven.compiler.target>${java.version}</maven.compiler.target>
    </properties>

    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-dependencies</artifactId>
                <version>3.2.1</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-enforcer-plugin</artifactId>
                <version>3.4.1</version>
            </plugin>
        </plugins>
    </build>
</project>
```

## 生命周期阶段

```
validate → compile → test → package → verify → install → deploy
```

## 有用的命令

```bash
mvn dependency:tree                    # 查看依赖
mvn dependency:analyze                 # 查找未使用/未声明的依赖
mvn versions:display-dependency-updates  # 检查更新
mvn help:effective-pom                 # 查看有效POM
mvn -B verify                          # 批处理模式构建
```

## 故障排除

| 问题 | 解决方案 |
|------|----------|
| 依赖未找到 | 检查仓库、版本 |
| 版本冲突 | 使用BOM或enforcer |
| 构建OOM | 设置 MAVEN_OPTS=-Xmx1g |

## 使用

```
Skill("java-maven")
```
