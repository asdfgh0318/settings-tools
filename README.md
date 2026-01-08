# Settings Tools for i3

A pair of terminal-based (TUI) tools for managing system settings and applications on i3 window manager. Uses `whiptail` for a clean interface similar to `nmtui`.

## Tools Overview

| Tool | Command | Purpose |
|------|---------|---------|
| **Settings** | `settings` | Quick launcher for installed apps only |
| **Settings Hub** | `settings-hub` | App store - browse, discover & install new apps |

## Files

```
settings-tools/
├── settings          # Quick launcher (installed apps only)
├── settings-hub      # App store (browse & install)
└── README.md         # This file
```

## Installation

```bash
# Create symlinks to ~/bin
ln -sf "$(pwd)/settings" ~/bin/settings
ln -sf "$(pwd)/settings-hub" ~/bin/settings-hub
```

## Settings (`settings`)

Fast launcher that **only shows installed applications**.

**Features:**
- Categories only appear if they contain installed apps
- Apps only appear if installed
- Instant launch on selection
- No install prompts - pure launcher

**Categories:** System, Display, Network, Audio, Power, Appearance, Files, Printing, Security, Development, Monitoring, Screenshot, Utilities, Office, Communication, Backup

## Settings Hub (`settings-hub`)

App store interface for **browsing and installing** new tools.

**Features:**
- Shows all available apps with `[X]` installed / `[ ]` not installed
- Click uninstalled app to install it
- "Install All Essential" option for quick setup
- Detects package manager (apt, dnf, pacman, zypper)

**Categories:** Same 16 categories as Settings, plus install functionality

## Technical Details

- **UI Framework:** `whiptail` (same as nmtui)
- **Shell:** Bash
- **Package Detection:** `command -v` checks
- **Launch Method:** `nohup` for background execution

## Suggested i3 Keybindings

Add to `~/.config/i3/config`:
```bash
bindsym $mod+s exec --no-startup-id alacritty -e settings
bindsym $mod+Shift+s exec --no-startup-id alacritty -e settings-hub
```

## Adding New Apps

To add a new app to both tools:

1. **In `settings`:** Add to the appropriate `menu_*` function:
```bash
command -v app-cmd &>/dev/null && items+=("app-cmd" "Description")
```

2. **In `settings-hub`:** Add to the appropriate `category_*` function:
```bash
"app-cmd" "$(chk app-cmd) Description" \
```
And handle package name mapping if different from command name.

## Dependencies

- `whiptail` (usually pre-installed)
- A terminal emulator for settings-hub installations
