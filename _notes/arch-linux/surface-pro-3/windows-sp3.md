---
title: "Arch Linux - Surface Pro 3"
tags:
  - arch linux
sidebar:
    nav: "arch-config"
next-section: /notes/arch-linux/apps/firefox/
---

# Windows Patches

## Network Fixes

Surface products have some weird issues with WiFi drivers.

They can be flaky (packet loss), experience strange ping spikes and sometimes disconnects after waking up from suspending.

> ### >> Update Network Driver - #TODO

You may need to update network driver manually.

> ### >> Regedit Network Fix

[Windows Support](https://support.microsoft.com/en-us/topic/poor-wireless-connectivity-on-surface-devices-running-windows-10-and-using-netgear-r8000-or-verizon-mifi-router-e5d4faa4-ba4b-f2c3-7688-4391c06803c5)

1. Open Windows `regedit`

2. Navigate to PATH:
```
HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Services\mrvlpcie8897
```

3. Modify value `TXAMSDU` from 1 to 0.

4. Restart Machine


## Update GPU Driver - #TODO

Sometimes it is best to update Intel Integrated Graphics for better performance and battery saving capabilities.


##  Power Management

Surface Pro 3, runs hot and is power hungry at times making battery life horrendous. Here are some fixes that has significantly improved my battery and my fan's well being.

> ### >> Firefox  - h264 fix (e.g Youtube)

Addon h264ify - plays media using h264 instead of vp9

* h264 = low cpu, gpu hardware accelerated  = better battery
* VP9  = low net bandwidth, cpu accelerated = shorter battery

> ### >> Enable Hidden Power Settings

For some reason Windows has disable power saving features in the Control Panel.

1. Open Windows `regedit`

2. Navigate to PATH:

```
HKLM\System\CurrentControlSet\Control\Power\PowerSettings
```

3. For all GUID, add a `REG_DWORD` with name of `Attributes` to `2`

4. Now in Power Settings you should have extra Power Saving Modes. Similiarly for Wireless Adapters and Graphics Settings in Device Manager should have Power Plan and Power Saving Modes.

> ### >> Other methods:

* Use Edge browser
* Use Spotify web
* Use Tablet Mode when possible

