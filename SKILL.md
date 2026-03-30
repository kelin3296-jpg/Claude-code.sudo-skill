---
name: sudo
description: Explicit privileged workflow for Claude Code with backup, audit logs, diff, and guarded rollback helpers. Use when the user invokes /sudo, /sudo exit, /sudo history, /sudo rollback, or asks to work on sensitive files or system locations with reversible change tracking. 适用于用户输入 /sudo、/sudo exit、/sudo history、/sudo rollback，或需要以可回滚方式处理敏感文件、系统路径和高风险修改的场景。
---

# /sudo

Use this skill for **explicit** privileged workflows in Claude Code.

This skill does **not** automatically bypass Claude Code sandboxing, and it does **not** automatically modify bash tool parameters. Its job is to track state, backups, diffs, and rollback metadata so that sensitive changes are reversible and auditable.

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

- Roll back only the most recent active operations.
- Refuse destructive rollback when the current file object no longer matches the recorded snapshot.
- Treat `/sudo diff` as the first inspection tool before rollbacking risky changes.
- Still ask for extra confirmation before destructive shell commands such as `rm -rf`, even inside `/sudo`.

## 中文说明

这是一个 **显式特权工作流**，不是“自动提权模式”。

它不会自动绕过 Claude Code 的沙箱，也不会自动帮你改 bash 参数；它真正负责的是：记录状态、备份、diff 和可审计的回滚元数据。

### 高风险操作前

- 修改文件前：`python3 ~/.claude/skills/sudo/sudo.py log-modify <path>`
- 修改完成后：`python3 ~/.claude/skills/sudo/sudo.py finalize-modify <path>`
- 删除文件前：`python3 ~/.claude/skills/sudo/sudo.py log-delete <path>`
- 创建文件后：`python3 ~/.claude/skills/sudo/sudo.py log-create <path>`
- 移动/重命名完成后：`python3 ~/.claude/skills/sudo/sudo.py log-move <src> <dst>`
- chmod 完成后：`python3 ~/.claude/skills/sudo/sudo.py log-chmod <path> <旧权限八进制> <新权限八进制>`

### 使用原则

- `/sudo` 只意味着进入了“显式特权工作流”，不是自动提权。
- 敏感变更完成后，先看 `/sudo diff`，再决定是否回滚。
- 如果当前对象已经和记录时不一致，回滚应拒绝执行 destructive 操作。
- 即使在 `/sudo` 下，`rm -rf` 这类命令仍需要额外确认。
