# System Monitoring & Process Management

---

## Memory

```bash
free -h                                              # memory and swap usage (human-readable)
free -m                                              # in megabytes
free -s 2                                            # refresh every 2 seconds

cat /proc/meminfo                                    # detailed memory info from kernel

# Memory usage as percentage
free | awk '/Mem:/ {printf "%.1f%%\n", $3/$2*100}'

vmstat                                               # virtual memory stats
vmstat 1 5                                           # 5 samples, 1 second apart
vmstat -s                                            # summary of memory stats
```

---

## CPU

```bash
top                        # live process and CPU monitor (press q to quit)
htop                       # better interactive monitor (install if missing)

# top keyboard shortcuts
# P  sort by CPU
# M  sort by memory
# k  kill process by PID
# r  renice process
# 1  toggle per-core CPU view
# q  quit

lscpu                      # CPU architecture, cores, threads, cache
cat /proc/cpuinfo          # raw CPU info from kernel
nproc                      # number of processing units available
uptime                     # load averages for 1, 5, 15 minutes
cat /proc/loadavg          # same in raw form

# Load average explained: values = average runnable processes
# > number of cores means CPU is overloaded
```

Install htop:
```bash
sudo apt install htop      # Ubuntu
sudo yum install htop      # CentOS
```

---

## Disk & Storage

```bash
df -h                         # disk space per filesystem (human-readable)
df -hT                        # include filesystem type
df -i                         # inode usage instead of block usage
df -h /var/log                # disk space for specific path's filesystem

du -sh foldername/            # total size of a directory
du -sh *                      # size of every item in current directory
du -sh /* 2>/dev/null         # size of top-level directories
du -ah directory/             # size of every file and directory (all)
du --max-depth=1 -h /var/     # one level deep
du -h --threshold=100M /var/  # show only items over 100MB

lsblk                         # list block devices (disks, partitions)
lsblk -f                      # include filesystem type and UUID
blkid                         # UUIDs and filesystem types
sudo fdisk -l                 # list all disk partitions
sudo parted -l                # same, more detail
```

Finding what's eating disk space:
```bash
du -sh /* 2>/dev/null | sort -h | tail -20     # largest directories at root
du -ah /var/ 2>/dev/null | sort -h | tail -20  # largest items in /var
find / -size +100M 2>/dev/null                 # files over 100MB
```

---

## System Information

```bash
uname -a                      # kernel version, hostname, architecture
uname -r                      # just kernel version
uname -m                      # machine hardware (x86_64, aarch64, etc.)

hostnamectl                   # OS name, hostname, virtualization type
cat /etc/os-release           # distro name and version
lsb_release -a                # distribution info (if available)

uptime                        # how long system has been running + load
hostname                      # current hostname
hostname -I                   # all IP addresses

# Hardware info
lscpu                         # CPU details
lsmem                         # memory ranges
lspci                         # PCI devices (graphics, network, etc.)
lsusb                         # USB devices
dmidecode -t memory           # physical RAM sticks (needs sudo)
dmidecode -t system           # system model info

# Virtual environment detection
systemd-detect-virt           # detect if running in VM/container
cat /proc/version             # kernel + compiler info
```

---

## Processes

```bash
ps aux                        # all running processes (BSD style)
ps -ef                        # all processes (UNIX style)
ps aux | grep nginx           # filter by name
ps -u alice                   # processes owned by alice
ps axjf                       # process tree format

pgrep nginx                   # find PID(s) by name
pgrep -l nginx                # PID + process name
pgrep -a nginx                # PID + full command

pidof nginx                   # PID of running process

# Process tree
pstree                        # tree of all processes
pstree -p                     # include PIDs
pstree alice                  # tree for specific user
```

---

## Killing Processes

```bash
kill PID                      # send SIGTERM (graceful shutdown request)
kill -15 PID                  # same as above — SIGTERM
kill -9 PID                   # SIGKILL (force kill, cannot be caught)
kill -1 PID                   # SIGHUP (reload config for many daemons)
kill -2 PID                   # SIGINT (same as Ctrl+C)
kill -STOP PID                # pause process
kill -CONT PID                # resume paused process

killall nginx                 # kill all processes named nginx (by name)
killall -9 nginx              # force kill all
pkill nginx                   # kill by name pattern
pkill -u alice                # kill all processes owned by alice
pkill -f "python script.py"   # match against full command line

# Kill process by port
sudo fuser -k 8080/tcp        # kill whatever is using port 8080
sudo lsof -ti:8080 | xargs kill -9
```

Use SIGTERM first. Only use SIGKILL (-9) if the process doesn't respond, since SIGKILL doesn't allow cleanup.

---

## Background Jobs & Job Control

```bash
command &                     # run in background
./script.sh &

jobs                          # list background jobs
jobs -l                       # with PIDs

fg                            # bring most recent background job to foreground
fg %1                         # bring job 1 to foreground
fg %2                         # bring job 2

bg                            # resume most recent stopped job in background
bg %1                         # resume job 1 in background

Ctrl+Z                        # suspend foreground process (sends to background, stopped)
Ctrl+C                        # terminate foreground process

disown %1                     # detach job from shell (keeps running if you log out)
disown -h %1                  # mark to not receive SIGHUP
nohup ./script.sh &           # run immune to hangup signal (stays after logout)
nohup ./script.sh > output.log 2>&1 &
```

---

## Process Priority (nice)

```bash
nice -n 10 ./cpu-heavy.sh     # start with lower priority (nicer to others)
nice -n -10 ./urgent.sh       # higher priority (requires sudo for negative)
renice 10 -p PID              # change priority of running process
renice -n 5 -u alice          # lower priority for all of alice's processes

# Priority range: -20 (highest) to 19 (lowest), default 0
```

---

## User Sessions

```bash
who                           # currently logged-in users
w                             # logged-in users + what they're doing + load
last                          # login/logout history
last alice                    # history for specific user
lastlog                       # most recent login for each user
lastb                         # failed login attempts (needs sudo)
```

---

## Scheduling Tasks with Cron

```bash
crontab -e                    # edit your cron jobs
crontab -l                    # list your cron jobs
crontab -r                    # remove all your cron jobs
sudo crontab -u alice -l      # list another user's cron jobs
sudo crontab -u alice -e      # edit another user's cron jobs
```

Cron syntax:
```
* * * * * /path/to/command
│ │ │ │ └── day of week (0–7, 0 and 7 = Sunday)
│ │ │ └──── month (1–12)
│ │ └────── day of month (1–31)
│ └──────── hour (0–23)
└────────── minute (0–59)
```

```bash
# Examples
0 2 * * *      /home/user/backup.sh         # 2:00 AM every day
*/10 * * * *   /home/user/check.sh          # every 10 minutes
0 9 * * 1      /home/user/report.sh         # 9:00 AM every Monday
0 0 1 * *      /home/user/monthly.sh        # midnight on 1st of month
@reboot        /home/user/startup.sh        # on system boot
@daily         /home/user/daily.sh          # once per day (midnight)
@weekly        /home/user/weekly.sh         # once per week
```

System-wide cron: edit `/etc/crontab` or drop scripts in `/etc/cron.d/`, `/etc/cron.daily/`, etc.

---

## systemd Timers (modern alternative to cron)

```bash
systemctl list-timers                 # list all active timers
systemctl list-timers --all           # include inactive timers
systemctl status my.timer            # status of a specific timer
```

---

## System Control

```bash
sudo reboot                           # reboot
sudo shutdown -r now                  # reboot immediately
sudo shutdown -r +10                  # reboot in 10 minutes
sudo shutdown now                     # power off immediately
sudo shutdown -h now                  # halt (power off)
sudo poweroff                         # power off
sudo halt                             # halt CPU

sudo shutdown -c                      # cancel scheduled shutdown

# View system logs
journalctl                            # all journal logs
journalctl -b                         # logs since last boot
journalctl -b -1                      # logs from previous boot
journalctl -u nginx                   # logs for specific service
journalctl -f                         # follow live (like tail -f)
journalctl --since "1 hour ago"
journalctl --since "2024-01-01" --until "2024-01-02"
journalctl -p err                     # errors only
journalctl -p warning                 # warnings and above
```

---

## Passwords

```bash
passwd                                # change your own password
sudo passwd username                  # change another user's password
sudo passwd -l username               # lock account (disable password)
sudo passwd -u username               # unlock account
sudo passwd -e username               # expire password (force change on next login)
chage -l username                     # password aging info
sudo chage -M 90 username             # set password to expire in 90 days
```
