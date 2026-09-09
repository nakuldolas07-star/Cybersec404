# Master Roadmap v2: Zero to Paid Cybersecurity Internship (Complete A-to-Z)
### Red Team / Ethical Hacking / Network Penetration Testing Track — Fully Merged & Sequenced

This is your **single source of truth**. It merges your original 8-week plan with every gap identified from community-sourced material (Reddit r/AskNetsec, r/netsecstudents, r/oscp, Quora, Twitter/X infosec circles, PortSwigger/THM/HTB community norms). Nothing from either version is dropped — everything is placed in the order you should actually learn it. Follow it top to bottom.

Timeline note: original core (Phases 0-6) is ~8 weeks if you go hard. The added material (marked **[NEW]**) extends this to roughly **10-12 weeks** for real depth. If you must hit 8 weeks for an application deadline, use the "8-week vs 12-week" markers at the end of each phase.

---

## PHASE 0 — Setup & Ground Rules (Day 1, before anything else)

### Environment
- Install VirtualBox or VMware (free tier is fine)
- Install Kali Linux as your primary attack VM
- Download Metasploitable2 and 2-3 easy TryHackMe/HackTheBox targets as practice victims
- Create accounts: GitHub, TryHackMe, Hack The Box, LinkedIn
- **[NEW]** Also create: HackerOne and Bugcrowd accounts (dormant for now, you'll use them in Phase 6)
- Set up a notes system: Obsidian, Notion, or CherryTree — document literally everything from today onward

### Legal/Ethical Baseline (non-negotiable — learn this Day 1)
- Only attack systems you own or are explicitly authorized to test (your own VMs, TryHackMe/HTB labs, or a signed scope-of-work). Attacking anything else is a crime, not a grey area.
- Understand "scope," "rules of engagement," and "authorization" — you will be asked about this in interviews as a filter question.
- Interviewers specifically probe for whether you understand the difference between a hacker and a criminal. Knowing this cold is a credibility signal.
- **[NEW]** Extend this mindset now to every later phase: wireless attacks, social engineering, and bug bounty work all have their own scope rules — "authorized" always means something specific and written, never assumed.

---

## PHASE 1 — Unbreakable Foundations (Weeks 1-2)

You cannot hack what you don't understand. Do not rush this phase.

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
- Tools: `ping`, `traceroute`, `ifconfig`/`ipconfig`, `netstat`, `ss`, `tcpdump`, Wireshark (read a full packet capture, don't just glance at it)

### 2. Linux Fundamentals
- Navigation: `ls`, `cd`, `pwd`, `cp`, `mv`, `rm`, `find`, `locate`
- Permissions/ownership: `chmod`, `chown`, understanding rwx for user/group/other
- Text processing: `grep`, `awk`, `sed`, `cat`, `less`, `tail`, `head`
- System management: `ps`, `top`/`htop`, `kill`, `systemctl`, `apt`/`yum`
- User/group management: `useradd`, `usermod`, `passwd`, `sudo` configuration
- Bash scripting: loops, variables, if-statements — write 2-3 small automation scripts this week
- File system hierarchy: know what `/etc`, `/var`, `/tmp`, `/home`, `/bin` are for

### 3. Windows Fundamentals
- Windows architecture: registry, services, processes, threads
- CMD basics: `dir`, `cd`, `ipconfig`, `netstat`, `tasklist`, `taskkill`
- PowerShell basics: cmdlets, `Get-Help`, `Get-Command`, simple scripts
- Active Directory concepts (intro level — deeper AD comes in Phase 4b):
  - Domains, trees, forests
  - Domain Controllers (DC)
  - Users, groups, computers, Organizational Units (OUs)
  - Group Policy Objects (GPOs)
  - Authentication protocols: NTLM, Kerberos (high-level understanding is enough for now)

### Practice for this phase
TryHackMe "Network Fundamentals" + "Linux Fundamentals" (1-3) + OverTheWire "Bandit" (first 15+ levels)

**Week 1-2 checkpoint**: You can navigate Kali entirely by terminal, explain the TCP handshake and OSI model unprompted, subnet by hand, and describe what a Domain Controller does.

---

## PHASE 2 — Offensive Methodologies & Reconnaissance (Week 3)

### 4. Information Gathering (OSINT)
- Passive recon: WHOIS lookups, DNS enumeration, Google Dorking (advanced search operators)
- Search engine hacking: Shodan, Censys for exposed devices
- Subdomain enumeration: Sublist3r, Amass, assetfinder
- Web archives: Wayback Machine for old/hidden endpoints

### 5. Scanning & Enumeration (Active Recon)
- **Nmap** — master this tool:
  - Port scanning (TCP SYN `-sS`, UDP `-sU`)
  - Service version detection (`-sV`)
  - OS fingerprinting (`-O`)
  - Nmap Scripting Engine for auto vuln detection (`-sC`, `--script`)
- SMB enumeration: `enum4linux`, `smbclient` (find shares, null sessions)
- Web enumeration: directory brute-forcing with Gobuster, Dirb, Feroxbuster
- Vulnerability scanning basics: Nessus (free tier), Nikto

### Practice for this phase
Do recon-and-enumeration-only against 5-8 easy boxes before touching exploitation — this discipline (fully map before you attack) is exactly what separates "script kiddie" from someone who understands methodology, and interviewers notice the difference.

**Week 3 checkpoint**: Given a target IP with zero info, you can independently produce a clean recon report (open ports, services, versions, likely attack surface) in under 20 minutes.

---

## PHASE 3 — Exploitation & Initial Access (Weeks 4-5)

### 6. Network Penetration Testing
- Metasploit Framework:
  - Core commands (`search`, `use`, `set`, `exploit`)
  - Payloads: reverse shells, bind shells, Meterpreter
  - Post-exploitation modules
- ExploitDB / `searchsploit` — finding public exploits for identified services
- Practice against known vulnerable services: vsftpd, ProFTPd, Samba, EternalBlue/MS17-010

### 7. Web Application Hacking (OWASP Top 10) — single most important block for entry-level roles
- Burp Suite — master this: proxy setup, intercepting requests, Repeater, Intruder
- SQL Injection: error-based, union-based, blind (boolean/time-based); automate with `sqlmap` but understand it manually first
- Cross-Site Scripting (XSS): reflected, stored, DOM-based
- File Inclusion: LFI/RFI to read `/etc/passwd` or achieve code execution
- File Upload Vulnerabilities: bypassing filters to upload web shells
- Command Injection: exploiting apps that pass input to a system shell
- Authentication Bypass: default creds, logic flaws, brute-forcing with Hydra/Burp Intruder
- IDOR, CSRF, SSRF, Broken Access Control — know all 10, not just the famous 3

### 7b. **[NEW]** API Security (its own OWASP Top 10 now — don't treat as identical to web app testing)
- REST vs GraphQL basics
- Broken Object Level Authorization (BOLA) — the single most common real-world API vuln
- Tools: Postman, Burp Suite API-focused extensions, `Kiterunner` for endpoint discovery
- Rate limiting bypass; JWT attacks (`alg:none`, weak secret brute-forcing with `jwt_tool`)
- SSRF via API endpoints is a very common real-world chain into cloud credential theft (ties into Phase 4c)

### 8. Password Attacks & Cracking
- Hashing concepts: MD5, SHA family, NTLM, bcrypt — know which is "crackable fast" vs not
- Hash identification (recognize hash types before attacking them)
- Online attacks: brute-forcing SSH/FTP/web logins with Hydra
- Offline cracking: Hashcat or John the Ripper with wordlists (rockyou.txt)
- Wordlist generation: CeWL, Mentalist

**Week 4-5 checkpoint**: You've fully compromised (recon → exploit → shell) at least 10 machines across a mix of network and web-based challenges, with notes on each.

---

## PHASE 3.5 — **[NEW]** Wireless Network Attacks (Week 5, slot in alongside password attacks)

Skipped in most beginner roadmaps, then asked about in interviews anyway.

- 802.11 basics: management/control/data frames, WPA2 4-way handshake, WPA3 differences
- Tools: `aircrack-ng` suite, `Wifite`, `Kismet`, `Bettercap`
- Attacks: handshake capture + offline crack, Evil Twin / rogue AP, deauth attacks, WPS PIN attacks (Reaver)
- Concept-level only (no hardware needed yet): Bluetooth (BLE) sniffing, RFID/NFC cloning — just know what these terms mean when they come up

---

## PHASE 4 — Post-Exploitation & Privilege Escalation (Weeks 5-6)

You're in as a low-priv user. Now you become root/SYSTEM — this is what most beginners never practice, and it's a huge differentiator.

### 9. Linux Privilege Escalation
- Enumeration: LinPEAS, manual LinEnum
- Sudo misconfigurations (e.g. `sudo find`, `sudo vim` → check GTFOBins)
- SUID/SGID binary abuse
- Cron job exploitation (writable scripts run by root)
- PATH variable hijacking
- Kernel exploits (e.g. Dirty Cow) — know the concept even if you don't run every CVE

### 10. Windows Privilege Escalation
- Enumeration: WinPEAS, PowerUp
- Unquoted service paths
- Weak service permissions (modifying a service binary path)
- AlwaysInstallElevated MSI abuse
- Stored credentials in registry/config files/Credential Manager
- Token impersonation basics (RoguePotato/JuicyPotato — concept-level is fine)

### 11. Active Directory Exploitation (Intro)
- Enumeration: BloodHound + SharpHound to map attack paths
- AS-REP Roasting, Kerberoasting (extracting hashes for offline cracking)
- Lateral movement: Pass-the-Hash (PtH)
- Tooling: CrackMapExec (CME), Impacket suite (`psexec.py`, `wmiexec.py`, `secretsdump.py`)

### 11b. **[NEW]** Active Directory — Going Deeper (interviewers increasingly expect this beyond "intro")
- Delegation attacks (unconstrained/constrained/RBCD) — concept level is enough
- Golden Ticket / Silver Ticket — know what they are and why they're dangerous
- DCSync and `mimikatz` — know what it extracts and why (interview/concept topic; only run in your own lab, never outside authorized scope)
- Tooling to add: `PowerView`, `Rubeus` (concept level, real usage later)

**Week 5-6 checkpoint**: You can take a low-priv shell on a Linux or Windows box and independently escalate to root/SYSTEM on at least 5 different machines using different techniques (not the same trick every time), AND explain one delegation-based AD attack conceptually even if you haven't executed it yet.

---

## PHASE 4b — **[NEW]** Mobile Application Pentesting (Week 6-7)

- Android architecture: APK structure, Manifest, activities/intents
- Tools: `MobSF` (automated static/dynamic analysis — best starting point), `jadx` (decompiling), `apktool`, `Frida` (runtime instrumentation/hooking)
- Intercepting traffic: Burp Suite + rooted emulator or Genymotion
- OWASP Mobile Top 10 (run in parallel with the web OWASP Top 10 you already know)
- iOS: know it exists, know jailbreak-based testing is the norm — don't go deep unless you own a Mac; this is a "know the landscape" item, not a mastery item yet

---

## PHASE 4c — **[NEW]** Cloud Security Basics (Week 7)

Increasingly asked about even in junior interviews, and it's where a lot of real-world SSRF/API chains actually land (ties back to Phase 7b).

- AWS fundamentals: IAM misconfigurations, S3 bucket exposure, security groups
- Tools: `ScoutSuite`, `Prowler` (misconfiguration scanners), `Pacu` (AWS exploitation framework)
- Concepts: shared responsibility model, cloud metadata service abuse (SSRF → credential theft is one of the most common real chains today), container basics (Docker escape concepts, misconfigured Kubernetes at a high level)
- TryHackMe has a dedicated AWS/cloud track — efficient way to check this box without spinning up your own AWS bill

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
- Report writing: translate technical findings (XSS, LFI, PrivEsc) into business risk language for a non-technical audience — this is explicitly screened for by hiring managers and almost no self-taught beginner practices it
- Proof of Concept discipline: screenshot everything, capture flags as evidence

### 14. Operating Systems for Hackers
- Kali Linux — know your pre-installed toolset well enough to not need to Google basic tool locations
- Parrot OS — worth knowing exists as an alternative, not required to switch

### 15. **[NEW]** Social Engineering & Physical Security (expanded from a one-line mention)
- Phishing infrastructure concepts: `Gophish` (framework — lab/authorized use only)
- Pretexting, tailgating, USB drop concepts
- Heavily ethics-sensitive: always frame any writeup or discussion as "simulated, authorized engagement"

### 16. **[NEW]** Evasion & Defensive Awareness (know the concepts — don't weaponize)
This exists so you understand *why* defenses fail, which is a real interview differentiator:
- Signature-based vs behavioral AV/EDR detection, at a conceptual level
- Blue team basics: what a SOC analyst sees when you attack (log sources, SIEM concepts — Splunk/ELK exist by name, you don't need to operate one yet)
- Being able to say "here's what the defender would have seen" turns a technical walkthrough into a much stronger interview answer

### 17. **[NEW]** Binary/Exploit Basics (light touch only — don't over-invest before your internship)
- Buffer overflow concept (stack-based), how `EIP` gets overwritten — do ONE guided walkthrough (TryHackMe "Buffer Overflow Prep")
- `gdb`, `pwndbg` — know they exist and roughly what they're for
- This is normally a Year 2 skill; don't let it eat your application timeline

### 18. **[NEW]** Forensics/Incident Response Literacy (not your track, but interviewers test for baseline awareness)
- Know what "chain of custody" means
- Basic log analysis: reading auth logs, web server logs for indicators of compromise
- This is 2-3 hours of reading, not a phase — you are not becoming a forensics analyst

---

## PHASE 6 — Portfolio, Certs, and Career Assets (Weeks 7-8, built continuously from Week 2)

### Portfolio deliverables
- Public writeups: one per completed box (methodology: recon → findings → exploitation → priv esc → impact → fix). Publish on GitHub or a simple blog.
- One polished vulnerability report written like a real client deliverable — this single artifact often outweighs a whole resume in interviews.
- 1-2 original scripts (a recon automation tool, a basic scanner) — shows initiative beyond following tutorials.
- **[NEW]** One bug bounty writeup (see below) — public, real-world validation carries more weight than another lab box.

### **[NEW]** Bug Bounty as a Parallel Track
- Platforms: HackerOne, Bugcrowd — even a zero-payout, valid finding is portfolio gold
- Start with wide-scope, low-competition programs, including Vulnerability Disclosure Programs (VDPs, no bounty but still real-world and citable)
- A single public bug bounty report demonstrates you can find real vulns, not just solve pre-built labs

### Certification/credential (pick one based on time/budget)
- TryHackMe Jr Penetration Tester path certificate (cheapest, matches this roadmap directly)
- CompTIA Security+ (recognized by HR/ATS filters, needs dedicated study time)
- eJPT by INE (~$200, hands-on, well-regarded specifically for pentest roles)
- **[NEW] PNPT (TCM Security)** — increasingly recommended alongside eJPT/THM Jr Pentester; cheaper than OSCP and includes a real reporting component that matches your Phase 6 portfolio goal directly
- **[NEW] CRTP (Altered Security)** — the community-standard "next step" after AD basics if you want a red-team-flavored cert
- If budget-constrained: skip the paid exam, list it as "in progress," lean harder on the portfolio
- **Note on OSCP**: it's the long-term goal almost everyone mentions, but community consensus is clear — don't attempt it before this roadmap. Do it 3-6 months later, once fundamentals are automatic.

### Resume & LinkedIn
- Resume rebuild: lead with labs/projects framed like real engagements, not "I'm a student with no experience." List THM/HTB stats, writeup links, GitHub, any CTF placements, and your bug bounty finding if you have one.
- LinkedIn: active profile, headline reflecting your direction (e.g. "Aspiring Penetration Tester | OWASP Top 10 | TryHackMe Top X%"), weekly progress posts starting Week 3-4, not Week 7.

### **[NEW]** Communities — Join From Day 1, Not Week 7
- **Reddit**: r/AskNetsec, r/netsecstudents, r/oscp, r/HowToHack
- **Discord**: TryHackMe official Discord, HackTheBox official Discord — both have active "career" and "help" channels
- **Twitter/X**: search hashtags `#infosec`, `#OSCP`, `#bugbountytips` rather than following one fixed list of accounts, since this space moves fast
- **Quora search worth doing**: "How did you get your first pentest internship with no experience" — the recurring answer pattern always matches this roadmap: public writeups + one polished report + active community presence

### **[NEW]** Interview Prep Specifics
- Be ready to whiteboard the TCP 3-way handshake AND narrate a full attack chain (recon → exploit → privesc → impact) verbally, not just execute it hands-on
- Have GTFOBins / LOLBAS knowledge sharp — these come up as rapid-fire interview questions
- Practice explaining ONE of your writeups in under 3 minutes — interviewers care more about methodology narration than the specific CVE name

---

## Full Sequence at a Glance

| Phase | Topic | When |
|---|---|---|
| 0 | Setup + Ethics/Legal baseline | Day 1 |
| 1 | Networking, Linux, Windows fundamentals | Weeks 1-2 |
| 2 | OSINT, Scanning, Enumeration | Week 3 |
| 3 | Network exploitation, Web (OWASP 10), API security, Password attacks | Weeks 4-5 |
| 3.5 | Wireless attacks | Week 5 |
| 4 | Linux/Windows PrivEsc, AD intro, AD deeper | Weeks 5-6 |
| 4b | Mobile pentesting | Weeks 6-7 |
| 4c | Cloud security | Week 7 |
| 5 | Scripting, docs/reporting, social engineering, evasion/blue-team awareness, binary basics, forensics literacy | Parallel, Weeks 2-8 |
| 6 | Portfolio, bug bounty, certs, resume/LinkedIn, communities, interview prep | Weeks 7-8, built continuously from Week 2 |

**Compressed 8-week version**: run Phases 0-4 and 5/6 exactly as your original plan, and treat 3.5, 4b, 4c, and Phase 5's new items (15-18) as *single-session reading + one lab each*, not mastery — bookmark full depth on those for immediately after you land the internship.

**Full 10-12 week version**: give each [NEW] block its own 2-4 day slot as written above — this is the version that leaves genuinely no concept uncovered.
