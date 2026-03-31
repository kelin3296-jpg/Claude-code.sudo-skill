# Security Policy

This repository ships a Claude Code skill plus safety helpers for backup, diff, audit logs, and guarded rollback. Because the project touches sensitive file workflows, please report security problems carefully and avoid publishing exploit details before maintainers have time to respond.

## Supported versions

| Version | Supported |
| --- | --- |
| 0.1.x | Yes |
| < 0.1.0 | No |

For now, the latest `0.1.x` release is the supported line.

## How to report a vulnerability

Please **do not** open a public issue with full exploit details.

Preferred order:

1. Use GitHub private vulnerability reporting or a security advisory flow if it is enabled for this repository.
2. If private reporting is not available, open a minimal issue without exploit details and ask the maintainer for a private channel.
3. Include only the information needed to reproduce safely: affected version, platform, impact, and high-level steps.

Helpful details:

- affected file or command path
- whether the issue impacts backup, diff, logging, or rollback
- whether it can cause unsafe deletion, overwrite, or data exposure
- the smallest safe reproduction you can provide

## What to expect

The maintainer will try to:

- confirm receipt
- assess impact and reproduce the issue
- ship a fix or mitigation in a later release
- credit the reporter when appropriate

Response times are best-effort for now.

## Scope notes

Security-sensitive areas for this project include:

- destructive rollback behavior
- object identity validation before rollback
- backup storage and restore paths
- command flows that could be misread as implicit privilege escalation

## 中文说明

这个仓库提供的是一个 Claude Code skill，以及围绕备份、diff、审计日志和安全回滚的辅助能力。因为项目涉及敏感文件操作流程，发现安全问题时请尽量避免直接公开完整利用细节。

### 支持版本

当前支持最新的 `0.1.x` 版本线；更早版本默认不再维护。

### 安全问题反馈方式

请**不要**直接公开带完整利用细节的 issue。

建议按下面顺序处理：

1. 如果仓库启用了 GitHub 私密漏洞反馈或 Security Advisory，优先走私密通道。
2. 如果暂时没有私密通道，请先开一个不含利用细节的最小 issue，请维护者提供私下沟通方式。
3. 只提供安全复现所需的最小信息，例如影响版本、平台、影响范围和高层步骤。

建议补充的信息：

- 受影响的文件或命令路径
- 是否影响备份、diff、日志或 rollback
- 是否可能导致误删、误覆盖或数据泄露
- 能安全提供的最小复现
