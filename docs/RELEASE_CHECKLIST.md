# CounterLab Release Checklist

Use this checklist for every public CounterLab Pre-Alpha, Alpha, or Stable release. Apply only the feature gates that the release actually claims; do not turn future Alpha roadmap items into false Pre-Alpha blockers.

## 1. Release readiness

- [ ] The intended private CounterLab source commit is identified and recorded internally.
- [ ] Version number is valid SemVer, for example `0.1.0-pre-alpha.1` or `0.1.0-alpha.1`.
- [ ] Release build passes the project's required automated tests and a real packaged Windows/NSIS build.
- [ ] No debug-only credentials, test secrets, plaintext passwords, development provider keys, local user database, or private signing material are present in the build output.
- [ ] Fresh-install onboarding is validated on a clean Windows user/VM.
- [ ] Existing-user upgrade/database persistence is validated when compatibility is expected.
- [ ] GSI configuration/install behavior is validated on a clean or representative Windows environment.
- [ ] Main-window ↔ Live-window lifecycle is validated in a real supported CS2 match.
- [ ] CounterLab Live opens once per match and does not reload/reposition each round.
- [ ] CounterLab Live does not minimize or steal focus from CS2.
- [ ] Match-end/crash/disconnect recovery restores the main application safely.
- [ ] Manual local demo linking/deep analysis works for Pre-Alpha.
- [ ] Automatic demo acquisition is validated only for platforms/builds where the release explicitly claims it is supported.

## 2. Pre-Alpha core acceptance flow

- [ ] Fresh install contains no previous/developer Steam identity, credentials, match history, or database state.
- [ ] Guided setup covers language, Steam, CS2 match access, GSI, Live display, startup choice, and optional integrations that are active.
- [ ] English/Polish switching works and Polish characters render correctly.
- [ ] Steam identity and CS2 match access validate with real user values without exposing credentials in logs/UI.
- [ ] Optional Windows autostart can be enabled/disabled.
- [ ] Background launch does not unnecessarily force the main dashboard open.
- [ ] Only one CounterLab backend/listener/tray instance exists.
- [ ] Launch CS2 and remain in menus: Live must not open merely because `cs2.exe` exists.
- [ ] Start a supported match: main CounterLab hides and CounterLab Live opens automatically once.
- [ ] Live opens on the configured display and continues through round transitions without focus/reload problems.
- [ ] Displayed live data is limited to supported/direct/derived data; no fabricated/private enemy information is exposed.
- [ ] Finish/exit the match: Live closes and main CounterLab returns to the correct match overview.
- [ ] Later Steam sync does not create a duplicate if the sharing code can be reconciled to the Live-backed match unambiguously.
- [ ] Link/import the correct local demo and verify deep analysis enriches the same match record.

## 3. Optional/platform integration acceptance

### FACEIT

When the release claims FACEIT account tracking:

- [ ] Server-side FACEIT Data API service is deployed and configured.
- [ ] Correct player nickname, ELO, skill level, region/country and recent matches are returned from a verified Steam identity.
- [ ] Desktop/log output contains no FACEIT developer API key.
- [ ] If Downloads API access is absent, UI says automatic FACEIT demo download is unavailable rather than pretending it works.

When the release claims automatic FACEIT demo acquisition:

- [ ] Approved FACEIT Downloads API access is configured server-side.
- [ ] Match resource URL is exchanged for a signed download URL through the supported Downloads API.
- [ ] Download/retry/parser/reconciliation behavior passes end to end.

### Valve automatic replay acquisition

Do not check this box for the first limited Pre-Alpha unless a supported/reviewed resolver is actually present:

- [ ] Valve sharing-code/replay resolution is implemented through an accepted mechanism and end-to-end demo download passes without memory access, injection, gameplay automation, fabricated URLs, or unreviewed undocumented session behavior.

## 4. Build and updater signing

For updater-enabled releases:

- [ ] Tauri updater artifacts are enabled for the release build.
- [ ] Updater artifact is signed using the CounterLab updater **private key from secure build secrets**.
- [ ] Private updater key is not copied into either repository or release assets.
- [ ] Public updater verification key is compiled into the release build.
- [ ] Generated signature file is preserved for the release manifest.
- [ ] Human-facing Windows installer is generated.
- [ ] Windows installer behavior is tested on a machine/environment that does not rely on the developer checkout.

For an internal/manual-install Pre-Alpha candidate where the signed updater has not yet been activated, mark this explicitly in release notes rather than presenting the updater as active.

## 5. Public repository preparation

- [ ] Move relevant entries from `CHANGELOG.md` → `Unreleased` into a dated version section.
- [ ] Prepare release notes using `docs/RELEASE_NOTES_TEMPLATE.md`.
- [ ] Mention significant known issues honestly.
- [ ] Mention data migration/reset requirements if any.
- [ ] State whether automatic Valve/FACEIT demo acquisition is available in this exact build.
- [ ] State whether signed in-app updates are active in this exact build.
- [ ] Confirm all documentation/release notes contain no secrets or private repository implementation details that should remain confidential.

## 6. GitHub Release

- [ ] Create tag `v<version>`, for example `v0.1.0-pre-alpha.1`.
- [ ] Create the GitHub Release in `Wxyziii/CounterLab-Releases`.
- [ ] Mark Pre-Alpha/Alpha builds as prereleases.
- [ ] Upload the real installer.
- [ ] Upload the Tauri updater artifact/signature when the updater is active.
- [ ] Include/apply the CounterLab license agreement/notice required for that release.
- [ ] Publish the user-facing release notes.
- [ ] Verify the installer SHA-256 recorded in the release process.

## 7. Update channel

For an updater-enabled release:

- [ ] Confirm every URL that will appear in the selected channel manifest resolves successfully.
- [ ] Confirm the manifest contains the **contents** of the generated Tauri signature, not a path to the `.sig` file.
- [ ] Update `updater/<channel>/latest.json` only after real release assets are live.
- [ ] Confirm `version`, `pub_date`, platform key, signature, and URL are correct.
- [ ] Do not modify another channel's manifest accidentally.

Channels:

```text
pre-alpha
alpha
stable
```

## 8. End-to-end updater validation

Before relying on signed updates for testers, test a real installed transition, for example:

`0.1.0-pre-alpha.1 → 0.1.0-pre-alpha.2`

- [ ] New version is detected exactly once.
- [ ] Correct channel/release notes/version are displayed.
- [ ] Update can be deferred.
- [ ] Update is not forced over an active CS2 match.
- [ ] **Update now** downloads the expected package.
- [ ] Signature verification succeeds.
- [ ] Installer completes and CounterLab restarts/returns correctly.
- [ ] SQLite data, account setup, language, Live display, autostart and expected local data persist.
- [ ] Only one CounterLab process/tray/backend instance exists after restart.
- [ ] About/Settings shows the new version.
- [ ] A second update check reports no newer version.

## 9. Post-publication

- [ ] Download the installer from the public Release page and perform a final smoke test.
- [ ] Verify README download link reaches the correct Releases page.
- [ ] Monitor new Pre-Alpha/Alpha bug reports.
- [ ] For a security-sensitive regression, remove/replace affected updater metadata promptly and follow `SECURITY.md`.
