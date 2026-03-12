---
name: review
description: 全库健康检查，发现孤立文件、死链、空目录等问题
---

# 全库健康检查

## 检查项

依次执行以下 5 项检查，汇总生成报告。

### 1. 孤立文件检查

**目标**：找出不在任何 MOC 中被引用的 .md 文件。

**步骤**：
1. 收集所有 MOC 文件（`**/MOC-*.md`）和 `Home.md` 中的 wikilink
2. 扫描 `10-Projects/`、`20-Areas/`、`30-Resources/` 下所有 .md 文件
3. 排除 MOC 文件自身和 README.md
4. 比对：如果某个 .md 文件未被任何 MOC 或 Home.md 引用，标记为孤立

### 2. 死链检查

**目标**：找出 MOC 和 Home.md 中引用了但实际不存在的文件。

**步骤**：
1. 提取所有 MOC 文件和 Home.md 中的 `[[xxx]]` wikilink
2. 对每个 wikilink，检查是否存在对应的 .md 文件
3. 不存在的标记为死链

### 3. 空目录检查

**目标**：找出没有任何 .md 文件的目录。

**步骤**：
1. 扫描 PARA 四个顶级目录下的所有子目录
2. 如果某个子目录中没有 .md 文件，标记为空目录
3. 排除 `Extra/Attachments/`、`Extra/Templates/`（这些空目录是预期的）

### 4. Frontmatter 检查

**目标**：找出缺少 YAML frontmatter 的笔记。

**步骤**：
1. 扫描所有 .md 文件（排除 MOC 和 Home.md）
2. 检查文件是否以 `---` 开头
3. 缺少 frontmatter 的文件列出，并按目录分组

### 5. Inbox 积压检查

**目标**：检查收件箱中是否有未处理的笔记。

**步骤**：
1. 扫描 `00-Inbox/` 下所有 .md 文件
2. 列出文件名和修改时间
3. 如果有文件，提示用户运行"整理收件箱"

## 输出报告

按以下格式输出：

```markdown
## 笔记库健康检查报告

### 总览
- 总文件数：X
- 孤立文件：X 个
- 死链：X 个
- 空目录：X 个
- 缺 Frontmatter：X 个
- Inbox 积压：X 个

### 详情

#### 孤立文件（未被 MOC 引用）
- `path/to/file.md`

#### 死链（引用了不存在的文件）
- `[[不存在的文件]]` ← 出现在 MOC-xxx.md

#### 空目录
- `20-Areas/xxx/`

#### 缺少 Frontmatter
- `30-Resources/electron/01-main-process.md`

#### Inbox 积压
- `00-Inbox/待处理笔记.md`（N 天前）

### 建议操作
{根据检查结果给出具体建议}
```

## 修复建议

报告生成后，用 AskUserQuestion 询问用户是否要自动修复某些问题：
- 死链：可以从 MOC 中移除
- 空目录：可以删除
- Inbox 积压：可以启动 inbox 归档流程
