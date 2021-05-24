---
title: "Arch Linux - Base Install"
tags:
  - arch linux
sidebar:
    nav: "arch-install"
---

# DRIVERS

## 1. CPU

Install CPU's microcode - processor's firmware for security and stability patches.

> __Choose One:__

> ### >> Intel

```sh
$   pacman -S intel-ucode
```

> ### >> AMD

```sh
$   pacman -S amd-ucode
```

## 2. Display Server

Essential for GUI Applications

> ### >> Xorg

Install xorg and extra applications (useful for debugging and testing):

```sh
$   pacman -S xorg xorg-apps
```

## 3. GPU

> __Choose One:__

> ### >> Intel - Integrated Graphics

```sh
$   pacman -S xf86-video-intel mesa lib32-mesa vulkan-intel lib32-vulkan-intel
```

To prevent screen tearing add entry to :

`/etc/X11/xorg.conf.d/20-intel.conf`
```conf
Section "Device"
  Identifier "Intel Graphics"
  Driver "intel"
  Option "TearFree" "true"
EndSection
```

> ### >> NVIDIA - Proprietary

```sh
$   pacman -S nvidia nvidia-utils lib32-nvidia-utils nvidia-settings
```

Automatic configuration for `/etc/X11/xorg.conf`

```sh
$   nvidia-xconfig
```

To prevent screen tearing add entry to:

`/etc/X11/xorg.conf`
```conf
Section "Screen"

    ...

    Option         "MetaModes" "nvidia-auto-select +0+0 {ForceFullCompositionPipeline=On}"
    Option         "AllowIndirectGLXProtocol" "off"
    Option         "TripleBuffer" "on"

    ...

EndSection
```

You may want to add hooks during system update, incase the linux kernel updates you want to force build initramfs to include nvidia modules:

`/etc/pacman.d/hooks/nvidia.hook`
```ini
[Trigger]
Operation=Install
Operation=Upgrade
Operation=Remove
Type=Package
Target=nvidia
Target=linux
# Change the linux part above and in the Exec line if a different kernel is used

[Action]
Description=Update Nvidia module in initcpio
Depends=mkinitcpio
When=PostTransaction
NeedsTargets
Exec=/bin/sh -c 'while read -r trg; do case $trg in linux) exit 0; esac; done; /usr/bin/mkinitcpio -P'
```
