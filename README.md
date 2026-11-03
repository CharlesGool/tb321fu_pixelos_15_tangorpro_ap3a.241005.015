# tb321fu_pixelos_15_tangorpro_ap3a.241005.015

**简体中文** | [English](doc/en/README.md) | [Español](doc/es/README.md)

联想拯救者 Y700 三代(TB321FU)刷 Pixel Tablet Android 15 GSI(`AP3A.241005.015`)的 9008 刷机包.

[![Release](https://img.shields.io/github/v/release/CharlesGool/tb321fu_pixelos_15_tangorpro_ap3a.241005.015?logo=github)](https://github.com/CharlesGool/tb321fu_pixelos_15_tangorpro_ap3a.241005.015/releases/latest)

## 文档

- 项目概览: [README](README.md)

- 设计思路: [DESIGN](doc/DESIGN.md)

- 项目状态: [LOG](doc/LOG.md)
- 历史记录: [HISTORY](doc/HISTORY.md)
- 变更日志: [CHANGELOG](doc/CHANGELOG.md)

- 第三方声明: [THIRD_PARTY_NOTICES](doc/THIRD_PARTY_NOTICES.md)

## 简介

在 TB321FU 上用 Pixel Tablet(`tangorpro`)的 Android 15 GSI 取代 ZUI, 并补上 GSI 在这台机器上缺的功能和修复. 底包是 Mystic GSI 的 `AP3A.241005.015`, vendor 和 boot 用联想原厂 ZUI 17.0.12.

当前正式版 user-v1.2(内部版本 V129)提供:

- Pixel 系统, 身份还原成原厂机型, 通过 Play 完整性检查.
- 人脸解锁, 自由旋转, 隐藏导航栏, 流畅显示档位(最高 165Hz).
- 蓝牙音频, 6GHz 热点, 自动亮度, 自适应刷新率, 微距相机等硬件修复.
- 32 位应用支持, Pixel 相机.
- `herald-core`: 系统里的命令和插件入口.

模块清单见 [modules-user-v1.2](doc/modules-user-v1.2.md). 补丁和构建系统在 [TB321FU-GSI-Mods](https://github.com/CharlesGool/TB321FU-GSI-Mods). PixelOS 15 tangorpro 有多个底包版本, 每个底包版本一个仓库, 本仓库只对应 `AP3A.241005.015`.

## 要求

- 联想拯救者 Y700 三代 TB321FU, 能进 9008(EDL)模式.
- Windows 电脑, USB 数据线, 7-Zip.
- 保数据刷只适用于手机上原来就是本项目的系统; 其他情况用清数据刷.

## 安装

### 快速安装

从 [Releases](https://github.com/CharlesGool/tb321fu_pixelos_15_tangorpro_ap3a.241005.015/releases/latest) 下载全部分卷(`.7z.001`, `.7z.002`)放在同一目录, 用 7-Zip 解压 `.7z.001`, 设备进 9008 后在解压目录运行 `flash.bat`(清数据).

### 常规安装

```bash
sha256sum -c SHA256SUMS.txt
7z x pixelos_tangorpro_ap3a.241005.015_user-v1.2_optional.7z.001
```

保数据刷运行 `flash_keep_data.bat`. 两个脚本都在解压目录根部.

## 指南

| 文件 | 内容 |
| --- | --- |
| `…user-v1.2_optional.7z.001`, `.002` | 完整 9008 刷机包的 7z 分卷, 每卷 2000 MiB |
| `SHA256SUMS.txt` | 分卷的校验值; 两卷按顺序拼接后的 sha256 为 `4cc450d58ef89097fe3a4b07b5aa53d01032e390371208e002aeb985fabe6cf2` |
| `module-list.md` | 本版模块列表, 同 [modules-user-v1.2](doc/modules-user-v1.2.md) |

版本标识: 对外版本 `user-vMAJOR.MINOR`, 内部版本号 `V<数字>` 写在镜像里, user-v1.2 = V129.

## 升级

暂无

## 卸载

快速卸载没有单独的办法. 完全卸载: 用联想原厂 ZUI 17.0.12 的 9008 包整套重刷, 数据会被清除.

## 致谢

- Mystic GSI 的 Pixel Tablet GSI 作为底包.
- 认证引擎 fork 自 [ITxiao6666/OhMyKeymint](https://github.com/ITxiao6666/OhMyKeymint)(原作者 James Clef / qwq233).
- 联想 ZUI 原厂固件和刷机工具.

署名和合规信息见 [THIRD_PARTY_NOTICES](doc/THIRD_PARTY_NOTICES.md).

## 许可证

本仓库尚未选定许可证, 未授予任何许可. 第三方组件各自的许可证状态见 [THIRD_PARTY_NOTICES](doc/THIRD_PARTY_NOTICES.md).
