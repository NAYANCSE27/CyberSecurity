# Day 3: Linux Permissions & Ownership

**Roadmap:** Zero to Hired – Cybersecurity (Month 1, Week 1)

**Goal:** Understand Linux file permissions, ownership, and privilege management.

---

# Learning Objectives

By the end of this lab, I should be able to:

- Explain Linux permission notation.
- Interpret symbolic (`rwx`) and octal permissions.
- Change permissions using `chmod`.
- Change ownership using `chown` and `chgrp`.
- Understand the difference between `sudo` and the root user.
- Apply proper permissions based on security best practices.
- Explain why overly permissive permissions (e.g., `777`) are dangerous.

---

# 1. Linux File Permissions

Every file and directory in Linux has permissions that determine who can:

- Read the file
- Modify the file
- Execute the file

Permissions are assigned to three categories of users:

| Category | Meaning |
|----------|---------|
| User (u) | File owner |
| Group (g) | Users belonging to the file's group |
| Others (o) | Everyone else |

Example:

```bash
-rwxr-xr-x
```

Breaking it down:

```
-
rwx
r-x
r-x
```

| Symbol | Meaning |
|---------|---------|
| - | Regular file |
| rwx | Owner permissions |
| r-x | Group permissions |
| r-x | Others permissions |

---

# 2. Permission Types

| Symbol | Meaning | Value |
|---------|---------|------:|
| r | Read | 4 |
| w | Write | 2 |
| x | Execute | 1 |

Example

```
rwx = 4+2+1 = 7
rw- = 4+2 = 6
r-x = 4+1 = 5
r-- = 4
--- = 0
```

---

# 3. Octal Permissions

Linux commonly represents permissions using octal notation.

| Octal | Binary | Symbolic | Meaning |
|-------:|--------|----------|---------|
|777|111111111|rwxrwxrwx|Everyone has full access|
|755|111101101|rwxr-xr-x|Owner full control; others can read and execute|
|700|111000000|rwx------|Only owner has access|
|644|110100100|rw-r--r--|Owner can modify; others read only|
|600|110000000|rw-------|Private file|

---

# Understanding Each Digit

Example:

```
754
```

Break it into three numbers.

```
7     5     4
│     │     │
│     │     └── Others
│     └──────── Group
└────────────── Owner
```

Meaning

Owner

```
7 = rwx
```

Group

```
5 = r-x
```

Others

```
4 = r--
```

---

# What Does the Third Digit Control?

Example

```
754
```

The **third digit** controls the permissions granted to **Others** (everyone who is neither the owner nor a member of the file's group).

```
754

Owner  → 7 → rwx

Group  → 5 → r-x

Others → 4 → r--
```

In this example, other users can only **read** the file.

---

# 4. Viewing Permissions

Use

```bash
ls -l
```

Example

```bash
-rwxr-xr-x 1 kali kali 125 Jun 20 secretfile.txt
```

Explanation

| Field | Description |
|---------|------------|
|-rwxr-xr-x|Permission bits|
|1|Number of hard links|
|kali|Owner|
|kali|Group|
|125|File size|
|Jun 20|Last modified|
|secretfile.txt|File name|

---

# 5. chmod

`chmod` changes file permissions.

Syntax

```bash
chmod PERMISSION filename
```

Example

```bash
chmod 700 secretfile.txt
```

Result

```
rwx------
```

Only the owner has access.

---

Another example

```bash
chmod 755 secretfile.txt
```

Result

```
rwxr-xr-x
```

Others may read and execute but cannot modify.

---

Another example

```bash
chmod 777 secretfile.txt
```

Result

```
rwxrwxrwx
```

Everyone has full access.

---

# 6. chown

Changes file ownership.

Syntax

```bash
sudo chown username filename
```

Example

```bash
sudo chown testuser secretfile.txt
```

Now

```
Owner = testuser
```

---

# 7. chgrp

Changes the group owner.

Syntax

```bash
sudo chgrp developers secretfile.txt
```

---

# 8. chmod vs chown

| chmod | chown |
|---------|-------|
|Changes permissions|Changes owner|
|Controls who can access|Controls who owns|
|Uses rwx values|Uses usernames|
|Does not change ownership|Does not change permissions|

---

# 9. sudo vs Root

## Root

Root is the superuser.

Root can

- Read every file
- Delete every file
- Modify every file
- Install software
- Manage users

---

## sudo

`sudo` temporarily grants administrator privileges to a normal user.

Example

```bash
sudo apt update
```

Instead of logging in as root, Linux encourages using `sudo` because it is safer and provides accountability through logs.

---

# Lab Exercise

## Step 1

Create workspace

```bash
mkdir CyberLab
cd CyberLab
```

---

## Step 2

Create a file

```bash
touch secretfile.txt
```

---

## Step 3

Set permission to 700

```bash
chmod 700 secretfile.txt
```

Verify

```bash
ls -l
```

Expected

```
-rwx------
```

---

## Step 4

Change to 755

```bash
chmod 755 secretfile.txt
```

Verify

```bash
ls -l
```

Expected

```
-rwxr-xr-x
```

---

## Step 5

Change to 777

```bash
chmod 777 secretfile.txt
```

Verify

```bash
ls -l
```

Expected

```
-rwxrwxrwx
```

---

# Create a Test User

```bash
sudo adduser testuser
```

Switch user

```bash
su testuser
```

Navigate

```bash
cd /home/kali/CyberLab
```

Attempt to read

```bash
cat secretfile.txt
```

Observe the output.

Return

```bash
exit
```

---

# Observations

Permission 700

```
Permission denied
```

Permission 755

```
Readable
```

Permission 777

```
Readable and writable by everyone
```

---

# Reflection Questions

## Why is 777 dangerous?

Permission **777** allows every user on the system to read, modify, and execute the file.

Potential risks include:

- Malware modification
- Unauthorized data changes
- Privilege escalation opportunities
- Accidental deletion
- Integrity compromise

Because of these risks, production systems should almost never use `777`.

---

## What does the third digit in 754 control?

The third digit represents permissions for **Others**.

```
754

Owner = rwx

Group = r-x

Others = r--
```

---

## Difference between chmod and chown

`chmod`

- Changes permissions
- Controls access rights

`chown`

- Changes ownership
- Controls who owns the file

---

# Best Practices

✔ Never use `777` unless absolutely necessary.

✔ Apply the **Principle of Least Privilege**.

✔ Use `sudo` instead of logging in as root.

✔ Regular files should generally use:

```
644
```

✔ Executable scripts should generally use:

```
755
```

✔ Sensitive configuration files should use:

```
600
```

---

# Screenshot Section

Include screenshots of:

- `ls -l` after `chmod 700`
- `ls -l` after `chmod 755`
- `ls -l` after `chmod 777`
- `testuser` attempting to access the file
- Permission denied (if applicable)

---

# Interview Questions

### What does `chmod 755` mean?

Owner has full permissions, while group and others have read and execute permissions.

---

### Why should we avoid 777?

Because it gives unrestricted access to every user, violating the Principle of Least Privilege.

---

### Difference between chmod and chown?

`chmod` changes permissions.

`chown` changes ownership.

---

### Why use sudo instead of root?

`sudo` provides temporary administrative privileges, reduces risk, and creates an audit trail.

---

# Key Takeaways

- Linux permissions are divided into **Owner**, **Group**, and **Others**.
- Symbolic permissions (`rwx`) correspond to octal values.
- `chmod` changes permissions.
- `chown` changes ownership.
- `chgrp` changes group ownership.
- `sudo` is preferred over logging in directly as the root user.
- Following the **Principle of Least Privilege** is essential for system security.

---

# Deliverables

- ✅ Completed permission exercises (`700`, `755`, `777`)
- ✅ Created and tested a secondary user
- ✅ Documented observations
- ✅ Added permissions reference to `linux-cheatsheet.md`
- ✅ Captured screenshots of permission changes and access tests
