---
title: "Arch Linux - Basics"
tags:
  - arch linux
sidebar:
    nav: "arch-install"
next-section: /notes/arch-linux/config/00-time-fix/
---

# POST-INSTALL

> ## >> AUR

Arch User Repository - best thing about Arch:

```sh
$   git clone https://aur.archlinux.org/yay.git
$   cd yay
$   makepkg -si
```

> ## >> LightDM

I prefer to use `lightdm`, since it is easier to run start-up custom scripts at login.

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

> ## >> dotfiles

Custom configs to make your Arch prettier

* [Unixporn for Linux Ricing](https://www.reddit.com/r/unixporn/)

* [My dotfiles](https://github.com/jhwshin/dotfiles)

> ## >> rEFIND (dreary-theme)

* [My rEFIND config](https://github.com/jhwshin/refind-dreary)
