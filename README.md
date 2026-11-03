# tb321fu_pixelos_15_tangorpro_ap3a.241005.015

联想拯救者 Y700 三代(TB321FU)刷 Pixel Tablet(`tangorpro`)Android 15 `AP3A.241005.015` GSI 的成品刷机包.

底包是 Pixel Tablet 的 GSI, vendor 和 boot 用联想原厂 ZUI 17.0.12(Android 15). 补丁本身见 [TB321FU-GSI-Mods](https://github.com/CharlesGool/TB321FU-GSI-Mods). PixelOS 15 tangorpro 有多个底包版本, 每个底包版本一个仓库, 本仓库只对应 `AP3A.241005.015`.

## 版本

| 版本 | 内容 |
|---|---|
| user-v1.2 | 正式版. 在 user-v1.1 的补丁集上修蓝牙. 模块清单见 [模块列表说明](docs/user-v1.2-模块列表说明.md) |

Release 只提供完整 9008 刷机包, 用 7z 分卷(每卷 2000 MiB), 下载全部 `.7z.001`, `.7z.002` ... 放在同一目录, 用 7-Zip 解压 `.7z.001` 即可. 校验值见 `SHA256SUMS.txt`.

清数据刷用包内 `flash.bat`, 保数据刷用 `flash_keep_data.bat`(只适用于手机上原来就是本项目的系统).
