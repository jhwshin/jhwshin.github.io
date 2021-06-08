---
title: "Arch Linux - Surface Pro 3"
tags:
  - arch linux
sidebar:
    nav: "arch-config"
redirect_from:
  - /notes/arch-linux/surface-pro-3/
prev-section: /notes/arch-linux/config/09-backup/
---

# Arch Patches

* Add rEFIND Image
* Add Arch Image with my dotfiles

## 0. Surface Arch Patch

[Linux Surface Kernel Patch](https://github.com/linux-surface/linux-surface)

> ### >> Import Keys

```sh
$   wget -qO - https://raw.githubusercontent.com/linux-surface/linux-surface/master/pkg/keys/surface.asc \
    | sudo pacman-key --add -
```

For security, verify the fingerprint of the key and then sign it locally:
```sh
$   sudo pacman-key --finger 56C464BAAC421453
$   sudo pacman-key --lsign-key 56C464BAAC421453
```

> ### >> Add Mirrors

Add mirror to: `/etc/pacman.conf`:
```ini
[linux-surface]
Server = https://pkg.surfacelinux.com/arch/
```

> ### >> Install Patches

Refresh repository and then install binary dependencies:
```sh
$   sudo pacman -Syu
$   sudo pacman -S linux-surface linux-surface-headers linux-surface-lts linux-surface-lts-headers iptsd surface-ipts-firmware
```

Enable iptsd for touchscreen support:
```sh
$   sudo systemctl enable iptsd
```

```sh
$   yay -S libwacom-surface
```


## 1. Secure Boot

To remove the ugly orange screen you need to sign kernel and bootloader using Machine Owner Key to boot into Secure Boot Mode.

> ### >> MOK Sign

Install `shim`:
```sh
$   pacman -S shim-signed sbsigntools
```

Create keys:
```sh
$   refind-install --shim /usr/share/shim-signed/shimx64.efi --localkeys
```

Sign keys:
```sh
$   sbsign --key /etc/refind.d/keys/refind_local.key --cert /etc/refind.d/keys/refind_local.crt --output /boot/vmlinuz-linux-surface /boot/vmlinuz-linux-surface
```

Setup auto sign using pacman hook `/etc/pacman.d/hooks/sbsign.hook`:
```systemd
[Trigger]
Operation = Install
Operation = Upgrade
Type = Package
Target = linux
Target = linux-lts
Target = linux-surface
Target = linux-surface-lts
Target = refind
Target = intel-ucode

[Action]
Description = Signing Kernel with MOK for Secure Boot
When = PostTransaction
Exec = /usr/bin/find /boot/ -maxdepth 1 -name 'vmlinuz-*' -exec /usr/bin/sh -c 'if ! /usr/bin/sbverify --list {} 2>/dev/null | /usr/bin/grep -q "signature certificates"; then /usr/bin/sbsign --key /etc/refind.d/keys/refind_local.key --cert /etc/refind.d/keys/refind_local.crt --output {} {}; fi' ;
Depends = sbsigntools
Depends = findutils
Depends = grep
```

Now test to see if hooks works:
```sh
$   sudo pacman -S linux linux-lts linux-surface linux-surface-lts
```

Finally, enrol __refind_local.cer__ to MOK LIST using mok_tool at bootloader to allow Secure Boot. It should be located in `/boot/EFI/efi/refind/keys/`

And remember to boot into correct linux kernel, it should be `linux-surface`.


## 2. Power Options

> ### >> WiFi Hibernation Fix

Due to bugs in Marvell Technology [AVASTAR] Wireless drivers, hibernation kills the WiFi device making it irrecoverable even if you reload it after the crash.
Hence a solution is to gracefully unload and reload the module manually when hibernating.


Execute the script pre and post hibernation:

`~/bin/sp3-hibernate-hook [pre|post]`
```sh
#!/usr/bin/env sh

case $1 in
    "pre")
        systemctl stop NetworkManager;
        modprobe -r mwifiex_pcie;
        modprobe -r mwifiex;
    ;;
    "post")
        modprobe -i mwifiex;
        modprobe -i mwifiex_pcie;
        systemctl start NetworkManager;
    ;;
esac
```

To automate the process you can use a systemd UNIT file:

`/etc/systemd/system/[pre|post]-hibernate.service`
```systemd
[Unit]
Description=[Pre|Post]-Hibernation Script
[Before|After]=hibernate.target

[Service]
Type=oneshot
ExecStart=/bin/sh /home/hws/bin/sp3-hibernate-hook [pre|post]

[Install]
WantedBy=hibernate.target
```

```sh
$   systemctl enable [pre|post]-hibernate
```

> ### >> Power Switch / Lid

[Power Switch]({{ site.baseurl }}{% link _notes/arch-linux/config/06-power-switch.md %})

> ### >> Low Battery

[Power Manager]({{ site.baseurl }}{% link _notes/arch-linux/config/04-power-manager.md %})

> ### >> Power Saving

[Power Saving]({{ site.baseurl }}{% link _notes/arch-linux/config/05-power-saving.md %})

## 3. Gestures - #TODO

> ### >> Touch Screen

> ### >> Touchpad

## 4. Network - #TODO

> ### >> Reverse SSH

> ### >> Reverse VPN
