# tb321fu_pixelos_15_tangorpro_ap3a.241005.015

[简体中文](../../README.md) | **English** | [Español](../es/README.md)

9008 flashing package for the Pixel Tablet Android 15 GSI (`AP3A.241005.015`) on the Lenovo Legion Y700 Gen 3 (TB321FU).

[![Release](https://img.shields.io/github/v/release/CharlesGool/tb321fu_pixelos_15_tangorpro_ap3a.241005.015?logo=github)](https://github.com/CharlesGool/tb321fu_pixelos_15_tangorpro_ap3a.241005.015/releases/latest)

## Documentation

- Project overview: [README](README.md)

- Design rationale: [DESIGN](DESIGN.md)

- Project status: [LOG](LOG.md)
- Historical records: [HISTORY](HISTORY.md)
- Version changelog: [CHANGELOG](CHANGELOG.md)

- Third-party notices: [THIRD_PARTY_NOTICES](THIRD_PARTY_NOTICES.md)

## Introduction

The Pixel Tablet Android 15 GSI (`AP3A.241005.015`) 9008 flashing package for the Lenovo Legion Y700 Gen 3 (TB321FU). The current release is user-v1.3 (internal build V132). Known issues are in [LOG](LOG.md#limitations).

### Key Points Up Front

1. This is a 9008 flashing package that can be flashed without unlocking the bootloader (BL). It is signed, and disabling vbmeta verification is not required. The package includes the complete Lenovo stock ZUI 17.0.12.044 9008 firmware, so you do not need to flash an official base image beforehand.
2. All features below are implemented rootless.
3. The system environment is not affected: detection apps report the same results as stock. The only exception is the "Global device spoofing" below, which is detected as an abnormal system mount when enabled. With it off, the environment is perfect.
4. Apart from Bluetooth hardware offload (A2DP offload), all hardware bugs encountered on this device have been fixed. Bluetooth works normally, though the fix is not perfect.
5. This package can be built automatically. With a Linux PC, you can replace the GSI and base-image versions and build it yourself (the base image and stock firmware must be supplied by you); see [TB321FU-GSI-Mods](https://github.com/CharlesGool/TB321FU-GSI-Mods).

The function of each module is described in [modules-user-v1.3](../modules-user-v1.3.md). This release includes 30 modules, with the same patch set as user-v1.2: all required modules plus 5 optional modules.

### Identity and Attestation

- Restores the real TB321FU identity (`ro.product.*`, fingerprint, and build descriptors taken from the stock firmware).
- Rootless key attestation engine: keybox import is supported, and RKP keys can be issued locally (refer to the functionality of the Oh My Keymint module).
- Global device spoofing (optional module `global-pif`): one-tap spoofing as a Pixel Tablet and other models. Spoofing as a Pixel model passes Play Integrity checks. It is currently the rootless approach with the least impact for passing Play attestation that has been found, but enabling it will be detected as an abnormal system mount. Leave it off if you do not want this.
- `herald-core`: root-free command and plugin entry point (`heraldctl`); the front-end app uses it to control system features.

### Camera

- Built-in Pixel Camera (Google Camera 4.4).
- Macro camera fix: the macro camera (camera 2) is available to third-party camera apps.

### Face Unlock

- New face unlock, ported from PixelOS's ParanoidSense (Megvii SDK). It uses the front camera and can be used for lock screen unlock and for apps and other non-payment scenarios. It is a WEAK (Class 2) biometric and cannot authorize payments or open StrongBox credentials.

### Display

- Auto brightness fix: restores the adaptive brightness toggle in Settings and uses Lenovo's stock brightness curve and response speed. The lowest manual level is restored to stock.
- Screen orientation fix: the Pixel Tablet system and this device have different default orientations, so apps that only support landscape (such as Bilibili fullscreen) no longer rotate upside down.
- Adaptive refresh rate fix: restores stock idle and touch timers and content detection. It downshifts when the screen is static, upshifts on touch, and follows the frame rate for video.
- Smooth display mode: in Settings, "Smooth display" on = no cap (panel up to 165Hz), off = 120Hz. The original Pixel system switches between 60Hz and 165Hz; 120Hz and 165Hz is more practical.
- Free rotation: auto-rotates at 90, 180 and 270 degrees, including portrait upside down.

### Network and Bluetooth

- 6GHz Wi-Fi band and country code fix; Wi-Fi APEX repackaged.
- Hotspot UI fix: the Pixel Tablet hides the WLAN hotspot entry by default. The Settings entry and Quick Settings tile are restored.
- Bluetooth audio fix: disables A2DP hardware offload and LE Audio, and uses vendor software encoding instead. Fixes headphones with no sound and callers not being heard.

### App Compatibility

- Ported Tango, which supports 32-bit APKs so that 32-bit apps can run (refer to OnePlus 12 Android 15 ColorOS).

### System Trimming

- Removes Pixel-exclusive apps and data, trims old VNDK, and removes Pixel hardware components this device does not have.
- Google app trimming: this release is level 3, which removes most Google apps, including accessibility apps such as TalkBack. Reinstall what you need.
- Cleans up GSI (phh/Mystic) leftovers.

### Trace Removal and Cleanup

- Disables debugging (stock adb root and debugging are on by default).
- Hides GSI identity traces (against GSI detection).
- Removes phh's writable system mount.
- Decompiled and removed the "Internal problem with the device" popup at boot.
- Unified the kernel build-user string, cleaned up expired prebuilts, and repackaged boot, re-signing it for this device's AVB.

### Interface

- The navigation bar can be hidden (supported in both tablet and phone modes).

### Stability Fixes

- SELinux rule fix: Enforcing on boot (stock was missing rules and reported errors).
- DeviceConnectionService domain fix: no longer crashes every 10 seconds.

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
7z x pixelos_tangorpro_ap3a.241005.015_user-v1.3_optional.7z.001
```

For a keep-data flash, run `flash_keep_data.bat`. Both scripts are in the root of the extracted directory.

## Usage

| File | Contents |
| --- | --- |
| `…user-v1.3_optional.7z.001`, `.002` | The 7z volumes of the complete 9008 flashing package, 2000 MiB each |
| `…user-v1.2_to_user-v1.3_patch.zip` | Patch for a keep-data upgrade from user-v1.2 to user-v1.3, 14MB |
| `SHA256SUMS.txt` | Checksums for the volumes and the patch; the sha256 of the concatenated complete package is in the notes of the corresponding Release |
| `module-list.md` | Module list for this release, same as [modules-user-v1.3](../modules-user-v1.3.md) |

### Using Face Unlock

Settings → Security & privacy → Device unlock → Face unlock → enter PIN → complete enrollment; afterward, point the front camera at your face on the lock screen to unlock. To delete: in Settings, face model → Delete. It is a WEAK biometric, and **do not** use it to protect payment or banking apps. The menu path follows the wording used in earlier versions and has not been step-by-step verified on user-v1.2.

### Version Naming

The public version is `user-vMAJOR.MINOR`, and the internal build number `V<数字>` is written into the image; user-v1.3 = V132.

## Upgrade

| From | Method |
| --- | --- |
| user-v1.2(V129) | Keep data, using the patch (14MB); steps below |
| user-v1.2(V129) | Keep data, using the full package: download the user-v1.3 full package, extract it, put the device into 9008 mode, and run `flash_keep_data.bat` |
| Other versions | Wipe data: run `flash.bat` from the full package |

Keep-data flashing only applies to a device already running this project's system. Verification: after boot, the version label in Settings should read `user-v1.3`.

### Upgrading from user-v1.2 to user-v1.3 with the Patch

Download `pixelos_tangorpro_ap3a.241005.015_user-v1.2_to_user-v1.3_patch.zip` from the Release. The patch modifies `image\super_4.img` (system) and `image\vbmeta_system.img`; all other files are byte-for-byte identical in both versions.

1. Locate the directory where the user-v1.2 complete 9008 package was extracted (the one containing `flash.bat`, `flash_keep_data.bat`, `image\`, and `tool\`). The `image\super_4.img` in it must be the original user-v1.2 file.
2. Extract the whole patch zip into this directory, overwriting files with the same names.
3. Double-click `apply_patch.bat`. It verifies the sha256 of `super_4.img`, uses xdelta3 to restore the user-v1.3 version and verifies it again. After it passes, it replaces the file and installs the user-v1.3 `vbmeta_system.img`. The old files are renamed to `super_4.user-v1.2.img.bak` and `vbmeta_system.user-v1.2.img.bak`. At least 2GB of free disk space is required.
4. Put the device into 9008 mode and run `flash_keep_data.bat`.
5. To roll back: rename the two `.bak` files back to their original names, then run `flash_keep_data.bat`.

The sha256 of the patch base `super_4.img` is `5b1da8f2a6ccf389d8e6fedb1f69fb3389e6dd8eb6d39fd112c1f3d802277f9b`, and the restored result is `70fcf1b3d41440e8d9eca791fc546ddd640c9f2568c2c6cb9cf595c4be135bc9`. The restored result has been verified on Linux using the `super_4.img` from the complete user-v1.2 package; `apply_patch.bat` has not been run on real Windows.

## Uninstall

There is no separate quick uninstall. For a full uninstall, re-flash the complete Lenovo stock ZUI 17.0.12 9008 package. All data will be erased.

## Acknowledgements

- The Pixel Tablet GSI from Mystic GSI, used as the base image.
- The attestation engine is forked from [ITxiao6666/OhMyKeymint](https://github.com/ITxiao6666/OhMyKeymint) (original author James Clef / qwq233).
- Lenovo's stock ZUI firmware and flashing tools.

For attribution and compliance information, see [THIRD_PARTY_NOTICES](THIRD_PARTY_NOTICES.md).

## License

No license has been chosen for this repository, and no license is granted. For the license status of each third-party component, see [THIRD_PARTY_NOTICES](THIRD_PARTY_NOTICES.md).
