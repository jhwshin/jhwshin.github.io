---
title: "Arch Linux - Base Install"
tags:
  - arch linux
sidebar:
    nav: "arch-install"
---

# BOOTLOADER

> __rEFIND or GRUB__

* Add `/boot/<MICROCODE>.img` as the FIRST initrd kernel parameter in bootloader config file.

> ## >> rEFIND (UEFI ONLY)

```sh
$   pacman -S refind
```

Install rEFIND in `/boot`:
```sh
$   refind-install
```

Get `/` PARTUUID:
```sh
$   lsblk -o NAME,PARTUUID | grep <sdXY> >> /boot/refind_linux.conf
```

<br>

rEFIND boot parameter bug fix - edit:

`/boot/refind_linux.conf`
```sh
$   nano /boot/refind_linux.conf
```

```ini
"Boot using default options"     "root=PARTUUID=XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX rw add_efi_memmap"

"boot with std" "root=UUID=XXX rw quiet"
"boot to single" "root=UUID=XXX rw quiet single"
"boot with minimal" "ro root=UUID=XXX"
```

* NOTE: If you are unable to boot to Windows after install (dual boot) you may need to disable Intel Integrated Graphics when running with another dedicated GPU in BIOS.

> ## >> GRUB

```sh
$   pacman -S grub
```

Install grub to `/boot`
```sh
$   grub-install /dev/<sdX>
```

Auto-generate grub config and save to `/boot`
```sh
$   grub-mkconfig -o /boot/grub/grub.cfg
```
