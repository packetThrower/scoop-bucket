# scoop-bucket

[Scoop](https://scoop.sh/) bucket for [packetThrower](https://github.com/packetThrower)
projects.

## Apps

| Manifest | Channel | Description |
|---|---|---|
| [`portfinder`](bucket/portfinder.json) | stable | Network switch port discovery via CDP / LLDP / MNDP. [Source](https://github.com/packetThrower/PortFinder). |
| [`portfinder-prerelease`](bucket/portfinder-prerelease.json) | pre-release | Same app, alpha / beta / rc channel. Coexists with stable. |
| [`baudrun`](bucket/baudrun.json) | stable | Cross-platform serial terminal for network devices. [Source](https://github.com/packetThrower/Baudrun). |
| [`baudrun-prerelease`](bucket/baudrun-prerelease.json) | pre-release | Same app, alpha / beta / rc channel. Coexists with stable. |

Stable and pre-release for either project coexist — install one,
both, or neither. State is shared between channels (preferences,
saved window position) because each project's stable + pre-release
ship under the same internal app identifier.

## Install

Scoop needs git to fetch and update third-party buckets. If your
fresh Scoop install doesn't have it yet, run this first:

```powershell
scoop install git
```

(Scoop fails fast with `ERROR Git is required for buckets.` if you
skip this — same fix.)

Add the bucket once:

```powershell
scoop bucket add packetThrower https://github.com/packetThrower/scoop-bucket
```

### PortFinder

```powershell
scoop install portfinder
# or pre-release channel:
scoop install portfinder-prerelease
```

Puts `portfinder` on your `PATH` and creates a `PortFinder` Start
menu shortcut. Same binary runs as the GUI when launched without
args and as the CLI when given a subcommand:

```powershell
portfinder capture --interface "Ethernet" --protocol LLDP
portfinder list --with-ip
portfinder --help
```

The pre-release CLI is exposed as `portfinder-alpha` and its Start
menu shortcut is `PortFinder Alpha`, so the two never collide.

Packet capture on Windows requires [Npcap](https://npcap.com/#download) —
tick "Allow non-administrators to capture" during install.

### Baudrun

```powershell
scoop install baudrun
# or pre-release channel:
scoop install baudrun-prerelease
```

Creates a `Baudrun` Start menu shortcut and adds `Baudrun` to your
`PATH` so you can launch it from a terminal. The pre-release shim
is `baudrun-alpha` with shortcut `Baudrun Alpha`.

USB-serial adapter compatibility varies by chipset. Some need a
vendor driver; others work out of the box via Baudrun's bundled
libusb backend. See the support matrix at
[docs/ADAPTERS.md](https://github.com/packetThrower/Baudrun/blob/main/docs/ADAPTERS.md).

## Update

```powershell
scoop update
scoop update portfinder
scoop update portfinder-prerelease    # if installed
scoop update baudrun
scoop update baudrun-prerelease       # if installed
```

## Uninstall

```powershell
scoop uninstall portfinder portfinder-prerelease
scoop uninstall baudrun baudrun-prerelease
```

## Reporting issues

Bucket bugs (install fails, wrong hash, broken autoupdate): file in
this repo. App bugs: file at the project's own repo
([PortFinder](https://github.com/packetThrower/PortFinder/issues),
[Baudrun](https://github.com/packetThrower/Baudrun/issues)).

## Auto-update

The bucket runs a GitHub Actions workflow every 6 hours that
iterates every manifest and runs Scoop's first-party
`checkver.ps1 -Update`. Stable manifests track the most recent
non-prerelease GitHub release; pre-release manifests match the
most recent tag with a SemVer pre-release suffix (`-alpha.N`,
`-beta.N`, `-rc.N`). New versions land as commits straight to
`main`. Same pattern as
[packetThrower/homebrew-tap](https://github.com/packetThrower/homebrew-tap).
