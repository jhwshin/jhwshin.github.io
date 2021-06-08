---
title: "Arch Linux - Base Install"
tags:
  - arch linux
sidebar:
    nav: "arch-install"
---

# BASE INSTALL

> Reflector or Manually

## 1. Update Mirrors

Create backup for mirrors:
```sh
$   cd /etc/pacmand.d
$   cp mirrorlist mirrorlist.bak
```

> ### >> Reflector

Force update mirrors and install `reflector`:
```sh
$   pacman -Syy reflector
```

* NOTE: With latest Arch ISO it is usually already included.

Choose from a list of countries:
```sh
$   reflector --list-countries
```

Update mirrorlist:
```sh
$   reflector -c "<COUNTRY>" --fastest 12 --latest 12 --number 12 --save /etc/pacman.d/mirrorlist
```

> ### >> Manually

If `reflector` failed to run, change the mirror manually:
```sh
$   cat mirrorlist.bak | grep "<COUNTRY>" -A 1 || sed 's/--//' > mirrorlist
```

<br>

If update fails, sometimes arch keyrings could be out of date, so download and then refresh them:
```sh
$   pacman -S archlinux-keyring
$   pacman-key --populate archlinux
$   pacman-key --refresh-keys
```

## 2. Install Arch Base

Install base, developer packages, linux-longterm (for a stable version), version control (for installing AUR) and the very best text editor with highlighting:
```sh
$   pacstrap /mnt base base-devel linux linux-firmware linux-lts linux-headers linux-headers-lts linux-api-headers git nano nano-syntax-highlighting
```

## 3. Generate fstab

Create partition entries for automount (-U using UUID):
```sh
$   genfstab -U /mnt >> /mnt/etc/fstab
```
