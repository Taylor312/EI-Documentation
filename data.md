---
title: Data & backup
layout: default
nav_order: 9
---

# Data & backup

## Live data on this PC

Runtime state lives under:

```text
%APPDATA%\Easy Inspection\
```

| File / folder | Contents |
|---------------|----------|
| `projects.json` | Projects, routines, waypoints, homes, clearance, compiled schemas |
| `app-preferences.json` | UI / run / camera / Modbus preferences |
| `robot-settings.json` | Controller URL + DPAPI-encrypted API token |
| `scans.json` | Run / scan history |
| `downloads/` | Cognex job downloads |

**Git revert does not restore or clear these files.** Reinstalling the same Windows app usually leaves AppData in place.

### Factory / HUD

Factory lock settings and some HUD positions use Chromium **localStorage** for this Windows user. They are not inside `projects.json`.

## Portable `.ie` packages

A `.ie` file is a ZIP-based export/import package. AppData remains the day-to-day database; `.ie` is for backup, USB handoff, or another machine.

Typical contents include project JSON, per-routine waypoints / schema / clearance, and assets. Import assigns new IDs and writes into `projects.json`.

## Moving to another PC

| Travels with `.ie` / file copy | Does not travel |
|--------------------------------|-----------------|
| Projects and routines (via `.ie` or carefully copying `projects.json`) | Encrypted robot token (DPAPI is per Windows user/machine) |
| Preference files (optional manual copy) | Expect to paste a fresh API token on the new PC |

First install on a new PC starts from empty AppData and code defaults.
