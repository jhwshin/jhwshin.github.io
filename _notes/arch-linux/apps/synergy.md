---
title: "Applications"
tags:
  - arch linux
sidebar:
    nav: "arch-apps"
---

# Synergy

Install package:
```
$   pacman -S synergy
```

> ## Connect

Before attempting to automate Synergy connections run at Synegy GUI least once and connect to save SSL configs on both USER and ROOT and GRACEFULLY EXIT.

```sh
$   synergy
$   sudo synergy
```

You may want to run seperate instances for Display Manager and Desktop Environment.

For example, in `LightDM` start `synergyc` in login manager then kill the process after logging it to handover to Desktop Environment:
`/etc/lightdm/lightdm.conf`
```ini
greeter-setup-script=/usr/bin/synergyc --enable-crypto --name <NAME> <IP>:<PORT>
session-setup-script=/usr/bin/killall -w synergyc
```

Then for example in `i3`:
```sh
exec synergy
```

---

> ## Mouse Buttons FIX

Windows and Linux may have different mouse bindings, so edit in SERVER.

Windows (HOST) to Linux (CLIENT):
```conf
section: options
    mousebutton(4) = mousebutton(6)
    mousebutton(5) = mousebutton(7)
end
```
for reverse, vice versa.
