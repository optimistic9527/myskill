---
name: new-item
description: 在 PARA 结构中创建新的项目、领域或资源
---

# 新建 PARA 条目

## 确定类型

如果用户未明确类型，用 AskUserQuestion 询问：

```
你想创建什么类型的条目？
- Project（项目）— 有明确目标和截止日期
- Area（领域）— 持续负责、没有截止日期
- Resource（资源）— 学习资料或参考内容
```

## 创建 Project

### 输入
- 项目名称（用户提供，建议用英文短横线连接，如 `feature-user-auth`）

### 步骤
1. 创建目录：`mkdir -p 10-Projects/{项目名}/`
2. 创建 README.md：

```markdown
---
title: {项目标题}
date: {今天日期}
status: 进行中
tags:
  - project
---

# {项目标题}

## 目标

{待填写}

## 关键文档

{待填写}
```

3. 读取 `rules/home-sync.md` 更新 Home.md

## 创建 Area

### 输入
- 领域名称
- 是否创建对应 MOC（默认是）

### 步骤
1. 创建目录：`mkdir -p 20-Areas/{领域名}/`
2. 如果需要 MOC，创建 `20-Areas/MOC-{领域中文名}.md`：

```markdown
# MOC - {领域名称}

## 概述

{待填写}

## 文档

{后续自动填充}
```

3. 读取 `rules/home-sync.md` 更新 Home.md

## 创建 Resource

### 输入
- 资源主题名称
- 是否创建对应 MOC（默认是）

### 步骤
1. 创建目录：`mkdir -p 30-Resources/{主题名}/`
2. 如果需要 MOC，创建 `30-Resources/MOC-{主题中文名}.md`：

```markdown
# MOC - {主题名称}

## 学习资料

{后续自动填充}
```

3. 读取 `rules/home-sync.md` 更新 Home.md

## 完成后

告知用户创建结果和文件位置，提示用户可以开始往新目录中添加笔记。
