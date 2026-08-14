# CounterLab Releases

Official public distribution and update repository for **CounterLab**, a Windows desktop companion for Counter-Strike 2.

> **Alpha software:** CounterLab is under active development. Alpha builds may contain bugs, incomplete features, breaking changes, or data-format changes. Back up anything important and report reproducible issues.

## What this repository is

This repository exists to publish:

- official CounterLab Windows installers and updater bundles;
- Tauri updater channel metadata and updater signatures;
- release notes and version history;
- Alpha testing instructions;
- public bug reports, feature requests, and support information.

**CounterLab source code is proprietary and is not hosted in this repository.** This repository must never contain source code from the private CounterLab repository, updater private keys, API secrets, Steam credentials, Supabase secrets, access tokens, or other private material.

## Download CounterLab

Use the **Releases** section of this repository for official builds:

**https://github.com/Wxyziii/CounterLab-Releases/releases**

During Alpha, only download CounterLab from this repository or from a location explicitly linked by the CounterLab application.

### Current target

- Windows 10/11
- x64
- Counter-Strike 2 installed through Steam

Additional platforms are not currently part of the Alpha target.

## CounterLab Alpha experience

The Alpha is being built around an automatic match lifecycle:

1. CounterLab can optionally start with Windows and remain in the background.
2. CounterLab watches for CS2 and receives supported Game State Integration (GSI) telemetry.
3. When an actual supported match starts, the main CounterLab window is hidden and **CounterLab Live** opens automatically on the configured display.
4. CounterLab Live shows live match information available through supported telemetry and CounterLab's own calculations.
5. When the match finishes, the Live window closes and the main CounterLab window returns directly to that match's overview.
6. CounterLab discovers and downloads supported post-match demos automatically where the connected platform permits it.
7. The demo is parsed and the match overview is upgraded with verified post-match analysis.

The application is designed as an external companion. CounterLab does **not** require DLL injection, CS2 process-memory reading, automated gameplay input, or other invasive game modification for this workflow.

## Updates

CounterLab uses the Tauri updater model. Release builds are expected to include a built-in **Check for updates / Update now** flow.

CounterLab's Alpha channel uses a public `latest.json` manifest that points to the current updater package on GitHub Releases. The manifest contains the signature generated for that updater package, and the installed application verifies that signature using its embedded updater public key before accepting the update.

See [docs/UPDATER.md](docs/UPDATER.md) for the public release format and security rules.

## Reporting problems

Before opening an issue, check the existing issues and the [support guide](SUPPORT.md).

- **Bug:** use the Bug Report issue template.
- **Feature request:** use the Feature Request template.
- **Security vulnerability:** **do not file a public issue**. Follow [SECURITY.md](SECURITY.md).

When reporting an Alpha problem, include the CounterLab version, Windows version, CS2 mode/platform involved, reproduction steps, expected behavior, actual behavior, and relevant sanitized logs.

Never post Steam API keys, authentication codes, access tokens, passwords, private updater keys, session cookies, or other secrets in an issue.

## Changelog

See [CHANGELOG.md](CHANGELOG.md).

Each GitHub Release should also contain user-facing release notes describing important additions, fixes, known issues, and any migration or compatibility notes.

## Alpha testing

See [docs/ALPHA_TESTING.md](docs/ALPHA_TESTING.md) for the recommended acceptance flow used by testers.

## Licensing

CounterLab is proprietary software. Distribution of binaries through this public repository does **not** make CounterLab open source.

See [LICENSE.md](LICENSE.md). The complete CounterLab license agreement supplied with a release or application governs use of that release.

## Disclaimer

CounterLab is an independent project and is not affiliated with, endorsed by, sponsored by, or otherwise associated with Valve Corporation, Steam, Counter-Strike 2, or FACEIT. Counter-Strike, Counter-Strike 2, Steam, FACEIT, and related names and marks belong to their respective owners.

## Contact

Project owner: **Marcel Mikołaj Białk**  
Email: **marcelbialk008@gmail.com**
