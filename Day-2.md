# Linux Filesystem Cheat Sheet

> **Roadmap:** Zero to Hired - Cybersecurity Roadmap  
> **Month:** 1 - Linux & Networking Foundations  
> **Week:** 1  
> **Day:** 2 - Linux File System  
> **Platform:** Kali Linux (VirtualBox)  
> **Date:** 2026-07-17

---

# Objective

Learn the Linux file system and practice essential file and directory management commands.

---

# Lab Environment

| Item | Details |
|------|---------|
| Operating System | Kali Linux |
| Virtualization | VirtualBox |
| Shell | Bash |
| User | kali |
| Working Directory | ~/CyberLab |

---

# Lab Setup

## Create Working Directory

```bash
mkdir CyberLab
cd CyberLab

mkdir notes
mkdir scripts
mkdir reports
mkdir projects
mkdir logs
```

---

## Install Required Package

```bash
sudo apt update
sudo apt install tree
```

---

# Directory Structure

```text
CyberLab/
├── notes/
├── scripts/
├── reports/
├── projects/
└── logs/
```

> 📷 **Screenshot:** Insert the output of `tree CyberLab`

---

# Linux Commands Documentation

---

## 1. pwd

### Purpose

Displays the current working directory.

### Syntax

```bash
pwd
```

### Example

```bash
pwd
```

### Output

```text
/home/kali/CyberLab
```

### Notes

- Shows the absolute path.
- Useful for verifying your current location.

---

## 2. ls

### Purpose

Lists files and directories.

### Syntax

```bash
ls
```

### Example

```bash
ls -la
```

### Output

```text
drwxr-xr-x notes
drwxr-xr-x reports
...
```

### Notes

- `-l` → Long format
- `-a` → Hidden files

---

## 3. cd

### Purpose

Changes the current directory.

### Syntax

```bash
cd directory_name
```

### Example

```bash
cd reports
```

### Output

```text
(Current directory changed)
```

### Notes

```bash
cd ..
```

Moves one directory up.

---

## 4. mkdir

### Purpose

Creates a new directory.

### Syntax

```bash
mkdir directory_name
```

### Example

```bash
mkdir backup
```

### Output

```text
(No output if successful)
```

---

## 5. touch

### Purpose

Creates an empty file.

### Syntax

```bash
touch filename
```

### Example

```bash
touch notes.txt
```

---

## 6. cp

### Purpose

Copies files or directories.

### Syntax

```bash
cp source destination
```

### Example

```bash
cp notes.txt backup/
```

---

## 7. mv

### Purpose

Moves or renames files.

### Syntax

```bash
mv source destination
```

### Example

```bash
mv notes.txt reports/
```

---

## 8. rm

### Purpose

Deletes files or directories.

### Syntax

```bash
rm filename
```

### Example

```bash
rm notes.txt
```

### Remove Directory

```bash
rm -r projects
```

---

## 9. cat

### Purpose

Displays the contents of a file.

### Example

```bash
cat report.txt
```

---

## 10. less

### Purpose

Views long files page by page.

### Example

```bash
less report.txt
```

### Useful Keys

| Key | Action |
|------|--------|
| Space | Next Page |
| b | Previous Page |
| q | Quit |

---

## 11. head

### Purpose

Displays the first 10 lines of a file.

### Example

```bash
head report.txt
```

---

## 12. tail

### Purpose

Displays the last 10 lines of a file.

### Example

```bash
tail report.txt
```

### Live Monitoring

```bash
tail -f logfile.log
```

---

## 13. find

### Purpose

Searches for files and directories.

### Example

```bash
find . -name "*.txt"
```

---

## 14. locate

### Purpose

Searches files using a database.

### Example

```bash
locate passwd
```

> Update the database first if needed:

```bash
sudo updatedb
```

---

## 15. tree

### Purpose

Displays the directory structure in a tree format.

### Example

```bash
tree CyberLab
```

### Sample Output

```text
CyberLab
├── logs
├── notes
├── projects
├── reports
└── scripts
```

---

# Lab Exercises Completed

- [x] Created CyberLab directory
- [x] Created subdirectories
- [x] Installed tree
- [x] Practiced pwd
- [x] Practiced ls
- [x] Practiced cd
- [x] Practiced mkdir
- [x] Practiced touch
- [x] Practiced cp
- [x] Practiced mv
- [x] Practiced rm
- [x] Practiced cat
- [x] Practiced less
- [x] Practiced head
- [x] Practiced tail
- [x] Practiced find
- [x] Practiced locate
- [x] Generated tree output

---

# Screenshots

## CyberLab Directory Structure

> Insert Screenshot Here

---

## tree Command Output

> Insert Screenshot Here

---

# Key Takeaways

- Learned Linux directory navigation.
- Managed files and folders using essential commands.
- Understood file viewing and searching techniques.
- Built a reusable Linux workspace for future cybersecurity labs.

---

# Git Commands

```bash
git add .

git commit -m "Linux Filesystem Completed"

git push
```

---

# Deliverable

**File Name**

```text
linux-cheatsheet.md
```

**Repository**

```text
cybersecurity-notes
```

**Status**

✅ Completed
