# Changelog

All notable user-facing changes to CounterLab will be documented in this file.

The project follows the principles of [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) and uses Semantic Versioning-compatible version numbers for application releases.

## [Unreleased]

### Added

- Public CounterLab release and update repository.
- Release documentation, Pre-Alpha testing guidance, support policy, security reporting guidance, and issue templates.
- Guided first-run setup for language, Steam identity, CS2 match access, optional FACEIT, GSI, Live display and Windows startup.
- CounterLab Live second-window architecture for supported CS2 match telemetry.
- Windows background startup, system tray and single-instance behavior.
- Valve match-history discovery with truthful metadata-pending states for share-code-only historical records.
- Live/GSI-to-Steam match reconciliation for future matches when evidence is unambiguous.
- Manual local demo linking and verified deep match analysis as the first Pre-Alpha fallback.
- Official FACEIT Data API integration for account identity, ELO, skill level, statistics, ranking and recent match metadata once the service is configured.
- Signed Tauri updater architecture with separate `pre-alpha`, `alpha` and `stable` channels once release signing is activated.

### Changed

- The first limited tester release is classified as **Pre-Alpha** rather than Alpha.
- CounterLab Live opens once per match lifecycle rather than reopening at each round transition.
- Historical Steam records without verified metadata are labeled as Valve matches with metadata pending instead of fabricated/ambiguous match information.
- Sensitive CS2 match-access credentials are masked in normal UI and kept out of public release artifacts.

### Fixed

- Fixed CounterLab Live reopening/repositioning each round and potentially minimizing or stealing focus from CS2.
- Fixed post-final Live state transitions that could corrupt later Steam match reconciliation.
- Fixed future Live sessions being able to reuse an old match session identifier.
- Fixed manual demo linking so the selected local demo attaches to the selected match and can open the existing deep analyzer.

### Security

- CounterLab Live remains external and does not use CS2 process-memory access, injection, renderer hooks or gameplay automation.
- Live window is explicitly non-focusable.
- Updater private signing keys remain outside release artifacts and source control.
- FACEIT developer credentials remain server-side and are not shipped in the desktop application.
- Production CSP remains restrictive and allows only the specific Steam/FACEIT image hosts required by the UI.

### Known Pre-Alpha limitations

- Automatic Valve demo retrieval is not yet available; Valve sharing codes are not resolved through an undocumented Game Coordinator shortcut.
- Automatic FACEIT demo download requires separate FACEIT Downloads API approval/access; manual demo linking remains available.
- Real clean-install, Steam/CS2/GSI, multi-monitor and match-lifecycle acceptance must pass before the first limited external Pre-Alpha is published.
- Windows Authenticode signing may be absent initially, so SmartScreen can warn on a new installer even though CounterLab updater artifacts use their own cryptographic signatures once the updater channel is activated.

## Release format

CounterLab limited tester versions should use a Pre-Alpha prerelease identifier, for example:

- `0.1.0-pre-alpha.1`
- `0.1.0-pre-alpha.2`

Later Alpha versions can use:

- `0.1.0-alpha.1`
- `0.1.0-alpha.2`

Stable releases can later use versions such as `1.0.0`.

For every release:

1. Move completed entries from **Unreleased** into a new version section.
2. Add the release date in `YYYY-MM-DD` format.
3. Keep entries user-facing and specific.
4. Separate additions, changes, fixes, removals, deprecations, and security changes when relevant.
5. Do not publish secrets, exploit details, private infrastructure details, or internal credentials in the changelog.

Example:

```markdown
## [0.1.0-pre-alpha.1] - 2026-08-14

### Added
- First limited CounterLab Pre-Alpha build.

### Fixed
- Fixed an issue where ...

### Known issues
- ...
```
