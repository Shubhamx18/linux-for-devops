# Linux Networking Commands

---

## ip — Network Interfaces and Routing

`ip` is the modern replacement for `ifconfig` and `route`.

```bash
# Addresses
ip a                              # show all interfaces and IPs
ip addr show                      # same as ip a
ip addr show eth0                 # specific interface only
ip -4 a                           # IPv4 only
ip -6 a                           # IPv6 only

# Add / remove IP
sudo ip addr add 192.168.1.100/24 dev eth0
sudo ip addr del 192.168.1.100/24 dev eth0

# Interfaces
ip link show                      # list all interfaces
sudo ip link set eth0 up          # bring interface up
sudo ip link set eth0 down        # bring interface down

# Routing
ip route                          # show routing table
ip route show                     # same
ip route get 8.8.8.8              # show which route is used to reach 8.8.8.8
sudo ip route add default via 192.168.1.1         # add default gateway
sudo ip route add 10.0.0.0/8 via 192.168.1.1      # add static route
sudo ip route del default                         # remove default gateway

# ARP table
ip neigh                          # show ARP/neighbor table
ip neigh flush all                # clear ARP cache
```

---

## ping — Test Connectivity

```bash
ping google.com                   # continuous ping (Ctrl+C to stop)
ping -c 4 google.com              # send exactly 4 packets
ping -c 4 -i 0.5 google.com       # 0.5 second interval between packets
ping -s 1000 google.com           # set packet size to 1000 bytes
ping -t 5 google.com              # set TTL to 5
ping -W 2 google.com              # timeout after 2 seconds per reply
ping -q google.com                # quiet — only show summary
ping 192.168.1.1                  # ping a local IP
```

---

## traceroute — Trace Network Path

Shows each router a packet passes through on its way to the destination.

```bash
traceroute google.com             # standard trace
traceroute -n google.com          # skip DNS (show IPs only, faster)
traceroute -I google.com          # use ICMP (like ping) instead of UDP
traceroute -T google.com          # use TCP SYN packets
traceroute -p 443 google.com      # trace using port 443
traceroute -m 15 google.com       # limit to 15 hops
tracepath google.com              # alternative, no root needed
mtr google.com                    # live combined ping + traceroute
mtr --report google.com           # run mtr and produce a report
```

---

## ss — Socket Statistics

Modern replacement for `netstat`. Faster and more detailed.

```bash
ss -tuln                          # TCP and UDP listening ports
ss -tulnp                         # same + show process name and PID
ss -s                             # summary of all socket stats
ss -lnt                           # TCP listening only
ss -lnu                           # UDP listening only
ss -an                            # all connections (established + listening)
ss -tnp                           # established TCP with processes
ss -unp                           # established UDP with processes
ss -4                             # IPv4 only
ss -6                             # IPv6 only
ss -o state established           # only established connections
ss -o state established '( dport = :22 )'   # filter by destination port
ss -t dst 192.168.1.10            # connections to a specific IP
```

---

## netstat — Legacy (Still Common)

```bash
netstat -tuln                     # TCP/UDP listening ports
netstat -tulnp                    # same + show process name/PID
netstat -an                       # all connections
netstat -rn                       # routing table
netstat -i                        # interface stats
netstat -s                        # per-protocol statistics
```

> `netstat` is deprecated on modern systems. Prefer `ss`.

---

## DNS Tools

```bash
# nslookup
nslookup google.com               # basic DNS query
nslookup google.com 8.8.8.8       # use a specific DNS server
nslookup -type=MX google.com      # query MX records

# dig (more detailed)
dig google.com                    # full DNS response
dig google.com +short             # IP only
dig google.com A                  # query A (IPv4) record
dig google.com AAAA               # query AAAA (IPv6) record
dig google.com MX                 # mail exchange records
dig google.com TXT                # TXT records
dig google.com NS                 # name server records
dig -x 8.8.8.8                   # reverse DNS lookup
dig @8.8.8.8 google.com          # query a specific DNS server
dig +trace google.com             # trace delegation from root

# host (simple)
host google.com                   # basic DNS lookup
host 8.8.8.8                     # reverse lookup
host -t MX google.com             # query MX records
```

---

## lsof — List Open Files and Network Connections

```bash
lsof -i                           # all network connections
lsof -i :22                       # who is using port 22
lsof -i :80                       # who is using port 80
lsof -i tcp                       # TCP connections only
lsof -i udp                       # UDP connections only
lsof -i @192.168.1.10             # connections to a specific IP
lsof -u alice                     # all files/connections opened by alice
lsof -p 1234                      # files opened by PID 1234
lsof +D /var/log                  # all files opened inside /var/log
```

---

## Port Testing

```bash
# Test if a port is open
nc -zv google.com 80              # test port 80 (TCP)
nc -zv -u google.com 53           # test port 53 (UDP)
nc -l 4444                        # listen on port 4444
nc 192.168.1.10 4444              # connect to listening nc

# telnet (simple port test)
telnet google.com 80

# Check if a local port is listening
ss -tlnp | grep :8080
```

---

## Network Monitoring Tools

| Tool | What it does | Install |
|------|-------------|---------|
| `nload` | Live bandwidth per interface | `apt install nload` |
| `iftop` | Live per-connection bandwidth | `apt install iftop` |
| `nethogs` | Per-process bandwidth usage | `apt install nethogs` |
| `vnstat` | Historical traffic statistics | `apt install vnstat` |
| `mtr` | Live traceroute + ping stats | `apt install mtr` |
| `tcpdump` | Capture and inspect packets | usually pre-installed |
| `wireshark` | GUI packet analyzer | `apt install wireshark` |

```bash
sudo nload
sudo iftop
sudo nethogs eth0
vnstat -i eth0 -l              # live stats for eth0
sudo mtr google.com
sudo tcpdump -i eth0
sudo tcpdump -i eth0 port 80   # capture only HTTP traffic
sudo tcpdump -w capture.pcap   # write to file for Wireshark
```

---

## Firewall

```bash
# Ubuntu — ufw
sudo ufw status
sudo ufw status verbose
sudo ufw enable
sudo ufw disable
sudo ufw allow 22/tcp
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw deny 3306/tcp
sudo ufw delete allow 80/tcp
sudo ufw allow from 192.168.1.0/24               # allow a subnet
sudo ufw allow from 192.168.1.10 to any port 22  # allow specific IP on port 22
sudo ufw reset                                   # reset all rules

# CentOS / RHEL — firewalld
sudo firewall-cmd --list-all
sudo firewall-cmd --add-port=22/tcp --permanent
sudo firewall-cmd --add-service=http --permanent
sudo firewall-cmd --remove-port=8080/tcp --permanent
sudo firewall-cmd --reload
sudo firewall-cmd --state
```

---

## Network Troubleshooting Flow

When a server is unreachable, work through this step by step:

| Step | Command | What to check |
|------|---------|---------------|
| 1 | `ip a` | Does the interface have an IP address? |
| 2 | `ip route` | Is there a default gateway? |
| 3 | `ping 192.168.1.1` | Can you reach the gateway? |
| 4 | `ping 8.8.8.8` | Can you reach the internet? |
| 5 | `nslookup google.com` | Is DNS working? |
| 6 | `ss -tulnp` | Is your service listening on the right port? |
| 7 | `sudo ufw status` | Is a firewall blocking the port? |
| 8 | `curl -v http://localhost` | Is the service responding? |
| 9 | `journalctl -u nginx -n 50` | What do the service logs say? |
