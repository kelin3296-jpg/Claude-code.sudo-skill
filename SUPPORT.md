# Support

Thanks for using `sudo-skill`.

This repository is maintained as a small open-source project, so support is best-effort. The fastest path usually depends on the type of question.

## Where to ask for what

- **Bug or regression**: open a GitHub bug report
- **Feature idea**: open a GitHub feature request
- **Usage question**: open a GitHub issue and prefix the title with `[Support]`
- **Security concern**: follow [`SECURITY.md`](SECURITY.md) and avoid posting exploit details publicly

## Before opening a support request

Please include as much of this as you can:

- sudo-skill version or release tag
- Python version
- OS and shell
- the exact `python sudo.py ...` command you ran
- expected behavior vs actual behavior
- relevant stdout, stderr, diff output, or screenshots

## What this project currently supports

This repository currently supports:

- **Claude Code** as the target runtime
- the documented `/sudo` explicit workflow
- installable release zips published on GitHub Releases

This repository does **not** currently provide first-class support for:

- OpenClaw, Codex CLI, or other runtimes
- implicit sandbox bypass or hidden privilege escalation
- environment-specific production operations outside the documented workflow

## Response expectations

Maintainer response time is best-effort. Clear, focused reports with reproduction steps are much easier to help with.

## Good support questions

Helpful examples:

- "Rollback refuses to run after a move even though the destination file was not changed."
- "The release zip installs, but `python sudo.py diff` returns an unexpected binary summary."
- "I want to add a new guard to rollback. Which tests should I update?"

## 中文说明

感谢使用 `sudo-skill`。

这个仓库目前是一个精简的开源项目，支持主要是 best-effort。通常最快的处理方式取决于问题类型：

- **Bug / 回归问题**：提交 GitHub bug report
- **功能建议**：提交 GitHub feature request
- **使用问题**：提交一个 GitHub issue，并在标题前加 `[Support]`
- **安全问题**：按 [`SECURITY.md`](SECURITY.md) 处理，不要公开完整利用细节

提交支持请求前，建议尽量附上：

- sudo-skill 版本或 release tag
- Python 版本
- 操作系统与 shell
- 实际运行的 `python sudo.py ...` 命令
- 预期行为与实际行为
- 相关 stdout、stderr、diff 输出或截图

当前支持范围主要包括：

- **Claude Code** 运行时
- 文档中定义的 `/sudo` 显式工作流
- GitHub Releases 发布的安装包

当前**不提供一线支持**的范围包括：

- OpenClaw、Codex CLI 或其他运行时
- 隐式绕过沙箱或隐藏提权能力
- 文档范围之外的环境定制操作
