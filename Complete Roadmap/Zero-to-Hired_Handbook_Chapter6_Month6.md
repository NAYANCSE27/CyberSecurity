# Zero-to-Hired Cybersecurity Roadmap (Version 2026)
### A Complete 6-Month Handbook

---

# Chapter 6 — Month 6: Job Readiness, Certification, and the Final Application Push

Theme of the month: **You stop building skills and start selling them.**
Five months of real, validated, documented work now needs to reach a hiring manager's eyes in a form that gets you an interview — and once you're in that interview, you need to be able to narrate your own work with total confidence.

---

## Week 21 — Portfolio Polish, Resume, and LinkedIn

### Week 21 Overview

**Theme**
A brilliant home lab that nobody can find is worthless to your job search. This week turns five months of work into materials that survive a 6-second recruiter scan and reward a 6-minute hiring manager read.

**Week 21 Objectives**

```
✅ Draft an ATS-optimized, metrics-driven one-page resume
✅ Rebuild your LinkedIn headline, About section, and Featured projects
✅ Build a GitHub profile README tying all 5 repos together
✅ Get real feedback and incorporate it
```

**Success Criteria**

```
- Does your resume fit one page with zero paragraphs, only scannable bullets?
- Does every bullet include a concrete result or metric, not just a task description?
- Can a stranger find and understand all 5 of your Crown Jewel repos within 60 seconds of landing on your GitHub profile?
```

**Week 21 Resources**

```
Your own 5 Crown Jewel repositories (Months 1-5)
A free ATS resume checker (e.g., a resume-scanning tool of your choice)
r/cybersecurity or a relevant Discord community for peer feedback
```

---

### DAY 141

**Goal**
Draft resume version 1.

**Hour 1 — Core Concept**

Reading/video: ATS resume formatting rules — standard section headers, no tables/graphics/columns that confuse parsers, keyword alignment with real job descriptions.

**Hour 2 — Lab**

Draft the full resume structure:
```
Header (name, email, phone, LinkedIn, GitHub)
Summary (2-3 lines)
Skills (grouped: SOC/Detection, Offensive Security, Scripting, Tools)
Projects (your 5 Crown Jewels, 1-2 bullets each)
Education / Certifications (in progress noted honestly)
```

Pull 3 real entry-level SOC Analyst job descriptions and highlight every recurring keyword/skill mentioned — you'll align your bullets to these in Day 142.

**Hour 3 — Documentation**

Save as:
```
job-search/resume-v1.md
```

Also save the 3 job description keyword lists you pulled.

Commit:
```
git add .
git commit -m "Resume v1 Drafted"
git push
```

**Deliverable**
A complete first-draft resume plus a keyword-alignment reference from real job postings.

---

### DAY 142

**Goal**
Rewrite every bullet with quantified achievements.

**Hour 1 — Core Concept**

Reading/video: the "action verb + what you did + measurable result" bullet formula.

**Hour 2 — Lab**

Rewrite each project bullet using this formula, for example:
```
Weak: "Worked on a SIEM project using Wazuh."
Strong: "Deployed a Wazuh SIEM ingesting Sysmon and auditd telemetry from 2 hosts; authored and validated 5 custom detection rules mapped to MITRE ATT&CK, achieving 100% detection rate against Atomic Red Team simulations."
```

Do this for all 5 Crown Jewel bullets plus your top 3 skill-section items.

**Hour 3 — Documentation**

Update `resume-v1.md` with all rewritten bullets.

Commit:
```
git add .
git commit -m "Resume Bullets Quantified"
git push
```

**Deliverable**
A resume where every bullet demonstrates a measurable result, not just a listed task.

---

### DAY 143

**Goal**
Rebuild LinkedIn headline and About section.

**Hour 1 — Core Concept**

Reading/video: what recruiters actually scan for in a LinkedIn headline (role target + top 2-3 keywords) and About section (narrative + proof points).

**Hour 2 — Lab**

Draft:
```
Headline: "Aspiring SOC Analyst | Wazuh · Detection Engineering · Incident Response | Home-Lab Builder"

About section:
- 2 sentences: your background and why cybersecurity
- 3-4 sentences: what you built (reference your 5 Crown Jewels specifically)
- 1 sentence: what you're looking for (entry-level SOC/Security Analyst roles)
```

Update your live LinkedIn profile with this content.

**Hour 3 — Documentation**

Save a copy for reference:
```
job-search/linkedin-content.md
```

Commit:
```
git add .
git commit -m "LinkedIn Headline and About Section Rebuilt"
git push
```

**Deliverable**
A live, updated LinkedIn profile with a targeted headline and proof-driven About section.

---

### DAY 144

**Goal**
Build the GitHub profile README.

**Hour 1 — Core Concept**

Reading/video: GitHub profile README best practices — a special repo named exactly as your username that renders on your profile page.

**Hour 2 — Lab**

Create a repo named exactly as your GitHub username (e.g., if your username is `janedoe`, create a repo called `janedoe`), then add:
```
README.md
```

Content:
```
# Hi, I'm [Name] — Aspiring SOC Analyst

## My Journey
(1 short paragraph: 6 months, self-taught, hands-on home lab focus)

## Featured Projects
| Project | Description | Skills |
|---|---|---|
| homelab-network-foundations | ... | Networking, Wireshark |
| ad-homelab-and-automation | ... | Active Directory, PowerShell, Python |
| wazuh-detection-lab | ... | SIEM, Detection Engineering, MITRE ATT&CK |
| incident-response-casefile | ... | IR, Investigation, Reporting |
| junior-pentest-portfolio | ... | Web App Security, HTB, Pentest Reporting |

## Skills
(grouped list)

## Let's Connect
(LinkedIn link)
```

**Hour 3 — Documentation**

Push the profile README live and verify it renders correctly on your GitHub profile page.

Commit:
```
git add .
git commit -m "GitHub Profile README Published"
git push
```

**Deliverable**
A live, rendering GitHub profile README linking all 5 Crown Jewel repositories.

---

### DAY 145

**Goal**
Get real external feedback.

**Hour 1 — Core Concept**

Reading/video: how to ask for feedback effectively (specific questions get specific answers — avoid just posting "roast my resume" with no context).

**Hour 2 — Lab**

Post your resume (redact personal contact info if preferred) to r/cybersecurity, a relevant Discord community, or a trusted mentor, with specific questions:
```
"Does this read as job-ready for entry-level SOC roles?"
"Are my project bullets clear to someone outside my head?"
"Is anything here a red flag?"
```

While waiting for responses, do a final self-review pass: read your resume upside down or from the bottom up (a real trick to catch typos you'd otherwise skim past).

**Hour 3 — Documentation**

Create:
```
job-search/feedback-log.md
```

Log every piece of feedback received, even feedback you disagree with — you'll triage it tomorrow.

Commit:
```
git add .
git commit -m "External Feedback Requested and Logged"
git push
```

**Deliverable**
A logged set of real, external feedback on your resume.

---

### DAY 146

**Goal**
Incorporate feedback and finalize materials.

**Hour 1 — Core Concept**

Reading/video: none — this is an editing day. Reading is replaced by critically re-reading your own feedback log.

**Hour 2 — Lab**

Triage the feedback from Day 145:
```
For each piece of feedback: Accept and revise / Consider but decline (with reason) / Needs more research
```

Apply all accepted changes to your resume and LinkedIn content.

**Hour 3 — Documentation**

Finalize:
```
job-search/resume-FINAL.md (and export to PDF)
```

Update `linkedin-content.md` with final wording.

Commit:
```
git add .
git commit -m "Resume and LinkedIn Finalized After Feedback"
git push
```

**Deliverable**
A finalized, feedback-tested resume (PDF) and LinkedIn profile.

---

### DAY 147

**Goal**
Consolidate and review — Week 21 capstone.

**Hour 1 — Core Concept**

Re-read your final resume, LinkedIn content, and GitHub README out loud, as if you were a hiring manager encountering them for the very first time.

**Hour 2 — Lab**

Self-test:
```
1. Time yourself explaining your GitHub profile to an imaginary recruiter in under 60 seconds
2. Check that your resume, LinkedIn, and GitHub all tell a perfectly consistent story
3. Confirm every link (GitHub repos, LinkedIn) actually works when clicked
```

**Hour 3 — Documentation**

Create:
```
week-21-summary.md
```

Structure:
```
Materials finalized: resume, LinkedIn, GitHub profile (all linked)
Feedback incorporated
Ready for: Security+ exam sprint (Week 22)
```

Commit and push:
```
git add .
git commit -m "Week 21 Completed — Job Search Materials Finalized"
git push
```

**Deliverable**
A fully consistent, polished, externally-validated professional presence across resume, LinkedIn, and GitHub.

---

## Week 22 — Security+ Exam Prep Sprint

### Week 22 Overview

**Theme**
Five months of hands-on work means exam theory now has somewhere to "stick." This week is a concentrated, domain-by-domain sprint using free practice resources, converting your lab experience into exam-ready recall.

**Week 22 Objectives**

```
✅ Cover all 5 CompTIA Security+ domains systematically
✅ Map exam concepts back to your own hands-on lab experience
✅ Take full-length timed practice exams
✅ Identify and close your weakest domain gaps
```

**Success Criteria**

```
- Are you consistently scoring 85%+ on domain-specific practice questions?
- Are you scoring 80%+ on full-length timed practice exams?
- Can you explain your 2 weakest domains' core concepts without notes by the end of the week?
```

**Week 22 Resources**

```
Professor Messer's free Security+ course and practice exams
ExamCompass free practice tests
Official CompTIA Security+ exam objectives (SY0- current version) as your syllabus checklist
```

---

### DAY 148

**Goal**
Domain 1 — General Security Concepts.

**Hour 1 — Core Concept**

Professor Messer (free): Domain 1 videos — security controls, CIA/AAA, zero trust, cryptographic solutions overview.

**Hour 2 — Lab**

Take 25 Domain 1 practice questions. For every question you get wrong, write down why the correct answer is correct, not just what it is.

Explicitly connect at least 3 concepts to your own lab work (e.g., your Month 4 CIA Triad scenario table).

**Hour 3 — Documentation**

Create:
```
job-search/security-plus-notes/domain-1-notes.md
```

Document weak areas and your lab-connections.

Commit:
```
git add .
git commit -m "Security+ Domain 1 Studied"
git push
```

**Deliverable**
Domain 1 practice score logged, weak areas documented.

---

### DAY 149

**Goal**
Domain 2 — Threats, Vulnerabilities, and Mitigations.

**Hour 1 — Core Concept**

Professor Messer (free): Domain 2 videos — malware types, social engineering, vulnerability types, mitigation techniques.

**Hour 2 — Lab**

Take 25 Domain 2 practice questions, reviewing every wrong answer.

Explicitly map this domain to your Month 4 phishing/malware triage work and Month 3 detection rules — this domain should feel the most "familiar" of all five given your lab history.

**Hour 3 — Documentation**

Create:
```
job-search/security-plus-notes/domain-2-notes.md
```

Commit:
```
git add .
git commit -m "Security+ Domain 2 Studied"
git push
```

**Deliverable**
Domain 2 practice score logged, with explicit lab-experience connections noted.

---

### DAY 150

**Goal**
Domain 3 — Security Architecture.

**Hour 1 — Core Concept**

Professor Messer (free): Domain 3 videos — architecture models, cloud/hybrid considerations, network segmentation, resilience/recovery.

**Hour 2 — Lab**

Take 25 Domain 3 practice questions, reviewing every wrong answer.

Connect concepts to your Month 1 lab network segmentation design (Week 4).

**Hour 3 — Documentation**

Create:
```
job-search/security-plus-notes/domain-3-notes.md
```

Commit:
```
git add .
git commit -m "Security+ Domain 3 Studied"
git push
```

**Deliverable**
Domain 3 practice score logged.

---

### DAY 151

**Goal**
Domain 4 — Security Operations.

**Hour 1 — Core Concept**

Professor Messer (free): Domain 4 videos — incident response, digital forensics, SIEM/log management, vulnerability management.

**Hour 2 — Lab**

Take 25 Domain 4 practice questions. This domain should feel the easiest given your Months 3-4 work — if it doesn't, that's a signal to revisit your Wazuh and IR documentation, not just exam prep material.

**Hour 3 — Documentation**

Create:
```
job-search/security-plus-notes/domain-4-notes.md
```

Commit:
```
git add .
git commit -m "Security+ Domain 4 Studied"
git push
```

**Deliverable**
Domain 4 practice score logged — expect (and confirm) your highest domain score here.

---

### DAY 152

**Goal**
Domain 5 — Security Program Management and Oversight.

**Hour 1 — Core Concept**

Professor Messer (free): Domain 5 videos — governance, risk management, third-party risk, compliance basics, security awareness.

**Hour 2 — Lab**

Take 25 Domain 5 practice questions, reviewing every wrong answer. This domain will likely feel least "hands-on" — that's expected; focus on memorization aids (e.g., flashcards for policy/framework names) rather than trying to force a lab connection that doesn't exist.

**Hour 3 — Documentation**

Create:
```
job-search/security-plus-notes/domain-5-notes.md
```

Commit:
```
git add .
git commit -m "Security+ Domain 5 Studied"
git push
```

**Deliverable**
Domain 5 practice score logged — all 5 domains now covered once.

---

### DAY 153

**Goal**
First full-length timed practice exam.

**Hour 1 — Core Concept**

None — this hour also goes toward the exam itself given its length; treat Hours 1-2 as one continuous block.

**Hour 2 — Lab**

Take one full-length, timed practice exam (ExamCompass or Professor Messer's practice test), under real exam conditions — no notes, no pausing.

**Hour 3 — Documentation**

Create:
```
job-search/security-plus-notes/practice-exam-01-review.md
```

Review every single wrong answer, and identify your 2 weakest domains by score.

Commit:
```
git add .
git commit -m "First Full Security+ Practice Exam Completed"
git push
```

**Deliverable**
A scored practice exam with your 2 weakest domains explicitly identified for Day 154's focused review.

---

### DAY 154

**Goal**
Targeted weak-area review + second practice exam (if time allows).

**Hour 1 — Core Concept**

Re-watch Professor Messer's videos for your 2 weakest domains specifically, focusing only on the concepts you got wrong.

**Hour 2 — Lab**

Take a second full-length practice exam if your schedule allows, or take 25 additional targeted practice questions specifically from your 2 weakest domains.

**Hour 3 — Documentation**

Update the relevant domain notes files with corrected understanding.

Create:
```
week-22-summary.md
```

Structure:
```
Domain scores (all 5, plus full exam scores)
Weakest areas and how they were addressed
Exam readiness: scheduled / not yet scheduled (with honest reasoning)
```

Commit and push:
```
git add .
git commit -m "Week 22 Completed — Security+ Exam Prep Sprint Finished"
git push
```

**Deliverable**
`week-22-summary.md` with honest, data-backed exam readiness assessment — and either a scheduled exam date or a clear plan for after this program, per the Month 5-6 Reality Check principle.

---

## Week 23 — Mock Interviews and Application Blitz

### Week 23 Overview

**Theme**
Skills without interview-readiness don't get hired. This week you drill both technical and behavioral interview performance, then start applying at real volume.

**Week 23 Objectives**

```
✅ Prepare strong answers to common SOC analyst technical questions
✅ Build STAR-method behavioral answers grounded in your real projects
✅ Complete 2 mock interviews and incorporate feedback
✅ Submit 20+ tailored applications
```

**Success Criteria**

```
- Can you answer "walk me through investigating a phishing alert" fluently, unaided?
- Do you have a ready STAR answer for at least 5 common behavioral questions?
- Have you submitted 20+ applications with resume bullets tailored to each posting's keywords?
```

**Week 23 Resources**

```
Your own 5 Crown Jewel projects (as evidence for every answer)
A peer, mentor, or AI-based mock interview partner
Job boards: LinkedIn Jobs, Indeed, company career pages
```

---

### DAY 155

**Goal**
Prepare technical interview answers.

**Hour 1 — Core Concept**

Reading/video: common SOC analyst technical interview questions — log analysis walkthroughs, alert triage prioritization, "what would you do if..." scenarios.

**Hour 2 — Lab**

Draft and rehearse spoken (not just written) answers to 10 common technical questions, e.g.:
```
"Walk me through how you'd investigate a phishing alert."
"How do you prioritize alerts when you have 50 in your queue?"
"Explain the difference between a false positive and a true negative."
"What would you do if you found a scheduled task you didn't recognize on a server?"
```

Record yourself answering 3 of these out loud, then listen back critically.

**Hour 3 — Documentation**

Create:
```
job-search/interview-prep/technical-questions.md
```

Document all 10 questions with your refined written answers.

Commit:
```
git add .
git commit -m "Technical Interview Answers Drafted"
git push
```

**Deliverable**
10 rehearsed, documented technical interview answers.

---

### DAY 156

**Goal**
Build STAR-method behavioral answers.

**Hour 1 — Core Concept**

Reading/video: the STAR method (Situation, Task, Action, Result) for structuring behavioral answers concisely and concretely.

**Hour 2 — Lab**

Draft STAR answers for 5 behavioral questions, using your actual project experiences as evidence:
```
"Tell me about a time you had to investigate something with incomplete information." -> Your Month 4 capstone incident
"Describe a time you had to learn a new tool quickly." -> Your Wazuh deployment (Month 3)
"Tell me about a mistake you made and what you learned." -> A specific lab failure (e.g., a rule that didn't fire correctly at first)
"How do you handle repetitive or high-volume work?" -> Your PowerShell/Python automation work
"Why cybersecurity, and why now?" -> Your personal narrative
```

**Hour 3 — Documentation**

Create:
```
job-search/interview-prep/behavioral-star-answers.md
```

Commit:
```
git add .
git commit -m "STAR Behavioral Answers Drafted"
git push
```

**Deliverable**
5 concrete, evidence-backed STAR answers ready for any behavioral interview.

---

### DAY 157

**Goal**
First mock interview.

**Hour 1 — Core Concept**

Reading/video: none — instead, re-read your technical and behavioral answer docs one final time before the mock.

**Hour 2 — Lab**

Conduct a full mock interview (peer, mentor, or AI-based mock interview tool), covering both technical and behavioral questions. Take notes on where you hesitated, rambled, or gave a weak answer.

**Hour 3 — Documentation**

Create:
```
job-search/interview-prep/mock-interview-01-feedback.md
```

Document specific weak spots identified.

Commit:
```
git add .
git commit -m "Mock Interview 1 Completed"
git push
```

**Deliverable**
Documented feedback from your first mock interview.

---

### DAY 158

**Goal**
Fix weak spots + research target companies.

**Hour 1 — Core Concept**

Reading/video: none — this hour goes toward revising your weakest answers from Day 157's feedback.

**Hour 2 — Lab**

Revise your 2-3 weakest answers from the mock interview. Then research 5 target companies:
```
For each: what does their SOC team likely look like (size, tools mentioned in job postings)?
What's one thing you could mention in an interview that shows you researched them specifically?
```

**Hour 3 — Documentation**

Update `mock-interview-01-feedback.md` with your revised answers.

Create:
```
job-search/target-companies.md
```

Commit:
```
git add .
git commit -m "Mock Interview Weak Spots Fixed, Target Companies Researched"
git push
```

**Deliverable**
Revised answers plus a researched target-company list.

---

### DAY 159

**Goal**
Second mock interview — technical whiteboard style.

**Hour 1 — Core Concept**

Reading/video: none — review your technical answers one more time, focusing specifically on scenario-based "walk me through" questions.

**Hour 2 — Lab**

Conduct a second mock interview, focused specifically on scenario/whiteboard-style technical questions (e.g., "an alert just fired for encoded PowerShell — walk me through your next 10 minutes").

**Hour 3 — Documentation**

Create:
```
job-search/interview-prep/mock-interview-02-feedback.md
```

Commit:
```
git add .
git commit -m "Mock Interview 2 Completed"
git push
```

**Deliverable**
A second round of documented interview feedback, focused on live scenario reasoning.

---

### DAY 160

**Goal**
First application push.

**Hour 1 — Core Concept**

Reading/video: job search strategy basics — using job boards effectively, the value of referrals, and how to spot a role that's actually entry-level friendly vs. one that says "entry-level" but lists 3+ years required.

**Hour 2 — Lab**

Apply to 10 tailored roles:
```
For each application: customize 2-3 resume bullets to match that specific posting's keywords
Log the company, role, and date applied
```

**Hour 3 — Documentation**

Create:
```
job-search/application-tracker.md
```

Structure:
```
| Date | Company | Role | Status | Notes |
```

Commit:
```
git add .
git commit -m "First 10 Applications Submitted"
git push
```

**Deliverable**
10 tailored applications submitted and tracked.

---

### DAY 161

**Goal**
Second application push + networking outreach.

**Hour 1 — Core Concept**

Reading/video: how to write a genuine, non-spammy LinkedIn connection request to someone in a role you want.

**Hour 2 — Lab**

Apply to 10 more tailored roles, logging each in your tracker.

Send 5 personalized LinkedIn connection requests to SOC analysts or hiring managers at your target companies, each with a specific, genuine note (not a copy-paste template).

**Hour 3 — Documentation**

Update `application-tracker.md` with the 10 new applications.

Create:
```
week-23-summary.md
```

Structure:
```
Total applications submitted this week: 20
Mock interviews completed: 2 (feedback linked)
Networking outreach sent: 5
Ready for: capstone finalization and final push (Week 24)
```

Commit and push:
```
git add .
git commit -m "Week 23 Completed — Interview Prep and Application Blitz Done"
git push
```

**Deliverable**
20 total applications submitted, 2 mock interviews completed, and real networking outreach underway.

---

## Week 24 — Capstone Finalization and Final Application Push

### Week 24 Overview

**Theme**
The final week ties every month of work into one capstone artifact and pushes the job search into its highest gear. This is graduation week.

**Week 24 Objectives**

```
✅ Design and execute a multi-stage capstone attack simulation
✅ Investigate it yourself and write the incident report
✅ Publish a polished, cross-linked GitHub profile tying all 6 projects together
✅ Submit 10+ more applications and confirm interview readiness
```

**Success Criteria**

```
- Does your capstone chain at least 3 MITRE ATT&CK techniques across a believable attack narrative?
- Did your Month 3 Wazuh detection rules actually fire during the simulation?
- Is your full 6-project GitHub portfolio reviewable, end to end, by a stranger in under 10 minutes?
- Have you submitted 30+ total applications this month?
```

**Week 24 Resources**

```
Your own full lab environment (AD, Wazuh, Atomic Red Team) from Months 2-3
Your IR report and timeline templates from Month 4
```

---

### DAY 162

**Goal**
Design the capstone attack chain.

**Hour 1 — Core Concept**

Reading/video: none — review your own Month 3 detection matrix and Month 4 IR report structure before designing.

**Hour 2 — Lab**

Design a believable multi-stage attack chain using techniques your lab can actually generate telemetry for:
```
Stage 1: Initial Access - Suspicious PowerShell execution (T1059.001)
Stage 2: Persistence - Scheduled task creation (T1053.005)
Stage 3: Privilege Escalation - Account added to Domain Admins (T1098)
```

**Hour 3 — Documentation**

Create:
```
month-06-crown-jewel/capstone-scenario-design.md
```

Document the narrative: what a real attacker's goal and story would be across these 3 stages.

Commit:
```
git add .
git commit -m "Capstone Attack Chain Designed"
git push
```

**Deliverable**
A designed, MITRE-grounded, 3-stage attack scenario ready for execution.

---

### DAY 163

**Goal**
Execute capstone stages 1–2.

**Hour 1 — Core Concept**

Reading/video: none — review your Atomic Red Team commands from Month 3, Week 12.

**Hour 2 — Lab**

Execute Stage 1 and Stage 2 using Atomic Red Team, confirming each corresponding Wazuh rule fires:
```powershell
Invoke-AtomicTest T1059.001
Invoke-AtomicTest T1053.005
```

Screenshot both alerts firing in Wazuh with timestamps.

**Hour 3 — Documentation**

Begin:
```
month-06-crown-jewel/capstone-investigation-notes.md
```

Log the execution and alert confirmation for both stages.

Commit:
```
git add .
git commit -m "Capstone Stages 1-2 Executed"
git push
```

**Deliverable**
2 of 3 attack stages executed and confirmed detected.

---

### DAY 164

**Goal**
Execute capstone stage 3 and confirm full detection coverage.

**Hour 1 — Core Concept**

Reading/video: none — review your rule 100014 (privileged group change) logic from Month 3.

**Hour 2 — Lab**

Execute Stage 3:
```powershell
Invoke-AtomicTest T1098
```

Confirm rule 100014 fires, then clean up:
```powershell
Invoke-AtomicTest T1098 -Cleanup
```

Review the full Wazuh dashboard timeline across all 3 stages together, confirming the complete chain is visible and correctly ordered.

**Hour 3 — Documentation**

Update `capstone-investigation-notes.md` with Stage 3 execution and the full 3-stage detection confirmation.

Commit:
```
git add .
git commit -m "Capstone Stage 3 Executed - Full Chain Detected"
git push
```

**Deliverable**
All 3 attack stages executed, with 100% detection coverage confirmed across your own custom rule set.

---

### DAY 165

**Goal**
Write the capstone investigation narrative.

**Hour 1 — Core Concept**

Reading/video: none — review your Month 4 IR report template one final time.

**Hour 2 — Lab**

Write the investigation as if you were the on-call analyst who received these 3 alerts in sequence with no prior knowledge of the "attack" you designed:
```
What alert came in first, and what was your initial hypothesis?
How did each subsequent alert changed or confirmed your understanding?
What would you have done differently if this were a real, unknown incident?
```

**Hour 3 — Documentation**

Create:
```
month-06-crown-jewel/capstone-investigation-narrative.md
```

Commit:
```
git add .
git commit -m "Capstone Investigation Narrative Written"
git push
```

**Deliverable**
A "day in the life" investigation narrative — the emotional and practical centerpiece of your capstone.

---

### DAY 166

**Goal**
Write the full capstone IR report.

**Hour 1 — Core Concept**

Reading/video: none — this is a writing day, using your own Month 4 `ir-report-template.md`.

**Hour 2 — Lab**

Complete the full IR report for the capstone incident using your reusable template:
```
Executive Summary
Timeline (all 3 stages)
Technical Findings
IOCs
MITRE ATT&CK Mapping (all 3 techniques)
Remediation Recommendations
Lessons Learned
```

**Hour 3 — Documentation**

Save as:
```
month-06-crown-jewel/capstone-incident-report-FINAL.md
```

Commit:
```
git add .
git commit -m "Capstone Incident Report Completed"
git push
```

**Deliverable**
A complete, polished IR report for a self-designed, self-detected, self-investigated incident — closing the loop on your entire 6-month journey.

---

### DAY 167

**Goal**
Assemble and publish the Month 6 Crown Jewel + final GitHub profile — Crown Jewel Day.

**Hour 1 — Core Concept**

Re-read your entire 6-month journey, chapter by chapter, out loud. This is the last time you'll do this as a structured exercise — from here forward, this knowledge simply is who you are professionally.

**Hour 2 — Lab**

Assemble the final capstone repository:
```
capstone-soc-simulation/
├── README.md
├── capstone-scenario-design.md
├── capstone-investigation-notes.md
├── capstone-investigation-narrative.md
└── capstone-incident-report-FINAL.md
```

Do a final polish pass across ALL 6 repositories: check every link, fix any typos, ensure consistent formatting.

Update your GitHub profile README (from Week 21) to include the 6th project.

**Hour 3 — Documentation**

Write the master `README.md` for the capstone:
```
# Capstone SOC Simulation

## What this repo demonstrates
- A self-designed, 3-stage attack chain executed via Atomic Red Team
- 100% detection coverage using custom Wazuh rules built in Month 3
- A full "day in the life" investigation narrative
- A complete, polished Incident Response Report

## This project ties together
- Networking & home lab foundations (Month 1)
- Active Directory & scripting (Month 2)
- SIEM & detection engineering (Month 3)
- Incident response methodology (Month 4)
- Offensive security understanding (Month 5)
```

Final commit and push:
```
git add .
git commit -m "Month 6 Completed — Final Crown Jewel Published, Portfolio Complete"
git push
```

**Deliverable**
A fully published `capstone-soc-simulation` repository and a complete, cross-linked, 6-project GitHub portfolio — **the entire 6-month journey is now complete and publicly demonstrable.**

---

### DAY 168

**Goal**
Final review and final application blitz — Program Completion Day.

**Hour 1 — Core Concept**

Reading/video: none — instead, read through your resume, LinkedIn, and full GitHub portfolio one final time, exactly as a hiring manager would encounter them in sequence.

**Hour 2 — Lab**

Final application blitz:
```
Submit 10+ final tailored applications
Follow up on any earlier applications that have gone quiet (polite, brief follow-up messages)
Confirm your resume/LinkedIn/GitHub are perfectly consistent with each other
```

**Hour 3 — Documentation**

Create the final capstone document of the entire program:
```
program-completion-summary.md
```

Structure:
```
## 6 Crown Jewel Projects (all linked)
1. homelab-network-foundations
2. ad-homelab-and-automation
3. wazuh-detection-lab
4. incident-response-casefile
5. junior-pentest-portfolio
6. capstone-soc-simulation

## Total applications submitted: [your real number]
## Mock interviews completed: 2+
## Security+ status: [exam sat / scheduled / studied and ready]

## What I'm most proud of
## What I'll keep building after this program
```

Final commit and push:
```
git add .
git commit -m "Program Completed — 6 Months, 6 Crown Jewel Projects, Job Search Underway"
git push
```

**Deliverable**
`program-completion-summary.md` — the final artifact of a genuinely complete, evidence-backed, 6-month transformation from basic Python knowledge to a job-ready, portfolio-proven SOC/Security Analyst candidate.

---

# Closing Note

You now have exactly what Part 4 of this roadmap promised on Day 1: a resume, LinkedIn, and GitHub that all tell the same true story, backed by 6 real projects a hiring manager can click into and verify themselves. That is genuinely rare at the entry level — most candidates have certifications and no proof; you have proof and are closing the certification gap in parallel.

The job search timeline from here is the one variable this handbook cannot control. Keep applying at volume, keep your mock-interview muscle warm even after Week 24 ends, and treat every "no" as a data point to refine your materials, not a verdict on your ability. You built all of this in 168 days, three hours at a time. That discipline is itself the strongest signal of hireability you have.

*End of Handbook.*
