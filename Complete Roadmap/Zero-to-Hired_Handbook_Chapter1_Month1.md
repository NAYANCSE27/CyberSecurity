# Zero-to-Hired Cybersecurity Roadmap (Version 2026)
### A Complete 6-Month Handbook

---

# Chapter 1 — Month 1: Build the Foundation

Theme of the month: **You are not learning to hack. You are learning to operate.**
Every elite SOC analyst, pentester, and detection engineer started exactly where you are — comfortable with a computer, uncomfortable with a terminal. Month 1 fixes that permanently.

---

## Week 1 — Becoming Comfortable with Computers Like a Security Professional

### Week 1 Overview

**Theme**
Everything in cybersecurity starts with understanding how computers actually work.
This week is not about hacking.
This week is about becoming comfortable using Linux, Windows, networking, Git, and your home lab.

Think of yourself as an apprentice mechanic.
A Formula 1 driver doesn't start by driving at 300 km/h.
They first understand the engine.
Cybersecurity works exactly the same way.

**Week 1 Objectives**

By the end of Week 1 you should be able to:

```
✅ Install and configure your cybersecurity lab
✅ Navigate Linux entirely from the terminal
✅ Understand files, permissions and processes
✅ Understand how computers communicate
✅ Capture packets using Wireshark
✅ Create your first professional GitHub repository
```

**Success Criteria**

At the end of this week, you should confidently answer these questions:

```
- What happens when you type google.com into your browser?
- What is the difference between a process and a service?
- Why is Linux permission 755 different from 777?
- How does DHCP assign an IP address?
- How does DNS resolve a domain?
- How do you analyze packets using Wireshark?
- How do you document your work professionally?
```

If you cannot answer these without searching Google, repeat the relevant day's labs before moving on.

**Week 1 Resources**

Primary Platform
```
TryHackMe (Free)
Rooms:
- Pre Security
- Introduction to Cyber Security
- Linux Fundamentals Part 1
```

Secondary
```
Cisco Skills For All
- Networking Basics
```

Practice Platform
```
OverTheWire
- Bandit, Levels 0–5
```

Documentation
```
- Linux man pages
- GitHub Docs
- Microsoft Learn (Windows)
```

**Week 1 Daily Schedule**

Every day follows the same structure.

```
Hour 1 — Core Concept          (video/reading, handwritten notes)
Hour 2 — Hands-on Lab          (build/practice/execute)
Hour 3 — Documentation + Notes + GitHub commit
```

---

### DAY 1

**Goal**
Build your cybersecurity workspace.

**Hour 1 — Core Concept**

Watch (45–60 min): TryHackMe → **Pre Security**

Sections:
```
- What is Cyber Security?
- Offensive vs Defensive Security
- Career Paths
- CIA Triad
```

Take handwritten notes. Do not copy the slides.

**Hour 2 — Lab**

Install everything.

Required software:
```
VirtualBox
Git
GitHub Desktop (optional)
VS Code
Wireshark
Nmap
Python 3
7-Zip
Notepad++
Windows Terminal
```

If using Kali as your primary VM, ensure:
```
sudo apt update
sudo apt full-upgrade -y
```

Verify installations:
```
python3 --version
git --version
nmap --version
```

Create GitHub repositories:
```
cybersecurity-roadmap
cybersecurity-notes
cybersecurity-home-lab
```

**Hour 3 — Documentation**

Write your first README.

Example structure:
```
Who am I?
Why Cybersecurity?
Learning Goal
Current Skills
Daily Progress Log
Resources
Projects
```

Commit:
```
git add .
git commit -m "Day 1 Completed"
git push
```

**Deliverable**
GitHub Repository #1 — `cybersecurity-roadmap` initialized with README.

---

### DAY 2

**Goal**
Linux File System.

**Hour 1 — Core Concept**

THM: **Linux Fundamentals Part 1**

Topics:
```
pwd
ls
cd
mkdir
touch
rm
cp
mv
cat
less
head
tail
```

**Hour 2 — Lab**

Open Kali terminal. Create this structure:
```
mkdir CyberLab
cd CyberLab
mkdir notes
mkdir scripts
mkdir reports
mkdir projects
mkdir logs
```

Practice:
```
cp
mv
rm
find
locate
tree
```

Install:
```
sudo apt install tree
```

Run and screenshot the output of:
```
tree CyberLab
```

**Hour 3 — Documentation**

Create:
```
linux-cheatsheet.md
```

Document every command using this pattern:
```
Command: pwd
Purpose:
Example:
Output:
```

Commit:
```
git add .
git commit -m "Linux Filesystem Completed"
git push
```

**Deliverable**
`linux-cheatsheet.md` with 12+ documented commands, pushed to `cybersecurity-notes`.

---

### DAY 3

**Goal**
Linux Permissions & Ownership.

**Hour 1 — Core Concept**

THM: **Linux Fundamentals Part 1** (continued) — Permissions section.

Topics:
```
rwx notation
Octal notation (755, 644, 777)
chmod
chown
chgrp
sudo vs root
```

**Hour 2 — Lab**

Create test files and practice permission changes:
```
cd CyberLab
touch secretfile.txt
chmod 700 secretfile.txt
ls -l secretfile.txt

chmod 755 secretfile.txt
ls -l secretfile.txt

chmod 777 secretfile.txt
ls -l secretfile.txt
```

Answer for yourself, in writing, before moving on:
```
Why is 777 dangerous on a real system?
What does the 3rd digit in 754 control?
What's the difference between chmod and chown?
```

Create a second user and test access:
```
sudo adduser testuser
su testuser
cd /home/kali/CyberLab
cat secretfile.txt   (observe permission denied/allowed based on your chmod setting)
exit
```

**Hour 3 — Documentation**

Add a "Permissions" section to `linux-cheatsheet.md`:
```
Octal | Binary | Permission meaning | Example use case
777   | 111111111 | rwxrwxrwx | (explain why this is risky)
755   | 111101101 | rwxr-xr-x | (explain typical use)
700   | 111000000 | rwx------ | (explain typical use)
```

Commit:
```
git add .
git commit -m "Linux Permissions Completed"
git push
```

**Deliverable**
Permissions section added to cheatsheet + screenshot of the `testuser` access test.

---

### DAY 4

**Goal**
Understand how computers communicate — networking fundamentals.

**Hour 1 — Core Concept**

THM: **Pre Security** → Networking modules.

Topics:
```
What is a network?
IP addresses (IPv4)
MAC addresses
DHCP
DNS
The OSI Model (all 7 layers)
```

**Hour 2 — Lab**

Run these commands on your Kali VM and record the output:
```
ip a
ip route
cat /etc/resolv.conf
dig google.com
nslookup google.com
ping -c 4 google.com
traceroute google.com
```

Answer in writing:
```
What happens when you type google.com into your browser?
(Walk through: DNS lookup → TCP handshake → HTTP request → response → render)
```

**Hour 3 — Documentation**

Create:
```
networking-notes.md
```

Include a hand-drawn (or draw.io) diagram of:
```
Your laptop → Router → ISP → DNS server → Google's server → back to you
```

Commit:
```
git add .
git commit -m "Networking Fundamentals Day 1 Completed"
git push
```

**Deliverable**
`networking-notes.md` with command outputs + a request/response flow diagram.

---

### DAY 5

**Goal**
Packet capture fundamentals with Wireshark.

**Hour 1 — Core Concept**

THM: **Pre Security** → "Wireshark: The Basics" (or equivalent intro room).

Topics:
```
What is a packet?
Capture filters vs display filters
TCP 3-way handshake (SYN, SYN-ACK, ACK)
Common display filters: ip.addr, tcp.port, http, dns
```

**Hour 2 — Lab**

Open Wireshark on your Kali VM, start a capture, then in another terminal:
```
ping -c 4 google.com
curl http://example.com
dig google.com
```

Stop the capture. Apply these display filters one at a time and screenshot each:
```
icmp
dns
tcp.flags.syn == 1
http
```

Find and screenshot the exact 3 packets of a TCP handshake (SYN / SYN-ACK / ACK).

**Hour 3 — Documentation**

Create:
```
wireshark-lab-01.md
```

Structure:
```
Objective
Tools used
Filters applied
Screenshot 1 — ICMP capture
Screenshot 2 — DNS query/response
Screenshot 3 — TCP 3-way handshake
What I learned
```

Commit:
```
git add .
git commit -m "Wireshark Lab 01 Completed"
git push
```

**Deliverable**
`wireshark-lab-01.md` — your first analyst-style packet capture write-up.

---

### DAY 6

**Goal**
OverTheWire Bandit — apply Linux + networking skills under pressure.

**Hour 1 — Core Concept**

Read: OverTheWire Bandit rules and Level 0 instructions.

Topics to review before starting:
```
SSH connection basics
ssh username@host -p port
Reading files with cat, less, file
```

**Hour 2 — Lab**

Connect and solve:
```
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

Solve Levels 0 through 5. For each level, note in your terminal history:
```
Level | Command(s) used | Password found (do not publish real passwords)
```

If stuck longer than 15 minutes on any single level, look up ONE hint — not the full solution — and note that you needed help.

**Hour 3 — Documentation**

Create:
```
bandit-writeup.md
```

For each of the 5 levels completed, write (without publishing actual passwords):
```
Level:
Objective:
Commands used:
Concept practiced:
```

Commit:
```
git add .
git commit -m "Bandit Levels 0-5 Completed"
git push
```

**Deliverable**
`bandit-writeup.md` documenting Levels 0–5, with concepts (not credentials) explained.

---

### DAY 7

**Goal**
Consolidate and review — Week 1 capstone.

**Hour 1 — Core Concept**

Re-read your own notes from Days 1–6, cover to cover, out loud. This is intentional — teaching yourself back your own week is the single highest-retention study method available.

**Hour 2 — Lab**

Self-test: without looking at notes, complete each of these live in your Kali VM:
```
1. Create a directory structure 3 levels deep
2. Set permission 750 on a file and explain what it means, out loud
3. Run ping, dig, and traceroute against a domain of your choice
4. Open Wireshark, capture your own DNS query, filter for it, and screenshot it
5. SSH into Bandit and solve one level you haven't done yet (Level 6, bonus)
```

If any of the 5 fail, redo that specific day's lab section before Week 2 begins.

**Hour 3 — Documentation**

Create:
```
week-01-summary.md
```

Structure:
```
What I built this week
Skills I can now perform without notes
Skills I still need to reinforce
Screenshots index (links to Day 1-6 files)
```

Commit and push everything:
```
git add .
git commit -m "Week 1 Completed — Foundations Locked In"
git push
```

**Deliverable**
`week-01-summary.md` — a self-assessed, evidence-linked summary proving Week 1 mastery.

---

## Week 2 — Linux Mastery & Automation Basics

### Week 2 Overview

**Theme**
You can already navigate Linux. Now you learn to *administer* it — permissions at scale, processes, services, and your first bash scripts. This is the week you stop being a Linux tourist and start being a Linux operator.

**Week 2 Objectives**

```
✅ Master file/process management and service control
✅ Understand package management (apt)
✅ Read and interpret running processes and system logs
✅ Write your first bash scripts
✅ Schedule automated tasks with cron
✅ Push a working automation script to GitHub
```

**Success Criteria**

```
- Can you kill a specific process by PID and explain why you'd need to?
- Can you explain the difference between a process and a systemd service?
- Can you write a 10-line bash script with a loop and a conditional, unaided?
- Can you schedule a cron job and verify it ran?
- Can you find failed SSH login attempts in a log file using grep?
```

**Week 2 Resources**

Primary Platform
```
TryHackMe (Free)
Rooms:
- Linux Fundamentals Part 2
- Linux Fundamentals Part 3
```

Practice Platform
```
OverTheWire — Bandit, Levels 6–12
```

Documentation
```
- bash man pages (man bash)
- explainshell.com (paste any command to see it broken down)
- crontab.guru (for cron syntax)
```

---

### DAY 8

**Goal**
Processes and services.

**Hour 1 — Core Concept**

THM: **Linux Fundamentals Part 2** — Processes section.

Topics:
```
ps aux
top / htop
kill, kill -9
systemctl status/start/stop/restart
Difference: process vs service vs daemon
```

**Hour 2 — Lab**

```
ps aux | less
top
```

Start a long-running dummy process, find its PID, and kill it:
```
sleep 300 &
ps aux | grep sleep
kill <PID>
```

Check and control a real service:
```
sudo systemctl status ssh
sudo systemctl stop ssh
sudo systemctl start ssh
sudo systemctl enable ssh
```

**Hour 3 — Documentation**

Add a "Processes & Services" section to `linux-cheatsheet.md`:
```
Command | Purpose | Example
ps aux
kill -9
systemctl status
```

Commit:
```
git add .
git commit -m "Linux Processes and Services Completed"
git push
```

**Deliverable**
Updated `linux-cheatsheet.md` + screenshot of a killed process and a controlled service.

---

### DAY 9

**Goal**
Package management and system updates.

**Hour 1 — Core Concept**

THM: **Linux Fundamentals Part 2** — Package Management section.

Topics:
```
apt update / upgrade / full-upgrade
apt install / remove / purge
dpkg -l
Where packages come from (repositories)
```

**Hour 2 — Lab**

```
sudo apt update
sudo apt list --upgradable
sudo apt install neofetch
neofetch
sudo apt remove neofetch
dpkg -l | grep python
```

Install a tool you'll need later and verify it:
```
sudo apt install net-tools
netstat -tulnp
```

**Hour 3 — Documentation**

Add "Package Management" section to cheatsheet with 6+ documented commands.

Commit:
```
git add .
git commit -m "Package Management Completed"
git push
```

**Deliverable**
Cheatsheet updated + `netstat -tulnp` output screenshot explained in your own words.

---

### DAY 10

**Goal**
Bash scripting fundamentals — variables, conditionals, loops.

**Hour 1 — Core Concept**

Reading/video on bash scripting basics.

Topics:
```
Shebang: #!/bin/bash
Variables: name="value"
Conditionals: if / elif / else
Loops: for, while
Comparison operators: -eq, -lt, -gt, ==
```

**Hour 2 — Lab**

Create your first script:
```
mkdir -p CyberLab/scripts
cd CyberLab/scripts
touch hello.sh
chmod +x hello.sh
```

`hello.sh`:
```
#!/bin/bash
echo "Hello, $(whoami). Today is $(date)."
```

Run it:
```
./hello.sh
```

Now build a slightly harder one — a number checker:
```
#!/bin/bash
read -p "Enter a number: " num
if [ $num -gt 10 ]; then
  echo "Bigger than 10"
elif [ $num -eq 10 ]; then
  echo "Exactly 10"
else
  echo "Smaller than 10"
fi
```

**Hour 3 — Documentation**

Create:
```
scripts/README.md
```

Document both scripts: purpose, code, sample run output.

Commit:
```
git add .
git commit -m "First Bash Scripts Completed"
git push
```

**Deliverable**
Two working bash scripts in `cybersecurity-home-lab/scripts/` with documentation.

---

### DAY 11

**Goal**
Bash scripting for security — parsing logs.

**Hour 1 — Core Concept**

Reading/video on `grep`, `awk`, `sed` for text processing.

Topics:
```
grep -i, grep -c, grep -v
awk '{print $1}'
sed 's/old/new/'
Piping commands together
```

**Hour 2 — Lab**

Generate sample failed login attempts (safe, local test — do not attack real systems):
```
sudo tail -50 /var/log/auth.log
```

Write a script `find_failed_logins.sh`:
```
#!/bin/bash
echo "Failed login attempts by IP:"
grep "Failed password" /var/log/auth.log | awk '{print $(NF-3)}' | sort | uniq -c | sort -nr
```

Run it and review the output. If your log is empty, generate test entries by attempting a few deliberate failed local logins.

**Hour 3 — Documentation**

Update `scripts/README.md` with this script's purpose, code, and a redacted sample output.

Commit:
```
git add .
git commit -m "Log Parsing Script Completed"
git push
```

**Deliverable**
`find_failed_logins.sh` — your first security-relevant automation script.

---

### DAY 12

**Goal**
Task automation with cron.

**Hour 1 — Core Concept**

Reading/video on cron and crontab.

Topics:
```
crontab -e
Cron syntax: minute hour day month weekday
crontab -l
/var/log/syslog for cron verification
```

**Hour 2 — Lab**

Schedule your Day 11 script to run every 5 minutes:
```
crontab -e
```
Add:
```
*/5 * * * * /home/kali/CyberLab/scripts/find_failed_logins.sh >> /home/kali/CyberLab/logs/login_report.log 2>&1
```

Wait for at least two runs, then verify:
```
cat /home/kali/CyberLab/logs/login_report.log
grep CRON /var/log/syslog
```

**Hour 3 — Documentation**

Add a "Cron Automation" entry to `scripts/README.md` explaining the schedule syntax and what the job does.

Commit:
```
git add .
git commit -m "Cron Automation Completed"
git push
```

**Deliverable**
A verified, running cron job with log output as proof.

---

### DAY 13

**Goal**
OverTheWire Bandit, Levels 6–12 — apply scripting and search skills under pressure.

**Hour 1 — Core Concept**

Review before starting:
```
find / -type f -name "filename" 2>/dev/null
file <filename>
Data encodings: base64, hex, ROT13
```

**Hour 2 — Lab**

```
ssh bandit6@bandit.labs.overthewire.org -p 2220
```

Solve Levels 6 through 12. Expect to use:
```
find
file
base64 -d
xxd
tar / gzip / bzip2 (for compressed file levels)
```

If stuck longer than 20 minutes on one level, use ONE hint, and note it.

**Hour 3 — Documentation**

Extend `bandit-writeup.md` with Levels 6–12 (concepts and commands, not credentials).

Commit:
```
git add .
git commit -m "Bandit Levels 6-12 Completed"
git push
```

**Deliverable**
`bandit-writeup.md` extended through Level 12.

---

### DAY 14

**Goal**
Consolidate and review — Week 2 capstone.

**Hour 1 — Core Concept**

Re-read your Week 2 notes and scripts out loud, end to end.

**Hour 2 — Lab**

Self-test, live, without notes:
```
1. Find and kill a running process by PID
2. Install and remove a package with apt
3. Write a 5-line bash script with a loop from scratch
4. Grep your auth.log for failed logins and count them by IP
5. Schedule a one-off cron job and verify it fired
```

Redo any failed item before Week 3.

**Hour 3 — Documentation**

Create:
```
week-02-summary.md
```

Structure:
```
Scripts built this week (with links)
Skills now automatic
Skills needing reinforcement
Bandit levels completed
```

Commit and push:
```
git add .
git commit -m "Week 2 Completed — Linux Operator Level Reached"
git push
```

**Deliverable**
`week-02-summary.md` + two working, documented scripts + a verified cron job — your first real automation portfolio pieces.

---

## Week 3 — Windows Fundamentals & Active Directory Intro

### Week 3 Overview

**Theme**
Most corporate breaches happen on Windows and Active Directory, not Linux. This week you learn to read Windows the way you now read Linux — registry, event logs, services — and understand the AD hierarchy that almost every SOC alert will eventually reference.

**Week 3 Objectives**

```
✅ Navigate Windows via GUI and PowerShell
✅ Understand Event Viewer and key Event IDs
✅ Understand services, the registry, and Sysinternals tools
✅ Understand Active Directory: domains, OUs, GPOs, DCs
✅ Run core PowerShell cmdlets confidently
✅ Diagram an AD environment
```

**Success Criteria**

```
- Can you locate Event ID 4625 in Event Viewer and explain what it means?
- Can you explain the difference between a domain, an OU, and a GPO?
- Can you run 5 PowerShell cmdlets from memory (no notes)?
- Can you explain, at a high level, how Kerberos authentication works?
```

**Week 3 Resources**

Primary Platform
```
TryHackMe (Free)
Rooms:
- Windows Fundamentals 1, 2, 3
- Intro to Active Directory
```

Documentation
```
- Microsoft Learn: Active Directory Domain Services
- ss64.com/ps (PowerShell command reference)
```

---

### DAY 15

**Goal**
Windows file system and registry.

**Hour 1 — Core Concept**

THM: **Windows Fundamentals 1**

Topics:
```
File system layout (C:\Windows, C:\Users, C:\Program Files)
Registry hives: HKLM, HKCU, HKCR, HKU, HKCC
regedit navigation
```

**Hour 2 — Lab**

On your Windows VM:
```
Open regedit
Navigate to HKEY_LOCAL_MACHINE\SOFTWARE
Navigate to HKEY_CURRENT_USER\Environment
```

Open Command Prompt and PowerShell side by side, run:
```
systeminfo
whoami /all
echo %PATH%
```

**Hour 3 — Documentation**

Create:
```
windows-notes.md
```

Document registry hive purposes and 3 command outputs with your own explanation of each.

Commit (in your Linux/Git environment, syncing notes across your lab):
```
git add .
git commit -m "Windows Filesystem and Registry Completed"
git push
```

**Deliverable**
`windows-notes.md` with registry hive breakdown + command outputs.

---

### DAY 16

**Goal**
Event Viewer and Task Manager.

**Hour 1 — Core Concept**

THM: **Windows Fundamentals 2**

Topics:
```
Event Viewer structure: Application, Security, System logs
Key Event IDs: 4624 (successful logon), 4625 (failed logon), 4688 (process creation)
Task Manager: Processes, Performance, Startup tabs
```

**Hour 2 — Lab**

```
Open Event Viewer (eventvwr.msc)
Navigate to Windows Logs > Security
Filter Current Log for Event ID 4624 and 4625
```

Generate a test failed logon (log out, deliberately mistype your password once, log back in), then find that exact Event ID 4625 entry and screenshot it.

**Hour 3 — Documentation**

Add "Event Viewer" section to `windows-notes.md` with Event ID table and your screenshot reference.

Commit:
```
git add .
git commit -m "Event Viewer Fundamentals Completed"
git push
```

**Deliverable**
Screenshot + documented explanation of a real 4625 event you generated yourself.

---

### DAY 17

**Goal**
Services, Sysinternals, and process inspection.

**Hour 1 — Core Concept**

THM: **Windows Fundamentals 3**

Topics:
```
services.msc
Sysinternals Suite overview (Process Explorer, Autoruns, TCPView)
Difference between a process and a Windows service
```

**Hour 2 — Lab**

```
Download Sysinternals Suite (docs.microsoft.com/sysinternals)
Run procexp.exe (Process Explorer)
Run autoruns.exe
Run tcpview.exe
```

Explore:
```
Find the process for your web browser in Process Explorer, inspect its handles/DLLs
In Autoruns, identify 3 items that launch at startup
In TCPView, identify any process with an active network connection
```

**Hour 3 — Documentation**

Add "Services & Sysinternals" section to `windows-notes.md` with 3 screenshots and a one-line explanation for each tool.

Commit:
```
git add .
git commit -m "Sysinternals Tools Explored"
git push
```

**Deliverable**
Sysinternals findings documented — this becomes reference material for Month 3's Sysmon work.

---

### DAY 18

**Goal**
Active Directory core concepts.

**Hour 1 — Core Concept**

THM: **Intro to Active Directory**

Topics:
```
Domain, Forest, Tree
Domain Controller (DC)
Organizational Units (OUs)
Group Policy Objects (GPOs)
Users, Groups, Computers as AD objects
```

**Hour 2 — Lab**

No AD server yet (that's Month 2) — instead, build your understanding visually:
```
Open draw.io (or diagrams.net)
Diagram: 1 Forest > 1 Domain > 2 OUs > 3 Users > 1 DC
```

Research and write down, in your own words:
```
Why do organizations use OUs instead of one big flat list of users?
What is a GPO actually enforcing, technically?
```

**Hour 3 — Documentation**

Save the AD diagram as `ad-structure-diagram.png` in `cybersecurity-home-lab/diagrams/`.

Create `active-directory-notes.md` with your written answers.

Commit:
```
git add .
git commit -m "Active Directory Concepts Completed"
git push
```

**Deliverable**
AD structure diagram + concept notes — this diagram gets rebuilt for real in Month 2.

---

### DAY 19

**Goal**
PowerShell fundamentals for security.

**Hour 1 — Core Concept**

Reading/video: PowerShell basics.

Topics:
```
Cmdlet naming: Verb-Noun
The pipeline ( | )
Get-Help
Objects vs plain text output
```

**Hour 2 — Lab**

Run and screenshot each of these, with a one-line note on what each does:
```
Get-Process
Get-Service
Get-EventLog -LogName Security -Newest 20
Get-ChildItem -Path C:\ -Recurse -ErrorAction SilentlyContinue | Select-Object -First 20
Get-Help Get-Process -Examples
```

Practice piping:
```
Get-Process | Sort-Object CPU -Descending | Select-Object -First 5
```

**Hour 3 — Documentation**

Create:
```
powershell-cheatsheet.md
```

Document each cmdlet: purpose, example, sample output.

Commit:
```
git add .
git commit -m "PowerShell Fundamentals Completed"
git push
```

**Deliverable**
`powershell-cheatsheet.md` with 5+ documented cmdlets.

---

### DAY 20

**Goal**
Windows authentication concepts (NTLM & Kerberos, conceptually).

**Hour 1 — Core Concept**

THM: **Active Directory Basics** (or equivalent authentication-focused room).

Topics:
```
NTLM authentication flow (high level)
Kerberos authentication flow (high level): AS-REQ, AS-REP, TGT, TGS
Why Kerberos is generally preferred over NTLM
```

**Hour 2 — Lab**

On your Windows VM (standalone, no domain yet):
```
klist
whoami /groups
```

Draw the Kerberos flow yourself on paper or in draw.io:
```
Client → Authentication Server (AS) → Ticket Granting Ticket (TGT)
Client → Ticket Granting Server (TGS) → Service Ticket
Client → Application Server (using Service Ticket)
```

**Hour 3 — Documentation**

Add "Authentication Concepts" section to `active-directory-notes.md` with your Kerberos flow diagram description and `klist`/`whoami` output.

Commit:
```
git add .
git commit -m "Windows Authentication Concepts Completed"
git push
```

**Deliverable**
Kerberos flow diagram + authentication notes — this will directly support Month 2's AD lab build.

---

### DAY 21

**Goal**
Consolidate and review — Week 3 capstone.

**Hour 1 — Core Concept**

Re-read all Week 3 notes out loud, end to end.

**Hour 2 — Lab**

Self-test, live, without notes:
```
1. Find a specific Event ID (4625) in Event Viewer unaided
2. Open Process Explorer and identify 2 running processes you don't recognize, then research what they are
3. Explain out loud (recorded, if possible): Domain vs OU vs GPO
4. Run 5 PowerShell cmdlets from memory
5. Explain the Kerberos flow out loud without looking at your diagram
```

Redo any failed item before Week 4.

**Hour 3 — Documentation**

Create:
```
week-03-summary.md
```

Structure:
```
Windows concepts mastered
PowerShell cmdlets I can run from memory
AD structure diagram (linked)
What I'm not fully confident on yet
```

Commit and push:
```
git add .
git commit -m "Week 3 Completed — Windows and AD Foundations Locked In"
git push
```

**Deliverable**
`week-03-summary.md` + PowerShell cheatsheet + AD diagram — all cross-linked and ready to support Month 2's real AD build.

---

## Week 4 — Security Fundamentals + Home Lab Build (Crown Jewel Week)

### Week 4 Overview

**Theme**
You now understand computers, networks, Linux, and Windows individually. This week you fuse it all together: security fundamentals (CIA Triad, crypto, controls) plus your first real multi-VM home lab, captured, documented, and published as your **Month 1 Crown Jewel Project**.

**Week 4 Objectives**

```
✅ Understand CIA Triad and core security controls
✅ Understand hashing vs encryption vs encoding
✅ Design and deploy a segmented multi-VM home lab
✅ Capture and analyze real cross-VM traffic
✅ Publish a polished, professional Crown Jewel repository
```

**Success Criteria**

```
- Can you explain Confidentiality, Integrity, and Availability with a real example of each?
- Can you explain the difference between hashing and encryption, and why you'd use each?
- Is your home lab live, with all VMs able to ping each other?
- Have you captured and documented at least 3 distinct traffic types between your VMs?
- Is your Crown Jewel repository published, with a diagram, screenshots, and a clean README?
```

**Week 4 Resources**

Primary Platform
```
TryHackMe (Free)
Rooms:
- Cyber Security 101
- Cryptography Basics
- Intro to Cyber Threat Intel
```

Tools
```
VirtualBox / VMware
draw.io (network diagram)
Wireshark
nmap
```

---

### DAY 22

**Goal**
CIA Triad and security controls.

**Hour 1 — Core Concept**

THM: **Cyber Security 101**

Topics:
```
Confidentiality, Integrity, Availability
Technical vs Administrative vs Physical controls
Preventive vs Detective vs Corrective controls
```

**Hour 2 — Lab**

For 5 real-world scenarios, classify which part of the CIA Triad is being violated and what control type would help. Write this as a table:
```
Scenario | CIA element violated | Control type that helps
Ransomware encrypts files | Availability | Backups (Corrective)
Employee reads unauthorized files | Confidentiality | Access controls (Preventive)
Website defaced | Integrity | File integrity monitoring (Detective)
DDoS attack on a server | Availability | Rate limiting/WAF (Preventive)
Insider leaks database | Confidentiality | DLP + least privilege (Preventive/Detective)
```

**Hour 3 — Documentation**

Create:
```
security-fundamentals-notes.md
```

Include your completed CIA Triad table plus a short written explanation in your own words of each control type.

Commit:
```
git add .
git commit -m "CIA Triad and Security Controls Completed"
git push
```

**Deliverable**
`security-fundamentals-notes.md` with a fully reasoned CIA Triad scenario table.

---

### DAY 23

**Goal**
Cryptography basics — hashing vs encryption vs encoding.

**Hour 1 — Core Concept**

THM: **Cryptography Basics**

Topics:
```
Hashing (MD5, SHA-256) — one-way, used for integrity
Encryption (symmetric vs asymmetric) — two-way, used for confidentiality
Encoding (Base64) — NOT security, just representation
```

**Hour 2 — Lab**

On Kali:
```
echo -n "password123" | md5sum
echo -n "password123" | sha256sum
echo -n "password123" | base64
echo "cGFzc3dvcmQxMjM=" | base64 -d
```

Answer in writing:
```
Why can't you "decrypt" an MD5 hash back to the original text?
Why is Base64 not a security measure at all?
When would you use symmetric encryption vs asymmetric encryption?
```

**Hour 3 — Documentation**

Add "Cryptography Basics" section to `security-fundamentals-notes.md` with your command outputs and written answers.

Commit:
```
git add .
git commit -m "Cryptography Basics Completed"
git push
```

**Deliverable**
Hashing/encryption/encoding comparison table with real command outputs as evidence.

---

### DAY 24

**Goal**
Design and diagram your home lab network.

**Hour 1 — Core Concept**

Reading/video: network segmentation principles for home labs.

Topics:
```
Why segment attacker/victim/monitoring machines
Internal-only ("Host-Only" or "Internal Network") vs NAT networking in VirtualBox/VMware
Static IP addressing for lab consistency
```

**Hour 2 — Lab**

In VirtualBox/VMware, configure networking:
```
Create an Internal Network (e.g., "CyberLabNet")
Assign Kali: 192.168.50.10
Assign Windows VM: 192.168.50.20
Assign Ubuntu VM: 192.168.50.30
```

Set static IPs on each VM and verify:
```
# Linux (Kali/Ubuntu)
ip addr show
sudo nano /etc/network/interfaces   (or netplan config on Ubuntu)

# Windows
Get-NetIPAddress
```

**Hour 3 — Documentation**

Build your topology diagram in draw.io: router/internal network, all 3 VMs with IPs labeled, save as `lab-topology.png`.

Commit:
```
git add .
git commit -m "Home Lab Network Design Completed"
git push
```

**Deliverable**
`lab-topology.png` — a professional network diagram, the centerpiece visual of your Crown Jewel.

---

### DAY 25

**Goal**
Deploy the lab fully and verify connectivity.

**Hour 1 — Core Concept**

Quick review: `ping`, `nmap -sn`, ARP, and what "verified connectivity" actually means at each OSI layer.

**Hour 2 — Lab**

From Kali, verify every VM can see every other VM:
```
ping -c 4 192.168.50.20
ping -c 4 192.168.50.30
nmap -sn 192.168.50.0/24
```

From Windows, verify it can reach Kali and Ubuntu:
```
Test-Connection 192.168.50.10
Test-Connection 192.168.50.30
```

Fix any connectivity issues (firewall rules, adapter settings) before proceeding — do not move on with a broken lab.

**Hour 3 — Documentation**

Create:
```
lab-connectivity-report.md
```

Include the `nmap -sn` output and both ping/Test-Connection results, with a short explanation of what each proves.

Commit:
```
git add .
git commit -m "Home Lab Fully Deployed and Verified"
git push
```

**Deliverable**
`lab-connectivity-report.md` — proof your 3-VM lab is fully live and communicating.

---

### DAY 26

**Goal**
Capture and analyze real cross-VM traffic.

**Hour 1 — Core Concept**

Quick review: applying display filters efficiently, saving PCAP files, annotating packets in Wireshark.

**Hour 2 — Lab**

Start Wireshark on Kali capturing on the internal network interface. From Windows and Ubuntu, generate 3 distinct traffic types toward Kali or each other:
```
# ICMP
ping -c 4 192.168.50.10

# DNS (point a query at a DNS-capable host or use public DNS through the lab's routing)
dig @192.168.50.10 example.com    (or nslookup from Windows)

# HTTP (spin up a simple server on Kali first)
python3 -m http.server 8080         # on Kali
curl http://192.168.50.10:8080      # from Ubuntu or Windows
```

Stop the capture, save as `crossvm-capture.pcapng`, and apply filters to isolate and screenshot each traffic type:
```
icmp
dns
http
```

**Hour 3 — Documentation**

Create:
```
crossvm-traffic-analysis.md
```

Structure (repeat for each of the 3 traffic types):
```
Traffic type:
Filter used:
Screenshot:
What's happening at each layer (source, destination, protocol behavior):
```

Commit:
```
git add .
git commit -m "Cross-VM Traffic Capture and Analysis Completed"
git push
```

**Deliverable**
`crossvm-traffic-analysis.md` + `crossvm-capture.pcapng` — your core analyst-style evidence artifact.

---

### DAY 27

**Goal**
Assemble the Crown Jewel repository.

**Hour 1 — Core Concept**

Reading/video: what makes a GitHub security portfolio repo look professional (structure, README quality, clear evidence trail) — review 2-3 real public security portfolio repos for inspiration on structure only, not content copying.

**Hour 2 — Lab**

Create the final repository structure:
```
homelab-network-foundations/
├── README.md
├── diagrams/
│   ├── lab-topology.png
│   └── ad-structure-diagram.png
├── captures/
│   └── crossvm-capture.pcapng
├── reports/
│   ├── lab-connectivity-report.md
│   ├── crossvm-traffic-analysis.md
│   └── wireshark-lab-01.md
└── notes/
    ├── linux-cheatsheet.md
    ├── networking-notes.md
    ├── windows-notes.md
    ├── active-directory-notes.md
    ├── powershell-cheatsheet.md
    └── security-fundamentals-notes.md
```

Move/organize all Month 1 files into this structure using `git mv` (preserves history) where possible:
```
git mv linux-cheatsheet.md notes/
git mv lab-topology.png diagrams/
```

**Hour 3 — Documentation**

Write the master `README.md` for the repository:
```
# Home Lab Network Foundations

## What this repo demonstrates
- A segmented 3-VM home lab (Kali, Windows, Ubuntu)
- Full network connectivity verification
- Wireshark packet capture and protocol analysis (ICMP, DNS, HTTP, TCP handshake)
- Linux, Windows, and Active Directory foundational documentation
- CIA Triad and cryptography fundamentals applied to real scenarios

## Structure
(explain folders)

## Skills demonstrated
(bullet list: Linux administration, networking fundamentals, Wireshark analysis, security fundamentals, professional documentation)

## About me
(1-2 sentences: your background and what you're working toward)
```

Commit:
```
git add .
git commit -m "Crown Jewel Repository Assembled"
git push
```

**Deliverable**
A fully organized, professional `homelab-network-foundations` repository — ready to be shown to a hiring manager.

---

### DAY 28

**Goal**
Final polish and Month 1 review — Crown Jewel Day.

**Hour 1 — Core Concept**

Re-read your entire Month 1 journey: Week 1 through Week 4 summaries, in order, out loud.

**Hour 2 — Lab**

Final quality pass on the Crown Jewel repo:
```
Check every image renders correctly on GitHub
Check every internal markdown link works
Re-read the README as if you were a stranger seeing it for the first time
Fix any typos, broken formatting, or unclear explanations
```

Do a final live self-test covering all of Month 1, unaided:
```
1. Explain the CIA Triad with real examples
2. Subnet a /24 network by hand (bonus reinforcement from Week 1)
3. Show your lab topology and explain every connection
4. Open your PCAP and explain the TCP 3-way handshake live
5. Explain Domain vs OU vs GPO
```

**Hour 3 — Documentation**

Create:
```
month-01-summary.md
```

Structure:
```
Crown Jewel Project: homelab-network-foundations (link)
Skills mastered this month
Weekly summaries (linked)
What I'm most proud of
What I'm carrying into Month 2
```

Final commit and push:
```
git add .
git commit -m "Month 1 Completed — Crown Jewel Published"
git push
```

**Deliverable**
Fully published, polished `homelab-network-foundations` repository + `month-01-summary.md` — **Month 1 is complete.**

---

*End of Chapter 1. Chapter 2 (Month 2 — System Administration, Active Directory Build, and Security Scripting) continues in the same format.*
