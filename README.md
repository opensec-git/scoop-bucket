# OpenSec Scoop bucket

[![Tests](https://github.com/opensec-git/scoop-bucket/actions/workflows/ci.yml/badge.svg)](https://github.com/opensec-git/scoop-bucket/actions/workflows/ci.yml) [![Install](https://github.com/opensec-git/scoop-bucket/actions/workflows/install.yml/badge.svg)](https://github.com/opensec-git/scoop-bucket/actions/workflows/install.yml) [![Excavator](https://github.com/opensec-git/scoop-bucket/actions/workflows/excavator.yml/badge.svg)](https://github.com/opensec-git/scoop-bucket/actions/workflows/excavator.yml)

[Scoop](https://scoop.sh) manifests for [Pi-Bolt](https://github.com/opensec-git/Pi-Bolt), the Pi coding agent compiled ahead
of time to native code.

## Install

```pwsh
scoop bucket add opensec-git https://github.com/opensec-git/scoop-bucket
scoop install opensec-git/pi-bolt
```

This installs the latest Pi-Bolt release for Windows x64 (`pi-bolt-win32-x64.zip`) and puts `pi-bolt` on PATH.

## Upgrade

```pwsh
scoop update pi-bolt
```

`pi-bolt update` does not replace a Scoop installation: it tells you to run `scoop update pi-bolt`.

## Uninstall

```pwsh
scoop uninstall pi-bolt
scoop bucket rm opensec-git
```

Your sessions and settings in `~\.pi` stay.

## Other ways to install

The Windows installer (`irm https://pi-bolt.opensec.in/install.ps1 | iex`) and the npm package are described in
[Pi-Bolt's installation guide](https://pi-bolt.opensec.in/docs/installation.html). The installer also offers the JIT build,
which this manifest does not.

## How the manifest is updated

The Excavator workflow runs every four hours. It reads the latest `bolt-vX.Y.Z` release of Pi-Bolt, takes the archive's SHA-256
from the release's `SHA256SUMS`, and commits the new version to `bucket/pi-bolt.json`. The Install workflow installs the manifest
with Scoop on a Windows runner and runs `pi-bolt --version`, on every push and pull request and once a day.
