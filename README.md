# GameCI Scoop Bucket

[Scoop](https://scoop.sh) bucket for [GameCI](https://game.ci).

## Install

```powershell
scoop bucket add game-ci https://github.com/game-ci/scoop-bucket
scoop install game-ci
```

Upgrade later with:

```powershell
scoop update game-ci
```

## What this installs

The `game-ci` CLI — build and test commands for Unity, Godot, Unreal and Bevy
projects, locally and in CI. See the
[documentation](https://game.ci/docs/cli) for usage.

Scoop puts `game-ci` on your `PATH` and handles upgrades and uninstall for you.
If you would rather not use Scoop, the install script works anywhere:

```powershell
irm https://raw.githubusercontent.com/game-ci/cli/main/install.ps1 | iex
```

## A note on packaging

The `game-ci` binary is not self-contained: it resolves static assets
(`default-build-script/`, `platforms/*`, `unity-config/`) from a `dist/`
directory that must sit alongside it on disk, because those paths are mounted
into Docker containers during a build (see
[game-ci/cli#73](https://github.com/game-ci/cli/issues/73)).

Scoop extracts the whole release archive into the app directory and shims the
executable in place, which keeps the binary and `dist/` together. Packaging that
assumes "one archive, one binary" will produce an install that passes
`game-ci --help` and then fails on any real build.

## Updating the manifest

Manifest updates are automated from the
[game-ci/cli](https://github.com/game-ci/cli) release workflow, and the manifest
also carries `checkver`/`autoupdate` so `scoop bucket` tooling can refresh it. To
update by hand, bump `version`, `url` and `hash` to match the `checksums.txt`
published with the release.

## License

MIT
