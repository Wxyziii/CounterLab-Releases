# CounterLab Alpha Testing Guide

Thank you for testing CounterLab. Alpha testing is intended to find real-world failures in installation, CS2 detection, Live View, match discovery, demo handling, analysis, updates, and recovery behavior.

## Before testing

- Install only an official build from this repository's Releases page.
- Keep CS2 and Steam updated.
- Do not share Steam API keys, CS2 Game Authentication Codes, access tokens, passwords, or other secrets in public bug reports.
- Expect Alpha builds to change frequently.

## Recommended first-run test

1. Install CounterLab.
2. Open the application normally.
3. Complete the required account/platform setup shown by CounterLab.
4. Open Settings and select the display to use for CounterLab Live.
5. Optionally enable **Start CounterLab with Windows**.
6. Restart CounterLab once and verify saved settings persist.
7. If autostart is enabled, restart Windows at a convenient time and verify CounterLab starts in the intended background state rather than forcing the main dashboard open.

## Match lifecycle test

### Before the match

1. Open or leave CounterLab running in the background.
2. Launch CS2.
3. Stay in the CS2 menus for a short period.
4. Confirm CounterLab Live does **not** open merely because CS2 is running.

### When the match starts

For a supported match:

1. Confirm the main CounterLab window hides automatically.
2. Confirm CounterLab Live opens automatically.
3. Confirm it opens on the configured display.
4. Confirm it identifies the correct map/match state.
5. Confirm displayed live stats change as the match progresses.
6. Confirm the UI remains responsive through round transitions, death/spectating states, halftime/side changes, overtime when applicable, and reconnects when applicable.

### When the match ends

1. Finish the match normally.
2. Confirm CounterLab Live closes or transitions out of the live state automatically.
3. Confirm the main CounterLab window returns automatically.
4. Confirm CounterLab opens the overview for the match that just ended rather than an unrelated previous match.
5. Confirm the initial live-collected summary is visible when available.
6. Confirm automatic demo acquisition begins when the platform/match supports it.
7. Confirm the same match record updates as download/parsing progresses rather than creating duplicates.
8. Confirm post-match analysis becomes available after parsing.

## Recovery tests

Please test these separately when convenient:

- close CounterLab Live during an active match;
- close CS2 unexpectedly;
- disconnect/reconnect to a match;
- lose network connectivity temporarily;
- start CounterLab after CS2 is already running;
- start CounterLab after a supported match has already begun;
- change the selected monitor between sessions;
- run CounterLab after a Windows restart with autostart enabled;
- manually open CounterLab while its background instance is already running.

Expected behavior: CounterLab should recover without leaving an invisible stuck process, duplicate backend listeners, duplicate matches, or a permanently hidden main window.

## Update test

When a newer Alpha is published:

1. Open CounterLab outside an active match.
2. Use the built-in update check or wait for the app to report the update.
3. Confirm the offered version is newer than the installed version.
4. Confirm you can defer the update.
5. Choose **Update now**.
6. Confirm download and installation complete without manually downloading the installer.
7. Reopen/return to CounterLab and confirm the displayed version changed.
8. Confirm settings and expected local data persisted.

If an update becomes available during an active match, CounterLab should avoid interrupting the Live View with a normal update prompt.

## Demo and analysis test

For each supported platform you use:

- verify the match is discovered automatically;
- verify map, score, teams/players, date/time, and mode are identified correctly when available;
- verify the demo starts downloading without manual import when automatic acquisition is supported;
- verify failed or expired downloads produce a useful error state;
- verify parser progress/error states are understandable;
- verify reopening CounterLab does not create a duplicate match;
- verify cached/reopened analysis belongs to the correct match.

## What makes a good bug report

Use the repository's Bug Report template and include exact reproduction steps. Screenshots/video are particularly useful for window-placement and lifecycle issues.

For crashes or parsing errors, sanitized logs are useful. Remove secrets before attaching anything publicly.

## What not to test

Do not attempt to make CounterLab interact with CS2 through DLL injection, process-memory reading/writing, automated gameplay input, anti-cheat bypasses, or other invasive game manipulation. Those are outside CounterLab's intended product boundary.
