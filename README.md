# daily-skill

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

一个只包含 `para-manager` 的 Claude Code plugin，用于管理 Obsidian 笔记库中的 PARA + MOC 结构。

## 功能简介

`para-manager` skill 用于帮助你维护 Obsidian 笔记库，支持：

- 整理 `00-Inbox`
- 同步 MOC 导航页
- 更新 `Home.md`
- 归档已完成项目
- 新建项目 / 领域 / 资源
- 笔记库健康检查

## 插件信息

- 插件名：`daily-skill`
- 作者：`guoxingyong`
- 邮箱：`guoxingyong9627@gmail.com`
- 描述：日常工作总结skill分享

## 目录结构

```text
.
├── .claude-plugin/
│   └── marketplace.json
├── para-manager/
│   ├── SKILL.md
│   └── rules/
│       ├── archive.md
│       ├── home-sync.md
│       ├── inbox.md
│       ├── moc-sync.md
│       ├── new-item.md
│       └── review.md
├── README.md
└── LICENSE
```

## 安装方式

### 前置要求

- 已安装 Claude Code CLI
- 需要使用 Obsidian 的笔记库环境

### 方式一：Plugin Marketplace 安装（推荐）

发布到 Claude Code plugin marketplace 后，可使用以下命令安装：

```text
/plugin marketplace add optimistic9527/myskill
/plugin install daily-skill
```

安装完成后，重启 Claude Code 以加载该 plugin。

### 方式二：手动安装

如果还没有发布到 marketplace，可以直接手动安装 skill：

```bash
# 克隆仓库
git clone https://github.com/optimistic9527/myskill.git

# 复制 para-manager skill 到 Claude Code skills 目录
cp -r myskill/para-manager ~/.claude/skills/
```

复制完成后，重启 Claude Code。

### 方式三：本地作为 plugin 使用

如果你直接在本地以 plugin 目录结构使用本仓库，请确保包含：

- `.claude-plugin/marketplace.json`
- `para-manager/SKILL.md`

然后在 Claude Code 中按 plugin 方式加载该仓库。

## Skill 说明

`para-manager/SKILL.md` 中定义了 skill 的触发词、使用场景和规则入口。

对应规则文件：

- `rules/inbox.md`：整理收件箱
- `rules/moc-sync.md`：同步 MOC
- `rules/home-sync.md`：同步首页
- `rules/archive.md`：归档项目
- `rules/new-item.md`：新建 PARA 条目
- `rules/review.md`：健康检查

## 使用示例

你可以在 Claude Code 中用类似方式触发：

```text
帮我整理一下 Obsidian 收件箱
更新一下 MOC
同步 Home 首页
帮我归档已完成项目
帮我新建一个项目
检查一下我的笔记库有没有遗漏
```

## License

MIT License
