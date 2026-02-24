---
name: java-performance
description: JVM performance tuning - GC optimization, profiling, memory analysis, benchmarking
sasmp_version: "1.3.0"
version: "3.0.0"
bonded_agent: 02-java-advanced
bond_type: SECONDARY_BOND
allowed-tools: Read, Write, Bash, Glob, Grep

# Parameter Validation
parameters:
  focus:
    type: string
    enum: [gc, memory, cpu, profiling]
    description: Performance focus area
---

## Language / 语言

- **English** - Scroll down to the English section below
- **中文** - 向下滚动到下方的中文部分

---

# Java Performance Skill

Optimize JVM performance through profiling, GC tuning, and memory analysis.

## Overview

This skill covers JVM performance optimization including garbage collection tuning, memory analysis, CPU profiling, and benchmarking with JMH.

## When to Use This Skill

Use when you need to:
- Tune GC for low latency or throughput
- Profile CPU hotspots
- Analyze memory leaks
- Benchmark code performance
- Optimize container settings

## Quick Reference

### GC Presets

```bash
# High-throughput
-XX:+UseG1GC
-XX:MaxGCPauseMillis=200
-Xms4g -Xmx4g
-XX:+AlwaysPreTouch

# Low-latency
-XX:+UseZGC
-XX:+ZGenerational
-Xms8g -Xmx8g

# Memory-constrained
-XX:+UseSerialGC
-Xms512m -Xmx512m
-XX:+UseCompressedOops

# Container-optimized
-XX:+UseContainerSupport
-XX:MaxRAMPercentage=75.0
-XX:+ExitOnOutOfMemoryError
```

### Profiling Commands

```bash
# Thread dump
jstack -l <pid> > threaddump.txt

# Heap dump
jmap -dump:format=b,file=heap.hprof <pid>

# GC analysis
jstat -gcutil <pid> 1000 10

# Flight recording
jcmd <pid> JFR.start duration=60s filename=app.jfr

# Async profiler
./profiler.sh -d 30 -f profile.html <pid>
```

### JMH Benchmark

```java
@BenchmarkMode(Mode.Throughput)
@Warmup(iterations = 3, time = 1)
@Measurement(iterations = 5, time = 1)
@State(Scope.Benchmark)
public class MyBenchmark {

    @Benchmark
    public void testMethod(Blackhole bh) {
        bh.consume(compute());
    }
}
```

## GC Comparison

| GC | Latency | Throughput | Heap Size |
|----|---------|------------|-----------|
| G1 | Medium | High | 4-32GB |
| ZGC | Very Low | Medium | 8GB-16TB |
| Shenandoah | Very Low | Medium | 8GB+ |
| Parallel | High | Very High | Any |

## Troubleshooting

| Problem | Cause | Solution |
|---------|-------|----------|
| GC thrashing | Heap too small | Increase heap |
| High latency | GC pauses | Switch to ZGC |
| Memory leak | Object retention | Heap dump + MAT |
| CPU spikes | Hot loops | Profile + optimize |

## Usage

```
Skill("java-performance")
```

---

# Java 性能技能

通过分析、GC 调优和内存分析优化 JVM 性能。

## 概述

本技能涵盖 JVM 性能优化，包括垃圾收集调优、内存分析、CPU 分析和使用 JMH 进行基准测试。

## 何时使用此技能

当您需要以下操作时使用：
- 为低延迟或吞吐量调优 GC
- 分析 CPU 热点
- 分析内存泄漏
- 基准测试代码性能
- 优化容器设置

## 快速参考

### GC 预设

```bash
# High-throughput
-XX:+UseG1GC
-XX:MaxGCPauseMillis=200
-Xms4g -Xmx4g
-XX:+AlwaysPreTouch

# Low-latency
-XX:+UseZGC
-XX:+ZGenerational
-Xms8g -Xmx8g

# Memory-constrained
-XX:+UseSerialGC
-Xms512m -Xmx512m
-XX:+UseCompressedOops

# Container-optimized
-XX:+UseContainerSupport
-XX:MaxRAMPercentage=75.0
-XX:+ExitOnOutOfMemoryError
```

### 分析命令

```bash
# Thread dump
jstack -l <pid> > threaddump.txt

# Heap dump
jmap -dump:format=b,file=heap.hprof <pid>

# GC analysis
jstat -gcutil <pid> 1000 10

# Flight recording
jcmd <pid> JFR.start duration=60s filename=app.jfr

# Async profiler
./profiler.sh -d 30 -f profile.html <pid>
```

### JMH 基准测试

```java
@BenchmarkMode(Mode.Throughput)
@Warmup(iterations = 3, time = 1)
@Measurement(iterations = 5, time = 1)
@State(Scope.Benchmark)
public class MyBenchmark {

    @Benchmark
    public void testMethod(Blackhole bh) {
        bh.consume(compute());
    }
}
```

## GC 比较

| GC | 延迟 | 吞吐量 | 堆大小 |
|----|------|--------|--------|
| G1 | 中等 | 高 | 4-32GB |
| ZGC | 极低 | 中等 | 8GB-16TB |
| Shenandoah | 极低 | 中等 | 8GB+ |
| Parallel | 高 | 极高 | 任意 |

## 故障排除

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| GC 抖动 | 堆太小 | 增加堆大小 |
| 高延迟 | GC 暂停 | 切换到 ZGC |
| 内存泄漏 | 对象保留 | 堆转储 + MAT |
| CPU 峰值 | 热点循环 | 分析 + 优化 |

## 使用方法

```
Skill("java-performance")
```
