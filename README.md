# devops-journey
Documenting my hands-on journey from Linux administration into DevOps — Proxmox, automation, containers, and CI/CD.

02 — Proxmox Virtualization

Status: In progress Started: 10 October 2026

Overview

I run a home lab on a dedicated PC using Proxmox VE as the hypervisor. This folder documents how the lab is built, one VM at a time, with the exact steps, settings and problems I ran into.

Lab host

Item	Value
Hypervisor	Proxmox VE 9.2.2
CPU	AMD Ryzen 9 3900X (12 cores / 24 threads)
RAM	~28 GB
Storage	~500 GB NVMe SSD (whole disk given to Proxmox)
Management	Web UI from my laptop at https://<host-ip>:8006
VMs
VM ID	Name	OS	CPU	RAM	Disk	Status
100	ubuntu-01	Ubuntu Server 24.04.4 LTS	2 cores	4 GB	40 GB	Running
101	(SUSE VM)	SUSE Linux Enterprise / openSUSE	2 cores	4 GB	40 GB	Planned
VM 100: ubuntu-01 — step by step
Step 1: Get the Ubuntu ISO onto Proxmox
In the Proxmox web UI: pve → local (pve) → ISO Images → Download from URL.
Pasted the direct link to ubuntu-24.04.4-live-server-amd64.iso from releases.ubuntu.com.
Clicked Query URL to check it. It reported 3.17 GiB and the type application/x-iso9660-image, which confirms it is the real ISO.
Clicked Download and waited for "TASK OK".
Step 2: Create the VM

Clicked Create VM and used these settings:

Tab	Setting
General	Name ubuntu-01, VM ID 100
OS	ISO image: Ubuntu 24.04.4 live server, type Linux (7.x / 2.6 kernel)
System	Defaults, Qemu Agent enabled
Disks	scsi0, 40 GiB on local-lvm, VirtIO SCSI single, IO thread on
CPU	1 socket, 2 cores, type x86-64-v2-AES
Memory	4096 MiB
Network	Bridge vmbr0, VirtIO model
Confirm	Start after created
Step 3: Install Ubuntu Server (via the Proxmox console)

The installer is text-based, so everything is done with the keyboard (arrow keys, Tab, Space, Enter).

Language: English. Keyboard: default.
Install type: Ubuntu Server.
Network: DHCP (picked up an address from my router).
Proxy: none. Mirror: default.
Storage: Use an entire disk with LVM (no encryption). Result:
/boot 2 GB (ext4)
/ ~19 GB on an LVM logical volume
Volume group ubuntu-vg ~38 GB, leaving ~19 GB free for LVM practice later
Profile: set server name ubuntu-01, created my user and password.
Ubuntu Pro: skipped.
SSH: Install OpenSSH server ticked, password authentication allowed.
Featured snaps: none.
Step 4: First boot
After the install finished, detached the ISO: Hardware → CD/DVD Drive → Do not use any media.
The installer hung on reboot (see "Problems" below), so I stopped and started the VM from Proxmox.
Logged in at the console and found the VM's IP address:
bash
ip -br a

Output showed ens18  UP  192.168.0.160/24.

Step 5: Connect over SSH from my laptop
bash
ssh <username>@192.168.0.160

Accepted the host key on first connection, then logged in with my password. From here on, all practice is done over SSH in a normal terminal.

Step 6: Verify the system
bash
whoami
hostname
cat /etc/os-release
ip -br a

Confirmed the user, hostname ubuntu-01, Ubuntu 24.04.4 LTS, and the IP address.

Step 7: Update the system
bash
sudo apt update
sudo apt upgrade

Both ran successfully, which also confirms the VM has working internet access through the bridge.

Problems I ran into
Problem	Cause	Fix
"Parameter verification failed (400): url does not match the regex pattern" when downloading the ISO	The URL was missing https:// and was not a direct link to the file	Copied the link address of the .iso file itself, with https:// at the start
Query URL returned a 246 KiB file of type application/x-bittorrent	I copied the .torrent file link instead of the .iso	Copied the link for the file ending exactly in .iso. Query URL then showed 3.17 GiB
Installer hung on reboot with "Failed unmounting /cdrom"	The installer ISO was detached while the installer was still running from it	Stopped the VM from Proxmox and started it again. It booted from its own disk normally
Screenshots

Add these to a screenshots/ folder in this directory and link them here:

<img width="1507" height="812" alt="image" src="https://github.com/user-attachments/assets/b57399a2-19d6-422b-9f94-3a3029711d40" />

<img width="971" height="510" alt="image" src="https://github.com/user-attachments/assets/6c329db7-bce4-4ae2-88a3-c736a6cafa93" />


proxmox-dashboard.png: Proxmox web UI showing the node
create-vm-confirm.png: the Confirm tab of the Create VM wizard
storage-summary.png: the Ubuntu installer storage summary (LVM layout)
ssh-verify.png: terminal showing whoami, hostname, os-release and ip -br a
What I learned

Setting up a VM turned out to be easier than I expected. Proxmox is simple to navigate, and each part of the build went smoothly: assigning the RAM, adding the disk, setting up LVM and installing the OpenSSH server. Connecting the lab box to the network over Ethernet was easy too.

The main thing I took away is that installing a VM isn't hard once you know what you're doing. The step that matters most is picking the right OS image. For a first attempt, it went well.
