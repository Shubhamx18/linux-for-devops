# Linux Navigation Commands

---

## pwd — Where you are

```bash
pwd
# /home/user/projects
```

---

## ls — List directory contents

```bash
ls                    # basic list
ls -l                 # long format (permissions, owner, size, date)
ls -a                 # include hidden files (dotfiles)
ls -la                # long + hidden
ls -lh                # long with human-readable sizes (KB, MB, GB)
ls -lt                # sort by modification time, newest first
ls -ltr               # sort by modification time, oldest first
ls -lS                # sort by file size, largest first
ls -R                 # recursive — list all subdirectories too
ls -d */              # list only directories
ls -1                 # one file per line
ls -i                 # show inode numbers
ls --color=auto       # colorize output (usually on by default)
```

Reading `ls -l` output:
```
-rw-r--r-- 1 alice developers 4096 Mar 10 14:22 notes.txt
drwxr-xr-x 3 alice developers 4096 Mar 08 09:00 projects/
```

| Field | Meaning |
|-------|---------|
| `-rw-r--r--` | File type + permissions (user/group/others) |
| `1` | Hard link count |
| `alice` | Owner |
| `developers` | Group |
| `4096` | Size in bytes |
| `Mar 10 14:22` | Last modified |
| `notes.txt` | Name |

First character of permissions: `-` = file, `d` = directory, `l` = symlink, `b` = block device, `c` = character device.

---

## cd — Change directory

```bash
cd Documents              # relative path (from current location)
cd /home/user/Documents   # absolute path (from root)
cd ..                     # up one level
cd ../..                  # up two levels
cd ~                      # home directory
cd                        # also goes home
cd -                      # previous directory (toggle back and forth)
cd /                      # root directory
cd /var/log               # jump anywhere with absolute path
```

---

## Absolute vs Relative Paths

| Type | Starts from | Example |
|------|-------------|---------|
| Absolute | Root `/` | `/home/user/docs/file.txt` |
| Relative | Current directory | `docs/file.txt` or `../sibling/` |

Special path symbols:

| Symbol | Means |
|--------|-------|
| `.` | Current directory |
| `..` | Parent directory |
| `~` | Home directory |
| `-` | Previous directory (in `cd`) |
| `/` | Root directory |

---

## tree — Visual directory structure

```bash
tree                      # tree from current directory
tree /etc                 # tree from a specific path
tree -L 2                 # limit depth to 2 levels
tree -a                   # include hidden files
tree -d                   # directories only
tree -f                   # show full paths
tree --du -h              # show disk usage per item
```

Install if missing:
```bash
sudo apt install tree       # Ubuntu/Debian
sudo yum install tree       # CentOS/RHEL
```

---

## stat — Detailed file info

```bash
stat file.txt
stat /etc/passwd
```

Shows: size, permissions, inode, block count, access/modify/change times.

---

## file — Identify file type

```bash
file image.png
file script.sh
file /bin/bash
```

Tells you what a file actually is (JPEG, ELF binary, ASCII text, etc.) regardless of extension.

---

## Useful Navigation Tricks

```bash
# Show full path of a command
which python3
which nginx

# Show all locations of a command
type -a python3

# Push/pop directory stack
pushd /var/log        # go there and remember current location
popd                  # return to where you were
dirs                  # show directory stack
```
