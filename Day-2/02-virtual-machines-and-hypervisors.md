<h1 align="center">🖥️ Day 2 – Virtual Machines & Hypervisors</h1>

<p align="center">
  <img src="https://img.shields.io/badge/Topic-Virtualization-blueviolet?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Focus-DevOps_&_Cloud-success?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Level-Foundation-blue?style=for-the-badge"/>
</p>

<p align="center">
  <i>Virtualization is the backbone of cloud computing and modern DevOps infrastructure.</i>
</p>

---

## 🎯 Learning Objectives

- Understand what a **Virtual Machine (VM)** is  
- Understand **virtualization architecture**  
- Clearly explain what a **Hypervisor** does  
- Learn **types of hypervisors**  
- Know **benefits and real-world uses of VMs**  
- Learn tools like **PuTTY and others** to connect to Linux VMs  

---

# 🧠 What is a Virtual Machine (VM)?

A **Virtual Machine (VM)** is a **software-based computer** running inside a physical computer.

Each VM includes:
- Its own **Operating System**
- Virtual **CPU**
- Virtual **RAM**
- Virtual **Disk**
- Virtual **Network Interface**

Multiple VMs can run on one physical machine at the same time.

---

# 🏗️ Virtualization Architecture

Virtualization works using a **Hypervisor**, which sits between hardware and virtual machines.

<p align="center">
  <img src="https://upload.wikimedia.org/wikipedia/commons/6/6e/Hypervisor.png" width="600"/>
</p>

The **hypervisor** divides physical hardware resources and assigns them to multiple virtual machines.

---

# ⚙️ What is a Hypervisor?

A **Hypervisor** is software that **creates and manages Virtual Machines**.

It acts as a **resource controller** between hardware and VMs.

## 🧩 Hypervisor Responsibilities

| Resource | Hypervisor Role |
|----------|-----------------|
| CPU | Shares processor time |
| RAM | Allocates memory safely |
| Storage | Creates virtual disks |
| Network | Provides virtual network adapters |
| Security | Ensures VM isolation |

Without a hypervisor, virtualization is impossible.

---

# 🧱 Types of Hypervisors

## 🥇 Type 1 – Bare Metal Hypervisor

Runs **directly on hardware**.

<p align="center">
  <img src="https://upload.wikimedia.org/wikipedia/commons/9/9c/Hyperviseur_Type_1.png" width="600"/>
</p>

**Examples:** VMware ESXi, Microsoft Hyper-V, Xen

---

## 🥈 Type 2 – Hosted Hypervisor

Runs **on top of an existing OS**.

<p align="center">
  <img src="https://upload.wikimedia.org/wikipedia/commons/6/64/Hyperviseur_Type_2.png" width="600"/>
</p>

**Examples:** VirtualBox, VMware Workstation

---

# 🌟 Benefits of Virtual Machines

✔ Multiple OS on one machine  
✔ Strong isolation  
✔ Easy snapshots & backups  
✔ Fast server deployment  
✔ Safe testing environments  
✔ Efficient hardware usage  
✔ Foundation of cloud platforms  

---

# 🌍 Real-World Uses

- Cloud servers (AWS EC2, Azure VMs)  
- DevOps testing environments  
- Enterprise data centers  
- Learning Linux safely  

---

# 🔌 Tools to Connect to Linux Virtual Machines

| Tool | Purpose |
|------|---------|
| PuTTY | SSH client for Windows |
| WinSCP | Secure file transfer |
| MobaXterm | Terminal + file transfer |
| Windows Terminal | Command-line interface |
| SSH | Built-in remote access |

Example SSH command:

