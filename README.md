# 🖥️ My Setup

Personal reference for my CachyOS configuration and tools.

---

## OS

**[CachyOS](https://cachyos.org/)**
- Arch-based distro optimized for performance
- Uses the BORE/EEVDF scheduler by default for improved responsiveness
- Comes with a custom optimized kernel (`linux-cachyos`)

### Useful Commands

```bash
# Update system
sudo pacman -Syu

# Install a package
sudo pacman -S <package>

# Search for a package
pacman -Ss <keyword>

# Remove a package and its unused dependencies
sudo pacman -Rns <package>

# Clean package cache
sudo paccache -r
```

---

## Desktop Environment — KDE Plasma

| Setting | Value |
|---------|-------|
| Theme | CachyOS Nord |
| Icons | Papirus |
| Mouse cursor | Pop |

### Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Alt + F` | Toggle fullscreen |
| `Alt + T` | Open terminal (Konsole) |
| `Alt + B` | Open browser (Brave) |
| `Alt + Q` | Close/quit window |

Set via: **System Settings → Shortcuts → Custom Shortcuts**

### Window Management — KWinScripts + Mouse Tiler

**[Mouse Tiler](https://github.com/Qelxiros/mouse-tiler)** — KWinScript that enables mouse-driven tiling window management in KDE.

**Install via KDE Store:**

System Settings → Window Management → KWin Scripts → Get New Scripts → search **Mouse Tiler**

**Or install manually:**

```bash
# Clone and install
git clone https://github.com/Qelxiros/mouse-tiler
cd mouse-tiler
kpackagetool6 --type KWin/Script --install .
```

Then enable it under **System Settings → Window Management → KWin Scripts**.

---

## Terminal — Konsole

| Setting | Value |
|---------|-------|
| Theme | Breeze |
| Font | MesloLGL Nerd Font, 14pt |

MesloLGL Nerd Font enables icon glyphs used by tools like `eza`, `btop`, and `neofetch`.

---

## Fonts

### Cascadia Mono Nerd Font
Installed for use across the UI.

```bash
sudo pacman -Syu ttf-cascadia-mono-nerd
```

---

## Shell — Bash

Config location: `~/.bashrc`

```bash
# ~/.bashrc

neofetch

alias cat='bat'
alias ll='eza -la --icons'
```

---

## Browser

**[Brave](https://brave.com/) (Origin / Nightly)**
- Chromium-based with built-in ad/tracker blocking
- Origin = the early-access/dev channel build

### Tips

- Shields settings: `brave://settings/shields`
- Flags: `brave://flags`
- Force-enable hardware acceleration: `brave://settings/system`
- Profile path: `~/.config/BraveSoftware/Brave-Browser/`

---

## Notes / Knowledge Base — Obsidian

| Setting | Value |
|---------|-------|
| Interface font | ABeeZee |
| Text font | ABeeZee |
| Monospace font | ABeeZee |

Config location: `~/.config/obsidian/` or inside the vault under `.obsidian/appearance.json`

---

## CLI Tools

### btop
**[btop](https://github.com/aristocratos/btop)** — Resource monitor for CPU, memory, disks, network, and processes.

```bash
sudo pacman -S btop
```

| Key | Action |
|-----|--------|
| `q` | Quit |
| `F2` / `o` | Options |
| `F6` / `s` | Sort processes |
| `m` | Cycle memory display |
| `k` | Kill selected process |
| `e` | Toggle expanded CPU view |
| `/` | Filter processes |

Config: `~/.config/btop/btop.conf`

**Theme: Catppuccin Mocha**

```bash
# Download the theme
curl -o ~/.config/btop/themes/catppuccin_mocha.theme \
  https://raw.githubusercontent.com/catppuccin/btop/main/themes/catppuccin_mocha.theme
```

Then in btop press `F2` → **Color theme** → select `catppuccin_mocha`.

---

### nvtop
**[nvtop](https://github.com/Syllo/nvtop)** — GPU process monitor (supports NVIDIA, AMD, Intel).

```bash
sudo pacman -S nvtop
```

| Key | Action |
|-----|--------|
| `q` | Quit |
| `F2` | Setup / options |
| `F9` | Kill a process |
| `↑` / `↓` | Navigate processes |

---

### tldr
**[tldr](https://tldr.sh/)** — Simplified, community-driven man pages.

```bash
sudo pacman -S tldr

# Update local cache
tldr --update

# Usage
tldr <command>
# e.g.
tldr tar
tldr eza
```

---

### eza
**[eza](https://github.com/eza-community/eza)** — Modern replacement for `ls`, with icons and Git integration.

```bash
sudo pacman -S eza
```

Aliased in `.bashrc`:
```bash
alias ll='eza -la --icons'
```

Useful flags:

| Flag | Description |
|------|-------------|
| `-l` | Long format |
| `-a` | Show hidden files |
| `--icons` | File type icons (requires Nerd Font) |
| `--git` | Show Git status |
| `-T` | Tree view |
| `--sort=size` | Sort by file size |

---

### neofetch
**[neofetch](https://github.com/dylanaraps/neofetch)** — System info display. Runs on every shell start via `.bashrc`.

```bash
sudo pacman -S neofetch
```

Config: `~/.config/neofetch/config.conf`

---

### bat
**[bat](https://github.com/sharkdp/bat)** — `cat` replacement with syntax highlighting and line numbers.

```bash
sudo pacman -S bat
```

Aliased in `.bashrc`:
```bash
alias cat='bat'
```

Config: `~/.config/bat/config`

---

## Sudo Without Password (NOPASSWD)

To allow your user to run `sudo` without being prompted for a password:

1. Install nano if not already available:

```bash
sudo pacman -S nano
```

2. Open the sudoers file safely with visudo:

```bash
sudo EDITOR=nano visudo
```

3. Scroll to the bottom and add (username is `jayp`):

```
jayp ALL=(ALL) NOPASSWD: ALL
```

4. Save and exit nano: `Ctrl+O` → `Enter` → `Ctrl+X`

5. Test in a new terminal:

```bash
sudo whoami
# Should print: root (no password prompt)
```

> ⚠️ Always use `visudo` instead of editing `/etc/sudoers` directly — it validates syntax before saving so you can't accidentally lock yourself out.
> If you ever switch to `doas`, the config file is `/etc/doas.conf` instead.

---

## Notes

- This file is a living document — update as the setup evolves.
