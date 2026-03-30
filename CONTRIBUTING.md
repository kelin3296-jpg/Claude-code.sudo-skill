# Contributing to sudo-skill

Thanks for taking the time to contribute. This repository is intentionally small: it ships a Claude Code skill, a thin CLI wrapper, and the safety logic behind backup, diff, audit logs, and guarded rollback.

## Good first contributions

- tighten rollback safety checks
- improve docs or examples
- add tests for edge cases
- improve release or repository automation
- refine contributor experience for issues and pull requests

## Local development

```bash
python3 -m venv .venv
./.venv/bin/pip install pytest
./.venv/bin/python -m pytest
python3 scripts/build_release.py
```

Optional release note preview:

```bash
python3 scripts/build_release_notes.py v0.1.1-preview
```

## Project boundaries

Please keep these constraints intact unless the maintainers explicitly decide otherwise:

- runtime target is **Claude Code** only
- `/sudo` is an **explicit workflow**, not an implicit sandbox bypass
- rollback should prefer refusing unsafe destructive actions over forcing success
- `operation_logger.py` is internal; user-facing commands go through `sudo.py`
- release zip should stay clean and installable as a skill package

## Before opening a pull request

- keep changes focused and explain the user-facing impact
- add or update tests when behavior changes
- update docs when commands, workflow, or safety guarantees change
- run `./.venv/bin/python -m pytest`
- run `python3 scripts/build_release.py` if packaging logic changed

## Pull request checklist

Include these points in your PR description when relevant:

- what problem this change solves
- what safety or behavior changed
- what tests you ran
- whether docs or release notes changed
- any follow-up work that should happen separately

## Release expectations

Tags like `v0.1.1` trigger the release workflow. The workflow runs tests, builds `dist/sudo-skill.zip`, generates structured release notes, and publishes a GitHub Release.

If your change affects packaging, docs, or release automation, please mention that clearly in the PR.

## Code of collaboration

Be kind, precise, and practical. Small, reviewable pull requests are preferred over large mixed changes.
