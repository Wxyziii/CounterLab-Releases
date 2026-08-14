# CounterLab Updater

This document defines the public update-channel layout for CounterLab releases.

## Goals

The CounterLab updater should:

- cost nothing to host during Alpha;
- use GitHub Releases for binary assets;
- use Tauri's updater signature verification;
- never require a GitHub personal access token in the installed application;
- keep the updater private signing key outside this public repository;
- support an Alpha channel now and a Stable channel later;
- allow the user to choose when an available update is installed.

## Recommended channel layout

CounterLab should use channel-specific static manifests rather than depending on GitHub's `/releases/latest/` alias for Alpha builds.

Planned public paths:

```text
updater/
  alpha/
    latest.json
  stable/
    latest.json
```

The Alpha application can use an endpoint equivalent to:

```text
https://raw.githubusercontent.com/Wxyziii/CounterLab-Releases/main/updater/alpha/latest.json
```

A future stable application can use:

```text
https://raw.githubusercontent.com/Wxyziii/CounterLab-Releases/main/updater/stable/latest.json
```

This allows GitHub releases carrying SemVer prerelease versions such as `0.1.0-alpha.3` to remain GitHub prereleases without relying on GitHub's definition of the repository's "latest" non-prerelease release.

## Tauri static manifest format

Tauri v2 static updater metadata requires a valid version and, for each supported target, a download URL and the **contents** of the generated updater signature.

For the current Windows x64 Alpha target:

```json
{
  "version": "0.1.0-alpha.1",
  "notes": "CounterLab Alpha update",
  "pub_date": "2026-08-14T16:00:00Z",
  "platforms": {
    "windows-x86_64": {
      "signature": "CONTENTS_OF_THE_GENERATED_SIG_FILE",
      "url": "https://github.com/Wxyziii/CounterLab-Releases/releases/download/v0.1.0-alpha.1/COUNTERLAB_UPDATER_BUNDLE"
    }
  }
}
```

Do not publish an active `latest.json` with placeholder values. Tauri validates the manifest, so the live channel manifest should be created only when a real signed updater bundle exists.

A non-active example is stored in [`updater/latest.example.json`](../updater/latest.example.json).

## Required release artifacts

A normal Windows Alpha release should contain, as applicable:

- a user-facing CounterLab Windows installer;
- the Tauri updater artifact produced by the build;
- the updater artifact's generated `.sig` file;
- release notes on the GitHub Release page;
- the CounterLab license agreement distributed with that release when required by the application/release process.

Exact generated file names may change with the Tauri bundler configuration. The manifest URL must point to the updater artifact expected by the installed CounterLab build, not merely to the human-facing installer.

## Signing-key rules

### Private key

The updater signing private key is a secret.

It must **never** be:

- committed to this repository;
- committed to the private source repository;
- placed in `latest.json`;
- embedded in the application;
- attached to a GitHub Release;
- pasted into an issue, log, screenshot, or release note.

For automated builds, store the private key and any password needed to use it in the private build/release system's encrypted secrets.

### Public key

The corresponding updater public key is not secret. It belongs in the CounterLab Tauri updater configuration so installed applications can verify downloaded updates.

Losing the private key can prevent existing installations from accepting future updates. Back it up securely outside the repositories.

## Publishing an Alpha update

At a high level:

1. Prepare and validate the release in the private CounterLab source repository.
2. Set the application version to the intended SemVer prerelease version.
3. Build with Tauri updater artifacts enabled.
4. Sign the updater artifact using the CounterLab updater private key.
5. Create the matching tag/release in this repository.
6. Upload the installer, updater artifact, and generated signature.
7. Create/update `updater/alpha/latest.json` with:
   - the exact version;
   - release notes/summary;
   - RFC 3339 publication date;
   - exact updater artifact URL;
   - exact contents of the generated signature file.
8. Test update discovery from an older installed CounterLab Alpha build.
9. Test download, signature validation, installation, restart, and post-update version display.

Only update the live Alpha manifest after all referenced release assets exist.

## Rollout behavior

Recommended Alpha behavior:

- background startup may check for updates;
- the application may show "Update available" in the main UI;
- installation is user-triggered through **Update now**;
- do not force-install ordinary Alpha updates while the user is in a live CS2 match;
- if an update is discovered during a match, defer the visible prompt until CounterLab returns to the main post-match window;
- never replace the running Live match workflow with an updater prompt.

## Failure behavior

CounterLab should fail safely when:

- the manifest cannot be reached;
- JSON is malformed;
- the target is missing;
- the update package cannot be downloaded;
- the updater signature is invalid;
- installation fails.

An updater failure must not prevent the existing installed CounterLab version from launching normally unless there is a separate explicit minimum-version policy in the future.

## Security principle

The public release repository may be modified only by authorized maintainers, but update trust must not depend solely on repository access. Installed clients should accept updater packages only when Tauri signature verification succeeds using the embedded CounterLab updater public key.
