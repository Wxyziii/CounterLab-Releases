# Contributing to CounterLab Releases

CounterLab itself is proprietary software. This public repository is **not** the CounterLab source repository and is not intended for source-code contributions to the application.

## What is welcome here

You can help by:

- reporting reproducible CounterLab Alpha bugs;
- suggesting product improvements;
- improving public release/support documentation;
- reporting broken release links or updater metadata;
- privately reporting security vulnerabilities according to `SECURITY.md`.

## What does not belong here

Do not submit:

- copied/decompiled CounterLab source or proprietary implementation details;
- binaries directly into the Git tree;
- private source-repository files;
- Steam credentials or CS2 Game Authentication Codes;
- Supabase credentials;
- GitHub access tokens;
- updater private keys;
- passwords, cookies, or unrelated personal data;
- anti-cheat bypasses, DLL injection, CS2 process-memory access, automated gameplay input, or other invasive game modifications.

Release binaries belong on GitHub Releases rather than in normal repository commits.

## Documentation pull requests

Small documentation fixes are welcome. Keep them focused and explain what is being corrected. A documentation pull request should not change live updater metadata unless it is part of an authorized CounterLab release.

## Updater metadata

Files under a live updater channel such as `updater/alpha/latest.json` are security-sensitive operational metadata. Do not submit changes to a live updater manifest unless you are the project owner/authorized release maintainer and the referenced signed release artifacts already exist.

## Bug reports and feature requests

Use the provided GitHub issue forms. Search existing issues first and avoid posting secrets.

## Security reports

Do not open a public issue or pull request for an exploitable security vulnerability. Follow `SECURITY.md`.
