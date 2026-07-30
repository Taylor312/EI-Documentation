---
title: Connect the robot
layout: default
nav_order: 3
---

# Connect the robot

## Steps

1. Connect the workstation to the robot cabinet network.
2. Open Easy Inspection.
3. Open **Settings**, verify the robot URL, and enter the authorization token once.
4. In the robot web UI, enable both **ROS2 API** and **ROS2 bridge** under **Settings → Configure Developer API**.
5. Enter the control-box LAN IPv4 address. If automatic adapter selection is ambiguous, also enter the Windows Ethernet adapter IPv4 address.
6. Select **Configure Windows ROS2 firewall** and approve the administrator prompt when prompted.
7. Save settings. The app starts read-only REST telemetry.
8. Resolve robot faults, unbrake if appropriate, then assert API control before jogging.

## Token storage

The token is encrypted with Electron `safeStorage` (Windows DPAPI) under the current user's app data. It is not returned to the UI after saving and is not written to logs.

Local runtime data lives under:

```text
%APPDATA%\Easy Inspection\
```

Changing settings format in experiments, or regenerating the Developer API token on the tablet, requires updating the token in Easy Inspection (**Encrypt & save** → Connect) again.

## If connection fails

- Confirm tablet **Play** works with the same token before debugging the desktop app.
- A `401` on motion routes is controller auth — not a teach/compile bug.
- After regenerating a token on the tablet, reboot the control box if tablet Play still returns `401 Invalid token`, then reconnect from Easy Inspection.
