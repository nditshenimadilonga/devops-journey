# Section 14 — Logical Volume Manager (LVM)

**Status:** Planned
**VMs:** ubuntu-01, suse-01

## What I practise in this section

I practise LVM end to end: physical volumes, volume groups, logical volumes, striping, mirroring, resizing, snapshots and rollback.

## Before I start

I need extra virtual disks added in Proxmox for these exercises. Ubuntu already installs on LVM, which makes a good comparison.

## Exercises

| # | What I practise | Works on | Ubuntu | SUSE | Notes |
|---|-----------------|----------|--------|------|-------|
| 1 | Creating a physical volume, a volume group and a logical volume | Both | ⬜ | ⬜ | |
| 2 | Creating a striped logical volume | Both | ⬜ | ⬜ | |
| 3 | Creating a mirrored logical volume | Both | ⬜ | ⬜ | |
| 4 | Resizing a volume group | Both | ⬜ | ⬜ | |
| 5 | Resizing a logical volume and the file system on it | Both | ⬜ | ⬜ | |
| 6 | Creating and exploring LVM snapshots | Both | ⬜ | ⬜ | |
| 7 | Rolling back a file system with an LVM snapshot | Both | ⬜ | ⬜ | |
| 8 | Configuring LVM with YaST | SUSE only | n/a | ⬜ | |

Change ⬜ to ✅ when an exercise is done on that VM. "n/a" means the exercise only runs on SUSE.

## My notes

Each finished exercise gets an entry here, using the template in the [main README](../README.md).

## Navigation

- Previous: [Section 13: Storage Management Fundamentals](../13-storage-fundamentals)
- Next: [Section 15: Btrfs Management](../15-btrfs)
