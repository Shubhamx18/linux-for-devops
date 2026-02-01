<h1 align="center">👤 Day 8 – Users, Permissions & Remote Access</h1>

<p align="center">
  <img src="https://img.shields.io/badge/Linux-Users_&_Permissions-FCC624?style=for-the-badge&logo=linux&logoColor=black"/>
  <img src="https://img.shields.io/badge/Day-8-System_Admin-success?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Level-Intermediate-blue?style=for-the-badge"/>
</p>

<p align="center">
  Learn how to install applications, manage users, run admin commands, connect remotely, and control file permissions.
</p>

---

# 📦 INSTALL APPLICATIONS

### 🐧 Ubuntu / Debian
```bash
sudo apt update
sudo apt install nginx
```

### 🐧 CentOS / RHEL
```bash
sudo yum install nginx
```
or
```bash
sudo dnf install nginx
```

---

# 👤 USER MANAGEMENT

### Create a new user
```bash
sudo useradd username
sudo passwd username
```

### Delete a user
```bash
sudo userdel username
```

### Add user to a group
```bash
sudo usermod -aG groupname username
```

### View current user
```bash
whoami
```

### Show logged-in users
```bash
who
```

---

# 🔄 SWITCH USERS

```bash
su username
su -
```

Run a command as root:
```bash
sudo command
```

---

# 🔐 SUDO ACCESS

Edit sudo permissions safely:
```bash
sudo visudo
```

Add user to sudo group (Ubuntu):
```bash
sudo usermod -aG sudo username
```

---

# 🌐 REMOTE ACCESS (SSH)

### Connect to remote server
```bash
ssh user@server_ip
```

### SSH with key
```bash
ssh -i key.pem user@server_ip
```

---

# 🔑 GENERATE SSH KEY

```bash
ssh-keygen
```

Copy key to server:
```bash
ssh-copy-id user@server_ip
```

---

# 📂 COPY FILES BETWEEN MACHINES

### Send file to server
```bash
scp file.txt user@server_ip:/home/user/
```

### Send folder
```bash
scp -r myfolder user@server_ip:/home/user/
```

### Download file from server
```bash
scp user@server_ip:/home/user/file.txt .
```

---

# 🔐 FILE PERMISSIONS

Permission format:
```
-rwxr-xr--
```

| Symbol | Meaning |
|--------|---------|
| r | Read |
| w | Write |
| x | Execute |
| - | No permission |

Groups:
- User (Owner)
- Group
- Others

---

# 🔧 CHANGE PERMISSIONS (`chmod`)

Symbolic:
```bash
chmod +x file.sh
chmod -w file.txt
```

Numeric:
```bash
chmod 755 script.sh
chmod 644 file.txt
```

---

# 👤 CHANGE OWNER (`chown`)

```bash
sudo chown user file.txt
sudo chown user:group file.txt
```

---

# 👥 CHANGE GROUP (`chgrp`)

```bash
sudo chgrp developers file.txt
```

---

# 🧮 DEFAULT PERMISSIONS (`umask`)

Check default permission mask:
```bash
umask
```

Set temporary umask:
```bash
umask 022
```

---

# ⭐ SPECIAL PERMISSIONS

### Set SUID
```bash
chmod u+s file
```

### Set SGID
```bash
chmod g+s directory
```

### Sticky Bit (shared folders like /tmp)
```bash
chmod +t directory
```

---

# ⚠️ PERMISSION RULES

✔ Only **owner or root** can change permissions  
✔ Only **root** can change ownership  
✔ Groups control shared access  
✔ Permissions protect system security  

---

<p align="center">
  🎉 You now understand Linux users, sudo, SSH, file transfers, and full permission control!
</p>
