# Claude Code Sudo Skill

面向 Claude Code 的显式特权工作流，用备份、日志、diff 和安全回滚来降低敏感文件修改时的后顾之忧。

## 功能特性

- 🔄 **可回滚** - 所有修改都有备份，支持一键回滚
- 📝 **操作日志** - 完整记录所有文件变更
- 🔍 **Diff 查看** - 修改前后对比一目了然
- 🛡️ **安全校验** - 对象不一致时拒绝破坏性回滚
- 🤖 **自动确认** - 可选的自动点击"Allow"按钮守护进程

## 安装

```bash
# 克隆仓库
git clone https://github.com/kelin3296-jpg/Claude-code.sudo-skill.git ~/.claude/skills/sudo
```

## 使用方法

### 基础命令

| 命令 | 说明 |
|------|------|
| `/sudo` | 进入特权工作流 |
| `/sudo exit` | 退出特权工作流 |
| `/sudo status` | 查看当前状态 |
| `/sudo history [n]` | 查看最近 n 条操作记录 |
| `/sudo diff [path\|n]` | 查看变更差异 |
| `/sudo rollback [n]` | 回滚最近 n 条操作 |
| `/sudo backup-clean` | 清理 7 天前的备份 |
| `/sudo backup-purge` | 清空所有备份和日志 |

### 手动记录操作（高级）

```bash
# 修改文件前
python3 ~/.claude/skills/sudo/sudo.py log-modify <path>
# 执行修改...
# 修改完成后
python3 ~/.claude/skills/sudo/sudo.py finalize-modify <path>

# 删除文件前
python3 ~/.claude/skills/sudo/sudo.py log-delete <path>

# 创建文件后
python3 ~/.claude/skills/sudo/sudo.py log-create <path>

# 移动文件后
python3 ~/.claude/skills/sudo/sudo.py log-move <src> <dst>

# 修改权限后
python3 ~/.claude/skills/sudo/sudo.py log-chmod <path> <old_mode> <new_mode>
```

## 数据存储

- 备份目录: `~/.claude/sudo-backups/`
- 日志目录: `~/.claude/sudo-logs/`

## 许可证

MIT License
