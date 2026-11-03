---
name: project-changelog-en
description: Changelog
metadata:
  version: "1.0.0"
  lang: "en"
---

# Changelog

## Multi-language

[简体中文](../CHANGELOG.md) | **English** | [Español](../es/CHANGELOG.md)

## Documentation

- Project overview: [README](README.md)

- Design rationale: [DESIGN](DESIGN.md)

- Project status: [LOG](LOG.md)
- Historical records: [HISTORY](HISTORY.md)
- Version changelog: [CHANGELOG](CHANGELOG.md)

- Third-party notices: [THIRD_PARTY_NOTICES](THIRD_PARTY_NOTICES.md)

## Changelog

### user-v1.2(V129)- 2026-11-04

- Added: The first release of this repository, providing the complete 9008 flashing package volumes, `SHA256SUMS.txt`, and the module list.
- Fixed: Bluetooth. `vendor-bind` now grants the `update_engine` domain `mounton` and read access to `vendor_file`, so Bluetooth audio policy and SCO binds take effect under Enforcing.
