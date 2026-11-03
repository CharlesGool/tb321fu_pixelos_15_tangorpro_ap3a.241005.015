# tb321fu_pixelos_15_tangorpro_ap3a.241005.015

[简体中文](../../README.md) | **English** | [Español](../es/README.md)

A 9008 flashing package that installs the Pixel Tablet Android 15 GSI (`AP3A.241005.015`) on the Lenovo Legion Y700 Gen 3 (TB321FU).

[![Release](https://img.shields.io/github/v/release/CharlesGool/tb321fu_pixelos_15_tangorpro_ap3a.241005.015?logo=github)](https://github.com/CharlesGool/tb321fu_pixelos_15_tangorpro_ap3a.241005.015/releases/latest)

## Documentation

- Project overview: [README](README.md)

- Design rationale: [DESIGN](DESIGN.md)

- Project status: [LOG](LOG.md)
- Historical records: [HISTORY](HISTORY.md)
- Version changelog: [CHANGELOG](CHANGELOG.md)

- Third-party notices: [THIRD_PARTY_NOTICES](THIRD_PARTY_NOTICES.md)

## Introduction

This project replaces ZUI on the TB321FU with the Pixel Tablet (`tangorpro`) Android 15 GSI, and adds the GSI features and fixes this device is missing. Flashing the community GSI directly runs into problems such as auto brightness not working, no sound from Bluetooth headphones, callers not heard over Bluetooth calls, apps that only support landscape rotating the wrong way, and no face unlock. This project fixes these.

System: Android 15 `AP3A.241005.015`, Pixel style. The base is the Pixel Tablet (`tangorpro`) from Mystic GSI; vendor and boot come from Lenovo's stock ZUI 17.0.12.044. The flashing package is a complete 9008 package, already signed, and does not require disabling vbmeta verification.

The current release is user-v1.2 (internal build V129). Known issues are in [LOG](LOG.md#limitations).

### ROM Features

- Identity restored to the original TB321FU device model, debugging off by default, GSI and virtual machine traces removed; SELinux Enforcing on boot.
- Global fingerprint spoofing and key attestation, to pass Play Integrity checks.
- Face unlock: built in PixelOS's ParanoidSense (Megvii SDK), uses the front camera, and is a WEAK (Class 2) biometric.
- Free rotation: all four orientations auto-rotate, including portrait upside down.
- Smooth display mode: in Settings, "Smooth display" on = no cap (panel up to 165 Hz), off = 120 Hz.
- Hidden navigation bar (phone-mode navigation bar, gesture hint line, tablet taskbar), toggled with `heraldctl`.
- 32-bit app support (Tango binary translation), built-in Pixel Camera (Google Camera 4.4).
- `herald-core`: root-free command and plugin entry point; the front-end app uses it to control system features.

### What Was Fixed

- Auto brightness: restores the adaptive brightness toggle in Settings, uses Lenovo's stock brightness curve and response speed, and the lowest manual level is restored to stock.
- Bluetooth headphones with no sound, callers not heard over Bluetooth: disables A2DP hardware offload and uses vendor software encoding instead; adds checks for audio policy and SCO. Disables unusable LE Audio; dual-mode headphones use classic Bluetooth.
- Apps that only support landscape (such as Bilibili fullscreen) rotate the wrong way: fixes the screen orientation and removes the Pixel Tablet dock orientation setting.
- Adaptive refresh rate: restores stock idle and touch timers and content detection (downshift when static, upshift on touch, match frame rate for video).
- WLAN hotspot: restores the Settings entry and Quick Settings tile; the 6 GHz hotspot works.
- Macro camera: after restoring a property, the camera HAL reports camera 2 as the macro camera.
- Boot popup and crash loop: removes the "An internal problem has occurred with the device" popup and fixes the device connection service crashing every 10 seconds.
- Trimming: removes Pixel components whose hardware this device does not have (dock, casting, UWB, side fingerprint, strong light/UV, baseband, etc.), Pixel-exclusive apps, old VNDK and GSI leftovers, and at trim level 3 removes most Google apps (including accessibility apps such as TalkBack); reinstall what you need.

The function of each module is described in [modules-user-v1.2](../modules-user-v1.2.md).

### Supported Hardware

The hardware covered by the fixes above: CPU/GPU, Bluetooth (headphones, calls), Wi-Fi and WLAN hotspot (including 6 GHz), auto brightness, 165 Hz high refresh rate, front, rear and macro cameras, auto rotation, and face unlock. The list shows the items the fixes cover; there is no per-item test record.

Patches and the build system are in [TB321FU-GSI-Mods](https://github.com/CharlesGool/TB321FU-GSI-Mods). PixelOS 15 tangorpro has several base-image versions, each with its own repository; this repository only covers `AP3A.241005.015`.

## Requirements

- Lenovo Legion Y700 Gen 3 TB321FU, able to enter 9008 (EDL) mode.
- A Windows PC, a USB data cable, and 7-Zip.
- Keep-data flashing only applies to a device already running this project's system; in all other cases, use the wipe-data flash.

## Install

### Quick Install

Download all volumes (`.7z.001`, `.7z.002`) from [Releases](https://github.com/CharlesGool/tb321fu_pixelos_15_tangorpro_ap3a.241005.015/releases/latest) into the same directory. Extract `.7z.001` with 7-Zip. Once the device is in 9008 mode, run `flash.bat` (wipe data) in the extracted directory. The flashing package includes the complete Lenovo stock 9008 firmware, so there is no need to flash an official base image beforehand.

### Normal Install

```bash
sha256sum -c SHA256SUMS.txt
7z x pixelos_tangorpro_ap3a.241005.015_user-v1.2_optional.7z.001
```

For a keep-data flash, run `flash_keep_data.bat`. Both scripts are in the root of the extracted directory.

## Usage

| File | Contents |
| --- | --- |
| `…user-v1.2_optional.7z.001`, `.002` | The 7z volumes of the complete 9008 flashing package, 2000 MiB each |
| `SHA256SUMS.txt` | Checksums for the volumes; the sha256 of the two volumes concatenated in order is `4cc450d58ef89097fe3a4b07b5aa53d01032e390371208e002aeb985fabe6cf2` |
| `module-list.md` | Module list for this release, same as [modules-user-v1.2](../modules-user-v1.2.md) |

### Using Face Unlock

Settings → Security & privacy → Device unlock → Face unlock → enter PIN → complete enrollment; afterward, point the front camera at your face on the lock screen to unlock. To delete: in Settings, face model → Delete. It is a WEAK biometric, and **do not** use it to protect payment or banking apps. The menu path follows the wording used in earlier versions and has not been step-by-step verified on user-v1.2.

### Version Naming

The public version is `user-vMAJOR.MINOR`, and the internal build number `V<数字>` is written into the image; user-v1.2 = V129.

## Upgrade

Not yet available.

## Uninstall

There is no separate quick uninstall. For a full uninstall, re-flash the complete Lenovo stock ZUI 17.0.12 9008 package. All data will be erased.

## Acknowledgements

- The Pixel Tablet GSI from Mystic GSI, used as the base image.
- The attestation engine is forked from [ITxiao6666/OhMyKeymint](https://github.com/ITxiao6666/OhMyKeymint) (original author James Clef / qwq233).
- Lenovo's stock ZUI firmware and flashing tools.

For attribution and compliance information, see [THIRD_PARTY_NOTICES](THIRD_PARTY_NOTICES.md).

## License

No license has been chosen for this repository, and no license is granted. For the license status of each third-party component, see [THIRD_PARTY_NOTICES](THIRD_PARTY_NOTICES.md).
