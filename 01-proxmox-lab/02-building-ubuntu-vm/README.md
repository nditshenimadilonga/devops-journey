# 1.2 Building the Ubuntu VM (`ubuntu-01`)

**Status:** Done

## VM summary

| VM ID | Name | OS | CPU | RAM | Disk |
|-------|------|----|-----|-----|------|
| 100 | ubuntu-01 | Ubuntu Server 24.04.4 LTS | 2 cores | 4 GB | 40 GB |

## Step 1: Get the Ubuntu ISO onto Proxmox

In the web UI: **pve → local (pve) → ISO Images → Download from URL**.

1. Pasted the direct link to `ubuntu-24.04.4-live-server-amd64.iso` from releases.ubuntu.com.
2. Clicked **Query URL**. It reported 3.17 GiB and type `application/x-iso9660-image`, which confirms it is the real ISO.
3. Clicked **Download** and waited for `TASK OK`.

## Step 2: Create the VM

| Tab | Setting |
|-----|---------|
| General | Name `ubuntu-01`, VM ID 100 |
| OS | ISO image: Ubuntu 24.04.4 live server, type Linux |
| System | Defaults, Qemu Agent enabled |
| Disks | scsi0, 40 GiB on local-lvm, VirtIO SCSI single, IO thread on |
| CPU | 1 socket, 2 cores, type x86-64-v2-AES |
| Memory | 4096 MiB |
| Network | Bridge `vmbr0`, VirtIO model |
| Confirm | Start after created |



## Step 3: Install Ubuntu Server (Proxmox console)

The installer is text-based: arrow keys, Tab, Space, Enter.

| Screen | Choice |
|--------|--------|
| Language / keyboard | English / default |
| Install type | Ubuntu Server |
| Network | DHCP (address from my router) |
| Proxy / mirror | none / default |
| Storage | Entire disk with LVM, no encryption |
| Profile | Server name `ubuntu-01`, created my user and password |
| Ubuntu Pro | Skipped |
| SSH | Install OpenSSH server ticked, password authentication allowed |
| Featured snaps | None |

**Resulting layout:**

- `/boot` 2 GB (ext4)
- `/` ~19 GB on an LVM logical volume
- Volume group `ubuntu-vg` ~38 GB, leaving ~19 GB free for LVM practice later

![Storage summary](screenshots/storage-summary.png)
<img width="1899" height="817" alt="{E78164A9-5F9D-4DB1-8AAD-ECA9012C80B9}" src="https://github.com/user-attachments/assets/317be03f-9967-4229-bccb-e5fa6398acfb" />


## Step 4: First boot

1. Detached the ISO: **Hardware → CD/DVD Drive → Do not use any media**.
2. The installer hung on reboot (see Problems below), so I stopped and started the VM from Proxmox.
3. Logged in at the console and found the IP address:

```bash
ip -br a
```

Output showed `ens18 UP 192.168.0.160/24`.

## Step 5: Connect over SSH from my laptop

```bash
ssh <username>@192.168.0.160
```

Accepted the host key on first connection, then logged in with my password. From here on, all practice is done over SSH.

## Step 6: Verify the system

```bash
whoami
hostname
cat /etc/os-release
ip -br a
```

Confirmed the user, hostname `ubuntu-01`, Ubuntu 24.04.4 LTS, and the IP address.

![SSH verify](screenshots/ssh-verify.png)
<img width="1507" height="812" alt="image" src="https://github.com/user-attachments/assets/5dc14198-59e4-4eb9-acc4-331e8f1e6f05" />


## Step 7: Update the system

```bash
sudo apt update
sudo apt upgrade
```

Both ran successfully, which also confirms the VM has working internet through the bridge.

## Problems I ran into

| Problem | Cause | Fix |
|---------|-------|-----|
| `Parameter verification failed (400): url does not match the regex pattern` | URL was missing `https://` and was not a direct link to the file | Copied the link address of the `.iso` itself, starting with `https://` |
| Query URL returned a 246 KiB file of type `application/x-bittorrent` | I copied the `.torrent` link instead of the `.iso` | Copied the link ending exactly in `.iso`. Query URL then showed 3.17 GiB |
| Installer hung on reboot with `Failed unmounting /cdrom` | ISO was detached while the installer was still running from it | Stopped the VM from Proxmox and started it again. It booted from its own disk |

## What I learned

Setting up a VM turned out to be easier than I expected. Proxmox is simple to navigate, and each part of the build went smoothly: assigning the RAM, adding the disk, setting up LVM and installing the OpenSSH server. Connecting the lab box to the network over Ethernet was easy too.

The main thing I took away is that installing a VM isn't hard once you know what you're doing. The step that matters most is picking the right OS image. For a first attempt, it went well.

---
Previous: [1.1 Installing Proxmox](../01-installing-proxmox/README.md)
