---
name: project-changelog
description: 变更日志
metadata:
  version: "1.0.0"
  lang: "zh-CN"
---

# 变更日志

## 多语言

**简体中文** | [English](en/CHANGELOG.md) | [Español](es/CHANGELOG.md)

## 文档

- 项目概览: [README](../README.md)

- 设计思路: [DESIGN](DESIGN.md)

- 项目状态: [LOG](LOG.md)
- 历史记录: [HISTORY](HISTORY.md)
- 变更日志: [CHANGELOG](CHANGELOG.md)

- 第三方声明: [THIRD_PARTY_NOTICES](THIRD_PARTY_NOTICES.md)

## 变更日志

### user-v1.3(V132)- 2026-11-04

- 新增: 本仓库的第二个 Release, 并提供从 user-v1.2 保数据升级的补丁(14MB).
- 变更: `herald-core` 升到 V1.3, 工作目录回到 `/data/local/tmp`, 修复 V1.2 在真机上的 SELinux 标签问题.
- 变更: 认证引擎换成含安全加固的新构建: 未知版本不 panic, `keymint.dat` 原子写, keybox 解析失败不覆盖已有文件.

### user-v1.2(V129)- 2026-11-04

- 新增: 本仓库的首个 Release, 提供完整 9008 刷机包分卷, `SHA256SUMS.txt` 和模块列表.
- 修复: 蓝牙. `vendor-bind` 给 `update_engine` 域补 `mounton` 和读 `vendor_file`, Enforcing 下蓝牙音频策略和 SCO 的 bind 才能生效.
