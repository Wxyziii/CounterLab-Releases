# Changelog

All notable user-facing changes to CounterLab will be documented in this file.

The project follows the principles of [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) and uses Semantic Versioning-compatible version numbers for application releases.

## [Unreleased]

### Added

- Public CounterLab release and update repository.
- Release documentation, Alpha testing guidance, support policy, security reporting guidance, and issue templates.

### Changed

- Nothing yet.

### Fixed

- Nothing yet.

### Security

- Nothing yet.

## Release format

CounterLab Alpha versions should use a prerelease identifier, for example:

- `0.1.0-alpha.1`
- `0.1.0-alpha.2`
- `0.2.0-alpha.1`

Stable releases can later use versions such as `1.0.0`.

For every release:

1. Move completed entries from **Unreleased** into a new version section.
2. Add the release date in `YYYY-MM-DD` format.
3. Keep entries user-facing and specific.
4. Separate additions, changes, fixes, removals, deprecations, and security changes when relevant.
5. Do not publish secrets, exploit details, private infrastructure details, or internal credentials in the changelog.

Example:

```markdown
## [0.1.0-alpha.1] - 2026-08-14

### Added
- First CounterLab Alpha build.

### Fixed
- Fixed an issue where ...

### Known issues
- ...
```
