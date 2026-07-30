---
title: Downloads and versions
layout: default
parent: Overview
nav_order: 3
description: Installers and version history for Easy Inspection
---

# Downloads and versions

Windows installers and version history for Easy Inspection.

{: .warning }
Only install builds from a source you trust, and prefer signed installers. Do not upgrade a production station mid-shift. Validate a new build against a taught routine before running parts on it.

## Current release

| Version | Date | Notes | Download |
|---|---|---|---|
| **3.7.0** | — | Teach, run, factory mode, Modbus bridge, Cognex result polling | *Installer link to be added* |

## Older versions

| Version | Date | Notes | Download |
|---|---|---|---|
| — | — | No archived public builds published yet | — |

---

## Install notes

- **Platform:** Windows. The installer is a Squirrel-based `Setup.exe`.
- **No developer tooling needed.** Operator and integrator machines do not need Node, Python, ROS 2, or Visual Studio. Everything the app needs ships inside the installer.
- **Not portable as a folder.** The unpacked application directory depends on the files beside it. To move a build, copy the whole directory, or reinstall from `Setup.exe`.
- **After installing,** configure the robot connection in **Settings** — see [Connect the robot]({{ site.baseurl }}/connect-robot.html).

## Upgrading

Application data lives outside the install directory, so upgrading in place keeps your projects, routines, preferences, and scan history. See [Projects, storage and backup]({{ site.baseurl }}/data.html).

Before upgrading a commissioned station:

1. Export a `.ie` package of the production project as a backup.
2. Note the current version in case you need to roll back.
3. After upgrading, run one validation scan before releasing the station back to production.

{: .warning }
The robot API token is encrypted per Windows user and machine. It does not transfer to a different PC, and it cannot be recovered from a copied data folder. Keep the token available separately when you re-image or replace a station.

---

## Publishing a build to this page

For whoever maintains releases:

1. Build the installer in the application repository (`npm run make`), which writes a `Setup.exe` under `out/make/`.
2. Create a GitHub Release tagged with the version, for example `v3.7.0`, and attach the installer.
3. Update the table above with the version, date, a one-line summary of what changed, and a direct link to the release asset.
4. Move the previous entry into **Older versions**.
