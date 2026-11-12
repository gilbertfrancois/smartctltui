## smartctltui

A Vim-navigable terminal TUI for `smartctl` (smartmontools), with the functionality of GSmartControl — fully in a terminal. Pure Python standard library + `curses`.

### Features

- Drive list with model, serial, size and SMART health; add USB/RAID devices by hand (`/dev/sdb -d sat`)
- Tabs: **General**, **Attributes**, **Statistics**, **Self-Tests**, **Error Log**, **Temperature** (with history chart), **Advanced**, **Raw** (`smartctl -x`)
- Start short / extended / conveyance self-tests, offline data collection, abort a test, enable/disable SMART; progress is polled automatically
- Save the current tab (text), the full report (text) or the full report (JSON) to disk
- Works for ATA/SATA, NVMe and (basically) SCSI drives

### Controls

| Key                     | Action                              |
| :---------------------- | :---------------------------------- |
| `j` / `k`, `gg` / `G`   | Move / scroll, top / bottom         |
| `Enter`                 | Open selected drive                 |
| `h` / `l`, `Tab`, `1-8` | Switch tab                          |
| `Ctrl-d` / `Ctrl-u`     | Page down / up                      |
| `t`                     | Self-tests and SMART actions        |
| `s`                     | Save report to disk                 |
| `r`                     | Refresh (rescan in the drive list)  |
| `o`                     | Open a device manually (drive list) |
| `?`, `q`                | Help, back / quit                   |

### Installation

Copy `smartctltui` to e.g. `/usr/local/bin` or `$HOME/.local/bin`. Requires Python >= 3.11 and smartmontools:

```bash
sudo dnf install smartmontools      # Fedora
sudo apt install smartmontools      # Ubuntu
```

smartctl needs root to open drives, so `smartctltui` re-runs itself under `sudo` when started as a normal user (disable with `--no-sudo`). Saved reports default to your home directory (override with `--output-dir`) and are owned by you, not root.
