# Recommended GitHub Repository Settings

The Git tree is prepared for CounterLab public releases. The following repository-level settings should also be applied in GitHub when available.

## About section

Recommended description:

> Official CounterLab Windows releases, updater metadata, changelog, Alpha testing and support.

Recommended topics:

- `counterlab`
- `counter-strike-2`
- `cs2`
- `tauri`
- `windows`
- `releases`
- `game-analytics`

Do not set the private CounterLab source repository as a public homepage unless that repository is intentionally made public in the future.

## Features

Recommended:

- **Issues:** enabled
- **Projects:** disable unless they will be used publicly for CounterLab planning
- **Wiki:** disable unless a public wiki is intentionally maintained
- **Discussions:** optional; leave disabled for early Alpha if Issues are sufficient

## Main branch protection

Because `main` can contain live updater-channel metadata, protect it where practical.

Recommended controls:

- prevent branch deletion;
- prevent force pushes;
- require review for changes from collaborators when the team grows;
- use CODEOWNERS for updater/security-sensitive paths;
- keep an owner/admin recovery path so an urgent bad updater manifest can be replaced quickly.

A solo Alpha project may allow the owner to bypass review requirements while still preventing accidental force-push/deletion.

## Security

Enable available GitHub security features for the public repository, especially:

- secret scanning / push protection where available;
- dependency/security alerts if workflows or dependencies are later added;
- private vulnerability reporting if desired in addition to the email process documented in `SECURITY.md`.

Never use repository variables or non-secret configuration fields for updater private keys or passwords. If release automation is added, private signing material belongs only in encrypted secrets accessible to the trusted release workflow.

## Releases

- Publish CounterLab Alpha versions as GitHub prereleases.
- Attach binaries to Releases; do not commit installers/updater archives to the normal Git tree.
- Keep release tags immutable after publication whenever possible.
- If a release must be withdrawn, stop the updater channel from referencing it and clearly mark/remove affected assets as appropriate.

## Actions permissions

If GitHub Actions is later used in this public release repository:

- grant only the minimum permissions needed by each workflow;
- prefer explicit `permissions:` blocks in workflow YAML;
- pin important third-party actions to trusted versions/commits;
- never expose private-repository source or secrets to untrusted pull-request workflows;
- separate build/signing privileges from ordinary documentation checks.
