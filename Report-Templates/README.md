# Report Templates

**Author:** r0tn3x

Professional OSCP exam report templates to save time during reporting phase.

---

## 📝 Available Templates

### 1. Markdown Template (noraj)
**Location:** `markdown/`  
**Format:** Markdown → PDF  
**Best for:** Clean, professional reports with code syntax highlighting  
**GitHub:** https://github.com/noraj/OSCP-Exam-Report-Template-Markdown

**Features:**
- ✅ Automated PDF generation with Pandoc
- ✅ Syntax highlighting for code
- ✅ Professional layout
- ✅ Easy to edit

**Usage:**
```bash
cd markdown/
# Edit the .md file
generate.sh
```

---

### 2. Word Template (whoisflynn)
**Location:** `word/`  
**Format:** Microsoft Word .docx  
**Best for:** Those comfortable with Word, easy customization  
**GitHub:** https://github.com/whoisflynn/OSCP-Exam-Report-Template

**Features:**
- ✅ Easy to use
- ✅ No special tools required
- ✅ Track changes support
- ✅ Widely accepted format

**Usage:**
```
Open in Microsoft Word or LibreOffice
Edit and save as PDF
```

---

### 3. LaTeX Template (Eisvogel)
**Location:** `latex/`  
**Format:** LaTeX → PDF  
**Best for:** Professional typesetting, academic-style reports  
**GitHub:** https://github.com/Wandmalfarbe/pandoc-latex-template

**Features:**
- ✅ Beautiful typography
- ✅ Consistent formatting
- ✅ Version control friendly
- ✅ Highly customizable

**Usage:**
```bash
pandoc report.md -o report.pdf --template eisvogel --listings
```

---

## 🎯 Report Structure

All templates follow OSCP exam requirements:

### Required Sections

1. **High-Level Summary**
   - Overview of the assessment
   - Key findings summary
   - Risk rating

2. **Methodology**
   - Information Gathering
   - Service Enumeration
   - Penetration Testing
   - Privilege Escalation
   - Post-Exploitation

3. **Machine 1 (10 points - Buffer Overflow)**
   - Service Enumeration
   - Vulnerability Identification
   - Exploitation (step-by-step)
   - Screenshots with proof.txt

4. **Machine 2 (20 points)**
   - Initial Foothold
   - Privilege Escalation
   - Screenshots with proof.txt

5. **Machine 3 (20 points)**
   - Initial Foothold
   - Privilege Escalation
   - Screenshots with proof.txt

6. **Active Directory Set (40 points)**
   - MS01 - Initial Foothold
   - MS02 - Privilege Escalation
   - DC - Domain Admin
   - Screenshots with proof.txt

7. **Additional Items (Optional)**
   - Appendix
   - Remediation Steps
   - References

---

## 📸 Screenshot Requirements

### What to Include

**Every machine must have:**

1. **Initial shell screenshot showing:**
   - `ipconfig` or `ifconfig` output
   - `whoami` or `id` output

2. **Proof screenshot showing:**
   - `type proof.txt` (Windows) or `cat proof.txt` (Linux)
   - Full path visible
   - Hash displayed

3. **Exploitation screenshots:**
   - Key commands executed
   - Successful exploitation
   - Output showing success

### Screenshot Tips

```bash
# Linux - Take screenshot with timestamp
scrot '%Y-%m-%d_%H-%M-%S_$wx$h.png' -e 'mv $f ~/oscp-exam/screenshots/'

# Windows - Use Snipping Tool or
# PrintScreen → Paint → Save

# Organize by machine
~/oscp-exam/
├── 10.10.10.10/
│   ├── 01-nmap.png
│   ├── 02-exploit.png
│   ├── 03-proof.png
```

---

## ✍️ Writing Tips

### Do's ✅

1. **Be detailed** - Explain every step
2. **Show commands** - Include exact commands used
3. **Explain why** - Not just what, but why it worked
4. **Use screenshots** - Visual proof is essential
5. **Proofread** - Check for typos and errors
6. **Be professional** - Formal business writing

### Don'ts ❌

1. **Don't be vague** - "I ran an exploit" is not enough
2. **Don't skip steps** - Include ALL steps
3. **Don't forget timestamps** - Date/time on screenshots
4. **Don't use automated tools output only** - Explain it
5. **Don't submit without proofreading** - Quality matters

---

## 📋 Report Checklist

Before submitting, verify:

- [ ] All machine sections completed
- [ ] Screenshots show proof.txt with hash
- [ ] Screenshots show ipconfig/whoami
- [ ] All commands documented
- [ ] Explanations are clear
- [ ] No sensitive information (your IP, VPN IP only)
- [ ] PDF format (not Word unless required)
- [ ] File size < 100MB
- [ ] Filename: OSCP-OS-XXXXX-Exam-Report.pdf
- [ ] Proofread entire document
- [ ] Exam ID on cover page

---

## 🕐 Reporting Timeline

**You have 24 hours after exam ends to submit report**

**Recommended approach:**

1. **During exam (24 hours):**
   - Take detailed notes
   - Organize screenshots immediately
   - Document commands as you go
   - Use template to fill in real-time

2. **After exam (24 hours):**
   - Sleep 4-6 hours first (seriously!)
   - Review all screenshots
   - Fill in any gaps
   - Write detailed explanations
   - Proofread 2-3 times
   - Submit with 2-3 hours to spare

---

## 🎨 Customization

### Markdown Template

**Edit these files:**
- `src/OSCP-exam-report.md` - Main report
- `src/OSCP-exam-report.yml` - Metadata (name, ID, etc.)

### Word Template

**Customize:**
- Header/Footer with your info
- Color scheme (keep professional)
- Add your logo (optional)

### LaTeX Template

**Edit YAML frontmatter:**
```yaml
---
title: "Offensive Security OSCP Exam Report"
author: "r0tn3x"
date: "December 7, 2025"
---
```

---

## 📚 Example Reports

Good examples to review:
- https://github.com/noraj/OSCP-Exam-Report-Template-Markdown/tree/master/examples
- https://github.com/whoisflynn/OSCP-Exam-Report-Template/tree/master/examples

---

## 🎯 Final Tips

1. **Start early** - Fill template during exam
2. **Be thorough** - More detail is better
3. **Stay organized** - Folders per machine
4. **Screenshot everything** - You can always delete later
5. **Professional tone** - Write for a non-technical manager
6. **Proofread** - Typos look unprofessional
7. **Submit early** - Don't wait until last minute
8. **Keep a copy** - Backup before submitting

---

## ⏰ Time Management

**Typical breakdown:**

- Documentation during exam: 2-3 hours
- Post-exam report writing: 6-8 hours
- Sleep: 6 hours (IMPORTANT!)
- Review and proofread: 2-3 hours
- Buffer time: 3-5 hours

**Don't rush! You have 24 hours for a reason.**

---

**Good luck on your exam and report!**

**Author:** r0tn3x | OSCP+ December 2025
