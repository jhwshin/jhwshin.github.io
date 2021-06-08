---
title: "Applications"
tags:
  - arch linux
sidebar:
    nav: "arch-apps"
redirect_from:
  - /notes/arch-linux/apps/
prev-section: /notes/arch-linux/surface-pro-3/windows-sp3/
---

# Firefox

To configure settings type this in URL `about:config`

Prevent Screen Tearing:
```sh
layers.acceleration.force-enabled true
webgl.force-enabled true
media.hardware-video-decoding.force-enabled true
browser.tabs.remote.autostart true
```

Useful when using fullscreen windowed:
```sh
full-screen-api.ignore-widgets true
```

Sometimes, you may need to reload nvidia configs if it is laggy:
```sh
$   sudo nvidia-xconfig
```

Check if graphics module is loaded (e.g nvidia):
```sh
$   glxinfo | grep -i nvidia
```
