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
$   pacman -S xfce4 xfce-goodies
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

> ### >> LightDM

For some reason it is best to follow this method to prevent weird bugs:

First install `gdm` and enable then reboot:
```sh
$   pacman -S gdm
$   systemctl enable gdm
```

However I prefer to use `lightdm`, since it is easier to run start-up custom scripts at login.

Boot into a DE and install `lightdm` after `gdm` and `lightdm-webkit2-greeter`
```sh
$   pacman -S lightdm
$   yay -S lightdm-webkit2-greeter
$   systemctl disable gdm
$   systemctl enable lightdm
```

Change config to run webkit2-greeter and allow graphics to load by logind:

`/etc/lightdm.conf`
```ini
...
greeter-session=lightdm-webkit2-greeter
...
logind-check-graphical=true
...
```

Reboot into system, however for some reason default webkit2 theme has extremely high CPU usage, so I prefer to use a different theme:
```sh
$   yay -S lightdm-webkit-theme-litarvan
```

then finally change theme:

`/etc/lightdm/lightdm-webkit2-greeter.conf`
```ini
...
webkit_theme        = litarvan
```
