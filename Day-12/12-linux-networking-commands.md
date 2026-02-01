<h1 align="center">🌐 Day 12 – Linux Networking Commands (Deep Dive)</h1>

<p align="center">
  Complete explanation of Linux networking tools with command options and real-world use cases.
</p>

---

# 📡 1. ping — Test Connectivity

### 🔹 What it does
Sends ICMP packets to check if a host is reachable.

### 🔹 Why we use it
- Check internet connectivity
- Check if a server is up
- Measure latency

### 🔹 Commands

```bash
ping google.com
ping -c 4 google.com        # Send 4 packets only
ping -i 2 google.com        # Interval of 2 seconds
ping -s 1000 google.com     # Packet size
ping -t 5 google.com        # TTL value
```

---

# 🧭 2. traceroute — Track Network Path

### 🔹 What it does
Shows each router (hop) your packet passes through to reach destination.

### 🔹 Why we use it
- Find where network delay happens
- Identify blocked routers/firewalls
- Troubleshoot slow connections

### 🔹 How it works
It sends packets with increasing TTL values. Each router decreases TTL and replies when TTL = 0.

### 🔹 Commands

```bash
traceroute google.com            # Normal trace
traceroute -n google.com         # Don't resolve hostnames (faster)
traceroute -I google.com         # Use ICMP instead of UDP
traceroute -T google.com         # Use TCP SYN packets
traceroute -p 80 google.com      # Trace using port 80
traceroute -m 5 google.com       # Max hops = 5
```

### 🔹 Alternative
```bash
tracepath google.com
```

---

# 🔌 3. netstat — Network Statistics (Legacy Tool)

### 🔹 What it does
Shows active connections, listening ports, routing tables.

### 🔹 Why we use it
- Check which services are running
- See open ports
- Find network issues

### 🔹 Commands

```bash
netstat -tuln       # TCP/UDP listening ports
netstat -tulnp      # Show process using port
netstat -rn         # Routing table
netstat -i          # Network interfaces
netstat -s          # Network statistics
netstat -an         # All connections
```

---

# 🚀 4. ss — Modern Replacement for netstat

### 🔹 What it does
Shows socket statistics (faster and more powerful).

### 🔹 Why we use it
Preferred tool in modern Linux for checking ports and connections.

### 🔹 Commands

```bash
ss -tuln         # Listening ports
ss -tulnp        # Ports with process info
ss -s            # Summary stats
ss -lnt          # TCP listening ports
ss -lnu          # UDP listening ports
ss -o state established '( dport = :ssh )'
```

---

# 🖥️ 5. ip — Network Configuration Tool

### 🔹 What it does
Replaces old commands like `ifconfig` and `route`.

### 🔹 Commands

```bash
ip a                     # Show IP addresses
ip addr show             # Same as above
ip link show             # Network interfaces
ip route                 # Routing table
ip neigh                 # ARP table
ip route add default via 192.168.1.1
ip route del default
```

Enable/Disable interface:
```bash
sudo ip link set eth0 up
sudo ip link set eth0 down
```

---

# 🌍 6. DNS Tools

## nslookup
```bash
nslookup google.com
nslookup google.com 8.8.8.8
```

## dig
```bash
dig google.com
dig google.com +short
dig -x 8.8.8.8          # Reverse DNS
```

## host
```bash
host google.com
host 8.8.8.8
```

---

# 🌐 7. curl — API & Web Testing Tool

```bash
curl https://example.com
curl -I https://example.com
curl -O https://example.com/file.zip
curl -X POST -d "name=test" https://example.com/api
curl -H "Content-Type: application/json" -d '{"name":"shubham"}' https://example.com/api
```

---

# 📥 8. wget — Download Files

```bash
wget https://example.com/file.zip
wget -c https://example.com/file.zip
wget -O newname.zip https://example.com/file.zip
```

---

# 🔍 9. lsof — List Open Network Files

```bash
lsof -i
lsof -i :22
lsof -i tcp
lsof -i udp
```

---

# 🧪 10. Port Testing

## telnet
```bash
telnet google.com 80
```

## netcat (nc)
```bash
nc -zv google.com 80
nc -l 1234
```

---

# 📈 11. Network Monitoring

| Tool | Purpose |
|------|---------|
| nload | Bandwidth usage |
| iftop | Who uses bandwidth |
| vnstat | Traffic stats |
| tcpdump | Packet capture |
| mtr | Live traceroute |

```bash
nload
sudo iftop
vnstat
sudo tcpdump -i eth0
mtr google.com
```

---

# 🔥 12. Firewall Check

Ubuntu:
```bash
sudo ufw status
```

CentOS:
```bash
sudo firewall-cmd --list-all
```

---

# 🧠 REAL-WORLD TROUBLESHOOT FLOW

| Step | Command |
|------|---------|
| Check IP | `ip a` |
| Check route | `ip route` |
| Ping gateway | `ping 192.168.1.1` |
| Ping internet | `ping 8.8.8.8` |
| DNS check | `nslookup google.com` |
| Check open ports | `ss -tulnp` |

---

<p align="center">
  🎉 This covers the core networking toolkit used by Linux System Administrators and DevOps Engineers.
</p>
