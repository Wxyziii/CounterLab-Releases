# CounterLab Releases

Official public distribution and update repository for **CounterLab**, a proprietary Windows desktop companion for Counter-Strike 2.

> **Pre-Alpha software:** CounterLab is under active development. Pre-Alpha builds are intended for limited testing and may contain bugs, incomplete features, breaking changes, or data-format changes. Keep important local demos/backups and report reproducible issues.

## What this repository is

This repository exists to publish:

- official CounterLab Windows installers and updater bundles;
- Tauri updater channel metadata and updater signatures;
- release notes and version history;
- Pre-Alpha/Alpha testing instructions;
- public bug reports, feature requests, and support information.

**CounterLab source code is proprietary and is not hosted in this repository.** This repository must never contain source code from the private CounterLab repository, updater private keys, API secrets, Steam credentials, Supabase secrets, access tokens, or other private material.

## Download CounterLab

Use the **Releases** section of this repository for official builds:

**https://github.com/Wxyziii/CounterLab-Releases/releases**

During Pre-Alpha/Alpha, only download CounterLab from this repository or from a location explicitly linked by the CounterLab application.

### Current target

- Windows 10/11
- x64
- Counter-Strike 2 installed through Steam

Additional platforms are not currently part of the Pre-Alpha target.

## CounterLab Pre-Alpha experience

The first limited tester build is centered on the core installed-app lifecycle:

1. A fresh user receives guided setup for language, Steam identity, CS2 match access, optional FACEIT, CounterLab GSI, Live display and optional Windows startup.
2. CounterLab can start quietly with Windows and remain available through the system tray when the user enables that option.
3. CounterLab receives supported CS2 Game State Integration (GSI) telemetry through its local authenticated endpoint.
4. When a supported real match starts, the main CounterLab window is hidden and **CounterLab Live** opens once on the configured display.
5. Live updates throughout the match without reopening/repositioning every round and is configured not to take keyboard focus from CS2.
6. When the match finishes or telemetry is interrupted, Live closes/restores safely and the main CounterLab window returns to the Match Overview.
7. Valve match-history sync can attach the later sharing code to the same Live-backed record when the evidence is unambiguous.
8. For the first Pre-Alpha, the user can link/import a local demo to unlock verified deep analysis on that same match record.

Automatic Valve replay retrieval is **not** presented as a finished Pre-Alpha feature. Valve's sharing-code path currently does not provide CounterLab with a documented public REST replay resolver, so manual/local demo linking remains the supported fallback instead of using an undocumented Game Coordinator shortcut.

FACEIT account tracking uses its official Data API once CounterLab's server-side service is configured. Automatic FACEIT demo download additionally requires separate FACEIT Downloads API access and is not claimed as working until that access is approved and validated.

The application is designed as an external companion. CounterLab does **not** require DLL injection, CS2 process-memory reading/writing, renderer hooks, automated gameplay input, or other invasive game modification for this workflow.

## Updates

CounterLab contains a signed Tauri updater architecture with separate channels for:

- `pre-alpha`
- `alpha`
- `stable`

Internal builds may intentionally show the updater as inactive. Public updater-enabled builds contain only the updater **public verification key**. The private signing key remains outside both repositories and is used only by the controlled release workflow.

A channel's `latest.json` manifest is published only after the corresponding signed release artifact exists. Installed CounterLab verifies the updater signature before accepting an update.

See [docs/UPDATER.md](docs/UPDATER.md) for the public release format and security rules.

## Reporting problems

Before opening an issue, check the existing issues and the [support guide](SUPPORT.md).

- **Bug:** use the Bug Report issue template.
- **Feature request:** use the Feature Request template.
- **Security vulnerability:** **do not file a public issue**. Follow [SECURITY.md](SECURITY.md).

When reporting a Pre-Alpha/Alpha problem, include the CounterLab version, Windows version, CS2 mode/platform involved, reproduction steps, expected behavior, actual behavior, and relevant sanitized logs.

Never post Steam API keys, Game Authentication Codes, access tokens, passwords, private updater keys, session cookies, or other secrets in an issue.

## Changelog

See [CHANGELOG.md](CHANGELOG.md).

Each GitHub Release should also contain user-facing release notes describing important additions, fixes, known issues, and any migration or compatibility notes.

## Testing

See [docs/ALPHA_TESTING.md](docs/ALPHA_TESTING.md) for the acceptance flow. The same checklist is used during the limited Pre-Alpha, with automatic demo retrieval treated as an Alpha roadmap item rather than a Pre-Alpha release gate.

## Licensing

CounterLab is proprietary software. Distribution of binaries through this public repository does **not** make CounterLab open source.

See [LICENSE.md](LICENSE.md). The complete CounterLab license agreement supplied with a release or application governs use of that release.

## Disclaimer

CounterLab is an independent project and is not affiliated with, endorsed by, sponsored by, or otherwise associated with Valve Corporation, Steam, Counter-Strike 2, or FACEIT. Counter-Strike, Counter-Strike 2, Steam, FACEIT, and related names and marks belong to their respective owners.

## Contact

Project owner: **Marcel Mikołaj Białk**  
Email: **marcelbialk008@gmail.com**
