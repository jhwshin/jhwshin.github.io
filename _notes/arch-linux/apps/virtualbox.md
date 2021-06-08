---
title: "Applications"
tags:
  - arch linux
sidebar:
    nav: "arch-apps"
last-post: true
---

# Virtualbox

> ## >> Host

Install Virtual Box package:
```sh
$   pacman -S virtualbox
```

Choose: `virtualbox-host-modules-arch` for arch

> ## >> Guest

Install Guest Virtal Box Utils:
```sh
$   pacman -S virtualbox-guest-utils
```

Run command inside Guest Box (loading kernel modules):
```sh
$   systemctl enable vboxservice
```
