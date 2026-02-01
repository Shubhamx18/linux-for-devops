<h1 align="center">🖥️ Day 9 – System Monitoring, Processes & User Management</h1>

<p align="center">
  <img src="https://img.shields.io/badge/Linux-System_Monitoring-FCC624?style=for-the-badge&logo=linux&logoColor=black"/>
  <img src="https://img.shields.io/badge/Day-9-Admin_Tools-success?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Level-Intermediate-blue?style=for-the-badge"/>
</p>

<p align="center">
  Learn system resource monitoring, process control, system info commands, and user/group management.
</p>

---

# 🧠 MEMORY INFORMATION

```bash
free -h
```

Memory usage in percentage:
```bash
free | awk '/Mem:/ {print $3/$2 * 100.0 "%"}'
```

---

# ⚙️ CPU UTILIZATION

```bash
top
```

Better view:
```bash
htop
```

---

# 💽 FILESYSTEM & DISK SPACE

Check disk space:
```bash
df -h
```

Check folder size:
```bash
du -sh foldername
```

---

# 🖥️ SYSTEM INFORMATION

```bash
uname -a        # Kernel info
hostnamectl     # OS & architecture
lscpu           # CPU cores & threads
lsblk           # Storage devices
fdisk -l        # Disk partitions
```

Check OS name:
```bash
cat /etc/os-release
```

---

# 🔄 PROCESS MANAGEMENT

List processes:
```bash
ps aux
```

Find process ID (PID):
```bash
pidof nginx
```

Kill process:
```bash
kill PID
kill -9 PID
```

Start service:
```bash
sudo systemctl start nginx
```

Stop service:
```bash
sudo systemctl stop nginx
```

Restart service:
```bash
sudo systemctl restart nginx
```

---

# 🧵 JOB CONTROL (FOREGROUND/BACKGROUND)

Run script in background:
```bash
./script.sh &
```

List jobs:
```bash
jobs
```

Bring job to foreground:
```bash
fg %1
```

Resume job in background:
```bash
bg %1
```

---

# 🔁 SYSTEM CONTROL

Reboot system:
```bash
sudo reboot
```

Shutdown system:
```bash
sudo shutdown now
```

Schedule shutdown:
```bash
sudo shutdown +10
```

---

# 🔑 CHANGE USER PASSWORD

```bash
passwd
sudo passwd username
```

---

# 👥 USER & GROUP MANAGEMENT

Create user:
```bash
sudo useradd username
sudo passwd username
```

Delete user:
```bash
sudo userdel username
```

Create group:
```bash
sudo groupadd groupname
```

Delete group:
```bash
sudo groupdel groupname
```

Add user to group:
```bash
sudo usermod -aG groupname username
```

Check user ID & groups:
```bash
id username
groups username
```

Change user's primary group:
```bash
sudo usermod -g groupname username
```

---

# ⏰ SCHEDULE TASKS (CRON)

Edit cron jobs:
```bash
crontab -e
```

List cron jobs:
```bash
crontab -l
```

Example cron job (run script every day at 5 AM):
```bash
0 5 * * * /home/user/script.sh
```

---

# 📂 COPY FILE FROM ANOTHER LOCATION

```bash
cp /path/to/source/file.txt .
```

---

<p align="center">
  🎉 You now know how to monitor system resources, manage processes, control users & groups, and schedule tasks in Linux!
</p>
