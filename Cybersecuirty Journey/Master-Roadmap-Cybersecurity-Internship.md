# Master Roadmap: Zero to Paid Cybersecurity Internship (8 Weeks)
### Red Team / Ethical Hacking / Network Penetration Testing Track

This merges the full technical skill list with the career-side actions (portfolio, resume, applying) so you have one document to execute against, in order, with nothing skipped.

---

## PHASE 0 — Setup & Ground Rules (Day 1, before Week 1 starts)

**Environment:**
- Install VirtualBox or VMware (free)
- Install **Kali Linux** as your primary attack VM
- Download **Metasploitable2** and 2-3 easy TryHackMe/HackTheBox targets as practice victims
- Create accounts: GitHub, TryHackMe, Hack The Box, LinkedIn (if you don't have these already)
- Set up a notes system: **Obsidian**, **Notion**, or **CherryTree** — you will document literally everything from today onward

**Legal/Ethical baseline (non-negotiable, learn this Day 1):**
- Only attack systems you own or are explicitly authorized to test (your own VMs, TryHackMe/HTB labs, or a signed scope-of-work). Attacking anything else is a crime, not a grey area.
- Understand what "scope," "rules of engagement," and "authorization" mean in a real pentest — you'll be asked about this in interviews as a filter question.
- This isn't just legal CYA — internship interviewers specifically probe for whether you understand the difference between a hacker and a criminal. Knowing this cold is a credibility signal.

---

## PHASE 1 — Unbreakable Foundations (Weeks 1-2)

*You cannot hack what you don't understand. Do not rush this phase.*

### 1. Computer Networking
- OSI Model & TCP/IP Model — what happens at every layer, not just names
- IP addressing: IPv4, IPv6, subnetting (CIDR), public vs private IPs, NAT
- Protocols in depth:
  - TCP vs UDP (handshakes, statefulness)
  - HTTP/HTTPS (requests/responses, status codes, headers, cookies)
  - DNS (resolution process, record types: A, CNAME, MX, TXT)
  - DHCP (IP assignment)
  - SSH, FTP, SFTP, Telnet
  - SMB (critical for Windows environments)
  - RDP
- Network architecture: routers, switches, firewalls, VPNs, proxies, DMZ
- Tools to get comfortable with: `ping`, `traceroute`, `ifconfig`/`ipconfig`, `netstat`, `ss`, `tcpdump`, **Wireshark** (read a full packet capture, don't just glance at it)

### 2. Linux Fundamentals
- Navigation: `ls`, `cd`, `pwd`, `cp`, `mv`, `rm`, `find`, `locate`
- Permissions/ownership: `chmod`, `chown`, understanding `rwx` for user/group/other
- Text processing: `grep`, `awk`, `sed`, `cat`, `less`, `tail`, `head`
- System management: `ps`, `top`/`htop`, `kill`, `systemctl`, `apt`/`yum`
- User/group management: `useradd`, `usermod`, `passwd`, `sudo` configuration
- Bash scripting: loops, variables, if-statements — write 2-3 small automation scripts this week
- File system hierarchy: know what `/etc`, `/var`, `/tmp`, `/home`, `/bin` are for

### 3. Windows Fundamentals
- Windows architecture: registry, services, processes, threads
- CMD basics: `dir`, `cd`, `ipconfig`, `netstat`, `tasklist`, `taskkill`
- PowerShell basics: cmdlets, `Get-Help`, `Get-Command`, simple scripts
- **Active Directory concepts (critical for Red Team):**
  - Domains, trees, forests
  - Domain Controllers (DC)
  - Users, groups, computers, Organizational Units (OUs)
  - Group Policy Objects (GPOs)
  - Authentication protocols: NTLM, Kerberos (high-level understanding is enough for now)

**Practice for this phase:** TryHackMe "Network Fundamentals" + "Linux Fundamentals" (1-3) + OverTheWire "Bandit" (first 15+ levels)

**Week 1-2 checkpoint:** You can navigate Kali entirely by terminal, explain the TCP handshake and OSI model unprompted, subnet by hand, and describe what a Domain Controller does.

---

## PHASE 2 — Offensive Methodologies & Reconnaissance (Week 3)

### 4. Information Gathering (OSINT)
- Passive recon: WHOIS lookups, DNS enumeration, Google Dorking (advanced search operators)
- Search engine hacking: **Shodan**, **Censys** for exposed devices
- Subdomain enumeration: `Sublist3r`, `Amass`, `assetfinder`
- Web archives: Wayback Machine for old/hidden endpoints

### 5. Scanning & Enumeration (Active Recon)
- **Nmap — master this tool:**
  - Port scanning (TCP SYN `-sS`, UDP `-sU`)
  - Service version detection (`-sV`)
  - OS fingerprinting (`-O`)
  - Nmap Scripting Engine for auto vuln detection (`-sC`, `--script`)
- SMB enumeration: `enum4linux`, `smbclient` (find shares, null sessions)
- Web enumeration: directory brute-forcing with `Gobuster`, `Dirb`, `Feroxbuster`
- Vulnerability scanning basics: Nessus (free tier), Nikto

**Practice for this phase:** Do recon-and-enumeration-only against 5-8 easy boxes before touching exploitation — this discipline (fully map before you attack) is exactly what separates "script kiddie" from someone who understands methodology, and interviewers notice the difference.

**Week 3 checkpoint:** Given a target IP with zero info, you can independently produce a clean recon report (open ports, services, versions, likely attack surface) in under 20 minutes.

---

## PHASE 3 — Exploitation & Initial Access (Weeks 4-5)

### 6. Network Penetration Testing
- **Metasploit Framework:**
  - Core commands (`search`, `use`, `set`, `exploit`)
  - Payloads: reverse shells, bind shells, Meterpreter
  - Post-exploitation modules
- ExploitDB / `searchsploit` — finding public exploits for identified services
- Practice against known vulnerable services: vsftpd, ProFTPd, Samba, EternalBlue/MS17-010

### 7. Web Application Hacking (OWASP Top 10) — single most important block for entry-level roles
- **Burp Suite — master this:** proxy setup, intercepting requests, Repeater, Intruder
- **SQL Injection:** error-based, union-based, blind (boolean/time-based); automate with `sqlmap` but understand it manually first
- **Cross-Site Scripting (XSS):** reflected, stored, DOM-based
- **File Inclusion:** LFI/RFI to read `/etc/passwd` or achieve code execution
- **File Upload Vulnerabilities:** bypassing filters to upload web shells
- **Command Injection:** exploiting apps that pass input to a system shell
- **Authentication Bypass:** default creds, logic flaws, brute-forcing with Hydra/Burp Intruder
- **IDOR, CSRF, SSRF, Broken Access Control** — the OWASP items most lists forget to name explicitly; know all 10, not just the famous 3

### 8. Password Attacks & Cracking
- Hashing concepts: MD5, SHA family, NTLM, bcrypt — know which is "crackable fast" vs not
- Hash identification (recognizing hash types before attacking them)
- Online attacks: brute-forcing SSH/FTP/web logins with **Hydra**
- Offline cracking: **Hashcat** or **John the Ripper** with wordlists (`rockyou.txt`)
- Wordlist generation: `CeWL`, `Mentalist`

**Week 4-5 checkpoint:** You've fully compromised (recon → exploit → shell) at least 10 machines across a mix of network and web-based challenges, with notes on each.

---

## PHASE 4 — Post-Exploitation & Privilege Escalation (Weeks 5-6)

*You're in as a low-priv user. Now you become root/SYSTEM — this is what most beginners never practice, and it's a huge differentiator.*

### 9. Linux Privilege Escalation
- Enumeration: **LinPEAS**, manual `LinEnum`
- Sudo misconfigurations (e.g. `sudo find`, `sudo vim` → check **GTFOBins**)
- SUID/SGID binary abuse
- Cron job exploitation (writable scripts run by root)
- PATH variable hijacking
- Kernel exploits (e.g. Dirty Cow) — know the concept even if you don't run every CVE

### 10. Windows Privilege Escalation
- Enumeration: **WinPEAS**, **PowerUp**
- Unquoted service paths
- Weak service permissions (modifying a service binary path)
- AlwaysInstallElevated MSI abuse
- Stored credentials in registry/config files/Credential Manager
- Token impersonation basics (RoguePotato/JuicyPotato — concept-level is fine)

### 11. Active Directory Exploitation (Intro)
- Enumeration: **BloodHound** + **SharpHound** to map attack paths
- AS-REP Roasting, Kerberoasting (extracting hashes for offline cracking)
- Lateral movement: Pass-the-Hash (PtH)
- Tooling: **CrackMapExec (CME)**, **Impacket** suite (`psexec.py`, `wmiexec.py`, `secretsdump.py`)

**Week 5-6 checkpoint:** You can take a low-priv shell on a Linux or Windows box and independently escalate to root/SYSTEM on at least 5 different machines using different techniques (not the same trick every time).

---

## PHASE 5 — Professional Skills (Runs in Parallel From Week 2 Onward)

### 12. Scripting & Automation
- Python: custom port scanners, API interaction, JSON/XML parsing
- Bash: automate Nmap scans, parse output
- PowerShell: basic reverse shells, AD enumeration scripts
- Git/GitHub basics: commit, push, branch, write a real README — your portfolio lives here

### 13. Documentation & Reporting
- Markdown for clean notes
- Note-taking discipline: log every command, every "aha," every failure (failures make the best writeup material — they show real methodology, not luck)
- **Report writing:** translate technical findings (XSS, LFI, PrivEsc) into business risk language for a non-technical audience — this is a skill hiring managers explicitly screen for and almost no self-taught beginner practices
- Proof of Concept discipline: screenshot everything, capture flags as evidence

### 14. Operating Systems for Hackers
- Kali Linux — know your pre-installed toolset well enough to not need to Google basic tool locations
- Parrot OS — worth knowing exists as an alternative, not required to switch

---

## PHASE 6 — Portfolio, Certs, and Career Assets (Weeks 6-7, built continuously from Week 2)

- **Public writeups:** one per completed box (methodology: recon → findings → exploitation → priv esc → impact → fix). Publish on GitHub or a simple blog.
- **One polished vulnerability report** written like a real client deliverable — this single artifact often outweighs a whole resume in interviews.
- **1-2 original scripts** (a recon automation tool, a basic scanner) — shows initiative beyond following tutorials.
- **Certification/credential (pick one based on time/budget):**
  - TryHackMe Jr Penetration Tester path certificate (cheapest, matches this roadmap directly)
  - CompTIA Security+ (recognized by HR/ATS filters, needs dedicated study time)
  - eJPT by INE (~$200, hands-on, well-regarded specifically for pentest roles)
  - If budget-constrained: skip the paid exam, list it as "in progress," lean harder on the portfolio
- **Resume rebuild:** lead with labs/projects framed like real engagements, not "I'm a student with no experience." List THM/HTB stats, writeup links, GitHub, any CTF placements.
- **LinkedIn:** active profile, headline reflecting your direction (e.g. "Aspiring Penetration Tester | OWASP Top 10 | TryHackMe Top X%"), weekly progress posts starting Week 3-4, not Week 7.

---

## PHASE 7 — The Hunt: Applying With Intent (Weeks 7-8)

- **Where to look:** LinkedIn (filter Internship, past week), company career pages directly (MSSPs and small/mid consultancies are far more likely to take a raw beginner than big tech), CyberSecJobs.com, InfoSec-Jobs.com
- **Warm outreach beats cold applications:** message real people in the industry with your GitHub/writeups attached — a specific, non-generic message converts far better than volume alone
- **Volume target:** 5-10 tailored applications/day, resume keywords matched to each posting's ATS filter
- **Bug bounty (optional but high-signal):** even one valid low-severity report on HackerOne/Bugcrowd is a strong talking point
- **Interview prep:**
  - Be ready to walk through 3-4 of your best boxes methodology-first, out loud, unscripted
  - Know OWASP Top 10 cold with concrete examples
  - Prepare for: "Why cybersecurity?" / "Walk me through testing a web app you've never seen" / "Tell me about a time you got stuck and how you solved it"
  - Be upfront about being early-career — internships exist to hire people still learning; demonstrated hands-on effort is what actually gets you hired

---

## DAILY EXECUTION SCHEDULE (repeat this structure daily, adjust content per week)

| Time Block | Activity |
|---|---|
| Hours 1-2 | Theory: docs, videos, TryHackMe learning-path material — understand *why*, not just *how* |
| Hours 2-4 (or more) | Hands-on labs — struggle for 30-45 min before checking a hint, never skip straight to walkthroughs |
| Final 30-60 min | Documentation: write notes, update your cheat sheet, publish a writeup if you finished something today |
| Weekly (30 min) | LinkedIn progress post + resume/portfolio update |

---

## QUICK-REFERENCE TOOL LIST (expanded)

| Category | Tools |
|---|---|
| Recon/OSINT | Shodan, Censys, Sublist3r, Amass, assetfinder, WHOIS, Wayback Machine |
| Scanning/Enum | Nmap, enum4linux, smbclient, Gobuster, Dirb, Feroxbuster, Nikto, Nessus |
| Exploitation | Metasploit, searchsploit/ExploitDB, sqlmap |
| Web App | Burp Suite, OWASP Top 10 methodology |
| Password Attacks | Hydra, Hashcat, John the Ripper, CeWL, Mentalist |
| Linux PrivEsc | LinPEAS, LinEnum, GTFOBins |
| Windows PrivEsc | WinPEAS, PowerUp |
| Active Directory | BloodHound, SharpHound, CrackMapExec, Impacket suite |
| Traffic Analysis | Wireshark, tcpdump |
| Practice Platforms | TryHackMe, HackTheBox, OverTheWire, picoCTF |
| Docs/Notes | Obsidian, Notion, CherryTree |

---

## THINGS THAT QUIETLY KILL YOUR CHANCES

- Tutorial hell — watching walkthroughs without struggling first
- No writeups/portfolio — unverifiable claims mean nothing to interviewers
- Generic, un-tailored applications sent in bulk
- Skipping networking fundamentals to "get to the hacking part" faster
- Waiting to feel "ready" before applying — start applying in Week 5-6, in parallel with learning, not after

---
