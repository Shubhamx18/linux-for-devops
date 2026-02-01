<h1 align="center">🔐 Day 11 – SSH, Server Management & systemctl</h1>

<p align="center">
  <img src="https://img.shields.io/badge/Linux-SSH_&_Systemd-FCC624?style=for-the-badge&logo=linux&logoColor=black"/>
  <img src="https://img.shields.io/badge/Day-11-Server_Management-success?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Level-Intermediate-blue?style=for-the-badge"/>
</p>

<p align="center">
  Learn SSH, passwordless login, and how to manage Linux services using systemctl.
</p>

---

# 🔐 SSH (Secure Shell)

### What is SSH?
SSH is a **secure network protocol** that allows two computers to communicate securely over a network.

✔ Encrypted communication  
✔ Remote server access  
✔ Secure file transfer  

---

## 📌 Default SSH Port

```
22
```

You can change it in:
```
/etc/ssh/sshd_config
```

---

## 🔗 Connect to Remote Server

```bash
ssh username@ip_address
```

Example:
```bash
ssh shubham@192.168.1.10
```

---

# 🛠️ Installing SSH

Check if installed:
```bash
rpm -qa | grep ssh
```

If not installed:
```bash
sudo yum install openssh-clients openssh-server
```

Start and enable SSH:
```bash
sudo systemctl start sshd
sudo systemctl enable sshd
```

Check status:
```bash
sudo systemctl status sshd
```

---

# 🔑 Passwordless SSH Login

## Why use SSH key login?
- No need to enter password every time
- More secure
- Used in automation & DevOps

---

## Step 1: Generate SSH Key on Local Machine

```bash
ssh-keygen
```

Keys are stored in:
```
~/.ssh/
```

---

## Step 2: Copy Public Key to Remote Server

```bash
ssh-copy-id user@ip_address
```

Now login without password:
```bash
ssh user@ip_address
```

---

# 🖥️ Server Management Using systemctl

systemctl is used to manage system services in Linux.

---

## ▶ Start a Service

```bash
sudo systemctl start service_name
```

---

## ⏹ Stop a Service

```bash
sudo systemctl stop service_name
```

---

## 🔄 Restart a Service

```bash
sudo systemctl restart service_name
```

---

## 📊 Check Service Status

```bash
sudo systemctl status service_name
```

---

## 🔁 Enable Service on Boot

```bash
sudo systemctl enable service_name
```

Enable and start immediately:
```bash
sudo systemctl enable --now service_name
```

---

## ❌ Disable Service

```bash
sudo systemctl disable service_name
```

---

## 🚫 Mask Service (Prevent Start)

```bash
sudo systemctl mask service_name
```

Unmask:
```bash
sudo systemctl unmask service_name
```

---

## 📋 Check if Service is Enabled

```bash
sudo systemctl is-enabled service_name
```

---

# 🔌 List IPC Sockets

```bash
systemctl list-sockets
```

Show socket types:
```bash
systemctl --show-types list-sockets
```

---

# 🖥️ System Control Commands

Power off system:
```bash
sudo systemctl poweroff
```

Reboot system:
```bash
sudo systemctl reboot
```

Force reboot (ignore logged-in users):
```bash
sudo systemctl -i reboot
```

---

# 🌍 Access Linux Server From Another Server

From Server A:
```bash
ssh user@serverB_ip
```

Make sure SSH service is running on Server B.

---

<p align="center">
  🎉 You now know SSH, passwordless login, and full Linux service management using systemctl!
</p>
