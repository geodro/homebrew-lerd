# homebrew-lerd

> Open-source Herd-like local PHP development environment, packaged as the
> [`lerd-env/lerd`](https://github.com/lerd-env/homebrew-lerd) Homebrew tap
> for macOS and Linux.

[![Release](https://img.shields.io/github/v/release/lerd-env/lerd)](https://github.com/lerd-env/lerd/releases)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://github.com/lerd-env/lerd/blob/main/LICENSE)
[![Docs](https://img.shields.io/badge/docs-lerd.sh-blue)](https://lerd.sh)
[![Reddit](https://img.shields.io/badge/Reddit-r%2Flerd-ff2d20?logo=reddit)](https://reddit.com/r/lerd)
[![Discord](https://img.shields.io/badge/Discord-Join-5865F2?logo=discord&logoColor=white)](https://discord.gg/5JK54s7xCC)

![Lerd dashboard tour](https://raw.githubusercontent.com/lerd-env/lerd/main/docs/assets/screenshots/tour.gif)

[Lerd](https://lerd.sh) runs Nginx, PHP-FPM, and your services as rootless
[Podman](https://podman.io) containers: automatic `.test` domains with HTTPS,
per-project PHP versions, one-click databases and services, a built-in web UI,
TUI, CLI and MCP server. No Docker, no sudo, no system pollution. This repo
makes it a first-class Homebrew citizen: `brew install` brings up the whole
stack on its own, and every update after that arrives with your normal
`brew upgrade`.

## Install

```bash
brew install lerd-env/lerd/lerd
lerd install
```

Recent Homebrew versions block third-party taps until you trust them; if brew
asks, run `brew trust lerd-env/lerd` first.

On macOS the formula pulls in Podman from Homebrew automatically. On Linux,
lerd integrates with the distro's Podman, so the formula deliberately does not
depend on Homebrew's; `lerd install` tells you what to install if it is missing.

Updates arrive through brew like any other formula:

```bash
brew upgrade lerd
```

To uninstall cleanly, tear the stack down before removing the binary:

```bash
lerd uninstall
brew uninstall lerd
```

## How it works

The `lerd.rb` formula here is not written by hand. [GoReleaser](https://goreleaser.com)
generates it as part of every [upstream release](https://github.com/lerd-env/lerd/releases)
and pushes it to this repo: the formula points at the prebuilt per-OS,
per-architecture tarballs already published on the release, pinned by sha256,
and installs the `lerd` binary (plus `lerd-tray` where the tarball ships it).

Unlike [lerd-deb](https://github.com/lerd-env/lerd-deb) and
[lerd-rpm](https://github.com/lerd-env/lerd-rpm), which poll upstream daily,
this tap needs no workflow of its own: the main repo's release pipeline pushes
the updated formula the moment a release goes out, so the tap is never behind.
Manual edits to `lerd.rb` are overwritten by the next release; formula changes
belong in the `brews` section of the main repo's `.goreleaser.yaml`.
