# Docs as Code

[English](./README.md) | [中文](./README.zh-CN.md)

> Manage knowledge like code: write in Markdown, isolate changes in branches, review through pull requests, and preserve history with Git.

Docs-as-code is a documentation workflow for individuals and teams. It works for research, software, product design, study notes, operations manuals, and any knowledge base that must stay current.

## The idea in one sentence

```text
Write first → change on a branch → discuss and review in a PR → merge the current version → keep history in Git
```

Docs-as-code is more than replacing Word with Markdown. The important part is giving documentation the same lifecycle as code:

1. Store documents in a Git repository;
2. Do not silently overwrite the current version with important changes;
3. Use Pull Requests to show diffs and discuss changes line by line;
4. Link decisions, tasks, discussions, and final documents;
5. Keep old decisions as history instead of deleting them.

## Choose the right GitHub object

| Situation | Use | Why |
| --- | --- | --- |
| Explain what a project is and how to start | `README.md` | Project landing page |
| Record current status and next steps | `STATUS.md` | One current status page |
| Track work with an owner or completion criteria | **Issue** | Actionable work that can be closed |
| Explore an open-ended question | **Discussion** | Exchange ideas before committing |
| Add or change a document | **Branch + Pull Request** | Isolate, compare, and review changes |
| Record an important long-lived decision | **RFC / ADR / RFD** | Preserve rationale and history |
| See many tasks at once | **Project** | Organize Issues and PRs on a board |

Simple rule: **a discussion is not a task, a task is not a durable conclusion, and a conclusion should not live only in comments.** Give each object one job, then connect them with links.

## Workflow 1: Change a document

For a new guide, revised plan, updated protocol, or correction:

1. Create a short-lived branch from `main`, such as `docs/update-workflow`;
2. Create or edit the Markdown file on that branch;
3. Commit with a message that explains the change;
4. Open a Pull Request describing purpose, impact, and open questions;
5. Discuss the diff line by line in **Files changed**;
6. Merge into `main` once review is complete;
7. Delete the merged branch.

### GitHub web flow

```text
Edit a file or choose Add file
→ Create a new branch for this commit
→ Propose changes
→ Create pull request
→ Review changes
→ Ready for review (if Draft)
→ Merge pull request
→ Delete branch
```

Tiny typo and link fixes may go directly to `main`. Changes to meaning, process, interfaces, or conclusions should use a pull request.

## Workflow 2: From meeting to result

A meeting note records what was discussed. An Issue drives the work. A final document preserves the reusable conclusion.

```text
Meeting note
→ Extract an actionable ToDo
→ Create an Issue
→ Research, design, or implement
→ Write the result on a branch
→ Review and merge the PR
→ Link the result in the Issue and close it
→ Check off the ToDo in the meeting note
```

A useful Issue contains context, the question or action, definition of done, an owner when needed, and links to documents, PRs, and evidence. Do not create an Issue for every five-minute task.

## Workflow 3: From discussion to decision

Use GitHub Discussions while the question is still open. Once a concrete option emerges, write a numbered proposal. Choose one convention—RFC, ADR, or RFD—instead of using all three.

```text
Discussion → candidate options → RFD-0001 → PR discussion
→ Accepted / Rejected → link Issues and PRs
→ mark Superseded if a later decision replaces it
```

Suggested filenames and statuses:

```text
rfds/0001-use-docs-as-code.md
rfds/0002-adopt-a-static-site.md
```

- `draft`: still being written;
- `discussion`: collecting feedback;
- `accepted`: adopted;
- `rejected`: explicitly not adopted;
- `superseded`: replaced by a later decision.

Never delete an accepted or superseded decision merely because it is no longer current. Update its status and link to the replacement.

## README-driven work

Before building a substantial feature, experiment, or project, write its README, proposal, or interface first:

1. What is the goal?
2. Who will use it?
3. What are the inputs and outputs?
4. What counts as complete?
5. What are the constraints and risks?

Agree on the problem through documentation before investing in implementation. Documentation is a design tool, not cleanup work.

## Individual and team modes

### Individual

- Small fixes may go directly to `main`;
- Use PRs for important decisions as a self-review through the diff;
- Use Issues to keep tasks out of notes;
- Use RFDs to preserve why a decision was made.

### Team

- Everyone starts meaningful work on a branch;
- Important changes receive at least one non-author review;
- Discuss exact wording in PRs and open questions in Discussions;
- Use `CODEOWNERS` to assign maintainers to critical paths;
- Use GitHub Projects to show overall task status.

## Minimal structure

```text
README.md
README.zh-CN.md
STATUS.md
meetings/
notes/
rfds/
```

Add templates, validation scripts, and a static site only when they are needed:

```text
.github/
  ISSUE_TEMPLATE/
  PULL_REQUEST_TEMPLATE.md
  CODEOWNERS
templates/
scripts/
docs/
```

## Seven rules

1. **One fact has one source of truth.** Other places contain summaries and links.
2. **Use PRs for meaningful changes.** A PR is a discussion space, not merely a merge button.
3. **Issues must be closable.** Open-ended questions belong in Discussions.
4. **Move conclusions into documents.** Do not leave final answers only in chats or comments.
5. **Do not delete old decisions.** Mark them `superseded` and link the replacement.
6. **Separate evidence from interpretation.** Link documents to data, code, logs, or sources.
7. **Process serves clarity.** Keep small changes light and review important changes more carefully.

## Start in five minutes

- [ ] Create a repository and `README.md`;
- [ ] State the repository's purpose, audience, and boundaries;
- [ ] Create a first meeting note or working note;
- [ ] Turn one actionable item into an Issue;
- [ ] Change a document on a branch and open a PR;
- [ ] Review, merge, and delete the branch;
- [ ] Link the result in the Issue and close the task.

## Guides

- [Markdown writing cheat sheet](guides/markdown-cheatsheet.md)
- [Collaboration and conflict handling](guides/collaboration-and-conflicts.md)

## Roadmap

- Meeting note, Issue, PR, and RFD templates;
- `CODEOWNERS` example;
- GitHub Projects example;
- Markdown link and metadata checks;
- MkDocs / Docusaurus static-site example;
- Complete individual and team examples.

Contributions and refinements should follow the same workflow described here: branch, pull request, review, and merge.
