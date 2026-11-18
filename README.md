# Immunity releases

Signed builds of Immunity, the Mac app of [Artificial Immunity](https://artificialimmunity.ai), and the feed the app updates from. This repository holds builds only. There is no source code here.

Immunity watches one Mac for signs of attack and shows what it found and what it could not see. Its detection core is open source: [nuanu-ai/immune](https://github.com/nuanu-ai/immune). The app around the core is developed outside this repository.

## Install

You need a Mac with Apple Silicon and macOS 15 or later.

1. Open the [latest release](https://github.com/nuanu-ai/immunity-releases/releases/latest) and download `Immunity-<version>.pkg`.
2. Check the download as described below.
3. Open the package and follow the installer.

## Updates

After the first install the app updates itself with [Sparkle](https://sparkle-project.org). You do not need to download a new package.

The app reads the feed `appcast.xml` from the release tagged [`updates`](https://github.com/nuanu-ai/immunity-releases/releases/tag/updates) and downloads the archive the feed names from the same release. It installs an archive only when the archive carries a valid EdDSA signature made with the update key. The public half of that key is built into the app:

```
roAf6Hipz4MEHZ8aXbwKh6ijcv76N5bEfsbeXnjUyU4=
```

"Check for Updates…" in the app's menu checks at once. "Check for Updates Automatically" in the same menu turns the scheduled check on and off.

## Check a download

Every package is signed with an Apple Developer ID and notarized by Apple. The notes of each release list the SHA-256 of its files.

```sh
shasum -a 256 Immunity-<version>.pkg
pkgutil --check-signature Immunity-<version>.pkg
spctl --assess --type install -vv Immunity-<version>.pkg
```

- `shasum` prints the sum given in the release notes.
- `pkgutil` reports a package signed by a Developer ID Installer certificate with a chain to Apple.
- `spctl` answers `accepted` with `source=Notarized Developer ID`.

If any of the three differs, do not install the package, and report it as [SECURITY.md](SECURITY.md) says.

## What a release holds

| File | Where | What it is for |
|---|---|---|
| `Immunity-<version>.pkg` | the release of that version, such as `v0.2.0` | The installer for a first install. |
| `Immunity-<version>-<build>.zip` | the release `updates` | The same app as an archive, for Sparkle. |
| `appcast.xml` | the release `updates` | The feed: the builds on offer, with the signature of each archive. |

## Problems and questions

- The installer or an update does not work: open an [issue](https://github.com/nuanu-ai/immunity-releases/issues) here. Leave out anything real from your Mac, such as paths, host names and command lines.
- A security problem in a build or in the update path: report it privately, as [SECURITY.md](SECURITY.md) says.
- What Immune detects and how: the core's repository, [nuanu-ai/immune](https://github.com/nuanu-ai/immune).
