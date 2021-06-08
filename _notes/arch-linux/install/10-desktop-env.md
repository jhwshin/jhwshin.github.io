---
title: "Arch Linux - Basics"
tags:
  - arch linux
sidebar:
    nav: "arch-install"
---

# DESKTOP ENVIRONMENT

> __Choose Any:__

> ### >> i3

Install i3 - a tiling windows manager, an i3 status bar and a menu launcher.

```sh
$   pacman -S i3 i3status dmenu
```

> ### >> XFCE

Install XFCE and extra plugins/apps.

```sh
$   pacman -S xfce4 xfce4-goodies
```

> ### >> GNOME

Install GNOME and extra plugins/apps.

```sh
$   pacman -S gnome gnome-extra
```

> ### >> KDE

Install KDE and extra plugins/apps.

```sh
$   pacman -S plasma-meta kde-applications-meta
```

> ### >> Cinnamon

```sh
$   pacman -S cinnamon
```

## DESKTOP MANAGER

> __Choose One:__

> ### >> Xinit

This method will boot your Arch into a TTY.

1. Copy default xinitrc configs to home:
```sh
$   cp /etc/X11/xinit/xinitrc /home/<USER>/.xinitrc
```

2. Add startx entries to Desktop Environments at the end of the file depending on your Desktop Environment:
```sh
$   nano /home/<USER>/.xinitrc
```
```ini
...
exec i3
# exec xfce4-session
# exec gnome-session
# exec startplasma-x11
# exec cinnamon-session
```

3. Start an xsession run:
```sh
$   startx
```

Otherwise if you are a sane person use a proper DM:

> ### >> GDM

Install `gdm` and enable:
```sh
$   pacman -S gdm
$   systemctl enable gdm
```
