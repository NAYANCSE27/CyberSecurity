# Zero-to-Hired Cybersecurity Roadmap (Version 2026)
### A Complete 6-Month Handbook

---

# Chapter 5 — Month 5: Web Application Security and the Junior Pentester Stretch Goal

Theme of the month: **You learn to think like the adversary you've spent four months defending against.**
Even if you land purely on the defensive track, this month makes you a dramatically sharper analyst — you'll finally see *why* your Month 3 detection rules matter, because you'll have caused the exact behavior they detect.

---

## Week 17 — Web App Security I: Injection and Authentication

### Week 17 Overview

**Theme**
Most real-world breaches still start with a basic web vulnerability. This week you build hands-on fluency in the two vulnerability classes that show up in almost every bug bounty report and pentest finding: SQL injection and authentication flaws.

**Week 17 Objectives**

```
✅ Understand and exploit SQL injection across multiple contexts
✅ Understand and exploit authentication logic flaws
✅ Learn Burp Suite's core workflow (Proxy, Repeater, Intruder)
✅ Build a personal SQLi/Auth vulnerability cheat sheet
```

**Success Criteria**

```
- Can you explain UNION-based, blind, and out-of-band SQLi differently from each other?
- Have you completed all PortSwigger SQL Injection labs through Practitioner level?
- Have you completed all PortSwigger Authentication labs through Practitioner level?
- Can you intercept and modify a request in Burp Repeater, unaided?
```

**Week 17 Resources**

Primary Platform
```
PortSwigger Web Security Academy (Free)
Learning Paths:
- SQL Injection
- Authentication
```

Secondary
```
TryHackMe: Burp Suite: The Basics
```

---

### DAY 113

**Goal**
SQL injection fundamentals — basic and error-based.

**Hour 1 — Core Concept**

PortSwigger Academy: **SQL Injection** — read the "What is SQL injection" and "SQL injection UNION attacks" theory sections in full before touching labs.

Topics:
```
How SQL queries are built dynamically from user input
The single-quote breakout test
Error-based vs blind SQLi at a high level
```

**Hour 2 — Lab**

PortSwigger: **SQL Injection** — Labs 1–3:
```
Lab: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data
Lab: SQL injection vulnerability allowing login bypass
Lab: SQL injection UNION attack, determining the number of columns returned
```

Solve each lab fully (not just to "solved," but understanding why your payload worked).

**Hour 3 — Documentation**

Create:
```
scripts_and_notes/sqli-cheatsheet.md
```

For each lab: document the vulnerability, the exact payload used, and why it worked.

Commit:
```
git add .
git commit -m "SQL Injection Labs 1-3 Completed"
git push
```

**Deliverable**
3 solved PortSwigger SQLi labs, documented with working payloads and explanations.

---

### DAY 114

**Goal**
UNION-based and blind SQL injection.

**Hour 1 — Core Concept**

PortSwigger Academy: read "Blind SQL injection" theory section.

Topics:
```
Boolean-based blind SQLi (true/false conditions inferred from page behavior)
Time-based blind SQLi (using SLEEP()/WAITFOR DELAY to infer data)
```

**Hour 2 — Lab**

PortSwigger: **SQL Injection** — Labs 4–7 (UNION-based data extraction and blind SQLi labs).

Solve each fully, extracting the actual flag/data required by the lab.

**Hour 3 — Documentation**

Add each lab's payload and technique to `sqli-cheatsheet.md`.

Commit:
```
git add .
git commit -m "SQL Injection Labs 4-7 Completed"
git push
```

**Deliverable**
7 total solved SQLi labs, cheat sheet growing with real, tested payloads.

---

### DAY 115

**Goal**
Advanced SQLi contexts — second-order and out-of-band.

**Hour 1 — Core Concept**

PortSwigger Academy: read "Second-order SQL injection" and "Out-of-band SQL injection" theory sections.

Topics:
```
Second-order SQLi: payload stored now, triggered later in a different query
Out-of-band SQLi: exfiltrating data via DNS/HTTP when no direct response is visible
```

**Hour 2 — Lab**

PortSwigger: **SQL Injection** — remaining labs (second-order + any out-of-band labs available at your access level).

Solve each fully.

**Hour 3 — Documentation**

Finalize the "SQL Injection" section of `sqli-cheatsheet.md` with all contexts covered.

Commit:
```
git add .
git commit -m "SQL Injection Learning Path Completed"
git push
```

**Deliverable**
The full PortSwigger SQL Injection learning path completed through Practitioner level.

---

### DAY 116

**Goal**
Authentication vulnerabilities — brute force and logic flaws.

**Hour 1 — Core Concept**

PortSwigger Academy: read "Authentication" theory section in full.

Topics:
```
Brute-forcing with account lockout bypass techniques
Logic flaws (e.g., trusting a hidden field, flawed 2FA logic)
```

**Hour 2 — Lab**

PortSwigger: **Authentication** — Labs 1–4.

Solve each, noting specifically which assumption the application made incorrectly.

**Hour 3 — Documentation**

Create:
```
scripts_and_notes/auth-vuln-cheatsheet.md
```

Document each lab's flaw and exploitation technique.

Commit:
```
git add .
git commit -m "Authentication Labs 1-4 Completed"
git push
```

**Deliverable**
4 solved authentication labs, documented with the exact logic flaw exploited in each.

---

### DAY 117

**Goal**
Password reset and MFA bypass flaws.

**Hour 1 — Core Concept**

PortSwigger Academy: read remaining "Authentication" theory on password reset poisoning and multi-factor bypass.

**Hour 2 — Lab**

PortSwigger: **Authentication** — Labs 5–8.

Solve each fully.

**Hour 3 — Documentation**

Finalize `auth-vuln-cheatsheet.md` with all 8 labs documented.

Commit:
```
git add .
git commit -m "Authentication Learning Path Completed"
git push
```

**Deliverable**
The full PortSwigger Authentication learning path completed through Practitioner level.

---

### DAY 118

**Goal**
Burp Suite fundamentals.

**Hour 1 — Core Concept**

THM: **Burp Suite: The Basics**

Topics:
```
Proxy: intercepting and modifying requests in-flight
Repeater: resending and manually tweaking a single request
Intruder: automating payload testing across a parameter
```

**Hour 2 — Lab**

Complete the room's hands-on tasks:
```
Configure your browser to proxy through Burp
Intercept a login request in Proxy
Send it to Repeater and manually alter a parameter
Run a basic Intruder attack against a login form using a small wordlist
```

Re-solve one of your Day 113-117 PortSwigger labs using Burp Repeater deliberately, even if you solved it a different way originally, to build the muscle memory.

**Hour 3 — Documentation**

Create:
```
scripts_and_notes/burp-suite-workflow-notes.md
```

Document your Proxy → Repeater → Intruder workflow with screenshots.

Commit:
```
git add .
git commit -m "Burp Suite Fundamentals Completed"
git push
```

**Deliverable**
Documented, hands-on Burp Suite workflow — the tool you'll use for every remaining week this month.

---

### DAY 119

**Goal**
Consolidate and review — Week 17 capstone.

**Hour 1 — Core Concept**

Re-read `sqli-cheatsheet.md` and `auth-vuln-cheatsheet.md` out loud, end to end.

**Hour 2 — Lab**

Self-test, live, without notes:
```
1. Given a new login form, attempt a basic SQLi login bypass unaided
2. Explain boolean-based vs time-based blind SQLi with your own example
3. Intercept and modify a request in Burp Proxy/Repeater unaided
```

Redo any failed item before Week 18.

**Hour 3 — Documentation**

Create:
```
week-17-summary.md
```

Structure:
```
SQLi and Auth labs completed (11 total)
Burp Suite workflow now comfortable
Ready for: XSS, CSRF, SSRF (Week 18)
```

Commit and push:
```
git add .
git commit -m "Week 17 Completed — SQLi and Authentication Mastered"
git push
```

**Deliverable**
`week-17-summary.md` plus two growing vulnerability cheat sheets.

---

## Week 18 — Web App Security II: XSS, CSRF, SSRF

### Week 18 Overview

**Theme**
Client-side and server-side request vulnerabilities round out your core web vulnerability toolkit. By the end of this week, you'll have hands-on experience with the vulnerability classes that appear in the vast majority of real bug bounty payouts.

**Week 18 Objectives**

```
✅ Exploit reflected, stored, and DOM-based XSS
✅ Understand CSRF mechanics and defenses
✅ Understand SSRF mechanics, including cloud metadata risk
✅ Begin the THM Junior Penetration Tester learning path
✅ Master Nmap for real-world enumeration
```

**Success Criteria**

```
- Can you distinguish reflected, stored, and DOM XSS by where the payload executes?
- Have you completed the PortSwigger CSRF and SSRF labs?
- Can you run a full Nmap scan with service/version detection and explain every flag used?
```

**Week 18 Resources**

Primary Platform
```
PortSwigger Web Security Academy (Free)
Learning Paths:
- Cross-site scripting (XSS)
- CSRF
- SSRF
```

Secondary
```
TryHackMe: Junior Penetration Tester path (intro modules)
TryHackMe: Nmap
```

---

### DAY 120

**Goal**
Reflected, stored, and DOM XSS fundamentals.

**Hour 1 — Core Concept**

PortSwigger Academy: read "Cross-site scripting" theory section in full.

Topics:
```
Reflected XSS: payload in the request, reflected immediately in the response
Stored XSS: payload saved server-side, executes for other users later
DOM XSS: vulnerability exists entirely in client-side JavaScript
```

**Hour 2 — Lab**

PortSwigger: **XSS** — Labs 1–4.

Solve each fully with a working `<script>` or event-handler payload.

**Hour 3 — Documentation**

Create:
```
scripts_and_notes/xss-cheatsheet.md
```

Document each lab's type (reflected/stored/DOM), payload, and injection context.

Commit:
```
git add .
git commit -m "XSS Labs 1-4 Completed"
git push
```

**Deliverable**
4 solved XSS labs spanning all three types, documented.

---

### DAY 121

**Goal**
XSS filter bypass and Content Security Policy basics.

**Hour 1 — Core Concept**

PortSwigger Academy: read remaining XSS theory on filter evasion and CSP.

Topics:
```
Common filter bypass techniques (case variation, event handlers, encoding)
What CSP restricts and why it makes some payloads fail
```

**Hour 2 — Lab**

PortSwigger: **XSS** — Labs 5–8 (filter bypass and CSP-related labs).

Solve each fully.

**Hour 3 — Documentation**

Finalize `xss-cheatsheet.md` with filter-bypass techniques documented alongside working payloads.

Commit:
```
git add .
git commit -m "XSS Learning Path Completed"
git push
```

**Deliverable**
The full PortSwigger XSS learning path completed through Practitioner level.

---

### DAY 122

**Goal**
CSRF mechanics and defenses.

**Hour 1 — Core Concept**

PortSwigger Academy: read "CSRF" theory section in full.

Topics:
```
Why CSRF relies on the victim's authenticated session
CSRF tokens as the primary defense
SameSite cookie attribute as a modern mitigation
```

**Hour 2 — Lab**

PortSwigger: **CSRF** — all available labs at your access level.

Solve each fully, building the malicious auto-submitting HTML form required for each lab.

**Hour 3 — Documentation**

Create:
```
scripts_and_notes/csrf-ssrf-cheatsheet.md
```

Document each CSRF lab's exploit HTML and why the target app's defense was missing/flawed.

Commit:
```
git add .
git commit -m "CSRF Learning Path Completed"
git push
```

**Deliverable**
Full PortSwigger CSRF learning path completed, with working exploit HTML documented.

---

### DAY 123

**Goal**
SSRF mechanics and cloud metadata risk.

**Hour 1 — Core Concept**

PortSwigger Academy: read "SSRF" theory section in full.

Topics:
```
Basic SSRF: server fetches a URL you control the destination of
SSRF against cloud metadata endpoints (e.g., 169.254.169.254) and why this is critical-severity
Bypassing basic blacklist-based SSRF filters
```

**Hour 2 — Lab**

PortSwigger: **SSRF** — all available labs at your access level.

Solve each fully.

**Hour 3 — Documentation**

Add SSRF section to `csrf-ssrf-cheatsheet.md` documenting each lab's payload and the underlying trust flaw exploited.

Commit:
```
git add .
git commit -m "SSRF Learning Path Completed"
git push
```

**Deliverable**
Full PortSwigger SSRF learning path completed, with cloud-metadata risk explained in your own words.

---

### DAY 124

**Goal**
Begin the THM Junior Penetration Tester path.

**Hour 1 — Core Concept**

THM: **Junior Penetration Tester** path — introductory modules.

Topics:
```
Pentest engagement types (black/grey/white box)
Rules of engagement and scope
The standard pentest methodology overview
```

**Hour 2 — Lab**

Complete the intro modules' hands-on tasks as provided.

**Hour 3 — Documentation**

Create:
```
pentest-methodology-notes.md
```

Document the pentest methodology stages in your own words, plus what "scope" and "rules of engagement" mean practically.

Commit:
```
git add .
git commit -m "Junior Pentester Path - Methodology Intro Completed"
git push
```

**Deliverable**
`pentest-methodology-notes.md` — the mental framework for everything in Weeks 19–20.

---

### DAY 125

**Goal**
Master Nmap for real enumeration.

**Hour 1 — Core Concept**

THM: **Nmap**

Topics:
```
TCP connect scan vs SYN scan (-sT vs -sS)
Service/version detection (-sV)
Default script scanning (-sC)
Timing templates (-T4) and output formats (-oA)
```

**Hour 2 — Lab**

Complete the room's tasks, and additionally run a full scan against a target it provides:
```
nmap -sC -sV -oA scan_results <target-ip>
nmap -p- <target-ip>
nmap --script vuln <target-ip>
```

**Hour 3 — Documentation**

Create:
```
scripts_and_notes/nmap-cheatsheet.md
```

Document each flag used and what it changes about the scan.

Commit:
```
git add .
git commit -m "Nmap Enumeration Mastered"
git push
```

**Deliverable**
A working, well-understood Nmap command reference — the very first step of every HTB machine starting next week.

---

### DAY 126

**Goal**
Consolidate and review — Week 18 capstone.

**Hour 1 — Core Concept**

Re-read `xss-cheatsheet.md` and `csrf-ssrf-cheatsheet.md` out loud, end to end.

**Hour 2 — Lab**

Self-test, live, without notes:
```
1. Given a new input field, write a working XSS payload unaided
2. Explain why a CSRF token defeats a CSRF attack, in one sentence
3. Explain why SSRF against 169.254.169.254 is dangerous specifically in cloud environments
4. Run a full Nmap scan (-sC -sV) against a target unaided
```

Redo any failed item before Week 19.

**Hour 3 — Documentation**

Create:
```
week-18-summary.md
```

Structure:
```
XSS/CSRF/SSRF labs completed
Nmap enumeration mastered
Ready for: HackTheBox machines (Week 19)
```

Commit and push:
```
git add .
git commit -m "Week 18 Completed — Web Vulnerability Classes Mastered"
git push
```

**Deliverable**
`week-18-summary.md` — your web vulnerability foundation is now genuinely broad and hands-on.

---

## Week 19 — HackTheBox: Enumeration and Easy Machines

### Week 19 Overview

**Theme**
Labs with guided steps are training wheels. This week you apply everything to real, unguided HackTheBox machines — starting with the guided Starting Point tier to build confidence, then moving toward independent Tier 1 machines.

**Week 19 Objectives**

```
✅ Apply full enumeration methodology to real HTB targets
✅ Practice Linux and Windows privilege escalation basics
✅ Use gobuster/ffuf for web directory enumeration
✅ Use Metasploit for at least one guided exploitation
✅ Complete HTB Starting Point Tier 0 and Tier 1
```

**Success Criteria**

```
- Have you captured user and root/system flags on at least 6 HTB Starting Point machines?
- Can you explain your enumeration methodology out loud, start to finish, for any one machine?
- Can you identify at least one privilege escalation vector on a Linux box and one on a Windows box, unaided?
```

**Week 19 Resources**

Primary Platform
```
HackTheBox — Starting Point (Free tier)
Tier 0: Meow, Fawn, Dancing, Redeemer, Explosion, Preignition, Mongod, Synced (pick at least 6)
Tier 1: Vaccine, Archetype, Oopsie, (pick at least 2)
```

---

### DAY 127

**Goal**
Full enumeration methodology + first 2 HTB machines.

**Hour 1 — Core Concept**

Reading/video: the standard enumeration methodology — recon → port scan → service enumeration → identify version-specific vulnerabilities → exploit → escalate.

**Hour 2 — Lab**

HTB Starting Point Tier 0: **"Meow"** and **"Fawn"**

For each:
```
nmap -sC -sV -oA <machine>_scan <target-ip>
Enumerate the identified service(s) manually
Exploit and capture the flag
```

**Hour 3 — Documentation**

Create:
```
htb-writeups/meow.md
htb-writeups/fawn.md
```

For each, document: Recon → Enumeration → Exploitation → Flag, with exact commands used.

Commit:
```
git add .
git commit -m "HTB Meow and Fawn Completed"
git push
```

**Deliverable**
2 fully documented HTB machine write-ups.

---

### DAY 128

**Goal**
Service enumeration deep dive + 2 more HTB machines.

**Hour 1 — Core Concept**

Reading/video: enumerating SMB (`smbclient`, `enum4linux`), FTP (anonymous login checks), and basic HTTP enumeration.

**Hour 2 — Lab**

HTB Starting Point Tier 0: **"Dancing"** and **"Redeemer"**

For each, apply the relevant service enumeration technique before exploiting:
```
smbclient -L //<target-ip>/ -N          (for SMB-based machines)
```

**Hour 3 — Documentation**

Create write-ups:
```
htb-writeups/dancing.md
htb-writeups/redeemer.md
```

Commit:
```
git add .
git commit -m "HTB Dancing and Redeemer Completed"
git push
```

**Deliverable**
2 more fully documented HTB write-ups (4 total this week so far).

---

### DAY 129

**Goal**
Linux privilege escalation basics + 2 more HTB machines.

**Hour 1 — Core Concept**

Reading/video: common Linux privesc vectors — SUID binaries, sudo misconfigurations, cron jobs, kernel exploits (at a conceptual level).

**Hour 2 — Lab**

HTB Starting Point Tier 0: **"Explosion"** and **"Preignition"**

For any Linux target, practice enumeration commands:
```
sudo -l
find / -perm -4000 -type f 2>/dev/null
```

**Hour 3 — Documentation**

Create write-ups:
```
htb-writeups/explosion.md
htb-writeups/preignition.md
```

Include a "Privilege Escalation" section explaining the specific vector found (or noting the machine didn't require privesc, if applicable).

Commit:
```
git add .
git commit -m "HTB Explosion and Preignition Completed"
git push
```

**Deliverable**
2 more documented write-ups (6 total this week) — Tier 0 fully complete.

---

### DAY 130

**Goal**
Windows privilege escalation basics + Tier 1 machine.

**Hour 1 — Core Concept**

Reading/video: common Windows privesc vectors — unquoted service paths, weak service permissions, stored credentials, `winPEAS` overview.

**Hour 2 — Lab**

HTB Starting Point Tier 1: **"Archetype"**

Apply full methodology:
```
nmap -sC -sV -oA archetype_scan <target-ip>
Enumerate SQL Server / SMB as applicable
Escalate privileges using the identified vector
```

**Hour 3 — Documentation**

Create:
```
htb-writeups/archetype.md
```

Document the full chain including the specific Windows privesc technique used.

Commit:
```
git add .
git commit -m "HTB Archetype Completed"
git push
```

**Deliverable**
First Tier 1 machine documented — a meaningfully harder, less-guided challenge than Tier 0.

---

### DAY 131

**Goal**
Web enumeration tools + second Tier 1 machine.

**Hour 1 — Core Concept**

Reading/video: `gobuster`/`ffuf` for directory/file brute-forcing, and `whatweb` for technology fingerprinting.

**Hour 2 — Lab**

HTB Starting Point Tier 1: **"Vaccine"** (or another available Tier 1 web-focused box)

```
whatweb http://<target-ip>
gobuster dir -u http://<target-ip> -w /usr/share/wordlists/dirb/common.txt
```

Use findings to identify and exploit the vulnerability, escalating privileges as needed.

**Hour 3 — Documentation**

Create:
```
htb-writeups/vaccine.md
```

Commit:
```
git add .
git commit -m "HTB Vaccine Completed"
git push
```

**Deliverable**
A second Tier 1 write-up — 8 total HTB machines documented this week.

---

### DAY 132

**Goal**
Metasploit basics — guided exploitation.

**Hour 1 — Core Concept**

Reading/video: Metasploit Framework core workflow — `search`, `use`, `show options`, `set`, `exploit`.

**Hour 2 — Lab**

Revisit one earlier machine (or a new simple one) and deliberately solve it using Metasploit instead of a manual exploit, to build familiarity with the framework:
```
msfconsole
search <relevant-service-or-CVE>
use <module>
show options
set RHOSTS <target-ip>
set LHOST <your-ip>
exploit
```

**Hour 3 — Documentation**

Add a "Metasploit Workflow" section to `pentest-methodology-notes.md` documenting the exact command sequence and what each step configures.

Commit:
```
git add .
git commit -m "Metasploit Basics Practiced"
git push
```

**Deliverable**
Documented, hands-on Metasploit workflow — a tool every junior pentester is expected to know at a basic level.

---

### DAY 133

**Goal**
Consolidate and review — Week 19 capstone.

**Hour 1 — Core Concept**

Re-read all 8 HTB write-ups out loud, end to end, explaining your methodology for each from memory.

**Hour 2 — Lab**

Self-test, live, without notes:
```
1. Pick a 9th unattempted Starting Point machine and solve it fully, timing yourself
2. Explain your enumeration methodology out loud, start to finish, without looking at notes
3. Name 3 Linux and 3 Windows privilege escalation vectors from memory
```

**Hour 3 — Documentation**

Create:
```
week-19-summary.md
```

Structure:
```
HTB machines completed (9 total, linked)
Methodology now internalized
Ready for: formal pentest report writing (Week 20)
```

Commit and push:
```
git add .
git commit -m "Week 19 Completed — HTB Enumeration and Exploitation Skills Built"
git push
```

**Deliverable**
9 fully documented HTB machine write-ups — a genuinely strong offensive portfolio foundation.

---

## Week 20 — Formal Pentest Report (Crown Jewel Week)

### Week 20 Overview

**Theme**
Solving machines proves skill. Writing a report that a client or hiring manager can actually use proves professionalism. This week you package everything into your Month 5 Crown Jewel — a formal penetration test report plus your 5 best HTB write-ups.

**Week 20 Objectives**

```
✅ Deploy and test a deliberately vulnerable web app (Juice Shop or DVWA)
✅ Identify and document 3-4 real vulnerabilities in it
✅ Write a formal pentest report (Exec Summary, Findings, CVSS, Remediation)
✅ Finalize and polish 5 HTB write-ups
✅ Publish the Month 5 Crown Jewel repository
```

**Success Criteria**

```
- Does your pentest report follow a real industry-standard structure?
- Does every finding have a CVSS-style severity rating with justification?
- Are your 5 HTB write-ups polished enough that a stranger could follow your methodology exactly?
```

**Week 20 Resources**

Tools
```
OWASP Juice Shop (Docker) or DVWA (Docker)
Burp Suite
```

---

### DAY 134

**Goal**
Deploy the target application and begin testing.

**Hour 1 — Core Concept**

Reading/video: CVSS scoring basics — Attack Vector, Attack Complexity, Privileges Required, Impact — enough to justify a severity rating, not full formal certification-level mastery.

**Hour 2 — Lab**

Deploy the target:
```
docker run -d -p 3000:3000 bkimminich/juice-shop
```

Begin testing, using Burp Suite as your proxy:
```
Identify and confirm 1 SQL injection vulnerability
Identify and confirm 1 XSS vulnerability
```

**Hour 3 — Documentation**

Create:
```
month-05-crown-jewel/pentest-working-notes.md
```

Document both findings with screenshots and exact reproduction steps.

Commit:
```
git add .
git commit -m "Pentest Target Deployed - First 2 Findings Confirmed"
git push
```

**Deliverable**
Target deployed, first 2 vulnerabilities confirmed and documented.

---

### DAY 135

**Goal**
Identify remaining findings.

**Hour 1 — Core Concept**

Reading/video: broken authentication and IDOR (Insecure Direct Object Reference) patterns — quick refresher before hunting for them.

**Hour 2 — Lab**

Continue testing:
```
Identify and confirm 1 broken authentication issue (e.g., weak password policy, predictable reset tokens)
Identify and confirm 1 IDOR (e.g., accessing another user's data by changing an ID in a request)
```

**Hour 3 — Documentation**

Add both findings to `pentest-working-notes.md` with screenshots and reproduction steps.

Commit:
```
git add .
git commit -m "Pentest - All 4 Findings Confirmed"
git push
```

**Deliverable**
4 confirmed, documented vulnerabilities — enough for a credible formal report.

---

### DAY 136

**Goal**
Draft the Findings section with CVSS-style ratings.

**Hour 1 — Core Concept**

Reading/video: writing a finding that includes Title, Severity, Description, Reproduction Steps, Impact, and Remediation — the standard structure used industry-wide.

**Hour 2 — Lab**

For each of your 4 findings, draft the full structured write-up:
```
## Finding 1: SQL Injection in [parameter]
Severity: High (CVSS-style justification: unauthenticated, high impact on confidentiality)
Description:
Reproduction Steps:
Impact:
Remediation:
```

Repeat for all 4 findings.

**Hour 3 — Documentation**

Save as:
```
month-05-crown-jewel/pentest-report-DRAFT.md
```

Commit:
```
git add .
git commit -m "Pentest Report - Findings Section Drafted"
git push
```

**Deliverable**
4 fully structured findings, each with severity justification and remediation advice.

---

### DAY 137

**Goal**
Draft the Executive Summary and finalize the report.

**Hour 1 — Core Concept**

Reading/video: writing an Executive Summary for a pentest report — overall risk posture in plain language, without technical jargon.

**Hour 2 — Lab**

Draft:
```
## Executive Summary
(Overview of the engagement, overall risk level, number of findings by severity)

## Scope
(What was tested, what wasn't)

## Methodology
(Brief description of your approach)
```

Assemble the complete report: Executive Summary → Scope → Methodology → Findings (all 4) → Overall Remediation Priorities.

**Hour 3 — Documentation**

Finalize:
```
month-05-crown-jewel/pentest-report-FINAL.md
```

Commit:
```
git add .
git commit -m "Formal Pentest Report Finalized"
git push
```

**Deliverable**
A complete, professional-grade formal penetration test report.

---

### DAY 138

**Goal**
Select and polish 5 HTB write-ups.

**Hour 1 — Core Concept**

Reading/video: none — review a couple of real public HTB write-up examples (structure only, not content) to calibrate what "polished" looks like.

**Hour 2 — Lab**

Select your 5 strongest write-ups from Week 19 (mix of Tier 0 and Tier 1 recommended, e.g., Meow, Dancing, Explosion, Archetype, Vaccine). For each:
```
Ensure every command is exact and reproducible
Add a screenshot of the flag capture
Add a "Lessons Learned" one-liner
```

**Hour 3 — Documentation**

Move the 5 selected write-ups into:
```
month-05-crown-jewel/htb-writeups/
```

Commit:
```
git add .
git commit -m "5 HTB Write-ups Selected and Polished"
git push
```

**Deliverable**
5 polished, portfolio-ready HTB machine write-ups.

---

### DAY 139

**Goal**
Cross-link and build the portfolio narrative.

**Hour 1 — Core Concept**

Reading/video: none — reflect on how your offensive work (this month) connects back to your defensive work (Months 2-4) — this narrative is genuinely valuable in interviews.

**Hour 2 — Lab**

Write a short "Defense Through Offense" reflection: pick 2 of your Month 3 Wazuh detection rules and explain specifically how this month's offensive work deepened your understanding of why those rules matter.

**Hour 3 — Documentation**

Create:
```
month-05-crown-jewel/defense-through-offense-reflection.md
```

Commit:
```
git add .
git commit -m "Cross-Portfolio Reflection Written"
git push
```

**Deliverable**
A written reflection tying your offensive and defensive portfolios together — a strong, differentiated interview talking point.

---

### DAY 140

**Goal**
Assemble and publish the Month 5 Crown Jewel — Crown Jewel Day.

**Hour 1 — Core Concept**

Re-read your entire Month 5 journey (Weeks 17–20) out loud, end to end.

**Hour 2 — Lab**

Assemble the final repository structure:
```
junior-pentest-portfolio/
├── README.md
├── pentest-report-FINAL.md
├── defense-through-offense-reflection.md
└── htb-writeups/
    ├── meow.md
    ├── dancing.md
    ├── explosion.md
    ├── archetype.md
    └── vaccine.md
```

Run a final live self-test:
```
1. Explain your formal pentest report's Executive Summary from memory
2. Pick any HTB write-up and walk through your methodology from memory
3. Explain, out loud, how this month changed your understanding of detection engineering
```

**Hour 3 — Documentation**

Write the master `README.md`:
```
# Junior Penetration Tester Portfolio

## What this repo demonstrates
- A formal penetration test report against OWASP Juice Shop (4 findings, CVSS-style severity, full remediation guidance)
- 5 polished HackTheBox machine write-ups spanning Linux and Windows targets
- A cross-portfolio reflection connecting offensive testing to defensive detection engineering

## Structure
(explain folders)

## Skills demonstrated
(web application vulnerability assessment, enumeration methodology, privilege escalation, professional pentest reporting, Burp Suite, Nmap, Metasploit)
```

Final commit and push:
```
git add .
git commit -m "Month 5 Completed — Crown Jewel Published"
git push
```

**Deliverable**
A fully published `junior-pentest-portfolio` repository — **Month 5 is complete**, and your stretch-goal offensive portfolio now stands alongside your defensive work.

---

*End of Chapter 5. Chapter 6 (Month 6 — Job Readiness, Certification, and the Final Application Push) continues in the same format.*
