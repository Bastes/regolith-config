# Regolith 3 config

Personal [Regolith](https://regolith-desktop.com) 3 configuration (X11 / i3 session).

## Install on a fresh system

### 1. Add the Regolith apt repository

From the [official install guide](https://regolith-desktop.com/docs/using-regolith/install/).
Adjust `noble` (Ubuntu codename) and `v3.4` (Regolith release) as needed.

```sh
wget -qO - https://archive.regolith-desktop.com/regolith.key | \
  gpg --dearmor | sudo tee /usr/share/keyrings/regolith-archive-keyring.gpg > /dev/null

echo deb "[arch=amd64 signed-by=/usr/share/keyrings/regolith-archive-keyring.gpg] \
https://archive.regolith-desktop.com/ubuntu/stable noble v3.4" | \
  sudo tee /etc/apt/sources.list.d/regolith.list

sudo apt update
```

### 2. Install Regolith and the dependencies of this config

```sh
sudo apt install regolith-desktop regolith-session-flashback \
  regolith-look-gruvbox jq ubuntu-wallpapers-noble
```

### 3. Clone this config

```sh
# Move any existing ~/.config/regolith3 aside first
git clone <this-repo-url> ~/.config/regolith3
```

Then reboot (so the login manager picks up the Regolith session), or if
Regolith was already running, apply with `regolith-look refresh`.

## Contents

| Path                                | Purpose                                                       |
|-------------------------------------|---------------------------------------------------------------|
| `Xresources`                        | Look (gruvbox), wallpaper/lockscreen image, gaps              |
| `i3/config.d/90_rotate-windows`     | `<Super>]` / `<Super>[` rotate tiled windows on the workspace |
| `i3/config.d/91_move-window-output` | `<Super>\` move window to next monitor and follow it          |
| `scripts/rotate-windows`            | Helper for the rotate bindings (needs `jq`)                   |

Files in `i3/config.d/` are merged with Regolith's defaults in
`/usr/share/regolith/{common,i3}/config.d/`. A file with the same name as a
default replaces that default.

`flags/` (first-run markers written by `regolith-ftue`) is git-ignored, so a
fresh install gets the shortcuts overlay and the gnome-terminal profile setup.
