# Introduction to Linux

Linux is an open-source operating system kernel — the core software that manages communication between hardware and programs. It's the foundation of virtually every server, cloud platform, and container runtime in use today.

You'll encounter Linux in AWS EC2 instances, Docker containers, CI/CD pipelines, Kubernetes nodes, and almost every backend system. Learning it early saves a lot of pain later.

---

## What Linux Actually Is

Linux is just the **kernel** — not a complete OS on its own. It gets bundled with tools, a shell, libraries, and a package manager to form a **distribution** (distro).

What the kernel manages:

| Resource | What it does |
|----------|-------------|
| CPU | Schedules and runs processes |
| Memory | Allocates and protects RAM |
| Storage | Reads/writes files through filesystems |
| Devices | Talks to hardware via drivers |
| Network | Manages network interfaces and routing |
| Users | Enforces permissions and isolation |

---

## Linux vs Unix

Linux was written from scratch in 1991 by Linus Torvalds, inspired by Unix but not derived from it.

| | Unix | Linux |
|-|------|-------|
| Source | Proprietary (mostly) | Open source |
| Origin | AT&T Bell Labs, 1970s | Linus Torvalds, 1991 |
| Cost | Expensive licenses | Free |
| Examples | Solaris, AIX, HP-UX | Ubuntu, Debian, RHEL |
| Used in | Legacy enterprise | Modern cloud and servers |

macOS is Unix-based (BSD lineage). Linux is Unix-like but independent.

---

## Distributions

A distro = Linux kernel + package manager + default tools + release cycle.

| Distro | Used for |
|--------|---------|
| Ubuntu | Cloud servers, beginner-friendly, large ecosystem |
| Debian | Stability-first, base for many other distros |
| RHEL / Rocky / AlmaLinux | Enterprise servers, long-term support |
| Fedora | Cutting-edge features, Red Hat upstream |
| Kali Linux | Penetration testing and security research |
| Alpine | Minimal footprint, popular in Docker images |
| Arch Linux | Rolling release, manual setup, advanced users |

Ubuntu and RHEL-family are the two you'll see most in DevOps and cloud work.

---

## The Shell

The shell is the program that reads your commands and runs them. Most Linux systems default to **Bash** (Bourne Again Shell).

Other shells:

| Shell | Notes |
|-------|-------|
| `bash` | Default on most distros |
| `zsh` | Popular for local dev (macOS default since 2019) |
| `sh` | POSIX-compliant, minimal, used in scripts |
| `fish` | Friendly interactive shell, not POSIX |
| `dash` | Fast, often used as `/bin/sh` on Ubuntu |

Your current shell:
```bash
echo $SHELL
```

---

## The Filesystem

Linux uses a single root `/` tree — no drive letters like Windows.

| Path | Contents |
|------|---------|
| `/` | Root of everything |
| `/home/` | User home directories |
| `/root/` | Root user's home |
| `/etc/` | System-wide config files |
| `/var/` | Logs, databases, variable data |
| `/tmp/` | Temporary files, cleared on reboot |
| `/usr/` | Installed programs and libraries |
| `/bin/`, `/sbin/` | Essential binaries (symlinked to `/usr/bin` on modern distros) |
| `/lib/` | Shared libraries |
| `/dev/` | Device files (disks, terminals, etc.) |
| `/proc/` | Virtual filesystem — live kernel/process info |
| `/sys/` | Virtual filesystem — hardware and kernel state |
| `/mnt/`, `/media/` | Mount points for drives |
| `/opt/` | Optional/third-party software |
| `/boot/` | Kernel and bootloader files |

---

## Key Concepts

**Everything is a file** — devices, sockets, pipes, and processes all appear as files somewhere under `/`.

**Case sensitive** — `File.txt` and `file.txt` are different files.

**Hidden files** start with a dot: `.bashrc`, `.ssh/`

**No file extensions required** — Linux doesn't need `.exe` or `.bat`. Executable permission determines runnability.

**Root user** (`uid=0`) has unrestricted access to everything. Use `sudo` for individual privileged commands instead of logging in as root.

---

## Why Linux for DevOps

- Containers (Docker) run Linux namespaces and cgroups
- Kubernetes nodes are Linux
- Most cloud instances are Linux
- CI/CD runners are Linux
- Configuration management tools (Ansible, Chef, Puppet) primarily target Linux
- The tooling ecosystem (bash, grep, awk, sed, curl) is unmatched for automation

The sooner you get comfortable at the command line, the easier everything else becomes.
