# Zero-to-Hired Cybersecurity Roadmap (Version 2026)
### A Complete 6-Month Handbook

---

# Chapter 2 — Month 2: System Administration, Active Directory, and Security Scripting

Theme of the month: **You stop being a visitor in Windows and Linux and become the administrator who knows exactly where the evidence lives.**
This month you build a real Active Directory domain, configure it to log what matters, and write the scripts that turn raw logs into answers.

---

## Week 5 — Building a Real Active Directory Lab

### Week 5 Overview

**Theme**
You diagrammed Active Directory in Month 1. Now you build it — a real Domain Controller, real domain-joined clients, real users. This is the infrastructure every remaining month depends on.

**Week 5 Objectives**

```
✅ Install Windows Server and promote it to a Domain Controller
✅ Create a domain, OUs, and test user accounts
✅ Join Windows and Linux clients to the domain
✅ Verify domain authentication end-to-end
✅ Document the full build as a repeatable guide
```

**Success Criteria**

```
- Is your Domain Controller live and resolving DNS for its own domain?
- Can you log in to a client machine using a domain account?
- Can you explain, unaided, what "promoting a server to a DC" actually changes?
- Could a stranger follow your README and rebuild this lab from scratch?
```

**Week 5 Resources**

Primary Platform
```
TryHackMe (Free)
Rooms:
- Intro to Active Directory (review/reinforce)
- Windows Fundamentals 3 (reinforce services)
```

Documentation
```
- Microsoft Learn: Install Active Directory Domain Services
- Microsoft Learn: DNS Server role
```

Tools
```
Windows Server evaluation ISO (Microsoft Evaluation Center)
Windows 10/11 evaluation VM
```

---

### DAY 29

**Goal**
Install Windows Server and prepare it for the AD DS role.

**Hour 1 — Core Concept**

Reading/video: what the AD DS role actually installs, and why DNS is a hard dependency.

Topics:
```
Windows Server editions (Standard vs Datacenter — doesn't matter for a lab)
Roles vs Features in Server Manager
Why AD DS requires DNS
```

**Hour 2 — Lab**

```
Download Windows Server Evaluation ISO
Create a new VM: 4GB RAM minimum, 60GB disk, attach to your CyberLabNet internal network
Install Windows Server, set a strong local Administrator password
Set a static IP: 192.168.50.5
Rename the server: DC01
```

Verify:
```
Get-NetIPAddress
hostname
```

**Hour 3 — Documentation**

Create:
```
ad-lab-build-guide.md
```

Start documenting step-by-step, screenshot-by-screenshot, as if a stranger will follow it:
```
## Step 1 — Server Provisioning
- VM specs used
- Static IP configuration
- Hostname set
```

Commit:
```
git add .
git commit -m "Windows Server Provisioned as DC01"
git push
```

**Deliverable**
`DC01` server live on the lab network with static IP `192.168.50.5`.

---

### DAY 30

**Goal**
Install AD DS and DNS roles, promote to Domain Controller.

**Hour 1 — Core Concept**

Reading/video: the "promotion" process — what changes on disk (SYSVOL, NTDS.dit) and in memory when a server becomes a DC.

**Hour 2 — Lab**

In Server Manager:
```
Add Roles and Features > Active Directory Domain Services > Install
Add Roles and Features > DNS Server > Install
```

Promote to Domain Controller:
```
Promote this server to a domain controller
Add a new forest
Root domain name: corp.local
Set DSRM password
Complete the wizard, allow reboot
```

Verify after reboot:
```
Get-ADDomain
Get-ADForest
nslookup corp.local
```

**Hour 3 — Documentation**

Add "Step 2 — Domain Promotion" section to `ad-lab-build-guide.md` with the exact settings used and verification command outputs.

Commit:
```
git add .
git commit -m "DC01 Promoted to Domain Controller for corp.local"
git push
```

**Deliverable**
A live `corp.local` domain with `DC01` as its Domain Controller, verified via `Get-ADDomain`.

---

### DAY 31

**Goal**
Create Organizational Units and test users.

**Hour 1 — Core Concept**

Reading/video: OU design principles — why organizations split by department/function, and how OUs enable targeted GPOs later.

**Hour 2 — Lab**

Using Active Directory Users and Computers (`dsa.msc`) or PowerShell:
```
New-ADOrganizationalUnit -Name "IT" -Path "DC=corp,DC=local"
New-ADOrganizationalUnit -Name "Sales" -Path "DC=corp,DC=local"

New-ADUser -Name "Alice IT" -SamAccountName "alice" -Path "OU=IT,DC=corp,DC=local" -AccountPassword (ConvertTo-SecureString "P@ssw0rd123!" -AsPlainText -Force) -Enabled $true
New-ADUser -Name "Bob Sales" -SamAccountName "bob" -Path "OU=Sales,DC=corp,DC=local" -AccountPassword (ConvertTo-SecureString "P@ssw0rd123!" -AsPlainText -Force) -Enabled $true
New-ADUser -Name "Carol Admin" -SamAccountName "carol" -Path "OU=IT,DC=corp,DC=local" -AccountPassword (ConvertTo-SecureString "P@ssw0rd123!" -AsPlainText -Force) -Enabled $true
```

Verify:
```
Get-ADUser -Filter * | Select-Object Name, SamAccountName, DistinguishedName
```

**Hour 3 — Documentation**

Add "Step 3 — OUs and Users" section to `ad-lab-build-guide.md` with the exact commands and a screenshot of ADUC showing the structure.

Commit:
```
git add .
git commit -m "OUs and Test Users Created"
git push
```

**Deliverable**
2 OUs (IT, Sales) and 3 users, verified via `Get-ADUser -Filter *`.

---

### DAY 32

**Goal**
Join a Windows client to the domain.

**Hour 1 — Core Concept**

Reading/video: what happens technically when a machine "joins" a domain (computer account creation, secure channel trust).

**Hour 2 — Lab**

On your Windows 10/11 client VM:
```
Set DNS server to 192.168.50.5 (point it at DC01)
Set static IP in the CyberLabNet range, e.g. 192.168.50.21
```

Join the domain:
```
System Properties > Change > Member of: Domain > corp.local
Authenticate with Administrator credentials from corp.local
Reboot
```

Verify from the client:
```
whoami
whoami /all
```

Verify from DC01:
```
Get-ADComputer -Filter *
```

**Hour 3 — Documentation**

Add "Step 4 — Domain-Joining a Windows Client" section to `ad-lab-build-guide.md` with DNS settings used and verification output.

Commit:
```
git add .
git commit -m "Windows Client Joined to corp.local"
git push
```

**Deliverable**
A domain-joined Windows client, confirmed via `Get-ADComputer -Filter *` on the DC.

---

### DAY 33

**Goal**
Log in as a domain user and verify authentication end-to-end.

**Hour 1 — Core Concept**

Reading/video: Kerberos ticket issuance in practice — connecting your Day 20 diagram to a real login.

**Hour 2 — Lab**

On the domain-joined client:
```
Log out of the local account
Log in as: corp\alice (password: P@ssw0rd123!)
```

Once logged in as `alice`:
```
whoami /all
klist
```

Confirm a Kerberos ticket was actually issued (look for `krbtgt/CORP.LOCAL` in `klist` output).

**Hour 3 — Documentation**

Add "Step 5 — Domain Authentication Verified" section to `ad-lab-build-guide.md` with your `klist` output and a short explanation of what the ticket proves.

Commit:
```
git add .
git commit -m "Domain Authentication Verified via Kerberos"
git push
```

**Deliverable**
Screenshot of a successful domain logon as `alice` with a valid Kerberos ticket in `klist`.

---

### DAY 34

**Goal**
Attempt Linux domain integration (or document the limitation).

**Hour 1 — Core Concept**

Reading/video: how Linux can join AD via `realmd`/`sssd`, and why this is optional for a SOC-focused lab (many real environments keep Linux hosts standalone, feeding logs to a SIEM instead).

**Hour 2 — Lab**

On your Ubuntu VM, attempt:
```
sudo apt install realmd sssd sssd-tools libnss-sss libpam-sss adcli samba-common-bin -y
sudo realm discover corp.local
sudo realm join corp.local -U administrator
```

If successful, verify:
```
realm list
```

If unsuccessful (common in lab environments due to time sync/DNS quirks), troubleshoot once, then explicitly decide: keep Ubuntu standalone and note this as an intentional design decision, not a failure.

**Hour 3 — Documentation**

Add "Step 6 — Linux Integration Decision" section to `ad-lab-build-guide.md`:
```
Outcome: joined / standalone (with reason)
If standalone: how Ubuntu will still contribute logs (via Wazuh agent in Month 3)
```

Commit:
```
git add .
git commit -m "Linux Domain Integration Attempted and Documented"
git push
```

**Deliverable**
A clear, honest architectural decision documented — this is exactly the kind of judgment call a hiring manager respects seeing explained.

---

### DAY 35

**Goal**
Consolidate and review — Week 5 capstone.

**Hour 1 — Core Concept**

Re-read the entire `ad-lab-build-guide.md` out loud, end to end, as if presenting it to a colleague.

**Hour 2 — Lab**

Self-test, live, without notes:
```
1. Explain what changes on a server during "dcpromo" (AD DS promotion)
2. Create one more OU and one more user, unaided
3. Log in as a different domain user on the client and verify with klist
4. Explain the difference between a Domain, an OU, and a GPO out loud
```

Fix any gaps in your build before Week 6 (which depends on this lab being fully stable).

**Hour 3 — Documentation**

Create:
```
week-05-summary.md
```

Structure:
```
AD lab architecture (link to build guide + diagram)
What's live and verified
What I'd do differently if rebuilding this from scratch
```

Commit and push:
```
git add .
git commit -m "Week 5 Completed — Active Directory Lab Live"
git push
```

**Deliverable**
A fully live, documented AD lab: 1 DC, 2 OUs, 3+ users, 1 domain-joined client, verified authentication.

---

## Week 6 — Group Policy, Auditing, and Defensive Configuration

### Week 6 Overview

**Theme**
An AD lab with no logging is invisible to a SOC. This week you turn on the audit policies and Sysmon configuration that make Month 3's SIEM work possible at all.

**Week 6 Objectives**

```
✅ Understand and configure GPOs relevant to security (not general admin GPOs)
✅ Enable and verify Windows audit policies
✅ Deploy Sysmon with a well-known community configuration
✅ Configure Linux auditd with a real watch rule
✅ Correlate configuration changes to specific Event IDs
```

**Success Criteria**

```
- Does a deliberate failed logon produce a 4625 event you can find in under 30 seconds?
- Is Sysmon installed and logging process creation events (Event ID 1)?
- Is auditd watching a real file and logging access attempts?
- Can you explain what GPO inheritance means and how enforcement overrides it?
```

**Week 6 Resources**

Primary Platform
```
TryHochMe/TryHackMe (Free) — reinforcement rooms as needed on Windows event logging
```

Documentation
```
- Microsoft Learn: Group Policy overview
- Microsoft Learn: Advanced security audit policies
- SwiftOnSecurity Sysmon config (GitHub)
- Linux auditd man pages (man auditd, man auditctl)
```

---

### DAY 36

**Goal**
GPO structure, inheritance, and your first real GPO.

**Hour 1 — Core Concept**

Reading/video: GPO processing order (Local > Site > Domain > OU), inheritance, and the "Enforced" and "Block Inheritance" settings.

**Hour 2 — Lab**

On DC01, open Group Policy Management (`gpmc.msc`):
```
Create a new GPO: "Password Policy - IT"
Link it to the IT OU
Edit: Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Password Policy
  - Minimum password length: 12
  - Enforce password history: 10
  - Password must meet complexity requirements: Enabled
```

On the domain-joined client:
```
gpupdate /force
gpresult /r
```

**Hour 3 — Documentation**

Create:
```
gpo-audit-configuration.md
```

Document the GPO created, its settings, and the `gpresult /r` output proving it applied.

Commit:
```
git add .
git commit -m "First Security GPO Created and Applied"
git push
```

**Deliverable**
A working password policy GPO, confirmed applied via `gpresult /r`.

---

### DAY 37

**Goal**
Enable Windows audit policy for logon events.

**Hour 1 — Core Concept**

Reading/video: the difference between basic Audit Policy and Advanced Audit Policy Configuration, and why 4624/4625 specifically matter to a SOC analyst.

**Hour 2 — Lab**

Create a second GPO:
```
Create GPO: "Audit Policy - Domain"
Link it to the Domain (corp.local) root, so it applies everywhere
Edit: Computer Configuration > Policies > Windows Settings > Security Settings > Advanced Audit Policy Configuration > Logon/Logoff
  - Audit Logon: Success and Failure
  - Audit Account Lockout: Success and Failure
```

Apply and test:
```
gpupdate /force   (run on DC01 and client)
```

Deliberately fail a logon on the client (wrong password 1x), then log in correctly. On DC01, open Event Viewer > Security log, filter for Event ID 4625 and 4624, confirm both appear.

**Hour 3 — Documentation**

Add to `gpo-audit-configuration.md`: the audit GPO settings, and screenshots of both the 4624 and 4625 events you generated.

Commit:
```
git add .
git commit -m "Domain-Wide Logon Auditing Enabled"
git push
```

**Deliverable**
Verified 4624 and 4625 events, domain-wide, enforced via GPO rather than local settings.

---

### DAY 38

**Goal**
Deploy Sysmon on the Windows client.

**Hour 1 — Core Concept**

Reading/video: what Sysmon adds beyond native Windows logging — process creation with full command line, network connections, and file creation events.

**Hour 2 — Lab**

```
Download Sysmon (Microsoft Sysinternals)
Download the SwiftOnSecurity sysmonconfig-export.xml from GitHub
```

Install with the config:
```
sysmon64.exe -accepteula -i sysmonconfig-export.xml
```

Verify:
```
Get-Service Sysmon64
Open Event Viewer > Applications and Services Logs > Microsoft > Windows > Sysmon > Operational
```

Generate a test event:
```
notepad.exe    (then close it)
```
Find the corresponding Sysmon Event ID 1 (Process Creation) for `notepad.exe`.

**Hour 3 — Documentation**

Create:
```
sysmon-deployment.md
```

Document the install command, config source (with link/attribution), and a screenshot of the `notepad.exe` Event ID 1 entry with the full command-line field visible.

Commit:
```
git add .
git commit -m "Sysmon Deployed with SwiftOnSecurity Config"
git push
```

**Deliverable**
Sysmon live and logging, with a verified Event ID 1 capture — this feeds directly into Month 3's Wazuh lab.

---

### DAY 39

**Goal**
Linux auditd configuration.

**Hour 1 — Core Concept**

Reading/video: auditd architecture — the audit daemon, rules, and `ausearch`/`aureport` for querying results.

**Hour 2 — Lab**

On Ubuntu:
```
sudo apt install auditd audispd-plugins -y
sudo systemctl enable auditd
sudo systemctl start auditd
```

Add a watch rule on a sensitive file:
```
sudo auditctl -w /etc/passwd -p wa -k passwd_changes
```

Trigger it:
```
sudo cat /etc/passwd >> /dev/null
echo "test" | sudo tee -a /etc/passwd_test_file
```

Query the results:
```
sudo ausearch -k passwd_changes
sudo aureport -f
```

**Hour 3 — Documentation**

Create:
```
auditd-configuration.md
```

Document the rule added, the trigger action, and the `ausearch`/`aureport` output.

Commit:
```
git add .
git commit -m "Linux auditd Watch Rule Configured and Verified"
git push
```

**Deliverable**
A working auditd rule on `/etc/passwd` with verified log output — the Linux equivalent of your Sysmon deployment.

---

### DAY 40

**Goal**
GPO enforcement and inheritance testing.

**Hour 1 — Core Concept**

Reading/video: "Block Inheritance" and "Enforced" GPO settings — when a lower-level OU setting overrides a higher one, and when it can't.

**Hour 2 — Lab**

Create a conflicting test GPO:
```
Create GPO: "Sales - Relaxed Password (TEST ONLY)"
Link it to the Sales OU
Set Minimum password length: 6   (deliberately weaker, for the exercise)
```

Run `gpresult /r` on a client in the Sales OU and observe which policy wins based on link order/inheritance.
Then set "Enforced" on the domain-wide "Audit Policy - Domain" GPO and re-test to confirm enforcement behavior.

Delete the deliberately weak test GPO once the exercise is complete — never leave a real password-weakening policy active in your lab.

**Hour 3 — Documentation**

Add "GPO Inheritance & Enforcement Test" section to `gpo-audit-configuration.md` explaining what you observed and why, including the `gpresult /r` evidence.

Commit:
```
git add .
git commit -m "GPO Inheritance and Enforcement Tested"
git push
```

**Deliverable**
Documented proof that you understand — and can demonstrate — how GPO precedence actually resolves in practice.

---

### DAY 41

**Goal**
Correlate configuration to detection — a mini investigation.

**Hour 1 — Core Concept**

Reading/video: how a SOC analyst reads a chain of events (login attempt → process creation → file access) as a single story rather than isolated log lines.

**Hour 2 — Lab**

Simulate a small "suspicious" sequence on the Windows client:
```
1. Fail a domain logon 2 times, then succeed
2. Immediately open PowerShell and run: Get-Process | Out-File C:\Users\alice\processlist.txt
3. Open the resulting file in Notepad
```

On DC01/client, find and screenshot the full evidence chain:
```
Event ID 4625 x2, then 4624 (Security log)
Sysmon Event ID 1 for powershell.exe with the full command line
Sysmon Event ID 11 (File Create) for processlist.txt
```

**Hour 3 — Documentation**

Create:
```
mini-investigation-01.md
```

Structure it like a real analyst note:
```
Trigger: (what you did)
Evidence found: (each Event ID, with screenshot)
Narrative: (the story the logs tell, in order)
```

Commit:
```
git add .
git commit -m "Mini Investigation - Correlated Event Chain Documented"
git push
```

**Deliverable**
Your first true "investigation" artifact — this is a direct preview of Month 4's incident response work.

---

### DAY 42

**Goal**
Consolidate and review — Week 6 capstone.

**Hour 1 — Core Concept**

Re-read all Week 6 documentation out loud, end to end.

**Hour 2 — Lab**

Self-test, live, without notes:
```
1. Create a new GPO and link it to an OU, unaided
2. Trigger a 4625 event and find it in under 30 seconds
3. Trigger a Sysmon Event ID 1 and explain what field shows the full command line
4. Add a new auditd watch rule on a different file and verify it fires
```

Redo any failed item before Week 7.

**Hour 3 — Documentation**

Create:
```
week-06-summary.md
```

Structure:
```
Auditing/logging now live: (list of Event IDs and sources)
GPOs created this week
Mini-investigation linked
What this enables for Month 3
```

Commit and push:
```
git add .
git commit -m "Week 6 Completed — Lab Fully Instrumented for Detection"
git push
```

**Deliverable**
A fully audited, logged AD + Linux lab — the exact telemetry foundation Month 3's Wazuh SIEM will ingest.

---

## Week 7 — PowerShell for Security Automation

### Week 7 Overview

**Theme**
Clicking through Event Viewer doesn't scale. This week you learn to query, filter, and export security data programmatically — the exact skill that separates a Tier 1 analyst who "looks around" from one who builds repeatable tools.

**Week 7 Objectives**

```
✅ Query Windows Event Logs precisely with Get-WinEvent
✅ Export structured security data to CSV
✅ Use PowerShell remoting across your lab
✅ Automate a recurring security script with Task Scheduler
✅ Add error handling to make scripts production-usable
```

**Success Criteria**

```
- Can you pull all 4625 events from the last 24 hours using Get-WinEvent, unaided?
- Can you export that data to a clean CSV with only the fields that matter?
- Does your script run automatically on a schedule and produce a usable output file?
- Does your script handle an error (e.g., missing log) without crashing silently?
```

**Week 7 Resources**

Documentation
```
- Microsoft Learn: Get-WinEvent
- ss64.com/ps — PowerShell reference
- Microsoft Learn: PowerShell Remoting overview
```

---

### DAY 43

**Goal**
Master `Get-WinEvent` and XPath-style filtering.

**Hour 1 — Core Concept**

Reading/video: `Get-WinEvent` vs the older `Get-EventLog`, and using `-FilterHashtable` for fast, precise queries.

**Hour 2 — Lab**

```
Get-WinEvent -LogName Security -MaxEvents 20
Get-WinEvent -FilterHashtable @{LogName='Security'; Id=4625} -MaxEvents 20
Get-WinEvent -FilterHashtable @{LogName='Security'; Id=4625; StartTime=(Get-Date).AddHours(-24)}
```

Generate a few more test failed logons, then re-run the last command and confirm they appear.

**Hour 3 — Documentation**

Create:
```
scripts/powershell/get-winevent-notes.md
```

Document each query used, what it returns, and when you'd use `-FilterHashtable` vs simpler cmdlets.

Commit:
```
git add .
git commit -m "Get-WinEvent Filtering Mastered"
git push
```

**Deliverable**
Documented, working `Get-WinEvent` queries filtered by log, ID, and time window.

---

### DAY 44

**Goal**
Build the failed-logon extraction script (v1).

**Hour 1 — Core Concept**

Reading/video: parsing Event properties (`.Properties[index].Value`) to extract structured fields like username and source IP from a 4625 event.

**Hour 2 — Lab**

Create:
```
scripts/powershell/Get-FailedLogons.ps1
```

```
$events = Get-WinEvent -FilterHashtable @{LogName='Security'; Id=4625; StartTime=(Get-Date).AddHours(-24)}

foreach ($event in $events) {
    [PSCustomObject]@{
        Time      = $event.TimeCreated
        Username  = $event.Properties[5].Value
        SourceIP  = $event.Properties[19].Value
    }
}
```

Run it:
```
.\Get-FailedLogons.ps1
```

Adjust property indexes if your output doesn't match expectations (event property indexes can shift slightly between Windows versions — this troubleshooting is itself a real skill).

**Hour 3 — Documentation**

Update `scripts/powershell/get-winevent-notes.md` with the script, sample output, and how you diagnosed the correct property indexes.

Commit:
```
git add .
git commit -m "Get-FailedLogons Script v1 Completed"
git push
```

**Deliverable**
`Get-FailedLogons.ps1` — a working script that extracts structured failed-logon data.

---

### DAY 45

**Goal**
Export to CSV and add aggregation.

**Hour 1 — Core Concept**

Reading/video: `Export-Csv`, `Group-Object`, and `Sort-Object` for turning raw events into an analyst-ready summary.

**Hour 2 — Lab**

Extend the script:
```
$events = Get-WinEvent -FilterHashtable @{LogName='Security'; Id=4625; StartTime=(Get-Date).AddHours(-24)}

$results = foreach ($event in $events) {
    [PSCustomObject]@{
        Time      = $event.TimeCreated
        Username  = $event.Properties[5].Value
        SourceIP  = $event.Properties[19].Value
    }
}

$results | Export-Csv -Path "C:\CyberLab\reports\failed_logons.csv" -NoTypeInformation

$results | Group-Object SourceIP | Sort-Object Count -Descending | Select-Object Name, Count
```

Run it and inspect the CSV output plus the aggregated IP summary.

**Hour 3 — Documentation**

Add a sample (redacted) CSV excerpt and the aggregation output to `get-winevent-notes.md`.

Commit:
```
git add .
git commit -m "Failed Logon Script Now Exports CSV with IP Aggregation"
git push
```

**Deliverable**
`Get-FailedLogons.ps1` v2 — produces a clean CSV plus a "top offending IPs" summary.

---

### DAY 46

**Goal**
PowerShell remoting across the lab.

**Hour 1 — Core Concept**

Reading/video: WinRM, `Enable-PSRemoting`, and `Invoke-Command` for running commands on a remote machine from your own.

**Hour 2 — Lab**

On both DC01 and the client:
```
Enable-PSRemoting -Force
```

From DC01, remotely query the client:
```
Invoke-Command -ComputerName <client-ip-or-name> -Credential (Get-Credential) -ScriptBlock { Get-Process | Select-Object -First 5 }
```

Run your `Get-FailedLogons.ps1` remotely against the client from DC01:
```
Invoke-Command -ComputerName <client-ip-or-name> -Credential (Get-Credential) -FilePath "C:\CyberLab\scripts\Get-FailedLogons.ps1"
```

**Hour 3 — Documentation**

Create:
```
scripts/powershell/remoting-notes.md
```

Document the setup steps and the remote script execution output.

Commit:
```
git add .
git commit -m "PowerShell Remoting Configured and Tested"
git push
```

**Deliverable**
Verified remote execution of your own script across two lab machines — a real "centralized query" capability.

---

### DAY 47

**Goal**
Automate the script with Task Scheduler.

**Hour 1 — Core Concept**

Reading/video: Task Scheduler triggers, actions, and running PowerShell scripts non-interactively (execution policy considerations).

**Hour 2 — Lab**

```
Open Task Scheduler
Create Task: "FailedLogonReport"
Trigger: Daily, repeat every 15 minutes for a duration of 1 day
Action: Start a program
  Program: powershell.exe
  Arguments: -ExecutionPolicy Bypass -File "C:\CyberLab\scripts\Get-FailedLogons.ps1"
```

Let it run for at least 30 minutes, then verify:
```
Get-Content C:\CyberLab\reports\failed_logons.csv | Select-Object -First 10
```

Check Task Scheduler's history/last run result to confirm success.

**Hour 3 — Documentation**

Add "Task Scheduler Automation" section to `get-winevent-notes.md` with the exact trigger/action config and proof of at least 2 successful automated runs.

Commit:
```
git add .
git commit -m "Failed Logon Script Automated via Task Scheduler"
git push
```

**Deliverable**
A script that now runs itself on schedule, producing a continuously updated report — no manual execution required.

---

### DAY 48

**Goal**
Add error handling and hardening.

**Hour 1 — Core Concept**

Reading/video: `try/catch`, `-ErrorAction`, and writing your own error log so a failed run doesn't fail silently.

**Hour 2 — Lab**

Harden the script:
```
try {
    $events = Get-WinEvent -FilterHashtable @{LogName='Security'; Id=4625; StartTime=(Get-Date).AddHours(-24)} -ErrorAction Stop

    $results = foreach ($event in $events) {
        [PSCustomObject]@{
            Time      = $event.TimeCreated
            Username  = $event.Properties[5].Value
            SourceIP  = $event.Properties[19].Value
        }
    }

    $results | Export-Csv -Path "C:\CyberLab\reports\failed_logons.csv" -NoTypeInformation
}
catch {
    $errorMessage = "$(Get-Date) - ERROR: $($_.Exception.Message)"
    Add-Content -Path "C:\CyberLab\logs\script_errors.log" -Value $errorMessage
}
```

Deliberately break it once (e.g., typo the log name) to confirm the catch block logs the error correctly, then fix it.

**Hour 3 — Documentation**

Add "Error Handling" section to `get-winevent-notes.md` explaining the try/catch logic and showing a sample logged error.

Commit:
```
git add .
git commit -m "Get-FailedLogons Script Hardened with Error Handling"
git push
```

**Deliverable**
`Get-FailedLogons.ps1` v3 — production-style, self-logging, scheduled, and resilient to failure.

---

### DAY 49

**Goal**
Consolidate and review — Week 7 capstone.

**Hour 1 — Core Concept**

Re-read all Week 7 scripts and notes out loud, explaining the purpose of each block of code.

**Hour 2 — Lab**

Self-test, live, without notes:
```
1. Write a Get-WinEvent query for a different Event ID (e.g., 4720 - user created) from scratch
2. Export any dataset to CSV unaided
3. Run a command remotely against another lab machine
4. Explain your try/catch block line by line
```

Redo any failed item before Week 8.

**Hour 3 — Documentation**

Create:
```
week-07-summary.md
```

Structure:
```
Scripts built this week (linked)
Automation now running unattended
Skills now automatic
What's next: Python automation (Week 8)
```

Commit and push:
```
git add .
git commit -m "Week 7 Completed — PowerShell Security Automation Mastered"
git push
```

**Deliverable**
A fully automated, hardened PowerShell detection script — one of your strongest interview talking points so far.

---

## Week 8 — Python for Security Automation (Crown Jewel Week)

### Week 8 Overview

**Theme**
Your basic Python now gets pointed directly at security problems. This week produces two real tools plus the Month 2 Crown Jewel — everything from Weeks 5–8 assembled into one polished, professional repository.

**Week 8 Objectives**

```
✅ Parse Linux auth logs for brute-force patterns in Python
✅ Ingest and analyze the Windows CSV exported by PowerShell
✅ Add time-window based anomaly logic
✅ Turn both scripts into proper CLI tools with argparse
✅ Publish the Month 2 Crown Jewel repository
```

**Success Criteria**

```
- Does your Python script correctly flag an IP with 5+ failed SSH attempts?
- Does your script correctly flag a user with 3+ failures inside a 10-minute window?
- Can you run both tools from the command line with arguments, unaided?
- Is the Crown Jewel repository published, documented, and cross-linking Weeks 5-8?
```

**Week 8 Resources**

Documentation
```
- Python docs: re, collections, csv, argparse, datetime
```

---

### DAY 50

**Goal**
Python regex and file parsing fundamentals.

**Hour 1 — Core Concept**

Reading/video: Python's `re` module — `re.search`, `re.findall`, and capturing groups for extracting IPs/usernames from log lines.

**Hour 2 — Lab**

On Ubuntu (or Kali), create:
```
scripts/python/parse_auth_log.py
```

```python
import re

with open("/var/log/auth.log", "r") as f:
    lines = f.readlines()

pattern = r"Failed password for (invalid user )?(\S+) from (\S+)"

for line in lines:
    match = re.search(pattern, line)
    if match:
        user = match.group(2)
        ip = match.group(3)
        print(f"Failed login - User: {user}, IP: {ip}")
```

Run it:
```
python3 parse_auth_log.py
```

If your log has no failed attempts, generate a few by deliberately mistyping an SSH password against your own Ubuntu VM.

**Hour 3 — Documentation**

Create:
```
scripts/python/README.md
```

Document the script's regex pattern, purpose, and sample output.

Commit:
```
git add .
git commit -m "Python Auth Log Parser v1 Completed"
git push
```

**Deliverable**
A working Python script that extracts failed SSH attempts with user and IP fields.

---

### DAY 51

**Goal**
Aggregate and threshold with `Counter`.

**Hour 1 — Core Concept**

Reading/video: `collections.Counter` for counting occurrences efficiently, and setting a meaningful detection threshold.

**Hour 2 — Lab**

Extend `parse_auth_log.py`:
```python
import re
from collections import Counter

with open("/var/log/auth.log", "r") as f:
    lines = f.readlines()

pattern = r"Failed password for (invalid user )?(\S+) from (\S+)"
ip_counter = Counter()

for line in lines:
    match = re.search(pattern, line)
    if match:
        ip = match.group(3)
        ip_counter[ip] += 1

THRESHOLD = 5
print("Brute-force candidates (5+ failed attempts):")
for ip, count in ip_counter.most_common():
    if count >= THRESHOLD:
        print(f"  {ip}: {count} failed attempts  <-- FLAGGED")
    else:
        print(f"  {ip}: {count} failed attempts")
```

Generate enough failed attempts from one source to cross the threshold and confirm the flag triggers.

**Hour 3 — Documentation**

Update `scripts/python/README.md` with the threshold logic and a sample flagged/unflagged output.

Commit:
```
git add .
git commit -m "Auth Log Parser Now Flags Brute-Force IPs"
git push
```

**Deliverable**
A script that correctly distinguishes normal noise from a genuine brute-force pattern.

---

### DAY 52

**Goal**
Ingest the Windows CSV exported by PowerShell.

**Hour 1 — Core Concept**

Reading/video: Python's `csv` module (or `pandas` if you prefer) for reading structured data exported from another tool — a very real cross-platform SOC workflow.

**Hour 2 — Lab**

Copy `failed_logons.csv` (from Week 7, Day 45) into your Linux environment, then create:
```
scripts/python/parse_windows_csv.py
```

```python
import csv
from collections import Counter

user_counter = Counter()

with open("failed_logons.csv", newline="") as f:
    reader = csv.DictReader(f)
    for row in reader:
        user_counter[row["Username"]] += 1

print("Failed logons by username:")
for user, count in user_counter.most_common():
    print(f"  {user}: {count}")
```

Run it against your real exported CSV and confirm the counts match what you'd expect from Week 7's data.

**Hour 3 — Documentation**

Add to `scripts/python/README.md`: how this script bridges your Windows (PowerShell) and Linux (Python) tooling.

Commit:
```
git add .
git commit -m "Windows CSV Ingestion Script Completed"
git push
```

**Deliverable**
A Python tool that consumes real data generated by your PowerShell automation — proof of cross-platform workflow thinking.

---

### DAY 53

**Goal**
Time-window anomaly logic.

**Hour 1 — Core Concept**

Reading/video: Python's `datetime` module for comparing timestamps and detecting "N events within X minutes" patterns — a step beyond simple counting.

**Hour 2 — Lab**

Extend `parse_windows_csv.py`:
```python
import csv
from datetime import datetime, timedelta
from collections import defaultdict

events_by_user = defaultdict(list)

with open("failed_logons.csv", newline="") as f:
    reader = csv.DictReader(f)
    for row in reader:
        ts = datetime.strptime(row["Time"], "%m/%d/%Y %I:%M:%S %p")  # adjust format to match your CSV
        events_by_user[row["Username"]].append(ts)

WINDOW = timedelta(minutes=10)
THRESHOLD = 3

for user, timestamps in events_by_user.items():
    timestamps.sort()
    for i in range(len(timestamps)):
        window_events = [t for t in timestamps if timestamps[i] <= t <= timestamps[i] + WINDOW]
        if len(window_events) >= THRESHOLD:
            print(f"ALERT: {user} had {len(window_events)} failed logons within 10 minutes starting {timestamps[i]}")
            break
```

Adjust the `strptime` format string to match your actual CSV's timestamp format exactly — this troubleshooting step is a normal and expected part of real log analysis work.

**Hour 3 — Documentation**

Add "Time-Window Detection Logic" section to `scripts/python/README.md` explaining the sliding-window approach in your own words.

Commit:
```
git add .
git commit -m "Time-Window Anomaly Detection Added"
git push
```

**Deliverable**
A script that distinguishes "5 failures over a week" (probably noise) from "3 failures in 10 minutes" (probably an attack) — genuine detection logic.

---

### DAY 54

**Goal**
Convert both scripts into proper CLI tools with `argparse`.

**Hour 1 — Core Concept**

Reading/video: Python's `argparse` module for building real command-line tools with flags and help text.

**Hour 2 — Lab**

Refactor `parse_auth_log.py`:
```python
import re
import argparse
from collections import Counter

parser = argparse.ArgumentParser(description="Detect brute-force SSH attempts from an auth.log file.")
parser.add_argument("--file", required=True, help="Path to the auth.log file")
parser.add_argument("--threshold", type=int, default=5, help="Number of failures to flag as brute-force")
args = parser.parse_args()

with open(args.file, "r") as f:
    lines = f.readlines()

pattern = r"Failed password for (invalid user )?(\S+) from (\S+)"
ip_counter = Counter()

for line in lines:
    match = re.search(pattern, line)
    if match:
        ip_counter[match.group(3)] += 1

for ip, count in ip_counter.most_common():
    flag = " <-- FLAGGED" if count >= args.threshold else ""
    print(f"{ip}: {count} failed attempts{flag}")
```

Run it properly as a CLI tool:
```
python3 parse_auth_log.py --file /var/log/auth.log --threshold 5
python3 parse_auth_log.py --file /var/log/auth.log --threshold 3
```

Apply the same `argparse` pattern to `parse_windows_csv.py`.

**Hour 3 — Documentation**

Update `scripts/python/README.md` with usage examples (`--help` output and real run examples) for both tools.

Commit:
```
git add .
git commit -m "Both Python Tools Converted to Proper CLI Utilities"
git push
```

**Deliverable**
Two genuinely reusable CLI security tools — the kind you can run against any environment, not just your own lab.

---

### DAY 55

**Goal**
Code cleanup, docstrings, and final hardening.

**Hour 1 — Core Concept**

Reading/video: docstrings, PEP 8 basics, and adding graceful error handling (missing file, malformed line) to Python scripts.

**Hour 2 — Lab**

Add docstrings and error handling to both scripts:
```python
"""
parse_auth_log.py

Parses a Linux auth.log file for failed SSH login attempts and flags
source IPs that exceed a configurable brute-force threshold.

Usage:
    python3 parse_auth_log.py --file /var/log/auth.log --threshold 5
"""
```

Wrap the file read in error handling:
```python
try:
    with open(args.file, "r") as f:
        lines = f.readlines()
except FileNotFoundError:
    print(f"ERROR: File not found: {args.file}")
    exit(1)
```

Test the error path deliberately:
```
python3 parse_auth_log.py --file /path/that/does/not/exist.log
```

**Hour 3 — Documentation**

Finalize `scripts/python/README.md` with a clean "Usage," "Requirements," and "Example Output" structure for both tools.

Commit:
```
git add .
git commit -m "Python Scripts Cleaned, Documented, and Hardened"
git push
```

**Deliverable**
Two polished, professional-grade Python security tools, ready to be the centerpiece of your Crown Jewel repo.

---

### DAY 56

**Goal**
Assemble and publish the Month 2 Crown Jewel — Crown Jewel Day.

**Hour 1 — Core Concept**

Reading/video: none — instead, re-read your entire Month 2 journey (Weeks 5–8) out loud, end to end, as final consolidation.

**Hour 2 — Lab**

Assemble the final repository structure:
```
ad-homelab-and-automation/
├── README.md
├── ad-lab-build-guide.md
├── diagrams/
│   └── ad-structure-diagram.png
├── auditing/
│   ├── gpo-audit-configuration.md
│   ├── sysmon-deployment.md
│   ├── auditd-configuration.md
│   └── mini-investigation-01.md
└── scripts/
    ├── powershell/
    │   ├── Get-FailedLogons.ps1
    │   ├── get-winevent-notes.md
    │   └── remoting-notes.md
    └── python/
        ├── parse_auth_log.py
        ├── parse_windows_csv.py
        └── README.md
```

Run a final live self-test covering all of Month 2, unaided:
```
1. Create a new AD user and place them in an OU
2. Trigger and locate a 4625 event
3. Run Get-FailedLogons.ps1 and explain each line
4. Run parse_auth_log.py with a custom --threshold and explain the Counter logic
```

**Hour 3 — Documentation**

Write the master `README.md`:
```
# Active Directory Home Lab & Security Automation

## What this repo demonstrates
- A fully built Active Directory domain (corp.local) with OUs, users, and a domain-joined client
- Domain-wide security auditing via GPO (Event IDs 4624/4625)
- Sysmon deployment for detailed process-level telemetry
- Linux auditd configuration for file integrity monitoring
- PowerShell automation: scheduled, error-handled security log extraction
- Python automation: brute-force detection with threshold and time-window logic

## Structure
(explain folders)

## Skills demonstrated
(Active Directory administration, GPO configuration, Windows/Linux audit logging, PowerShell scripting, Python scripting, detection logic design)
```

Final commit and push:
```
git add .
git commit -m "Month 2 Completed — Crown Jewel Published"
git push
```

**Deliverable**
A fully published `ad-homelab-and-automation` repository — **Month 2 is complete**, and your lab is now fully instrumented and ready for Month 3's SIEM.

---

*End of Chapter 2. Chapter 3 (Month 3 — SOC Foundations, Wazuh SIEM, and Detection Engineering) continues in the same format.*
