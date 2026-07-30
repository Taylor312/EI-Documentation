---
title: Introduction
layout: default
parent: Overview
nav_order: 1
description: What Easy Inspection is, who it is for, and how this guide is organized
---

# Easy Inspection

Easy Inspection is a Windows desktop application that sits alongside a Standard Bots robot and turns it into a camera-based part inspection station.

It does three things that are painful to do with the robot's own tooling alone:

- **Teaching.** A guided workflow for capturing inspection poses, keep-out volumes, and safe home positions in a live 3D view, with a jog control that responds immediately instead of lagging behind every step.
- **Inspection.** A run screen that triggers a Cognex camera at each taught point, reads pass/fail and part-count values back out of your Cognex job, and tallies results per part.
- **Integration.** A Modbus TCP bridge so the robot program, and optionally a PLC, can coordinate with the PC in a real production cell.

{: .warning }
This software commands physical industrial machinery. Guard the work cell, keep a trained operator at the hardwired emergency stop, and read [Safety]({{ site.baseurl }}/safety.html) before commissioning. The on-screen red button and Spacebar shortcut are a *software* stop only.

---

## Why use it instead of programming the robot by hand

You can build an inspection routine directly on the Standard Bots tablet. Easy Inspection exists because doing that at scale is slow and hard to maintain.

- **Jogging is faster.** The robot's built-in jog waits roughly a second before each move commits, which makes precise teaching tedious. Easy Inspection drives finite Cartesian steps over the REST API, so a jog press moves the arm right away. See [Move and jogging]({{ site.baseurl }}/move.html).
- **Teaching is structured.** Instead of hand-placing dozens of moves, you capture waypoints against a live 3D model, define no-go volumes once, and let the app plan approach paths around them. See [Teaching a routine]({{ site.baseurl }}/teach-routine.html).
- **Routines are generated, not hand-written.** The app compiles your taught data into a single Standard Bots routine, including the Modbus handshake and the camera trigger outputs. Re-teaching a part means re-compiling, not rewriting robot code. See [Compile and deploy the schema]({{ site.baseurl }}/deploy-schema.html).
- **Vision results come back into one place.** Pass/fail and count values from the Cognex job are polled during the run and mapped onto the specific waypoint that produced them, so you get a per-feature result rather than one verdict for the whole part.
- **Operators get a locked screen.** Factory mode hides everything except the run screen and pins the station to one project, so a line operator cannot wander into teach mode. See [Factory mode setup]({{ site.baseurl }}/factory-config.html).

### What it is not

Easy Inspection is a quality-of-life layer, not a robot controller and not a safety system.

- It does **not** replace the Standard Bots controller, its safety configuration, or its routine editor. Routines still live on and execute from the robot.
- It does **not** provide functional safety. All stops it offers are software stops.
- It does **not** ship a vision program. You train your own Cognex job; the app only reads cells out of it. See [Cognex vision setup]({{ site.baseurl }}/cognex.html).
- In factory mode it *emulates* external start/stop by driving the robot over the REST API. Real external control from a PLC still has to be configured on the robot itself. See [External control and PLC integration]({{ site.baseurl }}/external-control.html).

---

## Who this guide is for

This site is written primarily for the **integrator**: the person commissioning the cell, training the camera, wiring Modbus, teaching routines, and locking the station down.

There is a separate, self-contained [Operator manual]({{ site.baseurl }}/operator/) at the end for the person who just runs parts on a finished station.

---

## How this guide is organized

- **[Overview]({{ site.baseurl }}/overview/)** — this page, the [system and control model]({{ site.baseurl }}/system-overview.html), and [downloads]({{ site.baseurl }}/downloads.html). Read this first to understand how the pieces fit together.
- **[Setup and integration]({{ site.baseurl }}/setup/)** — the commissioning sequence, in order, from installing the app to enabling factory mode. This is the bulk of the guide.
- **[Reference]({{ site.baseurl }}/reference/)** — the end-to-end [workflow summary]({{ site.baseurl }}/workflow.html), [where data is stored]({{ site.baseurl }}/data.html), a full [settings reference]({{ site.baseurl }}/settings.html), [troubleshooting]({{ site.baseurl }}/troubleshooting.html), and [safety]({{ site.baseurl }}/safety.html).
- **[Operator manual]({{ site.baseurl }}/operator/)** — how to run parts once the station is locked into factory mode.

Conventions used throughout:

- **Bold** text names something you click or type in the app.
- Warning callouts flag anything that can move the robot unexpectedly or lose data.
- Screenshot callouts mark where an annotated screenshot belongs; they are placeholders until the image is added.

{: .screenshot }
The Easy Inspection Home dashboard on a connected station, with a red box around the sidebar navigation.

---

## Where to start

If you are commissioning a new station, work straight through [Setup and integration]({{ site.baseurl }}/setup/), beginning with [Install and first launch]({{ site.baseurl }}/install.html).

If you want the short version of the whole process first, read [Typical workflow]({{ site.baseurl }}/workflow.html).
