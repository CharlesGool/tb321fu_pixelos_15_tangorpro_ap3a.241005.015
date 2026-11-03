---
name: project-log-en
description: Project bugs, limitations, decisions, and handoff
metadata:
  version: "1.0.0"
  lang: "en"
---

# Log

## Multi-language

[简体中文](../LOG.md) | **English** | [Español](../es/LOG.md)

## Documentation

- Project overview: [README](README.md)

- Design rationale: [DESIGN](DESIGN.md)

- Project status: [LOG](LOG.md)
- Historical records: [HISTORY](HISTORY.md)
- Version changelog: [CHANGELOG](CHANGELOG.md)

- Third-party notices: [THIRD_PARTY_NOTICES](THIRD_PARTY_NOTICES.md)

## Records

- [History](HISTORY.md)
- [Changelog](CHANGELOG.md)

## Bugs

No confirmed bugs.

## Limitations

- The system image ships with a backup keybox seed. It stops working once it expires or is revoked, after which key attestation requires the user to import a valid keybox. The seed bundled with user-v1.2 is valid until 2026-11-10 (source: project maintenance notes; not verified in the image). The seed in user-v1.3 has not been verified.
- The per-app permission hardening that cuts network and sensor access (similar to GrapheneOS) has been shelved and is not in the repository. The network part could use `cmd connectivity chain3`, and motion sensors can only be handled via Java hooks, which is quite difficult.
- Keep-data flashing only applies to a device already running this project's system.
- LE Audio is disabled; dual-mode headphones use classic Bluetooth.
- Face unlock is a WEAK biometric: it can unlock and do weak verification, but it cannot authorize payments or open StrongBox credentials.
- Trim level 3 removed accessibility apps (TalkBack, etc.) and most Google apps; reinstall what you need.
- The Bluetooth call fix targets the ZUI 17.0.12.044 vendor bundled in this package. If the device's vendor is replaced with another version, the fix may not apply (not verified).

## Decisions

| Date | Decision | Status | Reason |
| --- | --- | --- | --- |
| 2026-11-04 | One repository per base-image version | Accepted | PixelOS 15 tangorpro has several base-image versions |
| 2026-11-04 | Releases contain only the 9008 flashing package, not root variants | Accepted | Specified by the user |
| 2026-11-04 | 7z volumes are 2000 MiB each | Accepted | Below GitHub's 2 GiB per-asset limit |
| 2026-11-04 | Third-party licenses not yet verified when the repository is made public | Accepted | The user explicitly asked for the repository to be made public; verification is listed as a remaining step |

## Handoff

The current handoff is maintained in the [Simplified Chinese LOG.md](../LOG.md#交接).
