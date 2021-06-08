---
title: "Power Settings"
tags:
  - arch linux
sidebar:
    nav: "arch-config"
---

# Hibernation

```sh
$   sudo filefrag -v /swapfile
```

Check `<OFFSET>` get the fourth
col `38912`:
```
Filesystem type is: ef53
File size of /swapfile is 4294967296 (1048576 blocks of 4096 bytes)
 ext:     logical_offset:        physical_offset: length:   expected: flags:
   0:        0..       0:      38912..     38912:      1:
```

add to kernel parameters in `/boot/efi/EFI/refind/refind.conf` (rEFIND):
```
"Boot with standard options" "root=... resume=UUID=<UUID> resume_offset=<OFFSET>"
```
* NOTE: UUID is same as root UUID


add resume to `/etc/mkinitcpio.conf`
```ini
HOOKS=(... udev ... resume fsck)
```

rebuild initramfs:
```sh
$   sudo mkinitcpio -P
```

Finally, to hibernate and to check its status:
```sh
$   systemctl hibernate

$   systemctl status systemd-hiberate
```

> * NOTE: You may need to disable Fast Boot in Windows or Hibernation (read-only)
