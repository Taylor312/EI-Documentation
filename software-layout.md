---
title: Software layout tour
layout: default
parent: Setup and integration
nav_order: 2
---

# Software layout tour

A map of the interface, so the rest of this guide can say "open **Routine Editor**" without explaining where that is.

{: .screenshot }
The full application window with red boxes around the sidebar, the title bar, and the main content area, labelled 1, 2, and 3.

## The three regions

| Region | What lives there |
|---|---|
| **Sidebar** (left) | Navigation between the eight main screens, plus **Settings** and the documentation link |
| **Title bar** (top) | Project name, status messages, application menus, factory mode chip |
| **Main area** | Whichever screen you selected |

## Sidebar navigation

**Home** sits at the top as a large button. The remaining screens are grouped:

| Group | Screens |
|---|---|
| **Workspace** | Robot settings, Projects, SB Controller, Move |
| **Inspection** | Routine Editor, Test Run |
| **Plant** | Factory config |

| Screen | What you do there |
|---|---|
| **Home** | Session overview: connection status, active project, camera and robot link indicators, quick actions |
| **Robot settings** | Connect telemetry, assert API control, unbrake, recover, toggle offline mode |
| **Projects** | Create, open, import, and export projects; manage the routines inside them |
| **SB Controller** | The Standard Bots web interface embedded in the app; used mainly to select the tooltip |
| **Move** | Full-screen 3D view with the jog controls and live telemetry |
| **Routine Editor** | The five-phase teaching workflow for one part |
| **Test Run** | Start inspection scans and review scan history |
| **Factory config** | Lock the station to one project for operators |

At the bottom of the sidebar are **Need help? Read the documentation** (this site) and **Settings**.

The sidebar can be collapsed to an icon-only rail using the handle on its edge.

### Two navigation behaviours worth knowing

- **Robot settings**, **Projects**, **SB Controller**, and **Move** open as tiles in a 2x2 workspace on the Home screen. Selecting the same tab again returns you to Home.
- **Move**, and the Routine Editor phases that need 3D, take over the whole window. Exit by choosing **Home** or by selecting the same tab again.

{: .screenshot }
The Home 2x2 workspace with red boxes around each of the four tiles: Robot settings, Projects, SB Controller, and Move.

## Title bar

- **Centre:** the active project name, or *Project: none*.
- **Status chip:** transient notices, warnings, and errors. Expand it to read the last message if it disappeared before you saw it.
- **Wrist TCP chip:** appears when the robot's active tooltip looks like the bare wrist flange instead of the camera tip. This blocks waypoint capture and running. See [End effector and tooltip]({{ site.baseurl }}/end-effector.html).
- **Factory mode chip and Exit factory mode:** only in factory mode.

### Menus

| Menu | Contents |
|---|---|
| **File** | New project, Save project, Download `.ie`, Import `.ie`, Quit |
| **View** | Shortcuts to every screen, plus zoom in, zoom out, reset zoom |
| **Edit** | Capture waypoint, Clear waypoints |
| **Window** | Minimize, Maximize, Close |

## Settings overlay

**Settings** in the sidebar opens a modal with three categories:

| Category | Contents |
|---|---|
| **Network** | Robot URL, API token, ROS 2 and firewall helpers, data repair actions |
| **API** | Camera connection, protocol probe, Cognex Native Mode console, FTP browser |
| **User preferences** | Appearance, default jog steps and speed, camera tooltip offset, pass/fail source, Modbus server, keyboard shortcuts |

Every field is documented in [Settings reference]({{ site.baseurl }}/settings.html).

{: .screenshot }
The Settings overlay with a red box around the three category names in the left rail.

## Detachable windows

Two views can pop out into their own OS window, which is useful on a multi-monitor station:

- **Camera window** — the live Cognex feed, detached from **Move**.
- **SB Controller window** — the Standard Bots interface, detached from its tile.

When SB Controller is detached, selecting its sidebar tab focuses the detached window instead of switching tabs.

## Next

Continue to [Connect the robot]({{ site.baseurl }}/connect-robot.html).
