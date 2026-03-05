# Users, Permissions & Remote Access

---

## Package Management

### Ubuntu / Debian (apt)

```bash
sudo apt update                          # refresh package index
sudo apt upgrade                         # upgrade all packages
sudo apt install nginx                   # install package
sudo apt install nginx curl git -y       # install multiple, no prompt
sudo apt remove nginx                    # remove package
sudo apt purge nginx                     # remove + delete config files
sudo apt autoremove                      # remove unused dependencies
sudo apt search nginx                    # search for package
apt show nginx                           # package details
dpkg -l | grep nginx                     # check if installed
dpkg -l                                  # list all installed packages
```

### CentOS / RHEL / Rocky (yum / dnf)

```bash
sudo yum install nginx                   # install
sudo dnf install nginx                   # dnf (modern yum)
sudo yum update                          # update all
sudo yum remove nginx                    # remove
sudo yum search nginx                    # search
sudo yum info nginx                      # package details
rpm -qa | grep nginx                     # check if installed
rpm -qa                                  # list all installed
rpm -qi nginx                            # info on installed package
rpm -ql nginx                            # files installed by package
```

---

## User Management

```bash
sudo useradd username                    # create user (no home dir by default on some distros)
sudo useradd -m username                 # create user with home directory
sudo useradd -m -s /bin/bash username    # with home dir and bash shell
sudo useradd -m -G sudo username         # with sudo group
sudo useradd -u 1500 username            # specify UID

sudo passwd username                     # set or change password

sudo usermod -aG groupname username      # add user to additional group
sudo usermod -g groupname username       # change primary group
sudo usermod -s /bin/zsh username        # change shell
sudo usermod -d /new/home username       # change home directory
sudo usermod -l newname oldname          # rename user
sudo usermod -L username                 # lock account
sudo usermod -U username                 # unlock account

sudo userdel username                    # delete user (keep home dir)
sudo userdel -r username                 # delete user and home directory

# View user info
whoami                                   # current user
who                                      # who is logged in
w                                        # logged in users + what they're doing
id username                              # UID, GID, and all groups
id                                       # your own UID/GID
finger username                          # user info (if installed)
last                                     # login history
lastlog                                  # last login for each user
cat /etc/passwd                          # all user accounts
getent passwd username                   # lookup user entry
```

---

## Group Management

```bash
sudo groupadd groupname                  # create group
sudo groupadd -g 1500 groupname          # with specific GID
sudo groupdel groupname                  # delete group
sudo groupmod -n newname oldname         # rename group
groups username                          # show groups for user
groups                                   # your own groups
cat /etc/group                           # all groups
getent group groupname                   # group info
```

---

## Switching Users

```bash
su username                              # switch to user (keeps environment)
su - username                            # switch with user's full environment
su -                                     # switch to root with root's environment
sudo command                             # run one command as root
sudo -u alice command                    # run as specific user
sudo -i                                  # open root shell (interactive)
sudo -s                                  # root shell but keep your environment
sudo !!                                  # re-run last command as sudo
exit                                     # return to previous user
```

---

## Sudo Access

```bash
sudo visudo                              # safely edit /etc/sudoers
sudo usermod -aG sudo username           # grant sudo on Ubuntu/Debian
sudo usermod -aG wheel username          # grant sudo on CentOS/RHEL

# Check sudo access
sudo -l                                  # list your sudo permissions
sudo -l -U username                      # list another user's sudo permissions
```

In `/etc/sudoers`:
```
alice ALL=(ALL) ALL                      # full sudo access
alice ALL=(ALL) NOPASSWD: ALL            # no password required
alice ALL=(ALL) NOPASSWD: /bin/systemctl # specific command only
%developers ALL=(ALL) ALL               # entire group
```

---

## File Permissions

Permission string format: `-rwxr-xr--`

```
  - rwx r-x r--
  │ │   │   └── Others: read only
  │ │   └────── Group: read + execute
  │ └────────── Owner: read + write + execute
  └──────────── Type: - file, d directory, l symlink
```

| Symbol | Value | Permission |
|--------|-------|-----------|
| `r` | 4 | Read |
| `w` | 2 | Write |
| `x` | 1 | Execute |
| `-` | 0 | None |

Common permission numbers:

| Number | Symbolic | Typical use |
|--------|----------|-------------|
| `755` | rwxr-xr-x | Executable, scripts, directories |
| `644` | rw-r--r-- | Regular files |
| `600` | rw------- | Private keys, sensitive configs |
| `700` | rwx------ | Private directories |
| `777` | rwxrwxrwx | Fully open (avoid in production) |
| `664` | rw-rw-r-- | Group-writable files |

---

## chmod — Change Permissions

```bash
# Numeric mode
chmod 755 script.sh               # rwxr-xr-x
chmod 644 file.txt                # rw-r--r--
chmod 600 ~/.ssh/id_rsa           # rw-------
chmod 400 key.pem                 # r--------  (AWS key files)
chmod -R 755 directory/           # recursive

# Symbolic mode
chmod +x script.sh                # add execute for all
chmod -w file.txt                 # remove write for all
chmod u+x script.sh               # add execute for owner only
chmod g+w file.txt                # add write for group
chmod o-r file.txt                # remove read from others
chmod ug+rw file.txt              # add read+write for user and group
chmod a+x script.sh               # add execute for all (same as +x)
chmod u=rwx,g=rx,o=r file.txt     # set exact permissions symbolically
chmod -R u+X directory/           # add execute only on directories (capital X)
```

---

## chown / chgrp — Change Ownership

```bash
sudo chown alice file.txt                  # change owner
sudo chown alice:developers file.txt       # change owner and group
sudo chown :developers file.txt            # change group only (same as chgrp)
sudo chown -R alice:alice /home/alice/     # recursive
sudo chgrp developers file.txt            # change group only
sudo chgrp -R developers /var/app/        # recursive group change

# Take ownership of current directory tree
sudo chown -R $(whoami):$(whoami) .
```

---

## umask — Default permission mask

```bash
umask                             # show current (usually 022)
umask 027                         # files: 640, dirs: 750
umask 077                         # files: 600, dirs: 700 (very restrictive)
```

New files = 666 − umask. New directories = 777 − umask.
With umask `022`: files get `644`, directories get `755`.

---

## Special Permissions

```bash
# SUID — run as file's owner (common on /usr/bin/passwd)
chmod u+s /path/to/file
chmod 4755 file

# SGID — new files in directory inherit the group
chmod g+s /shared/directory
chmod 2755 directory

# Sticky bit — only file owner can delete (used on /tmp)
chmod +t /tmp
chmod 1777 /tmp

# Find files with special permissions set
find / -perm /4000 2>/dev/null    # find SUID files
find / -perm /2000 2>/dev/null    # find SGID files
find / -perm /1000 2>/dev/null    # find sticky bit directories
```

---

## ACL — Access Control Lists

For fine-grained permissions beyond user/group/others:

```bash
getfacl file.txt                         # view ACL
setfacl -m u:alice:rwx file.txt          # give alice rwx
setfacl -m g:devs:rx directory/          # give devs group rx
setfacl -m o::- file.txt                 # remove all permissions for others
setfacl -x u:alice file.txt              # remove alice's ACL entry
setfacl -b file.txt                      # remove all ACL entries
setfacl -R -m u:alice:rwx directory/     # recursive
```

Install if needed: `sudo apt install acl`

---

## SSH — Remote Access

```bash
ssh user@192.168.1.10                     # basic connection
ssh -p 2222 user@192.168.1.10             # custom port
ssh -i ~/.ssh/mykey.pem user@server       # specific key file
ssh -v user@server                        # verbose (debug connection issues)
ssh -X user@server                        # forward X11 (GUI applications)
ssh -L 8080:localhost:80 user@server      # local port forwarding
ssh -R 9090:localhost:3000 user@server    # remote port forwarding
ssh -N -f -L 5432:db:5432 user@jump       # background tunnel, no command
ssh -J jumphost user@target               # jump through bastion host
ssh user@server 'command to run'          # run command without interactive shell
ssh user@server 'df -h'                   # example: check disk remotely
```

---

## SSH Key Setup

```bash
# Generate key pair (on your local machine)
ssh-keygen                                # RSA, interactive
ssh-keygen -t ed25519 -C "your@email"     # Ed25519 (recommended, stronger)
ssh-keygen -t rsa -b 4096                 # RSA 4096-bit
ssh-keygen -f ~/.ssh/mykey                # specify filename

# Keys are stored in ~/.ssh/
# id_ed25519      — private key (never share, never copy to server)
# id_ed25519.pub  — public key (safe to share)

# Copy public key to server
ssh-copy-id user@server                   # recommended method
ssh-copy-id -i ~/.ssh/mykey.pub user@server

# Manually add key (if ssh-copy-id isn't available)
cat ~/.ssh/id_ed25519.pub | ssh user@server 'mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys'

# Set correct permissions on authorized_keys
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys

# Test passwordless login
ssh user@server
```

---

## SSH Config File

`~/.ssh/config` — define shortcuts for servers you connect to often.

```
Host myserver
    HostName 192.168.1.50
    User alice
    Port 2222
    IdentityFile ~/.ssh/mykey

Host prod
    HostName prod.example.com
    User deploy
    IdentityFile ~/.ssh/prod_key

Host bastion
    HostName bastion.example.com
    User alice

Host internal
    HostName 10.0.1.5
    User alice
    ProxyJump bastion
```

Then just: `ssh myserver` instead of `ssh -p 2222 -i ~/.ssh/mykey alice@192.168.1.50`
