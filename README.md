# Settings Tools for i3

Terminal-based (TUI) tools for managing system settings and applications on i3 window manager. Uses `whiptail` for a clean interface similar to `nmtui`.

## Screenshots

### Settings (Quick Launcher)
```
┌──────────────────────┤ Settings ├──────────────────────┐
│                                                        │
│ Select a category:                                     │
│                                                        │
│          1  System Settings                            │
│          2  Display & Graphics                         │
│          3  Network & Internet                         │
│          4  Audio & Video                              │
│          5  Power & Battery                            │
│          6  Appearance & Themes                        │
│          7  Files & Storage                            │
│          ...                                           │
│                                                        │
│            <Ok>                <Cancel>                │
└────────────────────────────────────────────────────────┘
```

### Settings Hub (App Store)
```
┌────────────────────┤ Settings Hub ├────────────────────┐
│                                                        │
│ Select a category:                                     │
│                                                        │
│          1   System Settings                           │
│          2   Display & Graphics                        │
│          3   Network & Internet                        │
│          ...                                           │
│          17  Install All Essential                     │
│                                                        │
│            <Ok>                <Cancel>                │
└────────────────────────────────────────────────────────┘
```

### Category View (with install status)
```
┌────────────────────┤ Audio & Video ├───────────────────┐
│                                                        │
│ [X] = Installed  [ ] = Not installed                   │
│                                                        │
│   pavucontrol       [X] PulseAudio volume control      │
│   qpwgraph          [ ] PipeWire patchbay              │
│   easyeffects       [ ] Audio effects (EQ, compressor) │
│   audacity          [X] Audio editor                   │
│   vlc               [X] Media player                   │
│   obs-studio        [ ] Screen recording & streaming   │
│                                                        │
│            <Ok>                <Cancel>                │
└────────────────────────────────────────────────────────┘
```

## Tools Overview

| Tool | Command | Purpose |
|------|---------|---------|
| **Settings** | `settings` | Quick launcher for installed apps only |
| **Settings Hub** | `settings-hub` | App store - browse, discover & install new apps |

## Installation

```bash
# Clone the repository
git clone https://github.com/asdfgh0318/settings-tools.git
cd settings-tools

# Create symlinks to ~/bin
mkdir -p ~/bin
ln -sf "$(pwd)/settings" ~/bin/settings
ln -sf "$(pwd)/settings-hub" ~/bin/settings-hub

# Make sure ~/bin is in your PATH
echo 'export PATH="$HOME/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

## Usage

```bash
settings       # Quick launcher - only shows installed apps
settings-hub   # App store - browse and install new apps
```

## Settings (`settings`)

Fast launcher that **only shows installed applications**.

**Features:**
- Categories only appear if they contain installed apps
- Apps only appear if installed
- Instant launch on selection
- No install prompts - pure launcher

## Settings Hub (`settings-hub`)

App store interface for **browsing and installing** new tools.

**Features:**
- Shows all available apps with `[X]` installed / `[ ]` not installed
- Click uninstalled app to install it
- "Install All Essential" option for quick setup
- Detects package manager (apt, dnf, pacman, zypper)

## Categories

Both tools organize apps into 16 categories:

| Category | Examples |
|----------|----------|
| System Settings | GNOME Settings, DConf Editor |
| Display & Graphics | ARandR, NVIDIA Settings, Redshift |
| Network & Internet | Network Manager, Bluetooth, Wireshark |
| Audio & Video | PulseAudio, VLC, OBS Studio, Audacity |
| Power & Battery | XFCE Power Manager, TLP |
| Appearance & Themes | LXAppearance, Qt5ct, Nitrogen |
| Files & Storage | Thunar, Nautilus, GParted, Disks |
| Printing & Scanning | Printers, Simple Scan |
| Security & Privacy | KeePassXC, Seahorse, Firewall |
| Development Tools | VS Code, Geany, Meld, DBeaver |
| System Monitoring | htop, btop, System Monitor |
| Screenshot & Recording | Flameshot, Peek, OBS |
| Utilities | Rofi, CopyQ, Picom, Dunst |
| Office & Documents | LibreOffice, Evince, Okular |
| Communication | Discord, Thunderbird, Telegram |
| Backup & Sync | Timeshift, Syncthing, Deja Dup |

## i3 Keybindings

Add to `~/.config/i3/config`:
```bash
# Quick settings launcher
bindsym $mod+s exec --no-startup-id alacritty -e settings

# App store / installer
bindsym $mod+Shift+s exec --no-startup-id alacritty -e settings-hub
```

Then reload i3: `$mod+Shift+r`

## Adding New Apps

**In `settings`:** Add to the appropriate `menu_*` function:
```bash
command -v app-cmd &>/dev/null && items+=("app-cmd" "Description")
```

**In `settings-hub`:** Add to the appropriate `category_*` function:
```bash
"app-cmd" "$(chk app-cmd) Description" \
```

## Dependencies

- `whiptail` (usually pre-installed on most Linux distros)
- `bash`
- A terminal emulator (alacritty, kitty, gnome-terminal, etc.)

## License

MIT
