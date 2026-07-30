---
title: Modbus
layout: default
nav_order: 8
---

# Modbus

Easy Inspection runs a **Modbus TCP server** on this PC. The robot equipment **Master** is a Modbus TCP **client** that reads holding registers into routine environment variables.

## Quick connectivity check

1. App running → Preferences → **Modbus TCP server** shows `Listening`.
2. Click **Self-test (FC03 localhost)** — should report `OK`.
3. Click **Open firewall for Modbus** (UAC) if Master stays red.
4. Set Master IP to **Use this IP in Master**. If you have both Ethernet (camera) and Wi‑Fi (robot control box) on similar subnets, they may still be **different physical networks** — Master must use the NIC the control box can reach (often Wi‑Fi to the control box, not the Cognex Ethernet IP).
5. Enable Master. Preferences should show **Clients ≥ 1** and a last-client address from the robot (not `127.0.0.1`).

## Master equipment settings

| Setting | Value |
|---------|--------|
| Name | `Master` |
| Enabled | On |
| IP address | Preferred LAN IPv4 from Preferences (not `0.0.0.0`) |
| Port | `502` (or the listen port in Preferences) |
| Timeout | `10` or higher if the link flaps |

Do **not** use `0.0.0.0` as the client IP — that is only valid as a listen address on the server.

Also set schema **Modbus host** to the same LAN IP when saving the routine (Save schema fills it automatically when blank).

## Holding registers

| Field | Offset | Format | Role |
|-------|--------|--------|------|
| `Inspect` | `0` | UInt16BE | `0` = idle; `1..N` = 1-based screw / step index |
| `Return` | `1` | UInt16BE | `0` = wait; `1` = return toward home |
| `Routine` | `2` | UInt16BE | Nested routine select in factory / master schema flows |

## Two ways data can move

1. **Equipment Master + Network Request steps** (tablet / hand-built routines) — Master must be green.
2. **Easy Inspection compiled schema** — the routine CodeBlock opens its own Modbus TCP client in Python to `MODBUS_HOST:502`. It does not use Network Request steps. If Master is red for the same IP/port, Python usually fails too (firewall or wrong NIC).

Green Master is still the easiest proof that the robot can reach this PC.

## If Master stays red

| Symptom | Likely cause |
|---------|----------------|
| Self-test fails | Server not started / wrong port |
| Self-test OK, Clients = 0 | Wrong Master IP, firewall, or Master disabled |
| Clients ≥ 1 but robot vars stuck | Field offsets / format mismatch, or schema Modbus host blank |
| Two NICs on similar subnets | Point Master at the NIC on the robot subnet |
