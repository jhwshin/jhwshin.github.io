---
title: "Applications"
tags:
  - arch linux
sidebar:
    nav: "arch-apps"
---

# Macchanger

Install package:
```sh
$   pacman -S macchanger
```

#### >> One Timeshot


```sh
$   macchanger [-r|-e|--mac|-p] <INTERFACE>

-r  complete randomize
-e  randomize (same vendor)
--mac=XX:XX:XX:XX:XX:XX
-p  default
```

#### >> Automatically (At boot)

Create systemd unit file `/etc/systemd/system/macspoof@.service`:
```ini
[Unit]
Description=macchanger on %I
Wants=network-pre.target
Before=network-pre.target
BindsTo=sys-subsystem-net-devices-%i.device
After=sys-subsystem-net-devices-%i.device

[Service]
ExecStart=/usr/bin/macchanger [-r|-e|--mac|-p] <INTERFACE>
Type=oneshot

[Install]
WantedBy=multi-user.target
```
Enable unit file:
```sh
$   systemctl enable macspoof@<INTERFACE>.service
```
