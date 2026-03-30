# sudo-skill

[![CI](https://github.com/kelin3296-jpg/sudo-skill/actions/workflows/ci.yml/badge.svg)](https://github.com/kelin3296-jpg/sudo-skill/actions/workflows/ci.yml)
![Claude Code](https://img.shields.io/badge/runtime-Claude%20Code-5b5bd6)
![Python](https://img.shields.io/badge/python-3.10%2B-3776ab)
![License](https://img.shields.io/badge/license-MIT-green)

A Claude Code skill for explicit privileged workflows with backup, audit logs, diff, and rollback helpers.

中文说明见 [`README.zh-CN.md`](README.zh-CN.md).

## What this is

`sudo-skill` keeps the familiar `/sudo` mental model, but it does **not** claim to automatically bypass Claude Code sandboxing or mutate bash tool parameters. Instead, it helps the host agent work explicitly and safely around sensitive changes by recording:

- pre-change backups
- operation history
- unified diff for text files
- guarded rollback with object validation
- explicit enter / exit workflow state

## Platform boundary

This project is **Claude Code only** in v1.
It does not attempt to support OpenClaw, Codex, or any other runtime yet.

## Public commands

```bash
python sudo.py enter
python sudo.py exit
python sudo.py status
python sudo.py clean --days 7
python sudo.py purge --yes
python sudo.py history 20
python sudo.py rollback 1 --yes
python sudo.py diff [path|history-index]
```

## Install

Install from a local working tree:

```bash
mkdir -p ~/.claude/skills
cp -R ./sudo-skill ~/.claude/skills/sudo
```

Install from the release zip:

```bash
mkdir -p ~/.claude/skills
unzip dist/sudo-skill.zip -d /tmp/sudo-skill-release
rm -rf ~/.claude/skills/sudo
mv /tmp/sudo-skill-release/sudo-skill ~/.claude/skills/sudo
```

## Integrator commands used by the skill

These commands keep `operation_logger.py` internal while still letting the skill track changes via the public CLI:

```bash
python sudo.py log-modify <path>
python sudo.py finalize-modify <path> [--id OP_ID]
python sudo.py log-delete <path>
python sudo.py log-create <path>
python sudo.py log-move <src> <dst>
python sudo.py log-chmod <path> <old_mode_octal> <new_mode_octal>
```

## Storage

By default the skill stores state under `~/.claude`:

- `~/.claude/sudo-backups/`
- `~/.claude/sudo-logs/`
- `~/.claude/sudo-state.json`

Set `SUDO_SKILL_HOME` to isolate development, testing, or custom installations.

## Safety notes

- The skill does **not** automatically elevate Claude Code commands.
- Rollback refuses destructive actions if the tracked file object no longer matches the recorded snapshot.
- `delete` rollback refuses to overwrite a path that has been reused.
- `create` rollback refuses to delete a file that changed after creation.

## Demo walkthrough

```text
$ python sudo.py enter
Entered /sudo explicit privileged workflow.

$ python sudo.py log-modify ~/.ssh/config
Recorded modify operation #1 for /Users/you/.ssh/config

$ python sudo.py finalize-modify ~/.ssh/config
Finalized modify operation #1 for /Users/you/.ssh/config

$ python sudo.py diff ~/.ssh/config
--- before:/Users/you/.ssh/config
+++ current:/Users/you/.ssh/config
@@ ...

$ python sudo.py rollback 1 --yes
Rolled back modify: /Users/you/.ssh/config

$ python sudo.py exit
Exited /sudo workflow.
```

## Development

```bash
python3 -m venv .venv
./.venv/bin/pip install pytest
./.venv/bin/python -m pytest
python3 scripts/build_release.py
```

The release builder creates `dist/sudo-skill.zip` without `__MACOSX`, tests, or cache files.

If you publish this repository under a different GitHub owner or repo name, update the CI badge URL at the top of this file.
