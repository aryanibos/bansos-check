# Changelog

All notable changes to bansos-check are documented in this file.

The project follows Semantic Versioning.

## [Unreleased]

### Changed

- Moved the canonical skill to `skills/bansos-check/SKILL.md`, matching the repository layout of aryanibos/arx-backend.
- Rewrote the README in the same house style: badges, principle callout, verdict table, worked example.

### Added

- `LICENSE` (MIT), `CONTRIBUTING.md`, `.gitignore`, and `.gitattributes`.
- Expanded security coverage in the skill: threat model (credentials/sessions, machine access, wallet drainers, API keys, fees), ClickFix paste-instruction pattern, wallet signature/approval drainer mechanics, APK sideloading and out-of-store extension risks, QR-code and support-DM funnels, red-flag quick list, an explicit verdict rubric, and a full incident-mode containment checklist (session/OAuth revocation, wallet approval revocation, persistence checks, mailbox-rule traps).

## [0.1.0] - 2026-11-07

### Added

- Initial release of the `bansos-check` skill: a read-only evaluation procedure for freebie/giveaway offers with AMAN / HATI-HATI / JANGAN verdicts.
- Automatic JANGAN categories: pipe-to-shell installs, unknown remote-control agents, logins on non-official domains, API key / seed phrase requests, and activation fees.
- Worked example based on a real evaluation (superbot.gg "free Claude Opus credits" Telegram post).
