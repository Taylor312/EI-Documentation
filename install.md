---
title: Install and first launch
layout: default
parent: Setup and integration
nav_order: 1
---

# Install and first launch

**Prerequisites:** a Windows PC on the same network as the robot controller, and the installer from [Downloads and versions]({{ site.baseurl }}/downloads.html).

## What the PC needs

The station PC does the vision polling, hosts the Modbus server, and renders a live 3D view, so it should be a real workstation rather than a thin client.

| Requirement | Notes |
|---|---|
| Windows | The installer is a Windows Squirrel package |
| Network access to the robot controller | Usually a wired plant subnet |
| Network access to the Cognex camera | Often a **separate** NIC from the robot network |
| Administrator rights (once) | Only to open the Windows firewall for Modbus |

{: .warning }
Two network interfaces on similar-looking subnets is the single most common source of trouble in this system. If the camera is on one NIC and the robot on another, note which address belongs to which before you start. See [Modbus setup]({{ site.baseurl }}/modbus.html).

## Install

1. Run `Setup.exe`.
2. Launch **Easy Inspection**.

No separate runtime installation is required. Everything the application needs is bundled.

## First launch

On a machine with no saved robot credentials, the app opens the **Settings** overlay on the **Network** page automatically. This is expected — it is asking for the robot address and API token before it will try to talk to anything.

{: .screenshot }
The Settings overlay on first launch, with a red box around the Network category in the left rail and the Robot URL and Authorization token fields.

You have two ways to proceed:

- **Connect to a real robot now.** Continue to [Connect the robot]({{ site.baseurl }}/connect-robot.html).
- **Explore without hardware.** Close Settings and turn on **Offline mode** from the Home dashboard. The app then simulates a robot so you can learn the interface, create projects, and capture waypoints without a controller.

### Offline mode

Offline mode bypasses the robot REST API entirely and drives a simulated arm instead.

- Teaching, waypoint capture, path editing, and offline schema simulation all work.
- The software stop only clears simulated motion.
- You must **exit offline mode** before connecting to a live robot.

It is the right choice for learning the app, for building a project before the cell is wired, and for reproducing a customer issue at a desk.

{: .screenshot }
The Home dashboard with a red box around the Offline mode toggle.

## Verify the install

Before moving on, confirm:

1. The app opens to the Home dashboard.
2. The sidebar shows **Home**, **Robot settings**, **Projects**, **SB Controller**, **Move**, **Routine Editor**, **Test Run**, and **Factory config**.
3. **Settings** opens and closes cleanly.

If the sidebar is missing entirely and the title bar shows a **Factory mode** chip, the station is locked. Use **Exit factory mode** with the unlock password to get back to the full application — see [Factory mode setup]({{ site.baseurl }}/factory-config.html).

## Next

Get a tour of the interface in [Software layout tour]({{ site.baseurl }}/software-layout.html), or go straight to [Connect the robot]({{ site.baseurl }}/connect-robot.html).
