<div align="center">

<img src="snap/gui/omnidiff.png" alt="OmniDiff logo" width="128" />

# OmniDiff

**Compare code, pictures, archives, fonts and PDFs in your terminal.**

[![omnidiff](https://snapcraft.io/omnidiff/badge.svg)](https://snapcraft.io/omnidiff)
[![Base: core26](https://img.shields.io/badge/Base-core26-2C8C3C?logo=canonical&logoColor=white)](https://snapcraft.io/core26)
![Confinement: strict](https://img.shields.io/badge/Confinement-strict-2C8C3C)
[![Maintainer: sidaliteir](https://img.shields.io/badge/Maintainer-sidaliteir-2C8C3C?logo=snapcraft&logoColor=white)](https://snapcraft.io/publisher/sidaliteir)
![Architectures: amd64, arm64](https://img.shields.io/badge/Architectures-amd64%20%7C%20arm64-2C8C3C?logo=linux&logoColor=white)

[Getting Started](#getting-started) · [Configure](#configure) · [Limitations](#limitations) · [Build](#build) · [Support](#support) · [License](#license)

Unofficial snap packaging for [OmniDiff](https://github.com/ivankovic/omnidiff), a content-aware diff tool with an interactive terminal viewer, text output and JSON output.

</div>

---

## Getting Started

<a href="https://snapcraft.io/omnidiff"><img alt="Get it from the Snap Store" src="https://snapcraft.io/en/dark/install.svg" width="180"></a>

```bash
sudo snap install omnidiff
omnidiff before.rs after.rs
```

Run `omnidiff` to choose files interactively, `omnidiff --headless before.rs after.rs` for text output, or `omnidiff --mode json before.rs after.rs` for JSON. Press `?` in the viewer for keyboard shortcuts.

## Configure

Use the viewer's settings. Configuration stays inside `~/snap/omnidiff/current`; there are no `snap set` options.

For files on removable storage:

```bash
sudo snap connect omnidiff:removable-media
```

For host Git integration, configure Git outside the snap and place its temporary files in an accessible directory:

```bash
mkdir -p "$HOME/snap/omnidiff/common/tmp"
git config --global difftool.omnidiff.cmd 'omnidiff "$LOCAL" "$REMOTE"'
TMPDIR="$HOME/snap/omnidiff/common/tmp" git difftool --tool=omnidiff
```

## Limitations

- Files outside accessible home and connected removable-storage locations, including top-level hidden home directories, remain confined. The snap has its own `/tmp`; host tools must use an accessible temporary directory when passing files.
- Git is included for local repository review. Host Git/Jujutsu configuration, host editors and Jujutsu executables are unavailable. Configure integrations from the host; the in-app editor action needs an executable inside the snap.
- Terminal image rendering depends on your terminal. Use `OMNIDIFF_GRAPHICS=halfblocks omnidiff` if its graphics protocol is unavailable.
- Updates come through `snap refresh omnidiff`.

## Build

```bash
git clone https://github.com/sidalit/omnidiff-snap.git
cd omnidiff-snap
sudo snap install snapcraft --classic
snapcraft pack
```

```bash
sudo snap install --dangerous ./omnidiff_*.snap
omnidiff
```

## Support

- **Installation or snap issues:** [open a packaging issue](https://github.com/sidalit/omnidiff-snap/issues).
- **Application bugs:** [report them upstream](https://github.com/ivankovic/omnidiff/issues).

## License

Snap packaging: [MIT](LICENSE).
