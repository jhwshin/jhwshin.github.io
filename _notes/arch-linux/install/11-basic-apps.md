---
title: "Arch Linux - Basics"
tags:
  - arch linux
sidebar:
    nav: "arch-install"
---

# BASIC APPLICATIONS

> ## >> Audio

Pulse Audio (pavucontrol) is a sound server abstraction layer that sits on top of ALSA (alsamixer) the sound kernel driver.

```sh
$   pacman -S alsa-utils pavucontrol
```

> ## >> Network

Install Network Manager and its tray applet, then enable autostart:

```sh
$   pacman -S networkmanager network-manager-applet
$   systemctl enable NetworkManager
```

* Note: To have network manager start before login, run `nm-connection-editor` and edit connection to enable `All users may connect to this network`.

> ## >> Bluetooth

Install Bluetooth protocol stack and its tray applet, load driver to kernel module then enable autostart:

```sh
$   pacman -S bluez bluez-utils blueman
$   modprobe btusb
$   systemctl enable bluetooth
```

> ## >> SSH

```sh
$   pacman -S openssh
$   systemctl enable sshd
```

* This will open up your system to the network! Remember to setup `/etc/sshd` config and use keys instead of password for security.

> ## >> XDG

Catalogs for software configurations (dotfiles):

```sh
$   pacman -S xdg-utils xdg-user-dirs
```

## !! THE FINAL STEP !!

Exit chroot, umount then reboot.

```sh
$   exit
$   umount -R /mnt
$   reboot
```

---

If you've gotten this far, good job.

This install will set you up with a VERY basic Linux system if everything goes well.

If boot fails, don't give up! I have failed Arch install more times than I'd like to admit. Check the [Arch Wiki](https://wiki.archlinux.org/) for more details as these notes are far from comprehensive.

This is only the beginning so check out `CONFIGURATIONS` for ricing to customize your very own system.

Good luck!

---
