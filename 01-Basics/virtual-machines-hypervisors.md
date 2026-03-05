# Virtual Machines & Hypervisors

---

## What is a Virtual Machine?

A virtual machine (VM) is a software-based computer that runs inside a physical machine. Each VM behaves like a completely independent computer — it has its own operating system, virtual CPU, RAM, storage, and network adapter.

Multiple VMs can run simultaneously on one physical host, each isolated from the others.

---

## What is a Hypervisor?

A hypervisor is the software layer that creates and manages VMs. It divides the physical hardware into virtual resources and distributes them to each VM.

| Resource | What the hypervisor does |
|----------|------------------------|
| CPU | Allocates processor time across VMs |
| RAM | Partitions physical memory |
| Storage | Creates virtual disk files |
| Network | Provides virtual network interfaces |
| Security | Keeps VMs isolated from each other |

---

## Type 1 vs Type 2 Hypervisors

### Type 1 — Bare Metal

Runs directly on hardware. No host OS is required. Better performance, used in production.

| Product | Vendor |
|---------|--------|
| VMware ESXi | VMware |
| Microsoft Hyper-V | Microsoft |
| Xen | Open Source |
| KVM | Linux kernel (built-in) |

Used in: data centers, cloud providers (AWS, Azure, GCP all use Type 1), enterprise servers.

### Type 2 — Hosted

Runs on top of an existing operating system. Easier to set up, but with more overhead.

| Product | Vendor |
|---------|--------|
| VirtualBox | Oracle |
| VMware Workstation | VMware |
| VMware Fusion | VMware (macOS) |
| Parallels | Parallels (macOS) |
| QEMU | Open Source |

Used in: local development, learning environments, testing.

---

## KVM — Linux Built-in Virtualization

KVM (Kernel-based Virtual Machine) is built into the Linux kernel. It turns Linux into a Type 1 hypervisor when combined with QEMU.

```bash
# Check if CPU supports virtualization
grep -E "(vmx|svm)" /proc/cpuinfo    # vmx = Intel VT-x, svm = AMD-V
lscpu | grep Virtualization

# Install KVM on Ubuntu
sudo apt install qemu-kvm libvirt-daemon-system virtinst virt-manager

# Check the service
sudo systemctl status libvirtd
sudo systemctl enable --now libvirtd

# Add your user to the KVM group
sudo usermod -aG kvm $USER
sudo usermod -aG libvirt $USER

# List running VMs
virsh list

# List all VMs (including stopped)
virsh list --all

# Start / stop / restart a VM
virsh start vm-name
virsh shutdown vm-name
virsh reboot vm-name
virsh destroy vm-name       # force stop (like pulling the power)

# Suspend and resume
virsh suspend vm-name
virsh resume vm-name

# VM info
virsh dominfo vm-name
virsh domifaddr vm-name     # show IP address

# Connect to VM console
virsh console vm-name

# Delete a VM
virsh undefine vm-name
virsh undefine vm-name --remove-all-storage   # also delete disk

# Create a VM (example)
virt-install \
  --name ubuntu-server \
  --ram 2048 \
  --vcpus 2 \
  --disk path=/var/lib/libvirt/images/ubuntu.qcow2,size=20 \
  --os-variant ubuntu22.04 \
  --cdrom /path/to/ubuntu.iso \
  --graphics none \
  --console pty,target_type=serial
```

---

## VirtualBox Quick Reference

```bash
# List VMs
VBoxManage list vms
VBoxManage list runningvms

# Start / stop
VBoxManage startvm "VM Name" --type headless   # start without GUI
VBoxManage controlvm "VM Name" poweroff
VBoxManage controlvm "VM Name" savestate       # save state (hibernate)

# Snapshots
VBoxManage snapshot "VM Name" take "before-update"
VBoxManage snapshot "VM Name" list
VBoxManage snapshot "VM Name" restore "before-update"
VBoxManage snapshot "VM Name" delete "before-update"

# Get VM IP (requires VirtualBox Guest Additions)
VBoxManage guestproperty get "VM Name" "/VirtualBox/GuestInfo/Net/0/V4/IP"
```

---

## Why VMs Matter for DevOps

- Cloud servers (AWS EC2, Azure VM, GCP Compute) are all VMs
- You can test infrastructure changes on a VM before touching production
- VMs are easily snapshotted, cloned, and restored
- Docker containers often run inside VMs in cloud environments
- Learning Linux on a local VM costs nothing and risks nothing

---

## Tools to Connect to Linux VMs

| Tool | Platform | Purpose |
|------|----------|---------|
| `ssh` | Linux / macOS / Windows | Native terminal access |
| PuTTY | Windows | SSH terminal client |
| MobaXterm | Windows | SSH + file transfer + X11 |
| WinSCP | Windows | File transfer (SFTP/SCP) |
| Windows Terminal | Windows | Built-in SSH support |
| virt-manager | Linux | GUI for KVM VMs |

```bash
# Connect to a VM by IP
ssh user@192.168.122.10

# Connect to a VM with a key
ssh -i ~/.ssh/vm_key.pem user@192.168.122.10

# Find a KVM VM's IP
virsh domifaddr my-vm
```

---

## Common VM Networking Modes

| Mode | Description | Use Case |
|------|-------------|---------|
| NAT | VM shares host's IP, can reach internet, not reachable from outside | Default, internet access only |
| Bridged | VM gets its own IP on your network, reachable by other machines | Server testing, access from LAN |
| Host-only | VM can only talk to the host | Isolated testing |
| Internal | VMs talk to each other only, no host/internet access | Multi-VM isolated lab |
