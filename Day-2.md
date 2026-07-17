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
| **#** | **Command** | **Purpose**                                | **Syntax**                    | **Example**             | **Expected Output**                               | **Notes**                                               |
| :---: | :---------- | :----------------------------------------- | :---------------------------- | :---------------------- | :------------------------------------------------ | :------------------------------------------------------ |
|   1   | `pwd`       | Display the current working directory.     | `pwd`                         | `pwd`                   | `/home/kali/CyberLab`                             | Shows the absolute path of the current directory.       |
|   2   | `ls`        | List files and directories.                | `ls [options]`                | `ls -la`                | Displays files with permissions and hidden files. | `-l` = long listing, `-a` = hidden files.               |
|   3   | `cd`        | Change the current directory.              | `cd <directory>`              | `cd reports`            | Changes to the `reports` directory.               | `cd ..` moves one level up.                             |
|   4   | `mkdir`     | Create a new directory.                    | `mkdir <directory>`           | `mkdir backup`          | Creates a directory named `backup`.               | Use `mkdir -p` to create nested directories.            |
|   5   | `touch`     | Create an empty file.                      | `touch <filename>`            | `touch notes.txt`       | Creates `notes.txt`.                              | Can also update the timestamp of an existing file.      |
|   6   | `cp`        | Copy files or directories.                 | `cp <source> <destination>`   | `cp notes.txt backup/`  | Copies `notes.txt` to `backup/`.                  | Use `-r` to copy directories.                           |
|   7   | `mv`        | Move or rename files/directories.          | `mv <source> <destination>`   | `mv notes.txt reports/` | Moves the file to `reports/`.                     | Also used for renaming files.                           |
|   8   | `rm`        | Remove files or directories.               | `rm <file>`                   | `rm notes.txt`          | Deletes `notes.txt`.                              | Use `rm -r` for directories. Be careful—no recycle bin. |
|   9   | `cat`       | Display file contents.                     | `cat <file>`                  | `cat report.txt`        | Prints the file contents.                         | Useful for small text files.                            |
|   10  | `less`      | View large files page by page.             | `less <file>`                 | `less report.txt`       | Opens an interactive viewer.                      | Press **q** to quit.                                    |
|   11  | `head`      | Show the first lines of a file.            | `head <file>`                 | `head report.txt`       | Displays the first 10 lines.                      | Use `-n` to specify the number of lines.                |
|   12  | `tail`      | Show the last lines of a file.             | `tail <file>`                 | `tail report.txt`       | Displays the last 10 lines.                       | `tail -f logfile.log` monitors a log file in real time. |
|   13  | `find`      | Search for files or directories.           | `find <path> -name <pattern>` | `find . -name "*.txt"`  | Lists all `.txt` files.                           | Searches recursively.                                   |
|   14  | `locate`    | Find files using a pre-built database.     | `locate <filename>`           | `locate passwd`         | Shows matching file paths.                        | Run `sudo updatedb` if the database is outdated.        |
|   15  | `tree`      | Display the directory structure as a tree. | `tree <directory>`            | `tree CyberLab`         | Prints the folder hierarchy.                      | Install using `sudo apt install tree`.                  |

---
# Frequently Used Options
---
| **Option** | **Description**                     | **Example**            |
| :--------: | :---------------------------------- | :--------------------- |
|    `-a`    | Show hidden files                   | `ls -a`                |
|    `-l`    | Long listing format                 | `ls -l`                |
|    `-la`   | Long listing including hidden files | `ls -la`               |
|    `-r`    | Recursive operation                 | `cp -r folder backup/` |
|    `-f`    | Follow file updates (tail)          | `tail -f logfile.log`  |
|    `-n`    | Specify number of lines             | `head -n 20 file.txt`  |
|    `-p`    | Create parent directories           | `mkdir -p notes/linux` |
---


# Commands Practiced During the Lab

| **Task**              | **Command**                                 |
| :-------------------- | :------------------------------------------ |
| Create CyberLab       | `mkdir CyberLab`                            |
| Enter CyberLab        | `cd CyberLab`                               |
| Create subdirectories | `mkdir notes scripts reports projects logs` |
| Create a file         | `touch notes/readme.txt`                    |
| Copy a file           | `cp notes/readme.txt reports/`              |
| Move a file           | `mv reports/readme.txt logs/`               |
| Delete a file         | `rm logs/readme.txt`                        |
| Search a file         | `find . -name "*.txt"`                      |
| View folder structure | `tree CyberLab`                             |

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

---

# Deliverable

**File Name**

```text
Day-2.md
```

**Repository**

```text
CyberSecurity
```

**Status**

✅ Completed
