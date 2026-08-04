# Docs as Code

> 像管理代码一样管理知识：用 Markdown 写作，用分支隔离修改，用 Pull Request 讨论和评审，用 Git 保存完整历史。
> Manage knowledge like code: write in Markdown, isolate changes in branches, review through pull requests, and preserve history with Git.

这是一套适用于**个人与团队**的文档工作流。它可以用于科研、软件项目、产品设计、学习笔记、运营手册或任何需要长期维护的知识库。

This is a documentation workflow for **individuals and teams**. It works for research, software, product design, study notes, operations manuals, and any knowledge base that must stay current.

## 一句话理解 / The idea in one sentence

```text
先写下来 → 在分支中修改 → 用 PR 讨论和评审 → 合并为现役版本 → 用 Git 保留历史
Write first → change on a branch → discuss and review in a PR → merge the current version → keep history in Git
```

Docs-as-code 不是“把 Word 换成 Markdown”这么简单。关键是让重要文档和代码共享同一套生命周期：

1. 文档存放在 Git 仓库中；
2. 重要修改不直接覆盖现役版本；
3. 修改通过 Pull Request 展示差异并接受逐行评论；
4. 决策、任务、讨论和最终文档互相链接；
5. 旧决策不删除，而是标记为已取代，留下可搜索的历史。

Docs-as-code is more than replacing Word with Markdown. The important part is giving documentation the same lifecycle as code: versioned files, reviewable changes, linked decisions and tasks, and durable history.

## 先判断该用什么 / Choose the right GitHub object

| 你现在面对的事情 / Situation | 使用 / Use | 原因 / Why |
| --- | --- | --- |
| 需要说明项目是什么、怎么开始 | `README.md` | 项目的首页和入口 / Project landing page |
| 需要记录当前状态和下一步 | `STATUS.md` | 提供一个现役状态入口 / One current status page |
| 有明确动作、负责人或完成标准 | **Issue** | 追踪可关闭的工作 / Track actionable work |
| 问题还很开放，需要自由交换观点 | **Discussion** | 先探索，不急着承诺方案 / Explore before committing |
| 要修改或新增文档 | **Branch + Pull Request** | 隔离修改、展示差异、逐行评审 / Isolate, compare, and review changes |
| 要记录一项重要且长期有效的决定 | **RFC / ADR / RFD** | 保存提案、理由、状态和替代历史 / Preserve proposal, rationale, status, and history |
| 需要查看很多任务的整体进度 | **Project** | 用看板组织 Issues 与 PRs / Organize issues and PRs on a board |

简单原则：**讨论不是任务，任务不是结论，结论也不应该只留在评论里。** 让每种对象只承担一种职责，再用链接把它们串起来。

Simple rule: **a discussion is not a task, a task is not a durable conclusion, and a conclusion should not live only in comments.** Give each object one job, then connect them with links.

## 标准路径一：修改一份文档 / Change a document

适用于新增指南、修改方案、更新协议或修正文档。

1. 从 `main` 创建一个短期分支，例如 `docs/update-workflow`；
2. 在分支中创建或编辑 Markdown 文件；
3. 提交修改，写清本次改变了什么；
4. 创建 Pull Request，说明目的、影响和待讨论问题；
5. 在 PR 的 **Files changed** 中逐行评论和修改；
6. 达成一致后合并到 `main`；
7. 删除已合并的短期分支。

For any meaningful document change: create a short-lived branch, edit and commit there, open a pull request, review the diff, merge into `main`, and delete the merged branch.

### GitHub 网页操作 / GitHub web flow

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

Tiny typo and link fixes may go directly to `main`. Changes to meaning, process, interfaces, or conclusions should use a pull request.

### 多人同时编辑与冲突 / Concurrent edits and conflicts

GitHub 不是实时共同编辑器。如果两个人同时修改同一文件的同一段落，合并时可能出现冲突。这不是数据丢失，而是 Git 要求人工确认两边内容应该如何组合。

GitHub is not a real-time collaborative editor. If two people edit the same part of a file at the same time, Git may report a merge conflict. A conflict is a request for a human decision about how to combine both changes.

减少冲突：

- 重要修改先创建 Draft PR，让别人知道文件正在修改；
- 尽量按文件或目录分工，避免多人同时编辑同一篇长文档；
- 组会记录按日期拆成独立文件，例如 `meetings/YYYY-MM-DD-topic.md`；
- 为高频修改的总览文档指定维护者，其他人通过 Issue 或 PR 提议修改；
- 不要同时在网页和本地修改同一个文件后再互相覆盖。

To reduce conflicts:

- Open a draft PR early so others can see that a file is being edited;
- Divide work by file or directory where possible;
- Store meeting notes as separate date-based files;
- Assign an owner to frequently edited overview documents;
- Do not edit the same file independently in the web UI and a local clone.

如果 PR 出现冲突：

1. 打开 PR 中的 **Resolve conflicts**；
2. 阅读两边的修改，不要机械地全部选择 “ours” 或 “theirs”；
3. 保留双方有价值的内容，删除 `<<<<<<<`、`=======`、`>>>>>>>` 冲突标记；
4. 点击 **Mark as resolved** 并提交；
5. 重新检查渲染后的文档，再合并 PR。

If a PR has conflicts, use **Resolve conflicts**, read both versions, preserve the useful parts, remove the conflict markers, mark the files resolved, and review the rendered document before merging.

简单规则 / Simple rule:

> 同一文件同一时间尽量只由一个人负责修改；其他人通过 Issue 或 PR 评论提出意见。
> Prefer one active editor per file; everyone else contributes through issues or PR comments.

## 标准路径二：从会议到结果 / From meeting to result

会议记录负责保存“当时讨论了什么”，Issue 负责推动工作，最终文档负责保存可复用结论。

```text
Meeting note
→ 提取可执行 ToDo
→ 创建 Issue
→ 调研、设计或实现
→ 在分支中写结果文档
→ PR 评审并合并
→ 在 Issue 中链接结果并关闭
→ 回到会议记录勾选 ToDo
```

一个好的 Issue 至少包含：

- 背景 / Context
- 要回答的问题或要完成的动作 / Question or action
- 完成标准 / Definition of done
- 负责人（团队使用时）/ Owner when working as a team
- 相关文档、PR 和证据链接 / Links to documents, PRs, and evidence

不要为每个五分钟的小动作创建 Issue。需要多次工作、会产生独立结果、需要协作或容易被遗忘的事项，才值得成为 Issue。

Do not create an issue for every five-minute task. Use issues for work that spans multiple steps, produces a result, needs coordination, or could otherwise be forgotten.

## 标准路径三：从开放讨论到正式决定 / From discussion to decision

当问题尚未收敛时，先用 GitHub Discussions 收集观点。出现候选方案后，再起草编号提案：RFC、ADR 或 RFD 三选一即可，不必同时采用。

Use GitHub Discussions while the question is still open. Once a concrete option emerges, write a numbered proposal. Choose one convention—RFC, ADR, or RFD—rather than using all three.

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

Never delete an accepted or superseded decision merely because it is no longer current. Update its status and link to the replacement so readers can reconstruct why the project changed direction.

## README 驱动 / README-driven work

在开始实现一个较大的功能、实验或项目之前，先写出它的 README、方案或接口说明：

1. 目标是什么；
2. 谁会使用；
3. 输入和输出是什么；
4. 什么算完成；
5. 有哪些约束和风险。

先通过文档把问题说清楚并达成共识，再投入实现。文档不是完成后的补作业，而是设计工具。

Before building a substantial feature, experiment, or project, write its README, proposal, or interface first. Agree on the goal, audience, inputs, outputs, completion criteria, and constraints before implementation. Documentation is a design tool, not cleanup work.

## 个人与团队如何使用 / Individual and team modes

### 个人 / Individual

- 小修可以直接提交到 `main`；
- 重大决定仍建议开 PR，利用 diff 做一次自我评审；
- 用 Issue 防止任务埋在笔记里；
- 用 RFD 保存“当时为什么这样决定”。

Solo users can self-review important changes through PRs, use issues to keep tasks out of notes, and use decision records to preserve rationale.

### 团队 / Team

- 所有人从分支开始工作；
- 重要修改至少由一名非作者评审；
- 在 PR 中讨论具体文字，在 Discussion 中讨论开放问题；
- 用 `CODEOWNERS` 为关键目录指定维护者；
- 用 GitHub Projects 展示任务整体状态。

Teams should require branch-based work for meaningful changes, at least one non-author review for important documents, and clear ownership for critical areas.

## 最小目录 / Minimal structure

不要一开始建立几十个空目录。下面的结构足够启动：

```text
README.md
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

Start small. Add templates, validation scripts, and a static site only when the repository has enough contributors or documents to justify them.

## 七条规则 / Seven rules

1. **一个事实只有一个权威版本。** 其他地方只写摘要和链接。<br>
   **One fact has one source of truth.** Other places contain summaries and links.
2. **重要修改走 PR。** PR 是讨论空间，不只是合并按钮。<br>
   **Use PRs for meaningful changes.** A PR is a discussion space, not merely a merge button.
3. **Issue 必须可关闭。** 没有完成标准的开放问题应进入 Discussion。<br>
   **Issues must be closable.** Open-ended questions belong in Discussions.
4. **结论进入文档。** 不让最终答案只存在于聊天、会议或 Issue 评论中。<br>
   **Move conclusions into documents.** Do not leave final answers only in chats or comments.
5. **旧决策不删除。** 标记为 `superseded` 并链接新决策。<br>
   **Do not delete old decisions.** Mark them `superseded` and link the replacement.
6. **原始证据与解释分开。** 文档链接到数据、代码、日志或来源。<br>
   **Separate evidence from interpretation.** Link documents to data, code, logs, or sources.
7. **流程服务于清晰度。** 小修改保持轻量，重大修改提高评审强度。<br>
   **Process serves clarity.** Keep small changes light and review important changes more carefully.

## 五分钟开始 / Start in five minutes

- [ ] 创建仓库和 `README.md`
- [ ] 写清仓库目标、读者和内容边界
- [ ] 创建第一份会议记录或工作笔记
- [ ] 把其中一个可执行事项转成 Issue
- [ ] 从分支修改文档并创建第一个 PR
- [ ] 评审、合并并删除分支
- [ ] 在 Issue 中链接结果并关闭任务

If you complete this checklist once, you have already practiced the core docs-as-code loop.

## 下一步 / Roadmap

- Meeting note、Issue、PR 和 RFD 模板
- `CODEOWNERS` 示例
- GitHub Projects 示例
- Markdown 链接和元数据自动检查
- MkDocs / Docusaurus 静态站点示例
- 个人知识库与团队知识库的完整案例

Contributions and refinements should follow the same workflow described here: branch, pull request, review, and merge.
