# 🏴‍☠️ OverTheWire Bandit — Complete Walkthrough (Levels 0-6)

> **Author:** Muhammad Sadiq  
> **Date:** 2026  
> **Platform:** [OverTheWire Bandit](https://overthewire.org/wargames/bandit/)  
> **Levels Completed:** 0 — 6  
> **Focus:** Linux CLI, SSH, Permissions, File Management

---

## 📌 Table of Contents
1. [Level 0 → 1](#level-0--1)
2. [Level 1 → 2](#level-1--2)
3. [Level 2 → 3](#level-2--3)
4. [Level 3 → 4](#level-3--4)
5. [Level 4 → 5](#level-4--5)
6. [Level 5 → 6](#level-5--6)
7. [Key Takeaways](#-key-takeaways)

---

## 🎯 Overview

The **Bandit** wargame is designed to teach the fundamentals of Linux command-line and security concepts. Each level teaches a new skill — from basic navigation to advanced file manipulation.

**Skills Learned:**
- SSH connections
- File permissions
- Command-line utilities (`ls`, `cat`, `find`, `strings`)
- Working with special filenames
- Hidden files
- File size filtering

---

## 🔓 Level 0 → 1

### 🎯 Objective
Connect to the Bandit server using SSH and retrieve the password for Level 1.

### 🛠️ Tools Used
- `ssh` — Secure Shell
- `cat` — Read file contents

### 📝 Solution

**Step 1:** Connect to the server
```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

**Step 2:** Enter the password
```
bandit0
```

**Step 3:** List files in the current directory
```bash
ls
```
Output:
```
readme
```

**Step 4:** Read the file
```bash
cat readme
```

**Step 5:** Capture the flag
```
6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR
```

### ✅ Level 1 Password
```
6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR
```

---

## 🔓 Level 1 → 2

### 🎯 Objective
Find the password in a file named `-` (dash) in the home directory.

### 🛠️ Tools Used
- `cat` — Read file contents
- `./` — Specify file path

### 💡 Key Concept
Files starting with `-` can't be read directly with `cat -` because it's interpreted as a command option. You need to specify the full path using `./-`.

### 📝 Solution

**Step 1:** Connect as bandit1
```bash
ssh bandit1@bandit.labs.overthewire.org -p 2220
```
Password: `6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR`

**Step 2:** Read the file
```bash
cat ./-
```

**Step 3:** Capture the flag
```
PK8fYLZg2hnHSz83plBL1iEPKdD3QToB
```

### ✅ Level 2 Password
```
PK8fYLZg2hnHSz83plBL1iEPKdD3QToB
```

---

## 🔓 Level 2 → 3

### 🎯 Objective
Find the password in a file with spaces in the filename.

### 🛠️ Tools Used
- `cat` — Read file contents
- Quotes for filenames with spaces

### 💡 Key Concept
Filenames with spaces need to be quoted or escaped with `\`.

### 📝 Solution

**Step 1:** Connect as bandit2
```bash
ssh bandit2@bandit.labs.overthewire.org -p 2220
```
Password: `PK8fYLZg2hnHSz83plBL1iEPKdD3QToB`

**Step 2:** List files
```bash
ls
```
Output:
```
spaces in this filename
```

**Step 3:** Read the file (use quotes)
```bash
cat "./spaces in this filename"
```

**Step 4:** Capture the flag
```
7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME
```

### ✅ Level 3 Password
```
7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME
```

---

## 🔓 Level 3 → 4

### 🎯 Objective
Find the password in a hidden file inside the `inhere` directory.

### 🛠️ Tools Used
- `cd` — Change directory
- `ls -la` — List all files (including hidden)

### 💡 Key Concept
Hidden files start with a dot `.` and require `-a` flag to be visible.

### 📝 Solution

**Step 1:** Connect as bandit3
```bash
ssh bandit3@bandit.labs.overthewire.org -p 2220
```
Password: `7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME`

**Step 2:** Go to the directory
```bash
cd inhere
```

**Step 3:** List all files (including hidden)
```bash
ls -la
```
Output:
```
total 12
drwxr-xr-x 2 root    root    4096 Apr 23 18:04 .
drwxr-xr-x 3 root    root    4096 Apr 23 18:04 ..
-rw-r----- 1 bandit4 bandit3   33 Apr 23 18:04 .hidden
```

**Step 4:** Read the hidden file
```bash
cat .hidden
```

**Step 5:** Capture the flag
```
xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq
```

### ✅ Level 4 Password
```
xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq
```

---

## 🔓 Level 4 → 5

### 🎯 Objective
Find the human-readable password among 10 files in the `inhere` directory.

### 🛠️ Tools Used
- `find` — Find files
- `cat` — Read file contents
- Wildcards (`./*`) — Match all files

### 💡 Key Concept
Not all files are text files. Use `file` command or read all files to find the human-readable one.

### 📝 Solution

**Step 1:** Connect as bandit4
```bash
ssh bandit4@bandit.labs.overthewire.org -p 2220
```
Password: `xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq`

**Step 2:** Go to the directory
```bash
cd inhere
```

**Step 3:** Find all files and read them
```bash
find ./* -type f -exec cat {} \;
```
OR
```bash
cat ./* 2>/dev/null
```

**Step 4:** Look for the human-readable text

**Step 5:** Capture the flag
```
6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG
```

### ✅ Level 5 Password
```
6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG
```

---

## 🔓 Level 5 → 6

### 🎯 Objective
Find the password in a file with specific properties (1033 bytes, non-executable, human-readable).

### 🛠️ Tools Used
- `find` — Search for files with specific properties
- `-size` — File size filter
- `-type f` — Regular file
- `xargs` — Execute commands on found files
- `strings` — Extract human-readable text

### 💡 Key Concept
The `find` command is powerful for searching files with specific attributes. Combine with `xargs` and `strings` to extract text.

### 📝 Solution

**Step 1:** Connect as bandit5
```bash
ssh bandit5@bandit.labs.overthewire.org -p 2220
```
Password: `6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG`

**Step 2:** Go to the directory
```bash
cd inhere
```

**Step 3:** Find the file and extract strings
```bash
find . -type f -size 1033c ! -executable | xargs strings
```

**Step 4:** Capture the flag
```
pXa26xhMWaC2SvDotA4r9EgZkulOeSBW
```

### ✅ Level 6 Password
```
pXa26xhMWaC2SvDotA4r9EgZkulOeSBW
```

---

## 🎯 Key Takeaways

### 🛠️ Essential Commands Learned

| Command | Purpose | Example |
|---------|---------|---------|
| `ssh` | Secure remote connection | `ssh user@host -p 2220` |
| `cat` | View file contents | `cat filename` |
| `ls` | List files | `ls -la` (show hidden) |
| `cd` | Change directory | `cd inhere` |
| `find` | Search for files | `find . -size 1033c` |
| `strings` | Extract text from binary | `strings file` |
| `xargs` | Execute commands | `find ... \| xargs strings` |

### 💡 Core Security Concepts

| Concept | Description |
|---------|-------------|
| **SSH Authentication** | Password-based login to remote servers |
| **Hidden Files** | `.` files require `-a` flag to view |
| **Special Filenames** | Files with `-` or spaces need special handling |
| **File Properties** | Size, type, executability matter |
| **Binary vs Text** | Use `strings` to extract readable text |

### 🔑 Password Progression

| Level | Password |
|-------|----------|
| 0→1 | `6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR` |
| 1→2 | `PK8fYLZg2hnHSz83plBL1iEPKdD3QToB` |
| 2→3 | `7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME` |
| 3→4 | `xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq` |
| 4→5 | `6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG` |
| 5→6 | `pXa26xhMWaC2SvDotA4r9EgZkulOeSBW` |

---

## 📊 Statistics

| Metric | Count |
|--------|-------|
| **Levels Completed** | 6 (0→6) |
| **Commands Mastered** | 10+ |
| **Flags Captured** | 6 |
| **Key Concepts Learned** | 8 |

---

## 🔗 Resources

- [OverTheWire Bandit](https://overthewire.org/wargames/bandit/)
- [Linux Command Cheat Sheet](https://www.geeksforgeeks.org/linux-commands-cheat-sheet/)
- [TryHackMe — Linux Fundamentals](https://tryhackme.com/room/linuxfundamentalspart1)
- [Explain Shell](https://explainshell.com/)

---

## 📝 Final Thoughts

The Bandit wargame is an excellent foundation for anyone starting in cybersecurity. These first 6 levels cover:

✅ Basic SSH connections  
✅ File navigation  
✅ Hidden files  
✅ Special filenames  
✅ File properties  
✅ Data extraction  

These skills are directly applicable to penetration testing, SOC analysis, and system administration.

**Next Steps:**
- Continue to Bandit Levels 7-14
- Start TryHackMe rooms
- Build a home lab
- Practice CTFs regularly

---

## 💬 Connect With Me

> 📧 **Email:** [muhammadsadiq.cyber@gmail.com](mailto:muhammadsadiq.cyber@gmail.com)  
> 🔗 **LinkedIn:** [linkedin.com/in/muhammadsadiqcyber](https://linkedin.com/in/muhammadsadiqcyber)  
> 🐙 **GitHub:** [github.com/muhammadsadiqX1](https://github.com/muhammadsadiqX1)  
> 🏴 **TryHackMe:** [tryhackme.com/p/muhammadsadiqX1](https://tryhackme.com/p/muhammadsadiqX1)

---

> *"Break things, learn faster, secure better."* 🔴



*Made with ❤️ by Muhammad Sadiq | Red Team Operator in Training*
