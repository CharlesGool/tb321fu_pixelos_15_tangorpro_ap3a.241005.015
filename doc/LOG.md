---
name: project-log
description: 项目缺陷, 限制, 决策和交接
metadata:
  version: "1.0.0"
  lang: "zh-CN"
---

# 日志

## 多语言

**简体中文** | [English](en/LOG.md) | [Español](es/LOG.md)

## 文档

- 项目概览: [README](../README.md)

- 设计思路: [DESIGN](DESIGN.md)

- 项目状态: [LOG](LOG.md)
- 历史记录: [HISTORY](HISTORY.md)
- 变更日志: [CHANGELOG](CHANGELOG.md)

- 第三方声明: [THIRD_PARTY_NOTICES](THIRD_PARTY_NOTICES.md)

## 记录

- [历史记录](HISTORY.md)
- [变更日志](CHANGELOG.md)

## 缺陷

暂无已确认的缺陷.

## 限制

- 系统镜像内带有备用 keybox 种子, 过期或被吊销后失效, 此后密钥认证需要用户自己导入有效 keybox. user-v1.2 随镜像带的种子有效期到 2026-11-10(来源: 项目维护备忘, 未在镜像中复核).
- 按 App 关网络/传感器的权限加固(类似石墨烯)已搁置, 不在仓库里: 网络部分可用 `cmd connectivity chain3`, 运动传感器只能靠 Java 钩子, 难度较大.
- 保数据刷只适用于手机上原来就是本项目的系统.
- LE Audio 已关闭, 双模耳机走经典蓝牙.
- 人脸解锁是 WEAK 生物识别, 可解锁和弱校验, 不能授权支付或打开 StrongBox 凭据.
- 按精简级别 3 删掉了无障碍(TalkBack 等)和大部分 Google 应用, 需要的自己装回来.
- 蓝牙通话修复针对本包自带的 ZUI 17.0.12.044 vendor; 手机的 vendor 换成其他版本时修复不一定适用(未验证).

## 决策

| 日期 | 决策 | 状态 | 原因 |
| --- | --- | --- | --- |
| 2026-11-04 | 一个底包版本一个仓库 | 接受 | PixelOS 15 tangorpro 有多个底包版本 |
| 2026-11-04 | Release 只放 9008 刷机包, 不放 root 变体 | 接受 | 用户指定 |
| 2026-11-04 | 7z 分卷每卷 2000 MiB | 接受 | 低于 GitHub 单个资产 2 GiB 的上限 |
| 2026-11-04 | 仓库公开时第三方许可证尚未核验 | 接受 | 用户明确要求公开, 核验列为剩余步骤 |

## 交接

- 当前分支: `main`. 标签 `user-v1.2` 已发布 Release.
- 已完成: user-v1.2(V129)的 9008 包分卷, `SHA256SUMS.txt` 和模块列表已上传(上传后大小与本地一致); 仓库已改为公开; 项目文档和英文, 西班牙文翻译已写入.
- 已验证: 两个分卷按顺序拼接后的 sha256 与原 `.7z` 一致, 分卷 7z 测试通过.
- 未验证: 发布出去的包未在新下载后重新刷机验证; 第三方组件许可证未核验.
- 剩余步骤: 核验 `THIRD_PARTY_NOTICES.md` 中全部"未核验"项并补许可证文本; 选定许可证; 发布 user-v1.3 时同步更新文档.
- 临时项目规则: 未发现.
