<h1 align="center">🐧 Linux Engine</h1>

<p align="center">
  <img src="https://img.shields.io/badge/Linux-Learning_Path-FCC624?style=for-the-badge&logo=linux&logoColor=black"/>
  <img src="https://img.shields.io/badge/Days-13_Covered-blue?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Level-Beginner_→_Intermediate-orange?style=for-the-badge"/>
</p>

<p align="center">
  Linux notes organized by topic — covering everything from the basics to shell scripting, built for DevOps and cloud work.
</p>

---

## 📁 Structure

Content is grouped by topic — so it's easy to find exactly what you need without hunting through numbered folders.

```
linux-engine/
│
├── 01-Basics/
│   ├── introduction-to-linux.md
│   └── virtual-machines-hypervisors.md
│
├── 02-Navigation-and-Files/
│   ├── linux-navigation-commands.md
│   ├── file-and-directory-management.md
│   └── file-copy-move-sort.md
│
├── 03-System-Utilities/
│   ├── search-compare-utilities.md
│   └── archives-downloads-text-processing.md
│
├── 04-Users-and-Permissions/
│   └── users-permissions-ssh.md
│
├── 05-System-Administration/
│   ├── system-monitoring-processes.md
│   └── file-transfer-windows-linux.md
│
├── 06-Networking/
│   ├── ssh-server-management-systemctl.md
│   └── linux-networking-commands.md
│
├── 07-Scripting/
│   └── shell-scripting-basics.md
│
└── README.md
```

---

## 📋 Course Index

### 🟦 Module 1 — Basics

| Topic | What's Covered |
|-------|----------------|
| [Introduction to Linux](./01-Basics/Day-01-introduction-to-linux.md) | Linux kernel, distributions (Ubuntu, Debian, RHEL, Kali), OS responsibilities (CPU/RAM/Storage/Users), Linux vs Unix, why Linux runs the internet and cloud |
| [Virtual Machines & Hypervisors](./01-Basics/Day-02-virtual-machines-hypervisors.md) | What a VM is, how a hypervisor allocates CPU/RAM/Disk to VMs, Type 1 (ESXi, Hyper-V, Xen) vs Type 2 (VirtualBox, VMware Workstation), tools to connect: PuTTY, MobaXterm, WinSCP, SSH |

---

### 🟩 Module 2 — Navigation & Files

| Topic | What's Covered |
|-------|----------------|
| [Linux Navigation](./02-Navigation-and-Files/Day-03-linux-navigation-commands.md) | `pwd`, `ls` with all flags (`-l`, `-a`, `-la`, `-lh`, `-lt`, `-R`), `cd` (absolute, relative, `~`, `/`, `-`) |
| [File & Directory Management](./02-Navigation-and-Files/Day-04-file-and-directory-management.md) | `cat`, `less`, `more`, `head`, `tail`, `tail -f`, `touch`, `echo`, `mkdir -p`, `rm -rf`, `cp`, `mv`, editing with `nano` / `vi` / `vim` |
| [Copy, Move & Sort](./02-Navigation-and-Files/Day-05-file-copy-move-sort.md) | `cp` (single, multiple, folder, from parent), `mv` (move + rename), `sort` (alpha, numeric, reverse), `uniq`, piping `sort \| uniq -c`, absolute vs relative paths |

---

### 🟨 Module 3 — System Utilities

| Topic | What's Covered |
|-------|----------------|
| [Search, Compare & Utilities](./03-System-Utilities/Day-06-search-compare-utilities.md) | `grep` (`-i`, `-n`, `-c`, `-r`), wildcards (`*`, `?`, `[]`), `wc -l`, `diff`, `cmp`, `find` (by name, type, extension), `locate`, `which`, `whereis`, `history`, `man`, `cal`, `script` |
| [Archives, Downloads & Text Processing](./03-System-Utilities/Day-07-archives-downloads-text-processing.md) | `zip`/`unzip`, `gzip`/`gunzip`, `tar` (`-cf`, `-xf`, `-czf`, `-xzf`), `wget`, `curl` (GET, POST, headers), `export` env vars, `~/.bashrc`, `cut`, `tr`, `sed -n`, `fold`, `column`, `alias` |

---

### 🟥 Module 4 — Users & Permissions

| Topic | What's Covered |
|-------|----------------|
| [Users, Permissions & Remote Access](./04-Users-and-Permissions/Day-08-users-permissions-ssh.md) | `apt`/`yum`/`dnf` package install, `useradd`, `passwd`, `userdel`, `usermod`, `whoami`, `who`, `su`, `sudo`, `visudo`, SSH connect + key-based login (`ssh-keygen`, `ssh-copy-id`), `scp` (file + folder), `chmod` (symbolic + numeric: 755, 644), `chown`, `chgrp`, `umask`, SUID/SGID/sticky bit |

---

### 🟧 Module 5 — System Administration

| Topic | What's Covered |
|-------|----------------|
| [System Monitoring & Processes](./05-System-Administration/Day-09-system-monitoring-processes.md) | `free -h`, `top`, `htop`, `df -h`, `du -sh`, `uname -a`, `lscpu`, `lsblk`, `cat /etc/os-release`, `ps aux`, `pidof`, `kill -9`, `systemctl` (start/stop/restart), background jobs (`&`, `jobs`, `fg`, `bg`), `reboot`, `shutdown`, `crontab -e`, user & group management (`groupadd`, `groupdel`, `usermod`, `id`) |
| [File Transfer Windows ↔ Linux](./05-System-Administration/Day-10-file-transfer-windows-linux.md) | WinSCP setup (SFTP, port 22), drag-drop transfer, `scp` (local→remote, remote→local, remote→remote), `scp -i` with key, `scp -p` preserve permissions, `scp -C` compression, `sftp` interactive session (`put`, `get`), `rsync -avz`, common errors and fixes |

---

### 🟪 Module 6 — Networking

| Topic | What's Covered |
|-------|----------------|
| [SSH & Server Management](./06-Networking/Day-11-ssh-server-management-systemctl.md) | SSH protocol, default port 22, `/etc/ssh/sshd_config`, `rpm -qa \| grep ssh`, install openssh, `systemctl` full service lifecycle (start/stop/restart/enable/disable/mask/unmask/is-enabled), `systemctl list-sockets`, `poweroff`, `reboot -i`, passwordless SSH (keygen → copy-id → login) |
| [Linux Networking Commands](./06-Networking/Day-12-linux-networking-commands.md) | `ping` (flags: `-c`, `-i`, `-s`, `-t`), `traceroute` (flags: `-n`, `-I`, `-T`, `-p`, `-m`), `netstat` vs `ss` (`-tuln`, `-tulnp`, `-s`), `ip a` / `ip route` / `ip neigh` / `ip link set`, DNS tools (`nslookup`, `dig`, `host`), `curl` (GET/POST/headers), `wget`, `lsof -i`, `nc`, `tcpdump`, `mtr`, firewall (`ufw`, `firewall-cmd`), real-world troubleshoot flow |

---

### 🔶 Module 7 — Scripting

| Topic | What's Covered |
|-------|----------------|
| [Shell Scripting](./07-Scripting/Day-13-shell-scripting-basics.md) | Shebang (`#!/bin/bash`), variables, `read`, special vars (`$0`, `$1`, `$#`, `$?`), arithmetic (`$(( ))`), `if`/`elif`/`else`, `for`/`while`/`until` loops, `case`, functions, file tests (`-f`, `-d`, `-r`, `-x`), string ops, command substitution `$()`, output redirection, `bash -x` debugging, cron scheduling |

---

## 📊 Progress Tracker

| # | Topic | Status |
|---|-------|--------|
| 1 | Introduction to Linux | ✅ |
| 2 | Virtual Machines & Hypervisors | ✅ |
| 3 | Linux Navigation Commands | ✅ |
| 4 | File & Directory Management | ✅ |
| 5 | Copy, Move & Sort | ✅ |
| 6 | Search, Compare & Utilities | ✅ |
| 7 | Archives, Downloads & Text Processing | ✅ |
| 8 | Users, Permissions & Remote Access | ✅ |
| 9 | System Monitoring & Processes | ✅ |
| 10 | File Transfer Windows ↔ Linux | ✅ |
| 11 | SSH, Server Management & systemctl | ✅ |
| 12 | Linux Networking Commands | ✅ |
| 13 | Shell Scripting Complete Guide | ✅ |

---

## 🛠️ How to Use This Repo

Clone it and open any `.md` file directly — each file is self-contained with commands, examples, and explanations.

```bash
git clone https://github.com/Shubhamx18/linux-engine.git
cd linux-engine
```

Each topic builds on the previous one, so going in order is recommended for beginners.  
If you already know the basics, jump directly to any module using the index above.

---

## ⚙️ Environment

All commands are tested on:

- Ubuntu 22.04 / 24.04 LTS
- CentOS / RHEL 8+
- Works on any Debian or RPM-based distro

---

<p align="center">
  If this repo helped you — drop a ⭐
</p>
