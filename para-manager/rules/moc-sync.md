---
name: moc-sync
description: 扫描目录并自动更新 MOC 文件中的 wikilink 列表
---

# MOC 同步

## MOC 与目录映射

```
MOC-蜜罐系统.md     ↔ 10-Projects/ms_honeypot-*, 20-Areas/ms_honeypot/
MOC-前端开发.md      ↔ 30-Resources/electron/
MOC-网络技术.md      ↔ 30-Resources/networking/, 10-Projects/video-*
MOC-Obsidian.md     ↔ 30-Resources/obsidian/
```

如果存在其他 MOC 文件（`MOC-*.md`），也应扫描并处理。

## 执行步骤

### 1. 收集所有 MOC 文件

用 Glob 搜索 `**/MOC-*.md`，获取所有 MOC 文件列表。

### 2. 对每个 MOC 执行同步

对每个 MOC 文件：

1. **读取 MOC 当前内容**，提取所有已存在的 wikilink（`[[xxx]]` 格式）
2. **扫描对应目录**中的所有 .md 文件（递归扫描子目录）
3. **比对差异**：
   - **新增文件**：目录中存在但 MOC 中未链接的文件
   - **缺失文件**：MOC 中链接了但目录中不存在的文件

### 3. 报告差异

如果有差异，向用户展示：

```
MOC-蜜罐系统.md 需要更新：
  新增 2 个文件：
    + new-feature-design.md
    + api-refactor-spec.md
  缺失 1 个链接（文件已不存在）：
    - old-deprecated-doc.md
```

### 4. 执行更新

- 对于**新增文件**：在 MOC 的合适章节末尾添加 `- [[文件名]]` 链接
  - 根据文件所在的子目录判断应该放在哪个章节
  - 如果无法确定章节，放在 MOC 末尾新建一个"## 未分类"章节
- 对于**缺失链接**：从 MOC 中移除该行
- 保留 MOC 中用户手写的描述文字和结构，只增删链接条目

### 5. 确认方式

- 如果变更较少（≤5 处），直接执行并告知用户
- 如果变更较多（>5 处），先展示变更计划，用 AskUserQuestion 确认后再执行
