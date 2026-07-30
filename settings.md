---
title: Settings reference
layout: default
parent: Reference
nav_order: 3
---

# Settings reference

Every setting the app exposes, grouped as it appears in the **Settings** overlay.

{: .screenshot }
The Settings overlay with a red box around the Network, API, and User preferences categories in the left rail.

---

## Network

Robot connectivity and local data recovery.

| Setting | Default | Purpose |
|---|---|---|
| **Robot URL** | `http://192.168.1.22:3000` | Standard Bots controller address |
| **Control-box LAN address** | — | Controller's LAN IPv4 address |
| **ROS 2 Ethernet adapter IPv4** | Auto | Pin the adapter on a multi-NIC PC |
| **ROS 2 bot ID** | Auto | Leave blank unless auto-detection fails |
| **Authorization token** | — | Developer API token, encrypted on save |
| **Connect telemetry automatically** | On | Reconnect read-only telemetry at launch |

| Action | Effect |
|---|---|
| **Encrypt & save settings** | Stores the settings; the token is encrypted with Windows DPAPI |
| **Configure Windows ROS2 firewall** | Adds an app-scoped UDP rule for private and domain profiles on the local subnet; needs administrator approval |
| **Reset robot connection settings** | Clears the URL and token |
| **Repair local data** | Rewrites unreadable application data files |

Leave telemetry autoconnect on for a production station so a reboot recovers without an integrator.

See [Connect the robot]({{ site.baseurl }}/connect-robot.html).

---

## API

Camera connectivity and diagnostics.

| Setting | Default | Purpose |
|---|---|---|
| **Camera IP** | `192.168.1.20` | Cognex camera address |
| **Native Mode port** | `23` | TCP port used to read cells |

| Tool | Purpose |
|---|---|
| **Run Protocol Probe** | Confirms the PC can reach the camera and read cells |
| **Native Mode console** | Send commands manually while debugging a job |
| **FTP browser** | Browse job files on the camera |

See [Cognex vision setup]({{ site.baseurl }}/cognex.html).

---

## User preferences

### Appearance

| Setting | Purpose |
|---|---|
| **Theme** | Application colour scheme |
| **UI scale** | Interface size; useful on a panel PC |

### Jog defaults

Applied when **Move** opens; adjustable live in the jog HUD.

| Setting | Default | Range |
|---|---|---|
| **Speed** | 40% | 1–100% of the teach speed ceiling |
| **Linear step** | 1 mm | about 0.5–200 mm |
| **Rotational step** | 1 degree | about 0.5–45 degrees |

See [Move and jogging]({{ site.baseurl }}/move.html).

### Camera tooltip offset

X, Y, Z in millimetres and roll, pitch, yaw in degrees, describing the camera tip relative to the wrist. Used to classify the active tooltip and to drive the simulated arm offline.

{: .warning }
Change only if your end effector geometry differs from the configured default. A wrong offset makes the tooltip gate misjudge the robot's state. See [End effector and tooltip]({{ site.baseurl }}/end-effector.html).

### Pass / fail source

| Setting | Default | Purpose |
|---|---|---|
| **Result source** | Cognex | Cognex polling, or manual operator scoring |
| **Result cell** | `K15` | Classification cell, `1` pass and `0` fail |
| **Screw count cell** | `L15` | Accumulator cell, increments once per feature |
| **Pass values** | `1` | Comma-separated values treated as a pass |
| **Poll interval** | 200 ms | How often the cells are read during a run |
| **Count reset event** | `1` | Cognex soft event fired before a run to zero the count |

Setting the source to **Manual** is the fastest way to validate motion independently of the vision job. See [Test run and validation]({{ site.baseurl }}/test-run.html).

### Modbus TCP server

| Setting | Default | Purpose |
|---|---|---|
| **Enable on launch** | On | Start the server automatically |
| **Listen port** | `502` | Standard Modbus TCP port |

| Action | Purpose |
|---|---|
| **Start / restart server** | Apply a port change or recover the server |
| **Self-test** | Local read to confirm the server answers |
| **Open firewall for Modbus** | Inbound rule; needs administrator approval |

The panel also reports status, connected client count, and the last client address. See [Modbus setup]({{ site.baseurl }}/modbus.html).

### Keyboard shortcuts

All rebindable.

| Action | Default |
|---|---|
| Jog X | `A` / `D` |
| Jog Y | `W` / `S` |
| Jog Z | `Q` / `E` |
| Toggle XYZ / Angle | `P` |
| Capture waypoint | `Enter` |
| Software emergency stop | `Space` |

{: .warning }
If you rebind the emergency stop, tell every operator on the station. Leaving it on `Space` is usually the right call.

---

## Settings that live elsewhere

| Setting | Where |
|---|---|
| Active tooltip | On the robot, via **SB Controller** |
| Factory project, unlock password, HMI cell addresses | **Factory config** |
| Robot routine name expected by the app | Schema options when compiling |
| Cognex job logic and cell contents | The Cognex job itself |
