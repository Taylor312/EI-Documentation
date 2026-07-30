---
title: Downloads & versions
layout: default
nav_order: 10
description: Installers and version history for Easy Inspection
---

# Downloads & versions

Use this page for Windows installers and a short version history.

{: .warning }
Only install builds from a source you trust. Prefer signed `Setup.exe` packages when available. Keep a trained operator and a hardware e-stop ready when testing a new build against a live robot.

## Current release

| Version | Date | Notes | Download |
|---------|------|-------|----------|
| **3.7.0** | — | Current app version in development (Teach / Run / factory / Modbus) | _Installer link TBD_ |

When you publish a Squirrel installer, drop the file into GitHub **Releases** (app repo or this docs repo) and replace the TBD cell with a direct link.

## How to publish an installer here

1. Build with `npm run make` in the Easy Inspection app repo (produces `EasyInspectionSetup.exe` under `out/make/...`).
2. Create a [GitHub Release](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository) (tag e.g. `v3.7.0`) and attach the Setup.exe.
3. Update the table above with the version, date, short notes, and the release asset URL.

## Older versions

| Version | Date | Notes | Download |
|---------|------|-------|----------|
| — | — | No archived public builds listed yet | — |

## Install notes

- Target OS: **Windows** (Squirrel installer).
- End-user machines do **not** need Node, ROS2, Pixi, or Visual Studio — the packaged app includes required sidecars.
- After install, configure the robot URL and API token in **Settings** — see [Connect the robot](connect-robot.md).
- App data stays under `%APPDATA%\Easy Inspection\` across upgrades — see [Data & backup](data.md).
