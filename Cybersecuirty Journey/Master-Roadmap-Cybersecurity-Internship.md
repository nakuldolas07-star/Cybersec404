# The Complete Ethical Hacker Roadmap: Zero to Elite
### Red Team / Penetration Testing / Offensive Security — Full Skill Progression

This roadmap is organized by **skill tier**, not by calendar time — progress when you've actually mastered a tier's checkpoint, not on a schedule. Every concept is sequenced so each tier builds directly on the last. Nothing is skipped.

---

## TIER 0 — Setup & Non-Negotiable Ground Rules

### Environment
- Install VirtualBox or VMware
- Install Kali Linux as your primary attack VM
- Download Metasploitable2 and 2-3 easy TryHackMe/HackTheBox targets as practice victims
- Create accounts: GitHub, TryHackMe, Hack The Box
- Set up a notes system: Obsidian, Notion, or CherryTree — document literally everything from day one

### Legal & Ethical Baseline (learn this before anything else)
- Only attack systems you own or are explicitly authorized to test (your own VMs, TryHackMe/HTB labs, or a signed scope-of-work). Attacking anything else is a crime, not a grey area.
- Understand what "scope," "rules of engagement," and "authorization" mean in a real engagement.
- This mindset applies to every tier below — wireless attacks, social engineering, and real-world testing all have their own scope rules. "Authorized" always means something specific and written, never assumed.
- Knowing the line between a hacker and a criminal cold, and being able to articulate it, is foundational to being taken seriously in this field at any level.

---

## TIER 1 — Unbreakable Foundations

You cannot hack what you don't understand. Do not rush this tier no matter how tempting it is to jump to "real hacking."

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
- Permissions/ownership: `chmod`, `chown`, rwx for user/group/other
- Text processing: `grep`, `awk`, `sed`, `cat`, `less`, `tail`, `head`
- System management: `ps`, `top`/`htop`, `kill`, `systemctl`, `apt`/`yum`
- User/group management: `useradd`, `usermod`, `passwd`, `sudo` configuration
- Bash scripting: loops, variables, if-statements — write several small automation scripts
- File system hierarchy: `/etc`, `/var`, `/tmp`, `/home`, `/bin`

### 3. Windows Fundamentals
- Windows architecture: registry, services, processes, threads
- CMD basics: `dir`, `cd`, `ipconfig`, `netstat`, `tasklist`, `taskkill`
- PowerShell basics: cmdlets, `Get-Help`, `Get-Command`, simple scripts
- Active Directory concepts (intro level — deeper AD comes in Tier 4):
  - Domains, trees, forests
  - Domain Controllers (DC)
  - Users, groups, computers, Organizational Units (OUs)
  - Group Policy Objects (GPOs)
  - Authentication protocols: NTLM, Kerberos (high-level understanding for now)

### Practice
TryHackMe "Network Fundamentals" + "Linux Fundamentals" (1-3) + OverTheWire "Bandit" (first 15+ levels)

**Tier 1 checkpoint**: You can navigate Kali entirely by terminal, explain the TCP handshake and OSI model unprompted, subnet by hand, and describe what a Domain Controller does.

---

## TIER 2 — Offensive Methodology & Reconnaissance

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

### Practice
Do recon-and-enumeration-only against 5-8 easy boxes before touching exploitation — fully mapping a target before attacking is exactly what separates real methodology from guesswork.

**Tier 2 checkpoint**: Given a target IP with zero info, you can independently produce a clean recon report (open ports, services, versions, likely attack surface) in under 20 minutes.

---

## TIER 3 — Exploitation & Initial Access

### 6. Network Penetration Testing
- Metasploit Framework:
  - Core commands (`search`, `use`, `set`, `exploit`)
  - Payloads: reverse shells, bind shells, Meterpreter
  - Post-exploitation modules
- ExploitDB / `searchsploit` — finding public exploits for identified services
- Practice against known vulnerable services: vsftpd, ProFTPd, Samba, EternalBlue/MS17-010

### 7. Web Application Hacking — OWASP Top 10 (the single most important skill block in this entire roadmap)
- Burp Suite — master this: proxy setup, intercepting requests, Repeater, Intruder
- SQL Injection: error-based, union-based, blind (boolean/time-based); automate with `sqlmap` but understand it manually first
- Cross-Site Scripting (XSS): reflected, stored, DOM-based
- File Inclusion: LFI/RFI to read `/etc/passwd` or achieve code execution
- File Upload Vulnerabilities: bypassing filters to upload web shells
- Command Injection: exploiting apps that pass input to a system shell
- Authentication Bypass: default creds, logic flaws, brute-forcing with Hydra/Burp Intruder
- IDOR, CSRF, SSRF, Broken Access Control — know all 10, not just the famous 3

### 8. API Security (its own discipline now, not identical to general web testing)
- REST vs GraphQL basics
- Broken Object Level Authorization (BOLA) — the single most common real-world API vuln
- Tools: Postman, Burp Suite API extensions, `Kiterunner` for endpoint discovery
- Rate limiting bypass; JWT attacks (`alg:none`, weak secret brute-forcing with `jwt_tool`)
- SSRF via API endpoints is a very common chain into cloud credential theft (ties into Tier 5)

### 9. Password Attacks & Cracking
- Hashing concepts: MD5, SHA family, NTLM, bcrypt — know which is "crackable fast" vs not
- Hash identification before attacking
- Online attacks: brute-forcing SSH/FTP/web logins with Hydra
- Offline cracking: Hashcat or John the Ripper with wordlists (rockyou.txt)
- Wordlist generation: CeWL, Mentalist

### 10. Wireless Network Attacks
- 802.11 basics: management/control/data frames, WPA2 4-way handshake, WPA3 differences
- Tools: `aircrack-ng` suite, `Wifite`, `Kismet`, `Bettercap`
- Attacks: handshake capture + offline crack, Evil Twin / rogue AP, deauth attacks, WPS PIN attacks (Reaver)
- Concept-level (hardware not required yet): Bluetooth (BLE) sniffing, RFID/NFC cloning

**Tier 3 checkpoint**: You've fully compromised (recon → exploit → shell) at least 10-15 machines across a mix of network, web, and wireless-based challenges, with notes on each.

---

## TIER 4 — Post-Exploitation, Privilege Escalation & Active Directory

You're in as a low-priv user. Now you become root/SYSTEM — this is where most self-taught people stop practicing, and it's a massive skill differentiator.

### 11. Linux Privilege Escalation
- Enumeration: LinPEAS, manual LinEnum
- Sudo misconfigurations (e.g. `sudo find`, `sudo vim` → check GTFOBins)
- SUID/SGID binary abuse
- Cron job exploitation (writable scripts run by root)
- PATH variable hijacking
- Kernel exploits (e.g. Dirty Cow) — know the concept even if you don't run every CVE

### 12. Windows Privilege Escalation
- Enumeration: WinPEAS, PowerUp
- Unquoted service paths
- Weak service permissions (modifying a service binary path)
- AlwaysInstallElevated MSI abuse
- Stored credentials in registry/config files/Credential Manager
- Token impersonation basics (RoguePotato/JuicyPotato — concept-level is fine here)

### 13. Active Directory Exploitation — Foundations
- Enumeration: BloodHound + SharpHound to map attack paths
- AS-REP Roasting, Kerberoasting (extracting hashes for offline cracking)
- Lateral movement: Pass-the-Hash (PtH)
- Tooling: CrackMapExec (CME), Impacket suite (`psexec.py`, `wmiexec.py`, `secretsdump.py`)

### 14. Active Directory Exploitation — Advanced
- Delegation attacks (unconstrained/constrained/RBCD)
- Golden Ticket / Silver Ticket — know what they are, why they're dangerous, and how they're detected
- DCSync and `mimikatz` — know exactly what's extracted and why (run only in your own authorized lab)
- Tooling: `PowerView`, `Rubeus`
- Trust relationship abuse across domains/forests — concept level, this is genuinely elite-tier material

**Tier 4 checkpoint**: You can take a low-priv shell on a Linux or Windows box and independently escalate to root/SYSTEM on at least 5-8 different machines using different techniques each time, and you can explain (and, in your own lab, execute) at least one advanced AD attack chain end to end.

---

## TIER 5 — Specialized Attack Surfaces

### 15. Mobile Application Pentesting
- Android architecture: APK structure, Manifest, activities/intents
- Tools: `MobSF` (automated static/dynamic analysis), `jadx` (decompiling), `apktool`, `Frida` (runtime instrumentation/hooking)
- Intercepting traffic: Burp Suite + rooted emulator or Genymotion
- OWASP Mobile Top 10 (run in parallel with the web OWASP Top 10)
- iOS: jailbreak-based testing is the standard approach — go deeper here if you have a Mac available

### 16. Cloud Security
- AWS fundamentals: IAM misconfigurations, S3 bucket exposure, security groups
- Tools: `ScoutSuite`, `Prowler` (misconfiguration scanners), `Pacu` (AWS exploitation framework)
- Concepts: shared responsibility model, cloud metadata service abuse (SSRF → credential theft is one of the most common real-world chains today), container basics (Docker escape concepts, misconfigured Kubernetes)
- Azure and GCP equivalents — worth knowing the landscape exists even if AWS is your primary focus

### 17. Binary Exploitation & Reverse Engineering
- Buffer overflow concept (stack-based), how `EIP`/`RIP` gets overwritten, ASLR/DEP/stack canaries as mitigations
- Tools: `gdb`, `pwndbg`, `ghidra`, `IDA Free`
- Format string vulnerabilities, basic ROP (Return-Oriented Programming) chains
- This is a genuinely deep specialization — most generalist pentesters only go conceptually deep here, but elite-level offensive security requires real fluency in this tier

### 18. Exploit Development & Malware Concepts
- Understanding how public exploits (from ExploitDB) are constructed, not just how to run them
- Shellcoding basics
- Antivirus/EDR evasion concepts: signature-based vs behavioral detection, why obfuscation and living-off-the-land techniques work
- **Important boundary**: this tier is about understanding offense deeply enough to defend and to operate within authorized red-team engagements — not about building tools to use outside authorized scope

---

## TIER 6 — Professional Craft (Runs Continuously Alongside Every Tier Above)

### 19. Scripting & Automation
- Python: custom port scanners, API interaction, JSON/XML parsing, exploit PoC scripting
- Bash: automate Nmap scans, parse output
- PowerShell: AD enumeration scripts, offensive tooling
- Git/GitHub: commit, push, branch, write real documentation — your work lives here

### 20. Documentation & Reporting
- Markdown for clean notes
- Note-taking discipline: log every command, every "aha," every failure — failures make the best writeup material because they show real methodology
- Report writing: translate technical findings into business risk language for a non-technical audience — this single skill separates a technician from a true security professional
- Proof of Concept discipline: screenshot everything, capture evidence properly

### 21. Social Engineering & Physical Security
- Phishing infrastructure concepts: `Gophish` (framework — authorized lab use only)
- Pretexting, tailgating, USB drop concepts
- Always simulated and authorized — this is the most trust-sensitive skill in the entire field

### 22. Defensive & Blue Team Awareness
- Signature-based vs behavioral AV/EDR detection, conceptually
- What a SOC analyst sees when you attack: log sources, SIEM concepts (Splunk/ELK by name)
- Understanding detection is what elevates offensive work from "breaking things" to genuine security expertise — elite operators think like defenders

### 23. Forensics & Incident Response Literacy
- Chain of custody concept
- Basic log analysis: reading auth logs, web server logs for indicators of compromise
- Not a specialization to master, but baseline literacy every well-rounded offensive practitioner should have

### 24. Operating Systems for Offensive Work
- Kali Linux — know your pre-installed toolset well enough to not need to Google basic tool locations
- Parrot OS — worth knowing as an alternative

---

## TIER 7 — Continuous Mastery (No Ceiling — This Is the "Elite" Layer)

Elite-level skill in this field isn't a destination, it's an ongoing practice. This tier never "completes" — it's how you keep sharpening after everything above is second nature.

- **Original research**: read and reproduce recent CVEs and public disclosures to understand novel vulnerability classes as they emerge
- **CTF competitions**: regularly compete in live CTFs (not just static labs) — this is where real-time, adversarial-pressure skill is built
- **Contribute to open-source security tools**: submitting to or building tools used by the community (Impacket, BloodHound, custom Burp extensions, etc.) is a marker of genuine depth
- **Deep-dive one specialization**: pick one of AD attacks, binary exploitation, cloud security, or mobile security and go past "competent" into genuine expert depth in that one area
- **Teach**: writing detailed technical breakdowns of attacks (blogs, conference talks, detailed writeups) forces a level of understanding that solo practice never does
- **Stay current continuously**: this field changes fast — new CVEs, new cloud misconfig classes, new evasion techniques appear constantly, and elite practitioners treat ongoing learning as permanent, not a phase they finish

---

## Full Sequence at a Glance

| Tier | Focus |
|---|---|
| 0 | Setup, legal/ethical baseline |
| 1 | Networking, Linux, Windows fundamentals |
| 2 | OSINT, scanning, enumeration |
| 3 | Network exploitation, web (OWASP 10), API security, password attacks, wireless attacks |
| 4 | Linux/Windows privilege escalation, AD foundations, AD advanced |
| 5 | Mobile pentesting, cloud security, binary exploitation, exploit development |
| 6 | Scripting, reporting, social engineering, blue-team awareness, forensics literacy — runs alongside every other tier |
| 7 | Continuous mastery: original research, live CTFs, open-source contribution, deep specialization, teaching |

Progress tier by tier, but treat Tier 6 as always-on rather than something you do once and move past. There is no true "finish line" at Tier 7 — that's the point of calling it elite.
