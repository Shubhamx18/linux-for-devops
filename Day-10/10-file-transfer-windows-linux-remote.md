<h1 align="center">🌐 Day 10 – File Transfer (Windows ↔ Linux & Remote ↔ Remote)</h1>

<p align="center">
  <img src="https://img.shields.io/badge/Linux-File_Transfer-FCC624?style=for-the-badge&logo=linux&logoColor=black"/>
  <img src="https://img.shields.io/badge/Windows-WinSCP-0078D6?style=for-the-badge&logo=windows&logoColor=white"/>
  <img src="https://img.shields.io/badge/Protocols-SCP_|_SFTP-success?style=for-the-badge"/>
</p>

<p align="center">
  Learn how to transfer files between local machine, remote Linux servers, and between two remote servers securely.
</p>

---

# 🖥️ WinSCP (Windows ➜ Linux)

## What is WinSCP?
WinSCP is a Windows tool for secure file transfer between:
- Windows ↔ Linux
- Local ↔ Remote
- Supports **SFTP, SCP, FTP, FTPS**

---

## Install & Setup WinSCP

1. Download WinSCP  
2. Open → New Site  
3. Select **File Protocol: SFTP**  
4. Host Name = Linux Server IP  
5. Port = 22  
6. Username & Password  
7. Click **Login**

---

## WinSCP Interface

| Left Panel | Right Panel |
|-----------|-------------|
| Windows Files | Linux Server Files |

✔ Drag & Drop to transfer  
✔ Right-click → Upload / Download  

---

## Transfer Files Using WinSCP

### Windows ➜ Linux
Drag file from left → right

### Linux ➜ Windows
Drag file from right → left

### Transfer Folders
Drag full folder — WinSCP copies recursively

---

# 🐧 SCP (Secure Copy) – Linux CLI

SCP uses SSH for secure transfer.

---

## 1️⃣ Local ➜ Remote Linux

Copy file:
```bash
scp file.txt user@IP:/home/user/
```

Copy folder:
```bash
scp -r myfolder user@IP:/home/user/
```

---

## 2️⃣ Remote Linux ➜ Local

Copy file:
```bash
scp user@IP:/home/user/file.txt .
```

Copy folder:
```bash
scp -r user@IP:/home/user/myfolder .
```

`.` means current directory.

---

## 3️⃣ Remote ➜ Remote (Using Local Machine)

You are on your local PC copying between two servers.

```bash
scp user1@IP1:/path/file user2@IP2:/path/
```

Copy folder:
```bash
scp -r user1@IP1:/home/user1/myfolder user2@IP2:/home/user2/
```

---

## 4️⃣ Remote ➜ Remote (Directly From Server)

SSH into Server 1 first:
```bash
ssh user1@IP1
```

Then run:
```bash
scp file.txt user2@IP2:/home/user2/
```

---

# 🔑 SSH Must Be Enabled

On remote server:
```bash
sudo systemctl enable ssh --now
```

---

# 🔐 Use SCP with SSH Key

```bash
scp -i key.pem file.txt user@IP:/home/user/
```

---

# 📦 Preserve File Permissions

```bash
scp -p file.txt user@IP:/home/user/
```

---

# 🚀 Faster Copy with Compression

```bash
scp -C file.txt user@IP:/home/user/
```

---

# 📊 Transfer Progress

```bash
scp -v file.txt user@IP:/home/user/
```

---

# 🌍 SFTP (Interactive Secure Transfer)

```bash
sftp user@IP
```

Commands inside SFTP:
```
put file.txt
get file.txt
ls
cd folder
bye
```

---

# 🔁 rsync (Advanced Transfer Tool)

Faster and resumable transfers.

```bash
rsync -avz file.txt user@IP:/home/user/
```

Copy folder:
```bash
rsync -avz myfolder user@IP:/home/user/
```

---

# ⚠️ Common Errors

| Problem | Fix |
|--------|-----|
| Permission denied | Check username/password or key |
| Connection refused | SSH not running |
| No such file | Check path |
| Timeout | Check firewall/IP |

---

<p align="center">
  🎉 You now know WinSCP, SCP, SFTP, and remote-to-remote transfers like a DevOps engineer!
</p>
