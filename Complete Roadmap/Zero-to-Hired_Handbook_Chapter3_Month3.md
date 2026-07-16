# Zero-to-Hired Cybersecurity Roadmap (Version 2026)
### A Complete 6-Month Handbook

---

# Chapter 3 — Month 3: SOC Foundations, SIEM Deployment, and Detection Engineering

Theme of the month: **You stop being someone who reacts to alerts and become someone who builds the system that generates them.**
This month you deploy a real SIEM, feed it real telemetry from your Month 2 lab, and write detection rules you personally validate against real attack simulations.

---

## Week 9 — SOC Foundations and SIEM Concepts

### Week 9 Overview

**Theme**
Before touching Wazuh, you need the mental model of what a SOC actually does and how a SIEM turns noise into signal. This week is 60% concept, 40% hands-on Splunk practice — the one week where theory slightly outweighs labs, because the concepts here govern everything for the rest of the month.

**Week 9 Objectives**

```
✅ Understand SOC tiers and analyst workflow (Tier 1/2/3)
✅ Understand log aggregation, correlation, and alerting at a SIEM level
✅ Run real SPL (Splunk Search Processing Language) queries
✅ Build a basic Splunk dashboard
✅ Build a personal "SIEM vocabulary" reference
```

**Success Criteria**

```
- Can you explain the difference between a Tier 1, Tier 2, and Tier 3 analyst's responsibilities?
- Can you explain, unaided, why a SIEM is more useful than reading individual log files?
- Can you write an SPL query using stats, eval, and where without notes?
- Could you explain "correlation rule" to a non-technical person in one sentence?
```

**Week 9 Resources**

Primary Platform
```
TryHackMe (Free)
Rooms:
- Intro to SOC (or equivalent SOC Level 1 path intro room)
- Security Logging Concepts
- Splunk: Basics
- Splunk: Search Fundamentals
```

---

### DAY 57

**Goal**
Understand the SOC and analyst tiers.

**Hour 1 — Core Concept**

THM: **Intro to SOC**

Topics:
```
What a SOC monitors and why
Tier 1 (triage) vs Tier 2 (investigation) vs Tier 3 (threat hunting/engineering)
Shift-based operations, escalation paths
```

**Hour 2 — Lab**

Write out, in your own words, a full "day in the life" of a Tier 1 analyst — an alert comes in, what do they do first, second, third, and when do they escalate? Base this entirely on what you learned, not assumptions.

Then map your own Month 1-2 lab work to each tier:
```
Tier 1 skill you already have: (e.g., reading Event Viewer for 4625)
Tier 2 skill you already have: (e.g., correlating Sysmon + Security log events)
Tier 3 skill you're building toward: (e.g., writing your own detection rules)
```

**Hour 3 — Documentation**

Create:
```
soc-fundamentals-notes.md
```

Include your "day in the life" narrative and the tier-mapping exercise.

Commit:
```
git add .
git commit -m "SOC Tiers and Analyst Workflow Understood"
git push
```

**Deliverable**
`soc-fundamentals-notes.md` with a self-written analyst workflow narrative.

---

### DAY 58

**Goal**
Log aggregation and correlation concepts.

**Hour 1 — Core Concept**

THM: **Security Logging Concepts**

Topics:
```
Log sources (endpoint, network, application, cloud)
Aggregation: why centralize logs at all
Correlation rules: combining multiple weak signals into one strong alert
```

**Hour 2 — Lab**

Design (on paper/draw.io, no tool yet) a correlation rule using your own lab's real log sources:
```
Signal 1: Sysmon Event ID 1 - powershell.exe with an encoded command
Signal 2: Sysmon Event ID 3 - network connection from powershell.exe to an external IP
Correlation rule: IF both signals occur from the same host within 60 seconds, THEN raise a HIGH severity alert
```

Write out why neither signal alone is sufficient, but together they're strong evidence of malicious activity.

**Hour 3 — Documentation**

Add "Log Correlation Design" section to `soc-fundamentals-notes.md` with your correlation rule design and reasoning.

Commit:
```
git add .
git commit -m "Log Aggregation and Correlation Concepts Completed"
git push
```

**Deliverable**
A hand-designed correlation rule — the exact rule you'll implement for real in Week 11.

---

### DAY 59

**Goal**
Splunk basics and architecture.

**Hour 1 — Core Concept**

THM: **Splunk: Basics**

Topics:
```
Splunk architecture: Forwarders, Indexers, Search Heads
Indexes and sourcetypes
The Splunk Search interface
```

**Hour 2 — Lab**

Complete the THM room's hands-on tasks in the provided Splunk instance:
```
Navigate the Search & Reporting app
Run a basic search: index=main
Identify at least 3 different sourcetypes present in the sample data
```

**Hour 3 — Documentation**

Create:
```
splunk-notes.md
```

Document Splunk's architecture in your own words with a simple diagram (forwarder → indexer → search head).

Commit:
```
git add .
git commit -m "Splunk Architecture and Basics Completed"
git push
```

**Deliverable**
`splunk-notes.md` with an original architecture diagram.

---

### DAY 60

**Goal**
SPL search fundamentals.

**Hour 1 — Core Concept**

THM: **Splunk: Search Fundamentals**

Topics:
```
Basic search syntax
Time range picker
Pipe ( | ) to chain commands
```

**Hour 2 — Lab**

Run and document 5 SPL searches in the THM Splunk instance:
```
index=main sourcetype=* error
index=main | top limit=10 sourcetype
index=main | stats count by host
index=main status=404
index=main | timechart count
```

**Hour 3 — Documentation**

Add "SPL Basics" section to `splunk-notes.md` with each query and a one-line explanation of what it returns.

Commit:
```
git add .
git commit -m "SPL Search Fundamentals Completed"
git push
```

**Deliverable**
5 documented, working SPL queries.

---

### DAY 61

**Goal**
Advanced SPL: `stats`, `eval`, `where`.

**Hour 1 — Core Concept**

Reading/video (THM room continuation or Splunk docs): `stats` for aggregation, `eval` for computed fields, `where` for filtering on computed values.

**Hour 2 — Lab**

Write 5 more advanced SPL queries:
```
index=main | stats count by src_ip | sort -count
index=main | eval risk_score = if(status=="failure", 10, 1)
index=main | stats sum(risk_score) as total_risk by src_ip
index=main | where count > 5
index=main | stats count(eval(status="failure")) as failures by user
```

**Hour 3 — Documentation**

Add "Advanced SPL" section to `splunk-notes.md` documenting each query and result.

Commit:
```
git add .
git commit -m "Advanced SPL Queries Completed"
git push
```

**Deliverable**
A working "risk scoring" style SPL query — direct conceptual preparation for Week 11's rule-writing.

---

### DAY 62

**Goal**
Build a basic Splunk dashboard.

**Hour 1 — Core Concept**

Reading/video: Splunk dashboard basics — panels, visualizations, saving searches as dashboard panels.

**Hour 2 — Lab**

```
Create a new Dashboard: "Mini SOC Dashboard"
Add Panel 1: a table of "top 10 src_ip by failure count"
Add Panel 2: a timechart of events over time
Add Panel 3: a pie chart of event count by sourcetype
```

Save and screenshot the finished dashboard.

**Hour 3 — Documentation**

Add "My First Dashboard" section to `splunk-notes.md` with the dashboard screenshot and the SPL query behind each panel.

Commit:
```
git add .
git commit -m "First Splunk Dashboard Built"
git push
```

**Deliverable**
A working 3-panel Splunk dashboard — conceptual preview of the Wazuh dashboard you'll build in Week 10.

---

### DAY 63

**Goal**
Consolidate and review — Week 9 capstone.

**Hour 1 — Core Concept**

Re-read all Week 9 notes out loud, end to end.

**Hour 2 — Lab**

Self-test, live, without notes:
```
1. Explain Tier 1 vs Tier 2 vs Tier 3 out loud
2. Write an SPL query using stats and eval together, from scratch
3. Explain your Day 58 correlation rule design from memory
4. Build one new dashboard panel unaided
```

Redo any failed item before Week 10.

**Hour 3 — Documentation**

Create:
```
week-09-summary.md
```

Structure:
```
SOC concepts mastered
SPL queries I can write from memory
Correlation rule designed (linked)
Ready for: real SIEM deployment (Wazuh, Week 10)
```

Commit and push:
```
git add .
git commit -m "Week 9 Completed — SOC and SIEM Concepts Locked In"
git push
```

**Deliverable**
`week-09-summary.md` — your conceptual foundation is now solid enough to deploy a real SIEM.

---

## Week 10 — Deploying Wazuh SIEM

### Week 10 Overview

**Theme**
Concepts become real. This week you deploy Wazuh, connect it to the Windows and Linux hosts you built in Month 2, and get real telemetry flowing into a real dashboard.

**Week 10 Objectives**

```
✅ Deploy a Wazuh manager
✅ Install and register Wazuh agents on your Windows and Linux hosts
✅ Confirm Sysmon and auditd data are flowing into Wazuh
✅ Navigate the Wazuh dashboard confidently
✅ Understand Wazuh's default rule structure
```

**Success Criteria**

```
- Does the Wazuh dashboard show both your Windows and Linux agents as "Active"?
- Can you filter the dashboard by agent, rule level, and time range unaided?
- Can you find and explain one default Wazuh rule that's already firing in your lab?
```

**Week 10 Resources**

Documentation
```
- Wazuh official documentation (Installation guide, Agent enrollment)
- Wazuh ruleset reference (GitHub: wazuh/wazuh-ruleset)
```

Tools
```
A new Ubuntu Server VM (dedicated to the Wazuh manager, 4GB+ RAM recommended)
```

---

### DAY 64

**Goal**
Deploy the Wazuh manager.

**Hour 1 — Core Concept**

Reading/video: Wazuh architecture — Manager, Indexer, Dashboard, and Agents, and how they communicate.

**Hour 2 — Lab**

Provision a new Ubuntu VM (`192.168.50.40`) dedicated to Wazuh, then run the all-in-one installer per official docs:
```
curl -sO https://packages.wazuh.com/4.x/wazuh-install.sh
sudo bash wazuh-install.sh -a
```

Note the admin credentials the installer outputs at the end. Access the dashboard:
```
https://192.168.50.40
```

**Hour 3 — Documentation**

Create:
```
wazuh-lab-build.md
```

Document the install command used, the version installed, and a screenshot of the initial dashboard login.

Commit:
```
git add .
git commit -m "Wazuh Manager Deployed"
git push
```

**Deliverable**
A live Wazuh manager, accessible via HTTPS dashboard.

---

### DAY 65

**Goal**
Install the Wazuh agent on the Windows client.

**Hour 1 — Core Concept**

Reading/video: how Wazuh agents register with a manager (agent key, `ossec.conf`), and what "Active" vs "Disconnected" status means.

**Hour 2 — Lab**

On your Windows client:
```
Download the Wazuh Windows agent MSI from packages.wazuh.com
Install it, specifying the manager IP: 192.168.50.40
```

Start the agent:
```
NET START WazuhSvc
```

On the Wazuh dashboard, confirm the agent appears and shows "Active" status.

**Hour 3 — Documentation**

Add "Windows Agent Installation" section to `wazuh-lab-build.md` with the install steps and a screenshot of the agent showing Active in the dashboard.

Commit:
```
git add .
git commit -m "Wazuh Agent Installed on Windows Client"
git push
```

**Deliverable**
Windows client reporting into Wazuh as an Active agent.

---

### DAY 66

**Goal**
Configure Wazuh to ingest Sysmon logs specifically.

**Hour 1 — Core Concept**

Reading/video: Wazuh's Windows Event Log collection module, and how to add the Sysmon channel specifically (it's not collected by default).

**Hour 2 — Lab**

On the Windows client, edit the agent's `ossec.conf` to add:
```xml
<localfile>
  <location>Microsoft-Windows-Sysmon/Operational</location>
  <log_format>eventchannel</log_format>
</localfile>
```

Restart the agent:
```
NET STOP WazuhSvc
NET START WazuhSvc
```

Generate a test event (`notepad.exe` again) and confirm the corresponding Sysmon Event ID 1 appears in the Wazuh dashboard under that agent.

**Hour 3 — Documentation**

Add "Sysmon Ingestion" section to `wazuh-lab-build.md` with the config snippet and a screenshot of the Sysmon event appearing in Wazuh.

Commit:
```
git add .
git commit -m "Sysmon Logs Now Ingested into Wazuh"
git push
```

**Deliverable**
Verified Sysmon telemetry flowing into Wazuh — the single most important data source for Week 11's detection rules.

---

### DAY 67

**Goal**
Install the Wazuh agent on the Ubuntu (auditd) host.

**Hour 1 — Core Concept**

Reading/video: Wazuh's Linux agent installation and its default log collection modules (syslog, auditd integration).

**Hour 2 — Lab**

On your Ubuntu VM (from Month 2, with auditd already configured):
```
curl -so wazuh-agent.deb https://packages.wazuh.com/4.x/apt/pool/main/w/wazuh-agent/wazuh-agent_amd64.deb
sudo WAZUH_MANAGER='192.168.50.40' dpkg -i wazuh-agent.deb
sudo systemctl daemon-reload
sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent
```

Trigger your existing auditd rule from Month 2 (`/etc/passwd` watch) and confirm the event appears in the Wazuh dashboard.

**Hour 3 — Documentation**

Add "Linux Agent Installation" section to `wazuh-lab-build.md` with install commands and a screenshot of the auditd event appearing in Wazuh.

Commit:
```
git add .
git commit -m "Wazuh Agent Installed on Ubuntu with auditd Integration"
git push
```

**Deliverable**
Both Windows and Linux hosts now fully reporting into a single Wazuh dashboard.

---

### DAY 68

**Goal**
Navigate the Wazuh dashboard like an analyst.

**Hour 1 — Core Concept**

Reading/video: Wazuh dashboard modules — Security Events, Agents, Rule levels, and the underlying index structure.

**Hour 2 — Lab**

Practice filtering:
```
Filter by agent name (Windows client only)
Filter by rule level >= 5
Filter by a specific time range (last 15 minutes)
Filter by rule.description containing "sysmon"
```

For each filter, screenshot the result and note how many events matched.

**Hour 3 — Documentation**

Create:
```
wazuh-dashboard-notes.md
```

Document each filter used and what kind of investigation it would support.

Commit:
```
git add .
git commit -m "Wazuh Dashboard Navigation Practiced"
git push
```

**Deliverable**
`wazuh-dashboard-notes.md` — proof of practical, filter-based dashboard fluency.

---

### DAY 69

**Goal**
Understand Wazuh's default rule structure.

**Hour 1 — Core Concept**

Reading/video: Wazuh rule XML structure — rule ID, level, group, and `if_sid` (rule chaining).

**Hour 2 — Lab**

On the Wazuh manager:
```
ls /var/ossec/ruleset/rules/ | head -20
cat /var/ossec/ruleset/rules/0575-win-security_rules.xml | head -50
```

Identify 3 default rules that have already fired in your lab this week (cross-reference dashboard rule IDs against this file), and read their XML definitions.

**Hour 3 — Documentation**

Add "Default Rule Analysis" section to `wazuh-dashboard-notes.md`: for each of the 3 rules, note the rule ID, level, and what condition triggers it.

Commit:
```
git add .
git commit -m "Wazuh Default Rule Structure Analyzed"
git push
```

**Deliverable**
Documented breakdown of 3 real default rules already active in your environment — the exact syntax you'll reuse to write your own in Week 11.

---

### DAY 70

**Goal**
Consolidate and review — Week 10 capstone.

**Hour 1 — Core Concept**

Re-read all Week 10 documentation out loud, end to end.

**Hour 2 — Lab**

Self-test, live, without notes:
```
1. Confirm both agents are Active in the dashboard
2. Filter the dashboard by rule level >= 5 unaided
3. Locate the raw XML for one specific default rule on the manager
4. Explain, out loud, the path a log takes from Sysmon on the Windows client to appearing in the Wazuh dashboard
```

Fix any connectivity or ingestion gaps before Week 11 — detection rules can't be written against data that isn't flowing.

**Hour 3 — Documentation**

Create:
```
week-10-summary.md
```

Structure:
```
Wazuh architecture built (link to build doc)
Agents live: Windows + Linux
Data sources confirmed flowing: Sysmon, auditd
Ready for: custom detection rule writing (Week 11)
```

Commit and push:
```
git add .
git commit -m "Week 10 Completed — Wazuh SIEM Fully Live"
git push
```

**Deliverable**
A fully live, dual-agent Wazuh SIEM — your Crown Jewel's technical foundation is now built.

---

## Week 11 — Detection Engineering: Custom Rules and MITRE ATT&CK

### Week 11 Overview

**Theme**
Default rules only catch what the vendor anticipated. This week you write your own — each one deliberately mapped to a real adversary technique from MITRE ATT&CK, the framework every serious SOC uses to talk about threats.

**Week 11 Objectives**

```
✅ Understand MITRE ATT&CK structure (tactics, techniques, sub-techniques)
✅ Write 5 custom Wazuh detection rules
✅ Map each rule to a specific ATT&CK technique ID
✅ Understand false-positive tuning
✅ Build a "detection engineering notebook"
```

**Success Criteria**

```
- Can you explain the difference between a Tactic and a Technique in MITRE ATT&CK?
- Have you written 5 syntactically correct custom Wazuh rules?
- Can you explain why each rule's threshold/condition was chosen the way it was?
```

**Week 11 Resources**

Documentation
```
- attack.mitre.org
- Wazuh documentation: Custom rules and decoders
```

---

### DAY 71

**Goal**
Learn the MITRE ATT&CK framework structure.

**Hour 1 — Core Concept**

Reading/video: MITRE ATT&CK's matrix — Tactics (the "why," e.g., Initial Access) containing Techniques (the "how," e.g., T1110 Brute Force) containing Sub-techniques.

**Hour 2 — Lab**

Browse attack.mitre.org and select 5 techniques relevant to what your lab can actually generate telemetry for:
```
T1110 — Brute Force
T1059.001 — Command and Scripting Interpreter: PowerShell
T1053.005 — Scheduled Task/Job: Scheduled Task
T1204.002 — User Execution: Malicious File
T1098 — Account Manipulation
```

For each, write down: which Tactic it belongs to, and what log source in your lab could detect it.

**Hour 3 — Documentation**

Create:
```
detection-engineering-notebook.md
```

Document the 5 chosen techniques with their Tactic, description, and your planned detection log source.

Commit:
```
git add .
git commit -m "MITRE ATT&CK Techniques Selected for Detection"
git push
```

**Deliverable**
A documented plan mapping 5 real ATT&CK techniques to your lab's actual telemetry.

---

### DAY 72

**Goal**
Write custom rule #1 — Brute Force detection (T1110).

**Hour 1 — Core Concept**

Reading/video: Wazuh custom rule syntax — `<rule>`, `if_matched_sid`, `frequency`, `timeframe` for building a threshold-based rule.

**Hour 2 — Lab**

On the Wazuh manager, create/edit:
```
/var/ossec/etc/rules/local_rules.xml
```

```xml
<group name="local,brute_force,">
  <rule id="100010" level="10" frequency="5" timeframe="300" if_matched_sid="60122">
    <description>Multiple failed logon attempts - possible brute force (T1110)</description>
    <mitre>
      <id>T1110</id>
    </mitre>
  </rule>
</group>
```

(Adjust `if_matched_sid` to match the actual base rule ID your Windows 4625 events trigger — find this via the dashboard.)

Restart the manager and test:
```
sudo systemctl restart wazuh-manager
```

Trigger 5+ failed logons on the Windows client within 5 minutes and confirm rule 100010 fires.

**Hour 3 — Documentation**

Add "Rule #1 — Brute Force (T1110)" section to `detection-engineering-notebook.md` with the full rule XML and a screenshot of it firing.

Commit:
```
git add .
git commit -m "Custom Rule 1 - Brute Force Detection Completed"
git push
```

**Deliverable**
Your first working, MITRE-mapped custom detection rule.

---

### DAY 73

**Goal**
Write custom rule #2 — Suspicious PowerShell execution (T1059.001).

**Hour 1 — Core Concept**

Reading/video: detecting encoded/obfuscated PowerShell via Sysmon Event ID 1's command-line field, and Wazuh's `<field>` matching against specific event data.

**Hour 2 — Lab**

Add to `local_rules.xml`:
```xml
<rule id="100011" level="12">
  <if_sid>61603</if_sid>
  <field name="win.eventdata.commandLine" type="pcre2">(?i)-enc |-EncodedCommand|FromBase64String</field>
  <description>Suspicious encoded PowerShell command detected (T1059.001)</description>
  <mitre>
    <id>T1059.001</id>
  </mitre>
</rule>
```

(Adjust `if_sid` to match the actual base Sysmon Event ID 1 rule in your environment.)

Restart the manager and test by running an encoded PowerShell command on the Windows client:
```
powershell.exe -EncodedCommand SQBFAFgAKABJAFcAUgAoACcAaAB0AHQAcAA6AC8ALwBleGFtcGxlAC4AY29tACcAKQAp
```

Confirm rule 100011 fires.

**Hour 3 — Documentation**

Add "Rule #2 — Encoded PowerShell (T1059.001)" section to the notebook with rule XML and firing screenshot.

Commit:
```
git add .
git commit -m "Custom Rule 2 - Encoded PowerShell Detection Completed"
git push
```

**Deliverable**
A working rule that catches a genuinely common real-world attacker technique.

---

### DAY 74

**Goal**
Write custom rule #3 — Suspicious scheduled task creation (T1053.005).

**Hour 1 — Core Concept**

Reading/video: Sysmon Event ID 1 for `schtasks.exe` executions, and why attackers commonly abuse scheduled tasks for persistence.

**Hour 2 — Lab**

Add to `local_rules.xml`:
```xml
<rule id="100012" level="10">
  <if_sid>61603</if_sid>
  <field name="win.eventdata.image" type="pcre2">(?i)schtasks\.exe</field>
  <description>Scheduled task creation detected - possible persistence (T1053.005)</description>
  <mitre>
    <id>T1053.005</id>
  </mitre>
</rule>
```

Restart the manager and test:
```
schtasks /create /tn "TestPersistence" /tr "notepad.exe" /sc onlogon
```

Confirm rule 100012 fires, then clean up the test task:
```
schtasks /delete /tn "TestPersistence" /f
```

**Hour 3 — Documentation**

Add "Rule #3 — Scheduled Task Persistence (T1053.005)" section to the notebook.

Commit:
```
git add .
git commit -m "Custom Rule 3 - Scheduled Task Detection Completed"
git push
```

**Deliverable**
A working persistence-detection rule, plus proof you clean up your own test artifacts responsibly.

---

### DAY 75

**Goal**
Write custom rule #4 — Suspicious process from Office application (T1204.002).

**Hour 1 — Core Concept**

Reading/video: parent-child process relationships in Sysmon (`ParentImage`/`Image` fields), and why `winword.exe` or `excel.exe` spawning `powershell.exe`/`cmd.exe` is a classic malicious-macro indicator.

**Hour 2 — Lab**

Add to `local_rules.xml`:
```xml
<rule id="100013" level="12">
  <if_sid>61603</if_sid>
  <field name="win.eventdata.parentImage" type="pcre2">(?i)winword\.exe|excel\.exe</field>
  <field name="win.eventdata.image" type="pcre2">(?i)powershell\.exe|cmd\.exe</field>
  <description>Office application spawned a shell - possible malicious macro (T1204.002)</description>
  <mitre>
    <id>T1204.002</id>
  </mitre>
</rule>
```

Test by manually simulating the parent-child relationship (since building a real malicious macro is out of scope): open `winword.exe`, then from Task Manager's "Run new task" spawn `cmd.exe` with Word as context if your test setup allows, or note this rule as logic-verified via manual XML/event review if a live trigger isn't safely reproducible in your lab.

**Hour 3 — Documentation**

Add "Rule #4 — Office Spawning Shell (T1204.002)" section to the notebook, being explicit about how it was tested/verified.

Commit:
```
git add .
git commit -m "Custom Rule 4 - Office Macro Shell Detection Completed"
git push
```

**Deliverable**
A rule targeting one of the most common real-world initial-access patterns, with honest documentation of your testing method.

---

### DAY 76

**Goal**
Write custom rule #5 — Privileged group membership change (T1098).

**Hour 1 — Core Concept**

Reading/video: Windows Event ID 4728/4732 (member added to a security-enabled group) and why attackers add accounts to Domain Admins for persistence.

**Hour 2 — Lab**

Add to `local_rules.xml`:
```xml
<rule id="100014" level="12">
  <if_sid>60122</if_sid>
  <match>4728|4732</match>
  <description>User added to a privileged security group (T1098)</description>
  <mitre>
    <id>T1098</id>
  </mitre>
</rule>
```

Test on DC01:
```
Add-ADGroupMember -Identity "Domain Admins" -Members "bob"
```

Confirm rule 100014 fires, then immediately revert:
```
Remove-ADGroupMember -Identity "Domain Admins" -Members "bob" -Confirm:$false
```

**Hour 3 — Documentation**

Add "Rule #5 — Privileged Group Change (T1098)" section to the notebook.

Commit:
```
git add .
git commit -m "Custom Rule 5 - Privileged Group Membership Detection Completed"
git push
```

**Deliverable**
5 complete, MITRE-mapped custom detection rules, all written this week.

---

### DAY 77

**Goal**
Consolidate and review — Week 11 capstone.

**Hour 1 — Core Concept**

Re-read all 5 rules and their MITRE mappings out loud, explaining the logic of each XML block from memory.

**Hour 2 — Lab**

Self-test, live, without notes:
```
1. Explain if_sid, field, and frequency/timeframe in Wazuh rule syntax
2. Pick a 6th MITRE technique and sketch (on paper) what a rule for it might look like
3. Re-trigger 2 of your 5 rules from scratch and confirm they still fire correctly
```

Fix any rule that no longer fires correctly (rules can break after a manager restart if XML syntax has a subtle error) before Week 12.

**Hour 3 — Documentation**

Create:
```
week-11-summary.md
```

Structure:
```
5 custom rules built (linked to notebook)
MITRE techniques covered
What tuning I'd still want to do
Ready for: Atomic Red Team validation (Week 12)
```

Commit and push:
```
git add .
git commit -m "Week 11 Completed — Detection Engineering Rules Built"
git push
```

**Deliverable**
5 documented, MITRE-mapped, manually-tested detection rules — ready for formal validation next week.

---

## Week 12 — Atomic Red Team Validation (Crown Jewel Week)

### Week 12 Overview

**Theme**
A detection rule you haven't formally validated is a guess, not a control. This week you use Atomic Red Team — the industry-standard adversary emulation framework — to prove each of your 5 rules actually works, then assemble the Month 3 Crown Jewel.

**Week 12 Objectives**

```
✅ Install and safely run Atomic Red Team tests
✅ Validate all 5 custom rules against real atomic tests
✅ Document each validation with rule logic + atomic test + alert evidence
✅ Publish the Month 3 Crown Jewel repository
```

**Success Criteria**

```
- Do all 5 rules fire correctly when their corresponding atomic test is executed?
- Is each validation documented with a screenshot of the actual Wazuh alert?
- Is the Crown Jewel repository published with an architecture diagram, all 5 validated rules, and dashboard screenshots?
```

**Week 12 Resources**

Documentation
```
- Atomic Red Team (GitHub: redcanaryco/atomic-red-team)
- Invoke-AtomicRedTeam PowerShell module documentation
```

---

### DAY 78

**Goal**
Install Atomic Red Team safely in the lab.

**Hour 1 — Core Concept**

Reading/video: what Atomic Red Team actually does — small, discrete, documented "atomic tests" that simulate one specific technique's behavior, safely and reversibly, for detection validation.

**Hour 2 — Lab**

On the Windows client (never on a production or internet-facing machine):
```powershell
IEX (IWR 'https://raw.githubusercontent.com/redcanaryco/invoke-atomicredteam/master/install-atomicredteam.ps1' -UseBasicParsing)
Install-AtomicRedTeam -getAtomics
```

Verify installation:
```powershell
Import-Module "C:\AtomicRedTeam\invoke-atomicredteam\Invoke-AtomicRedTeam.psd1" -Force
Invoke-AtomicTest T1082 -ShowDetailsBrief
```

**Hour 3 — Documentation**

Create:
```
atomic-validation-report.md
```

Document the install process and the safety principle you're following (lab-only, documented, reversible tests).

Commit:
```
git add .
git commit -m "Atomic Red Team Installed"
git push
```

**Deliverable**
A working Atomic Red Team installation, ready to validate your rules.

---

### DAY 79

**Goal**
Validate Rule #1 (Brute Force, T1110).

**Hour 1 — Core Concept**

Reading/video: reviewing the specific atomic test for T1110 and what it actually executes before you run it (never run a test you haven't read).

**Hour 2 — Lab**

```powershell
Invoke-AtomicTest T1110 -ShowDetailsBrief
Invoke-AtomicTest T1110
```

If the specific atomic test doesn't perfectly match your rule's exact trigger condition, supplement with your manual test method from Day 72 (repeated failed logons) to confirm firing.

Check the Wazuh dashboard and confirm rule 100010 fired with a timestamp matching your test execution.

**Hour 3 — Documentation**

Add "Validation — Rule #1 (T1110)" section to `atomic-validation-report.md`:
```
Atomic test used:
Command executed:
Wazuh alert screenshot:
Result: PASS / FAIL (with notes)
```

Commit:
```
git add .
git commit -m "Rule 1 Validated via Atomic Red Team"
git push
```

**Deliverable**
Formal validation evidence for your brute-force detection rule.

---

### DAY 80

**Goal**
Validate Rule #2 (Encoded PowerShell, T1059.001).

**Hour 1 — Core Concept**

Reading/video: review the T1059.001 atomic test details before running.

**Hour 2 — Lab**

```powershell
Invoke-AtomicTest T1059.001 -ShowDetailsBrief
Invoke-AtomicTest T1059.001
```

Check the Wazuh dashboard for rule 100011 firing on the exact command executed by the atomic test.

**Hour 3 — Documentation**

Add "Validation — Rule #2 (T1059.001)" section to the report with the same structure as Day 79.

Commit:
```
git add .
git commit -m "Rule 2 Validated via Atomic Red Team"
git push
```

**Deliverable**
Formal validation evidence for your encoded PowerShell detection rule.

---

### DAY 81

**Goal**
Validate Rule #3 (Scheduled Task, T1053.005).

**Hour 1 — Core Concept**

Reading/video: review the T1053.005 atomic test details before running.

**Hour 2 — Lab**

```powershell
Invoke-AtomicTest T1053.005 -ShowDetailsBrief
Invoke-AtomicTest T1053.005
```

Confirm rule 100012 fires in Wazuh, then run the test's built-in cleanup:
```powershell
Invoke-AtomicTest T1053.005 -Cleanup
```

**Hour 3 — Documentation**

Add "Validation — Rule #3 (T1053.005)" section to the report, including confirmation that cleanup was run.

Commit:
```
git add .
git commit -m "Rule 3 Validated via Atomic Red Team"
git push
```

**Deliverable**
Formal validation evidence for your persistence detection rule.

---

### DAY 82

**Goal**
Validate Rules #4 and #5 (T1204.002, T1098).

**Hour 1 — Core Concept**

Reading/video: review both remaining atomic tests. Note that T1204.002 (malicious file execution) may need a manual, controlled simulation rather than a direct atomic test, since real malicious macros are out of scope — document this honestly.

**Hour 2 — Lab**

For T1098:
```powershell
Invoke-AtomicTest T1098 -ShowDetailsBrief
Invoke-AtomicTest T1098
```
Confirm rule 100014 fires, then run cleanup:
```powershell
Invoke-AtomicTest T1098 -Cleanup
```

For T1204.002, re-run your Day 75 manual verification method and re-confirm rule 100013 still fires correctly.

**Hour 3 — Documentation**

Add "Validation — Rule #4 (T1204.002)" and "Validation — Rule #5 (T1098)" sections to the report, being explicit about atomic-test-based vs manually-verified methodology for each.

Commit:
```
git add .
git commit -m "Rules 4 and 5 Validated"
git push
```

**Deliverable**
All 5 rules now formally validated, with honest documentation of exactly how each was tested.

---

### DAY 83

**Goal**
Write the full detection engineering report.

**Hour 1 — Core Concept**

Reading/video: none — instead, review how real detection engineering teams document rule coverage (a "detection matrix" mapping rules to techniques to validation status).

**Hour 2 — Lab**

Build a summary detection matrix table:
```
Rule ID | Description | MITRE Technique | Validation Method | Status
100010  | Brute Force | T1110           | Atomic Red Team   | PASS
100011  | Encoded PS  | T1059.001       | Atomic Red Team   | PASS
100012  | Sched Task  | T1053.005       | Atomic Red Team   | PASS
100013  | Office Shell| T1204.002       | Manual Simulation | PASS
100014  | Priv Group  | T1098           | Atomic Red Team   | PASS
```

Take final, clean screenshots of the Wazuh dashboard showing all 5 rules having fired historically (filter by rule ID range 100010-100014).

**Hour 3 — Documentation**

Finalize `atomic-validation-report.md` with the detection matrix table at the top, followed by the detailed per-rule sections already written.

Commit:
```
git add .
git commit -m "Detection Engineering Report Finalized"
git push
```

**Deliverable**
A complete, professional detection engineering report with a clean summary matrix — exactly the kind of document a detection engineer produces at a real job.

---

### DAY 84

**Goal**
Assemble and publish the Month 3 Crown Jewel — Crown Jewel Day.

**Hour 1 — Core Concept**

Re-read your entire Month 3 journey (Weeks 9–12) out loud, end to end.

**Hour 2 — Lab**

Assemble the final repository structure:
```
wazuh-detection-lab/
├── README.md
├── wazuh-lab-build.md
├── wazuh-dashboard-notes.md
├── detection-engineering-notebook.md
├── atomic-validation-report.md
├── rules/
│   └── local_rules.xml
└── screenshots/
    ├── dashboard-overview.png
    └── rule-100010-through-100014-firing.png
```

Run a final live self-test covering all of Month 3, unaided:
```
1. Explain the path of a log from Sysmon to a fired Wazuh alert, end to end
2. Explain what "if_sid" chaining means in Wazuh rule syntax
3. Pick any one of your 5 rules and explain its MITRE mapping and validation method from memory
4. Explain why an unvalidated detection rule is a liability, not an asset
```

**Hour 3 — Documentation**

Write the master `README.md`:
```
# Wazuh Detection Engineering Lab

## What this repo demonstrates
- A fully deployed Wazuh SIEM ingesting Windows Sysmon and Linux auditd telemetry
- 5 custom detection rules, each mapped to a specific MITRE ATT&CK technique
- Formal validation of every rule using Atomic Red Team (or documented manual methodology)
- A detection engineering report with a full coverage matrix

## Structure
(explain folders)

## Skills demonstrated
(SIEM deployment, detection rule authoring, MITRE ATT&CK mapping, adversary emulation/validation, technical report writing)
```

Final commit and push:
```
git add .
git commit -m "Month 3 Completed — Crown Jewel Published"
git push
```

**Deliverable**
A fully published `wazuh-detection-lab` repository — **Month 3 is complete**, and you now have a genuinely rare-for-entry-level artifact: validated detection engineering work.

---

*End of Chapter 3. Chapter 4 (Month 4 — Incident Response, Phishing Analysis, and Threat Intelligence) continues in the same format.*
