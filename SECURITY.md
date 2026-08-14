# Security Policy

Security reports are welcome and should be handled privately when they could expose CounterLab users, credentials, update infrastructure, or local systems.

## Supported versions

During Alpha, only the newest published CounterLab release is expected to receive security fixes. Testers should update to the latest available build before reporting an issue that may already have been fixed.

## Report a vulnerability privately

**Do not open a public GitHub issue for a security vulnerability.**

Email: **marcelbialk008@gmail.com**

Use a clear subject such as:

`CounterLab security report - short description`

Please include, where possible:

- affected CounterLab version;
- Windows version and architecture;
- a concise description of the vulnerability;
- reproduction steps;
- impact and realistic attack scenario;
- relevant sanitized logs or screenshots;
- whether the issue requires local access, user interaction, network access, or specific account permissions.

Do not send real passwords, Steam authentication codes, API keys, access tokens, session cookies, updater private keys, or unrelated personal information.

## High-priority security areas

Reports are especially useful for issues involving:

- updater signature verification or update-package substitution;
- arbitrary code execution;
- unsafe command execution or argument handling;
- path traversal or writes outside intended CounterLab locations;
- credential, token, or secret exposure;
- insecure local HTTP/GSI handling;
- privilege escalation;
- unsafe external URL or protocol handling;
- database corruption caused by untrusted input;
- unintended interaction with CS2 beyond CounterLab's documented external-companion boundary.

## Public disclosure

Please allow the issue to be investigated and fixed before publishing technical exploit details. A public advisory or changelog entry may be created after a fix is available when disclosure is appropriate.

## CounterLab security boundary

CounterLab's intended match companion and analysis workflows are external to the game. They should not require DLL injection, CS2 process-memory reading, automated gameplay input, or bypassing anti-cheat protections.

A behavior that crosses this boundary unexpectedly should be reported as a security-sensitive defect.
