# scoop-bucket

[Scoop](https://scoop.sh/) bucket for [packetThrower](https://github.com/packetThrower)
projects.

## Apps

| App | Channel | Description |
|---|---|---|
| [`portfinder`](bucket/portfinder.json) | stable | Network switch port discovery via CDP / LLDP / MNDP. [Source](https://github.com/packetThrower/PortFinder). |
| [`portfinder-prerelease`](bucket/portfinder-prerelease.json) | pre-release | Same app, alpha / beta / rc channel. Coexists with stable. |

## Install

Add the bucket once:

```powershell
scoop bucket add packetThrower https://github.com/packetThrower/scoop-bucket
```

### Stable

```powershell
scoop install portfinder
```

Puts `portfinder` on your `PATH` and creates a `PortFinder` Start
menu shortcut. Same binary runs as the GUI when launched without
args and as the CLI when given any subcommand:

```powershell
portfinder capture --interface "Ethernet" --protocol LLDP
portfinder list --with-ip
portfinder --help
```

### Pre-release

```powershell
scoop install portfinder-prerelease
```

Installs alongside stable (`scoop` puts each manifest in its own
per-app directory). The pre-release CLI is exposed as
`portfinder-alpha`, and its Start menu shortcut is `PortFinder
Alpha`, so the two never collide:

```powershell
portfinder-alpha capture --interface "Ethernet" --protocol LLDP
portfinder-alpha --version
```

State (preferences, saved window position) is shared between
channels because both ship with the same internal app identifier.
File regressions at
[packetThrower/PortFinder/issues](https://github.com/packetThrower/PortFinder/issues).

## Update

```powershell
scoop update
scoop update portfinder
scoop update portfinder-prerelease    # if installed
```

## Uninstall

```powershell
scoop uninstall portfinder
scoop uninstall portfinder-prerelease    # if installed
```

## Reporting issues

Bucket bugs (install fails, wrong hash, broken autoupdate): file in
this repo. App bugs: file at
[packetThrower/PortFinder](https://github.com/packetThrower/PortFinder/issues).

## Auto-update

The bucket runs a GitHub Actions workflow every 6 hours that
iterates every manifest and runs Scoop's first-party
`checkver.ps1 -Update`. The stable manifest tracks the most recent
non-prerelease GitHub release; the pre-release manifest matches the
most recent tag with a SemVer pre-release suffix (`-alpha.N`,
`-beta.N`, `-rc.N`). New versions land as commits straight to
`main`. Same pattern as
[packetThrower/homebrew-portfinder](https://github.com/packetThrower/homebrew-portfinder).
