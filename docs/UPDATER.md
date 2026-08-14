# CounterLab Updater

This document defines the public update-channel layout for CounterLab releases.

## Goals

The CounterLab updater should:

- cost nothing to host during Pre-Alpha/Alpha;
- use GitHub Releases for binary assets;
- use Tauri's updater signature verification;
- never require a GitHub personal access token in the installed application;
- keep the updater private signing key outside this public repository;
- keep Pre-Alpha, Alpha, and Stable channels independent;
- allow the user to choose when an available update is installed.

## Channel layout

CounterLab uses channel-specific static manifests rather than GitHub's `/releases/latest/` alias.

```text
updater/
  pre-alpha/
    latest.json
  alpha/
    latest.json
  stable/
    latest.json
```

Example endpoints:

```text
https://raw.githubusercontent.com/Wxyziii/CounterLab-Releases/main/updater/pre-alpha/latest.json
https://raw.githubusercontent.com/Wxyziii/CounterLab-Releases/main/updater/alpha/latest.json
https://raw.githubusercontent.com/Wxyziii/CounterLab-Releases/main/updater/stable/latest.json
```

This allows prerelease versions such as `0.1.0-pre-alpha.2` and `0.1.0-alpha.3` to remain GitHub prereleases while CounterLab still has a deterministic manifest for the channel installed on the user's PC.

## Tauri static manifest format

Tauri v2 static updater metadata requires a valid version and, for each supported target, a download URL and the **contents** of the generated updater signature.

For a Windows x64 Pre-Alpha target:

```json
{
  "version": "0.1.0-pre-alpha.1",
  "notes": "CounterLab Pre-Alpha update",
  "pub_date": "2026-08-14T16:00:00Z",
  "platforms": {
    "windows-x86_64": {
      "signature": "CONTENTS_OF_THE_GENERATED_SIG_FILE",
      "url": "https://github.com/Wxyziii/CounterLab-Releases/releases/download/v0.1.0-pre-alpha.1/COUNTERLAB_UPDATER_ARTIFACT"
    }
  }
}
```

Do not publish an active `latest.json` with placeholder values. The live channel manifest is created only after a real signed release artifact exists.

A non-active structural example is stored in [`updater/latest.example.json`](../updater/latest.example.json).

## Required release artifacts

A normal Windows release should contain, as applicable:

- a user-facing CounterLab Windows installer;
- the Tauri updater artifact produced by the build;
- the updater artifact's generated `.sig` file;
- release notes on the GitHub Release page;
- the CounterLab license agreement/notice distributed with that release.

The manifest URL must point to the artifact format accepted by the installed Tauri updater for that target. The private source repository's signed release workflow is responsible for using the actual artifact it built rather than a placeholder name.

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

The corresponding updater public key is not secret. Release builds compile it into CounterLab so installed applications can verify downloaded updates. Internal builds may intentionally omit it and show the signed updater as inactive.

Losing the private key can prevent existing installations from accepting future updates. Back it up securely outside the repositories.

## Publishing an update

The private CounterLab repository contains the controlled release workflow. At a high level it:

1. receives an explicit version, channel, and release notes;
2. validates the source candidate;
3. sets matching application versions;
4. builds with Tauri updater artifacts enabled;
5. signs the updater artifact using the private key supplied only through CI secrets;
6. verifies the installer/signature exist and computes SHA-256;
7. creates the matching release in this public repository;
8. uploads real installer/updater/signature assets;
9. creates/updates `updater/<channel>/latest.json` using the actual version, URL, date, notes, and signature;
10. commits the manifest only after the release assets exist.

Required private-repository GitHub Actions secrets are documented in CounterLab's internal release documentation. The release repository never receives the updater private key.

## First updater acceptance

Before relying on the updater for external testers, perform a real installed transition, for example:

```text
0.1.0-pre-alpha.1
        ↓
Check for updates
        ↓
0.1.0-pre-alpha.2
        ↓
signature verified
        ↓
install + restart
```

Verify that the update preserves:

- CounterLab SQLite data and match history;
- Steam/CS2 setup state and Credential Manager-backed authorization;
- language;
- Live display preference;
- Windows startup preference;
- single-instance/tray behavior.

A source-level or CI-only updater test is not a substitute for this installed-runtime acceptance.

## Rollout behavior

Recommended Pre-Alpha/Alpha behavior:

- the application may check for updates while idle/backgrounded;
- the user sees **Update available** in the main UI;
- installation is user-triggered through **Update now**;
- do not interrupt a live CS2 match with an updater prompt;
- if an update is discovered during a match, defer the visible prompt until CounterLab returns to the main post-match window;
- successful installation relaunches CounterLab where supported by the updater/installer flow.

## Failure behavior

CounterLab must fail safely when:

- the manifest cannot be reached;
- JSON is malformed;
- the target is missing;
- the update package cannot be downloaded;
- the updater signature is invalid;
- installation fails.

An updater failure must leave the existing CounterLab installation usable unless a future explicit minimum-version policy says otherwise.

## Security principle

The public release repository may be modified only by authorized maintainers, but update trust must not depend solely on repository access. Installed clients accept updater packages only when Tauri signature verification succeeds using the CounterLab updater public key compiled into that release channel.
