---
name: review-commit-push
description: Reviews git changes first, then (only if review passes) commits with a user-provided message and pushes. If review finds issues, block the commit/push and report the potential problems. Use when the user asks to “提交代码/commit/push/提交并推送” and requires a pre-review with zero AI code modifications.
---

# 触发场景

当用户要求“提交代码/commit/push/提交并推送”，且强调 **先审查再提交**、并且 **AI 不能擅自改动任何一行代码** 时，使用本 skill。

## 核心约束（必须遵守）

- **禁止任何代码/文件改动**：在审查与提交全过程中，不得对工作区文件做任何写入/格式化/修复/自动修改（包括但不限于：ApplyPatch、编辑器自动保存、lint --fix、格式化、重排 import）。
- **只允许执行 git 命令** 来获取信息与提交推送（如 `git status`/`git diff`/`git log`/`git add`/`git commit`/`git push`）。
- **提交信息必须来自用户提供的 message**：不得自行生成、改写或补充 message。

## 工作流

### 1) 先审查（只读）

1. 运行提交前审查 skill：`commit-pre-check`
2. 仅基于 **git 当前改动文件** 做检查，并按 `commit-pre-check` 的输出格式列出问题清单（如有）。

### 2) 分支：审查结论决定是否继续

- **若审查发现问题**：
  - **阻塞**：不要执行 `git add` / `git commit` / `git push`
  - 直接把问题清单反馈给用户（文件 + 位置/摘要 + 风险说明 + 建议）
  - 明确告知：需要用户先修复后再继续提交

- **若审查未发现问题**：
  - 进入提交流程（下一节）

### 3) 提交并推送（仅在审查通过后）

1. 再次确认工作区状态（`git status`）与差异（`git diff`），确保与审查时一致
2. `git add` 仅添加当前改动的相关文件（避免误 add 机密文件，如 `.env` 等）
3. 使用用户提供的 message 进行提交（按仓库约定用 HEREDOC 传入 message；message 内容必须逐字一致）
4. `git push` 推送到当前分支的远端
5. `git status` 确认工作区干净且已推送成功

## 输出要求

- 审查阶段：严格按 `commit-pre-check` 的“改动范围/问题列表/无问题/结尾”结构输出
- 提交阶段：只汇报关键信息（提交是否成功、提交 hash、push 是否成功、远端分支）

## 示例触发语句

- “帮我提交代码，message 是：xxx”
- “检查下没问题就 commit 并 push”
- “提交前先审查，不要改任何代码，审查通过再提交推送”

