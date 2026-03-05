# SSH & Service Management (systemctl)

---

## SSH Overview

SSH (Secure Shell) is an encrypted protocol for remote access and file transfer. It uses asymmetric key cryptography to authenticate and establish a secure channel.

- Default port: **22**
- Server config: `/etc/ssh/sshd_config`
- Client config: `~/.ssh/config`
- Keys: `~/.ssh/`

---

## Install & Start SSH

```bash
# Ubuntu / Debian
sudo apt install openssh-server
sudo systemctl start ssh
sudo systemctl enable ssh

# CentOS / RHEL
sudo yum install openssh-server
sudo systemctl start sshd
sudo systemctl enable sshd

# Check if running
sudo systemctl status sshd
ss -tlnp | grep :22
```

---

## Connect to a Server

```bash
ssh user@192.168.1.10                      # basic
ssh -p 2222 user@192.168.1.10              # custom port
ssh -i ~/.ssh/mykey.pem user@server        # specific private key
ssh -v user@server                         # verbose (debug)
ssh -vvv user@server                       # very verbose
ssh user@server 'uptime'                   # run single command, exit
ssh user@server 'df -h && free -h'         # run multiple commands
```

---

## SSH Key Authentication (Passwordless Login)

```bash
# 1. Generate key pair (on your LOCAL machine)
ssh-keygen -t ed25519 -C "your@email.com"
# or RSA if ed25519 isn't supported:
ssh-keygen -t rsa -b 4096

# Keys saved to ~/.ssh/
# id_ed25519     → private key  (protect this, never share)
# id_ed25519.pub → public key   (this goes to the server)

# 2. Copy public key to server
ssh-copy-id user@server                    # recommended
ssh-copy-id -i ~/.ssh/mykey.pub user@server

# Manually if ssh-copy-id isn't available:
cat ~/.ssh/id_ed25519.pub | ssh user@server \
  'mkdir -p ~/.ssh && chmod 700 ~/.ssh && cat >> ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys'

# 3. Test it
ssh user@server   # should not ask for password

# Key permissions must be correct
chmod 700 ~/.ssh
chmod 600 ~/.ssh/id_ed25519
chmod 644 ~/.ssh/id_ed25519.pub
chmod 600 ~/.ssh/authorized_keys
```

---

## SSH Tunneling & Port Forwarding

```bash
# Local port forwarding: access remote service via local port
# Access remote MySQL (3306) as if it's on localhost:3306
ssh -L 3306:localhost:3306 user@server

# Access a service on an internal network host via a jump server
ssh -L 8080:internal-host:80 user@jumpserver

# Remote port forwarding: expose local service on remote server
ssh -R 9000:localhost:3000 user@server

# SOCKS proxy (dynamic port forwarding)
ssh -D 1080 user@server                    # configure browser to use SOCKS proxy at localhost:1080

# Background tunnel (no command, just the tunnel)
ssh -N -f -L 5432:localhost:5432 user@server

# Jump through bastion/jump host
ssh -J user@bastion user@internal-server
ssh -J bastion1,bastion2 user@target       # multiple hops
```

---

## SSH Agent

```bash
eval $(ssh-agent)                          # start agent
ssh-add ~/.ssh/id_ed25519                  # add key to agent
ssh-add -l                                 # list loaded keys
ssh-add -d ~/.ssh/id_ed25519              # remove key from agent
ssh-add -D                                 # remove all keys

# Agent forwarding (use your local keys on the remote server)
ssh -A user@server
# Or in ~/.ssh/config:
# ForwardAgent yes
```

---

## SSH Config File (~/.ssh/config)

```
Host prod
    HostName prod.example.com
    User deploy
    IdentityFile ~/.ssh/prod_key
    Port 22

Host staging
    HostName staging.example.com
    User ubuntu
    IdentityFile ~/.ssh/staging_key

Host bastion
    HostName bastion.example.com
    User alice
    ForwardAgent yes

Host internal
    HostName 10.0.1.5
    User alice
    ProxyJump bastion

# Apply to all hosts
Host *
    ServerAliveInterval 60
    ServerAliveCountMax 3
    AddKeysToAgent yes
```

Usage: `ssh prod` instead of `ssh -i ~/.ssh/prod_key deploy@prod.example.com`

---

## Server-Side SSH Config (/etc/ssh/sshd_config)

Common settings to harden SSH:

```
Port 2222                          # change default port
PermitRootLogin no                 # never allow direct root login
PasswordAuthentication no          # keys only (after you've set up keys)
PubkeyAuthentication yes
AuthorizedKeysFile .ssh/authorized_keys
AllowUsers alice bob               # whitelist users
DenyUsers baduser
MaxAuthTries 3
ClientAliveInterval 300
ClientAliveCountMax 2
X11Forwarding no
UsePAM yes
```

After editing:
```bash
sudo sshd -t                       # test config for syntax errors
sudo systemctl restart sshd
```

---

## systemctl — Service Management

`systemctl` is the command to manage services (daemons) on systemd-based Linux systems (virtually all modern distros).

```bash
# Basic service control
sudo systemctl start nginx         # start
sudo systemctl stop nginx          # stop
sudo systemctl restart nginx       # stop then start
sudo systemctl reload nginx        # reload config without downtime (if supported)
sudo systemctl status nginx        # check status and recent logs

# Boot behavior
sudo systemctl enable nginx        # start on boot
sudo systemctl disable nginx       # don't start on boot
sudo systemctl enable --now nginx  # enable and start immediately
sudo systemctl disable --now nginx # disable and stop immediately

# Prevent service from running at all
sudo systemctl mask nginx          # mask (blocks manual start too)
sudo systemctl unmask nginx        # undo mask

# Check state
systemctl is-active nginx          # running?
systemctl is-enabled nginx         # enabled on boot?
systemctl is-failed nginx          # did it fail?

# Reload daemon config (after editing unit files)
sudo systemctl daemon-reload
```

---

## Listing and Inspecting Services

```bash
systemctl list-units --type=service                    # all service units
systemctl list-units --type=service --state=running    # only running
systemctl list-units --type=service --state=failed     # only failed
systemctl list-unit-files --type=service               # all service files with state
systemctl list-units --all                             # all unit types

systemctl cat nginx                                    # show the unit file
systemctl show nginx                                   # all properties
systemctl show nginx --property=MainPID                # single property

# Dependencies
systemctl list-dependencies nginx                      # what nginx needs
systemctl list-dependencies --reverse nginx            # what depends on nginx
```

---

## Viewing Service Logs

```bash
journalctl -u nginx                        # all logs for nginx
journalctl -u nginx -f                     # follow live
journalctl -u nginx -n 50                  # last 50 lines
journalctl -u nginx --since "1 hour ago"
journalctl -u nginx -p err                 # errors only
journalctl -u nginx -b                     # since last boot
journalctl -u nginx -b -1                  # from previous boot
journalctl --disk-usage                    # how much space logs are using
sudo journalctl --vacuum-size=500M         # reduce journal to 500MB
sudo journalctl --vacuum-time=7d           # delete logs older than 7 days
```

---

## System Targets (Runlevels)

```bash
systemctl get-default                      # current default target
sudo systemctl set-default multi-user.target   # boot to CLI (no GUI)
sudo systemctl set-default graphical.target    # boot to GUI
sudo systemctl isolate rescue.target           # switch to single-user mode now
```

| Target | Old Runlevel | Description |
|--------|-------------|-------------|
| `poweroff` | 0 | Shutdown |
| `rescue` | 1 | Single user mode |
| `multi-user` | 3 | Multi-user, no GUI |
| `graphical` | 5 | Multi-user with GUI |
| `reboot` | 6 | Reboot |

---

## Power Commands

```bash
sudo systemctl poweroff              # shutdown
sudo systemctl reboot                # reboot
sudo systemctl suspend               # suspend to RAM
sudo systemctl hibernate             # hibernate to disk
sudo systemctl hybrid-sleep          # suspend + hibernate
sudo shutdown now                    # poweroff immediately
sudo shutdown -r now                 # reboot immediately
sudo shutdown -h +10                 # poweroff in 10 minutes
sudo shutdown -r +5 "Rebooting soon" # with broadcast message
sudo shutdown -c                     # cancel pending shutdown
```

---

## Creating a Custom systemd Service

Example: run a Python app as a service.

Create `/etc/systemd/system/myapp.service`:
```ini
[Unit]
Description=My Python Application
After=network.target

[Service]
Type=simple
User=alice
WorkingDirectory=/home/alice/myapp
ExecStart=/usr/bin/python3 app.py
Restart=on-failure
RestartSec=5
StandardOutput=journal
StandardError=journal

[Install]
WantedBy=multi-user.target
```

```bash
sudo systemctl daemon-reload
sudo systemctl enable --now myapp
sudo systemctl status myapp
journalctl -u myapp -f
```
