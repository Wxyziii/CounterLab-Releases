## Summary

Describe the documentation/release-repository change.

## Scope

- [ ] Documentation only
- [ ] Issue/support configuration
- [ ] Authorized release metadata
- [ ] Other public release-repository maintenance

## Safety checks

- [ ] No CounterLab private source code is included.
- [ ] No binaries were committed to the Git tree; release binaries belong in GitHub Releases.
- [ ] No passwords, Steam credentials, CS2 Game Authentication Codes, API keys, access tokens, Supabase secrets, session cookies, or updater private keys are included.
- [ ] This change does not disclose an unpatched exploitable security vulnerability.

## Updater metadata changes

If this PR changes a live updater manifest:

- [ ] I am an authorized CounterLab release maintainer.
- [ ] Referenced release assets already exist.
- [ ] Version, target, URL, publication date, and updater signature were verified.
- [ ] The signature field contains the actual generated signature contents.
- [ ] Update discovery/install was tested from a supported older CounterLab build.
