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

联想拯救者 Y700 三代(TB321FU)的 Pixel Tablet Android 15 GSI(`AP3A.241005.015`)9008 刷机包. 当前正式版 user-v1.2(内部版本 V129). 已知问题见 [LOG](doc/LOG.md#限制).

### 为什么做这个刷机包

1. 联想系统太难用了, 更喜欢类原生/Pixel OS.
2. 想实现一些高级功能, 但是不想 root, 不想弄麻烦的环境检测.
3. 我有 Claude Max 20x 🤣

### 重点, 写在前面

1. 本刷机包是 9008 刷机包, 可在不解锁 BL 的情况下刷入. 已签名, 不需要关 vbmeta 验证. 包里带完整的联想原厂 ZUI 17.0.12.044 9008 固件, 不需要事先刷官方底包.
2. 下列所有功能都是 rootless 实现.
3. 不影响系统环境, 检测软件里的结果和原厂系统一样; 唯一的例外是下面的"全局机型伪装", 开启后会被检测到系统异常挂载, 不开启则环境是完美的.
4. 除蓝牙硬件卸载(A2DP offload)外, 本机上遇到的硬件 Bug 都已修复. 蓝牙功能可以正常使用, 只是修得不够完美.
5. 本刷机包可自动化构建. 有 Linux PC 的话, 可以自己更换 GSI 和底包版本并构建(底包和原厂固件需自备), 见 [TB321FU-GSI-Mods](https://github.com/CharlesGool/TB321FU-GSI-Mods).

每个模块的作用见 [modules-user-v1.2](doc/modules-user-v1.2.md). 本版共 30 个模块: 全部必选模块加 5 个可选模块.

### 身份和认证

- 还原真实 TB321FU 身份(`ro.product.*`, 指纹, build 描述符取自原厂固件).
- rootless 密钥认证引擎: 可导入 keybox, 可本地下发 RKP 密钥(参考 Oh My Keymint 模块的功能).
- 全局机型伪装(可选模块 `global-pif`): 一键伪装成 Pixel Tablet 等机型, 伪装成 Pixel 机型后可通过 Play 完整性检查. 这是目前找到的 rootless 方案里影响最小的通过 Play 认证的办法, 但开启后会被检测到系统异常挂载. 不想要就不开启.
- `herald-core`: 免 root 的命令和插件入口(`heraldctl`), 前端 App 通过它控制系统功能.

### 相机

- 内置 Pixel 相机(Google 相机 4.4).
- 微距相机修复, 2 号微距相机对第三方相机可用.

### 人脸解锁

- 新增人脸解锁, 移植自 PixelOS 的 ParanoidSense(旷视 Megvii SDK), 走前置摄像头, 可用于锁屏解锁和 App 等非支付场景. 它是 WEAK(Class 2)生物识别, 不能授权支付或打开 StrongBox 凭据.

### 屏幕和显示

- 自动亮度修复: 补回设置里的自适应亮度开关, 换上联想原厂的亮度曲线和反应速度, 手动最低档还原原厂.
- 屏幕方向修复: Pixel Tablet 系统和本机默认方向不同, 只能横屏的应用(如 B 站全屏)不再倒过来.
- 自适应刷新率修复: 补回原厂的空闲/触摸定时器和内容检测, 静止降档, 触摸升档, 视频按帧率.
- 流畅显示档位: 设置里"流畅显示"开 = 不设上限(面板最高 165Hz), 关 = 120Hz(Pixel 原系统是 60/165Hz 切换, 改成 120/165Hz 更实用).
- 自由旋转: 90/180/270 度都能自动旋转, 包括竖屏倒过来.

### 网络和蓝牙

- 6GHz Wi-Fi 频段和国家码修复, Wi-Fi APEX 重新打包.
- 热点界面修复: Pixel Tablet 默认隐藏 WLAN 热点入口, 已补回设置入口和快捷设置磁贴.
- 蓝牙音频修复: 关 A2DP 硬件 offload 和 LE Audio, 改走 vendor 软件编码, 修耳机没声音和通话听不到.

### 应用兼容

- 移植 Tango, 支持 32 位 APK, 可以玩 32 位应用(参考一加 12 Android 15 ColorOS).

### 系统精简

- 删 Pixel 专属应用和数据, 精简旧版 VNDK, 精简本机没有的 Pixel 硬件组件.
- Google 应用级别精简, 本版是级别 3: 删大部分 Google 应用, 含 TalkBack 等无障碍, 需要的自己装回来.
- 清理 GSI(phh/Mystic)残留痕迹.

### 去痕迹和收尾

- 关闭调试(原版 adb root/调试默认开着).
- 隐藏 GSI 身份痕迹(防 GSI 检测).
- 去掉 phh 的 system 可写挂载.
- 反编译去掉开机"设备内部出现了问题"弹窗.
- 统一内核编译者字符串, 清理过期预编译, boot 重新打包并针对本机 AVB 重签.

### 界面

- 可隐藏导航栏(平板/手机模式均支持).

### 稳定性修复

- SELinux 规则修复: 开机即 Enforcing(原版缺规则会报错).
- 设备连接服务(DeviceConnectionService)域修复, 不再每 10 秒崩一次.

### 没打进本版的模块

这些模块仓库里有, 但 user-v1.2 没有打进来. 测试状态是作者自己的记录.

日常功能:

- 刷新率控制(`refresh-control`): `heraldctl refresh` 锁定或限定 30~165Hz. 已通过稳定性测试.
- 按应用/电量自动换刷新率(`refresh-auto-switch`): 依赖刷新率控制. 已通过稳定性测试.
- 电池管理(`battery`): 寿命查看, 长期插电保护, 充电上限, 旁路充电. 节点和取值来自联想电池 HAL 反编译. 已通过稳定性测试.
- 热点控制(`hotspot-control`): 自定义热点名称, 密码, 加密, 频段, `heraldctl wifi`. 不太稳定, 固定频宽还有一点问题.
- 解锁 6GHz 热点(`hotspot-6ghz-unlock`): 放开能力位, 信道列表, 设置页三道门. 已通过稳定性测试.
- HBM 不限时(`brightness/hbm-unlimited`): 去掉 782 尼特的 5 分钟时限. 已通过稳定性测试.
- 按应用伪装(`spoof/app-spoof`): 按 App 伪装 Build.*, 依赖 global-pif 的开机脚本. 已通过稳定性测试, 但是会被检测, 所以没实装.

高级功能(默认不打):

- 状态栏网速(`statusbar-netspeed`): 不改 SystemUI APK, 走 framework 钩子. 已通过稳定性测试, 但是有一点丑, 也没实装.
- 开发者选项隐藏(`devopts-hide`): 名单内 App 读开发者选项/ADB 状态得到 0. 不太稳定, 部分 App 依然可以读到.
- 自定义字体(`custom-font`): 读 `/data/fonts/herald` 字体包, 不占 system. 未测试.
- 应用备份还原(`app-backup`): apk(含 split)加数据备份到指定目录, 不定时. 已实现, 未测试.
- 游戏模式(`game-mode`): 游戏名单, 前台触发, 锁退出途径, 自动勿扰. 不太稳定.
- 性能调节(`perf`): CPU/GPU 频率上下限, 省电/均衡/性能一键切档, 温度读数. 已通过稳定性测试.
- 游戏性能联动(`perf-game-boost`): 游戏模式的性能档钩子. 不太稳定.
- overlay 缓存自愈(`overlay-idmap-reset`): 开机删旧 idmap, 防 idmap2d 崩溃. 已通过稳定性测试.

额外精简:

- 精简无障碍应用(`slim/accessibility`): 删读屏等, 需要读屏的人别用. 已通过稳定性测试(本版已随 Google 应用级别 3 一起删除).
- 精简 Google 应用(`slim/google-apps`): 删 Google 预装应用, 助理, TTS 数据. 已通过稳定性测试(本版已按级别 3 精简).

调试和调研(正常使用不需要):

- adb 可抓日志(`shell-logcat`), 开机自动开 ADB(`adb-on-boot`, 免授权).
- adb root(`rooted-adbd`, `ro.debuggable=1`, adbd/shell 域 permissive).
- root 只读命令(`herald-readonly-shell`, 默认关), root shell(`herald-rooted-shell`, 默认关, 限时打开).
- zygote 时序测量(`herald-zygisk-timing-probe`), zygote 注入点验证(`herald-zygisk-fork-observer`), 开机相机日志(`diag-boot-camera-log`).

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
