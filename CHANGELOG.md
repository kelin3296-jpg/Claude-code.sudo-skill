# Changelog

All notable changes to this project will be documented in this file.
此文件记录这个项目的重要变更。

The format is inspired by Keep a Changelog, and this project follows semantic versioning in a lightweight, release-oriented way.

## [0.1.3] - 2026-03-31

### Added

- formal `CHANGELOG.md` for repository-level release history
- GitHub social preview assets in `docs/social-preview.svg` and `docs/social-preview.png`
- copy-paste Claude Code installer prompts in English and Chinese

### Changed

- rewrote the README story around background, pain points, and the emotional cost of privileged edits
- clarified the fallback path: logs plus backups support rollback and manual recovery when users feel unsure after sensitive changes
- refreshed `SKILL.md` so the skill description explains the problem, the safety net, and what `/sudo` is actually promising
- included `CHANGELOG.md`, `SECURITY.md`, and `SUPPORT.md` in the release zip payload

## [0.1.2] - 2026-03-31

### Added

- `SECURITY.md` with vulnerability reporting guidance and scope notes
- `SUPPORT.md` with support boundaries and issue guidance

### Changed

- linked security and support docs from the README contribution area

## [0.1.1] - 2026-03-31

### Added

- contributor onboarding assets, including `CONTRIBUTING.md`, `CONTRIBUTING.zh-CN.md`, issue templates, and a PR template
- structured release note generation via `scripts/build_release_notes.py`
- repository demo artwork in `docs/demo-terminal.svg`

### Changed

- polished the repository homepage copy in English and Chinese
- updated the release workflow to publish structured release notes

## [0.1.0] - 2026-03-31

### Added

- initial open-source release of the Claude Code `sudo` skill
- explicit privileged workflow CLI with backup, diff, audit logging, and guarded rollback
- clean release zip build, CI workflow, and automated GitHub Release publishing
