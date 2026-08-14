# CounterLab Release Checklist

Use this checklist for every public CounterLab Alpha release.

## 1. Release readiness

- [ ] The intended private CounterLab source commit is identified and recorded internally.
- [ ] Version number is valid SemVer, for example `0.1.0-alpha.1`.
- [ ] Release build passes the project's required automated tests and packaging checks.
- [ ] No debug-only credentials, test secrets, plaintext passwords, development API keys, or private signing material are present in the build output.
- [ ] GSI configuration/install behavior is validated on a clean or representative Windows environment.
- [ ] Main-window ↔ Live-window lifecycle is validated.
- [ ] Match-end recovery is validated if CS2 closes/crashes unexpectedly.
- [ ] Automatic demo acquisition behavior is validated for every platform claimed as supported by the release.
- [ ] Existing user data/database migration is validated when schema or storage changes are included.

## 2. Alpha acceptance flow

- [ ] Install the new build over the previous Alpha version when upgrade compatibility is expected.
- [ ] Launch CounterLab normally.
- [ ] Verify optional Windows autostart can be enabled and disabled.
- [ ] Verify autostart/background launch does not unnecessarily open the main dashboard.
- [ ] Verify only one CounterLab backend instance/listener is active.
- [ ] Launch CS2 and remain in menus: Live View must not open merely because `cs2.exe` exists.
- [ ] Start a supported match: main CounterLab window hides and CounterLab Live opens automatically.
- [ ] Verify Live opens on the configured display.
- [ ] Verify live values update and no unsupported/private enemy information is exposed.
- [ ] Finish/exit the match: Live closes and main CounterLab returns to the correct match overview.
- [ ] Verify demo discovery/download starts automatically when supported.
- [ ] Verify parsing finishes and post-match metrics populate the same match record.
- [ ] Verify the user is not required to manually import a normal supported match demo.

## 3. Build and signing

- [ ] Tauri updater artifacts are enabled for the release build.
- [ ] Updater artifact is signed using the CounterLab updater **private key from secure build secrets**.
- [ ] Private updater key is not copied into this repository or release assets.
- [ ] Generated signature file is preserved for the release manifest.
- [ ] Human-facing installer is generated.
- [ ] Windows installer behavior is tested on a machine/environment that does not rely on the developer checkout.

## 4. Public repository preparation

- [ ] Move relevant entries from `CHANGELOG.md` → `Unreleased` into a dated version section.
- [ ] Prepare release notes using `docs/RELEASE_NOTES_TEMPLATE.md`.
- [ ] Mention significant known issues honestly.
- [ ] Mention data migration/reset requirements if any.
- [ ] Confirm all documentation and release notes contain no secrets or private repository information.

## 5. GitHub Release

- [ ] Create tag `v<version>`, for example `v0.1.0-alpha.1`.
- [ ] Create the GitHub Release in `Wxyziii/CounterLab-Releases`.
- [ ] Mark Alpha builds as prereleases.
- [ ] Upload the installer.
- [ ] Upload the Tauri updater artifact.
- [ ] Upload the generated updater `.sig` asset when part of the publishing workflow.
- [ ] Include/apply the CounterLab license agreement required for that release.
- [ ] Publish the user-facing release notes.

## 6. Update channel

- [ ] Confirm every URL that will appear in the Alpha manifest resolves successfully.
- [ ] Confirm the manifest contains the **contents** of the generated Tauri signature, not a path to the `.sig` file.
- [ ] Update `updater/alpha/latest.json` only after the release assets are live.
- [ ] Confirm `version`, `pub_date`, platform key, signature, and URL are correct.
- [ ] Do not modify `updater/stable/latest.json` for an Alpha-only release.

## 7. End-to-end updater validation

From an older supported CounterLab Alpha build:

- [ ] Check for updates.
- [ ] New version is detected exactly once.
- [ ] Release notes/version are displayed correctly.
- [ ] Update can be deferred.
- [ ] Update is not forced over an active CS2 match.
- [ ] **Update now** downloads the expected package.
- [ ] Signature verification succeeds.
- [ ] Installer completes.
- [ ] CounterLab restarts/returns correctly.
- [ ] Settings and user data expected to persist are intact.
- [ ] About/Settings shows the new version.
- [ ] A second update check reports no newer version.

## 8. Post-publication

- [ ] Download the installer from the public Release page and perform a final smoke test.
- [ ] Verify README download link reaches the correct Releases page.
- [ ] Monitor new Alpha bug reports.
- [ ] For a security-sensitive regression, remove/replace affected updater metadata promptly and follow `SECURITY.md`.
