# sudo state tracking

## English

The skill stores workflow state in `sudo-state.json` under `SUDO_SKILL_HOME` or `~/.claude`.

- `active: true` means `/sudo` is currently entered.
- `entered_at` records when the explicit workflow began.
- `mode: explicit` makes the contract clear: the skill tracks safety metadata, but it does not auto-change Claude Code sandbox or bash tool parameters.

### Enter flow

1. User invokes `/sudo`.
2. The skill runs `python sudo.py enter`.
3. The state file is written and the agent switches to explicit privileged workflow guidance.

### Exit flow

1. User invokes `/sudo exit`.
2. The skill runs `python sudo.py exit`.
3. The state file is marked inactive.

## 中文

该 skill 会把状态写入 `SUDO_SKILL_HOME` 或 `~/.claude` 下的 `sudo-state.json`。

- `active: true` 表示当前已经进入 `/sudo` 工作流。
- `entered_at` 表示进入时间。
- `mode: explicit` 明确说明：这个 skill 负责记录安全元数据，不会自动修改 Claude Code 的沙箱或 bash 参数。

### 进入流程

1. 用户输入 `/sudo`。
2. skill 执行 `python sudo.py enter`。
3. 写入状态文件，并进入显式特权工作流说明。

### 退出流程

1. 用户输入 `/sudo exit`。
2. skill 执行 `python sudo.py exit`。
3. 状态文件更新为 inactive。
