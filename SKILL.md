---
name: sudo
description: Explicit privileged workflow for Claude Code that reduces the anxiety around sensitive file edits by keeping backup, audit logs, diff, and guarded rollback helpers. Use when the user invokes /sudo, /sudo exit, /sudo history, /sudo rollback, or needs a reversible workflow for sensitive files and system paths. 适用于用户输入 /sudo、/sudo exit、/sudo history、/sudo rollback，或需要以可回滚方式处理敏感文件、系统路径和高风险修改的场景。
---

# /sudo

Use this skill when the user wants a `/sudo`-style workflow for sensitive edits, but also wants a clear undo story.

## Why this skill exists

The stressful part of privileged edits is usually not the command. It is the fear that a risky file change, deletion, move, or permission update will be hard to unwind later. This skill exists to remove that hesitation.

## What problem it solves

- users want a familiar `/sudo` mental model
- sensitive paths need auditable change tracking
- shell history alone is not a rollback plan
- privileged edits feel safer when there is a logged fallback path

## Safety net

If something feels wrong after a risky change, the fallback path is:

1. inspect `/sudo diff`
2. review `/sudo history`
3. roll back the newest active change when object validation still matches
4. inspect `~/.claude/sudo-backups/` and `~/.claude/sudo-logs/` for manual recovery context

This skill does **not** automatically bypass Claude Code sandboxing, and it does **not** automatically modify bash tool parameters. Its job is to track state, backups, diffs, and rollback metadata so that sensitive changes are reversible and auditable.

For installation help and copy-paste installer prompts, see the repository README.

## Command mapping

- `/sudo` -> `python3 ~/.claude/skills/sudo/sudo.py enter`
- `/sudo exit` -> `python3 ~/.claude/skills/sudo/sudo.py exit`
- `/sudo status` -> `python3 ~/.claude/skills/sudo/sudo.py status`
- `/sudo history [n]` -> `python3 ~/.claude/skills/sudo/sudo.py history [n]`
- `/sudo rollback [n]` -> `python3 ~/.claude/skills/sudo/sudo.py rollback [n]`
- `/sudo diff [path|n]` -> `python3 ~/.claude/skills/sudo/sudo.py diff [path|n]`
- `/sudo backup-clean` -> `python3 ~/.claude/skills/sudo/sudo.py clean --days 7`
- `/sudo backup-purge` -> `python3 ~/.claude/skills/sudo/sudo.py purge`

## Before a sensitive change

### Modify a file

1. Run `python3 ~/.claude/skills/sudo/sudo.py log-modify <path>` before the edit.
2. Perform the edit.
3. Run `python3 ~/.claude/skills/sudo/sudo.py finalize-modify <path>` after the edit.

### Delete a file

1. Run `python3 ~/.claude/skills/sudo/sudo.py log-delete <path>` before deletion.
2. Delete the file.

### Create a file

1. Create the file.
2. Run `python3 ~/.claude/skills/sudo/sudo.py log-create <path>` after creation.

### Move or rename a file

1. Move the file.
2. Run `python3 ~/.claude/skills/sudo/sudo.py log-move <src> <dst>` after the move completes.

### Change permissions

1. Capture the old mode.
2. Run the chmod.
3. Run `python3 ~/.claude/skills/sudo/sudo.py log-chmod <path> <old_mode_octal> <new_mode_octal>`.

## Rollback rules

- roll back only the most recent active operations
- refuse destructive rollback when the current file object no longer matches the recorded snapshot
- treat `/sudo diff` as the first inspection tool before rollbacking risky changes
- still ask for extra confirmation before destructive shell commands such as `rm -rf`, even inside `/sudo`

## 中文说明

这是一个 **显式特权工作流**，不是“自动提权模式”。

### 背景与痛点

用户担心的通常不是命令本身，而是高风险修改之后有没有明确兜底：

- 敏感文件改坏了怎么撤回
- 系统路径动了之后如何留痕
- shell history 不足以承担 rollback 的责任

### 它能解决什么问题

- 给 `/sudo` 这类高风险修改补上一条可追溯、可回滚的后路
- 在修改前记录备份，在修改后保留日志与 diff
- 用对象校验来阻止不安全的 destructive rollback

### 兜底方案

如果改完之后不放心，优先：

1. 看 `/sudo diff`
2. 查 `/sudo history`
3. 在对象仍匹配时回滚最近活跃操作
4. 必要时检查 `~/.claude/sudo-backups/` 和 `~/.claude/sudo-logs/`

它不会自动绕过 Claude Code 的沙箱，也不会自动帮你改 bash 参数；它真正负责的是：记录状态、备份、diff 和可审计的回滚元数据，让用户在进入特权模式时少一些后顾之忧。
