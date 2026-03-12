---
name: archive
description: 将已完成的项目归档到 40-Archive
---

# 项目归档

## 执行步骤

### 1. 确定归档目标

如果用户指定了项目名，直接使用。否则：

1. 扫描 `10-Projects/` 列出所有活跃项目
2. 用 AskUserQuestion 让用户选择要归档的项目

### 2. 确认归档

向用户展示将要归档的内容：

```
即将归档项目：10-Projects/{项目名}/
包含 N 个文件
目标位置：40-Archive/{当前年份}/{项目名}/
```

等待用户确认。

### 3. 执行归档

1. 创建目标目录：`mkdir -p 40-Archive/{year}/{项目名}/`
2. 移动项目：`mv 10-Projects/{项目名}/* 40-Archive/{year}/{项目名}/`
3. 删除空的源目录：`rmdir 10-Projects/{项目名}/`

### 4. 更新导航

1. 在相关 MOC 中，将该项目的链接标记为已归档，或移到"## 归档"章节
2. 读取 `rules/home-sync.md` 更新 Home.md（移除已归档项目的链接）

### 5. 汇报结果

```
已归档：{项目名}
  文件数：N
  归档位置：40-Archive/{year}/{项目名}/
  已更新：Home.md, MOC-xxx.md
```
