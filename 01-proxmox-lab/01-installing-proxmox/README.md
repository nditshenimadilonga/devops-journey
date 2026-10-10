# 1.1 Installing Proxmox

**Started:** 10 October 2026
**Status:** In progress

## Goal

Turn a dedicated PC into a virtualization host so I can build and break Linux servers safely.

## Lab host

| Item | Value |
|------|-------|
| Hypervisor | Proxmox VE 9.2.2 |
| CPU | AMD Ryzen 9 3900X (12 cores / 24 threads) |
| RAM | ~28 GB |
| Storage | ~500 GB NVMe SSD (whole disk given to Proxmox) |
| Network | Wired Ethernet to my router |
| Management | Web UI from my laptop at `https://<host-ip>:8006` |

## Steps

<!-- Fill in from what you actually did. Suggested headings: -->

1. Downloaded the Proxmox VE ISO
2. Wrote it to a USB drive (tool used: ___)
3. Booted the PC from the USB and ran the installer (disk, country/timezone, password, network)
4. Rebooted and logged in to the web UI from my laptop

## Screenshot

![Proxmox dashboard](screenshots/proxmox-dashboard.png)
*Proxmox web UI showing the node.*

## What I learned

<!-- Your own words. -->

---
Next: [1.2 Building the Ubuntu VM](../02-building-ubuntu-vm/README.md)
