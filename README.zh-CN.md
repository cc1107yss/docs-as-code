# Docs as Code：文档即代码

[English](./README.md) | [中文](./README.zh-CN.md)

> 像管理代码一样管理知识：用 Markdown 写作，用分支隔离修改，用 Pull Request 讨论和评审，用 Git 保存完整历史。

这是一套适用于**个人与团队**的文档工作流。它可以用于科研、软件项目、产品设计、学习笔记、运营手册，以及任何需要长期维护的知识库。

## 说白了

```text
先写下来 → 在分支中修改 → 用 PR 讨论和评审 → 合并为现役版本 → 用 Git 保留历史
```

Docs-as-code 并非“把 Word 换成 Markdown”这么简单。关键是让重要文档和代码共享同一套生命周期：

1. 文档存放在 Git 仓库中；
2. 重要修改不直接覆盖现役版本；
3. 修改通过 Pull Request 展示差异并接受逐行评论；
4. 决策、任务、讨论和最终文档互相链接；
5. 旧决策不删除，而是标记为已取代，留下可搜索的历史。

## 怎么用

| 你现在面对的事情 | 使用 | 原因 |
| --- | --- | --- |
| 需要说明项目是什么、怎么开始 | `README.md` | 项目的首页和入口 |
| 需要记录当前状态和下一步 | `STATUS.md` | 提供一个现役状态入口 |
| 有明确动作、负责人或完成标准 | **Issue** | 追踪可关闭的工作 |
| 问题还很开放，需要自由交换观点 | **Discussion** | 先探索，不急着承诺方案 |
| 要修改或新增文档 | **Branch + Pull Request** | 隔离修改、展示差异、逐行评审 |
| 要记录一项重要且长期有效的决定 | **RFC / ADR / RFD** | 保存提案、理由、状态和替代历史 |
| 需要查看很多任务的整体进度 | **Project** | 用看板组织 Issues 与 PRs |

简单原则：**讨论不是任务，任务不是结论，结论也不应该只留在评论里。** 让每种对象只承担一种职责，再用链接把它们串起来。

## 标准路径一：修改一份文档

适用于新增指南、修改方案、更新协议或修正文档。

1. 从 `main` 创建一个短期分支，例如 `docs/update-workflow`；
2. 在分支中创建或编辑 Markdown 文件；
3. 提交修改，写清本次改变了什么；
4. 创建 Pull Request，说明目的、影响和待讨论问题；
5. 在 PR 的 **Files changed** 中逐行评论和修改；
6. 达成一致后合并到 `main`；
7. 删除已合并的短期分支。

### GitHub 网页操作

```text
编辑文件或 Add file
→ Create a new branch for this commit
→ Propose changes
→ Create pull request
→ Review changes
→ Ready for review（如果是 Draft）
→ Merge pull request
→ Delete branch
```

小型拼写修正和链接修复可以直接提交到 `main`。会改变含义、流程、接口或结论的修改应走 PR。

## 标准路径二：从会议到结果

会议记录负责保存“当时讨论了什么”，Issue 负责推动工作，最终文档负责保存可复用结论。

```text
组会笔记
→ 提取可执行 ToDo
→ 创建 Issue
→ 调研、设计或实现
→ 在分支中写结果文档
→ PR 评审并合并
→ 在 Issue 中链接结果并关闭
→ 回到会议记录勾选 ToDo
```

一个好的 Issue 至少包含：

- 背景；
- 要回答的问题或要完成的动作；
- 完成标准；
- 负责人（团队使用时）；
- 相关文档、PR 和证据链接。

不要为每个五分钟的小动作创建 Issue。需要多次工作、会产生独立结果、需要协作或容易被遗忘的事项，才值得成为 Issue。

## 标准路径三：从开放讨论到正式决定

当问题尚未收敛时，先用 GitHub Discussions 收集观点。出现候选方案后，再起草编号提案：RFC、ADR 或 RFD 三选一即可，不必同时采用。

```text
Discussion
→ 形成候选方案
→ 起草 RFD-0001
→ PR 逐行讨论
→ Accepted / Rejected
→ 实施并链接相关 Issues 与 PRs
→ 后续被替代时标记 Superseded，不删除旧文档
```

推荐文件名：

```text
rfds/0001-use-docs-as-code.md
rfds/0002-adopt-a-static-site.md
```

推荐状态：

- `draft`：仍在起草；
- `discussion`：正在征求意见；
- `accepted`：已经采纳；
- `rejected`：明确不采用；
- `superseded`：后来被另一份决策取代。

不要因为一项决策已经过时就删除它。更新状态并链接替代方案，让读者能够还原项目为什么改变方向。

## README 驱动开发

在开始实现一个较大的功能、实验或项目之前，先写出它的 README、方案或接口说明：

1. 目标是什么；
2. 谁会使用；
3. 输入和输出是什么；
4. 什么算完成；
5. 有哪些约束和风险。

先通过文档把问题说清楚并达成共识，再投入实现。文档不是完成后的补作业，而是设计工具。

## 个人与团队如何使用

### 个人

- 小修可以直接提交到 `main`；
- 重大决定仍建议开 PR，利用 diff 做一次自我评审；
- 用 Issue 防止任务埋在笔记里；
- 用 RFD 保存“当时为什么这样决定”。

### 团队

- 所有人从分支开始工作；
- 重要修改至少由一名非作者评审；
- 在 PR 中讨论具体文字，在 Discussion 中讨论开放问题；
- 用 `CODEOWNERS` 为关键目录指定维护者；
- 用 GitHub Projects 展示任务整体状态。

## 最小目录

```text
README.md
README.zh-CN.md
STATUS.md
meetings/
notes/
rfds/
```

需要任务模板、自动检查或发布网站时，再逐步增加：

```text
.github/
  ISSUE_TEMPLATE/
  PULL_REQUEST_TEMPLATE.md
  CODEOWNERS
templates/
scripts/
docs/
```

## 七条规则

1. **一个事实只有一个权威版本。** 其他地方只写摘要和链接。
2. **重要修改走 PR。** PR 是讨论空间，不只是合并按钮。
3. **Issue 必须可关闭。** 没有完成标准的开放问题应进入 Discussion。
4. **结论进入文档。** 不让最终答案只存在于聊天、会议或 Issue 评论中。
5. **旧决策不删除。** 标记为 `superseded` 并链接新决策。
6. **原始证据与解释分开。** 文档链接到数据、代码、日志或来源。
7. **流程服务于清晰度。** 小修改保持轻量，重大修改提高评审强度。

## 五分钟开始

- [ ] 创建仓库和 `README.md`；
- [ ] 写清仓库目标、读者和内容边界；
- [ ] 创建第一份会议记录或工作笔记；
- [ ] 把其中一个可执行事项转成 Issue；
- [ ] 从分支修改文档并创建第一个 PR；
- [ ] 评审、合并并删除分支；
- [ ] 在 Issue 中链接结果并关闭任务。

## 指南

- [Markdown 写作速查表](guides/markdown-cheatsheet.md)
- [协作与冲突处理](guides/collaboration-and-conflicts.md)

## 后续建设

- Meeting note、Issue、PR 和 RFD 模板；
- `CODEOWNERS` 示例；
- GitHub Projects 示例；
- Markdown 链接和元数据自动检查；
- MkDocs / Docusaurus 静态站点示例；
- 个人知识库与团队知识库的完整案例。

对本方法的贡献和改进，也应遵循这里描述的流程：分支、Pull Request、评审和合并。
