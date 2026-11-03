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

The Pixel Tablet Android 15 GSI (`AP3A.241005.015`) 9008 flashing package for the Lenovo Legion Y700 Gen 3 (TB321FU). The current release is user-v1.2 (internal build V129). Known issues are in [LOG](LOG.md#limitations).

### Why This Package Exists

1. The Lenovo system is hard to use, and I prefer a stock-like Pixel OS.
2. I want some advanced features without rooting, and without troublesome environment detection.
3. I have Claude Max 20x 🤣

### Key Points Up Front

1. This is a 9008 flashing package that can be flashed without unlocking the bootloader (BL). It is signed, and disabling vbmeta verification is not required. The package includes the complete Lenovo stock ZUI 17.0.12.044 9008 firmware, so you do not need to flash an official base image beforehand.
2. All features below are implemented rootless.
3. The system environment is not affected: detection apps report the same results as stock. The only exception is the "Global device spoofing" below, which is detected as an abnormal system mount when enabled. With it off, the environment is perfect.
4. Apart from Bluetooth hardware offload (A2DP offload), all hardware bugs encountered on this device have been fixed. Bluetooth works normally, though the fix is not perfect.
5. This package can be built automatically. With a Linux PC, you can replace the GSI and base-image versions and build it yourself (the base image and stock firmware must be supplied by you); see [TB321FU-GSI-Mods](https://github.com/CharlesGool/TB321FU-GSI-Mods).

The function of each module is described in [modules-user-v1.2](../modules-user-v1.2.md). This release includes 30 modules: all required modules plus 5 optional modules.

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

### Modules Not Included in This Release

These modules are in the repository but are not included in user-v1.2. Test status is the author's own record.

Everyday features:

- Refresh rate control (`refresh-control`): `heraldctl refresh` locks or limits the rate to 30~165Hz. Passed stability testing.
- Automatic refresh rate switching by app or battery (`refresh-auto-switch`): depends on refresh rate control. Passed stability testing.
- Battery management (`battery`): battery life view, long-term plug-in protection, charge limit, and bypass charging. The nodes and values come from decompiling Lenovo's battery HAL. Passed stability testing.
- Hotspot control (`hotspot-control`): custom hotspot name, password, encryption, band, and `heraldctl wifi`. Not very stable; the fixed bandwidth still has some issues.
- Unlock 6GHz hotspot (`hotspot-6ghz-unlock`): removes the capability bit restriction, the channel list, and the three gates in the settings page. Passed stability testing.
- Unlimited HBM (`brightness/hbm-unlimited`): removes the 5-minute time limit at 782 nits. Passed stability testing.
- Per-app spoofing (`spoof/app-spoof`): spoofs Build.* per app and depends on global-pif's boot script. Passed stability testing, but it can be detected, so it was not shipped.

Advanced features (not included by default):

- Status bar network speed (`statusbar-netspeed`): does not modify the SystemUI APK and uses a framework hook. Passed stability testing, but it looks a bit ugly, so it was not shipped.
- Developer options hiding (`devopts-hide`): apps on the list read 0 for developer options and ADB status. Not very stable; some apps can still read the real value.
- Custom font (`custom-font`): reads font packs from `/data/fonts/herald` and does not occupy system. Untested.
- App backup and restore (`app-backup`): backs up APKs (including splits) and data to a specified directory, not on a schedule. Implemented, untested.
- Game mode (`game-mode`): game list, foreground trigger, exit methods on lock, and automatic Do Not Disturb. Not very stable.
- Performance tuning (`perf`): CPU/GPU frequency limits, one-tap power saving, balanced and performance profiles, and temperature readings. Passed stability testing.
- Game performance boost (`perf-game-boost`): performance profile hooks for game mode. Not very stable.
- Overlay cache self-healing (`overlay-idmap-reset`): deletes old idmap files at boot to prevent idmap2d crashes. Passed stability testing.

Additional trimming:

- Accessibility app trimming (`slim/accessibility`): removes screen readers and similar apps; people who need a screen reader should not use it. Passed stability testing (already removed in this release along with Google app level 3).
- Google app trimming (`slim/google-apps`): removes pre-installed Google apps, Assistant, and TTS data. Passed stability testing (this release already trimmed them per level 3).

Debugging and research (not needed for normal use):

- adb log capture (`shell-logcat`), and ADB enabled automatically at boot (`adb-on-boot`, no authorization needed).
- adb root (`rooted-adbd`, `ro.debuggable=1`, adbd and shell domains permissive).
- Root read-only commands (`herald-readonly-shell`, off by default) and root shell (`herald-rooted-shell`, off by default, time-limited).
- zygote timing measurement (`herald-zygisk-timing-probe`), zygote injection-point verification (`herald-zygisk-fork-observer`), and boot camera logging (`diag-boot-camera-log`).

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
