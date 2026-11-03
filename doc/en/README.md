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

This project replaces ZUI on the TB321FU with the Pixel Tablet (`tangorpro`) Android 15 GSI, and adds the GSI features and fixes this device is missing. The base is `AP3A.241005.015` from Mystic GSI; vendor and boot come from Lenovo's stock ZUI 17.0.12.

The current release, user-v1.2 (internal build V129), provides:

- Pixel system with its identity restored to the original device model, passing Play Integrity checks.
- Face unlock, free rotation, hidden navigation bar, and smooth display modes (up to 165 Hz).
- Hardware fixes for Bluetooth audio, 6 GHz hotspot, auto brightness, adaptive refresh rate, and macro camera.
- 32-bit app support and the Pixel Camera.
- `herald-core`: the command and plugin entry point in the system.

The module list is in [modules-user-v1.2](../modules-user-v1.2.md). Patches and the build system are in [TB321FU-GSI-Mods](https://github.com/CharlesGool/TB321FU-GSI-Mods). PixelOS 15 tangorpro has several base-image versions, each with its own repository; this repository only covers `AP3A.241005.015`.

## Requirements

- Lenovo Legion Y700 Gen 3 TB321FU, able to enter 9008 (EDL) mode.
- A Windows PC, a USB data cable, and 7-Zip.
- Keep-data flashing only applies to a device already running this project's system; in all other cases, use the wipe-data flash.

## Install

### Quick Install

Download all volumes (`.7z.001`, `.7z.002`) from [Releases](https://github.com/CharlesGool/tb321fu_pixelos_15_tangorpro_ap3a.241005.015/releases/latest) into the same directory. Extract `.7z.001` with 7-Zip. Once the device is in 9008 mode, run `flash.bat` (wipe data) in the extracted directory.

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

Version naming: the public version is `user-vMAJOR.MINOR`, and the internal build number `V<数字>` is written into the image; user-v1.2 = V129.

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
