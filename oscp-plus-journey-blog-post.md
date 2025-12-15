# My Journey: OSCP (2023) → OSCP+ (2025)

**Date: December 7, 2025**  
**Author: r0tn3x**

I'm thrilled to announce that I've successfully passed the **Offensive Security Certified Professional Plus (OSCP+)** certification! This wasn't my first rodeo—I originally earned my OSCP back in 2023, but when I won a free voucher from a CTF competition, it was an easy decision to take on the updated OSCP+ challenge.

Spoiler alert: **The exam has evolved quite a bit**, and I learned just as much the second time around.

## What is OSCP+?

The OSCP+ is the updated version of the renowned OSCP certification, one of the most respected hands-on penetration testing certifications in the cybersecurity industry. Having taken both the original OSCP (2023) and OSCP+ (2025), I can confirm the evolution is real.

### What Changed?
- **More Active Directory focus** - The AD set is now mandatory and more complex
- **Modern tooling** - Updated to reflect current industry practices
- **Enhanced difficulty** - Machines feel more realistic and interconnected
- **Better structure** - Clearer point system and exam flow

### Core Skills Validated:
- Network penetration testing
- Web application security
- Active Directory exploitation & lateral movement
- PostJourney: From OSCP to OSCP+

### The First Attempt (OSCP 2023)

My original OSCP journey taught me the fundamentals. It was challenging, rewarding, and pushed me to develop a solid pentesting methodology. I passed on my first attempt after months of preparation in the PWK labs.

### The Return (OSCP+ 2025)

When I won a free voucher from a CTF competition, I saw it as the perfect opportunity to:
1. **Update my skills** - See how the exam had evolved
2. **Challenge myself** - Test against the enhanced difficulty
3. **Validate my growth** - Measure my progress over 2 years

**Was it worth it?** Absolutely. The new OSCP+ format is significantly more challenging, especially the Active Directory portion. Even with my 2023 OSCP experience, I had to learn new techniques and approaches.

### Lab Time & Practice

The key to success was **consistent practice**. I spent time in the updated OffSec labs and Proving Grounds, focusing on the new AD scenarios. Every compromised machine taught me something new, and having prior OSCP experience actually helped me identify what had changed.

### The Mindset

The most important lesson (still true from 2023)? **Enumeration is key.** I can't stress this enough. The OSCP+ machines require even more thorough enumeration and lateral thinking. Document everything, trust your methodology
### Lab Time & Practice

The key to success was **consistent practice**. I spent months in the OffSec labs, attacking machines of varying difficulty levels. Every compromised machine taught me something new, and every failure made me more determined.

### The Mindset

The most important lesson? **Enumeration is key.** I can't stress this enough. Most of my initial failures came from rushing. Once I learned to enumerate thoroughly and document everything, the path forward became clearer.

## Essential Resources That Helped Me

### Official Materials
- **OffSec PEN-200 Course Materials** - The foundational content provided by Offensive Security
- **OffSec Practice Labs** - Invaluable hands-on experience with 70+ machines
- **OffSec Proving Grounds** - Additional practice machines (Practice & Play)

### Community Resources

#### Enumeration & Methodology
- **AutoRecon** (https://github.com/Tib3rius/AutoRecon) - Automated enumeration tool
- **nmapAutomator** (https://github.com/21y4d/nmapAutomator) - Network scanning automation
- **LinPEAS & WinPEAS** (https://github.com/carlospolop/PEASS-ng) - Privilege escalation enumeration scripts

#### Learning Platforms
- **TryHackMe** - Great for beginners and intermediate learners
  - OSCP Preparation Path
  - Active Directory rooms
- **HackTheBox** - Excellent retired machines for practice
  - TJnull's OSCP-like machines list
- **VulnHub** - Free vulnerable VMs for offline practice

#### Reference Guides
- **HackTricks** (https://book.hacktricks.xyz/) - Comprehensive pentesting methodology
- **PayloadsAllTheThings** (https://github.com/swisskyrepo/PayloadsAllTheThings) - Attack payloads and bypasses
- **GTFOBins** (https://gtfobins.github.io/) - Unix binaries for privilege escalation
- **LOLBAS** (https://lolbas-project.github.io/) - Living Off The Land Binaries for Windows

#### Active Directory
- **Attacking Active Directory** by zer1t0
- **Active Directory Security** (https://adsecurity.org/) - Sean Metcalf's blog
- **Orange Cyberdefense's AD Mindmap** - Visual reference for AD attacks

### Note-Taking & Documentation
- **CherryTree** - Hierarchical note-taking (my personal choice)
- **Obsidian** - Markdown-based knowledge base
- **Notion** - Collaborative documentation platform
- **KeepNote** - Classic OSCP note-taking tool

### Report Writing
- **Offensive Security's Report Templates** - Use the official templates
- **whoisflynn's OSCP Report Template** (https://github.com/whoisflynn/OSCP-Exam-Report-Template) - Community-enhanced version

## Key Tips for Success

### 1. Master the Fundamentals
Don't skip the basics. Understanding how services work is more valuable than memorizing exploits.

### 2. Build Your Methodology
Develop a consistent approach:
- **Enumerate** → Document → Analyze → Exploit → Document
- Keep detailed notes during practice
- Create your own checklist

### 3. Practice Report Writing
Your report matters. Practice writing clear, professional penetration testing reports during your lab time.

### 4. Time Management
During the exam:
- Don't get stuck on one machine for too long
- Take breaks (seriously, take them!)
- Start with machines that play to your strengths

### 5. Active Directory is Critical
Make sure you're comfortable with:
- BloodHound and SharpHound
- Mimikatz and credential dumping
- Lateral movement techniques
- Kerberos attacks (Kerberoasting, AS-REP Roasting)

### 6. Don't Just Follow Walkthroughs
When practicing, try to solve machines independently first. Walkthroughs should be learning tools, not crutches.
Having experienced both OSCP (2023) and OSCP+ (2025), I can confidently say the evolution is significant and worthwhile. OSCP+ isn't just a certification—it's a validation of your ability to think like an attacker, adapt to challenges, and persist through difficulty.

**For those with OSCP considering the upgrade:** The exam has matured. The AD focus alone makes it worth attempting if you want to validate your current skills against modern standards.

**For first-time OSCP+ candidates:** You're getting the best version of this certification yet. The challenges are realistic, the skills are immediately applicable, and the satisfaction of passing is unmatched.

To anyone preparing for OSCP+: **You can do this.** Stay consistent, practice deliberately, and remember that every failed attempt is a learning opportunity.

## My OSCP+ Resources Repository

I've compiled all my notes, tools, and resources into a comprehensive GitHub repository to help future OSCP+ students:

**🔗 https://github.com/r0tn3x/OSCP**

The repository includes:
- ✅ 18 essential penetration testing tools
- ✅ 9 comprehensive markdown guides (170KB+)
- ✅ Active Directory attack methodology (50KB guide)
- ✅ Linux & Windows privilege escalation guides
- ✅ Buffer overflow complete methodology
- ✅ Professional report templates
- ✅ CVE database and common exploits

All organized, documented, and ready to use. If this repository helps you pass, please ⭐ star it and share with others!
The 24-hour exam was intense. I started methodically, documenting everything from the beginning. Around hour 12, I hit a wall on a difficult machine, so I took a break, walked around, and came back with fresh eyes. That break saved me.

By hour 18, I had enough points to pass, but I kept going to maximize my score. The final 6 hours were spent cleaning up my notes and preparing for the report.

### Report Writing

After a few hours of sleep, I spent the next 12 hours crafting my penetration test report. Clear screenshots, detailed exploitation steps, and remediation recommendations were key.

## Final Thoughts

Going from OSCP (2023) to OSCP+ (2025) showed me just how much the field advances in a short time. Stay curious, keep practicing, and never stop learning.

If you're on this journey, feel free to reach out. The community is here to support you.

📚 **Check out my resources:** https://github.com/r0tn3x/OSCP  
🎯 **Author:** r0tn3x  
📅 **OSCP:** 2023 | **OSCP+:** December 7, 2025

**#OSCP #OSCP+ #OffSec #CyberSecurity #PenetrationTesting #InfoSec #TryHarder #r0tn3x deliberately, and remember that every failed attempt is a learning opportunity.

## Resources Summary

**Practice Platforms:**
- OffSec Proving Grounds (PG Practice & Play)
- HackTheBox (Retired machines from TJnull's list)
- TryHackMe (OSCP Prep path)
- VulnHub

**Tools to Master:**
- nmap
- Burp Suite / OWASP ZAP
- Metasploit (know the limits for exam)
- BloodHound
- Impacket suite
- PowerView / SharpView
- Chisel / ligolo-ng (for pivoting)

**Study Resources:**
- OffSec PEN-200 official materials
- HackTricks book
- PayloadsAllTheThings GitHub
- IppSec's YouTube videos (HackTheBox walkthroughs)
- Active Directory mindmaps

---

**Try Harder. Stay Humble. Keep Learning.**

The OSCP+ journey doesn't end with certification—it's just the beginning. The cybersecurity landscape is always evolving, and so must we.

If you're on this journey, feel free to reach out. The community is here to support you.

**#OSCP #OSCP+ #OffSec #CyberSecurity #PenetrationTesting #InfoSec #TryHarder**
