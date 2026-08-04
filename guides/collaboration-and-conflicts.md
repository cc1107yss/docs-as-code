# 协作与冲突处理

## Collaboration and conflict handling

GitHub 适合版本化协作，但不是 Google Docs 那种实时共同编辑器。两个人同时修改同一文件的同一段落时，合并可能产生冲突。冲突不代表内容丢失，而是 Git 要求人工决定两边修改如何组合。

GitHub is built for versioned collaboration, not real-time co-editing. When two people edit the same part of a file, Git may report a merge conflict. A conflict is not data loss; it is a request for a human decision about how to combine both changes.

## 如何减少冲突 / Prevent conflicts

- 重要修改尽早创建 Draft PR，让其他人知道文件正在修改；
- 尽量按文件或目录分工，避免多人同时编辑同一篇长文档；
- 组会记录按日期拆成独立文件，例如 `meetings/YYYY-MM-DD-topic.md`；
- 为频繁修改的总览文档指定维护者，其他人通过 Issue 或 PR 提议修改；
- 同一时间不要在网页和本地分别修改同一个文件；
- 修改前先查看该文件是否已有未合并的 PR。

To reduce conflicts:

- Open a draft PR early so others can see that a file is being edited;
- Divide work by file or directory where possible;
- Store meeting notes as separate date-based files;
- Assign an owner to frequently edited overview documents;
- Do not edit the same file independently in the web UI and a local clone;
- Check for existing open PRs before starting a change.

## 推荐的协作分工 / Recommended coordination

```text
一个人负责修改文件
其他人通过 Issue、Discussion 或 PR 评论提出意见
修改者集中处理意见并更新 PR
```

```text
One person edits a file
Others contribute through Issues, Discussions, or PR comments
The editor incorporates the agreed changes into the PR
```

README、STATUS、路线图等高频总览文档最好有明确维护者。多人共同写作时，可以把内容拆成多个相互链接的文件，而不是让所有人同时编辑一篇超长文档。

## 出现冲突时怎么处理 / Resolve a conflict

当 PR 页面显示冲突时：

1. 打开 PR 中的 **Resolve conflicts**；
2. 阅读冲突文件两边的修改；
3. 判断哪些内容应保留、合并或删除；
4. 删除 Git 自动插入的冲突标记；
5. 点击 **Mark as resolved**；
6. 提交解决结果；
7. 重新检查 GitHub 渲染后的 Markdown，再合并 PR。

When a PR reports conflicts:

1. Open **Resolve conflicts**;
2. Read both versions of the conflicted file;
3. Decide what to keep, combine, or remove;
4. Remove Git's conflict markers;
5. Click **Mark as resolved**;
6. Commit the resolution;
7. Review the rendered Markdown again before merging.

冲突标记通常长这样：

```text
&lt;&lt;&lt;&lt;&lt;&lt;&lt; HEAD
当前分支中的内容
&#61;&#61;&#61;&#61;&#61;&#61;&#61;
另一个分支中的内容
&gt;&gt;&gt;&gt;&gt;&gt;&gt; other-branch
```

解决后，文件中不能残留 `<<<<<<<`、`=======` 或 `>>>>>>>`。

Do not blindly choose “ours” or “theirs”. Preserve the meaning of both changes where appropriate, and never merge a document you have not re-read after resolving the conflict.

## 特殊情况 / Special cases

### 组会记录 / Meeting notes

不要让所有人长期共同编辑一个 `meeting-notes.md`。建议每次会议单独建文件：

```text
meetings/2026-08-04-group-meeting.md
meetings/2026-08-11-group-meeting.md
```

### 状态总览 / Status pages

`STATUS.md` 只能有一个现役版本。多人需要修改时，先在 Issue 或 PR 中协调，由维护者合并最终版本。

### 长期决策 / Durable decisions

重大决策使用编号的 RFC、ADR 或 RFD。不要通过多人同时改一份决策稿来“抢答”；先在 Discussion 或 Draft PR 中讨论，再由提案维护者整理。

## 最简单的规则 / The simplest rule

> 同一文件同一时间尽量只由一个人负责修改；其他人通过 Issue、Discussion 或 PR 评论提出意见。
>
> Prefer one active editor per file; everyone else contributes through issues, discussions, or pull request comments.
