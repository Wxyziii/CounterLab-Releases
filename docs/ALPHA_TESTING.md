# CounterLab Pre-Alpha / Alpha Testing Guide

Thank you for testing CounterLab. The first limited Pre-Alpha is intended to find real-world failures in installation, onboarding, Steam/CS2 setup, Live View, match discovery, local demo linking, analysis, updates, and recovery behavior.

Automatic Valve/FACEIT demo retrieval is an Alpha roadmap item unless the required supported replay/download access is available in the build being tested.

## Before testing

- Install only an official build from this repository's Releases page.
- Keep CS2 and Steam updated.
- Do not share Steam API keys, CS2 Game Authentication Codes, access tokens, passwords, or other secrets in public bug reports.
- Expect Pre-Alpha/Alpha builds to change frequently.
- Keep original local demos while testing deep analysis.

## Clean first-run test

Prefer a clean Windows user profile or disposable VM for this test.

1. Install CounterLab with no previous CounterLab AppData/Credential Manager entries.
2. Open the application normally.
3. Confirm the guided onboarding appears automatically.
4. Confirm no developer/test Steam identity, authentication code, sharing code, match history, or previous-user data is present.
5. Choose English or Polish and verify Polish characters render correctly when selected.
6. Sign in through the official Steam browser flow.
7. Configure/validate CS2 match access.
8. Optionally connect FACEIT if that integration is active in the build; skipping it must not block setup.
9. Install/repair CounterLab's GSI configuration.
10. Select the display to use for CounterLab Live.
11. Optionally enable **Start CounterLab with Windows**.
12. Complete the validation step and enter the normal application.
13. Restart CounterLab once and verify saved settings persist.
14. If autostart is enabled, restart Windows at a convenient time and verify CounterLab starts in the intended background state rather than forcing the main dashboard open.

## Existing-user upgrade test

Install a newer candidate over an existing CounterLab installation and verify these survive:

- Steam identity and match access;
- existing matches and analysis;
- language;
- GSI configuration/state;
- Live monitor preference;
- Windows startup preference;
- local database migrations.

An upgrade should preserve the same user's state. A genuine clean install should not contain another user's state.

## Match lifecycle test

### Before the match

1. Open or leave CounterLab running in the background.
2. Launch CS2.
3. Stay in the CS2 menus for a short period.
4. Confirm CounterLab Live does **not** open merely because CS2 is running.

### When the match starts

For a supported Premier/Competitive match:

1. Confirm the main CounterLab window hides automatically.
2. Confirm CounterLab Live opens automatically **once**.
3. Confirm it opens on the configured display.
4. Confirm CS2 is not minimized and does not lose keyboard/mouse focus because Live opened.
5. Confirm Live does **not** reload/reposition when a round ends and the next round begins.
6. Confirm available live stats change as the match progresses.
7. Confirm the UI remains responsive through round transitions, death/spectating states, halftime/side changes, overtime when applicable, and reconnects when applicable.

If the build cannot reliably distinguish Premier from classic Competitive through its supported telemetry, report the generic mode presentation as a labeling issue rather than expecting CounterLab to invent platform metadata.

### When the match ends

1. Finish the match normally.
2. Confirm CounterLab Live closes or transitions out of the live state automatically.
3. Confirm the main CounterLab window returns automatically.
4. Confirm CounterLab opens the overview for the match that just ended rather than an unrelated previous match.
5. Confirm the initial Live/GSI-collected summary is visible when available.
6. Allow Steam match-history sync to run and confirm the later sharing code attaches to the same Live-backed record when CounterLab can reconcile it unambiguously.
7. Confirm no duplicate match is created for that one played match.

## Manual demo fallback — required for Pre-Alpha

Until automatic replay acquisition is active for the platform:

1. Obtain/keep the local demo normally.
2. Select the correct CounterLab match.
3. Use **Link demo… / Add demo…** and select the correct `.dem` file.
4. Confirm the selected demo attaches to that same match record.
5. Run/open deep analysis.
6. Confirm parsed map/round/player/tactical evidence belongs to the correct match.
7. Confirm deep analysis does not create a second duplicate match.
8. Confirm an incomplete/corrupt/changed demo fails safely instead of replacing verified evidence silently.

Historical Valve share-code-only records may remain `Valve Match #… / metadata pending` until a real demo or another verified metadata source enriches them. This is preferable to fabricated map/score/date information.

## Automatic demo test — only when explicitly enabled

Do **not** fail the first limited Pre-Alpha solely because this section is unavailable.

When a build explicitly says automatic acquisition is supported for the connected platform:

- verify the match queues the correct replay job;
- verify the replay/download URL came from a supported platform path;
- verify download progress and restart recovery;
- verify incomplete files are never parsed;
- verify the completed demo enriches the existing match rather than creating a duplicate;
- verify expired/unavailable resources produce a truthful retry/error state.

For FACEIT, Data API demo resource discovery and Downloads API signed-file access are separate capabilities. Do not treat a discovered resource URL as proof that automatic download is enabled.

## Recovery tests

Please test these separately when convenient:

- close CounterLab Live during an active match;
- close CS2 unexpectedly;
- disconnect/reconnect to a match;
- lose network connectivity temporarily;
- start CounterLab after CS2 is already running;
- start CounterLab after a supported match has already begun;
- disconnect the selected secondary monitor;
- run CounterLab after a Windows restart with autostart enabled;
- manually open CounterLab while its background instance is already running.

Expected behavior: CounterLab should recover without leaving an invisible stuck process, duplicate backend listeners, duplicate matches, or a permanently hidden main window.

## Update test

Run this only after the signed updater is active in the build.

For the first real acceptance, test a complete installed transition such as:

`0.1.0-pre-alpha.1 → 0.1.0-pre-alpha.2`

1. Open CounterLab outside an active match.
2. Use **Check for updates**.
3. Confirm the offered version and channel are correct.
4. Confirm you can defer the update.
5. Choose **Update now**.
6. Confirm the signed update downloads and installs without manually downloading a new installer.
7. Confirm CounterLab restarts/returns and displays the new version.
8. Confirm settings, account setup, match data and autostart state persisted.
9. Confirm only one CounterLab instance/tray icon exists after the update.

If an update becomes available during an active match, normal update UI should not replace or interrupt the Live View.

## FACEIT test

When the server-side FACEIT integration is configured:

- connect FACEIT from a verified Steam identity;
- confirm nickname, ELO, skill level and region/country match the real FACEIT account;
- confirm refresh updates recent matches/stats;
- confirm the desktop never displays or logs the FACEIT developer API key;
- if Downloads API access is not configured, the UI must state that automatic demo download is unavailable instead of pretending it works.

## What makes a good bug report

Use the repository's Bug Report template and include exact reproduction steps. Screenshots/video are particularly useful for window-placement and lifecycle issues.

For crashes or parsing errors, sanitized logs are useful. Remove secrets before attaching anything publicly.

## What not to test

Do not attempt to make CounterLab interact with CS2 through DLL injection, process-memory reading/writing, automated gameplay input, anti-cheat bypasses, or other invasive game manipulation. Those are outside CounterLab's intended product boundary.
