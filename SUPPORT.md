# CounterLab Support

This repository is the public support and release channel for CounterLab Alpha builds.

## Before reporting a bug

1. Confirm you are running the newest published CounterLab release.
2. Restart CounterLab and CS2 once if the problem may be session-specific.
3. Check existing GitHub issues for the same problem.
4. Reproduce the issue if possible and note the exact steps.
5. Collect only the logs needed for the report and remove secrets before posting them.

## What to include in a bug report

A useful report should contain:

- CounterLab version;
- Windows version;
- whether CounterLab was started normally or through Windows autostart;
- CS2 match type or platform involved, for example Premier, Competitive, FACEIT, Workshop, or training;
- exact reproduction steps;
- expected behavior;
- actual behavior;
- whether the problem reproduces consistently;
- relevant sanitized logs, screenshots, or video;
- whether restarting CounterLab changes the result.

For Live View problems, also include:

- number of monitors;
- which display was selected for CounterLab Live;
- whether CS2 was fullscreen, borderless, or windowed;
- whether the Live window opened, opened on the wrong display, froze, or closed unexpectedly;
- whether the main CounterLab window returned after the match.

For demo or match-analysis problems, also include:

- map and approximate match time;
- Valve matchmaking or FACEIT;
- whether the match was discovered automatically;
- whether demo download began;
- whether download, decompression, parsing, caching, or analysis failed;
- the error shown by CounterLab, if any.

## Never post secrets

Remove or redact:

- Steam Web API keys;
- CS2 Game Authentication Codes;
- access or refresh tokens;
- passwords;
- session cookies;
- Supabase secrets or service-role keys;
- updater private keys;
- private repository tokens;
- unrelated personal information.

A match sharing code may also reveal information about a match. Only include one when it is genuinely needed for reproduction and you are comfortable sharing it publicly.

## Feature requests

Use the Feature Request issue template. Explain the problem or workflow first, then describe the proposed behavior. Screenshots or mockups are welcome when they clarify the idea.

## Security issues

Do not report exploitable security vulnerabilities publicly. Follow [SECURITY.md](SECURITY.md).

## Contact

For matters that should not be handled in a public issue:

**marcelbialk008@gmail.com**
