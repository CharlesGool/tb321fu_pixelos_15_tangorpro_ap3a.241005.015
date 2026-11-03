---
name: project-third-party-notices-en
description: Third-party attribution and compliance notices
metadata:
  version: "1.0.0"
  lang: "en"
---

# Third-Party Notices

## Multi-language

[简体中文](../THIRD_PARTY_NOTICES.md) | **English** | [Español](../es/THIRD_PARTY_NOTICES.md)

## Documentation

- Project overview: [README](README.md)

- Design rationale: [DESIGN](DESIGN.md)

- Project status: [LOG](LOG.md)
- Historical records: [HISTORY](HISTORY.md)
- Version changelog: [CHANGELOG](CHANGELOG.md)

- Third-party notices: [THIRD_PARTY_NOTICES](THIRD_PARTY_NOTICES.md)

## Third-Party Notices

### Components

| Component | Version or hash | Upstream URL | License | Usage | Copyright holder | Release obligations | Verified on |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Mystic GSI Pixel Tablet | `AP3A.241005.015`, incremental 12366759 | Not verified | Not verified | Base image, repackaged after modification | Not verified | Not verified | Not verified |
| Lenovo ZUI stock firmware and 9008 tools | ZUI 17.0.12.044 | Not verified | Not verified | Distributed in the 9008 package, including vendor, boot and other firmware and flashing tools | Lenovo | Not verified | Not verified |
| OhMyKeymint (attestation engine fork) | Baseline commit bafe5ba | https://github.com/ITxiao6666/OhMyKeymint | Not verified (upstream includes AGPL-3.0 text and an additional agreement by qwq233) | Built into `keymint` and `inject`, placed in the system image | James Clef / qwq233 | Not verified | Not verified |
| Tango (32-bit app binary translation) | v2.1.0 | Not verified | Not verified | Translator and related components placed in the system image | Not verified | Not verified | Not verified |
| Google Camera 4.4 | 4.4 | Not verified | Not verified | Installed as `system/app` | Google | Not verified | Not verified |

### License Texts

No license texts are available yet for components that have not been verified. Until they are added, this file does not grant any license for those components.

### Source Code Offer

The attestation engine source code is in the `engine/` directory of the [herald-core](https://github.com/CharlesGool/herald-core) repository. The other components are not verified.

### Compliance Review

Not yet done. OhMyKeymint is subject to copyleft terms, and there is no record yet of a distribution and separation analysis.
