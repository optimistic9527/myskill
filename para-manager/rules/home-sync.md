---
name: home-sync
description: 根据当前库状态更新 Home.md 首页
---

# Home 首页同步

## 执行步骤

### 1. 收集当前状态

并行扫描以下内容：

- `10-Projects/` 下的所有子目录（每个子目录 = 一个活跃项目）
- `20-Areas/` 下的所有 MOC 文件和子目录
- `30-Resources/` 下的所有 MOC 文件
- `40-Archive/` 下的年份目录

### 2. 读取现有 Home.md

读取当前 `Home.md` 内容，了解现有结构。

### 3. 重新生成 Home.md

按以下模板生成新的 Home.md 内容：

```markdown
# Home

欢迎回来！这是你的知识库总入口。

## 导航

### 收件箱

- [[00-Inbox/]] — 新笔记落地处

### 项目 (Projects)

{对 10-Projects/ 下每个子目录生成一条链接}
- [[10-Projects/{目录名}/|{可读名称}]]

### 领域 (Areas)

{列出 20-Areas/ 下的 MOC 文件}
- [[MOC-xxx]] — {描述}
{列出 20-Areas/ 下不在 MOC 中但有实际内容的子目录}

### 资源 (Resources)

{列出 30-Resources/ 下的 MOC 文件}
- [[MOC-xxx]] — {描述}

### 归档 (Archive)

{列出 40-Archive/ 下的年份目录}
- [[40-Archive/{年份}/]] — {年份}年归档文件
```

### 4. 更新文件

将新内容写入 Home.md，并向用户展示变更摘要。
