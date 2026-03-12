---
name: para-manager
description: >
  管理 Obsidian 笔记库的 PARA + MOC 结构。自动整理收件箱、同步 MOC 导航页、
  更新 Home 首页、归档已完成项目、创建新项目/领域/资源、全库健康检查。
  当用户提到整理笔记、整理收件箱、更新 MOC、更新首页、归档项目、新建项目、
  新建领域、新建资源、检查笔记库、笔记管理、PARA、MOC 等关键词时触发此技能。
  即使用户只是简单说"帮我整理一下"或"看看有没有遗漏的笔记"，也应该触发。
metadata:
  tags: obsidian, para, moc, note-management, organization
  category: Note Management
  version: 1.0.0
---

# PARA + MOC 笔记管理器

这个技能帮助用户按照 PARA 方法论管理 Obsidian 笔记库，自动维护 MOC 导航页和 Home 首页。

## 库结构约定

当前库遵循以下固定结构：

```
00-Inbox/           → 新笔记默认落地
10-Projects/        → 有明确目标和截止日期的项目
20-Areas/           → 持续负责的领域（无截止日期）
30-Resources/       → 感兴趣的学习资料和参考
40-Archive/         → 已完成或不再活跃的内容（按年份分子目录）
Extra/              → 支持文件（模板、附件、代码项目）
Home.md             → 库的总入口导航页
```

## MOC 文件映射

每个 MOC 文件负责索引特定目录的内容：

| MOC 文件 | 索引目录 |
|----------|---------|
| `20-Areas/MOC-蜜罐系统.md` | `10-Projects/ms_honeypot-*`, `20-Areas/ms_honeypot/` |
| `30-Resources/MOC-前端开发.md` | `30-Resources/electron/` |
| `30-Resources/MOC-网络技术.md` | `30-Resources/networking/`, `10-Projects/video-*` |
| `30-Resources/MOC-Obsidian.md` | `30-Resources/obsidian/` |

新创建的领域或资源也可以有自己的 MOC，遵循 `MOC-{主题名}.md` 命名。

## 可用命令

根据用户意图，读取对应的 rules 文件并执行：

| 用户意图 | 规则文件 | 说明 |
|---------|---------|------|
| 整理收件箱 / 处理 Inbox | [rules/inbox.md](rules/inbox.md) | 扫描 00-Inbox，引导归档 |
| 更新 MOC / 同步 MOC | [rules/moc-sync.md](rules/moc-sync.md) | 扫描目录并更新 MOC 链接 |
| 更新首页 / 同步 Home | [rules/home-sync.md](rules/home-sync.md) | 根据当前状态更新 Home.md |
| 归档项目 | [rules/archive.md](rules/archive.md) | 移动完成的项目到 Archive |
| 新建项目/领域/资源 | [rules/new-item.md](rules/new-item.md) | 创建新的 PARA 条目 |
| 检查笔记库 / 健康检查 | [rules/review.md](rules/review.md) | 全库完整性和健康检查 |

## 使用方式

1. 根据用户意图判断需要执行哪个命令
2. 读取对应的 rules/*.md 获取详细执行步骤
3. 按规则执行操作，必要时用 AskUserQuestion 与用户交互
4. 操作完成后，如果涉及文件移动或新增，自动触发 moc-sync 和 home-sync

## 通用原则

- 所有文件操作前先确认，避免数据丢失
- wikilink 使用 Obsidian 风格：`[[文件名]]` 或 `[[文件名|显示名]]`
- 移动文件时使用 `mv` 命令（git 会自动追踪）
- 新建的 .md 文件编码必须是 UTF-8
- 操作完成后给出简洁的变更摘要
