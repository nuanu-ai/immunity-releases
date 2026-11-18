# Security policy

Immunity is a security tool, and this repository is where its builds and updates come from. A flaw here can put a changed program on a Mac. Please report one privately.

## Reporting a vulnerability

Use GitHub's private vulnerability reporting: open the repository's Security tab and choose "Report a vulnerability". Only the maintainers see the report. Please do not open a public issue for it.

Say what you found, which file of which release you tested, and how to reproduce it on a Mac. Use invented data in your example and leave out anything real from your own machine: paths, host names, addresses, command lines.

Reports are taken against the latest release.

## What counts

- A file in a release fails the checks in the README: its sum differs from the release notes, its signature is missing or wrong, or Apple did not notarize it.
- The app installs an update whose archive has no valid signature by the update key.
- The feed or an archive can be replaced by someone who is not a maintainer.
- The installer or an update leaves something that runs as root in a place another account can write.

A flaw in the detection core itself belongs in its own repository: https://github.com/nuanu-ai/immune/security.
