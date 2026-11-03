# user-v1.2 模块列表说明

本版(内部版本 V129)由 30 个补丁模块构建, 构建预设 `user-v1.2`: 全部 `required` 模块, 加 5 个 `optional` 模块. 每个模块的实际应用记录见同目录 `模块日志/`, 原始清单见 `MODULES.txt` 和 `SELECTION.txt`.

构建参数: `VERSION=V129 VERSION_LABEL=user-v1.2 PROFILE=user-v1.2 GOOGLE_SLIM=3`.
设备: 联想拯救者 Y700 三代 TB321FU, 底包 Pixel Tablet(tangorpro)Android 15 `AP3A.241005.015` GSI, vendor 和 boot 用联想原厂 ZUI 17.0.12.044.

## 身份与隐藏

| 模块 | 作用 |
|---|---|
| 机型还原 `identity` | `ro.product.*` 改成 TB321FU, 指纹和 build 描述符从原厂固件取, `ro.build.display.id` 写版本号 |
| 关闭调试 `debug-off` | 关掉调试相关开关 |
| 隐藏 GSI 痕迹 `gsi-hide` | `partition.*.verified` 改 1, 去掉虚拟机属性标签 |
| 全局指纹伪装 `global-pif` (可选) | 全局指纹伪装, 用于通过 Play 完整性检查 |
| 密钥认证 `attestation-fix` | keymint + inject: 签出 deviceLocked / verifiedBootState=green 的证书链, 附指纹伪装, keybox, 安全补丁同步命令 |
| herald 核心 `herald-core` | 免 root 的控制后端: broker + `heraldctl` + 插件接口. 只提供命令通道, 配对和接入方式, 具体能力由别的补丁接入 |

## 精简

| 模块 | 作用 |
|---|---|
| 精简旧版 VNDK `old-vndk` | 只留 vendor 要用的 VNDK apex, 删其余版本, 约 246M |
| 精简 Pixel 专属应用和数据 `pixel-leftovers` | 删 Play 自动安装配置, "正在播放"歌曲库, Pixel 相机, 儿童模式 |
| 精简 Pixel 硬件组件 `pixel-hardware` | 删本机没有对应硬件的组件: 底座, 投屏, 零售演示, Tensor 服务, 侧边指纹, UWB, 强光/UV, 基带, NFC 应用 |
| 精简 Google 应用 `google-slim` | 按级别删 Google 应用, 本版 `GOOGLE_SLIM=3`: 冷门应用, 日常应用(时钟, 天气, 相册, Gmail, 地图等), Google 助理, GoogleTTS 语音数据, 离线语音模型, 无障碍(TalkBack 等); 依赖被删应用的下拉栏磁贴一并去掉 |
| 精简 GSI 残留 `gsi-traces` | 删 Mystic 的 vendor overlay 和开机 root logcat, phh 的按键布局, 远程 adb 隧道, 属性处理脚本 |
| 去 phh 可写挂载 `rw-system-tmpfs` | 去掉 phh 脚本的可写 tmpfs 挂载 |

## 启动与 SELinux

| 模块 | 作用 |
|---|---|
| SELinux 修复 `selinux/fix` | 开机即 Enforcing: 删 Mystic 的 permissiver, early-init 就 `setenforce 1`, 内核命令行加 `enforcing=1 selinux=1` |
| 设备连接服务域修复 `dcservice-seapp-fix` | 删 `seapp_contexts` 里指向 `dcservice_app` 的两行规则, 否则设备连接服务每 10 秒崩一次 |
| 去开机内部问题弹窗 `build-consistency-dialog-fix` | 去掉开机"设备内部出现了问题"弹窗 |
| 清过期预编译 `stale-boot-image` | 清掉因改 jar 而过期的预编译产物 |
| 内核编译者字符串 `kernel-builder-string` | 修改内核编译者字符串 |
| boot 打包重签 `boot-assemble` | 汇总改动, 重签 boot |

## 硬件修复

| 模块 | 作用 |
|---|---|
| 自动亮度修复 `auto-brightness-fix` | 补回设置里的自适应亮度开关, 换上联想原厂的自动亮度曲线和反应速度, 手动最低档还原原厂 |
| 自适应刷新率修复 `adaptive-refresh-fix` | 补回原厂 SurfaceFlinger 的空闲/触摸定时器和内容检测(静止降档, 触摸升档, 视频按帧率) |
| 屏幕方向修复 `rotation-fix` | 只能横屏的应用画面不再倒过来; 去掉 Pixel Tablet 底座的方向设置 |
| 热点界面修复 `hotspot-ui-fix` | 补回设置里的 WLAN 热点入口和快捷设置磁贴 |
| 6GHz 修复 `6ghz-fix` | Wi-Fi 国家码默认 DE, 驱动才允许 6GHz 热点; 设置里选 6GHz 时把热点固定在 6GHz 频段 |
| Wi-Fi 打包 `wifi-apex-assemble` | 把各 Wi-Fi 补丁登记的 smali 补丁一次性应用到 `service-wifi.jar`, 回编, 重签 APEX |
| 蓝牙音频修复 `bluetooth-fix` | 关 A2DP 硬件 offload 和 LE Audio, 改走 vendor 软件编码; 修耳机没声音和通话听不到. 本版另在 `vendor-bind` 里给 `update_engine` 域补 SELinux 权限, 使 Enforcing 下两个 bind 能生效 |
| 微距相机修复 `macro-camera-fix` | 补回 `ro.vendor.qti.va_aosp.support=1`, 相机 HAL 才报出 2 号微距相机 |

## 功能

| 模块 | 作用 |
|---|---|
| Pixel 相机 `pixel-camera` | 内置 Google 相机 4.4(通用版, 体积小) |
| 32 位应用支持 `tango` | Tango 二进制翻译: 翻译器, sepolicy, 内核模块, 32 位 vendor 库, 32 位 zygote 和开机保险 |
| 人脸解锁 `faceunlock` (可选) | 生物识别放行钩子 + FaceUnlock App 和权限 + 设置里的人脸入口 |
| 自由旋转 `free-rotation` (可选) | 四个方向都能自动旋转, 包括竖屏倒过来; 不受"显示大小"影响 |
| 流畅显示档位 `smooth-display` (可选) | "流畅显示"开 = 不设上限(最高 165Hz), 关 = 120Hz |
| 隐藏导航栏 `navbar-hide` (可选) | 隐藏手机模式导航栏, 手势提示线, 平板任务栏, 带 `heraldctl` 开关和导航模式守护 |

## 没有打的模块

`user-v1.2` 预设只含上面的模块. 默认不打的高级功能(应用隐藏, 字体替换, 应用备份等)不在本版里.
