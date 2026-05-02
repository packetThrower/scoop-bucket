# scoop-bucket

[Scoop](https://scoop.sh/) bucket for [packetThrower](https://github.com/packetThrower)
projects.

## Apps

| App | Description |
|---|---|
| [`portfinder`](bucket/portfinder.json) | Network switch port discovery via CDP / LLDP / MNDP. [Source](https://github.com/packetThrower/PortFinder). |

## Install

Add the bucket once:

```powershell
scoop bucket add packetThrower https://github.com/packetThrower/scoop-bucket
```

Then install any app from it:

```powershell
scoop install portfinder
```

This puts `PortFinder.exe` on your `PATH` so the headless CLI works
from any shell:

```powershell
portfinder capture --interface "Ethernet" --protocol LLDP
portfinder list --with-ip
portfinder --help
```

A Start menu shortcut is also created.

## Update

```powershell
scoop update
scoop update portfinder
```

## Uninstall

```powershell
scoop uninstall portfinder
```

## Reporting issues

Bucket bugs (install fails, wrong hash, broken autoupdate): file in
this repo. App bugs: file at
[packetThrower/PortFinder](https://github.com/packetThrower/PortFinder/issues).

## Auto-update

The bucket runs a GitHub Actions workflow every 6 hours that compares
each manifest's `version` against the latest GitHub release, downloads
the matching artifact, and pushes a commit with the new SHA256 when
they differ. Same pattern as
[packetThrower/homebrew-portfinder](https://github.com/packetThrower/homebrew-portfinder).
