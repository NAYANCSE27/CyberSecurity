# Day 3 — Linux Permissions & Ownership
### Expert Field Notes: Why Permissions Are the Single Most Common Way Companies Get Breached

---

## Goal
Understand and control **who can read, write, or execute** every file on a Linux system — and understand why getting this wrong is one of the top real-world causes of data breaches, privilege escalation, and "how did they get root?!" incidents.

---

## Hour 1 — Core Concept

**Resource:** TryHackMe → Linux Fundamentals Part 1 (continued) — Permissions section

### Topics Covered
```
rwx notation
Octal notation (755, 644, 777)
chmod
chown
chgrp
sudo vs root
```

### The Mental Model (read this before anything else)

Every file and directory on Linux has **three identities** attached to it and **three permission types** for each identity.

**The three identities:**
| Identity | Symbol | Meaning |
|---|---|---|
| Owner (User) | `u` | The specific user who owns the file |
| Group | `g` | A group of users who share access |
| Others | `o` | Literally everyone else on the system |

**The three permission types:**
| Permission | Symbol | On a file | On a directory |
|---|---|---|---|
| Read | `r` | View file contents | List directory contents (`ls`) |
| Write | `w` | Modify/delete file contents | Create/delete/rename files inside it |
| Execute | `x` | Run the file as a program/script | `cd` into the directory |

> **Real-world gotcha:** People assume `x` on a directory means "list it." It doesn't — `r` lists it. `x` lets you *enter and traverse* it, and access things *inside* it *if you know their exact name*. This is exactly why real servers set `711` on certain directories (e.g., `/home/username` is often `750` or `700`) — so users can't browse each other's home folders but specific subpaths can still be reached by services that know the exact path.

### rwx Notation vs Octal Notation — Same Thing, Two Languages

```
Symbolic:  rwxr-xr-x
Position:  [owner][group][others]
Binary:     rwx | r-x | r-x
Octal:      7   |  5  |  5    →  755
```

Each `r`, `w`, `x` is a bit:
```
r = 4
w = 2
x = 1
- = 0
```

Add them per identity:
```
rwx = 4+2+1 = 7
r-x = 4+0+1 = 5
r-- = 4+0+0 = 4
rw- = 4+2+0 = 6
--- = 0+0+0 = 0
```

**Memorize this table once and you never need a calculator again:**

| Octal | Symbolic | Meaning |
|---|---|---|
| 0 | `---` | No access |
| 1 | `--x` | Execute only |
| 2 | `-w-` | Write only (rare) |
| 3 | `-wx` | Write + execute |
| 4 | `r--` | Read only |
| 5 | `r-x` | Read + execute |
| 6 | `rw-` | Read + write |
| 7 | `rwx` | Read + write + execute |

### chmod, chown, chgrp — What Each Actually Does

```
chmod  = CHange MODe        → changes WHAT is allowed (the permission bits)
chown  = CHange OWNer       → changes WHO owns the file (user, and optionally group)
chgrp  = CHange GRouP       → changes WHICH group owns the file
```

**This is the #1 confusion point for beginners:**
- `chmod 700 file.txt` → same owner, same group, but now *only the owner* can touch it.
- `chown alice file.txt` → the file now *belongs to* alice, but the permission bits (rwx) don't change at all.
- `chown alice:developers file.txt` → changes owner to alice AND group to developers, in one command.

**Real-life example:** A DevOps engineer inherits a legacy server. A script owned by a former employee `bob` (`bob:bob`) is still running as a cron job. The company disables `bob`'s account. The cron job now fails silently because the cron daemon runs it as `bob`, and `bob` no longer exists.
```bash
sudo chown newservice:newservice /opt/scripts/backup.sh
```
This reassigns ownership without touching a single permission bit — the script keeps its `rwxr-xr-x` exactly as-is, but now runs under a real, valid account.

### sudo vs root — The Distinction That Matters in Every Security Interview

```
root  = the actual superuser account (UID 0), unrestricted access to everything
sudo  = a mechanism that lets an AUTHORIZED user run a command AS root (or another user),
        temporarily, with logging, without ever knowing the root password
```

**Why this distinction is a real security control, not trivia:**
- If you log in directly as `root`, there is no per-user audit trail — every action just says "root did this."
- If you use `sudo`, every command is logged (usually to `/var/log/auth.log` or `/var/log/secure`) **with the actual username** who ran it.
- This is why most hardened production servers **disable direct root login entirely** (`PermitRootLogin no` in `sshd_config`) and force everyone through `sudo` — it's an accountability control, not just a convenience feature.

**Real-life example:** In an incident response case, an analyst finds a malicious cron job was added on a production server. Because the server had root SSH login enabled and three admins all used the shared root password, there was no way to determine which admin's credentials were compromised — or whether it was an outsider entirely. A server enforcing `sudo`-only access would have shown exactly which named account executed the change, in `/var/log/auth.log`, with a timestamp.

---

## Hour 2 — Lab

### Step 1: Create a Test File and Practice Permission Changes

```bash
cd CyberLab
touch secretfile.txt
chmod 700 secretfile.txt
ls -l secretfile.txt
```
Expected output:
```
-rwx------ 1 kali kali 0 Jul 19 10:02 secretfile.txt
```
Owner (`kali`) has full rwx. Group and Others have nothing. This is the correct permission set for something like an SSH private key or a personal password vault file.

```bash
chmod 755 secretfile.txt
ls -l secretfile.txt
```
Expected output:
```
-rwxr-xr-x 1 kali kali 0 Jul 19 10:02 secretfile.txt
```
Now Group and Others can read and execute it, but not modify it. This is the standard permission set for a shared script or binary that everyone should be able to run, but only the owner should be able to edit.

```bash
chmod 777 secretfile.txt
ls -l secretfile.txt
```
Expected output:
```
-rwxrwxrwx 1 kali kali 0 Jul 19 10:02 secretfile.txt
```
**Everyone on the system can now read, modify, delete, or replace the contents of this file — including any low-privilege user, any compromised service account, and any process running under any other identity.**

> **Field note:** `chmod 777` is one of the first things a penetration tester greps for during a Linux privilege escalation assessment:
> ```bash
> find / -perm -o+w -type f 2>/dev/null
> ```
> This command finds every world-writable file on the system. If any of those files are executed by a privileged process (a cron job running as root, a service startup script, a sudoers-referenced script), that's an instant, trivial path to full root compromise — no exploit code required, just overwriting the file with your own payload and waiting for it to run.

### Step 2: Answer These in Writing Before Moving On

**Q1: Why is 777 dangerous on a real system?**

> `777` removes every access boundary on that file or directory. In a real environment, this means:
> - **Real-life example — the WordPress `wp-config.php` incident pattern:** A sysadmin sets `chmod -R 777 /var/www/html` to "fix a permissions error" quickly (a very common shortcut under deadline pressure). Now `wp-config.php` — which contains the database username and password in plaintext — is world-writable. Any other tenant on a shared host, any compromised low-privilege service (like a misconfigured PHP-FPM pool running as `www-data`), or any malicious script uploaded through an unrelated vulnerability can now silently modify that file, inject a backdoor, or exfiltrate the database credentials. This exact pattern (over-permissive `777` fixes under deadline pressure) shows up repeatedly in real breach post-mortems for exactly this reason — it "fixes" the symptom (a permission-denied error) while opening the door to everyone.
> - It also breaks the principle of least privilege, which is the foundation nearly every compliance framework (PCI-DSS, HIPAA, SOC 2, ISO 27001) is built on. An auditor who finds world-writable files containing credentials or business logic will flag it as a critical finding every time.

**Q2: What does the 3rd digit in 754 control?**

> In `754`, the three digits map to **owner, group, others** in that order:
> ```
> 7  5  4
> u  g  o
> ```
> So the 3rd digit (`4`) controls **Others** — meaning literally every other user account on the system, with no special relationship to the file at all. In this example, `4` = read-only. Others can view the file's contents but cannot modify it, delete it, or execute it.
>
> **Real-life example:** A company's public-facing documentation site stores its static HTML files as `754` — the web server's own account (owner) has full control (`7`), the deployment group (`g`) can read and execute to serve the files (`5`), and everyone else on the shared server (`o`) can only read them (`4`) — enough for a `cat` to work if needed for debugging, but nowhere near enough to tamper with the site.

**Q3: What's the difference between chmod and chown?**

> `chmod` changes **what actions are permitted** (the rwx bits) — it never changes who owns the file.
> `chown` changes **who the file belongs to** (the user, and optionally the group) — it never changes what the permission bits say.
>
> **Real-life example:** A shared team folder `/data/reports` is owned by `alice:analysts` with permissions `770` (owner and group get full access, others get nothing). When Bob joins the analytics team, you don't touch the folder's permission bits at all (`770` already correctly allows full group access) — you simply add Bob to the `analysts` group:
> ```bash
> sudo usermod -aG analysts bob
> ```
> No `chmod` needed. The permission *policy* (`770`) was already correct; only the *membership* needed to change. Conflating these two concepts is the most common real-world permissions mistake — engineers often reach for `chmod 777` to "just make it work" when the actual fix is a one-line `chown`/`usermod` group change.

### Step 3: Create a Second User and Test Real Access Control

```bash
sudo adduser testuser
```
You'll be prompted to set a password and optional user info (name, room number, etc. — these can all be left blank by pressing Enter).

```bash
su testuser
cd /home/kali/CyberLab
cat secretfile.txt
```

**What you should observe, depending on the permission state you left the file in:**

If the file is still `777` (world-readable/writable):
```
(the file's contents print with no error — testuser can read it, and could edit it too)
```

If you re-run `chmod 700 secretfile.txt` as `kali` first, then repeat the test as `testuser`:
```
cat: secretfile.txt: Permission denied
```

```bash
exit
```
This returns you to your original `kali` session.

> **Real-life example — this exact test is a real security control validation step.** Before deploying a multi-tenant application server, security teams run precisely this kind of test: create a low-privilege test account, attempt to read/write/execute every sensitive file (config files, credential stores, log files) as that low-privilege account, and confirm every single one returns `Permission denied`. This is often called a **"negative access test"** — proving that access is *correctly denied*, not just that access *works* for the intended user. Missing this step is how misconfigured file shares end up letting any authenticated user read every other user's files (a real, recurring category of breach in corporate file-share environments).

---

## Hour 3 — Documentation

### Add This "Permissions" Section to `linux-cheatsheet.md`

```markdown
## Permissions

| Octal | Binary (u/g/o) | Symbolic    | Meaning              | Real-world use case |
|-------|-----------------|-------------|-----------------------|----------------------|
| 777   | 111 111 111     | rwxrwxrwx   | Everyone: full control | **Almost never correct.** Seen in rushed "quick fixes" for permission errors; a top target for privilege escalation scans (`find / -perm -o+w`). Avoid on any file containing credentials, code, or config. |
| 755   | 111 101 101     | rwxr-xr-x   | Owner: full; Group/Others: read+execute | Standard for scripts/binaries everyone should run but only the owner should edit — e.g., `/usr/bin` executables, web server document roots for static files. |
| 700   | 111 000 000     | rwx------   | Owner only, full control | SSH private keys (`~/.ssh/id_rsa` is enforced at 600 by OpenSSH — it will refuse to use a key with looser permissions), personal scripts with embedded credentials, home directories on hardened servers. |
| 644   | 110 100 100     | rw-r--r--   | Owner: read+write; Group/Others: read only | Standard for regular files like configuration files that should be readable but not editable by non-owners (e.g., `/etc/passwd`, most `.conf` files). |
| 600   | 110 000 000     | rw-------   | Owner only, read+write, no execute | Private keys, credential files, `.env` files, browser cookie stores — anything sensitive that never needs to be "run" as a program. |
| 750   | 111 101 000     | rwxr-x---   | Owner: full; Group: read+execute; Others: nothing | Shared team directories where only a specific group should even see what's inside — common for `/home/username` on multi-user servers. |

### Commands Reference

| Command | Purpose | Example |
|---|---|---|
| `chmod` | Change permission bits | `chmod 644 config.yml` |
| `chown` | Change file owner (and optionally group) | `chown alice:analysts report.csv` |
| `chgrp` | Change only the group | `chgrp analysts report.csv` |
| `chmod -R` | Apply recursively to a directory tree | `chmod -R 750 /data/reports` (use with caution — never `-R 777`) |
| `find / -perm -o+w` | Find world-writable files (privesc audit) | Used by pentesters and hardening scripts alike |

### Key Takeaways
- **rwx** = what's allowed; **octal** is just rwx written as one digit per identity (owner/group/others).
- **chmod** changes permissions; **chown/chgrp** change ownership — they solve different problems and are frequently confused.
- **sudo** is not "root" — it's an accountability-preserving way to *act as* root, and real production environments disable direct root login specifically so every privileged action is attributable to a named human.
- **777 is a red flag, not a fix.** If you're reaching for `777` to solve a permission-denied error, the real fix is almost always a `chown`/`chgrp`/group-membership change instead.
```

---

## Deliverable

- ✅ "Permissions" section added to `linux-cheatsheet.md` (above)
- ✅ Screenshot of the `testuser` access test showing `Permission denied` on a `700` file, and successful read on a `755`/`777` file, for comparison

```bash
git add linux-cheatsheet.md
git commit -m "Linux Permissions and Ownership Completed - with real-world risk examples"
git push
```
