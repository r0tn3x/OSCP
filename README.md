# OSCP+ Resources

**Author:** [r0tn3x](https://github.com/r0tn3x)  
**OSCP+ Certified:** December 7, 2025  
**Purpose:** Comprehensive OSCP preparation resources to help students pass the certification

---

## 📚 Repository Structure

```
OSCP+/
├── Tools/                     # Essential penetration testing tools
│   ├── enumeration/           # AutoRecon, SecLists, nmapAutomator
│   ├── exploitation/          # PowerShell, web shells, exploit frameworks
│   ├── privilege-escalation/  # LinPEAS, WinPEAS, PrivescCheck, pspy
│   └── active-directory/      # BloodHound, Mimikatz, Impacket, Rubeus
├── CVE/                       # CVE exploits and vulnerability databases
│   ├── exploitdb/             # Searchsploit database
│   └── oscp-common-cves.md    # Frequently seen CVEs in exam
├── Report-Templates/          # OSCP exam report templates
│   ├── markdown/              # Markdown templates by noraj
│   ├── word/                  # Word templates by whoisflynn
│   └── latex/                 # LaTeX Eisvogel template
├── Notes/                     # Comprehensive study guides (9 files)
│   ├── enumeration.md         # Complete enumeration methodology
│   ├── pivoting.md            # Chisel, ligolo-ng, SSH tunneling
│   ├── cheatsheet.md          # Quick reference for exam day
│   ├── linux-privesc.md       # Linux privilege escalation
│   ├── windows-privesc.md     # Windows privilege escalation
│   ├── active-directory.md    # AD exploitation & attacks
│   ├── buffer-overflow.md     # BOF methodology with scripts
│   ├── web-exploitation.md    # SQLi, XSS, LFI/RFI, uploads
│   └── resources.md           # Links, blogs, Discord, platforms
└── README.md                  # This file
```

---

## 🛠️ Tools

Essential tools for OSCP exam preparation:

- **[Enumeration Tools](Tools/enumeration/)** - AutoRecon, SecLists, nmapAutomator
- **[Exploitation Tools](Tools/exploitation/)** - PowerShell scripts, web shells, exploit frameworks
- **[Privilege Escalation](Tools/privilege-escalation/)** - LinPEAS, WinPEAS, PrivescCheck
- **[Active Directory](Tools/active-directory/)** - BloodHound, Mimikatz, Impacket, Rubeus

See [Tools Directory](Tools/) for complete list.

---

## 📝 Notes & Guides

Comprehensive study materials:

### Core Methodology
- **[Enumeration Guide](Notes/enumeration.md)** - Complete enumeration methodology
- **[Pivoting & Port Forwarding](Notes/pivoting.md)** - Chisel, ligolo-ng, SSH tunneling
- **[Cheat Sheet](Notes/cheatsheet.md)** - Quick reference for exam day

### Privilege Escalation
- **[Linux Privilege Escalation](Notes/linux-privesc.md)** - SUID, sudo, capabilities, kernel exploits
- **[Windows Privilege Escalation](Notes/windows-privesc.md)** - Tokens, services, registry, UAC bypass

### Exploitation
- **[Buffer Overflow](Notes/buffer-overflow.md)** - Complete BOF methodology with scripts
- **[Web Exploitation](Notes/web-exploitation.md)** - SQLi, XSS, LFI/RFI, file uploads
- **[Active Directory](Notes/active-directory.md)** - BloodHound, Kerberos, lateral movement

### Resources
- **[Important Resources](Notes/resources.md)** - Links, blogs, Discord, practice platforms

---

## 🐛 CVE & Exploits

- [CVE Directory](CVE/) - Organized vulnerability exploits
- [ExploitDB Mirror](CVE/exploitdb/) - Searchsploit database
- [Common OSCP CVEs](CVE/oscp-common-cves.md) - Frequently seen in exam

---

## 📄 Report Templates

Professional OSCP exam report templates:

- [Markdown Template](Report-Templates/markdown/) - By noraj
- [Word Template](Report-Templates/word/) - By whoisflynn
- [LaTeX Template](Report-Templates/latex/) - Eisvogel template

See [Report Templates Guide](Report-Templates/README.md)

---

## 🎯 Quick Start

### 1. Clone Repository
```bash
git clone https://github.com/r0tn3x/OSCP-Resources.git
cd OSCP-Resources
```

### 2. Read Methodology
Start with the [Enumeration Guide](Notes/enumeration.md) and [Cheat Sheet](Notes/cheatsheet.md)

### 3. Setup Tools
```bash
cd Tools/
# Install required tools
```

### 4. Practice
Use [Important Resources](Notes/resources.md) for practice platforms

---

## 🌟 Highlights

- ✅ **Curated Tools** - 18 essential tools across 4 categories (3.1GB)
- ✅ **Comprehensive Notes** - 9 detailed markdown guides (170KB total)
- ✅ **Proven Methodology** - Used to pass OSCP+ December 2025
- ✅ **Complete Documentation** - Every tool and technique documented
- ✅ **Report Templates** - 3 professional exam report formats
- ✅ **Active Directory Focus** - 50KB comprehensive AD attack guide
- ✅ **No Bloat** - Only what you need, nothing you don't

---

## 📖 Study Path

**Recommended order:**

1. Read [Enumeration Guide](Notes/enumeration.md)
2. Review [Cheat Sheet](Notes/cheatsheet.md)
3. Practice with [Resources](Notes/resources.md) (HTB, PG Practice)
4. Study [Pivoting Guide](Notes/pivoting.md)
5. Review [CVE Exploits](CVE/)
6. Prepare [Report Template](Report-Templates/)

---

## 🤝 Contributing

Found useful resources? Open an issue or PR!

---

## 📜 License

Educational purposes only. All tools remain under their original licenses.

---

## 👤 Author

**r0tn3x**  
- OSCP+ Certified: December 7, 2025
- Created to help future OSCP students

---

## ⭐ Acknowledgments

Thanks to the infosec community for creating these amazing tools and resources.

If this repository helped you, please ⭐ star it and share with others!

---

**Last Updated:** December 15, 2025
