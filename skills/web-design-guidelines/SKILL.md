---
name: web-design-guidelines
description: Review UI code for Web Interface Guidelines compliance. Use when asked to "review my UI", "check accessibility", "audit design", "review UX", or "check my site against best practices".
metadata:
  author: vercel
  version: "1.0.0"
  argument-hint: <file-or-pattern>
---

## Language / 语言

- [English](#english)
- [中文](#中文)

## English

# Web Interface Guidelines

Review files for compliance with Web Interface Guidelines.

## How It Works

1. Fetch the latest guidelines from the source URL below
2. Read the specified files (or prompt user for files/pattern)
3. Check against all rules in the fetched guidelines
4. Output findings in the terse `file:line` format

## Guidelines Source

Fetch fresh guidelines before each review:

```
https://raw.githubusercontent.com/vercel-labs/web-interface-guidelines/main/command.md
```

Use WebFetch to retrieve the latest rules. The fetched content contains all the rules and output format instructions.

## Usage

When a user provides a file or pattern argument:
1. Fetch guidelines from the source URL above
2. Read the specified files
3. Apply all rules from the fetched guidelines
4. Output findings using the format specified in the guidelines

If no files specified, ask the user which files to review.

## 中文

# Web Interface Guidelines（网页界面指南）

检查文件是否符合 Web Interface Guidelines 规范。

## 工作原理

1. 从下方的源 URL 获取最新的指南
2. 读取指定的文件（或提示用户提供文件/模式）
3. 根据获取的指南中的所有规则进行检查
4. 以简洁的 `file:line` 格式输出检查结果

## 指南来源

每次审查前获取最新指南：

```
https://raw.githubusercontent.com/vercel-labs/web-interface-guidelines/main/command.md
```

使用 WebFetch 获取最新规则。获取的内容包含所有规则和输出格式说明。

## 使用方法

当用户提供文件或模式参数时：
1. 从上述源 URL 获取指南
2. 读取指定的文件
3. 应用获取的指南中的所有规则
4. 使用指南中指定的格式输出检查结果

如果未指定文件，请询问用户要审查哪些文件。
