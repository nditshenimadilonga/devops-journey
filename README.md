# 02 — Linux Admin Practice

I am working through the SUSE Linux Enterprise Server Operations (SLE201v15) lab manual, section by section, on my two lab VMs: `ubuntu-01` (Ubuntu Server 24.04) and `suse-01` (SUSE). I covered this material earlier in the year. I am going through it again to prepare for the SUSE Certified Administrator (SCA) exam and to document the process properly.

I follow the manual's order and skip Sections 1 and 2 (course introduction and overview), because there is nothing to practise in them. I aim to do about one section a day and repeat each exercise on both VMs, so I can compare the commands and build recall. Some sections are big and will take two days.

Everything here is written in my own words. The manual's exercise text is not copied.

## Sections

| Section | Topic | Exercises | Status |
|---------|-------|-----------|--------|
| 3 | [The Command Line](./03-command-line) | 11 | Planned |
| 4 | [The Linux File System](./04-linux-file-system) | 2 | Planned |
| 5 | [Text Editors (Vim)](./05-text-editors-vim) | 9 | Planned |
| 6 | [Users and Groups](./06-users-and-groups) | 5 | Planned |
| 7 | [File and Directory Permissions](./07-permissions) | 3 | Planned |
| 8 | [Process Management](./08-process-management) | 4 | Planned |
| 9 | [System and Service Management](./09-system-and-service-management) | 5 | Planned |
| 10 | [Task Scheduling](./10-task-scheduling) | 3 | Planned |
| 11 | [Privilege Delegation](./11-privilege-delegation) | 3 | Planned |
| 12 | [Remote Administration](./12-remote-administration) | 4 | Planned |
| 13 | [Storage Management Fundamentals](./13-storage-fundamentals) | 5 | Planned |
| 14 | [Logical Volume Manager (LVM)](./14-lvm) | 8 | Planned |
| 15 | [Btrfs Management](./15-btrfs) | 7 | Planned |
| 16 | [Network Management Fundamentals](./16-network-fundamentals) | 3 | Planned |
| 17 | [Software Management](./17-software-management) | 4 | Planned |
| 18 | [System Logging](./18-system-logging) | 5 | Planned |

## Which VM each exercise runs on

Most exercises run on both VMs. Some use SUSE-only tools (YaST, `zypper`, Btrfs with Snapper, `supportconfig`), so they run on `suse-01` only. Each section's table shows this in the **Works on** column.

## How I write each exercise up

Each section folder has a README with a checklist table. As I finish an exercise I add an entry in that section's **My notes** area using this template:

```markdown
### Exercise N: <what I practised, in my own words>

**Date:**
**VM:** ubuntu-01 / suse-01

**What I did:**

**Commands:**

    (my commands here)

**What I saw:**

**Ubuntu vs SUSE:** (only if I did both and something differed)

**Problems and fixes:** (if any)

![screenshot](./screenshots/exN-short-name.png)

**What I learned:**
```

Screenshots go in a `screenshots/` folder inside the section folder.
