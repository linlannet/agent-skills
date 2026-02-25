---
name: java-fundamentals
description: Master core Java programming - syntax, OOP, collections, streams, and exception handling
sasmp_version: "1.3.0"
version: "3.0.0"
bonded_agent: 01-java-fundamentals
bond_type: PRIMARY_BOND
allowed-tools: Read, Write, Bash, Glob, Grep

# Parameter Validation
parameters:
  java_version:
    type: string
    default: "21"
    enum: ["8", "11", "17", "21"]
  topic:
    type: string
    enum: [syntax, oop, collections, streams, exceptions, generics]
---

# Java 基础技能

掌握具有生产质量模式的核心Java编程。

## 概述

此技能涵盖Java基础，包括语法、面向对象编程、集合、流API和异常处理，适用于Java 8-21。

## 何时使用此技能

当您需要：
- 编写干净、地道的Java代码
- 遵循面向对象原则设计类
- 选择合适的集合类型
- 实现函数式编程模式
- 正确处理异常

## 涵盖的主题

### 核心语法（Java 8-21）
- 变量、数据类型、运算符
- 控制流、方法、类
- 记录（Java 16+）、密封类（Java 17+）
- 模式匹配（Java 21）

### 面向对象编程
- 类、继承、多态
- 接口和抽象类
- SOLID原则

### 集合框架
- List: ArrayList, LinkedList
- Set: HashSet, TreeSet
- Map: HashMap, ConcurrentHashMap
- Queue: ArrayDeque, PriorityQueue

### 流API
- filter, map, flatMap, reduce, collect
- Optional处理
- 并行流

### 异常处理
- 检查型与非检查型异常
- Try-with-resources
- 自定义异常

## 快速参考

```java
// 记录（Java 16+）
public record User(String name, String email) {}

// 模式匹配（Java 21）
String format(Object obj) {
    return switch (obj) {
        case Integer i -> "Int: %d".formatted(i);
        case String s -> "String: %s".formatted(s);
        default -> obj.toString();
    };
}

// 流操作
List<String> names = users.stream()
    .filter(User::isActive)
    .map(User::getName)
    .sorted()
    .toList();

// Optional处理
String name = Optional.ofNullable(user)
    .map(User::getName)
    .orElse("Unknown");
```

## 集合选择

| 需求 | 使用 | 原因 |
|------|-----|------|
| 索引访问 | ArrayList | O(1) 随机访问 |
| 唯一元素 | HashSet | O(1) 包含检查 |
| 排序唯一 | TreeSet | O(log n) 排序 |
| 键值对 | HashMap | O(1) 获取/放入 |

## 故障排除

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| NullPointerException | 空引用 | 使用 Optional |
| ConcurrentModificationException | 迭代期间修改 | 使用 Iterator.remove() |
| ClassCastException | 类型错误 | 使用泛型 |

## 使用

```
Skill("java-fundamentals")
```