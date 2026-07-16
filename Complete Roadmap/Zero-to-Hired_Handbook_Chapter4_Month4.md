# Zero-to-Hired Cybersecurity Roadmap (Version 2026)
### A Complete 6-Month Handbook

---

# Chapter 4 — Month 4: Incident Response, Threat Intelligence, and Investigation

Theme of the month: **You stop being someone who finds an alert and become someone who owns the case until it's closed.**
This month you learn the full incident lifecycle, analyze real phishing and malware artifacts safely, correlate threat intelligence, and run a complete simulated investigation from first alert to final report.

---

## Week 13 — Incident Response Methodology

### Week 13 Overview

**Theme**
Before you can investigate anything, you need the structure that keeps an investigation from becoming chaos. This week is NIST 800-61 internalized until it's instinct, not a slide you memorized.

**Week 13 Objectives**

```
✅ Understand the full NIST 800-61 IR lifecycle
✅ Understand containment strategy tradeoffs
✅ Understand evidence handling and chain of custody basics
✅ Build a reusable IR timeline template
✅ Practice log-based investigation on real Windows Event Logs
```

**Success Criteria**

```
- Can you name and explain all 6 phases of the NIST 800-61 lifecycle, unaided?
- Can you explain the tradeoff between short-term and long-term containment?
- Can you explain, in one sentence, why chain of custody matters even in a home lab exercise?
```

**Week 13 Resources**

Primary Platform
```
TryHackMe (Free)
Rooms:
- Incident Response Fundamentals (or equivalent)
- Incident Handling Process
- Windows Event Logs
```

Documentation
```
- NIST Special Publication 800-61 Rev. 2 (Computer Security Incident Handling Guide)
```

---

### DAY 85

**Goal**
Learn the NIST 800-61 IR lifecycle.

**Hour 1 — Core Concept**

THM: **Incident Response Fundamentals** (or equivalent room)

Topics:
```
Preparation
Detection & Analysis
Containment, Eradication & Recovery
Post-Incident Activity (Lessons Learned)
```

**Hour 2 — Lab**

For each phase, write a concrete example from your own Month 2/3 lab work of what that phase would look like in practice:
```
Preparation: (e.g., your GPO audit policy and Sysmon deployment ARE preparation)
Detection & Analysis: (e.g., your Wazuh custom rules firing)
Containment: (what would you actually do if rule 100011 fired for real - isolate the host? disable the account?)
Post-Incident: (what would you update in your rules/config afterward?)
```

**Hour 3 — Documentation**

Create:
```
ir-fundamentals-notes.md
```

Document all 6 phases with your own lab-grounded examples for each.

Commit:
```
git add .
git commit -m "NIST 800-61 IR Lifecycle Understood"
git push
```

**Deliverable**
`ir-fundamentals-notes.md` grounding IR theory directly in your own lab's real capabilities.

---

### DAY 86

**Goal**
Containment strategy deep dive.

**Hour 1 — Core Concept**

THM: **Incident Handling Process**

Topics:
```
Short-term containment (isolate now, minimal disruption)
Long-term containment (rebuild/patch, more disruption, more thorough)
Decision factors: business impact vs security risk
```

**Hour 2 — Lab**

Work through 3 scenario decisions and write your reasoning for each:
```
Scenario 1: A single workstation shows ransomware encryption starting. Short-term or long-term first? Why?
Scenario 2: A domain admin account is confirmed compromised. What's your first containment action?
Scenario 3: A web server is being used for outbound C2 but is business-critical and can't go offline. What do you do?
```

**Hour 3 — Documentation**

Add "Containment Decision Framework" section to `ir-fundamentals-notes.md` with your 3 scenario answers.

Commit:
```
git add .
git commit -m "Containment Strategy Framework Documented"
git push
```

**Deliverable**
A documented decision framework for real containment tradeoffs — a common interview scenario question.

---

### DAY 87

**Goal**
Chain of custody and evidence handling basics.

**Hour 1 — Core Concept**

Continue THM: **Incident Handling Process**, or supplement with **Intro to Digital Forensics**.

Topics:
```
Why evidence integrity matters (hashing evidence files, e.g., SHA-256)
Documenting who accessed what evidence, when
Order of volatility (RAM before disk, disk before logs, etc.)
```

**Hour 2 — Lab**

Practice hashing a piece of "evidence" to demonstrate integrity verification:
```
sha256sum sample_evidence_file.txt
```

Make a copy, hash it again, confirm the hashes match. Then modify one byte of the copy and re-hash it to see the hash change completely.

Write out the "order of volatility" from most to least volatile, in your own words, with a one-line reason for each item's position.

**Hour 3 — Documentation**

Add "Evidence Handling" section to `ir-fundamentals-notes.md` with your hash verification demo and order-of-volatility list.

Commit:
```
git add .
git commit -m "Chain of Custody and Evidence Handling Completed"
git push
```

**Deliverable**
A concrete, hands-on demonstration of why hashing matters for evidence integrity.

---

### DAY 88

**Goal**
Log-based investigation practice on Windows Event Logs.

**Hour 1 — Core Concept**

THM: **Windows Event Logs**

Topics:
```
Reading unfamiliar Event IDs efficiently (using Microsoft's Event ID reference)
Building a timeline from raw event data
```

**Hour 2 — Lab**

Complete the THM room's investigative tasks. Where the room provides a scenario log file or challenge, work through it methodically:
```
Identify the earliest suspicious event
Identify the attacker's apparent goal based on the sequence of events
Note every Event ID used as evidence, in order
```

**Hour 3 — Documentation**

Create:
```
event-log-investigation-practice.md
```

Document the scenario, your timeline, and your conclusion.

Commit:
```
git add .
git commit -m "Windows Event Log Investigation Practice Completed"
git push
```

**Deliverable**
A practiced, real investigative walkthrough using unfamiliar log data — direct rehearsal for Week 16's capstone.

---

### DAY 89

**Goal**
Build a reusable IR timeline template.

**Hour 1 — Core Concept**

Reading/video: what makes an IR timeline useful to someone who wasn't present during the investigation — clarity, chronological order, and explicit evidence linkage.

**Hour 2 — Lab**

Design a timeline template you will reuse for the rest of the program:
```
| Timestamp | Event | Source (log/tool) | Evidence Reference | Analyst Notes |
```

Fill it in retroactively using your Day 88 investigation as a test case, to confirm the template actually works in practice.

**Hour 3 — Documentation**

Create:
```
templates/ir-timeline-template.md
```

Save the blank template plus your filled Day 88 example as a reference.

Commit:
```
git add .
git commit -m "Reusable IR Timeline Template Built"
git push
```

**Deliverable**
`ir-timeline-template.md` — a tool you will use again in Week 16 and beyond.

---

### DAY 90

**Goal**
Build a reusable IR report template.

**Hour 1 — Core Concept**

Reading/video: standard IR report sections used across the industry (Executive Summary, Timeline, Technical Findings, IOCs, MITRE Mapping, Remediation, Lessons Learned).

**Hour 2 — Lab**

Draft the skeleton structure:
```
# Incident Report: [Title]

## Executive Summary
(2-3 sentences, non-technical, for leadership)

## Timeline
(uses the ir-timeline-template)

## Technical Findings
(detailed, technical, evidence-linked)

## Indicators of Compromise (IOCs)
(IPs, hashes, domains, usernames)

## MITRE ATT&CK Mapping
(techniques observed)

## Remediation Recommendations

## Lessons Learned
```

**Hour 3 — Documentation**

Create:
```
templates/ir-report-template.md
```

Commit:
```
git add .
git commit -m "Reusable IR Report Template Built"
git push
```

**Deliverable**
A complete, reusable IR report skeleton — this exact template gets filled in for real in Week 16.

---

### DAY 91

**Goal**
Consolidate and review — Week 13 capstone.

**Hour 1 — Core Concept**

Re-read all Week 13 notes out loud, end to end.

**Hour 2 — Lab**

Self-test, live, without notes:
```
1. Name all 6 phases of NIST 800-61, in order, unaided
2. Explain short-term vs long-term containment with your own example
3. Explain why you'd hash a piece of evidence before analyzing it
4. Walk through your IR timeline template and explain each column
```

Redo any failed item before Week 14.

**Hour 3 — Documentation**

Create:
```
week-13-summary.md
```

Structure:
```
IR lifecycle mastered
Templates built (timeline + report, both linked)
Ready for: phishing and malware analysis (Week 14)
```

Commit and push:
```
git add .
git commit -m "Week 13 Completed — IR Methodology Internalized"
git push
```

**Deliverable**
Two reusable, professional-grade templates — the operational backbone of everything left in Month 4.

---

## Week 14 — Phishing Analysis and Malware Triage

### Week 14 Overview

**Theme**
Phishing is still the #1 initial access vector in real breaches, and a Tier 1 analyst's single most common ticket type. This week you learn to read an email like a forensic document and safely observe malware behavior without ever risking your own systems.

**Week 14 Objectives**

```
✅ Analyze email headers for spoofing/routing anomalies
✅ Identify phishing red flags systematically, not by gut feeling
✅ Understand static vs dynamic malware analysis
✅ Safely use an online sandbox for behavioral analysis
✅ Extract and document IOCs properly
```

**Success Criteria**

```
- Can you identify a spoofed sender using SPF/DKIM/DMARC results in a header, unaided?
- Can you list at least 6 concrete phishing red flags without repeating the same idea twice?
- Can you explain the difference between static and dynamic malware analysis in one sentence each?
```

**Week 14 Resources**

Primary Platform
```
TryHackMe (Free)
Rooms:
- Phishing Analysis Fundamentals
- Phishing Emails (series)
- Dissecting PE Headers (or equivalent MAL: introductory room)
```

Tools
```
any.run or Hybrid-Analysis (free tier, for sandbox reports only — never submit real/unknown files from outside a lab)
```

---

### DAY 92

**Goal**
Email header anatomy.

**Hour 1 — Core Concept**

THM: **Phishing Analysis Fundamentals**

Topics:
```
Received: header chain (reading bottom-to-top)
SPF, DKIM, DMARC — what each actually verifies
Return-Path vs From header mismatches
```

**Hour 2 — Lab**

Obtain a sample phishing email header from the THM room's provided materials. Work through it manually:
```
Trace the Received chain, bottom to top
Identify the SPF/DKIM/DMARC pass/fail results
Identify any mismatch between the "From" display name and the actual sending domain
```

**Hour 3 — Documentation**

Create:
```
phishing-analysis-notes.md
```

Document your header walkthrough with the specific lines that proved spoofing (or legitimacy).

Commit:
```
git add .
git commit -m "Email Header Analysis Completed"
git push
```

**Deliverable**
A fully annotated email header walkthrough proving or disproving spoofing.

---

### DAY 93

**Goal**
Phishing red flags — systematic identification.

**Hour 1 — Core Concept**

THM: **Phishing Emails 1**

Topics:
```
Urgency/fear-based language
Mismatched/lookalike domains (typosquatting)
Suspicious attachments and links
Generic greetings, poor grammar (less reliable now with AI-written phishing, note this caveat)
```

**Hour 2 — Lab**

Complete the room's tasks, identifying red flags in each provided sample. Build a personal checklist as you go — don't just answer the room's questions, extract the checklist itself.

**Hour 3 — Documentation**

Add "Phishing Red Flag Checklist" section to `phishing-analysis-notes.md` — a reusable list of 8+ items you'll apply to every future analysis.

Commit:
```
git add .
git commit -m "Phishing Red Flag Checklist Built"
git push
```

**Deliverable**
A reusable phishing red-flag checklist, grounded in real examples you personally analyzed.

---

### DAY 94

**Goal**
Continued phishing analysis practice.

**Hour 1 — Core Concept**

THM: **Phishing Emails 2** (or equivalent continuation room).

Topics:
```
URL analysis (hovering vs actual href, URL shorteners, redirect chains)
Attachment risk assessment without opening the file
```

**Hour 2 — Lab**

Complete the room's tasks. For any URLs provided, practice identifying the real destination vs the displayed text without visiting the link directly (use the room's safe analysis tools/environment only).

**Hour 3 — Documentation**

Add "URL and Attachment Analysis" section to `phishing-analysis-notes.md` with your findings from this room.

Commit:
```
git add .
git commit -m "Phishing URL and Attachment Analysis Completed"
git push
```

**Deliverable**
Documented URL/attachment analysis technique added to your growing analyst notes.

---

### DAY 95

**Goal**
Static vs dynamic malware analysis concepts.

**Hour 1 — Core Concept**

THM: **Dissecting PE Headers** (or an equivalent introductory malware analysis room).

Topics:
```
Static analysis: examining a file without running it (hashes, strings, PE header structure)
Dynamic analysis: observing behavior in a sandbox (network calls, file writes, registry changes)
Why analysts do static first, then dynamic
```

**Hour 2 — Lab**

Complete the room's PE header inspection tasks. If tools like `strings` or a PE viewer are available in the room's environment, practice extracting readable strings from a sample file and noting anything suspicious (URLs, IPs, suspicious API names).

**Hour 3 — Documentation**

Create:
```
malware-triage-notes.md
```

Document static vs dynamic analysis in your own words, plus your PE header findings from this room.

Commit:
```
git add .
git commit -m "Static Malware Analysis Concepts Completed"
git push
```

**Deliverable**
`malware-triage-notes.md` with a clear static-vs-dynamic distinction and hands-on PE header findings.

---

### DAY 96

**Goal**
Safe sandbox analysis practice.

**Hour 1 — Core Concept**

Reading/video: how online sandboxes (any.run, Hybrid Analysis) work, and the critical safety rule — only ever submit known-safe test files or files provided within a controlled lab room; never submit real unknown files from the open internet.

**Hour 2 — Lab**

Submit the EICAR test file (a universally recognized, harmless antivirus test string, not real malware) to any.run or Hybrid Analysis:
```
Create a text file containing the standard EICAR test string
Submit it to the sandbox
```

Read the resulting report structure carefully: process tree, network activity (should be none for EICAR), detection verdicts from various engines.

**Hour 3 — Documentation**

Add "Sandbox Report Structure" section to `malware-triage-notes.md` explaining each section of the report you reviewed, using the EICAR report as your concrete example.

Commit:
```
git add .
git commit -m "Sandbox Analysis Practice Completed"
git push
```

**Deliverable**
A documented understanding of sandbox report structure, safely demonstrated with a harmless test file.

---

### DAY 97

**Goal**
IOC extraction and documentation.

**Hour 1 — Core Concept**

Reading/video: IOC types (file hashes, IPs, domains, registry keys, mutexes) and why analysts document them in a structured, shareable format.

**Hour 2 — Lab**

Using a THM room's provided sample report or your own EICAR sandbox result, extract every possible IOC and organize it:
```
IOC Type | Value | Source | Confidence
File Hash (SHA256) | ... | Sandbox report | High
```

**Hour 3 — Documentation**

Create:
```
templates/ioc-extraction-template.md
```

Save this as a reusable template, filled with your Day 96/97 example as a reference.

Commit:
```
git add .
git commit -m "IOC Extraction Template Built"
git push
```

**Deliverable**
A reusable IOC extraction template — another tool you carry forward into Week 16's capstone incident.

---

### DAY 98

**Goal**
Consolidate and review — Week 14 capstone.

**Hour 1 — Core Concept**

Re-read all Week 14 notes out loud, end to end.

**Hour 2 — Lab**

Self-test, live, without notes:
```
1. Given a new sample email header, trace the Received chain and check SPF/DKIM/DMARC unaided
2. List 8 phishing red flags from memory
3. Explain static vs dynamic malware analysis out loud
4. Fill out the IOC extraction template for a new sample
```

Redo any failed item before Week 15.

**Hour 3 — Documentation**

Create:
```
week-14-summary.md
```

Structure:
```
Phishing analysis skills mastered
Malware triage concepts mastered
Templates built this week (linked)
Ready for: threat intel and traffic analysis (Week 15)
```

Commit and push:
```
git add .
git commit -m "Week 14 Completed — Phishing and Malware Triage Skills Built"
git push
```

**Deliverable**
`week-14-summary.md` plus a working phishing red-flag checklist and IOC template — real analyst tools, not just notes.

---

## Week 15 — Threat Intelligence and Traffic Analysis

### Week 15 Overview

**Theme**
An IOC by itself is just a piece of data. This week you learn to give it context — is this IP known-bad? Is this pattern a known C2 beacon? — by correlating your own findings against real threat intelligence sources.

**Week 15 Objectives**

```
✅ Understand threat intel types (strategic, tactical, operational)
✅ Use real threat intel tools to check IOCs
✅ Recognize C2 beaconing patterns in network traffic
✅ Correlate multiple IOCs across different sources
✅ Practice full alert-triage workflow in a guided investigation
```

**Success Criteria**

```
- Can you check an IP against VirusTotal and AbuseIPDB and interpret the results correctly?
- Can you describe what "beaconing" looks like in a packet capture, and why it's suspicious?
- Can you complete a full guided SOC investigation room without getting stuck for more than 20 minutes at a time?
```

**Week 15 Resources**

Primary Platform
```
TryHackMe (Free)
Rooms:
- Threat Intelligence Tools
- Traffic Analysis Essentials
- A SOC Level 1 investigative/capstone-style room
```

Tools
```
VirusTotal (free)
AbuseIPDB (free)
```

---

### DAY 99

**Goal**
Threat intelligence types and use.

**Hour 1 — Core Concept**

THM: **Threat Intelligence Tools**

Topics:
```
Strategic threat intel (for leadership, high-level trends)
Tactical threat intel (TTPs, for defenders)
Operational threat intel (specific IOCs, for immediate action)
```

**Hour 2 — Lab**

Complete the room's tasks using the actual tools it introduces (likely VirusTotal, URLscan, AbuseIPDB, or similar). For each IOC the room provides, record the verdict and the tool used.

**Hour 3 — Documentation**

Create:
```
threat-intel-notes.md
```

Document the 3 threat intel types with a concrete example of each from the room, plus your IOC-checking results.

Commit:
```
git add .
git commit -m "Threat Intelligence Fundamentals Completed"
git push
```

**Deliverable**
`threat-intel-notes.md` with real, tool-verified IOC lookups.

---

### DAY 100

**Goal**
Deeper threat intel practice using your own lab's IOCs.

**Hour 1 — Core Concept**

Reading/video: how analysts pivot from one IOC to related infrastructure (e.g., an IP leading to a domain, leading to related samples).

**Hour 2 — Lab**

Take 3 IOCs from your Week 14 phishing/malware work (or from a THM sample) and check each in both VirusTotal and AbuseIPDB:
```
IOC 1: (IP) - VirusTotal verdict: ___ - AbuseIPDB score: ___
IOC 2: (domain) - VirusTotal verdict: ___
IOC 3: (hash) - VirusTotal verdict: ___ (detection ratio, e.g., 45/70 engines)
```

Write a one-paragraph conclusion on whether these IOCs represent a credible threat based on the evidence.

**Hour 3 — Documentation**

Add "Cross-Source IOC Correlation" section to `threat-intel-notes.md` with your 3-IOC table and conclusion.

Commit:
```
git add .
git commit -m "Cross-Source IOC Correlation Practiced"
git push
```

**Deliverable**
A real, multi-source IOC correlation exercise with a documented conclusion — exactly what a Tier 1 analyst does before escalating a ticket.

---

### DAY 101

**Goal**
Traffic analysis essentials — recognizing malicious patterns.

**Hour 1 — Core Concept**

THM: **Traffic Analysis Essentials**

Topics:
```
Normal vs abnormal traffic baselines
C2 beaconing: regular time intervals, small consistent packet sizes
DNS tunneling indicators
```

**Hour 2 — Lab**

Complete the room's tasks, identifying beaconing or tunneling patterns in the provided PCAP(s). For each pattern found, note the specific Wireshark filter or statistic (e.g., `Statistics > Conversations`) that revealed it.

**Hour 3 — Documentation**

Add "Recognizing Beaconing" section to `threat-intel-notes.md` with a description of what beaconing looks like structurally in traffic, and the exact Wireshark technique used to spot it.

Commit:
```
git add .
git commit -m "Traffic Analysis - Beaconing Detection Completed"
git push
```

**Deliverable**
A documented, tool-verified explanation of how to spot C2 beaconing in real traffic.

---

### DAY 102

**Goal**
Network-based detection tools overview (Suricata/Snort concepts).

**Hour 1 — Core Concept**

THM: **Snort** (or equivalent network IDS room).

Topics:
```
Signature-based network detection
Snort/Suricata rule structure basics (alert, protocol, source, destination, options)
```

**Hour 2 — Lab**

Complete the room's tasks, writing or interpreting at least 2 basic Snort/Suricata rules against sample traffic provided in the room.

**Hour 3 — Documentation**

Add "Network IDS Concepts" section to `threat-intel-notes.md` with the 2 rules examined/written and what each detects.

Commit:
```
git add .
git commit -m "Network IDS Concepts Completed"
git push
```

**Deliverable**
A conceptual bridge between your host-based Wazuh rules (Month 3) and network-based IDS rules.

---

### DAY 103

**Goal**
Full guided SOC investigation practice.

**Hour 1 — Core Concept**

Preview the chosen SOC Level 1 investigative room's scenario before starting — read the room's introduction fully so you understand what you're being asked to determine.

**Hour 2 — Lab**

Work through the investigative room methodically:
```
Identify the initial alert/trigger
Follow the evidence trail using the room's provided tools/logs
Reach a conclusion (was this malicious? what happened? what's the scope?)
```

If stuck for more than 20 minutes on a single question, use one hint, and note where you needed help.

**Hour 3 — Documentation**

Create:
```
guided-investigation-01.md
```

Document your investigation process, evidence found, and final conclusion, in your own words (not copied from the room's answer key).

Commit:
```
git add .
git commit -m "Guided SOC Investigation Completed"
git push
```

**Deliverable**
A fully documented, self-narrated investigation — direct rehearsal for Week 16's independent capstone.

---

### DAY 104

**Goal**
Review and reinforce weak areas from Week 15.

**Hour 1 — Core Concept**

Reading/video: revisit whichever Week 15 topic felt least solid (threat intel correlation, beaconing recognition, or network IDS rules) with a second source or deeper dive.

**Hour 2 — Lab**

Repeat one relevant THM room task type you found hardest this week, using a fresh sample if the room allows retries, until you can complete it without hints.

**Hour 3 — Documentation**

Update `threat-intel-notes.md` with any corrections or deeper explanations from today's reinforcement.

Commit:
```
git add .
git commit -m "Week 15 Weak Areas Reinforced"
git push
```

**Deliverable**
A stronger, gap-free `threat-intel-notes.md` heading into the Week 15 review day.

---

### DAY 105

**Goal**
Consolidate and review — Week 15 capstone.

**Hour 1 — Core Concept**

Re-read all Week 15 notes out loud, end to end.

**Hour 2 — Lab**

Self-test, live, without notes:
```
1. Explain strategic vs tactical vs operational threat intel with an example of each
2. Check a new IOC in VirusTotal and AbuseIPDB and interpret the result
3. Explain what beaconing looks like in traffic, out loud
4. Summarize your Day 103 investigation from memory in under 2 minutes
```

Redo any failed item before Week 16.

**Hour 3 — Documentation**

Create:
```
week-15-summary.md
```

Structure:
```
Threat intel tools now comfortable using
Traffic analysis skills mastered
Guided investigation completed (linked)
Ready for: independent capstone incident (Week 16)
```

Commit and push:
```
git add .
git commit -m "Week 15 Completed — Threat Intel and Traffic Analysis Mastered"
git push
```

**Deliverable**
`week-15-summary.md` — you are now fully prepared to run an investigation independently.

---

## Week 16 — Full Simulated Incident (Crown Jewel Week)

### Week 16 Overview

**Theme**
Everything from Weeks 13–15 converges here. You will run one complete, independent investigation from first alert to final report — the single most important artifact of Month 4, and one of the most important in your entire portfolio.

**Week 16 Objectives**

```
✅ Independently investigate a realistic simulated incident
✅ Build a complete evidence-linked timeline
✅ Extract and organize all IOCs
✅ Map findings to MITRE ATT&CK
✅ Write a polished, professional Incident Report
```

**Success Criteria**

```
- Have you completed the full investigation without relying on a walkthrough/answer key?
- Does your final report follow your Week 13 template completely (Exec Summary through Lessons Learned)?
- Would a SOC manager reading this report understand exactly what happened, without needing to ask you follow-up questions?
```

**Week 16 Resources**

Primary Platform
```
TryHackMe (Free)
Room: a blue-team investigative capstone room (e.g., "Boogeyman 1" or a similarly structured incident-investigation room)
```

Tools
```
Your ir-timeline-template.md
Your ir-report-template.md
Your ioc-extraction-template.md
```

---

### DAY 106

**Goal**
Begin the capstone investigation — initial triage.

**Hour 1 — Core Concept**

Read the room's scenario introduction fully. Do not skip this — understanding what you're being asked to determine shapes your entire investigative approach.

**Hour 2 — Lab**

Begin the investigation:
```
Identify the initial alert/entry point
Note your very first hypothesis about what may have happened
Begin populating your ir-timeline-template.md with the first 2-3 confirmed events
```

**Hour 3 — Documentation**

Start:
```
month-04-crown-jewel/investigation-working-notes.md
```

Log your triage process and initial hypothesis honestly — including if it turns out to be wrong later, that's part of a real investigation.

Commit:
```
git add .
git commit -m "Capstone Incident - Initial Triage Started"
git push
```

**Deliverable**
Investigation underway with a documented initial hypothesis and first timeline entries.

---

### DAY 107

**Goal**
Continue the investigation — evidence gathering.

**Hour 1 — Core Concept**

No new content — review your Week 13-15 templates and checklists before continuing, to make sure you're being systematic rather than jumping around.

**Hour 2 — Lab**

Continue working through the room:
```
Follow the evidence trail methodically
Update your timeline with every new confirmed event
Extract every IOC encountered into your ioc-extraction-template.md
```

**Hour 3 — Documentation**

Update `investigation-working-notes.md` with today's progress and any hypothesis changes.

Commit:
```
git add .
git commit -m "Capstone Incident - Evidence Gathering Continued"
git push
```

**Deliverable**
A growing, evidence-linked timeline and IOC list.

---

### DAY 108

**Goal**
Complete the investigation and reach a final conclusion.

**Hour 1 — Core Concept**

No new content — this is a focused lab day.

**Hour 2 — Lab**

Finish the room's remaining questions/tasks:
```
Confirm the full attack chain, start to finish
Determine root cause
Determine scope (what was affected)
Finalize your timeline and IOC list
```

**Hour 3 — Documentation**

Write a "Final Conclusion" section in `investigation-working-notes.md` summarizing exactly what happened, in your own words, as if explaining it to a colleague who wasn't there.

Commit:
```
git add .
git commit -m "Capstone Incident - Investigation Completed"
git push
```

**Deliverable**
A fully completed, independently-run investigation with a clear final conclusion.

---

### DAY 109

**Goal**
Draft the Executive Summary and Timeline sections of the final report.

**Hour 1 — Core Concept**

Reading/video: how to write an Executive Summary that a non-technical director could read in 30 seconds and understand the business impact.

**Hour 2 — Lab**

Using your `ir-report-template.md`, draft:
```
## Executive Summary
(what happened, impact, current status - 3-4 sentences, zero jargon)

## Timeline
(your completed ir-timeline-template.md content, cleaned up)
```

**Hour 3 — Documentation**

Save progress as:
```
month-04-crown-jewel/incident-report-DRAFT.md
```

Commit:
```
git add .
git commit -m "IR Report - Executive Summary and Timeline Drafted"
git push
```

**Deliverable**
The first two sections of a polished IR report, written for two different audiences (executive and technical).

---

### DAY 110

**Goal**
Draft Technical Findings and MITRE ATT&CK mapping.

**Hour 1 — Core Concept**

Reading/video: how to write Technical Findings so they're detailed enough for another analyst to verify your work, but organized enough not to read like a stream of consciousness.

**Hour 2 — Lab**

Draft:
```
## Technical Findings
(organized by attack chain stage: Initial Access -> Execution -> Persistence -> etc., each with supporting evidence)

## MITRE ATT&CK Mapping
(table: Technique ID | Technique Name | Evidence Observed)
```

**Hour 3 — Documentation**

Continue building `incident-report-DRAFT.md` with these two sections.

Commit:
```
git add .
git commit -m "IR Report - Technical Findings and MITRE Mapping Drafted"
git push
```

**Deliverable**
Detailed, evidence-backed Technical Findings and a complete MITRE ATT&CK mapping table.

---

### DAY 111

**Goal**
Draft Remediation Recommendations and Lessons Learned.

**Hour 1 — Core Concept**

Reading/video: writing remediation recommendations that are specific and actionable (not generic "improve security" statements).

**Hour 2 — Lab**

Draft:
```
## Remediation Recommendations
(specific, prioritized: e.g., "Disable local admin rights for standard users," "Deploy the T1059.001 detection rule from Month 3 fleet-wide")

## Lessons Learned
(what would have caught this sooner, what worked well in this response)
```

Cross-reference your Month 3 Wazuh rules explicitly here where relevant — this ties your whole portfolio together.

**Hour 3 — Documentation**

Finalize `incident-report-DRAFT.md` with all sections complete.

Commit:
```
git add .
git commit -m "IR Report - Remediation and Lessons Learned Drafted"
git push
```

**Deliverable**
A complete first full draft of your Incident Response Report, all 6 sections written.

---

### DAY 112

**Goal**
Assemble and publish the Month 4 Crown Jewel — Crown Jewel Day.

**Hour 1 — Core Concept**

Re-read your entire Month 4 journey (Weeks 13–16) out loud, end to end, then re-read your full draft report as if you were a SOC manager seeing it for the first time.

**Hour 2 — Lab**

Final polish pass:
```
Fix any unclear technical explanations
Ensure every claim in Technical Findings links to specific evidence
Export the report to PDF in addition to the Markdown version
```

Assemble the final repository structure:
```
incident-response-casefile/
├── README.md
├── incident-report-FINAL.md
├── incident-report-FINAL.pdf
├── investigation-working-notes.md
└── templates/
    ├── ir-timeline-template.md
    ├── ir-report-template.md
    └── ioc-extraction-template.md
```

**Hour 3 — Documentation**

Write the master `README.md`:
```
# Incident Response Casefile

## What this repo demonstrates
- A complete, independently-run incident investigation
- A polished Incident Response Report following NIST 800-61-aligned structure
- Reusable IR timeline, report, and IOC extraction templates
- MITRE ATT&CK mapping of the full attack chain

## Structure
(explain folders)

## Skills demonstrated
(incident response methodology, evidence-based investigation, MITRE ATT&CK mapping, professional technical writing for both executive and technical audiences)
```

Final commit and push:
```
git add .
git commit -m "Month 4 Completed — Crown Jewel Published"
git push
```

**Deliverable**
A fully published `incident-response-casefile` repository — **Month 4 is complete**, and you now hold arguably your single strongest interview artifact.

---

*End of Chapter 4. Chapter 5 (Month 5 — Web Application Security and the Junior Pentester Stretch Goal) continues in the same format.*
