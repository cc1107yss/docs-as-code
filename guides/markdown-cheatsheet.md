# Markdown 写作速查表

这份速查表面向刚开始使用 GitHub Markdown 的个人和团队成员。复制下面的示例即可开始写作。

## 1. 标题 / Headings

```markdown
# 一级标题
## 二级标题
### 三级标题
```

## 2. 强调文字 / Emphasis

```markdown
**粗体**
*斜体*
***粗体斜体***
~~删除线~~
```

## 3. 段落和换行 / Paragraphs and line breaks

空一行表示新段落。需要强制换行时，可使用 `<br>`：

```markdown
这是第一段。

这是第二段。

上一行<br>
下一行
```

## 4. 列表 / Lists

### 无序列表

```markdown
- 第一项
- 第二项
  - 子项目
  - 另一个子项目
```

### 有序列表

```markdown
1. 第一步
2. 第二步
3. 第三步
```

### 任务清单 / Task list

```markdown
- [ ] 尚未完成
- [x] 已完成
```

## 5. 链接 / Links

```markdown
[GitHub 官网](https://github.com)
```

同一仓库内的文件建议使用相对链接：

```markdown
[项目状态](../STATUS.md)
```

GitHub Issue 或 Pull Request 可以使用完整链接：

```markdown
[Issue #2](https://github.com/cc1107yss/llm-post-training-research/issues/2)
[Pull Request #1](https://github.com/cc1107yss/docs-as-code/pull/1)
```

链接必须使用单层格式：

```markdown
[显示文字](链接)
```

不要嵌套成：

```markdown
[显示文字]([另一个链接](链接))
```

## 6. 图片 / Images

```markdown
![图片说明](https://example.com/image.png)
```

## 7. 引用 / Blockquotes

```markdown
> 这是一段引用。
>
> 引用可以有多行。
```

## 8. 行内代码和代码块 / Code

行内代码使用一对反引号：

```markdown
使用 `README.md` 文件作为项目入口。
```

多行代码使用三个反引号，并尽量注明语言：

````markdown
```python
print("Hello")
```
````

常见语言标记包括 `python`、`javascript`、`bash`、`json`、`yaml` 和 `markdown`。

## 9. 表格 / Tables

```markdown
| 项目 | 状态 | 负责人 |
| --- | --- | --- |
| 文献调研 | 进行中 | Clara |
| 实验复现 | 未开始 | Alex |
```

设置对齐方式：

```markdown
| 左对齐 | 居中 | 右对齐 |
| :--- | :---: | ---: |
| A | B | C |
```

## 10. 分隔线 / Horizontal rule

```markdown
---
```

## 11. 折叠内容 / Collapsible sections

GitHub 支持使用 HTML 创建折叠区域：

```html
<details>
<summary>点击展开</summary>

这里是隐藏内容。

</details>
```

## 12. Mermaid 图 / Mermaid diagrams

GitHub 支持 Mermaid 流程图：

````markdown
```mermaid
flowchart LR
    A[组会笔记] --> B[创建 Issue]
    B --> C[建立分支]
    C --> D[创建 PR]
    D --> E[评审并合并]
```
````

## 13. HTML 注释 / Comments

不会显示在页面上的注释：

```html
<!-- 这段内容不会显示在页面上 -->
```

## 14. 常用文档模板 / Reusable document skeleton

```markdown
# 文档标题

## 背景

为什么要写这份文档。

## 目标

这份文档要解决什么问题。

## 内容

正文内容。

## 结论

最终结论或当前状态。

## 相关链接

- [相关 Issue](链接)
- [相关 PR](链接)
- [相关文件](链接)
```

## 15. GitHub 文档的推荐组合 / Recommended combination

```markdown
# 任务名称

## 背景

任务为什么产生。

## ToDo

- [ ] 第一个任务
- [ ] 第二个任务
- [x] 已完成任务

## 结论

当前结论。

## 相关资料

- [论文](链接)
- [代码](链接)
- [Issue](链接)
```

## 写作提醒 / Writing reminders

- 每份文档只保留一个明确主题；
- 标题层级按顺序使用，不要从 `#` 直接跳到 `###`；
- 重要结论附上来源、Issue、PR 或实验链接；
- 同一仓库内优先使用相对链接，外部资源使用完整 URL；
- 提交前打开 GitHub 的 **Preview** 检查列表、表格、链接和代码块；
- 先写清楚目标和完成标准，再开始执行。
