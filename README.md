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

在 TB321FU 上用 Pixel Tablet(`tangorpro`)的 Android 15 GSI 取代 ZUI, 并补上 GSI 在这台机器上缺的功能和修复. 直接刷社区 GSI 会碰到自动亮度不工作, 蓝牙耳机没声音, 蓝牙通话听不见, 只能横屏的应用方向反, 没有人脸解锁等问题, 本项目把这些修了.

系统: Android 15 `AP3A.241005.015`, Pixel 风格. 底包是 Mystic GSI 的 Pixel Tablet(`tangorpro`), vendor 和 boot 用联想原厂 ZUI 17.0.12.044. 刷机包是完整 9008 包, 已签名, 不需要关 vbmeta 验证.

当前正式版 user-v1.2(内部版本 V129). 已知问题见 [LOG](doc/LOG.md#限制).

### ROM 特性

- 身份还原成原厂机型 TB321FU, 默认关调试, 去掉 GSI 和虚拟机痕迹, 开机即 SELinux Enforcing.
- 全局指纹伪装和密钥认证, 用于通过 Play 完整性检查.
- 人脸解锁: 内置 PixelOS 的 ParanoidSense(旷视 Megvii SDK), 走前置摄像头, 是 WEAK(Class 2)生物识别.
- 自由旋转: 四个方向都能自动旋转, 包括竖屏倒过来.
- 流畅显示档位: 设置里"流畅显示"开 = 不设上限(面板最高 165Hz), 关 = 120Hz.
- 隐藏导航栏(手机模式导航栏, 手势提示线, 平板任务栏), 可用 `heraldctl` 开关.
- 32 位应用支持(Tango 二进制翻译), 内置 Pixel 相机(Google 相机 4.4).
- `herald-core`: 免 root 的命令和插件入口, 前端 App 通过它控制系统功能.

### 修了什么

- 自动亮度: 补回设置里的自适应亮度开关, 换上联想原厂的亮度曲线和反应速度, 手动最低档还原原厂.
- 蓝牙耳机没声音, 蓝牙通话听不见: 关 A2DP 硬件 offload, 改走 vendor 软件编码; 补音频策略和 SCO 的检查. 关闭不可用的 LE Audio, 双模耳机走经典蓝牙.
- 只能横屏的应用(如 B 站全屏)方向反: 修屏幕方向, 去掉 Pixel Tablet 底座的方向设置.
- 自适应刷新率: 补回原厂的空闲/触摸定时器和内容检测(静止降档, 触摸升档, 视频按帧率).
- WLAN 热点: 补回设置入口和快捷设置磁贴; 6GHz 热点可用.
- 微距相机: 补回属性后相机 HAL 才报出 2 号微距相机.
- 开机弹窗和崩溃循环: 去掉"设备内部出现了问题"弹窗, 修设备连接服务每 10 秒崩一次.
- 精简: 删本机没有对应硬件的 Pixel 组件(底座, 投屏, UWB, 侧边指纹, 强光/UV, 基带等), Pixel 专属应用, 旧版 VNDK 和 GSI 残留, 并按级别 3 删大部分 Google 应用(含 TalkBack 等无障碍), 需要的自己装回来.

每个模块的作用见 [modules-user-v1.2](doc/modules-user-v1.2.md).

### 可用硬件

以上修复针对的硬件: CPU/GPU, 蓝牙(耳机, 通话), Wi-Fi 和 WLAN 热点(含 6GHz), 自动亮度, 165Hz 高刷, 前后和微距摄像头, 自动旋转, 人脸解锁. 本表列的是修复覆盖的项, 没有对每一项逐个写测试记录.

补丁和构建系统在 [TB321FU-GSI-Mods](https://github.com/CharlesGool/TB321FU-GSI-Mods). PixelOS 15 tangorpro 有多个底包版本, 每个底包版本一个仓库, 本仓库只对应 `AP3A.241005.015`.

## 要求

- 联想拯救者 Y700 三代 TB321FU, 能进 9008(EDL)模式.
- Windows 电脑, USB 数据线, 7-Zip.
- 保数据刷只适用于手机上原来就是本项目的系统; 其他情况用清数据刷.

## 安装

### 快速安装

从 [Releases](https://github.com/CharlesGool/tb321fu_pixelos_15_tangorpro_ap3a.241005.015/releases/latest) 下载全部分卷(`.7z.001`, `.7z.002`)放在同一目录, 用 7-Zip 解压 `.7z.001`, 设备进 9008 后在解压目录运行 `flash.bat`(清数据). 刷机包带完整的联想原厂 9008 固件, 不需要事先刷官方底包.

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

### 使用人脸解锁

设置 → 安全与隐私 → 设备解锁 → 人脸解锁 → 输入 PIN → 走完录入, 之后锁屏对准前置摄像头即可. 删除: 设置里的人脸模型 → 删除. 它是 WEAK 生物识别, **禁止**用来保护支付, 银行这类应用. 菜单路径沿用旧版本的写法, 未在 user-v1.2 上逐步复核.

### 版本标识

对外版本 `user-vMAJOR.MINOR`, 内部版本号 `V<数字>` 写在镜像里, user-v1.2 = V129.

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
