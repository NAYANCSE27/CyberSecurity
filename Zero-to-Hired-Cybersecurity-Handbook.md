# Zero-to-Hired Cybersecurity Roadmap (Version 2026)
## A Complete 6-Month Handbook

---

## How This Handbook Works

Every week follows the same rhythm:

- **Week Overview** — theme, mindset, objectives, success-criteria questions, resources
- **Daily Schedule** — 7 days, each split into three 1-hour blocks:

```
Hour 1   Core Concept   — targeted theory (video/reading)
Hour 2   Lab            — hands-on execution
Hour 3   Documentation  — notes, cheat sheet, GitHub commit
```

Each day ends with a **Deliverable** — something committed to your `soc-journey` GitHub organization. By Day 168 you will have six flagship projects and 168 days of visible commit history.

---

# Chapter 1 — Month 1: Build the Foundation

**Chapter Theme:** Everything in cybersecurity starts with understanding how computers actually work.
**Mindset Shift:** Stop being a GUI user. Become a systems operator who thinks in files, packets, and permissions.
**Skill Target:** Linux CLI fluency, TCP/IP mastery, Windows/AD fundamentals, a working home lab.
**Crown Jewel Project:** A 4-VM home lab (Kali, Windows 10, Ubuntu Server, pfSense) with a network topology diagram and 3 annotated Wireshark packet captures, published on GitHub.

---

## Week 1 — Becoming Comfortable with Computers Like a Security Professional

### Week 1 Overview

**Theme**

This week is not about hacking. This week is about becoming comfortable using Linux, Windows, networking, Git, and your home lab.

Think of yourself as an apprentice mechanic. A Formula 1 driver doesn't start by driving at 300 km/h — they first understand the engine. Cybersecurity works exactly the same way.

**Objectives**

By the end of Week 1 you should be able to:

- ✅ Install and configure your cybersecurity lab
- ✅ Navigate Linux entirely from the terminal
- ✅ Understand files, permissions, and processes
- ✅ Understand how computers communicate
- ✅ Capture packets using Wireshark
- ✅ Create your first professional GitHub repository

**Success Criteria**

At the end of this week, you should confidently answer these questions:

- What happens when you type `google.com` into your browser?
- What is the difference between a process and a service?
- Why is Linux permission `755` different from `777`?
- How does DHCP assign an IP address?
- How does DNS resolve a domain?
- How do you analyze packets using Wireshark?
- How do you document your work professionally?

If you cannot answer these without searching Google, repeat the relevant day's labs before moving on.

**Resources**

*Primary Platform*
- TryHackMe (Free) — Rooms: `Pre Security`, `Introduction to Cyber Security`, `Linux Fundamentals Part 1`

*Secondary*
- Cisco Skills For All — Networking Basics

*Practice Platform*
- OverTheWire: Bandit, Levels 0–5

*Documentation*
- Linux `man` pages
- GitHub Docs
- Microsoft Learn (Windows)

---

### Week 1 Daily Schedule

#### DAY 1 — Build Your Cybersecurity Workspace

**Goal:** Set up every tool you'll use for the next six months.

**Hour 1 — Core Concept**

Watch TryHackMe **Pre Security**, sections:
- What is Cyber Security?
- Offensive vs Defensive Security
- Career Paths
- CIA Triad

Take handwritten notes — do not copy the slides.

**Hour 2 — Lab**

Install required software:
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

If using Kali as your primary VM:
```bash
sudo apt update
sudo apt full-upgrade -y
```

Verify installations:
```bash
python3 --version
git --version
nmap --version
```

Create your GitHub repositories:
```
cybersecurity-roadmap
cybersecurity-notes
cybersecurity-home-lab
```

**Hour 3 — Documentation**

Write your first README:
```
Who am I?
Why Cybersecurity?
Learning Goal
Current Skills
Daily Progress Log
Resources
Projects
```

Commit: `"Day 1 completed — workspace initialized"`

**Deliverable:** GitHub Repository #1 (`cybersecurity-roadmap`) live with a real README.

---

#### DAY 2 — Linux File System

**Goal:** Move around Linux with zero hesitation.

**Hour 1 — Core Concept**

THM **Linux Fundamentals Part 1**. Topics:
```
pwd    ls     cd     mkdir
touch  rm     cp     mv
cat    less   head   tail
```

**Hour 2 — Lab**

Open your Kali terminal and build a working directory structure:
```bash
mkdir CyberLab && cd CyberLab
mkdir notes scripts reports projects logs
```

Practice file operations:
```bash
cp  mv  rm  find  locate  tree
```

Install `tree`:
```bash
sudo apt install tree
```

**Hour 3 — Documentation**

Create `linux-cheatsheet.md`. Document every command using this format:
```
Command: pwd
Purpose: prints the current working directory
Example: pwd
Output: /home/kali/CyberLab
```

Commit: `"Day 2 completed — Linux filesystem mastered"`

**Deliverable:** `linux-cheatsheet.md` with 12+ documented commands, pushed to `cybersecurity-notes`.

---

#### DAY 3 — Permissions, Users & Ownership

**Goal:** Understand who can do what to which file, and why.

**Hour 1 — Core Concept**

THM **Linux Fundamentals Part 2** — permissions, users, groups. Study the octal model:
```
r = 4    w = 2    x = 1
755 = rwxr-xr-x     777 = rwxrwxrwx (dangerous — world-writable/executable)
```

**Hour 2 — Lab**

```bash
touch testfile.sh
chmod 755 testfile.sh
ls -l testfile.sh
chmod u+x,g-w,o-r testfile.sh
sudo useradd -m analyst
sudo passwd analyst
sudo chown analyst:analyst testfile.sh
```

Explain out loud why `chmod 777` on a script is a security red flag.

**Hour 3 — Documentation**

Add a "Permissions" section to your cheat sheet with a worked example of `755` vs `777` and why the difference matters operationally.

Commit: `"Day 3 completed — permissions and ownership"`

**Deliverable:** Cheat sheet updated; a short written answer (3–4 sentences) explaining `755` vs `777` saved in `notes/permissions.md`.

---

#### DAY 4 — Processes & Services

**Goal:** Understand what's actually running on a machine.

**Hour 1 — Core Concept**

THM **Linux Fundamentals Part 3** — package management, processes. Study the distinction:
```
Process = a running instance of a program (has a PID)
Service = a background process managed by the OS (systemd unit)
```

**Hour 2 — Lab**

```bash
ps aux
top
kill -9 <PID>
systemctl status ssh
systemctl list-units --type=service
sudo apt install neofetch
neofetch
```

Start a background process yourself, find its PID, then kill it.

**Hour 3 — Documentation**

Write a `processes-vs-services.md` note answering: *"What is the difference between a process and a service?"* in your own words with a real example from today's lab.

Commit: `"Day 4 completed — processes and services"`

**Deliverable:** `processes-vs-services.md` committed.

---

#### DAY 5 — How Computers Communicate (Networking Intro)

**Goal:** Understand what happens when data leaves your machine.

**Hour 1 — Core Concept**

Cisco Skills For All — Networking Basics, Module 1. Study:
- What is an IP address, a MAC address, a port
- What DHCP does
- What DNS does

**Hour 2 — Lab**

```bash
ip a
ip route
cat /etc/resolv.conf
dig google.com
nslookup google.com
traceroute google.com
```

Answer for yourself, in plain language: *"What happens when you type `google.com` into your browser?"* (DNS lookup → TCP handshake → TLS → HTTP request/response).

**Hour 3 — Documentation**

Write `how-the-internet-works.md` — a step-by-step plain-English walkthrough of the `google.com` request lifecycle.

Commit: `"Day 5 completed — networking fundamentals"`

**Deliverable:** `how-the-internet-works.md` committed.

---

#### DAY 6 — Wireshark & Packet Capture

**Goal:** See the network traffic you've been talking about all week.

**Hour 1 — Core Concept**

THM **Wireshark: The Basics** — interface overview, capture filters vs display filters.

**Hour 2 — Lab**

```bash
sudo wireshark
```
Start a capture on your active interface, then in another terminal:
```bash
ping google.com -c 4
curl http://example.com
```
Apply display filters:
```
tcp.port == 80
dns
icmp
```
Locate a TCP 3-way handshake (SYN, SYN-ACK, ACK) and screenshot it.

**Hour 3 — Documentation**

Annotate the screenshot: label each of the three handshake packets and explain its role.

Commit: `"Day 6 completed — first packet capture analyzed"`

**Deliverable:** Annotated handshake screenshot saved to `cybersecurity-home-lab/captures/`.

---

#### DAY 7 — OverTheWire Bandit + Weekly Review

**Goal:** Prove Week 1 skills under a game-like challenge, then consolidate.

**Hour 1 — Core Concept**

Reread your Day 1–6 notes. Rewatch any section you couldn't explain out loud.

**Hour 2 — Lab**

OverTheWire **Bandit**, Levels 0–5:
```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```
Use `ls`, `cat`, `find`, permissions knowledge, and file navigation to progress through each level.

**Hour 3 — Documentation**

Write a `week1-retrospective.md`: what you learned, what was hardest, and answer all 7 Week 1 Success Criteria questions from memory.

Commit: `"Week 1 completed — foundations locked in"`

**Deliverable:** Bandit Levels 0–5 solved; `week1-retrospective.md` published answering every success-criteria question.

**Week 1 Success Criteria (recap):** You can confidently answer all 7 questions from the overview without searching Google.

---

## Week 2 — Networking Fundamentals & Wireshark Mastery

### Week 2 Overview

**Theme**

Last week you saw a packet. This week you learn to read it fluently — subnetting on paper, protocols by sight, and the TCP/IP model as second nature.

**Objectives**

- ✅ Explain the OSI and TCP/IP models layer by layer
- ✅ Subnet a network by hand
- ✅ Read DNS queries and responses in Wireshark
- ✅ Filter and isolate specific traffic types
- ✅ Build a personal networking cheat sheet

**Success Criteria**

- What are the 7 OSI layers, and what happens at each?
- What's the difference between TCP and UDP, and when does each get used?
- Given a `/24` network, can you list its usable host range and broadcast address?
- Can you find a DNS query in a raw pcap and explain what it's asking?
- What do `tcp.port`, `ip.addr`, and `http.request` filter for?

**Resources**

- TryHackMe: `Intro to Networking`, `What is Networking?`, `DNS in Detail`, `Wireshark: Packet Operations`
- Subnetting practice: subnetting-questions.com (free)

### Week 2 Daily Schedule

#### DAY 8 — The OSI & TCP/IP Models
**Goal:** Memorize and internalize the layered model of networking.
**Hour 1 — Core Concept:** Watch an OSI model breakdown (e.g. PowerCert/NetworkChuck style). Memorize: `Physical, Data Link, Network, Transport, Session, Presentation, Application`.
**Hour 2 — Lab:** THM **Intro to Networking** — complete all tasks. For each layer, find a real example on your own machine (e.g., Ethernet = Data Link, IP = Network, TCP = Transport).
**Hour 3 — Documentation:** Build an `osi-model.md` table: Layer | Protocol Example | Real-World Analogy. Commit: `"Day 8 completed — OSI model internalized"`.
**Deliverable:** `osi-model.md` committed.

#### DAY 9 — TCP vs UDP & Your First Real Capture
**Goal:** Understand connection-oriented vs connectionless communication.
**Hour 1 — Core Concept:** THM **What is Networking?** — TCP vs UDP section.
**Hour 2 — Lab:** Capture 5 minutes of your own browsing in Wireshark. Filter `tcp` then `udp` separately. Identify one application using each (e.g. HTTPS = TCP, DNS = UDP).
**Hour 3 — Documentation:** Add a TCP-vs-UDP comparison table to your cheat sheet with the two examples you found. Commit: `"Day 9 completed — TCP vs UDP"`.
**Deliverable:** Comparison table + 2 labeled screenshots.

#### DAY 10 — The TCP 3-Way Handshake, In Depth
**Goal:** Be able to point at any handshake and narrate it.
**Hour 1 — Core Concept:** THM **Wireshark: The Basics** — remaining tasks. Study SYN / SYN-ACK / ACK flag bits.
**Hour 2 — Lab:**
```bash
curl http://example.com
```
Capture it live, locate the handshake, and expand the TCP flags for each of the 3 packets.
**Hour 3 — Documentation:** Screenshot and annotate all 3 packets with flag values. Commit: `"Day 10 completed — 3-way handshake dissected"`.
**Deliverable:** Annotated 3-packet handshake breakdown.

#### DAY 11 — DNS Resolution
**Goal:** Understand exactly how a domain becomes an IP address.
**Hour 1 — Core Concept:** THM **DNS in Detail** — complete all tasks.
**Hour 2 — Lab:**
```bash
dig google.com
dig +trace google.com
nslookup google.com
```
Capture a `dig` query in Wireshark; find the DNS query and response packets.
**Hour 3 — Documentation:** Write `dns-resolution.md` explaining the recursive resolver → root → TLD → authoritative server chain. Commit: `"Day 11 completed — DNS resolution mapped"`.
**Deliverable:** `dns-resolution.md` + one annotated DNS pcap screenshot.

#### DAY 12 — HTTP/HTTPS & Common Ports
**Goal:** Know the top 20 ports cold.
**Hour 1 — Core Concept:** HTTP methods and status codes; memorize:
```
20/21 FTP   22 SSH   23 Telnet   25 SMTP   53 DNS
80 HTTP   110 POP3   143 IMAP   443 HTTPS   3389 RDP
```
**Hour 2 — Lab:** THM **Wireshark: Packet Operations** — complete all tasks. Capture an HTTP request to a non-HTTPS test site; follow the TCP stream to read the raw request/response.
**Hour 3 — Documentation:** Flashcards (physical or Anki) for all 20 ports. Commit: `"Day 12 completed — ports memorized"`.
**Deliverable:** Port flashcard set + one "Follow TCP Stream" screenshot.

#### DAY 13 — Subnetting by Hand
**Goal:** Subnet any network without a calculator.
**Hour 1 — Core Concept:** CIDR notation, subnet masks, host/broadcast address calculation.
**Hour 2 — Lab:** THM **Subnetting** room. Manually subnet 5 different `/24` networks on paper; verify each against an online subnet calculator only after you've committed to an answer.
**Hour 3 — Documentation:** Write out your 5 worked subnetting problems with full working, not just answers. Commit: `"Day 13 completed — subnetting by hand"`.
**Deliverable:** 5 fully worked subnetting problems.

#### DAY 14 — Traffic Analysis + Weekly Review
**Goal:** Combine everything into one analysis exercise.
**Hour 1 — Core Concept:** Review all Week 2 notes; rewatch weakest topic.
**Hour 2 — Lab:** THM **Wireshark: Traffic Analysis** — complete all tasks. Capture a mixed session (browsing + `dig` + `ping`) and label every protocol seen.
**Hour 3 — Documentation:** Write `week2-retrospective.md` answering all 5 success-criteria questions from memory. Commit: `"Week 2 completed — networking fluency achieved"`.
**Deliverable:** Mixed-traffic annotated pcap + `week2-retrospective.md`.

---

## Week 3 — Windows Fundamentals & Active Directory Basics

### Week 3 Overview

**Theme**

Most corporate environments run on Windows and Active Directory. A SOC analyst who only knows Linux is only half-trained.

**Objectives**

- ✅ Navigate Windows via CLI and PowerShell
- ✅ Understand Active Directory's core objects (domains, OUs, GPOs)
- ✅ Read Windows Event Logs and recognize key Event IDs
- ✅ Inventory running services on a Windows host

**Success Criteria**

- What does a Domain Controller actually do?
- What is a GPO, and what's one real-world example of one?
- What does Event ID 4625 mean, and where do you find it?
- Can you list all running services on a Windows box and flag anything unusual?

**Resources**

- TryHackMe: `Windows Fundamentals 1/2/3`, `Active Directory Basics`
- Microsoft Learn — Windows Event Log documentation

### Week 3 Daily Schedule

#### DAY 15 — Windows OS Structure
**Goal:** Understand the Windows filesystem and Registry.
**Hour 1 — Core Concept:** THM **Windows Fundamentals 1** — OS structure, Registry basics.
**Hour 2 — Lab:** On your Windows 10 VM, explore `C:\Windows\System32`, open `regedit`, browse `HKEY_LOCAL_MACHINE`.
**Hour 3 — Documentation:** Note the 5 Registry hives and what each stores. Commit: `"Day 15 completed — Windows OS structure"`.
**Deliverable:** Registry hive reference note.

#### DAY 16 — File System & User Accounts
**Goal:** Manage users and permissions the Windows way.
**Hour 1 — Core Concept:** THM **Windows Fundamentals 2**.
**Hour 2 — Lab:**
```powershell
net user
net user testuser Passw0rd! /add
net localgroup administrators
```
Create a standard (non-admin) user and confirm its restricted privileges.
**Hour 3 — Documentation:** Compare Windows user permission model to Linux `chmod`/`chown` in your own words. Commit: `"Day 16 completed — Windows accounts"`.
**Deliverable:** Windows-vs-Linux permissions comparison note.

#### DAY 17 — PowerShell Basics
**Goal:** Operate Windows entirely from the command line.
**Hour 1 — Core Concept:** THM **Windows Fundamentals 3** — PowerShell cmdlets and the pipeline.
**Hour 2 — Lab:**
```powershell
Get-Process
Get-Service
Get-EventLog -LogName Security -Newest 10
Get-ChildItem C:\Windows\System32 | Select-Object -First 20
```
**Hour 3 — Documentation:** Build a `powershell-cheatsheet.md` with 10 cmdlets and their purpose. Commit: `"Day 17 completed — PowerShell fluency"`.
**Deliverable:** `powershell-cheatsheet.md`.

#### DAY 18 — Active Directory Concepts
**Goal:** Understand how enterprise Windows environments are structured.
**Hour 1 — Core Concept:** THM **Active Directory Basics** — domains, OUs, GPOs, trusts.
**Hour 2 — Lab:** Continue THM room tasks; if resources allow, browse a pre-built AD lab environment (THM-hosted) using `dsa.msc`-style tools to view OU structure.
**Hour 3 — Documentation:** Draw a simple AD hierarchy diagram (Domain → OUs → Users/Computers → GPOs). Commit: `"Day 18 completed — AD fundamentals"`.
**Deliverable:** AD hierarchy diagram.

#### DAY 19 — Windows Event Logs
**Goal:** Learn to read the logs a SOC analyst lives in every day.
**Hour 1 — Core Concept:** Study key Event IDs: `4624` (successful logon), `4625` (failed logon), `4688` (process creation), `4720` (account created).
**Hour 2 — Lab:** On your Windows VM, deliberately fail a login 3 times. Open Event Viewer → Security log → locate the `4625` entries.
**Hour 3 — Documentation:** Screenshot the `4625` event, annotate each field (Account Name, Source IP, Logon Type). Commit: `"Day 19 completed — Event Log analysis"`.
**Deliverable:** Annotated `4625` event screenshot.

#### DAY 20 — Services & Startup Processes
**Goal:** Build the habit of asking "should this be running?"
**Hour 1 — Core Concept:** Study Windows service states and common legitimate vs suspicious services.
**Hour 2 — Lab:**
```powershell
Get-Service | Where-Object {$_.Status -eq "Running"}
msconfig
```
Inventory all running services; flag 5 you don't recognize and research each.
**Hour 3 — Documentation:** Write `services-inventory.md` — service name, purpose, "expected or investigate" verdict for each. Commit: `"Day 20 completed — services audited"`.
**Deliverable:** `services-inventory.md`.

#### DAY 21 — Weekly Review
**Goal:** Consolidate the Windows/AD foundation.
**Hour 1 — Core Concept:** Review all Week 3 notes.
**Hour 2 — Lab:** Finish any incomplete THM Windows Fundamentals tasks.
**Hour 3 — Documentation:** Write `week3-retrospective.md` answering all 4 success-criteria questions from memory. Commit: `"Week 3 completed — Windows and AD fundamentals locked in"`.
**Deliverable:** `week3-retrospective.md`.

---

## Week 4 — Home Lab Build (Crown Jewel #1)

### Week 4 Overview

**Theme**

Everything you've learned becomes real this week. You build a genuine, networked, multi-host lab — the environment every future project in this roadmap will run on.

**Objectives**

- ✅ Deploy a 4-VM lab behind a pfSense router
- ✅ Configure static IPs and basic firewall rules
- ✅ Produce a professional network topology diagram
- ✅ Capture and annotate 3 meaningful pcaps
- ✅ Publish it all as a polished GitHub repository

**Success Criteria**

- Can you explain your lab's topology to someone with zero context, using your diagram?
- Can you show a DNS query, a TCP handshake, and an HTTP request — each in its own annotated capture?
- Is your GitHub repo something you'd be proud to show a hiring manager today?

**Resources**

- pfSense official documentation
- draw.io (free)
- VirtualBox / VMware Workstation Player

### Week 4 Daily Schedule

#### DAY 22 — Hypervisor & pfSense Install
**Goal:** Lay the physical foundation of the lab.
**Hour 1 — Core Concept:** Type 1 vs Type 2 hypervisors; pfSense's role as a virtual router/firewall.
**Hour 2 — Lab:** Download Kali, Ubuntu Server, Windows 10 evaluation, and pfSense ISOs. Install pfSense as a VM with 2 virtual NICs.
**Hour 3 — Documentation:** Note your VM specs (RAM/CPU allocated) and ISO versions used. Commit: `"Day 22 completed — hypervisor and pfSense installed"`.
**Deliverable:** pfSense VM booted and reachable via web GUI.

#### DAY 23 — Virtual Networking Modes
**Goal:** Get your lab machines talking to each other, safely isolated from your host network.
**Hour 1 — Core Concept:** NAT vs Bridged vs Host-only vs Internal Network adapters.
**Hour 2 — Lab:** Configure pfSense: WAN interface on NAT, LAN interface on an Internal Network. Install Kali on that same Internal Network segment.
**Hour 3 — Documentation:** Diagram (rough sketch) of interfaces and adapter modes so far. Commit: `"Day 23 completed — virtual networking configured"`.
**Deliverable:** Kali VM can reach the internet through pfSense.

#### DAY 24 — Full Lab Assembly + Firewall Rules
**Goal:** All 4 machines online, on one segment, with basic rules in place.
**Hour 1 — Core Concept:** Firewall rule logic — source, destination, port, action, order-of-evaluation.
**Hour 2 — Lab:** Install Ubuntu Server and Windows 10 on the same LAN segment. Assign static IPs to all 4 machines. In pfSense, write 2 rules (e.g., allow LAN-to-WAN, block a specific port).
**Hour 3 — Documentation:** Record your final IP scheme (e.g., `10.10.10.1`–`10.10.10.4`) in `lab-ip-scheme.md`. Commit: `"Day 24 completed — full lab assembled"`.
**Deliverable:** All 4 VMs pingable from each other.

#### DAY 25 — Network Topology Diagram
**Goal:** Produce a diagram good enough to lead an interview with.
**Hour 1 — Core Concept:** Study standard network diagram conventions (router/firewall/host icons, subnet labeling).
**Hour 2 — Lab:** Build the full topology in draw.io: pfSense, Kali, Ubuntu Server, Windows 10, all IPs, all interfaces.
**Hour 3 — Documentation:** Export as PNG; write a 1-paragraph explanation of the design. Commit: `"Day 25 completed — topology diagram published"`.
**Deliverable:** `topology-diagram.png`.

#### DAY 26 — Meaningful Packet Captures
**Goal:** Capture the 3 pcaps that anchor your Crown Jewel.
**Hour 1 — Core Concept:** Review `ip.addr`, `tcp.port`, `dns`, `http.request` filter syntax.
**Hour 2 — Lab:** Capture: (1) a DNS query from Ubuntu to `8.8.8.8`, (2) a TCP handshake from Kali `curl`-ing the Windows box, (3) an HTTP request between two lab VMs.
**Hour 3 — Documentation:** Save all 3 `.pcapng` files into `captures/`. Commit: `"Day 26 completed — 3 pcaps captured"`.
**Deliverable:** 3 raw pcap files saved.

#### DAY 27 — Annotate & Draft README
**Goal:** Turn raw captures into a readable technical artifact.
**Hour 1 — Core Concept:** Review technical-writing conventions for lab reports.
**Hour 2 — Lab:** In Wireshark, add comments to key packets in each of the 3 captures. Export annotated screenshots.
**Hour 3 — Documentation:** Draft `README.md`: lab purpose, topology summary, what each capture demonstrates. Commit: `"Day 27 completed — captures annotated"`.
**Deliverable:** 3 annotated screenshots + README draft.

#### DAY 28 — Publish Crown Jewel #1
**Goal:** Ship a portfolio-ready GitHub repository.
**Hour 1 — Core Concept:** Review strong GitHub README examples for technical projects.
**Hour 2 — Lab:** Final proofread of README, diagram, and captures. Organize repo folders: `/diagram`, `/captures`, `/notes`.
**Hour 3 — Documentation:** Push everything to `cybersecurity-home-lab`. Write a short LinkedIn post draft about finishing your first month.
**Deliverable:** **Crown Jewel #1 — Home Lab** live on GitHub: topology diagram, 3 annotated pcaps, polished README.

---

# Chapter 2 — Month 2: Think Like a Defender & Attacker

**Chapter Theme:** Security is not a checklist — it's an adversarial mental model.
**Mindset Shift:** For every tool you learn, ask "how would I break this, and how would I detect that?"
**Skill Target:** CIA triad in practice, core cryptography, Python for security automation, OWASP Top 10.
**Crown Jewel Project:** A custom Python CLI tool — multi-threaded port scanner + auth-log brute-force parser — published with tests and a README.

---

## Week 5 — Security Principles & Cryptography Basics

### Week 5 Overview

**Theme:** Before you touch an attack or a defense tool, you need the vocabulary and mental models that underpin all of security.

**Objectives**
- ✅ Apply the CIA Triad to real scenarios, not just define it
- ✅ Explain AAA (Authentication, Authorization, Accounting)
- ✅ Distinguish symmetric vs asymmetric encryption
- ✅ Hash and verify file integrity from the command line
- ✅ Understand PKI and the TLS handshake conceptually

**Success Criteria**
- Can you give a real example of a Confidentiality, an Integrity, and an Availability failure?
- What's the difference between Authentication and Authorization?
- Why can't you "decrypt" a hash?
- What problem does PKI actually solve?

**Resources**
- TryHackMe: `Cyber Security 101`, `Cryptography Basics`
- OpenSSL documentation

### Week 5 Daily Schedule

#### DAY 29 — The CIA Triad in Practice
**Goal:** Move CIA from a memorized acronym to a working lens.
**Hour 1 — Core Concept:** THM **Cyber Security 101** — intro tasks, CIA Triad with real breach examples.
**Hour 2 — Lab:** Find 3 real-world breach news stories; classify each as primarily a Confidentiality, Integrity, or Availability failure.
**Hour 3 — Documentation:** Write up your 3 classifications with reasoning in `cia-triad-examples.md`. Commit: `"Day 29 completed — CIA triad applied"`.
**Deliverable:** `cia-triad-examples.md`.

#### DAY 30 — AAA & Access Control Models
**Goal:** Understand how systems decide who gets in and what they can do.
**Hour 1 — Core Concept:** THM **Cyber Security 101** continued — AAA, RBAC vs DAC vs MAC.
**Hour 2 — Lab:** In your home lab, identify 3 real examples of Authentication, Authorization, and Accounting (e.g., Windows login = Authn, folder permissions = Authz, Event Log = Accounting).
**Hour 3 — Documentation:** Document your 3 examples. Commit: `"Day 30 completed — AAA mapped to my lab"`.
**Deliverable:** AAA mapping note.

#### DAY 31 — Symmetric vs Asymmetric Encryption
**Goal:** Understand the two fundamental encryption models.
**Hour 1 — Core Concept:** THM **Cryptography Basics** — complete relevant tasks.
**Hour 2 — Lab:**
```bash
openssl enc -aes-256-cbc -salt -in file.txt -out file.enc
openssl genrsa -out private.pem 2048
openssl rsa -in private.pem -pubout -out public.pem
```
**Hour 3 — Documentation:** Diagram symmetric vs asymmetric encryption flow. Commit: `"Day 31 completed — encryption fundamentals"`.
**Deliverable:** Encryption flow diagram.

#### DAY 32 — Hashing
**Goal:** Verify file integrity without ever "decrypting" anything.
**Hour 1 — Core Concept:** MD5 vs SHA family, why hashing is one-way.
**Hour 2 — Lab:**
```bash
sha256sum file.txt > original.sha256
echo "x" >> file.txt
sha256sum -c original.sha256
```
Observe the mismatch after modifying the file by even one byte.
**Hour 3 — Documentation:** Write `hashing-vs-encryption.md` explaining the difference in your own words. Commit: `"Day 32 completed — hashing demonstrated"`.
**Deliverable:** `hashing-vs-encryption.md`.

#### DAY 33 — Common Attack Types (Conceptual Overview)
**Goal:** Build a mental catalog of attack categories before diving deep later.
**Hour 1 — Core Concept:** THM **Cyber Security 101** — remaining tasks (phishing, malware, MITM, DDoS overview).
**Hour 2 — Lab:** Research one real, publicly documented incident for each attack type; note the attacker's method and the defender's response.
**Hour 3 — Documentation:** Build an `attack-types-catalog.md` reference table. Commit: `"Day 33 completed — attack catalog built"`.
**Deliverable:** `attack-types-catalog.md`.

#### DAY 34 — PKI & TLS
**Goal:** Understand what's happening behind the padlock icon in your browser.
**Hour 1 — Core Concept:** PKI trust chains, certificate authorities, the TLS handshake at a conceptual level.
**Hour 2 — Lab:**
```bash
openssl req -x509 -newkey rsa:2048 -keyout key.pem -out cert.pem -days 365 -nodes
```
Inspect a real website's certificate chain via your browser's dev tools (Security tab).
**Hour 3 — Documentation:** Screenshot the cert chain; annotate Root CA → Intermediate → Leaf. Commit: `"Day 34 completed — PKI and TLS understood"`.
**Deliverable:** Annotated cert chain screenshot.

#### DAY 35 — Weekly Review
**Goal:** Consolidate fundamentals before moving into Python.
**Hour 1 — Core Concept:** Review all Week 5 notes.
**Hour 2 — Lab:** Take a short practice quiz (THM or Professor Messer) on this week's material.
**Hour 3 — Documentation:** Write `week5-retrospective.md` answering all success-criteria questions. Commit: `"Week 5 completed — security fundamentals internalized"`.
**Deliverable:** `week5-retrospective.md`.

---

## Week 6 — Python for Security

### Week 6 Overview

**Theme:** A security analyst who can script isn't waiting on someone else to build the tool they need.

**Objectives**
- ✅ Build a TCP port scanner from scratch using `socket`
- ✅ Add multi-threading for speed
- ✅ Parse a log file with regex to detect brute-force patterns
- ✅ Make your tool a proper CLI with `argparse`

**Success Criteria**
- Can you explain every line of your scanner without looking anything up?
- Why does multi-threading dramatically speed up a port scan?
- What regex would you use to pull failed SSH logins from `auth.log`?

**Resources**
- Python `socket`, `threading`/`concurrent.futures`, `re`, `argparse` docs

### Week 6 Daily Schedule

#### DAY 36 — Sockets 101
**Goal:** Open your first raw TCP connection in Python.
**Hour 1 — Core Concept:** How `socket.socket()`, `connect()`, and `AF_INET`/`SOCK_STREAM` work.
**Hour 2 — Lab:**
```python
import socket
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(("scanme.nmap.org", 80))
s.send(b"GET / HTTP/1.1\r\nHost: scanme.nmap.org\r\n\r\n")
print(s.recv(4096))
```
**Hour 3 — Documentation:** Comment every line of the script explaining what it does. Commit: `"Day 36 completed — first raw socket connection"`.
**Deliverable:** `socket_test.py`.

#### DAY 37 — Scanning a Port Range
**Goal:** Turn a single connection into a real scanner.
**Hour 1 — Core Concept:** Exception handling for `ConnectionRefusedError` and timeouts.
**Hour 2 — Lab:** Extend Day 36's script to loop ports `1-1024` against `localhost`, catching connection errors gracefully and printing only open ports.
**Hour 3 — Documentation:** Note scan runtime; predict how much faster threading could make it. Commit: `"Day 37 completed — port range scanner"`.
**Deliverable:** `scanner_v1.py`.

#### DAY 38 — Multi-Threading
**Goal:** Make the scanner fast enough to be actually useful.
**Hour 1 — Core Concept:** `ThreadPoolExecutor` basics.
**Hour 2 — Lab:** Rewrite the scanner using `concurrent.futures.ThreadPoolExecutor` with 20 workers. Benchmark before/after with `time`.
**Hour 3 — Documentation:** Record the speed comparison in your README draft. Commit: `"Day 38 completed — multi-threaded scanner"`.
**Deliverable:** `scanner_v2.py` (threaded) + benchmark note.

#### DAY 39 — Banner Grabbing
**Goal:** Extract useful service information, not just "open/closed."
**Hour 1 — Core Concept:** How service banners leak version info.
**Hour 2 — Lab:** Add banner-grabbing: read the first bytes returned by each open port and print them alongside the port number.
**Hour 3 — Documentation:** Run against your lab VMs; log which services revealed version info. Commit: `"Day 39 completed — banner grabbing added"`.
**Deliverable:** `scanner_v3.py` (with banners).

#### DAY 40 — Log Parsing with Regex
**Goal:** Build the second half of your Crown Jewel tool.
**Hour 1 — Core Concept:** Python `re` module basics; regex for IP addresses and timestamps.
**Hour 2 — Lab:** Write `log_parser.py` that reads a sample `auth.log` and extracts failed SSH login attempts (source IP + timestamp) via regex.
**Hour 3 — Documentation:** Test against a synthetic log with 20+ lines; verify correct extraction count. Commit: `"Day 40 completed — log parser built"`.
**Deliverable:** `log_parser.py`.

#### DAY 41 — Argparse & CLI Polish
**Goal:** Make both tools usable from the command line like real utilities.
**Hour 1 — Core Concept:** `argparse` positional vs optional arguments.
**Hour 2 — Lab:** Add `--target`, `--ports`, and `--output` flags to the scanner; add `--file` and `--threshold` flags to the log parser.
**Hour 3 — Documentation:** Write usage examples for both tools. Commit: `"Day 41 completed — CLI flags added"`.
**Deliverable:** Both scripts accept CLI arguments correctly.

#### DAY 42 — Weekly Review & Refactor
**Goal:** Clean, working code ready for Week 8's final polish.
**Hour 1 — Core Concept:** PEP8 style basics.
**Hour 2 — Lab:** Refactor both scripts for readability; add docstrings and inline comments.
**Hour 3 — Documentation:** Push both scripts to `soc-journey/month2-python-tool`. Commit: `"Week 6 completed — Python security tools functional"`.
**Deliverable:** Clean, committed base for the Crown Jewel tool.

---

## Week 7 — Web Fundamentals & OWASP Top 10

### Week 7 Overview

**Theme:** Most real-world breaches start on the web layer. You need fluency in how web apps break.

**Objectives**
- ✅ Understand HTTP methods, status codes, and request/response cycles
- ✅ Exploit SQL injection and XSS in a legal lab environment
- ✅ Understand session/cookie-based authentication
- ✅ Use Burp Suite's Proxy and Repeater

**Success Criteria**
- Can you explain, with an example, how a SQL injection bypasses a login form?
- What's the difference between reflected, stored, and DOM-based XSS?
- What does Burp Suite's Repeater actually let you do?

**Resources**
- PortSwigger Web Security Academy (free account)
- Burp Suite Community Edition

### Week 7 Daily Schedule

#### DAY 43 — How the Web Works
**Goal:** Build the request/response mental model.
**Hour 1 — Core Concept:** Client-server architecture, HTTP methods, status codes.
**Hour 2 — Lab:** PortSwigger — complete "How web applications work" intro material. Use browser dev tools to inspect real requests/responses on a site you visit daily.
**Hour 3 — Documentation:** Note 5 status codes and their meaning. Commit: `"Day 43 completed — HTTP fundamentals"`.
**Deliverable:** HTTP status code reference note.

#### DAY 44 — SQL Injection, Part 1
**Goal:** Successfully bypass a login form via SQLi.
**Hour 1 — Core Concept:** How unsanitized input reaches a SQL query.
**Hour 2 — Lab:** PortSwigger — complete "SQL injection vulnerability in WHERE clause" and "SQL injection allowing login bypass" labs.
**Hour 3 — Documentation:** Write up your payload and why it worked. Commit: `"Day 44 completed — first SQLi labs solved"`.
**Deliverable:** 2 solved SQLi labs, documented.

#### DAY 45 — SQL Injection, Part 2
**Goal:** Extract data via UNION-based injection.
**Hour 1 — Core Concept:** UNION SELECT mechanics, column count matching.
**Hour 2 — Lab:** PortSwigger — complete 2 UNION attack SQLi labs.
**Hour 3 — Documentation:** Document each payload step by step. Commit: `"Day 45 completed — UNION SQLi mastered"`.
**Deliverable:** 2 more solved SQLi labs, documented.

#### DAY 46 — Cross-Site Scripting (XSS)
**Goal:** Understand and exploit the 3 XSS types.
**Hour 1 — Core Concept:** Reflected vs stored vs DOM-based XSS.
**Hour 2 — Lab:** PortSwigger — complete "Reflected XSS into HTML context" and "Stored XSS into HTML context" labs.
**Hour 3 — Documentation:** Diagram the 3 XSS types with one real payload example each. Commit: `"Day 46 completed — XSS fundamentals"`.
**Deliverable:** XSS type diagram + 2 solved labs.

#### DAY 47 — Authentication Mechanics
**Goal:** Understand sessions, cookies, and how auth can fail.
**Hour 1 — Core Concept:** Session tokens, cookie attributes (`HttpOnly`, `Secure`, `SameSite`).
**Hour 2 — Lab:** PortSwigger — complete 2 "Authentication" apprentice labs (username enumeration, brute-force protection bypass).
**Hour 3 — Documentation:** Note what made each authentication flaw exploitable. Commit: `"Day 47 completed — authentication vulnerabilities"`.
**Deliverable:** 2 solved authentication labs.

#### DAY 48 — Burp Suite Fundamentals
**Goal:** Learn the tool professional web testers live in.
**Hour 1 — Core Concept:** Burp's Proxy and Repeater tabs.
**Hour 2 — Lab:** Install Burp Suite Community. Configure your browser to proxy through Burp. Intercept a PortSwigger lab request and replay/modify it in Repeater.
**Hour 3 — Documentation:** Screenshot your intercepted and modified request. Commit: `"Day 48 completed — Burp Suite basics"`.
**Deliverable:** Annotated Burp Repeater screenshot.

#### DAY 49 — Weekly Review
**Goal:** Consolidate OWASP Top 10 knowledge.
**Hour 1 — Core Concept:** Review all Week 7 notes.
**Hour 2 — Lab:** Attempt 1 additional PortSwigger lab of your choice, unaided.
**Hour 3 — Documentation:** Write `owasp-top10-cheatsheet.md` with your own examples for each category covered so far. Commit: `"Week 7 completed — OWASP fundamentals solid"`.
**Deliverable:** `owasp-top10-cheatsheet.md`.

---

## Week 8 — Python Tool Completion (Crown Jewel #2)

### Week 8 Overview

**Theme:** Ship it. A half-finished tool on your laptop is worth nothing — a polished one on GitHub is a portfolio piece.

**Objectives**
- ✅ Add logging, JSON output, and basic tests
- ✅ Merge scanner + parser into one CLI tool with subcommands
- ✅ Write a professional README
- ✅ Run it against your real home lab and capture real output

**Success Criteria**
- Does `python3 tool.py scan --target 10.10.10.2` actually work end to end?
- Do your tests pass?
- Would a hiring manager understand what this tool does within 30 seconds of opening the README?

**Resources**
- Python `logging`, `unittest`/`pytest`, `json` docs

### Week 8 Daily Schedule

#### DAY 50 — Logging
**Goal:** Replace `print()` debugging with real logging.
**Hour 1 — Core Concept:** Python `logging` module — levels, handlers, formatters.
**Hour 2 — Lab:** Add proper logging to both scripts; add a `--verbose` flag that toggles `DEBUG` level.
**Hour 3 — Documentation:** Note log level choices in code comments. Commit: `"Day 50 completed — logging added"`.
**Deliverable:** Logging integrated into both tools.

#### DAY 51 — JSON Output
**Goal:** Make the tool's output usable by other tools.
**Hour 1 — Core Concept:** Structuring scan results as JSON.
**Hour 2 — Lab:** Add `--output json` flag to the scanner that writes results to a `.json` file.
**Hour 3 — Documentation:** Validate the JSON output with `python3 -m json.tool`. Commit: `"Day 51 completed — JSON output"`.
**Deliverable:** Working `--output json` flag.

#### DAY 52 — Basic Testing
**Goal:** Prove your log parser actually works, with tests, not just eyeballing.
**Hour 1 — Core Concept:** `unittest`/`pytest` basics.
**Hour 2 — Lab:** Write 3–5 tests for `log_parser.py` (e.g., correctly counts failed logins from a known sample file).
**Hour 3 — Documentation:** Run `pytest` and screenshot the passing output. Commit: `"Day 52 completed — tests passing"`.
**Deliverable:** Test suite + passing screenshot.

#### DAY 53 — Merge Into One CLI Tool
**Goal:** One polished entry point instead of two loose scripts.
**Hour 1 — Core Concept:** `argparse` subparsers.
**Hour 2 — Lab:** Merge scanner and parser into `tool.py` with subcommands: `tool.py scan ...` and `tool.py parse ...`.
**Hour 3 — Documentation:** Update usage examples for the merged tool. Commit: `"Day 53 completed — unified CLI tool"`.
**Deliverable:** Single `tool.py` with two working subcommands.

#### DAY 54 — Professional README
**Goal:** Write documentation good enough to stand alone in an interview.
**Hour 1 — Core Concept:** Strong technical README structure (purpose, install, usage, limitations).
**Hour 2 — Lab:** Write the full README with real usage examples and sample output.
**Hour 3 — Documentation:** Add a "Limitations & Future Work" section — honesty here builds credibility. Commit: `"Day 54 completed — README written"`.
**Deliverable:** Full `README.md`.

#### DAY 55 — Real-World Test Run
**Goal:** Prove it works against your actual lab, not just localhost.
**Hour 1 — Core Concept:** Review ethical/legal boundaries — only ever scan systems you own or are authorized to test.
**Hour 2 — Lab:** Run the full tool against your home lab VMs (Month 1). Capture real terminal output for the README.
**Hour 3 — Documentation:** Insert real screenshots into the README. Commit: `"Day 55 completed — real-world validation"`.
**Deliverable:** README with real output screenshots.

#### DAY 56 — Publish Crown Jewel #2
**Goal:** Ship the finished, tested, documented tool.
**Hour 1 — Core Concept:** Review how to write a short, genuine LinkedIn project-launch post.
**Hour 2 — Lab:** Final bug pass; clean up repo structure.
**Hour 3 — Documentation:** Push everything to `soc-journey/month2-python-tool`. Draft (don't necessarily post yet) a LinkedIn write-up about the tool.
**Deliverable:** **Crown Jewel #2 — Python Security CLI Tool** live on GitHub.

---

# Chapter 3 — Month 3: Becoming the Analyst

**Chapter Theme:** Detection engineering — moving from "I can use a tool" to "I can explain why this alert fired."
**Mindset Shift:** Proactive threat hunting over reactive log-watching.
**Skill Target:** Splunk SPL, Wazuh deployment, Suricata IDS, alert triage.
**Crown Jewel Project:** A working "Home SOC" — Wazuh + Suricata monitoring your lab, with 5 documented, MITRE-mapped alerts.

---

## Week 9 — SIEM Concepts & Splunk Fundamentals

### Week 9 Overview

**Theme:** A SIEM is where every SOC analyst's day actually happens. This week you learn to ask it questions in its own language.

**Objectives**
- ✅ Explain what a SIEM does and why correlation matters
- ✅ Write SPL queries from scratch
- ✅ Build a basic Splunk dashboard
- ✅ Explore the Boss of the SOC (BOTS) dataset

**Success Criteria**
- What does `index=main sourcetype=access_combined | stats count by src_ip` actually do?
- What's the difference between an index and a sourcetype?
- Can you build a dashboard panel from a saved search?

**Resources**
- TryHackMe: `Introduction to SIEM`, `Splunk: Basics`, `Investigating with Splunk`
- Splunk BOTS v1 dataset (free)

### Week 9 Daily Schedule

#### DAY 57 — What Is a SIEM?
**Goal:** Understand log aggregation, correlation, and alerting at a conceptual level.
**Hour 1 — Core Concept:** THM **Introduction to SIEM** — complete all tasks.
**Hour 2 — Lab:** Sketch how logs would flow from your 3 home-lab VMs into a central SIEM (sources → forwarders → indexer).
**Hour 3 — Documentation:** Save the sketch as `siem-architecture.md`. Commit: `"Day 57 completed — SIEM concepts"`.
**Deliverable:** `siem-architecture.md`.

#### DAY 58 — Splunk Architecture
**Goal:** Understand indexers, forwarders, and sourcetypes.
**Hour 1 — Core Concept:** THM **Splunk: Basics** — complete all tasks.
**Hour 2 — Lab:** Explore the Splunk UI (via THM's hosted instance or Splunk Free locally); identify indexes and sourcetypes present in the sample data.
**Hour 3 — Documentation:** Note 3 real sourcetypes you found and what each represents. Commit: `"Day 58 completed — Splunk architecture"`.
**Deliverable:** Sourcetype reference note.

#### DAY 59 — SPL Fundamentals
**Goal:** Write your first real searches.
**Hour 1 — Core Concept:** Base search syntax, pipes, common commands.
**Hour 2 — Lab:** THM **Investigating with Splunk** — start tasks. Write 5 basic SPL queries against sample data.
**Hour 3 — Documentation:** Log each query and what it returns in `spl-cheatsheet.md`. Commit: `"Day 59 completed — SPL fundamentals"`.
**Deliverable:** `spl-cheatsheet.md` (started).

#### DAY 60 — SPL: stats, eval, table
**Goal:** Move from raw events to summarized answers.
**Hour 1 — Core Concept:** `stats`, `eval`, `table` command syntax.
**Hour 2 — Lab:** Write 10 SPL queries, e.g.:
```
index=main sourcetype=access_combined | stats count by src_ip | sort -count
index=main | eval hour=strftime(_time,"%H") | stats count by hour
```
**Hour 3 — Documentation:** Add all 10 queries to your cheat sheet with plain-English explanations. Commit: `"Day 60 completed — stats/eval/table mastered"`.
**Deliverable:** `spl-cheatsheet.md` updated to 15+ queries.

#### DAY 61 — Building Dashboards
**Goal:** Turn a saved search into a visual panel.
**Hour 1 — Core Concept:** Dashboard panel types (chart, table, single value).
**Hour 2 — Lab:** Build a simple dashboard with 2–3 panels from your saved searches (e.g., top source IPs, events over time).
**Hour 3 — Documentation:** Screenshot the finished dashboard. Commit: `"Day 61 completed — first Splunk dashboard"`.
**Deliverable:** Dashboard screenshot.

#### DAY 62 — Boss of the SOC (BOTS) Dataset
**Goal:** Practice against a realistic, incident-based dataset.
**Hour 1 — Core Concept:** Overview of what BOTS simulates (a real compromise scenario).
**Hour 2 — Lab:** Explore the BOTS v1 dataset (via THM's hosted version or local load); answer 3–5 sample investigative questions using SPL.
**Hour 3 — Documentation:** Write up your findings for those questions. Commit: `"Day 62 completed — BOTS dataset explored"`.
**Deliverable:** BOTS investigation notes.

#### DAY 63 — Weekly Review
**Goal:** Consolidate SPL fluency.
**Hour 1 — Core Concept:** Review all Week 9 notes.
**Hour 2 — Lab:** Complete any remaining THM Splunk room tasks.
**Hour 3 — Documentation:** Finalize `spl-cheatsheet.md`; write `week9-retrospective.md`. Commit: `"Week 9 completed — Splunk fluency achieved"`.
**Deliverable:** Finalized SPL cheat sheet.

---

## Week 10 — Deploy Wazuh

### Week 10 Overview

**Theme:** Stop reading about SIEMs — build one that watches your own lab, live.

**Objectives**
- ✅ Deploy a Wazuh manager
- ✅ Register agents on Windows and Ubuntu
- ✅ Confirm real log ingestion
- ✅ Enable File Integrity Monitoring (FIM)

**Success Criteria**
- Can you show a live Wazuh dashboard with 2 active agents?
- Can you trigger a real alert (failed login or FIM) and see it appear within minutes?

**Resources**
- Official Wazuh documentation and install script

### Week 10 Daily Schedule

#### DAY 64 — Wazuh Manager Install
**Goal:** Stand up the Wazuh server.
**Hour 1 — Core Concept:** Wazuh architecture — manager, indexer, dashboard, agents.
**Hour 2 — Lab:** Provision a new Ubuntu Server VM dedicated to Wazuh. Run the official install script:
```bash
curl -sO https://packages.wazuh.com/4.x/wazuh-install.sh
sudo bash ./wazuh-install.sh -a
```
**Hour 3 — Documentation:** Note install steps and any errors encountered + fixes. Commit: `"Day 64 completed — Wazuh manager installed"`.
**Deliverable:** Wazuh manager running.

#### DAY 65 — Dashboard Access
**Goal:** Confirm the manager is healthy and reachable.
**Hour 1 — Core Concept:** Wazuh dashboard components overview.
**Hour 2 — Lab:** Access the Wazuh dashboard via browser; log in with generated credentials; explore the default views.
**Hour 3 — Documentation:** Screenshot the healthy dashboard. Commit: `"Day 65 completed — dashboard verified"`.
**Deliverable:** Dashboard access confirmed.

#### DAY 66 — Windows Agent
**Goal:** Get your first agent reporting.
**Hour 1 — Core Concept:** Agent-manager communication (registration keys, ports).
**Hour 2 — Lab:** Install the Wazuh agent MSI on your Windows 10 VM; register it against your manager's IP.
**Hour 3 — Documentation:** Confirm agent shows "active" in dashboard; screenshot it. Commit: `"Day 66 completed — Windows agent connected"`.
**Deliverable:** Windows agent active.

#### DAY 67 — Ubuntu Agent
**Goal:** Get a second agent reporting from your Month 1 Ubuntu Server VM.
**Hour 1 — Core Concept:** Log ingestion pipeline concepts (decoders parsing raw logs into fields).
**Hour 2 — Lab:**
```bash
curl -so wazuh-agent.deb https://packages.wazuh.com/4.x/apt/pool/main/w/wazuh-agent/wazuh-agent_amd64.deb
sudo WAZUH_MANAGER='<manager-ip>' dpkg -i ./wazuh-agent.deb
sudo systemctl start wazuh-agent
```
**Hour 3 — Documentation:** Confirm both agents active; screenshot the agent list. Commit: `"Day 67 completed — both agents active"`.
**Deliverable:** 2 active agents (Windows + Ubuntu).

#### DAY 68 — First Real Alert
**Goal:** See a triggered detection end-to-end.
**Hour 1 — Core Concept:** Wazuh rule structure — decoders and rules working together.
**Hour 2 — Lab:** On the Windows VM, deliberately fail a login 3 times. Watch for the corresponding alert in the Wazuh dashboard.
**Hour 3 — Documentation:** Screenshot the alert; note the rule ID that fired. Commit: `"Day 68 completed — first alert confirmed"`.
**Deliverable:** Screenshot of a real, live alert.

#### DAY 69 — File Integrity Monitoring
**Goal:** Enable and test FIM.
**Hour 1 — Core Concept:** How FIM detects unauthorized file changes.
**Hour 2 — Lab:** Enable FIM on a test directory (e.g., `C:\ImportantFiles`) on the Windows agent. Modify a file inside it and confirm Wazuh alerts.
**Hour 3 — Documentation:** Screenshot the FIM alert. Commit: `"Day 69 completed — FIM working"`.
**Deliverable:** FIM alert screenshot.

#### DAY 70 — Weekly Review & Documentation
**Goal:** Consolidate the Wazuh deployment as a reusable artifact.
**Hour 1 — Core Concept:** Review all Week 10 notes.
**Hour 2 — Lab:** Verify both agents and FIM are still stable after a lab reboot.
**Hour 3 — Documentation:** Write full deployment notes (install steps, agent setup, FIM config) to `soc-journey/month3-wazuh`. Commit: `"Week 10 completed — Wazuh SIEM deployed"`.
**Deliverable:** Wazuh deployment documentation published.

---

## Week 11 — IDS/IPS with Suricata

### Week 11 Overview

**Theme:** A SIEM shows you logs. An IDS tells you when someone's actively probing your network.

**Objectives**
- ✅ Understand signature-based vs anomaly-based detection
- ✅ Install and configure Suricata
- ✅ Write a custom detection rule
- ✅ Forward Suricata alerts into Wazuh

**Success Criteria**
- Can Suricata detect and log an Nmap scan against your lab?
- Does that alert also appear inside your Wazuh dashboard, correlated?

**Resources**
- TryHackMe: `Snort` / `Intro to IDS/IPS`
- Suricata official documentation, Emerging Threats (ET Open) ruleset

### Week 11 Daily Schedule

#### DAY 71 — IDS vs IPS Concepts
**Goal:** Understand detection philosophy before touching the tool.
**Hour 1 — Core Concept:** THM **Intro to IDS/IPS** or **Snort** — start tasks.
**Hour 2 — Lab:** Continue THM room; compare signature-based (known patterns) vs anomaly-based (baseline deviation) detection with examples.
**Hour 3 — Documentation:** Write a short comparison note. Commit: `"Day 71 completed — IDS/IPS concepts"`.
**Deliverable:** IDS-vs-IPS comparison note.

#### DAY 72 — Suricata Install
**Goal:** Get Suricata running where it can see lab traffic.
**Hour 1 — Core Concept:** Suricata architecture and deployment placement (inline vs passive).
**Hour 2 — Lab:**
```bash
sudo apt install suricata
sudo suricata -c /etc/suricata/suricata.yaml -i <interface>
```
Install on your pfSense box or a dedicated Ubuntu VM positioned to see lab traffic.
**Hour 3 — Documentation:** Note your interface choice and why. Commit: `"Day 72 completed — Suricata installed"`.
**Deliverable:** Suricata running and logging.

#### DAY 73 — Writing a Custom Rule
**Goal:** Understand rule syntax by writing one yourself.
**Hour 1 — Core Concept:** Rule anatomy: `action protocol src_ip src_port -> dst_ip dst_port (options)`.
**Hour 2 — Lab:** Write a rule to detect ICMP (ping) traffic:
```
alert icmp any any -> any any (msg:"ICMP Ping Detected"; sid:1000001; rev:1;)
```
Ping across the lab and confirm the alert fires.
**Hour 3 — Documentation:** Screenshot the fired alert in the Suricata log. Commit: `"Day 73 completed — custom rule fired"`.
**Deliverable:** Custom rule + fired-alert screenshot.

#### DAY 74 — Community Ruleset & Real Scan Detection
**Goal:** Detect a real reconnaissance technique, not just ICMP.
**Hour 1 — Core Concept:** What the Emerging Threats (ET Open) ruleset covers.
**Hour 2 — Lab:** Enable the ET Open ruleset. From Kali, run:
```bash
nmap -sS 10.10.10.0/24
```
Confirm Suricata logs the scan.
**Hour 3 — Documentation:** Screenshot the scan-detection alert; note the signature that matched. Commit: `"Day 74 completed — scan detected"`.
**Deliverable:** Nmap-scan detection screenshot.

#### DAY 75 — eve.json & SIEM Forwarding
**Goal:** Get Suricata alerts flowing into your SIEM, not sitting in an isolated log file.
**Hour 1 — Core Concept:** Suricata's `eve.json` output format.
**Hour 2 — Lab:** Configure `eve.json` output and forward it into Wazuh (via Filebeat or Wazuh's native Suricata integration).
**Hour 3 — Documentation:** Note the config changes made. Commit: `"Day 75 completed — Suricata-to-Wazuh pipeline built"`.
**Deliverable:** Suricata logs configured to forward to Wazuh.

#### DAY 76 — Correlated Detection
**Goal:** Confirm the full pipeline works end-to-end.
**Hour 1 — Core Concept:** Why correlation across tools (IDS + SIEM) beats either alone.
**Hour 2 — Lab:** Re-run the Day 74 Nmap scan. Confirm the alert now appears inside the Wazuh dashboard.
**Hour 3 — Documentation:** Screenshot the correlated Wazuh alert. Commit: `"Day 76 completed — correlated detection confirmed"`.
**Deliverable:** Screenshot of Suricata alert visible inside Wazuh.

#### DAY 77 — Weekly Review
**Goal:** Document the full IDS integration.
**Hour 1 — Core Concept:** Review all Week 11 notes.
**Hour 2 — Lab:** Verify the pipeline survives a Suricata/Wazuh service restart.
**Hour 3 — Documentation:** Push all Suricata rules and integration notes to `soc-journey/month3-suricata`. Commit: `"Week 11 completed — IDS/SIEM integration live"`.
**Deliverable:** Suricata integration documentation published.

---

## Week 12 — Home SOC Integration (Crown Jewel #3)

### Week 12 Overview

**Theme:** Simulate real attacks against your own lab and prove you can triage them like an analyst on shift.

**Objectives**
- ✅ Simulate 5 distinct attack techniques
- ✅ Triage each using MITRE ATT&CK mapping
- ✅ Build a SOC Runbook table
- ✅ Publish the full Home SOC as Crown Jewel #3

**Success Criteria**
- For each of your 5 simulated attacks, can you state: what fired, what MITRE technique it maps to, and what your disposition was?
- Would this repo convince a hiring manager you can operate in a real SOC?

**Resources**
- MITRE ATT&CK framework (attack.mitre.org)
- Hydra (brute-force tool, lab use only)

### Week 12 Daily Schedule

#### DAY 78 — Attack #1: Reconnaissance (Nmap Scan)
**Goal:** Formally triage a scan as a mapped MITRE technique.
**Hour 1 — Core Concept:** MITRE ATT&CK basics — tactics vs techniques; look up T1046 (Network Service Discovery).
**Hour 2 — Lab:** Re-run an Nmap scan against the lab; capture the Wazuh/Suricata alert.
**Hour 3 — Documentation:** Write a formal disposition: Alert / Source / MITRE Technique / Verdict / Action. Commit: `"Day 78 completed — Attack 1 triaged"`.
**Deliverable:** Case #1 write-up.

#### DAY 79 — Attack #2: Brute-Force
**Goal:** Simulate and detect credential brute-forcing.
**Hour 1 — Core Concept:** T1110 (Brute Force) technique overview.
**Hour 2 — Lab:**
```bash
hydra -l analyst -P rockyou.txt ssh://10.10.10.3
```
Run against your own lab VM only. Capture the resulting alert.
**Hour 3 — Documentation:** Write Case #2 disposition. Commit: `"Day 79 completed — Attack 2 triaged"`.
**Deliverable:** Case #2 write-up.

#### DAY 80 — Attack #3: Malicious PowerShell
**Goal:** Simulate a Living-off-the-Land technique.
**Hour 1 — Core Concept:** T1059.001 (PowerShell) and LOLBins concept.
**Hour 2 — Lab:** In a sandboxed lab VM only, run a benign-but-suspicious-looking PowerShell one-liner (e.g., a script that just writes a test file, styled like a downloader). Capture the alert.
**Hour 3 — Documentation:** Write Case #3 disposition. Commit: `"Day 80 completed — Attack 3 triaged"`.
**Deliverable:** Case #3 write-up.

#### DAY 81 — Attack #4: File Integrity Violation
**Goal:** Trigger and triage a FIM alert as a formal case.
**Hour 1 — Core Concept:** T1565 (Data Manipulation) as a loose mapping for unauthorized file changes.
**Hour 2 — Lab:** Modify a file inside your Day 69 monitored directory; capture the FIM alert.
**Hour 3 — Documentation:** Write Case #4 disposition. Commit: `"Day 81 completed — Attack 4 triaged"`.
**Deliverable:** Case #4 write-up.

#### DAY 82 — Attack #5: Failed Logon Spray + Runbook
**Goal:** Complete the 5th case and assemble the full SOC Runbook.
**Hour 1 — Core Concept:** T1110.003 (Password Spraying) overview.
**Hour 2 — Lab:** Simulate multiple failed logons across accounts; capture the alert.
**Hour 3 — Documentation:** Write Case #5 disposition. Assemble all 5 cases into one `soc-runbook.md` table (Alert / Source / MITRE Technique / Disposition / Action Taken). Commit: `"Day 82 completed — SOC Runbook assembled"`.
**Deliverable:** `soc-runbook.md` with all 5 cases.

#### DAY 83 — Dashboard Presentation
**Goal:** Make the evidence visually compelling.
**Hour 1 — Core Concept:** Dashboard design for clarity (what a hiring manager should see in 10 seconds).
**Hour 2 — Lab:** Build/curate a Wazuh dashboard view showing all 5 alert types together.
**Hour 3 — Documentation:** Take final polished screenshots. Commit: `"Day 83 completed — dashboard finalized"`.
**Deliverable:** Final dashboard screenshot set.

#### DAY 84 — Publish Crown Jewel #3
**Goal:** Ship the complete Home SOC project.
**Hour 1 — Core Concept:** Review strong "security operations" project READMEs for structure ideas.
**Hour 2 — Lab:** Final proofread of all 5 case write-ups and the runbook table.
**Hour 3 — Documentation:** Push architecture diagram, 5 case write-ups, SOC Runbook, and dashboard screenshots to `soc-journey/month3-homesoc`.
**Deliverable:** **Crown Jewel #3 — Home SOC** live on GitHub.

---

# Chapter 4 — Month 4: The Responder

**Chapter Theme:** Calm, methodical, evidence-driven — from detection to action.
**Mindset Shift:** You are now the person others trust during a bad day.
**Skill Target:** NIST 800-61 IR lifecycle, phishing analysis, malware static/dynamic analysis, memory & disk forensics.
**Crown Jewel Project:** A full Incident Response case study — phishing → malware → memory forensics → IOCs → remediation.

---

## Week 13 — Incident Response Lifecycle

### Week 13 Overview

**Theme:** Every real incident, no matter how chaotic, follows a structure. Learn the structure before you're ever in the chaos.

**Objectives**
- ✅ Recite the 6 NIST 800-61 IR phases
- ✅ Classify incidents by severity
- ✅ Apply containment strategy to a hypothetical compromise
- ✅ Draft a reusable Lessons-Learned template

**Success Criteria**
- Can you name and explain all 6 NIST IR phases without notes?
- Given a hypothetical incident, can you assign a severity and justify it?
- What's the difference between containment and eradication?

**Resources**
- TryHackMe: `Incident Response` / `Intro to Digital Forensics`
- NIST SP 800-61 (free PDF)

### Week 13 Daily Schedule

#### DAY 85 — The 6 NIST IR Phases
**Goal:** Learn the framework that structures the rest of this month.
**Hour 1 — Core Concept:** THM **Incident Response** — start tasks. Phases: Preparation, Detection & Analysis, Containment, Eradication, Recovery, Lessons Learned.
**Hour 2 — Lab:** Continue THM room tasks; apply each phase to a made-up scenario (e.g., ransomware on a single workstation).
**Hour 3 — Documentation:** Write `nist-ir-lifecycle.md` with your own explanation of each phase. Commit: `"Day 85 completed — NIST IR lifecycle"`.
**Deliverable:** `nist-ir-lifecycle.md`.

#### DAY 86 — Incident Classification & Severity
**Goal:** Learn to triage by impact, not by panic.
**Hour 1 — Core Concept:** Severity scoring factors — scope, data sensitivity, business impact.
**Hour 2 — Lab:** Continue THM room tasks. Classify 3 hypothetical incidents (e.g., single phishing click, database exfiltration, DDoS) using a sample severity matrix.
**Hour 3 — Documentation:** Write up your 3 classifications with justification. Commit: `"Day 86 completed — severity classification"`.
**Deliverable:** Severity classification write-up.

#### DAY 87 — Chain of Custody
**Goal:** Understand why evidence handling matters, even in a home lab.
**Hour 1 — Core Concept:** THM room — evidence handling tasks.
**Hour 2 — Lab:** Continue THM room tasks. Practice documenting a hypothetical evidence transfer (who, what, when, hash value) as if for a real case.
**Hour 3 — Documentation:** Write a mock chain-of-custody log entry. Commit: `"Day 87 completed — chain of custody"`.
**Deliverable:** Mock chain-of-custody log.

#### DAY 88 — Containment Strategy
**Goal:** Practice making a real containment decision.
**Hour 1 — Core Concept:** Network isolation vs host isolation vs account disablement.
**Hour 2 — Lab:** Given a "compromised" VM in your lab, write out and execute the exact containment steps (e.g., a pfSense rule isolating that VM's subnet segment).
**Hour 3 — Documentation:** Document the containment rule and reasoning. Commit: `"Day 88 completed — containment executed"`.
**Deliverable:** Containment rule + write-up.

#### DAY 89 — Communication & Escalation
**Goal:** Understand the human side of incident response.
**Hour 1 — Core Concept:** THM room — remaining tasks on communication/escalation.
**Hour 2 — Lab:** Draft a mock incident notification email to "management" for a hypothetical breach — clear, non-technical, actionable.
**Hour 3 — Documentation:** Save the mock email as a template. Commit: `"Day 89 completed — communication template"`.
**Deliverable:** Incident notification email template.

#### DAY 90 — Post-Incident Review
**Goal:** Build the template you'll reuse for your Crown Jewel report.
**Hour 1 — Core Concept:** What makes a good Lessons-Learned report (root cause, what worked, what didn't, action items).
**Hour 2 — Lab:** Draft a full Lessons-Learned template with all standard sections.
**Hour 3 — Documentation:** Save the template to `templates/lessons-learned-template.md`. Commit: `"Day 90 completed — lessons-learned template"`.
**Deliverable:** Reusable Lessons-Learned template.

#### DAY 91 — Weekly Review
**Goal:** Consolidate the full IR framework before applying it to real scenarios.
**Hour 1 — Core Concept:** Review all Week 13 notes.
**Hour 2 — Lab:** Complete any remaining THM IR room tasks.
**Hour 3 — Documentation:** Write `week13-retrospective.md` answering all success-criteria questions from memory. Commit: `"Week 13 completed — IR framework internalized"`.
**Deliverable:** `week13-retrospective.md`.

---

## Week 14 — Phishing & Email Header Analysis

### Week 14 Overview

**Theme:** Phishing is still the #1 initial access vector. Learn to dissect an email the way an analyst does.

**Objectives**
- ✅ Read raw email headers for spoofing indicators
- ✅ Check SPF/DKIM/DMARC results
- ✅ Analyze suspicious URLs safely
- ✅ Publish a standalone phishing analysis report

**Success Criteria**
- Given a raw header, can you identify the real sending server vs a spoofed "From" address?
- What do SPF, DKIM, and DMARC each actually check?
- How do you safely check a suspicious URL without visiting it directly?

**Resources**
- TryHackMe: `Phishing Analysis Fundamentals`, `Phishing Emails 1`, `Phishing Emails 2`
- VirusTotal, urlscan.io

### Week 14 Daily Schedule

#### DAY 92 — Email Architecture
**Goal:** Understand SMTP and header structure before analyzing anything.
**Hour 1 — Core Concept:** THM **Phishing Analysis Fundamentals** — complete all tasks.
**Hour 2 — Lab:** Open a raw email header from your own inbox (Gmail: "Show Original"). Identify `Received`, `Return-Path`, `From`, `Reply-To`.
**Hour 3 — Documentation:** Annotate each header field with its purpose. Commit: `"Day 92 completed — email architecture"`.
**Deliverable:** Annotated header breakdown.

#### DAY 93 — Header Spoofing Indicators
**Goal:** Learn to spot a forged sender.
**Hour 1 — Core Concept:** SPF/DKIM/DMARC — what each validates.
**Hour 2 — Lab:** Analyze 3 sample headers (THM-provided) for spoofing red flags; check SPF/DKIM/DMARC pass/fail status on each.
**Hour 3 — Documentation:** Write up your verdict for each of the 3 samples. Commit: `"Day 93 completed — spoofing indicators identified"`.
**Deliverable:** 3-sample header analysis write-up.

#### DAY 94 — URL Analysis
**Goal:** Safely investigate suspicious links.
**Hour 1 — Core Concept:** THM **Phishing Emails 1** — complete all tasks.
**Hour 2 — Lab:** Use urlscan.io and VirusTotal to analyze 2 suspicious URLs from the THM room without visiting them directly in a browser.
**Hour 3 — Documentation:** Document findings for both URLs. Commit: `"Day 94 completed — URL analysis"`.
**Deliverable:** URL analysis write-up.

#### DAY 95 — Attachment Analysis (Hash-First)
**Goal:** Learn the safe first step before ever opening an attachment.
**Hour 1 — Core Concept:** THM **Phishing Emails 2** — complete all tasks.
**Hour 2 — Lab:** Hash a sample attachment (`sha256sum`) and check it against VirusTotal before any further analysis.
**Hour 3 — Documentation:** Document the hash-check workflow and result. Commit: `"Day 95 completed — attachment triage"`.
**Deliverable:** Hash-check write-up.

#### DAY 96 — Real Sample Analysis
**Goal:** Apply the full workflow to real (redacted) samples.
**Hour 1 — Core Concept:** Social engineering tactics catalog — urgency, authority, pretexting.
**Hour 2 — Lab:** Find 2 real phishing samples (phishing museum sites, or your own redacted spam folder). Analyze headers + URLs for both.
**Hour 3 — Documentation:** Note which social engineering tactics each sample used. Commit: `"Day 96 completed — real samples analyzed"`.
**Deliverable:** 2 analyzed real-world samples.

#### DAY 97 — Draft the Report
**Goal:** Turn analysis into a professional deliverable.
**Hour 1 — Core Concept:** Phishing report conventions — Summary, Headers, URLs, IOCs, Verdict, Recommended Action.
**Hour 2 — Lab:** Draft a full standalone phishing analysis report on one of your Day 96 samples.
**Hour 3 — Documentation:** Redact any personal information from screenshots. Commit: `"Day 97 completed — report drafted"`.
**Deliverable:** Draft phishing analysis report.

#### DAY 98 — Publish
**Goal:** Ship a polished, reusable interview artifact.
**Hour 1 — Core Concept:** Final proofreading pass principles for technical reports.
**Hour 2 — Lab:** Polish formatting, verify all screenshots are properly redacted.
**Hour 3 — Documentation:** Push the final report to `soc-journey/month4-phishing-analysis`. Commit: `"Week 14 completed — phishing report published"`.
**Deliverable:** Published phishing analysis report.

---

## Week 15 — Malware Analysis Basics

### Week 15 Overview

**Theme:** Understand what a malicious file actually does — safely, and only in isolation.

**Objectives**
- ✅ Perform static analysis (hashes, strings, PE inspection)
- ✅ Use VirusTotal's multi-engine scanning
- ✅ Perform safe dynamic analysis via sandboxing
- ✅ Extract and document formal IOCs

**Success Criteria**
- Why must malware analysis always happen in an isolated, internet-disconnected-from-host VM?
- What's the difference between static and dynamic analysis?
- What counts as a valid IOC?

**Resources**
- TryHackMe: `Intro to Malware Analysis`
- MalwareBazaar / theZoo (known-safe samples for education)
- PEStudio, any.run (free tier)

### Week 15 Daily Schedule

#### DAY 99 — Malware Analysis Safety & Pyramid
**Goal:** Learn the safety rules before touching any sample.
**Hour 1 — Core Concept:** THM **Intro to Malware Analysis** — complete all tasks. Golden rule: isolated VM, snapshot before, no host-network bridging.
**Hour 2 — Lab:** Set up a dedicated, network-isolated analysis VM (separate from your main lab). Take a clean snapshot.
**Hour 3 — Documentation:** Write your personal "malware analysis safety checklist." Commit: `"Day 99 completed — analysis environment prepared"`.
**Deliverable:** Safety checklist + isolated VM ready.

#### DAY 100 — Static Analysis Tools
**Goal:** Learn what a file reveals before you ever run it.
**Hour 1 — Core Concept:** Hashing, `strings`, PE header structure.
**Hour 2 — Lab:** Download a known-safe educational sample from MalwareBazaar/theZoo (isolated VM only):
```bash
sha256sum sample.exe
strings sample.exe | less
```
Inspect it with PEStudio.
**Hour 3 — Documentation:** Note 3 interesting strings/indicators found. Commit: `"Day 100 completed — static analysis performed"`.
**Deliverable:** Static analysis notes.

#### DAY 101 — VirusTotal Multi-Engine Scanning
**Goal:** Get a broad detection consensus.
**Hour 1 — Core Concept:** How multi-engine AV scanning works, and its limitations.
**Hour 2 — Lab:** Submit the sample's hash (not the file, unless you consent to sharing) to VirusTotal. Review the detection ratio and flagged behaviors.
**Hour 3 — Documentation:** Document the detection ratio and named threats. Commit: `"Day 101 completed — VirusTotal results documented"`.
**Deliverable:** VirusTotal results write-up.

#### DAY 102 — Dynamic Analysis (Sandboxing)
**Goal:** Watch the malware actually behave, safely.
**Hour 1 — Core Concept:** What a sandbox observes — network calls, registry changes, process tree.
**Hour 2 — Lab:** Detonate the sample in any.run (free tier). Observe network connections, registry changes, and spawned processes.
**Hour 3 — Documentation:** Document all observed behaviors. Commit: `"Day 102 completed — dynamic analysis performed"`.
**Deliverable:** Dynamic analysis write-up.

#### DAY 103 — IOC Extraction
**Goal:** Turn observations into a formal, reusable IOC list.
**Hour 1 — Core Concept:** What qualifies as a valid IOC (hash, IP, domain, mutex, registry key).
**Hour 2 — Lab:** Compile a formal IOC table from sample #1's static + dynamic findings.
**Hour 3 — Documentation:** Format the IOC table cleanly (Type / Value / Source). Commit: `"Day 103 completed — IOC list compiled"`.
**Deliverable:** Formal IOC table for sample #1.

#### DAY 104 — Second Sample, Independently
**Goal:** Prove you can repeat the process without hand-holding.
**Hour 1 — Core Concept:** Review your own Day 100–103 notes as your only "guide."
**Hour 2 — Lab:** Repeat full static + dynamic analysis on a second sample (e.g., a documented phishing-delivered payload) independently.
**Hour 3 — Documentation:** Write the full analysis and IOC table for sample #2. Commit: `"Day 104 completed — second analysis complete"`.
**Deliverable:** Full independent analysis of sample #2.

#### DAY 105 — Weekly Review & Publish
**Goal:** Consolidate both write-ups into a portfolio piece.
**Hour 1 — Core Concept:** Review all Week 15 notes.
**Hour 2 — Lab:** Proofread and format both analyses consistently.
**Hour 3 — Documentation:** Push both malware analysis write-ups and IOC lists to `soc-journey/month4-malware-analysis`. Commit: `"Week 15 completed — malware analysis portfolio published"`.
**Deliverable:** 2 published malware analysis reports with IOC lists.

---

## Week 16 — Digital Forensics + IR Case Study (Crown Jewel #4)

### Week 16 Overview

**Theme:** Combine everything from Month 4 into the single most important artifact in your portfolio.

**Objectives**
- ✅ Perform disk forensics with Autopsy
- ✅ Perform memory forensics with Volatility
- ✅ Build a full incident timeline
- ✅ Publish a complete, end-to-end IR case study

**Success Criteria**
- Can you extract a suspicious process and its network connections from a memory image using Volatility?
- Does your final report read like something a real SOC team would produce?

**Resources**
- TryHackMe: `Autopsy`, `Volatility`

### Week 16 Daily Schedule

#### DAY 106 — Disk Forensics with Autopsy
**Goal:** Learn to examine a disk image for evidence.
**Hour 1 — Core Concept:** THM **Autopsy** room — start tasks.
**Hour 2 — Lab:** Continue THM room tasks — load a sample disk image, examine file system artifacts, deleted files, and timeline view.
**Hour 3 — Documentation:** Note 3 interesting artifacts found. Commit: `"Day 106 completed — Autopsy fundamentals"`.
**Deliverable:** Autopsy findings note.

#### DAY 107 — Memory Forensics with Volatility
**Goal:** Learn to examine what was running in memory at time of capture.
**Hour 1 — Core Concept:** THM **Volatility** room — start tasks.
**Hour 2 — Lab:** Continue THM room tasks — identify OS profile, list running processes from a sample memory image.
**Hour 3 — Documentation:** Note the identified profile and process list. Commit: `"Day 107 completed — Volatility fundamentals"`.
**Deliverable:** Volatility basics note.

#### DAY 108 — Volatility Plugins Deep Dive
**Goal:** Extract meaningful, specific evidence — not just a process list.
**Hour 1 — Core Concept:** Key plugins: `pslist`, `netscan`, `malfind`.
**Hour 2 — Lab:**
```bash
vol.py -f memory.img --profile=Win7SP1x64 pslist
vol.py -f memory.img --profile=Win7SP1x64 netscan
vol.py -f memory.img --profile=Win7SP1x64 malfind
```
Extract a suspicious process and its associated network connections.
**Hour 3 — Documentation:** Document the suspicious process, PID, and connections found. Commit: `"Day 108 completed — suspicious process identified"`.
**Deliverable:** Volatility findings write-up.

#### DAY 109 — Timeline Construction
**Goal:** Turn scattered evidence into a coherent chronological story.
**Hour 1 — Core Concept:** Timeline analysis techniques — correlating timestamps across sources.
**Hour 2 — Lab:** Build a timeline combining the phishing chain (Days 92–105 artifacts) with today's forensics findings.
**Hour 3 — Documentation:** Draft the timeline in table form (Time / Event / Source / Evidence). Commit: `"Day 109 completed — incident timeline drafted"`.
**Deliverable:** Draft incident timeline.

#### DAY 110 — Report: Executive Summary & Timeline
**Goal:** Begin writing the Crown Jewel report itself.
**Hour 1 — Core Concept:** Executive Summary conventions — one paragraph a non-technical exec would actually read.
**Hour 2 — Lab:** Write the Executive Summary and finalize the Timeline section of the case study.
**Hour 3 — Documentation:** Save as `ir-case-study.md` section 1–2. Commit: `"Day 110 completed — Exec Summary and Timeline written"`.
**Deliverable:** Report sections 1–2 complete.

#### DAY 111 — Report: Technical Analysis
**Goal:** Write the technical heart of the report.
**Hour 1 — Core Concept:** How to weave multiple evidence sources into one coherent technical narrative.
**Hour 2 — Lab:** Write the Technical Analysis section, combining phishing header analysis + malware sandbox findings + the Volatility excerpt.
**Hour 3 — Documentation:** Insert supporting screenshots inline. Commit: `"Day 111 completed — Technical Analysis written"`.
**Deliverable:** Report section 3 complete.

#### DAY 112 — Finalize & Publish Crown Jewel #4
**Goal:** Complete and ship the single strongest artifact in your portfolio.
**Hour 1 — Core Concept:** Remediation-recommendation conventions — specific, actionable, prioritized.
**Hour 2 — Lab:** Write the IOC Table and Remediation Recommendations sections.
**Hour 3 — Documentation:** Final proofread; push complete case study to `soc-journey/month4-ir-casestudy` with all supporting screenshots.
**Deliverable:** **Crown Jewel #4 — Full IR Case Study** live on GitHub.

---

# Chapter 5 — Month 5: Crossing the Mirror

**Chapter Theme:** You can't defend what you don't understand how to break.
**Mindset Shift:** For every exploit you run, immediately ask "what log entry would this generate?"
**Skill Target:** Web app pentesting, enumeration methodology, privilege escalation, CTF machine completion.
**Crown Jewel Project:** 3–5 fully documented CTF writeups, each including a "detection opportunities" section.

---

## Week 17 — Web App Pentesting Deep Dive

### Week 17 Overview

**Theme:** Go beyond the basics from Month 2 into the vulnerability classes that show up constantly in real bug bounty and pentest work.

**Objectives**
- ✅ Exploit blind and time-based SQL injection
- ✅ Bypass filters with advanced XSS
- ✅ Exploit broken access control
- ✅ Exploit CSRF and SSRF

**Success Criteria**
- How do you extract data via a blind SQLi when there's no visible output?
- What makes an access-control vulnerability different from an authentication vulnerability?
- What's a real-world impact scenario for SSRF?

**Resources**
- PortSwigger Web Security Academy (continue from Month 2)

### Week 17 Daily Schedule

#### DAY 113 — Blind SQL Injection
**Goal:** Extract data with no visible query output.
**Hour 1 — Core Concept:** Boolean-based and time-based blind SQLi theory.
**Hour 2 — Lab:** PortSwigger — complete 2 "Blind SQL injection" labs.
**Hour 3 — Documentation:** Document each payload and how you inferred data without seeing it directly. Commit: `"Day 113 completed — blind SQLi solved"`.
**Deliverable:** 2 solved blind SQLi labs, documented.

#### DAY 114 — DOM-Based & Filter-Bypass XSS
**Goal:** Defeat basic XSS filters.
**Hour 1 — Core Concept:** DOM-based XSS sinks and sources; common filter evasion techniques.
**Hour 2 — Lab:** PortSwigger — complete 2 "DOM-based XSS" or filter-bypass XSS labs.
**Hour 3 — Documentation:** Document the bypass technique used for each. Commit: `"Day 114 completed — advanced XSS solved"`.
**Deliverable:** 2 solved advanced XSS labs.

#### DAY 115 — Broken Access Control
**Goal:** Exploit authorization flaws, not just authentication ones.
**Hour 1 — Core Concept:** Horizontal vs vertical privilege escalation via access control flaws.
**Hour 2 — Lab:** PortSwigger — complete 2 "Access control vulnerabilities" labs.
**Hour 3 — Documentation:** Document each flaw and its business impact. Commit: `"Day 115 completed — access control labs solved"`.
**Deliverable:** 2 solved access-control labs.

#### DAY 116 — CSRF
**Goal:** Understand and exploit cross-site request forgery.
**Hour 1 — Core Concept:** CSRF mechanics — how a forged request rides on an authenticated session.
**Hour 2 — Lab:** PortSwigger — complete 2 "Cross-site request forgery" labs.
**Hour 3 — Documentation:** Document the CSRF PoC HTML used for each. Commit: `"Day 116 completed — CSRF labs solved"`.
**Deliverable:** 2 solved CSRF labs.

#### DAY 117 — SSRF
**Goal:** Understand server-side request forgery and its real-world danger (cloud metadata endpoints, internal network access).
**Hour 1 — Core Concept:** SSRF fundamentals and common real-world impact scenarios.
**Hour 2 — Lab:** PortSwigger — complete 2 "Server-side request forgery" labs.
**Hour 3 — Documentation:** Document each exploit path. Commit: `"Day 117 completed — SSRF labs solved"`.
**Deliverable:** 2 solved SSRF labs.

#### DAY 118 — Authentication Vulnerabilities Revisited
**Goal:** Go deeper than Week 7's authentication basics.
**Hour 1 — Core Concept:** Session fixation, 2FA bypass patterns.
**Hour 2 — Lab:** PortSwigger — complete 2 more "Authentication" labs.
**Hour 3 — Documentation:** Document each flaw. Commit: `"Day 118 completed — advanced authentication labs solved"`.
**Deliverable:** 2 more solved authentication labs.

#### DAY 119 — Weekly Review
**Goal:** Confirm you've built real breadth across OWASP categories.
**Hour 1 — Core Concept:** Review all Week 17 notes.
**Hour 2 — Lab:** Tally your total PortSwigger labs completed (Month 2 + Month 5); aim for 15+.
**Hour 3 — Documentation:** Commit a "PortSwigger completion log" (lab name + one-line technique summary each) to `soc-journey/month5-portswigger`. Commit: `"Week 17 completed — 15+ PortSwigger labs solved"`.
**Deliverable:** PortSwigger completion log.

---

## Week 18 — Enumeration & First Boxes

### Week 18 Overview

**Theme:** Enumeration is 80% of hacking. Build a repeatable methodology instead of guessing.

**Objectives**
- ✅ Build a personal enumeration checklist
- ✅ Use Nmap's scripting engine
- ✅ Root/own an Easy Windows box
- ✅ Root/own an Easy Linux/web box

**Success Criteria**
- Can you walk through your enumeration methodology from memory, in order?
- Did you complete both machines using your own process, not a walkthrough?

**Resources**
- TryHackMe: `Nmap`, machines like `Blue`
- HackTheBox Easy-rated machines

### Week 18 Daily Schedule

#### DAY 120 — Enumeration Methodology
**Goal:** Build the checklist you'll reuse for every future machine.
**Hour 1 — Core Concept:** The enumeration phases: host discovery → port scan → service/version detection → script scanning.
**Hour 2 — Lab:**
```bash
nmap -sn 10.10.10.0/24
nmap -sV -sC -p- 10.10.10.5
```
Run the full methodology against your own lab VM.
**Hour 3 — Documentation:** Write `enumeration-checklist.md`. Commit: `"Day 120 completed — enumeration checklist built"`.
**Deliverable:** `enumeration-checklist.md`.

#### DAY 121 — Nmap Scripting Engine
**Goal:** Go beyond default scans with NSE.
**Hour 1 — Core Concept:** THM **Nmap** room — NSE categories (`vuln`, `default`, `safe`).
**Hour 2 — Lab:** THM **Nmap** room — complete all tasks.
```bash
nmap --script vuln 10.10.10.5
```
**Hour 3 — Documentation:** Note 3 useful NSE scripts and when to use each. Commit: `"Day 121 completed — NSE mastered"`.
**Deliverable:** NSE script reference note.

#### DAY 122 — Machine 1: Recon & Foothold
**Goal:** Start your first real box using your own methodology.
**Hour 1 — Core Concept:** Review common Windows service vulnerabilities (e.g., SMB).
**Hour 2 — Lab:** Start THM **Blue** (or an equivalent Easy-rated Windows box). Perform full enumeration and identify the initial foothold vulnerability.
**Hour 3 — Documentation:** Log your enumeration output and findings so far. Commit: `"Day 122 completed — Machine 1 foothold identified"`.
**Deliverable:** Machine 1 recon notes.

#### DAY 123 — Machine 1: Exploitation
**Goal:** Get a shell and capture the flag.
**Hour 1 — Core Concept:** Review the specific exploit/module you'll use.
**Hour 2 — Lab:** Exploit the identified vulnerability, obtain a shell, and capture the flag.
**Hour 3 — Documentation:** Log the full exploit chain, command by command. Commit: `"Day 123 completed — Machine 1 rooted"`.
**Deliverable:** Machine 1 fully rooted, notes complete.

#### DAY 124 — Machine 2: Recon & Foothold (Linux/Web)
**Goal:** Apply your methodology to a different OS/attack surface.
**Hour 1 — Core Concept:** Web-focused Linux box methodology — directory brute-forcing, CMS enumeration.
**Hour 2 — Lab:**
```bash
gobuster dir -u http://10.10.10.6 -w /usr/share/wordlists/dirb/common.txt
```
Start an Easy-rated Linux/web box; identify the initial foothold.
**Hour 3 — Documentation:** Log enumeration output. Commit: `"Day 124 completed — Machine 2 foothold identified"`.
**Deliverable:** Machine 2 recon notes.

#### DAY 125 — Machine 2: Exploitation
**Goal:** Complete the second box end to end.
**Hour 1 — Core Concept:** Review the specific vulnerability class involved (e.g., file upload, LFI).
**Hour 2 — Lab:** Exploit the vulnerability, obtain a shell, and capture the flag.
**Hour 3 — Documentation:** Log the full exploit chain. Commit: `"Day 125 completed — Machine 2 rooted"`.
**Deliverable:** Machine 2 fully rooted, notes complete.

#### DAY 126 — Weekly Review
**Goal:** Consolidate raw notes ahead of Week 20's polished writeups.
**Hour 1 — Core Concept:** Review all Week 18 notes.
**Hour 2 — Lab:** Reproduce both exploit chains from your notes alone (no re-Googling) to confirm real understanding.
**Hour 3 — Documentation:** Clean up rough notes and screenshots for both machines. Commit: `"Week 18 completed — 2 machines rooted"`.
**Deliverable:** Clean raw notes for 2 machines, ready for Week 20 polish.

---

## Week 19 — Privilege Escalation

### Week 19 Overview

**Theme:** Getting a low-privilege shell is only half the job. Learn to go from user to root/admin.

**Objectives**
- ✅ Identify Linux privesc vectors (SUID, cron, PATH abuse)
- ✅ Identify Windows privesc vectors (unquoted paths, token impersonation)
- ✅ Use LinPEAS and WinPEAS effectively
- ✅ Build a combined privesc cheat sheet

**Success Criteria**
- Given LinPEAS output, can you spot 3 exploitable vectors?
- Given WinPEAS output, can you spot 3 exploitable vectors?

**Resources**
- TryHackMe: `Linux PrivEsc`, `Windows PrivEsc`
- LinPEAS, WinPEAS (PEASS-ng)

### Week 19 Daily Schedule

#### DAY 127 — Linux PrivEsc, Part 1
**Goal:** Learn SUID and cron-based privesc.
**Hour 1 — Core Concept:** THM **Linux PrivEsc** — start tasks (SUID, cron jobs).
**Hour 2 — Lab:**
```bash
find / -perm -4000 -type f 2>/dev/null
cat /etc/crontab
```
Complete the SUID and cron sections of the THM room.
**Hour 3 — Documentation:** Note 3 exploitable SUID binaries and why. Commit: `"Day 127 completed — SUID/cron privesc"`.
**Deliverable:** SUID/cron privesc notes.

#### DAY 128 — Linux PrivEsc, Part 2
**Goal:** Learn PATH abuse, NFS, and capabilities-based privesc.
**Hour 1 — Core Concept:** PATH variable abuse, NFS `no_root_squash`, Linux capabilities.
**Hour 2 — Lab:** THM **Linux PrivEsc** — complete remaining sections.
**Hour 3 — Documentation:** Add these 3 new vectors to your growing notes. Commit: `"Day 128 completed — Linux PrivEsc room finished"`.
**Deliverable:** Completed THM Linux PrivEsc notes.

#### DAY 129 — LinPEAS
**Goal:** Learn to read automated enumeration output like a pro.
**Hour 1 — Core Concept:** How LinPEAS categorizes and color-codes findings.
**Hour 2 — Lab:**
```bash
./linpeas.sh > linpeas_output.txt
```
Run against a lab VM you intentionally misconfigured; identify 3 privesc vectors from the output.
**Hour 3 — Documentation:** Write up the 3 vectors found and how you'd exploit each. Commit: `"Day 129 completed — LinPEAS analysis"`.
**Deliverable:** LinPEAS findings write-up.

#### DAY 130 — Windows PrivEsc, Part 1
**Goal:** Learn unquoted service paths and AlwaysInstallElevated.
**Hour 1 — Core Concept:** THM **Windows PrivEsc** — start tasks.
**Hour 2 — Lab:**
```powershell
wmic service get name,pathname,startmode
reg query "HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer" /v AlwaysInstallElevated
```
**Hour 3 — Documentation:** Note findings so far. Commit: `"Day 130 completed — Windows PrivEsc started"`.
**Deliverable:** Windows PrivEsc notes (part 1).

#### DAY 131 — Windows PrivEsc, Part 2
**Goal:** Learn token impersonation and remaining vectors.
**Hour 1 — Core Concept:** Token impersonation concept (e.g., PrintSpoofer-style attacks).
**Hour 2 — Lab:** THM **Windows PrivEsc** — complete remaining tasks.
**Hour 3 — Documentation:** Add these vectors to your notes. Commit: `"Day 131 completed — Windows PrivEsc room finished"`.
**Deliverable:** Completed THM Windows PrivEsc notes.

#### DAY 132 — WinPEAS
**Goal:** Practice reading automated Windows enumeration output.
**Hour 1 — Core Concept:** How WinPEAS highlights likely privesc vectors.
**Hour 2 — Lab:**
```powershell
.\winpeas.exe > winpeas_output.txt
```
Run against your Windows lab VM; identify 3 privesc vectors from the output.
**Hour 3 — Documentation:** Write up the 3 vectors found. Commit: `"Day 132 completed — WinPEAS analysis"`.
**Deliverable:** WinPEAS findings write-up.

#### DAY 133 — Weekly Review
**Goal:** Build the combined cheat sheet you'll use for the rest of your career.
**Hour 1 — Core Concept:** Review all Week 19 notes.
**Hour 2 — Lab:** Reproduce one Linux and one Windows privesc technique from memory, unaided.
**Hour 3 — Documentation:** Publish a combined Linux + Windows privesc cheat sheet (in your own words) to `soc-journey/month5-privesc`. Commit: `"Week 19 completed — privesc cheat sheet published"`.
**Deliverable:** Combined privesc cheat sheet.

---

## Week 20 — CTF Writeups Portfolio (Crown Jewel #5)

### Week 20 Overview

**Theme:** Package your offensive work into the portfolio format that recruiters and hiring managers actually read.

**Objectives**
- ✅ Write 2 polished writeups for Machines 1 & 2 (Week 18)
- ✅ Root and document 2 new Easy machines
- ✅ Include a "detection opportunities" section in every writeup
- ✅ Publish the full portfolio

**Success Criteria**
- Does every writeup follow: Recon → Foothold → Privesc → Root → Detection Opportunities?
- Would a SOC hiring manager (not just a pentest one) find these relevant?

**Resources**
- HackTheBox / TryHackMe Easy-rated machines

### Week 20 Daily Schedule

#### DAY 134 — Writeup: Machine 1
**Goal:** Convert raw notes into a polished writeup.
**Hour 1 — Core Concept:** Technical writeup structure — Recon, Foothold, Privesc, Root, Detection Opportunities.
**Hour 2 — Lab:** Write the full polished writeup for Machine 1 using your Week 18 notes.
**Hour 3 — Documentation:** Format with headers, code blocks, and screenshots. Commit: `"Day 134 completed — Machine 1 writeup published"`.
**Deliverable:** Polished Machine 1 writeup.

#### DAY 135 — Writeup: Machine 2 + Detection Opportunities
**Goal:** Learn to map exploit steps to what a SOC would actually see.
**Hour 1 — Core Concept:** How to map exploit steps to log sources and MITRE techniques.
**Hour 2 — Lab:** Write the full polished writeup for Machine 2, including a Detection Opportunities section (what log/alert would have caught this).
**Hour 3 — Documentation:** Finalize formatting. Commit: `"Day 135 completed — Machine 2 writeup published"`.
**Deliverable:** Polished Machine 2 writeup with detection section.

#### DAY 136 — Machine 3: Recon & Root
**Goal:** Add a third machine to the portfolio.
**Hour 1 — Core Concept:** Review your enumeration checklist before starting.
**Hour 2 — Lab:** Choose and fully root/own a new Easy-rated machine (recon → foothold → privesc → root), end to end.
**Hour 3 — Documentation:** Log raw notes and screenshots as you go. Commit: `"Day 136 completed — Machine 3 rooted"`.
**Deliverable:** Machine 3 rooted, raw notes complete.

#### DAY 137 — Writeup: Machine 3
**Goal:** Polish Machine 3 into portfolio format.
**Hour 1 — Core Concept:** Review your own Day 134–135 writeups as a style guide for consistency.
**Hour 2 — Lab:** Write the full polished writeup for Machine 3, including Detection Opportunities.
**Hour 3 — Documentation:** Finalize formatting. Commit: `"Day 137 completed — Machine 3 writeup published"`.
**Deliverable:** Polished Machine 3 writeup.

#### DAY 138 — Machine 4: Recon & Root
**Goal:** Add a fourth machine, ideally a different OS than the others.
**Hour 1 — Core Concept:** Review your privesc cheat sheet before starting.
**Hour 2 — Lab:** Choose and fully root/own a new Easy-rated machine (different OS if possible).
**Hour 3 — Documentation:** Log raw notes and screenshots as you go. Commit: `"Day 138 completed — Machine 4 rooted"`.
**Deliverable:** Machine 4 rooted, raw notes complete.

#### DAY 139 — Writeup: Machine 4
**Goal:** Complete the fourth writeup and decide on scope for Day 140.
**Hour 1 — Core Concept:** Review overall portfolio consistency (formatting, tone, depth).
**Hour 2 — Lab:** Write the full polished writeup for Machine 4, including Detection Opportunities.
**Hour 3 — Documentation:** Decide: attempt a 5th machine, or spend Day 140 polishing existing 4. Commit: `"Day 139 completed — Machine 4 writeup published"`.
**Deliverable:** Polished Machine 4 writeup.

#### DAY 140 — Publish Crown Jewel #5
**Goal:** Ship the complete CTF writeups portfolio.
**Hour 1 — Core Concept:** Platform rules on flag redaction — always redact actual flag values in public writeups.
**Hour 2 — Lab:** Final formatting pass across all writeups; ensure consistency.
**Hour 3 — Documentation:** Publish all writeups with an index README to `soc-journey/month5-ctf-writeups`.
**Deliverable:** **Crown Jewel #5 — CTF Writeups Portfolio** (3–5 machines) live on GitHub.

---

# Chapter 6 — Month 6: The Launch

**Chapter Theme:** You are no longer "learning security" — you are a practitioner with evidence. Interviews become a demo, not a test.
**Mindset Shift:** Confident, articulate, evidence-backed communication.
**Skill Target:** Security+ level knowledge, resume/LinkedIn/GitHub as a coherent narrative, interview performance.
**Crown Jewel Project (Capstone):** A polished portfolio hub tying all 5 prior projects together, plus a flagship "Detecting and Responding to a Simulated Ransomware Attack" report.

---

## Week 21 — Security+ Domain Review Sprint

### Week 21 Overview

**Theme:** Consolidate the theory that ties everything you've built together — and decide, honestly, whether sitting the exam is the best use of your remaining weeks.

**Objectives**
- ✅ Review all 5 Security+ domains
- ✅ Complete two full-length timed practice exams
- ✅ Identify and close remaining knowledge gaps
- ✅ Make a clear-eyed go/no-go decision on the actual exam

**Success Criteria**
- Are you scoring 85%+ on consecutive full practice exams?
- For each domain, can you explain the core concept in one sentence?

**Resources**
- Professor Messer Security+ free video series
- Free Security+ practice question banks

### Week 21 Daily Schedule

#### DAY 141 — Domain 1: General Security Concepts
**Goal:** Refresh and formalize your foundational knowledge.
**Hour 1 — Core Concept:** Professor Messer — Domain 1 videos.
**Hour 2 — Lab:** Complete 30 practice questions on Domain 1.
**Hour 3 — Documentation:** Log weak areas in `sec-plus-gaps.md`. Commit: `"Day 141 completed — Domain 1 reviewed"`.
**Deliverable:** Domain 1 practice score + gap log.

#### DAY 142 — Domain 2: Threats, Vulnerabilities, Mitigations
**Goal:** Connect this domain to your actual lab experience — it should feel familiar.
**Hour 1 — Core Concept:** Professor Messer — Domain 2 videos.
**Hour 2 — Lab:** Complete 30 practice questions on Domain 2; review Day 141's weak areas.
**Hour 3 — Documentation:** Update `sec-plus-gaps.md`. Commit: `"Day 142 completed — Domain 2 reviewed"`.
**Deliverable:** Domain 2 practice score + updated gap log.

#### DAY 143 — Domain 3: Security Architecture
**Goal:** Solidify architecture-level thinking.
**Hour 1 — Core Concept:** Professor Messer — Domain 3 videos.
**Hour 2 — Lab:** Complete 30 practice questions on Domain 3.
**Hour 3 — Documentation:** Update `sec-plus-gaps.md`. Commit: `"Day 143 completed — Domain 3 reviewed"`.
**Deliverable:** Domain 3 practice score.

#### DAY 144 — Domain 4: Security Operations
**Goal:** Confirm this domain feels easy — it's what you've been living for 3 months.
**Hour 1 — Core Concept:** Professor Messer — Domain 4 videos.
**Hour 2 — Lab:** Complete 30 practice questions on Domain 4.
**Hour 3 — Documentation:** Note how much of this overlapped with your Home SOC and IR work. Commit: `"Day 144 completed — Domain 4 reviewed"`.
**Deliverable:** Domain 4 practice score.

#### DAY 145 — Domain 5: Security Program Management & Oversight
**Goal:** Cover governance, risk, and compliance basics.
**Hour 1 — Core Concept:** Professor Messer — Domain 5 videos.
**Hour 2 — Lab:** Complete 30 practice questions on Domain 5.
**Hour 3 — Documentation:** Update `sec-plus-gaps.md`. Commit: `"Day 145 completed — Domain 5 reviewed"`.
**Deliverable:** Domain 5 practice score.

#### DAY 146 — Full Practice Exam #1
**Goal:** Simulate real exam conditions.
**Hour 1 — Core Concept:** Review exam-day logistics and question-style expectations.
**Hour 2 — Lab:** Take a full-length, timed practice exam under real conditions (no notes, timed).
**Hour 3 — Documentation:** Review every missed question in depth; re-study those specific sub-topics. Commit: `"Day 146 completed — Practice Exam 1 taken"`.
**Deliverable:** Practice Exam 1 score + missed-question review.

#### DAY 147 — Full Practice Exam #2 & Go/No-Go Decision
**Goal:** Confirm readiness and make the call.
**Hour 1 — Core Concept:** Review your Day 146 missed-question notes one more time.
**Hour 2 — Lab:** Take a second full-length, timed practice exam.
**Hour 3 — Documentation:** Review every missed question. Per the Reality Check: if 85%+ on both, schedule the real exam; if not, consciously choose to deprioritize it and protect Weeks 23–24. Commit: `"Week 21 completed — exam readiness assessed"`.
**Deliverable:** Practice Exam 2 score + documented go/no-go decision.

---

## Week 22 — Portfolio, Resume, LinkedIn Polish + Capstone Build

### Week 22 Overview

**Theme:** Turn five months of real work into a narrative a recruiter can understand in 30 seconds.

**Objectives**
- ✅ Rewrite resume around your projects, tailored to real job postings
- ✅ Rebuild LinkedIn headline and About section
- ✅ Build a GitHub profile README
- ✅ Build the capstone ransomware-simulation project to ~80%

**Success Criteria**
- Does your resume's "Projects" section lead, not your education?
- Does your GitHub profile README make your 5 Crown Jewels the first thing a visitor sees?
- Is your capstone attack chain fully triggered and detected?

**Resources**
- Real SOC Analyst job postings (10+, for keyword research)
- EICAR test file (safe, industry-standard "malware" test string)

### Week 22 Daily Schedule

#### DAY 148 — Job Posting Research & Resume Rewrite
**Goal:** Ground your resume in what employers are actually asking for.
**Hour 1 — Core Concept:** Analyze 10 real SOC Analyst job postings for common keywords and requirements.
**Hour 2 — Lab:** Rewrite your resume: 1 page, quantified bullet points, tailored to the keywords found.
**Hour 3 — Documentation:** Save both the keyword research and the resume draft. Commit: `"Day 148 completed — resume rewritten"`.
**Deliverable:** Job-posting keyword research + resume draft v1.

#### DAY 149 — Resume "Projects" Section
**Goal:** Make your Crown Jewels the headline of your resume.
**Hour 1 — Core Concept:** Strong technical resume "Projects" section examples.
**Hour 2 — Lab:** Write a "Projects" section listing all 5 Crown Jewels with a 1-line impact statement each, linked to their GitHub repos.
**Hour 3 — Documentation:** Finalize resume v2. Commit: `"Day 149 completed — Projects section added"`.
**Deliverable:** Resume v2 with Projects section.

#### DAY 150 — LinkedIn Rebuild
**Goal:** Make your LinkedIn presence match your actual work.
**Hour 1 — Core Concept:** Effective LinkedIn "About" sections for career-changers.
**Hour 2 — Lab:** Rewrite LinkedIn headline and About section. Publish your Day 56 draft post about the Python tool.
**Hour 3 — Documentation:** Save your final LinkedIn copy for reference. Commit: `"Day 150 completed — LinkedIn rebuilt"`.
**Deliverable:** Updated LinkedIn profile + 1 published post.

#### DAY 151 — GitHub Profile README
**Goal:** Make your GitHub itself a portfolio landing page.
**Hour 1 — Core Concept:** GitHub profile README best practices (pinned repos, skills badges, short bio).
**Hour 2 — Lab:** Build a GitHub profile README pinning your 5 Crown Jewels with a short bio and skills badges.
**Hour 3 — Documentation:** Proofread and finalize. Commit: `"Day 151 completed — GitHub profile README published"`.
**Deliverable:** Live GitHub profile README.

#### DAY 152 — Capstone: Attack Simulation
**Goal:** Build the technical core of your final flagship project.
**Hour 1 — Core Concept:** Map how Home SOC + IR skills + attacker knowledge combine into one ransomware simulation story.
**Hour 2 — Lab:** Set up the capstone scenario in your lab: simulate an initial phishing foothold, then a safe "ransomware" execution using an EICAR-based or custom benign encryptor test script — never a real malicious payload.
**Hour 3 — Documentation:** Log each step of the simulated attack chain. Commit: `"Day 152 completed — capstone attack simulated"`.
**Deliverable:** Capstone attack chain executed in the lab.

#### DAY 153 — Capstone: Detection & Narrative
**Goal:** Prove your defenses actually caught it.
**Hour 1 — Core Concept:** Review how to structure a combined attack-and-detection narrative.
**Hour 2 — Lab:** Trigger Wazuh/Suricata detection of the simulated attack; capture all resulting alerts.
**Hour 3 — Documentation:** Begin writing the capstone narrative (attack steps ↔ detection points). Commit: `"Day 153 completed — capstone detection captured"`.
**Deliverable:** Capstone alerts captured + narrative draft started.

#### DAY 154 — Weekly Review & External Feedback
**Goal:** Get outside eyes on your work before Week 23's interview prep.
**Hour 1 — Core Concept:** Review all Week 22 output for consistency across resume/LinkedIn/GitHub.
**Hour 2 — Lab:** Finish the capstone draft to ~80% completion.
**Hour 3 — Documentation:** Get feedback on resume/LinkedIn from 1–2 people (r/cybersecurity, a Discord community, or a mentor). Commit: `"Week 22 completed — portfolio polished, capstone 80% done"`.
**Deliverable:** Resume, LinkedIn, GitHub profile finalized; capstone ~80% complete.

---

## Week 23 — Mock Interviews & Behavioral Prep

### Week 23 Overview

**Theme:** All the work means nothing if you can't articulate it clearly under pressure. This week is about the demo, not new material.

**Objectives**
- ✅ Prepare answers to 10 common SOC technical questions
- ✅ Prepare STAR-format answers to 5 behavioral questions
- ✅ Complete 3 mock interviews
- ✅ Publish the finished capstone

**Success Criteria**
- Can you answer any of the 5 target behavioral questions fluently, without notes?
- Can you narrate a real log-triage scenario using your own Home SOC project as evidence?

**Resources**
- r/cybersecurity mock interview threads, local meetups, career centers
- STAR method reference

### Week 23 Daily Schedule

#### DAY 155 — Technical Question Prep
**Goal:** Ground every technical answer in your own project evidence.
**Hour 1 — Core Concept:** Common SOC Analyst technical interview questions (e.g., "walk me through triaging an alert").
**Hour 2 — Lab:** Write out full answers to 10 common technical questions, each referencing a specific project you built.
**Hour 3 — Documentation:** Save all 10 answers in `interview-prep.md`. Commit: `"Day 155 completed — technical answers drafted"`.
**Deliverable:** 10 drafted technical answers.

#### DAY 156 — Behavioral Question Prep (STAR)
**Goal:** Structure your personal stories for maximum clarity.
**Hour 1 — Core Concept:** The STAR method — Situation, Task, Action, Result.
**Hour 2 — Lab:** Draft STAR-format answers for the 5 target behavioral questions (see the Candidate Profile at the end of this handbook).
**Hour 3 — Documentation:** Save all 5 STAR answers. Commit: `"Day 156 completed — STAR answers drafted"`.
**Deliverable:** 5 drafted STAR answers.

#### DAY 157 — Mock Interview #1 (Technical Focus)
**Goal:** Test your technical answers out loud, under mild pressure.
**Hour 1 — Core Concept:** Review your Day 155 answers once more.
**Hour 2 — Lab:** Conduct a mock interview (peer, mentor, or AI role-play) — 5 technical questions. Record yourself.
**Hour 3 — Documentation:** Review the recording for clarity/confidence gaps; note what to fix. Commit: `"Day 157 completed — Mock Interview 1 done"`.
**Deliverable:** Mock Interview #1 recording + self-review notes.

#### DAY 158 — Mock Interview #2 (Behavioral Focus)
**Goal:** Tighten your weakest behavioral answers.
**Hour 1 — Core Concept:** Review Day 157's feedback.
**Hour 2 — Lab:** Redo your weakest STAR answers based on that feedback; conduct a second mock interview focused on behavioral questions.
**Hour 3 — Documentation:** Note remaining gaps. Commit: `"Day 158 completed — Mock Interview 2 done"`.
**Deliverable:** Mock Interview #2 completed + revised STAR answers.

#### DAY 159 — Mock Interview #3 (Real Person, Full Loop)
**Goal:** Get the most realistic practice possible before applications begin.
**Hour 1 — Core Concept:** Quick research on entry-level SOC market rates and basic negotiation posture.
**Hour 2 — Lab:** Conduct Mock Interview #3, ideally with a real person (r/cybersecurity mock interview thread, local meetup, or career center).
**Hour 3 — Documentation:** Log all feedback received. Commit: `"Day 159 completed — Mock Interview 3 done"`.
**Deliverable:** Mock Interview #3 completed + feedback log.

#### DAY 160 — Close the Gaps
**Goal:** Fix your single weakest area before Week 24 begins.
**Hour 1 — Core Concept:** Review all 3 mock interviews' feedback together; identify the one recurring weakness.
**Hour 2 — Lab:** Targeted drilling on that weakest area (technical depth or communication clarity) — repeat the relevant answer 5+ times until fluent.
**Hour 3 — Documentation:** Update `interview-prep.md` with the improved answer. Commit: `"Day 160 completed — weakest area addressed"`.
**Deliverable:** Improved, fluent answer to your weakest question type.

#### DAY 161 — Capstone Finalization
**Goal:** Ship the final Crown Jewel before the application sprint begins.
**Hour 1 — Core Concept:** Final review of capstone narrative structure.
**Hour 2 — Lab:** Complete any remaining capstone sections; finalize screenshots and formatting.
**Hour 3 — Documentation:** Publish the finished capstone to `soc-journey/month6-capstone`; finalize a portfolio hub README linking all 6 projects. Commit: `"Week 23 completed — capstone published, interview-ready"`.
**Deliverable:** **Crown Jewel #6 — Capstone Ransomware Detection & Response** live on GitHub; full portfolio hub linking all 6 projects.

---

## Week 24 — Application Sprint

### Week 24 Overview

**Theme:** Execution week. Everything you've built exists to make this week effective.

**Objectives**
- ✅ Submit 20+ tailored applications
- ✅ Start 3+ genuine networking conversations
- ✅ Track everything in an application pipeline
- ✅ Publish a public retrospective on your 6-month journey

**Success Criteria**
- Is your portfolio linked in every application and outreach message?
- Have you had at least 3 real conversations with people in the field this week, not just cold-submitted forms?

**Resources**
- LinkedIn Jobs, company career pages, r/cybersecurity job threads
- A simple spreadsheet (Google Sheets is fine) for tracking

### Week 24 Daily Schedule

#### DAY 162 — Build the Pipeline
**Goal:** Set up a system before you start applying blindly.
**Hour 1 — Core Concept:** How Applicant Tracking Systems (ATS) parse resumes and why keyword matching matters.
**Hour 2 — Lab:** Set up a tracking spreadsheet (Company / Role / Date Applied / Status / Contact). Identify 30 target roles from the Candidate Profile job-title list below.
**Hour 3 — Documentation:** Finalize the spreadsheet structure. Commit process notes to `soc-journey`. 
**Deliverable:** Application tracking spreadsheet with 30 target roles identified.

#### DAY 163 — Applications Batch 1 + Outreach
**Goal:** Start executing.
**Hour 1 — Core Concept:** Effective, non-spammy cold outreach/networking message structure.
**Hour 2 — Lab:** Send 5 tailored applications (custom resume tweaks per posting). Send 3 personalized LinkedIn connection requests to SOC analysts or hiring managers.
**Hour 3 — Documentation:** Log all 5 applications and 3 outreach messages in your spreadsheet.
**Deliverable:** 5 applications submitted, 3 outreach messages sent.

#### DAY 164 — Applications Batch 2 + Informational Interview Outreach
**Goal:** Keep momentum and add a deeper networking touch.
**Hour 1 — Core Concept:** Research one target company's security posture (news, blog, culture) for a potential referral conversation.
**Hour 2 — Lab:** Send 5 more applications. Send 1 informational-interview request message.
**Hour 3 — Documentation:** Log progress in your spreadsheet.
**Deliverable:** 5 more applications submitted (10 total), 1 informational-interview request sent.

#### DAY 165 — Applications Batch 3 + Interview Prep
**Goal:** Keep the pipeline moving while staying ready for responses.
**Hour 1 — Core Concept:** Review your `interview-prep.md` answers once more.
**Hour 2 — Lab:** Send 5 more applications. Prepare for any interviews scheduled this week.
**Hour 3 — Documentation:** Log progress in your spreadsheet.
**Deliverable:** 5 more applications submitted (15 total).

#### DAY 166 — Applications Batch 4 + Follow-Ups
**Goal:** Don't let Day 163's outreach go cold.
**Hour 1 — Core Concept:** Effective, brief follow-up message structure (no more than 2 lines).
**Hour 2 — Lab:** Send 5 more applications. Follow up on Day 163's LinkedIn connections that haven't responded.
**Hour 3 — Documentation:** Log progress in your spreadsheet.
**Deliverable:** 5 more applications submitted (20 total).

#### DAY 167 — Applications Batch 5 + Community Engagement
**Goal:** Round out the application count and build genuine visibility.
**Hour 1 — Core Concept:** Review your capstone and phishing/IR reports once more — these are what you'll be discussing if a call comes.
**Hour 2 — Lab:** Send remaining applications to exceed 20 total. Genuinely engage in one r/cybersecurity or Discord community thread — answer someone else's question, don't just self-promote.
**Hour 3 — Documentation:** Log final application count.
**Deliverable:** 20+ applications submitted total.

#### DAY 168 — Retrospective & Recruiter Reach
**Goal:** Close the loop on 6 months of work, and put your story where employers can find it.
**Hour 1 — Core Concept:** Review your entire `soc-journey` repository from Day 1 to today.
**Hour 2 — Lab:** Reach out directly to 1–2 recruiters at target companies with a short, specific message linking your portfolio.
**Hour 3 — Documentation:** Write and publish a public "My 6-Month Journey into Cybersecurity" post (LinkedIn or blog) summarizing the path and linking your portfolio hub. Commit: `"Day 168 completed — 6-month roadmap finished"`.
**Deliverable:** Public retrospective published; 20+ applications submitted; full portfolio live and linked everywhere.

---

# Chapter 7 — The Final Candidate Profile (End of Month 6)

## GitHub Snapshot

A `soc-journey` GitHub presence with a profile README pinning your 6 Crown Jewels:

1. **Home Lab** — topology diagram + annotated packet captures
2. **Python Security Tool** — multi-threaded scanner + log parser, tested and documented
3. **Home SOC** — Wazuh + Suricata, 5 triaged, MITRE-mapped alerts
4. **Incident Response Case Study** — phishing → malware → memory forensics → remediation
5. **CTF Writeups Portfolio** — 3–5 machines, each with a Detection Opportunities section
6. **Capstone** — simulated ransomware attack, detected and documented end to end

168+ days of visible commit activity. Every repo has a clear README, real screenshots, and a "what I learned" section.

## Resume Snapshot

One page. Header with GitHub and LinkedIn links. A **Projects** section leading — not buried under Education — with all 6 Crown Jewels and a quantified impact line for each (e.g., *"Deployed Wazuh SIEM and Suricata IDS across a 4-host lab; detected and triaged 5 simulated attack techniques mapped to MITRE ATT&CK"*). A Skills section matched directly to real job-posting keywords.

## LinkedIn Snapshot

**Headline:** *"Aspiring SOC Analyst | Home-Lab SIEM, IR, and Detection Engineering | Python for Security."*

**About:** 4–5 sentences telling the honest transition story, linking the portfolio hub. 3 posts published across the journey (Month 2 tool launch, Month 4 IR case study, Month 6 retrospective) showing sustained public momentum — not a resume that appeared overnight.

## The 5 Technical Skills You Will Dominate

1. **Log analysis & SIEM triage** (Splunk SPL + Wazuh dashboards) — raw alert to disposition, fast.
2. **Network traffic analysis** (Wireshark, protocol-level reasoning).
3. **Incident response methodology** (NIST 800-61, applied to a real documented case).
4. **Scripting for security automation** (Python — built from scratch, understood line by line).
5. **Offensive fundamentals in defensive context** (enumeration, common exploitation, and — critically — mapping every exploit to its detection signature).

## The 5 Behavioral Questions You Will Ace

1. *"Tell me about a time you had to learn something quickly under pressure."* → Your Wazuh deployment week, or the Week 16 IR case-study crunch.
2. *"Describe a time you found a mistake in your own work."* → A real debugging moment from the Python tool, or a misconfigured Wazuh rule you caught and fixed.
3. *"How do you prioritize when everything feels urgent?"* → Triaging your 5 Home SOC alerts, or juggling the Week 12/16/20 Crown Jewel deadlines.
4. *"Tell me about a time you had to explain something technical to a non-technical audience."* → Your README explanations, or the phishing report's plain-language verdict section.
5. *"Why security, and why now?"* → Your authentic, provable 6-month transition story — the portfolio sitting right there is the proof.

## Job Titles to Target in Week 24

- SOC Analyst I / Tier 1 SOC Analyst
- Security Operations Analyst
- Cybersecurity Analyst (entry-level / associate)
- Information Security Analyst I
- Threat Detection Analyst (entry-level)
- Junior Penetration Tester / Associate Penetration Tester (stretch — apply selectively where the writeup portfolio is strong)
- Security Monitoring Analyst
- IT Security Analyst (entry-level, especially at MSSPs — often the most realistic first door in)

---

## Closing Note — The Honest Reality Check

No roadmap guarantees a job. Market conditions, geography, and timing all matter, and entry-level security hiring is genuinely competitive right now. What this handbook guarantees, if followed, is that you will not walk in as an unproven candidate. You will walk in with six real, defensible, hands-on projects and a demonstrated six-month pattern of daily discipline — which is exactly what separates hired candidates from the pile of "I have a cert but no lab" resumes.

**If you finish a week early:** move on to the next week's Day 1 rather than idling — momentum compounds.
**If you fall behind:** protect the Crown Jewel deliverable for that month above all else; compress theory, not hands-on practice.
